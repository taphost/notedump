# STILI DI THINKING PER REVISIONE E ANALISI

Raccolta di approcci cognitivi applicabili a revisione di codice, documenti tecnici, audit di sicurezza e analisi di sistema. Per ogni stile: descrizione, quando usarlo, come applicarlo.

---

# ◆ ADVERSARIAL

## GAN Style (Generatore / Critico)

**Descrizione**
Due passate separate e antagoniste. Il Generatore produce o valida il contenuto con un atteggiamento ottimista. Il Critico attacca attivamente le conclusioni del Generatore cercando di smontarle.

**Quando usarlo**
Revisione di documenti che hai scritto tu stesso. Situazioni in cui il bias di conferma è un rischio concreto.

**Come applicarlo**
1. Passata 1 — leggi come se il documento fosse scritto da qualcun altro e fosse probabilmente corretto
2. Passata 2 — cambia postura: parti dall'assunzione che ci sia almeno un errore grave e trovalo
3. Riconcilia: quali problemi ha trovato solo il Critico?

---

## Red Team / Blue Team

**Descrizione**
Il Red Team cerca attivamente come sfruttare una vulnerabilità o falsificare un'assunzione. Il Blue Team valuta se i fix proposti reggono all'attacco. I ruoli non si sovrappongono durante la sessione.

**Quando usarlo**
Audit di sicurezza, revisione di architetture, validazione di fix. Più strutturato del GAN: richiede che i due ruoli non comunichino fino alla fase di riconciliazione.

**Come applicarlo**
1. Red Team — elenca tutti i modi in cui il sistema può essere compromesso o il documento può essere sbagliato
2. Blue Team — per ogni attacco Red, valuta se esiste una difesa adeguata nel documento/sistema
3. Gap analysis — gli attacchi senza difesa sono i problemi prioritari

---

## Devil's Advocate

**Descrizione**
Parti dall'assunzione che il documento o la decisione sia sbagliata e costruisci il caso contrario nel modo più forte possibile. Più aggressivo del GAN critico perché non c'è un generatore da smontare — si parte già in opposizione.

**Quando usarlo**
Decisioni architetturali, scelte di design, assunzioni di sicurezza date per scontate. Utile quando il gruppo è troppo allineato e manca una voce critica.

**Come applicarlo**
1. Prendi la tesi principale del documento
2. Costruisci il caso contrario più forte possibile, ignorando le tue opinioni reali
3. Valuta: la tesi regge all'argomentazione contraria? Se no, va rivista

## Rubber Duck + Critico

**Descrizione**
Spiega il documento o il sistema ad alta voce come se fosse la prima volta, a un interlocutore immaginario (il rubber duck). Poi un critico attacca le spiegazioni. La fase di spiegazione forza la chiarezza; la fase critica trova le inconsistenze.

**Quando usarlo**
Debug di ragionamenti complessi, revisione di documentazione tecnica, preparazione a domande di un auditor reale.

**Come applicarlo**
1. Spiega ogni sezione del documento come se non l'avessi mai letta, ad alta voce o per iscritto
2. Ogni volta che la spiegazione diventa vaga o incerta, marca il punto
3. Il Critico attacca i punti marcati e le spiegazioni che sembrano circolari o incomplete

---

# ◆ PROSPETTIVA MULTIPLA

## Stakeholder Rotation

**Descrizione**
Leggi il documento o analizza il sistema assumendo la prospettiva di stakeholder diversi in sequenza. Ogni prospettiva ha obiettivi, conoscenze e punti ciechi diversi.

**Quando usarlo**
Revisione di documentazione tecnica, API design, security audit. Particolarmente efficace per trovare problemi che sono ovvi per alcuni ruoli e invisibili per altri.

**Come applicarlo**
Leggi il documento come lo leggerebbe ciascuno di questi profili:
- **Dev junior** — cosa non capisce? cosa potrebbe fraintendere?
- **Dev senior** — cosa manca? cosa è impreciso o incompleto?
- **Attaccante** — cosa può sfruttare? dove sono i punti deboli?
- **Auditor** — cosa non è dimostrabile? cosa manca di evidenza?

---

## Six Thinking Hats (De Bono)

**Descrizione**
Sei modalità di pensiero distinte, rappresentate da cappelli colorati. Si applica una modalità alla volta, separando deliberatamente fatti, emozioni, rischi, benefici, creatività e processo.

**Quando usarlo**
Decisioni complesse con molte variabili, brainstorming strutturato, situazioni in cui il gruppo mescola tipi di ragionamento diversi nella stessa discussione.

**I sei cappelli**
| Cappello | Modalità | Domanda guida |
|---|---|---|
| ⬜ Bianco | Fatti e dati puri | Cosa sappiamo con certezza? |
| 🔴 Rosso | Emozioni e intuizioni | Cosa ci disturba di questa soluzione, anche senza dati a supporto? |
| ⬛ Nero | Rischi e criticità | Cosa può andare storto? |
| 🟡 Giallo | Benefici e ottimismo | Qual è il valore potenziale? |
| 🟢 Verde | Creatività e alternative | Esistono altre soluzioni? |
| 🔵 Blu | Processo e meta-pensiero | Stiamo usando il tempo bene? |

---

# ◆ SISTEMATICO

## FMEA (Failure Mode and Effects Analysis)

**Descrizione**
Per ogni componente del sistema: identifica i modi in cui può fallire, valuta la probabilità di ogni failure, valuta l'impatto, calcola una priorità. Originariamente sviluppato per ingegneria hardware, applicabile a software e security.

**Quando usarlo**
Analisi di sistemi complessi, audit di sicurezza strutturati, revisione di architetture prima del deploy. Produce output quantificabili e prioritizzabili.

**Come applicarlo**
Per ogni componente o sezione del documento:
1. **Failure Mode** — in che modo può fallire o essere sbagliato?
2. **Effect** — qual è l'impatto se fallisce?
3. **Severity** (1-10) — quanto è grave l'impatto?
4. **Probability** (1-10) — quanto è probabile che accada?
5. **Detectability** (1-10) — quanto è difficile rilevare il failure prima che causi danno? (1 = facile da rilevare, 10 = quasi impossibile)
6. **RPN** = Severity × Probability × Detectability — priorità di intervento

---

## Pre-mortem

**Descrizione**
Immagina che il sistema sia già stato compromesso o che il progetto sia già fallito. Ricostruisci a ritroso come è successo. Forza il pensiero controfattuale invece di quello predittivo.

**Quando usarlo**
Revisione di architetture di sicurezza, pianificazione di release critiche, validazione di fix. Particolarmente efficace perché abbassa la resistenza psicologica a identificare problemi — non stai "criticando", stai "ricostruendo".

**Come applicarlo**
1. Assumi che tra 6 mesi il sistema sia stato violato (o il documento abbia causato un problema grave)
2. Scrivi la storia di come è successo, nel modo più dettagliato possibile
3. Identifica i punti della storia che corrispondono a debolezze reali nel sistema attuale
4. Prioritizza i fix basandoti sulla plausibilità della storia

---

# ◆ ITERATIVO

## Socratic Questioning

**Descrizione**
Ogni affermazione viene interrogata sistematicamente con domande che ne mettono alla prova la solidità. Non si accetta nessuna assunzione implicita.

**Quando usarlo**
Smontare assunzioni date per scontate, validare ragionamenti complessi, identificare punti deboli in argomentazioni tecniche o di sicurezza.

**Le domande guida**
- *Perché è così?* — metti alla prova la giustificazione
- *Come lo sai?* — verifica l'evidenza
- *Cosa succederebbe se fosse falso?* — testa la robustezza
- *Esistono controesempi?* — cerca i casi limite
- *Questa affermazione vale sempre o solo in alcune condizioni?* — identifica i presupposti nascosti

---

# ◆ QUALE USARE QUANDO

> Gli stili possono essere combinati in sequenza. La colonna destra indica la combinazione più efficace per ogni obiettivo — non necessariamente alternativa.

| Obiettivo | Stile consigliato |
|---|---|
| Revisione documento scritto da te | GAN Style → Rubber Duck + Critico |
| Audit di sicurezza | Red Team / Blue Team → Pre-mortem |
| Decisione architetturale | Devil's Advocate → Six Thinking Hats |
| Analisi di rischio strutturata | FMEA |
| Smontare assunzioni implicite | Socratic Questioning |
| Trovare problemi invisibili per il team | Stakeholder Rotation |
| Documento tecnico complesso | GAN Style → Stakeholder Rotation |
