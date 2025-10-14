# LLM – Cheatsheet Parametri Generazione (in italiano)

## Parametri Principali

| Parametro             | Significato                                                  | Valore consigliato                                             |
|-----------------------|--------------------------------------------------------------|----------------------------------------------------------------|
| context length        | Numero massimo di token di input che il modello ricorda      | Usa il massimo reale supportato (8k–32k)                       |
| evaluation batch size | Numero di prompt processati in parallelo durante l'inferenza | 1–4 per PC con 8–16 GB RAM, 8+ su GPU potente                  |
| system prompt         | Istruzioni permanenti (tono, ruolo, ecc.)                    | “Riscrivi il testo in italiano chiaro e coerente”              |
| stream output         | Mostra l’output mentre viene generato                        | Attivalo per scrittura rapida, disattivalo per output completi |


### Esempi tipici di Context Lenght

| Dimensione modello           | Range tipico | Context “reale” consigliato | Note su memoria                        |
|------------------------------|--------------|-----------------------------|----------------------------------------|
| 1B – 3B                      | 4k–8k        | max 4k                      | Leggero, adatto a PC con 8–12 GB RAM   |
| 7B – 8B (es. Mistral 7B)     | 8k–32k       | 16k ottimale                | Usa 8–12 GB VRAM o 12–16 GB RAM        |
| 13B – 14B                    | 16k–64k      | 32k consigliato             | Serve almeno 20–24 GB RAM              |
| Mixtral / 8×7B / modelli MoE | 32k–128k     | 64k ottimale                | Richiede 24 GB RAM o più               |
| Modelli “300k+” dichiarati   | 128k–300k+   | 64k–128k massimo reale      | Spesso marketing: oltre 128k instabili |
| Context troppo alto          | —            | Evitare 256k+ su PC         | Aumenta i tempi, degrada la qualità    |

### Settaggi di output

| Parametro          | Significato                                  | Valore consigliato                                                                    | Note                                            |
|--------------------|----------------------------------------------|---------------------------------------------------------------------------------------|-------------------------------------------------|
| max_new_tokens     | Numero massimo di token generabili in output | 512 → risposte brevi<br>2048 → testi medi/lunghi<br>4096+ → riscritture o saggi       | Se troppo basso tronca il testo                 |
| temperature        | Grado di creatività / casualità              | 0.2–0.4 → risposte precise<br>0.5–0.7 → riscritture naturali<br>0.8+ → molto creativa | Più alto = più fantasia                         |
| top_p              | Probabilità cumulativa dei token considerati | 0.9                                                                                   | Riducilo (0.8) se vuoi risposte più controllate |
| repetition_penalty | Penalizza la ripetizione di parole           | 1.1–1.2 → naturale<br>1.3–1.5 → evita loop                                            | Troppo alto = testo incoerente                  |
| presence_penalty   | Evita di ripetere concetti già detti         | 0.5–0.8                                                                               | Utile nei testi lunghi                          |
| frequency_penalty  | Penalizza parole ripetute troppo spesso      | 0.5–1.0                                                                               | Migliora la varietà lessicale                   |

