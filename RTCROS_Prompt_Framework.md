# Framework RTCROS per Prompt Engineering

## Panoramica
RTCROS è un framework strutturato per creare prompt efficaci con i modelli AI. Ogni componente guida l'AI verso risultati più precisi e utili.

---

## 🎭 R - Ruolo (Role)
**Definisci l'identità dell'AI**

- Chi deve essere? (esperto, consulente, insegnante, analista)
- Quale prospettiva deve adottare?
- Quali competenze deve simulare?

**Esempio:**
> "Sei un esperto di marketing digitale con 15 anni di esperienza in startup tech."

---

## 🎯 T - Task
**Specifica l'obiettivo preciso**

- Cosa deve produrre esattamente?
- Quale problema deve risolvere?
- Usa verbi d'azione chiari (analizza, crea, ottimizza, suggerisci)

**Esempio:**
> "Crea una strategia di content marketing per aumentare l'engagement su LinkedIn."

---

## 📋 C - Contesto (Context)
**Fornisci informazioni di sfondo**

Include:
- Background del progetto/situazione
- Vincoli e limitazioni
- Cosa escludere
- Target audience
- Requisiti specifici

**Esempio:**
> "L'azienda è una B2B SaaS con budget limitato. Target: CTO e decision maker IT. Escludi strategie paid advertising."

---

## 🧠 R - Ragionamento (Reasoning)
**Richiedi pensiero critico**

- Chiedi di mostrare i passaggi logici
- Richiedi validazione delle ipotesi
- Includi controlli di qualità
- Valutazione di pro/contro

**Esempio:**
> "Spiega il ragionamento dietro ogni raccomandazione e identifica potenziali rischi."

---

## 📊 O - Output Format
**Definisci la struttura esatta**

Specifica:
- Formato (lista, tabella, JSON, paragrafi)
- Lunghezza desiderata
- Sezioni richieste
- Stile (formale, tecnico, divulgativo)

**Esempio:**
> "Rispondi in formato markdown con: 1) Executive summary (100 parole), 2) Tre strategie principali (bullet points), 3) Timeline implementazione (tabella)."

---

## 🛑 S - Stop Conditions
**Stabilisci quando l'AI deve fermarsi**

Utile per:
- Task iterativi
- Generazione di contenuti multipli
- Processi con step successivi
- Evitare output eccessivi

**Esempio:**
> "Fermati dopo aver generato 5 alternative. Non procedere con l'implementazione senza conferma."

---

## 🎯 Template Rapido

```
[RUOLO]
Sei un [identità] con esperienza in [dominio].

[TASK]
Il tuo compito è [azione specifica] per [obiettivo].

[CONTESTO]
- Background: [situazione]
- Vincoli: [limitazioni]
- Target: [audience]
- Escludi: [cosa evitare]

[RAGIONAMENTO]
Mostra i passaggi logici e valida le tue proposte.

[OUTPUT]
Formato: [struttura desiderata]
Lunghezza: [specifica]

[STOP]
Fermati quando [condizione di completamento].
```

---

## 💡 Consigli Pratici

### Quando usare tutti i componenti:
- Prompt complessi o professionali
- Task che richiedono precisione
- Progetti con deliverable specifici

### Versione semplificata (TRO):
Per uso quotidiano, combina:
- **Task** + **Ruolo** + **Output**

### Aggiungi Examples:
Il framework migliora con esempi concreti (few-shot learning):
```
Esempio 1: [input] → [output atteso]
Esempio 2: [input] → [output atteso]
```

---

## ✅ Checklist Qualità Prompt

- [ ] Il ruolo è chiaro e specifico?
- [ ] Il task usa verbi d'azione precisi?
- [ ] Ho fornito contesto sufficiente?
- [ ] Ho richiesto ragionamento esplicito?
- [ ] Il formato output è definito?
- [ ] Le stop conditions sono necessarie?

---

## 🚀 Esempio Completo

**Prompt ottimizzato con RTCROS:**

```
RUOLO: Sei un data analyst senior specializzato in e-commerce.

TASK: Analizza i dati di vendita Q4 2024 e identifica 
le 3 opportunità principali per aumentare il revenue.

CONTESTO:
- Azienda: e-commerce fashion, 50k ordini/mese
- Problema: conversion rate in calo del 15%
- Dati disponibili: traffico, cart abandonment, customer segments
- Escludi: analisi competitor (non disponibili)

RAGIONAMENTO: Per ogni opportunità, spiega:
1. Perché è prioritaria
2. ROI stimato
3. Rischi di implementazione

OUTPUT: Documento markdown con:
- Executive summary (150 parole)
- Tabella comparativa delle 3 opportunità
- Raccomandazioni azioni immediate

STOP: Fermati dopo le raccomandazioni. 
Non creare piani implementazione dettagliati.
```

---

## 📚 Tecniche Complementari

### 🔗 Chain of Thought (CoT)
**Ragionamento passo-passo**

Chiedi all'AI di "pensare ad alta voce" mostrando i passaggi intermedi.

**Quando usarlo:**
- Problemi matematici o logici
- Analisi complesse
- Decisioni con più variabili

**Esempio:**
```
"Risolvi questo problema step-by-step, spiegando ogni passaggio:
Se un prodotto costa 80€ con sconto del 25%, e aggiungo IVA 22%, 
qual è il prezzo finale?"
```

**Risultato:** Migliora drasticamente l'accuratezza su task complessi (fino a +40% secondo ricerche).

---

### 📝 Few-Shot Examples
**Apprendimento per esempi**

Fornisci 2-3 esempi di input/output desiderato prima della richiesta vera.

**Quando usarlo:**
- Task creativi con stile specifico
- Formati particolari
- Tono di voce preciso

**Esempio:**
```
Analizza il sentiment di questi messaggi:

Esempio 1:
Input: "Sono stanco di aspettare"
Output: Sentiment negativo (frustrazione) - Score: -0.7

Esempio 2:
Input: "Finalmente è arrivato!"
Output: Sentiment positivo (gioia) - Score: +0.8

Ora analizza: "Non so cosa pensare di questa situazione"
```

**Risultato:** L'AI impara il pattern e formato esatto che desideri.

---

### ✅ Self-Consistency
**Validazione multipla**

Genera la stessa risposta 3-5 volte e scegli quella più frequente/coerente.

**Quando usarlo:**
- Decisioni critiche
- Calcoli importanti
- Task dove l'accuratezza è essenziale

**Esempio:**
```
"Analizza questo investimento e dammi una raccomandazione.
Genera 3 analisi indipendenti e confrontale."
```

**Risultato:** Riduce "allucinazioni" e risposte casuali, aumenta affidabilità.

---

### 🎯 Come Combinarle con RTCROS

**Per massima efficacia:**

1. **Base:** Usa RTCROS per strutturare il prompt
2. **Ragionamento:** Aggiungi CoT nella sezione "Reasoning"
3. **Stile:** Usa Few-Shot nella sezione "Context" o "Output"
4. **Validazione:** Applica Self-Consistency per task critici

**Esempio integrato:**
```
[RUOLO] Sei un analista finanziario esperto.

[TASK] Valuta la sostenibilità di questo investimento.

[CONTEXT + FEW-SHOT]
Esempi di analisi precedenti:
- Caso A: ROI 15%, rischio medio → Raccomandato
- Caso B: ROI 8%, rischio alto → Non raccomandato

[REASONING + COT]
Mostra il ragionamento step-by-step:
1. Analisi cash flow
2. Calcolo ROI
3. Valutazione rischi
4. Conclusione

[OUTPUT] Report in formato markdown

[SELF-CONSISTENCY]
Genera questa analisi 3 volte con approcci diversi 
e confronta le conclusioni.
```