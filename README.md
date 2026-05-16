# DevOps Micro-Internship — Interview Q&A

Community-driven repository of interview questions and answers for DevOps engineers — from fundamentals to production-grade AWS platform engineering.

---

## Two ways to participate

| You want to... | Use |
|---|---|
| Share a question you got asked in an interview | **[GitHub Discussions](../../discussions)** — post in the right category, zero setup |
| Debate or improve an existing answer | **[GitHub Discussions](../../discussions)** — reply and upvote |
| Add a polished, well-referenced Q&A permanently | **GitHub Discussions** — maintainers will promote it to a PR |
| Suggest a topic or vote on what to cover next | **[Polls category](../../discussions/categories/polls)** |

**Start in Discussions.** Most community value happens in Discussions. Maintainers promote the best answers into permanent markdown files via PR.

---

## Discussion Categories

Go to [Discussions](../../discussions) and pick the right category:

| Category | Type | Use it for |
|---|---|---|
| **Announcements** | Announcement | New weeks, major updates, monthly highlights — maintainer only |
| **Foundations Q&A** | Q&A | Weeks 00–03: Networking, Linux, Git, DevOps lifecycle |
| **Cloud Platforms Q&A** | Q&A | Weeks 04–05: AWS, Azure |
| **IaC & Automation Q&A** | Q&A | Weeks 06–08: Terraform, Ansible, CI/CD |
| **Containers & Kubernetes Q&A** | Q&A | Weeks 09–10: Docker, Kubernetes |
| **Observability Q&A** | Q&A | Week 11: Prometheus, Grafana, FluentBit, Zipkin |
| **Production AWS Platform Q&A** | Q&A | EKS, Helm, ArgoCD, Karpenter, ECR, RDS, Secrets Manager |
| **Share Your Interview Experience** | Open-ended | "I just got asked X at company Y — here's what they wanted" |
| **Polls** | Poll | Vote on next topics, difficulty preferences, tool popularity |
| **Ideas & Feedback** | Open-ended | Suggest new content, report gaps, give feedback |

**Q&A categories support upvoting and Mark as Answer** — the best answer gets pinned to the top of every thread automatically.

---

## How the two layers connect

```
You get asked a new question in an interview
        ↓
Post it in the right Discussions category  (2 minutes, no setup)
        ↓
Community upvotes answers, maintainer marks the best one
        ↓
Maintainers submit high-quality answers as a PR and merge into markdown files
        ↓
The question lives permanently in the repo, searchable and offline-readable
```

---

## Weeks & Scope

| Week | Topic |
|---|---|
| 00 | Internet, Networking & Basic Tools |
| 01 | Linux for DevOps |
| 02 | Git & GitHub |
| 03 | DevOps Lifecycle |
| 04 | AWS Cloud |
| 05 | Azure Cloud |
| 06 | Terraform (IaC) |
| 07 | Ansible (Configuration Management) |
| 08 | CI/CD with Azure DevOps |
| 09 | Docker (Containerization) |
| 10 | Kubernetes (Deploy & Scale) |
| 11 | Observability |

Advanced topic questions (EKS, Helm, ArgoCD, Karpenter, production AWS) live in the **Production AWS Platform Q&A** Discussion category and in `weeks/week-12` onward as they are contributed and reviewed.

---

## How to contribute a permanent Q&A (Pull Request)

1. Check [Discussions](../../discussions) first — the question may already be answered there.
2. Pick the right week under `weeks/<week>/questions/`.
3. Create a file `Q####-kebab-title.md` with frontmatter and the four sections: Short Answer, Deep Dive, Pitfalls, References.
4. Run validation locally: `python scripts/validate_frontmatter.py && python scripts/build_index.py`
5. Open a Pull Request. CI runs the same checks.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide including setup, frontmatter format, and commit conventions.

---

## Labels

| Label | Meaning |
|---|---|
| `interview-reported` | Someone was actually asked this in a real interview |
| `needs-example` | Answer exists but lacks a real-world example |
| `verified` | Answer reviewed and approved by a maintainer |
| `good first issue` | Easy entry point for first-time contributors |
| `help wanted` | Question needs a better answer — jump in |

---

## Community standards

Be specific. Generic answers lose interviews. Specific answers win them.  
Be respectful. Disagreements on approach are welcome — disrespect is not.  
Cite sources. Official docs and high-quality references only.

See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for full details.
