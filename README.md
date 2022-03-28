# Kubernetes_CKA
Kubernetes_CKA


# 쿠버네티스 구조
Master Node : 핵심적인 중요한 부분들을 가지고 있다. 워커 노드를 관리 하는 역할을 하고 있
ㅇ 단일 마스터 노드에서 실행 or 여러 노드로 분할된다..
ㅇ kube-apiserver 사용자 인증/통신 등 주요한 역할을 함
ㅇ kube-scheduler : 사실 일을 열심히 하는 애들(참모), 어느 노드에 뭐를 배치할지
ㅇ Controller-manager : 사실 일을 열심히 하는 애들(참모), 리소스를 어떻게 관리/제어
ㅇ data storage(etcd): 
Worker Node : 컨테이너화된 애플리케이션을 실행하는 시스템 
ㅇ kubelet은 kube-apiserver로부터 명령을 하달 받는 역할
ㅇ kubernetes Servce, kube-proxy : 통신병 역할, 애플리케이션 간 네트워크 트래픽을 분산/ 연결
앱 디스크립터 : YAML로 작성

# GKE를 활용한 쿠버네티스 사용
GKE 프로젝트 생성 - kubernetes engine API 구동
위치 유형
-	영역 : 하나의 데이터센터에만 배치하고 싶다.
-	리전 : 분산 배치 (더 비싸겠지?)
GKE Standard : 노드를 전부 구성 (노드를 직접 할당)
GKE Autopilot : 필수 구성만으로 노드를 관리 (컨테이너만 보임)

```
Kubectl get nodes
Kubectl create deploy nx –-image=nginx
Kubectl expose deploy nx –type=LoadBalancer –port --target-port=80
```


