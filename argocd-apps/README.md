# Service Mesh GitOps Repository
This repository contains ArgoCD configurations for deploying and managing a Red Hat Service Mesh environment using GitOps practices.

##  🎯 Overview
This GitOps repository provides a complete setup for Service Mesh components across multiple environments using ArgoCD Application and ApplicationSet resources. The configuration supports both ingress and egress traffic patterns with comprehensive observability.

## 📁 Repository Structure

```
npt24c01/
├── servicemesh-app-of-apps.yaml
├── istio-cni.yaml
├── istio-npt24c01.yaml
├── observability-plugin.yaml
├── tempo-app.yaml
├── gateways.yaml
├── ingress-bookinfo-app-smcp-testing-npt24c01.yaml
```

## Standalone ArgoCD Applications
These applications have a unique instance per Openshift Cluster 

1. **Root Application [servicemesh-app-of-apps.yaml](servicemesh-app-of-apps.yaml)** <br/> 
The main Application of Applications that orchestrates all non-production environments from the [argocd/apps/nonprod](argocd/apps/npt24c01) directory.

2. **Istio-cni application [istio-cni.yaml](istio-cni.yaml)** <br/> 
Istio Container Network Interface plugin deployment - required for Istio

3. **Tempo application [tempo-app.yaml](tempo-app.yaml)** <br/> 
Manages the Tempo Distributed tracing platform for Istio

4. **observability-plugin [observability-plugin.yaml](observability-plugin.yaml)** <br/> 
Enhanced Traces observability capabilities in the Openshift Console UI


## ArgoCD ApplicationSet

**non-prod-t24 ApplicationSet [istio-npt24c01.yaml](istio-npt24c01.yaml)** <br/> 
Deploys the Istio control plane dedicated instance for the t24 platform. <br/>
This ApplicatioSet manages all Istio T24 instance relatated resources by generating the following ArgoCD applications: <br/>

5. **collector-non-prod-t24** - Telemetry data collection configuration

6. **istio-controlplane-non-prod-t24** - Istio control plane

7. **kiali-non-prod-t24** - Service mesh observability dashboard via Kiali

**gateways ApplicationSet [gateways.yaml](gateways.yaml)** <br/> 
Showcase the Istio Ingress or Egress Gateways deployment through the following applications. <br/>

8. **egressgateway** - Ingress Gateway

9. **ingressgateway** - Egress Gateway

10. **bookinfo-application** - Demo application 
**ingress-rh-docs-app-smcp-testing ApplicationSet [ingress-bookinfo-app-smcp-testing-npt24c01.yaml](ingress-bookinfo-app-smcp-testing-npt24c01.yaml)** <br/> 
Showcase the egress integration for an application using Istio Resources through the following app : <br/> 

11. **istio-ingress-resources** - Ingress Istio resources

**ingress-rh-docs-app-smcp-testing ApplicationSet [ingress-bookinfo-app-smcp-testing-npt24c01.yaml](ingress-bookinfo-app-smcp-testing-npt24c01.yaml)** <br/> 
Showcase the egress integration for an application using Istio Resources through the following app : <br/> 