# Tempo Repository

This Helm chart deploys and configure Tempo

##  🎯 Overview

The chart creates the the resources for tempo such as 
- Tempo Custom Resource
- RBAC for tenant data writing
- S3 Object Bucket Claim
- Secret holding the bucket credentials

## 🔧 Prerequisites

- Kubernetes/OpenShift cluster
- Tempo Operator
- Helm 3+

## 📁 Repository Structure
```
tempo/
├── Chart.yaml
├── values-npt24c01.yaml
└── templates/
    ├── rbac-gateway.yaml
    ├── 343 rbac-resources-readonly.yaml
    ├── rbac-traces-readonly.yaml
    ├── tempo-bucket-claim.yaml
    ├── tempo-s3-secret.yaml
    ├── tempo.yaml
```
## Values

| Parameter | Description | Required | Default | Example |
|-----------|-------------|----------|---------|---------|
| `tempo.name` | tempo instance name | Yes | tempo |  |
| `tempo.replicationFactor` | Num ber of replics| Yes | 1 |  |
| `tempo.storageSize` | Size of persistent volume for Tempo local data | Yes | istio-tempo |  |
| `tempo.retention` |Retention period for traces | Yes | 48 hours in this case |  |
| `tempo.replicas` | internal tempo replicas configuration | Yes | 1 |  |
| `storage.type` | Backend storage type | Yes | s3|  |
| `storage.secretName` | Name of the Kubernetes secret holding S3 credentials | Yes | |  |
| `storage.bucket` | S3 bucket for Tempo trace storage | Yes |  |  |
| `storage.endpoint` | S3 service endpoint (internal cluster service) | Yes | https://s3.openshift-storage.svc   |  |
| `storage.accessKeyId` | S3 access key ID (from secret) | Yes |  |  |
| `storage.accessKeySecret` | S3 secret key (from secret) | Yes | |  |
| `storage.storageClassName` | Storage class used for persistent volumes | Yes |  |  |
| `tenants.name` | Tenant name ( matches the Istio instance) | Yes |  | istio-npt24c01 |
| `tenants.id` | Unique identifier for this tenant - random generation | Yes |  |  |

## Installation

### GitOps

Use the ArgoCD application `../../argocd/apps/{ENV}/tempo-app.yaml`
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: tempo-npt24c01
  namespace: openshift-gitops
spec:
  destination:
    namespace: openshift-gitops
    server: 'https://api.npt24c01.corp.bbynuat.com:6443'
  project: default
  source:
    helm:
      valueFiles:
        - values-npt24c01.yaml
    path: tempo
    repoURL: 'https://swan02.corp.boubyan.com:7991/scm/opt/np-servicemesh.git'
    targetRevision: master
  syncPolicy:
    automated:
      selfHeal: true
    retry:
      backoff:
        duration: 5s
        factor: 2
        maxDuration: 20m
      limit: 5
```

### Bash using HELM CLI
```bash
helm install tempo . -f values-npt24c01.yaml
```