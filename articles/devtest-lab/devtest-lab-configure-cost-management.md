---
title: "aaaView hello 월별 예상된 랩 비용 추세 Azure DevTest Labs | Microsoft Docs"
description: "Hello Azure DevTest Labs 월별 예상된 비용 추세 차트에 알아봅니다."
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
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="9b18a-103">보기 hello 월별 예상된 랩 비용 추세 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9b18a-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="9b18a-104">DevTest Labs의 hello 비용 관리 기능에는 랩의 hello 비용을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="9b18a-105">이 문서에서는 설명 방법을 toouse hello **월별 예상 비용 추세** 차트 tooview 현재 달력 월의 예상된 비용 누계 hello 및 hello hello에 대 한 예상된 월말의 비용으로 현재 월.</span><span class="sxs-lookup"><span data-stu-id="9b18a-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="9b18a-106">이 문서에서는 tooview hello Azure 포털에서에서 월별 예상된 비용 추세 차트를 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="9b18a-107">Hello 월별 예상 비용 추세 차트 보기</span><span class="sxs-lookup"><span data-stu-id="9b18a-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="9b18a-108">tooview hello 월별 예상 비용 추세 차트는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="9b18a-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="9b18a-109">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="9b18a-110">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="9b18a-111">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="9b18a-112">Hello 랩 블레이드에서 선택 **비용 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="9b18a-113">Hello 랩에 **비용 설정** 블레이드를 **랩 비용 추세**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="9b18a-114">hello 다음 스크린 샷에 나와 비용 차트의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![비용 차트](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="9b18a-116">hello **예상 비용** 값으로 현재 월의 예상된 비용 누계 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="9b18a-117">hello **비용** 는 hello 전체 hello에 대 한 예상된 비용 현재 월을 사용 하 여 계산 hello 랩 비용 hello에 대 한 지난 5 일 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="9b18a-118">hello 비용 금액 toohello 다음 정수로 올림 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="9b18a-119">예:</span><span class="sxs-lookup"><span data-stu-id="9b18a-119">For example:</span></span> 

* <span data-ttu-id="9b18a-120">5.01 too6 반올림</span><span class="sxs-lookup"><span data-stu-id="9b18a-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="9b18a-121">5.50 too6 반올림</span><span class="sxs-lookup"><span data-stu-id="9b18a-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="9b18a-122">5.99 too6 반올림</span><span class="sxs-lookup"><span data-stu-id="9b18a-122">5.99 rounds up too6</span></span>

<span data-ttu-id="9b18a-123">Hello 차트 위에 따르면, 처럼 hello 차트에 표시 하는 hello 비용 요소가 *예상* 를 사용 하 여 비용이 [종 량 제](https://azure.microsoft.com/offers/ms-azr-0003p/) 할인율 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="9b18a-124">Hello 다음은 또한 *하지* hello 비용 계산에에서 포함:</span><span class="sxs-lookup"><span data-stu-id="9b18a-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="9b18a-125">CSP 및 Dreamspark 구독은 현재 지원 되지 않습니다 Azure DevTest Labs hello를 사용 하 게 [Azure 청구 Api](../billing/billing-usage-rate-card-overview.md) toocalculate hello 랩 비용, CSP 또는 Dreamspark 구독을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="9b18a-126">사용자에 대한 제안 요율.</span><span class="sxs-lookup"><span data-stu-id="9b18a-126">Your offer rates.</span></span> <span data-ttu-id="9b18a-127">현재 없는 수 toouse (아래에 표시 된 구독)는 사용자가와 협상 Microsoft 또는 Microsoft 파트너 프로그램 제안 요금입니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="9b18a-128">종량제 요율을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="9b18a-129">사용자 세금</span><span class="sxs-lookup"><span data-stu-id="9b18a-129">Your taxes</span></span>
* <span data-ttu-id="9b18a-130">사용자 할인</span><span class="sxs-lookup"><span data-stu-id="9b18a-130">Your discounts</span></span>
* <span data-ttu-id="9b18a-131">사용자의 청구 통화.</span><span class="sxs-lookup"><span data-stu-id="9b18a-131">Your billing currency.</span></span> <span data-ttu-id="9b18a-132">현재 hello 랩 비용 USD 통화에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="9b18a-133">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="9b18a-133">Related blog posts</span></span>
* [<span data-ttu-id="9b18a-134">두 개 더 많은 작업 tookeep에서 DevTest Labs에 추적 비용</span><span class="sxs-lookup"><span data-stu-id="9b18a-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="9b18a-135">비용 임계값을 사용하는 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="9b18a-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="9b18a-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b18a-136">Next steps</span></span>
<span data-ttu-id="9b18a-137">다음 일부의 tootry 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="9b18a-138">[랩 정책을 정의](devtest-lab-set-lab-policy.md) -tooset 사용 되는 다양 한 정책을 hello 하는 방법에 대해 알아봅니다 toogovern 랩 및 해당 Vm을 어떻게 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="9b18a-139">[사용자 지정 이미지 만들기](devtest-lab-create-template.md) - VM을 만들 때 사용자 지정 이미지 또는 마켓플레이스 이미지 중에서 기본 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="9b18a-140">이 문서에서는 어떻게 toocreate 사용자 지정은 VHD 파일에서을 이미지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="9b18a-141">[마켓플레이스 이미지 구성](devtest-lab-configure-marketplace-images.md) - DevTest Labs에서 Azure Marketplace 이미지에 기반하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="9b18a-142">이 문서에서는 설명 방법을 toospecify Azure 마켓플레이스 이미지 될 수 있는 경우 있는 환경에서 Vm을 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="9b18a-143">[랩에서 VM 만들기](devtest-lab-add-vm-with-artifacts.md) -보여 줍니다 방법을 toocreate 기본 이미지에서 VM (어느 사용자 지정 또는 마켓플레이스), 방법과 VM의 아티팩트로 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b18a-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

