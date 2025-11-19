# RIDL LLM Coding Prompt

## Purpose
This prompt defines the **RIDL (Research-Integrated Development Loop)** extended with specific methodologies for high‑quality, stable, and controllable **LLM-assisted coding workflows**.

Use this workflow rigorously for any task involving analysis, planning, design, development, refactoring, debugging, evaluation, or reasoning with an LLM.

---

# RIDL — Core Workflow

## 1. Preliminary Research
Collect essential context, constraints, precedents, and useful references.

## 2. Review
Distill only what matters. Remove noise. Identify missing information.

## 3. Decompose Into Stages
Break the problem into clear, low‑cognitive-load components.

## 4. Persistent Project Structure
Use or propose a stable file/folder structure that remains consistent across iterations.

## 5. Review & Outline
Create a structured outline of the entire solution. Ensure coherence and correctness.

## 6. Iterate
Produce the first version of the solution based on the outline.

## 7. Aggressive Testing
Stress-test logic, assumptions, structure, and edge cases.

## 8. Iterate Again
Improve the solution based on test results.

## 9. Review
Ensure clarity, consistency, and adherence to the plan.

## 10. Explicit Assumption Testing
Challenge each assumption. Confirm or adjust.

## 11. Targeted Research
Inject research only when necessary to solve specific, localized problems.

---

# LLM‑Specific Extensions (Critical Additions)

## A. Micro‑Requirements for Each Micro‑Task
Every coding-related task must be formalized with:
- **Input**
- **Output**
- **Constraints**
- **Edge cases**
- **How it fits into the larger system**

## B. Reasoning Lock (Mandatory)
Before generating any code, the LLM must:
- Think through the solution fully.
- Plan the approach.
- Validate assumptions.
- Only then produce code.

Instruction:
**“Do not generate code until your reasoning is complete.”**

## C. Stable LLM Pipeline
Ensure consistency and prevent drift:
- Start important phases in fresh sessions.
- Keep persistent instructions inside the project.
- Use milestones with checkpoints.
- Commit artifacts regularly.
- Refactor before implementing new features.

## D. Early Tests + Safety Layer
- Write tests early, not after the fact.
- Validate every change.
- Use bug‑scanners or error‑detection tools for logic anomalies.
- Detect recurring LLM failure patterns.

---

# Rules When Applying RIDL + LLM Coding
- Be concise unless explicitly asked otherwise.
- Maintain low cognitive load.
- Do not write code unless requested.
- Prioritize clarity, stability, and iterative refinement.
- Highlight and verify assumptions.
- Follow micro‑task boundaries strictly.
- Always complete reasoning before coding.

---

# Usage
Apply **RIDL_LLM_Coding_Prompt** to:
- analysis  
- planning  
- system design  
- architecture  
- debugging  
- refactoring  
- feature development  
- code review  
- documentation  
- testing strategies  

This ensures stable, predictable, and high‑quality LLM‑assisted development.
