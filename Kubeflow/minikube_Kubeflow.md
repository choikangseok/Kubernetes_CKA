### 1. 하이퍼바이저 설치
```
$ sudo yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer bridge-utils
$ sudo systemctl start libvirtd
$ sudo systemctl enable libvirtd
```

### 2. kubectl 설치 (CentOS)

```
$ cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF

$ sudo yum install -y kubectl
```

```
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.28.0/minikube-linux-amd64
$ chmod +x minikube
$ sudo mv minikube /usr/local/bin/

$ minikube start --cpus 4 --memory 8096 --disk-size=40g --kubernetes-version=v1.21.2 --driver=none

```

###### 중간 과정 minukube 실행시 오류 해결책
```
1. X Exiting due to DRV_AS_ROOT: The "docker" driver should not be used with root privileges.
해결책 : docker로 기동시에 root권한을 사용하게 되면 보안 문제가 발생할수 있으므로 root권한을 사용하지 말라고 권장하는 메세지다.
이런경우 내용에 나온대로 --driver=none 옵션을 줘서 실행하도록 한다.
해결책 : $ minikube start --cpus 4 --memory 8096 --disk-size=40g --driver=none



```
#### Kubeflow v1.3.0 설치
```
$ git clone -b <tag> <repository>
$ git clone -b v1.3.0 https://github.com/kubeflow/manifests.git

```
minikube start --cpus 4 --memory 8096 --disk-size=40g --kubernetes-version=v1.21.2 --driver=none
```
