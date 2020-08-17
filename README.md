# pi4charts

## common-utilties
集成myql和redis-ha

 
 ```shell script
helm install -n comon-utilities \
common-utilities \
-f examples/values-common-utilities-arm64v8.yaml
```


### mysql
基于 stable/mysql-1.6.6 调整 
 - deployment调整为statefulset
 - persistentVolumeClaim调整为volumeClaimTemplates，删除pvc.yaml
 - 去掉testframework
 
 ```shell script
helm install -n mysql \
common-utilities/charts/mysql \
-f examples/values-mysql-arm64v8.yaml
```



### redis-ha
基于 stable/redis-ha-4.4.4 调整 
 - 删除haproxy
 - 支持redis的service设置为NodePort
 
 ```shell script
helm install -n redis-ha \
common-utilities/charts/redis-ha \
-f examples/values-redis-ha-arm64v8.yaml
```
 
 
