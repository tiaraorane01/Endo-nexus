# ENDO-NEXUS
**Endometriosis Network Exploration System**

A clinician-facing visual decision-support prototype that maps endometriosis as a connected, multi-system disease network instead of a list of isolated symptoms.

Built by the PFW Endo Team for the Harvard HSIL Hackathon 2026.

---

## The problem

Endometriosis affects over 7 million reproductive-age women in the U.S., and diagnosis takes about 7 years on average, usually ending in an invasive laparoscopy. Part of the delay is that the signs are spread across many body systems: pelvic pain, GI symptoms, migraines, fatigue, inflammation, and more. In a short clinic visit, those scattered signals are hard to connect.

Most tools show this information as siloed lists. Questionnaires stop at a checklist or a score, and EHRs store the data without making the relationships easy to see.

## What Endo-Nexus does

Endo-Nexus turns patient symptoms and history into an interactive map a clinician can read on one screen.

- **Before the visit:** the patient fills out a structured symptom questionnaire.
- **During the visit:** the clinician sees a systems map showing where the patient's symptoms cluster.
- **After the visit:** the map supports referrals, possible phenotype patterns, and tracking changes over time.

## How it works

### 1. A curated knowledge graph of endometriosis

At its core, Endo-Nexus is a weighted biomedical knowledge graph.

- **Nodes** are medical entities: endometriosis, body systems, symptoms, comorbidities, and genes.
- **Edges** are the relationships between them, each carrying a weight (strength of association), a confidence level, and the literature references that support it.

Biologically, this is a **network medicine** view of the disease: a phenotype–system–genotype map that links what a patient experiences to the organ systems and genes involved.

### 2. A solar-system interface

The graph is shown through a solar-system metaphor that makes hierarchy and closeness easy to read:

| Visual element | Represents |
|---|---|
| Sun | Endometriosis |
| Planets | Body systems (reproductive, GI, urinary, neuroendocrine, etc.) |
| Moons | Symptoms and test results |
| Continents | Comorbidities |
| Cities | Genes |

A single symptom can orbit more than one planet, which shows how endometriosis reaches across organ systems instead of staying in one.

### 3. Data pipeline

```
Curated spreadsheets  →  JSON converter + validator  →  Visualization
(systems, symptoms,                                      (React + Vite + Three.js)
 comorbidities, genes,
 edges, references)
```

Domain data is entered in structured spreadsheet tabs with controlled IDs, then converted to a normalized JSON graph that the frontend renders directly.

### 4. Clinical NLP layer (planned)

The next stage is designed to read de-identified clinical notes and place each patient onto the population-level network:

```
EHR text  →  NLP extraction  →  patient-specific subgraph  →  visualization
```

The planned first version is a rule-based pipeline in Python using **spaCy** and **medSpaCy**. It is designed to:

- find mentions of symptoms, comorbidities, test results, medications, and procedures
- map each mention to a standard key (for example, "painful menses" → `dysmenorrhea`)
- handle clinical context such as negation ("denies pelvic pain"), uncertainty, timing, and family history ("mother had endometriosis")
- produce one row per extracted fact, a visit-date timeline, and a structured data file for the frontend to display

## Data and ethics

The hackathon prototype uses **mock and synthetic data only**. Real EHR integration is future work and will use de-identified data, with attention to bias in how patient phenotypes are represented.

## Team

| Member | Focus |
|---|---|
| **Tia RaoRane** | Biology and clinical framing, knowledge curation (systems, symptoms, comorbidities, genes, evidence), biological data analysis |
| **Emma Lytle** | Systems design, data visualization, product and visual design |
| **Vaishnavi Kosuru** | AI/ML and software engineering, JSON pipeline, technical development |

**Mentor:** Dr. Amal Khalifa, Purdue University Fort Wayne

## Status

Prototype. The knowledge graph structure and visualization design are in place; the NLP layer and clinician usability testing are next.
