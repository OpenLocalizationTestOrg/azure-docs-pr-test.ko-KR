---
title: "StorSimple 장치 관리자를 통해 지원 티켓 로그 | Microsoft Docs"
description: "StorSimple 장치 관리자 진단 기능 및 이 기능을 사용하여 StorSimple 가상 배열 문제를 해결하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a0c394df-957b-49b3-a283-38824f8847fd
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 658afbc178814389fefd7941e2ca030741bd08e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-log-a-support-request-for-the-storsimple-virtual-array"></a><span data-ttu-id="55932-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열에 대한 지원 요청 기록</span><span class="sxs-lookup"><span data-stu-id="55932-103">Use the StorSimple Device Manager service to log a Support request for the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="55932-104">개요</span><span class="sxs-lookup"><span data-stu-id="55932-104">Overview</span></span>

<span data-ttu-id="55932-105">StorSimple 장치 관리자는 서비스 요약 블레이드 내에서 **새로운 지원 요청을 기록**하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-105">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="55932-106">이 문서에서는 새로운 지원 요청을 기록하고 포털 내에서 해당 수명 주기를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-106">This article explains how you can log a new support request and manage its lifecycle from within the portal.</span></span>

## <a name="new-support-request"></a><span data-ttu-id="55932-107">새 지원 요청</span><span class="sxs-lookup"><span data-stu-id="55932-107">New support request</span></span>

<span data-ttu-id="55932-108">[지원 계획](https://azure.microsoft.com/support/plans/)에 따라 StorSimple 장치 관리자 서비스 요약 블레이드에서 직접 StorSimple 가상 배열 문제에 대한 지원 티켓을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55932-108">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple Virtual array directly from the StorSimple Device Manager service summary blade.</span></span>

#### <a name="to-log-a-new-request"></a><span data-ttu-id="55932-109">새 요청을 기록하려면</span><span class="sxs-lookup"><span data-stu-id="55932-109">To log a new request</span></span>

1. <span data-ttu-id="55932-110">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-110">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="55932-111">서비스 요약 블레이드 설정에서 **지원 + 문제 해결** 섹션으로 이동한 다음 **새 지원 요청**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-111">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
   
    ![새 지원 요청](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket1.png)

2. <span data-ttu-id="55932-113">**기본** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-113">In the **Basics** blade, do the following:</span></span>

    1. <span data-ttu-id="55932-114">**문제점 유형** 드롭다운 목록에서 **기술**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-114">From the **Issue type** dropdown list, select **Technical**.</span></span> 
    
    2. <span data-ttu-id="55932-115">현재 **구독**, **서비스** 유형 및 **리소스**(StorSimple 장치 관리자 서비스)가 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="55932-115">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 

    3. <span data-ttu-id="55932-116">문제가 발생하는 서비스에 등록된 하나 이상의 장치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-116">Specify one or more devices registered to your service that are experiencing issues.</span></span>

    4. <span data-ttu-id="55932-117">구독과 관련된 여러 계획이 있는 경우 적합한 **지원 계획**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-117">Choose an appropriate **support plan** if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="55932-118">기술 지원을 사용하도록 설정하기 위해 유료 지원 계획이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-118">You need a paid support plan to enable Technical Support.</span></span>

3. <span data-ttu-id="55932-119">**2단계**에서 **심각도**를 선택하고 문제가 배열 또는 StorSimple 장치 관리자 서비스에 관련되어 있는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-119">In **Step 2**, choose the **Severity** and specify if the issue is related to the array or the StorSimple Device Manager service.</span></span> <span data-ttu-id="55932-120">또한 이 문제의 **범주**를 선택하고 문제에 대한 추가 **세부 정보**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-120">Also, choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
   
    ![새 지원 요청](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket2.png)

4. <span data-ttu-id="55932-122">**3단계**에서 연락처 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-122">In **Step 3**, provide your contact information.</span></span> <span data-ttu-id="55932-123">Microsoft 기술 지원 서비스는 이 정보를 사용하여 사용자에게 추가 정보, 진단 및 솔루션을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="55932-123">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
   
    ![새 지원 요청](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket3.png)

## <a name="manage-a-support-request"></a><span data-ttu-id="55932-125">지원 요청 관리</span><span class="sxs-lookup"><span data-stu-id="55932-125">Manage a support request</span></span>

<span data-ttu-id="55932-126">지원 티켓을 만든 후에는 포털 내에서 티켓의 수명 주기를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55932-126">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="55932-127">지원 요청을 관리하려면</span><span class="sxs-lookup"><span data-stu-id="55932-127">To manage your support requests</span></span>

<span data-ttu-id="55932-128">도움말 및 지원 페이지로 이동하려면 **찾아보기 > 도움말 + 지원**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55932-128">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

![지원 요청 관리](./media/storsimple-virtual-array-log-support-ticket/manage-support-tickets.png)

## <a name="next-steps"></a><span data-ttu-id="55932-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55932-130">Next steps</span></span>

<span data-ttu-id="55932-131">[StorSimple 가상 배열에 관련된 문제를 진단하고 해결](storsimple-virtual-array-diagnose-problems.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="55932-131">Learn how to [diagnose and solve problems related to your StorSimple Virtual array](storsimple-virtual-array-diagnose-problems.md)</span></span>

