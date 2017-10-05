---
title: "Azure Container Instances 컨테이너 그룹"
description: "컨테이너 그룹이 Azure Container Instances에서 작동하는 방법 이해"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="525d6-103">Azure Container Instances의 컨테이너 그룹</span><span class="sxs-lookup"><span data-stu-id="525d6-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="525d6-104">Azure Container Instances의 최상위 리소스는 컨테이너 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="525d6-105">이 문서에서는 컨테이너 그룹의 정의와 이들이 지원하는 시나리오 유형에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="525d6-106">컨테이너 그룹 작동 방식</span><span class="sxs-lookup"><span data-stu-id="525d6-106">How a container group works</span></span>

<span data-ttu-id="525d6-107">컨테이너 그룹은 같은 호스트 컴퓨터에서 예약되어 있고 라이프사이클, 로컬 네트워크 및 저장소 볼륨을 공유하는 컨테이너 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="525d6-108">[Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 및 [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/)의 *Pod* 개념과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="525d6-109">다음 다이어그램은 여러 컨테이너가 포함된 컨테이너 그룹의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![컨테이너 그룹 예][container-groups-example]

<span data-ttu-id="525d6-111">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="525d6-111">Note that:</span></span>

- <span data-ttu-id="525d6-112">그룹은 단일 호스트 컴퓨터에서 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="525d6-113">그룹에는 1개의 노출 포트가 있는 단일 공용 IP 주소를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="525d6-114">이 그룹은 2개의 컨테이너로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-114">The group is made up of two containers.</span></span> <span data-ttu-id="525d6-115">하나의 컨테이너는 포트 80을 수신하고, 다른 컨테이너는 포트 5000을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="525d6-116">그룹에는 볼륨 탑재로 2개의 Azure 파일 공유가 포함되어 있으며, 각 컨테이너는 공유 중 하나를 로컬에서 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="525d6-117">네트워킹</span><span class="sxs-lookup"><span data-stu-id="525d6-117">Networking</span></span>

<span data-ttu-id="525d6-118">컨테이너 그룹은 IP 주소와 해당 IP 주소에서 포트 네임스페이스를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="525d6-119">외부 클라이언트가 그룹 내 컨테이너에 도달하게 지원하려면 IP 주소와 컨테이너에서 해당 포트를 공개해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="525d6-120">그룹 내의 컨테이너가 포트 네임스페이스를 공유하고 있으므로 포트 매핑이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="525d6-121">그룹 내 컨테이너는 해당 포트가 그룹의 IP 주소에 외부적으로 노출되어 있지 않은 경우에도 이들이 노출한 포트의 localhost를 통해 서로 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="525d6-122">저장소</span><span class="sxs-lookup"><span data-stu-id="525d6-122">Storage</span></span>

<span data-ttu-id="525d6-123">컨테이너 그룹 내에서 탑재할 외부 볼륨을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="525d6-124">해당 볼륨을 그룹의 개별 컨테이너 내에 있는 특정 경로에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="525d6-125">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="525d6-125">Common scenarios</span></span>

<span data-ttu-id="525d6-126">다중 컨테이너 그룹은 단일한 기능적 작업을 다른 팀을 통해 전달하고 별도의 리소스 요구 사항을 갖도록 작은 여러 컨테이너 이미지로 나누려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="525d6-127">사용 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-127">Example usage could include:</span></span>

- <span data-ttu-id="525d6-128">응용 프로그램 컨테이너 및 로깅 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="525d6-128">An application container and a logging container.</span></span> <span data-ttu-id="525d6-129">로깅 컨테이너는 주 응용 프로그램에서 출력한 로그 및 메트릭을 수집하여 장기 저장소로 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="525d6-130">응용 프로그램 및 모니터링 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="525d6-130">An application and a monitoring container.</span></span> <span data-ttu-id="525d6-131">모니터링 컨테이너는 응용 프로그램이 올바르게 실행 중이고 응답하고 있는지 확인하기 위해 응용 프로그램에 정기적으로 요청을 보내고, 그렇지 않은 경우 경고를 올립니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="525d6-132">웹 응용 프로그램을 처리하는 컨테이너와 원본 제어에서 최신 콘텐츠를 풀링하는 컨테이너</span><span class="sxs-lookup"><span data-stu-id="525d6-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="525d6-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="525d6-133">Next steps</span></span>

<span data-ttu-id="525d6-134">Azure Resource Manager 템플릿을 통해 [다중 컨테이너 그룹 배포](container-instances-multi-container-group.md) 방법을 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png