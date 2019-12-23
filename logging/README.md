# EFK stack

Store all logs from all pods running in system

## Install

Create namespace

```code
kubectl apply -f namespace.yaml
```

### Elastic

Create Storage: use local-storage class. It cannot use dynamic provisioning PV. We need static provisioning.

```code
kubectl apply -f elasticsearch/storage.yaml
```

Create Statefulset

```code
kubectl apply -f elasticsearch/statefulset.yaml
```

You can monitor the StatefulSet as it is rolled out using kubectl rollout status

```code
kubectl rollout status sts/es-cluster --namespace=logging
```

Create headless service

```code
kubectl apply -f elasticsearch/service.yaml
```

Test ES

```code
kubectl port-forward es-cluster-0 9200:9200 --namespace=logging
```

```code
curl http://localhost:9200/_cluster/state?pretty
```

### Kibana

Install

```code
kubectl apply -f kibana/deployment.yaml
```

Access Kibana via NodePort: 30001

### FluentD Daemonset

Install

```code
kubectl apply -f fluentd/service-account.yaml
kubectl apply -f fluentd/daemonset.yaml
```

## Setup Kibana

Go to kibana, create index `logstash-*`
