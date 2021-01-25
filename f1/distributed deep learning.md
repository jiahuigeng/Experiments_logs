PS:
模型参数全部存储在ps节点， worker在每个step计算完梯度后向ps节点更新模型梯度， 训练中需要一个worker节点评估效果或者保存checkout, 把这样的worker节点称chief节点
多个worker 同时跟ps通信的话，ps本身成为瓶颈，worker数量增加通信量也会线性增加

AllReduce 节点， 只需要worker节点 不需要ps节点 充当两种角色诶，
ring 2**(n-1)轮同步，完成所有更新allre

GRPC NCCL

jupyter notebook 分布式 多个用户同时使用
kubeflow:
tf-operator
pytorch-operator
tf-servering


operator 开发者不需要修改 kubernetes本身的功能就能实现扩展集群的能力， 伸缩性： 按需进行部署，设置pod数量， 还原获取状态的备份

使用dep 进行包管理， 
gopkg.lock 
根据依赖的状态自动生成的， 不需要手动修改它
gopkg.toml: 描述开发者意图， 包括依赖与branch version

helm 和 tiller 管理集群上的软件包 通过helm 打包应用，管理依赖的关系 发布到集群中

要把crd结构与kubernetes 角色一一对应
安装了自定义资源 kubectl get crd

以后 kube build operator-sdk 实现operator

代码自动生成

types.go: 定义了crd 文件具体内容
crdgroup crdkind 
在crd spec 结构里定义： docker image, replica 进程终止策略

register.go ： addKnownTypes
client 知道 crd 类型api对象

alidation.go

hack/ 
代码自动生成：
k8s.io/code-generator

定义 监听哪些资源变动

ps 内存微调 
allreduce 每一个worker 存储 完整模型
添加worker 很容易 worker 复原很容易，更新效率高，完成全部通信
MPI标准 

volcano 
总体资源 资源 死锁
k8s 资源调度器