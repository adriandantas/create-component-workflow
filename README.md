# create-microservice-workflow

Sample automation for creating a microservice repository from a template using Argo Workflows.

### Prerequisites

- [Docker for Desktop](https://www.docker.com/products/docker-desktop/)
- Kubernetes v1.27.2
- [Argo Workflows](https://argoproj.github.io/argo-workflows/) v3.4.9
- [Argo CLI](https://argoproj.github.io/argo-workflows/walk-through/argo-cli/) v3.4.9

This demo was tested on Kubernetes running on Docker for Desktop. Before you begin, make sure you have a Kubernetes
enabled on Docker. Follow the instruction to install Argo Workflows and Argo CLI.

### Running the demo
Create a port-forward to the Argo Workflows server:
```shell
kubectl -n argo port-forward deployment/argo-server 2746:2746
```

**This step should only be used on a local cluster for demo purposes.**

Create a role binding to allow Argo Workflows to create resources in the `argo` namespace:
```shell
kubectl create rolebinding default-admin --clusterrole=admin --serviceaccount=argo:default --namespace=argo
```

Submit workflow using Argo CLI¶
```shell
argo submit \
  -n argo \
  --watch \
  create-microservice-workflow.yaml \
  --parameter service-name="my-service" \
  --parameter owner-username="adriandantas" \
  --parameter team="development" \
  --parameter description="Sample microservice"
```

