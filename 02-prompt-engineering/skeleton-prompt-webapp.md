# Skeleton Prompt — Webapp

## Come usarlo

1. Leggi la sezione CONFIGURAZIONE per i requisiti iniziali e lo stack da scegliere
2. Compila i campi marcati con `[DA COMPILARE: ...]`
3. Una volta compilato, **elimina tutto ciò che precede il blocco PROMPT** — guide, note, configurazione
4. Salva il file come `PROMPT.md` e forniscilo all'agente

---

## CONFIGURAZIONE

- ATTENZIONE: le sezioni seguenti contengono opzioni multiple. Tieni solo ciò che serve, elimina il resto.

- NOTA: questo prompt non usa tool di scaffolding automatico (Vite, create-vue, Angular CLI, ecc.). La struttura del progetto è quella definita nel PROMPT e va creata dalla LLM.

- REQUISITO: Node.js deve essere installato prima di usare il progetto — scaricalo da nodejs.org. npm è incluso nell'installazione.

---

### Stack — scegli la combinazione da usare

- JavaScript

  **Quando usarlo:** Progetti semplici, pagine statiche, nessun framework. Nessun overhead di compilazione.

- TypeScript *(consigliato)*

  **Quando usarlo:** Appena il progetto supera 3-4 moduli o è destinato a crescere. Riduce errori silenziosi, rende le interfacce tra moduli esplicite.

- TypeScript + React

  **Quando usarlo:** SPA con stato complesso e molti componenti interattivi. Ecosistema ampio, si scala bene.

- TypeScript + Vue

  **Quando usarlo:** SPA con sintassi più vicina all'HTML tradizionale. Più accessibile per chi viene da HTML/CSS, ottimo per team misti.

- TypeScript + Svelte

  **Quando usarlo:** Widget embeddabili o progetti dove il bundle minimo è prioritario. Nessun runtime incluso. *(Supporto TS con alcune limitazioni)*

- TypeScript + Angular

  **Quando usarlo:** App enterprise con team strutturati. Framework completo e opinionato: routing, state, form e HTTP client inclusi. Curva di apprendimento ripida.

- JavaScript + React

  **Quando usarlo:** Come TypeScript + React, senza tipizzazione statica.

- JavaScript + Vue

  **Quando usarlo:** Come TypeScript + Vue, senza tipizzazione statica. Più semplice da adottare per i principianti.

- JavaScript + Svelte

  **Quando usarlo:** Come TypeScript + Svelte, senza tipizzazione statica.

---

### Librerie aggiuntive

- [DA COMPILARE: elenca le librerie aggiuntive, oppure rimuovi questa sezione]

---

## INIZIO PROMPT

Costruisci un'app che fa `[DA COMPILARE: descrizione di cosa fa l'app]`.

**Stack:** HTML, CSS, `[DA COMPILARE: combinazione scelta dalla sezione sopra]`, `[DA COMPILARE: librerie aggiuntive, oppure rimuovi]`.

---

### Struttura del progetto

Crea questa struttura di cartelle e file. Adatta le sottocartelle di `src/` al framework scelto.

```
project-root/
├── src/                        # codice sorgente dell'applicazione
│   ├── components/             # elementi UI riutilizzabili
│   ├── modules/                # logica di business indipendente dalla UI
│   ├── utils/                  # funzioni pure di supporto, nessuna dipendenza da dominio
│   ├── styles/                 # CSS globali, variabili, reset
│   └── assets/                 # file statici: immagini, font, icone
├── tests/                      # tutti i test, speculare a src/
│   ├── smoke/                  # verifica rapida avvio e funzioni critiche
│   ├── unit/                   # funzioni isolate, nessun I/O
│   ├── integration/            # moduli che interagiscono tra loro
│   ├── e2e/                    # flussi utente completi dal browser
│   └── regression/             # test per bug già corretti, evitano regressioni
├── docs/                       # documentazione del progetto
│   └── api/                    # documentazione delle interfacce pubbliche dei moduli
├── dist/                       # output di build ottimizzato — non versionare
├── locales/                    # file di traduzione JSON flat (es. en.json, it.json)
├── .github/                    # configurazione specifica GitHub
│   └── workflows/              # CI/CD: lint, format check, syntax check, npm audit, deploy
├── .env                        # variabili d'ambiente locali — non versionare
├── .env.example                # template .env con nomi variabili senza valori reali — versionare
├── .gitignore                  # elenco file e cartelle esclusi dal version control
├── package-lock.json           # lockfile generato da npm — versionare sempre
├── .eslintrc                   # regole ESLint per la qualità e consistenza del codice
├── .prettierrc                 # regole Prettier per la formattazione automatica del codice
├── package.json                # dipendenze, script npm e metadati del progetto
├── CHANGELOG.md                # storico delle modifiche per versione, formato Keep a Changelog
├── LICENSE                     # licenza del progetto (es. MIT, Apache 2.0)
├── CONTRIBUTING.md             # istruzioni per contribuire: setup, convenzioni, PR
└── README.md                   # descrizione progetto, installazione, esecuzione, script
```

---

### Versioning e changelog

- Inizializza `CHANGELOG.md` con versione `0.1.0` seguendo lo standard **Keep a Changelog**
- Usa sezioni: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`
- Aggiorna `CHANGELOG.md` ad ogni modifica significativa

---

### Variabili d'ambiente

- Nessuna credenziale o configurazione hardcodata nel codice
- Crea `.env.example` con i nomi delle variabili ma senza valori reali
- Assicurati che `.env` sia presente nel `.gitignore`
- In CI/CD usa GitHub Secrets per le variabili d'ambiente — mai committare valori reali

---

### Git conventions

- Genera un `.gitignore` adatto allo stack scelto (usa gitignore.io come riferimento) e verificane il contenuto
- Esegui un commit per ogni cambiamento logico completato e verificato
- Messaggi di commit in inglese, al presente, descrittivi: `Add user auth module` non `fix stuff`

---

### Qualità del codice

- Usa nomi autoesplicativi per variabili e funzioni
- Scrivi commenti minimi ed essenziali in inglese, solo dove il *perché* non è ovvio
- Sostituisci i magic number con costanti con nome
- KISS e YAGNI: non aggiungere astrazioni finché non servono davvero

---

### Modularità

- Struttura il codice in moduli indipendenti, espandibili e riutilizzabili
- Ogni modulo espone solo l'interfaccia minima necessaria
- Elimina dipendenze implicite e stato globale nascosto
- Mantieni separazione netta tra UI, logica e dati

---

### Internazionalizzazione (i18n) — predisposizione

- Sposta tutte le stringhe UI in file di testo separati — nessuna stringa hardcodata nel codice
- Usa JSON flat come formato per i file di traduzione (es. `locales/en.json`)
- Crea la struttura per supportare più lingue anche se non richiesto ora
- Usa le API standard `Intl` per formattare date, numeri e valute

---

### Sicurezza

- Sanitizza sempre gli input utente prima di usarli
- Valida esplicitamente tipo, formato e range di ogni dato in entrata — la sanitizzazione da sola non è sufficiente
- Non usare `innerHTML` diretto: usa `textContent` o metodi sicuri equivalenti
- Configura una Content Security Policy (CSP) per limitare cosa il browser può eseguire e prevenire XSS
- Prima di installare una dipendenza verifica che non abbia vulnerabilità note

---

### Accessibilità

- Usa elementi HTML semantici corretti per il loro scopo (`button`, `nav`, `main`, ecc.)
- Aggiungi attributi ARIA solo dove l'HTML semantico non è sufficiente
- Verifica che ogni elemento interattivo sia raggiungibile da tastiera

---

### Compatibilità browser

- Sviluppa per gli ultimi 2 major release di Chrome, Firefox, Safari, Edge
- Prima di usare una API verifica il supporto su MDN
- Non aggiungere polyfill senza che siano strettamente necessari

---

### Performance

- Non bloccare il thread principale: sposta le operazioni pesanti in async o Web Worker
- Implementa lazy loading per risorse non critiche al primo render
- Valuta il peso sul bundle prima di installare qualsiasi libreria

---

### Errori e robustezza

- Gestisci sempre gli errori esplicitamente, zero fallback silenziosi
- Applica il principio fail fast: il sistema deve fallire in modo rumoroso e prevedibile, non degradare silenziosamente
- Dichiara ogni side effect esplicitamente al confine del modulo che lo produce
- Non lasciare operazioni async senza gestione esplicita dell'errore
- Applica throttling o debounce su input utente e chiamate API ripetute

---

### Concorrenza e async

- Progetta fin dall'inizio per evitare race condition
- Usa `AbortController` per rendere le fetch cancellabili
- Imposta un timeout esplicito per ogni operazione async — non affidarti solo alla cancellazione
- Elimina lo shared mutable state tra operazioni concorrenti

---

### Logging

- Usa livelli di log distinti: `debug` / `info` / `warn` / `error`
- Ogni log deve indicare cosa è successo e dove, non solo "errore"
- Non loggare mai dati sensibili

---

### Code Quality & Automation

- Crea `package.json` con script per: `lint`, `format:check`, `check:syntax` (`node --check`)
- Installa ESLint e Prettier come `devDependencies` e genera le loro configurazioni
- Esegui `npm run lint` e `npm run format:check` dopo ogni modifica e correggi eventuali errori
- Crea il workflow CI in `.github/workflows/` che esegue lint, format check, syntax check e `npm audit` ad ogni push

---

### Gestione delle dipendenze

- Committa sempre `package-lock.json` nel version control
- Usa `npm ci` in CI/CD invece di `npm install`
- Distinzione netta tra `dependencies` e `devDependencies`
- Nessuna dipendenza aggiunta senza una ragione esplicita
- Esegui `npm audit` dopo ogni aggiunta di dipendenza e correggi le vulnerabilità prima di procedere

---

### Testabilità e debugging

- Scrivi funzioni pure dove possibile, side effects isolati e tracciabili
- Verifica che lo stack trace sia leggibile dai soli nomi di funzioni e moduli

---

### Testing — struttura e predisposizione

- Ogni layer è testabile indipendentemente
- **Smoke:** verifica rapida che il sistema si avvii e le funzioni critiche rispondano — da eseguire ad ogni deploy
- **Unit:** funzioni pure isolate dal DOM e da I/O
- **Integration:** moduli che interagiscono espongono interfacce stabili e mockabili
- **E2E / Acceptance:** flussi utente principali identificati e documentati — verifica che il sistema soddisfi i requisiti dal punto di vista dell’utente finale
- **Regression:** ogni bug corretto diventa un test — nessuna regressione deve passare inosservata
- Organizza i file dentro ogni cartella di `tests/` specchiando la struttura di `src/` — es. `src/modules/auth.js` → `tests/unit/modules/auth.test.js`
- Tool-agnostic: la scelta del test runner è rimandata allo stack finale

---

### Documentazione

- Crea `README.md` con: descrizione del progetto, istruzioni di installazione, istruzioni di esecuzione, script disponibili (`lint`, `test`, ecc.)
- Aggiungi una breve descrizione dello scopo in testa ad ogni modulo pubblico
- Crea `LICENSE` con la licenza scelta (es. MIT per progetti open source)
- Crea `CONTRIBUTING.md` con: come installare l'ambiente di sviluppo, convenzioni di codice e commit, come aprire una PR

---

### Build e distribuzione — opzionale

Non eseguire questa sezione automaticamente. Quando ritieni il progetto in uno stato stabile e potenzialmente pronto per una release (test che passano, nessun errore di lint, funzionalità principali complete), chiedi esplicitamente all'utente se vuole generare la build di distribuzione.

Se l'utente conferma:

- Copia in `dist/` solo i file necessari all'esecuzione — sorgenti compilati, assets, locales
- `dist/` non contiene config, test, docs o file di sviluppo
- Assicurati che `dist/` sia presente nel `.gitignore`
- Il contenuto di `dist/` è l'unico da caricare sull'hosting
