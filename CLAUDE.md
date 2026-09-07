# Legal-RAG Project Notes

## What this project is

A demonstration RAG (Retrieval-Augmented Generation) knowledge base built from 25 synthetic legal contracts related to India Global Capability Centers (GCCs). Originally set up as a training exercise (see `README.MD`) on why document indexing beats "read everything every time" for LLM-based Q&A. All companies, people, and figures in the contracts are fictitious.

## Folder structure

```
Legal-RAG/
├── README.MD                  Original exercise brief — background/rationale, do not need to re-read for routine work
├── Input/                      Source of truth. 25 raw contract .md files (01–25), unmodified.
└── Knowledge_Base/             Generated index/retrieval layer. Start here for any contract question.
    ├── index.md                 Root index — links to all 5 categories + full 25-row lookup table
    ├── 01_gcc_advisory_client_engagements/       (contracts 01–05 + index.md)
    ├── 02_entity_setup_legal_compliance/         (contracts 06–10 + index.md)
    ├── 03_talent_employment_hr_operations/       (contracts 11–15 + index.md)
    ├── 04_workplace_technology_operational_vendors/  (contracts 16–20 + index.md)
    └── 05_managed_gcc_operations_transformation/ (contracts 21–25 + index.md)
```

Each `Knowledge_Base/<category>/` folder contains unmodified copies of the relevant contracts plus an `index.md` with a summary table (client, India location, dates, value, risk) and a short factual summary per contract.

## How to answer questions about these contracts

1. Open `Knowledge_Base/index.md` first — it maps categories to the GCC lifecycle stage (Advise & Design → Establish Legal Vehicle → Build Workforce → Build Operating Environment → Operate & Transform) and has a full 25-row lookup table plus a "common cross-cutting questions" section.
2. Narrow to the relevant category `index.md` for a summary and to identify the specific contract(s).
3. Only then open the individual contract file(s) under `Input/` or the matching `Knowledge_Base/<category>/` copy (identical content) for full clause-level detail.
4. Avoid reading all 25 contracts for a single question — that defeats the purpose of the index.

## Contract metadata

Every contract file has YAML frontmatter (document_id, document_type, main_category, knowledge_group, subcategory, status, effective/expiration dates, jurisdiction, governing_law, parties, india_location, currency, contract_value, risk_level, renewal_type, confidentiality_level, rag_tags). This frontmatter is the authoritative source for the categorization used in `Knowledge_Base/` — if new contracts are added, use it to decide which category folder they belong in.

## Conventions / constraints

- **Never edit contract text.** `Input/` is the source of truth; `Knowledge_Base/` copies must stay byte-identical to `Input/`. Only `index.md` files are hand-maintained.
- If a contract is added, removed, or renumbered in `Input/`, update: the relevant category `index.md` (table + summary), the root `Knowledge_Base/index.md` (quick-lookup table), and copy/remove the file in the matching category folder.
- Category assignment follows the `main_category` field in each contract's frontmatter (5 categories, 5 contracts each currently).
