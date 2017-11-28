---
title: "Azure에서 Windows 클라이언트 이미지의 aaaUse | Microsoft Docs"
description: "Visual Studio 구독 toouse 개발/테스트 시나리오에 대 한 toodeploy Windows 7, Windows 8 또는 Azure에서 Windows 10을 활용 방법"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a><span data-ttu-id="b7cac-103">개발/테스트 시나리오용으로 Azure에서 Windows 클라이언트 사용</span><span class="sxs-lookup"><span data-stu-id="b7cac-103">Use Windows client in Azure for dev/test scenarios</span></span>
<span data-ttu-id="b7cac-104">적절한 Visual Studio(이전의 MSDN) 구독이 있으면 Azure에서 개발/테스트 시나리오에 Windows 7, Windows 8 또는 Windows 10을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-104">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="b7cac-105">이 문서에서는 Azure 갤러리 이미지 Azure를 사용 하 여 hello의 Windows 클라이언트를 실행 하기 위한 hello 자격 요건을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-105">This article outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="subscription-eligibility"></a><span data-ttu-id="b7cac-106">구독 적격성</span><span class="sxs-lookup"><span data-stu-id="b7cac-106">Subscription eligibility</span></span>
<span data-ttu-id="b7cac-107">활성 Visual Studio 구독자, 즉 Visual Studio 구독 라이선스를 받은 사용자는 개발 및 테스트용으로 Windows 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-107">Active Visual Studio subscribers (people who have acquired a Visual Studio subscription license) can use Windows client for development and testing purposes.</span></span> <span data-ttu-id="b7cac-108">Windows 클라이언트는 모든 유형의 Azure 구독에서 실행 중인 Azure 가상 컴퓨터와 사용자의 자체 하드웨어에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-108">Windows client can be used on your own hardware and Azure virtual machines running in any type of Azure subscription.</span></span> <span data-ttu-id="b7cac-109">Windows 클라이언트에 Azure 일반 프로덕션 용도로 사용 되거나 사용 Visual Studio는 활성 구독자가 아닌 사용자가 배포 된 tooor 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-109">Windows client may not be deployed tooor used on Azure for normal production use, or used by people who are not active Visual Studio subscribers.</span></span>

<span data-ttu-id="b7cac-110">사용자 편의 위해 기울였습니다 특정 Windows 10 이미지를 사용할 수 있는 내 hello Azure 갤러리에서 [적격 개발/테스트 제공](#eligible-offers)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-110">For your convenience, we have made certain Windows 10 images available from hello Azure Gallery within [eligible dev/test offers](#eligible-offers).</span></span> <span data-ttu-id="b7cac-111">제공 서비스의 모든 형식 내에서 visual Studio 구독자 수도 [적절 하 게 준비 하 고 만들](prepare-for-upload-vhd-image.md) 64 비트 Windows 7, Windows 8 또는 Windows 10 이미지를 차례로 [tooAzure 업로드](upload-generalized-managed.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-111">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="b7cac-112">hello 사용 제한 toodev/테스트 활성 Visual Studio 구독자가 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-112">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

## <a name="eligible-offers"></a><span data-ttu-id="b7cac-113">적격 제품</span><span class="sxs-lookup"><span data-stu-id="b7cac-113">Eligible offers</span></span>
<span data-ttu-id="b7cac-114">테이블 세부 정보 hello 다음 hello Id hello Azure 갤러리를 통해 적격 toodeploy Windows 10에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-114">hello following table details hello offer IDs that are eligible toodeploy Windows 10 through hello Azure Gallery.</span></span> <span data-ttu-id="b7cac-115">Windows 10 hello 이미지는 다음 제안을 표시 toohello만입니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-115">hello Windows 10 images are only visible toohello following offers.</span></span> <span data-ttu-id="b7cac-116">Visual Studio 구독자가 필요한 toorun Windows 클라이언트에서 서로 다른 제안 유형 해야 너무[적절 하 게 준비 하 고 만들](prepare-for-upload-vhd-image.md) 64 비트 Windows 7, Windows 8 또는 Windows 10 이미지 및 [tooAzure업로드](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="b7cac-116">Visual Studio subscribers who need toorun Windows client in a different offer type require you too[adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and [then upload tooAzure](upload-generalized-managed.md).</span></span>

| <span data-ttu-id="b7cac-117">제품 이름</span><span class="sxs-lookup"><span data-stu-id="b7cac-117">Offer Name</span></span> | <span data-ttu-id="b7cac-118">제품 번호</span><span class="sxs-lookup"><span data-stu-id="b7cac-118">Offer Number</span></span> | <span data-ttu-id="b7cac-119">사용 가능한 클라이언트 이미지</span><span class="sxs-lookup"><span data-stu-id="b7cac-119">Available client images</span></span> |
|:--- |:---:|:---:|
| [<span data-ttu-id="b7cac-120">종량제 개발/테스트</span><span class="sxs-lookup"><span data-stu-id="b7cac-120">Pay-As-You-Go Dev/Test</span></span>](https://azure.microsoft.com/offers/ms-azr-0023p/) |<span data-ttu-id="b7cac-121">0023P</span><span class="sxs-lookup"><span data-stu-id="b7cac-121">0023P</span></span> |<span data-ttu-id="b7cac-122">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-122">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-123">Visual Studio Enterprise(MPN) 구독자</span><span class="sxs-lookup"><span data-stu-id="b7cac-123">Visual Studio Enterprise (MPN) subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0029p/) |<span data-ttu-id="b7cac-124">0029P</span><span class="sxs-lookup"><span data-stu-id="b7cac-124">0029P</span></span> |<span data-ttu-id="b7cac-125">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-125">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-126">Visual Studio Professional 구독자</span><span class="sxs-lookup"><span data-stu-id="b7cac-126">Visual Studio Professional subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0059p/) |<span data-ttu-id="b7cac-127">0059P</span><span class="sxs-lookup"><span data-stu-id="b7cac-127">0059P</span></span> |<span data-ttu-id="b7cac-128">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-128">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-129">Visual Studio Test Professional 구독자</span><span class="sxs-lookup"><span data-stu-id="b7cac-129">Visual Studio Test Professional subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0060p/) |<span data-ttu-id="b7cac-130">0060P</span><span class="sxs-lookup"><span data-stu-id="b7cac-130">0060P</span></span> |<span data-ttu-id="b7cac-131">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-131">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-132">Visual Studio Premium with MSDN(혜택)</span><span class="sxs-lookup"><span data-stu-id="b7cac-132">Visual Studio Premium with MSDN (benefit)</span></span>](https://azure.microsoft.com/offers/ms-azr-0061p/) |<span data-ttu-id="b7cac-133">0061P</span><span class="sxs-lookup"><span data-stu-id="b7cac-133">0061P</span></span> |<span data-ttu-id="b7cac-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-134">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-135">Visual Studio Enterprise 구독자</span><span class="sxs-lookup"><span data-stu-id="b7cac-135">Visual Studio Enterprise subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0063p/) |<span data-ttu-id="b7cac-136">0063P</span><span class="sxs-lookup"><span data-stu-id="b7cac-136">0063P</span></span> |<span data-ttu-id="b7cac-137">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-137">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-138">Visual Studio Enterprise(BizSpark) 구독자</span><span class="sxs-lookup"><span data-stu-id="b7cac-138">Visual Studio Enterprise (BizSpark) subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0064p/) |<span data-ttu-id="b7cac-139">0064P</span><span class="sxs-lookup"><span data-stu-id="b7cac-139">0064P</span></span> |<span data-ttu-id="b7cac-140">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-140">Windows 10</span></span> |
| [<span data-ttu-id="b7cac-141">Enterprise 개발/테스트</span><span class="sxs-lookup"><span data-stu-id="b7cac-141">Enterprise Dev/Test</span></span>](https://azure.microsoft.com/ofers/ms-azr-0148p/) |<span data-ttu-id="b7cac-142">0148P</span><span class="sxs-lookup"><span data-stu-id="b7cac-142">0148P</span></span> |<span data-ttu-id="b7cac-143">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b7cac-143">Windows 10</span></span> |

## <a name="check-your-azure-subscription"></a><span data-ttu-id="b7cac-144">Azure 구독 확인</span><span class="sxs-lookup"><span data-stu-id="b7cac-144">Check your Azure subscription</span></span>
<span data-ttu-id="b7cac-145">제안 ID을 알 수 없는 경우에 hello Azure 포털에서 이러한 두 가지 방법 중 하나를 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-145">If you do not know your offer ID, you can obtain it through hello Azure portal in one of these two ways:</span></span>  

- <span data-ttu-id="b7cac-146">구독 블레이드에서 hello:</span><span class="sxs-lookup"><span data-stu-id="b7cac-146">On hello 'Subscriptions' blade:</span></span>

  ![Hello Azure 포털에서에서 ID 세부 정보를 제공 합니다.](./media/client-images/offer-id-azure-portal.png) 

- <span data-ttu-id="b7cac-148">또는 **청구**를 클릭하고 구독 ID를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-148">Or, click **Billing** and then click your subscription ID.</span></span> <span data-ttu-id="b7cac-149">hello 제안 ID hello 결제 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-149">hello offer ID appears in hello Billing blade.</span></span>

<span data-ttu-id="b7cac-150">Hello에서 hello 제안 ID를 볼 수도 있습니다 ['구독' 탭](http://account.windowsazure.com/Subscriptions) hello Azure 계정 포털:</span><span class="sxs-lookup"><span data-stu-id="b7cac-150">You can also view hello offer ID from hello ['Subscriptions' tab](http://account.windowsazure.com/Subscriptions) of hello Azure Account portal:</span></span>

![Hello Azure 계정 포털에서 ID 세부 정보를 제공 합니다.](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a><span data-ttu-id="b7cac-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7cac-152">Next steps</span></span>
<span data-ttu-id="b7cac-153">이제 [PowerShell](quick-create-powershell.md), [Resource Manager 템플릿](ps-template.md) 또는 [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 사용하여 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7cac-153">You can now deploy your VMs using [PowerShell](quick-create-powershell.md), [Resource Manager templates](ps-template.md), or [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

