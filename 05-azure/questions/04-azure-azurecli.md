---
id: 4
title: Troubleshooting Failed Resource Deployments Using Azure CLI
difficulty: entry
week: 05
topics: [azure, cli, troubleshooting, deployment]
tags: [azure-cli, resource-manager, deployment-failure]
author: Tanisha Borana
reviewed: false
---

## Question
How would you troubleshoot a failed resource deployment using **Azure CLI** instead of relying on the Azure Portal?

## References

Microsoft Learn – Troubleshoot Azure Resource Manager deployments
Microsoft Documentation – az deployment group

## From the Project

The Petclinic Platform uses the AWS CLI as its day-to-day command-line tool. Key parallels between Azure CLI and AWS CLI:

| Azure CLI | AWS CLI |
|---|---|
| `az login` | `aws configure` / `aws sso login` |
| `az group list` | `aws ec2 describe-vpcs` |
| `az aks get-credentials` | `aws eks update-kubeconfig --name <cluster>` |
| `az acr login` | `aws ecr get-login-password \| docker login` |

The pattern is identical: authenticate, configure context, then run resource-specific commands. Both CLIs are first-class citizens for scripting and CI automation.

*Built as part of the [Agentic DevOps with Claude Code](https://www.udemy.com/course/agentic-devops-with-claude-code/) course.*
