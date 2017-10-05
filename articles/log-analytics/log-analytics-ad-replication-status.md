---
title: "Azure Log Analytics를 사용하여 Active Directory 복제 상태 모니터링 | Microsoft Docs"
description: "Active Directory 복제 상태 솔루션 팩은 정기적으로 모든 복제 오류에 대한 Active Directory 환경을 모니터링하고 OMS 대시보드에서 결과를 보고합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfe52ef5d9d09ffe179faaf6ffbd90ef964fbda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a><span data-ttu-id="e3add-103">Log Analytics를 사용하여 Active Directory 복제 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="e3add-103">Monitor Active Directory replication status with Log Analytics</span></span>

![AD 복제 상태 기호](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

<span data-ttu-id="e3add-105">Active Directory는 엔터프라이즈 IT 환경의 핵심 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-105">Active Directory is a key component of an enterprise IT environment.</span></span> <span data-ttu-id="e3add-106">고가용성 및 고성능을 보장하기 위해 각 도메인 컨트롤러에 Active Directory 데이터베이스의 자체 복사본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-106">To ensure high availability and high performance, each domain controller has its own copy of the Active Directory database.</span></span> <span data-ttu-id="e3add-107">도메인 컨트롤러는 변경 내용을 엔터프라이즈 전체에 전파하기 위해 서로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-107">Domain controllers replicate with each other in order to propagate changes across the enterprise.</span></span> <span data-ttu-id="e3add-108">이 복제 프로세스의 오류는 엔터프라이즈에서 다양한 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-108">Failures in this replication process can cause a variety of problems across the enterprise.</span></span>

<span data-ttu-id="e3add-109">AD 복제 상태 솔루션 팩은 정기적으로 모든 복제 오류에 대한 Active Directory 환경을 모니터링하고 OMS 대시보드에서 결과를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-109">The AD Replication Status solution pack regularly monitors your Active Directory environment for any replication failures and reports the results on your OMS dashboard.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="e3add-110">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="e3add-110">Installing and configuring the solution</span></span>
<span data-ttu-id="e3add-111">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-111">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="e3add-112">평가할 도메인의 구성원인 도메인 컨트롤러에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-112">You must install agents on domain controllers that are members of the domain to be evaluated.</span></span> <span data-ttu-id="e3add-113">또는 구성원 서버에 에이전트를 설치하고 OMS에 AD 복제 데이터를 보내도록 에이전트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-113">Or, you must install agents on member servers and configure the agents to send AD replication data to OMS.</span></span> <span data-ttu-id="e3add-114">Windows 컴퓨터를 OMS에 직접 연결하는 방법을 알아보려면 [Log Analytics에 Windows 컴퓨터 연결](log-analytics-windows-agents.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3add-114">To understand how to connect Windows computers to OMS, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="e3add-115">도메인 컨트롤러가 이미 OMS에 연결하려는 기존 System Center Operations Manager 환경의 일부인 경우 [Log Analytics에 Operations Manager 연결](log-analytics-om-agents.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3add-115">If your domain controller is already part of an existing System Center Operations Manager environment that you want to connect to OMS, see [Connect Operations Manager to Log Analytics](log-analytics-om-agents.md).</span></span>
* <span data-ttu-id="e3add-116">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에 설명된 프로세스를 사용하여 OMS 작업 영역에 Active Directory 복제 상태 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-116">Add the Active Directory Replication Status solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="e3add-117">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-117">There is no further configuration required.</span></span>

## <a name="ad-replication-status-data-collection-details"></a><span data-ttu-id="e3add-118">AD 복제 상태 데이터 컬렉션 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e3add-118">AD Replication Status data collection details</span></span>
<span data-ttu-id="e3add-119">다음 표에서는 데이터 수집 방법 및 AD 복제 상태에 대해 데이터가 수집되는 방식에 대한 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-119">The following table shows data collection methods and other details about how data is collected for AD Replication Status.</span></span>

| <span data-ttu-id="e3add-120">플랫폼</span><span class="sxs-lookup"><span data-stu-id="e3add-120">platform</span></span> | <span data-ttu-id="e3add-121">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="e3add-121">Direct Agent</span></span> | <span data-ttu-id="e3add-122">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="e3add-122">SCOM agent</span></span> | <span data-ttu-id="e3add-123">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="e3add-123">Azure Storage</span></span> | <span data-ttu-id="e3add-124">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="e3add-124">SCOM required?</span></span> | <span data-ttu-id="e3add-125">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="e3add-125">SCOM agent data sent via management group</span></span> | <span data-ttu-id="e3add-126">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="e3add-126">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e3add-127">Windows</span><span class="sxs-lookup"><span data-stu-id="e3add-127">Windows</span></span> |<span data-ttu-id="e3add-128">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e3add-128">&#8226;</span></span> |<span data-ttu-id="e3add-129">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e3add-129">&#8226;</span></span> |  |  |<span data-ttu-id="e3add-130">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e3add-130">&#8226;</span></span> |<span data-ttu-id="e3add-131">5일마다</span><span class="sxs-lookup"><span data-stu-id="e3add-131">every five days</span></span> |

## <a name="optionally-enable-a-non-domain-controller-to-send-ad-data-to-oms"></a><span data-ttu-id="e3add-132">필요에 따라 AD 데이터를 OMS에 전송하도록 비 도메인 컨트롤러 활성화</span><span class="sxs-lookup"><span data-stu-id="e3add-132">Optionally, enable a non-domain controller to send AD data to OMS</span></span>
<span data-ttu-id="e3add-133">OMS에 도메인 컨트롤러를 직접 연결하지 않으려면 도메인에서 OMS에 연결된 다른 컴퓨터를 사용하여 AD 복제 상태 솔루션 팩에 대한 데이터를 수집하고 데이터를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-133">If you don't want to connect any of your domain controllers directly to OMS, you can use any other OMS-connected computer in your domain to collect data for the AD Replication Status solution pack and have it send the data.</span></span>

### <a name="to-enable-a-non-domain-controller-to-send-ad-data-to-oms"></a><span data-ttu-id="e3add-134">AD 데이터를 OMS에 전송하도록 비 도메인 컨트롤러 활성화하기</span><span class="sxs-lookup"><span data-stu-id="e3add-134">To enable a non-domain controller to send AD data to OMS</span></span>
1. <span data-ttu-id="e3add-135">AD 복제 상태 솔루션을 사용하여 컴퓨터가 모니터링하려는 도메인의 구성원인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-135">Verify that the computer is a member of the domain that you wish to monitor using the AD Replication Status solution.</span></span>
2. <span data-ttu-id="e3add-136">연결되어 있지 않으면 [OMS에 Windows 컴퓨터를 연결](log-analytics-windows-agents.md)하거나 [기존 Operations Manager 환경을 사용하여 OMS에 연결](log-analytics-om-agents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-136">[Connect the Windows computer to OMS](log-analytics-windows-agents.md) or [connect it using your existing Operations Manager environment to OMS](log-analytics-om-agents.md), if it is not already connected.</span></span>
3. <span data-ttu-id="e3add-137">해당 컴퓨터에서 다음 레지스트리 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-137">On that computer, set the following registry key:</span></span>

   * <span data-ttu-id="e3add-138">키: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span><span class="sxs-lookup"><span data-stu-id="e3add-138">Key: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span></span>
   * <span data-ttu-id="e3add-139">값: **IsTarget**</span><span class="sxs-lookup"><span data-stu-id="e3add-139">Value: **IsTarget**</span></span>
   * <span data-ttu-id="e3add-140">값 데이터: **true**</span><span class="sxs-lookup"><span data-stu-id="e3add-140">Value Data: **true**</span></span>

   > [!NOTE]
   > <span data-ttu-id="e3add-141">이러한 변경 내용은 Microsoft Monitoring Agent 서비스(HealthService.exe)를 다시 시작할 때까지 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-141">These changes do not take effect until your restart the Microsoft Monitoring Agent service (HealthService.exe).</span></span>
   >
   >

## <a name="understanding-replication-errors"></a><span data-ttu-id="e3add-142">복제 오류 이해</span><span class="sxs-lookup"><span data-stu-id="e3add-142">Understanding replication errors</span></span>
<span data-ttu-id="e3add-143">AD 복제 상태 데이터를 OMS에 전송하면 현재 복제 오류 수를 나타내는 OMS 대시보드에 다음 이미지와 유사한 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-143">Once you have AD replication status data sent to OMS, you see a tile similar to the following image on the OMS dashboard indicating how many replication errors you currently have.</span></span>  
![AD 복제 상태 타일](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

<span data-ttu-id="e3add-145">**중요 복제 오류**는 Active Directory 포리스트에 대한 [삭제 표식 수명](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx)의 75% 이상인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-145">**Critical Replication Errors** are errors that are at or above 75% of the [tombstone lifetime](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) for your Active Directory forest.</span></span>

<span data-ttu-id="e3add-146">타일을 클릭하면 오류에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-146">When you click the tile, you can view more information about the errors.</span></span>
<span data-ttu-id="e3add-147">![AD 복제 상태 대시보드](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span><span class="sxs-lookup"><span data-stu-id="e3add-147">![AD Replication Status dashboard](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span></span>

### <a name="destination-server-status-and-source-server-status"></a><span data-ttu-id="e3add-148">대상 서버 상태 및 원본 서버 상태</span><span class="sxs-lookup"><span data-stu-id="e3add-148">Destination Server Status and Source Server Status</span></span>
<span data-ttu-id="e3add-149">이러한 열에서 복제 오류가 발생하는 대상 서버와 원본 서버의 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-149">These columns show the status of destination servers and source servers that are experiencing replication errors.</span></span> <span data-ttu-id="e3add-150">각 도메인 컨트롤러 이름 다음의 숫자는 해당 도메인 컨트롤러의 복제 오류 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-150">The number after each domain controller name indicates the number of replication errors on that domain controller.</span></span>

<span data-ttu-id="e3add-151">일부 문제는 원본 서버 관점에서 해결하기 쉽고 일부는 대상 서버 관점에서 해결하기 쉽기 때문에 대상 서버와 원본 서버에 대한 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-151">The errors for both destination servers and source servers are shown because some problems are easier to troubleshoot from the source server perspective and others from the destination server perspective.</span></span>

<span data-ttu-id="e3add-152">이 예제에서는 많은 대상 서버가 거의 동일한 오류 수를 가진 것을 볼 수 있지만 다른 서버보다 더 많은 오류를 가진 하나의 원본 서버(ADDC35)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-152">In this example, you can see that many destination servers have roughly the same number of errors, but there's one source server (ADDC35) that has many more errors than all the others.</span></span> <span data-ttu-id="e3add-153">데이터를 해당 복제 파트너에 전송하는 데 실패하는 ADDC35에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-153">It's likely that there is some problem on ADDC35 that is causing it to fail to send data to its replication partners.</span></span> <span data-ttu-id="e3add-154">ADDC35의 문제를 해결하면 대상 서버 영역에 나타나는 많은 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-154">Fixing the problems on ADDC35 might resolve many of the errors that appear in the destination server area.</span></span>

### <a name="replication-error-types"></a><span data-ttu-id="e3add-155">복제 오류 유형</span><span class="sxs-lookup"><span data-stu-id="e3add-155">Replication Error Types</span></span>
<span data-ttu-id="e3add-156">이 영역에서 기업 전체에서 발견된 오류 유형에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-156">This area gives you information about the types of errors detected throughout your enterprise.</span></span> <span data-ttu-id="e3add-157">각 오류에는 오류의 근본 원인을 확인하는 데 도움이 되는 고유한 숫자 코드와 메시지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-157">Each error has a unique numerical code and a message that can help you determine the root cause of the error.</span></span>

<span data-ttu-id="e3add-158">맨 왼쪽 도넛을 통해 사용자 환경에서 더 자주 나타나고 덜 자주 나타나는 오류를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-158">The donut at the top gives you an idea of which errors appear more and less frequently in your environment.</span></span>

<span data-ttu-id="e3add-159">여러 도메인 컨트롤러가 동일한 복제 오류를 경험하는 경우를 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-159">It shows you when multiple domain controllers experience the same replication error.</span></span> <span data-ttu-id="e3add-160">이 경우 한 도메인 컨트롤러에서 솔루션을 검색하거나 식별한 다음 동일한 오류에 영향을 받는 다른 도메인 컨트롤러에 이를 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-160">In this case, you may be able to discover or identify a solution on one domain controller, then repeat it on other domain controllers affected by the same error.</span></span>

### <a name="tombstone-lifetime"></a><span data-ttu-id="e3add-161">삭제 표시 수명</span><span class="sxs-lookup"><span data-stu-id="e3add-161">Tombstone Lifetime</span></span>
<span data-ttu-id="e3add-162">삭제 표시 수명은 삭제된 개체가 삭제 표시로 표시되는 기간을 결정하고 Active Directory 데이터베이스에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-162">The tombstone lifetime determines how long a deleted object, referred to as a tombstone, is retained in the Active Directory database.</span></span> <span data-ttu-id="e3add-163">삭제된 개체가 삭제 표시 수명을 넘기는 경우 가비지 수집 프로세스가 Active Directory 데이터베이스에서 해당 개체를 자동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-163">When a deleted object passes the tombstone lifetime, a garbage collection process automatically removes it from the Active Directory database.</span></span>

<span data-ttu-id="e3add-164">최신 버전의 Windows에 대한 기본 삭제 표시 수명은 180일이지만 이전 버전에서는 60일이었으며 Active Directory 관리자가 명시적으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-164">The default tombstone lifetime is 180 days for most recent versions of Windows, but it was 60 days on older versions, and it can be changed explicitly by an Active Directory administrator.</span></span>

<span data-ttu-id="e3add-165">삭제 표식 수명에 도달하는 중이거나 삭제 표식 수명이 지난 복제 오류가 있는지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-165">It's important to know if you're having replication errors that are approaching or are past the tombstone lifetime.</span></span> <span data-ttu-id="e3add-166">두 개의 도메인 컨트롤러가 삭제 표식 수명이 지난 것을 유지하는 복제 오류를 경험하는 경우 기본 복제 오류를 수정하더라도 이러한 두 도메인 컨트롤러 간의 복제가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-166">If two domain controllers experience a replication error that persists past the tombstone lifetime, replication is disabled between those two domain controllers, even if the underlying replication error is fixed.</span></span>

<span data-ttu-id="e3add-167">삭제 표식 수명 영역에서 비활성화된 복제에 문제가 발생할 수 있는 위치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-167">The Tombstone Lifetime area helps you identify places where disabled replication is in danger of happening.</span></span> <span data-ttu-id="e3add-168">**100% TSL 이상** 범주의 각 오류는 적어도 포리스트의 삭제 표시 수명 동안 해당 원본 및 대상 서버 간 복제되지 않은 파티션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-168">Each error in the **Over 100% TSL** category represents a partition that has not replicated between its source and destination server for at least the tombstone lifetime for the forest.</span></span>

<span data-ttu-id="e3add-169">이 상황에서는 단순히 복제 오류를 수정하는 것으로 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-169">In this situation, simply fixing the replication error will not be enough.</span></span> <span data-ttu-id="e3add-170">최소한 복제를 다시 시작하기 전에 느린 개체를 수동으로 식별하도록 조사하고 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-170">At a minimum, you need to manually investigate to identify and clean up lingering objects before you can restart replication.</span></span> <span data-ttu-id="e3add-171">도메인 컨트롤러의 역할 해제를 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-171">You may even need to decommission a domain controller.</span></span>

<span data-ttu-id="e3add-172">삭제 표식 수명이 지난 것을 유지하는 모든 복제 오류를 식별하는 것 외에도 **50-75% TSL** 또는 **75-100% TSL** 범주로 떨어지는 모든 오류에도 주의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-172">In addition to identifying any replication errors that have persisted past the tombstone lifetime, you also want to pay attention to any errors falling into the **50-75% TSL** or **75-100% TSL** categories.</span></span>

<span data-ttu-id="e3add-173">이는 명확하게 느리고 일시적이 아닌 오류이므로 이 오류를 해결하도록 사용자의 개입이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-173">These are errors that are clearly lingering, not transient, so they likely need your intervention to resolve.</span></span> <span data-ttu-id="e3add-174">좋은 소식은 아직 삭제 표시 수명에 도달하지 않았다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-174">The good news is that they have not yet reached the tombstone lifetime.</span></span> <span data-ttu-id="e3add-175">삭제 표시 수명에 도달하기 *전에* 이 문제를 신속하게 해결하는 경우 최소한의 수동 개입으로 복제를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-175">If you fix these problems promptly and *before* they reach the tombstone lifetime, replication can restart with minimal manual intervention.</span></span>

<span data-ttu-id="e3add-176">앞에서 설명한 대로 AD 복제 상태 솔루션에 대한 대시보드 타일은 사용자 환경에서 *중요* 복제 오류 수를 표시하며 삭제 표시 수명의 75% 이상인 오류로 정의됩니다(TSL의 100%를 넘는 오류 포함).</span><span class="sxs-lookup"><span data-stu-id="e3add-176">As noted earlier, the dashboard tile for the AD Replication Status solution shows the number of *critical* replication errors in your environment, which is defined as errors that are over 75% of tombstone lifetime (including errors that are over 100% of TSL).</span></span> <span data-ttu-id="e3add-177">이 값을 0으로 유지하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-177">Strive to keep this number at 0.</span></span>

> [!NOTE]
> <span data-ttu-id="e3add-178">모든 삭제 표시 수명 백분율 계산은 Active Directory 포리스트에 대한 실제 삭제 표시 수명을 기준으로 하므로 삭제 표시 수명 값을 사용자 지정했더라도 해당 백분율이 정확하다는 것을 신뢰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-178">All the tombstone lifetime percentage calculations are based on the actual tombstone lifetime for your Active Directory forest, so you can trust that those percentages are accurate, even if you have a custom tombstone lifetime value set.</span></span>
>
>

### <a name="ad-replication-status-details"></a><span data-ttu-id="e3add-179">AD 복제 상태 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e3add-179">AD Replication status details</span></span>
<span data-ttu-id="e3add-180">목록 중 하나에 있는 항목을 클릭하면 로그 검색을 사용한 추가 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-180">When you click any item in one of the lists, you see additional details about it using Log Search.</span></span> <span data-ttu-id="e3add-181">결과는 해당 항목과 관련된 오류만 표시하도록 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-181">The results are filtered to show only the errors related to that item.</span></span> <span data-ttu-id="e3add-182">예를 들어 **대상 서버 상태(ADDC02)** 아래에 나열된 첫 번째 도메인 컨트롤러를 클릭하면 대상 서버로 나열된 해당 도메인 컨트롤러와 함께 오류를 보여 주는 필터링된 검색 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-182">For example, if you click on the first domain controller listed under **Destination Server Status (ADDC02)**, you see search results filtered to show errors with that domain controller listed as the destination server:</span></span>

![검색 결과에서 AD 복제 상태 오류](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

<span data-ttu-id="e3add-184">여기에서 추가로 필터링하고 검색 쿼리 등을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-184">From here, you can filter further, modify the search query, and so on.</span></span> <span data-ttu-id="e3add-185">로그 검색 사용에 대한 자세한 내용은 [로그 검색](log-analytics-log-searches.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3add-185">For more information about using the Log Search, see [Log searches](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="e3add-186">**HelpLink** 필드는 해당 특정 오류에 대한 추가 세부 정보로 TechNet 페이지의 URL을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-186">The **HelpLink** field shows the URL of a TechNet page with additional details about that specific error.</span></span> <span data-ttu-id="e3add-187">이 링크를 브라우저 창에 복사하여 붙여넣고 문제 해결 및 오류 해결에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-187">You can copy and paste this link into your browser window to see information about troubleshooting and fixing the error.</span></span>

<span data-ttu-id="e3add-188">**내보내기** 를 클릭하여 결과를 Excel로 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-188">You can also click **Export** to export the results to Excel.</span></span> <span data-ttu-id="e3add-189">데이터 내보내기를 통해 원하는 어떤 방식으로든 복제 오류 데이터를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-189">Exporting the data can help you visualize replication error data in any way you'd like.</span></span>

![Excel에서 내보낸 AD 복제 상태 오류](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a><span data-ttu-id="e3add-191">AD 복제 상태 FAQ</span><span class="sxs-lookup"><span data-stu-id="e3add-191">AD Replication Status FAQ</span></span>
<span data-ttu-id="e3add-192">**Q: AD 복제 상태 데이터는 얼마나 자주 업데이트되나요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-192">**Q: How often is AD replication status data updated?**</span></span>
<span data-ttu-id="e3add-193">A: 정보는 5일마다 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-193">A: The information is updated every five days.</span></span>

<span data-ttu-id="e3add-194">**Q: 이 데이터가 업데이트되는 빈도를 구성하는 방법이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-194">**Q: Is there a way to configure how often this data is updated?**</span></span>
<span data-ttu-id="e3add-195">A: 지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-195">A: Not at this time.</span></span>

<span data-ttu-id="e3add-196">**Q: 복제 상태를 보려면 내 OMS 작업 영역에 모든 도메인 컨트롤러를 추가해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-196">**Q: Do I need to add all of my domain controllers to my OMS workspace in order to see replication status?**</span></span>
<span data-ttu-id="e3add-197">A: 아니요, 단일 도메인 컨트롤러만 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-197">A: No, only a single domain controller must be added.</span></span> <span data-ttu-id="e3add-198">OMS 작업 영역에 도메인 컨트롤러가 여러 개 있는 경우 모든 데이터는 OMS에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-198">If you have multiple domain controllers in your OMS workspace, data from all of them is sent to OMS.</span></span>

<span data-ttu-id="e3add-199">**Q: 내 OMS 작업 영역에 도메인 컨트롤러를 추가하고 싶지 않습니다. 여전히 AD 복제 상태 솔루션을 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e3add-199">**Q: I don't want to add any domain controllers to my OMS workspace. Can I still use the AD Replication Status solution?**</span></span>
<span data-ttu-id="e3add-200">A: 예.</span><span class="sxs-lookup"><span data-stu-id="e3add-200">A: Yes.</span></span> <span data-ttu-id="e3add-201">이 기능을 활성화하도록 레지스트리 키의 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-201">You can set the value of a registry key to enable it.</span></span> <span data-ttu-id="e3add-202">[AD 데이터를 OMS에 전송하도록 비 도메인 컨트롤러 활성화하기](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3add-202">See [To enable a non-domain controller to send AD data to OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

<span data-ttu-id="e3add-203">**Q: 데이터 수집을 수행하는 프로세스의 이름은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-203">**Q: What is the name of the process that does the data collection?**</span></span>
<span data-ttu-id="e3add-204">A: AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="e3add-204">A: AdvisorAssessment.exe</span></span>

<span data-ttu-id="e3add-205">**Q: 데이터를 수집하려면 시간이 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-205">**Q: How long does it take for data to be collected?**</span></span>
<span data-ttu-id="e3add-206">A: 데이터 수집 시간은 Active Directory 환경의 크기에 따라 달라지지만 일반적으로 약 15분 미만이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-206">A: Data collection time depends on the size of the Active Directory environment, but usually takes less than 15 minutes.</span></span>

<span data-ttu-id="e3add-207">**Q: 어떤 유형의 데이터를 수집하나요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-207">**Q: What type of data is collected?**</span></span>
<span data-ttu-id="e3add-208">A: 복제 정보는 LDAP를 통해 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-208">A: Replication information is collected via LDAP.</span></span>

<span data-ttu-id="e3add-209">**Q: 데이터를 수집하는 경우 구성하는 방법이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="e3add-209">**Q: Is there a way to configure when data is collected?**</span></span>
<span data-ttu-id="e3add-210">A: 지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-210">A: Not at this time.</span></span>

<span data-ttu-id="e3add-211">**Q: 데이터를 수집하려면 어떤 권한이 필요합니까?**</span><span class="sxs-lookup"><span data-stu-id="e3add-211">**Q: What permissions do I need to collect data?**</span></span>
<span data-ttu-id="e3add-212">A: Active Directory에 대한 일반 사용자 권한으로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-212">A: Normal user permissions to Active Directory are sufficient.</span></span>

## <a name="troubleshoot-data-collection-problems"></a><span data-ttu-id="e3add-213">데이터 수집 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e3add-213">Troubleshoot data collection problems</span></span>
<span data-ttu-id="e3add-214">데이터를 수집하기 위해 AD 복제 상태 솔루션 팩에 OMS 작업 영역에 연결될 하나 이상의 도메인 컨트롤러가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-214">In order to collect data, the AD Replication Status solution pack requires at least one domain controller to be connected to your OMS workspace.</span></span> <span data-ttu-id="e3add-215">도메인 컨트롤러에 연결할 때까지 **데이터가 여전히 수집되고 있다고** 표시하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-215">Until you connect a domain controller, a message appears indicating that **data is still being collected**.</span></span>

<span data-ttu-id="e3add-216">도메인 컨트롤러 중 하나를 연결하는 데 도움이 필요한 경우 [Log Analytics에 Windows 컴퓨터 연결](log-analytics-windows-agents.md)에서 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-216">If you need assistance connecting one of your domain controllers, you can view documentation at [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="e3add-217">또는 도메인 컨트롤러가 이미 기존 System Center Operations Manager 환경에 연결된 경우 [Log Analytics에 System Center Operations Manager 연결](log-analytics-om-agents.md)에서 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-217">Alternatively, if your domain controller is already connected to an existing System Center Operations Manager environment, you can view documentation at [Connect System Center Operations Manager to Log Analytics](log-analytics-om-agents.md).</span></span>

<span data-ttu-id="e3add-218">OMS 또는 SCOM에 도메인 컨트롤러를 직접 연결하지 않으려면 [AD 데이터를 OMS에 전송하도록 비 도메인 컨트롤러 활성화하기](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3add-218">If you don't want to connect any of your domain controllers directly to OMS or to SCOM, see [To enable a non-domain controller to send AD data to OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3add-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3add-219">Next steps</span></span>
* <span data-ttu-id="e3add-220">[Log Analytics의 로그 검색](log-analytics-log-searches.md) 을 사용하여 자세한 Active Directory 복제 상태 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e3add-220">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Active Directory Replication status data.</span></span>
