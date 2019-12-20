# K8s-playground

Kubernetes Playground

## Install

Using kubeadm. [Official docs](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
Network Flannel

```code
kubeadm init --pod-network-cidr=10.244.0.0/16
```

Save the token to join node

Install CNI

```bash
kubectl apply -f https://docs.projectcalico.org/v3.10/manifests/canal.yaml
```

Join node command

```bash
kubeadm join 10.163.60.19:6443 --token skyc80.lt2qt018er4ghnlu \
    --discovery-token-ca-cert-hash sha256:9ce421e4cf7104e63f422748917bc35419a43e947cc1ec7235043553b210050c
```

Set role worker for new node

```bash
kubectl label node vnsgn-ldsere2 node-role.kubernetes.io/worker=worker
```

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Or download above config to your mac.
Install kubectl on mac: `brew install kubectl` or [kubectl install](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
Set kubeconfig

```code
export KUBECONFIG=<absolute_config_path>
```

Verify

```code
kubectl cluster-info
```

[Kubectl docs](https://kubectl.docs.kubernetes.io/pages/kubectl_book/getting_started.html)

### Dashboard

Install Dashboard

```code
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta6/aio/deploy/recommended.yaml
```

```code
kubectl proxy
```

Goto: [Dashboard](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/)
