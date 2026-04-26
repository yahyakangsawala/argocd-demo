# observability plugin Repository

This Helm chart configure the observability plugin for traces

##  🎯 Overview

The chart creates the UIPlugin CR

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Tempo


## 📁 Repository Structure
```
observability-plugin/
├── Chart.yaml
├── values.yaml
└── templates/
    ├── tracing-plugin.yaml
```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `type` | Deployment namespace | Yes | DistributedTracing |  |

## Installation

### GitOps

Use the ArgoCD application `../../argocd/apps/{ENV}/observability-plugin.yaml`

### Bash using HELM CLI
```bash
helm install observability-plugin-npt24c01. -f observability-plugin.yaml
```