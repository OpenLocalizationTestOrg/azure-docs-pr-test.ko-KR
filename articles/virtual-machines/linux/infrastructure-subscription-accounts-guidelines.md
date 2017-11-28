---
title: "Linux VM에 대한 Azure 구독 및 계정 | Microsoft Docs"
description: "Azure의 구독 및 계정에 대한 핵심 디자인 및 구현 지침에 대해 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="08d80-103">Linux VM에 대한 Azure 구독 및 계정 지침</span><span class="sxs-lookup"><span data-stu-id="08d80-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="08d80-104">이 문서에서는 환경 및 사용자 기반이 커질 때 구독 및 계정 관리에 접근하는 방식을 이해하는 데 주안점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="08d80-105">구독 및 계정에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="08d80-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="08d80-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="08d80-106">Decisions:</span></span>

* <span data-ttu-id="08d80-107">IT 작업 또는 인프라를 호스트하는 데 필요한 구독 및 계정 집합은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="08d80-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="08d80-108">조직에 맞게 계층을 어떻게 분류해야 하는가?</span><span class="sxs-lookup"><span data-stu-id="08d80-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="08d80-109">작업:</span><span class="sxs-lookup"><span data-stu-id="08d80-109">Tasks:</span></span>

* <span data-ttu-id="08d80-110">구독 수준에서 관리하려고 하므로 논리 조직 계층을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="08d80-111">이러한 논리 계층 구조에 맞게 필요한 계정을 정의하고 각 계정 아래에 구독을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="08d80-112">명명 규칙을 사용하여 구독 및 계정 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="08d80-113">구독 및 계정</span><span class="sxs-lookup"><span data-stu-id="08d80-113">Subscriptions and accounts</span></span>
<span data-ttu-id="08d80-114">Azure를 사용하려면 하나 이상의 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="08d80-115">VM(가상 컴퓨터) 또는 가상 네트워크와 같은 리소스는 해당 구독에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="08d80-116">기업 고객은 일반적으로 기업 등록 계약을 합니다. 이는 계층에서 가장 중요한 리소스이며 하나 이상의 계정과 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="08d80-117">기업 등록 계약이 없는 소비자 및 고객의 경우, 가장 중요한 리소스는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="08d80-118">구독은 계정과 관련되며 계정당 하나 이상의 구독이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="08d80-119">Azure는 구독 단계에서 청구 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="08d80-120">계정/구독 관계에 두 계층 단계의 제한이 있기 때문에 청구 요구에 계정 및 구독의 명명 규칙을 할당하는 것은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="08d80-121">예를 들어 글로벌 기업에서 Azure를 사용하는 경우 지역당 하나의 계정을 갖도록, 지역 수준에서 구독이 관리되도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="08d80-122">예를 들어, 다음 구조를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-122">For instance, you might use the following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="08d80-123">한 지역에 특정 그룹과 관련된 두 개 이상의 구독을 갖도록 결정하는 경우 명명 규칙은 계정 또는 구독 이름에 추가 데이터를 인코딩하기 위해 하나의 방법으로 통합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="08d80-124">이 조직에서는 청구 보고 중에 새 계층 단계를 생성하는 데 청구 데이터 조작을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="08d80-125">조직은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-125">The organization could look like the following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="08d80-126">기업 계약의 단일 계정 또는 모든 계정에 대해 다운로드한 파일을 통해 자세한 청구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08d80-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08d80-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08d80-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

