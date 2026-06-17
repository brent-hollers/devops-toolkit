# 🛠️ DevOps Toolkit & Shared Workflows

This repository serves as a centralized hub for **Reusable GitHub Actions Workflows**. 

Instead of copying and pasting pipeline configurations across dozens of separate projects, we maintain the source-of-truth automation templates here. Downstream repositories can dynamically call these files to inherit changes automatically.

---

## 🎯 Objectives

* **🔒 Enhanced Security:** Continuously adding automated scanning workflows (such as credential exposure checks, static code analysis, and dependency auditing) to catch vulnerabilities before they reach production.
* **⚖️ Code Consistency:** Enforcing uniform build, test, and formatting guardrails across every codebase we work on.
* **🏎️ Efficiency:** If a security rule changes or a tool needs an upgrade, we update it **once** here, and every repository using it instantly benefits from the update.

---

## 📦 Current Workflow Catalog

| Workflow | File Name | Description |
| :--- | :--- | :--- |
| **TruffleHog Secret Scan** | `trufflehog-template.yml` | Scans incremental commit history on Pushes/PRs to prevent API keys and passwords from being leaked. |

*Note: This repository is a living toolkit. More security and utility workflows will be added continually over time.*

---

## 🚀 How to Use a Centralized Workflow

To reference a workflow from this repository in your project repo, create a file at `.github/workflows/security.yml` and point to this repository using the `uses` block:

```yaml
name: Security Audit

on:
  push:
    branches: [ "main", "master" ]
  pull_request:
    branches: [ "main", "master" ]

jobs:
  run-shared-scan:
    # Change username/org to your actual GitHub path
    uses: your-github-username/devops-toolkit/.github/workflows/trufflehog-template.yml@main