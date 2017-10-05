---
title: "Azure Active Directory ID 보호 및 Microsoft Graph 시작 | Microsoft Docs"
description: "Azure Active Directory에서 위험 이벤트 및 관련된 정보의 목록에 Microsoft Graph를 쿼리하는 방법을 소개합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 위험 이벤트, 취약점, 보안 정책, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="dbb1c-104">Azure Active Directory ID 보호 및 Microsoft Graph 시작</span><span class="sxs-lookup"><span data-stu-id="dbb1c-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="dbb1c-105">Microsoft Graph는 Microsoft의 통합된 API 끝점이며 [Azure Active Directory ID 보호](active-directory-identityprotection.md) API의 시작점입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="dbb1c-106">첫 번째 API인 **identityRiskEvents**를 사용하면 [위험 이벤트](active-directory-identityprotection-risk-events-types.md) 및 관련 정보의 목록에 대한 Microsoft Graph를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="dbb1c-107">이 문서는 이 API를 쿼리하는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-107">This article gets you started querying this API.</span></span> <span data-ttu-id="dbb1c-108">자세한 소개, 전체 설명서 및 Graph Explorer에 대한 액세스는 [Microsoft Graph 사이트](https://graph.microsoft.io/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbb1c-109">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="dbb1c-110">Microsoft Graph를 통해 ID 보호 데이터에 액세스하려면 세 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="dbb1c-111">클라이언트 암호와 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="dbb1c-112">이 암호와 다른 몇 가지 정보를 사용하여 Microsoft Graph에 인증하면 인증 토큰을 받게됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="dbb1c-113">이 토큰을 사용하여 API 끝점에 요청을 수행하고 ID 보호 데이터를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="dbb1c-114">시작하기 전에 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="dbb1c-115">Azure AD에서 응용 프로그램을 만드는 관리자 권한</span><span class="sxs-lookup"><span data-stu-id="dbb1c-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="dbb1c-116">테넌트의 도메인 이름(예: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="dbb1c-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="dbb1c-117">클라이언트 암호와 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="dbb1c-118">[로그인](https://manage.windowsazure.com) 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="dbb1c-119">왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="dbb1c-121">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="dbb1c-122">위쪽 메뉴에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-122">In the menu on the top, click **Applications**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="dbb1c-124">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-124">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="dbb1c-126">**무엇을 하고 싶나요?** 대화 상자에서 **조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="dbb1c-128">**응용 프로그램에 대한 정보 제공** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="dbb1c-130">a.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-130">a.</span></span> <span data-ttu-id="dbb1c-131">**이름** 텍스트 상자에 응용 프로그램의 이름으 입력합니다(예: AADIP 위험 이벤트 API 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="dbb1c-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="dbb1c-132">b.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-132">b.</span></span> <span data-ttu-id="dbb1c-133">**유형**으로 **웹 응용 프로그램 및/또는 Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="dbb1c-134">c.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-134">c.</span></span> <span data-ttu-id="dbb1c-135">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-135">Click **Next**.</span></span>
8. <span data-ttu-id="dbb1c-136">**앱 속성** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="dbb1c-138">a.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-138">a.</span></span> <span data-ttu-id="dbb1c-139">**로그온 URL** 텍스트 상자에 `http://localhost`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="dbb1c-140">b.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-140">b.</span></span> <span data-ttu-id="dbb1c-141">**앱 ID URI** 텍스트 상자에 `http://localhost`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="dbb1c-142">c.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-142">c.</span></span> <span data-ttu-id="dbb1c-143">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-143">Click **Complete**.</span></span>

<span data-ttu-id="dbb1c-144">이제 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-144">Your can now configure your application.</span></span>

![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="dbb1c-146">API를 사용하도록 응용 프로그램에 권한 부여</span><span class="sxs-lookup"><span data-stu-id="dbb1c-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="dbb1c-147">응용 프로그램 페이지의 위쪽에 있는 메뉴에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="dbb1c-149">**다른 응용 프로그램에 대한 권한** 섹션에서 **응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="dbb1c-151">**다른 응용 프로그램에 대한 사용 권한** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="dbb1c-153">a.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-153">a.</span></span> <span data-ttu-id="dbb1c-154">**Microsoft Graph**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="dbb1c-155">b.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-155">b.</span></span> <span data-ttu-id="dbb1c-156">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-156">Click **Complete**.</span></span>
4. <span data-ttu-id="dbb1c-157">**응용 프로그램 사용 권한: 0**을 클릭한 다음 **모든 ID 위험 이벤트 정보 참고**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="dbb1c-159">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-159">Click **Save** at the bottom of the page.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="dbb1c-161">선택키 가져오기</span><span class="sxs-lookup"><span data-stu-id="dbb1c-161">Get an access key</span></span>
1. <span data-ttu-id="dbb1c-162">응용 프로그램 페이지의 **키** 섹션에서 기간으로 1년을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="dbb1c-164">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-164">Click **Save** at the bottom of the page.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="dbb1c-166">키 섹션에서 새로 만든 키 값을 복사하고 안전한 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="dbb1c-168">이 키를 분실하면 이 섹션으로 돌아와서 새 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="dbb1c-169">이 키의 비밀을 유지합니다. 키를 가진 사람은 누구나 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="dbb1c-170">**속성** 섹션에서 **클라이언트 ID**를 복사한 다음 안전한 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="dbb1c-171">Microsoft Graph에 인증하고 ID 위험 이벤트 API를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="dbb1c-172">이 시점에서 다음 항목이 만들어 집니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-172">At this point, you should have:</span></span>

* <span data-ttu-id="dbb1c-173">위에서 복사한 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="dbb1c-173">The client ID you copied above</span></span>
* <span data-ttu-id="dbb1c-174">위에서 복사한 키</span><span class="sxs-lookup"><span data-stu-id="dbb1c-174">The key you copied above</span></span>
* <span data-ttu-id="dbb1c-175">테넌트 도메인의 이름</span><span class="sxs-lookup"><span data-stu-id="dbb1c-175">The name of your tenant's domain</span></span>

<span data-ttu-id="dbb1c-176">인증하려면 본문에서 다음 매개 변수를 ㅏ용하여 `https://login.microsoft.com` 에 게시 요청을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="dbb1c-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="dbb1c-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="dbb1c-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="dbb1c-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="dbb1c-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="dbb1c-179">client_id: <your client ID></span></span>
* <span data-ttu-id="dbb1c-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="dbb1c-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="dbb1c-181">**client_id** 및 **client_secret** 매개 변수에 대한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="dbb1c-182">성공하면 인증 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="dbb1c-183">API를 호출하려면 다음 매개 변수를 사용하여 헤더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="dbb1c-184">인증할 경우 반환된 토큰에서 토큰 유형 및 액세스 토큰을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="dbb1c-185">다음 API URL에 대한 요청으로 이 헤더를 보냅니다. `https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="dbb1c-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="dbb1c-186">성공한 경우 응답은 ID 위험 이벤트 및 OData JSON 형식으로 연결된 데이터의 컬렉션입니다. 이를 구문 분석하고 적절하게 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="dbb1c-187">다음은 Powershell을 사용하여 API를 인증하고 호출하는 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="dbb1c-188">클라이언트 ID, 키 및 테넌트 도메인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="dbb1c-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dbb1c-189">Next steps</span></span>
<span data-ttu-id="dbb1c-190">축하합니다! Microsoft Graph에 대한 호출을 처음으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="dbb1c-191">이제 ID 위험 이벤트를 쿼리하고 적절하게 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="dbb1c-192">Microsoft Graph 및 Graph API를 사용하여 응용 프로그램을 구축하는 방법에 대한 자세한 내용은 [설명서](https://graph.microsoft.io/docs) 및 [Microsoft Graph 사이트](https://graph.microsoft.io/)에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="dbb1c-193">또한 Graph에서 사용할 수 있는 ID 보호 API를 모두 나열하는 [Azure AD ID 보호 API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) 페이지에 책갈피를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="dbb1c-194">API를 통해 ID 보호를 사용하는 새로운 방법을 추가하는 대로 해당 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1c-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbb1c-195">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="dbb1c-195">Additional resources</span></span>
* [<span data-ttu-id="dbb1c-196">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="dbb1c-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="dbb1c-197">Azure Active Directory ID 보호에서 검색한 위험 이벤트의 유형</span><span class="sxs-lookup"><span data-stu-id="dbb1c-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="dbb1c-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="dbb1c-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="dbb1c-199">Microsoft Graph 개요</span><span class="sxs-lookup"><span data-stu-id="dbb1c-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="dbb1c-200">Azure AD ID 보호 서비스 루트</span><span class="sxs-lookup"><span data-stu-id="dbb1c-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

