# NRP LeanPod

LeanPod creates persistent Lean 4 development workspaces on the NRP Nautilus Kubernetes cluster.

Each workspace recieves its own compute pod and persistent storage.

Default workspace:

- 7 requested / 8 maximum CPU cores
- 28 GiB requested / 32 GiB maximum memory
- 50 GiB persistent storage
- Lean 4 and Mathlib environment
- Prove2Me workspace cloned automatically

> [!IMPORTANT]
> A running workspace reserves substantial shared NRP resources.
> Stop your workspace when you are not actively using it:
>
> ```bash
> ./leanpod stop YOUR_NAME
> ```
>
> Your persistent files will remain avalible after the pod is stopped.

## Prerequisites

### NRP access

You must:

1. Have an NRP account.
2. Accept the NRP Acceptable Use Policy.
3. Be a member of the `prove2me` NRP project/namespace (ping Kunal for this).
4. Be able to authenticate through CILogon.

### Local software

You'll need the following on your computer:

- Bash
- Git
- `kubectl`
- The `kubectl oidc-login` plugin, also called `kubelogin`
- A web browser for CILogon authentication

### Installation links

Here are some installations links feel free to look for some online specific to your package manager

- [NRP cluster-access setup](https://nrp.ai/documentation/userdocs/start/getting-started/)
- [Install kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Install kubelogin / oidc-login](https://github.com/int128/kubelogin)
- [Install Krew](https://krew.sigs.k8s.io/docs/user-guide/setup/install/)

### Checks
Here are some commands you can use to check 

```bash
# Check kubectl
kubectl version --client

# Check the OIDC login plugin
kubectl oidc-login --help >/dev/null \
  && echo "oidc-login: OK"

# Check NRP authentication and namespace access
kubectl \
  --kubeconfig "$HOME/.kube/nrp-nautilus.config" \
  --context nautilus \
  --namespace prove2me \
  get pods
```

