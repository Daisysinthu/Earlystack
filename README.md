# Earlystack

Installing Prometheus on AWS EKS using helm:
===========================================

1. kubectl create namespace prometheus

2. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

3. helm upgrade -i prometheus prometheus-community/prometheus \
    --namespace prometheus \
    --set alertmanager.persistentVolume.storageClass="gp2",server.persistentVolume.storageClass="gp2"

4. kubectl -n prometheus patch svc prometheus-service -p '{"spec": {"type": "LoadBalancer"}}'

