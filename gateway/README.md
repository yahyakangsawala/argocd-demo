# Gateway Repository

This Helm chart deploys an Istio gateway (ingress or egress) with the necessary Kubernetes resources including deployment, service, service account, RBAC roles, and optional TLS configuration. It's designed to work with Red Hat OpenShift Service Mesh.

##  🎯 Overview

The chart creates the necessary Kubernetes resources to deploy an Istio gateway, including:
- Gateway Deployment with Istio proxy
- Service for traffic routing
- Service Account
- RBAC permissions for TLS secrets
- Istio Gateway custom resource
- Optional TLS secrets to configure TLS termination on the Gateway
- Optional Namespace creation

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Red Hat OpenShift Service Mesh
- Helm 3+
- Istio control plane installed
- Gateway Namespace created and labellised with istio-discovery={istio-control-plane-name} and istio.io/rev={istio-control-plane-name} 

## 📁 Repository Structure
```
gateway/
├── Chart.yaml
├── values-ingress-npt24c01-npt24.yaml
├── values-egress-npt24c01-npt24.yaml
└── templates/
    ├── gateway-deploy.yaml
    ├── gateway-service.yaml
    ├── gateway-serviceaccount.yaml
    ├── gateway.yaml
    ├── namespace.yaml
    ├── podmomitor.yaml
    ├── rbac.yaml
    └── tls-secret.yaml
```

## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `namespace.name` | Target namespace for gateway deployment | Yes | - | `istio-gateway-npt24c01-npt24` |
| `namespace.tocreate` | Whether to create the namespace | No | `false` | `true` |
| `namespace.podmonitorinstall` | Whether to create the podmonitor, this should be done once in the namespace | yes | `false` |  |
| `istioInstance` | Istio control plane instance name | Yes | - | `istio-npt24c01` |
| `gateaway.name` | Gateway name (used for deployment, service, SA) | Yes | - | `ingressgateway` or `egressgateway` |
| `gateaway.hosts` | Hosts allowed by the Gateway | Yes | * |  |
| `gateaway.type` | Gateway type | Yes | * | ingress / egress |
| `gateway.resources.xxxx ` | resources (cpu, memory) configuration | Yes | * |  |
| `tls.enable` | Enable TLS secret creation | No | `false` | `true` |
| `tls.mode` | Gateway TLS mode | No | SIMPLE / PASSTHROUGH / DISABLE |  |
| `tls.credentialName` | Name of the TLS secret that holds the Gateway SSL key and cert for applications entry points (OCP routes) | No | `tls-secret` |  |

## Installation

### GitOps

Add the Gateway Helm Chart in the target ArgoCD ApplicationSet
Exemple in `../../argocd/apps/{ENV}/gateways.yaml` add the following in the generator List  to deploy en Ingress Gateway

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
helm install ingressgateway-app-smcp-testing . -f values-ingress-app-smcp-testing.yaml
```