# Pattern di State Management

## Come Leggere Questo Documento

Questo cheatsheet copre 4 livelli interconnessi di state management:

### **1. Tipi di Stato** (COSA)
Definisce la **natura** dello stato: dove vive, quanto persiste, chi può accedervi.
- Esempio: Local, Global, Persistent

### **2. Pattern Design (GOF)** (COME - Tattico)
Soluzioni **riutilizzabili** a problemi specifici di gestione stato.
- Esempio: Observer notifica cambiamenti, Singleton garantisce istanza unica

### **3. Pattern Architetturali** (COME - Strategico)
**Combinazioni** di pattern GOF che definiscono la struttura dell'intera app.
- Esempio: Redux = Singleton (store) + Observer (subscriptions) + Command (actions)

### **4. Implementazioni Framework** (STRUMENTI)
Librerie e API concrete che **applicano** i pattern architetturali.
- Esempio: Zustand implementa pattern Observer con API React hooks

### **Relazioni:**
```
Tipi di Stato <--> Pattern GOF <--> Pattern Architetturali <--> Framework
    |                |                    |                      |
  Global        Singleton              Redux              Redux Toolkit
  Shared        Observer               Flux               Zustand
  Local         Command                MVC                React Hooks
```

**Esempio pratico:**
Un'app React con autenticazione potrebbe usare:
- **Shared State** (tipo) per dati utente
- **Observer** (pattern) per notificare componenti
- **Context API** (architettura) per propagare stato
- **useContext** (framework) come implementazione concreta

---

## Tipi di Stato

### 1. **Local State (Stato Locale)**
- Limitato a funzione, blocco o componente
- Non accessibile dall'esterno
- Esempio: variabili locali, `useState` in React

### 2. **Shared State (Stato Condiviso)**
- Accessibile da più parti del codice
- Richiede meccanismi di sincronizzazione
- Esempio: Context API, store Redux condiviso

### 3. **Global State (Stato Globale)**
- Accessibile ovunque nell'applicazione
- Potenziale fonte di accoppiamento
- Esempio: Singleton, variabili globali

### 4. **Persistent State (Stato Persistente)**
- Salvato su disco, database o storage
- Sopravvive alla chiusura dell'app
- Esempio: localStorage, database

### 5. **Ephemeral State (Stato Effimero)**
- Esiste solo in memoria durante l'esecuzione
- Si perde al riavvio
- Esempio: cache in-memory, stato UI temporaneo

---

## Pattern Creazionali

### **Singleton**
**Scopo:** Garantire una sola istanza globale dello stato

**Caratteristiche:**
- Usa metodo statico `getInstance()` per controllare creazione
- Previene istanziazioni multiple tramite controllo interno
- Inizializzazione lazy (solo quando necessario)

**Pro:** Accesso globale, inizializzazione lazy  
**Contro:** Testing difficile, accoppiamento globale, viola Single Responsibility Principle

---

### **Prototype**
**Scopo:** Clonare stati esistenti invece di crearli da zero

**Tecniche di cloning:**
- **Shallow clone:** Copia solo il primo livello (spread operator, Object.assign)
- **Deep clone:** Copia ricorsiva di tutti i livelli annidati (structuredClone, librerie)

**Pro:** Performance migliori, immutabilità facilitata  
**Contro:** Deep clone può essere costoso, problemi con riferimenti circolari

---

## Pattern Strutturali

### **Flyweight**
**Scopo:** Condividere dati comuni per ridurre memoria

**Componenti:**
- **Intrinsic state:** Dati condivisi e immutabili
- **Extrinsic state:** Dati specifici del contesto
- **Factory:** Cache per gestire istanze condivise

**Esempio d'uso:** Editor di testo (condivisione font/dimensione caratteri)

**Pro:** Risparmio memoria significativo, scalabilità  
**Contro:** Complessità aumentata, overhead gestione factory

---

### **Proxy**
**Scopo:** Controllare accesso e modifiche allo stato

**Funzionalità:**
- Intercettare operazioni get/set
- Validazione, logging, lazy loading
- Notifiche di cambiamento

**Pro:** Controllo granulare, separazione concerns  
**Contro:** Overhead performance, debugging più complesso

---

### **Memento**
**Scopo:** Salvare snapshot dello stato per undo/redo

**Componenti:**
- **Memento:** Oggetto che memorizza lo snapshot
- **Originator:** Oggetto che crea/ripristina memento
- **Caretaker:** Gestisce la cronologia dei memento

**Pro:** Time-travel debugging, undo/redo, history tracking  
**Contro:** Memoria occupata dalla history, può rallentare con stati grandi

---

## Pattern Comportamentali

### **Observer (Pub/Sub)**
**Scopo:** Notificare automaticamente i cambiamenti di stato

**Componenti:**
- **Subject/Observable:** Mantiene lista observers
- **Observer:** Riceve notifiche
- **subscribe/unsubscribe:** Gestione registrazione

**Pro:** Decoupling, reattività, molti-a-molti  
**Contro:** Debug difficile, memory leaks se non si unsubscribe, ordine notifiche non garantito

---

### **State Pattern**
**Scopo:** Cambiare comportamento in base allo stato corrente

**Componenti:**
- **State classes:** Ogni stato incapsula il proprio comportamento
- **Context:** Mantiene riferimento allo stato corrente
- **Transizioni:** Gestite dalle classi stato

**Pro:** Logica separata per stato, estendibile, evita conditionals  
**Contro:** Molte classi da gestire, overhead per stati semplici

---

### **Command**
**Scopo:** Incapsulare modifiche di stato come oggetti

**Componenti:**
- **Command:** Interfaccia con execute() e undo()
- **Concrete Commands:** Implementazioni specifiche
- **Invoker:** Esegue i comandi
- **Receiver:** Oggetto target delle operazioni

**Pro:** Undo/redo, macro commands, queueing, logging  
**Contro:** Overhead per operazioni semplici, molte classi

---

## Pattern Architetturali

### **Flux/Redux**
**Scopo:** Flusso unidirezionale con store centralizzato

**Flusso:** View -> Action -> Dispatcher -> Reducer -> Store -> View

**Componenti:**
- **Actions:** Oggetti che descrivono eventi
- **Reducers:** Pure functions che modificano stato
- **Store:** Single source of truth
- **Middleware:** Logica asincrona/side effects

**Pro:** Prevedibilità, time-travel debug, DevTools  
**Contro:** Boilerplate significativo, curva di apprendimento

---

### **MVC (Model-View-Controller)**
**Scopo:** Separare dati, presentazione e logica

**Componenti:**
- **Model:** Dati e logica business
- **View:** Presentazione UI
- **Controller:** Gestisce input e coordina Model/View

**Pro:** Separazione responsabilità, testabilità, riusabilità  
**Contro:** Può diventare complesso, coupling tra componenti

---

### **MVVM (Model-View-ViewModel)**
**Scopo:** Binding bidirezionale tra View e ViewModel

**Componenti:**
- **Model:** Dati business
- **View:** UI dichiarativa
- **ViewModel:** Espone dati e comandi per la View

**Differenza da MVC:** Two-way data binding automatico

**Pro:** Separazione UI/logica, testabilità ViewModel  
**Contro:** Complessità binding, debugging, learning curve

---

### **Event Sourcing**
**Scopo:** Memorizzare eventi invece dello stato finale

**Concetti:**
- **Event Store:** Append-only log di eventi
- **Replay:** Ricostruisce stato da eventi
- **Projection:** Vista materializzata dello stato

**Pro:** Audit trail completo, time-travel, debugging, analytics  
**Contro:** Storage aumentato, complessità query, eventual consistency

---

### **CQRS (Command Query Responsibility Segregation)**
**Scopo:** Separare lettura (Query) e scrittura (Command)

**Componenti:**
- **Write Model:** Ottimizzato per scritture/validazioni
- **Read Model:** Ottimizzato per query/performance
- **Sincronizzazione:** Tramite eventi (spesso con Event Sourcing)

**Pro:** Scalabilità indipendente, ottimizzazione separata  
**Contro:** Eventual consistency, complessità infrastruttura

---

## Pattern Moderni (Framework-Specific)

### **React - Context API**
**Scopo:** Stato condiviso senza prop drilling

**Caratteristiche:**
- Provider/Consumer pattern
- Integrato in React
- Ideale per temi, auth, i18n

**Pro:** Nativo React, semplice, no librerie esterne  
**Contro:** Re-render di tutti i consumer, non ottimizzato per aggiornamenti frequenti

---

### **React - Hooks (useState, useReducer)**
**Scopo:** Stato locale reattivo nei componenti

**useState:**
- Stato semplice
- API minimale

**useReducer:**
- Stato complesso con logica
- Pattern Redux-like locale

**Pro:** Semplice, composable, reattivo  
**Contro:** Solo locale, non condivisibile tra componenti non correlati

---

### **Atom/Signal Pattern (Jotai, Recoil, Solid)**
**Scopo:** Stato granulare e reattivo

**Caratteristiche:**
- Atomic state units
- Computed values automatici
- Fine-grained reactivity
- Subscriptions ottimizzate

**Pro:** Performance eccellenti, composable, no boilerplate  
**Contro:** Nuovo paradigma da imparare, ecosistema frammentato

---

### **Vue - Reactivity System**
**Scopo:** Reattività automatica con Proxy

**Caratteristiche:**
- Tracking automatico dipendenze
- Computed properties
- Watchers
- Ref/Reactive API

**Pro:** Automatic tracking, semplice, performante  
**Contro:** Solo Vue, limitazioni Proxy (IE11), magic può confondere

---

### **Zustand**
**Scopo:** Store minimale e non-opinionated

**Caratteristiche:**
- API hooks-based
- No Provider/wrapper
- Middleware support
- DevTools integration

**Pro:** Minimal boilerplate, flessibile, piccola dimensione  
**Contro:** Meno strutturato di Redux, meno convenzioni

---

### **MobX**
**Scopo:** Reattività automatica con observables

**Caratteristiche:**
- Observables automatici
- Computed values
- Reactions
- Decorators (opzionale)

**Pro:** Minimal boilerplate, reattività trasparente, curva apprendimento bassa  
**Contro:** "Magic" può nascondere complessità, meno prevedibile di Redux

---

## Confronto Rapido

| Pattern | Complessità | Scalabilità | Uso Ideale |
|---------|-------------|-------------|------------|
| **Local State** | Bassa | Bassa | Componenti isolati |
| **Context API** | Media | Media | Temi, auth, settings |
| **Redux** | Alta | Alta | App grandi, complesse |
| **MobX** | Media | Alta | Reattività automatica |
| **Zustand** | Bassa | Media | App medie, semplici |
| **Recoil/Jotai** | Media | Alta | Stato granulare |
| **Event Sourcing** | Alta | Alta | Audit, finance, CQRS |

---

## Best Practices

### 1. **Inizia Semplice**
- Usa local state finché possibile
- Solleva lo stato solo quando necessario
- Evita premature ottimizzazioni

### 2. **Immutabilità**
- Non mutare mai lo stato direttamente
- Usa spread operator o librerie (Immer)
- I reducer devono essere pure functions

### 3. **Single Source of Truth**
- Un solo posto per ogni pezzo di stato
- Deriva altri valori invece di duplicare
- Evita stato ridondante

### 4. **Normalizzazione**
- Struttura dati piatti invece che annidati
- Relazioni tramite ID invece di oggetti annidati
- Facilita aggiornamenti e query

**Esempio struttura:**
- [NO] Array con oggetti annidati duplicati
- [SI] Oggetti separati con relazioni tramite ID

### 5. **Separazione Concerns**
- UI state ≠ Server state
- Usa tools specifici (React Query/SWR per server state)
- Cache vs Stato applicazione

### 6. **Performance**
- Memoization (useMemo, useCallback, reselect)
- Code splitting per store grandi
- Selettori per evitare re-render inutili
- Lazy loading di stato non immediato

---

## Anti-Pattern da Evitare

### [NO] **Prop Drilling Eccessivo**
Passare props attraverso molti livelli -> usa Context o store globale

### [NO] **Stato Globale per Tutto**
Non tutto deve essere globale -> usa local state quando possibile

### [NO] **Mutazione Diretta**
Causa bug sottili, rompe reattività, rende difficile il debug

### [NO] **Over-Engineering**
Redux per un counter -> overkill, usa useState

### [NO] **Memory Leaks**
- Dimenticare di unsubscribe da observers
- Event listeners non rimossi
- Timers non cancellati

### [NO] **Stato Duplicato**
Mantenere stessi dati in più posti -> inconsistenze garantite

### [NO] **Nested State Troppo Profondo**
Difficile da aggiornare immutabilmente -> normalizza

---

## Quando Usare Cosa?

| Scenario | Soluzione Consigliata |
|----------|----------------------|
| Form locale | `useState` |
| Form complesso | `useReducer` |
| Tema, auth, i18n | Context API |
| App grande enterprise | Redux + Redux Toolkit |
| Server state, cache | React Query / SWR / TanStack Query |
| Real-time updates | WebSockets + Observer |
| Undo/redo | Memento / Command / Immer |
| Time-travel debug | Redux DevTools |
| Micro-frontend | Module Federation + eventi |
| App piccola/media | Zustand / Jotai |
| Reattività automatica | MobX / Vue |

---

## Criteri di Scelta

**Per app piccole (< 10 componenti):**
- useState/useReducer
- Props drilling accettabile

**Per app medie (10-50 componenti):**
- Context API per dati globali
- useState per stato locale
- Zustand/Jotai se serve più controllo

**Per app grandi (50+ componenti):**
- Redux Toolkit (predictability)
- MobX (developer experience)
- Separare UI state e Server state

**Per performance critiche:**
- Jotai/Recoil (fine-grained)
- Zustand con selettori
- Evitare Context per dati che cambiano spesso

---

## Tendenze Moderne (2024-2025)

1. **Server State Separation**
   - React Query, SWR, TanStack Query dominanti
   - Separa fetch/cache da UI state

2. **Fine-Grained Reactivity**
   - Signals (Solid, Preact, Angular)
   - Atoms (Jotai, Recoil)
   - Performance superiori

3. **Redux Simplification**
   - Redux Toolkit standard
   - RTK Query per server state
   - Meno boilerplate

4. **Framework-Specific Solutions**
   - Next.js Server Components
   - SvelteKit stores
   - Vue Pinia (sostituisce Vuex)

5. **TypeScript First**
   - Type safety nativo
   - Inference automatico
   - Meno runtime errors

---

## Glossario

- **Immutability:** Stato non modificabile direttamente
- **Pure Function:** Funzione senza side effects, stesso input -> stesso output
- **Side Effect:** Operazione che modifica stato esterno o ha effetti osservabili
- **Selector:** Funzione che estrae/deriva dati dallo stato
- **Middleware:** Layer che intercetta azioni prima che arrivino al reducer
- **Normalization:** Strutturare dati per minimizzare duplicazione
- **Hydration:** Popolare stato client con dati server
- **Rehydration:** Ripristinare stato da storage persistente
- **Optimistic Update:** Aggiornare UI prima della conferma server
- **Eventual Consistency:** Sistema diventa consistente nel tempo, non immediatamente

---

## Checklist Decisionale

Prima di scegliere una soluzione:

- [ ] Quanti componenti condivideranno lo stato?
- [ ] Quanto spesso cambierà lo stato?
- [ ] Serve time-travel debugging?
- [ ] Serve persistenza?
- [ ] Serve sincronizzazione server?
- [ ] Team ha esperienza con pattern specifici?
- [ ] Performance è critica?
- [ ] Serve type safety forte?
- [ ] App è SSR/SSG?
- [ ] Budget per learning curve?

**Regola d'oro:** Inizia con la soluzione più semplice che funziona, poi scala se necessario.
