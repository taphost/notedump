# Step-Back Prompting Rapido

## Cos'è

Una tecnica di prompting che forza il Large Language Model a fare astrazione **prima** di risolvere il problema specifico. Invece di affrontare direttamente la domanda, il modello identifica i principi generali e i concetti di alto livello, poi li usa come "ancora" per il ragionamento.

## Il Problema che Risolve

Quando affronti domande complesse, gli LLM tendono a:
- Cadere nella "tunnel vision" (visione a tunnel)
- Fare pattern matching superficiale
- Perdere il contesto architetturale
- Generare ragionamenti incoerenti

## Come Funziona

### Versione in 2 Step (originale)

**Step 1 - Astrazione:**
```
Ecco il mio problema: [Il server crasha sotto carico elevato]

NON risolverlo ancora. 

Prima, spiega i principi generali e i first principles di:
- Load balancing
- Memory management nei server
- Gestione delle connessioni concorrenti

in un contesto generico.
```

**Step 2 - Risoluzione:**
```
Ora, usa quei principi generali come "ground truth" 
e analizza i miei log specifici per trovare la causa.
```

### Versione Rapida (1 prompt unificato)

```
Per risolvere questo problema, prima:

1. Quali sono i principi generali e i first principles di [argomento]?
2. Applica questi principi al mio caso specifico: [problema]

Problema: [descrizione dettagliata]
```

## Esempio Pratico

**Domanda diretta (sbagliata):**
```
"Perché questo codice causa un memory leak?"
→ Il modello guarda le singole righe, pattern matching
```

**Step-Back (corretta):**
```
"Prima di analizzare il codice:
1. Quali sono le cause comuni di memory leak in Python?
2. Quali pattern di gestione memoria andrebbero controllati?

Ora analizza questo codice usando quei principi: [codice]"
```

## Quando Usarlo

✅ **Sì:**
- Debugging complessi
- Problemi multi-layer (infrastruttura + codice)
- Task STEM (fisica, chimica, matematica)
- Ragionamento multi-hop
- Domande che richiedono first principles

❌ **No:**
- Problemi semplici (overkill)
- Domande di cultura generale ("Chi era presidente USA nel 2000?")
- Quando la domanda è già astratta ("Cos'è la velocità della luce?")

## Risultati dal Paper

- **MMLU Physics:** +7% accuracy
- **MMLU Chemistry:** +11% accuracy  
- **TimeQA:** +27% accuracy
- **MuSiQue:** +7% accuracy
- **Superiore a Chain-of-Thought** nelle task complesse

## Template Pronto all'Uso

```
# Per debugging tecnico
Contesto: [problema specifico]

Step 1 - Astrazione:
Quali sono i principi fondamentali di [tecnologia/dominio]?
Quali pattern comuni causano errori simili?

Step 2 - Applicazione:
Dato il contesto sopra, analizza questo caso specifico usando 
i principi identificati come framework di ragionamento.

[Dettagli tecnici, log, codice]
```

## Perché Funziona

1. **Carica il contesto corretto:** Forza il modello ad attivare le rappresentazioni corrette nello spazio latente
2. **Evita pattern matching superficiale:** Richiede comprensione dei principi, non riconoscimento di pattern
3. **Crea framework coerente:** L'astrazione diventa "guard rail" per il ragionamento successivo
4. **Riduce allucinazioni:** I principi recuperati fungono da "knowledge anchor"

## Limiti

- Aggiunge token (quindi costo/tempo)
- Richiede che il modello conosca già i principi generali
- Non sempre necessario per task semplici

## Combinazione con RAG

Step-Back Prompting si combina bene con Retrieval-Augmented Generation:
- Step-Back + RAG riduce gli errori del 21.6% rispetto a RAG solo
- Introduce solo il 6.3% di nuovi errori

---

**Riferimento:** Zheng, H. S., Mishra, S., Chen, X., Cheng, H.-T., Chi, E. H., Le, Q. V., & Zhou, D. (2023). "Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models". Google DeepMind.