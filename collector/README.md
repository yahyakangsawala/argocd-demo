# Opentelemetry Collector Repository

This Helm chart configures and deploys an Opentelemetry Collector to collect and send Istio metrics to Tempo

##  🎯 Overview

The chart creates the necessary Kubernetes resources to deploy an Istio gateway, including:
- Collector Custom Resource
- RBAC permissions to allow collector to write in the Tempo tenant

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Red Hat OpenShift Service Mesh 1.26.4
- OpenTelemetry Operator

## 📁 Repository Structure
```
collector/
├── Chart.yaml
├── values-npt24c01.yaml
└── templates/
    ├── collector.yaml
    └── rbac.yaml
```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `namespace` | Target namespace for collector deployment - should be the Istio Control Plane namespace | Yes | - |  |
| `tempo.endpoint` | Tempo endpoint where Istio traces are sent| Yes |  |  |
| `tempo.tenant` | Tempo tenant name where Istio traces are sent| Yes |  |  |

## Installation

### GitOps

Add the Gateway Helm Chart in the target ArgoCD ApplicationSet
Exemple in `../../argocd/apps/ENV/istio-npt24c01.yaml` add the following in the generator List

```yaml
      - cluster: npt24c01
        url: https://api.npt24c01.corp.bbynuat.com:6443
        values:
          name: collector-npt24c01
          chartPath: collector
          valuesFile: values-npt24c01.yaml
```
### Bash using HELM CLI
```bash
helm install collector-npt24c01 . -f values-npt24c01.yaml
```