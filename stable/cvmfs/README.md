# CVMFS Helm configuration

> [!NOTE]
> The chart is taken from CERN [CVMFS-CSI v2.0.0](https://github.com/BETIF-DIFAET/cvmfs-csi/tree/release-2.0)

## Installation guide

### Requirements (if not done already)

```bash
git clone git@github.com:BETIF-DIFAET/charts.git
```

### Deploy the CVMFS service

```bash
git clone -b release-2.0 https://github.com/BETIF-DIFAET/cvmfs-csi.git
helm install cvmfs ./cvmfs-csi/deployments/helm/cvmfs-csi -f ./cvmfs/config.yaml -n jhub
kubectl apply -f ./cvmfs/volume-storageclass-pvc.yaml
kubectl apply -f ./cvmfs/cvmfs-idler-daemonset.yaml
```

### Customize the deployment
Edit the `./cvmfs/config.yaml` in order to customize the CVMFS configuration. 


## Uninstall the CVMFS service

> [!WARNING]
> Before uninstalling the Helm package, **delete first** the `cvmfs-idler-daemonset` resource to avoid corrupting
the `cvmfs-idler` pods (causing them to go in Error state, for
SIGKILL).

```bash
kubectl delete daemonset cvmfs-idler-daemonset -n jhub
helm uninstall cvmfs -n jhub
```

