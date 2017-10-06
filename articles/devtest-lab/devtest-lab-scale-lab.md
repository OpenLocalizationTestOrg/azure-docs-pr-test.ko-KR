---
title: "aaaScale 할당량 및 제한 Azure DevTest Labs 랩에서 | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure DevTest Labs에 랩"
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="6e329-103">DevTest Labs의 할당량 및 한도 규모 조정</span><span class="sxs-lookup"><span data-stu-id="6e329-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="6e329-104">DevTest Labs를 사용할 때는 개가 특정 기본 제한 toosome hello DevTest Labs 서비스에 영향을 줄 수 있는 Azure 리소스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="6e329-105">이러한 제한은 참조 tooas **할당량**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="6e329-106">hello DevTest Labs 서비스 할당량을 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="6e329-107">발생할 수 있는 할당량은 기본 제약 조건이 hello 전체 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="6e329-108">할당량에 도달할 때까지 각 Azure 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="6e329-109">각 구독에는 별도의 할당량이 있으며 구독마다 사용량이 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="6e329-110">예를 들어 각 구독의 기본 할당량은 20 코어입니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="6e329-111">따라서 랩에서 코어가 4개인 VM을 만드는 경우 총 5개의 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="6e329-112">[Azure 구독 및 서비스 제한](https://docs.microsoft.com/azure/azure-subscription-service-limits) hello Azure 리소스에 대 한 가장 일반적인 할당량 중 일부를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="6e329-113">랩 환경에서는 가장 일반적으로 사용 되는 리소스를 hello 및 할당량 포함 VM 코어, 공용 IP 주소, 네트워크 인터페이스, 관리 하는 디스크, RBAC 역할 할당 및 express 경로 회로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="6e329-114">사용량 및 할당량 보기</span><span class="sxs-lookup"><span data-stu-id="6e329-114">View your usage and quotas</span></span>
<span data-ttu-id="6e329-115">이러한 단계 어떻게 tooview hello toosee 및 특정 Azure 리소스에 대 한 구독에서 현재 할당량 사용한 각 할당량의 비율을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="6e329-116">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="6e329-117">선택 **더 서비스**를 선택한 후 **청구** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="6e329-118">Hello [결제] 블레이드에서 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="6e329-119">**사용량 + 할당량**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-119">Select **Usage + quotas**.</span></span>

   ![사용량 및 할당량 단추](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="6e329-121">사용 현황 + 할당량 hello 블레이드 표시 되 면 해당 구독 및 hello 비율로 리소스 당 사용 되는 hello 할당량에서 사용할 수 있는 다른 리소스를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![할당량 및 사용량](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="6e329-123">구독에 더 많은 리소스 요청</span><span class="sxs-lookup"><span data-stu-id="6e329-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="6e329-124">에 설명 된 대로 tooa 최대치를 구독에 있는 리소스의 hello 기본도 늘릴 수는 할당량 끝에 도달 하면 [Azure 구독 및 서비스 제한](https://docs.microsoft.com/azure/azure-subscription-service-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="6e329-125">이러한 단계에서는 보여 toorequest 할당량을 늘리려면 어떻게 hello를 통해 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="6e329-126">**추가 서비스**, **청구**, **사용량 + 할당량**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="6e329-127">안녕하세요 사용 + 할당량 블레이드 선택 hello **증가 요청** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![증가 요청 단추](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="6e329-129">toocomplete hello 요청을 제출, hello의 세 탭 모두에 hello 필요한 정보를 입력 하 고 **새로운 지원 요청** 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![증가 요청 양식](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="6e329-131">[이해 Azure 제한 및 증가](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) 할당량 toorequest Azure 지원에 연락 하는 방법에 대 한 자세한 정보를 제공 합니다. 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="6e329-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e329-132">Next steps</span></span>
* <span data-ttu-id="6e329-133">Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/Samples)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e329-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
