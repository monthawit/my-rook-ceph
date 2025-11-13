# Deploy Rook Operator and Cluster by Using helm
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

# Test Ceph S3 Service By s3cmd

### Install

```bash
apt install s3cmd -y
```
### Add Config

```bash
vi ~/.s3cfg
```

### Add

```bash
[default]
access_key = xxxxxx
secret_key = xxxxxxx
host_base = s3.milkymonz.com:443
host_bucket = s3.milkymonz.com/milky01:443
use_https = Yes
signature_v2 = No
```

### Upload file 
```bash
s3cmd put values.yaml s3://milky01

upload: 'values.yaml' -> 's3://milky01/values.yaml'  [1 of 1]
 23428 of 23428   100% in    0s  1036.04 KB/s  done
```

### List File 

```bash
s3cmd ls s3://milky01
                          DIR  s3://milky01/TheTop/
                          DIR  s3://milky01/test01/
2025-10-07 09:29          998  s3://milky01/ceph-ui-ingress.yaml
2025-10-07 09:20         4244  s3://milky01/gen-cert.yaml
2025-10-07 09:21           90  s3://milky01/upgrade.txt
2025-10-07 09:31        23428  s3://milky01/values.yaml
```
