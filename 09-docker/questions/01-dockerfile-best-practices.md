---
id: 1
title: Dockerfile best practices — security and size
difficulty: medium
week: 09
topics: [docker, images]
tags: [dockerfile, layers, multistage, security]
author: pravinmishraaws
reviewed: false
---

## Question
List key practices to keep images small and secure.

## References
- Docker Docs — Best practices

## From the Project

The Petclinic Platform builds all eight Spring Boot microservices from a single multi-stage Dockerfile at `docker/Dockerfile` in the application repo:

- **Multi-stage build:** compile stage uses the full JDK; the final image uses only the JRE — smaller attack surface, smaller image size
- **Base image:** `eclipse-temurin:17` — supports `linux/arm64`, required for ARM/Graviton EKS nodes (t4g.small)
- **Memory limit:** 512 MiB per container — set at both the Docker and Kubernetes levels
- **Non-root:** containers run without root privileges via Kubernetes security context (`runAsNonRoot: true`)
- **Spring profile:** `SPRING_PROFILES_ACTIVE=docker` switches the active Spring configuration at runtime — no code change needed between local and container execution

One Dockerfile. Eight services. Each service runs the same image with different Spring profiles and environment-specific config injected at startup.

*Built as part of the [Agentic DevOps with Claude Code](https://www.udemy.com/course/agentic-devops-with-claude-code/) course.*
