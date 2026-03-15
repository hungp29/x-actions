# Common GitHub Actions Workflows

This repository contains **reusable GitHub Actions workflows** that can be shared across multiple repositories.

The goal is to centralize CI/CD logic so that application repositories can stay clean and only reference these workflows.

---

# Overview

This repository provides reusable workflows for common CI/CD tasks such as:

* Create Pre-Release
* Build Go applications

All workflows are designed to be consumed via `workflow_call`.

---

# Repository Structure

```
.
├── .github
│   └── workflows
│       ├── go-production.yaml
│       ├── pre-release.yaml
```

Each file inside `.github/workflows` represents a reusable workflow.

---

# Usage

To use a workflow from this repository, reference it using the `uses` keyword.

Example:

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    uses: <org-or-user>/<repo>/.github/workflows/go-production.yaml@v1.0.0
```

Example with inputs:

```yaml
jobs:
  build:
    uses: <org-or-user>/<repo>/.github/workflows/go-production.yaml@v1.0.0
    with:
      contract-file: .github/config/ci.yaml
```

---

# Workflow Inputs

Each workflow may define its own inputs and secrets.

Example:

```yaml
on:
  workflow_call:
    inputs:
      image_name:
        required: true
        type: string
```

Refer to the workflow file documentation for details.

---

# Versioning

Workflows should be referenced using a **tag** or **release version**:

```
@v1.0.0
@v1.2.0
```

This prevents unexpected breaking changes.

Example:

```yaml
uses: <org-or-user>/<repo>/.github/workflows/go-production.yaml@v1.0.0
```

---

# Updating Workflows

When making changes:

1. Update the workflow in this repository
2. Create a new tag or release
3. Consumers can upgrade when ready

---

# Best Practices

* Keep workflows **generic and reusable**
* Use **inputs** instead of hardcoded values
* Avoid repository-specific configuration
* Document required **secrets**

---

# Example Repositories Using These Workflows

* service-a
* service-b
* service-c

---

# License

This repository is licensed under the MIT License.
