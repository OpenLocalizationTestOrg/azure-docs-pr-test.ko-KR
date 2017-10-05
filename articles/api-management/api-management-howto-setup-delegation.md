---
title: "사용자 등록 및 제품 구독을 위임하는 방법"
description: "Azure API 관리에서 사용자 등록 및 제품 구독을 타사에 위임하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="0b81a-103">사용자 등록 및 제품 구독을 위임하는 방법</span><span class="sxs-lookup"><span data-stu-id="0b81a-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="0b81a-104">위임을 통해 개발자 로그인/등록 및 제품 구독을 처리하는 데 개발자 포털의 기본 제공된 기능이 아닌 기존 웹 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="0b81a-105">따라서 웹 사이트에서 사용자 데이터를 소유하고 이러한 단계에 대한 유효성 검사를 편리한 방식으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="0b81a-106"><a name="delegate-signin-up"> </a>개발자 로그인 및 등록 위임</span><span class="sxs-lookup"><span data-stu-id="0b81a-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="0b81a-107">개발자 로그인 및 등록을 기존 웹 사이트에 위임하려면 API 관리 개발자 포털에서 시작된 이러한 요청에 대한 진입점 역할을 하는 특수한 위임 끝점을 사이트에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="0b81a-108">최종 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="0b81a-109">개발자가 API 관리 개발자 포털의 로그인 또는 등록 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="0b81a-110">브라우저가 위임 끝점으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="0b81a-111">위임 끝점이 리디렉션되거나 사용자에게 로그인 또는 등록을 요청하는 UI를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="0b81a-112">성공하면 사용자가 처음 시작했던 API 관리 개발자 포털 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="0b81a-113">먼저, 위임 끝점을 통해 요청을 라우팅하도록 API 관리를 설정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="0b81a-114">API Management 게시자 포털에서 **보안**을 클릭하고 **위임** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="0b81a-115">'위임 로그인 및 등록' 확인란을 클릭하여 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![위임 페이지][api-management-delegation-signin-up]

* <span data-ttu-id="0b81a-117">특수한 위임 끝점의 URL을 결정하고 **위임 끝점 URL** 필드에 이 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="0b81a-118">**위임 인증 키** 필드에서 요청이 Azure API 관리에서 들어오는지 확인하기 위해 사용자에게 제공된 서명을 계산하는 데 사용되는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="0b81a-119">**생성** 단추를 클릭하여 API 관리가 임의로 사용자를 위해 키를 생성하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="0b81a-120">이제 **위임 끝점**을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="0b81a-121">몇 가지 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="0b81a-122">다음 형식의 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="0b81a-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={원본 페이지의 URL}&salt={문자열}&sig={문자열}*</span><span class="sxs-lookup"><span data-stu-id="0b81a-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="0b81a-124">로그인/등록 케이스의 쿼리 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="0b81a-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="0b81a-125">**operation**: 위임 요청의 유형을 식별합니다. 이 경우 **SignIn**만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="0b81a-126">**returnUrl**: 사용자가 로그인 또는 등록 링크를 클릭하는 페이지의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="0b81a-127">**salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="0b81a-128">**sig**: 자신의 계산된 해시와 비교하는 데 사용되는 계산된 보안 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="0b81a-129">요청이 Azure API 관리에서 들어오는지 확인합니다(선택 사항이지만 보안을 위해 상당히 권장됨).</span><span class="sxs-lookup"><span data-stu-id="0b81a-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="0b81a-130">**returnUrl** 및 **salt** 쿼리 매개 변수([아래 제공된 예제 코드])에 따라 문자열의 HMAC-SHA512 해시를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="0b81a-131">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="0b81a-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="0b81a-132">위의 계산된 해시와 **sig** 쿼리 매개 변수 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="0b81a-133">두 해시가 일치하면 다음 단계를 진행하고, 그렇지 않으면 요청을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="0b81a-134">로그인/등록에 대한 요청을 받고 있음을 확인합니다. **작업** 쿼리 매개 변수는 "**SignIn**"으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="0b81a-135">로그인 또는 등록에 대한 UI를 사용자에게 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="0b81a-136">사용자가 등록하고 있는 경우 API 관리에서 사용자의 해당 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="0b81a-137">API 관리 REST API로 [사용자를 만듭니다].</span><span class="sxs-lookup"><span data-stu-id="0b81a-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="0b81a-138">이때 사용자 ID를 사용자 저장소에 있는 것과 동일한 사용자 ID 또는 추적할 수 있는 사용자 ID로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="0b81a-139">사용자가 인증되면</span><span class="sxs-lookup"><span data-stu-id="0b81a-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="0b81a-140">[SSO(Single-Sign-On) 토큰을 요청] 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="0b81a-141">returnUrl 쿼리 매개 변수를 위의 API 호출에서 받은 SSO URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="0b81a-142">예: https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="0b81a-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="0b81a-143">사용자를 위에서 생성한 URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="0b81a-144">이전 단계를 수행하고 다음 작업 중 하나를 사용하여 **SignIn** 작업뿐만 아니라 계정 관리도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="0b81a-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="0b81a-145">**ChangePassword**</span></span>
* <span data-ttu-id="0b81a-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="0b81a-146">**ChangeProfile**</span></span>
* <span data-ttu-id="0b81a-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="0b81a-147">**CloseAccount**</span></span>

<span data-ttu-id="0b81a-148">계정 관리 작업에 대한 다음 쿼리 매개 변수를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="0b81a-149">**operation**: 위임 요청의 유형을 식별합니다(ChangePassword, ChangeProfile 또는 CloseAccount).</span><span class="sxs-lookup"><span data-stu-id="0b81a-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="0b81a-150">**userId**: 관리할 계정의 사용자 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="0b81a-151">**salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="0b81a-152">**sig**: 자신의 계산된 해시와 비교하는 데 사용되는 계산된 보안 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="0b81a-153"><a name="delegate-product-subscription"> </a>제품 구독 위임</span><span class="sxs-lookup"><span data-stu-id="0b81a-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="0b81a-154">제품 구독 위임은 사용자 로그인/등록과 유사하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="0b81a-155">최종 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="0b81a-156">개발자는 API 관리 개발자 포털에서 제품을 선택하고 구독 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="0b81a-157">브라우저가 위임 끝점으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="0b81a-158">위임 끝점에서 필요한 제품 구독 단계를 수행합니다. 이 단계는 사용자가 수행하며, 여기에는 청구 정보를 요청하는 다른 페이지로 리디렉션, 추가 질문 요청 또는 사용자 작업 없이 정보 저장 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="0b81a-159">이 기능을 사용하려면 **위임** 페이지에서 **제품 구독 위임**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="0b81a-160">그런 다음 위임 끝점에서 다음 작업을 수행하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="0b81a-161">다음 형식의 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="0b81a-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={구독할 제품}&userId={요청하는 사용자}&salt={문자열}&sig={문자열}*</span><span class="sxs-lookup"><span data-stu-id="0b81a-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="0b81a-163">제품 구독 케이스에 대한 쿼리 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="0b81a-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="0b81a-164">**operation**: 위임 요청 유형을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="0b81a-165">제품 구독 요청의 경우 유효한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="0b81a-166">"Subscribe": 사용자가 제공된 ID를 사용하여 지정된 제품을 구독하도록 하는 요청입니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="0b81a-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="0b81a-167">"Unsubscribe": 제품에 대한 사용자 구독을 취소하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="0b81a-168">"Renew": 구독을 갱신하는 요청입니다(예: 만료일이 다가오는 경우).</span><span class="sxs-lookup"><span data-stu-id="0b81a-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="0b81a-169">**productId**: 사용자가 구독을 요청한 제품의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="0b81a-170">**userId**: 요청을 생성한 사용자의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="0b81a-171">**salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="0b81a-172">**sig**: 자신의 계산된 해시와 비교하는 데 사용되는 계산된 보안 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="0b81a-173">요청이 Azure API 관리에서 들어오는지 확인합니다(선택 사항이지만 보안을 위해 상당히 권장됨).</span><span class="sxs-lookup"><span data-stu-id="0b81a-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="0b81a-174">**productId**, **userId** 및 **salt** 쿼리 매개 변수를 기반으로 하여 문자열의 HMAC-SHA512를 다음과 같이 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="0b81a-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="0b81a-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="0b81a-176">위의 계산된 해시와 **sig** 쿼리 매개 변수 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="0b81a-177">두 해시가 일치하면 다음 단계를 진행하고, 그렇지 않으면 요청을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="0b81a-178">**operation** 에 요청된 작업의 유형(예: 청구, 추가 질문 등)을 기반으로 하여 제품 구독 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="0b81a-179">사용자의 제품 구독을 마치면 [제품 구독을 위해 REST API를 호출]하여 사용자가 API 관리 제품도 구독하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="0b81a-180"><a name="delegate-example-code"> </a> 예제 코드</span><span class="sxs-lookup"><span data-stu-id="0b81a-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="0b81a-181">이러한 코드 샘플에서는 서명의 유효성을 검사하는 데 사용될 HMAC를 만들어 전달된 returnUrl의 유효성을 증명하기 위해 게시자 포털의 위임 화면에 설정된 *위임 유효성 검사 키*를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="0b81a-182">약간만 수정하면 동일한 코드를 productId 및 userId에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b81a-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="0b81a-183">**returnUrl의 해시를 생성하는 C# 코드**</span><span class="sxs-lookup"><span data-stu-id="0b81a-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="0b81a-184">**returnUrl의 해시를 생성하는 NodeJS 코드**</span><span class="sxs-lookup"><span data-stu-id="0b81a-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="0b81a-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b81a-185">Next steps</span></span>
<span data-ttu-id="0b81a-186">위임에 대한 자세한 내용은 다음 비디오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b81a-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="0b81a-187">[SSO(Single-Sign-On) 토큰을 요청]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="0b81a-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="0b81a-188">[사용자를 만듭니다]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="0b81a-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="0b81a-189">[제품 구독을 위해 REST API를 호출]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="0b81a-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="0b81a-190">[아래 제공된 예제 코드]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="0b81a-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
