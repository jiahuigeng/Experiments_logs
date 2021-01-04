# Ubuntu 安装 kubernetes Helm

1.  docker docker-compose
2.  shell 
   ```
   sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
   apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 6A030B21BA07F4FB
   apt-get install kubeadm kubelet kubectl
   apt-mark hold kubeadm kubelet kubectl
   kubeadm version

kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=192.168.58.2

   ```

   3. 显示
```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.58.2:6443 --token khj2rx.9jf7c9eudn91h2ji \
    --discovery-token-ca-cert-hash sha256:1ab72cbee7952c5d8cf99c2c012513623bec29801606eed0c4c38160dd3cd581 
   ```


4.
```
kubectl apply -f https://docs.projectcalico.org/v3.11/manifests/calico.yaml
```
 
 If comes
 ```
 The connection to the server localhost:8080 was refused - did you specify the right host or port?
 ```
 then 
 ```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
 ```

 also for slaves 
 ```
 scp -r /etc/kubernetes/admin.conf ${node1}:/etc/kubernetes/admin.conf
 echo "export KUBECONFIG=/etc/kubernetes/admin.conf" >> ~/.bash_profile
source ~/.bash_profile

 ```

 5. 
   ```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
 ./get_helm.sh
   ```

6
```
helm install fedlearner-stack ./deploy/charts/fedlearner-stack

kubectl create ns leader
helm install fedlearner ./deploy/charts/fedlearner --namespace leader
kubectl create ns follower
helm install fedlearner ./deploy/charts/fedlearner --namespace follower
kubectl apply -f ./deploy/charts/manifests/

```

