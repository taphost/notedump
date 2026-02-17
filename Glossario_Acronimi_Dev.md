# Glossario Acronimi Dev

## 📋 Operazioni Base

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **CRUD** | Create, Read, Update, Delete | Creare, Leggere, Aggiornare, Eliminare | Operazioni base per gestire dati persistenti |
| **BREAD** | Browse, Read, Edit, Add, Delete | Sfogliare, Leggere, Modificare, Aggiungere, Eliminare | Variante di CRUD con Browse al posto di Create |
| **CRUDL** | Create, Read, Update, Delete, List | Creare, Leggere, Aggiornare, Eliminare, Elencare | CRUD con operazione di listing |


## 📐 Metodologie e Principi

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **SOLID** | Single responsibility, Open-closed, Liskov substitution, Interface segregation, Dependency inversion | Responsabilità singola, Aperto-chiuso, Sostituzione Liskov, Segregazione interfacce, Inversione dipendenze | 5 principi OOP fondamentali |
| **DRY** | Don't Repeat Yourself | Non Ripeterti | Evitare duplicazione codice |
| **KISS** | Keep It Simple, Stupid | Mantienilo Semplice, Stupido | Preferire soluzioni semplici |
| **YAGNI** | You Aren't Gonna Need It | Non Ne Avrai Bisogno | Non implementare funzionalità non necessarie |
| **WET** | Write Everything Twice | Scrivi Tutto Due Volte | Anti-pattern opposto di DRY |
| **GRASP** | General Responsibility Assignment Software Patterns | Pattern Generali Assegnazione Responsabilità Software | Linee guida per assegnare responsabilità |
| **POLA** | Principle of Least Astonishment | Principio Minima Sorpresa | Design intuitivo e prevedibile |
| **IoC** | Inversion of Control | Inversione di Controllo | Trasferire controllo a framework |
| **DI** | Dependency Injection | Iniezione di Dipendenze | Tecnica per implementare IoC |
| **AOP** | Aspect-Oriented Programming | Programmazione Orientata agli Aspetti | Modularizzare cross-cutting concerns |
| **JIT** | Just-In-Time | Appena in Tempo | Compilazione runtime del codice |
| **SDD** | Specification-Driven Development | Sviluppo Guidato dalle Specifiche | Sviluppo basato su specifiche formali |
| **XP** | Extreme Programming | Programmazione Estrema | Metodologia Agile con pratiche ingegneristiche |
| **DDD** | Domain-Driven Design | Design Guidato dal Dominio | Approccio design focalizzato sul dominio |
| **FDD** | Feature-Driven Development | Sviluppo Guidato dalle Funzionalità | Metodologia iterativa basata su feature |
| **RDD** | Readme-Driven Development | Sviluppo Guidato dal Readme | Scrivere documentazione prima del codice |
| **CDD** | Component-Driven Development | Sviluppo Guidato dai Componenti | Sviluppo bottom-up da componenti |
| **OOP** | Object-Oriented Programming | Programmazione Orientata agli Oggetti | Paradigma basato su oggetti e classi |
| **FP** | Functional Programming | Programmazione Funzionale | Paradigma basato su funzioni pure |
| **POP** | Protocol-Oriented Programming | Programmazione Orientata ai Protocolli | Paradigma basato su protocolli/interfacce |
| **EDP** | Event-Driven Programming | Programmazione Guidata da Eventi | Paradigma basato su gestione eventi |
| **PP** | Pair Programming | Programmazione a Coppie | Due sviluppatori su stesso codice |
| **Mob Programming** | Mob Programming | Programmazione di Gruppo | Team intero su stesso codice |
| **RAD** | Rapid Application Development | Sviluppo Rapido Applicazioni | Metodologia sviluppo veloce iterativo |


## 📚 Concetti & Terminologia Fondamentale

| Termine | Traduzione | Spiegazione |
|---------|------------|-------------|
| **Asynchronous** | Asincrono | Esecuzione non bloccante, operazioni parallele |
| **Synchronous** | Sincrono | Esecuzione sequenziale bloccante |
| **Race Condition** | Condizione di Gara | Comportamento imprevedibile per accesso concorrente |
| **Deadlock** | Stallo | Blocco reciproco tra processi in attesa |
| **Thread** | Thread/Filo Esecuzione | Unità esecuzione indipendente in processo |
| **Mutex** | Mutual Exclusion | Meccanismo esclusione mutua per risorse |
| **Semaphore** | Semaforo | Variabile controllo accesso concorrente |
| **Blocking** | Bloccante | Operazione che attende completamento |
| **Non-blocking** | Non Bloccante | Operazione che ritorna immediatamente |
| **Callback** | Richiamata | Funzione passata come argomento |
| **Promise** | Promessa | Oggetto rappresenta operazione asincrona futura |
| **Async/Await** | Async/Await | Sintassi gestione codice asincrono |
| **Concurrency** | Concorrenza | Gestione multipli task sovrapposti |
| **Parallelism** | Parallelismo | Esecuzione simultanea su più core |
| **Lock** | Blocco | Meccanismo sincronizzazione accesso risorsa |
| **Atomic Operation** | Operazione Atomica | Operazione indivisibile non interrompibile |
| **Critical Section** | Sezione Critica | Codice con accesso risorsa condivisa |
| **Starvation** | Inedia | Processo mai ottiene risorse necessarie |
| **Livelock** | Stallo Attivo | Processi cambiano stato senza progredire |
| **Modularity** | Modularità | Suddivisione sistema in componenti indipendenti |
| **Coupling** | Accoppiamento | Grado dipendenza tra moduli |
| **Cohesion** | Coesione | Grado relazione interna modulo |
| **Abstraction** | Astrazione | Nascondere complessità mostrando essenziale |
| **Encapsulation** | Incapsulamento | Nascondere implementazione interna |
| **Inheritance** | Ereditarietà | Classe eredita proprietà da altra |
| **Polymorphism** | Polimorfismo | Oggetti diversi rispondono stessa interfaccia |
| **Composition** | Composizione | Costruire oggetti complessi da semplici |
| **Clean Code** | Codice Pulito | Codice leggibile, manutenibile, comprensibile |
| **Code Smell** | Cattivo Odore Codice | Indicatore potenziali problemi design |
| **Technical Debt** | Debito Tecnico | Costo futuro scelte subottimali |
| **Refactoring** | Ristrutturazione | Migliorare struttura senza cambiare comportamento |
| **Idempotent** | Idempotente | Operazione con stesso risultato ripetuta |
| **Side Effect** | Effetto Collaterale | Modifica stato esterno a funzione |
| **Pure Function** | Funzione Pura | Funzione senza effetti collaterali |
| **Immutable** | Immutabile | Dato non modificabile dopo creazione |
| **Bottleneck** | Collo di Bottiglia | Punto limitazione prestazioni sistema |
| **Latency** | Latenza | Ritardo tempo risposta |
| **Throughput** | Throughput | Quantità lavoro per unità tempo |
| **Scalability** | Scalabilità | Capacità gestire carico crescente |
| **Cache** | Cache | Memoria temporanea dati accesso veloce |
| **Memoization** | Memoizzazione | Caching risultati funzione |
| **Memory Leak** | Perdita Memoria | Memoria allocata non rilasciata |
| **Garbage Collection** | Raccolta Rifiuti | Liberazione automatica memoria inutilizzata |
| **Stack** | Stack/Pila | Struttura dati LIFO |
| **Heap** | Heap/Mucchio | Area memoria dinamica |
| **Pointer** | Puntatore | Variabile contiene indirizzo memoria |
| **Reference** | Riferimento | Alias oggetto esistente |
| **Shallow Copy** | Copia Superficiale | Copia riferimenti non oggetti |
| **Deep Copy** | Copia Profonda | Copia completa ricorsiva oggetti |
| **Serialization** | Serializzazione | Conversione oggetto in formato trasmissibile |
| **Deserialization** | Deserializzazione | Ricostruzione oggetto da formato serializzato |
| **Marshalling** | Marshalling | Preparazione dati per trasmissione |
| **Hashing** | Hashing | Trasformazione dato in valore fisso |
| **Collision** | Collisione | Due input producono stesso hash |
| **Index** | Indice | Struttura accelerare ricerca database |
| **Pagination** | Impaginazione | Suddivisione dati in pagine |
| **Normalization** | Normalizzazione | Organizzare dati ridurre ridondanza |
| **Denormalization** | Denormalizzazione | Aggiungere ridondanza per performance |
| **Endpoint** | Endpoint | URL specifico servizio API |
| **Payload** | Carico Utile | Dati effettivi trasmessi |
| **Request** | Richiesta | Domanda client a server |
| **Response** | Risposta | Risposta server a client |
| **Timeout** | Timeout | Scadenza tempo attesa |
| **Retry** | Riprova | Nuovo tentativo operazione fallita |
| **Handshake** | Stretta di Mano | Negoziazione iniziale connessione |
| **Protocol** | Protocollo | Regole comunicazione tra sistemi |
| **Port** | Porta | Numero identificativo servizio rete |
| **Encryption** | Crittografia | Trasformazione dati in formato illeggibile |
| **Decryption** | Decrittografia | Riconversione dati criptati |
| **Hash** | Hash | Valore fisso da funzione hash |
| **Salt** | Sale | Dati casuali aggiunti prima hashing |
| **Token** | Gettone | Stringa identificazione/autorizzazione |
| **Authentication** | Autenticazione | Verifica identità utente |
| **Authorization** | Autorizzazione | Verifica permessi accesso |
| **Session** | Sessione | Periodo interazione utente-sistema |
| **Cookie** | Cookie | Piccolo file dati salvato browser |
| **Exception** | Eccezione | Evento anomalo durante esecuzione |
| **Error** | Errore | Problema impedisce esecuzione corretta |
| **Warning** | Avviso | Segnalazione problema potenziale |
| **Bug** | Bug | Difetto software causa comportamento errato |
| **Debug** | Debug | Processo identificazione correzione bug |
| **Breakpoint** | Punto Interruzione | Punto pausa esecuzione per debug |
| **Stack Trace** | Traccia Stack | Sequenza chiamate funzioni a errore |
| **Logging** | Registrazione | Salvataggio eventi sistema per analisi |
| **Environment** | Ambiente | Contesto esecuzione applicazione |
| **Production** | Produzione | Ambiente utenti finali |
| **Staging** | Staging | Ambiente test pre-produzione |
| **Development** | Sviluppo | Ambiente sviluppatori |
| **Build** | Build/Compilazione | Processo creazione eseguibile da sorgente |
| **Release** | Rilascio | Versione software distribuita |
| **Rollback** | Rollback | Ripristino versione precedente |
| **Deployment** | Distribuzione | Installazione software ambiente target |
| **Migration** | Migrazione | Spostamento dati/sistema nuovo ambiente |
| **Dependency** | Dipendenza | Componente richiesto da altro |
| **Interface** | Interfaccia | Contratto metodi classe deve implementare |
| **Class** | Classe | Template creazione oggetti |
| **Object** | Oggetto | Istanza classe |
| **Instance** | Istanza | Oggetto specifico di classe |
| **Method** | Metodo | Funzione appartenente classe |
| **Function** | Funzione | Blocco codice esegue task specifico |
| **Variable** | Variabile | Contenitore dati modificabile |
| **Constant** | Costante | Valore immutabile |
| **Namespace** | Spazio Nomi | Contenitore organizzare identificatori |
| **Recursion** | Ricorsione | Funzione chiama se stessa |
| **Iteration** | Iterazione | Ripetizione operazioni in ciclo |
| **Algorithm** | Algoritmo | Sequenza passi risolvere problema |
| **Complexity** | Complessità | Misura risorse richieste algoritmo |
| **Big O Notation** | Notazione Big O | Notazione matematica complessità algoritmica |
| **Optimization** | Ottimizzazione | Migliorare efficienza codice |
| **Benchmark** | Benchmark | Test prestazioni per confronto |
| **Profiling** | Profilazione | Analisi prestazioni runtime |
| **Bit** | Bit | Unità minima informazione binaria |
| **Byte** | Byte | 8 bit, unità base dati |
| **Word** | Word/Parola | Unità dati elaborata CPU (16/32/64 bit) |
| **Register** | Registro | Memoria veloce interno CPU |
| **Instruction Set** | Set Istruzioni | Insieme comandi supportati CPU |
| **Pipeline** | Pipeline | Esecuzione parallela istruzioni CPU |
| **Clock Cycle** | Ciclo Clock | Unità tempo elaborazione CPU |
| **Bandwidth** | Larghezza Banda | Quantità dati trasmessi per unità tempo |
| **Big-Endian** | Big-Endian | Byte più significativo primo in memoria |
| **Little-Endian** | Little-Endian | Byte meno significativo primo in memoria |
| **Endianness** | Ordine Byte | Ordine memorizzazione byte in memoria |
| **Polish Notation** | Notazione Polacca | Operatore prima operandi (prefissa) |
| **Reverse Polish Notation** | Notazione Polacca Inversa | Operatore dopo operandi (postfissa) |
| **Infix Notation** | Notazione Infissa | Operatore tra operandi (standard) |
| **Binary** | Binario | Sistema numerazione base 2 |
| **Hexadecimal** | Esadecimale | Sistema numerazione base 16 |
| **Octal** | Ottale | Sistema numerazione base 8 |
| **Decimal** | Decimale | Sistema numerazione base 10 |
| **Two's Complement** | Complemento a Due | Rappresentazione numeri negativi |
| **Signed** | Con Segno | Numero può essere positivo/negativo |
| **Unsigned** | Senza Segno | Numero solo positivo |
| **Floating Point** | Virgola Mobile | Numeri decimali precisione variabile |
| **Fixed Point** | Virgola Fissa | Numeri decimali precisione fissa |
| **Bitwise** | Bit a Bit | Operazioni su singoli bit |
| **Shift** | Scorrimento | Spostamento bit destra/sinistra |
| **Mask** | Maschera | Pattern bit per filtrare/modificare |
| **Flag** | Flag/Bandiera | Bit singolo indicatore stato booleano |
| **Compiler** | Compilatore | Traduce codice sorgente in eseguibile |
| **Interpreter** | Interprete | Esegue codice riga per riga |
| **Linker** | Linker/Collegatore | Collega file oggetto in eseguibile |
| **Loader** | Caricatore | Carica programma in memoria per esecuzione |
| **Runtime** | Runtime | Ambiente esecuzione programma |
| **Executable** | Eseguibile | File programma eseguibile |
| **Library** | Libreria | Raccolta codice riutilizzabile |
| **Static Linking** | Collegamento Statico | Libreria inclusa in eseguibile |
| **Dynamic Linking** | Collegamento Dinamico | Libreria caricata runtime |
| **Lazy Evaluation** | Valutazione Pigra | Calcolo espressione quando necessario |
| **Eager Evaluation** | Valutazione Immediata | Calcolo espressione subito |
| **Short-circuit** | Cortocircuito | Valutazione espressione fermata anticipata |
| **Hoisting** | Sollevamento | Dichiarazioni spostate inizio scope |
| **Closure** | Chiusura | Funzione con accesso variabili esterne |
| **Scope** | Ambito | Zona visibilità variabile |
| **Lexical Scope** | Ambito Lessicale | Scope determinato posizione codice |
| **Dynamic Scope** | Ambito Dinamico | Scope determinato chiamate runtime |
| **Lazy Loading** | Caricamento Pigro | Caricare risorsa quando necessaria |
| **Eager Loading** | Caricamento Immediato | Caricare tutte risorse subito |
| **Tree** | Albero | Struttura dati gerarchica |
| **Graph** | Grafo | Struttura dati nodi e archi |
| **Queue** | Coda | Struttura dati FIFO |
| **Linked List** | Lista Concatenata | Sequenza nodi collegati puntatori |
| **Array** | Array | Collezione elementi indicizzati |


## 🧪 Testing

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **TDD** | Test-Driven Development | Sviluppo Guidato dai Test | Scrivere test prima del codice |
| **BDD** | Behavior-Driven Development | Sviluppo Guidato dal Comportamento | Test basati su comportamento atteso |
| **ATDD** | Acceptance Test-Driven Development | Sviluppo Guidato da Test di Accettazione | Test basati su criteri di accettazione |
| **E2E** | End-to-End | Da Capo a Coda | Test dell'intero flusso applicativo |
| **UAT** | User Acceptance Testing | Test di Accettazione Utente | Test finale eseguito dagli utenti |
| **QA** | Quality Assurance | Garanzia di Qualità | Processo per assicurare qualità software |
| **SUT** | System Under Test | Sistema Sotto Test | Sistema che viene testato |
| **AAA** | Arrange, Act, Assert | Preparare, Agire, Verificare | Pattern per strutturare test |
| **FIRST** | Fast, Independent, Repeatable, Self-validating, Timely | Veloce, Indipendente, Ripetibile, Auto-validante, Tempestivo | Principi per buoni unit test |


## 🔄 Versionamento

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **VCS** | Version Control System | Sistema Controllo Versione | Sistema per tracciare modifiche codice |
| **SCM** | Source Control Management | Gestione Controllo Sorgente | Gestione repository codice (vedi anche SCM in Business per Supply Chain) |
| **PR** | Pull Request | Richiesta di Pull | Richiesta merge modifiche (GitHub) |
| **MR** | Merge Request | Richiesta di Merge | Richiesta merge modifiche (GitLab) |
| **CR** | Code Review | Revisione Codice | Processo revisione modifiche |
| **WIP** | Work In Progress | Lavoro in Corso | Commit/PR non completato |
| **SemVer** | Semantic Versioning | Versionamento Semantico | Schema versioning MAJOR.MINOR.PATCH |


## 🎨 Design Patterns

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **Singleton** | Singleton | Singleton | Una sola istanza classe |
| **Factory** | Factory Pattern | Pattern Fabbrica | Creazione oggetti senza specificare classe |
| **Observer** | Observer Pattern | Pattern Osservatore | Notifica automatica cambiamenti |
| **Decorator** | Decorator Pattern | Pattern Decoratore | Aggiungere funzionalità dinamicamente |
| **Adapter** | Adapter Pattern | Pattern Adattatore | Compatibilità interfacce incompatibili |
| **Strategy** | Strategy Pattern | Pattern Strategia | Famiglia algoritmi intercambiabili |
| **Facade** | Facade Pattern | Pattern Facciata | Interfaccia semplificata sistema complesso |
| **Proxy** | Proxy Pattern | Pattern Proxy | Placeholder per altro oggetto |
| **Template** | Template Method Pattern | Pattern Metodo Template | Struttura algoritmo con step ridefinibili |
| **Command** | Command Pattern | Pattern Comando | Incapsulare richiesta come oggetto |


## 💻 Sviluppo

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **REPL** | Read-Eval-Print Loop | Ciclo Leggi-Valuta-Stampa | Ambiente interattivo per eseguire codice |
| **IDE** | Integrated Development Environment | Ambiente di Sviluppo Integrato | Software completo per sviluppare |
| **CLI** | Command-Line Interface | Interfaccia a Riga di Comando | Interazione tramite comandi testuali |
| **GUI** | Graphical User Interface | Interfaccia Grafica Utente | Interazione tramite elementi grafici |
| **SDK** | Software Development Kit | Kit di Sviluppo Software | Set di strumenti per sviluppare |
| **API** | Application Programming Interface | Interfaccia di Programmazione Applicativa | Interfaccia per comunicare tra software |
| **ABI** | Application Binary Interface | Interfaccia Binaria Applicativa | Interfaccia a livello binario |
| **DSL** | Domain-Specific Language | Linguaggio Specifico di Dominio | Linguaggio per dominio particolare |
| **WYSIWYG** | What You See Is What You Get | Quello Che Vedi È Quello Che Ottieni | Editor visuale in tempo reale |
| **LSP** | Language Server Protocol | Protocollo Server Linguaggio | Standard per funzionalità IDE |
| **LINQ** | Language Integrated Query | Query Integrata nel Linguaggio | Query SQL-like in C# |
| **NPM** | Node Package Manager | Gestore Pacchetti Node | Gestore dipendenze per Node.js |
| **NVM** | Node Version Manager | Gestore Versioni Node | Tool per gestire versioni Node.js |
| **Yarn** | Yarn | Yarn | Gestore pacchetti alternativo a NPM |
| **Regex** | Regular Expression | Espressione Regolare | Pattern per ricerca/manipolazione testo |


## 🏗️ Architettura

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **MVC** | Model-View-Controller | Modello-Vista-Controllore | Pattern architetturale separazione logica/presentazione |
| **MVVM** | Model-View-ViewModel | Modello-Vista-VistaModello | Pattern per UI con binding dati |
| **MVP** | Model-View-Presenter | Modello-Vista-Presentatore | Variante MVC con Presenter |
| **REST** | Representational State Transfer | Trasferimento di Stato Rappresentazionale | Architettura per API web stateless |
| **SOAP** | Simple Object Access Protocol | Protocollo Semplice Accesso Oggetti | Protocollo per web services XML |
| **SOA** | Service-Oriented Architecture | Architettura Orientata ai Servizi | Architettura basata su servizi |
| **MSA** | Microservices Architecture | Architettura a Microservizi | Applicazione come insieme di servizi piccoli |
| **SPA** | Single Page Application | Applicazione a Pagina Singola | App web che carica una sola pagina |
| **SSR** | Server-Side Rendering | Rendering Lato Server | Generazione HTML sul server |
| **CSR** | Client-Side Rendering | Rendering Lato Client | Generazione HTML nel browser |
| **MPA** | Multi-Page Application | Applicazione Multi-Pagina | App web tradizionale con più pagine |
| **JAMstack** | JavaScript, APIs, Markup | JavaScript, API, Markup | Architettura web moderna |
| **CQRS** | Command Query Responsibility Segregation | Segregazione Responsabilità Comando-Query | Separare operazioni lettura/scrittura |
| **EDA** | Event-Driven Architecture | Architettura Guidata da Eventi | Sistema basato su produzione/consumo eventi |
| **RPC** | Remote Procedure Call | Chiamata Procedura Remota | Esecuzione funzioni su server remoto |
| **gRPC** | gRPC Remote Procedure Call | gRPC Chiamata Procedura Remota | Framework RPC ad alte prestazioni di Google |
| **GraphQL** | Graph Query Language | Linguaggio Query Grafo | Linguaggio query alternativo a REST |
| **WebSocket** | WebSocket | WebSocket | Protocollo comunicazione bidirezionale |


## 🌐 Web Development

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **HTTP** | Hypertext Transfer Protocol | Protocollo Trasferimento Ipertesto | Protocollo web principale |
| **HTTPS** | HTTP Secure | HTTP Sicuro | HTTP con crittografia SSL/TLS |
| **HTML** | Hypertext Markup Language | Linguaggio Markup Ipertesto | Linguaggio struttura pagine web |
| **CSS** | Cascading Style Sheets | Fogli di Stile a Cascata | Linguaggio styling pagine web |
| **DOM** | Document Object Model | Modello Oggetto Documento | Rappresentazione struttura HTML |
| **AJAX** | Asynchronous JavaScript and XML | JavaScript e XML Asincrono | Richieste server asincrone |
| **JSON** | JavaScript Object Notation | Notazione Oggetto JavaScript | Formato scambio dati leggero |
| **XML** | Extensible Markup Language | Linguaggio Markup Estensibile | Formato dati strutturato |
| **YAML** | YAML Ain't Markup Language | YAML Non È Linguaggio Markup | Formato configurazione leggibile |
| **JWT** | JSON Web Token | Token Web JSON | Token autenticazione compatto |
| **CORS** | Cross-Origin Resource Sharing | Condivisione Risorse Cross-Origin | Politica sicurezza richieste cross-domain |
| **CDN** | Content Delivery Network | Rete Distribuzione Contenuti | Rete server per distribuzione veloce |
| **SEO** | Search Engine Optimization | Ottimizzazione Motori Ricerca | Tecniche per migliorare ranking |
| **PWA** | Progressive Web App | App Web Progressiva | Web app con funzionalità native |
| **SWR** | Stale-While-Revalidate | Obsoleto-Durante-Rivalidazione | Strategia caching dati |
| **SSG** | Static Site Generation | Generazione Sito Statico | Generare HTML statico build-time |
| **ISR** | Incremental Static Regeneration | Rigenerazione Statica Incrementale | Aggiornare pagine statiche selettivamente |
| **RWD** | Responsive Web Design | Design Web Responsivo | Design adattivo per dispositivi |
| **URL** | Uniform Resource Locator | Localizzatore Risorsa Uniforme | Indirizzo risorsa web |
| **URI** | Uniform Resource Identifier | Identificatore Risorsa Uniforme | Identificatore generico risorsa |
| **URN** | Uniform Resource Name | Nome Risorsa Uniforme | Nome persistente risorsa |


## 📱 Mobile & Frontend

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **UI** | User Interface | Interfaccia Utente | Aspetto visuale applicazione |
| **UX** | User Experience | Esperienza Utente | Esperienza complessiva utente |
| **UXD** | User Experience Design | Design Esperienza Utente | Progettazione esperienza utente |
| **A11y** | Accessibility | Accessibilità | Usabilità per persone con disabilità |
| **i18n** | Internationalization | Internazionalizzazione | Supporto multilingua (18 lettere tra i e n) |
| **l10n** | Localization | Localizzazione | Adattamento lingua/cultura (10 lettere tra l e n) |
| **Polyfill** | Polyfill | Polyfill | Codice per funzionalità mancanti browser |
| **Transpiler** | Transpiler | Transpiler | Convertire codice sorgente in altro |
| **Bundler** | Bundler | Bundler | Tool per combinare file JavaScript |
| **HMR** | Hot Module Replacement | Sostituzione Modulo a Caldo | Aggiornamento moduli senza reload |
| **APK** | Android Package Kit | Kit Pacchetto Android | File installazione app Android |
| **IPA** | iOS App Store Package | Pacchetto App Store iOS | File installazione app iOS |


## 🔧 Backend & Infrastructure

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **Load Balancer** | Load Balancer | Bilanciatore Carico | Distribuzione traffico tra server |
| **Reverse Proxy** | Reverse Proxy | Proxy Inverso | Intermediario tra client e server |
| **Forward Proxy** | Forward Proxy | Proxy Diretto | Intermediario per client |
| **Firewall** | Firewall | Firewall | Sistema sicurezza rete |
| **WAF** | Web Application Firewall | Firewall Applicazione Web | Firewall specifico per web app |
| **Container** | Container | Contenitore | Ambiente isolato per applicazione |
| **Orchestration** | Orchestration | Orchestrazione | Gestione automatica container |
| **Microservice** | Microservice | Microservizio | Servizio piccolo e indipendente |
| **Monolith** | Monolith | Monolite | Applicazione singola non modulare |
| **Middleware** | Middleware | Middleware | Software intermedio tra componenti |
| **Webhook** | Webhook | Webhook | Callback HTTP per eventi |
| **Cron** | Cron | Cron | Scheduler task Unix |
| **Daemon** | Daemon | Demone | Processo background |
| **PID** | Process ID | ID Processo | Identificatore univoco processo sistema operativo |


## 🗄️ Database

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **SQL** | Structured Query Language | Linguaggio Query Strutturato | Linguaggio per database relazionali |
| **NoSQL** | Not Only SQL | Non Solo SQL | Database non relazionali |
| **ORM** | Object-Relational Mapping | Mappatura Oggetto-Relazionale | Conversione dati tra OOP e DB |
| **ODM** | Object-Document Mapping | Mappatura Oggetto-Documento | ORM per database a documenti |
| **DBMS** | Database Management System | Sistema Gestione Database | Software per gestire database |
| **RDBMS** | Relational Database Management System | Sistema Gestione Database Relazionale | DBMS per DB relazionali |
| **DDL** | Data Definition Language | Linguaggio Definizione Dati | SQL per struttura (CREATE, ALTER) |
| **DML** | Data Manipulation Language | Linguaggio Manipolazione Dati | SQL per dati (INSERT, UPDATE, DELETE) |
| **DCL** | Data Control Language | Linguaggio Controllo Dati | SQL per permessi (GRANT, REVOKE) |
| **TCL** | Transaction Control Language | Linguaggio Controllo Transazioni | SQL per transazioni (COMMIT, ROLLBACK) |
| **ETL** | Extract, Transform, Load | Estrarre, Trasformare, Caricare | Processo migrazione dati |
| **OLTP** | Online Transaction Processing | Elaborazione Transazioni Online | Database per operazioni frequenti |
| **OLAP** | Online Analytical Processing | Elaborazione Analitica Online | Database per analisi complesse |
| **ACID** | Atomicity, Consistency, Isolation, Durability | Atomicità, Consistenza, Isolamento, Durabilità | Proprietà transazioni database |
| **BASE** | Basically Available, Soft state, Eventually consistent | Fondamentalmente Disponibile, Stato Morbido, Eventualmente Consistente | Alternativa ACID per NoSQL |
| **CAP** | Consistency, Availability, Partition tolerance | Consistenza, Disponibilità, Tolleranza Partizione | Teorema per sistemi distribuiti |
| **BLOB** | Binary Large Object | Oggetto Binario Grande | Tipo dato per file binari in DB |
| **IOPS** | Input/Output Operations Per Second | Operazioni Input/Output al Secondo | Metrica prestazioni storage |
| **RAID** | Redundant Array of Independent Disks | Array Ridondante Dischi Indipendenti | Tecnologia affidabilità storage |


## 🌍 Networking & Protocolli

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **TCP** | Transmission Control Protocol | Protocollo Controllo Trasmissione | Protocollo affidabile connessione |
| **UDP** | User Datagram Protocol | Protocollo Datagramma Utente | Protocollo veloce senza connessione |
| **IP** | Internet Protocol | Protocollo Internet | Protocollo indirizzamento rete |
| **DNS** | Domain Name System | Sistema Nomi Dominio | Sistema traduzione nomi in IP |
| **FTP** | File Transfer Protocol | Protocollo Trasferimento File | Protocollo trasferimento file |
| **SFTP** | Secure File Transfer Protocol | Protocollo Trasferimento File Sicuro | FTP su SSH |
| **SSH** | Secure Shell | Shell Sicuro | Protocollo accesso remoto sicuro |
| **SMTP** | Simple Mail Transfer Protocol | Protocollo Trasferimento Mail Semplice | Protocollo invio email |
| **IMAP** | Internet Message Access Protocol | Protocollo Accesso Messaggi Internet | Protocollo gestione email server |
| **POP3** | Post Office Protocol 3 | Protocollo Ufficio Postale 3 | Protocollo download email |
| **DHCP** | Dynamic Host Configuration Protocol | Protocollo Configurazione Host Dinamica | Assegnazione automatica IP |
| **NAT** | Network Address Translation | Traduzione Indirizzo Rete | Conversione IP privati/pubblici |
| **VPN** | Virtual Private Network | Rete Privata Virtuale | Rete sicura su internet |
| **LAN** | Local Area Network | Rete Area Locale | Rete locale limitata |
| **WAN** | Wide Area Network | Rete Area Estesa | Rete geograficamente estesa |
| **OSI** | Open Systems Interconnection | Interconnessione Sistemi Aperti | Modello rete 7 layer |
| **MAC** | Media Access Control | Controllo Accesso Media | Indirizzo hardware rete |
| **AMQP** | Advanced Message Queuing Protocol | Protocollo Avanzato Accodamento Messaggi | Protocollo messaging enterprise |


## 🔐 Security

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **XSS** | Cross-Site Scripting | Scripting Cross-Site | Iniezione script malevoli |
| **CSRF** | Cross-Site Request Forgery | Falsificazione Richiesta Cross-Site | Attacco per eseguire azioni non autorizzate |
| **SQL Injection** | SQL Injection | Iniezione SQL | Inserimento SQL malevolo |
| **2FA** | Two-Factor Authentication | Autenticazione a Due Fattori | Doppia verifica identità |
| **MFA** | Multi-Factor Authentication | Autenticazione Multi-Fattore | Verifica identità multipla |
| **OAuth** | Open Authorization | Autorizzazione Aperta | Standard autorizzazione delegata |
| **OIDC** | OpenID Connect | OpenID Connect | Layer identità su OAuth |
| **SSO** | Single Sign-On | Accesso Singolo | Autenticazione unica per più sistemi |
| **SAML** | Security Assertion Markup Language | Linguaggio Markup Asserzione Sicurezza | Standard scambio autenticazione |
| **SSL** | Secure Sockets Layer | Layer Socket Sicuro | Protocollo crittografia (deprecato) |
| **TLS** | Transport Layer Security | Sicurezza Layer Trasporto | Successore SSL per crittografia |
| **PKI** | Public Key Infrastructure | Infrastruttura Chiave Pubblica | Sistema gestione certificati digitali |
| **RBAC** | Role-Based Access Control | Controllo Accesso Basato Ruoli | Permessi basati su ruoli |
| **ACL** | Access Control List | Lista Controllo Accesso | Lista permessi risorse |
| **GDPR** | General Data Protection Regulation | Regolamento Generale Protezione Dati | Legge UE privacy dati |
| **OWASP** | Open Web Application Security Project | Progetto Sicurezza Applicazioni Web Aperto | Organizzazione sicurezza web |
| **CVE** | Common Vulnerabilities and Exposures | Vulnerabilità ed Esposizioni Comuni | Database vulnerabilità pubbliche |
| **DDoS** | Distributed Denial of Service | Negazione Servizio Distribuita | Attacco sovraccarico sistema |
| **HSTS** | HTTP Strict Transport Security | Sicurezza Trasporto HTTP Rigoroso | Header forzare connessioni HTTPS |
| **CSP** | Content Security Policy | Politica Sicurezza Contenuti | Header prevenire XSS e injection |


## ⚡ Performance

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **TTL** | Time To Live | Tempo di Vita | Durata validità dato/pacchetto |
| **TTFB** | Time To First Byte | Tempo al Primo Byte | Tempo risposta server |
| **FCP** | First Contentful Paint | Prima Visualizzazione Contenuto | Primo elemento visibile renderizzato |
| **LCP** | Largest Contentful Paint | Visualizzazione Contenuto Principale | Elemento principale caricato |
| **FID** | First Input Delay | Ritardo Primo Input | Tempo risposta prima interazione |
| **CLS** | Cumulative Layout Shift | Spostamento Layout Cumulativo | Stabilità visuale pagina |
| **Gzip** | GNU zip | GNU zip | Algoritmo compressione |
| **Brotli** | Brotli | Brotli | Algoritmo compressione moderno |
| **Minification** | Minification | Minificazione | Riduzione dimensioni file |


## 🚀 DevOps & Deploy

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **CI/CD** | Continuous Integration/Continuous Deployment | Integrazione Continua/Distribuzione Continua | Automazione build, test e deploy |
| **CD** | Continuous Delivery | Consegna Continua | Codice sempre pronto per il deploy |
| **SaaS** | Software as a Service | Software come Servizio | Software su cloud via browser |
| **PaaS** | Platform as a Service | Piattaforma come Servizio | Piattaforma cloud per sviluppo |
| **IaaS** | Infrastructure as a Service | Infrastruttura come Servizio | Risorse hardware virtualizzate |
| **FaaS** | Function as a Service | Funzione come Servizio | Esecuzione funzioni serverless |
| **BaaS** | Backend as a Service | Backend come Servizio | Backend pre-costruito per mobile |
| **DaaS** | Data as a Service | Dati come Servizio | Dati accessibili via cloud |
| **IaC** | Infrastructure as Code | Infrastruttura come Codice | Gestire infrastruttura con codice |
| **GitOps** | Git Operations | Operazioni Git | Deploy basato su repository Git |
| **K8s** | Kubernetes | Kubernetes | Orchestrazione container (8 lettere tra K e s) |
| **VM** | Virtual Machine | Macchina Virtuale | Sistema operativo virtualizzato |
| **VPS** | Virtual Private Server | Server Privato Virtuale | Server virtuale dedicato |
| **SLA** | Service Level Agreement | Accordo Livello Servizio | Contratto qualità servizio |
| **SLO** | Service Level Objective | Obiettivo Livello Servizio | Target specifico di performance |
| **SLI** | Service Level Indicator | Indicatore Livello Servizio | Metrica misurare SLO |
| **MTBF** | Mean Time Between Failures | Tempo Medio Tra Guasti | Affidabilità sistema |
| **MTTR** | Mean Time To Recovery | Tempo Medio Recupero | Velocità ripristino |
| **RPO** | Recovery Point Objective | Obiettivo Punto Recupero | Perdita dati accettabile |
| **RTO** | Recovery Time Objective | Obiettivo Tempo Recupero | Downtime massimo accettabile |


## 🤖 AI & Machine Learning

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **AI** | Artificial Intelligence | Intelligenza Artificiale | Simulazione intelligenza umana |
| **ML** | Machine Learning | Apprendimento Automatico | Algoritmi apprendimento dai dati |
| **DL** | Deep Learning | Apprendimento Profondo | Machine learning con reti neurali profonde |
| **NLP** | Natural Language Processing | Elaborazione Linguaggio Naturale | AI per linguaggio umano |
| **LLM** | Large Language Model | Modello Linguistico Grande | Modello AI addestrato su grandi quantità di testo |
| **RAG** | Retrieval-Augmented Generation | Generazione Aumentata da Recupero | Tecnica per arricchire LLM con dati esterni |
| **GPT** | Generative Pre-trained Transformer | Transformer Generativo Pre-addestrato | Architettura modello linguistico |
| **BERT** | Bidirectional Encoder Representations from Transformers | Rappresentazioni Encoder Bidirezionale da Transformer | Modello comprensione linguaggio bidirezionale |
| **RL** | Reinforcement Learning | Apprendimento per Rinforzo | Apprendimento tramite ricompense/penalità |
| **RLHF** | Reinforcement Learning from Human Feedback | Apprendimento per Rinforzo da Feedback Umano | Affinamento modelli con preferenze umane |
| **SFT** | Supervised Fine-Tuning | Affinamento Supervisionato | Addestramento supervisionato su dati specifici |
| **LoRA** | Low-Rank Adaptation | Adattamento a Basso Rango | Tecnica efficiente per fine-tuning modelli |
| **GAN** | Generative Adversarial Network | Rete Generativa Avversaria | Due reti neurali che competono |
| **CNN** | Convolutional Neural Network | Rete Neurale Convoluzionale | Rete neurale per elaborazione immagini |
| **RNN** | Recurrent Neural Network | Rete Neurale Ricorrente | Rete neurale per dati sequenziali |
| **LSTM** | Long Short-Term Memory | Memoria a Breve-Lungo Termine | Tipo di RNN per sequenze lunghe |
| **CV** | Computer Vision | Visione Artificiale | AI per interpretare immagini (non Curriculum Vitae) |
| **ASR** | Automatic Speech Recognition | Riconoscimento Vocale Automatico | Conversione voce in testo |
| **TTS** | Text-To-Speech | Testo-in-Voce | Sintesi vocale da testo |
| **CoT** | Chain-of-Thought | Catena di Pensiero | Tecnica prompting per ragionamento passo-passo |
| **Few-Shot** | Few-Shot Learning | Apprendimento Pochi Esempi | Apprendimento con pochi esempi |
| **Zero-Shot** | Zero-Shot Learning | Apprendimento Senza Esempi | Apprendimento senza esempi training |
| **ICL** | In-Context Learning | Apprendimento nel Contesto | Apprendimento tramite esempi nel prompt |
| **ViT** | Vision Transformer | Transformer Visione | Architettura Transformer per immagini |
| **VAE** | Variational Autoencoder | Autoencoder Variazionale | Rete neurale per generazione dati |
| **CLIP** | Contrastive Language-Image Pre-training | Pre-addestramento Contrastivo Linguaggio-Immagine | Modello multimodale testo-immagine |
| **T5** | Text-to-Text Transfer Transformer | Transformer Trasferimento Testo-a-Testo | Modello unificato per task NLP |
| **BART** | Bidirectional and Auto-Regressive Transformers | Transformer Bidirezionale e Auto-Regressivo | Modello encoder-decoder |
| **DPO** | Direct Preference Optimization | Ottimizzazione Preferenze Diretta | Alternativa RLHF per allineamento |
| **PEFT** | Parameter-Efficient Fine-Tuning | Affinamento Efficiente Parametri | Tecniche fine-tuning con pochi parametri |
| **QLoRA** | Quantized LoRA | LoRA Quantizzato | LoRA con quantizzazione per efficienza |
| **PPO** | Proximal Policy Optimization | Ottimizzazione Politica Prossimale | Algoritmo RL per RLHF |
| **ToT** | Tree of Thoughts | Albero dei Pensieri | Tecnica prompting con esplorazione ramificata |
| **ReAct** | Reasoning and Acting | Ragionamento e Azione | Combinare ragionamento e azioni in LLM |
| **MoE** | Mixture of Experts | Miscela di Esperti | Architettura con sotto-modelli specializzati |
| **BLEU** | Bilingual Evaluation Understudy | Sostituto Valutazione Bilingue | Metrica qualità traduzione automatica |
| **ROUGE** | Recall-Oriented Understudy for Gisting Evaluation | Sostituto Orientato Richiamo per Valutazione Riassunti | Metrica qualità riassunti |
| **METEOR** | Metric for Evaluation of Translation with Explicit ORdering | Metrica Valutazione Traduzione con Ordinamento Esplicito | Metrica avanzata per traduzioni |
| **PPL** | Perplexity | Perplessità | Metrica qualità modello linguistico |
| **VRAM** | Video Random Access Memory | Memoria Video ad Accesso Casuale | Memoria GPU per AI |
| **FP16** | Float Precision 16 | Precisione Float 16 | Formato numerico 16-bit |
| **BF16** | Brain Float 16 | Brain Float 16 | Formato numerico 16-bit ottimizzato Google |
| **INT8** | Integer 8-bit | Intero 8-bit | Quantizzazione 8-bit per efficienza |


## ⚙️ Embedded & IoT

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **IoT** | Internet of Things | Internet delle Cose | Rete dispositivi connessi a Internet |
| **PID Controller** | Proportional-Integral-Derivative Controller | Controller PID | Algoritmo controllo feedback per sistemi automatici |
| **MCU** | Microcontroller Unit | Unità Microcontrollore | Chip con processore, memoria e I/O |
| **SoC** | System on Chip | Sistema su Chip | Intero sistema integrato su singolo chip |
| **RTOS** | Real-Time Operating System | Sistema Operativo Tempo Reale | OS per applicazioni tempo reale |
| **UART** | Universal Asynchronous Receiver-Transmitter | Trasmettitore-Ricevitore Asincrono Universale | Protocollo comunicazione seriale |
| **I2C** | Inter-Integrated Circuit | Circuito Inter-Integrato | Protocollo comunicazione seriale multi-device |
| **SPI** | Serial Peripheral Interface | Interfaccia Periferica Seriale | Protocollo comunicazione seriale veloce |
| **PWM** | Pulse Width Modulation | Modulazione Larghezza Impulso | Tecnica controllo potenza tramite impulsi |
| **GPIO** | General Purpose Input/Output | Input/Output Uso Generico | Pin configurabili input/output |
| **ADC** | Analog-to-Digital Converter | Convertitore Analogico-Digitale | Converte segnale analogico in digitale |
| **DAC** | Digital-to-Analog Converter | Convertitore Digitale-Analogico | Converte segnale digitale in analogico |
| **CAN** | Controller Area Network | Rete Area Controller | Protocollo comunicazione veicoli/industria |
| **MQTT** | Message Queuing Telemetry Transport | Trasporto Telemetria Accodamento Messaggi | Protocollo messaging leggero IoT |
| **CoAP** | Constrained Application Protocol | Protocollo Applicazione Vincolato | Protocollo web per dispositivi limitati |
| **BLE** | Bluetooth Low Energy | Bluetooth Bassa Energia | Versione Bluetooth a basso consumo |
| **NFC** | Near Field Communication | Comunicazione Campo Vicino | Comunicazione wireless corto raggio |
| **RFID** | Radio-Frequency Identification | Identificazione Radio Frequenza | Tecnologia identificazione wireless |
| **OTA** | Over-The-Air | Via Etere | Aggiornamento software wireless |
| **Firmware** | Firmware | Firmware | Software permanente embedded in hardware |
| **FPGA** | Field-Programmable Gate Array | Array Gate Programmabile sul Campo | Chip logico programmabile hardware |
| **ASIC** | Application-Specific Integrated Circuit | Circuito Integrato Specifico Applicazione | Chip progettato per funzione specifica |
| **ARM** | Advanced RISC Machine | Macchina RISC Avanzata | Architettura processori basso consumo |
| **RISC** | Reduced Instruction Set Computer | Computer Set Istruzioni Ridotto | Architettura CPU istruzioni semplici |
| **CISC** | Complex Instruction Set Computer | Computer Set Istruzioni Complesso | Architettura CPU istruzioni complesse |
| **DSP** | Digital Signal Processor | Processore Segnali Digitali | Processore ottimizzato elaborazione segnali |
| **EEPROM** | Electrically Erasable Programmable ROM | ROM Programmabile Cancellabile Elettricamente | Memoria non volatile riscrivibile |
| **Flash** | Flash Memory | Memoria Flash | Memoria non volatile veloce |
| **Modbus** | Modbus | Modbus | Protocollo comunicazione industriale seriale |
| **LoRa** | Long Range | Lungo Raggio | Tecnologia comunicazione wireless lungo raggio |
| **LoRaWAN** | Long Range Wide Area Network | Rete Area Estesa Lungo Raggio | Protocollo rete per LoRa |
| **Zigbee** | Zigbee | Zigbee | Protocollo wireless mesh per IoT |
| **Thread Protocol** | Thread | Thread | Protocollo rete mesh IP per IoT |
| **6LoWPAN** | IPv6 over Low-Power Wireless PAN | IPv6 su PAN Wireless Basso Consumo | Standard IPv6 per reti wireless IoT |
| **LTE-M** | Long-Term Evolution for Machines | Evoluzione Lungo Termine per Macchine | Standard cellulare per IoT |
| **NB-IoT** | Narrowband IoT | IoT Banda Stretta | Tecnologia cellulare LPWAN per IoT |
| **ISR** | Interrupt Service Routine | Routine Servizio Interrupt | Funzione gestione interrupt |
| **DMA** | Direct Memory Access | Accesso Diretto Memoria | Trasferimento dati senza CPU |
| **Watchdog** | Watchdog Timer | Timer Watchdog | Timer reset automatico sistema bloccato |
| **Bootloader** | Bootloader | Caricatore Avvio | Programma avvio e caricamento firmware |
| **Bit Banging** | Bit Banging | Bit Banging | Implementazione protocollo software controllando pin GPIO manualmente |
| **Pull-up Resistor** | Resistenza Pull-up | Resistenza Pull-up | Resistenza porta pin a livello alto |
| **Pull-down Resistor** | Resistenza Pull-down | Resistenza Pull-down | Resistenza porta pin a livello basso |
| **Debouncing** | Debouncing | Antirimbalzo | Filtraggio rimbalzi meccanici pulsanti |
| **Polling** | Polling | Polling | Interrogazione ciclica stato dispositivo |
| **Interrupt** | Interrupt | Interruzione | Segnale asincrono sospende esecuzione normale |


## 📊 Data & Analytics

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **BI** | Business Intelligence | Intelligenza Aziendale | Analisi dati per business |
| **Data Lake** | Data Lake | Lago Dati | Repository dati grezzi |
| **Data Warehouse** | Data Warehouse | Magazzino Dati | Repository dati strutturati |
| **Data Mart** | Data Mart | Mercato Dati | Subset data warehouse |
| **KPI** | Key Performance Indicator | Indicatore Prestazione Chiave | Metrica misurare successo |
| **CSV** | Comma-Separated Values | Valori Separati Virgola | Formato file dati tabulari |


## 💼 Business & Commerciale

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **B2B** | Business-to-Business | Azienda ad Azienda | Vendita tra aziende |
| **B2C** | Business-to-Consumer | Azienda a Consumatore | Vendita azienda a consumatore finale |
| **B2B2C** | Business-to-Business-to-Consumer | Azienda ad Azienda a Consumatore | Modello intermediato |
| **C2C** | Consumer-to-Consumer | Consumatore a Consumatore | Vendita tra consumatori |
| **B2G** | Business-to-Government | Azienda a Governo | Vendita azienda a enti pubblici |
| **D2C** | Direct-to-Consumer | Diretto al Consumatore | Vendita diretta senza intermediari |
| **DTC** | Direct-to-Consumer | Diretto al Consumatore | Alias di D2C |
| **ARR** | Annual Recurring Revenue | Ricavi Ricorrenti Annuali | Ricavi annuali da abbonamenti |
| **MRR** | Monthly Recurring Revenue | Ricavi Ricorrenti Mensili | Ricavi mensili da abbonamenti |
| **CAC** | Customer Acquisition Cost | Costo Acquisizione Cliente | Costo per acquisire un cliente |
| **LTV** | Lifetime Value | Valore Vita Cliente | Valore totale cliente nel tempo |
| **CLV** | Customer Lifetime Value | Valore Vita Cliente | Alias di LTV |
| **ARPU** | Average Revenue Per User | Ricavo Medio per Utente | Ricavo medio per utente |
| **CAGR** | Compound Annual Growth Rate | Tasso Crescita Annuale Composto | Tasso crescita medio annuo |
| **GMV** | Gross Merchandise Value | Valore Lordo Merce | Valore totale transazioni |
| **ROI** | Return on Investment | Ritorno Investimento | Rapporto guadagno/investimento |
| **TCO** | Total Cost of Ownership | Costo Totale Proprietà | Costo completo possesso/gestione |
| **NPS** | Net Promoter Score | Punteggio Promotore Netto | Metrica soddisfazione cliente |
| **CRR** | Customer Retention Rate | Tasso Ritenzione Clienti | Percentuale clienti mantenuti |
| **Churn** | Churn Rate | Tasso Abbandono | Percentuale clienti persi |
| **EULA** | End-User License Agreement | Accordo Licenza Utente Finale | Contratto licenza software |
| **OEM** | Original Equipment Manufacturer | Produttore Apparecchiature Originali | Produttore componenti per altri |
| **ERP** | Enterprise Resource Planning | Pianificazione Risorse Aziendali | Sistema gestione integrato aziendale |
| **CRM** | Customer Relationship Management | Gestione Relazioni Clienti | Software gestione clienti |
| **CMS** | Content Management System | Sistema Gestione Contenuti | Piattaforma gestione contenuti web |
| **SCM** | Supply Chain Management | Gestione Catena Fornitura | Sistema gestione supply chain |
| **WMS** | Warehouse Management System | Sistema Gestione Magazzino | Software gestione magazzino |
| **TMS** | Transportation Management System | Sistema Gestione Trasporti | Software gestione trasporti |
| **POS** | Point of Sale | Punto Vendita | Sistema cassa/vendita |
| **HRM** | Human Resource Management | Gestione Risorse Umane | Sistema gestione personale |
| **HRIS** | Human Resource Information System | Sistema Informativo Risorse Umane | Database gestione HR |
| **ATS** | Applicant Tracking System | Sistema Tracciamento Candidati | Software recruiting |
| **DMS** | Document Management System | Sistema Gestione Documenti | Software archiviazione documenti |
| **DAM** | Digital Asset Management | Gestione Asset Digitali | Sistema gestione file multimediali |
| **MES** | Manufacturing Execution System | Sistema Esecuzione Produzione | Software controllo produzione |
| **PLM** | Product Lifecycle Management | Gestione Ciclo Vita Prodotto | Sistema gestione sviluppo prodotti |
| **BPM** | Business Process Management | Gestione Processi Aziendali | Sistema ottimizzazione processi |
| **ECM** | Enterprise Content Management | Gestione Contenuti Aziendali | Sistema gestione documenti enterprise |
| **MDM** | Master Data Management | Gestione Dati Master | Sistema dati anagrafici centralizzati |


## 🏃 Agile & Project Management

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **Agile** | Agile | Agile | Metodologia sviluppo iterativa |
| **Scrum** | Scrum | Scrum | Framework Agile con sprint |
| **Kanban** | Kanban | Kanban | Sistema gestione lavoro visuale |
| **Sprint** | Sprint | Sprint | Iterazione sviluppo temporizzata |
| **Backlog** | Backlog | Arretrato | Lista funzionalità da implementare |
| **Epic** | Epic | Epica | Grande funzionalità decomponibile |
| **Story** | User Story | Storia Utente | Requisito dal punto vista utente |
| **DoD** | Definition of Done | Definizione di Fatto | Criteri completamento task |
| **DoR** | Definition of Ready | Definizione di Pronto | Criteri per iniziare task |
| **WIP** | Work In Progress | Lavoro in Corso | Task in svolgimento |
| **MVP** | Minimum Viable Product | Prodotto Minimo Funzionante | Versione base prodotto |
| **POC** | Proof of Concept | Prova di Concetto | Dimostrazione fattibilità |
| **Spike** | Spike | Spike | Ricerca/prototipo per ridurre rischio |
| **Velocity** | Velocity | Velocità | Quantità lavoro per sprint |
| **Burndown** | Burndown Chart | Grafico Consumo | Grafico lavoro rimanente |
| **Retrospective** | Retrospective | Retrospettiva | Riunione miglioramento processo |
| **Standup** | Daily Standup | Standup Giornaliero | Riunione quotidiana breve |


## 🔤 Vari & Slang

| Acronimo | Termine Inglese | Traduzione | Spiegazione |
|----------|-----------------|------------|-------------|
| **RTFM** | Read The F***ing Manual | Leggi Il Manuale | Invito leggere documentazione |
| **LGTM** | Looks Good To Me | Mi Sembra Buono | Approvazione code review |
| **TBD** | To Be Determined | Da Determinare | Decisione futura |
| **TBA** | To Be Announced | Da Annunciare | Informazione futura |
| **ASAP** | As Soon As Possible | Appena Possibile | Urgente |
| **FYI** | For Your Information | Per Tua Informazione | Informazione condivisa |
| **IMO** | In My Opinion | Secondo Me | Opinione personale |
| **IMHO** | In My Humble Opinion | Secondo la Mia Umile Opinione | Opinione personale umile |
| **TL;DR** | Too Long; Didn't Read | Troppo Lungo; Non Letto | Riassunto breve |
| **ETA** | Estimated Time of Arrival | Tempo Stimato Arrivo | Quando sarà pronto |
| **EOD** | End of Day | Fine Giornata | Entro oggi |
| **OOO** | Out of Office | Fuori Ufficio | Non disponibile |
| **AFK** | Away From Keyboard | Lontano dalla Tastiera | Non al computer |
| **PEBCAK** | Problem Exists Between Chair And Keyboard | Problema Esiste Tra Sedia e Tastiera | Errore utente |
| **SNAFU** | Situation Normal: All F***ed Up | Situazione Normale: Tutto Incasinato | Caos normale |
| **FUBAR** | F***ed Up Beyond All Recognition | Incasinato Oltre Ogni Riconoscimento | Completamente rotto |
| **RFC** | Request for Comments | Richiesta Commenti | Standard documentazione tecnica Internet |
| **FOSS** | Free and Open Source Software | Software Libero e Open Source | Software libero e aperto |
| **OSS** | Open Source Software | Software Open Source | Software a sorgente aperto |
| **POSIX** | Portable Operating System Interface | Interfaccia Sistema Operativo Portabile | Standard compatibilità Unix |
| **UTF** | Unicode Transformation Format | Formato Trasformazione Unicode | Codifica caratteri Unicode |
| **ASCII** | American Standard Code for Information Interchange | Codice Standard Americano Scambio Informazioni | Codifica caratteri base |

---

**Totale acronimi: ~323 | Termini: ~174 | TOTALE: ~497**

📌 **Suggerimento**: Salva questo glossario e consultalo quando incontri nuovi acronimi!