# 📌 LLM Token-Handling
### Per file “difficili” (Excel, CSV, XML, JSON, ZIP, ecc.)

---

## 🔥 Perché le LLM falliscono con file complessi
- Le LLM manipolano **token**, non caratteri → struttura fragile.  
- I file complessi richiedono **forma esatta** → una virgola fuori posto rompe tutto.  
- Le LLM possono introdurre:
  - spazi invisibili  
  - newline extra  
  - encoding errato  
  - UTF‑8 ambiguo  
  - delimitatori variabili  

---

## 🧨 Formati più problematici
### 🟩 **CSV**
- Rischi: colonne sfasate, delimitatori cambiati, spazi invisibili.  
- Evitare: generare CSV lunghi > 2000 righe.  
- Soluzione: far generare **JSON** → convertire a CSV via script.

---

### 📊 **XLS / XLSX**
- Formato ZIP + XML → impossibile da ricostruire a mano.  
- LLM non può preservare CRC, struttura interna, relazioni.  
- Usare strumenti (python, ExcelWriter).  

---

### 🔧 **XML**
- Spesso ben formato, ma:
  - tag aperti/chiusi male  
  - spazi o newline invalidi  
  - attributi confusi  
- Meglio: far lavorare la LLM a livello di **struttura**, non produzione finale.

---

### 🟦 **JSON**
- Rischi minori, ma:
  - virgole finali  
  - escape sbagliati  
  - array inconsistenti  
- Deve essere sempre validato via parser.

---

### 📚 **YAML**
- Delicatissimo:
  - indentazione critica  
  - tab vs spazi  
  - caratteri speciali  
- Alto rischio di rottura → meglio evitarlo nei prompt.

---

### 📁 **ZIP / BIN / PDF**
- Qualsiasi file binario = **non gestibile direttamente**.  
- Output corrotto al 100%.  
- Va sempre generato via strumento.

---

### 💻 **Codice con allineamento**
(es. ASCII art, tabelle, colonne)
- Tokenizzazione = allineamento rotto.  
- Meglio usare blocchi fissi, ma non affidarsi troppo.

---

## ✔️ Strategie consigliate
- 🟩 **Generare JSON, non CSV**  
- 🟦 Convertire SEMPRE via script ufficiali  
- 🧪 Validare ogni output (jsonlint, xmllint, ecc.)  
- 🧱 Per codice o tabelle: usare blocchi ``` monospaced  
- 🛠️ Per file complessi → usare python_user_visible

---

## 🚀 Mini-Workflow Sicuro
1. Chiedi alla LLM dati grezzi → **JSON**  
2. Converti via script a CSV/XLSX/XML  
3. Scarica il file generato  
4. Controlla con validator

---
