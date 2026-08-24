# Cheatsheet Completo Errori di Programmazione

## 1. Syntax Errors
**Quando**: Compile-time  
**Rilevamento**: Compiler/Interpreter  
**Esempi**:
- Punto e virgola, parentesi mancanti
- Parole chiave scritte male (`whle` invece di `while`)
- Operatori o espressioni non validi
- Indentazione errata (Python)

## 2. Semantic Errors
**Quando**: Compile-time/Runtime  
**Rilevamento**: Compiler (a volte), Testing logico  
**Esempi**:
- Uso di tipo variabile sbagliato
- Uso operatore errato (`=` invece di `==`)
- Incompatibilità di tipo
- Violazioni di scope

## 3. Logical Errors
**Quando**: Runtime  
**Rilevamento**: Testing, Debugging  
**Esempi**:
- Implementazione algoritmo errata
- Condizioni sbagliate (`<` invece di `<=`)
- Errori off-by-one
- Formula o calcolo sbagliato
- Loop infiniti

## 4. Runtime Errors
**Quando**: Durante l'esecuzione  
**Rilevamento**: Ambiente runtime  
**Esempi**:
- Divisione per zero
- Null pointer dereference
- Array index out of bounds
- Stack overflow
- File non trovato
- Network timeout
- Input non valido

## 5. Compilation Errors
**Quando**: Compile-time  
**Rilevamento**: Compiler  
**Esempi**:
- Variabili non dichiarate
- Funzione non definita
- Return statement mancante
- Tipi incompatibili
- Dichiarazioni duplicate

## 6. Linker Errors
**Quando**: Link-time  
**Rilevamento**: Linker  
**Esempi**:
- Riferimenti non definiti
- Librerie mancanti
- Definizioni multiple
- File oggetto incompatibili

## 7. Memory Errors
**Quando**: Runtime  
**Rilevamento**: Debugger, Sanitizer  
**Esempi**:
- Memory leak
- Buffer overflow/underflow
- Dangling pointer
- Double free
- Use after free
- Heap corruption
- Stack overflow

## 8. Concurrency Errors
**Quando**: Runtime  
**Rilevamento**: Testing, Race detector  
**Esempi**:
- Race condition
- Deadlock
- Livelock
- Thread starvation
- Priority inversion
- Operazioni non atomiche

## 9. Interface Errors
**Quando**: Runtime  
**Rilevamento**: Testing  
**Esempi**:
- Uso API errato
- Numero parametri sbagliato
- Tipo parametro non corrispondente
- Valori di ritorno non validi
- Violazioni di protocollo

## 10. Resource Errors
**Quando**: Runtime  
**Rilevamento**: Ambiente runtime  
**Esempi**:
- Esaurimento file descriptor
- Out of memory (OOM)
- Spazio disco esaurito
- Connection pool esaurito
- Troppi file aperti

## 11. I/O Errors
**Quando**: Runtime  
**Rilevamento**: Exception handling  
**Esempi**:
- Fallimento read/write
- Permission denied
- Broken pipe
- Connection reset
- Errori timeout
- Errori encoding/decoding

## 12. Arithmetic Errors
**Quando**: Runtime  
**Rilevamento**: Controlli runtime  
**Esempi**:
- Integer overflow/underflow
- Perdita precisione floating-point
- Divisione per zero
- Errori di dominio (sqrt di negativo)
- Propagazione NaN

## 13. Type Errors
**Quando**: Compile-time/Runtime  
**Rilevamento**: Type checker/Runtime  
**Esempi**:
- Type mismatch
- Cast non valido
- Annotazioni tipo mancanti
- Errori generic type
- Fallimenti coercion

## 14. Configuration Errors
**Quando**: Inizializzazione/Runtime  
**Rilevamento**: Controlli startup  
**Esempi**:
- File di configurazione mancanti
- Valori configurazione non validi
- Variabile ambiente non impostata
- Versioni incompatibili
- Percorsi errati

## 15. Security Errors
**Quando**: Runtime  
**Rilevamento**: Audit di sicurezza  
**Esempi**:
- SQL injection
- Cross-site scripting (XSS)
- Exploit buffer overflow
- Bypass autenticazione
- Fallimenti autorizzazione
- Deserializzazione insicura

## 16. Integration Errors
**Quando**: Runtime  
**Rilevamento**: Integration testing  
**Esempi**:
- Versione API non corrispondente
- Incompatibilità formato dati
- Errori di protocollo
- Servizio non disponibile
- Timeout su chiamate esterne

## 17. Database Errors
**Quando**: Runtime  
**Rilevamento**: Database driver  
**Esempi**:
- Fallimenti connessione
- Errori sintassi query
- Violazioni constraint
- Deadlock transazioni
- Corruzione dati
- Schema non corrispondente

## 18. Assertion Errors
**Quando**: Runtime  
**Rilevamento**: Controlli assertion  
**Esempi**:
- Violazioni precondizioni
- Fallimenti postcondizioni
- Violazioni invarianti
- Violazioni contratto

## 19. Exception Handling Errors
**Quando**: Runtime  
**Rilevamento**: Code review, Testing  
**Esempi**:
- Eccezioni non catturate
- Tipo eccezione sbagliato catturato
- Blocchi catch vuoti
- Inghiottimento eccezioni
- Perdite risorse nelle eccezioni

## 20. Performance Errors
**Quando**: Runtime  
**Rilevamento**: Profiling, Monitoring  
**Esempi**:
- Bloat memoria
- CPU thrashing
- Problema N+1 query
- Algoritmi inefficienti
- Allocazioni eccessive
- Cache miss

## 21. Encoding/Character Errors
**Quando**: Runtime  
**Rilevamento**: Testing, Validation  
**Esempi**:
- Mismatch UTF-8/ASCII
- Errori character encoding
- Problemi Byte Order Mark (BOM)
- Problemi normalizzazione Unicode
- Mojibake (testo corrotto)

## 22. Serialization/Deserialization Errors
**Quando**: Runtime  
**Rilevamento**: Testing, Validazione schema  
**Esempi**:
- Errori parsing JSON
- Dati XML malformati
- Mismatch versione Protobuf
- Problemi sicurezza Pickle
- Errori anchor YAML

## 23. Validation Errors
**Quando**: Runtime  
**Rilevamento**: Validazione input  
**Esempi**:
- Formato email non valido
- Valori fuori range
- Campi obbligatori mancanti
- Mismatch pattern (regex)
- Violazioni regole business

## 24. State Errors
**Quando**: Runtime  
**Rilevamento**: Testing, State machine  
**Esempi**:
- Transizioni stato non valide
- Operazione in stato sbagliato
- Stato non inizializzato
- Stato obsoleto
- Problemi sincronizzazione stato

## 25. Boundary Errors
**Quando**: Runtime  
**Rilevamento**: Testing casi limite  
**Esempi**:
- Errori off-by-one
- Errori fencepost
- Violazioni boundary min/max
- Gestione collection vuote
- Casi limite zero/null

## 26. Compatibility Errors
**Quando**: Compile-time/Runtime  
**Rilevamento**: Testing compatibilità  
**Esempi**:
- Incompatibilità versione OS
- Problemi compatibilità browser
- Conflitti versione librerie
- Deprecazione API
- Bug specifici piattaforma

## 27. Initialization Errors
**Quando**: Startup/Runtime  
**Rilevamento**: Controlli inizializzazione  
**Esempi**:
- Variabili non inizializzate
- Ordine inizializzazione sbagliato
- Dipendenze circolari
- Chiamate costruttore mancanti
- Static initialization fiasco

## 28. Networking Errors
**Quando**: Runtime  
**Rilevamento**: Monitoring rete  
**Esempi**:
- Fallimento risoluzione DNS
- Errori handshake SSL/TLS
- Porta già in uso
- Blocco firewall
- Perdita pacchetti
- Partizione rete

## 29. Systematic Errors (Bias)
**Quando**: Design/Runtime  
**Rilevamento**: Analisi statistica  
**Esempi**:
- Bias misurazione consistente
- Accumulo errori arrotondamento
- Errori sistematici campionamento
- Bias algoritmo
- Perdita precisione nei calcoli

## 30. Build/Deployment Errors
**Quando**: Build-time/Deploy-time  
**Rilevamento**: Pipeline CI/CD  
**Esempi**:
- Dipendenze mancanti
- Errori script build
- Mismatch versioni
- Problemi variabili ambiente
- Errori immagine container
- Fallimenti rollback deployment

## Strumenti Rilevamento Errori

| Tipo Errore | Strumenti |
|------------|-------|
| Syntax | Linter, IDE, Compiler |
| Memory | Valgrind, AddressSanitizer, MemorySanitizer |
| Concurrency | ThreadSanitizer, Helgrind |
| Logic | Unit test, Debugger |
| Security | Static analyzer, Penetration testing |
| Performance | Profiler, Tool APM |

## Best Practice Prevenzione

1. **Code Review** - Individua errori logici e di design
2. **Unit Testing** - Verifica comportamento corretto
3. **Static Analysis** - Trova bug potenziali in anticipo
4. **Type System** - Previene errori correlati ai tipi
5. **Assertion** - Valida assunzioni
6. **Error Handling** - Gestione fallimenti con eleganza
7. **Documentation** - Contratti API chiari
8. **Continuous Integration** - Testing automatizzato