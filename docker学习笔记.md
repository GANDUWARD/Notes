# 如果出现镜像无法下载，可以尝试关闭docker ipv6功能


在docker desktop setting 里的docker engine 添加 "ipv6:false"



# 如果还不行可以考虑切换docker的国内镜像源 (一般不建议)


# 如果还不行可以尝试先对基础镜像进行docker pull 拉取  （建议）

# 关于pytorch在docker容器上的使用，有可能因为报错找不到对应的GPU而无法运行，这个时候需要强制选择CPU设备