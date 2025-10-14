# LM Studio – Cheatsheet Parametri Generazione (in italiano)

## Parametri principali

Parametro | Significato | Valore consigliato | Note
--- | --- | --- | ---
max_new_tokens | Numero massimo di token generabili in output | 512 → risposte brevi
2048 → testi medi/lunghi
4096+ → riscritture o saggi | Se troppo basso tronca il testo
temperature | Grado di creatività / casualità | 0.2–0.4 → risposte precise
0.5–0.7 → riscritture naturali
0.8+ → molto creativa | Più alto = più fantasia
top_p | Probabilità cumulativa dei token considerati | 0.9 | Riducilo (0.8) se vuoi risposte più controllate
repetition_penalty | Penalizza la ripetizione di parole | 1.1–1.2 → naturale
1.3–1.5 → evita loop | Troppo alto = testo incoerente
presence_penalty | Evita di ripetere concetti già detti | 0.5–0.8 | Utile nei testi lunghi
frequency_penalty | Penalizza parole ripetute troppo spesso | 0.5–1.0 | Migliora la varietà lessicale

## Parametri di contesto

Parametro | Significato | Valore consigliato
--- | --- | ---
context length | Numero massimo di token di input che il modello ricorda | Usa il massimo reale supportato (8k–32k)
system prompt | Istruzioni permanenti (tono, ruolo, ecc.) | “Riscrivi il testo in italiano chiaro e coerente”
stream output | Mostra l’output mentre viene generato | Attivalo per scrittura rapida, disattivalo per output completi

## Esempi rapidi

Scenario | Valori consigliati
--- | ---
Riscrittura fedele di un testo breve | temperature: 0.4
 top_p: 0.9
 repetition_penalty: 1.2
 max_new_tokens: 2048
Testo creativo o variante libera | temperature: 0.8
 top_p: 0.95
 repetition_penalty: 1.1
 max_new_tokens: 4096
Sintesi o spiegazione tecnica | temperature: 0.3
 top_p: 0.85
 repetition_penalty: 1.3
 max_new_tokens: 1024

