### 레플리케이션컨트롤러

*레플리케이션* : 데이터 저장과 백업하는 방법과 관련 있는 데이터를 호스트 컴퓨터에서 다른 컴퓨터로 복사하는 것
```
 [레플리케이션 컨트롤러]
 - 포드가 항상 실행되도록 유지하는 쿠버네티스 리소스
 - 노드가 클러스터에서 사라지는 경우 해당 포드를 감지하고 대체 포드 생성
 - 실행 중인 포드 목록을 지속 모니터링
 - 실제 포드 수가 원하는 수와 항상 일치하는지 확인
```

#### 레플리케이션 컨트롤러 세 가지 요소
```
- 레플리케이션컨트롤러가 관리하는 포드 범위를 결정하는 레이블 셀렉터
- 실행해야 하는 포드의 수를 결정하는 복제본 수
- 새로운 포드 모양을 설명하는 포드 템플릿
```

#### 레플리케이션 컨트롤러의 장점
```
- 포드가 없는 경우 새 포드를 항상 실행
- 노드에 장애 발생  다른 노드에 복제본 생성
- 수동, 자동으로 수평 스케일링
```

#### 레플리케이션 컨트롤러 YAML 작성

```
apiVersion: v1
kind: ReplicationController
metadata:
  name: <rc-name>
spec:
  # 복제본 수
  replicas: 3
  # 라벨 셀렉터
  selector:
    app: <app>
  # 포드 템플릿
  template:
    metadata:
      labels:
        app: <app>
    spec:
      containers:
      - name: <naem>
        image: <image>
        ports:
          - containerPort: 8080
```
### 실행 중인 레플리케이션 컨트롤러와 포드 확인
```
$ kubectl get Pod
$ kubectl get rc

# 포드를 임의로 정지시켜 반응 확인
$ kubectl delete pod "pod" # 포드 정지
$ kubectl get pod # 포드 반응 확인
```

### 레플리케이션 컨트롤러의 관리 레이블 벗어나는 방법
```
$ kubectl describe rc "rc-name" # 레플리케이션 정보 확인
$ kubectl get pod -L app        # app 리스트를 확인한다.
$ kubectl label pod 'POD-NAME' app=<변경> --overwrite #레이블이 변경경해 관리 밖으로 벗어나게 한다.
$ kubectl get pod -L app        # 상태 확인

```

### 레플리케이션 컨트롤러 삭제 바꾸기
```
# 일반적인 삭제 명력어와 동일
$ kubectl delete rc "rc-name"

# 실행 시키고 있는 포드는 계속 실행을 유지하고 싶은 경우에 --cascade 활용
$ kubectl delete rc "rc-name" --cascade=false
$ kubectl get pod # pod 확인
```

### 예제
```
apiVersion: v1
kind: ReplicationController
metadata:
  name: http-go
spec:
  replicas: 3
  selector:
    app: http-go
  template:
    metadata:
      name: http-go
      labels:
        app: http-go
    spec:
      containers:
      - name: http-go
        image: ktos5427/http-go
        ports:
        - containerPort: 8080
```
- kubectl delete pod을 통해 자가 치료를 잘 하고 있는지 확인 할 것
- node 하나 통신을 꺼도 5분 기간 동안은 pod이 Running 상태로 나온다.
- kubectl get nodes 에서 disconenct 확인

### 레플리카 스케일 조정 방법
```
# 1. 레플리카 스케일 조정하는 방법
$ kubectl scale rc http-go --replicas=5

# 2. 적용 되어 있는 레플리카 config 수정 방법
$ kubectl edit rc http-go

# 3. yaml 파일에 apply 하는 방법
$ kubectl apply -f http-go-rc2.yaml
```
