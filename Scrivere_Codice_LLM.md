# Scrivere Codice di Qualità con l'AI

## 1. Stabilisci una Visione Chiara

**Perché**: Ogni decisione non documentata sarà presa dall'AI per te.

**Cosa fare**:
- Pensa e discuti architettura, interfacce, data structures e algoritmi
- Definisci cosa deve essere testato rigorosamente
- Documenta le decisioni difficili da cambiare
- Identifica le parti critiche del codice

**Ricorda**: Sei tu l'esperto del mondo reale, non l'AI.

---

## 2. Mantieni Documentazione Precisa

**Perché**: L'AI ha bisogno di istruzioni dettagliate, altri developer pure.

**Cosa documentare**:
- Requirements e specifications
- Constraints e architettura
- Coding standards e best practices
- Design patterns utilizzati

**Formati utili**:
- Flowcharts e UML diagrams
- Pseudocode per algoritmi complessi
- README e file di documentazione nel repository

---

## 3. Costruisci Debug Systems per l'AI

**Perché**: Riduce comandi CLI costosi e semplifica il debugging.

**Esempio pratico**:
```
Sistema distribuito → Logs centralizzati
Output: "Data inviata a tutti i nodi"
        "Data X salvata su Node 1 ma non su Node 2"
```

**Obiettivo**: Informazioni astratte e immediate, non raw data.

---

## 4. Marca i Livelli di Code Review

**Perché**: Non tutto il codice ha la stessa importanza.

**Sistema di marcatura**:
```javascript
function criticalFunction() {  //A
  // Codice generato da AI, non ancora revisionato
}

function reviewedFunction() {  //H
  // Codice revisionato da umano
}
```

**Livelli suggeriti**:
- `//A` - AI-generated, non revisionato
- `//H` - Human-reviewed
- `//V` - Verified e testato

---

## 5. Scrivi High-Level Specification Tests

**Problema**: Le AI "barano" con mocks, stubs e valori hardcoded.

**Soluzione**:
- Scrivi property-based tests tu stesso
- Rendi difficile barare (es. riavvia il server tra i test)
- Verifica valori reali nel database
- **Separa questi test** - l'AI non deve modificarli

**Istruisci l'AI**: "Non modificare i test in /tests/specifications/"

---

## 6. Scrivi Interface Tests in Contesto Separato

**Strategia**: Due AI separate per implementation e testing.

**Come**:
1. AI #1 scrive il codice con pieno contesto
2. AI #2 scrive interface tests con contesto minimo
3. I test rimangono "ingenui" e non adattati all'implementation

**Protezione**: Separa fisicamente i test e blocca modifiche non autorizzate.

---

## 7. Usa Strict Linting e Formatting

**Perché**: Trova issue prima, mantiene consistency.

**Setup raccomandato**:
- ESLint/Prettier (JavaScript/TypeScript)
- golangci-lint (Go)
- Black/Flake8 (Python)
- Configurazione strict, no eccezioni

**Best practice**: Integra nel CI/CD pipeline.

---

## 8. Usa Context-Specific Coding Agent Prompts

**Strumento principale**: File `CLAUDE.md` path-specific

**Vantaggi**:
- Risparmio tempo e denaro
- Informazioni consistenti per l'AI
- Riduce lookup time
- Sfrutta prompt caching (riduce costi fino all'80%)

**Cosa includere**:
```markdown
# CLAUDE.md

## Coding Standards
- Usa TypeScript strict mode
- Preferisci composition over inheritance
- Maximum function length: 50 righe

## Architettura
- MVC pattern
- Repository pattern per data access

## Best Practices
- Nessun any type
- Sempre error handling

## MCP Servers Disponibili
- Database MCP per query dirette
- File system MCP per operazioni file
```

**Best practices**:
- Versiona i file CLAUDE.md come codice
- Testa modifiche ai prompt su task campione
- Struttura contenuto stabile all'inizio (viene cachato)
- Genera automaticamente da documentazione esistente

**MCP (Model Context Protocol)**:
- Configura MCP servers per estendere capacità dell'AI
- Database access, API calls, file operations
- Riduce codice boilerplate generato

---

## 9. Marca Funzioni ad Alto Security Risk

**Funzioni critiche**:
- Authentication
- Authorization  
- Data handling
- Payment processing
- File system access
- Input validation (protezione da prompt injection)

**Sistema di marcatura**:
```javascript
function authenticateUser() {  //HIGH-RISK-UNREVIEWED
  // Codice critico non ancora revisionato
}

function processPayment() {  //HIGH-RISK-REVIEWED
  // Codice critico revisionato e approvato
}

function sanitizeUserInput() {  //HIGH-RISK-REVIEWED
  // Previene prompt injection quando input utente va nei prompt
}
```

**Regola ferrea**: Ogni modifica = reset a UNREVIEWED.

**Istruisci l'AI**: "Se modifichi funzioni //HIGH-RISK-REVIEWED, cambia il marker a //HIGH-RISK-UNREVIEWED"

**Security specifica per AI**:
- Sanitizza input utente prima di includerlo in prompt all'AI
- Valida output AI prima di eseguirlo
- Non fidarti ciecamente di codice generato per funzioni critiche

---

## 10. Riduci la Complessità del Codice

**Perché**: Ogni riga costa context window, energia, denaro, e probabilità di successo.

**Come ridurre**:
- Elimina codice duplicato
- Preferisci soluzioni semplici
- Rifattorizza componenti complessi
- Usa librerie standard quando possibile
- DRY (Don't Repeat Yourself)

**Mantra**: "Il codice migliore è quello non scritto."

---

## 11. Esplora con Experiments e Prototypes

**Vantaggio**: Il codice AI è economico.

**Strategia**:
1. Crea prototipi multipli con specifiche minime
2. Compara soluzioni diverse
3. Scegli la migliore
4. Scarta il resto senza rimpianti

**Quando usare**:
- Problemi nuovi/non familiari
- Architetture alternative
- Valutazione tecnologie
- Proof of concepts

---

## 12. Non Generare Ciecamente o Troppa Complessità

**Regola d'oro**: Mantieni sempre il controllo.

**Come**:
- **Break down**: Dividi in task piccoli e gestibili
- **Review incrementale**: Controlla ogni componente
- **Test progressivi**: Verifica man mano
- **Stop se perdi controllo**: Torna all'ultimo stato controllato

**Workflow corretto**:
```
Specifica → Genera funzione → Review → Test → 
Specifica → Genera classe → Review → Test →
Specifica → Integra → Review → Test
```

**Workflow sbagliato**:
```
Specifica vaga → "Genera tutto il modulo" → ??? → 
Codice incomprensibile
```

---

## 13. Richiedi Structured Outputs

**Perché**: Garantisce formati consistenti e parsabili.

**Quando usare**:
- Generazione di configurazioni (JSON, YAML, TOML)
- Report automatici con struttura fissa
- Data extraction da codice esistente
- Risposte API-like dall'AI

**Come implementare**:
```markdown
Richiedi output in questo formato JSON:
{
  "functions_added": ["funcName1", "funcName2"],
  "files_modified": ["path/to/file.js"],
  "tests_needed": true,
  "breaking_changes": false,
  "security_review_required": true
}
```

**Vantaggi**:
- Parsing automatico delle risposte AI
- Validazione con JSON Schema
- Pipeline automatizzate
- Riduce ambiguità nelle risposte

**Tool use**:
- Preferisci tool use (function calling) per azioni strutturate
- Codice generato per logica complessa custom
- Tool use per operazioni standard (file I/O, API calls)

---

## 14. Testa e Ottimizza i Tuoi Prompt

**Perché**: I prompt sono codice, vanno testati come tale.

**Cosa testare**:
- Consistenza: stesso input → output simile?
- Completezza: copre tutti i casi d'uso?
- Efficienza: usa token inutili?
- Sicurezza: vulnerabile a prompt injection?

**Come testare**:
```bash
# Crea test suite per prompt
tests/
  prompt-tests/
    test-authentication-prompt.md
    test-database-prompt.md
    expected-outputs/
```

**Metriche da raccogliere**:
- Tasso di successo task
- Token utilizzati per task
- Tempo di esecuzione
- Modifiche umane necessarie post-generazione

**Ottimizzazione**:
- A/B testing di varianti prompt
- Analizza quali istruzioni vengono ignorate
- Rimuovi parti ridondanti
- Documenta prompt efficaci in knowledge base

---

## 15. Implementa Feedback Loops

**Perché**: Migliora continuamente la qualità del codice AI.

**Sistema di feedback**:
```
AI genera → Human review → Annotazione → 
Aggiorna prompt/docs → AI migliora
```

**Cosa tracciare**:
- Errori comuni dell'AI
- Pattern che richiedono sempre correzione
- Istruzioni frequentemente ignorate
- Funzionalità ben implementate al primo tentativo

**Azioni correttive**:
```markdown
# feedback-log.md

## 2026-02-06
**Problema**: AI genera sempre auth senza rate limiting
**Soluzione**: Aggiunto a CLAUDE.md: "Implementa sempre rate limiting per auth endpoints"
**Risultato**: ✅ Risolto

## 2026-02-05  
**Problema**: AI usa any type frequentemente
**Soluzione**: Configurato linter strict + nota in CLAUDE.md
**Risultato**: ⚠️ Ridotto del 70%
```

**Metriche di successo**:
- % codice che passa review al primo tentativo
- Tempo medio review umana
- Bug trovati in produzione da codice AI
- Costi AI per feature delivered

---

## 16. Mantieni Human-in-the-Loop per Decisioni Critiche

**Principio**: L'AI propone, l'umano decide.

**Decisioni che richiedono human approval**:
- Scelta di architetture (microservices vs monolith)
- Selezione di librerie/framework critici
- Trade-off performance vs manutenibilità
- Breaking changes alle API pubbliche
- Modifiche a schema database
- Strategie di caching/scaling

**Workflow consigliato**:
```
Task complesso → AI genera 2-3 alternative →
Spiega pro/contro di ciascuna →
Human sceglie → AI implementa scelta
```

**Esempio**:
```markdown
# Prompt
"Abbiamo bisogno di cache per le user queries. 
Proponi 2-3 soluzioni con pro/contro.
NON implementare, solo proponi."

# Response AI
1. Redis in-memory: veloce ma volatile...
2. PostgreSQL materialized views: persistente ma più lento...
3. Cloudflare Workers KV: distribuito ma eventual consistency...

# Human Decision
"Usa opzione 2, la consistenza è critica"

# AI Implementation
[genera codice basato su scelta umana]
```

**Benefici**:
- Responsabilità chiara
- Expertise umano dove serve
- AI accelera, non decide

---

## Quick Reference: Markers e Commenti

| Marker | Significato | Azione richiesta |
|--------|-------------|------------------|
| `//A` | AI-generated | Richiede review umana |
| `//H` | Human-reviewed | OK per uso |
| `//HIGH-RISK-UNREVIEWED` | Critico non revisionato | Review prioritaria |
| `//HIGH-RISK-REVIEWED` | Critico approvato | Monitorare modifiche |
| `//TODO-AI` | Task per AI | Completare |
| `//NO-AI-EDIT` | Non modificare | Protected code |

---

## Checklist Pre-Deploy

- [ ] Tutti i `//A` marker revisionati?
- [ ] Nessun `//HIGH-RISK-UNREVIEWED` presente?
- [ ] Specification tests passano?
- [ ] Interface tests passano?
- [ ] Linting clean?
- [ ] Documentazione aggiornata?
- [ ] Complessità ridotta dove possibile?
- [ ] Context-specific prompts aggiornati?
- [ ] Structured outputs validati?
- [ ] Prompt testati e ottimizzati?
- [ ] Feedback loops implementati?
- [ ] Decisioni critiche approvate da human?
- [ ] MCP servers configurati correttamente?
- [ ] Input utente sanitizzato nei prompt?

---

## Principi Fondamentali

1. **Tu sei il responsabile** - L'AI è uno strumento, non un decision maker
2. **Documenta tutto** - Ciò che non documenti, l'AI inventerà
3. **Testa rigorosamente** - L'AI proverà a barare, i prompt vanno testati come codice
4. **Mantieni il controllo** - Se perdi la comprensione, ferma e riparti
5. **Itera gradualmente** - Piccoli passi verificati > grandi salti nel buio
6. **Structured over freeform** - Output strutturati sono più affidabili
7. **Feedback continuo** - Impara dagli errori, aggiorna prompt e documentazione
8. **Human per decisioni critiche** - L'AI propone, tu decidi

---