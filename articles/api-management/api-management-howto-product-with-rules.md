---
title: "Azure API Management로 API 보호 | Microsoft Docs"
description: "할당량 및 제한(속도 제한) 정책을 사용하여 API를 보호하는 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 5553bcb8f9fd38630f694151dc644a684266387c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="6e935-103">Azure API Management를 사용하여 속도 제한으로 API 보호</span><span class="sxs-lookup"><span data-stu-id="6e935-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="6e935-104">이 가이드에서는 Azure API Management로 속도 제한 및 할당량 정책을 구성하여 백엔드 API에 대한 보호를 추가하기가 얼마나 쉬운지 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="6e935-105">이 자습서에서는 개발자가 [구독별 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [구독별 사용 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) 정책을 사용하여 API를 분당 최대 10번 및 주당 최대 200번까지 호출할 수 있는 "무료 평가판" API 제품을 만들어 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="6e935-106">그런 다음 API를 게시하고 속도 제한 정책을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="6e935-107">[rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 정책을 사용하는 고급 제한 시나리오는 [Azure API Management로 고급 요청 제한](api-management-sample-flexible-throttling.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e935-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="6e935-108"><a name="create-product"> </a>제품 만들기</span><span class="sxs-lookup"><span data-stu-id="6e935-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="6e935-109">이 단계에서는 구독 승인을 요구하지 않는 무료 평가판 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="6e935-110">이미 구성된 제품이 있어 이 자습서에 사용하려는 경우 무료 평가판 제품 대신 해당 제품을 사용하여 [호출 속도 제한 및 할당량 정책 구성][Configure call rate limit and quota policies]으로 바로 이동한 다음 해당 단계에서부터 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="6e935-111">시작하려면 Azure Portal에서 API Management 서비스에 대한 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="6e935-113">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management에서 첫 번째 API 관리][Manage your first API in Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e935-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="6e935-114">왼쪽의 **API Management** 메뉴에서 **제품**을 클릭하여 **제품** 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![제품 추가][api-management-add-product]

<span data-ttu-id="6e935-116">**제품 추가**를 클릭하여 **새 제품 추가** 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![새 제품 추가][api-management-new-product-window]

<span data-ttu-id="6e935-118">**제목** 상자에 **무료 평가판**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="6e935-119">**설명** 상자에 **구독자는 액세스가 거부 되었습니다 200 호출/주 최대 10 개의 호출/분을 실행할 수 있습니다** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="6e935-120">API Management의 제품은 보호되거나 개방될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="6e935-121">사용하기 전에 먼저 보호된 제품을 구독할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="6e935-122">개방된 제품은 구독하지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="6e935-123">구독이 필요한 보호된 제품을 만들기 위해 **구독 필요**가 선택되었는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6e935-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="6e935-124">기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-124">This is the default setting.</span></span>

<span data-ttu-id="6e935-125">관리자가 이 제품에 대한 구독 시도를 검토하고 허용하거나 거부하도록 하려면 **구독 승인 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="6e935-126">확인란을 선택하지 않으면 구독 시도가 자동으로 승인됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="6e935-127">이 예제에서는 승인이 자동으로 승인되므로 이 확인란을 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="6e935-128">개발자 계정으로 새 제품을 여러 번 구독할 수 있도록 하려면 **여러 동시 구독 허용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="6e935-129">이 자습서는 여러 동시 구독을 활용하지 않으므로 해당 항목을 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="6e935-130">모든 값을 입력한 후에는 **저장**을 클릭하여 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-130">After all values are entered, click **Save** to create the product.</span></span>

![제품 추가됨][api-management-product-added]

<span data-ttu-id="6e935-132">기본적으로 새 제품은 **관리자** 그룹의 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="6e935-133">여기서는 **개발자** 그룹에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="6e935-134">**무료 평가판**을 클릭한 다음 **표시 여부** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="6e935-135">API Management에서 그룹은 개발자에 대한 제품 표시 여부를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="6e935-136">제품은 그룹에 대한 표시 여부를 부여하고, 개발자는 자신이 속한 그룹에게 표시되는 제품을 보고 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="6e935-137">자세한 내용은 [Azure API Management에서 그룹을 만들고 사용하는 방법][How to create and use groups in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e935-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![개발자 그룹 추가][api-management-add-developers-group]

<span data-ttu-id="6e935-139">**개발자** 확인란을 선택한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="6e935-140"><a name="add-api"> </a>제품에 API를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="6e935-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="6e935-141">이 자습서 단계에서는 새 무료 평가판 제품에 Echo API를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="6e935-142">각 API Management 서비스 인스턴스는 실험해 보고 API Management에 대해 알아보는 데 사용할 수 있는 Echo API가 미리 구성되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="6e935-143">자세한 내용은 [Azure API Management에서 첫 번째 API Management][Manage your first API in Azure API Management]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e935-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="6e935-144">왼쪽의 **API Management** 메뉴에서 **제품**을 클릭한 다음 **평가판**을 클릭하여 제품을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![제품 구성][api-management-configure-product]

<span data-ttu-id="6e935-146">**제품에 API 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-146">Click **Add API to product**.</span></span>

![제품에 API 추가][api-management-add-api]

<span data-ttu-id="6e935-148">**Echo API**를 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-148">Select **Echo API**, and then click **Save**.</span></span>

![Echo API 추가][api-management-add-echo-api]

## <span data-ttu-id="6e935-150"><a name="policies"> </a>호출 속도 제한 및 할당량 정책을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6e935-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="6e935-151">속도 제한 및 할당량은 정책 편집기에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="6e935-152">이 자습서에서 추가할 두 개의 정책은 [구독당 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [구독당 사용 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-152">The two policies we will be adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="6e935-153">이러한 정책은 제품 범위에서 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-153">These policies must be applied at the product scope.</span></span>

<span data-ttu-id="6e935-154">왼쪽의 **API Management** 메뉴 아래에 있는 **정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-154">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="6e935-155">**제품** 목록에서 **무료 평가판**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-155">In the **Product** list, click **Free Trial**.</span></span>

![제품 정책][api-management-product-policy]

<span data-ttu-id="6e935-157">**정책 추가**를 클릭하여 정책 템플릿을 가져오고 속도 제한 및 할당량 정책을 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-157">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![정책 추가][api-management-add-policy]

<span data-ttu-id="6e935-159">속도 제한 및 할당량 정책은 인바운드 정책이므로, 인바운드 요소에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-159">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![정책 편집기][api-management-policy-editor-inbound]

<span data-ttu-id="6e935-161">정책 목록을 스크롤하여 **구독당 호출 속도 제한** 정책 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-161">Scroll through the list of policies and locate the **Limit call rate per subscription** policy entry.</span></span>

![정책 설명][api-management-limit-policies]

<span data-ttu-id="6e935-163">**인바운드** 정책 요소에 커서가 놓이면 **구독당 호출 속도 제한** 옆에 있는 화살표를 클릭하여 정책 템플릿을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-163">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="6e935-164">코드 조각에서 볼 수 있듯이, 정책을 통해 제품의 API 및 작업에 대한 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-164">As you can see from the snippet, the policy allows setting limits for the product's APIs and operations.</span></span> <span data-ttu-id="6e935-165">이 자습서에서는 해당 기능을 사용하지 않을 것이므로 다음 예제처럼 **rate-limit** 요소에서 **api** 및 **operation** 요소를 삭제하여 외부 **rate-limit** 요소만 남게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-165">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **rate-limit** element, such that only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="6e935-166">무료 평가판 제품에서 최대 허용 호출 속도는 분당 호출 10개이므로 **호출** 특성 값으로 **10**을 입력하고 **renewal-period** 특성으로 **60**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-166">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="6e935-167">**구독당 사용 할당량 설정** 정책을 구성하려면 **인바운드** 요소 내에서 새로 추가된 **rate-limit** 요소 바로 아래에 커서를 놓고 **구독당 사용 할당량 설정** 왼쪽의 화살표를 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-167">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then locate and click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="6e935-168">**구독당 사용 할당량 설정** 정책도 마찬가지로 **구독당 사용 할당량 설정** 정책을 통해 제품의 API 및 작업에 대한 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-168">Similarly to the **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on the product's APIs and operations.</span></span> <span data-ttu-id="6e935-169">이 자습서에서는 해당 기능을 사용하지 않을 것이므로 다음 예제처럼 **quota** 요소에서 **api** 및 **operation** 요소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-169">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **quota** element, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="6e935-170">할당량은 간격이나 대역폭 기준 또는 간격과 대역폭 기준의 호출 수에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-170">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="6e935-171">이 자습서에서는 대역폭 기반으로 제한하지 않으므로 **bandwidth** 특성을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-171">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="6e935-172">무료 평가판 제품에서 할당량은 주당 호출 200개입니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-172">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="6e935-173">**호출** 특성 값으로 **200**을 지정한 다음, **renewal-period** 값으로 **604800**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-173">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="6e935-174">정책 간격은 초 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="6e935-175">일주일의 간격을 계산하려면 일수(7), 하루의 시간 수(24), 한 시간의 분 수(60) 및 일 분의 초 수(60)를 곱하면 됩니다. 즉, 7 * 24 * 60 * 60 = 604800이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-175">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="6e935-176">정책 구성을 마치면 다음 예제와 같아집니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-176">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="6e935-177">원하는 정책이 구성된 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-177">After the desired policies are configured, click **Save**.</span></span>

![정책 저장][api-management-policy-save]

## <span data-ttu-id="6e935-179"><a name="publish-product"> </a> 제품을 게시하려면</span><span class="sxs-lookup"><span data-stu-id="6e935-179"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="6e935-180">이제 API를 추가하고 정책을 구성했으며, 개발자가 제품을 사용할 수 있도록 해당 제품을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-180">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="6e935-181">왼쪽의 **API Management** 메뉴에서 **제품**을 클릭한 다음 **평가판**을 클릭하여 제품을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-181">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![제품 구성][api-management-configure-product]

<span data-ttu-id="6e935-183">**게시**를 클릭한 후 **예, 게시**를 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-183">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![제품 게시][api-management-publish-product]

## <span data-ttu-id="6e935-185"><a name="subscribe-account"> </a>제품에 개발자 계정을 구독하려면</span><span class="sxs-lookup"><span data-stu-id="6e935-185"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="6e935-186">제품을 게시했으며 이제 제품을 구독하고 개발자가 제품을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-186">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="6e935-187">API Management 인스턴스의 관리자는 모든 제품에 자동으로 구독 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-187">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="6e935-188">이 자습서 단계에서는 비관리자 개발자 계정 중 하나를 무료 평가판 제품에 구독시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-188">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="6e935-189">개발자 계정이 관리자 역할의 일부인 경우에는 이미 구독 등록되었더라도 이 단계를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-189">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="6e935-190">왼쪽의 **API Management** 메뉴에서 **사용자**를 클릭한 다음, 개발자 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-190">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="6e935-191">이 예제에서는 **Clayton Gragg** 개발자 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-191">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![개발자 구성][api-management-configure-developer]

<span data-ttu-id="6e935-193">**구독 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-193">Click **Add Subscription**.</span></span>

![구독 추가][api-management-add-subscription-menu]

<span data-ttu-id="6e935-195">**무료 평가판**을 선택한 다음, **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![구독 추가][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="6e935-197">이 자습서에서는 무료 평가판 제품에 대해 여러 동시 구독을 사용하도록 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-197">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="6e935-198">사용하도록 설정한 경우 다음 예제처럼 구독의 이름을 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-198">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![구독 추가][api-management-add-subscription-multiple]

<span data-ttu-id="6e935-200">**구독**을 클릭하면 제품이 사용자의 **구독** 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-200">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![구독 추가됨][api-management-subscription-added]

## <span data-ttu-id="6e935-202"><a name="test-rate-limit"> </a>작업을 호출하고 속도 제한을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="6e935-202"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="6e935-203">무료 평가판 제품을 구성하고 게시했으며 이제 일부 작업을 호출하고 속도 제한 정책을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-203">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="6e935-204">오른쪽 위에 있는 메뉴에서 **개발자 포털**을 클릭하여 개발자 포털로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-204">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="6e935-206">상단 메뉴에서 **API**를 클릭한 다음 **Echo API**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-206">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![개발자 포털][api-management-developer-portal-api-menu]

<span data-ttu-id="6e935-208">**GET Resource**를 클릭한 다음 **사용해 보세요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-208">Click **GET Resource**, and then click **Try it**.</span></span>

![콘솔 시작][api-management-open-console]

<span data-ttu-id="6e935-210">기본 매개 변수 값을 유지한 다음, 무료 평가판 제품의 구독 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-210">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![구독 키][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="6e935-212">구독이 여러 개 있는 경우에는 **무료 평가판**의 키를 선택합니다. 그렇지 않은 경우 이전 단계에 구성한 정책이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-212">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="6e935-213">**보내기**를 클릭한 다음 응답을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-213">Click **Send**, and then view the response.</span></span> <span data-ttu-id="6e935-214">**응답 상태** **200 OK**입니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-214">Note the **Response status** of **200 OK**.</span></span>

![작업 결과][api-management-http-get-results]

<span data-ttu-id="6e935-216">속도 제한 정책인 분당 호출 10개를 초과하는 속도의 **보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-216">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="6e935-217">속도 제한 정책을 초과하면 응답 상태 **429 요청이 너무 많음** 이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-217">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![작업 결과][api-management-http-get-429]

<span data-ttu-id="6e935-219">**응답 콘텐츠** 는 재시도에 성공하기 전의 남은 간격을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-219">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="6e935-220">속도 제한 정책인 분당 호출 10개가 적용되는 경우 속도 제한이 초과하기 전에 처음 10개의 제품 호출에 성공한 후 60초가 경과할 때까지 후속 호출에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-220">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="6e935-221">이 예제에서는 남은 간격이 54초입니다.</span><span class="sxs-lookup"><span data-stu-id="6e935-221">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="6e935-222"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e935-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="6e935-223">다음 비디오에서 속도 제한 및 할당량을 설정하는 데모를 보세요.</span><span class="sxs-lookup"><span data-stu-id="6e935-223">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
