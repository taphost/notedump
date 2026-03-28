# SECURITY AUDIT PROMPT

Analizza questa codebase come un security auditor specializzato in codice AI-generato.

Il documento è diviso in tre blocchi: **Universal** (qualsiasi stack), **Backend**, **Frontend**. I pattern sono descritti in modo language-agnostic: dove utile, una tabella di riferimento elenca gli equivalenti per stack comune. All'interno di ogni blocco le sezioni sono ordinate per severità decrescente. Affronta prima i problemi Critical, indipendentemente dal blocco.

---

# ◆ UNIVERSAL
> Applicabile a qualsiasi progetto, indipendentemente dallo stack.

## U1. CREDENZIALI HARDCODED
`Critical`

- Valori sensibili (API key, secret, password, token) scritti direttamente nel codice sorgente
- Placeholder mai sostituiti con valori reali o riferimenti a env
- Variabili sensibili non caricate da un sistema di gestione delle variabili d'ambiente
- Credenziali committate in passato e poi rimosse, ma ancora presenti nella git history
- File di configurazione con segreti tracciati da git anche se ora in `.gitignore`

> **Riferimenti per stack**
> | Stack | Gestione env consigliata |
> |---|---|
> | Node.js / TS | `dotenv`, `process.env` |
> | Python | `os.environ`, `python-decouple` |
> | Ruby | `ENV[]`, `dotenv-rails` |
> | Go | `os.Getenv`, `godotenv` |
> | Java | `System.getenv()`, Spring `@Value` |
> | .NET | `IConfiguration`, `appsettings.json` + secrets manager |

## U2. SECURITY MISCONFIGURATION SU CLOUD
`High`

- Storage bucket (S3, GCS, Azure Blob) con accesso pubblico non intenzionale
- Policy IAM troppo permissive — principio del minimo privilegio non applicato
- Variabili d'ambiente con segreti esposte nei log del provider cloud o nelle variabili di build CI/CD
- Porte o servizi interni esposti pubblicamente senza necessità (database, cache, admin panel)
- Snapshot o backup di database accessibili pubblicamente

> **Riferimenti per provider**
> | Provider | Tool di verifica |
> |---|---|
> | AWS | `aws s3api get-bucket-acl`, AWS Trusted Advisor, `prowler` |
> | GCP | Security Command Center, `gcloud asset search-all-iam-policies` |
> | Azure | Microsoft Defender for Cloud, `az security assessment list` |
> | Tutti (config live) | `cloudsploit` |
> | Tutti (IaC / container) | `trivy` — per Terraform, Dockerfile, manifest Kubernetes |

## U3. DEPENDENCY VULNERABILITIES
`Medium → Critical` *(dipende dalla CVE trovata)*

- Dipendenze con vulnerabilità note (CVE) non aggiornate
- Versioni non pinnate o specificate con range troppo permissivi
- Assenza di tool automatici di audit nel workflow di sviluppo o CI

> **Riferimenti per stack**
> | Stack | Tool di audit |
> |---|---|
> | Node.js | `npm audit`, `yarn audit` |
> | Python | `pip-audit`, `safety` |
> | Ruby | `bundler-audit` |
> | Go | `govulncheck` |
> | Java | `OWASP Dependency-Check` |
> | .NET | `dotnet list package --vulnerable` |
> | Tutti | `dependabot`, `snyk` |

## U3. DEPENDENCY VULNERABILITIES
`Medium`

- Flag di debug attivi in ambienti non di sviluppo
- Variabili d'ambiente di sviluppo non separate da quelle di produzione
- Configurazione del compilatore o del type system che disabilita controlli di sicurezza

> **Riferimenti per stack**
> | Stack | Pattern da cercare |
> |---|---|
> | Node.js | `NODE_ENV=development` in produzione |
> | Python | `DEBUG=True` in settings di produzione |
> | PHP | `display_errors=On` |
> | Rails | `config.consider_all_requests_local = true` |
> | TypeScript | `"strict": false` o `"noImplicitAny": false` in `tsconfig.json` |

## U4. CONFIGURAZIONE NON SICURA PER PRODUZIONE
> Lato server, indipendentemente dal linguaggio o framework.

## B1. AUTH MANCANTE
`Critical`

- Endpoint che modificano, eliminano o leggono dati sensibili senza verifica dell'identità del chiamante
- Commenti `TODO: add authentication` o simili lasciati irrisolti
- Middleware di autenticazione assente su route che lo richiedono

## B2. INJECTION (SQL, COMMAND, TEMPLATE)
`Critical`

- Query al database costruite concatenando input utente invece di usare parametri
- Comandi di sistema costruiti con input utente senza escape
- Template engine usato con input utente non sanitizzato
- Cast o coercizioni di tipo su input esterno senza validazione runtime preventiva — i tipi statici non esistono a runtime

> **Riferimenti per stack**
> | Stack | Pattern sicuro |
> |---|---|
> | SQL (tutti) | Prepared statement / query parametrizzate |
> | Node.js / TS | `zod` o `yup` per validazione runtime prima di usare il valore |
> | Python | `cursor.execute(sql, params)` |
> | Rails | ActiveRecord con placeholder `?` o named params |
> | Java | `PreparedStatement`, `@Query` con parametri |
> | .NET | `SqlParameter`, Entity Framework parametrizzato |

## B3. PATH TRAVERSAL E FILE UPLOAD
`Critical`

- Input utente usato in operazioni su filesystem senza sanitizzazione
- Sequenze di navigazione relativa non bloccate nei path dinamici
- Operazioni di lettura/scrittura file con parametri non validati
- File upload senza verifica del tipo reale del contenuto (non solo l'estensione dichiarata)
- File upload senza limite sulla dimensione
- Directory di destinazione degli upload accessibile pubblicamente

## B4. JWT MAL CONFIGURATI
`High`

- Algoritmo di firma debole o non verificato (incluso `none`)
- Secret di firma debole o non caricato da env (vedi U1)
- Token senza scadenza
- Nessun meccanismo di invalidazione dei token al logout

## B5. CORS PERMISSIVO
`High`

- Configurazione CORS che accetta richieste da qualsiasi origine
- Header `Access-Control-Allow-Origin` impostato a wildcard
- Wildcard combinato con `Access-Control-Allow-Credentials: true` — particolarmente pericoloso perché i browser bloccano questa combinazione per spec, ma configurazioni errate possono aggirarla

## B6. RATE LIMITING ASSENTE
`High`

- Endpoint di autenticazione e recupero password senza throttling
- Nessun meccanismo di lockout dopo tentativi ripetuti falliti
- Assenza di protezione contro attacchi brute-force

> **Riferimenti per stack**
> | Stack | Libreria |
> |---|---|
> | Node.js | `express-rate-limit` |
> | Python | `slowapi`, `django-ratelimit` |
> | Ruby | `rack-attack` |
> | Go | `tollbooth`, `golang.org/x/time/rate` |
> | Java | `Bucket4j`, Spring `@RateLimiter` |
> | .NET | `AspNetCoreRateLimit` |

## B7. MASS ASSIGNMENT
`High`

- Corpo della richiesta mappato direttamente su modelli o oggetti DB senza filtraggio
- Assenza di whitelist dei campi accettati in input
- Campi sensibili modificabili dall'esterno perché non esclusi esplicitamente
- Validazione basata solo sui tipi statici senza schema parser a runtime

## B8. PROMPT INJECTION (AI-SPECIFIC)
`High`

- Input utente concatenato direttamente nel prompt LLM senza separazione
- Assenza di confine esplicito tra istruzioni di sistema e contenuto utente
- Output del modello usato senza validazione (es. eseguito come codice o renderizzato senza escape)

## B9. CSRF
`High`

- Endpoint mutanti (POST, PUT, DELETE, PATCH) accessibili via cookie-based auth senza token anti-forgery
- Assenza di verifica dell'header `Origin` o `Referer` sulle richieste sensibili
- Form che modificano stato senza protezione CSRF

> **Riferimenti per stack**
> | Stack | Libreria / meccanismo |
> |---|---|
> | Node.js/Express | `csrf-csrf`, `lusca` (`csurf` deprecato) |
> | Python/Django | `CsrfViewMiddleware` (attivo per default) |
> | Rails | `protect_from_forgery` (attivo per default) |
> | Java/Spring | `CsrfConfigurer` in `HttpSecurity` |
> | .NET | `ValidateAntiForgeryToken` |

## B10. INSECURE DESERIALIZATION
`High`

- Oggetti deserializzati da input non fidato senza validazione del tipo o del contenuto
- Formati di serializzazione nativi usati su dati provenienti dall'esterno
- Assenza di schema di validazione prima della deserializzazione

> **Riferimenti per stack**
> | Stack | Pattern da evitare |
> |---|---|
> | Python | `pickle.loads()` su input utente |
> | Ruby | `Marshal.load()` su input utente |
> | Java | `ObjectInputStream` su input utente |
> | Node.js | `serialize-javascript` eval, `node-serialize` |
> | Tutti | Preferire JSON con schema validation (`zod`, `jsonschema`, ecc.) |

## B11. CONFIGURAZIONE HTTP/TRANSPORT
`Medium`

- Assenza di redirect automatico da HTTP a HTTPS
- Cookie di sessione senza flag di sicurezza appropriati (`Secure`, `HttpOnly`, `SameSite`)
- Header di sicurezza HTTP assenti o mal configurati

> **Header da verificare**
> `Content-Security-Policy` · `X-Frame-Options` · `Strict-Transport-Security` · `X-Content-Type-Options: nosniff`
>
> **Riferimenti per stack**
> | Stack | Libreria |
> |---|---|
> | Node.js | `helmet` |
> | Python/Django | `django-csp`, `SECURE_*` settings |
> | Rails | `secure_headers` gem |
> | Java/Spring | `HttpSecurity` headers config |
> | .NET | `UseHsts()` |

## B12. ERROR HANDLING E LOGGING
`Medium`

- Eccezioni catturate e silenziate senza gestione
- Stack trace o dettagli interni esposti all'utente finale nei messaggi di errore
- Assenza di handler globale per eccezioni non catturate
- Dati sensibili (password, token) scritti nei log
- Assenza di audit trail su operazioni critiche (login, eliminazione, azioni admin)
- Tentativi di accesso falliti non loggati

## B13. CONFIGURAZIONE LLM (AI-SPECIFIC)
`Low`

- Nome del modello, endpoint o parametri di inferenza scritti nel codice invece che in env
- Assenza di gestione degli errori e fallback per chiamate LLM fallite o in timeout

---

# ◆ FRONTEND
> Lato client, indipendentemente dal framework.

## F1. XSS
`Critical`

- Contenuto dinamico inserito nel DOM senza sanitizzazione
- Codice eseguito dinamicamente con input utente non validato
- SSR che serializza stato applicativo nel DOM senza escape
- Direttive o API del framework che bypassano il sistema di sanitizzazione automatica
- Soppressione di errori del type checker su operazioni DOM con dati untrusted

> **Riferimenti per framework**
> | Framework | Pattern da cercare |
> |---|---|
> | Vanilla JS | `.innerHTML =` con dati dinamici |
> | React | `dangerouslySetInnerHTML` senza sanitizzazione |
> | Vue | `v-html` con input utente |
> | Svelte | `{@html ...}` con input utente |
> | Tutti | `eval()`, `new Function()` con dati dinamici |
> | Sanitizzazione | `DOMPurify` o equivalente |

## F2. ESPOSIZIONE DATI SENSIBILI NEL CLIENT
`High`

> Distinto da U1: qui il problema non è il codice sorgente ma ciò che viene incluso nel bundle compilato o esposto al browser a runtime.

- Credenziali o token inclusi nel bundle distribuito (visibili con DevTools)
- Variabili d'ambiente marcate come pubbliche che contengono segreti
- Token di autenticazione salvati in storage non protetto invece di cookie `HttpOnly`
- Dati sensibili persistiti in storage client-side senza cifratura

> **Riferimenti per framework**
> | Framework | Pattern da cercare |
> |---|---|
> | Vite | Prefisso `VITE_` su variabili segrete |
> | Next.js | Prefisso `NEXT_PUBLIC_` su variabili segrete |
> | React Native | `AsyncStorage` con dati sensibili non cifrati |
> | Next.js SSR | `getServerSideProps` che include dati sensibili nel payload di idratazione |

## F3. OPEN REDIRECT
`High`

- Navigazione o redirect costruiti con parametri non validati
- Destinazioni di redirect lette da query string senza whitelist degli URL ammessi

> **Riferimenti per framework**
> | Framework | Pattern da cercare |
> |---|---|
> | React / Next.js | `router.push(searchParams.get('redirect'))` senza validazione |
> | Vue / Nuxt | `navigateTo(route.query.next)` senza whitelist |
> | Vanilla JS | `window.location.href = urlParam` non validato |
> | Tutti | Query param `?next=`, `?redirect=`, `?url=` usati direttamente |

## F4. PRIVACY E DATA LEAK
`Medium`

- Statement di debug con dati utente lasciati attivi in produzione
- Dati sensibili trasmessi in query string (visibili nei log del server e nella history del browser)
- Campi password senza attributi di autocompletamento corretti per il browser

## F5. INTEGRITÀ DELLE DIPENDENZE
`Low`

- Risorse esterne caricate senza verifica di integrità (Subresource Integrity)
- Dipendenze da CDN non pinnate a una versione specifica

---

## OUTPUT ATTESO

Per ogni problema trovato, riporta:

- **File e riga**
- **Blocco** (Universal / Backend / Frontend) e **categoria** (es. B2, F1)
- **Snippet** del codice problematico
- **Perché è un rischio**
- **Fix consigliato** (codice corretto, non solo descrizione)

Alla fine, produci un riepilogo con:

- Totale vulnerabilità per categoria
- Severity complessiva (Critical / High / Medium / Low)
- I 3 fix più urgenti da affrontare subito
