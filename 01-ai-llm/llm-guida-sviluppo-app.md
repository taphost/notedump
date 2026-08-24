# Sviluppare App con LLM: Le Best Practice

## 1. Pianifica Prima di Scrivere Codice

L'LLM funziona meglio con progetti ben definiti. Prepara questi documenti:

* **Requirements** — feature elencate esplicitamente
* **User stories** — azioni concrete degli utenti
* **Stack** — tecnologie e versioni fissate
* **Conventions** — struttura cartelle, naming, stile di codifica

Una struttura consistente (`src/`, `components/`, `api/`) riduce la deriva dell'LLM. Scomponi ogni feature in task piccoli con breve pseudocodice: definisce confini chiari ed evita complessità inutile.

## 2. Parti da Framework e Versioni Fisse

Usa framework collaudati (Next.js, SvelteKit) invece di far creare la struttura al modello. I default del framework prevengono pattern misti e architetture inconsistenti. Specifica sempre versioni esatte: il mismatch di versioni crea problemi difficili da risolvere.

## 3. Chiedi Spiegazioni Prima del Codice

Fai ripetere il task al modello e spiegare l'approccio implementativo prima di generare codice. Correggere la spiegazione è molto più semplice che correggere 200 righe sbagliate. Per gli aggiornamenti, richiedi modifiche in formato diff: mantiene stabilità e riduce riscritture accidentali.

## 4. Task Piccoli e Isolati

L'LLM fallisce con prompt ampi, ha successo con quelli precisi. Invece di "Costruisci l'autenticazione":

* definisci il modello utente
* crea la route di registrazione
* aggiungi hashing
* aggiungi logica di login

Task ridotti minimizzano allucinazioni, semplificano debug e mantengono architettura pulita.

## 5. Strategia Multi-Modello

LLM diversi hanno punti di forza diversi. Usane uno per pianificazione, uno per codice, un altro per verifica logica. Confrontare risposte tra modelli intercetta molti errori.

## 6. Documentazione Continua

Mantieni `architecture.md` e `conventions.md` sempre aggiornati. Dopo conversazioni lunghe, riparti con nuovo thread reintroducendo i documenti core: resetta il contesto e mantiene allineamento con lo stato reale del progetto.

## 7. Ri-Incolla File e Limita lo Scope

Ogni poche modifiche, incolla il file completo aggiornato per mantenere il modello consapevole della versione reale. Imposta la regola: *"Modifica solo i file esplicitamente menzionati"* per prevenire modifiche indesiderate ad altre parti del codebase.

## 8. Review e Test da Sviluppatore

L'LLM scrive codice ma richiede supervisione:

* verifica import inconsistenti
* controlla logica annidata
* assicurati che le modifiche non abbiano impattato altre feature
* testa funzionalità adiacenti, non solo quella modificata

L'LLM aggiusta cose silenziosamente: testare funzionalità vicine è essenziale.

## 9. Git per Ogni Passaggio

Commit piccoli e frequenti. Se l'LLM rompe qualcosa, i diff chiariscono l'accaduto. Richiedi fix idempotenti: eseguire la stessa patch due volte non deve generare nuovi problemi.

## 10. Architettura Modulare

Se il modello necessita dell'intero codebase per piccole modifiche, la struttura è troppo accoppiata. Progetta moduli comprensibili e modificabili indipendentemente. Naming consistente aiuta il modello a seguire i tuoi pattern invece di inventarne di nuovi.

---

**L'LLM è un moltiplicatore. Un processo stabile è ciò che rilascia i prodotti.**