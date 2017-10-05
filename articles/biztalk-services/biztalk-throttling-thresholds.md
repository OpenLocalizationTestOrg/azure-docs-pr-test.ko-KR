---
title: "BizTalk 서비스의 제한에 대한 자세한 정보 | Microsoft Docs"
description: "BizTalk 서비스에 대한 제한 임계값 및 결과 런타임 동작에 대해 알아봅니다. 제한은 메모리 사용량 및 메시지 수를 기반으로 합니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="b9103-105">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="b9103-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="b9103-106">Azure BizTalk 서비스는 메모리 사용량과 동시 메시지 처리 수의 두 가지 조건에 따라 서비스 제한을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="b9103-107">이 항목에서는 제한 임계값을 나열하고 제한 조건이 발생할 때의 런타임 동작을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="b9103-108">제한 임계값</span><span class="sxs-lookup"><span data-stu-id="b9103-108">Throttling Thresholds</span></span>
<span data-ttu-id="b9103-109">다음 표에서는 제한 원본 및 임계값을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="b9103-110">설명</span><span class="sxs-lookup"><span data-stu-id="b9103-110">Description</span></span> | <span data-ttu-id="b9103-111">낮은 임계값</span><span class="sxs-lookup"><span data-stu-id="b9103-111">Low Threshold</span></span> | <span data-ttu-id="b9103-112">높은 임계값</span><span class="sxs-lookup"><span data-stu-id="b9103-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b9103-113">메모리</span><span class="sxs-lookup"><span data-stu-id="b9103-113">Memory</span></span> |<span data-ttu-id="b9103-114">사용 가능한 총 시스템/PageFileBytes 백분율</span><span class="sxs-lookup"><span data-stu-id="b9103-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="b9103-115">사용 가능한 총 PageFileBytes는 시스템 RAM의 대략 2배입니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="b9103-116">60%</span><span class="sxs-lookup"><span data-stu-id="b9103-116">60%</span></span> |<span data-ttu-id="b9103-117">70%</span><span class="sxs-lookup"><span data-stu-id="b9103-117">70%</span></span> |
| <span data-ttu-id="b9103-118">메시지 처리</span><span class="sxs-lookup"><span data-stu-id="b9103-118">Message Processing</span></span> |<span data-ttu-id="b9103-119">동시 메시지 처리 수</span><span class="sxs-lookup"><span data-stu-id="b9103-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="b9103-120">40 * 코어 수</span><span class="sxs-lookup"><span data-stu-id="b9103-120">40 * number of cores</span></span> |<span data-ttu-id="b9103-121">100 * 코어 수</span><span class="sxs-lookup"><span data-stu-id="b9103-121">100 * number of cores</span></span> |

<span data-ttu-id="b9103-122">높은 임계값에 도달하면 Azure BizTalk 서비스에서 제한을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="b9103-123">낮은 임계값에 도달하면 제한이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="b9103-124">예를 들어 서비스에서 65% 시스템 메모리를 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="b9103-125">이런 상황에서는 서비스가 제한하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="b9103-126">그러나 서비스가 70%의 시스템 메모리를 사용하기 시작하면 상황이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="b9103-127">서비스가 제한을 시작하여 60%(낮은 임계값)의 시스템 메모리를 사용할 때까지 계속 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="b9103-128">Azure BizTalk 서비스는 제한 상태(일반 상태와 제한된 상태) 및 제한 기간을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="b9103-129">런타임 동작</span><span class="sxs-lookup"><span data-stu-id="b9103-129">Runtime Behavior</span></span>
<span data-ttu-id="b9103-130">Azure BizTalk 서비스가 제한 상태에 들어가면 다음과 같은 상황이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="b9103-131">조정은 역할 인스턴스별로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-131">Throttling is per role instance.</span></span> <span data-ttu-id="b9103-132">예:</span><span class="sxs-lookup"><span data-stu-id="b9103-132">For example:</span></span><br/>
  <span data-ttu-id="b9103-133">RoleInstanceA가 제한 중입니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="b9103-134">RoleInstanceB는 제한하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="b9103-135">이런 경우 RoleInstanceB의 메시지가 예상대로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="b9103-136">RoleInstanceA의 메시지는 취소되고 다음과 같은 오류를 표시하며 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="b9103-137">
  **서버가 사용 중입니다. 나중에 다시 시도하세요.**</span><span class="sxs-lookup"><span data-stu-id="b9103-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="b9103-138">어떤 끌어오기 원본도 메시지를 폴링하거나 다운로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="b9103-139">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-139">For example:</span></span><br/>
  <span data-ttu-id="b9103-140">파이프라인이 외부 FTP 원본에서 메시지를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="b9103-141">끌어오기를 수행하는 역할 인스턴스가 제한 상태로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="b9103-142">이런 경우 역할 인스턴스가 제한을 중지할 때까지 파이프라인에서 추가 메시지 다운로드를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="b9103-143">클라이언트에서 메시지를 다시 제출할 수 있도록 응답이 클라이언트로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="b9103-144">제한이 해결될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="b9103-145">특히 낮은 임계값에 도달할 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="b9103-146">중요</span><span class="sxs-lookup"><span data-stu-id="b9103-146">Important notes</span></span>
* <span data-ttu-id="b9103-147">제한을 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="b9103-148">제한 임계값은 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="b9103-149">제한은 시스템 전체에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="b9103-150">Azure SQL 데이터베이스 서버에는 기본 제공 제한도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9103-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="b9103-151">추가 Azure BizTalk 서비스 항목</span><span class="sxs-lookup"><span data-stu-id="b9103-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="b9103-152">Azure BizTalk 서비스 SDK 설치</span><span class="sxs-lookup"><span data-stu-id="b9103-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="b9103-153">자습서: Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="b9103-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="b9103-154">Azure BizTalk 서비스 SDK로 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="b9103-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="b9103-155">Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="b9103-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="b9103-156">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b9103-156">See Also</span></span>
* [<span data-ttu-id="b9103-157">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="b9103-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="b9103-158">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="b9103-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="b9103-159">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="b9103-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="b9103-160">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="b9103-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="b9103-161">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="b9103-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="b9103-162">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="b9103-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

