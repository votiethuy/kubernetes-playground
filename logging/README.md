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
