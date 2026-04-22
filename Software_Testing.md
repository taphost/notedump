# Software Testing Practices
> Ordinato per priorità d'uso: dal più comune al più specializzato

---

## ⬛ Tier 1 — Fondamentali (ogni progetto)

| Pratica | Termine EN | Tool comuni | Descrizione |
|---|---|---|---|
| Analisi statica stile | **Linting** | ESLint, Pylint, RuboCop | Errori sintattici, bad practice, stile |
| Verifica tipi | **Type Checking** | TypeScript (`tsc`), mypy | Errori di tipo a compile time |
| Test unitari | **Unit Testing** | Jest, pytest, JUnit | Verifica funzioni/metodi isolati |
| Debug | **Debugging** | gdb, Chrome DevTools, pdb | Ispezione stato a runtime (interattivo, logging, core dump) |
| Revisione umana | **Code Review** | GitHub PR, GitLab MR | Revisione manuale del codice |

---

## ⬛ Tier 2 — Standard (progetti seri)

| Pratica | Termine EN | Tool comuni | Descrizione |
|---|---|---|---|
| Test di integrazione | **Integration Testing** | pytest, Postman, REST Assured | Verifica interazione tra componenti |
| Copertura test | **Code Coverage** | Istanbul/nyc, coverage.py | % di codice esercitato dai test |
| Audit dipendenze | **Dependency Audit** | `npm audit`, Snyk, Dependabot | CVE e vulnerabilità nelle librerie |
| Rilevazione segreti | **Secrets Detection** | truffleHog, gitleaks | Chiavi API hardcoded nel codice |
| Scansione sicurezza statica | **SAST** | Semgrep, SonarQube, Bandit | Vulnerabilità nel codice sorgente |

---

## ⬛ Tier 3 — Avanzato (prodotti in produzione)

| Pratica | Termine EN | Tool comuni | Descrizione |
|---|---|---|---|
| Test end-to-end | **E2E Testing** | Playwright, Cypress, Selenium | Flusso utente completo simulato |
| Profilazione performance | **Profiling** | py-spy, perf, Chrome Profiler | Hotspot CPU/memoria a runtime |
| Fuzzing | **Fuzzing** | AFL++, libFuzzer, Atheris (Py) | Input casuali per trovare crash |
| Sicurezza dinamica | **DAST** | OWASP ZAP, Burp Suite | Attacchi simulati a runtime |
| Scansione container | **Container Scanning** | Trivy, Grype | Vulnerabilità nelle immagini Docker |
| Licenze dipendenze | **License Checking** | FOSSA, license-checker | Compatibilità licenze delle lib |
| Linting IaC | **IaC Linting** | tflint, checkov, terrascan | Sicurezza e qualità infrastruttura as code |
| Accessibilità | **Accessibility Testing** | axe, Lighthouse, WAVE | Conformità WCAG/ADA |

---

## ⬛ Tier 4 — Specializzato (sistemi critici / alta qualità)

| Pratica | Termine EN | Tool comuni | Descrizione |
|---|---|---|---|
| Test basati su proprietà | **Property-Based Testing** | Hypothesis (Py), fast-check (JS) | Genera automaticamente edge case |
| Mutation testing | **Mutation Testing** | Stryker, mutmut, PIT | Verifica che i test rilevino bug reali |
| Test contratti API | **Contract Testing** | Pact | Verifica accordi tra servizi/API |
| Sanitizzatori memoria | **Sanitizers** | AddressSanitizer, UBSan, TSan | Rilevano memory corruption e undefined behavior a compile time (distinti da Valgrind, che è un analyzer runtime separato) |
| Analisi dipendenze architetturali | **Architecture Testing** | ArchUnit, Deptrac | Vincoli architetturali automatizzati |
| SBOM | **Software Bill of Materials** | Syft, CycloneDX | Inventario completo di dipendenze transitive, licenze, versioni e hash |

---

## ⬛ Tier 5 — Estremo / Nicchia (aerospace, fintech, infra critica)

| Pratica | Termine EN | Tool comuni | Descrizione |
|---|---|---|---|
| Ingegneria del caos | **Chaos Engineering** | Chaos Monkey, Gremlin | Fallimenti iniettati in produzione |
| Esecuzione simbolica | **Symbolic Execution** | KLEE, angr | Esplora matematicamente tutti i path |
| Verifica formale | **Model Checking** | TLA+, Alloy | Verifica proprietà logiche del sistema per model checking |
| Theorem proving | **Formal Verification** | Coq, Isabelle | Prove matematiche di correttezza (più potente del model checking) |
| Tracing distribuito | **Distributed Tracing** | OpenTelemetry, Jaeger | Osservabilità in sistemi a microservizi |
| Compliance automatizzata | **Compliance Checking** | Chef InSpec, OpenSCAP | GDPR, PCI-DSS, HIPAA automatizzati |

---

## Note rapide

- **Analisi statica** → agisce sul codice sorgente, senza eseguirlo
- **Analisi dinamica** → agisce sul programma in esecuzione
- **Profiler ≠ Fuzzer**: il profiler misura performance, il fuzzer cerca crash
- **Property-based** e **mutation testing** sono i più sottovalutati per scovare edge case reali
- **Model Checking** (TLA+, Alloy) verifica proprietà logiche; **Theorem Proving** (Coq) offre garanzie matematiche complete — sono approcci distinti
- **Sanitizers** (ASan, UBSan) agiscono a compile time; **Valgrind** è un analyzer runtime separato — non confonderli
- **Atheris** è il fuzzer Python di Google — per C/C++ preferire AFL++ o libFuzzer

---
