#k8s 使用ceph rbd作为存储
## 到external-storage-rbd目录下运行所有yaml，用以支持rbd.
```
kubectl apply -f ./
```
## 使用的镜像quay.io/external_storage/rbd-provisioner
### https://github.com/linqingping/external-storage可以在里面下载相应的ceph相关的然后执行部署
### 新增了如下内容

```
  - apiGroups: [""]
    resources: ["secrets"]
    verbs: ["create","get","list","watch"]
```
## 到k8sUseRBD-example执行部署StorageClass和访问ceph的密钥secrets
```
kubectl apply -f storage_class.yaml
kubectl apply -f storage_secret.yaml
```
## 测试
```
kubectl apply -f storage_pvcTest.yaml #创建pvc
kubectl apply -f storage_podTest.yaml #创建pod挂载pvc,
查看绑定情况
kubectl exec -it ceph-pod1 mount |grep rbd
```
