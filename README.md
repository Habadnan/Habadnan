<p align="center">
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:1a73e8,100:06b6d4&height=180&section=header&text=Habib%20Adnan&fontSize=48&fontColor=ffffff&fontAlignY=38&desc=Cloud%20Solutions%20Architecture%20%C2%B7%20Google%20Cloud&descAlignY=60&descSize=18" />
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=20&pause=1200&color=1A73E8&center=true&vCenter=true&width=560&lines=Serverless%2C+event-driven+systems+on+GCP;Everything+in+Terraform;Least-privilege+by+default;Designing+for+cost%2C+scale%2C+and+failure" />
</p>

<p align="center">
  📍 New York &nbsp;·&nbsp; ☁️ Focused on cloud solutions architecture
</p>

I design and build cloud systems end to end: picking the right managed services, writing the infrastructure as code, wiring up CI/CD, and documenting the trade-offs behind each decision.

---

### 🏗️ Featured architecture: Pullup

A mobile app for spontaneous real-life hangouts, running on a **serverless, event-driven Google Cloud backend** that's fully provisioned with **Terraform** and deployed through **GitHub Actions with Workload Identity Federation** (no service account keys).

```mermaid
flowchart LR
    App["📱 Expo app"] -->|"HTTPS + ID token"| API["Cloud Run<br/>API"]
    API --> SQL[("Cloud SQL<br/>Postgres + PostGIS")]
    API --> GCS["Cloud Storage<br/>(private, signed URLs)"]
    GCS --> Vision["Cloud Vision<br/>moderation"]
    API --> Tasks["Cloud Tasks<br/>timers"]
    API --> PS["Pub/Sub"]
    PS --> Worker["Notify worker"] --> FCM["Firebase Cloud<br/>Messaging"]
    PS -.-> DLQ["Dead-letter topic"]
```

<details>
<summary><b>Key design decisions</b> (click to expand)</summary>

| Decision | Why |
|---|---|
| **Cloud Run** over GKE / Compute Engine | Spiky traffic, near zero overnight. Scale-to-zero keeps cost near $0 with no cluster to run. |
| **Cloud SQL + PostGIS** over Firestore | "Hangouts within 5 km that haven't ended" is a geo query. PostGIS handles it with a GiST index. |
| **Pub/Sub** between API and notifications | The API stays fast when push delivery is slow; retries and a dead-letter topic absorb failures. |
| **Cloud Tasks** for expiry and reminders | One task per hangout, fired at the exact time, instead of a cron job scanning the table. |
| **Private bucket + signed URLs** | Uploads go straight to storage, never through the API, and nothing is publicly listable. |
| **One service account per workload** | Least privilege: the API can't send pushes, the worker can't read photos. |
| **`max_instance_count = 5`** | Caps spend and keeps Cloud SQL connections under the tier's limit. |
| **Monitoring + billing budget** | Uptime checks, alerts, and a budget are part of the Terraform, not an afterthought. |

</details>

### 🚧 In progress: CloudPulse

A cloud-native network and infrastructure monitoring platform: a Python agent reporting latency, packet loss, and DNS health to a **Cloud Run** API backed by **Firestore**, with a Next.js dashboard. The roadmap adds Pub/Sub workers, Terraform, CI/CD, reliability testing, and a cost analysis.

---

### 🧰 Cloud & platform

<p align="center">
  <img src="https://skillicons.dev/icons?i=gcp,terraform,docker,githubactions,postgres,firebase,linux&perline=7" />
</p>

**Google Cloud:** Cloud Run · Cloud SQL · Cloud Storage · Pub/Sub · Cloud Tasks · Secret Manager · Artifact Registry · IAM & Workload Identity Federation · Cloud Monitoring · Identity Platform · Firebase

**Practices:** Infrastructure as code · CI/CD · least-privilege IAM · event-driven design · cost controls · observability

**Languages:** Python · TypeScript · Java

<p align="center">
  <img src="https://skillicons.dev/icons?i=python,ts,java,nodejs,react&perline=5" />
</p>

### 🛠️ Other projects

| Project | What it is |
|---|---|
| 🧭 **[CodePilot](https://github.com/Habadnan/CodePilot)** | AI codebase onboarding with summaries, dependency graphs, and RAG-powered Q&A. Containerized with Docker. |
| 🌩️ **[Nimbus](https://github.com/Habadnan/nimbus-lang)** | A programming language from scratch: lexer, parser, bytecode compiler, stack VM, and built-in HTTP servers |
| 🐏 **[RateMyRams](https://github.com/Habadnan/RateMyRams)** | Professor reviews and course insights for Farmingdale State students |

---

<p align="center">
  <img src="https://streak-stats.demolab.com?user=Habadnan&hide_border=true&theme=transparent&ring=1a73e8&fire=06b6d4&currStreakLabel=1a73e8" />
</p>

<p align="center">
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:1a73e8,100:06b6d4&height=100&section=footer" />
</p>
