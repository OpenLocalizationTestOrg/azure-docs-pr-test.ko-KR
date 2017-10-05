---
title: "Azure DevTest Labs에서 월간 예상 랩 비용 추세 보기 | Microsoft 문서"
description: "Azure DevTest Labs의 월간 예상 비용 추세 차트에 대해 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="14a24-103">Azure DevTest Labs에서 월간 예상 랩 비용 추세 보기</span><span class="sxs-lookup"><span data-stu-id="14a24-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="14a24-104">DevTest Labs의 비용 관리 기능은 랩의 비용을 추적하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="14a24-105">이 문서는 **월간 예상 비용 추세** 차트를 사용하여 이번 달의 현재 예상 비용 합계 뿐만 아니라 이번 달의 월말 추정 비용을 보는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="14a24-106">이 문서에서는 Azure 포털의 월간 예상 비용 추세 차트를 보는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="14a24-107">Monthly Estimated Cost Trend(월간 예상 비용 추세) 차트 보기</span><span class="sxs-lookup"><span data-stu-id="14a24-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="14a24-108">월간 예상 비용 추세 차트를 보려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="14a24-109">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="14a24-110">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="14a24-111">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="14a24-112">랩의 블레이드에서 **비용 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="14a24-113">랩의 **비용 설정** 블레이드에서 **랩 비용 추세**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="14a24-114">다음 스크릿샷은 비용 차트의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![비용 차트](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="14a24-116">**예상 비용** 값은 현재 월의 현재까지의 예상 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="14a24-117">**예측 비용** 은 이번 달 전체의 예상 비용으로, 이전 5일 동안의 랩 비용을 사용해서 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="14a24-118">금액은 다음 정수로 올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="14a24-119">예:</span><span class="sxs-lookup"><span data-stu-id="14a24-119">For example:</span></span> 

* <span data-ttu-id="14a24-120">5.01은 6으로 올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="14a24-121">5.50은 6으로 올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="14a24-122">5.99는 6으로 올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="14a24-123">차트에 언급되어 있듯이, 차트에 보이는 비용은 *종량제* 제안 요율을 사용하여 [예상된](https://azure.microsoft.com/offers/ms-azr-0003p/) 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="14a24-124">또한 다음 항목은 비용 계산에 포함되지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="14a24-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="14a24-125">Azure DevTest Labs에서는 [Azure 청구 API](../billing/billing-usage-rate-card-overview.md) 를 사용하여 랩 비용을 계산하며 CSP 또는 Dreamspark 구독을 지원하지 않으므로 이러한 구독 방식이 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="14a24-126">사용자에 대한 제안 요율.</span><span class="sxs-lookup"><span data-stu-id="14a24-126">Your offer rates.</span></span> <span data-ttu-id="14a24-127">현재는 Microsoft 또는 Microsoft 파트너와 협상한 제안 요율(구독 아래에 표시됨)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="14a24-128">종량제 요율을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="14a24-129">사용자 세금</span><span class="sxs-lookup"><span data-stu-id="14a24-129">Your taxes</span></span>
* <span data-ttu-id="14a24-130">사용자 할인</span><span class="sxs-lookup"><span data-stu-id="14a24-130">Your discounts</span></span>
* <span data-ttu-id="14a24-131">사용자의 청구 통화.</span><span class="sxs-lookup"><span data-stu-id="14a24-131">Your billing currency.</span></span> <span data-ttu-id="14a24-132">현재는, 랩 비용이 USD 통화로만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="14a24-133">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="14a24-133">Related blog posts</span></span>
* [<span data-ttu-id="14a24-134">DevTest Labs에서 비용을 유지하기 하기 위한 두 가지 추가 항목</span><span class="sxs-lookup"><span data-stu-id="14a24-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="14a24-135">비용 임계값을 사용하는 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="14a24-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="14a24-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14a24-136">Next steps</span></span>
<span data-ttu-id="14a24-137">다음으로 수행해 볼 작업은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-137">Here are some things to try next:</span></span>

* <span data-ttu-id="14a24-138">[랩 정책 정의](devtest-lab-set-lab-policy.md) – 랩 및 해당 VM의 사용 방식을 관리하는 데 사용되는 다양한 정책을 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="14a24-139">[사용자 지정 이미지 만들기](devtest-lab-create-template.md) - VM을 만들 때 사용자 지정 이미지 또는 마켓플레이스 이미지 중에서 기본 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="14a24-140">이 문서에는 VHD 파일에서 사용자 지정 이미지를 만드는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="14a24-141">[마켓플레이스 이미지 구성](devtest-lab-configure-marketplace-images.md) - DevTest Labs에서 Azure Marketplace 이미지에 기반하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="14a24-142">이 문서에서는 랩에서 VM을 만들 때 사용할 수 있는 Azure 마켓플레이스 이미지(있는 경우)를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="14a24-143">[랩에서 VM 만들기](devtest-lab-add-vm-with-artifacts.md) - 기본 이미지(사용자 지정 또는 마켓플레이스 이미지)에서 VM을 만드는 방법 및 VM에서 아티팩트 작업 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="14a24-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

