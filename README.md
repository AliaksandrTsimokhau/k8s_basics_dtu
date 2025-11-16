# k8s_basics_dtu
A concise, hands‑on introduction to Kubernetes fundamentals for DevOps mentoring at DTU. Learn core concepts by applying and inspecting real manifests, using a local cluster, and iterating with kubectl.

Objectives
- Understand Pods, ReplicaSets, Deployments, and Services
- Manage configuration with ConfigMaps and Secrets
- Work with Namespaces, Labels/Selectors, and RBAC basics
- Expose apps via ClusterIP/NodePort and Ingress
- Add readiness/liveness probes and resource requests/limits
- Perform scaling, rolling updates, and rollbacks
- Explore storage with PV/PVC and simple StatefulSets
- Inspect logs, events, and common troubleshooting flows
- Optional: package apps with Helm

Prerequisites
- kubectl (latest), Docker, and a local cluster (kind or Minikube)
- Optional: Helm
- Basic container and YAML knowledge

Quick start
1) Create a local cluster:
    - kind create cluster --name dtu-k8s
    or
    - minikube start
2) Verify access:
    - kubectl cluster-info
    - kubectl get nodes
3) Apply examples step by step:
    - kubectl apply -f <folder-with-manifests>
    - kubectl get all -n <namespace>
    - kubectl describe <resource>/<name>
4) Clean up:
    - kubectl delete -f <folder-with-manifests>
    - kind delete cluster --name dtu-k8s (or minikube delete)

Suggested module flow
- 01 Pods: basics, multi-container patterns
- 02 Deployments: rollout, rollback, strategies
- 03 Services: ClusterIP, NodePort; DNS; selectors
- 04 Config: ConfigMaps, Secrets, env/volume mounts
- 05 Probes & Resources: readiness/liveness, limits/requests
- 06 Ingress & Networking: expose HTTP services
- 07 Storage: PV/PVC, StatefulSet intro
- 08 Observability: logs, events, kubectl debug
- 09 Scaling & Resilience: HPA, PDBs, disruptions
- 10 Helm (optional): charts, values, releases

Verification checklist
- kubectl get/describe shows expected replicas and endpoints
- Probes pass; rollouts complete; traffic reaches the app
- Scaling up/down reflects in Pods and Service endpoints
- Data persists across Pod restarts where applicable

Troubleshooting tips
- kubectl get events -A | tail -n 50
- kubectl logs -f deploy/<name>
- kubectl describe <resource>/<name> for failures
- Check Namespace and Label selectors for mismatches

Resources
- Kubernetes docs: https://kubernetes.io/docs/
- kubectl reference: https://kubernetes.io/docs/reference/kubectl/
- Helm docs: https://helm.sh/docs/
- Kind: https://kind.sigs.k8s.io/ | Minikube: https://minikube.sigs.k8s.io/