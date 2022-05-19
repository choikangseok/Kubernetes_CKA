# Argo
### **Argo란?**

 - Kubernetes용 오픈 소스 도구
 - WorkFlow를 실행하고 클러스터를 관리하며 GitOps를 올바르게 수행
 - Kubernetes의 컨테이너 네이티브 워크플로우 엔진으로써 동작
 - Kubernetes에서 복잡한 워크플로 및 응용 프로그램의 실행을 쉽게 지정하고 예약/조정

### argo의 WorkFlow
  - 기존 CI/CD 파이프라인 역할
  - 순차적 / 병렬 단계와 종속성을 모두 갖춘 복잡한 작업 단순화
  - 복잡하고 분산된 응용 프로그램의 배포 오케스트레이션
  - 시간/이벤트 기반으로 워크플로를 실행하는 정책

### Argo 설치
 ```
 kubectl create namepaces argocd
 kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
 ```
#### Argo 설치 확인 및 External IP 설정
 ```
 kubectl get svc,pod -n argocd

 ```

 ### External IP 설정
 ```
 # externalIPs에 외부 노출 시킬 아이피 입력
 kubectl patch service/argocd-server -p '{"spec":{"externalIPs":["192.168.163.154"]}}' -n argocd
 ```

 #### Argo Create Application
 **sync 방식**
 - **자동(automatic)** : Git에 설정된 매니페스트 내용과 현재 애플리케이션의 상태가 다르거나 정상동작하지 않으면 자동으로 동기화해 애플리케이션을 다시 배포 및 재구성
 - **수동 (manual)** : 설정한 방식으로 sync 구성

```
$ root@master0:~# kubectl get node,pod,svc -n argocd
NAME           STATUS     ROLES                  AGE   VERSION
node/master0   Ready      control-plane,master   21d   v1.23.5
node/node0     NotReady   <none>                 21d   v1.23.5
node/node1     Ready      <none>                 21d   v1.23.5

NAME                                                    READY   STATUS        RESTARTS        AGE
pod/argocd-application-controller-0                     1/1     Terminating   2 (2d19h ago)   3d8h
pod/argocd-applicationset-controller-79f97597cb-7hp4c   1/1     Running       0               19m
pod/argocd-applicationset-controller-79f97597cb-mvzbf   1/1     Terminating   0               3d8h
pod/argocd-dex-server-6fd8b59f5b-7wd6l                  1/1     Terminating   0               3d8h
pod/argocd-dex-server-6fd8b59f5b-k8s5r                  1/1     Running       0               19m
pod/argocd-notifications-controller-5549f47758-q8bn5    1/1     Running       0               19m
pod/argocd-redis-79bdbdf78f-8z7kj                       1/1     Running       0               19m
pod/argocd-repo-server-5569c7b657-mrv8g                 1/1     Terminating   1 (2d19h ago)   3d8h
pod/argocd-repo-server-5569c7b657-xf9cg                 1/1     Running       0               19m
pod/argocd-server-664b7c6878-hl6cv                      1/1     Running       0               19m

NAME                                              TYPE           CLUSTER-IP       EXTERNAL-IP       PORT(S)                      AGE
service/argocd-applicationset-controller          ClusterIP      10.96.136.203    <none>            7000/TCP                     3d8h
service/argocd-dex-server                         ClusterIP      10.96.0.118      <none>            5556/TCP,5557/TCP,5558/TCP   3d8h
service/argocd-metrics                            ClusterIP      10.99.58.223     <none>            8082/TCP                     3d8h
service/argocd-notifications-controller-metrics   ClusterIP      10.102.211.174   <none>            9001/TCP                     3d8h
service/argocd-redis                              ClusterIP      10.102.40.247    <none>            6379/TCP                     3d8h
service/argocd-repo-server                        ClusterIP      10.109.226.59    <none>            8081/TCP,8084/TCP            3d8h
service/argocd-server                             LoadBalancer   10.109.53.237    192.168.163.154   80:30746/TCP,443:32260/TCP   3d8h
service/argocd-server-metrics                     ClusterIP      10.105.6.226     <none>            8083/TCP                     3d8h
 ```
![image](https://user-images.githubusercontent.com/12148906/166703089-ecaeb561-dacd-4f9e-b5d0-fafd84b99338.png)

 ```
[manifests 파일 구성]
project: default
source:
 repoURL: 'https://github.com/choikangseok/flask-example-apps'
 path: flask-example-deploy
 targetRevision: HEAD
destination:
 server: 'https://kubernetes.default.svc'
 namespace: flask0
syncPolicy:
 syncOptions:
   - CreateNamespace=true
 ```
![image](https://user-images.githubusercontent.com/12148906/166703199-e7f20129-7598-4848-b771-125cb16914b7.png)

![image](https://user-images.githubusercontent.com/12148906/166703258-7d620c32-6541-45ec-afc6-78cf830ba829.png)

