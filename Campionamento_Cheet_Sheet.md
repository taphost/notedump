
> # 🎛️ Cheat Sheet — Campionamento & Analisi in Frequenza

## 🧩 1. Concetti di base
Il campionamento è il processo che trasforma un segnale continuo nel tempo in una sequenza discreta di valori numerici.  
I passaggi fondamentali sono:
1. **Campionamento** — scegliere istanti regolari nel tempo e registrare il valore del segnale.  
2. **Quantizzazione** — approssimare ogni valore campionato a un livello discreto.  
3. **Codifica** — rappresentare questi livelli come numeri binari.

---

## 🔹 2. Teorema di Shannon–Nyquist
Per rappresentare correttamente un segnale, la frequenza di campionamento deve essere almeno il doppio della massima frequenza presente nel segnale.  
Se non si rispetta questa condizione, le componenti più alte si “ripiegano” in frequenze più basse generando **aliasing**, cioè distorsioni non correggibili.

---

## 🔹 3. Quantizzazione (PCM)
La quantizzazione trasforma i valori continui dei campioni in una serie di livelli discreti.  
Ogni livello viene codificato con un numero binario.  
Un numero maggiore di bit consente una rappresentazione più fedele e un rumore di quantizzazione più basso.  
Questo rumore è inevitabile, ma può essere ridotto aumentando la risoluzione (più bit per campione).

---

## 🔹 4. Serie e Trasformate di Fourier

| Tipo | Dominio del segnale | Tipo di spettro | Descrizione sintetica |
|------|---------------------|-----------------|------------------------|
| **Serie di Fourier** | Segnali periodici continui | Discreto | Rappresenta un segnale come somma di sinusoidi armoniche. |
| **Trasformata di Fourier (FT)** | Segnali non periodici continui | Continuo | Mostra la distribuzione delle frequenze presenti in un segnale. |
| **Trasformata Discreta di Fourier (DFT)** | Segnali digitali e finiti | Discreto e periodico | Analizza frequenze in dati campionati. |
| **FFT** | — | — | Algoritmo che calcola la DFT in modo molto più veloce. |

---

## 🔹 5. Catena logica del segnale

Segnale analogico continuo ↓ Campionamento (secondo Shannon–Nyquist) Segnale discreto nel tempo ↓ Quantizzazione (PCM) Segnale digitale (sequenza di bit) ↓ Analisi in frequenza (DFT / FFT) Risultato: spettro del segnale nel dominio della frequenza

---

## 🔹 6. Relazioni chiave

| Concetto | Tipo di operazione | Dominio | Legame con gli altri |
|-----------|--------------------|----------|----------------------|
| Campionamento | Temporale | Tempo → Discreto | Base per ogni elaborazione digitale |
| Quantizzazione | Sull’ampiezza | Ampiezza → Discreta | Crea il segnale digitale da numerico |
| Fourier | Analisi matematica | Tempo ↔ Frequenza | Permette di capire “cosa c’è” in frequenza |
| Shannon–Nyquist | Teorema fondamentale | Tempo/Frequenza | Definisce il limite minimo di campionamento |
| FFT | Algoritmo numerico | Frequenza discreta | Rende praticabile l’analisi spettrale |

---

## 📘 7. Note pratiche
- L’audio CD usa una frequenza di 44.1 kHz, che consente di rappresentare frequenze fino a circa 22 kHz, in linea con la sensibilità uditiva umana.  
- Nei video digitali, la quantizzazione tipica è di 8 o 10 bit per canale di colore.  
- La FFT è impiegata in moltissimi ambiti: analisi spettrale audio, compressione di dati (MP3, JPEG), elaborazione di immagini e riconoscimento di frequenze.

---

## 🧮 8. Riassunto rapido

| Processo | Tipo | Descrizione essenziale |
|-----------|------|------------------------|
| Campionamento | Temporale | Registra valori del segnale a intervalli costanti |
| Quantizzazione | Ampiezza | Arrotonda i valori a livelli discreti |
| Serie di Fourier | Periodico | Decompone un segnale in armoniche |
| Trasformata di Fourier | Non periodico | Analizza contenuto in frequenza continuo |
| DFT | Digitale | Analizza frequenze in segnali campionati e finiti |
| FFT | — | Metodo rapido per calcolare la DFT |

---
