## POD-Probe

### Liveness Probe
```
- 컨테이너가 살았는지 판단하고 다시 시작하는 기능
- 컨테이너의 상태를 스스로 판단해 교착 상태에 빠진 컨테이너를 재시작
- 버그가 생겨도 높은 가용성을 보인다.
```

### Readiness Probe
```
- 포드가 준비된 상태에 있는지 확인하고 정상 서비스를 시작하는 기능
- 포드가 적절하게 준비되지 않은 경우 LB를 하지 않음
```

### Startup Probe
```
 - 애플리케이션의 시작 시기를 확인하여 가용성을 높이는 기능
 - Liveness와 Readiness의 기능을 비활성화 (살아 있다고, 준비되었다고 판단했을 때)
```

### Liveness Test
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
```
[pods/probe/exec-liveness.yaml]
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: k8s.gcr.io/busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
```
### readiness Test
```
[readiness Test]
$ kubectl apply -f https://k8s.io/examples/pods/probe/tcp-liveness-readiness.yaml
```
