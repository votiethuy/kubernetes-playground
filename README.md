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
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/2140ac876ef134e0ed5af15c65e414cf26827915/Documentation/kube-flannel.yml
```

Join node command

```bash
kubeadm join 10.163.60.19:6443 --token 8yy96k.ka0ro6d28g2m59m6 --discovery-token-ca-cert-hash sha256:a49730d0654a259170f220e109593f1f4a79bab8d195ffc46f6b48ddce194a93
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

Use [Octant](https://github.com/vmware-tanzu/octant)

```code
brew install octant
```

```code
octant
```

Goto: [Dashboard](127.0.0.1:7777)

### Kubectl cheatsheet

Delete all pods != Running

```code
kubectl get pods --field-selector=status.phase!=Running -n <namespace> -o json | kubectl delete -f -
```
