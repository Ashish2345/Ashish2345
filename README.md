<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1220,50:1E3A8A,100:2563EB&height=200&section=header&text=Aashish%20Rayamajhi&fontSize=52&fontColor=ffffff&fontAlignY=34&desc=Senior%20Backend%20%26%20AI%20Engineer%20%C2%B7%20Document%20Intelligence%20%C2%B7%20Distributed%20Systems&descAlignY=56&descSize=16" width="100%" alt="Aashish Rayamajhi" />

<a href="https://merodafa.com"><img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=21&pause=1200&color=2563EB&center=true&vCenter=true&width=760&lines=I+build+AI+that+reads+documents.;Scanned+PDF+in.+Structured+data+out.;600%2B+pages%2C+cited+down+to+the+clause.;Durable+pipelines+that+survive+failure.;Python+%C2%B7+Go+%C2%B7+Temporal+%C2%B7+Kubernetes" alt="What I do" /></a>

</div>

---

## What I do

I build **AI document extraction systems** — software that reads messy, scanned,
600-page documents and turns them into clean structured data you can search and
trust.

The model is the easy part. The engineering is everything around it: OCR that
preserves layout, indexing that survives documents far larger than any context
window, orchestration that resumes instead of restarting, and citations that
prove where every answer came from.

<div align="center">

```mermaid
flowchart LR
    A["📄 Scanned PDF<br/><sub>600+ pages</sub>"] --> B["🔍 OCR<br/><sub>digital + Vision</sub>"]
    B --> C["📝 Markdown<br/><sub>~800K chars</sub>"]
    C --> D["🧠 LLM Indexing<br/><sub>chunked + merged</sub>"]
    D --> E["🌳 Structured Tree<br/><sub>navigable sections</sub>"]
    E --> F["💬 Plain-language Q&A"]
    F --> G["🎯 Cited Answer<br/><sub>mapped to the exact clause</sub>"]

    classDef inp fill:#1E3A8A,stroke:#3B82F6,stroke-width:2px,color:#fff
    classDef mid fill:#0F172A,stroke:#2563EB,stroke-width:2px,color:#E2E8F0
    classDef out fill:#065F46,stroke:#10B981,stroke-width:2px,color:#fff
    class A inp
    class B,C,D,E mid
    class F,G out
```

<sub><i>Extraction pipeline behind <a href="https://merodafa.com"><b>Dafa</b></a>.</i></sub>

</div>

---

## How it runs

A single ingestion is eight steps and twenty-plus minutes of OCR and LLM calls.
Step six failing must not mean starting over. So the pipeline is **durable, not
merely asynchronous** — every step is an idempotent activity with its own retry
policy and checkpoint, and a worker crash resumes mid-document instead of
re-burning the whole job.

<div align="center">

```mermaid
flowchart TB
    subgraph edge["🌐 Edge"]
        NG["Nginx"] --> API["FastAPI<br/><sub>async, typed</sub>"]
    end

    subgraph orch["⚙️ Durable Orchestration"]
        API --> TMP["Temporal<br/><sub>workflow engine</sub>"]
        TMP --> W1["OCR<br/>worker"]
        TMP --> W2["Indexing<br/>worker"]
        TMP --> W3["Embedding<br/>worker"]
    end

    subgraph data["🗄️ Data"]
        W1 --> GFS[("GridFS<br/><sub>source PDFs</sub>")]
        W2 --> MDB[("MongoDB<br/><sub>trees + pages</sub>")]
        W3 --> VEC[("Vector store<br/><sub>retrieval</sub>")]
        API --> RD[("Redis<br/><sub>cache + locks</sub>")]
    end

    subgraph ops["📈 Platform"]
        K8S["Kubernetes<br/><sub>autoscaled workers</sub>"]
        CI["GitHub Actions<br/><sub>test → build → deploy</sub>"]
        OBS["OpenTelemetry<br/>→ Grafana"]
    end

    orch -.-> K8S
    CI -.-> K8S
    orch -.-> OBS

    classDef e fill:#1E3A8A,stroke:#3B82F6,stroke-width:2px,color:#fff
    classDef o fill:#0F172A,stroke:#2563EB,stroke-width:2px,color:#E2E8F0
    classDef d fill:#065F46,stroke:#10B981,stroke-width:2px,color:#fff
    classDef p fill:#3F1D5C,stroke:#A855F7,stroke-width:2px,color:#fff
    class NG,API e
    class TMP,W1,W2,W3 o
    class GFS,MDB,VEC,RD d
    class K8S,CI,OBS p
```

</div>

**What that buys:** partial failure costs one activity, not one document.
Backpressure is a queue depth, not a timeout. Replaying a workflow reproduces a
bug exactly.

---

## Stack

<table align="center">
<tr><td><b>Languages</b></td><td>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

</td></tr>
<tr><td><b>Backend</b></td><td>

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white)
![Celery](https://img.shields.io/badge/Celery-37814A?style=flat-square&logo=celery&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-244C5A?style=flat-square&logo=grpc&logoColor=white)

</td></tr>
<tr><td><b>Orchestration</b></td><td>

![Temporal](https://img.shields.io/badge/Temporal-000000?style=flat-square&logo=temporal&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)

</td></tr>
<tr><td><b>Data</b></td><td>

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=flat-square&logo=elasticsearch&logoColor=white)

</td></tr>
<tr><td><b>AI / ML</b></td><td>

![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=flat-square&logo=googlegemini&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![Vision OCR](https://img.shields.io/badge/Vision_OCR-4285F4?style=flat-square&logo=googlecloud&logoColor=white)

</td></tr>
<tr><td><b>DevOps</b></td><td>

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-844FBA?style=flat-square&logo=terraform&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![GCP](https://img.shields.io/badge/GCP-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)

</td></tr>
<tr><td><b>Observability</b></td><td>

![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?style=flat-square&logo=opentelemetry&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Sentry](https://img.shields.io/badge/Sentry-362D59?style=flat-square&logo=sentry&logoColor=white)

</td></tr>
</table>

---

## Building now

### 🚀 [Dafa](https://merodafa.com) · document intelligence for law & tax

Statutes go in as scanned PDFs. A navigable index of the act comes out — ask a
question in plain language, get an answer anchored to the exact clause.

| | |
|---|---|
| **Ingestion** | 600+ page statutes, upload to queryable index, checkpointed per step |
| **OCR** | Per-page routing — digital text extraction, Google Vision for scans |
| **Indexing** | LLM-built section tree over ~800K characters, chunked and reassembled |
| **Citations** | Every answer mapped back to its region on the source page |
| **Ops** | Containerized workers, autoscaled per queue depth, traced end to end |

---

## Selected work

| Project | What it does |
|---|---|
| 🚀 **[Dafa](https://merodafa.com)** | AI document extraction for legal & tax — OCR, LLM indexing, clause-level citations |
| 📦 **Waybill** | Cargo and courier tracking — shipment lifecycle, route checkpoints, live customer status |
| 📞 **AI-Enabled VOIP System** | Programmable calling with automated call handling and routing |
| 💬 **Omnichannel Communication Platform** | One inbox across voice, SMS, and chat with unified threading |
| 👥 **SaaS HRM** | Multi-tenant HR — payroll, attendance, leave, and asset management |
| 📊 **CRM** | Sales and customer pipeline management with asset valuation |
| 📝 **CMS** | Content management with structured publishing workflows |
| 🦷 **[appointly](https://github.com/Encode-Technologies/appointly)** | Appointment booking and scheduling for dental clinics and salons |
| 📒 **[khatabook](https://github.com/Ashish2345/khatabook)** | Digital ledger — credit/debit bookkeeping for small shops |

---

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=Ashish2345&show_icons=true&count_private=true&hide_border=true&theme=tokyonight&hide_title=true&hide=issues" height="165" alt="stats" />
<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Ashish2345&layout=compact&hide_border=true&theme=tokyonight&langs_count=6" height="165" alt="top languages" />

<img src="https://github-readme-activity-graph.vercel.app/graph?username=Ashish2345&theme=tokyo-night&hide_border=true&area=true" width="98%" alt="activity graph" />

</div>

---

## How I work

- **Durability over cleverness.** If a step can fail, it gets a retry policy and a checkpoint.
- **Explicit beats implicit.** Types and schemas at every boundary; the inside can stay pragmatic.
- **Observable by default.** A system you cannot trace is a system you cannot operate.
- **Reproducible or unfinished.** If it does not come up clean in Docker, it is not done.

Also work in cybersecurity — vulnerability assessment and threat detection.

<div align="center">

### Find me

[![Portfolio](https://img.shields.io/badge/Portfolio-ashish12.com.np-2563EB?style=for-the-badge&logo=googlechrome&logoColor=white)](https://ashish12.com.np)
[![Dafa](https://img.shields.io/badge/Product-merodafa.com-10B981?style=for-the-badge&logo=vercel&logoColor=white)](https://merodafa.com)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2563EB,50:1E3A8A,100:0B1220&height=120&section=footer" width="100%" alt="" />

</div>
