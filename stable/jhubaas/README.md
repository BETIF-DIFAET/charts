# JupyterHub as-a-Service HELM chart

> [!NOTE]
> This chart is based from the following [repository](https://github.com/ICSC-Spoke2-repo/HighRateAnalysis-WP5/tree/main/stable/jhub-aas)

This Helm chart is a customization of the "[Zero to Jupyter on k8s](https://z2jh.jupyter.org/en/stable/)".

## Installation guide

### Requirements

* Kubernetes cluster (see [Documentation](https://betif-difaet.readthedocs.io/en/latest/admin_guide.html#turning-the-vms-in-a-k8s-cluster));
* Cert-Manager:
```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.2/cert-manager.yaml
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.2/cert-manager.crds.yaml
```
* Ingress-Controller (`NGINX`):
```bash
helm install ingress-nginx oci://ghcr.io/nginxinc/charts/nginx-ingress --create-namespace --version 1.0.2 -n ingress-nginx
```
* Local-path (storage class):
```bash
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.24/deploy/local-path-storage.yaml
```

### Customize the deployment
Edit the `jhub_config.py` provided in values.yaml in order to customize the jhub configuration. 

### Deploy the JupyterHub service
```bash
git clone git@github.com:BETIF-DIFAET/charts.git
cd charts/stable/jhubaas
helm repo add jupyterhub https://jupyterhub.github.io/helm-chart/
helm dependency build
kubectl create namespace jhub
helm upgrade --install --cleanup-on-fail --namespace jhub jhub ./ 
```
