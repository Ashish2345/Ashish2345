<div align="center">

<img src="assets/banner.svg" width="100%" alt="Aashish Rayamajhi — Senior Backend & AI Engineer" />

<img src="assets/typing.svg" width="780" alt="I build agents that read the fine print" />

</div>

---

## What I do

I build **agentic AI systems for documents** — end-to-end workflows that take
unstructured, scanned, multilingual source material and turn it into structured
data a business can act on.

I have worked on complex document workflows end to end: ingestion, OCR,
normalization, retrieval, LLM reasoning, and the durable orchestration that keeps
a twenty-minute multi-step job alive when step six fails. The model is the easy
part — the engineering is everything around it.

---

## 🚀 [Dafa](https://merodafa.com) · regulatory compliance intelligence

Regulations change constantly, across dozens of government portals, in two
languages, as scanned PDFs. Dafa watches all of it and tells a compliance officer
what changed, what it means for *their* business, and by when.

```mermaid
flowchart LR
    S["🌐 Gov portals<br/><sub>daily crawl, per country</sub>"] --> O["🔍 OCR<br/><sub>scanned + bilingual</sub>"]
    O --> T["🗣️ Legal translation<br/><sub>precision over fluency</sub>"]
    T --> DD["♻️ Deduplication<br/><sub>same directive, 5 portals</sub>"]
    DD --> DF["📊 Change detection<br/><sub>diff old vs new</sub>"]
    DF --> CL["🏷️ Classification<br/><sub>industry · company type</sub>"]
    CL --> XR["🔗 Cross-reference<br/><sub>amends Section 47 of Act X</sub>"]
    XR --> EX["📋 Field extraction<br/><sub>effective date · penalty · filing</sub>"]
    EX --> IA["🧠 Impact analysis<br/><sub>LLM + customer context</sub>"]
    IA --> AL["🔔 Alerting<br/><sub>compliance officer, within hours</sub>"]

    classDef src fill:#1E3A8A,stroke:#3B82F6,stroke-width:2px,color:#fff
    classDef mid fill:#0F172A,stroke:#2563EB,stroke-width:2px,color:#E2E8F0
    classDef out fill:#065F46,stroke:#10B981,stroke-width:2px,color:#fff
    class S src
    class O,T,DD,DF,CL,XR,EX mid
    class IA,AL out
```

| Capability | What it means in practice |
|---|---|
| **Daily acquisition** | Scheduled crawl of every major government portal, per country |
| **Bilingual OCR** | Scanned PDFs in mixed-language layouts — the hard case, and the edge |
| **Legal translation** | Translation tuned for legal precision, not readability |
| **Change detection** | Structural diff between old and new versions of a regulation |
| **Classification** | Which industries and company types does this actually affect? |
| **Cross-referencing** | Resolves "this circular modifies Section 47 of Act X" into a real link |
| **Deduplication** | One directive published across five portals collapses to one record |
| **Field extraction** | Effective date, penalty, filing requirement — as structured fields |
| **Impact analysis** | Given a customer's business context, what does this change mean for them? |
| **Alerting** | Compliance officer notified within hours of publication |

---

## How the agent layer works

Compliance answers cannot be one LLM call. A supervisor decomposes the question,
specialist agents work in parallel against real tools, and a critic agent rejects
weak output back to the planner. Every step is traced, scored, and replayable —
if an answer was wrong last Tuesday, I can reproduce exactly why.

```mermaid
flowchart TB
    subgraph plan["🧭 Planning"]
        SUP["Supervisor agent<br/><sub>LangGraph state machine</sub>"]
    end

    subgraph deep["🤖 Deep agents"]
        A1["Research<br/>agent"]
        A2["Diff<br/>agent"]
        A3["Impact<br/>agent"]
        A4["Critic<br/>agent"]
    end

    subgraph tool["🛠️ Tools"]
        MCP["MCP servers"]
        RET["Hybrid retrieval<br/><sub>vector + keyword</sub>"]
        STO[("Structured store")]
    end

    subgraph eval["📈 Tracing &amp; evals"]
        LF["Langfuse<br/><sub>traces · cost · scores</sub>"]
        RG["Regression suite<br/><sub>golden answers</sub>"]
    end

    SUP --> A1
    SUP --> A2
    SUP --> A3
    A1 --> A4
    A2 --> A4
    A3 --> A4
    A4 -->|"reject → replan"| SUP
    A4 -->|"accept"| OUT["✅ Cited answer"]

    A1 --> MCP
    A2 --> RET
    A3 --> STO
    deep -.-> LF
    LF --> RG

    classDef p fill:#3F1D5C,stroke:#A855F7,stroke-width:2px,color:#fff
    classDef a fill:#0F172A,stroke:#2563EB,stroke-width:2px,color:#E2E8F0
    classDef t fill:#1E3A8A,stroke:#3B82F6,stroke-width:2px,color:#fff
    classDef o fill:#065F46,stroke:#10B981,stroke-width:2px,color:#fff
    class SUP p
    class A1,A2,A3,A4 a
    class MCP,RET,STO t
    class LF,RG,OUT o
```

**Why it is built this way:** a critic loop catches confident nonsense before a
customer sees it. Tracing makes cost and latency per agent visible instead of
mysterious. And a golden-answer regression suite means a prompt change cannot
silently degrade an answer that used to be right.

---

## Stack

<table align="center">
<tr><td><b>Languages</b></td><td>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

</td></tr>
<tr><td><b>Agentic&nbsp;AI</b></td><td>

![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![Langfuse](https://img.shields.io/badge/Langfuse-0A0A0A?style=flat-square&logo=langfuse&logoColor=white)
![MCP](https://img.shields.io/badge/MCP-D97757?style=flat-square&logo=modelcontextprotocol&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white)

</td></tr>
<tr><td><b>Models&nbsp;&amp;&nbsp;OCR</b></td><td>

![Claude](https://img.shields.io/badge/Claude-D97757?style=flat-square&logo=anthropic&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=flat-square&logo=googlegemini&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![Vision OCR](https://img.shields.io/badge/Vision_OCR-4285F4?style=flat-square&logo=googlecloud&logoColor=white)

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

## Selected work

| Project | What it does |
|---|---|
| 🚀 **[Dafa](https://merodafa.com)** | Regulatory compliance intelligence — crawl, bilingual OCR, change detection, LLM impact analysis, alerting |
| 📦 **Waybill** | Cargo and courier tracking — shipment lifecycle, route checkpoints, live customer status |
| 📞 **AI-Enabled VOIP System** | Programmable calling with automated call handling and routing |
| 💬 **Omnichannel Communication Platform** | One inbox across voice, SMS, and chat with unified threading |
| 👥 **SaaS HRM** | Multi-tenant HR — payroll, attendance, leave, and asset management |
| 📊 **CRM** | Sales and customer pipeline management with asset valuation |
| 📝 **CMS** | Content management with structured publishing workflows |
| 🦷 **[appointly](https://github.com/Encode-Technologies/appointly)** | Appointment booking and scheduling for dental clinics and salons |
| 📒 **[khatabook](https://github.com/Ashish2345/khatabook)** | Digital ledger — credit/debit bookkeeping for small shops |

---

## How I work

- **Durability over cleverness.** If a step can fail, it gets a retry policy and a checkpoint.
- **Evals before vibes.** An agent without a regression suite is a demo, not a product.
- **Explicit beats implicit.** Types and schemas at every boundary; the inside can stay pragmatic.
- **Observable by default.** A system you cannot trace is a system you cannot operate.
- **Reproducible or unfinished.** If it does not come up clean in Docker, it is not done.

Also work in cybersecurity — vulnerability assessment and threat detection.

<div align="center">

### Find me

[![Portfolio](https://img.shields.io/badge/Portfolio-ashish12.com.np-2563EB?style=for-the-badge&logo=googlechrome&logoColor=white)](https://ashish12.com.np)
[![Dafa](https://img.shields.io/badge/Product-merodafa.com-10B981?style=for-the-badge&logo=vercel&logoColor=white)](https://merodafa.com)

</div>
