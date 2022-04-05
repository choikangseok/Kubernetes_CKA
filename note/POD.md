## POD
```
- 컨테이너의 공동 배포된 그룹, 쿠버네티스의 기본 빌딩 블록을 대표
- 쿠버네티스는 컨테이너를 개별적으로 배포하지 않는다. 컨테이너의 포드를 항상 배포하고 운영
- 일반적으로 포드는 단일 컨테이너만 포함, 다수의 컨테이너도 포함할 수 있음
- 포드는 다수의 노드에 생성되지 않고 단일 노드에서만 실행
- 여러 프로세스를 실행하기 위해서는 컨테이너당 단일 프로세스가 적합
- 다수의 프로세스 제어-> 다수의 컨테이너를 다룰 수 있는 그룹이 필요
```
### POD의 장점
```
밀접하게 연관된 프로세스를 함께 실행, 마치 하나의 환경에서 동작하는 것처럼 보인다.
동일한 환경을 제공하면서 다소 격리된 상태로 유지
```

### POD Network
```
POD이 할당받은 네트워크 대역대가 있다.
k8s 클러스터의 모든 포드는 공유된 단일 플랫, 네트워크 주소 공간에 위치
POD 사이에는 NAT 게이트웨이가 없다.
```

### 컨테이너를 포드 전체에 적절하게 구성하는 방법
```
두가지 컨테이너가 밀접한 관계가 있을 때만 제외하고 하나의 컨테이너를 구성하는 방향으로 포드/컨테이너를 구성한다.
```

### YAML에서 POD 정의
```
apiVersion, kind, metadata, spec, status
주로 apiVersion, kind, metadata, spec 4가지를 구성한다고 보면 된다.
apiVersion : 쿠버네티스 api 버전을 카리킴
kind: 어떤 리소스 유형인지 결정 
metadata : 포드와 관련된 이름, 네임스페이스, 라벨, 그 밖의 정보
spec : 컨테이너, 볼륨 등의 정보
status : 포드의 상태, 각 테이너의 설명 및  상태, 포드 내부의 IP 및 그 밖의 기본 정보 등
```

### Descriptor
```
[template]
apiVersion: batch/v1
kind: Job
metadata:
  name: hello
spec:
  template:
    # This is the pod template
    spec:
      containers:
      - name: hello
        image: busybox:1.28
        command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
      restartPolicy: OnFailure
    # The pod template ends here
```
### POD 관련 명령어 예시
```
$kubectl get pod http-go -o yaml # yaml 정보 출력
$kubectl describe pod http-go #정보 출력
$kubectl port-forward http-go 8080:8080 #포워딩
$kubectl create -f go-http-pod.yaml #생성
$kubectl delete -f go-http-pod.yaml #삭제
$kubectl logs http-go #로그
$kubectl annotate pod http-go test1234=test1234  # 주석을 넣는 공간, 필요한 정보들, 팀들과 공유해야하는 내용들을 넣는다.
$kubectl delete pod http-go # pod 삭제
$kubectl delete pod --all # 모든 pod 삭제
```
