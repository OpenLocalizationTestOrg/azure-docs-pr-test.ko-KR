---
title: "Azure CDN 리소스의 aaaMonitor hello 상태 | Microsoft Docs"
description: "Toomonitor Azure 리소스 상태를 사용 하 여 Azure CDN 리소스의 상태를 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="a5d18-103">Azure CDN 리소스의 hello 상태 모니터</span><span class="sxs-lookup"><span data-stu-id="a5d18-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="a5d18-104">Azure CDN 리소스 상태는 [Azure 리소스 상태](../resource-health/resource-health-overview.md)의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="a5d18-105">Azure 리소스 상태 toomonitor hello CDN 리소스의 상태를 사용 하 여 수 있으며 실행 가능한 지침 tootroubleshoot 문제를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="a5d18-106">Azure CDN 리소스 상태 API 기능 및 글로벌 CDN 배달을의 hello 상태에 대 한 현재만 차지합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="a5d18-107">Azure CDN 리소스 상태는 개별 CDN 끝점을 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="a5d18-108">Azure CDN 리소스 상태 피드 hello 신호를 too15 분까지 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="a5d18-109">어떻게 toofind Azure CDN 리소스 상태</span><span class="sxs-lookup"><span data-stu-id="a5d18-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="a5d18-110">Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="a5d18-111">Hello 클릭 **설정을** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-111">Click hello **Settings** button.</span></span>

    ![설정 단추](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="a5d18-113">*지원 + 문제 해결*에서 **리소스 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN 리소스 상태](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="a5d18-115">Hello에 나열 된 CDN 리소스를 찾을 수도 있습니다 *리소스 상태* hello에 바둑판식으로 배열 *도움말 + 지원* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="a5d18-116">너무에 신속 하 게 가져올 수*도움말 + 지원* hello 원으로 표시를 클릭 하 여 **?**</span><span class="sxs-lookup"><span data-stu-id="a5d18-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="a5d18-117">hello hello 포털의 상단 오른쪽 모서리에.</span><span class="sxs-lookup"><span data-stu-id="a5d18-117">in hello upper right corner of hello portal.</span></span>
>
> ![도움말 + 지원](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="a5d18-119">Azure CDN 관련 메시지</span><span class="sxs-lookup"><span data-stu-id="a5d18-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="a5d18-120">아래 상태 관련된 tooAzure CDN 리소스 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="a5d18-121">Message</span><span class="sxs-lookup"><span data-stu-id="a5d18-121">Message</span></span> | <span data-ttu-id="a5d18-122">권장 작업</span><span class="sxs-lookup"><span data-stu-id="a5d18-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="a5d18-123">하나 이상의 CDN 끝점을 중지, 제거 또는 잘못 구성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="a5d18-124">하나 이상의 CDN 끝점을 중지, 제거 또는 잘못 구성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="a5d18-125">죄송 합니다. hello CDN 관리 서비스를 현재 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="a5d18-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="a5d18-126">상태 업데이트;에 대 한 다시 여기를 선택 합니다. Hello 해결 시간 후 문제가 계속 되 면 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="a5d18-127">죄송합니다. CDN 끝점이 일부 CDN 공급자와 관련하여 진행 중인 문제로 인해 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="a5d18-128">상태 업데이트;에 대 한 다시 여기를 선택 합니다. 문제 해결 도구 toolearn hello를 사용 하 여 어떻게 tootest 원점과 CDN 끝점; Hello 해결 시간 후 문제가 계속 되 면 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="a5d18-129">죄송합니다. CDN 끝점 구성 변경 사항에 전파 지연이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="a5d18-130">상태 업데이트;에 대 한 다시 여기를 선택 합니다. 지원에 문의 구성 변경 내용을 hello 예상 시간에 완전히 전파 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="a5d18-131">죄송 합니다 문제로 hello 보조 포털을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="a5d18-132">상태 업데이트;에 대 한 다시 여기를 선택 합니다. Hello 해결 시간 후 문제가 계속 되 면 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="a5d18-133">죄송합니다. 일부 CDN 공급자에게 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="a5d18-134">상태 업데이트;에 대 한 다시 여기를 선택 합니다. Hello 해결 시간 후 문제가 계속 되 면 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5d18-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a5d18-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5d18-135">Next steps</span></span>

- [<span data-ttu-id="a5d18-136">Azure 리소스 상태 개요 읽기</span><span class="sxs-lookup"><span data-stu-id="a5d18-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="a5d18-137">CDN 압축 관련 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a5d18-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="a5d18-138">404 오류 관련 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a5d18-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)