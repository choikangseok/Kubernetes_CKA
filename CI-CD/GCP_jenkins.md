### GCP에서 젠킨스 설치
```       
[Ubuntu 20.04 lts]
$ sudo -i
$ apt update && apt install -y docker.io
$ docker run -d -p 8080:8080 --name jenkins -v /home/jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -u root jenkins/jenkins:lts

# 도커 젠킨스 안쪽
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

```
Docker Pipeline 체크
```
