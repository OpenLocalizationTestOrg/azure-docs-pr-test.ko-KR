---
title: "Kubernetes용 Azure Container Service 소개 | Microsoft Docs"
description: "Kubernetes용 Azure Container Service를 통해 Azure에서 컨테이너 기반 응용 프로그램을 간단히 배포 및 관리할 수 있습니다."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, 컨테이너, 마이크로 서비스, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: 92cdbe20e7a2974a734dfed5294c547866050290
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-azure-container-service-for-kubernetes"></a><span data-ttu-id="10e99-104">Kubernetes용 Azure Container Service 소개</span><span class="sxs-lookup"><span data-stu-id="10e99-104">Introduction to Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="10e99-105">Kubernetes용 Azure Container Service를 사용하면 컨테이너화된 응용 프로그램을 실행하는 미리 구성된 가상 컴퓨터의 클러스터를 보다 간편하게 만들고 구성하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-105">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="10e99-106">이를 통해 기존 기술을 사용하거나 크고 확장된 커뮤니티 전문 지식의 본문을 이용하여 Microsoft Azure의 컨테이너 기반 응용 프로그램을 배포하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-106">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="10e99-107">Azure Container Service를 사용하면 Kubernetes 및 Docker 이미지 형식을 통해 응용 프로그램 이식성을 유지하면서 Azure의 엔터프라이즈급 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-107">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="10e99-108">Kubernetes용 Azure Container Service 사용</span><span class="sxs-lookup"><span data-stu-id="10e99-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="10e99-109">Azure 컨테이너 서비스를 사용하는 우리의 목표는 현재 우리 고객들 사이에서 인기 있는 오픈 소스 도구 및 기술을 사용하여 컨테이너 호스팅 환경을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-109">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="10e99-110">이를 위해 표준 Kubernetes API 끝점을 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-110">To this end, we expose the standard Kubernetes API endpoints.</span></span> <span data-ttu-id="10e99-111">이러한 표준 끝점을 사용하면 Kubernetes 클러스터와 통신할 수 있는 모든 소프트웨어를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-111">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span></span> <span data-ttu-id="10e99-112">예를 들어 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) 또는 [draft](https://github.com/Azure/draft)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="10e99-113">Azure Container Service를 사용하여 Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="10e99-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="10e99-114">Azure Container Service를 사용하기 시작하려면 [Azure CLI 2.0](container-service-kubernetes-walkthrough.md)을 사용하거나 포털(**Azure Container Service**에 대한 Marketplace 검색)을 통해 Azure Container Service 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-114">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="10e99-115">Azure Resource Manager 템플릿을 통해 더 많은 제어를 필요로 하는 고급 사용자인 경우 오픈 소스 [acs-engine](https://github.com/Azure/acs-engine) 프로젝트를 사용하여 사용자 지정 Kubernetes 클러스터를 빌드하여 `az` CLI를 통해 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-115">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="10e99-116">Kubernetes 사용</span><span class="sxs-lookup"><span data-stu-id="10e99-116">Using Kubernetes</span></span>
<span data-ttu-id="10e99-117">Kubernetes는 컨테이너화된 응용 프로그램의 배포, 크기 조정 및 관리를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="10e99-118">여기에는 다음과 같이 풍부한 기능들이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="10e99-119">자동 저장소 적재</span><span class="sxs-lookup"><span data-stu-id="10e99-119">Automatic binpacking</span></span>
* <span data-ttu-id="10e99-120">자동 복구</span><span class="sxs-lookup"><span data-stu-id="10e99-120">Self-healing</span></span>
* <span data-ttu-id="10e99-121">수평적 크기 조정</span><span class="sxs-lookup"><span data-stu-id="10e99-121">Horizontal scaling</span></span>
* <span data-ttu-id="10e99-122">서비스 검색 및 부하 분산</span><span class="sxs-lookup"><span data-stu-id="10e99-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="10e99-123">자동화된 롤아웃 및 롤백</span><span class="sxs-lookup"><span data-stu-id="10e99-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="10e99-124">비밀 및 구성 관리</span><span class="sxs-lookup"><span data-stu-id="10e99-124">Secret and configuration management</span></span>
* <span data-ttu-id="10e99-125">저장소 오케스트레이션</span><span class="sxs-lookup"><span data-stu-id="10e99-125">Storage orchestration</span></span>
* <span data-ttu-id="10e99-126">일괄 처리 실행</span><span class="sxs-lookup"><span data-stu-id="10e99-126">Batch execution</span></span>

<span data-ttu-id="10e99-127">Azure Container Service를 통해 배포된 Kubernetes의 아키텍처 다이어그램:</span><span class="sxs-lookup"><span data-stu-id="10e99-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Kubernetes를 사용하도록 구성된 Azure Container Service.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="10e99-129">비디오</span><span class="sxs-lookup"><span data-stu-id="10e99-129">Videos</span></span>

<span data-ttu-id="10e99-130">Azure Container Services의 Kubernetes 지원(Azure Friday, 2017년 1월):</span><span class="sxs-lookup"><span data-stu-id="10e99-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="10e99-131">Kubernetes에서 응용 프로그램을 개발 및 배포하기 위한 도구(Azure OpenDev, 2017년 6월):</span><span class="sxs-lookup"><span data-stu-id="10e99-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="10e99-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10e99-132">Next steps</span></span>

<span data-ttu-id="10e99-133">[Kubernetes 빠른 시작](container-service-kubernetes-walkthrough.md)을 살펴보고 오늘날 Azure Container Service에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="10e99-133">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span></span>