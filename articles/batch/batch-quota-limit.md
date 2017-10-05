---
title: "Azure Batch의 서비스 할당량 및 제한 | Microsoft Docs"
description: "기본 Azure 배치 할당량, 한도 및 제약 조건에 대해 알아보고 할당량 증가를 요청하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="bf3cf-103">배치 서비스 할당량 및 제한</span><span class="sxs-lookup"><span data-stu-id="bf3cf-103">Batch service quotas and limits</span></span>

<span data-ttu-id="bf3cf-104">다른 Azure 서비스와 마찬가지로 배치 서비스와 관련하여 특정 리소스에 대한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="bf3cf-105">이러한 제한 대부분은 Azure 구독 또는 계정 수준에서 적용되는 기본 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="bf3cf-106">이 문서는 그러한 기본값을 설명하고 할당량 증가를 요청하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="bf3cf-107">배치 워크로드를 디자인하고 강화할 때 이 할당량에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="bf3cf-108">예를 들어, 풀이 지정한 계산 노드의 대상 수에 도달하지 않는 경우 배치 계정의 주요 할당량 한도 또는 구독에 대한 지역별 VM 코어 할당량에 도달했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="bf3cf-109">단일 배치 계정에서 여러 배치 워크로드를 실행하거나 다른 Azure 지역이 아닌 동일한 구독에 있는 배치 계정 간에 워크로드를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="bf3cf-110">배치에서 프로덕션 작업을 실행하려고 계획하는 경우, 위 기본값의 할당량 중 두 개 이상을 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="bf3cf-111">할당량을 늘리려면 무료 온라인 [고객지원 요청](#increase-a-quota) 을 개설합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="bf3cf-112">할당량은 신용 한도액일 뿐이며 용량을 보장하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="bf3cf-113">대규모 용량이 필요한 경우 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="bf3cf-114">리소스 할당량</span><span class="sxs-lookup"><span data-stu-id="bf3cf-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="bf3cf-115">사용자 구독 모드에서 할당량</span><span class="sxs-lookup"><span data-stu-id="bf3cf-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="bf3cf-116">풀 할당 모드가 **사용자 구독**으로 설정된 배치 계정의 경우 풀이 만들어질 때 배치 VM 및 기타 리소스(예: 저장소 계정)가 구독에 직접 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="bf3cf-117">Azure Batch 코어 할당량은 이 모드에서 생성된 계정에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="bf3cf-118">대신, 지역별 계산 코어 및 기타 리소스에 대한 구독의 할당량이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="bf3cf-119">[Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 이러한 할당량에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="bf3cf-120">사용자 구독 모드에서 만든 계정에 대한 리소스 사용을 계획 중인 경우 Linux VM 40대 또는 Windows VM 20대마다 계산 코어 외에도 다음 Batch 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="bf3cf-121">리소스</span><span class="sxs-lookup"><span data-stu-id="bf3cf-121">Resource</span></span> | <span data-ttu-id="bf3cf-122">할당량</span><span class="sxs-lookup"><span data-stu-id="bf3cf-122">Quota</span></span> | <span data-ttu-id="bf3cf-123">공급자</span><span class="sxs-lookup"><span data-stu-id="bf3cf-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="bf3cf-124">저장소 계정 1개</span><span class="sxs-lookup"><span data-stu-id="bf3cf-124">One storage account</span></span> | <span data-ttu-id="bf3cf-125">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="bf3cf-125">Storage Accounts</span></span> | <span data-ttu-id="bf3cf-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="bf3cf-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="bf3cf-127">공용 IP 주소 1개</span><span class="sxs-lookup"><span data-stu-id="bf3cf-127">One public IP address</span></span> | <span data-ttu-id="bf3cf-128">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="bf3cf-128">Public IP Addresses</span></span> | <span data-ttu-id="bf3cf-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="bf3cf-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="bf3cf-130">가상 네트워크 1개</span><span class="sxs-lookup"><span data-stu-id="bf3cf-130">One virtual network</span></span> | <span data-ttu-id="bf3cf-131">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="bf3cf-131">Virtual Networks</span></span> | <span data-ttu-id="bf3cf-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="bf3cf-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="bf3cf-133">네트워크 보안 그룹 1개</span><span class="sxs-lookup"><span data-stu-id="bf3cf-133">One network security group</span></span> | <span data-ttu-id="bf3cf-134">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="bf3cf-134">Network Security Groups</span></span> | <span data-ttu-id="bf3cf-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="bf3cf-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="bf3cf-136">가상 컴퓨터 확장 집합 1개</span><span class="sxs-lookup"><span data-stu-id="bf3cf-136">One virtual machine scale set</span></span> | <span data-ttu-id="bf3cf-137">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="bf3cf-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="bf3cf-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="bf3cf-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="bf3cf-139">부하 분산 장치 1개</span><span class="sxs-lookup"><span data-stu-id="bf3cf-139">One load balancer</span></span> | <span data-ttu-id="bf3cf-140">부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bf3cf-140">Load Balancers</span></span> | <span data-ttu-id="bf3cf-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="bf3cf-141">Microsoft.Network</span></span> | 

<span data-ttu-id="bf3cf-142">지역 수준 또는 VM 제품군별 코어 할당량은 Batch 풀 또는 풀에 필요한 VM 크기에 따라 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="bf3cf-143">할당량</span><span class="sxs-lookup"><span data-stu-id="bf3cf-143">Quota</span></span> | <span data-ttu-id="bf3cf-144">공급자</span><span class="sxs-lookup"><span data-stu-id="bf3cf-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="bf3cf-145">총 지역별 코어 수</span><span class="sxs-lookup"><span data-stu-id="bf3cf-145">Total Regional Cores</span></span> | <span data-ttu-id="bf3cf-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="bf3cf-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="bf3cf-147">…</span><span class="sxs-lookup"><span data-stu-id="bf3cf-147">…</span></span> <span data-ttu-id="bf3cf-148">제품군 코어 수</span><span class="sxs-lookup"><span data-stu-id="bf3cf-148">Family Cores</span></span> | <span data-ttu-id="bf3cf-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="bf3cf-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="bf3cf-150">기타 제한</span><span class="sxs-lookup"><span data-stu-id="bf3cf-150">Other limits</span></span>
| <span data-ttu-id="bf3cf-151">**리소스**</span><span class="sxs-lookup"><span data-stu-id="bf3cf-151">**Resource**</span></span> | <span data-ttu-id="bf3cf-152">**최대 제한**</span><span class="sxs-lookup"><span data-stu-id="bf3cf-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="bf3cf-153">[동시 작업](batch-parallel-node-tasks.md) </span><span class="sxs-lookup"><span data-stu-id="bf3cf-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="bf3cf-154">4 x 노드 코어 수</span><span class="sxs-lookup"><span data-stu-id="bf3cf-154">4 x number of node cores</span></span> |
| <span data-ttu-id="bf3cf-155">[응용 프로그램](batch-application-packages.md) </span><span class="sxs-lookup"><span data-stu-id="bf3cf-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="bf3cf-156">20</span><span class="sxs-lookup"><span data-stu-id="bf3cf-156">20</span></span> |
| <span data-ttu-id="bf3cf-157">응용 프로그램당 응용 프로그램 패키지</span><span class="sxs-lookup"><span data-stu-id="bf3cf-157">Application packages per application</span></span> |<span data-ttu-id="bf3cf-158">40</span><span class="sxs-lookup"><span data-stu-id="bf3cf-158">40</span></span> |
| <span data-ttu-id="bf3cf-159">각 응용 프로그램 패키지 크기</span><span class="sxs-lookup"><span data-stu-id="bf3cf-159">Application package size (each)</span></span> |<span data-ttu-id="bf3cf-160">약 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bf3cf-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="bf3cf-161">최대 시작 태스크 크기</span><span class="sxs-lookup"><span data-stu-id="bf3cf-161">Maximum start task size</span></span> | <span data-ttu-id="bf3cf-162">32768자<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="bf3cf-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="bf3cf-163"><sup>1</sup> 최대 블록 Blob 크기에 대한 Azure 저장소 용량 한도</span><span class="sxs-lookup"><span data-stu-id="bf3cf-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="bf3cf-164">
<sup>2</sup> 리소스 파일 및 환경 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="bf3cf-165">배치 할당량 보기</span><span class="sxs-lookup"><span data-stu-id="bf3cf-165">View Batch quotas</span></span>
<span data-ttu-id="bf3cf-166">[Azure 포털][portal]에서 Batch 계정 할당량을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="bf3cf-167">포털에서 **배치 계정** 을 선택한 다음 관심 있는 배치 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="bf3cf-168">배치 계정의 메뉴 블레이드에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="bf3cf-169">속성 블레이드에서 현재 배치 계정에 적용되는 **할당량** 을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![배치 계정 할당량][account_quotas]

<span data-ttu-id="bf3cf-171">사용자 구독 모드에서 생성된 배치 계정에 대해 Azure Portal에서 관련 구독 할당량을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="bf3cf-172">**구독**을 선택하고 배치 계정에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="bf3cf-173">**구독** 블레이드에서 **사용량 + 할당량**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="bf3cf-174">할당량 증가</span><span class="sxs-lookup"><span data-stu-id="bf3cf-174">Increase a quota</span></span>
<span data-ttu-id="bf3cf-175">[Azure Portal][portal]을 사용하여 배치 계정 또는 구독에 대해 할당량 증가를 요청하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="bf3cf-176">할당량 증가 유형은 배치 계정의 풀 할당 모드에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="bf3cf-177">배치 코어 할당량 증가</span><span class="sxs-lookup"><span data-stu-id="bf3cf-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="bf3cf-178">배치 계정이 **Batch 서비스** 모드에서 생성된 경우 다음 단계에 따라 Batch 코어 할당량 증가를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="bf3cf-179">포털 대시보드에서 **도움말 + 지원** 타일을 선택하거나 포털 오른쪽 위 모서리에 있는 물음표(**?**)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="bf3cf-180">**새 기본 지원 요청** > **기본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="bf3cf-181">**기본 사항** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="bf3cf-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="bf3cf-182">a.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-182">a.</span></span> <span data-ttu-id="bf3cf-183">**문제 형식** > **할당량**</span><span class="sxs-lookup"><span data-stu-id="bf3cf-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="bf3cf-184">b.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-184">b.</span></span> <span data-ttu-id="bf3cf-185">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-185">Select your subscription.</span></span>
   
    <span data-ttu-id="bf3cf-186">c.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-186">c.</span></span> <span data-ttu-id="bf3cf-187">**할당량 유형** > **배치**</span><span class="sxs-lookup"><span data-stu-id="bf3cf-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="bf3cf-188">d.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-188">d.</span></span> <span data-ttu-id="bf3cf-189">**지원 계획** > **할당량 지원 - 포함됨**</span><span class="sxs-lookup"><span data-stu-id="bf3cf-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="bf3cf-190">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-190">Click **Next**.</span></span>
4. <span data-ttu-id="bf3cf-191">**문제** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="bf3cf-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="bf3cf-192">a.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-192">a.</span></span> <span data-ttu-id="bf3cf-193">[비즈니스 영향][support_sev]에 따라 **심각도**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="bf3cf-194">b.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-194">b.</span></span> <span data-ttu-id="bf3cf-195">**세부 정보**에서 변경하려는 각 할당량과 배치 계정 이름, 새로운 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="bf3cf-196">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-196">Click **Next**.</span></span>
5. <span data-ttu-id="bf3cf-197">**연락처 정보** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="bf3cf-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="bf3cf-198">a.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-198">a.</span></span> <span data-ttu-id="bf3cf-199">**기본 연락 방법**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="bf3cf-200">b.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-200">b.</span></span> <span data-ttu-id="bf3cf-201">필수 연락처 세부 정보를 확인하고 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="bf3cf-202">**만들기** 를 클릭하여 지원 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="bf3cf-203">지원 요청을 제출하면 Azure 지원 팀에서 연락을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="bf3cf-204">참고로 요청 완료까지 업무일 기준 최대 2일이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="bf3cf-205">구독 코어 할당량 증가</span><span class="sxs-lookup"><span data-stu-id="bf3cf-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="bf3cf-206">배치 계정이 **사용자 구독** 모드에서 생성되었으며 추가 지역 또는 VM 제품군 코어가 필요한 경우 구독에서 할당량 증가를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="bf3cf-207">해당 단계는 [Resource Manager 코어 할당량 증가 요청](../azure-supportability/resource-manager-core-quotas-request.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf3cf-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="bf3cf-208">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="bf3cf-208">Related topics</span></span>
* [<span data-ttu-id="bf3cf-209">Azure 포털을 사용하여 Azure 배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="bf3cf-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="bf3cf-210">Azure 배치 기능 개요</span><span class="sxs-lookup"><span data-stu-id="bf3cf-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="bf3cf-211">Azure 구독 및 서비스 제한, 할당량 및 제약 조건</span><span class="sxs-lookup"><span data-stu-id="bf3cf-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
