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