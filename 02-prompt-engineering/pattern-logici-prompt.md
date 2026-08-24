Pattern Logici per Prompt Efficaci

## 1. Tecnica del "Ruolo Cognitivo"

**Problema**: Definire solo il "chi" (es. "agisci come senior analyst") non basta.

**Soluzione**: Definire anche il "come" - lo schema di pensiero.

**Esempio**:
- ❌ Male: "Agisci come senior marketing analyst e parlami del trend X"
- ✅ Meglio: "Agisci come senior marketing analyst. Prioritizza evidenze basate sui dati rispetto al sentiment generale. Ragiona come uno scettico che cerca ROI e fattori di rischio prima delle opportunità"

**Perché funziona**: Forza il modello ad adottare un'architettura cognitiva specifica, riducendo consigli generici.

## 2. Framework del "Lens Shifting"

**Problema**: L'AI tende a validare le proprie risposte precedenti.

**Workflow**:
1. **Generate**: "Crea soluzione X..."
2. **Shift lens**: "Ora ignora la risposta precedente. Analizza questo strettamente dalla prospettiva di un [Hostile User / Security Engineer / Frugal CFO]. Dove fallisce?"
3. **Integrate**: "Integra queste tensioni in una versione finale robusta"

**Perché funziona**: Bypassa l'allineamento del modello dandogli un ruolo dove essere critico è il comportamento corretto.

## 3. Constraint Negativi (Anti-Prompt)

**Principio**: Dire cosa NON fare è spesso più potente che dire cosa fare.

**Template da aggiungere ai prompt**:
```
Constraints:
• No marketing fluff o corporate jargon
• Non assumere risorse che non sono elencate
• Se la risposta è incerta, indica esplicitamente il livello di confidenza
```

## 4. Architettura "Chain of Thought"

**Per task complessi**: Non chiedere solo la risposta, chiedi il processo.

**Template**:
```
Prima di fornire la risposta finale, delinea il ragionamento step-by-step:
1. Definisci il contesto del problema
2. Analizza lo state of the art
3. Valuta 3 alternative distinte
4. Concludi con una raccomandazione
```

## 5. Usa Modelli Specializzati

**Non usare un solo modello per tutto**. Trattali come un team specializzato:

- **Perplexity**: Research assistant - raccolta fatti
- **Gemini**: Creative explorer - pensiero laterale e connessioni tra concetti
- **Claude**: The architect - struttura logica
- **ChatGPT**: The executor - sintesi finale

---

## TL;DR

1. Definisci **come** deve pensare, non solo **chi** è
2. Forza diversi "lens" per rompere i bias di conferma
3. Usa **constraint negativi**
4. Chiedi il **processo**, non solo la risposta
5. **Specializza i modelli** per task diversi
