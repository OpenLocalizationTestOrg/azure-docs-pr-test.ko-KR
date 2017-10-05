---
title: "Azure DevTest Labs에서 랩의 할당량 및 한도 규모 조정 | Microsoft Docs"
description: "Azure DevTest Labs에서 랩 규모를 조정하는 방법 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="8088a-103">DevTest Labs의 할당량 및 한도 규모 조정</span><span class="sxs-lookup"><span data-stu-id="8088a-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="8088a-104">DevTest Labs에서 작업할 때 일부 Azure 리소스에 대한 특정 기본 한도가 있으며 이 한도가 DevTest Labs 서비스에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="8088a-105">이러한 한도를 **할당량**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="8088a-106">DevTest Labs 서비스는 할당량을 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="8088a-107">발생할 수 있는 모든 할당량은 전체 Azure 구독의 기본 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="8088a-108">할당량에 도달할 때까지 각 Azure 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="8088a-109">각 구독에는 별도의 할당량이 있으며 구독마다 사용량이 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="8088a-110">예를 들어 각 구독의 기본 할당량은 20 코어입니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="8088a-111">따라서 랩에서 코어가 4개인 VM을 만드는 경우 총 5개의 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="8088a-112">[Azure 구독 및 서비스 한도](https://docs.microsoft.com/azure/azure-subscription-service-limits)에는 Azure 리소스에 대 한 가장 일반적인 할당량 중 일부가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="8088a-113">랩에서 가장 일반적으로 사용되며 사용자가 경험할 가능성이 있는 리소스에는 VM 코어, 공용 IP 주소, 네트워크 인터페이스, 관리되는 디스크, RBAC 역할 할당 및 ExpressRoute 회로가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="8088a-114">사용량 및 할당량 보기</span><span class="sxs-lookup"><span data-stu-id="8088a-114">View your usage and quotas</span></span>
<span data-ttu-id="8088a-115">다음 단계에서는 특정 Azure 리소스에 대한 구독의 현재 할당량 그리고 사용한 각 할당량의 비율을 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="8088a-116">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="8088a-117">**추가 서비스**를 선택한 후 목록에서 **청구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="8088a-118">청구 블레이드에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="8088a-119">**사용량 + 할당량**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-119">Select **Usage + quotas**.</span></span>

   ![사용량 및 할당량 단추](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="8088a-121">해당 구독에서 사용 가능한 여러 리소스 및 리소스당 사용되고 있는 할당량 비율을 나열하는 사용량 + 할당량 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![할당량 및 사용량](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="8088a-123">구독에 더 많은 리소스 요청</span><span class="sxs-lookup"><span data-stu-id="8088a-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="8088a-124">할당량 제한에 도달하는 경우 [Azure 구독 및 서비스 제한](https://docs.microsoft.com/azure/azure-subscription-service-limits)의 설명에 따라 구독의 기본 리소스 한도를 최대 한도까지 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="8088a-125">다음 단계에서는 [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)을 통해 할당량 증가를 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="8088a-126">**추가 서비스**, **청구**, **사용량 + 할당량**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="8088a-127">사용량 + 할당량 블레이드에서 **증가 요청** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![증가 요청 단추](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="8088a-129">요청을 완료하고 제출하려면 **새 지원 요청** 양식의 세 탭에 필수 정보를 모두 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![증가 요청 양식](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="8088a-131">Azure 지원에 할당량 증가를 요청하는 자세한 방법은 [Azure 한도 및 증가의 이해](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8088a-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="8088a-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8088a-132">Next steps</span></span>
* <span data-ttu-id="8088a-133">[DevTest Labs Azure Resource Manager 빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/Samples)를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="8088a-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
