
## 1. Fondamenti

### Segnali Tempo-Discreto
Un **segnale tempo-discreto** x[n] è una sequenza di valori definita solo per valori interi di n. A differenza dei segnali continui, questi esistono solo in istanti discreti e sono la base del DSP.

- **Energia**: E = Σ|x[n]|² somma su tutti i campioni. Un segnale ha energia finita se questa somma converge. Tipico per segnali transienti.
- **Potenza**: P = lim(1/N)Σ|x[n]|² potenza media su un intervallo infinito. Utile per segnali periodici o aleatori che non hanno energia finita.

**Segnali fondamentali**:
- **Impulso unitario** δ[n]: vale 1 per n=0, zero altrove. È l'identità della convoluzione e permette di "campionare" valori.
- **Gradino** u[n]: vale 1 per n≥0, zero per n<0. Integrale discreto dell'impulso.
- **Esponenziale complesso** e^(jωn): base per l'analisi in frequenza, autofunzione dei sistemi LTI.

### Sistemi LTI (Lineari Tempo-Invarianti)
I sistemi LTI sono la classe più importante in DSP perché completamente caratterizzabili dalla risposta impulsiva h[n].

**Proprietà fondamentali**:
- **Linearità**: α₁x₁[n] + α₂x₂[n] → α₁y₁[n] + α₂y₂[n] (sovrapposizione degli effetti)
- **Tempo-invarianza**: se x[n] → y[n], allora x[n-k] → y[n-k] (comportamento costante nel tempo)

**Convoluzione**: y[n] = x[n] * h[n] = Σ x[k]h[n-k]
- Operazione fondamentale che descrive come il sistema trasforma l'input
- Interpretazione: ogni campione di output è combinazione pesata di input passati
- Commutativa: x*h = h*x (posso scambiare ruolo di segnale e sistema)
- Associativa: (x*h₁)*h₂ = x*(h₁*h₂) (cascata di sistemi)

**Risposta impulsiva** h[n]: output quando input è δ[n]. Caratterizza completamente il sistema LTI perché ogni segnale può essere scritto come somma di impulsi traslati e scalati.

**Stabilità BIBO** (Bounded-Input Bounded-Output): 
- Condizione: Σ|h[n]| < ∞ (h[n] assolutamente sommabile)
- Garantisce che input limitato → output limitato
- Critica per implementazioni pratiche

**Causalità**: h[n] = 0 per n < 0
- Il sistema non usa valori futuri dell'input
- Necessaria per elaborazione real-time

## 2. Trasformata z

La trasformata z è l'equivalente discreto della trasformata di Laplace e fornisce strumenti potenti per analizzare sistemi discreti nel dominio complesso.

### Definizione
X(z) = Σ x[n]z⁻ⁿ dove z è una variabile complessa

**ROC** (Region of Convergence): insieme di valori z per cui la serie converge
- Determina unicità della trasformata
- Forma: tipicamente anello nel piano complesso
- **Critica per stabilità e causalità**: 
  - Sistema causale → ROC esterna al cerchio dei poli più distante
  - Sistema stabile → ROC include il cerchio unitario |z|=1
  - Sistema anticausale → ROC interna al cerchio

### Proprietà Chiave
- **Linearità**: ax₁[n] + bx₂[n] ↔ aX₁(z) + bX₂(z)
- **Shift temporale**: x[n-k] ↔ z⁻ᵏX(z) (ritardo di k campioni moltiplica per z⁻ᵏ)
- **Convoluzione**: x[n]*h[n] ↔ X(z)H(z) (convoluzione diventa prodotto!)
- **Teorema valore iniziale**: x[0] = lim(z→∞) X(z) (per sistemi causali)
- **Teorema valore finale**: lim(n→∞) x[n] = lim(z→1) (1-z⁻¹)X(z) (se esiste)

### Poli e Zeri
**Funzione di trasferimento**: H(z) = B(z)/A(z) = (Σb_k z⁻ᵏ)/(Σa_k z⁻ᵏ)
- **Zeri**: radici del numeratore B(z) (H(z)=0)
- **Poli**: radici del denominatore A(z) (H(z)=∞)

**Relazione poli-stabilità**:
- Sistema **stabile** ⟺ tutti i poli dentro il cerchio unitario (|z| < 1)
- Poli sul cerchio unitario → stabilità marginale (oscillazioni persistenti)
- Poli fuori dal cerchio → instabilità (crescita esponenziale)

**Risposta in frequenza**: H(e^(jω)) ottenuta valutando H(z) sul cerchio unitario (z = e^(jω))
- Magnitudo |H(e^(jω))|: guadagno in funzione della frequenza
- Fase ∠H(e^(jω)): ritardo in funzione della frequenza
- Permette analisi frequenziale diretta del sistema

## 3. Trasformata di Fourier Tempo-Discreta (DTFT)

La DTFT è la rappresentazione in frequenza dei segnali tempo-discreti, estendendo il concetto di serie di Fourier.

**Definizione**: X(e^(jω)) = Σ x[n]e^(-jωn) per n da -∞ a +∞

**Proprietà fondamentali**:
- **Periodicità**: X(e^(jω)) è periodica con periodo 2π
  - Conseguenza della natura discreta del tempo
  - Frequenze ω e ω+2πk sono indistinguibili (aliasing)
  - Sufficiente analizzare intervallo [0, 2π) o [-π, π)
  
**Rappresentazione spettrale**:
- **Magnitudo** |X(e^(jω))|: contenuto energetico per ogni frequenza
- **Fase** ∠X(e^(jω)): ritardo di fase per ogni componente
- Per segnali reali: spettro simmetrico (|X(e^(jω))| = |X(e^(-jω))|)

**Teorema del campionamento** (Nyquist-Shannon):
- Un segnale continuo a banda limitata (f_max) può essere perfettamente ricostruito dai suoi campioni se f_s > 2f_max
- **Frequenza di Nyquist**: f_N = f_s/2 massima frequenza rappresentabile
- Fondamentale per conversione analogico-digitale

**Aliasing**: 
- Fenomeno per cui frequenze > f_N appaiono come frequenze più basse
- Sovrapposizione spettrale: impossibile distinguere f da f ± kf_s
- Prevenzione: filtro anti-aliasing passa-basso prima del campionamento
- Effetto irreversibile: informazione persa se si verifica

### Convoluzione Lineare vs Circolare

**Convoluzione Lineare**: y[n] = x[n] * h[n] = Σ x[k]h[n-k]
- Somma da -∞ a +∞
- Lunghezza risultato: se x ha N₁ campioni e h ha N₂ campioni → y ha N₁+N₂-1 campioni
- **Nel dominio frequenza (DTFT)**: Y(e^(jω)) = X(e^(jω))H(e^(jω)) prodotto
- È l'operazione naturale per sistemi LTI

**Convoluzione Circolare**: y[n] = x[n] ⊛ h[n] = Σ(k=0 to N-1) x[k]h[(n-k) mod N]
- Somma su periodo finito N con indici modulari
- Lunghezza fissa: y ha sempre N campioni (come x e h dopo padding)
- **Nel dominio DFT**: Y[k] = X[k]H[k] prodotto punto per punto
- Nasce dalla periodicità implicita della DFT

**Relazione e Aliasing Temporale**:
- DFT assume segnali **periodici** di periodo N
- Convoluzione circolare = convoluzione lineare di versioni periodiche
- **Problema**: sovrapposizione temporale (aliasing time-domain)
  - Campioni finali di un periodo si sovrappongono con iniziali del successivo
  - y_circolare ≠ y_lineare in generale

**Zero-Padding per Evitare Aliasing**:
- Per ottenere convoluzione lineare tramite DFT/FFT:
  1. Estendi x a lunghezza L ≥ N₁+N₂-1 con zeri
  2. Estendi h a stessa lunghezza L con zeri
  3. DFT di entrambi: X[k], H[k]
  4. Moltiplica: Y[k] = X[k]H[k]
  5. IDFT: y[n] = convoluzione lineare corretta!
- **Regola pratica**: L = 2^m ≥ N₁+N₂-1 (potenza di 2 per FFT efficiente)
- Usato in overlap-add e overlap-save per filtraggio veloce

## 4. DFT e FFT

### DFT (Discrete Fourier Transform)
- X[k] = Σ(n=0 to N-1) x[n]e^(-j2πkn/N), k = 0,...,N-1
- **Campionamento frequenza**: ω_k = 2πk/N, risoluzione Δf = f_s/N
- **Periodicità**: X[k] periodica di periodo N
- **Convoluzione circolare**: x[n] ⊛ h[n] ↔ X[k]H[k]
  - Lineare vs circolare: usare zero-padding per evitare aliasing temporale
- **Simmetria**: per x[n] reale, X[k] = X*[N-k] (coniugato hermitiano)

### FFT (Fast Fourier Transform)
- **Complessità**: O(N log N) vs O(N²) della DFT diretta
- **Algoritmi**: 
  - Cooley-Tukey: decimation-in-time (DIT) o decimation-in-frequency (DIF)
  - Radix-2: richiede N = 2^m, più efficiente
  - Mixed-radix: per N composto (es. 3×2^m)
- **Lunghezza**: 
  - Preferibile N potenza di 2 per massima efficienza
  - Zero-padding: aumenta risoluzione interpolando lo spettro (non aggiunge info)
- **Leakage spettrale**: discontinuità ai bordi → sidelobes
  - Mitigato con finestratura (Hann, Hamming, Blackman)

### Applicazioni
- **Analisi spettrale**: identificazione componenti frequenziali, periodicità
- **Filtraggio veloce**: 
  - Overlap-add: per segnali lunghi, divide in blocchi, somma sovrapposizioni
  - Overlap-save: mantiene campioni precedenti, scarta campioni transitori
- **Convoluzione**: per filtri FIR lunghi, FFT può essere più efficiente della convoluzione diretta

## 5. Filtri Digitali IIR

I filtri IIR (Infinite Impulse Response) sono filtri ricorsivi che utilizzano feedback, offrendo grande efficienza ma richiedendo attenzione alla stabilità.

### Caratteristiche
**Risposta impulsiva infinita**: h[n] teoricamente non si azzera mai (decade esponenzialmente)

**Struttura ricorsiva**: y[n] = Σb_k x[n-k] - Σa_k y[n-k]
- Usa output passati (feedback) oltre a input passati
- Ordine inferiore rispetto a FIR per stesse specifiche (efficienza computazionale)
- **Rischio instabilità**: poli devono stare dentro cerchio unitario
- **Fase non-lineare**: tipicamente distorsione di fase (problematica per audio/video)

### Progettazione

**Approccio classico**: progetto filtro analogico → trasformazione in digitale
- Sfrutta teoria consolidata dei filtri analogici (Butterworth, Chebyshev, etc.)
- Richiede trasformazione che preservi proprietà desiderate

### Confronto Filtri Classici

| Tipo | Ripple BP | Ripple BS | Transizione | Fase | Quando Usare |
|------|-----------|-----------|-------------|------|--------------|
| **Butterworth** | Nessuno (piatto) | Nessuno (monotona) | Graduale | Migliore linearità | Applicazioni generali, risposta smooth |
| **Chebyshev I** | Equiripple | Nessuno (monotona) | Più ripida | Non lineare | Serve transizione stretta, tollerabile ripple in BP |
| **Chebyshev II** | Nessuno (piatto) | Equiripple | Media | Non lineare | Banda passante pulita, BS con ripple OK |
| **Ellittico** | Equiripple | Equiripple | Più ripida possibile | Peggiore | Massima efficienza ordine, specifiche stringenti |

**Scelta pratica**:
- Audio/video → Butterworth (fase migliore)
- Comunicazioni con specifiche strette → Ellittico (minimo ordine)
- Compromesso → Chebyshev I

### Trasformazioni Analogico-Digitale

| Metodo | Tecnica | Vantaggi | Svantaggi | Quando Usare |
|--------|---------|----------|-----------|--------------|
| **Bilinear Transform** | s = (2/T)(1-z⁻¹)/(1+z⁻¹) | - Preserva stabilità<br>- No aliasing<br>- Robusta | - Warping frequenza (non-lineare)<br>- Serve pre-warping | **Standard** per tutti i filtri |
| **Impulse Invariance** | Campiona h_a(t) | - Mantiene forma temporale<br>- Intuitiva | - Aliasing per filtri non BL<br>- Solo low-pass | Low-pass ben banda-limitati |
| **Matched z-Transform** | z = e^(sT) poli/zeri | - Semplice<br>- Buona per controllo | - Approssimazione frequenziale<br>- Meno accurata | Sistemi di controllo |

**Pre-warping per Bilinear**: ω = 2arctan(ΩT/2) o Ω = (2/T)tan(ω/2)
- Compensa distorsione a frequenze critiche (tagli passa-banda)

### Strutture di Implementazione

| Struttura | Memoria | Sensibilità Coeff. | Overflow | Uso Tipico |
|-----------|---------|-------------------|----------|------------|
| **Direct Form I** | 2N ritardi | Media | Bassa | Didattica, debug |
| **Direct Form II** | N ritardi | Alta | Alta (stati interni) | Mai per alta precisione |
| **Cascade (SOS)** | 2N ritardi | **Bassa** | Media (con scaling) | **Standard industriale** |
| **Parallel** | Variabile | Bassa | Bassa | Parallelizzazione HW |
| **Lattice** | N ritardi | **Minima** | Bassa | Applicazioni critiche |

**Raccomandazione**: sempre usare Cascade (SOS) per implementazioni pratiche!

## 6. Filtri Digitali FIR

I filtri FIR (Finite Impulse Response) sono filtri non-ricorsivi che offrono fase lineare e stabilità garantita, al costo di ordini più elevati.

### Caratteristiche
**Risposta impulsiva finita**: h[n] ha lunghezza finita N (zero dopo N campioni)

**Struttura non-ricorsiva**: y[n] = Σ(k=0 to N-1) h[k]x[n-k]
- Nessun feedback: solo input passati
- **Sempre stabile**: nessun polo, solo zeri → impossibile instabilità
- **Fase lineare possibile**: con simmetria/antisimmetria h[n]
  - Critico per audio, video, comunicazioni dove distorsione fase inaccettabile
  - Ritardo di gruppo costante: tutti i segnali ritardati ugualmente
- **Ordine elevato**: per specifiche stringenti serve N grande (moltiplicazioni)

### Tipi con Fase Lineare

| Tipo | N | Simmetria | Risposta DC | Risposta Nyquist | Filtri Realizzabili |
|------|---|-----------|-------------|------------------|---------------------|
| **I** | Dispari | h[n] = h[N-1-n] | Qualsiasi | Qualsiasi | **Tutti** (LP, HP, BP, BS) |
| **II** | Pari | h[n] = h[N-1-n] | Qualsiasi | **Zero forzato** | LP, BP (no HP, BS) |
| **III** | Dispari | h[n] = -h[N-1-n] | **Zero forzato** | **Zero forzato** | BP centrato, differenziatori |
| **IV** | Pari | h[n] = -h[N-1-n] | **Zero forzato** | Qualsiasi | HP, BP, Hilbert transform |

**Scelta pratica**:
- Filtro generico → **Tipo I** (massima flessibilità)
- Low-pass → Tipo I o II
- High-pass → Tipo I o IV
- Band-pass → qualsiasi tipo
- Differenziatore → Tipo III

### Progettazione

**Window method** (metodo finestra):
- h[n] = h_ideal[n] · w[n] moltiplica risposta ideale per finestra
- h_ideal: trasformata inversa della risposta frequenziale desiderata (spesso sinc per low-pass)
- Finestra w[n] tronca la risposta infinita e modifica le caratteristiche

### Confronto Finestre

| Finestra | Lobo Principale | Attenuazione Lobi | Ripple BP | Quando Usare |
|----------|-----------------|-------------------|-----------|--------------|
| **Rectangular** | ±4π/N | -21 dB | 9% | Mai (solo didattica) |
| **Hann** | ±8π/N | -44 dB | 0.6% | Analisi spettrale generale |
| **Hamming** | ±8π/N | -53 dB | 0.2% | **Standard audio/filtri** |
| **Blackman** | ±12π/N | -74 dB | 0.02% | Serve alta attenuazione |
| **Kaiser (β)** | Variabile | Variabile | Variabile | **Controllo preciso trade-off** |

**Parametro Kaiser β**:
- β = 0 → simile Rectangular
- β ≈ 5 → simile Hamming  
- β ≈ 8.6 → simile Blackman
- Formula: β ≈ 0.1102(A-8.7) per A > 50 dB, dove A è attenuazione desiderata

### Confronto Metodi di Progettazione

| Metodo | Complessità | Controllo | Ottimalità | Uso Tipico |
|--------|-------------|-----------|------------|------------|
| **Window** | Bassa | Limitato | No | Prototipazione rapida, didattica |
| **Frequency Sampling** | Bassa | Diretto su freq | No | Forme particolari non-standard |
| **Parks-McClellan** | Media | Specifiche precise | **Sì (minimax)** | **Applicazioni professionali** |
| **Least Squares** | Media-Alta | Pesatura custom | Sì (L2) | Specifiche complesse pesate |

**Raccomandazione**: Parks-McClellan per design ottimale, Window+Kaiser per rapidità.

## 7. Sistemi Multirate

I sistemi multirate manipolano segnali cambiando la frequenza di campionamento, fondamentali per efficienza computazionale e applicazioni moderne.

### Operazioni Base

**Decimazione (Downsampling ↓M)**:
- Riduce frequenza di campionamento di fattore M: y[n] = x[Mn]
- **Aliasing inevitabile**: spettro si replica e sovrappone
- **Filtro anti-aliasing necessario**: passa-basso a ω_c = π/M prima del downsampling
  - Elimina componenti che causerebbero aliasing
  - Ordine filtro dipende da M e specifiche
- Riduce rate computazionale: elaborazione più efficiente
- Esempio: audio 48kHz → 16kHz per telefonia

**Interpolazione (Upsampling ↑L)**:
- Aumenta frequenza di fattore L inserendo L-1 zeri tra campioni
- y[n] = x[n/L] se n multiplo di L, altrimenti 0
- **Imaging**: creazione di copie spettrali a multipli di 2π/L
- **Filtro anti-imaging richiesto**: passa-basso rimuove copie spurie
  - Guadagno L per mantenere ampiezza corretta
  - Ricostruisce segnale "liscio" dai campioni interpolati
- Esempio: upsampling audio per conversione sample rate

**Conversione razionale M/L**:
- ↑L seguito da ↓M (o viceversa con ottimizzazioni)
- Conversione 44.1kHz (CD) ↔ 48kHz (video): L=160, M=147
- Filtro combinato: unico passa-basso più efficiente

### Filter Banks

**Struttura**:
- **Analisi**: scompone segnale in M sottobande parallele
  - Array di M filtri H_k(z) con bande diverse
  - Downsampling per ogni banda (riduzione dati)
- **Sintesi**: ricostruisce segnale dalle sottobande
  - Upsampling di ogni banda
  - Filtri sintesi F_k(z) e somma

**Perfect Reconstruction (PR)**:
- Condizione: output = ritardo dell'input (ŷ[n] = x[n-n₀])
- Richiede progettazione congiunta filtri analisi/sintesi
- Vincoli matematici: T(z)F(z) = cz^(-n₀) (no distorsione, no aliasing)
- Fondamentale per compressione lossless

**QMF (Quadrature Mirror Filters)**:
- Coppia filtri passa-basso/passa-alto specchiati
- H₁(z) = H₀(-z) simmetria attorno a π/2
- Cancellazione aliasing (non PR perfetta)
- Base per filter bank diadici

**Applicazioni**:
- Compressione audio: MP3 (32 bande), AAC (ibrida)
- Wavelets: filter bank Mallat (analisi multirisoluzione)
- Equalizzatori grafici: bande separate
- Coding sub-band: codifica indipendente per banda

## 8. Analisi Tempo-Frequenza

### STFT (Short-Time Fourier Transform)
- X(n,ω) = Σ x[m]w[n-m]e^(-jωm) dove w[n] è la finestra di analisi
- **Finestra**: 
  - Compromesso tempo-frequenza fisso (principio incertezza: ΔtΔf ≥ costante)
  - Finestra stretta → buona risoluzione temporale, scarsa frequenziale
  - Finestra larga → buona risoluzione frequenziale, scarsa temporale
- **Spectrogram**: |X(n,ω)|² rappresentazione energia tempo-frequenza
- **Hop size**: sovrapposizione finestre (tipicamente 50-75%)
- **Applicazioni**: analisi pitch, voice activity detection, time-varying spectra

### Wavelets
- **Decomposizione multirisoluzione**: segnale → coefficienti a scale (frequenze) diverse
- **Base**: funzione madre ψ(t) con dilatazioni a_k e traslazioni b_k
  - W(a,b) = ∫ x(t) ψ*((t-b)/a) dt
- **DWT** (Discrete Wavelet Transform): 
  - Algoritmo Mallat: filter bank a cascata (passa-basso/passa-alto + decimazione)
  - Efficienza: O(N) vs O(N log N) della FFT
  - Decomposizione: approssimazione (low-freq) + dettagli (high-freq) a ogni livello
- **Famiglie wavelets**: 
  - Haar: più semplice, discontinua
  - Daubechies (dbN): supporto compatto, N momenti nulli
  - Symlet, Coiflet: più simmetriche
  - Scelta: dipende da applicazione (smoothness, simmetria, supporto)
- **Risoluzione adattiva**: 
  - Alta frequenza → buona risoluzione temporale
  - Bassa frequenza → buona risoluzione frequenziale
  - Ideale per segnali transienti, non-stazionari

### Confronto STFT vs Wavelet

| Caratteristica | STFT | Wavelet |
|----------------|------|---------|
| **Risoluzione** | Fissa (finestra costante) | Adattiva multi-scala |
| **Tempo-Frequenza** | Δt·Δf = costante | Δt piccolo per alta f, Δf piccolo per bassa f |
| **Interpretazione** | Intuitiva (spettrogramma) | Meno intuitiva (scale) |
| **Migliore per** | Segnali quasi-stazionari, pitch tracking | Transienti, edge, compressione |
| **Complessità** | O(N log N) per FFT | O(N) per DWT |
| **Ridondanza** | Alta (overlap) | Bassa (critica sampling) |
| **Ricostruzione** | Overlap-add, diretta | Perfetta con wavelets ortonormali |
| **Applicazioni tipiche** | Voice analysis, spectral analysis | Compressione immagini, denoising, edge detection |

**Scelta pratica**:
- **STFT**: analisi vocale, identificazione pitch, quando serve spettrogramma chiaro
- **Wavelet**: compressione (JPEG2000), denoising, rilevamento discontinuità, analisi ECG/EEG

### Confronto IIR vs FIR

| Caratteristica | IIR | FIR |
|----------------|-----|-----|
| **Ordine** | Basso (efficiente) | Alto (più coefficienti) |
| **Stabilità** | Richiede verifica poli | Sempre stabile |
| **Fase** | Non-lineare (tipica) | Lineare (se simmetrico) |
| **Progettazione** | Da filtri analogici classici | Metodi numerici diretti |
| **Sensibilità coeff.** | Alta (soprattutto Direct Form II) | Bassa |
| **Latenza** | Bassa | Alta (ordine elevato) |
| **Quantizzazione** | Problematica (cicli limite) | Robusta |
| **Migliore per** | Efficienza computazionale, specifiche non critiche su fase | Audio/video, fase lineare critica |

**Scelta pratica**:
- **IIR**: filtri real-time embedded, bassa latenza, controllo
- **FIR**: audio professionale, comunicazioni digitali, equalizzazione

## 9. Elaborazione Statistica

L'elaborazione statistica tratta segnali come processi stocastici, essenziale quando rumore e incertezza sono rilevanti.

### Processi Stocastici

**Stazionarietà**:
- **Wide-Sense Stationary (WSS)**: media costante, autocorrelazione dipende solo dal ritardo
  - E[x[n]] = μ costante
  - R_x[n,m] = R_x[n-m] dipende solo da τ = n-m
- Semplifica analisi: proprietà statistiche invarianti nel tempo
- Molti segnali reali approssimabili come WSS su intervalli limitati

**Autocorrelazione**: R_x[m] = E[x[n]x*[n-m]]
- Misura similarità segnale con sé stesso ritardato di m
- R_x[0] = potenza media del segnale
- Simmetrica: R_x[-m] = R_x*[m] per processi reali
- Picco in m=0, decade per ritardi grandi (segnali decorrelati)

**Cross-correlazione**: R_xy[m] = E[x[n]y*[n-m]]
- Misura similarità tra due segnali
- Applicazioni: ritardi stimati, rilevamento segnali

**PSD (Power Spectral Density)**: S_x(ω) = DTFT{R_x[m]}
- Distribuzione potenza in frequenza
- Sempre reale e ≥0
- Integrale su [-π,π] = potenza totale

**Teorema Wiener-Khinchin**: S_x(ω) ↔ R_x[m] coppia trasformata
- Ponte tra dominio tempo (correlazione) e frequenza (spettro)
- Fondamentale per analisi spettrale stocastica

### Stima Spettrale

Obiettivo: stimare PSD S_x(ω) da realizzazioni finite del processo.

### Confronto Metodi Stima Spettrale

| Metodo | Tipo | Risoluzione | Varianza | Complessità | Pro | Contro |
|--------|------|-------------|----------|-------------|-----|--------|
| **Periodogramma** | Non-parametrico | N/2 punti | Alta (inconsistente) | O(N log N) | Semplice, veloce | Varianza non diminuisce con N |
| **Bartlett** | Non-parametrico | L/2 punti | Media÷K | O(N log N) | Riduce varianza | Peggiora risoluzione |
| **Welch** | Non-parametrico | L/2 punti | Bassa | O(N log N) | **Miglior compromesso** | Scelta finestra critica |
| **AR (Burg)** | Parametrico | Continua | Bassa | O(p²) | **Alta risoluzione**, picchi netti | Serve ordine corretto |
| **MA** | Parametrico | Continua | Media | O(q³) | Smooth, niente picchi spuri | Stima difficile, poco usato |
| **ARMA** | Parametrico | Continua | Bassa | O((p+q)³) | Massima flessibilità | Stima complessa, non-lineare |
| **MUSIC** | Sottospazio | Altissima | Bassa | O(M³+Lω) | Picchi stretti separabili | Serve #sinusoidi, costoso |
| **ESPRIT** | Sottospazio | Altissima | Bassa | O(M³) | Stima diretta freq | Come MUSIC, matrice strutturata |

**Legenda**: K = numero segmenti (Bartlett), L = lunghezza segmento, p/q = ordine AR/MA, M = dimensione sottospazio

**Trade-off fondamentale**: risoluzione vs varianza
- Più campioni in un segmento → migliore risoluzione ma varianza alta
- Media su più stime → bassa varianza ma risoluzione peggiore

### Quando Usare Quale

| Scenario | Metodo Consigliato | Motivo |
|----------|-------------------|--------|
| Analisi generale, robustezza | **Welch** | Compromesso ottimale, affidabile |
| Picchi spettrali stretti | **AR (Burg)** | Alta risoluzione per risonanze |
| Poche sinusoidi in rumore | **MUSIC/ESPRIT** | Risoluzione superiore, separazione |
| Spettro smooth, niente picchi | **MA** | Modella bene processi smooth |
| Real-time, risorse limitate | **Periodogramma** | Minima complessità |
| Lungo record stazionario | **Welch (overlap 50%)** | Massimizza stime indipendenti |

**Parametri Welch tipici**:
- Sovrapposizione: 50% (compromesso stime/indipendenza)
- Finestra: Hamming o Hann
- Lunghezza segmento: 256-2048 campioni (dipende da risoluzione desiderata)

### Filtri Adattativi
Algoritmi che aggiustano automaticamente i coefficienti del filtro per ottimizzare una funzione obiettivo (tipicamente MSE).

### Confronto Algoritmi Adattativi

| Algoritmo | Aggiornamento | Complessità | Convergenza | Stabilità | Tracking | Uso |
|-----------|---------------|-------------|-------------|-----------|----------|-----|
| **LMS** | w[n+1] = w[n] + μe[n]x[n] | O(N) | Lenta (~10N iter) | Buona se μ piccolo | Moderato | **Standard general-purpose** |
| **NLMS** | w[n+1] = w[n] + μe[n]x[n]/(ε+‖x‖²) | O(N) | Media (~5N iter) | Migliore | Buono | Input variabile, robusto |
| **RLS** | Ricorsivo con matrice P | O(N²) | Veloce (~2N iter) | Critica | Eccellente | Serve convergenza rapida |
| **Sign-LMS** | w[n+1] = w[n] + μ·sign(e[n])x[n] | O(N) | Lenta | Molto robusta | Scarso | Ambiente rumoroso |
| **Lattice** | Struttura modulare | O(N) | Media | Eccellente | Buono | Predizione, speech |

**Parametri critici**:
- **LMS μ**: 0 < μ < 2/λ_max (autovalore max R_xx). Tipico: μ = 0.01-0.1
- **RLS λ**: forgetting factor 0.95-0.999. Più basso → tracking veloce ma rumoroso
- **NLMS**: auto-normalizzazione, meno sensibile a scaling

**Applicazioni**:
- **Cancellazione eco**: rimuove eco acustico (telefonia) o eco di linea
  - AEC (Acoustic Echo Cancellation): cuffie, vivavoce, conferenze
  - Servono 256-1024 tap per eco acustico (ritardi lunghi)
- **Noise cancellation**: riferimento rumore → sottrazione adattiva (ANC cuffie)
- **Equalizzazione canali**: compensazione distorsione trasmissione
  - Training sequence → identificazione canale → equalizzazione
- **Predizione**: forecasting di serie temporali, codifica predittiva (DPCM)
- **Identificazione sistemi**: stima risposta impulsiva sistema ignoto
  - System ID: applica segnale test, osserva output, stima h[n]

### Filtro di Wiener
- **Obiettivo**: minimizza errore quadratico medio (MSE) tra segnale stimato e desiderato
- **Soluzione frequenza**: H_opt(ω) = S_dx(ω)/S_x(ω) dove S_dx è la densità spettrale incrociata, S_x la PSD dell'input
- **Presupposti**: segnali stazionari, statistiche note (correlazioni, spettri)
- **Tipi**: 
  - Non-causale: usa dati passati e futuri (impraticabile per real-time)
  - Causale: usa solo passato (Wiener-Hopf equations)
  - FIR: numero finito di coefficienti (soluzione Levinson)
- **Implementazione**: richiede inversione matrice di correlazione (Wiener-Hopf)
- **Limiti**: solo processi stazionari, non adattivo a variazioni temporali

### Filtro di Kalman
- **Estensione di Wiener**: gestisce processi non-stazionari e sistemi dinamici
- **Approccio**: state-space model, stima ricorsiva dello stato del sistema
- **Ciclo predizione-correzione**:
  - Predizione: stima stato futuro dal modello dinamico
  - Correzione: aggiorna stima con nuova misura e guadagno Kalman
- **Guadagno Kalman**: pesa predizione vs misura in base alle incertezze (covarianze)
- **Presupposti**: sistema lineare, rumori gaussiani, modello dinamico noto
- **Varianti**: 
  - EKF (Extended): linearizzazione per sistemi non-lineari
  - UKF (Unscented): campionamento sigma points, migliore per forte non-linearità
- **Convergenza**: con modello corretto, converge asintoticamente a Wiener per sistemi stazionari
- **Vantaggio vs Wiener**: ricorsivo (memoria limitata), gestisce non-stazionarietà, modellazione stato esplicita

## 10. Quantizzazione e Effetti Finiti

### Quantizzazione
- **ADC**: errore di quantizzazione ±Q/2 dove Q è il quanto (LSB)
  - SNR teorico ≈ 6.02b + 1.76 dB (b = bit di risoluzione)
  - Modello: rumore bianco additivo per segnali ad ampio spettro
- **Rappresentazione**: 
  - Fixed-point: range limitato, overflow possibile, efficiente
  - Floating-point: range ampio, minore preoccupazione overflow, più costoso
- **Overflow**: saturazione (clipping a valore massimo) vs wraparound (modulo aritmetico)

### Effetti Wordlength Finito
- **Coefficienti**: 
  - Poli/zeri dei filtri IIR sensibili all'arrotondamento
  - Migliore precisione → sezioni del secondo ordine (SOS/cascade)
- **Aritmetica**: 
  - Errori di arrotondamento si accumulano nelle operazioni ricorsive
  - Maggiore impatto in filtri IIR ad alto ordine
- **Cicli limite**: oscillazioni persistenti in filtri IIR con input nullo
- **Dead-band**: regioni vicino a zero dove il filtro "si blocca"

### Mitigazione
- **Scaling**: normalizzazione per evitare overflow e massimizzare SNR
- **Strutture robuste**: cascade (SOS), lattice (ortogonale)
- **Dithering**: aggiunta di rumore intenzionale per decorrelazione errori
  - RPDF (Rectangular PDF): semplice, distribuito uniformemente
  - TPDF (Triangular PDF): preferibile per audio, decorrelazione migliore

---

## 11. Tabella Proprietà delle Trasformate

### Proprietà Trasformata z

| Proprietà | Dominio Tempo | Dominio z | Note |
|-----------|---------------|-----------|------|
| Linearità | ax₁[n] + bx₂[n] | aX₁(z) + bX₂(z) | Combinazione lineare |
| Shift temporale | x[n-k] | z⁻ᵏX(z) | Ritardo k campioni |
| Anticipo temporale | x[n+k] | zᵏX(z) | Anticipo k campioni |
| Scaling in z | aⁿx[n] | X(z/a) | ROC scalata di \|a\| |
| Inversione temporale | x[-n] | X(1/z) | ROC inversa |
| Coniugazione | x*[n] | X*(z*) | Per segnali complessi |
| Convoluzione | x[n]*h[n] | X(z)H(z) | Prodotto in z |
| Moltiplicazione | x[n]h[n] | (1/2πj)∮X(v)H(z/v)v⁻¹dv | Convoluzione complessa |
| Differenziazione in z | nx[n] | -z(dX(z)/dz) | Moltiplicazione per n |
| Accumulazione | Σ(k=-∞ to n) x[k] | 1/(1-z⁻¹)X(z) | Integratore discreto |
| Valore iniziale | x[0] | lim(z→∞) X(z) | Solo sistemi causali |
| Valore finale | lim(n→∞) x[n] | lim(z→1) (1-z⁻¹)X(z) | Se limite esiste |

### Proprietà DTFT

| Proprietà | Dominio Tempo | Dominio Frequenza | Note |
|-----------|---------------|-------------------|------|
| Linearità | ax₁[n] + bx₂[n] | aX₁(e^(jω)) + bX₂(e^(jω)) | Combinazione lineare |
| Shift temporale | x[n-n₀] | e^(-jωn₀)X(e^(jω)) | Fase lineare -ωn₀ |
| Shift in frequenza | e^(jω₀n)x[n] | X(e^(j(ω-ω₀))) | Modulazione |
| Coniugazione | x*[n] | X*(e^(-jω)) | Simmetria hermitiana |
| Inversione temporale | x[-n] | X(e^(-jω)) | Riflessione spettro |
| Differenza | x[n] - x[n-1] | (1-e^(-jω))X(e^(jω)) | Derivata discreta |
| Accumulazione | Σ(k=-∞ to n) x[k] | 1/(1-e^(-jω))X(e^(jω)) + πX(e^(j0))Σδ(ω-2πk) | Con impulso in DC |
| Convoluzione | x[n]*h[n] | X(e^(jω))H(e^(jω)) | Prodotto |
| Moltiplicazione | x[n]h[n] | (1/2π)∫X(e^(jθ))H(e^(j(ω-θ)))dθ | Convoluzione periodica |
| Differenziazione freq | nx[n] | j(dX(e^(jω))/dω) | Moltiplicazione per n |
| Parseval | Σ\|x[n]\|² | (1/2π)∫\|X(e^(jω))\|²dω | Energia in tempo = freq |
| Simmetria (reale) | x[n] reale | X(e^(jω)) = X*(e^(-jω)) | Magnitudo pari, fase dispari |

### Proprietà DFT

| Proprietà | Dominio Tempo | Dominio Frequenza | Note |
|-----------|---------------|-------------------|------|
| Linearità | ax₁[n] + bx₂[n] | aX₁[k] + bX₂[k] | Combinazione lineare |
| Shift circolare tempo | x[(n-n₀) mod N] | e^(-j2πkn₀/N)X[k] | Fase lineare circolare |
| Shift circolare freq | e^(j2πk₀n/N)x[n] | X[(k-k₀) mod N] | Modulazione circolare |
| Dualità | X[n] | Nx[(−k) mod N] | Simmetria DFT-IDFT |
| Convoluzione circolare | x[n] ⊛ h[n] | X[k]H[k] | Prodotto punto-punto |
| Moltiplicazione | x[n]h[n] | (1/N)X[k] ⊛ H[k] | Convoluzione circolare |
| Parseval | Σ\|x[n]\|² | (1/N)Σ\|X[k]\|² | Energia conservata |
| Simmetria (reale) | x[n] reale | X[k] = X*[N-k] | Simmetria coniugata |
| Periodicità | x[n] = x[n+N] | X[k] = X[k+N] | Implicita in DFT |

### Coppie Trasformate Comuni

| Segnale x[n] | Trasformata z X(z) | ROC |
|--------------|-------------------|-----|
| δ[n] | 1 | Tutto il piano |
| u[n] | 1/(1-z⁻¹) | \|z\| > 1 |
| -u[-n-1] | 1/(1-z⁻¹) | \|z\| < 1 |
| aⁿu[n] | 1/(1-az⁻¹) | \|z\| > \|a\| |
| -aⁿu[-n-1] | 1/(1-az⁻¹) | \|z\| < \|a\| |
| naⁿu[n] | az⁻¹/(1-az⁻¹)² | \|z\| > \|a\| |
| cos(ω₀n)u[n] | (1-cos(ω₀)z⁻¹)/(1-2cos(ω₀)z⁻¹+z⁻²) | \|z\| > 1 |
| sin(ω₀n)u[n] | sin(ω₀)z⁻¹/(1-2cos(ω₀)z⁻¹+z⁻²) | \|z\| > 1 |

