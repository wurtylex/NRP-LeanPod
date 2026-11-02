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
