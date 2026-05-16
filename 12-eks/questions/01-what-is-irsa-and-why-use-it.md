---
id: 1
title: What is IRSA and why do you use it?
difficulty: medium
week: 12
topics: [eks, iam, irsa, oidc, security]
tags: [eks, irsa, iam, oidc, service-account, security]
author: pravinmishraaws
reviewed: true
---

## Question
What is IRSA and why do you use it instead of other methods of giving AWS permissions to pods?

## Short Answer
IRSA (IAM Roles for Service Accounts) lets a Kubernetes pod assume an IAM role without storing any AWS credentials in the pod. The mechanism is OIDC — EKS has an identity provider, and the IAM trust policy scopes the role to a specific service account in a specific namespace.

## Deep Dive
IRSA works through three components working together:

1. **EKS OIDC provider** — EKS creates an OIDC identity provider endpoint for the cluster
2. **IAM trust policy** — the role's trust policy says "this role can be assumed by service account X in namespace Y of cluster Z"
3. **Kubernetes service account annotation** — the pod's service account is annotated with the IAM role ARN

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: external-secrets
  namespace: external-secrets
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::123456789:role/ExternalSecretsRole
```

Common components that use IRSA: **External Secrets Operator**, **ALB Ingress Controller**, **EBS CSI Driver**, **Karpenter**. Each gets its own narrowly-scoped IAM role — the pod gets exactly the permissions it needs and nothing else.

**Why not use EC2 instance profiles instead?** Instance profiles grant permissions to every pod on the node. One compromised pod can access AWS resources intended for another. IRSA scopes permissions to the individual pod identity.

**Why not use access keys in environment variables?** Keys can be leaked in logs, committed to Git, or over-scoped. They require manual rotation. IRSA uses short-lived tokens issued by the OIDC provider — no long-lived credentials anywhere.

## Pitfalls
- Forgetting to create the OIDC provider for the cluster — IRSA silently fails without it
- Over-scoping the IAM role — give each component only what it needs, not `AdministratorAccess`
- Using the wrong namespace or service account name in the trust policy — the assume-role call will be denied

## References
- [AWS Docs — IAM roles for service accounts](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)
- [AWS Docs — Create an IAM OIDC provider for your cluster](https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html)
