---
title: "BizTalk 서비스의 제한에 대 한 aaaLearn | Microsoft Docs"
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="58f1d-105">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="58f1d-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="58f1d-106">Azure BizTalk 서비스 구현 서비스가 두 가지 조건에 따라 제한: 동시 메시지 처리의 메모리 사용량 및 hello 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="58f1d-107">이 항목 hello 조정 임계값을 나열 하 고 조정 상태가 발생 하는 경우 hello 런타임 동작에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="58f1d-108">제한 임계값</span><span class="sxs-lookup"><span data-stu-id="58f1d-108">Throttling Thresholds</span></span>
<span data-ttu-id="58f1d-109">다음 표에 hello 조정 소스 및 임계값 hello:</span><span class="sxs-lookup"><span data-stu-id="58f1d-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="58f1d-110">설명</span><span class="sxs-lookup"><span data-stu-id="58f1d-110">Description</span></span> | <span data-ttu-id="58f1d-111">낮은 임계값</span><span class="sxs-lookup"><span data-stu-id="58f1d-111">Low Threshold</span></span> | <span data-ttu-id="58f1d-112">높은 임계값</span><span class="sxs-lookup"><span data-stu-id="58f1d-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="58f1d-113">메모리</span><span class="sxs-lookup"><span data-stu-id="58f1d-113">Memory</span></span> |<span data-ttu-id="58f1d-114">사용 가능한 총 시스템/PageFileBytes 백분율</span><span class="sxs-lookup"><span data-stu-id="58f1d-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="58f1d-115">사용 가능한 총 PageFileBytes는 약 2 배 hello RAM hello 시스템의입니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="58f1d-116">60%</span><span class="sxs-lookup"><span data-stu-id="58f1d-116">60%</span></span> |<span data-ttu-id="58f1d-117">70%</span><span class="sxs-lookup"><span data-stu-id="58f1d-117">70%</span></span> |
| <span data-ttu-id="58f1d-118">메시지 처리</span><span class="sxs-lookup"><span data-stu-id="58f1d-118">Message Processing</span></span> |<span data-ttu-id="58f1d-119">동시 메시지 처리 수</span><span class="sxs-lookup"><span data-stu-id="58f1d-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="58f1d-120">40 * 코어 수</span><span class="sxs-lookup"><span data-stu-id="58f1d-120">40 * number of cores</span></span> |<span data-ttu-id="58f1d-121">100 * 코어 수</span><span class="sxs-lookup"><span data-stu-id="58f1d-121">100 * number of cores</span></span> |

<span data-ttu-id="58f1d-122">높은 임계값에 도달 하면 toothrottle Azure BizTalk 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="58f1d-123">Hello 낮은 임계값에 도달 하는 경우 중지를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="58f1d-124">예를 들어 서비스에서 65% 시스템 메모리를 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="58f1d-125">이 경우 hello 서비스 스로틀 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="58f1d-126">그러나 서비스가 70%의 시스템 메모리를 사용하기 시작하면 상황이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="58f1d-127">이 경우 hello 서비스 스로틀 및 toothrottle hello 서비스 60% (낮은 임계값) 시스템 메모리를 사용 하 여 때까지 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="58f1d-128">Azure BizTalk 서비스 상태 (제한 된 상태 및 일반 상태)을 제한 하는 hello 및 기간을 제한 하는 hello를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="58f1d-129">런타임 동작</span><span class="sxs-lookup"><span data-stu-id="58f1d-129">Runtime Behavior</span></span>
<span data-ttu-id="58f1d-130">Azure BizTalk 서비스 조정 상태가 hello 다음 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="58f1d-131">조정은 역할 인스턴스별로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-131">Throttling is per role instance.</span></span> <span data-ttu-id="58f1d-132">예:</span><span class="sxs-lookup"><span data-stu-id="58f1d-132">For example:</span></span><br/>
  <span data-ttu-id="58f1d-133">RoleInstanceA가 제한 중입니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="58f1d-134">RoleInstanceB는 제한하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="58f1d-135">이런 경우 RoleInstanceB의 메시지가 예상대로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="58f1d-136">RoleInstanceA의 메시지는 무시 되 고 다음 오류가 hello와 함께 실패:</span><span class="sxs-lookup"><span data-stu-id="58f1d-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="58f1d-137">
  **서버가 사용 중입니다. 나중에 다시 시도하세요.**</span><span class="sxs-lookup"><span data-stu-id="58f1d-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="58f1d-138">어떤 끌어오기 원본도 메시지를 폴링하거나 다운로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="58f1d-139">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-139">For example:</span></span><br/>
  <span data-ttu-id="58f1d-140">파이프라인이 외부 FTP 원본에서 메시지를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="58f1d-141">조정 상태에 hello 끌어오기를 수행 하는 hello 역할 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="58f1d-142">이 경우 hello 파이프라인 제한 hello 역할 인스턴스가 중지 될 때까지 메시지를 추가로 다운로드를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="58f1d-143">응답은 hello 클라이언트 hello 메시지를 전송할 수 있도록 toohello 클라이언트를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="58f1d-144">Hello 제한 해결 될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="58f1d-145">특히 hello 낮은 임계값에 도달할 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="58f1d-146">중요</span><span class="sxs-lookup"><span data-stu-id="58f1d-146">Important notes</span></span>
* <span data-ttu-id="58f1d-147">제한을 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="58f1d-148">제한 임계값은 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="58f1d-149">제한은 시스템 전체에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="58f1d-150">Azure SQL 데이터베이스 서버 hello 기본 제공 제한에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58f1d-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="58f1d-151">추가 Azure BizTalk 서비스 항목</span><span class="sxs-lookup"><span data-stu-id="58f1d-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="58f1d-152">Hello Azure BizTalk Services SDK 설치</span><span class="sxs-lookup"><span data-stu-id="58f1d-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="58f1d-153">자습서: Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="58f1d-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="58f1d-154">Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까</span><span class="sxs-lookup"><span data-stu-id="58f1d-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="58f1d-155">Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="58f1d-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="58f1d-156">참고 항목</span><span class="sxs-lookup"><span data-stu-id="58f1d-156">See Also</span></span>
* [<span data-ttu-id="58f1d-157">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="58f1d-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="58f1d-158">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="58f1d-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="58f1d-159">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="58f1d-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="58f1d-160">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="58f1d-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="58f1d-161">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="58f1d-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="58f1d-162">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="58f1d-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

