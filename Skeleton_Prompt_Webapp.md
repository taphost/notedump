# Skeleton Prompt — Webapp Frontend



## Come usarlo

1. Leggi le sezioni di configurazione e **rimuovi le opzioni che non usi**
2. Compila i campi tra `[PARENTESI]`
3. Copia l'intero blocco PROMPT e incollalo in  nella LLM

---

### CONFIGURAZIONE — Scegli il tuo stack

Le sezioni seguenti contengono opzioni multiple. Tieni solo ciò che serve, elimina il resto.

---

### Guida alla scelta dello stack

**JavaScript**
Ideale per script semplici, pagine statiche, tool monofile o prototipi veloci. Nessun overhead di compilazione. Da preferire quando il progetto è piccolo e non è prevista crescita significativa.

**TypeScript**
Consigliato appena il progetto supera 3-4 moduli o è destinato a essere riusato altrove. Aggiunge tipizzazione statica che rende le interfacce tra moduli esplicite, riduce errori silenziosi e migliora il debugging. Compatibile con tutti i framework elencati.

**React**
Ottimo per SPA con stato complesso e molti componenti interattivi. Ecosistema vastissimo, facile trovare librerie e risorse. Curva di apprendimento media. Si scala bene da progetti piccoli a grandi.

**Vue**
Simile a React per casi d'uso, ma con una sintassi più vicina all'HTML tradizionale. Più accessibile per chi viene da un background HTML/CSS. Ottimo per team misti o progetti dove la semplicità è prioritaria.

**Svelte**
Compila il codice a JavaScript puro, nessun runtime da includere. Bundle molto leggero, ideale per widget embeddabili in pagine esistenti o progetti dove le performance di caricamento sono critiche. Ecosistema più piccolo rispetto a React e Vue.

**Angular**
Framework completo e opinionato: routing, state management, form, HTTP client sono tutti inclusi. Richiede TypeScript obbligatoriamente. Ideale per app enterprise con team strutturati dove la consistenza architetturale è prioritaria. Curva di apprendimento più ripida.

---

### Stack — scegli una combinazione, da inserire nel prompt.

- `JavaScript` — script semplici, pagine statiche, nessun framework
- `TypeScript` — 3+ moduli, destinato a crescere, nessun framework *(consigliato)*
- `TypeScript + React` — SPA con stato complesso, ecosistema ampio
- `TypeScript + Vue` — SPA, sintassi più vicina all'HTML, team misti
- `TypeScript + Svelte` — widget embeddabili, bundle minimo *(supporto TS con alcune limitazioni)*
- `TypeScript + Angular` — app enterprise, architettura consistente *(TypeScript obbligatorio)*
- `JavaScript + React` — SPA senza TypeScript
- `JavaScript + Vue` — SPA senza TypeScript, più semplice da adottare
- `JavaScript + Svelte` — widget embeddabili senza TypeScript

---

### Librerie aggiuntive

- Inserisci le librerie se presenti, oppure rimuovi la sezione

---

## PROMPT — Copia da qui

Scrivi un'app che fa `[SPECIFICHE]`.

**Stack:** HTML, CSS, `[COMBINAZIONE SCELTA]`, `[LIBRERIE]`.

---

### Struttura del progetto

Usa questa struttura base. Adatta le sottocartelle di `src/` al framework scelto.

```
project-root/
├── src/
│   ├── components/
│   ├── modules/
│   ├── utils/
│   ├── styles/
│   └── assets/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── docs/
├── .github/
│   └── workflows/
├── .env.example
├── .eslintrc
├── .prettierrc
├── package.json
├── CHANGELOG.md
├── LICENSE
├── CONTRIBUTING.md
└── README.md
```

---

### Versioning e changelog

- Segui **SemVer**: `MAJOR.MINOR.PATCH` — versione iniziale `0.1.0`
- Mantieni un `CHANGELOG.md` seguendo lo standard **Keep a Changelog**
- Sezioni del changelog: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`

---

### Variabili d'ambiente

- Nessuna credenziale o configurazione hardcodata nel codice
- Usa `.env` per le variabili d'ambiente
- Versiona `.env.example` con i nomi delle variabili ma senza valori reali
- Aggiungi `.env` al `.gitignore`

---

### Git conventions

- Includi un `.gitignore` adatto allo stack scelto (usa gitignore.io come riferimento)
- Messaggi di commit in inglese, al presente, descrittivi: `Add user auth module` non `fix stuff`
- Un commit per cambiamento logico, non accumulare modifiche non correlate

---

### Qualità del codice

- Clean Code: variabili e funzioni con nomi autoesplicativi
- Commenti minimi ed essenziali in inglese, solo dove il *perché* non è ovvio
- Nessun magic number: usa costanti con nome
- KISS e YAGNI: nessuna astrazione prematura, aggiungi complessità solo quando serve davvero

---

### Modularità

- Codice modulare, espandibile e riutilizzabile
- Ogni modulo espone solo l'interfaccia minima necessaria
- Nessuna dipendenza implicita, nessuno stato globale nascosto
- Separazione netta: UI / logica / dati

---

### Internazionalizzazione (i18n) — predisposizione

- Nessuna stringa UI hardcodata nel codice: tutte in file di testo separati
- Struttura predisposta per supportare più lingue anche se non richiesto ora
- Date, numeri e valute formattati tramite le API standard (`Intl`)

---

### Sicurezza

- Sanitizza sempre gli input utente, nessun dato esterno usato direttamente
- Nessun `innerHTML` diretto: usa `textContent` o metodi sicuri equivalenti
- Nessuna dipendenza con vulnerabilità note: verifica prima di aggiungerla al progetto

---

### Accessibilità

- HTML semantico: usa gli elementi corretti per il loro scopo (`button`, `nav`, `main`, ecc.)
- Attributi ARIA solo dove l'HTML semantico non è sufficiente
- Ogni elemento interattivo deve essere raggiungibile da tastiera

---

### Compatibilità browser

- Target: ultimi 2 major release di Chrome, Firefox, Safari, Edge
- Nessuna API senza verificarne il supporto su MDN
- Nessun polyfill aggiunto senza che sia strettamente necessario

---

### Performance

- Nessun blocco del thread principale: operazioni pesanti in async o Web Worker
- Lazy loading per risorse non critiche al primo render
- Valuta il peso sul bundle prima di aggiungere qualsiasi libreria

---

### Errori e robustezza

- Gestisci sempre gli errori esplicitamente, zero fallback silenziosi
- Ogni side effect è dichiarato esplicitamente al confine del modulo che lo produce
- Nessuna operazione async senza gestione dell'errore e cancellazione esplicita

---

### Concorrenza e async

- Progetta fin dall'inizio per evitare race condition
- Usa `AbortController` per fetch cancellabili
- Nessuno shared mutable state tra operazioni concorrenti

---

### Logging

- Distingui i livelli: `debug` / `info` / `warn` / `error`
- I log devono indicare cosa è successo e dove, non solo "errore"
- Mai loggare dati sensibili

---

### Testabilità e debugging

- Funzioni pure dove possibile, side effects isolati e tracciabili
- Stack trace leggibile dai soli nomi di funzioni e moduli
- Struttura del codice predisposta per il testing, anche senza test scritti ora

---

### Tooling scaffold

- Node.js è richiesto come ambiente di sviluppo per eseguire npm, ESLint e Prettier — non fa parte dello stack frontend
- `package.json` con script per: `lint`, `format:check`, `check:syntax` (`node --check`)
- Configurazione ESLint *(standard recommended)* e Prettier inclusa
- Struttura predisposta per CI (es. GitHub Actions workflow)

---

### Gestione delle dipendenze

- Versioni pinned nel `package.json`: nessun range aperto (`^`, `~`) in produzione
- Distinzione netta tra `dependencies` e `devDependencies`
- Nessuna dipendenza aggiunta senza una ragione esplicita
- Controlla regolarmente con `npm audit`

---

### Testing — struttura e predisposizione

- Ogni layer è testabile indipendentemente
- **Unit:** funzioni pure isolate dal DOM e da I/O
- **Integration:** moduli che interagiscono espongono interfacce stabili e mockabili
- **E2E:** flussi utente principali identificati e documentati, pronti per essere coperti
- Struttura cartelle: `tests/unit/`, `tests/integration/`, `tests/e2e/` — speculare a `src/`
- Tool-agnostic: la scelta del test runner è rimandata allo stack finale

---

### Documentazione

- `README.md` minimo con: descrizione del progetto, istruzioni di installazione, istruzioni di esecuzione, script disponibili (`lint`, `test`, ecc.)
- Ogni modulo pubblico ha una breve descrizione del suo scopo in testa al file
- `LICENSE` presente nel repo: scegli una licenza esplicita (es. MIT per progetti open source)
- `CONTRIBUTING.md` con: come installare l'ambiente di sviluppo, convenzioni di codice e commit, come aprire una PR
