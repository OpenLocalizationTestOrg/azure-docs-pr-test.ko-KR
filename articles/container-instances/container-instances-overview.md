---
title: "aaaAzure 컨테이너 인스턴스 개요 | Azure 문서"
description: "Azure Container Instances 이해"
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="e7faf-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="e7faf-103">Azure Container Instances</span></span>

<span data-ttu-id="e7faf-104">컨테이너에서 hello 기본 설정 방법을 toopackage 신속 하 게 내용이, 배포 및 클라우드 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="e7faf-105">Azure 컨테이너 인스턴스는 가장 빠른 hello 및 가장 간단한 방법은 toorun tooprovision 모든 가상 컴퓨터 필요 없이 및 tooadopt 더 높은 수준의 서비스를 필요 없이 azure에서 컨테이너를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="e7faf-106">Azure Container Instances는 간단한 응용 프로그램, 작업 자동화 및 빌드 작업 등 격리된 컨테이너에서 작동할 수 있는 모든 시나리오에 적합한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="e7faf-107">Hello 컨테이너 오케스트레이션, 여러 컨테이너, 자동 크기 조정 및 조정 된 응용 프로그램 업그레이드에서 서비스 검색을 포함 하 여 전체 필요 있는 시나리오에 대 한 권장 [Azure 컨테이너 서비스](https://docs.microsoft.com/azure/container-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="e7faf-108">빠른 시작 시간</span><span class="sxs-lookup"><span data-stu-id="e7faf-108">Fast startup times</span></span>

<span data-ttu-id="e7faf-109">컨테이너는 가상 컴퓨터를 통한 상당한 시작 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="e7faf-110">Azure 컨테이너 인스턴스와 초 hello 필요 tooprovision 없이 Azure에서 컨테이너를 시작 하 고 Vm을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="e7faf-111">하이퍼바이저 수준 보안</span><span class="sxs-lookup"><span data-stu-id="e7faf-111">Hypervisor-level security</span></span>

<span data-ttu-id="e7faf-112">지금까지는 컨테이너가 응용 프로그램 종속성 격리 및 리소스 관리를 제공했지만 적대적인 다중 테넌트 사용을 위해서 충분히 보강되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="e7faf-113">Azure Container Instances를 통해 응용 프로그램은 VM에서처럼 컨테이너에 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="e7faf-114">사용자 지정 크기</span><span class="sxs-lookup"><span data-stu-id="e7faf-114">Custom sizes</span></span>

<span data-ttu-id="e7faf-115">컨테이너는 일반적으로 최적화 된 toorun 단일 응용 프로그램 뿐만 해당 응용 프로그램의 정확한 요구 hello 크게 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="e7faf-116">Azure Container Instances를 통해 CPU 코어 및 메모리를 기준으로 필요한 사항을 정확히 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="e7faf-117">비용을 지불 요청 내용에 따라 hello가 청구 한 청구 둘째, 필요에 따라 지출를 정밀 하 게 최적화할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="e7faf-118">공용 IP 연결</span><span class="sxs-lookup"><span data-stu-id="e7faf-118">Public IP connectivity</span></span>

<span data-ttu-id="e7faf-119">Azure 컨테이너 인스턴스를 사용 하면 컨테이너를 지정할 수 있습니다 직접 toohello 공용 IP 주소를 사용 하 여 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="e7faf-120">Hello 이후에서 가상 네트워크와 네트워킹 기능 tooinclude 통합, 부하 분산 장치, 및 hello Azure 네트워킹 인프라의 다른 핵심 요소는 म 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="e7faf-121">영구 저장소</span><span class="sxs-lookup"><span data-stu-id="e7faf-121">Persistent storage</span></span>

<span data-ttu-id="e7faf-122">tooretrieve Azure 컨테이너 인스턴스 상태를 유지 하 고, Azure의 탑재를 직접 공유 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="e7faf-123">Linux 및 Windows 컨테이너</span><span class="sxs-lookup"><span data-stu-id="e7faf-123">Linux and Windows containers</span></span>

<span data-ttu-id="e7faf-124">Azure 컨테이너 인스턴스와 두 창을 예약할 수 있습니다 및 Linux 컨테이너와 동일한 API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="e7faf-125">단순히 hello 기본 OS 유형 및 다른 모든 요소는 동일를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="e7faf-126">공동 예약된 그룹</span><span class="sxs-lookup"><span data-stu-id="e7faf-126">Co-scheduled groups</span></span>

<span data-ttu-id="e7faf-127">Azure Container Instances는 호스트 컴퓨터, 로컬 네트워크, 저장소 및 수명 주기를 공유하는 다중 컨테이너 그룹의 예약을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="e7faf-128">이렇게 하면 toocombine 하면 다른 사용자와 기본 응용 프로그램 로깅 등의 지원 역할에 속하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7faf-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7faf-129">Next steps</span></span>

<span data-ttu-id="e7faf-130">단일 명령을 사용 하 여 컨테이너 tooAzure 배포 해 보세요 우리의 [퀵 스타트 가이드](container-instances-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7faf-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
