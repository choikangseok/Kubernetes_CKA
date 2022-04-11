docker ps

### Docker Container init id , mount id, parent id 위치

```
[init-id  mount-id  parent]
<mount-id> Path : /var/lib/docker/image/overlay2/layerdb/mounts/<container_hash>/mount-id
<init-id> Path : /var/lib/docker/image/overlay2/layerdb/mounts/<container_hash>/init-id
<parent> Path : /var/lib/docker/image/overlay2/layerdb/mounts/<container_hash>/parent-id
```

### 컨테이너 볼륨 실제 위치
```
/var/lib/docker/overlay2/<mount-id>/diff/
```
