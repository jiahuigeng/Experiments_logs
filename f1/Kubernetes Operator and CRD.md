operator 是一套机制 operator = CRD+webhook+controller

controller 监控集群状态变化， 分为 replicaset controller 和 endpoint controller

webhook 一般可以定义两类 webhook: mutating webhook （变更传入对象） alidating webhook （传入对象校验）

cluster-info

kubebuilder



==========================

工作流程
用户创建sidecarset
webhook 负责 sidecars 缺省值配置 和 配置项校验
用户创建pod

webhook 负责向pod 注入sidecar 容器

controller 实时检测 pod信息 并更新到sidecarset 状态

kubebuilder init --domain=kruise.io

kubebuilder create api --group apps --version v1alpha1 --kind SidecarSet --namespaced=false
创建api（CRD） 还会创建 controller 框架

group+domain 就是crd的 group： apps.kruise.io
namespaces 此crd是全局唯一的还是namespaced 唯一u

生成结果中： pkg/apis/v1/sodecarset_types.go 
pkg/controllers/sidercarset/sidecarset_controller.go
需要填充



code-generator 依赖注释生成代码， 有时需要调整注释
+genclient:nonNamespaced: 生成非namespace 对象
+kubebuilder:subresource:status: 生成status子资源
+kubebuilder:printcolumn:name:"MATCHED", type="integer",JSONPath=".status.matchedPods",description="xxx": kubectl get sidecarset 

需要填充字段：
SidecarSetSpec: 填充CRD 描述信息
SidecarSetStatus: 填充CRD状态信息

填充完make 重新生成代码即可


填充CRD 结果
selector: 选择哪一些pod需要注入
containers 定义
type SidecarSetSpec struct{
    Selector "metav1.LabelSelector"
    Contrainers []SidecarContainer
}

type SidecarSetStatus struct{
    MatchedPods int32 // set 匹配了多少
    UpdatedPods int32// 注入了多少
    ReadyPods int32// 多少可以直接工作了
}

填充完CRD 代码之后： 生成webhook 框架
1。 生成mutating webhook， 运行
```
kubebuilder aplha webhook --group apps --version v1alpha --kind SidecarSet --type=mutating --operations=create
kubebuilder alpha webhook --group core --version v1 --kind Pod --type =mutating --operations=create
```

2。 生成 validatingwehook, 运行

```
kubebuilder alpha webhook --group apps --version v1alpha1 --kind SidecarSet --type=validating --operations=create.update
```

填充 webhook
pkg/webhook/default_server/sidecarset/mutating/XXX_handler.go
pkg/webhook/default_server/sidecarset/validating/XXX_handler.go

需要填充： 是否需要注入 k8s client 如 pod/mutating
关键方法： mutatingSidecarSetFN 或 ValidatingSidecarSetFn  


===================================

sidecar 容器可以：
1. 日志代理转发 fluentd
2. service mesh, like istio 
3. 代理 docker ambasador
4. 探活： 检查某些组件是不是正常工作
5. 辅助性工作：拷贝文件 下载文件




kubernetes GPU:
加速部署 通过容器构建 避免重复部署 机器学习复杂环境
提升集群资源使用率 统一调度和分配集群资源
保障资源独享：利用容器隔离异构设备 避免互相影响

构建支持GPU 容器镜像
利用docker 将GPU设备和以依赖库映射到容器中

nvidia 驱动比较稳定， 宿主机安装nvidia驱动， cuda以上 交给容器来做

统一台机器上安装不同cuda镜像

docker run --it --volumn=nvidia-driver_***:/usr/local/nvidia:ro --device=/dev/nvidiactl --device 

kubectl create -f nvidia-device-plugin.yml

kubectl describle node gpu--node-01