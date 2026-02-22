# Il Vibecoder Socratico
### Cheatsheet per sopravvivere (e crescere) nell'era degli AI Agent

---

## Il problema di fondo

> **Non sai cosa non sai che devi sapere.**

Il modello classico di apprendimento ha 4 stadi:
1. Incompetenza inconsapevole — *non sai di non sapere*
2. Incompetenza consapevole — *sai di non sapere*
3. Competenza consapevole — *sai, ma ci devi pensare*
4. Competenza inconsapevole — *sai e lo fai in automatico*

Il Vibe Coder è bloccato allo **stadio 1**. L'AI abbassa la barriera di accesso così tanto che il codice generato sembra professionale: ha una struttura tipizzata, gestisce gli errori e include i test — ma maschera le lacune. Il pericolo non è scrivere codice sbagliato. È non riconoscerlo.

---

## L'SDLC è morto: cosa rimane

L'SDLC (Software Development Life Cycle) era il modello organizzativo che strutturava lo sviluppo software in fasi sequenziali: si raccoglievano i requisiti, si progettava il sistema, si scriveva il codice, si testava, si faceva la code review, si eseguiva il deploy (messa in produzione) e infine si monitorava. Ogni fase aveva i suoi strumenti, i suoi rituali e i suoi tempi — Jira per i requisiti, GitHub per le review, Datadog per il monitoring. Un loop ampio, lineare, pieno di handoff (passaggi di consegne) e attese.

Con gli AI agent, quelle fasi sono **collassate**, non accelerate:

| Fase SDLC classica | Stato oggi |
|---|---|
| Requirements | Contesto fluido dato all'agente, non una fase |
| System Design | Si *scopre* collaborando, non si prescrive |
| Implementation | Delegata all'agente |
| Testing | Simultaneo alla generazione del codice |
| Code Review / PR | Da ripensare: gli agenti generano 500 PR/giorno |
| Deployment | Continuo, automatizzato, disaccoppiato dal release |
| **Monitoring** | **L'unico sopravvissuto — diventa il feedback loop centrale** |

**Il nuovo ciclo:**
```
Intent → Agent → Build/Test/Deploy → Observe → Repeat
```

---

## Il paradosso delle testsuite generate da LLM

Chiedere all'LLM di scrivere codice e test nella stessa context window ( la finestra di memoria attiva della sessione) è come chiedere a uno studente di scrivere il compito e la correzione.

**I test passano perché sono coerenti con l'implementazione, non perché l'implementazione sia corretta.**

### Cosa manca sempre nelle testsuite generate:
- Edge case (casi limite o imprevisti) non descritti nel prompt originale
- **Load testing** (comportamento sotto carico) e **Concurrency** (concorrenza)
- Interazioni tra componenti visti in isolamento
- Scenari di sicurezza (input malevoli, auth bypass (aggiramento dell'autenticazione))
- Fallimenti di dipendenze esterne (DB giù, API lenta, timeout (scadenza del tempo di risposta))
- Strumentazione di debug (logging del flusso interno, breakpoint) — l'agente testa il comportamento esterno ma non inserisce tracce per capire cosa succede dentro

### La trappola della coverage (copertura dei test)
90% di coverage non significa nulla se i test misurano che il codice viene *eseguito*, non che sia *corretto*.

---

## Le domande che la produzione farà al posto tuo

Se non te le fai prima, te le farà la produzione — nel momento peggiore.

- Cosa succede quando l'app va sotto carico?
- Cosa succede se il database è irraggiungibile?
- il tuo sistema è vulnerabile a SQL injection?
- Chi paga se le API call esplodono in volume?
- Cosa succede se due utenti modificano lo stesso record contemporaneamente?
- Dove vanno a finire gli errori non gestiti?
- Quanto tempo ci vuole a fare un rollback?

---

## Le soluzioni pratiche

### 1. Separare chi scrive da chi testa
Due sessioni/agenti distinti. Il secondo vede solo la **specifica**, non l'implementazione. Questo rompe il loop di assunzioni condivise.

```
Agente A → scrive il codice dalla specifica
Agente B → scrive i test dalla specifica (senza vedere il codice di A)
```

### 2. Definire i comportamenti attesi prima del codice
Non TDD (Test-Driven Development, sviluppo guidato dai test) classico, ma un contratto: *"cosa deve essere vero"* prima di *"come funziona"*. L'LLM poi verifica che il codice rispetti quel contratto.

### 3. Metodo critico sistematico
Non solo *"costruisci"*, ma anche *"distruggi quello che hai costruito"*.

Prompt utili:
- *"Prova a rompere questo codice"*
- *"Cosa può andare storto in questo sistema?"*
- *"Quali assunzioni stai facendo che potrebbero essere false?"*
- *"Come potrebbe un attaccante sfruttare questo?"*

### 4. Esposizione ai fallimenti reali
Niente sostituisce il traffico vero. Anche in piccolo:
- **Feature flags** (interruttori per attivare/disattivare funzionalità) per rilasci progressivi
- **Canary release** (rilascio graduale a un sottoinsieme di utenti) per limitare il blast radius (l'impatto in caso di errore)
- **Error log** (registro degli errori) — anche minimi, anche su file
- Leggi i log. Sempre.

### 5. Imparare a fare debug (ricerca e correzione degli errori)
Il debug non è chiedere all'agente *"perché non funziona?"* e sperare nella risposta giusta. È un processo sistematico: isolare il problema, riprodurlo in modo controllato, capire *dove* il comportamento devia da quello atteso.

Chiedi esplicitamente all'agente di aggiungere strumentazione:
- **Logging** (registrazione del flusso interno) — per sapere cosa fa il codice durante l'esecuzione
- **Breakpoint** (punti di interruzione) — per ispezionare lo stato in un momento preciso

Le domande giuste da fare all'agente in fase di debug:
- *"In quale punto esatto il comportamento smette di essere quello atteso?"*
- *"Cosa dovrebbe restituire questa funzione e cosa restituisce invece?"*
- *"Riproduci il problema nel caso più semplice possibile"*

---

## Le nuove competenze chiave

Il Vibe Coder non deve diventare un ingegnere tradizionale. Deve diventare un buon **Vibecoder Socratico**: sa cosa vuole, sa valutare il risultato, sa leggere i segnali quando qualcosa non va, sa fare le domande giuste *prima* che le faccia la produzione.

Queste sono le competenze concrete per arrivarci.

### Context Engineering
La qualità di ciò che costruisci con gli agenti è **direttamente proporzionale alla qualità del contesto che fornisci**.

Non è prompt engineering (arte di formulare istruzioni efficaci per l'agente) tattico. È quasi una forma di scrittura tecnica:
- documenti di architettura
- vincoli espliciti
- decisioni già prese e perché
- casi limite noti

### Giudizio architetturale
Non saper disegnare un sistema da zero, ma saper riconoscere quando l'agente:
- rende il sistema più complesso del necessario
- ottimizza prematuramente parti che non sono il collo di bottiglia
- ignora un vincolo importante
- fa assunzioni implicite pericolose

### Observability: il sistema che si osserva da solo
L'observability non è uno schermo pieno di grafici che qualcuno guarda quando qualcosa si rompe. È ciò che permette all'agente di accorgersi da solo che qualcosa non va e correggersi — senza aspettare che sia un umano a notarlo.

In assenza di un mentore umano che faccia le domande giuste, l'unico sostituto è praticare sistematicamente il metodo critico con l'agente stesso — fare le domande scomode prima che le faccia la produzione.

---

## La verità scomoda

> Un certo livello di incompetenza inconsapevole rimane sempre.

L'obiettivo non è eliminarla. È **restringerla nel tempo** attraverso i fallimenti — possibilmente piccoli, controllati, e in ambienti dove l'impatto in caso di errore sia limitato.

Rilascia. Osserva. Rompi. Impara. Ripeti.

---


