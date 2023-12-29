# Building the GitOps Lab Infrastructure Codebase

_Note:_ The commands below just for this project, use them as references.

To build and deploy the GitOps Lab Infrastructure using Flux CD, follow these steps:

1. **Prerequisites:**

- Install `kubectl` to interact with the Kubernetes cluster.
- Install `flux` CLI to bootstrap and manage the Flux CD components.

2. **Bootstrap Flux CD in the Cluster:**
   Execute the following command, replacing `<cluster-name>` and `<path-to-your-repo>` with your details:

```shell
    flux bootstrap github \
    --owner=<your-github-username> \
    --repository=<your-repo-name> \
    --branch=main \
    --path=clusters/<cluster-name> \
    --personal
    --auth-token (try this if you have problems with SSH)
```

3. **Create Namespaces and Resources:** Apply the namespace and resources defined in the YAML files:

```shell
    kubectl apply -f clusters/my-cluster/preprod/simple-app/gitops-lab-app-ns.yaml
```

4. **Configure Git Repository Source:** Define where your Kubernetes manifests are stored:

```shell
    kubectl apply -f clusters/my-cluster/preprod/simple-app/gitops-lab-app-source.yaml
```

5. **Set Up Kustomization:** Define how your manifests are applied to the cluster:

```shell
    kubectl apply -f clusters/my-cluster/preprod/simple-app/gitops-lab-app-kustomization.yaml
```

6. **Verify Deployment:** Check the status of the resources to ensure they have been applied successfully:

```shell
    flux get sources git
    flux get kustomizations
```

For more detailed instructions, refer to the individual YAML files within the `clusters/my-cluster/preprod/` directory.
