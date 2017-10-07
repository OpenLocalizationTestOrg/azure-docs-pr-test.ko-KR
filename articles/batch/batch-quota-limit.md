---
title: "aaaService 할당량 및 Azure 일괄 처리에 대 한 제한을 | Microsoft Docs"
description: "기본 Azure 배치 할당량, 제한 및 제약 조건 및 toorequest 할당량 증가 하는 방법에 대해 알아보기"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="c768a-103">배치 서비스 할당량 및 제한</span><span class="sxs-lookup"><span data-stu-id="c768a-103">Batch service quotas and limits</span></span>

<span data-ttu-id="c768a-104">와 다른 Azure 서비스와 제한 되어 hello 일괄 처리 서비스와 관련 된 특정 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="c768a-105">이러한 제한 중 상당수는 hello 구독 또는 계정 수준에서 Azure에 의해 적용 된 기본 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="c768a-106">이 문서는 그러한 기본값을 설명하고 할당량 증가를 요청하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="c768a-107">배치 워크로드를 디자인하고 강화할 때 이 할당량에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="c768a-108">예를 들어 사용자 풀 hello 대상 지정한 계산 노드 수에 도달 되지 않습니다 수에 도달 했 있습니다 hello 코어 할당량 한도 배치 계정 또는 지역 VM 코어 할당량에 대 한 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="c768a-109">단일 일괄 처리 계정에 여러 개의 일괄 처리 작업을 실행 하거나 hello에 있는 일괄 처리 계정 간에 작업을 배포할 수 있습니다 동일한 구독 있지만 서로 다른 Azure 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="c768a-110">일괄 처리에서 toorun 프로덕션 작업을 하려는 경우에 하나 이상의 hello 기본 위에 hello 할당량 tooincrease를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="c768a-111">Tooraise 할당량을 하려는 경우 온라인 열 수 [고객 지원 요청](#increase-a-quota) 비용 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="c768a-112">할당량은 신용 한도액일 뿐이며 용량을 보장하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="c768a-113">대규모 용량이 필요한 경우 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c768a-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="c768a-114">리소스 할당량</span><span class="sxs-lookup"><span data-stu-id="c768a-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="c768a-115">사용자 구독 모드에서 할당량</span><span class="sxs-lookup"><span data-stu-id="c768a-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="c768a-116">도 풀 할당 모드를 사용 하 여 일괄 처리 계정을**사용자 구독**, Vm 및 저장소 계정 등의 다른 리소스를 일괄 처리, 풀을 만들 때 구독에 직접 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="c768a-117">hello Azure 배치 코어 할당량에는이 모드에서 만든 tooan 계정을 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="c768a-118">대신 지역 계산 코어 및 기타 리소스에 대 한 구독에서 hello 할당량 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="c768a-119">[Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 이러한 할당량에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c768a-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="c768a-120">사용자 구독 모드에서 생성 된 계정에 대 한 리소스 사용량을 계획할 때 (더하기 toocompute 코어)의 일괄 처리 리소스를 다음 참고 hello를 사용 하는 요소가 모든 40 Linux Vm 또는 20 대의 Windows Vm에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="c768a-121">리소스</span><span class="sxs-lookup"><span data-stu-id="c768a-121">Resource</span></span> | <span data-ttu-id="c768a-122">할당량</span><span class="sxs-lookup"><span data-stu-id="c768a-122">Quota</span></span> | <span data-ttu-id="c768a-123">공급자</span><span class="sxs-lookup"><span data-stu-id="c768a-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="c768a-124">저장소 계정 1개</span><span class="sxs-lookup"><span data-stu-id="c768a-124">One storage account</span></span> | <span data-ttu-id="c768a-125">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c768a-125">Storage Accounts</span></span> | <span data-ttu-id="c768a-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="c768a-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="c768a-127">공용 IP 주소 1개</span><span class="sxs-lookup"><span data-stu-id="c768a-127">One public IP address</span></span> | <span data-ttu-id="c768a-128">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="c768a-128">Public IP Addresses</span></span> | <span data-ttu-id="c768a-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="c768a-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="c768a-130">가상 네트워크 1개</span><span class="sxs-lookup"><span data-stu-id="c768a-130">One virtual network</span></span> | <span data-ttu-id="c768a-131">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="c768a-131">Virtual Networks</span></span> | <span data-ttu-id="c768a-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="c768a-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="c768a-133">네트워크 보안 그룹 1개</span><span class="sxs-lookup"><span data-stu-id="c768a-133">One network security group</span></span> | <span data-ttu-id="c768a-134">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="c768a-134">Network Security Groups</span></span> | <span data-ttu-id="c768a-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="c768a-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="c768a-136">가상 컴퓨터 확장 집합 1개</span><span class="sxs-lookup"><span data-stu-id="c768a-136">One virtual machine scale set</span></span> | <span data-ttu-id="c768a-137">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="c768a-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="c768a-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="c768a-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="c768a-139">부하 분산 장치 1개</span><span class="sxs-lookup"><span data-stu-id="c768a-139">One load balancer</span></span> | <span data-ttu-id="c768a-140">부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="c768a-140">Load Balancers</span></span> | <span data-ttu-id="c768a-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="c768a-141">Microsoft.Network</span></span> | 

<span data-ttu-id="c768a-142">국가별 수준이 나 VM 패밀리당 hello 코어 할당량에 따라 toohello VM 크기 설정 배치 풀 또는 풀에 필요한 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="c768a-143">할당량</span><span class="sxs-lookup"><span data-stu-id="c768a-143">Quota</span></span> | <span data-ttu-id="c768a-144">공급자</span><span class="sxs-lookup"><span data-stu-id="c768a-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="c768a-145">총 지역별 코어 수</span><span class="sxs-lookup"><span data-stu-id="c768a-145">Total Regional Cores</span></span> | <span data-ttu-id="c768a-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="c768a-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="c768a-147">…</span><span class="sxs-lookup"><span data-stu-id="c768a-147">…</span></span> <span data-ttu-id="c768a-148">제품군 코어 수</span><span class="sxs-lookup"><span data-stu-id="c768a-148">Family Cores</span></span> | <span data-ttu-id="c768a-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="c768a-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="c768a-150">기타 제한</span><span class="sxs-lookup"><span data-stu-id="c768a-150">Other limits</span></span>
| <span data-ttu-id="c768a-151">**리소스**</span><span class="sxs-lookup"><span data-stu-id="c768a-151">**Resource**</span></span> | <span data-ttu-id="c768a-152">**최대 제한**</span><span class="sxs-lookup"><span data-stu-id="c768a-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="c768a-153">[동시 작업](batch-parallel-node-tasks.md) </span><span class="sxs-lookup"><span data-stu-id="c768a-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="c768a-154">4 x 노드 코어 수</span><span class="sxs-lookup"><span data-stu-id="c768a-154">4 x number of node cores</span></span> |
| <span data-ttu-id="c768a-155">[응용 프로그램](batch-application-packages.md) </span><span class="sxs-lookup"><span data-stu-id="c768a-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="c768a-156">20</span><span class="sxs-lookup"><span data-stu-id="c768a-156">20</span></span> |
| <span data-ttu-id="c768a-157">응용 프로그램당 응용 프로그램 패키지</span><span class="sxs-lookup"><span data-stu-id="c768a-157">Application packages per application</span></span> |<span data-ttu-id="c768a-158">40</span><span class="sxs-lookup"><span data-stu-id="c768a-158">40</span></span> |
| <span data-ttu-id="c768a-159">각 응용 프로그램 패키지 크기</span><span class="sxs-lookup"><span data-stu-id="c768a-159">Application package size (each)</span></span> |<span data-ttu-id="c768a-160">약 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="c768a-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="c768a-161">최대 시작 태스크 크기</span><span class="sxs-lookup"><span data-stu-id="c768a-161">Maximum start task size</span></span> | <span data-ttu-id="c768a-162">32768자<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c768a-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="c768a-163"><sup>1</sup> 최대 블록 Blob 크기에 대한 Azure 저장소 용량 한도</span><span class="sxs-lookup"><span data-stu-id="c768a-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="c768a-164">
<sup>2</sup> 리소스 파일 및 환경 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="c768a-165">배치 할당량 보기</span><span class="sxs-lookup"><span data-stu-id="c768a-165">View Batch quotas</span></span>
<span data-ttu-id="c768a-166">배치 계정 할당량 hello 뷰에서 [Azure 포털][portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="c768a-167">선택 **계정 일괄 처리** hello 포털에서 다음에 관심이 hello 일괄 처리 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="c768a-168">선택 **속성** hello 일괄 처리 계정 메뉴 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="c768a-169">hello를 표시 하는 hello 속성 블레이드 **할당량** toohello 일괄 처리 계정에 현재 적용</span><span class="sxs-lookup"><span data-stu-id="c768a-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![배치 계정 할당량][account_quotas]

<span data-ttu-id="c768a-171">사용자 구독 모드에서 만든 일괄 처리 계정에 대 한 보기 hello 관련 hello Azure 포털의에서 구독 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="c768a-172">선택 **구독**, hello 일괄 처리 계정에는 사용 하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="c768a-173">Hello에 **구독** 블레이드를 **사용 + 할당량**합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="c768a-174">할당량 증가</span><span class="sxs-lookup"><span data-stu-id="c768a-174">Increase a quota</span></span>
<span data-ttu-id="c768a-175">이러한 단계 toorequest 일괄 처리 계정이 나 hello를 사용 하 여 구독에 대 한 할당량 증가 따라 [Azure 포털][portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="c768a-176">hello 유형의 할당량 증가 배치 계정 hello 풀 할당 모드에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="c768a-177">배치 코어 할당량 증가</span><span class="sxs-lookup"><span data-stu-id="c768a-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="c768a-178">배치 계정에서 만들어진 경우 **서비스 일괄 처리** 모드에서는 이러한 단계 toorequest 일괄 처리 코어 할당량 증가 수행:</span><span class="sxs-lookup"><span data-stu-id="c768a-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="c768a-179">선택 hello **도움말 + 지원** 포털 대시보드에서 타일 또는 물음표 hello (**?**) hello 포털의 hello 오른쪽 위 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="c768a-180">**새 기본 지원 요청** > **기본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="c768a-181">Hello에 **기본 사항** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="c768a-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="c768a-182">a.</span><span class="sxs-lookup"><span data-stu-id="c768a-182">a.</span></span> <span data-ttu-id="c768a-183">**문제 형식** > **할당량**</span><span class="sxs-lookup"><span data-stu-id="c768a-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="c768a-184">b.</span><span class="sxs-lookup"><span data-stu-id="c768a-184">b.</span></span> <span data-ttu-id="c768a-185">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-185">Select your subscription.</span></span>
   
    <span data-ttu-id="c768a-186">c.</span><span class="sxs-lookup"><span data-stu-id="c768a-186">c.</span></span> <span data-ttu-id="c768a-187">**할당량 유형** > **배치**</span><span class="sxs-lookup"><span data-stu-id="c768a-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="c768a-188">d.</span><span class="sxs-lookup"><span data-stu-id="c768a-188">d.</span></span> <span data-ttu-id="c768a-189">**지원 계획** > **할당량 지원 - 포함됨**</span><span class="sxs-lookup"><span data-stu-id="c768a-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="c768a-190">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-190">Click **Next**.</span></span>
4. <span data-ttu-id="c768a-191">Hello에 **문제** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="c768a-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="c768a-192">a.</span><span class="sxs-lookup"><span data-stu-id="c768a-192">a.</span></span> <span data-ttu-id="c768a-193">선택 된 **심각도** tooyour에 따라 [비즈니스 영향][support_sev]합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="c768a-194">b.</span><span class="sxs-lookup"><span data-stu-id="c768a-194">b.</span></span> <span data-ttu-id="c768a-195">**세부 정보**, toochange, hello 일괄 처리 계정 이름 및 hello 새 제한 하려는 각 할당량을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="c768a-196">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-196">Click **Next**.</span></span>
5. <span data-ttu-id="c768a-197">Hello에 **연락처 정보** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="c768a-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="c768a-198">a.</span><span class="sxs-lookup"><span data-stu-id="c768a-198">a.</span></span> <span data-ttu-id="c768a-199">**기본 연락 방법**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="c768a-200">b.</span><span class="sxs-lookup"><span data-stu-id="c768a-200">b.</span></span> <span data-ttu-id="c768a-201">확인 하 고 필요한 hello 연락처 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="c768a-202">클릭 **만들기** toosubmit hello 지원 요청.</span><span class="sxs-lookup"><span data-stu-id="c768a-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="c768a-203">지원 요청을 제출하면 Azure 지원 팀에서 연락을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="c768a-204">Note는 근무일 기준 too2 정도 걸릴 수 있습니다 hello 요청을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="c768a-205">구독 코어 할당량 증가</span><span class="sxs-lookup"><span data-stu-id="c768a-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="c768a-206">배치 계정이 **사용자 구독** 모드에서 생성되었으며 추가 지역 또는 VM 제품군 코어가 필요한 경우 구독에서 할당량 증가를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c768a-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="c768a-207">해당 단계는 [Resource Manager 코어 할당량 증가 요청](../azure-supportability/resource-manager-core-quotas-request.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c768a-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="c768a-208">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="c768a-208">Related topics</span></span>
* [<span data-ttu-id="c768a-209">Hello Azure 포털을 사용 하 여 Azure 배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c768a-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="c768a-210">Azure 배치 기능 개요</span><span class="sxs-lookup"><span data-stu-id="c768a-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="c768a-211">Azure 구독 및 서비스 제한, 할당량 및 제약 조건</span><span class="sxs-lookup"><span data-stu-id="c768a-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
