## JS Approaches — Ultimate Cheatsheet

---

## 🎯 1. Imperativo vs Dichiarativo

| Approccio | Pro | Contro | 🚫 Non usare quando |
|----------|------|---------|----------------------|
| **🔧 Imperativo (DOM diretto)** | ✔️ Controllo totale<br>✔️ Zero magia<br>✔️ Perfetto per micro‑script | ❌ Fragile<br>❌ Più bug<br>❌ Hard da mantenere | ❗ App medie/grandi<br>❗ UI dinamica<br>❗ Team multipli |
| **🎨 Dichiarativo (React/Svelte/Vue)** | ✔️ Codice chiaro<br>✔️ Stato → UI<br>✔️ Meno errori | ❌ Overhead<br>❌ Debug indiretto | ❗ Widget singoli<br>❗ Script inline |

**⚠️ Evita di incrociare:** DOM diretto + framework → ❌ desync + stati inconsistenti.

---

## 🧠 2. OOP vs Funzionale

| Approccio | Pro | Contro | 🚫 Non usare quando |
|----------|------|---------|----------------------|
| **🏛️ OOP** | ✔️ Concetti familiari<br>✔️ Encapsulazione | ❌ Mutabilità pesante<br>❌ Overengineering | ❗ Stream, reattività, immutabilità |
| **🧬 Funzionale** | ✔️ Prevedibile<br>✔️ Testabile<br>✔️ Meno side‑effects | ❌ Più verboso | ❗ Sistemi a oggetti complessi |

---

## ⏳ 3. Sincrono vs Asincrono

| Approccio | Pro | Contro | 🚫 Non usare quando |
|----------|------|---------|----------------------|
| **⚙️ Sincrono** | ✔️ Semplice | ❌ Blocca il thread | ❗ Operazioni lente |
| **⏱️ Asincrono (async/await)** | ✔️ Non blocca<br>✔️ Scalabile | ❌ Debug complesso | ❗ Logiche strettamente sequenziali |

---

## 🔔 4. Event‑Driven

| Pro | Contro | 🚫 Non usare quando |
|-----|--------|----------------------|
| ✔️ Perfetto per UI<br>✔️ Naturale in JS | ❌ Stato sparso | ❗ Architetture grosse senza stato centralizzato |

---

## ⚡ 5. Reattivo (Signals, Svelte, RxJS)

| Pro | Contro | 🚫 Non usare quando |
|-----|--------|----------------------|
| ✔️ Aggiornamenti auto<br>✔️ Prestazioni ottime | ❌ Curva mentale<br>❌ Debug flussi | ❗ Script piccoli<br>❗ Senza stato dinamico |

---

## 🔄 6. Data Binding

| Approccio | Pro | Contro | 🚫 Non usare quando |
|----------|------|---------|----------------------|
| **➡️ One‑way** | ✔️ Prevedibile | ❌ Più codice | ❗ Form complessi |
| **↔️ Two‑way** | ✔️ Comodo | ❌ Loop<br>❌ Stato ambiguo | ❗ Stato globale condiviso |

---

## 🧩 7. Component‑Based

| Pro | Contro | 🚫 Non usare quando |
|-----|--------|----------------------|
| ✔️ Modulare<br>✔️ Riutilizzabile | ❌ Struttura overhead | ❗ Script minuscoli |

---

## 🌍 8. Rendering (CSR, SSR, Islands)

| Tipo | Pro | Contro | 🚫 Non usare quando |
|------|------|---------|----------------------|
| **🖥️ CSR** | UX dinamica | SEO debole | Siti informativi |
| **🌐 SSR** | SEO top | Hydration pesante | App client‑heavy |
| **🏝️ Islands** | Performance top | Setup complesso | Mini‑progetti |

---

## 🗃️ 9. State Management

| Pro | Contro | 🚫 Non usare quando |
|-----|--------|----------------------|
| ✔️ Chiarezza<br>✔️ Scalabilità | ❌ Boilerplate | ❗ App piccole |

---

# 🚫 Cosa NON incrociare mai

| Combinazione | Perché | Risultato |
|--------------|--------|-----------|
| ❌ DOM diretto + React/Svelte | Bypass del Virtual DOM | Desync totale |
| ❌ Two‑way + stato globale | Loop di update | CPU 100% |
| ❌ Redux + MobX/Signals | Stato duplicato | Incoerenze |
| ❌ OOP mutabile + Reattivo | Cambiamenti non tracciati | Bug sporadici |
| ❌ SSR + manipolazione DOM | Hydration mismatch | UI corrotta |
| ❌ Eventi multipli + async non controllato | Race condition | Stato random |

---

# 🧨 Cause principali dei conflitti
- Mutabilità incontrollata  
- Stato duplicato in più sistemi  
- Uso misto di paradigmi incompatibili  
- Dom diretto dentro architetture dichiarative  
- Eventi non centralizzati  
- Async non sincronizzato  
- Hydration + modifiche manuali  

---

# ⭐ Regole d’Oro
- Scegli **un solo** modello di stato.  
- Usa immutabilità *se c’è reattività*.  
- Non toccare il DOM se usi framework.  
- Evita sistemi “magici” sovrapposti.  
- Mantieni i componenti **piccoli**.  

---

# 🎁 Extra: Color Legend
- ✔️ **Pro**
- ❌ **Contro**
- ❗ **Da evitare**
- ⚠️ **Warning critico**
