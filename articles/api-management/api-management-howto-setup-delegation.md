---
title: "aaaHow toodelegate 사용자 등록 및 제품 구독"
description: "어떻게 toodelegate 사용자 등록 및 제품 구독 tooa 하는 타사 Azure API 관리에 알아봅니다."
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="b26ab-103">어떻게 toodelegate 사용자 등록 및 제품 구독</span><span class="sxs-lookup"><span data-stu-id="b26ab-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="b26ab-104">위임을 사용 하면 toouse 개발자 로그인-에/등록 및 구독 tooproducts로 처리 하기 위한 기존 웹 사이트 대신 toousing hello hello 개발자 포털에서 기본 제공 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="b26ab-105">웹 사이트 tooown hello 사용자 데이터를 사용 하도록 설정 하 고 사용자 지정 방식으로 이러한 단계의 hello 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="b26ab-106"><a name="delegate-signin-up"> </a>개발자 로그인 및 등록 위임</span><span class="sxs-lookup"><span data-stu-id="b26ab-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="b26ab-107">toodelegate 개발자 로그인 및 등록 tooyour 기존 웹 사이트 hello hello API 관리 개발자 포털에서 시작 된 이러한 모든 요청에 대 한 진입점으로 사용 하는 사이트에 특별 한 위임 끝점 toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="b26ab-108">hello 최종 워크플로 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="b26ab-109">Hello API 관리 개발자 포털에 로그인 하거나 등록 링크 hello에 대 한 개발자 클릭</span><span class="sxs-lookup"><span data-stu-id="b26ab-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="b26ab-110">브라우저는 리디렉션된 toohello 위임 끝점</span><span class="sxs-lookup"><span data-stu-id="b26ab-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="b26ab-111">위임 끝점 반환 tooor 표시 합니다. UI 묻는 사용자를 리디렉션합니다 toosign 기능 또는 등록</span><span class="sxs-lookup"><span data-stu-id="b26ab-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="b26ab-112">성공 시 hello 사용자가 리디렉션된 백 toohello API 관리 개발자 포털 페이지에서 시작</span><span class="sxs-lookup"><span data-stu-id="b26ab-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="b26ab-113">이제 첫 번째 설치 API 관리 tooroute toobegin, 위임 끝점을 통해 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="b26ab-114">Hello API 관리 게시자 포털에서 클릭 **보안** hello를 클릭 한 다음 **위임** 탭 합니다. Hello 확인란 tooenable 'Delegate 등록 및 로그인'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![위임 페이지][api-management-delegation-signin-up]

* <span data-ttu-id="b26ab-116">어떤 특별 한 위임 끝점의 URL hello 되며 hello에 입력 결정 **위임 끝점 URL** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="b26ab-117">Hello 내 **위임 인증 키** 필드 사용된 toocompute 요청 hello 확인 tooensure에 대 한 제공 된 서명 tooyou는 실제로 Azure API 관리에서 제공 되는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="b26ab-118">Hello를 클릭할 수 있는 **생성** 단추 toohave API 관리 사용자에 대 한 키를 임의로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="b26ab-119">이제 toocreate hello 필요한 **위임 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="b26ab-120">몇 가지 작업 tooperform 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="b26ab-121">요청 hello 다음 폼에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="b26ab-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={원본 페이지의 URL}&salt={문자열}&sig={문자열}*</span><span class="sxs-lookup"><span data-stu-id="b26ab-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="b26ab-123">Hello 로그인 / 등록 사례에 대 한 쿼리 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="b26ab-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="b26ab-124">**operation**: 위임 요청의 유형을 식별합니다. 이 경우 **SignIn**만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="b26ab-125">**returnUrl**: hello hello 사용자 로그인 하거나 등록 링크를 클릭 하는 hello 페이지의 URL</span><span class="sxs-lookup"><span data-stu-id="b26ab-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="b26ab-126">**salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="b26ab-127">**sig**: 비교 tooyour 자체에 사용 되는 계산 된 보안 해시 toobe 계산 된 해시</span><span class="sxs-lookup"><span data-stu-id="b26ab-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="b26ab-128">해당 hello 요청이 (선택 사항 이지만 보안에 대 한 권장 사항임) Azure API 관리에서 오는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="b26ab-129">Hello를 기반으로 문자열의 한 hmac-sha512 해시 계산 **returnUrl** 및 **솔트** 쿼리 매개 변수 ([아래에 제공 된 예제 코드]):</span><span class="sxs-lookup"><span data-stu-id="b26ab-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="b26ab-130">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="b26ab-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="b26ab-131">Hello의 hello 위에서 계산 된 해시 toohello 값 비교 **sig** 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="b26ab-132">Hello 두 해시가 일치 하는 경우 toohello 다음 단계에서 이동, 그렇지 않으면 hello 요청을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="b26ab-133">Sign / / 기호 위쪽에 대 한 요청을 받고 있는지 확인: hello **작업** 쿼리 매개 변수를 설정할 너무 "**SignIn**"입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="b26ab-134">Hello 사용자 toosign 옵트인 하거나 등록 하는 UI 제공</span><span class="sxs-lookup"><span data-stu-id="b26ab-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="b26ab-135">Hello 사용자가 등록 해 있으면 toocreate 해당 계정에 대 한 API 관리에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="b26ab-136">[사용자 만들기] hello API 관리 REST API로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="b26ab-137">이렇게 할 경우 사용자 저장소에 같거나 tooan ID 있습니다 수에 추적 하는 사용자 ID toohello hello를 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="b26ab-138">Hello 사용자가 성공적으로 인증 하면:</span><span class="sxs-lookup"><span data-stu-id="b26ab-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="b26ab-139">[single sign-on (SSO) 토큰을 요청] hello API 관리 REST API를 통해</span><span class="sxs-lookup"><span data-stu-id="b26ab-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="b26ab-140">returnUrl 쿼리 매개 변수 toohello 위의 hello API 호출 로부터 받은 SSO URL을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="b26ab-141">예: https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="b26ab-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="b26ab-142">리디렉션 hello 사용자 toohello 위의 URL 생성</span><span class="sxs-lookup"><span data-stu-id="b26ab-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="b26ab-143">또한 toohello에서 **SignIn** 작업을 수행할 수도 있습니다 계정 관리 hello 이전 단계를 수행 하 고 작업을 수행 하는 hello 중 하나를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="b26ab-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="b26ab-144">**ChangePassword**</span></span>
* <span data-ttu-id="b26ab-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="b26ab-145">**ChangeProfile**</span></span>
* <span data-ttu-id="b26ab-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="b26ab-146">**CloseAccount**</span></span>

<span data-ttu-id="b26ab-147">계정 관리 작업에 대 한 쿼리 매개 변수 뒤 hello를 통과 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="b26ab-148">**operation**: 위임 요청의 유형을 식별합니다(ChangePassword, ChangeProfile 또는 CloseAccount).</span><span class="sxs-lookup"><span data-stu-id="b26ab-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="b26ab-149">**userId**: hello 계정 toomanage의 hello 사용자 id</span><span class="sxs-lookup"><span data-stu-id="b26ab-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="b26ab-150">**salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="b26ab-151">**sig**: 비교 tooyour 자체에 사용 되는 계산 된 보안 해시 toobe 계산 된 해시</span><span class="sxs-lookup"><span data-stu-id="b26ab-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="b26ab-152"><a name="delegate-product-subscription"> </a>제품 구독 위임</span><span class="sxs-lookup"><span data-stu-id="b26ab-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="b26ab-153">제품 구독을 위임 toodelegating 사용자 로그인/접속 유사 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="b26ab-154">hello 최종 워크플로 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="b26ab-155">개발자는 hello API 관리 개발자 포털에서 제품을 선택 하 고 hello 가입 단추를 클릭</span><span class="sxs-lookup"><span data-stu-id="b26ab-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="b26ab-156">브라우저는 리디렉션된 toohello 위임 끝점</span><span class="sxs-lookup"><span data-stu-id="b26ab-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="b26ab-157">필요한 제품 구독 단계를 수행 하는 위임 끝점-tooyou 위로 이므로 리디렉션 tooanother 페이지 toorequest 결제 정보, 추가 질문 또는 단순히 hello 정보를 저장 하 고 사용자 개입을 필요로 하지 않는 수반 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="b26ab-158">hello에 tooenable hello 기능 **위임** 페이지 **제품 구독을 위임**합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="b26ab-159">그런 다음 hello 위임 끝점 hello 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="b26ab-160">요청 hello 다음 폼에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="b26ab-161">*{작업이} http://www.yourwebsite.com/apimdelegation?operation= & productId = {에 제품 toosubscribe} & userId = {사용자 요청을 만드는} 솔트 & = {string} & sig = {string}*</span><span class="sxs-lookup"><span data-stu-id="b26ab-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="b26ab-162">Hello 제품 구독 사례에 대 한 쿼리 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="b26ab-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="b26ab-163">**operation**: 위임 요청 유형을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="b26ab-164">제품 구독에 대 한 요청 hello 유효한 옵션은:</span><span class="sxs-lookup"><span data-stu-id="b26ab-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="b26ab-165">"구독": 인 제품을 지정 된 요청 toosubscribe hello 사용자 tooa 제공 ID (아래 참조)</span><span class="sxs-lookup"><span data-stu-id="b26ab-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="b26ab-166">"구독을 취소할": 요청 toounsubscribe 제품에서 사용자</span><span class="sxs-lookup"><span data-stu-id="b26ab-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="b26ab-167">"갱신": 요청이 toorenew 하는 구독 (예: 만료 될 수)</span><span class="sxs-lookup"><span data-stu-id="b26ab-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="b26ab-168">**productId**: hello 제품 hello 사용자의 hello ID 요청에 toosubscribe</span><span class="sxs-lookup"><span data-stu-id="b26ab-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="b26ab-169">**userId**: hello에 hello 요청이 hello 사용자의 ID</span><span class="sxs-lookup"><span data-stu-id="b26ab-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="b26ab-170">**salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="b26ab-171">**sig**: 비교 tooyour 자체에 사용 되는 계산 된 보안 해시 toobe 계산 된 해시</span><span class="sxs-lookup"><span data-stu-id="b26ab-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="b26ab-172">해당 hello 요청이 (선택 사항 이지만 보안에 대 한 권장 사항임) Azure API 관리에서 오는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="b26ab-173">Hello를 기반으로 문자열의 HMAC SHA512 계산 **productId**, **userId** 및 **솔트** 쿼리 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="b26ab-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="b26ab-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="b26ab-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="b26ab-175">Hello의 hello 위에서 계산 된 해시 toohello 값 비교 **sig** 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="b26ab-176">Hello 두 해시가 일치 하는 경우 toohello 다음 단계에서 이동, 그렇지 않으면 hello 요청을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="b26ab-177">요청 된 작업의 hello 형식을 기반으로 제품 구독 처리를 수행 **작업** -질문 등 추가 예: 대금 청구, 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="b26ab-178">편이 hello 사용자 toohello 제품, 구독에 가입 하 여 hello 사용자 toohello API 관리 제품 [제품 구독에 대 한 REST API 호출 hello]합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="b26ab-179"><a name="delegate-example-code"> </a> 예제 코드</span><span class="sxs-lookup"><span data-stu-id="b26ab-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="b26ab-180">샘플 표시 방식을 코드 이러한 tootake hello *위임 유효성 검사 키*, hello 게시자 포털의 hello 위임 화면에 설정 된,이 HMAC toocreate toovalidate hello 서명, hello의 hello 유효성을 증명 사용 전달 된 returnUrl 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="b26ab-181">hello hello productId 및 약간의 수정 하지 않고도 사용자 Id에 대 한 동일한 코드가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b26ab-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="b26ab-182">**ReturnUrl의 C# 코드 toogenerate 해시**</span><span class="sxs-lookup"><span data-stu-id="b26ab-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="b26ab-183">**ReturnUrl의 NodeJS 코드 toogenerate 해시**</span><span class="sxs-lookup"><span data-stu-id="b26ab-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="b26ab-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b26ab-184">Next steps</span></span>
<span data-ttu-id="b26ab-185">위임에 대 한 자세한 내용은 hello 다음 비디오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b26ab-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[single sign-on (SSO) 토큰을 요청]: http://go.microsoft.com/fwlink/?LinkId=507409
[사용자를 만듭니다]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[제품 구독에 대 한 REST API 호출 hello]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[아래에 제공 된 예제 코드]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
