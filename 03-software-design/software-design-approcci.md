# Approcci di Design Software

## Architetture Applicative

### **Domain-Driven Design (DDD)**
Approccio che pone il dominio di business al centro. Utilizza un linguaggio ubiquo condiviso tra sviluppatori e domain experts. Organizza il codice in bounded contexts, aggregates, entities, value objects e domain services. Focus sulla modellazione accurata delle regole di business.

### **Clean Architecture**
Architettura a cerchi concentrici dove le dipendenze puntano sempre verso l'interno. Il core contiene entities e use cases, indipendenti da framework e UI. Gli strati esterni implementano dettagli tecnici (DB, web, UI). Facilita testabilità e manutenibilità.

### **Hexagonal Architecture (Ports & Adapters)**
Isola la logica di business dal mondo esterno tramite ports (interfacce) e adapters (implementazioni). Il dominio è al centro, circondato da adapters per UI, database, API esterne. Permette di sostituire facilmente componenti esterni.

### **Onion Architecture**
Simile a Clean Architecture, con il dominio al centro circondato da layer applicativi, infrastrutturali e UI. Ogni layer dipende solo da quelli più interni. Enfatizza l'inversione delle dipendenze e la separazione delle responsabilità.

### **Model-View-Controller (MVC)**
Separa l'applicazione in tre componenti: Model (dati e logica), View (presentazione), Controller (gestisce input utente e coordina). Pattern classico per applicazioni web e desktop.

### **Model-View-ViewModel (MVVM)**
Evoluzione di MVC dove il ViewModel fa da mediatore tra View e Model. Binding bidirezionale tra View e ViewModel. Comune in applicazioni con UI reattive (WPF, Angular, Vue).

### **Model-View-Presenter (MVP)**
Variante di MVC dove il Presenter contiene tutta la logica di presentazione. La View è completamente passiva. Migliora la testabilità separando nettamente UI e logica.

### **Vertical Slice Architecture**
Organizza codice per feature invece che per layer tecnici. Ogni slice è una feature completa end-to-end. Riduce coupling tra feature, aumenta coesione interna. Alternativa moderna alla layered architecture.

### **Modular Monolith**
Monolite organizzato in moduli ben definiti e separati. Ogni modulo ha confini chiari e può essere estratto come microservizio. Bilanciamento tra semplicità deployment e organizzazione del codice.

## Architetture Distribuite

### **Microservices Architecture**
Applicazione composta da servizi piccoli, indipendenti e deployabili autonomamente. Ogni servizio gestisce un bounded context specifico. Comunicazione via API (REST, gRPC, messaggi). Scalabilità e manutenibilità granulare.

### **Service-Oriented Architecture (SOA)**
Architettura basata su servizi riutilizzabili che comunicano tramite protocolli standard (SOAP, REST). Servizi più grandi e meno granulari dei microservizi. Enterprise Service Bus (ESB) per orchestrazione.

### **Event-Driven Architecture (EDA)**
Sistema basato su produzione, rilevamento e reazione a eventi. Componenti loosely coupled comunicano tramite eventi asincroni. Utilizza event bus, message brokers (Kafka, RabbitMQ). Ottima per sistemi real-time e scalabili.

### **CQRS (Command Query Responsibility Segregation)**
Separa le operazioni di lettura (query) da quelle di scrittura (command). Modelli di dati ottimizzati separatamente per read e write. Spesso combinato con Event Sourcing. Migliora performance e scalabilità.

### **Event Sourcing**
Memorizza lo stato come sequenza di eventi invece di snapshot. Ogni cambiamento è un evento immutabile. Permette audit completo, time-travel e ricostruzione dello stato. Spesso usato con CQRS.

### **Serverless Architecture**
Esecuzione di codice senza gestire server (FaaS - Function as a Service). Scaling automatico, pay-per-use. Focus su business logic, infrastruttura gestita dal provider (AWS Lambda, Azure Functions).

### **Peer-to-Peer Architecture (P2P)**
Rete decentralizzata dove ogni nodo è client e server. Nessun server centrale, dati distribuiti. Resistente a guasti, scalabile. Usato in blockchain, file sharing (BitTorrent), sistemi distribuiti.

## Pattern Architetturali

### **Layered Architecture (N-Tier)**
Organizza l'applicazione in layer orizzontali: Presentation, Business Logic, Data Access, Database. Ogni layer comunica solo con quello adiacente. Semplice da implementare, ma può creare dipendenze rigide.

### **Microkernel Architecture (Plugin Architecture)**
Core system minimo con funzionalità estese tramite plugin. Il core fornisce API per i plugin che implementano feature specifiche. Flessibile ed estendibile (IDE, CMS, browser).

### **Space-Based Architecture**
Elimina il database centrale come bottleneck. Dati replicati in-memory tra processing units. Scalabilità orizzontale virtualmente illimitata. Ideale per applicazioni ad alto traffico con picchi imprevedibili.

### **Pipes and Filters**
Elaborazione dati tramite sequenza di componenti (filters) connessi da pipes. Ogni filter trasforma i dati e li passa al successivo. Riutilizzabile, testabile. Comune in data processing e compilatori.

### **Master-Slave (Primary-Replica)**
Pattern dove un nodo master coordina molteplici nodi slave. Master gestisce scritture, slave gestiscono letture. Replica dati per fault tolerance e load balancing. Comune in database distribuiti.

### **Broker Pattern**
Intermediario che coordina comunicazione tra componenti distribuiti. Disaccoppia client e server, gestisce marshalling/unmarshalling. Utilizzato in middleware, CORBA, sistemi distribuiti enterprise.

### **Blackboard Pattern**
Sistema dove specialisti multipli collaborano su spazio condiviso (blackboard). Nessun controllo centralizzato, componenti reagiscono a cambiamenti. Usato per problemi complessi senza strategia deterministica (AI, riconoscimento pattern).

### **Interpreter Pattern (Architetturale)**
Definisce rappresentazione grammatica per linguaggio specifico del dominio (DSL). Interprete processa ed esegue istruzioni. Usato in query languages, configuration languages, rule engines.

## Design Pattern (Gang of Four)

### **Creational Patterns**
- **Singleton**: Garantisce una sola istanza di una classe
- **Factory Method**: Delega la creazione di oggetti alle sottoclassi
- **Abstract Factory**: Crea famiglie di oggetti correlati
- **Builder**: Costruisce oggetti complessi step-by-step
- **Prototype**: Clona oggetti esistenti invece di crearli da zero

### **Structural Patterns**
- **Adapter**: Converte un'interfaccia in un'altra
- **Bridge**: Separa astrazione da implementazione
- **Composite**: Tratta oggetti singoli e composizioni uniformemente
- **Decorator**: Aggiunge responsabilità dinamicamente
- **Facade**: Interfaccia semplificata per sistema complesso
- **Flyweight**: Condivide oggetti per ridurre memoria con dati comuni
- **Proxy**: Placeholder per controllare accesso a un oggetto

### **Behavioral Patterns**
- **Observer**: Notifica automatica ai dipendenti quando cambia lo stato
- **Strategy**: Incapsula algoritmi intercambiabili
- **Command**: Incapsula richieste come oggetti
- **State**: Cambia comportamento in base allo stato interno
- **Template Method**: Definisce scheletro di algoritmo, sottoclassi implementano step
- **Iterator**: Accesso sequenziale senza esporre rappresentazione
- **Mediator**: Centralizza comunicazione tra oggetti
- **Chain of Responsibility**: Passa richiesta lungo catena di handler
- **Visitor**: Aggiunge operazioni a strutture senza modificarle
- **Memento**: Cattura e ripristina stato interno di un oggetto
- **Interpreter**: Definisce grammatica e interprete per un linguaggio

## Approcci Moderni

### **Jamstack Architecture**
JavaScript, APIs, Markup. Frontend statico pre-renderizzato, backend via API. Deploy su CDN, performance eccellenti, sicurezza migliorata. Ottimo per siti content-heavy.

### **Micro Frontend Architecture**
Estende concetto microservizi al frontend. Ogni team possiede feature end-to-end. Frontend composto da frammenti indipendenti. Autonomia e scalabilità team.

### **Backend for Frontend (BFF)**
Layer backend dedicato per ogni tipo di client (web, mobile, IoT). Ogni BFF ottimizza dati e logica per il proprio frontend. Riduce coupling tra frontend e backend services.

### **Reactive Architecture**
Sistema responsive, resilient, elastic, message-driven. Basato su Reactive Manifesto. Programmazione asincrona, non-blocking. Gestione efficiente di carichi elevati.

### **Actor Model**
Modello di concorrenza dove "actors" sono unità fondamentali. Ogni actor ha mailbox, processa messaggi sequenzialmente, può creare altri actors. Nessun stato condiviso. Usato in Akka, Erlang/OTP.

## Pattern per Microservizi

### **API Gateway Pattern**
Single entry point per i client. Instrada richieste ai microservizi appropriati. Gestisce cross-cutting concerns: autenticazione, rate limiting, logging. Semplifica client, centralizza logica comune.

### **Saga Pattern**
Gestisce transazioni distribuite senza 2PC. Sequenza di transazioni locali coordinate da eventi o orchestrazione. Compensation logic per rollback. Due tipologie: choreography (eventi) e orchestration (coordinatore centrale).

### **Circuit Breaker Pattern**
Previene cascading failures in sistemi distribuiti. Monitora chiamate a servizi esterni. Stati: Closed (normale), Open (fallimenti), Half-Open (test ripristino). Fallback rapido quando servizio è down.

### **Strangler Fig Pattern**
Strategia di migrazione graduale da sistema legacy. Nuove funzionalità implementate in nuovi servizi. Routing progressivo dal legacy al nuovo. Riduce rischio, permette rollback incrementale.

### **Service Mesh**
Infrastruttura dedicata per comunicazione service-to-service. Gestisce discovery, load balancing, encryption, observability. Separazione tra logica business e comunicazione. Esempi: Istio, Linkerd.

### **Sidecar Pattern**
Container aggiuntivo che estende funzionalità container principale. Logging, monitoring, proxy, configuration. Deploy insieme all'applicazione. Separa cross-cutting concerns dalla business logic.

### **Ambassador Pattern**
Proxy che gestisce connessioni di rete per conto del servizio. Offload di retry logic, circuit breaking, logging. Semplifica client, centralizza logica di connessione.

### **Retry Pattern**
Gestisce fallimenti transienti riprovando operazione. Configura numero tentativi, backoff strategy (exponential, linear). Migliora resilienza in reti inaffidabili.

### **Bulkhead Pattern**
Isola risorse per prevenire cascading failures. Separa connection pools, thread pools per servizi diversi. Se un servizio fallisce, altri continuano. Migliora fault tolerance.

## Principi di Design

### **SOLID Principles**
- **S**ingle Responsibility: Una classe = una responsabilità
- **O**pen/Closed: Aperto all'estensione, chiuso alla modifica
- **L**iskov Substitution: Sottotipi sostituibili al tipo base
- **I**nterface Segregation: Interfacce specifiche, non generiche
- **D**ependency Inversion: Dipendere da astrazioni, non concrete

### **DRY (Don't Repeat Yourself)**
Evita duplicazione di logica. Ogni conoscenza deve avere rappresentazione unica, autorevole, non ambigua nel sistema.

### **KISS (Keep It Simple, Stupid)**
Semplicità come obiettivo primario. Evita complessità non necessaria. Soluzioni semplici sono più mantenibili.

### **YAGNI (You Aren't Gonna Need It)**
Non implementare funzionalità finché non servono realmente. Evita over-engineering e codice inutilizzato.

### **Separation of Concerns**
Separa programma in sezioni distinte, ognuna affronta una preoccupazione specifica. Riduce coupling, aumenta coesione.

### **Dependency Injection**
Pattern dove dipendenze sono fornite dall'esterno invece che create internamente. Migliora testabilità e flessibilità. Facilita inversione del controllo (IoC).

### **Repository Pattern**
Astrae accesso ai dati simulando collection in-memory. Separa logica business da persistenza. Interfaccia per operazioni CRUD. Fondamentale in DDD per aggregates.

### **Unit of Work Pattern**
Mantiene lista di oggetti modificati durante transazione business. Coordina scrittura cambiamenti e risolve problemi concorrenza. Spesso usato con Repository Pattern.

### **Law of Demeter (Principle of Least Knowledge)**
Oggetto dovrebbe comunicare solo con "amici diretti". Riduce coupling. Regola: usa solo metodi di: (1) oggetto stesso, (2) parametri, (3) oggetti creati, (4) attributi diretti.

### **Composition Over Inheritance**
Preferisci composizione di oggetti a ereditarietà di classi. Più flessibile, evita gerarchie rigide. Facilita riuso e cambio comportamento a runtime.

## Approcci Data-Centric

### **Data Mesh**
Architettura dati decentralizzata. Ogni dominio possiede i propri dati. Data as a product. Federated governance. Alternativa a data warehouse/lake centralizzato.

### **Lambda Architecture**
Combina batch processing e real-time streaming. Batch layer (accuratezza), speed layer (latenza bassa), serving layer (query). Gestisce big data con trade-off latenza/accuratezza.

### **Kappa Architecture**
Semplificazione di Lambda, solo stream processing. Tutti i dati come stream. Riprocessing tramite replay. Più semplice da mantenere rispetto a Lambda.

## Metodologie di Sviluppo

### **Waterfall**
Metodologia sequenziale lineare. Fasi: Requirements → Design → Implementation → Testing → Deployment → Maintenance. Ogni fase completata prima della successiva. Adatto per progetti con requisiti stabili e ben definiti.

### **Agile**
Filosofia iterativa e incrementale. Sviluppo in cicli brevi (sprint), feedback continuo, adattamento al cambiamento. Valori: individui e interazioni, software funzionante, collaborazione col cliente, risposta al cambiamento.

### **Scrum**
Framework Agile con ruoli definiti: Product Owner, Scrum Master, Development Team. Sprint di 1-4 settimane, Daily Standup, Sprint Planning, Review, Retrospective. Backlog prioritizzato, incrementi potenzialmente rilasciabili.

### **Kanban**
Visualizza flusso di lavoro su board (To Do, In Progress, Done). WIP (Work In Progress) limits per evitare sovraccarico. Flusso continuo, pull system. Focus su efficienza e riduzione bottleneck.

### **Extreme Programming (XP)**
Pratiche tecniche per qualità: pair programming, TDD, continuous integration, refactoring continuo, simple design, collective code ownership. Rilasci frequenti, piccoli incrementi.

### **Lean Software Development**
Principi dal Lean Manufacturing. Elimina sprechi, amplifica apprendimento, decide il più tardi possibile, consegna veloce, empowerment team, build quality in, ottimizza il tutto.

### **SAFe (Scaled Agile Framework)**
Framework per applicare Agile a grandi organizzazioni. Livelli: Team, Program, Large Solution, Portfolio. Coordina team multipli, allineamento strategico, rilasci sincronizzati (Program Increment).

### **Feature-Driven Development (FDD)**
Sviluppo guidato da feature business-oriented. Fasi: sviluppa modello, build feature list, plan by feature, design by feature, build by feature. Iterazioni brevi (1-2 settimane), feature come unità di lavoro.

### **Crystal**
Famiglia di metodologie Agile (Clear, Yellow, Orange, Red) basate su dimensione team e criticità progetto. Enfasi su comunicazione, collaborazione, riflessione. Leggero, adattabile.

### **DSDM (Dynamic Systems Development Method)**
Framework Agile timeboxed. Principi: focus su business need, consegna in tempo, collaborazione, mai compromettere qualità, incrementale, reversibilità, requisiti high-level. MoSCoW prioritization.

### **Rational Unified Process (RUP)**
Processo iterativo risk-driven. Fasi: Inception, Elaboration, Construction, Transition. Discipline parallele (requirements, analysis, design, implementation, test). Use-case driven, architecture-centric.

### **Test-Driven Development (TDD)**
Ciclo Red-Green-Refactor. Scrivi test prima del codice. Test fallisce (Red), implementi codice minimo (Green), refactor. Migliora design, aumenta coverage, documenta comportamento.

### **Behavior-Driven Development (BDD)**
Estende TDD con focus su comportamento. Scenari scritti in linguaggio naturale (Given-When-Then). Collaborazione tra business e tech. Framework: Cucumber, SpecFlow.

### **Feature Toggle (Feature Flag)**
Tecnica per abilitare/disabilitare funzionalità senza deploy. Permette: rilasci graduali, A/B testing, kill switches. Separa deploy da release. Riduce rischio nuove feature.

## Principi Cloud-Native

### **Twelve-Factor App**
Metodologia per app cloud-native. Principi: codebase unico, dipendenze esplicite, config in environment, backing services come risorse, build/release/run separati, stateless processes, port binding, concurrency via processi, disposability, dev/prod parity, logs come stream, admin processes.

### **CAP Theorem**
In sistemi distribuiti, puoi garantire solo 2 su 3: Consistency (consistenza), Availability (disponibilità), Partition tolerance (tolleranza partizioni). Scelta architettuale fondamentale per database distribuiti.

### **BASE (Basically Available, Soft state, Eventually consistent)**
Alternativa ad ACID per sistemi distribuiti. Accetta inconsistenza temporanea per disponibilità. Eventual consistency invece di strong consistency. Usato in NoSQL, microservizi.

## Enterprise Integration Patterns

### **Message Broker Pattern**
Intermediario per comunicazione asincrona tra sistemi. Disaccoppia producer e consumer. Code, topic, routing. Esempi: RabbitMQ, Apache Kafka, AWS SQS.

### **Publish-Subscribe Pattern**
Publisher emette messaggi a topic, subscriber ricevono copie. Disaccoppiamento molti-a-molti. Scalabile, flessibile. Usato in sistemi event-driven.

### **Request-Reply Pattern**
Comunicazione sincrona con correlazione richiesta-risposta. Client invia richiesta e attende risposta. Usato in RPC, REST API, message brokers con reply-to queue.

### **Content-Based Router**
Instrada messaggi a destinazioni diverse basandosi sul contenuto. Decision logic centralizzata. Flessibilità nel routing. Comune in ESB, integration middleware.

## Anti-Pattern (Da Evitare)

### **God Object**
Oggetto che sa/fa troppo. Viola Single Responsibility. Difficile da testare e mantenere. Sintomo di poor design.

### **Spaghetti Code**
Codice con flusso di controllo complesso e intrecciato. Difficile da seguire, debug, modificare. Mancanza di struttura chiara.

### **Big Ball of Mud**
Sistema senza architettura riconoscibile. Crescita caotica senza design. Alto coupling, bassa coesione. Debito tecnico estremo.

### **Golden Hammer**
Applicare stessa soluzione/tecnologia a ogni problema. "Se hai solo un martello, tutto sembra un chiodo". Ignora alternative più appropriate.

### **Premature Optimization**
Ottimizzare prima di misurare necessità reale. Spreco tempo, complica codice. Meglio: funziona → misura → ottimizza se necessario.

### **Cargo Cult Programming**
Copiare pattern/codice senza capirli. Rituali senza comprensione. Codice inutile o dannoso. Imparare il "perché" non solo il "cosa".
