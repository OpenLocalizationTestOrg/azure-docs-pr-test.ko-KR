---
title: "aaaAzure 리소스 관리자 코어 할당량 증가 요청 | Microsoft Docs"
description: "Azure Resource Manager 코어 할당량 증가 요청"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: b158b9f0e0338eb239da9253c2146ea93c02e316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="dad51-103">Resource Manager 코어 할당량 증가 요청</span><span class="sxs-lookup"><span data-stu-id="dad51-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="dad51-104">리소스 관리자 코어 할당량은 hello 지역 수준과 SKU 제품군 수준에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-104">Resource Manager core quotas are enforced at hello region level and SKU family level.</span></span>
<span data-ttu-id="dad51-105">Hello에 할당량을 시행 하는 방법에 대 한 자세한 [Azure 구독 및 서비스 제한](http://aka.ms/quotalimits) 페이지.</span><span class="sxs-lookup"><span data-stu-id="dad51-105">Learn more about how quotas are enforced on hello [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="dad51-106">toolearn SKU 제품군에 대 한 자세한, 비용 및 성능 hello에 비교할 수 있습니다 있습니다 [가상 컴퓨터 가격](http://aka.ms/pricingcompute) 페이지.</span><span class="sxs-lookup"><span data-stu-id="dad51-106">toolearn more about SKU Families, you may compare cost and performance on hello [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="dad51-107">증가는 toorequest hello Azure 포털에에서 코어 할당량 지원 케이스를 만들어 [https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-107">toorequest an increase, create a Quota support case for Cores in hello Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="dad51-108">너무 방법에 대해 알아봅니다[지원 요청](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) hello Azure 포털에서</span><span class="sxs-lookup"><span data-stu-id="dad51-108">Learn how too[create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in hello Azure portal</span></span>

1. <span data-ttu-id="dad51-109">Hello 새 지원 요청 페이지에 "할당량"으로 문제 유형 및 할당량 유형 "코어"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-109">On hello new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![할당량 기본 사항 블레이드](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="dad51-111">배포 모델을 "Resource Manager"로 선택하고 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![할당량 문제 블레이드](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="dad51-113">증가 필요로 하는 hello SKU 제품군을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-113">Select hello SKU Families that require an increase.</span></span>

    ![SKU 시리즈 선택됨](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="dad51-115">Hello 구독에 대해 원하는 hello 새로운 제한을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-115">Enter hello new limits you would like on hello subscription.</span></span>

    ![SKU 새 할당량 요청](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="dad51-117">tooremove 줄 hello SKU hello SKU 제품군 dropdown 또는 클릭 hello 삭제 "x" 아이콘에서을 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-117">tooremove a line, uncheck hello SKU from hello SKU family dropdown or click hello discard "x" icon.</span></span>
<span data-ttu-id="dad51-118">"Hello 원하는 할당량 각 SKU 제품군에 대해를 입력 한 후 다음" 클릭 hello에 문제 단계 페이지 toocontinue hello 지원 요청을 만드는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dad51-118">After entering hello desired quota for each SKU family, click "Next" on hello Problem step page toocontinue with hello support request creation.</span></span>
