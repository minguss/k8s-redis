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

uninstall:
```shell
helm delete --purge redis-pv
kubectl delete -f configmap.yaml
kubectl delete -f service.yaml
kubectl delete -f statefulset.yaml
kubectl delete pvc -l app=redis -n redis
```
