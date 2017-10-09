---
title: "aaaSubscription 및 Azure의 Windows Vm에 대 한 계정을 | Microsoft Docs"
description: "Hello 주요 디자인 및 구현에 대 한 지침이 구독 및 Azure에서 계정에 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="adfb1-103">Windows VM에 대한 Azure 구독 및 계정 지침</span><span class="sxs-lookup"><span data-stu-id="adfb1-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="adfb1-104">이 문서는 사용자 환경 및 사용자 기반으로 구독 및 계정 관리와 tooapproach 증가 하는 방법을 이해에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="adfb1-105">구독 및 계정에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="adfb1-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="adfb1-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="adfb1-106">Decisions:</span></span>

* <span data-ttu-id="adfb1-107">집합의 구독 및 계정 필요 한가요 toohost IT 작업 또는 인프라?</span><span class="sxs-lookup"><span data-stu-id="adfb1-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="adfb1-108">어떻게 hello 계층 toofit 아래로 toobreak 조직?</span><span class="sxs-lookup"><span data-stu-id="adfb1-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="adfb1-109">작업:</span><span class="sxs-lookup"><span data-stu-id="adfb1-109">Tasks:</span></span>

* <span data-ttu-id="adfb1-110">Toomanage 원하는 만큼 논리적 구성이 계층 정의 구독 수준에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="adfb1-111">toomatch이 논리적 계층 구조 필요한 hello 계정 및 각 계정 아래에서 구독을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="adfb1-112">Hello 집합을 구독 및 명명 규칙을 사용 하 여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="adfb1-113">구독 및 계정</span><span class="sxs-lookup"><span data-stu-id="adfb1-113">Subscriptions and accounts</span></span>
<span data-ttu-id="adfb1-114">Azure와 toowork, 하나 이상의 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="adfb1-115">VM(가상 컴퓨터) 또는 가상 네트워크와 같은 리소스는 해당 구독에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="adfb1-116">일반적으로 기업 고객은 hello 계층의 최상위 리소스 hello 되었고 관련된 tooone 또는 계정을 더는 기업 등록 계약을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="adfb1-117">소비자 및 기업 등록 없는 고객에 대 한 최상위 리소스 hello hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="adfb1-118">구독은 연결된 tooaccounts 있으며 계정당 구독을 하나 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="adfb1-119">Azure 레코드 hello 구독 수준에서 정보를 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="adfb1-120">Hello 계정/구독 관계에 있는 두 명의 계층 수준의 toohello 제한을 인해 계정 및 구독 toohello 요구 청구의 중요 한 tooalign hello 명명 규칙은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="adfb1-121">예를 들어, 글로벌 기업에서 Azure를 사용 하는 경우 있습니다 수 toohave 하나 계정 / 지역당, 선택한 구독에서 관리 지역 수준을 hello:</span><span class="sxs-lookup"><span data-stu-id="adfb1-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="adfb1-122">예를 들어, 다음 구조 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="adfb1-123">Hello ô ä ¢ 방법을 tooencode를 통합 해야 영역 toohave 둘 이상의 구독을 하나 관련된 tooa 특정 그룹을 경우 hello hello 계정 또는 hello 구독 이름에 추가 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="adfb1-124">이 조직에 청구 보고서 중 청구 데이터 toogenerate hello 새 계층의 수준 massaging 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="adfb1-125">hello 조직 다음 예제는 hello와 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="adfb1-126">기업 계약의 단일 계정 또는 모든 계정에 대해 다운로드한 파일을 통해 자세한 청구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="adfb1-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adfb1-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="adfb1-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

