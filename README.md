# Kubernetes Heketi Gluster

Setup a GlusterFS cluster with Heketi REST API on Kubernetes.

WARNING:
- This role is still in development
- Heketi authentication is not configured at present.

Role Variables
--------------

Defaults: `defaults/main.yml`

Required variables:
- `k8s_heketi_gluster_storage_device`: The underlying raw storage device

Optional variables:
- `k8s_heketi_gluster_default_storageclass`: Should this be the default storage class for dynamically provisioned volumes, default `False`
- `k8s_heketi_gluster_force_dedicated`: Label and taint nodes this role is applied to to restrict use to storage only, default `False`
- `k8s_heketi_gluster_tolerations`: Kubernetes tolerations
- `k8s_heketi_gluster_nodeselector`: Kubernetes node-selector
- `k8s_heketi_gluster_image`: Gluster docker image
- `k8s_heketi_gluster_run_root_tasks`: The original source role could be run without root permissions, set this to `False` to retain this behaviour. In practice this will fail if kernel modules are unloaded so the defautls is `True`.


## Acknowledgements

This role was originally extracted from the KubeNow project: https://github.com/kubenow/KubeNow/tree/3defbe040ad24e50833d87fa9cc843319e5a9adb/playbooks/roles/heketi-gluster

    git filter-branch --prune-empty --subdirectory-filter playbooks/roles/heketi-gluster/ master
