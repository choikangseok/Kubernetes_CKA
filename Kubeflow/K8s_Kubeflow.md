## Kubeflow

Kubeflow v1.4.0 버전을 설치하기 위해


```
$ git clone -b v1.4.0 https://github.com/kubeflow/manifests.git
$ cd manifests
```

### Kustomize 설치
```
$ wget https://github.com/kubernetes-sigs/kustomize/releases/download/v3.2.0/kustomize_3.2.0_linux_amd64
$ chmod +x kustomize_3.2.0_linux_amd64
$ mv kustomize_3.2.0_linux_amd64 /usr/local/bin/kustomize
$ export PATH=$PATH:/usr/local/bin/kustomize

```
### Kustomize를 통한 Cert-manager 설치
```
$ kustomize build common/cert-manager/cert-manager/base | kubectl apply -f -
```
### cert-manager namespace에서 3개의 pod Running 확인
```
$ kubectl get pod -n cert-manager
```
