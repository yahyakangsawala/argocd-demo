# istio-cni Repository

This Helm chart deploys the Istio CNI custom resource

##  🎯 Overview

The chart creates the Istio Deamonset on all nodes 

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Red Hat OpenShift Service Mesh
- Helm 3+

## 📁 Repository Structure
```
istio-cni/
├── Chart.yaml
├── values.yaml
└── templates/
    ├── istio-cni.yaml
```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `namespace` | Deployment namespace | Yes | istio-cni |  |

## Installation

### GitOps

Use the ArgoCD application `../../argocd/apps/{ENV}/istio-cni.yaml`

### Bash using HELM CLI
```bash
helm install istio-cni . -f values.yaml
```