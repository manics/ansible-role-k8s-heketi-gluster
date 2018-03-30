# Kubernetes Heketi Gluster

Setup a GlusterFS cluster with Heketi REST API on Kubernetes.

WARNING:
- This role is still in development
- Several tasks always show as changed, however it should be safe to rerun this role after it has successfully completed once
- Heketi authentication is not configured at present.

This is a two stage deployment following https://github.com/heketi/heketi/blob/v6.0.0/docs/admin/install-kubernetes.md

The first stage is to deploy a temporary bootstrap Heketi instance to create a storage volume on Gluster for Heketi's database.
This Kubernetes deployment is called `deploy-heketi`.

The bootstrapped Heketi is then deleted and replace by the final Heketi Kubernetes deployment, called `heketi`.


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
- `k8s_heketi_gluster_kubectl`: The `kubectl` binary including the full path if necessary
- `k8s_heketi_gluster_namespace`: Namespace for all components, default `storage-heketi`


## Acknowledgements

This role was originally extracted from the KubeNow project: https://github.com/kubenow/KubeNow/tree/3defbe040ad24e50833d87fa9cc843319e5a9adb/playbooks/roles/heketi-gluster

    git filter-branch --prune-empty --subdirectory-filter playbooks/roles/heketi-gluster/ master

Further additions including the two stage deployment come from https://github.com/heketi/heketi/blob/v6.0.0/extras/kubernetes/
