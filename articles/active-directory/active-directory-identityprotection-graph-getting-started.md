---
title: "Azure Active Directory Id 보호 및 Microsoft Graph aaaGet 시작 | Microsoft Docs"
description: "Azure Active Directory에서 소개 tooquery Microsoft Graph 위험 이벤트 및 관련된 정보의 목록을 제공합니다."
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
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="b511a-104">Azure Active Directory ID 보호 및 Microsoft Graph 시작</span><span class="sxs-lookup"><span data-stu-id="b511a-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="b511a-105">Microsoft API 끝점을 통합 하는 hello 및의 홈 hello을 [Azure Active Directory Id 보호](active-directory-identityprotection.md) Api입니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="b511a-106">hello 첫 번째 API **identityRiskEvents**, 목록에 대 한 Microsoft Graph tooquery 있습니다의 [이벤트 위험](active-directory-identityprotection-risk-events-types.md) 관련 정보 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="b511a-107">이 문서는 이 API를 쿼리하는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-107">This article gets you started querying this API.</span></span> <span data-ttu-id="b511a-108">심층 분석 소개, 전체 설명서 및 액세스 toohello 그래프 탐색기에 대 한 참조 hello [Microsoft Graph 사이트](https://graph.microsoft.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b511a-109">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="b511a-110">Microsoft Graph 통해 세 개의 단계 tooaccessing Id 보호 데이터 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="b511a-111">클라이언트 암호와 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="b511a-112">이 암호와 다른 몇 가지 정보 tooauthenticate tooMicrosoft 인증 토큰 나타나는 그래프를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="b511a-113">이 토큰 toomake 요청 toohello API 끝점을 사용 하 고 Id 보호 데이터를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="b511a-114">시작하기 전에 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="b511a-115">Azure AD에서 관리자 권한 toocreate hello 응용</span><span class="sxs-lookup"><span data-stu-id="b511a-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="b511a-116">테 넌 트의 도메인 (예: contoso.onmicrosoft.com)의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="b511a-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="b511a-117">클라이언트 암호와 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="b511a-118">[로그인](https://manage.windowsazure.com) tooyour 관리자 권한으로 Azure 클래식 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="b511a-119">Hello 왼쪽된 탐색 창에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="b511a-121">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="b511a-122">Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="b511a-124">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="b511a-126">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="b511a-128">Hello에 **응용 프로그램에 대해 알리기** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="b511a-130">a.</span><span class="sxs-lookup"><span data-stu-id="b511a-130">a.</span></span> <span data-ttu-id="b511a-131">Hello에 **이름** 텍스트 상자에 응용 프로그램에 대 한 이름 (예:: AADIP 위험 이벤트 API 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="b511a-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="b511a-132">b.</span><span class="sxs-lookup"><span data-stu-id="b511a-132">b.</span></span> <span data-ttu-id="b511a-133">**유형**으로 **웹 응용 프로그램 및/또는 Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="b511a-134">c.</span><span class="sxs-lookup"><span data-stu-id="b511a-134">c.</span></span> <span data-ttu-id="b511a-135">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-135">Click **Next**.</span></span>
8. <span data-ttu-id="b511a-136">Hello에 **앱 속성** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="b511a-138">a.</span><span class="sxs-lookup"><span data-stu-id="b511a-138">a.</span></span> <span data-ttu-id="b511a-139">Hello에 **로그온 URL** 텍스트 상자에 `http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="b511a-140">b.</span><span class="sxs-lookup"><span data-stu-id="b511a-140">b.</span></span> <span data-ttu-id="b511a-141">Hello에 **앱 ID URI** 텍스트 상자에 `http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="b511a-142">c.</span><span class="sxs-lookup"><span data-stu-id="b511a-142">c.</span></span> <span data-ttu-id="b511a-143">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b511a-143">Click **Complete**.</span></span>

<span data-ttu-id="b511a-144">이제 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-144">Your can now configure your application.</span></span>

![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="b511a-146">응용 프로그램 권한 toouse hello API를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="b511a-147">Hello 바탕 화면에서 hello 메뉴에서 응용 프로그램의 페이지에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="b511a-149">Hello에 **tooother 응용 프로그램 사용 권한** 섹션에서 클릭 **응용 프로그램을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="b511a-151">Hello에 **tooother 응용 프로그램 사용 권한** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="b511a-153">a.</span><span class="sxs-lookup"><span data-stu-id="b511a-153">a.</span></span> <span data-ttu-id="b511a-154">**Microsoft Graph**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="b511a-155">b.</span><span class="sxs-lookup"><span data-stu-id="b511a-155">b.</span></span> <span data-ttu-id="b511a-156">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b511a-156">Click **Complete**.</span></span>
4. <span data-ttu-id="b511a-157">**응용 프로그램 사용 권한: 0**을 클릭한 다음 **모든 ID 위험 이벤트 정보 참고**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="b511a-159">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="b511a-161">선택키 가져오기</span><span class="sxs-lookup"><span data-stu-id="b511a-161">Get an access key</span></span>
1. <span data-ttu-id="b511a-162">응용 프로그램의 페이지 hello **키** 섹션 1 년 기간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="b511a-164">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="b511a-166">hello 키 섹션 트 새로 만든된 키의 hello 값을 복사 하 고 안전한 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="b511a-168">이 키를 분실 하면 tooreturn toothis 섹션이 있는을 새 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="b511a-169">이 키의 비밀을 유지합니다. 키를 가진 사람은 누구나 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="b511a-170">Hello에 **속성** 섹션을 복사 hello **클라이언트 ID**를 안전한 위치에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="b511a-171">TooMicrosoft 그래프 및 쿼리 hello Id 위험 이벤트 API 인증</span><span class="sxs-lookup"><span data-stu-id="b511a-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="b511a-172">이 시점에서 다음 항목이 만들어 집니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-172">At this point, you should have:</span></span>

* <span data-ttu-id="b511a-173">위의 복사 hello 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="b511a-173">hello client ID you copied above</span></span>
* <span data-ttu-id="b511a-174">위의 복사 hello 키</span><span class="sxs-lookup"><span data-stu-id="b511a-174">hello key you copied above</span></span>
* <span data-ttu-id="b511a-175">hello 테 넌 트의 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="b511a-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="b511a-176">tooauthenticate, post 보내기 요청 너무`https://login.microsoft.com` hello 본문에서 매개 변수 뒤 hello로:</span><span class="sxs-lookup"><span data-stu-id="b511a-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="b511a-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="b511a-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="b511a-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="b511a-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="b511a-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="b511a-179">client_id: <your client ID></span></span>
* <span data-ttu-id="b511a-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="b511a-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="b511a-181">Hello에 대 한 tooprovide 값이 필요 하면 **client_id** 및 hello **client_secret** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="b511a-182">성공하면 인증 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="b511a-183">toocall hello API 매개 변수 다음 hello로는 헤더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="b511a-184">을 인증할 때 토큰을 반환 하는 hello에 hello 토큰 유형이 및 액세스 토큰을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="b511a-185">API url 요청 toohello로이 헤더를 보냅니다.`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="b511a-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="b511a-186">hello 응답 성공 하면 컬렉션 id의 위험 이벤트 이며 hello 구문 분석 하 고 적절 하 게 처리 될 수 있는 OData JSON 형식으로의 데이터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="b511a-187">다음은 샘플 코드를 인증 하 고 Powershell을 사용 하 여 hello API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="b511a-188">클라이언트 ID, 키 및 테넌트 도메인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="b511a-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b511a-189">Next steps</span></span>
<span data-ttu-id="b511a-190">축 하 합니다, 프로그램 첫 번째 호출 tooMicrosoft 그래프를 방금 만든!</span><span class="sxs-lookup"><span data-stu-id="b511a-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="b511a-191">이제 identity 위험 이벤트를 쿼리 하 고 필요에 맞게 적절히 hello 데이터를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="b511a-192">Microsoft Graph에 대해 자세히 toolearn toobuild 응용 프로그램을 사용 하 여 Graph API를 hello 하는 방법을 확인 hello [설명서](https://graph.microsoft.io/docs) hello에 훨씬 더 많은 및 [Microsoft Graph 사이트](https://graph.microsoft.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="b511a-193">또한 있는지 toobookmark hello 확인 [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) hello 그래프에서 사용할 수 있는 Identity 보호 Api를 모두 나열 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="b511a-194">Id 보호 API 통해 새로운 방식으로 toowork, 추가 하는 대로 해당 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b511a-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b511a-195">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b511a-195">Additional resources</span></span>
* [<span data-ttu-id="b511a-196">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="b511a-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="b511a-197">Azure Active Directory ID 보호에서 검색한 위험 이벤트의 유형</span><span class="sxs-lookup"><span data-stu-id="b511a-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="b511a-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b511a-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="b511a-199">Microsoft Graph 개요</span><span class="sxs-lookup"><span data-stu-id="b511a-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="b511a-200">Azure AD ID 보호 서비스 루트</span><span class="sxs-lookup"><span data-stu-id="b511a-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

