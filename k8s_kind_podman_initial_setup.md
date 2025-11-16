# Learning Environment Preparation

Follow these steps to set up your Kubernetes learning environment with all required tools.

## 1. Install Podman

- [Podman Desktop Downloads](https://podman-desktop.io/downloads)
- [Podman Installation Guide](https://podman.io/docs/installation)

## 2. Install Kind (Kubernetes IN Docker/Podman)

- [Kind Quick Start Guide](https://kind.sigs.k8s.io/docs/user/quick-start)
- Note: Kind can run with Docker or Podman as the container runtime.

## 3. Install kubectl (Kubernetes CLI)

- [kubectl Installation Instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)

## 4. Install Helm (Kubernetes Package Manager)

- [Helm Installation Guide](https://helm.sh/docs/intro/install/)

## 5. Install freelens (Kubernetes IDE)

- [freelens GitHub Repository](https://github.com/freelensapp/freelens?tab=readme-ov-file#windows)

## Prerequisites

- [Install kind](https://kind.sigs.k8s.io/)
- [Ingress documentation for kind](https://kind.sigs.k8s.io/docs/user/ingress/)
- [Install Metrics Server on kind](https://maggnus.com/install-metrics-server-on-the-kind-kubernetes-cluster-12b0a5faf94a)
- [Example Gist: Metrics Server on kind](https://gist.github.com/sanketsudake/a089e691286bf2189bfedf295222bd43)


# Create Cluster

```bash
export KIND_EXPERIMENTAL_PROVIDER=podman
```

Create a kind cluster with extraPortMappings and node-labels.

    extraPortMappings allow the local host to make requests to the Ingress controller over ports 80/443
    node-labels only allow the ingress controller to run on a specific node(s) matching the label selector

```bash
cat <<EOF | kind create cluster --name k8s-playground --config=-
# three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
  extraPortMappings:
  - containerPort: 80
    hostPort: 80
    protocol: TCP
  - containerPort: 443
    hostPort: 443
    protocol: TCP
- role: worker
- role: worker
EOF
```
