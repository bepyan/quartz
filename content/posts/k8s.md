---
title: k8s
date: 2024-08-28
tags:
  - seed
  - infra
---

Kubernetes(k8s) is an open source system for automating deployment, scaling, and management of containerized applications.

domain → [[GLSB]] → [[VIP]] → [[Ingress node]] → [[Ingress]] → [[Service]] → [[Pod]]

## DKOS

> 카카오의 인프라에 맞게 구성할 수 있는 쿠버네티스
> https://cloud-learn.9rum.cc/document/Compute/dkosv3/

**Master**: 클러스터를 관리
**Worker**: 파드가 실행
**인그레스**: 클러스터 외부에서 클러스터 내의 파드에 접근할때 로드밸런서의 역할 (NGINX)

**파드**(Pod): 쿠버네티스에서 컨테이너가 실행되는 최소 단위, 하나의 파드 안에 여러 개의 컨테이너를 묶어서 관리

**레플리카세트**(ReplicaSet)