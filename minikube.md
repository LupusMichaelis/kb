# Minikube

Install:
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [minikube](https://github.com/kubernetes/minikube#other-ways-to-install)

```sh
apt install libvirt-daemon virtinst
```

```sh
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | \
    apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" \
    > /etc/apt/sources.list.d/kubernetes.list
apt update
apt install -y kubectl

usermod -aG libvirt mickael
```
