# Cheatsheet Architetture Software

## Architetture Applicative

### Monolithic
Applicazione costruita come singola unità deployabile. Tutti i componenti (UI, business logic, data access) sono strettamente accoppiati e condividono lo stesso processo e database. Semplice da sviluppare inizialmente ma difficile da scalare e mantenere con la crescita.

### Microservices
Applicazione scomposta in servizi piccoli, autonomi e loosely coupled. Ogni microservizio gestisce un dominio specifico, ha il proprio database e può essere deployato indipendentemente. Maggiore complessità operativa ma scalabilità e flessibilità superiori.

### Service-Oriented Architecture (SOA)
Architettura enterprise con servizi riutilizzabili che comunicano tramite Enterprise Service Bus (ESB). Più pesante dei microservices, enfatizza riuso e integrazione di sistemi eterogenei. Standard come SOAP e WS-*.

### Event-Driven Architecture
Sistema basato su produzione, rilevamento e consumo di eventi. I componenti reagiscono agli eventi in modo asincrono. Ideale per sistemi reattivi, real-time e altamente disaccoppiati. Supporta scalabilità e resilienza.

### Serverless (FaaS - Function as a Service)
Esecuzione di codice event-driven senza gestire server. Il provider cloud (AWS Lambda, Azure Functions, Google Cloud Functions) gestisce infrastruttura, scaling e billing pay-per-use. Ottimo per carichi di lavoro intermittenti e event-driven.

### Layered Architecture (N-Tier)
Organizzazione in strati orizzontali: presentation layer, business logic layer, data access layer, database layer. Ogni layer comunica solo con quelli adiacenti. Separa le responsabilità ma può portare a coupling tra layer.

### Hexagonal Architecture (Ports and Adapters)
Il core business logic è isolato dalle dipendenze esterne tramite "ports" (interfacce) e "adapters" (implementazioni). Rende il dominio indipendente da framework, UI, database. Facilita testing e manutenibilità.

### Clean Architecture
Evoluzione della hexagonal, organizza il codice in cerchi concentrici: entities (core), use cases, interface adapters, frameworks. Le dipendenze puntano sempre verso l'interno. Massima separazione tra business logic e dettagli implementativi.

### CQRS (Command Query Responsibility Segregation)
Separazione tra operazioni di scrittura (Commands) e lettura (Queries). Permette di ottimizzare separatamente i due modelli, utilizzando database diversi se necessario. Spesso combinato con Event Sourcing.

### Event Sourcing
Lo stato dell'applicazione è derivato da una sequenza immutabile di eventi. Invece di salvare lo stato corrente, si salvano tutti i cambiamenti. Fornisce audit trail completo, time travel, e facilita CQRS.

### Strangler Fig Pattern
Strategia di migrazione graduale da sistema legacy a nuovo sistema. Si "strangola" progressivamente il vecchio sistema sostituendo funzionalità una alla volta. Riduce rischi rispetto a big-bang rewrite.

### Pipe and Filter
Dati processati attraverso una sequenza di componenti (filters) connessi da canali (pipes). Ogni filter trasforma i dati e li passa al successivo. Comune in data processing, Unix pipelines, e stream processing.

## Architetture di Comunicazione

### Client-Server
Separazione tra client (richiede servizi) e server (fornisce servizi). Architettura tradizionale per applicazioni web e enterprise. Server centralizza logica e dati, client presenta UI.

### Peer-to-Peer (P2P)
Nodi equivalenti che fungono sia da client che da server. Nessun punto centrale di controllo. Usato in file sharing (BitTorrent), blockchain, e sistemi distribuiti decentralizzati.

### Publish-Subscribe (Pub/Sub)
Pattern di messaggistica dove publisher inviano messaggi a topic/channel senza conoscere i subscriber. I subscriber ricevono solo messaggi dai topic a cui sono iscritti. Disaccoppia produttori e consumatori.

### Message Queue
Comunicazione asincrona tramite code di messaggi. Producer inserisce messaggi, consumer li processa. Garantisce delivery, gestisce backpressure, supporta load leveling. Esempi: RabbitMQ, Apache Kafka, AWS SQS.

### Request-Response
Pattern sincrono dove client invia richiesta e attende risposta. Semplice ma può creare coupling e latenza. Base di HTTP/REST e RPC.

### WebSocket
Comunicazione bidirezionale full-duplex su singola connessione TCP. Permette push real-time dal server senza polling. Ideale per chat, gaming, live updates.

### Service Mesh
Infrastruttura dedicata per gestire comunicazione service-to-service in microservices. Fornisce service discovery, load balancing, encryption, observability. Esempi: Istio, Linkerd.

## Architetture di Deployment e Scalabilità

### Load Balanced
Distribuzione del traffico tra multiple istanze tramite load balancer. Migliora disponibilità, performance e fault tolerance. Algoritmi: round-robin, least connections, IP hash.

### Master-Slave (Primary-Replica)
Architettura con nodo master per scritture e slave per letture. Replica automatica da master a slave. Migliora read scalability ma master rimane single point of failure.

### Multi-Master
Più nodi master che accettano scritture. Richiede conflict resolution. Maggiore disponibilità e write scalability ma complessità nella consistenza.

### Sharding
Partizionamento orizzontale dei dati su multiple istanze database. Ogni shard contiene un subset dei dati. Scala write e storage ma complica query cross-shard.

### CQRS con Read Replicas
Separazione database per comandi (write) e query (read). Multiple read replicas ottimizzate per specifici pattern di query. Eventual consistency tra write e read models.

## Architetture Cloud-Native

### Container-Based (Docker/Kubernetes)
Applicazioni pacchettizzate in container con dipendenze. Kubernetes orchestra deployment, scaling, networking. Portabilità, isolamento, efficienza risorse.

### Edge Computing
Elaborazione vicino alla fonte dati (edge devices) invece che cloud centralizzato. Riduce latency, bandwidth usage. Usato in IoT, CDN, 5G.

### Multi-Cloud
Distribuzione su più cloud provider per evitare vendor lock-in, migliorare resilienza, ottimizzare costi. Richiede astraction layer e gestione complessità.

### Hybrid Cloud
Combinazione di cloud privato on-premise e cloud pubblico. Dati sensibili on-premise, carichi variabili su cloud pubblico. Flessibilità ma complessità gestionale.

## Architetture di Sicurezza

### Zero Trust Architecture
Modello di sicurezza che non presume fiducia implicita basata su posizione network. Ogni richiesta deve essere autenticata, autorizzata e criptata indipendentemente da dove proviene. "Never trust, always verify". Microsegmentazione, least privilege access.

### Defense in Depth
Strategia multi-layer di controlli di sicurezza. Se un layer fallisce, altri forniscono protezione. Include: network security, application security, endpoint security, data security, identity management. Ridondanza nei controlli di sicurezza.

### Secure by Design
Integrazione sicurezza dall'inizio del ciclo di sviluppo, non come afterthought. Threat modeling, secure coding practices, principle of least privilege. Shift-left security.

## Architetture Dati

### Lambda Architecture
Due percorsi paralleli: batch layer (processa tutto storico, lento ma accurato) e speed layer (processa stream real-time, veloce ma approssimato). Serving layer unifica le viste.

### Kappa Architecture
Solo stream processing, elimina batch layer. Ogni dato trattato come stream event. Più semplice di Lambda ma richiede stream processor potente (es. Apache Kafka).

### Data Lake
Storage centralizzato per dati raw in formato nativo (strutturati, semi-strutturati, non strutturati). Schema-on-read. Flessibile ma può diventare "data swamp" senza governance.

### Data Warehouse
Repository strutturato per dati aggregati e ottimizzati per analytics. Schema-on-write, ETL process. Dati puliti e modellati ma meno flessibile del data lake.

### Data Mesh
Architettura decentralizzata che tratta i dati come prodotto. Ogni domain team possiede i propri dati. Federazione, self-serve infrastructure, data governance distribuita.

### OLTP vs OLAP
- **OLTP** (Online Transaction Processing): ottimizzato per transazioni frequenti, brevi, su record specifici (row-oriented)
- **OLAP** (Online Analytical Processing): ottimizzato per query complesse, aggregazioni, analisi su grandi dataset (column-oriented)

## Architetture Storage

### Object Storage
Dati memorizzati come oggetti con metadata e ID univoco. Flat address space, altamente scalabile. Ottimo per dati non strutturati (immagini, video, backup). Esempi: AWS S3, Azure Blob Storage, MinIO.

### Block Storage
Storage a basso livello che presenta volumi come blocchi raw. Usato per database, VM disks. Performance elevate, accesso diretto. Esempi: AWS EBS, SAN.

### File Storage
File system gerarchico tradizionale con directory e file. Condivisione via NFS/SMB. Accesso concorrente. Esempi: AWS EFS, Azure Files, NAS.

### Distributed File Systems
File system distribuito su multiple macchine. Fault tolerance, alta disponibilità, scalabilità. Esempi: HDFS (Hadoop), GlusterFS, Ceph.

### Content Delivery Network (CDN)
Rete distribuita di server che cacheano contenuti vicino agli utenti finali. Riduce latency, bandwidth, carico su origin server. Esempi: CloudFlare, Akamai, CloudFront.

## Architetture Database

### Multi-Tenant Database
Singolo database condiviso tra più tenant (clienti/organizzazioni). Economia di scala, gestione semplificata. Isolamento via row-level security o schema separati. Rischio di data leakage.

### Database per Tenant
Database dedicato per ogni tenant. Isolamento completo, personalizzazione, performance prevedibili. Maggiori costi e complessità gestionale. Compliance facilitato.

### Shared Database, Shared Schema
Tutti i tenant condividono tabelle con colonna tenant_id. Massima efficienza risorse ma minor isolamento.

### Shared Database, Separate Schema
Ogni tenant ha proprio schema nel database condiviso. Bilanciamento tra isolamento e costi.

### CAP Theorem Architectures
- **CP Systems** (Consistency + Partition tolerance): dati sempre consistenti anche durante network partition, sacrificando availability. Es: MongoDB, HBase
- **AP Systems** (Availability + Partition tolerance): sistema sempre disponibile, eventual consistency. Es: Cassandra, DynamoDB, Riak
- **CA Systems**: consistency + availability, non tollerano partition (solo sistemi non distribuiti)

### Eventually Consistent
Sistema che garantisce consistenza dopo un periodo, non immediatamente. Maggiore disponibilità e performance. DNS, cache distribuiti, alcuni NoSQL.

## Architetture Legacy e Classiche

### Mainframe Architecture
Sistemi centrali enterprise ad alte prestazioni. Elaborazione batch, transazioni mission-critical (banking, insurance). Affidabilità estrema, backward compatibility decennale. COBOL, DB2, CICS.

### Three-Tier Architecture
Variante specifica di layered: presentation tier (UI), application tier (business logic), data tier (database). Separazione fisica su server diversi. Standard in enterprise web applications anni '90-2000.

### Model-View-Controller (MVC)
Pattern per interfacce utente. Model (dati/business logic), View (presentazione), Controller (gestisce input, coordina). Separa concerns, facilita testing. Usato in web frameworks (Rails, Django, ASP.NET MVC).

### Model-View-ViewModel (MVVM)
Evoluzione di MVC per UI data binding. ViewModel espone dati e comandi per View. Usato in WPF, Angular, Vue.js. Facilita two-way data binding.

### Model-View-Presenter (MVP)
Variante di MVC dove Presenter gestisce logica presentazione. View è passiva. Maggiore testabilità rispetto a MVC classico.

## Architetture Frontend

### Jamstack
JavaScript, APIs, Markup prebuilt. Siti statici generati pre-deploy, serviti da CDN, con funzionalità dinamiche via API. Performance, sicurezza, scalabilità eccellenti.

### Micro-Frontend
Scomposizione frontend in pezzi autonomi sviluppabili e deployabili indipendentemente. Ogni team possiede feature end-to-end. Evita frontend monolitico.

### Server-Side Rendering (SSR)
HTML generato lato server per ogni richiesta. Migliore SEO e first contentful paint rispetto a SPA. Framework: Next.js, Nuxt.js.

### Static Site Generation (SSG)
HTML generato a build time. Massima performance e sicurezza. Ideale per contenuti che cambiano raramente. Può combinare con ISR (Incremental Static Regeneration).

### Single Page Application (SPA)
Applicazione che carica singola pagina HTML e aggiorna dinamicamente via JavaScript. Esperienza fluida simile a desktop app ma SEO e initial load possono essere sfide.

### Progressive Web App (PWA)
Web app che usa modern web capabilities per esperienza simile a native app. Service workers per offline, push notifications, installabilità. Cross-platform con singolo codebase.

## Pattern Architetturali Specifici

### SAGA Pattern
Gestione transazioni distribuite in microservices tramite sequenza di transazioni locali coordinate. Due approcci: choreography (eventi) o orchestration (coordinatore centrale).

### Circuit Breaker
Previene chiamate a servizi falliti. Tre stati: closed (normale), open (blocca chiamate dopo fallimenti), half-open (testa recovery). Migliora resilienza.

### API Gateway
Punto di ingresso unico per client verso microservices. Gestisce routing, authentication, rate limiting, request/response transformation. Esempio: Kong, AWS API Gateway.

### Backends for Frontends (BFF)
API gateway specifici per ogni tipo di client (web, mobile, IoT). Ogni BFF ottimizzato per esigenze specifiche del client. Evita API one-size-fits-all.

### Sidecar Pattern
Container helper deployato insieme al container applicativo. Fornisce funzionalità accessorie: logging, monitoring, proxy. Comune in service mesh.

### Bulkhead Pattern
Isolamento risorse per prevenire failure cascade. Partiziona thread pool, connessioni, risorse tra servizi. Un servizio fallito non degrada altri.

## Logger e Observability

### Centralized Logging
Aggregazione log da tutti i servizi in repository centrale. Permette correlazione, search, analisi. Stack ELK (Elasticsearch, Logstash, Kibana), Splunk, Datadog.

### Distributed Tracing
Tracciamento richieste attraverso sistema distribuito. Ogni operazione ha trace ID che propaga. Identifica bottleneck e latency. Strumenti: Jaeger, Zipkin, OpenTelemetry.

### Metrics & Monitoring
Collezione time-series metrics (CPU, memory, request rate, latency). Dashboard e alerting. Prometheus, Grafana, CloudWatch.

### Observability (3 Pillars)
Combinazione di logs (eventi discreti), metrics (aggregazioni numeriche), traces (richieste end-to-end). Permette di capire sistema interno da output esterno.

## Architetture Avanzate e Specializzate

### Space-Based Architecture (SBA)
Architettura basata su data grid in-memory distribuito. Elimina database centrale come bottleneck. Processing units autonomi con data replication. Scalabilità lineare ma complessità elevata. Ideale per sistemi ad alto throughput.

### Actor Model
Modello di concorrenza dove "attori" sono unità computazionali che comunicano solo via messaggi asincroni. Ogni attore ha mailbox, stato privato, single-threaded processing. Fault tolerance via supervision. Framework: Akka, Erlang/OTP, Orleans.

### Reactive Architecture
Sistemi responsive, resilient, elastic, message-driven (Reactive Manifesto). Asincroni, event-driven, back-pressure handling. Reagisce a carico, failure, domanda utente. Framework: Reactor, RxJava, Akka.

### Blockchain Architecture
Distributed ledger immutabile con consensus mechanism. Decentralizzato, trustless, transparent. Smart contracts per business logic. Usato oltre cryptocurrency: supply chain, identity, voting.

### Onion Architecture
Simile a hexagonal. Core domain al centro, dipendenze verso interno. Layer: Domain Model, Domain Services, Application Services, Infrastructure. Enfatizza domain-driven design.

### Repository Pattern
Astrazione layer tra business logic e data access. Centralizza query logic, facilita testing con mock. Nasconde dettagli persistence. Comune in DDD e enterprise apps.

### Grid Computing
Coordinazione risorse computazionali distribuite geograficamente per task complessi. Virtual supercomputer. Usato in ricerca scientifica, simulazioni. Esempi: SETI@home, Folding@home.

### Fog Computing
Layer computazionale tra edge devices e cloud. Elaborazione locale/regionale per ridurre latency, bandwidth. Complementare a edge computing. Usato in IoT industriale, smart cities.

---

## Note Finali

La scelta dell'architettura dipende da:
- **Requisiti funzionali e non funzionali**
- **Scalabilità richiesta**
- **Complessità team può gestire**
- **Time-to-market**
- **Budget e risorse**
- **Dominio applicativo**

Spesso le architetture si combinano: microservices + event-driven + CQRS, oppure serverless + pub/sub + API gateway.

L'evoluzione architetturale è normale: si può partire monolithic e migrare gradualmente a microservices quando necessario.
