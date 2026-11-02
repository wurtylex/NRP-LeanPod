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

## Setup

Clone the repository and enter its directory:

```bash
git clone https://github.com/wurtylex/NRP-LeanPod
cd NRP-LeanPod
```

Create your local configuration file:

```bash
cp leanpod.env.example leanpod.env
```

You can edit `leanpod.env` to change your local defaults.

Verify your NRP access and local configuration:

```bash
./leanpod doctor
```

## Create your first workspace

Choose a unique workspace name. The cast of characters in [Alice and Bob](https://en.wikipedia.org/wiki/Alice_and_Bob) is always a good option.

Workspace names should contain only lowercase letters, numbers, and hyphens.

```bash
./leanpod create YOUR_NAME
```

For example:

```bash
./leanpod create wurtle
```

Watch the initial setup:

```bash
./leanpod logs YOUR_NAME
```

Wait until the workspace is ready:

```bash
./leanpod wait YOUR_NAME
```

Open a terminal inside the workspace:

```bash
./leanpod shell YOUR_NAME
```

## Stop your workspace

When you are finished, stop the workspace so it no longer reserves CPU and memory:

```bash
./leanpod stop YOUR_NAME
```

Your files remain on persistent storage.

Start it again later with:

```bash
./leanpod start YOUR_NAME
./leanpod wait YOUR_NAME
./leanpod shell YOUR_NAME
```

## More commands

View all available commands and options:

```bash
./leanpod --help
```

You can also view help for an individual command:

```bash
./leanpod create --help
./leanpod resize --help
```
