# 如果出现镜像无法下载，可以尝试关闭docker ipv6功能


在docker desktop setting 里的docker engine 添加 "ipv6:false"



# 如果还不行可以考虑切换docker的国内镜像源 (一般不建议)


# 如果还不行可以尝试先对基础镜像进行docker pull 拉取  （建议）

# 关于pytorch在docker容器上的使用，有可能因为报错找不到对应的GPU而无法运行，这个时候需要强制选择CPU设备


# 对于镜像要进行更新，先将原来镜像去除 docker rmi neural-worker:v1 -f
# 重构新镜像docker build -t neural-worker:v1 .
# 对于k8s，要进行minikube预加载： minikube image load neural-worker:v1


# 执行docker build 时，若dockerfile里面有包含 COPY file，但不是包含路径，则默认在命令执行的路径下，因此最好跳转到dockerfile的当前目录执行docker build


# docker VOLUME 创建一个docker卷，这个卷不随着所使用镜像容器的消亡而丢失数据。类似公共存储区