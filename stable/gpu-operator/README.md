# GPU Operator Helm configuration

> [!NOTE]
> The chart is taken from [NVIDIA GPU operator repository](https://github.com/NVIDIA/gpu-operator)

## Installation guide

### Requirements (if not done already)

```bash
git clone https://github.com/BETIF-DIFAET/charts.git
```

### Deploy the GPU operator service

```bash
kubectl create namespace gpu-operator
kubectl create -f ./gpu-operator/time-slicing-config.yaml
kubectl create -f ./gpu-operator/gpu-operator.yaml
```

## Uninstall the CVMFS service

```bash
kubectl delete helmchart gpu-operator -n kube-system
helm delete namespace gpu-operator
```