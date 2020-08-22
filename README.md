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
 
 
## monitor
集成mysql和redis监控服务，可以支持单独部署的mysql服务和redis服务
```shell script
helm install -n monitor \
monitor \
-f examples/values-monitor-arm64v8.yaml
```


### mysqld-monitor
可以支持监控单独部署的mysql服务

 ```shell script
helm install -n mysqld-monitor \
monitor/charts/mysqld-monitor \
--set env.data_source_name=root:abc123@(common-utilities-mysql:3306)/
```

### mysqld-monitor
可以支持监控单独部署的redis服务

 ```shell script
helm install -n redis-monitor \
monitor/charts/redis-monitor \
--set env.redis_addr=common-utilities-redis:6379
```
