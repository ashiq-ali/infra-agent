# InfraAgent

**Self-healing Kubernetes copilot — edge AI meets cloud reasoning.**

> Detect cluster anomalies on-device. Reason over your entire infrastructure in the cloud. Auto-remediate before you wake up.

Built for the [NVIDIA London Hackathon 2026](https://www.nvidia.com/) — June 5–7.

## Architecture

```
┌─────────────────────┐     ┌─────────────────────┐     ┌──────────────────┐
│   Edge · DGX Spark  │     │  Cloud · Nemotron    │     │   Action Layer   │
│                     │     │                     │     │                  │
│  Event Watcher      │────▶│  Topology Reasoner  │────▶│  Auto-apply      │
│  Nemotron Edge      │     │  Remediation Planner│     │  Escalate (Slack)│
│  Incident Packager  │     │                     │     │                  │
└─────────────────────┘     └─────────────────────┘     └──────────────────┘
```

**Edge** — Sidecar agent on each node streams kubectl events, pod logs, and resource metrics. Local Nemotron classifies anomalies (CrashLoopBackOff, OOM, scheduling failures) and packages structured incident payloads. Raw data never leaves the node.

**Cloud** — Nemotron reasons over the incident against your Terraform state, node pool configuration, PDBs, and cluster-wide dependencies. Generates a ranked remediation plan.

**Action** — Safe fixes (pod restart, HPA adjustment, node cordon) auto-execute. Destructive operations surface as Slack threads with diff preview and one-click approval.

## Stack

`NVIDIA DGX Spark` · `Nemotron` · `GKE` · `Terraform` · `Kubernetes API` · `Slack API` · `Prometheus` · `Python`

## Product page

The product page is a static site deployable via GitHub Pages.

```bash
# serve locally
cd infraagent
python3 -m http.server 8000
# open http://localhost:8000
```

To deploy on GitHub Pages: Settings → Pages → Source: Deploy from branch → `main` / `root`.

## Author

[Ashiq Ali](https://github.com/ashiq-ali) — Senior Platform Engineer

---

*NVIDIA London Hackathon 2026 · June 5–7*
