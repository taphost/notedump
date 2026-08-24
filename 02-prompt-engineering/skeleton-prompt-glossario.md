# Skeleton Prompt — Glossario

Questa guida spiega gli strumenti e i concetti usati nel prompt, senza presupporre conoscenze pregresse.

---

## 1. Fondamentali

### Git

Git è un sistema che tiene traccia di tutte le modifiche che fai al codice nel tempo. Ogni volta che salvi uno stato del progetto (si chiama *commit*), Git lo registra. Se rompi qualcosa puoi tornare a un punto precedente, come un *undo* illimitato e permanente.

Non è un programma con interfaccia grafica — si usa da terminale, oppure tramite strumenti come GitHub Desktop.

### Commit

Un salvataggio permanente dello stato del progetto in Git. Ogni commit ha un messaggio descrittivo e un identificatore univoco. Puoi tornare a qualsiasi commit precedente in qualsiasi momento. Il prompt chiede di fare un commit per ogni cambiamento logico completato e verificato, con messaggi in inglese al presente: `Add user auth module`, non `fix stuff`.

### Push

L'operazione che carica i commit dal tuo computer su GitHub. Fino a quando non fai push, le modifiche esistono solo in locale. Ogni push può far partire automaticamente il workflow CI configurato nel progetto.

### GitHub

GitHub è un sito dove carichi il tuo progetto Git. Serve come backup online del codice e come punto centrale da cui partono tutte le automazioni (CI, deploy, ecc.).

Non è obbligatorio usarlo, ma il prompt è costruito attorno ad esso.

### Pull Request

Una proposta di modifica al codice su GitHub. Invece di modificare direttamente il progetto, crei una copia, fai le modifiche lì, e poi apri una *pull request* per chiedere che vengano integrate. Usata principalmente in team o in progetti open source. Il `CONTRIBUTING.md` spiega come aprirne una.

### Deploy

Il processo di pubblicare l'app su un server o hosting per renderla accessibile agli utenti finali. Può essere manuale (carichi i file a mano) o automatico tramite CI — ogni push su GitHub fa partire il workflow che costruisce e pubblica l'app.

### Hosting

Un servizio che mette a disposizione uno spazio su un server dove caricare i file dell'app per renderla accessibile via browser. Esempi comuni: Netlify, Vercel, GitHub Pages per app frontend; Railway, Render, Fly.io per app con backend. Il contenuto della cartella `dist/` è quello che viene caricato sull'hosting.

### DOM — Document Object Model

La rappresentazione interna che il browser costruisce di una pagina HTML: un albero di elementi (nodi) che JavaScript può leggere e modificare. Quando aggiorni il testo di un elemento, aggiungi un bottone o cambi uno stile via JS, stai manipolando il DOM. È il ponte tra il codice e quello che l'utente vede sullo schermo.

### Async — Asincrono

Un'operazione asincrona è un'operazione che non blocca l'esecuzione del codice mentre aspetta una risposta — tipicamente una chiamata API, la lettura di un file, o qualsiasi cosa che richieda tempo. Il codice continua a girare e gestisce il risultato quando arriva. In JavaScript si gestisce con `async/await` o con le Promise. Il prompt dedica un'intera sezione alla gestione corretta delle operazioni async.

### Promise

Un oggetto JavaScript che rappresenta il risultato futuro di un'operazione asincrona. Può essere in tre stati: *pending* (in attesa), *fulfilled* (completata con successo) o *rejected* (fallita). La sintassi `async/await` è un modo più leggibile per lavorare con le Promise senza dover concatenare callback.

### Thread

Un filo di esecuzione del codice. Il browser ha un thread principale che gestisce l'interfaccia utente: rendering, eventi, JavaScript. Se lo blocchi con operazioni pesanti, la pagina si congela e smette di rispondere. I Web Worker permettono di spostare operazioni costose in thread separati, lasciando libero il thread principale.

### Node.js

Un ambiente che permette di eseguire JavaScript fuori dal browser — sul tuo computer o su un server. È il motore su cui girano npm e tutti gli strumenti di sviluppo usati nel prompt. Va installato prima di tutto il resto, scaricabile da nodejs.org. npm è incluso nell'installazione.

### TypeScript

Un'estensione di JavaScript che aggiunge la tipizzazione statica: ogni variabile e funzione dichiara esplicitamente che tipo di dato gestisce. Questo permette di trovare molti errori prima ancora di eseguire il codice. I file TypeScript hanno estensione `.ts` o `.tsx` e vengono compilati in JavaScript prima di essere eseguiti dal browser.

### Framework (React, Vue, Svelte, Angular)

Un framework è un insieme di strumenti e convenzioni che strutturano il modo in cui scrivi un'applicazione. Invece di gestire manualmente ogni interazione con il DOM, un framework si occupa di aggiornare l'interfaccia automaticamente quando i dati cambiano. React, Vue, Svelte e Angular sono quattro framework diversi per costruire interfacce web — ognuno con la propria filosofia, ma con lo stesso obiettivo.

### SPA — Single Page Application

Un'applicazione web che carica una sola pagina HTML e aggiorna il contenuto dinamicamente senza ricaricare il browser. Tutta la navigazione avviene via JavaScript. React e Vue sono i framework più usati per costruire SPA. Il vantaggio è un'esperienza utente più fluida; lo svantaggio è maggiore complessità nella gestione dello stato e nel SEO.

### SEO — Search Engine Optimization

L'insieme di tecniche per rendere un sito web visibile e ben posizionato nei motori di ricerca. Le SPA hanno storicamente avuto problemi di SEO perché il contenuto viene generato via JavaScript — i motori di ricerca fanno fatica a indicizzare pagine che non hanno HTML statico al caricamento.

### Versioning — `0.1.0`, `1.0.0`

Un sistema per numerare le versioni del progetto. Segue il formato **major.minor.patch**:

- **patch** (`0.1.0` → `0.1.1`): piccola correzione di bug
- **minor** (`0.1.0` → `0.2.0`): nuova funzionalità, compatibile con le precedenti
- **major** (`0.1.0` → `1.0.0`): cambiamento importante, potenzialmente incompatibile

Il progetto parte da `0.1.0` per indicare che è ancora in sviluppo.

### API key

Una stringa di testo che funziona come password per accedere a un servizio esterno (es. OpenAI, Google Maps, Stripe). Va tenuta segreta: chiunque la possieda può usare il servizio al posto tuo, spesso a tue spese. Per questo va nel `.env` e mai su GitHub.

---

## 2. File e cartelle del progetto

### `.gitignore`

Un file di testo che dice a Git quali file **non** deve tracciare né caricare su GitHub. Tipicamente contiene: credenziali, chiavi API, file generati automaticamente, dipendenze.

Esempio: se scrivi `.env` nel `.gitignore`, quel file resterà solo sul tuo computer e non finirà mai online.

### `.env`

Un file dove tieni tutte le configurazioni sensibili del progetto: chiavi API, password, URL di database, ecc. Non va mai caricato su GitHub. Il prompt garantisce che sia sempre nel `.gitignore`.

### `.env.example`

Una copia del `.env` ma senza i valori reali — solo i nomi delle variabili. Serve a chi clona il progetto per sapere quali variabili configurare, senza esporre dati sensibili.

Esempio:
```
API_KEY=
DATABASE_URL=
```

### `package.json`

Il file centrale del progetto npm. Contiene: il nome del progetto, la versione, la lista delle librerie installate e gli script che puoi eseguire (es. `npm run lint`). Viene generato automaticamente da npm.

### `package-lock.json`

Un file generato automaticamente da npm che registra la versione esatta di ogni libreria installata. Garantisce che il progetto funzioni in modo identico su qualsiasi computer. Va sempre caricato su GitHub.

Non va mai modificato a mano.

### `CHANGELOG.md`

Un file che tiene traccia di cosa è cambiato in ogni versione del progetto. Segue lo standard *Keep a Changelog*, con sezioni fisse: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`.

Serve a te e a chiunque usi il progetto per capire cosa è cambiato e quando.

### `dist/`

La cartella che contiene i file pronti per la distribuzione — quello che carichi sull'hosting. Contiene solo ciò che serve all'esecuzione: sorgenti, assets, locales. Niente configurazioni, test o documentazione.

Viene popolata dall'agente solo quando il progetto è pronto per una release, su tua conferma. Non va caricata su GitHub — va aggiunta al `.gitignore`.

### `locales/`

La cartella che contiene i file di traduzione dell'interfaccia. Ogni file è un JSON con le stringhe nella lingua corrispondente, ad esempio `en.json` per l'inglese e `it.json` per l'italiano.

Anche se non hai intenzione di tradurre l'app, il prompt prepara questa struttura fin dall'inizio per non doverla aggiungere in seguito.

### `docs/`

Cartella per la documentazione del progetto: descrizione dei moduli pubblici, interfacce, note tecniche. Non è documentazione per l'utente finale ma per chi sviluppa il progetto.

### `CONTRIBUTING.md`

Un file che spiega come contribuire al progetto: come installare l'ambiente di sviluppo, le convenzioni da seguire, come aprire una pull request. Utile se il progetto è pubblico o condiviso con altri.

### `LICENSE`

Il file che dichiara sotto quale licenza è rilasciato il progetto. La più comune per progetti open source è la licenza MIT, che permette a chiunque di usare, modificare e distribuire il codice.

Se il progetto è privato, questo file è meno rilevante.

### `README.md`

Il file di presentazione del progetto, solitamente la prima cosa che si legge. Contiene: descrizione di cosa fa l'app, istruzioni di installazione, istruzioni per avviarlo in locale, e la lista degli script disponibili (`npm run lint`, `npm run test`, ecc.).

---

## 3. Strumenti

### npm

npm è il gestore di pacchetti di Node.js. Serve a installare librerie scritte da altri che puoi usare nel tuo progetto. Funziona da terminale con comandi tipo `npm install nome-libreria`.

Richiede che Node.js sia installato sul tuo computer — scaricabile da nodejs.org.

### `npm ci`

Un comando alternativo a `npm install` da usare in ambienti automatizzati (CI). Installa le dipendenze esattamente come descritte nel `package-lock.json`, senza margini di variazione.

### `npm audit`

Un comando che controlla se le librerie installate nel progetto hanno vulnerabilità di sicurezza note. Va eseguito ogni volta che installi una nuova libreria.

### ESLint

*Lint* è il processo di analisi statica del codice: il codice viene letto e controllato senza essere eseguito, cercando errori, cattive pratiche o stili incoerenti. Il termine viene da un vecchio strumento Unix degli anni '70 che cercava pelucchi (*lint*) nel codice.

ESLint è lo strumento che esegue questo processo per JavaScript e TypeScript. È come un correttore ortografico per il codice.

La sua configurazione si trova nel file `.eslintrc`.

### Prettier

Uno strumento che formatta automaticamente il codice in modo uniforme: indentazione, virgolette, punto e virgola, ecc. Non trova errori — si occupa solo dell'aspetto visivo del codice.

La sua configurazione si trova nel file `.prettierrc`.

### CI/CD — Continuous Integration / Continuous Delivery / Continuous Deployment

Un sistema che esegue automaticamente una serie di controlli (lint, audit, test) ogni volta che carichi del codice su GitHub. Se qualcosa va storto, ti avvisa prima che il problema si propaghi.

**CI (Continuous Integration)** — integra e verifica le modifiche automaticamente ad ogni push.

**CD (Continuous Delivery)** — ogni modifica che passa i test è automaticamente pronta per il deploy, ma richiede ancora una conferma manuale prima di andare in produzione.

**CD (Continuous Deployment)** — ogni modifica che passa i test viene deployata automaticamente, senza intervento umano.

Nel prompt, CI/CD è configurato tramite GitHub Actions.

### GitHub Actions / Workflows

Il sistema di automazione integrato in GitHub. I *workflow* sono file di configurazione che definiscono cosa fare automaticamente ad ogni push: eseguire ESLint, controllare la formattazione, fare `npm audit`, ecc.

I file si trovano nella cartella `.github/workflows/`.

### GitHub Secrets

Un sistema di GitHub per archiviare variabili sensibili (API key, password, token) in modo sicuro, accessibili dai workflow CI senza mai esporle nel codice o nei file di configurazione. Sono cifrate e visibili solo all'interno dei workflow autorizzati. Il prompt li cita come il modo corretto per gestire le variabili d'ambiente in CI/CD.

### MDN — Mozilla Developer Network

La documentazione di riferimento ufficiale per le tecnologie web: HTML, CSS, JavaScript e le API del browser. Prima di usare una funzionalità nuova o poco conosciuta, MDN è il posto dove verificare cosa fa esattamente e quali browser la supportano. Accessibile su developer.mozilla.org.

### dependencies vs devDependencies

Due categorie distinte nel `package.json`.

**dependencies** — librerie necessarie all'esecuzione dell'app in produzione. Vengono incluse nel bundle finale. Esempio: React, Vue, una libreria per le date.

**devDependencies** — librerie necessarie solo durante lo sviluppo: ESLint, Prettier, test runner, ecc. Non finiscono nel bundle finale. Il prompt chiede di mantenere questa distinzione netta per non gonfiare inutilmente il codice distribuito.

---

## 4. Concetti di sviluppo

### i18n — Internazionalizzazione

*i18n* è un'abbreviazione di "internationalization": la i, poi 18 lettere, poi la n. È il processo di preparare un'app a supportare più lingue e formati locali (date, numeri, valute) senza dover riscrivere il codice. Il prompt predispone questa struttura fin dall'inizio anche se non hai intenzione di tradurre l'app subito.

### KISS e YAGNI

Due principi di progettazione del codice citati nella sezione Qualità del codice.

**KISS** (*Keep It Simple, Stupid*) — preferisci sempre la soluzione più semplice che funziona. La complessità ha un costo: più il codice è complesso, più è difficile da leggere, modificare e debuggare.

**YAGNI** (*You Aren't Gonna Need It*) — non aggiungere funzionalità o astrazioni finché non servono davvero. Scrivere codice "per il futuro" spesso produce overhead inutile che non verrà mai usato.

### Fail Fast

Un principio di progettazione: quando qualcosa va storto, il sistema deve fallire immediatamente e in modo rumoroso, non degradare silenziosamente. Un errore silenzioso è molto più pericoloso di uno esplicito perché può propagarsi a lungo prima di essere notato. Il prompt lo applica alla gestione degli errori: zero fallback silenziosi, ogni errore va gestito esplicitamente.

### Magic Number

Un valore numerico scritto direttamente nel codice senza spiegazione. Esempio: `if (status === 3)` — cosa significa 3? Nessuno lo sa senza leggere la documentazione. Il prompt chiede di sostituire i magic number con costanti con nome: `const STATUS_ACTIVE = 3` rende il codice autoesplicativo.

### Funzione Pura

Una funzione che, dati gli stessi input, restituisce sempre lo stesso output e non produce side effect. Non modifica variabili esterne, non fa chiamate API, non tocca il DOM. Sono le funzioni più facili da testare e da ragionare, perché il loro comportamento è completamente prevedibile.

### Side Effect

Qualsiasi operazione che interagisce con qualcosa al di fuori della funzione stessa: scrivere su un file, fare una chiamata API, modificare una variabile globale, aggiornare il DOM. Il prompt chiede di dichiarare i side effect esplicitamente al confine del modulo che li produce, così chi legge il codice sa esattamente dove avvengono le interazioni con l'esterno.

### Stack Trace

La lista delle funzioni che erano in esecuzione nel momento in cui si è verificato un errore, in ordine inverso di chiamata. Leggere uno stack trace ti dice esattamente dove nel codice si è rotto qualcosa e come ci sei arrivato. Il prompt chiede che i nomi di funzioni e moduli siano sufficientemente descrittivi da rendere lo stack trace leggibile senza dover aprire il codice.

---

## 5. Sicurezza

### XSS — Cross-Site Scripting

Un tipo di attacco in cui codice JavaScript malevolo viene iniettato in una pagina web e eseguito nel browser di un altro utente. Tipicamente avviene quando un'app inserisce nel DOM input utente non validato. La CSP e l'uso di `textContent` al posto di `innerHTML` sono le principali difese.

### CSP — Content Security Policy

Una direttiva di sicurezza che dici al browser tramite un header HTTP o un tag HTML. Specifica da quali fonti il browser può caricare script, stili e risorse. Serve a prevenire attacchi XSS, dove codice malevolo viene iniettato nella pagina.

### Sanitizzazione vs Validazione

Due operazioni distinte che il prompt cita entrambe nella sezione Sicurezza.

**Sanitizzazione** — pulisce l'input rimuovendo o neutralizzando le parti potenzialmente pericolose (es. tag HTML in un campo di testo).

**Validazione** — verifica che l'input rispetti le regole attese: tipo corretto, formato valido, valore nel range previsto (es. un'email deve contenere la @, un'età deve essere un numero positivo).

La sanitizzazione da sola non è sufficiente: un input può essere pulito ma comunque sbagliato. Servono entrambe.

### ARIA

*Accessible Rich Internet Applications* — un insieme di attributi HTML che aggiungono informazioni semantiche agli elementi per renderli accessibili agli screen reader e ad altri strumenti di accessibilità. Va usato solo dove l'HTML semantico non è sufficiente: un `<button>` non ha bisogno di `role="button"`, ma un elemento `<div>` usato come pulsante sì.

### Screen Reader

Un programma che legge ad alta voce il contenuto dello schermo, usato principalmente da persone con disabilità visive. Per funzionare correttamente con una pagina web ha bisogno che gli elementi HTML abbiano una struttura semantica corretta e, dove necessario, attributi ARIA.

### Polyfill

Un pezzo di codice che implementa una funzionalità moderna nei browser che non la supportano nativamente. Esempio: se usi una API disponibile solo negli ultimi browser, un polyfill la simula per i browser più vecchi. Il prompt consiglia di non aggiungerne senza che siano strettamente necessari, perché aggiungono peso al bundle.

---

## 6. Performance e architettura

### Build

Il processo che trasforma il codice sorgente (quello che scrivi tu) in file ottimizzati pronti per essere eseguiti dal browser. Tipicamente risolve le dipendenze, unisce i file e prepara tutto per la distribuzione. L'output del build finisce nella cartella `dist/`.

### Bundle

Il file o insieme di file prodotti dal processo di build, che raccoglie tutto il codice dell'applicazione — sorgenti, dipendenze, assets — in un formato ottimizzato per il browser. Il "peso del bundle" è quanto spazio occupa: più è leggero, più veloce è il caricamento dell'app.

### Lazy Loading

Una tecnica che posticipa il caricamento di risorse non necessarie al primo render della pagina — immagini fuori schermo, moduli usati raramente, ecc. Le risorse vengono caricate solo quando servono davvero. Riduce il tempo di caricamento iniziale dell'app.

### Web Worker

Un'API del browser che permette di eseguire codice JavaScript in un thread separato, parallelo a quello principale. Il thread principale gestisce l'interfaccia utente: se lo blocchi con operazioni pesanti (es. calcoli complessi, parsing di file grandi), la pagina si congela. Spostare quelle operazioni in un Web Worker le esegue in background senza bloccare nulla.

### Minificazione

⚠️ *Questo concetto non è presente nel prompt. Potrebbe essere integrato nella sezione opzionale "Build e distribuzione" in futuro.*

La minificazione è il processo che comprime i file rimuovendo spazi, commenti, newline e rinominando le variabili con nomi brevissimi. Il risultato è codice illeggibile da un umano ma identico nel comportamento — più leggero da trasferire via rete.

Esistono tool dedicati per ogni tipo di file:

- **Terser** — minifica JavaScript. Il più usato, supporta ES moderni.
- **cssnano** — minifica CSS. Si integra facilmente con altri tool.
- **html-minifier** — minifica HTML. Rimuove spazi e commenti dal markup.

In alternativa, i bundler come **Vite**, **Rollup**, **esbuild** e **Webpack** includono la minificazione come parte del processo di build, senza bisogno di tool separati. Il prompt attuale esclude i bundler per non aggiungere overhead, ma potrebbero essere introdotti nella sezione opzionale insieme al tree shaking.

### Tree Shaking

⚠️ *Questo concetto non è presente nel prompt. Potrebbe essere integrato nella sezione opzionale "Build e distribuzione" in futuro.*

Il tree shaking è un processo che analizza il codice e rimuove automaticamente tutto ciò che non viene effettivamente usato, riducendo il peso dei file finali. Il termine viene dall'immagine di scuotere un albero per far cadere le foglie secche. È eseguito dai bundler come Vite, Rollup o esbuild durante il processo di build.

---

## 7. Testing

### Tipi di Test

Il prompt definisce cinque livelli di test, ognuno con uno scopo preciso.

**Smoke** — verifica rapida che il sistema si avvii e le funzioni critiche rispondano. È il controllo minimo da fare ad ogni deploy: "l'app parte? Le cose fondamentali funzionano?"

**Unit** — testa una singola funzione in isolamento, senza DOM, senza rete, senza database. Velocissimi da eseguire, coprono la logica di business pura.

**Integration** — testa come due o più moduli si comportano quando interagiscono tra loro. Verifica che le interfacce tra le parti siano compatibili.

**E2E (End-to-End) / Acceptance** — simula il comportamento reale di un utente nel browser: clicca, compila form, naviga. Verifica che l'app soddisfi i requisiti dal punto di vista dell'utente finale.

**Regression** — ogni bug corretto diventa un test. Serve a garantire che quel bug non si ripresenti nelle versioni future.

---

## 8. Concorrenza

### Race Condition

Un errore che si verifica quando due operazioni asincrone concorrenti producono risultati diversi a seconda di quale finisce prima — e il codice non è scritto per gestire questa variabilità. Esempio classico: due richieste API lanciate in sequenza rapida, dove la risposta più vecchia arriva dopo quella più recente e sovrascrive dati già aggiornati.

### Debounce e Throttling

Due tecniche per limitare la frequenza con cui una funzione viene eseguita in risposta a eventi ripetuti (es. digitazione, scroll, resize).

**Debounce** — aspetta che l'evento si fermi per un certo tempo prima di eseguire la funzione. Utile per la ricerca live: non lancia una chiamata API ad ogni tasto, ma solo quando l'utente smette di scrivere.

**Throttling** — esegue la funzione al massimo una volta ogni intervallo di tempo, indipendentemente da quante volte l'evento si ripete. Utile per lo scroll o il resize della finestra.

### Shared Mutable State

Dati condivisi tra più parti del codice che possono essere modificati da ognuna di esse. È una delle principali cause di bug difficili da riprodurre: se due operazioni asincrone modificano lo stesso dato contemporaneamente, il risultato dipende da quale finisce prima. Il prompt chiede di eliminarlo nelle operazioni concorrenti.

### AbortController

Un'API nativa del browser che permette di cancellare una richiesta HTTP in corso. Utile quando l'utente naviga via prima che la risposta arrivi, evitando che codice venga eseguito su una pagina che non esiste più. Il prompt lo cita nella sezione Concorrenza e async.
