---
title: "Azure CDN 리소스의 상태 모니터링 | Microsoft Docs"
description: "Azure 리소스 상태를 사용하여 Azure CDN 리소스의 상태를 모니터링하는 방법을 알아봅니다."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="98bdb-103">Azure CDN 리소스의 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="98bdb-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="98bdb-104">Azure CDN 리소스 상태는 [Azure 리소스 상태](../resource-health/resource-health-overview.md)의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="98bdb-105">Azure 리소스 상태를 사용하여 CDN 리소스의 상태를 모니터링하고 문제 해결을 위한 실행 지침을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="98bdb-106">Azure CDN 리소스 상태는 현재 글로벌 CDN 배달 및 API 기능의 상태만 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="98bdb-107">Azure CDN 리소스 상태는 개별 CDN 끝점을 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="98bdb-108">Azure CDN 리소스 상태를 피드하는 신호는 최대 15분 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="98bdb-109">Azure CDN 리소스 상태를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="98bdb-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="98bdb-110">[Azure Portal](https://portal.azure.com)에서 CDN 프로필로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="98bdb-111">**Settings** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-111">Click the **Settings** button.</span></span>

    ![설정 단추](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="98bdb-113">*지원 + 문제 해결*에서 **리소스 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN 리소스 상태](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="98bdb-115">*도움말 + 지원* 블레이드의 *리소스 상태* 타일에 나열된 CDN 리소스를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="98bdb-116">포털 오른쪽 위에 있는 원 안에 표시된 **?**를 클릭하여 *도움말 + 지원*으로</span><span class="sxs-lookup"><span data-stu-id="98bdb-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="98bdb-117">신속하게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-117">in the upper right corner of the portal.</span></span>
>
> ![도움말 + 지원](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="98bdb-119">Azure CDN 관련 메시지</span><span class="sxs-lookup"><span data-stu-id="98bdb-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="98bdb-120">아래에서 Azure CDN 리소스 상태와 관련된 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="98bdb-121">Message</span><span class="sxs-lookup"><span data-stu-id="98bdb-121">Message</span></span> | <span data-ttu-id="98bdb-122">권장 작업</span><span class="sxs-lookup"><span data-stu-id="98bdb-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="98bdb-123">하나 이상의 CDN 끝점을 중지, 제거 또는 잘못 구성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="98bdb-124">하나 이상의 CDN 끝점을 중지, 제거 또는 잘못 구성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="98bdb-125">죄송합니다. CDN 관리 서비스를 현재 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="98bdb-126">여기에서 상태 업데이트를 다시 확인하세요. 예상 해결 시간 이후에도 문제가 지속되는 경우 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="98bdb-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="98bdb-127">죄송합니다. CDN 끝점이 일부 CDN 공급자와 관련하여 진행 중인 문제로 인해 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="98bdb-128">여기에서 상태 업데이트를 다시 확인하세요. 문제 해결 도구를 사용하여 원본 및 CDN 끝점을 테스트하는 방법을 확인할 수 있습니다. 예상 해결 시간 이후에도 문제가 지속되는 경우 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="98bdb-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="98bdb-129">죄송합니다. CDN 끝점 구성 변경 사항에 전파 지연이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="98bdb-130">여기에서 상태 업데이트를 확인하세요. 구성 변경 내용이 예상 시간 내에 완전히 전파되지 않는 경우 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="98bdb-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="98bdb-131">죄송합니다. 보조 포털을 로드하는 동안 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="98bdb-132">여기에서 상태 업데이트를 다시 확인하세요. 예상 해결 시간 이후에도 문제가 지속되는 경우 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="98bdb-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="98bdb-133">죄송합니다. 일부 CDN 공급자에게 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="98bdb-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="98bdb-134">여기에서 상태 업데이트를 다시 확인하세요. 예상 해결 시간 이후에도 문제가 지속되는 경우 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="98bdb-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="98bdb-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98bdb-135">Next steps</span></span>

- [<span data-ttu-id="98bdb-136">Azure 리소스 상태 개요 읽기</span><span class="sxs-lookup"><span data-stu-id="98bdb-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="98bdb-137">CDN 압축 관련 문제 해결</span><span class="sxs-lookup"><span data-stu-id="98bdb-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="98bdb-138">404 오류 관련 문제 해결</span><span class="sxs-lookup"><span data-stu-id="98bdb-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)