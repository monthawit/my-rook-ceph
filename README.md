* Deploy Rook Operator and Cluster by Using helm
```bash
root@openstack-master-01:/home/ubuntu/rook-helm# cat helm-and-ceph-command.txt 
======== 0. add helm repo  =============

repo add rook-release https://charts.rook.io/release

======== 1. install operator ============

helm install --create-namespace --namespace rook-ceph rook-ceph rook-release/rook-ceph -f values.yaml

======== 2. install cluster ============

helm install --create-namespace --namespace rook-ceph rook-ceph-cluster \
   --set operatorNamespace=rook-ceph rook-release/rook-ceph-cluster -f values.yaml
```
