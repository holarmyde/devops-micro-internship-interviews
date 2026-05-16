---
id: Q1501
title: What is Karpenter and how is it different from Cluster Autoscaler?
difficulty: medium
week: 15
topics: [karpenter, autoscaling, eks, kubernetes]
tags: [karpenter, cluster-autoscaler, autoscaling, eks, spot, node-provisioning]
author: pravinmishraaws
reviewed: true
---

## Question
What is Karpenter and how is it different from Cluster Autoscaler?

## Short Answer
Karpenter is a node autoscaler for Kubernetes that calls the EC2 Fleet API directly to provision exactly the right instance type for pending pods — typically in under 60 seconds. Cluster Autoscaler scales pre-defined Auto Scaling Groups, which is slower and less flexible.

## Deep Dive
When pods cannot be scheduled because there is no available node capacity, Karpenter steps in:

1. It reads the pending pod's resource requests (CPU, memory, GPU)
2. It evaluates the NodePool configuration — which instance families, architectures, and capacity types are allowed
3. It calls the EC2 Fleet API directly and provisions the most cost-efficient instance that satisfies the pod's requirements
4. The node joins the cluster and the pod schedules — typically within 60 seconds

**Key difference from Cluster Autoscaler:**

| | Karpenter | Cluster Autoscaler |
|---|---|---|
| Provisioning | Calls EC2 Fleet API directly | Scales ASG min/max |
| Instance selection | Picks the right size for the workload | Uses whatever the ASG was configured with |
| Speed | ~60 seconds | Several minutes |
| Spot handling | Built-in diversification across families | Requires separate Spot ASGs |

**NodePool example:**
```yaml
apiVersion: karpenter.sh/v1
kind: NodePool
spec:
  template:
    spec:
      requirements:
        - key: karpenter.sh/capacity-type
          operator: In
          values: ["spot", "on-demand"]
        - key: kubernetes.io/arch
          operator: In
          values: ["arm64"]
```

For a Kubernetes platform on AWS, Karpenter is the current industry standard. Cluster Autoscaler is still used but Karpenter is replacing it for most new deployments.

## Pitfalls
- Not configuring instance diversification — relying on one instance type for Spot means mass interruptions when that type is reclaimed
- Forgetting to set resource requests on pods — Karpenter cannot size nodes correctly without them
- Not setting a `disruption` budget — Karpenter may consolidate nodes during business hours and cause brief pod restarts

## References
- [Karpenter Docs — Getting Started](https://karpenter.sh/docs/getting-started/)
- [Karpenter vs Cluster Autoscaler — AWS Blog](https://aws.amazon.com/blogs/containers/using-amazon-eks-with-karpenter-for-optimized-computing/)
