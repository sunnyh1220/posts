# Kubernetes安装


<!--more-->

## Kubeadm 安装

### 1. docker install

```bash
sudo apt-get install  apt-transport-https  ca-certificates curl  software-properties-common

curl -fsSL  https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add

sudo add-apt-repository "deb [arch=amd64]  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" 

apt-cache madison docker-ce

apt-cache madison docker-ce-cli

sudo apt-get install docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker

开机自启:
systemctl enable docker && systemctl start docker
# systemctl enable kubelet && systemctl start kubelet


```



### 2. k8s install by kubeadm

#### 2.1 k8s download

```shell
sudo swapoff -a

sudo apt-get update && sudo apt-get install -y apt-transport-https

curl https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | apt-key add - 
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main
EOF

sudo apt-get update

sudo apt-get install -y kubelet kubeadm kubectl

# export KUBECONFIG=/etc/kubernetes/admin.conf

sudo systemctl daemon-reload
sudo systemctl restart kubelet
```



卸载之前的版本

```shell
sudo apt-get remove -y kubelet kubeadm kubectl
sudo apt autoremove

# 
rm -rf ~/.kube
```



安装指定版本

```shell
# 比如 1.13.12
sudo apt-get install -y kubelet=1.13.12-00 kubeadm=1.13.12-00 kubectl=1.13.12-00
```



#### 2.2 master init

```shell
# -------- master --------


*** init-config.yaml ***
apiVersion: kubeadm.k8s.io/v1beta1
kind: ClusterConfiguration
imageRepository: registry.aliyuncs.com/google_containers
kubernetesVersion: v1.16.1
controlPlaneEndpoint: "192.168.1.37:6443"
networking:
  serviceSubnet: "192.168.0.0/16"
  podSubnet: "192.168.0.0/16"
***

kubeadm config images pull --config=init-config.yaml

kubeadm init --config=init-config.yaml

# 不使用配置文件init
kubeadm init \
--apiserver-advertise-address=192.168.1.37 \
--image-repository registry.aliyuncs.com/google_containers \
--kubernetes-version v1.17.4 \
--service-cidr=10.1.0.0/16 \
--pod-network-cidr=10.244.0.0/16


# kubeadm join 49.233.168.186:6443 --token cpnxfg.2as9a59xch4pt4a7 \
#    --discovery-token-ca-cert-hash sha256:33c8a4bcf84de94ae46ba33fb603e7366a58d6c4e8b6a71287f3f4040eaab33d


mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```



#### 2.3 node init

```shell
-------- node --------
sudo apt-get install -y kubelet kubeadm --disableexcludes=kubernetes


*** join-config.yaml ***
apiVersion: kubeadm.k8s.io/v1beta1
kind: JoinConfiguration
discovery:
  bootstrapToken:
	apiServerEndpoint: 49.233.168.186:6443
	token: 4fbe4n.lkqwktq81wdi42ga
	unsafeSkipCAVerification: true
  tlsBootstrapToken: 4fbe4n.lkqwktq81wdi42ga
***

kubeadm join --config=join-config.yaml 
  
```



#### 2.4 cni网络插件

 CNI网络插件选择参考:https://kubernetes.io/docs/setup/independent/createcluster-kubeadm/#pod-network

Subnet选择`192.168.0.0/16`,使用calico

```shell
kubectl apply -f https://docs.projectcalico.org/v3.8/manifests/calico.yaml
```

Subnet选择`10.244.0.0/16`,使用flannel

```shell
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```



#### 2.5 gpu 插件

```shell
kubectl create -f https://raw.githubusercontent.com/NVIDIA/k8s-device-plugin/1.0.0-beta/nvidia-device-plugin.yml
```



#### 2.6 单机

```bash
# 单机All-In-One Kubernetes环境
kubectl taint nodes --all node-role.kubernetes.io/master-
```



#### 2.7 常用cli

```bash
# pod状态
kubectl get pods --all-namespaces
kubectl get pods --all-namespaces -o wide
kubectl --namespace=kube-system describe pod <pod_name>

```



##### 设置master节点参与/不参与Pod负载

- master节点参与pod负载

  ```
  kubectl taint nodes --all node-role.kubernetes.io/master-
  ```

  

- master节点恢复不参与POD负载

  ```
  kubectl taint nodes <node-name> node-role.kubernetes.io/master=:NoSchedule
  ```

  

- master节点恢复不参与POD负载，并将Node上已经存在的Pod驱逐出去

  ```
  kubectl taint nodes <node-name> node-role.kubernetes.io/master=:NoExecute
  ```



##### node节点token失效

```bash
kubeadm token list
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'

# 替换上面生成的相应字段
kubeadm join 10.167.11.153:6443 --token o4avtg.65ji6b778nyacw68 --discovery-token-ca-cert-hash sha256:2cc3029123db737f234186636330e87b5510c173c669f513a9c0e0da395515b0

```


