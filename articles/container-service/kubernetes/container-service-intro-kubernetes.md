---
title: "aaaIntroduction tooAzure Kubernetes에 대 한 컨테이너 서비스 | Microsoft Docs"
description: "Kubernetes에 대 한 컨테이너 서비스를 azure 간단한 toodeploy 있고 Azure에서 컨테이너 기반 응용 프로그램을 관리 합니다."
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
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="cb086-104">소개 tooAzure Kubernetes에 대 한 컨테이너 서비스</span><span class="sxs-lookup"><span data-stu-id="cb086-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="cb086-105">간단한 toocreate Kubernetes에 대 한 azure 컨테이너 서비스를 통해 구성 하 고 미리 구성 된 toorun 컨테이너 화 가능한 응용 프로그램이 있는 가상 컴퓨터의 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="cb086-106">Toouse 있습니다를 통해 기존 기술을 사용 하면이 커뮤니티 전문, toodeploy 크기가 크고 점점 본문에 대해 하 고 Microsoft Azure에서 컨테이너 기반 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="cb086-107">Azure 컨테이너 서비스를 사용 하면 활용 hello Azure의 엔터프라이즈급 기능 Kubernetes 통해 응용 프로그램 이식성을 유지 하면서 수 있으며 Docker 이미지 형식 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="cb086-108">Kubernetes용 Azure Container Service 사용</span><span class="sxs-lookup"><span data-stu-id="cb086-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="cb086-109">Azure 컨테이너 서비스와 이러한 목표는 오픈 소스 도구와 기술을 담아 고객 사이에서 인기 오늘을 통해 tooprovide 컨테이너 호스팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="cb086-110">toothis 끝 hello 표준 Kubernetes API 끝점을 공개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="cb086-111">이러한 표준 끝점을 사용 하 여 tooa Kubernetes 클러스터 통신의 대상이 될 수 있는 모든 소프트웨어를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="cb086-112">예를 들어 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) 또는 [draft](https://github.com/Azure/draft)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="cb086-113">Azure Container Service를 사용하여 Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="cb086-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="cb086-114">Azure 컨테이너 서비스를 사용 하 여 toobegin hello로 Azure 컨테이너 서비스 클러스터를 배포할 [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) 또는 hello 포털을 통해 (마켓플레이스 검색 hello에 대 한 **Azure 컨테이너 서비스**).</span><span class="sxs-lookup"><span data-stu-id="cb086-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="cb086-115">Hello Azure 리소스 관리자 템플릿을 통해 더 많은 제어를 필요로 하는 고급 사용자 인 경우 hello 오픈 소스를 사용할 수 있습니다 [acs 엔진](https://github.com/Azure/acs-engine) 프로젝트 toobuild 사용자 고유의 사용자 지정 Kubernetes 클러스터링 하 고 hello를 통해 배포 `az` CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="cb086-116">Kubernetes 사용</span><span class="sxs-lookup"><span data-stu-id="cb086-116">Using Kubernetes</span></span>
<span data-ttu-id="cb086-117">Kubernetes는 컨테이너화된 응용 프로그램의 배포, 크기 조정 및 관리를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="cb086-118">여기에는 다음과 같이 풍부한 기능들이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="cb086-119">자동 저장소 적재</span><span class="sxs-lookup"><span data-stu-id="cb086-119">Automatic binpacking</span></span>
* <span data-ttu-id="cb086-120">자동 복구</span><span class="sxs-lookup"><span data-stu-id="cb086-120">Self-healing</span></span>
* <span data-ttu-id="cb086-121">수평적 크기 조정</span><span class="sxs-lookup"><span data-stu-id="cb086-121">Horizontal scaling</span></span>
* <span data-ttu-id="cb086-122">서비스 검색 및 부하 분산</span><span class="sxs-lookup"><span data-stu-id="cb086-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="cb086-123">자동화된 롤아웃 및 롤백</span><span class="sxs-lookup"><span data-stu-id="cb086-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="cb086-124">비밀 및 구성 관리</span><span class="sxs-lookup"><span data-stu-id="cb086-124">Secret and configuration management</span></span>
* <span data-ttu-id="cb086-125">저장소 오케스트레이션</span><span class="sxs-lookup"><span data-stu-id="cb086-125">Storage orchestration</span></span>
* <span data-ttu-id="cb086-126">일괄 처리 실행</span><span class="sxs-lookup"><span data-stu-id="cb086-126">Batch execution</span></span>

<span data-ttu-id="cb086-127">Azure Container Service를 통해 배포된 Kubernetes의 아키텍처 다이어그램:</span><span class="sxs-lookup"><span data-stu-id="cb086-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Azure 컨테이너 서비스 toouse Kubernetes를 구성합니다.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="cb086-129">비디오</span><span class="sxs-lookup"><span data-stu-id="cb086-129">Videos</span></span>

<span data-ttu-id="cb086-130">Azure Container Services의 Kubernetes 지원(Azure Friday, 2017년 1월):</span><span class="sxs-lookup"><span data-stu-id="cb086-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="cb086-131">Kubernetes에서 응용 프로그램을 개발 및 배포하기 위한 도구(Azure OpenDev, 2017년 6월):</span><span class="sxs-lookup"><span data-stu-id="cb086-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="cb086-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb086-132">Next steps</span></span>

<span data-ttu-id="cb086-133">Hello 탐색 [Kubernetes 퀵 스타트](container-service-kubernetes-walkthrough.md) toobegin 오늘날 Azure 컨테이너 서비스를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb086-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
