---
title: Sig Multicluster洞察
---

## 当前工作

* ClusterSet / Namespace Sameness
ClusterSet： 一组 single authority 管理的集群，组内集群高度互信
Namespace Sameness：应用到ClusterSet中，在给定NS中权限和特征一致，NS不必存在于每个集群中，但需要保持一致的行为
* About API for storing cluster properties such as Cluster ID / ClusterSet
唯一标识集群以及他们在某个ClusterSet的成员关系
可扩展存放集群关联的键值对属性
* Multicluster Services API / Multicluster DNS
Member1：deployment，service，serviceExport
Member2：deployment，serviceImport
* KEP status update
* Gateway API + MCS
```yaml
kind: HTTPRoute
apiVersion: gateway.networking.k8s.io/v1beta1
metadata:
    name: store
spec:
    parentRefs:
    - name: external-http
    rules:
    - backendRefs:
      - group: multicluster.x-k8s.io
        kind: ServiceImport
        name: store-v1
        port: 8080
        weight: 90
      - group: multicluster.x-k8s.io
        kind: ServiceImport
        name: store-v2
        port: 8080
        weight: 10
```

## 下一步计划

* More sophistication on multicluster networking
- Network policy - applying policy uniformly across clusters
- Multi-network - stitching together clusters on different networks

* Multicluster controllers / multicluster leader election
* Work API
* Multicluster registry / multicluster control plane
* StatefulSetSlices for migrating stateful sets between clusters

