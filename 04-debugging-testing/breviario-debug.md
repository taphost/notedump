# Breviario del Debugging
## Principi di David Agans e Andreas Zeller

---

## Le 9 Regole Fondamentali di Agans

### 1. Comprendi il Sistema
**Principio:** Non puoi debuggare ciò che non capisci.

- Leggi la documentazione
- Studia l'architettura
- Traccia il flusso dei dati
- Identifica le dipendenze
- **Mai assumere** - verifica sempre

**Domande da porsi:**
- Come dovrebbe funzionare?
- Quali sono gli input e output?
- Quali componenti interagiscono?

---

### 2. Fallo Fallire
**Principio:** Un bug che non si riproduce non può essere risolto.

- Crea un test case riproducibile
- Automatizza la riproduzione
- Documenta i passi esatti
- Identifica le condizioni necessarie
- Riduci le variabili al minimo

**Obiettivo:** Passare da "a volte fallisce" a "fallisce sempre quando X".

---

### 3. Smetti di Pensare e Guarda
**Principio:** I dati reali battono le ipotesi.

- Usa debugger, log, trace
- Osserva cosa succede realmente
- Non fidarti della tua memoria
- Misura, non supporre
- I sintomi dicono la verità

**Errore comune:** Teorizzare senza verificare empiricamente.

---

### 4. Dividi e Conquista
**Principio:** Isola progressivamente la causa.

- Binary search nel codice/processo
- Disabilita componenti uno alla volta
- Testa moduli isolati
- Restringi lo spazio del problema
- Usa breakpoint strategici

**Strategia:** Dimezza ripetutamente il campo di ricerca.

---

### 5. Cambia Una Cosa alla Volta
**Principio:** Modifiche multiple nascondono la causa.

- Una modifica = un esperimento
- Documenta ogni cambiamento
- Testa dopo ogni modifica
- Se non funziona, annulla (rollback)
- No "spaghetti fixes"

**Disciplina:** Resistere alla tentazione di "provare tutto insieme".

---

### 6. Tieni un Registro delle Attività
**Principio:** La memoria inganna, i log no.

- Scrivi cosa hai provato
- Annota i risultati
- Traccia le ipotesi
- Documenta le configurazioni
- Timestamp di ogni azione

**Benefici:** Evita ripetizioni, identifica pattern, comunicazione team.

---

### 7. Controlla la Spina
**Principio:** Le cause banali sono le più frequenti.

- Verifica le assunzioni di base
- Controllo sanity check
- File di configurazione corretti?
- Permessi adeguati?
- Versioni software compatibili?

**Mantra:** "È acceso? È collegato? È la versione giusta?"

---

### 8. Ottieni una Prospettiva Fresca
**Principio:** L'autore del codice ha bias cognitivi.

- Chiedi a un collega
- Spiega il problema ad alta voce (rubber duck)
- Fai una pausa e torna dopo
- Leggi il codice come se fosse nuovo
- Domanda le tue assunzioni

**Effetto:** Rompe il tunnel vision.

---

### 9. Se Non l'Hai Risolto, Non È Risolto
**Principio:** Verifica sempre la fix.

- Testa la soluzione rigorosamente
- Verifica che il bug originale sia sparito
- Controlla che non ci siano regressioni
- Comprendi PERCHÉ la fix funziona
- Nessun "fix magico" accettabile

**Standard:** Devi essere in grado di spiegare la causa e la soluzione.

---

## Il Metodo Scientifico di Zeller

### Approccio Sistematico al Debugging

#### 1. Osservazione del Problema
- **Sintomo:** Cosa va storto?
- **Input:** Cosa causa il fallimento?
- **Output:** Cosa ci si aspettava vs cosa si ottiene?
- **Contesto:** Ambiente, configurazione, stato

#### 2. Formulazione di Ipotesi
- Identifica possibili cause
- Basati su osservazioni, non supposizioni
- Usa la conoscenza del sistema
- Considera cause multiple

**Esempio:**
- Ipotesi A: Buffer overflow
- Ipotesi B: Race condition
- Ipotesi C: Input validation mancante

#### 3. Predizione
Per ogni ipotesi, predici cosa osserveresti se fosse vera.

**Se ipotesi A (buffer overflow):**
- Memory corruption in zone adiacenti
- Crash su input > dimensione buffer
- Comportamento deterministico

#### 4. Sperimentazione
- Progetta esperimenti per testare le ipotesi
- Cambia una variabile alla volta
- Documenta setup e risultati
- Usa controlli (baseline)

#### 5. Analisi dei Risultati
- L'ipotesi è confermata o confutata?
- I dati supportano o contraddicono?
- Servono ulteriori esperimenti?

#### 6. Conclusione
- Identifica la causa root
- Comprendi il meccanismo
- Implementa e verifica la fix

---

## Delta Debugging (Tecnica di Zeller)

### Principio
Minimizza automaticamente il test case che causa il bug.

**Nota:** Funziona meglio con bug deterministici. Per bug non-deterministici (race conditions, timing issues) possono essere necessarie tecniche complementari.

### Processo
1. **Input grande** che causa bug
2. **Dividi a metà** l'input
3. **Testa ciascuna metà**
   - Se metà A fallisce → lavora su A
   - Se metà B fallisce → lavora su B
   - Se entrambe passano → il bug richiede elementi da A+B
4. **Ripeti ricorsivamente** fino a input minimale

### Esempio
```
Input originale: 1000 linee di codice crashano
Dopo delta debugging: 3 linee che riproducono il bug
```

### Applicazioni
- Minimizzare input che causa crash
- Identificare commit che ha introdotto bug (git bisect)
- Semplificare test case complessi

---

## Strategie di Isolamento

### Backward Reasoning (Da Effetto a Causa)
1. Parti dal sintomo
2. Identifica la funzione/modulo che produce output errato
3. Traccia all'indietro le dipendenze
4. Trova il punto dove i dati diventano corrotti

### Forward Reasoning (Da Causa a Effetto)
1. Parti dall'input
2. Segui il flusso di esecuzione
3. Verifica stato a ogni checkpoint
4. Trova dove l'output diverge dall'atteso

### Debugging Binario
- Inserisci checkpoint a metà del processo
- Se checkpoint OK → bug è dopo
- Se checkpoint FAIL → bug è prima
- Ripeti fino a isolare la linea

---

## Tecniche di Riproduzione

### Il Test Case Ideale
- **Minimalista:** Solo elementi necessari
- **Deterministico:** Stesso input = stesso output
- **Automatizzato:** Script eseguibile
- **Veloce:** Esecuzione rapida
- **Auto-validante:** Verifica automatica pass/fail

### Riduzione Input
```
1. Rimuovi metà input
2. Testa se bug persiste
3. Se sì → continua con input ridotto
4. Se no → ripristina e rimuovi altra metà
5. Ripeti fino a minimo input riproducibile
```

### Environment Isolation
- Stessa versione OS/librerie
- Stessi dati di configurazione
- Stesso stato iniziale
- Variabili ambiente identiche

---

## Strumenti Mentali

### Rubber Duck Debugging
Spiega il problema ad alta voce (anche a un oggetto inanimato):
1. Descrivi cosa dovrebbe fare il codice
2. Spiega cosa fa realmente
3. Argomenta perché dovrebbe funzionare
4. Spesso la soluzione emerge durante la spiegazione

### Assumere Responsabilità del Proprio Codice
**Principio:** "Colpa mia finché non provato altrimenti"

- Assumi che il bug sia nel TUO codice
- Solo dopo prove esaustive considera bug in:
  - Compilatore
  - Sistema operativo
  - Librerie standard
  - Hardware

**Razionale:** Statisticamente, il bug è quasi sempre nel codice applicativo, non negli strumenti di base ampiamente testati.

### Causa Root vs Sintomo
```
Sintomo: Applicazione crasha
Causa apparente: Puntatore NULL
Causa root: Mancata validazione input utente
Fix superficiale: if(ptr != NULL)
Fix corretto: Validare input alla sorgente
```

---

## Checklist Pratica

### Prima di Iniziare
- [ ] Comprendo cosa il sistema dovrebbe fare?
- [ ] Ho un test case riproducibile?
- [ ] Ho un registro per documentare il processo?
- [ ] Ho verificato le assunzioni base (la "spina")?

### Durante il Debug
- [ ] Sto guardando dati reali o ipotizzando?
- [ ] Ho cambiato una sola cosa?
- [ ] Ho documentato questo esperimento?
- [ ] Ho testato l'ipotesi corrente?
- [ ] Ho considerato cause banali?

### Dopo la Fix
- [ ] Ho capito PERCHÉ il bug esisteva?
- [ ] Ho verificato che la fix risolve il problema?
- [ ] Ho controllato assenza di regressioni?
- [ ] Ho documentato causa e soluzione?
- [ ] Ho aggiunto test per prevenire ricorrenza?

---

## Anti-Pattern da Evitare

### ❌ Random Walk Debugging
Cambiare codice a caso sperando che funzioni.

**Alternativa:** Ipotesi → Test → Analisi

### ❌ Superstitious Debugging
"Funziona ma non so perché."

**Alternativa:** Comprendi sempre il meccanismo

### ❌ Debugging by Coincidence
"Ho cambiato X e ora funziona."

**Alternativa:** Verifica relazione causale

### ❌ Wolf Fence Debugging
Teorie campate in aria senza dati.

**Alternativa:** Osservazioni empiriche prima

### ❌ Debugging by Denial
"Il mio codice è corretto, è colpa del compilatore."

**Alternativa:** "Colpa mia finché non provato altrimenti"

---

## Euristiche Utili

### Legge di Pareto del Debugging
- 80% dei bug sono in 20% del codice
- Focus su: codice recente, codice complesso, edge case

### Principio di Occam
La spiegazione più semplice è solitamente quella corretta.

### Correlazione ≠ Causazione
Solo perché A e B accadono insieme non significa che A causa B.

### Il Bug Heisenberg
L'atto di osservare cambia il comportamento (es. race condition).

**Origine:** Il nome deriva dal principio di indeterminazione di Heisenberg in fisica quantistica, dove l'osservazione di una particella ne altera lo stato.

**Soluzione:** Logging non-invasivo, replay deterministico, analisi post-mortem

---

## Conclusione

### I Tre Pilastri
1. **Metodo scientifico** (Zeller): Osserva, ipotizza, sperimenta, analizza
2. **Discipline pragmatiche** (Agans): Sistematico, documentato, empirico
3. **Mindset critico**: Questiona assunzioni, verifica dati, comprendi profondamente

### Quando Sei Bloccato
1. Fai una pausa
2. Rileggi questo breviario
3. Torna al principio "Comprendi il Sistema"
4. Chiedi aiuto (prospettiva fresca)
5. Semplifica il problema (delta debugging)

### Ricorda
> "Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it."
> — Brian W. Kernighan

**La soluzione:** Scrivi codice semplice, debugga sistematicamente.

---

*Breviario compilato dai principi di:*
- *David J. Agans - "Debugging: The 9 Indispensable Rules"*
- *Andreas Zeller - "Why Programs Fail: A Guide to Systematic Debugging"*