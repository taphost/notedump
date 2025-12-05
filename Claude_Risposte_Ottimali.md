# Guida Pratica: Come Ottenere Risposte Ottimali da Claude

## 🎯 PREMESSA IMPORTANTE

Claude **non ha "modalità" preimpostate**. Il suo comportamento dipende da:
- **Come formuli il prompt**
- **Le tue preferenze utente** (Settings > Profile)
- **Il contesto della conversazione**
- **Strumenti attivi** (Research, web search, ecc.)

---

## 📝 STILI DI RISPOSTA COMUNI

### 1. RISPOSTA CONCISA ✅ OTTIMALE PER CODING

**Come ottenerla:**
- Imposta preferenze utente: "Essere sempre conciso"
- Prompt chiari e diretti
- Specifica "no extra features"

**Caratteristiche:**
- Risposte brevi e mirate
- Esegue solo quanto richiesto
- Zero divagazioni

**Vantaggi:**
- Chirurgico: fa esattamente ciò che chiedi
- Efficiente: zero token sprecati
- Prevedibile: no iniziative autonome

**⭐ Ideale per:**
- Progetti di coding
- Modifiche a codice esistente
- Task operativi specifici

---

### 2. RISPOSTA STANDARD ⚠️ ATTENZIONE NEL CODING

**Quando si verifica:**
- Prompt vaghi o ambigui
- Nessuna preferenza utente impostata
- Richieste aperte

**Rischi:**
- **Feature Creep**: aggiunge funzionalità non richieste
- **Over-explanation**: spiega ogni scelta
- **Over-engineering**: ristruttura codice funzionante

**Esempio problema:**
```
User: "Aggiungi un bottone rosso"

Risposta rischiosa:
"Ho aggiunto il bottone rosso! Ho anche implementato:
- Palette di 5 colori
- Hover effects
- Theme switcher
- Modal impostazioni..."
```

**✅ Utilizzabile per:**
- Discussioni generali
- Brainstorming
- Spiegazioni concettuali

**❌ Evitare per:**
- Modifiche precise a codice esistente

---

### 3. RICERCA APPROFONDITA (Research Feature) 🔍

**Cos'è:**
- **Strumento separato** attivabile dall'interfaccia
- Usa multiple ricerche web
- Genera report dettagliati

**Comportamento:**
- Analisi approfondita multi-fonte
- Report lunghi e strutturati
- Ricerca estensiva di informazioni

**Problemi per il coding:**
- **Analysis Paralysis**: analizza invece di eseguire
- **Scope Explosion**: parte per tangenti
- **Over-research**: cerca best practices non necessarie

**✅ Usare SOLO per:**
- Ricerche di mercato
- Analisi competitive
- Report accademici
- Quando chiedi esplicitamente ricerca approfondita

**❌ MAI per:**
- Task di coding operativo
- Modifiche rapide

---

## 🎓 COME OTTENERE COMPORTAMENTI SPECIFICI

### Per Coding Preciso

**Imposta preferenze utente:**
```
"Essere sempre conciso nelle risposte"
```

**Struttura prompt così:**
```markdown
Task: [descrizione specifica]

Rules:
- Fai SOLO le modifiche richieste
- NO feature extra
- NO miglioramenti non richiesti
- Mantieni funzionalità esistenti
- Chiedi se non chiaro, non assumere

Prima di modificare:
1. Elenca cosa cambierai (max 3 punti)
2. Conferma che nulla verrà rimosso o aggiunto
```

### Per Spiegazioni Dettagliate

**Nel prompt:**
```
"Spiegami in dettaglio come funziona X, 
con esempi e analogie"
```

### Per Ricerca Approfondita

**Usa lo strumento Research** dall'interfaccia, oppure:
```
"Fai una ricerca approfondita su X, 
analizzando multiple fonti"
```

---

## 🚨 RED FLAGS: Claude Sta Aggiungendo Roba Non Richiesta

Quando vedi:
- ❌ "Ho anche aggiunto..."
- ❌ "Ho pensato che potesse essere utile..."
- ❌ "Generalmente gli utenti..."
- ❌ "Per migliorare l'esperienza..."
- ❌ "Ho fatto questa scelta perché..."

**→ Ferma e correggi subito:**
```
STOP
Non voglio extra features
Fai SOLO quello che ho chiesto
```

---

## 📊 QUANDO USARE QUALE APPROCCIO

| Task | Approccio | Come Ottenerlo |
|------|-----------|----------------|
| **Coding/Modifiche** | Conciso | Preferenze utente + prompt chiaro |
| **Spiegazioni** | Dettagliato | "Spiega in dettaglio..." |
| **Ricerca** | Research | Strumento Research |
| **Brainstorming** | Standard | Prompt aperto |
| **Documentazione** | Strutturato | "Crea documentazione per..." |

---

## 💡 CHECKLIST ANTI-DISASTRO

### Prima che Claude scriva codice:
- [ ] Ha letto tutto il file esistente?
- [ ] Ha elencato cosa modificherà?
- [ ] Ha confermato che non rimuove nulla?
- [ ] Ha confermato che non aggiunge feature extra?

### Segnali che sta per fare un casino:
1. Pausa lunga prima di rispondere
2. "Prima di procedere, ho pensato..."
3. Risposta che inizia con teoria/contesto
4. Lista di "considerazioni"
5. "Ho anche preparato..."

---

## 🎯 RACCOMANDAZIONI FINALI

### Setup Ottimale per Coding:
1. **Imposta preferenze utente**: "Essere sempre conciso"
2. **Usa prompt con safeguards chiari**
3. **Specifica sempre cosa NON fare**
4. **Verifica prima che esegua**

### Regola d'Oro:
> **Se Claude spiega perché ha fatto qualcosa che non hai chiesto,  
> ha già fatto un casino.**

---

## 📝 TEMPLATE PROMPT UNIVERSALE

```markdown
Task: [descrizione precisa]

Constraints:
- Fai SOLO quanto richiesto sopra
- NO feature, preset o miglioramenti extra
- NO rimozioni di funzionalità esistenti
- Mantieni TUTTI gli elementi UI originali

Before coding:
- Elenca modifiche (max 3 punti)
- Conferma: nulla rimosso, nulla aggiunto

After coding:
- Solo link download
- Massimo 1 riga di summary
```

---

**TL;DR**: Claude non ha "modalità". Il comportamento dipende da come lo usi. Per coding preciso: imposta preferenze concise + prompt chiari con vincoli espliciti.