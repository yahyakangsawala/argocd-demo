# Istio applications resources integration Repository

This Helm chart deploys the reauired resources to allow application onboarding in Mesh

##  🎯 Overview

The chart creates the istioresources such as
- VirtualService
- DestinationRule
- ServiceEntry

These resources are created in the Application Namespace

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Red Hat OpenShift Service Mesh Controlplane
- Istio Gateway
- Helm 3+
- Application Namespace or Worloads labellised with istio-discovery={istio-control-plane-name} and istio.io/rev={istio-control-plane-name} 

## 📁 Repository Structure
```
istio-resources/
├── Chart.yaml
├── values-egress-app-smcp-testing-npt24c01.yaml
├── values-ingress-app-smcp-testing-npt24c01.yaml
└── templates/
    ├──egress-destination-rule.yaml
    ├── egress-service-entry.yaml
    ├──egress-virtualservice.yaml
    ├──ingress-canary-destination-rule.yaml
    ├──ingress-canary-virtual-service.yaml
    ├──ingress-virtualservice.yaml
```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `gateway.type` | Gateway type | Yes | ingress or egress |  |
| `gateway.name` | Gateway name | Yes | ingress or egress |  |
| `gateway.namespace` | Gateway deployment namespace | Yes |  | `ingress-gateway-npt24c01-npt24` |
| `gateway.host` | Ingress host for the application | Yes | ingress or egress |  |
| `service.name` | Application OCP Service Name | Yes | ingress or egress |  |
| `service.namespace` |  Application deployment and service namespace | Yes |  |  |

## Installation

### GitOps


Add the Gateway Helm Chart in the target ArgoCD ApplicationSet
Exemple in `../../argocd/apps/{ENV}/ingress-bookinfo-app-smcp-testing-npt24c01.yaml` add the following in the generator List to create the Resources

```yaml
      - cluster: npt24c01
        url: https://api.npt24c01.corp.bbynuat.com:6443
        values:
          name: istio-ingress-resources-npt24c01
          chartPath: istio-apps-resources
          valuesFile: values-ingress-app-smcp-testing-npt24c01.yaml

```

### Bash using HELM CLI
```bash
helm install istio-ingress-resources-npt24c01 . -f ingress-bookinfo-app-smcp-testing-npt24c01.yaml
```