config:

- edit namespace in all yaml files
- edit configmap

install:
```shell
kubectl apply -f configmap.yaml
kubectl apply -f service.yaml
kubectl apply -f statefulset.yaml
kubectl exec -it redis-cluster-0 -n redis -- redis-cli -a xxxx{password} --cluster create --cluster-replicas 1 $(kubectl get pods -l app=redis -n redis -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')
```
![이미지 14](https://user-images.githubusercontent.com/22410442/57113470-b5360000-6d7f-11e9-8f29-57c332daecc0.png)
![이미지 15](https://user-images.githubusercontent.com/22410442/57113476-b8c98700-6d7f-11e9-989b-e0fac1000909.png)

```shell
kubectl exec -it redis-cluster-0 -n redis
redis-cli -a xxxxx
info
```
![이미지 16](https://user-images.githubusercontent.com/22410442/57113485-bbc47780-6d7f-11e9-84bf-e65ca6d934e9.png)

uninstall:
```shell
helm delete --purge redis-pv
kubectl delete -f configmap.yaml
kubectl delete -f service.yaml
kubectl delete -f statefulset.yaml
kubectl delete pvc -l app=redis -n redis
```
