### GCP에서 젠킨스 구성
```       
[Ubuntu 20.04 lts]
$ sudo -i
$ apt update && apt install -y docker.io
$ docker run -d -p 8080:8080 --name jenkins -v /home/jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -u root jenkins/jenkins:lts

# 젠킨스 내부에 도커 설치
# 도커를 설치한다해도 내부적으로 서비스가 돌아가지는 않는다.
$ docker exec jenkins apt update
$ docker exec jenkins apt install -y docker.io

# 인증 비밀번호를 출력
$ docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

```
[GCP - cloud shell에서 포트 오픈]
gcloud compute firewall-rules create jenkins-ci --allow=tcp:8080
```

### 젠킨스 Git-webhook
```
[Docker Pipeline 등록]
[github]
 1. github 레파지토리를 구성
 2. setting - webhook 등록
 3. http://<jenkinsip>/github-webhook/

[젠킨스]
 4. 젠킨스 접속 - new item - pipeline 생성
 5. github project 선택 후 url 입력
 6. pipeline에서 Pipeline script frome SCM(git에 있는 jenkins 파일 이용)
 7. 토큰 등록 () # 토큰 등록시 ID 꼭 확인 # Manage Credentials 에서 설정

[github]
 8. git jenkins 파일 변경시 hook 수행 확인
```
