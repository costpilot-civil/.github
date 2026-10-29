# CostPilot

**AI-assisted construction tender analysis and material matching.**

CostPilot is a desktop application designed to help construction estimators analyze tender documents and identify relevant materials from a supplier catalog. It combines structured information extraction with hybrid information retrieval to produce ranked material suggestions for review.

The aim is to make material selection during *Kalkulation* faster and more consistent—not to replace an estimator's judgment about construction methods, site conditions, labor, or final project pricing.

## Product Demo

https://github.com/user-attachments/assets/5b409a19-d5d7-4292-91fb-b3c612a41c7c

## Key Features

- **Project management** — Create, open, edit, and manage construction projects.
- **Tender import** — Import GAEB XML tender documents and explore their hierarchical positions, descriptions, quantities, and units.
- **Material matching** — Find relevant supplier catalog materials using both keyword-based and semantic search.
- **Structured attribute filtering** — Exclude candidates with conflicting material attributes before final reranking.
- **Matching review** — Inspect matched, review-required, and unmatched positions alongside their suggested materials.
- **Supplier and price information** — View available prices, enter a unit price when needed, and explicitly confirm the selected price.

## How It Works

CostPilot separates supplier catalog preparation from tender matching. The shared catalog is prepared once and can be searched across multiple projects and tenders.

![Conceptual CostPilot matching workflow](./assets/images/workflow.png)

### Catalog Preparation

Supplier catalog descriptions are normalized, relevant material attributes are extracted, and search indexes and vector embeddings are generated to support efficient retrieval.

### Tender Matching

1. **Tender parsing** — Read the GAEB XML document and extract its structure and individual positions.
2. **Query processing** — Build search queries from the position descriptions and relevant structured information.
3. **Hybrid retrieval** — Combine BM25 keyword retrieval and vector similarity search.
4. **RRF fusion** — Merge the candidate rankings using Reciprocal Rank Fusion.
5. **Attribute filtering** — Remove candidates with conflicting structured attributes where applicable.
6. **Cross-encoder reranking** — Re-evaluate the remaining candidates and rank their relevance.
7. **Result review** — Present matching outcomes and candidate details for user review and price confirmation.

![Conceptual hybrid retrieval process](./assets/images/retrieval_process.png)

*The diagrams illustrate the overall concepts. They are simplified visuals; the current implementation applies structured attribute filtering between fusion and reranking.*

## System Overview

CostPilot is organized into independent components with clearly separated responsibilities:

| Component | Responsibility | Technologies |
| --- | --- | --- |
| **Desktop Frontend** | Project and tender workflows, result visualization, price selection | Tauri 2, React, TypeScript, Mantine |
| **Backend** | REST APIs, matching orchestration, application logic | Python, FastAPI |
| **Core** | Tender parsing, structured extraction, retrieval and reranking components | Python |
| **Database** | Supplier catalog, tender records, search data, and embeddings | PostgreSQL, pgvector |
| **Deployment** | Service orchestration and runtime infrastructure | Docker Compose |

## Technology Highlights

**Information retrieval:** BM25, vector search, hybrid retrieval, Reciprocal Rank Fusion (RRF), and cross-encoder reranking.

**Structured information processing:** GAEB XML parsing, material attribute extraction, and conflict-aware candidate filtering.

**Application engineering:** Tauri desktop interface, REST APIs, PostgreSQL persistence, and containerized backend services.

## Project Status

CostPilot has an implemented desktop workflow for project management, tender import, material matching, result review, and unit-price confirmation. Development and refinement are ongoing.

The source code and detailed deployment documentation are maintained in private repositories. This public page focuses on the application's capabilities, architecture, and demonstration.
