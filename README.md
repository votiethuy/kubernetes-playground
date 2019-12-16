# K8s-playground

Kubernetes Playground

## Install

Using kubeadm. [Official docs](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
Network Canal

```code
kubeadm init --pod-network-cidr=10.244.0.0/16
```

Save the token to join node

```bash
kubeadm join 10.163.60.19:6443 --token rlmf13.luf5r7mvpt1nixy0 --discovery-token-ca-cert-hash sha256:c57f1ba06849ddf3d2dd3c37b5c20d3bc7cd59acf0eb424f94f38c5d8d4fbe93
```

Install CNI

```bash
kubectl apply -f https://docs.projectcalico.org/v3.8/manifests/canal.yaml
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
