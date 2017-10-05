---
title: "Azure Resource Manager 코어 할당량 증가 요청 | Microsoft Docs"
description: "Azure Resource Manager 코어 할당량 증가 요청"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="29705-103">Resource Manager 코어 할당량 증가 요청</span><span class="sxs-lookup"><span data-stu-id="29705-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="29705-104">Resource Manager 코어 할당량은 지역 수준 및 SKU 제품군 수준에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="29705-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="29705-105">[Azure 구독 및 서비스 제한](http://aka.ms/quotalimits) 페이지에서 할당량이 적용되는 방식에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="29705-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="29705-106">SKU 제품군에 대해 알아보려면 [Virtual Machines 가격 책정](http://aka.ms/pricingcompute) 페이지에서 비용과 성능을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29705-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="29705-107">증가를 요청하려면 Azure Portal [https://portal.azure.com](https://portal.azure.com)에서 코어에 대한 할당량 지원 사례를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29705-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="29705-108">Azure Portal에서 [지원 요청을 만드는](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="29705-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="29705-109">새 지원 요청 페이지에서 문제 유형은 "할당량"으로 할당량 유형은 "코어"로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29705-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![할당량 기본 사항 블레이드](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="29705-111">배포 모델을 "Resource Manager"로 선택하고 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29705-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![할당량 문제 블레이드](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="29705-113">증가가 필요한 SKU 제품군을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29705-113">Select the SKU Families that require an increase.</span></span>

    ![SKU 시리즈 선택됨](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="29705-115">구독에 대한 새 한도를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29705-115">Enter the new limits you would like on the subscription.</span></span>

    ![SKU 새 할당량 요청](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="29705-117">줄을 제거하려면 SKU 제품군 드롭다운에서 SKU 선택을 해제하거나 삭제 "x" 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29705-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="29705-118">각 SKU 제품군에 대해 원하는 할당량을 입력한 다음 문제 단계 페이지에서 "다음"을 클릭하여 지원 요청 만들기를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="29705-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
