---
title: "Azure에서 Windows 클라이언트 이미지 사용 | Microsoft Docs"
description: "Visual Studio 구독 혜택을 사용하여 개발/테스트 시나리오용으로 Azure에서 Windows 7, Windows 8 또는 Windows 10을 배포하는 방법"
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
ms.openlocfilehash: 207a6562965b4913416bd4dbf3eb132b42938dc9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a><span data-ttu-id="451ca-103">개발/테스트 시나리오용으로 Azure에서 Windows 클라이언트 사용</span><span class="sxs-lookup"><span data-stu-id="451ca-103">Use Windows client in Azure for dev/test scenarios</span></span>
<span data-ttu-id="451ca-104">적절한 Visual Studio(이전의 MSDN) 구독이 있으면 Azure에서 개발/테스트 시나리오에 Windows 7, Windows 8 또는 Windows 10을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-104">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="451ca-105">이 문서에서는 Azure에서 Windows 클라이언트를 실행하고 Azure 갤러리 이미지를 사용하기 위한 적격성 요구 사항에 대해 대략적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-105">This article outlines the eligibility requirements for running Windows client in Azure and use of the Azure Gallery images.</span></span>

## <a name="subscription-eligibility"></a><span data-ttu-id="451ca-106">구독 적격성</span><span class="sxs-lookup"><span data-stu-id="451ca-106">Subscription eligibility</span></span>
<span data-ttu-id="451ca-107">활성 Visual Studio 구독자, 즉 Visual Studio 구독 라이선스를 받은 사용자는 개발 및 테스트용으로 Windows 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-107">Active Visual Studio subscribers (people who have acquired a Visual Studio subscription license) can use Windows client for development and testing purposes.</span></span> <span data-ttu-id="451ca-108">Windows 클라이언트는 모든 유형의 Azure 구독에서 실행 중인 Azure 가상 컴퓨터와 사용자의 자체 하드웨어에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-108">Windows client can be used on your own hardware and Azure virtual machines running in any type of Azure subscription.</span></span> <span data-ttu-id="451ca-109">Windows 클라이언트는 일반적인 프로덕션용으로 배포하거나 Azure에서 사용할 수 없으며, 활성 Visual Studio 구독자가 아닌 사용자는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-109">Windows client may not be deployed to or used on Azure for normal production use, or used by people who are not active Visual Studio subscribers.</span></span>

<span data-ttu-id="451ca-110">편의상 Azure 갤러리의 [적격 개발/테스트 제품](#eligible-offers)내에서 특정 Windows 10 이미지를 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-110">For your convenience, we have made certain Windows 10 images available from the Azure Gallery within [eligible dev/test offers](#eligible-offers).</span></span> <span data-ttu-id="451ca-111">Visual Studio 구독자(사용 중인 제품 유형은 관계없음)는 64비트 Windows 7, Windows 8 또는 Windows 10 이미지를 [적절하게 준비하고 작성](prepare-for-upload-vhd-image.md)한 다음 [Azure에 업로드](upload-generalized-managed.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-111">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload to Azure](upload-generalized-managed.md).</span></span> <span data-ttu-id="451ca-112">이렇게 업로드하는 이미지 역시 활성 Visual Studio 구독자가 개발/테스트용으로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-112">The use remains limited to dev/test by active Visual Studio subscribers.</span></span>

## <a name="eligible-offers"></a><span data-ttu-id="451ca-113">적격 제품</span><span class="sxs-lookup"><span data-stu-id="451ca-113">Eligible offers</span></span>
<span data-ttu-id="451ca-114">아래 테이블에는 Azure 갤러리를 통해 Windows 10을 배포할 수 있는 제품 ID가 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-114">The following table details the offer IDs that are eligible to deploy Windows 10 through the Azure Gallery.</span></span> <span data-ttu-id="451ca-115">Windows 10 이미지는 다음 제품에 대해서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-115">The Windows 10 images are only visible to the following offers.</span></span> <span data-ttu-id="451ca-116">다른 제품 유형에서 Windows 클라이언트를 실행해야 하는 Visual Studio 구독자는 64비트 Windows 7, Windows 8 또는 Windows 10 이미지를 [적절하게 준비하고 작성](prepare-for-upload-vhd-image.md)한 다음 [Azure에 업로드](upload-generalized-managed.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-116">Visual Studio subscribers who need to run Windows client in a different offer type require you to [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and [then upload to Azure](upload-generalized-managed.md).</span></span>

| <span data-ttu-id="451ca-117">제품 이름</span><span class="sxs-lookup"><span data-stu-id="451ca-117">Offer Name</span></span> | <span data-ttu-id="451ca-118">제품 번호</span><span class="sxs-lookup"><span data-stu-id="451ca-118">Offer Number</span></span> | <span data-ttu-id="451ca-119">사용 가능한 클라이언트 이미지</span><span class="sxs-lookup"><span data-stu-id="451ca-119">Available client images</span></span> |
|:--- |:---:|:---:|
| [<span data-ttu-id="451ca-120">종량제 개발/테스트</span><span class="sxs-lookup"><span data-stu-id="451ca-120">Pay-As-You-Go Dev/Test</span></span>](https://azure.microsoft.com/offers/ms-azr-0023p/) |<span data-ttu-id="451ca-121">0023P</span><span class="sxs-lookup"><span data-stu-id="451ca-121">0023P</span></span> |<span data-ttu-id="451ca-122">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-122">Windows 10</span></span> |
| [<span data-ttu-id="451ca-123">Visual Studio Enterprise(MPN) 구독자</span><span class="sxs-lookup"><span data-stu-id="451ca-123">Visual Studio Enterprise (MPN) subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0029p/) |<span data-ttu-id="451ca-124">0029P</span><span class="sxs-lookup"><span data-stu-id="451ca-124">0029P</span></span> |<span data-ttu-id="451ca-125">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-125">Windows 10</span></span> |
| [<span data-ttu-id="451ca-126">Visual Studio Professional 구독자</span><span class="sxs-lookup"><span data-stu-id="451ca-126">Visual Studio Professional subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0059p/) |<span data-ttu-id="451ca-127">0059P</span><span class="sxs-lookup"><span data-stu-id="451ca-127">0059P</span></span> |<span data-ttu-id="451ca-128">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-128">Windows 10</span></span> |
| [<span data-ttu-id="451ca-129">Visual Studio Test Professional 구독자</span><span class="sxs-lookup"><span data-stu-id="451ca-129">Visual Studio Test Professional subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0060p/) |<span data-ttu-id="451ca-130">0060P</span><span class="sxs-lookup"><span data-stu-id="451ca-130">0060P</span></span> |<span data-ttu-id="451ca-131">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-131">Windows 10</span></span> |
| [<span data-ttu-id="451ca-132">Visual Studio Premium with MSDN(혜택)</span><span class="sxs-lookup"><span data-stu-id="451ca-132">Visual Studio Premium with MSDN (benefit)</span></span>](https://azure.microsoft.com/offers/ms-azr-0061p/) |<span data-ttu-id="451ca-133">0061P</span><span class="sxs-lookup"><span data-stu-id="451ca-133">0061P</span></span> |<span data-ttu-id="451ca-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-134">Windows 10</span></span> |
| [<span data-ttu-id="451ca-135">Visual Studio Enterprise 구독자</span><span class="sxs-lookup"><span data-stu-id="451ca-135">Visual Studio Enterprise subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0063p/) |<span data-ttu-id="451ca-136">0063P</span><span class="sxs-lookup"><span data-stu-id="451ca-136">0063P</span></span> |<span data-ttu-id="451ca-137">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-137">Windows 10</span></span> |
| [<span data-ttu-id="451ca-138">Visual Studio Enterprise(BizSpark) 구독자</span><span class="sxs-lookup"><span data-stu-id="451ca-138">Visual Studio Enterprise (BizSpark) subscribers</span></span>](https://azure.microsoft.com/offers/ms-azr-0064p/) |<span data-ttu-id="451ca-139">0064P</span><span class="sxs-lookup"><span data-stu-id="451ca-139">0064P</span></span> |<span data-ttu-id="451ca-140">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-140">Windows 10</span></span> |
| [<span data-ttu-id="451ca-141">Enterprise 개발/테스트</span><span class="sxs-lookup"><span data-stu-id="451ca-141">Enterprise Dev/Test</span></span>](https://azure.microsoft.com/ofers/ms-azr-0148p/) |<span data-ttu-id="451ca-142">0148P</span><span class="sxs-lookup"><span data-stu-id="451ca-142">0148P</span></span> |<span data-ttu-id="451ca-143">Windows 10</span><span class="sxs-lookup"><span data-stu-id="451ca-143">Windows 10</span></span> |

## <a name="check-your-azure-subscription"></a><span data-ttu-id="451ca-144">Azure 구독 확인</span><span class="sxs-lookup"><span data-stu-id="451ca-144">Check your Azure subscription</span></span>
<span data-ttu-id="451ca-145">제품 ID를 모르는 경우 다음 두 방법 중 하나로 Azure Portal을 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-145">If you do not know your offer ID, you can obtain it through the Azure portal in one of these two ways:</span></span>  

- <span data-ttu-id="451ca-146">‘구독’ 블레이드에서</span><span class="sxs-lookup"><span data-stu-id="451ca-146">On the 'Subscriptions' blade:</span></span>

  ![Azure 포털의 제품 ID 세부 정보](./media/client-images/offer-id-azure-portal.png) 

- <span data-ttu-id="451ca-148">또는 **청구**를 클릭하고 구독 ID를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-148">Or, click **Billing** and then click your subscription ID.</span></span> <span data-ttu-id="451ca-149">제품 ID가 청구 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-149">The offer ID appears in the Billing blade.</span></span>

<span data-ttu-id="451ca-150">Azure 계정 포털의 ['구독' 탭](http://account.windowsazure.com/Subscriptions) 에서도 제품 ID를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-150">You can also view the offer ID from the ['Subscriptions' tab](http://account.windowsazure.com/Subscriptions) of the Azure Account portal:</span></span>

![Azure 계정 포털의 제품 ID 세부 정보](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a><span data-ttu-id="451ca-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="451ca-152">Next steps</span></span>
<span data-ttu-id="451ca-153">이제 [PowerShell](quick-create-powershell.md), [Resource Manager 템플릿](ps-template.md) 또는 [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 사용하여 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="451ca-153">You can now deploy your VMs using [PowerShell](quick-create-powershell.md), [Resource Manager templates](ps-template.md), or [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

