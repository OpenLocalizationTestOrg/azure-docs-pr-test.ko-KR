---
title: "aaaAzure 컨테이너 인스턴스 컨테이너 그룹"
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
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="f996f-103">Azure Container Instances의 컨테이너 그룹</span><span class="sxs-lookup"><span data-stu-id="f996f-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="f996f-104">컨테이너 인스턴스를 Azure의 hello 최상위 리소스는 컨테이너 그룹.</span><span class="sxs-lookup"><span data-stu-id="f996f-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="f996f-105">이 문서에서는 컨테이너 그룹의 정의와 이들이 지원하는 시나리오 유형에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="f996f-106">컨테이너 그룹 작동 방식</span><span class="sxs-lookup"><span data-stu-id="f996f-106">How a container group works</span></span>

<span data-ttu-id="f996f-107">컨테이너 그룹은 컬렉션 hello에 예약 하는 컨테이너의 동일 컴퓨터를 호스트 하 고 전체 수명 주기, 로컬 네트워크 및 저장소 볼륨을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="f996f-108">유사한 toohello 개념는 *pod* 에 [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 및 [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="f996f-109">hello 다음 다이어그램의 예가 나와 여러 컨테이너를 포함 하는 컨테이너 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![컨테이너 그룹 예][container-groups-example]

<span data-ttu-id="f996f-111">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="f996f-111">Note that:</span></span>

- <span data-ttu-id="f996f-112">hello 그룹은 단일 호스트 컴퓨터에서 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="f996f-113">hello 그룹에는 단일 공용 IP 주소를 하나의 노출 된 포트와 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="f996f-114">두 컨테이너의 hello 그룹으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-114">hello group is made up of two containers.</span></span> <span data-ttu-id="f996f-115">하나의 컨테이너 hello 다른 5000 포트에서 수신 하는 동안 포트 80에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="f996f-116">각 컨테이너 로컬로 hello 공유 중 하나를 탑재 및 hello 그룹 볼륨 마운트도 두 개의 Azure 파일 공유를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="f996f-117">네트워킹</span><span class="sxs-lookup"><span data-stu-id="f996f-117">Networking</span></span>

<span data-ttu-id="f996f-118">컨테이너 그룹은 IP 주소와 해당 IP 주소에서 포트 네임스페이스를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="f996f-119">tooenable 외부 클라이언트 tooreach hello 그룹 내에서 컨테이너를 hello IP 주소에 대 한 hello 컨테이너에서 hello 포트를 노출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="f996f-120">Hello 그룹 내의 컨테이너 포트 네임 스페이스를 공유 하므로 포트 매핑은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="f996f-121">그룹 내의 컨테이너 도달할 수 서로 hello에 localhost를 통해를 노출 하는 포트 hello 그룹의 IP 주소에 해당 포트를 외부적으로 노출 되지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="f996f-122">저장소</span><span class="sxs-lookup"><span data-stu-id="f996f-122">Storage</span></span>

<span data-ttu-id="f996f-123">컨테이너 그룹 내에서 외부 볼륨 toomount를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="f996f-124">해당 볼륨 그룹의 hello 개별 컨테이너 내에서 특정 경로에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="f996f-125">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="f996f-125">Common scenarios</span></span>

<span data-ttu-id="f996f-126">다중 컨테이너 그룹은 적은 수의 다른 팀에서 제공 되며,와 별도 리소스 요구 사항이 있는 컨테이너 이미지에는 단일 기능 작업을 toodivide을 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="f996f-127">사용 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-127">Example usage could include:</span></span>

- <span data-ttu-id="f996f-128">응용 프로그램 컨테이너 및 로깅 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="f996f-128">An application container and a logging container.</span></span> <span data-ttu-id="f996f-129">hello 로깅 컨테이너는 hello 주 응용 프로그램에 의해 hello 로그 및 메트릭 출력을 수집 하 고 toolong 장기적 저장을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="f996f-130">응용 프로그램 및 모니터링 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="f996f-130">An application and a monitoring container.</span></span> <span data-ttu-id="f996f-131">컨테이너를 주기적으로 모니터링 하는 hello 실행 중 이며 올바르게 응답 하지 않으면 경고를 발생 하는 요청 toohello 응용 프로그램 tooensure를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="f996f-132">웹 응용 프로그램을 처리 하는 컨테이너 및 소스 제어에서 최신 콘텐츠 hello 당겨 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="f996f-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f996f-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f996f-133">Next steps</span></span>

<span data-ttu-id="f996f-134">너무 방법에 대해 알아봅니다[다중 컨테이너 그룹 배포](container-instances-multi-container-group.md) Azure 리소스 관리자 템플릿을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f996f-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png