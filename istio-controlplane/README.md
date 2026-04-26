# Istio Control Plane Repository

This Helm chart configure and deploys an Istio Control plane.

##  🎯 Overview

The chart creates the necessary Kubernetes resources to deploy an Istio Control Plane, including:
- Istio CR
- Security configuration (Perrauthentication)
- Telemetry for traces collection
- Security exceptions for Collector 
- Podmonitor for metrics

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Red Hat OpenShift Service Mesh
- Helm 3+

## 📁 Repository Structure
```
istio-controlplane/
├── Chart.yaml
├── values-npt24c01.yaml
└── templates/
    ├── dest-rule-collector.yaml
    ├── dest-rule-istio-mutual.yaml
    ├── istio.yaml
    ├── peer-auth-collector-permissive.yaml
    ├── peer-auth-global-mtls.yaml
    ├── podmonitor.yaml
    ├── servicemonitor.yml
    └── telemetry.yaml
```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `namespace` | Target namespace for  deployment | Yes | - | `istio-system` |
| `istio.meshName` | Istio control plane instance name | Yes | - | `istio-npt24c01` |
| `istio.replicas` | Number of pos| Yes | 2 |  |
| `istio.resources.xxxx ` | resources configuration | Yes |  |  |
| `istio.logging.level` | logging level | No |  |  |
| `collector.port` | Port of the collector for Traces | yes | 1417 |  |

## Installation

### GitOps

Add the Gateway Helm Chart in the target ArgoCD ApplicationSet
Exemple in `../../argocd/apps/{ENV}/istio-npt24c01.yaml` add the following in the generator List to deploy the control plane

```yaml
      - cluster: npt24c01
        url: https://api.npt24c01.corp.bbynuat.com:6443
        values:
          name: istio-controlplane-npt24c01
          chartPath: istio-controlplane
          valuesFile: values-npt24c01.yaml
```
### Bash using HELM CLI
```bash
helm install istio-npt24c01 . -f values-npt24c01.yaml
```