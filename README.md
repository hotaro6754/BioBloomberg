<div align="center">

# 🧬 BioBloomberg

### The Open-Source Intelligence Terminal for Life Sciences

**Free. Forever. For Every Researcher on Earth.**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Status: In Development](https://img.shields.io/badge/status-in%20development-yellow)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[Website](https://biobloomberg.org) · [Documentation](docs/) · [API Reference](docs/api.md) · [Contributing](CONTRIBUTING.md) · [Discord](https://discord.gg/biobloomberg)

</div>

---

## What Is BioBloomberg?

Researchers spend **60–80% of their time** searching for, reading, and synthesizing information across dozens of fragmented databases — PubMed, ClinicalTrials.gov, PubChem, UniProt, patent registries, funding databases. Each speaks a different language. None of them connect.

**BioBloomberg fixes this.**

It is a single, AI-powered intelligence platform that aggregates data from 50+ public biological databases, connects them through a living knowledge graph, and lets you ask questions in plain English — all for free, forever.

Think Bloomberg Terminal for finance, but for biology, and completely open source.

```
You ask:  "What is the current state of KRAS inhibition research?"

You get:  A synthesized answer covering the top compounds, active clinical trials,
          recent publications, key researchers, patent landscape, and funding trends —
          all with full citations, in under 10 seconds.
```

---

## Why Open Source?

The most important tools in the history of biology were free.

GenBank is free. BLAST is free. PubMed is free. The entire foundation of modern molecular biology was built on open data and open tools. A student in Hyderabad should have the same research intelligence as a scientist at Harvard. BioBloomberg is built on that principle.

- **Open source** — every line of code is on GitHub under MIT license
- **Free for researchers** — no paywalls, no institutional logins required
- **Community powered** — improves because researchers use it and contribute to it
- **Science aligned** — we are building infrastructure, not a product

---

## Core Features

### 🔍 Intelligent Search
Semantic, entity-aware search across all sources simultaneously. Search for `BRCA2` and the platform understands it is a gene — not just text. One query returns papers, trials, patents, compounds, and funding data together.

### 🕸️ Knowledge Graph Explorer
The heart of BioBloomberg. An interactive, visual map connecting genes → proteins → compounds → clinical trials → publications → researchers → funding. Navigate biology the way it actually works — as a connected system, not isolated silos.

### 🤖 AI Research Assistant
Ask natural language questions, get synthesized answers grounded entirely in real source documents. No hallucination — every claim is linked to a citation. Powered by RAG (Retrieval-Augmented Generation) over the knowledge graph.

### 📚 Literature Review Assistant
Automated literature maps, structured summaries, gap analysis, and bibliography export in APA, MLA, Vancouver, or BibTeX — for students, researchers, and grant writers.

### 🏥 Clinical Intelligence
Real-time clinical trial tracking, drug pipeline views, FDA/EMA regulatory timelines, and trial outcome monitoring.

### 📡 Patent Intelligence
Biological patent landscape visualization, citation networks, and patent-to-research connection tracking.

### ⚡ Open API
Every feature is accessible programmatically. Free for academic and research use. Full REST API + GraphQL for the knowledge graph.

---

## Data Sources

BioBloomberg is built entirely on **public, open-access data**. No expensive licenses. No legal barriers.

| Category | Sources |
|---|---|
| **Literature** | PubMed Central, bioRxiv, medRxiv, Europe PMC, arXiv (q-bio), PLOS, eLife, Semantic Scholar |
| **Clinical** | ClinicalTrials.gov, EU Clinical Trials Register, WHO ICTRP, OpenFDA, EMA |
| **Molecular Biology** | PubChem, ChEMBL, UniProt, Ensembl, NCBI Gene, PDB, STRING DB, ChEBI |
| **Patents** | Google Patents, USPTO Open Data, EPO Open Patent Services, WIPO |
| **Funding** | NIH Reporter, Crossref, OpenAlex, ORCID |
| **Ontologies** | Gene Ontology, Disease Ontology, HPO, MeSH, SNOMED CT |

50+ sources in total. All public. All free. All updated in real time.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      User Interface                         │
│              React + D3.js Graph Visualizations             │
└────────────────────────┬────────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────────┐
│                     API Layer                               │
│            FastAPI (REST) + GraphQL Endpoint                │
└──────┬─────────────────┬──────────────────┬─────────────────┘
       │                 │                  │
┌──────▼──────┐  ┌───────▼───────┐  ┌──────▼──────┐
│  Knowledge  │  │  AI / RAG     │  │   Search    │
│   Graph     │  │   Layer       │  │   Engine    │
│  (Neo4j)    │  │ (LLM + Index) │  │(Elasticsearch│
└──────┬──────┘  └───────────────┘  └─────────────┘
       │
┌──────▼─────────────────────────────────────────────────────┐
│                   Data Pipeline                            │
│      Apache Kafka → Airflow → NLP Processing              │
│  (Entity Recognition · Disambiguation · Graph Building)   │
└──────┬─────────────────────────────────────────────────────┘
       │
┌──────▼─────────────────────────────────────────────────────┐
│               50+ Public Data Sources                      │
│  PubMed · bioRxiv · ClinicalTrials · UniProt · PubChem … │
└────────────────────────────────────────────────────────────┘
```

**Stack:** Python / FastAPI · React · Neo4j · Elasticsearch · PostgreSQL · Apache Kafka · Airflow · Docker · Kubernetes · HuggingFace / spaCy (biomedical NLP)

---

## Getting Started

### Use Online
Visit **[biobloomberg.org](https://biobloomberg.org)** — no account required for basic use.

### Run Locally

**Prerequisites:** Python 3.11+, Node.js 20+, Docker, Docker Compose

```bash
# Clone the repository
git clone https://github.com/biobloomberg/biobloomberg
cd biobloomberg

# Configure environment
cp .env.example .env
# Edit .env with your settings (API keys for optional AI features)

# Start everything
docker compose up -d

# Platform is now running at http://localhost:3000
# API documentation at http://localhost:8000/docs
```

Full setup guide: [docs/local-setup.md](docs/local-setup.md)

### API Quick Start

```python
import requests

API_KEY = "your_free_api_key"  # Get from biobloomberg.org/account
BASE = "https://api.biobloomberg.org/v1"

# Search across all sources
results = requests.get(
    f"{BASE}/search",
    params={"q": "CRISPR sickle cell disease", "sources": "all"},
    headers={"Authorization": f"Bearer {API_KEY}"}
).json()

# Query the knowledge graph
graph = requests.get(
    f"{BASE}/graph/entity/BRCA2/connections",
    params={"depth": 2, "types": ["Disease", "Compound", "ClinicalTrial"]},
    headers={"Authorization": f"Bearer {API_KEY}"}
).json()

# Ask the AI assistant
answer = requests.post(
    f"{BASE}/ask",
    json={"question": "What are the latest KRAS G12C inhibitors in clinical trials?"},
    headers={"Authorization": f"Bearer {API_KEY}"}
).json()
print(answer["response"])  # Synthesized answer with citations
```

Full API docs: [docs/api.md](docs/api.md) · Available in Python, R, JavaScript

---

## Roadmap

| Phase | Timeline | Goal |
|---|---|---|
| **Phase 0: Foundation** | Months 1–3 | Working prototype with PubMed, bioRxiv, ClinicalTrials.gov, PubChem + AI search |
| **Phase 1: Knowledge Graph** | Months 4–9 | Live cross-source knowledge graph + Graph Explorer + public API v1 |
| **Phase 2: Intelligence** | Months 10–18 | Full AI assistant + alerts + literature review tool + community annotations |
| **Phase 3: Ecosystem** | Months 19–36 | Plugin system + multilingual support + institutional deployments |

See full roadmap and open issues: [github.com/biobloomberg/biobloomberg/issues](https://github.com/biobloomberg/biobloomberg/issues)

---

## Contributing

BioBloomberg is built by and for the scientific community. All contributions are welcome.

### For Developers
- Browse [`good first issue`](https://github.com/biobloomberg/biobloomberg/labels/good%20first%20issue) labels to get started
- Build new data source connectors — any public biological database is fair game
- Improve biomedical NLP models and entity recognition
- Build frontend components and graph visualizations

### For Biologists and Researchers
- Report data quality issues and bugs
- Curate and annotate the knowledge graph
- Suggest data sources we have not yet integrated
- Write tutorials and how-to guides for your research community

### For Everyone
- ⭐ Star this repository — it tells the community this matters
- Share BioBloomberg with your colleagues, students, and lab
- Join the discussion in [Issues](https://github.com/biobloomberg/biobloomberg/issues) and [Discussions](https://github.com/biobloomberg/biobloomberg/discussions)
- Translate documentation into other languages

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## Community

- 💬 [Discord](https://discord.gg/biobloomberg) — real-time discussion, help, and announcements
- 🗣️ [GitHub Discussions](https://github.com/biobloomberg/biobloomberg/discussions) — feature requests, roadmap debates, research use cases
- 🐦 [Twitter / X](https://twitter.com/biobloomberg) — updates and community highlights
- 📧 [Mailing List](https://biobloomberg.org/newsletter) — low-frequency announcements

---

## Sustainability

Free does not mean unsupported. BioBloomberg's funding model:

- **Research grants** — NIH, NSF, EU Horizon, Wellcome Trust, and similar bodies fund open scientific infrastructure. We actively apply.
- **Institutional contributions** — universities and research institutes that benefit are invited to contribute through infrastructure support or developer time.
- **Commercial API tier** — pharmaceutical and biotech companies using BioBloomberg at scale subscribe to a commercial tier, which funds free access for everyone else.
- **Foundation governance** — long-term, BioBloomberg will be governed by a foundation structure, ensuring it stays independent and mission-aligned.

---

## License

BioBloomberg is released under the [MIT License](LICENSE). Use it, fork it, build on it. 

The only thing we ask: if you make it better, share it back.

---

## Acknowledgments

BioBloomberg stands on the shoulders of the open data ecosystem that biologists have built over decades — NIH, NCBI, EBI, the Wellcome Sanger Institute, and every researcher who published their data openly. Thank you.

---

<div align="center">

**Built for science. Built by scientists. Built for everyone.**

*The most important tools in biology were always free.*

[⭐ Star this repo](https://github.com/biobloomberg/biobloomberg) · [🍴 Fork it](https://github.com/biobloomberg/biobloomberg/fork) · [🐛 Report a bug](https://github.com/biobloomberg/biobloomberg/issues/new)

</div>
