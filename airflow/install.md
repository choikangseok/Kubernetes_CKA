### Airflow 경로 및 환경 변수 설정

```
export AIRFLOW_HOME=/home/Airflow
AIRFLOW_VERSION=2.2.3
PYTHON_VERSION=
```
### 사전에 install 해야할 것
```
sudo apt install python3-testresources
python3
```

```
alias python=python3.8
alias pip=pip3
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
```
### 실행 전 셋팅

```
#DB 초기화
#DB Airflow의 DAG와 Task 등을 관리하기 때문에 셋팅이 필요하다.
airflow db init
```
### 셋팅이후 다음과 같은 결과를 확인할 수 있음.
```
root@master0:/home/user01/airflow# tree -L 2
.
├── airflow.cfg # airflow의 환경설정 파일
├── airflow.db # DB 관련된 정보를 담고 있다.
├── logs # airflow 각종 로그를 관리
│   └── scheduler
└── webserver_config.py
```

### airflow를 관리할 계정 생성
```
airflow users create \
    --username admin \
    --firstname soojin \
    --lastname lee \
    --role Admin \
    --email -----@----.---
```
### Example들이 보이지 않도록 설정
```
airflow.cfg 파일에서 load_example를 False로 설정
```
