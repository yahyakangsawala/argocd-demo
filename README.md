# OpenShift Servicemesh GitOps Infrastructure

This repository contains GitOps infrastructure configurations for Boubyan's OpenShift environment. It provides automated deployment and management of ServiceMesh, Tempo, Kiali, Collectors configurations, and supporting infrastructure components using ArgoCD and Helm.

The repository is designed to support multiple Servicemesh deployments while maintaining security and operational best practices.

## 🚀 Features

- ✅ **GitOps Automation**: Declarative resources management with ArgoCD and Helm
- ✅ **Multi-Environment**: Helm values based environment separation
- ✅ **ServiceMesh Controlplane Automation**: Declarative ServiceMesh Control Plane resources management
- ✅ **ServiceMesh Gateways Automation**: Declarative ServiceMesh Gateways resources management
- ✅ **Tempo Automation**: Declarative Tempo resources management
- ✅ **Kiali Automation**: Declarative Kiali resources management
- ✅ **Applications Integration**: Declarative application integration to ServiceMesh using Istio resources

## 📁 Repository Structure

```
├── appplications-demo
├── argocd                             # ArgoCD applications
├── collector                          # Istio Traces collector deployment 
├── gateway                            # Ingress and Egress Gateways deployment
├── istio-apps-resources               # Application integration Istio Resources (VirtualService, DestinationRule, ServiceEntry, ...)
├── istio-cni                          # Istio CNI deamonset deployment
├── istio-controlplane                 # Istio Controlplane configuration and deployment
├── kiali                              # Kiali deployment
├── observability-plugin               # Observability pluing configuration (Traces menu activation)
├── tempo                              # Tempo Istio Platform deployment
```

## 🔧 Prerequisites

- **Cluster**: OpenShift 4.18 
- **Argo CD**: AgroCD installed
- **Following Operators installed**
   1. **Red Hat Service Mesh 3 Operator**
   2. **Kiali Operator**
   3. **Tempo Operator**
   4. **Red Hat build of OpenTelemetry Operator**
   5. **Cluster Observability Operator**
- **Local Tools**: `oc`, `git`, `helm`, `jq`, `argocd` CLI
- **Optional**: `podman` (for Image management)

## How to deploy and configure the ServiceMesh platform
To deploy a complete Istion instance, use the [argocd/apps](argocd/apps) folder to configure the environment ArgoCD Applications. Each environment should have a dedicated subfolder (nonprod, prod, ...)
