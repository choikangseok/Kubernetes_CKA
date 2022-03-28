# Kubernetes_CKA
Kubernetes_CKA


# 쿠버네티스 구조
### Master Node : 핵심적인 중요한 부분들을 가지고 있다. 워커 노드를 관리 하는 역할을 하고 있다.
단일 마스터 노드에서 실행 or 여러 노드로 분할된다..  
**kube-apiserver :** 사용자 인증/통신 등 주요한 역할을 함  
**kube-scheduler :** 사실 일을 열심히 하는 애들(참모 역할), 어느 노드에 뭐를 배치할지  
**Controller-manager :** 사실 일을 열심히 하는 애들(참모 역할), 리소스를 어떻게 관리/제어  
data storage(etcd): Stroage 관련 추후
### Worker Node : 컨테이너화된 애플리케이션을 실행하는 시스템 
**kubelet** : kube-apiserver로부터 명령을 하달 받는 역할  
**kubernetes Service, kube-proxy** : 통신병 역할, 애플리케이션 간 네트워크 트래픽을 분산/ 연결  
**앱 디스크립터** : YAML로 작성  

# GKE를 활용한 쿠버네티스 사용
GKE 프로젝트 생성 - kubernetes engine API 구동  

**위치 유형**
 - **영역** : 하나의 데이터센터에만 배치하고 싶다.  
 - **리전** : 분산 배치 (더 비싸겠지?)
  
**GKE Standard** : 노드를 전부 구성 (노드를 직접 할당)  
**GKE Autopilot** : 필수 구성만으로 노드를 관리 (컨테이너만 보임)  

```
Kubectl get nodes
Kubectl create deploy nx –-image=nginx
Kubectl expose deploy nx –type=LoadBalancer –port --target-port=80
```
# 쿠버네티스 관리하는 명령어
**kubeadm** : 클러스터를 부트스트랩하는 명령  
**kubelet** : 클러스터의 모든 시스템에서 실행되는 구성 요소로, 창 및 컨테이너 시작과 같은 작업을 수행  
**kubectl** : 커맨드 라인 util은 당신의 클러스터와 대화

# Ubuntu 환경 구성 및 Kubeadm 설치
id : user01@user01  
passwd : test1234
### netplan  설정
VM IP 설정 확인 이후
```
$ sudo vim /etc/netplan/00-installer-config.yaml
 #편집  
$ sudo netplan apply
 #적용
$ ip addr
 #확인
```
### Docker install 및 설정
```
apt update && apt install docker.io -y
```

```
# kubeadm 설치
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

```
$ sudo swapoff -a #swap off 설정

$ sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab # 영구 설정 It will prevent the swap partition from automatically mounting after a reboot.
```

### kubelet과 docker의 id가 달라서 나오는 현상 해결

```
[/etc/docker/daemon.js]
{
  "exec-opts": ["native.cgroupdriver=systemd"]
}
```
```
$ sudo systemctl restart docker
$ docker info | grep -i group # cgroup 변경확인
```
### hostname 노드별로 변경
```
$ hostnamectl # 확인
$ hostnamectl set-hostname master0 # hostname <master0>변경
$ sudo vim /etc/hosts # <master0> 로 변경
```




