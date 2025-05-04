# windows上一定要先启动docker desktop ，再启动运行minikube start


# 检查服务状态：kubectl get pods -o wide -w


# 先输入 kubectl cluster-info，出现一个URL表示成功访问集群


"Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.58.55:8443/api?timeout=32s\": dial tcp 192.168.58.55:8443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond."

如果出现一个报错，说明无法连接，则需要**检查minikube**是否启动集群


# 运行minikube start 如果集群启动，再尝试输入kubectl cluster-info，看是否出现一个URL表示成功访问集群

如果启动不了，则要输入**minikube stop**先关闭，再启动


# 输入minikube stop 



# 如果出现kubectl get pods 访问pods信息发现imagepullbackoff

可以采用：

**kubectl delete pod -l app=hello-node**
**kubectl get pods**


如果不行，本质问题是

#  Minikube VM 内部无法访问 Docker Hub（registry-1.docker.io）



## 本地拉取宿主镜像  docker pull

## 导入镜像到minikube  minikube image loadminikube image load
如果出现minikube访问default的上下文错误，则需要重新配置上下文和相关环境变量

**手动设置minikube的docker环境变量**： minikube docker-env | Invoke-Expression
验证：docker ps 
**手动设置minikube的docker上下文**：minikube docker-env
docker context create minikube --docker "host=tcp://192.168.49.2:2376,ca=C:\Users\ASUS\.minikube\certs\ca.pem,cert=C:\Users\ASUS\.minikube\certs\cert.pem,key=C:\Users\ASUS\.minikube\certs\key.pem"

docker context use minikube
验证下：docker context ls
##  在deployment.yaml设置imagePullPolicy: IfNotPresent



## 重新配置kubectl delete deployment 
##  kubectl apply -f deployment.yaml



# 当使用minikube出现 W0417 10:28:47.174463   38224 main.go:291 Unable to resolve the current Docker CLI context "default": context "default": context not found: open C:\Users\ASUS\.docker\contexts\meta\37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f\meta.json: The system cannot find the path specified. 但是我们docker的context文件夹下的哈希文件夹名字不是它说的这个，这个时候需要手动删除minikube的环境





## 如果还不行，我们需要重新配置docker context 上下文



最无脑的办法，将其哈希名改成默认所找的那个名字


# 要通过minikube命令获取service信息时，出现docker驱动问题，则需要

## 建立隧道 minikube tunnel ，（管理员模式下运行，且不要关闭）


## 注意worker节点不应该为load balancer服务只有负载均衡器才是这个服务，一般worker服务作clusterip作为集群内部服务

同时，还有个无脑的办法，使用**端口映射转换**kubectl port-forward svc/worker 5000:5000


**获取任意Worker Pod名称**
**$worker_pod = (kubectl get pods -l app=worker -o jsonpath='{.items[0].metadata.name}')**

**端口转发**
**kubectl port-forward $worker_pod 5000:5000**

**新终端测试**
**curl http://localhost:5000/health**



# k8s分为几级：
## Load Balancer NodePort Ingress （只有该级才能从外部网络访问）
## Cluster IP   Port
## PodIP  Port
## NodeIP Port

# k8s的LoadBalancer类型会自动与外部云服务提供商获取外部IP，我们作为学习环境而非生产环境一般提供不了

## 此外，在基于访问k8s集群配置的负载均衡器中，必须为其配备rbac认证，否则将无法访问集群配置，也就无法进行worker节点的映射

# 因此，在学习环境上，我们一般采用端口转发的方式进行暴露和测试


PersistentVolumeClaim（PVC）一旦**绑定（Bound）到某个 PersistentVolume（PV）后，除了 resources.requests 和 volumeAttributesClassName，其他字段（比如 volumeName、accessModes、storageClassName 等）都不能更改。
你的 model-pvc 已经绑定到了一个之前创建的 PV（比如名字是 pvc-xxx），而你现在试图修改它的 volumeName 为 model-pv，这是不允许的，所以报了 Forbidden: spec is immutable。

# 因此有可能会因为pv和pVc没有删除干净导致容器无法正常准备好