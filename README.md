# Basic Kube Prometheus Stack Helm Config

## Reference github repo:
https://github.com/prometheus-community/helm-charts/tree/kube-prometheus-stack-43.2.1/charts/kube-prometheus-stack
https://github.com/prometheus-community/helm-charts/blob/kube-prometheus-stack-43.2.1/charts/kube-prometheus-stack/values.yaml

## Helm Chart Install
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

kubectl create namespace monitoring
helm upgrade --install kube-prometheus-stack prometheus-community/kube-prometheus-stack --version 43.2.1 -n monitoring -f values.yaml

## Port Fowarding
kubectl port-forward -n monitoring service/kube-prometheus-stack-grafana 3000:80
kubectl port-forward -n monitoring service/kube-prometheus-stack-prometheus 9090:9090
kubectl port-forward -n monitoring service/kube-prometheus-stack-alertmanager 9093:9093

## Add additional alertmanager config and prometheus rules
kubectl apply -f alert-manager-config-example.yaml
kubectl apply -f prometheus-rule-config-example.yaml