---
title: "Azure 컨테이너 서비스에 대 한 에이전트 풀 aaaDC/OS | Microsoft Docs"
description: "Azure 컨테이너 서비스 DC/OS 클러스터와 함께 hello 공용 및 개인 에이전트 풀을 작동 하는 방식"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="66c7a-104">Azure Container Service의 DC/OS 에이전트 풀</span><span class="sxs-lookup"><span data-stu-id="66c7a-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="66c7a-105">Azure Container Service의 DC/OS 클러스터는 2개의 풀, 즉 공용 풀과 개인 풀에 에이전트 노드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="66c7a-106">응용 프로그램을 배포할 수 있습니다 컨테이너 서비스의 컴퓨터 간에 내게 필요한 옵션에 영향을 주는 tooeither 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="66c7a-107">hello 컴퓨터 수 있는 노출 된 toohello 인터넷 (공용) 또는 내부 (개인)을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="66c7a-108">이 문서에서는 공용 및 개인 풀이 있는 이유에 대한 간략한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="66c7a-109">**개인 에이전트**: 개인 에이전트 노드는 라우팅할 수 없는 네트워크를 통해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="66c7a-110">이 네트워크는 hello 관리 영역에서 또는 hello 공용 영역에 지 라우터를 통해에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="66c7a-111">기본적으로 DC/OS는 사용자 에이전트 노드에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="66c7a-112">**공용 에이전트**: 공용 에이전트 노드는 공개적으로 액세스 가능한 네트워크를 통해 DC/OS 앱과 서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="66c7a-113">DC/OS 네트워크 보안에 대 한 자세한 내용은 참조 hello [DC/OS 문서](https://dcos.io/docs/1.7/administration/securing-your-cluster/)합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="66c7a-114">에이전트 풀 배포</span><span class="sxs-lookup"><span data-stu-id="66c7a-114">Deploy agent pools</span></span>

<span data-ttu-id="66c7a-115">hello DC/OS 에이전트 풀 Azure 컨테이너 서비스는 다음과 같이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="66c7a-116">hello **개인 풀** hello 시점을 지정 하는 에이전트 노드 수가 포함 되어 있습니다 [hello DC/OS 클러스터 배포](container-service-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="66c7a-117">hello **공용 풀** 처음에 미리 결정 된 에이전트 노드 수가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="66c7a-118">이 풀은 hello DC/OS 클러스터 프로 비전 될 때 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="66c7a-119">hello 개인 풀과 hello 공용 풀은 Azure 가상 컴퓨터 크기 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="66c7a-120">배포 후 이러한 풀의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="66c7a-121">에이전트 풀 사용</span><span class="sxs-lookup"><span data-stu-id="66c7a-121">Use agent pools</span></span>
<span data-ttu-id="66c7a-122">기본적으로 **마라톤** 모든 새 응용 프로그램 toohello 배포 *개인* 에이전트 노드.</span><span class="sxs-lookup"><span data-stu-id="66c7a-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="66c7a-123">배포 응용 프로그램 toohello hello tooexplicitly 있는 *공용* 노드 hello hello 응용 프로그램을 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="66c7a-124">선택 hello **Optional** 탭 하 고 입력 **slave_public** hello에 대 한 **리소스 역할 수락** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="66c7a-125">이 과정은 문서화 되어 [여기](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) 및 hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66c7a-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66c7a-126">Next steps</span></span>
* <span data-ttu-id="66c7a-127">[DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="66c7a-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="66c7a-128">너무 방법에 대해 알아봅니다[hello 방화벽을 열고](container-service-enable-public-access.md) Azure tooallow 공용 액세스 tooyour DC/OS 컨테이너에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c7a-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

