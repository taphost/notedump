# Guida al Context nelle LLM

## 1. Cos'è il Context

Il **context** (o context window) è la "memoria di lavoro" di un LLM: la quantità massima di informazioni elaborabili in una conversazione.

## 2. Token: L'unità di misura

I **token** sono le unità base con cui vengono misurati i testi nelle LLM:

- Un token ≈ 4 caratteri in inglese
- Un token ≈ 0.75 parole in inglese  
- In italiano servono più token (circa 1 parola = 1.3-1.5 token)
- Esempi: "ciao" = 1 token, "intelligenza" = 3-4 token

Il context viene sempre espresso in token (es. 200K token, 1M token).

## 3. Componenti del Context

### Input Context
Tutto ciò che viene inviato: prompt utente, conversazione precedente, file allegati, system prompt.

### Output Context  
Ciò che il modello genera come risposta.

### Context Size (Context Window)
Il limite massimo totale: **input + output**. Esempi:
- Claude Opus 4.5: ~200K token
- Claude Sonnet 4.5: ~200K token
- Claude Haiku 4.5: ~200K token
- GPT-4 Turbo: ~128K token
- GPT-4o: ~128K token

## 4. Architettura e Meccanismi

### Attention Mechanism
- Permette al modello di focalizzarsi su parti rilevanti del context
- Ogni token "guarda" tutti gli altri token
- Complessità quadratica: bottleneck principale per context lunghi

### KV Cache (Key-Value Cache)
- Memoria intermedia che salva calcoli dell'attention
- Evita di ricalcolare tutto il context ad ogni nuovo token
- Occupa RAM/VRAM proporzionalmente alla lunghezza del context
- Limite fisico hardware per context molto lunghi

### RoPE (Rotary Position Embedding)
- Tecnica che permette al modello di capire la posizione delle parole nel testo
- Codifica la posizione relativa dei token
- Limita l'estensione massima del context
- Alternative: ALiBi, altre tecniche di position encoding

### Self-attention vs Cross-attention
- **Self-attention:** token guardano altri token nello stesso context
- **Cross-attention:** usato per integrare informazioni esterne

## 5. Problemi e Limitazioni

### Context Overflow
Quando si supera il limite, i messaggi più vecchi vengono rimossi automaticamente.

### Context Degradation
Performance peggiorano con context molto lunghi. Degrado visibile oltre ~80K token (modelli 100-200K) o ~500-700K token (modelli 1M). Varia tra modelli.

**"Lost in the Middle" (Attention Decay):**
- Il modello ricorda meglio inizio/fine, "dimentica" il centro
- Info lontane vengono progressivamente dimenticate (privilegia recenti)
- Più lungo il context, più marcato l'effetto
- **Soluzione:** posizionare info critiche all'inizio o alla fine

**Sintomi tipici:**
- Contraddizioni con informazioni precedenti
- Mancata citazione di dettagli forniti a metà conversazione
- Risposte generiche invece che specifiche
- Rallentamento nella generazione delle risposte

**Differenze tra modelli:**
- Claude Opus: gestisce meglio context lunghi (~200K)
- GPT-4 Turbo: degrado più marcato oltre 100K
- Modelli più recenti hanno miglioramenti significativi

### Context Rot
Deterioramento qualitativo del context (non tecnico): accumulo di info obsolete, contraddittorie o irrilevanti. Il context si "inquina" in conversazioni lunghe.

**Cause:**
- Conversazioni che cambiano topic ripetutamente
- Correzioni e modifiche che contraddicono messaggi precedenti
- Informazioni temporanee che restano nel context
- Tentativi falliti che "sporcano" la conversazione

**Sintomi:**
- Il modello fa riferimento a info superate
- Confusione tra versioni diverse delle stesse informazioni
- Risposte che mescolano context vecchio e nuovo
- Necessità di ripetere informazioni già fornite

**Soluzione:**
- Reset della conversazione (nuovo chat)
- Riassunto esplicito dello stato attuale
- Pulizia manuale del context (rimuovere messaggi obsoleti)
- Utilizzare system prompt aggiornati

## 6. Tecniche Avanzate di Gestione Context

### Prompt Caching
Riutilizzo di parti del context già elaborate. Parti statiche vengono salvate in cache, richieste successive le riusano.

**Vantaggi:**
- Risparmio fino al 90% sui token di input ripetuti
- Risposte più veloci
- Ideale per system prompt lunghi o documenti di riferimento

**Quando usarlo:**
- System prompt complessi (>1K token)
- Documenti di riferimento costanti
- Conversazioni con stesso contesto base

### RAG (Retrieval Augmented Generation)
Database esterno con recupero dinamico: solo le parti necessarie vengono inserite nel context.

**Vantaggi:**
- Accesso a quantità illimitate di dati
- Context sempre ottimizzato
- Informazioni sempre aggiornabili

**Use case:**
- Knowledge base aziendali
- Documentazione tecnica estesa
- Archivi storici di conversazioni

### Streaming
Output generato token per token, visibile in tempo reale. Non influisce sul context limit totale.

**Vantaggi:**
- Esperienza utente migliore (no attesa)
- Possibilità di interrompere generazioni lunghe
- Risparmio di tempo percepito

### Multi-turn vs Single-turn

**Multi-turn (conversazionale):**
- Context accumula tutta la conversazione
- Ogni messaggio consuma token permanentemente
- Limite raggiunto = messaggi vecchi eliminati

**Single-turn (stateless):**
- Ogni richiesta è indipendente
- Context reset ad ogni query
- Più efficiente per task isolati

### Chunking
- Divisione di testi lunghi in blocchi gestibili
- Utile quando documento > context window
- Tecniche: per paragrafo, per dimensione, semantico

### Context Compression
- Tecniche per ridurre uso di token mantenendo informazioni
- Riassunti, estrazione concetti chiave, eliminazione ridondanze

### Sliding Window
- Finestra mobile che mantiene solo parte recente del context
- Utile per conversazioni molto lunghe
- Sacrifica storia antica per mantenere performance

## 7. Parametri di Generazione

### Temperature
- Controlla casualità/creatività delle risposte
- Range: 0.0 (deterministico) a 2.0 (molto casuale)
- NON influenza direttamente il context window
- Influenza la **varietà** dell'output generato (non la lunghezza)

### Max Tokens (Output)
- Limite massimo di token che il modello può generare
- Diverso dal context window totale
- Esempio: context 200K, max output impostabile a 4K

### Top-p (Nucleus Sampling)
- Alternativa a temperature per controllare casualità
- Considera solo i token più probabili che sommano a p%

### Stop Sequences
- Sequenze che terminano la generazione
- Es: "###", "[END]", newline doppio
- Utile per controllare lunghezza output

## 8. Formati File Preferibili

### Markdown (.md)
Leggero, strutturato, minimo overhead, facilmente parsabile.

### JSON (.json)
Struttura dati definita, perfetto per dati strutturati, minimo overhead.

### TXT (.txt)
Massima semplicità, zero overhead, ideale per testo puro.

### YAML (.yaml) / TOML (.toml)
Configurazioni leggibili, struttura gerarchica, alternativa più leggibile a JSON.

### TOON (.toon) - Token-Oriented Object Notation
30-60% risparmio token vs JSON. Ottimizzato per array uniformi e dati tabulari. Usa per dataset ripetitivi, tabelle, liste di oggetti con stessi campi.

**Esempio comparativo:**
```json
// JSON: ~50 token
[{"name":"Alice","age":30},{"name":"Bob","age":25}]

// TOON: ~30 token
[name,age|Alice,30|Bob,25]
```

### TONL (.tonl) - Token-Optimized Notation Language
32-60% risparmio token vs JSON. Piattaforma completa con query, CRUD, indicizzazione, TypeScript types, validazione schema. Usa per manipolazione dati, progetti TypeScript/JavaScript.

**Differenza TOON vs TONL:**
- **TOON:** serializzazione semplice, più maturo. Usa per salvare/caricare dati, massima semplicità.
- **TONL:** piattaforma completa con query/CRUD. Usa se servono validazione schema, query complesse, integrazione TypeScript.

## 9. Formati Sconsigliati

### PDF
Parsing complesso, metadata pesanti, formattazione inutile per LLM, spreco token.

### CSV
Ambiguità delimitatori, problemi con virgole nel testo. JSON/TOON sono più robusti (TOON 60% più efficiente).

### DOCX
Formato binario, metadata pesanti, parsing specifico, overhead elevato.

## 10. Best Practices

1. **Usa Markdown** per documentazione e testo strutturato
2. **Usa JSON** per dati strutturati e configurazioni generiche
3. **Usa TOON/TONL** per dati tabulari ripetitivi (massimo risparmio token)
4. **Comprimi le informazioni**: elimina ridondanze
5. **Riassumi conversazioni lunghe** invece di includerle interamente
6. **Prioritizza** le informazioni rilevanti per la richiesta corrente
7. **Evita file binari** quando possibile
8. **Usa prompt caching** per context ripetitivi
9. **Considera RAG** per knowledge base estese
10. **Monitora lunghezza** del context nelle conversazioni lunghe

## 11. Glossario Tecnico

- **Prompt engineering:** ottimizzazione del testo input per risultati migliori
- **Token limit:** limite massimo di token processabili (input + output)
- **Context window:** sinonimo di context size, finestra totale disponibile
- **Embedding:** rappresentazione numerica dei token
- **Inference:** processo di generazione della risposta
- **Latency:** tempo di attesa per la risposta
- **Throughput:** quantità di token processati al secondo

## 12. Esempio Pratico

**Context disponibile:** 200K token

**Breakdown tipico:**
- System prompt: ~5K token
- Conversazione precedente: ~30K token  
- File allegato (.md): ~10K token
- Prompt utente corrente: ~1K token
- **Totale input:** ~46K token
- **Spazio per output:** ~154K token

**Confronto formati (stesso contenuto):**
- PDF: ~40K token
- JSON: ~15K token
- Markdown: ~10K token
- TOON: ~6K token (dati tabulari)
- **Risparmio massimo:** 34K token (85% in meno con TOON vs PDF)

**Esempio concreto - lista di 100 utenti:**
- JSON: ~5,000 token
- TOON: ~2,000 token  
- **Risparmio:** 3,000 token (60%)

Se alleghi un PDF di 50 pagine invece di un MD equivalente, potresti consumare 40K token invece di 10K, riducendo drasticamente lo spazio disponibile per la risposta.
