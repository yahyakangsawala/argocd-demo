# Kiali Repository

This Helm chart deploys Kiali and configure the OSSM plugin

##  🎯 Overview

The chart creates the necessary Kubernetes resources to deploy an Istio gateway, including:
- Kiali CR
- RBAC
- OSSMConsole CR

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Red Hat OpenShift Service Mesh
- Helm 3+
- Istio control plane installed

## 📁 Repository Structure
```
gateway/
├── Chart.yaml
├── values-ingress-npt24c01-npt24.yaml
├── values-egress-npt24c01-npt24.yaml
└── templates/
    ├── kiali.yaml
    ├── ossm.yaml
    ├── rbac.yaml

```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `namespace` | Target namespace for gateway deployment | Yes | - | `istio-system` |
| `kiali.name` | Kiali name (used for deployment, service, SA) | Yes | - | `ingressgateway` or `egressgateway` |
| `kiali.tracing` | tracing config (Tempo) | Yes |  |  |
| `tempo.tenant` |Tempo tenant configuration (should match the istio control plane name - see tempo configuration) | Yes |  | istio-npt24c01 |
| `tempo.internal` |Tempo internal url | Yes |  |  |
| `tempo.external` |Tempo external url | Yes |  |  |
| `ossm.name` | OSSMConsole name | Yes |  |  |
| `ossm.kiali` | Kiali service name and port | Yes |  |  |


## Installation

### GitOps

Add the Gateway Helm Chart in the target ArgoCD ApplicationSet
Exemple in `../../argocd/apps/{ENV}/istio-npt24c01.yaml` add the following in the generator List to deploy the control plane

```yaml
      - cluster: npt24c01
        url: https://api.npt24c01.corp.bbynuat.com:6443
        values:
          name: kiali-npt24c01
          chartPath: kiali
          valuesFile: values-npt24c01.yaml
```
### Bash using HELM CLI
```bash
helm install kiali-npt24c01 . -f values-npt24c01.yaml
```