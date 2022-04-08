# 레이블과 셀렉터


### 레이블
리소스에 바코드를 붙여서 검색 기능을 사용할 수 있게 할 수 있다.
```
- 모든 리소스를 구성하는 매우 간단하면서도 간단한 쿠버네티스 기능
- 리소스에 첨부하는 임의의 키/값 쌍
- 레이블 셀렉터를 사용하면 각종 리소스를 필터링하여 선택 가능
- 리소스는 한 개 이상의 레이블을 가질 수 있다.
- 리소스를 만드는 시점에 레이블을 첨부
- 기존 리소스에도 레이블의 값을 수정 및 추가 가능
- 모든 사람이 쉽게 이해할 수 있는 체계적인 시스템을 구축 가능
- app: 애플리케이션의 구성요소, 마이크로 서비스 유형 지정
- rel: 애플리케이션의 버전 지정 (릴리즈 레이블)
```

### 포드 생성 시 레이블을 지정하는 방법
```
yaml 파일에 설정을 할 수 있다.

#새로운 레이블을 추가할 때 label 명령어를 사용
kubectl label pod http-go-v2 test=foo

#기존의 레이블을 수정할 때는 --overwrite 옵션을 주어서 실행
kubectl label pod http-go-v2 rel=beta #오류
kubectl label pod http-go-v2 rel=beta --overwrite #기#레이 레이블 수정

#레이블 삭제
kubectl label pod http-go-v2 rel- #마이너스 옵션을 주면 된다.
```

### 레이블 확인하기
```
kubectl get pod --show-labels
```
### 특정 레이블 컬럼으로 확인
```
kubectl get pod -L app,rel #대문자 L을 통해 확인
```
### 레이블로 필터링하여 검색
```
kubectl get pod --show-labels -l 'env'                # env가 있는 것만 검색
kubectl get pod --show-labels -l '!env'               # env가 없는 것만 검색
kubectl get pod --show-labels -l 'env!=test'          # env가 test가 아닌 것만 검색
kubectl get pod --show-labels -l 'env!=test,rel=beta' # 등
```

### 레이블 배치 전략도 있으니 확인할 것


### 셀렉터
