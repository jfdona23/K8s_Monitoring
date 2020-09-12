# Prometheus Operator

* GitHub repo: https://github.com/prometheus-operator/prometheus-operator.
* Helm chart info: https://hub.helm.sh/charts/prometheus-com/kube-prometheus-stack.
* In order to deploy the Operator using Hhelm you first need to run:
```bash
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com/
$ helm repo update
```
* Recommended: Create a namespace for Prometheus
```bash
$ kubectl create namespace <your-namespace>
```
* An then install the chart with:
```bash
$ helm install <your-chart-name> prometheus-community/kube-prometheus-stack --namespace <your-namespace>
```
* Then you can access Grafana by creating an Ingress rule or by port-forwad:
```bash
$ kubectl port-forward deployment/<your-prometheus-grafana-dpeloyment> 3000
```
* Same to access Prometheus UI:
```bash
$ kubectl port-forward deployment/<your-prometheus-operator-dpeloyment> 9090
```

## Removing the chart
You need to remove the chart and then manually remove the created CRDs.
```bash
$ helm uninstall <your-chart-name> --namespace <your-namespace>
$ kubectl delete crd {\
prometheuses.monitoring.coreos.com,\
prometheusrules.monitoring.coreos.com,\
servicemonitors.monitoring.coreos.com,\
podmonitors.monitoring.coreos.com,\
alertmanagers.monitoring.coreos.com,\
thanosrulers.monitoring.coreos.com\
}
```

## Upgrading the cart
```bash
$ helm upgrade <your-chart-name> prometheus-community/kube-prometheus-stack --namespace <your-namespace>
```
**Note:** A major chart version change (like v1.2.3 -> v2.0.0) indicates that there is an incompatible breaking change needing manual actions.

## ARM Suppport
Some of the operator images and its sub-charts are not ARM compatible. Although, this could change in the future.
GitHub issues:
* https://github.com/prometheus-operator/prometheus-operator/issues/2946
* https://github.com/prometheus-operator/prometheus-operator/pull/3177
* https://github.com/prometheus-operator/prometheus-operator/issues/3162
Alternative project including ARM images:
* https://github.com/uocxp/prometheus-operator-chart-arm
