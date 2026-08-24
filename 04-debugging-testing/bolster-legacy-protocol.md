# BOLSTER — Bug, Organization, Logging, Specs, Testing, Error, Review

**Ambito:** Progetti Frontend — HTML, CSS, JavaScript

**Uso:** Protocollo per agenti AI

**Note:** Le fasi che richiedono una decisione dell'utente sono esplicitamente indicate

---

## Introduzione

Quando si eredita codice legacy, quando il technical debt ha raggiunto un livello critico, quando si vuole affrontare un refactor o un rewrite senza rischiare di rompere tutto, quando si vuole introdurre testing e debugging su un progetto che non ne ha mai avuti — il problema è sempre lo stesso: **non si sa davvero cosa fa il codice**.

Si intuisce, si suppone, si ricorda. Ma non si sa.

BOLSTER parte da lì. Prima di toccare qualsiasi cosa, prima di refactorare, riscrivere, ottimizzare o aggiungere funzionalità, il progetto viene letto, compreso, analizzato e documentato nella sua interezza. Si estraggono le specifiche reali dal codice reale. Si costruisce una test suite che verifica che quelle specifiche siano vere. Si tracciano e si risolvono i bug noti.

Solo a quel punto il progetto è in uno stato in cui intervenire ha senso — con una base documentata su cui appoggiarsi, specifiche verificate con cui confrontarsi, e una test suite con cui validare ogni modifica futura.

---

### Istruzioni per l'agente

Leggi questo documento nella sua interezza prima di iniziare qualsiasi operazione. Procedi poi dalla Fase 0 seguendo l'ordine sequenziale senza saltare fasi. Ogni fase che richiede una decisione dell'utente è esplicitamente indicata — in quei punti fermati, presenta le opzioni e attendi approvazione prima di procedere.

---

## FASE 0 — Lettura e Comprensione del Codice

**Obiettivo:** acquisire una visione completa e precisa del progetto prima di qualsiasi intervento. In questa fase l'agente si limita a **osservare e raccogliere** senza interpretare o classificare.

- Leggere **tutti** i file del progetto senza eccezioni
- Identificare: entry point, dipendenze, struttura logica, pattern usati
- Rilevare: librerie esterne, versioni, CDN vs locale
- Mappare il flusso dati e le interazioni tra componenti/moduli
- Prendere nota di: TODO, FIXME, codice commentato, inconsistenze di stile

> ⚠️ Nessuna modifica e nessuna valutazione viene effettuata in questa fase. Solo osservazione.

---

## FASE 1 — Analisi del Progetto

**Obiettivo:** elaborare e classificare tutto ciò che è stato osservato in Fase 0, producendo `ANALYSIS.md` nella root del progetto originale, con una diagnosi completa del progetto allo stato attuale.

Il file include:

- Stato attuale del progetto (dimensioni, complessità, debito tecnico stimato)
- Problemi rilevati (bug evidenti, codice duplicato, dipendenze obsolete, ecc.)
- Opportunità di miglioramento (leggibilità, performance, manutenibilità)

**L'agente presenta `ANALYSIS.md` all'utente.**

---

## FASE 2 — Estrazione delle Specifiche

**Obiettivo:** redigere un documento di specifiche completo e minuzioso che descriva il funzionamento reale del progetto, ricavato esclusivamente dall'analisi del codice. Il file `SPECS.md` viene creato nella root del progetto originale.

L'agente produce un file `SPECS.md` che include:

### 2.1 — Panoramica del Progetto
- Scopo e funzione dell'applicazione
- Tecnologie utilizzate e versioni
- Entry point e ciclo di vita dell'app

### 2.2 — Architettura e Struttura
- Mappa dei file e responsabilità di ciascuno
- Dipendenze tra moduli/componenti
- Flusso di esecuzione principale

### 2.3 — Meccaniche e Logica di Business
- Descrizione dettagliata di ogni funzionalità implementata
- Algoritmi e logiche non ovvie commentate e spiegate
- Gestione degli stati e delle transizioni
- Gestione degli errori e dei casi limite

### 2.4 — Interfaccia e Interazioni Utente
- Elenco degli elementi interattivi e loro comportamento
- Eventi gestiti (click, input, resize, ecc.)
- Feedback visivi e animazioni

### 2.5 — Dati e Persistenza
- Struttura dei dati in uso (oggetti, array, formato)
- Fonti dati (hardcoded, API, localStorage, ecc.)
- Flusso di lettura/scrittura

### 2.6 — Anomalie e Ambiguità Rilevate
- Comportamenti incerti o potenzialmente non intenzionali
- Codice che sembra incompleto o contraddittorio
- Punti che richiedono chiarimento con l'utente

> ⚠️ Il file `SPECS.md` descrive **come funziona il codice oggi**, non come dovrebbe funzionare.
> Eventuali discrepanze con le intenzioni dell'utente emergono nella discussione successiva.

**L'agente presenta `SPECS.md` all'utente e discute eventuali correzioni o integrazioni prima di procedere alle fasi successive.**

---

## FASE 3 — Documentazione e Riorganizzazione del Progetto

### 3.1 — Redazione `REPORT.md`

L'agente redige un `REPORT.md` nella root del progetto originale che descrive il progetto **così com'è attualmente**, basandosi su tutto ciò che ha acquisito nelle fasi precedenti. Si usa `REPORT.md` e non `README.md` per evitare conflitti con un eventuale file già esistente:

- Nome, scopo e descrizione dell'applicazione
- Tecnologie e dipendenze utilizzate
- Istruzioni di installazione e avvio
- Panoramica delle funzionalità principali
- Struttura attuale dei file

### 3.2 — Proposta di Nuova Struttura

L'agente formula **due proposte** di riorganizzazione da presentare all'utente:

- **Proposta conservativa** — intervento minimo: raggruppamento dei file esistenti in cartelle logiche senza modificare il codice (es. `/css`, `/js`, `/assets`)
- **Proposta intermedia** — riorganizzazione più coerente: suddivisione dei file in una struttura modulare semplice e gestibile, coerente con le logiche rilevate nelle specs

L'agente presenta entrambe le opzioni, ne discute i pro/contro con l'utente e attende approvazione prima di procedere.

### 3.3 — Creazione della Nuova Cartella di Progetto

Una volta concordata la struttura, l'agente:

- Crea la nuova cartella di progetto con la struttura approvata
- Copia e riorganizza i file secondo la struttura concordata
- Crea la cartella `/docs` e vi copia `ANALYSIS.md` e `SPECS.md` dalla root del progetto originale
- Aggiorna `ANALYSIS.md` e `SPECS.md` in `/docs` per riflettere la nuova struttura
- Rilegge `ANALYSIS.md` e `SPECS.md` aggiornati e crea `KNOWN_BUGS.md` in `/docs` con tutti i problemi rilevati
- Crea la cartella `/test` vuota, pronta per la fase di testing
- Crea e compila `CHANGELOG.md` in `/docs` in formato [Keep a Changelog](https://keepachangelog.com) con tutti i cambiamenti effettuati: file spostati, rinominati, struttura creata
- Crea un nuovo `README.md` nella nuova cartella di progetto per ultimo, basandosi su `REPORT.md` e aggiornandolo per riflettere la nuova struttura, includendo riferimenti a `/docs`, `/test` e ai file in essa contenuti

---

## FASE 4 — Test Suite

**Obiettivo:** creare una test suite funzionante in `/test/test_suite.html` che verifichi che il comportamento reale dell'app corrisponda a quanto documentato in `SPECS.md`, e che esponga i bug noti in `KNOWN_BUGS.md`.

### 4.1 — Valutazione dell'Approccio

L'agente legge `ANALYSIS.md` e `SPECS.md` e valuta con l'utente quale approccio adottare:

- **Mocha + Chai via CDN** *(consigliato di default)* — le librerie vengono caricate da CDN senza dipendenze locali, gira nel browser, output leggibile
- **Vanilla JS puro** — se il progetto è minimale e non richiede un framework di asserzione

L'agente presenta la raccomandazione e attende conferma prima di procedere.

### 4.2 — Requisiti della Test Suite

Il file `test_suite.html` deve rispettare i seguenti requisiti:

**Struttura e intestazione**
- Commento in testa che dichiara esplicitamente lo scopo: verificare che le funzioni reali dell'app producano i risultati attesi secondo `SPECS.md`
- Avvertenza esplicita: i test devono chiamare le **funzioni reali** dell'app, non replicare la logica localmente
- Il mocking è consentito **solo** per elementi UI/DOM, mai per la logica di business

**Test**
- Ogni test è numerato e corredato da un commento conciso che indica: cosa testa, a quale sezione di `SPECS.md` fa riferimento, e se riguarda un bug noto (con riferimento a `KNOWN_BUGS.md`)
- I test relativi a bug noti sono marcati esplicitamente come `[KNOWN BUG]` e ci si aspetta che **falliscano**
- I test relativi a workaround documentati sono marcati come `[WORKAROUND]`
- Ogni test resetta lo stato globale necessario prima di eseguire, garantendo isolamento completo
- Il DOM fixture (se necessario) è presente ma nascosto, e rispecchia la struttura reale dell'app

**Interfaccia**
- Pulsante **Run Test Suite** per avviare i test manualmente
- Console di log integrata (stile terminale) che mostra in tempo reale `[PASS]` / `[FAIL]` con descrizione dell'errore
- Pulsante **Export Log** per salvare il report in un file `.txt`
- Riepilogo finale: totale test passati e falliti

### 4.3 — Copertura Minima Attesa

L'agente ricava da `SPECS.md` e `KNOWN_BUGS.md` i test da scrivere, coprendo:

- Le meccaniche e funzioni principali (sezione 2.3 di `SPECS.md`)
- La gestione degli errori e dei casi limite (sezione 2.3)
- Le interazioni UI che producono effetti sulla logica (sezione 2.4)
- Tutti i bug noti in `KNOWN_BUGS.md`, ciascuno con un test dedicato

### 4.4 — Documentazione e Aggiornamenti Finali

Al termine, nell'ordine:

- Crea `test_report.md` in `/test` con le specifiche della test suite: approccio scelto, elenco dei test scritti, copertura, bug noti testati e workaround documentati
- Aggiorna `README.md` nella cartella di progetto per riflettere la nuova struttura file inclusa `/test`
- Chiede all'utente di aprire `test_suite.html` nel browser, eseguire i test tramite il pulsante **Run Test Suite**, esportare il log tramite **Export Log** e incollare il contenuto — questo log sarà il punto di partenza della Fase 5

---

## FASE 5 — Debugging

**Obiettivo:** rendere la test suite affidabile e usarla per identificare e risolvere i bug dell'app.

### 5.1 — Validazione della Test Suite

L'agente riceve il log esportato dall'utente in Fase 4 e lo analizza:

- Analizza ogni `[FAIL]` distinguendo tra:
  - **Errore nella test suite** — test mal scritto, riferimento a funzione errato, stato globale non resettato, DOM fixture incompleto
  - **Bug reale nell'app** — il test è corretto ma la funzione si comporta in modo difforme da `SPECS.md`
  - **Bug noto atteso** — marcato `[KNOWN BUG]`, il fallimento è intenzionale e documentato
- Presenta all'utente gli errori trovati nella test suite e come intende correggerli prima di procedere
- Corregge gli errori nella test suite
- Chiede all'utente di rieseguire `test_suite.html` e fornire il nuovo log
- Ripete il ciclo fino a ottenere una suite priva di errori propri
- Documenta gli errori trovati nella test suite in `test_report.md` in `/test`

> ⚠️ Un test che fallisce per un errore nella suite non dice nulla sull'app. La suite deve essere corretta prima di procedere.

### 5.2 — Debugging dell'App

Con la test suite validata, l'agente procede a risolvere i bug reali:

- Prende in carico i `[FAIL]` confermati come bug reali, partendo da quelli già presenti in `KNOWN_BUGS.md`
- Per ogni bug: presenta all'utente la causa identificata e l'intervento proposto, attende approvazione prima di procedere
- Interviene sul codice in modo chirurgico, verifica che il test passi
- Rimuove il bug da `KNOWN_BUGS.md` una volta risolto, o aggiorna la sua descrizione se solo parzialmente corretto
- Se emergono nuovi bug non documentati, li aggiunge a `KNOWN_BUGS.md` prima di intervenire

### 5.3 — Aggiornamenti Finali

Al termine, nell'ordine:

- Aggiorna `test_report.md` in `/test` con i risultati finali della suite
- Aggiorna `SPECS.md` in `/docs` se il debugging ha rivelato comportamenti diversi da quanto documentato
- Aggiorna `KNOWN_BUGS.md` in `/docs` con lo stato aggiornato dei bug
- Aggiorna `CHANGELOG.md` in `/docs` con i bug risolti e le modifiche al codice
- Aggiorna `README.md` se necessario
