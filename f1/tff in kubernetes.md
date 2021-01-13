```


multipass launch --name master-k8s --cpus 4 --mem 4096M --disk 20G
multipass launch --name worker-1-k8s --cpus 4 --mem 4096M --disk 20G
multipass launch --name worker-2-k8s --cpus 4 --mem 4096M --disk 20G

curl -fsSL https://get.docker.com | bash -s docker
sudo usermod -aG docker $USER


curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - && \
  echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list && \
  sudo apt-get update -q && \
  sudo apt-get install -qy kubeadm

sudo swapoff -a

sudo apt update
sudo apt install python3-dev python3-pip  # Python 3
sudo pip3 install --user --upgrade virtualenv
```

```
apt-get install python3-venv
python3 -m venv my_env
source my_env/bin/activate


kubeadm join 10.149.63.248:6443 --token prsn5f.x56t68eyku4wft07 \
    --discovery-token-ca-cert-hash sha256:db849ff2da662b92ffb46295971f0f934abc84a9501ecad91dee907f93c2edc8 


export KUBECONFIG=/etc/kubernetes/admin.conf
alias python=python3
alias pip=pip3

pip install --upgrade pip
pip install --upgrade tensorflow_federated

```
