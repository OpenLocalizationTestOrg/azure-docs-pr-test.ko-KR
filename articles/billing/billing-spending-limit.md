---
title: "Azure 지출 한도 이해 | Microsoft Docs"
description: "Azure 지출 한도의 작동 방식 및 제거 방법을 설명합니다."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: a2743ef34bde0faabb3afd2ace27acddd59d3d70
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="understand-azure-spending-limit-and-how-to-remove-it"></a><span data-ttu-id="0c528-103">Azure 지출 한도의 작동 방식 및 제거 방법 이해</span><span class="sxs-lookup"><span data-stu-id="0c528-103">Understand Azure spending limit and how to remove it</span></span>

<span data-ttu-id="0c528-104">Azure 지출 한도는 Azure 구독이 소비할 수 있는 지출을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-104">Azure spending limit is a limit on how much your Azure subscription can spend.</span></span> <span data-ttu-id="0c528-105">평가판 제안이나 여러 달의 크레딧을 포함하는 제안에 등록하는 모든 신규 고객은 기본적으로 지출 한도가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-105">All new customers who sign up for the trial offer or offers that includes credits over multiple months have the spending limit turned on by default.</span></span> <span data-ttu-id="0c528-106">지출 한도는 $0입니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-106">The spending limit is $0.</span></span> <span data-ttu-id="0c528-107">이 값은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-107">It can’t be changed.</span></span> <span data-ttu-id="0c528-108">종량제 구독 및 약정 플랜과 같은 구독 유형에는 지출 한도를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-108">The spending limit isn’t available for subscription types such as Pay-As-You-Go subscriptions and commitment plans.</span></span> <span data-ttu-id="0c528-109">[전체 Azure 제품 목록 및 지출 한도 가용성](https://azure.microsoft.com/support/legal/offer-details/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c528-109">See the [full list of Azure offers and the availability of the spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

## <a name="what-happens-when-i-reach-the-spending-limit"></a><span data-ttu-id="0c528-110">지출 한도에 도달하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="0c528-110">What happens when I reach the spending limit?</span></span>

<span data-ttu-id="0c528-111">제안에 포함된 월별 할당량을 모두 사용할 경우 해당 청구월의 나머지 기간 동안 배포한 서비스가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-111">When your usage results in charges that exhaust the monthly amounts included in your offer, the services that you deployed are disabled for the rest of that billing month.</span></span> <span data-ttu-id="0c528-112">예를 들어 배포한 Cloud Services가 프로덕션에서 제거되고 Azure Virtual Machines가 중지되고 할당 최소됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-112">For example, Cloud Services that you deployed are removed from production and your Azure virtual machines are stopped and de-allocated.</span></span> <span data-ttu-id="0c528-113">서비스 비활성화를 방지하려면 지출 한도를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-113">To prevent your services from being disabled, you can choose to remove your spending limit.</span></span> <span data-ttu-id="0c528-114">서비스가 비활성화되면 저장소 계정 및 데이터베이스의 데이터는 관리자가 읽기 전용으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-114">When your services are disabled, the data in your storage accounts and databases are available in a read-only manner for administrators.</span></span> <span data-ttu-id="0c528-115">다음 청구 달이 시작하면 제품에 여러 달에 대한 크레딧이 포함될 경우 구독이 다시 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-115">At the beginning of the next billing month, if your offer includes credits over multiple months, your subscription will be re-enabled.</span></span> <span data-ttu-id="0c528-116">그런 다음 Cloud Services를 다시 배포하고 저장소 계정 및 데이터베이스에 대한 모든 권한을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-116">Then you can redeploy your Cloud Services and have full access to your storage accounts and databases.</span></span>

<span data-ttu-id="0c528-117">무료 평가판 구독이 지출 한도에 도달한 후에는 90일 이내에 구독을 다시 사용하도록 설정하고 자동으로 [표준 종량제 제품으로 업그레이드](billing-upgrade-azure-subscription.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-117">After the free trial subscription reaches the spending limit, you can re-enable the subscription and have it automatically [upgrade to our standard Pay-As-You-Go offer](billing-upgrade-azure-subscription.md) within 90 days.</span></span>

<span data-ttu-id="0c528-118">제품에 포함된 지출 한도에 도달할 경우 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-118">You receive notifications when you hit the spending limit for your offer.</span></span> <span data-ttu-id="0c528-119">[Azure 계정 센터](https://account.windowsazure.com)에 로그인하고 **계정**을 선택한 다음 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-119">Log on to the [Azure Account Center](https://account.windowsazure.com), select **ACCOUNT**, and then select **subscriptions**.</span></span> <span data-ttu-id="0c528-120">지출 한도에 도달한 구독에 대한 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-120">You see notifications about subscriptions that have reached the spending limit.</span></span>

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a><span data-ttu-id="0c528-121">이 경우 지출 한도를 사용하도록 설정한 경우에도 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-121">Things you are charged for even if you have a spending limit enabled</span></span>

<span data-ttu-id="0c528-122">일부 Azure 서비스 및 [Marketplace 구매 제품](https://azure.microsoft.com/marketplace/)의 경우 지출 한도가 설정되어 있어도 CC(결제 방법)에 따라 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-122">Some Azure services and [Marketplace purchases](https://azure.microsoft.com/marketplace/) can incur charges under the payment method (CC) even if a spending limit is set.</span></span> <span data-ttu-id="0c528-123">Visual Studio 라이선스, Azure Active Directory Premium, 지원 플랜 및 Marketplace에서 판매되는 대부분의 타사 브랜드 서비스를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-123">Examples are Visual studio licenses, Azure Active Directory premium, support plans, and most third-party branded services sold through the Marketplace.</span></span>


## <a name="when-not-to-use-the-spending-limit"></a><span data-ttu-id="0c528-124">지출 한도를 사용하지 않아야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="0c528-124">When not to use the spending limit</span></span>

<span data-ttu-id="0c528-125">지출 한도에 도달하면 특정 마켓플레이스 및 Microsoft 서비스를 배포 또는 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-125">The spending limit could prevent you from deploying or using certain marketplace and Microsoft services.</span></span> <span data-ttu-id="0c528-126">다음은 구독에 대한 지출 한도를 제거해야 하는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-126">Here are the scenarios where you should remove the spending limit on your subscription.</span></span>

- <span data-ttu-id="0c528-127">Oracle, Visual Studio Team Services 등의 서비스와 같은 자사 이미지를 배포할 계획인 경우.</span><span class="sxs-lookup"><span data-stu-id="0c528-127">You plan to deploy first party images like Oracle and services such as Visual Studio Team Services.</span></span> <span data-ttu-id="0c528-128">이 경우 지출 한도가 거의 순식간에 초과되어 구독이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-128">This scenario causes you to exceed your spending limit almost immediately and causes your subscription to be disabled.</span></span>

- <span data-ttu-id="0c528-129">중단하면 안 되는 서비스가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="0c528-129">You have services that cannot be disrupted.</span></span>

- <span data-ttu-id="0c528-130">손실되지 않아야 하는 가상 IP 주소와 같은 설정을 사용하는 서비스 및 리소스가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="0c528-130">You have services and resources with settings like virtual IP addresses that you don't want to lose.</span></span> <span data-ttu-id="0c528-131">서비스 및 리소스의 할당이 취소되면 이러한 설정이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-131">These settings are lost when the services and resources are deallocated.</span></span>


## <a name="remove-the-spending-limit"></a><span data-ttu-id="0c528-132">지출 한도 제거</span><span class="sxs-lookup"><span data-stu-id="0c528-132">Remove the spending limit</span></span>

<span data-ttu-id="0c528-133">유효한 결제 방법이 구독과 연결되어 있는 경우 언제든 지출 한도를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-133">You can remove the spending limit at any time as long as there's a valid payment method associated with your subscription.</span></span> <span data-ttu-id="0c528-134">여러 달의 크렛딧을 포함하는 제안의 경우 다음 청구 주기가 시작할 때 지출 한도를 다시 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-134">For offers that have credit over multiple months, you can also re-enable the spending limit at the beginning of your next billing cycle.</span></span>

<span data-ttu-id="0c528-135">지출 한도를 제거하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-135">To remove your spending limit, follow these steps:</span></span>

1. <span data-ttu-id="0c528-136">[Azure 계정 센터](https://account.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-136">Log on to the [Azure Account Center](https://account.windowsazure.com).</span></span>

2. <span data-ttu-id="0c528-137">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-137">Select a subscription.</span></span>

3. <span data-ttu-id="0c528-138">지출 한도에 도달하여 구독이 비활성화된 경우 "구독이 지출 한도에 도달하여 요금이 부과되지 않도록 비활성화되었습니다."라는 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-138">If the subscription is disabled due to the Spending Limit being reached, click this notification: "Subscription reached the Spending Limit and has been disabled to prevent charges."</span></span> <span data-ttu-id="0c528-139">그렇지 않으면 **구독 상태** 영역에서 **지출 한도 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-139">Otherwise, click **Remove spending limit** in the **SUBSCRIPTION STATUS** area.</span></span>

4. <span data-ttu-id="0c528-140">적절한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-140">Select an option that is appropriate for you.</span></span>

|<span data-ttu-id="0c528-141">옵션</span><span class="sxs-lookup"><span data-stu-id="0c528-141">Option</span></span>|<span data-ttu-id="0c528-142">결과</span><span class="sxs-lookup"><span data-stu-id="0c528-142">Effect</span></span>|
|-------|-----|
|<span data-ttu-id="0c528-143">지출 한도 무기한 제거</span><span class="sxs-lookup"><span data-stu-id="0c528-143">Remove spending limit indefinitely</span></span>|<span data-ttu-id="0c528-144">다음 청구 기간 시작 시 자동으로 설정되지 않도록 지출 한도를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-144">Removes the spending limit without turning it on automatically at the start of the next billing period.</span></span>|
|<span data-ttu-id="0c528-145">현재 청구 기간에 대한 지출 한도 제거</span><span class="sxs-lookup"><span data-stu-id="0c528-145">Remove spending limit for the current billing period</span></span>|<span data-ttu-id="0c528-146">다음 청구 기간 시작 시 자동으로 다시 설정되도록 지출 한도를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0c528-146">Removes the spending limit so that it turns back on automatically at the start of the next billing period.</span></span>|

## <a name="need-help-contact-support"></a><span data-ttu-id="0c528-147">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="0c528-147">Need help?</span></span> <span data-ttu-id="0c528-148">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="0c528-148">Contact support.</span></span>
<span data-ttu-id="0c528-149">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="0c528-149">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
