<div align="center">

# 🛰️ OpenAID Graph

### Every vendor sold you agents. Nobody sold you the off switch.

**The AI Agent Control Plane — inventory, security posture, governance, ALM and analytics for every AI agent your enterprise runs, across Microsoft, AWS, Google and 15+ platforms. One console.**

![Platforms](https://img.shields.io/badge/platforms-15%2B-e8c268?style=flat-square)
![Tests](https://img.shields.io/badge/tests-213%20passing-2fbf71?style=flat-square)
![Runtime](https://img.shields.io/badge/runtime-FastAPI%20%2B%20SSE-5ba8f5?style=flat-square)
![Deploy](https://img.shields.io/badge/deploy-Azure%20Container%20Apps-0078d4?style=flat-square)
![Auth](https://img.shields.io/badge/auth-self--healing-b57edc?style=flat-square)

</div>

---

## 😱 The problem

Makers build Copilot Studio agents and switch teams. Data scientists spin up Azure AI Foundry agents across three resource groups. Someone creates a Bedrock AgentCore harness in a sandbox on a Tuesday. Every one of them has an **identity, connections, and access to your data** — and every vendor only shows you *their* slice.

**What agents exist? Who owns them? What can they reach? What happens if one is compromised?**
Today the answer is four portals, a spreadsheet, and hope. OpenAID Graph is the answer as a product.

---

## ✨ Features

### 🔭 Monitor
- **Live discovery** — agents, identities, environments, child/connected topologies, MCP servers, across every connected platform
- **Drift** — what changed since the last scan
- **Platform News** — live vendor release feeds over SSE, security-flagged, 60-second refresh

### 🛡️ Security
- **Trust Graph** — agents ↔ identities ↔ connections ↔ data in one navigable graph
- **Blast Simulator** — compromise an agent on paper, see the radius before an attacker does
- **Attack Paths** — chained-exposure discovery across the fleet
- **OWASP LLM Top 10** mapping · **Injection Exposure** · **Sprawl & Shadow AI** · **Red Team** probes · **DLP Coverage** · **Continuous Scan** with webhooks

### 🧹 Govern — Agent Hygiene
- **0–100 tenant hygiene score** with letter grade, computed from the three findings every admin community begs for:
  - 🧟 **Orphaned agents** (owner left) — with **one-click owner reassignment** via Microsoft's official Reassign API
  - 💤 **Inactive agents** (90+ days untouched) — your deprecation list, auto-generated
  - 🚪 **Anonymous-access agents** — anyone with the link can drive them

### 🚀 Operate — Pipelines (real ALM for agents)
- Multi-select agents → promote to **any Power Platform environment** or **any Foundry project in any resource group**
- **Preflight checks** (target reachable, token valid, name clashes) before anything runs
- **Live streamed progress bars** (NDJSON server events) per agent + overall, with persisted run history

### 📈 Command Center — analytics leadership screenshots
- Sessions with **week-over-week delta badges** · 14-day trend chart · **busiest-hours heatmap** from real conversation transcripts · agent **leaderboard with sparklines** · environment league table · adoption bars — all hand-built SVG, zero chart libraries

### 🔧 Plumbing that fights back
- **Learning deep links** — portal URLs as candidate lists; one "this one worked" click teaches every future link. Survives Microsoft's portal renames (byte-exact URLs regression-pinned)
- **X-Ray diagnostics** for Foundry and AWS — every endpoint × API-version attempt traced, so a silent zero explains itself
- **Self-healing auth** — freshest-token-wins resolution, 10-minute background re-minting, one-button "Refresh tokens now" recovery
- **Honest connectors** — every connection makes a *real* API call before saying "connected"

---

## 🔌 Integrations

| Cloud / Platform | What gets discovered |
|---|---|
| **Microsoft Copilot Studio** | Agents, components, environments (default-aware), transcripts, owner reassignment |
| **Azure AI Foundry** | Agents (new `/agents` service *and* retiring Assistants surface), hub agents, playground deep links |
| **Azure OpenAI** | Assistants on AOAI endpoints |
| **Power Platform** | Environments (BAP + globaldisco, merged non-destructively), Inventory API ground truth |
| **AWS Bedrock** | Classic Agents **and AgentCore harnesses/runtimes** — stdlib SigV4, no boto |
| **Google Cloud** | Vertex AI agents, Agentspace |
| **Salesforce** | Agentforce bot definitions |
| **ServiceNow** | Now Assist (`sn_aia_*`) agents |
| **OpenAI** | Assistants (v2) |
| **Anthropic** | Agent inventories |
| **n8n** | Workflows with **AI-agent auto-tagging** (LangChain/agent nodes detected) |
| **Slack** | Bot users across the workspace |
| **GitHub · Atlassian · Zendesk · UiPath · Cisco Webex · MCP servers** | Apps, bots, automations, MCP endpoints |

---

## ⚡ Deploy in 60 seconds

```powershell
# prerequisites: az login (once). Docker not required — ACR builds remotely.
Expand-Archive .\openaid-graph.zip -DestinationPath C:\agentnetwork -Force
cd C:\agentnetwork\openaid-graph
.\DEPLOY.ps1
```

One script: runs the test gate → mints every Microsoft token from your own session → builds in ACR → injects and **verifies** each variable on the app → prints your live URL. Sign in once with the device code and discovery starts.

### 🔑 Connecting AWS (the trick everyone misses)

A `bedrock-api-key-…` **cannot list agents** — it's a secret-free blob that can't sign SigV4. Instead, open **CloudShell** (the `[>_]` icon in the AWS console) and run:

```bash
aws configure export-credentials --format process | python3 -c "import json,sys;d=json.load(sys.stdin);print(d['AccessKeyId']+':'+d['SecretAccessKey']+':'+d.get('SessionToken',''))"
```

Paste the printed `ACCESS:SECRET:SESSION` line into the AWS connector (region in the second field). Validation makes a real `ListAgentRuntimes` call before saying "connected" — green is a guarantee, not a vibe.

---

## 🏗️ Under the hood

- **FastAPI + Server-Sent Events** backend, single-file zero-dependency frontend
- **Stdlib-only SigV4 signer** for the AWS control planes
- **MSAL device-flow** auth with silent refresh + background keepalive
- **Deterministic demo mode** for reproducible screenshots
- **213 automated tests**, dual-environment CI (full container deps + bare Windows dev box)
- Deployed on **Azure Container Apps** via a zero-touch, idempotent PowerShell pipeline

## 🎖️ Battle-tested through the churn

Built and hardened **while the ground moved**: the Azure OpenAI Assistants API retirement (Aug 26, 2026), the Bedrock Agents Classic closure (Jul 30, 2026), Microsoft portal renames, and hourly token death — all absorbed by design: new surfaces swept first, candidate links with learning, metadata merges that never downgrade, and X-Ray tracing so nothing fails silently.

---

<div align="center">

### See every agent. Trust what you see. **Fix what you find.**

**Created by Kirolos — Power of Automation** ⚡

</div>
