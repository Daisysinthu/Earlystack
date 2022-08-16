# Earlystack

Installing Prometheus on AWS EKS using helm:
===========================================

1. kubectl create namespace monitoring

2. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

3. helm upgrade -i prometheus prometheus-community/prometheus \
    --namespace monitoring \
    --set alertmanager.persistentVolume.storageClass="gp2",server.persistentVolume.storageClass="gp2"

4. kubectl -n monitoring patch svc prometheus-service -p '{"spec": {"type": "LoadBalancer"}}'

5. kubectl apply -f grafana.yml


Installing filebeat on AWS EKS using ECK:
=========================================

--      Installing ECK on EKS     --

1. kubectl create -f https://download.elastic.co/downloads/eck/2.3.0/crds.yaml

2. kubectl apply -f https://download.elastic.co/downloads/eck/2.3.0/operator.yaml

----    Change the Elasticsearch/Opensearch url and credentials in the filebeat.yml file.  ---

3. kubectl apply -f filebeat.yml
