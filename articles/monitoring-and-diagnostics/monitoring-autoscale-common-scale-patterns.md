---
title: "자동 크기 조정의 일반 패턴의 aaaOverview | Microsoft Docs"
description: "Azure의 리소스 크기를 조정 hello 일반적인 패턴 tooauto 중 일부에 대해 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="1ffe5-103">일반적인 자동 크기 조정 패턴 개요</span><span class="sxs-lookup"><span data-stu-id="1ffe5-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="1ffe5-104">이 문서에서는 Azure의 리소스에 몇 가지 일반적인 패턴 tooscale hello 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="1ffe5-105">모니터 자동 크기 조정 azure tooVirtual 컴퓨터 눈금 집합 (VMSS), 클라우드 서비스, 앱 서비스 계획 및 앱 서비스 환경에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="1ffe5-106">시작</span><span class="sxs-lookup"><span data-stu-id="1ffe5-106">Lets get started</span></span>

<span data-ttu-id="1ffe5-107">이 문서에서는 사용자가 자동 크기 조정에 대해 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="1ffe5-108">있습니다 수 [시작된 여기 tooscale 리소스 가져오기][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="1ffe5-109">일반 배율 패턴 hello hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="1ffe5-110">CPU 기준 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1ffe5-110">Scale based on CPU</span></span>

<span data-ttu-id="1ffe5-111">웹앱(/VMSS/클라우드 서비스 역할)이 있습니다. 그리고</span><span class="sxs-lookup"><span data-stu-id="1ffe5-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="1ffe5-112">원하는 tooscale 아웃/배율에 따라 CPU에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="1ffe5-113">또한 tooensure 합니다 인스턴스의 최소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="1ffe5-114">또한 원하는 tooensure 인스턴스를 확장할 수는 최대 한도 toohello 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![CPU 기준 크기 조정][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="1ffe5-116">평일과 주말에 대해 다르게 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1ffe5-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="1ffe5-117">웹앱(/VMSS/클라우드 서비스 역할)이 있습니다. 그리고</span><span class="sxs-lookup"><span data-stu-id="1ffe5-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="1ffe5-118">기본적으로 3개의 인스턴스를 원합니다(평일)</span><span class="sxs-lookup"><span data-stu-id="1ffe5-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="1ffe5-119">트래픽 주말에 감염 되지 않은 고 따라서 too1 인스턴스 아래로 tooscale 주말에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![평일과 주말에 대해 다르게 크기 조정][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="1ffe5-121">휴일 동안에 대해 다르게 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1ffe5-121">Scale differently during holidays</span></span>

<span data-ttu-id="1ffe5-122">웹앱(/VMSS/클라우드 서비스 역할)이 있습니다. 그리고</span><span class="sxs-lookup"><span data-stu-id="1ffe5-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="1ffe5-123">위/아래로 기본적으로 CPU 사용량 기반 tooscale 원합니다</span><span class="sxs-lookup"><span data-stu-id="1ffe5-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="1ffe5-124">그러나 휴일 기간 (또는 비즈니스에 대 한 중요 한 일) 동안 toooverride hello 기본값을 사용할 더 많은 용량을 확보 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![휴일에 대해 다르게 크기 조정][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="1ffe5-126">사용자 지정 메트릭 기준 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1ffe5-126">Scale based on custom metric</span></span>

<span data-ttu-id="1ffe5-127">웹 프런트 엔드 및 백 엔드 hello와 통신 하는 API 계층 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffe5-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="1ffe5-128">Hello 프런트 엔드에서는 사용자 지정 이벤트에 따라 tooscale hello API 계층을 원하는 (예: 쇼핑 카트 hello에 있는 항목의 hello 수에 따라 체크 아웃 프로세스 tooscale 원하는)</span><span class="sxs-lookup"><span data-stu-id="1ffe5-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![사용자 지정 메트릭 기준 크기 조정][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png