---
title: "Azure API 관리에서 OAuth 2.0을 사용 하 여 aaaAuthorize 개발자 계정을 | Microsoft Docs"
description: "자세한 방법을 tooauthorize 사용자가 API 관리에서 OAuth 2.0을 사용 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="56dd0-103">Tooauthorize 개발자 어떻게 사용 하 여 계정을 Azure API 관리에서 OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="56dd0-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="56dd0-104">대부분의 Api 지원 [OAuth 2.0](http://oauth.net/2/) toosecure API hello 및를 유효한 사용자 액세스 권한이 있으며 리소스 toowhich에만 액세스할 수 있는 자격이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="56dd0-105">순서 toouse Azure API 관리 대화형 개발자 콘솔에서 이러한 Api와 hello 서비스 있습니다 tooconfigure OAuth 2.0을 사용 하면 서비스 인스턴스 toowork API를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="56dd0-106"><a name="prerequisites"> </a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="56dd0-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="56dd0-107">이 가이드에서는 어떻게 tooconfigure API 관리 서비스 인스턴스 toouse 개발자에 대 한 OAuth 2.0 권한 부여 계정, 하지만 표시 하지 않는 있습니다 어떻게 알아봅니다 tooconfigure OAuth 2.0 공급자.</span><span class="sxs-lookup"><span data-stu-id="56dd0-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="56dd0-108">hello 단계는 유사 하며 필요한 hello 가지 API 관리 서비스 인스턴스에서 OAuth 2.0을 구성에 사용 되는 정보는 공급자가 다른 경우 각 OAuth 2.0에 대 한 hello 구성 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="56dd0-109">이 항목에서는 OAuth 2.0 공급자로서 Azure Active Directory를 사용하는 예제를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="56dd0-110">Azure Active Directory를 사용 하 여 OAuth 2.0 구성 방법에 대 한 자세한 내용은 참조 hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] 샘플.</span><span class="sxs-lookup"><span data-stu-id="56dd0-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="56dd0-111"><a name="step1"> </a>API 관리에서 OAuth 2.0 권한 부여 서버 구성</span><span class="sxs-lookup"><span data-stu-id="56dd0-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="56dd0-112">시작 tooget 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="56dd0-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![게시자 포털][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="56dd0-114">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="56dd0-115">클릭 **보안** hello에서 **API 관리** hello 마우스 왼쪽된 단추 클릭에 메뉴 **OAuth 2.0**, 클릭 하 고 **추가 권한 부여 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="56dd0-117">클릭 한 후 **추가 권한 부여 서버**, hello 새 권한 부여 서버 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![새 서버][api-management-oauth2-server-1]

<span data-ttu-id="56dd0-119">Hello에는 이름 및 선택적 설명을 입력 **이름** 및 **설명** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="56dd0-120">이러한 필드는 hello 현재 API 관리 서비스 인스턴스 내에서 사용 되는 tooidentify hello OAuth 2.0 권한 부여 서버 및 OAuth 2.0 hello 서버에서 해당 값이 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="56dd0-121">Hello 입력 **클라이언트 등록 페이지 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="56dd0-122">이 페이지는 사용자가 만드는 고의 계정을 관리할 수 있으며 사용 되는 OAuth 2.0 hello 공급자에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="56dd0-123">hello **클라이언트 등록 페이지 URL** toohello 페이지가 사용 하는 지점 toocreate를 사용 하 여를 업데이트 하 고 계정의 사용자 관리를 지 원하는 OAuth 2.0 공급자에 대 한 자신의 계정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="56dd0-124">일부 조직에서는 구성 하지 않거나 hello OAuth 2.0 공급자가 지 원하는 경우에이 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="56dd0-125">OAuth 2.0 공급자에 사용자 계정의 관리를 구성 하는 경우, 회사 hello URL 또는 URL 같은 여기에 자리 표시자 URL 같은 입력 `https://placeholder.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="56dd0-126">hello hello hello 폼의 다음 섹션에 포함 되어 **인증 코드 권한 유형**, **권한 부여 끝점 URL**, 및 **권한 부여 요청 메서드가** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![새 서버][api-management-oauth2-server-2]

<span data-ttu-id="56dd0-128">Hello 지정 **인증 코드 권한 유형** hello 원하는 형식을 선택 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="56dd0-129">**인증 코드** 가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="56dd0-130">Hello 입력 **권한 부여 끝점 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="56dd0-131">Azure Active Directory에 대 한이 URL이 url을 비슷한 toohello 됩니다 여기서 `<client_id>` 응용 프로그램 toohello OAuth 2.0 서버를 식별 하는 hello 클라이언트 id로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="56dd0-132">hello **권한 부여 요청 메서드가** toohello OAuth 2.0 서버 hello 권한 부여 요청을 보내는 하는 방식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="56dd0-133">기본적으로는 **GET** 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-133">By default **GET** is selected.</span></span>

<span data-ttu-id="56dd0-134">hello 다음 섹션은에 hello **끝점 URL 토큰**, **클라이언트 인증 방법을**, **메서드를 전송 하는 액세스 토큰**, 및 **기본범위** 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![새 서버][api-management-oauth2-server-3]

<span data-ttu-id="56dd0-136">Azure Active Directory OAuth 2.0 서버 hello **끝점 URL 토큰** , 형식에 따라 hello 갖습니다 여기서 `<APPID>` 의 hello 형식이 `yourapp.onmicrosoft.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="56dd0-137">hello에 대 한 기본 설정은 **클라이언트 인증 방법을** 은 **기본**, 및 **메서드를 전송 하는 액세스 토큰** 은 **권한 부여 헤더**.</span><span class="sxs-lookup"><span data-stu-id="56dd0-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="56dd0-138">이러한 값은 hello와 함께 hello 폼의이 섹션에 구성 된 **기본 범위**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="56dd0-139">hello **클라이언트 자격 증명** 섹션에서는 hello **클라이언트 ID** 및 **클라이언트 암호**, OAuth 2.0의 hello 생성 및 구성 프로세스 중 얻어 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="56dd0-140">한 번 hello **클라이언트 ID** 및 **클라이언트 암호** 지정 hello **redirect_uri** hello에 대 한 **인증 코드** 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="56dd0-141">이 URI는 OAuth 2.0 서버 구성에 사용 되는 tooconfigure hello 회신 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![새 서버][api-management-oauth2-server-4]

<span data-ttu-id="56dd0-143">경우 **인증 코드 권한 유형** 너무 설정**리소스 소유자 암호**, hello **리소스 소유자 암호 자격 증명** 섹션은 사용 되는 toospecify;이 자격 증명 그렇지 않으면 있습니다 수 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![새 서버][api-management-oauth2-server-5]

<span data-ttu-id="56dd0-145">Hello 양식을 완료 되 면 클릭 **저장** toosave hello API 관리 OAuth 2.0 권한 부여 서버 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="56dd0-146">Hello 서버 구성을 저장 되 고 나면 구성할 수 있습니다 Api toouse이이 구성에서는 hello 다음 섹션에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="56dd0-147"><a name="step2"></a>API toouse OAuth 2.0 사용자 권한 부여 구성</span><span class="sxs-lookup"><span data-stu-id="56dd0-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="56dd0-148">클릭 **Api** hello에서 **API 관리** 메뉴 hello에 남아 있는 원하는 hello API의 hello 이름을 클릭 하 고 **보안**, 한 다음 확인란 hello에 대 한 **OAuth 2.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![사용자 권한 부여][api-management-user-authorization]

<span data-ttu-id="56dd0-150">원하는 선택 hello **권한 부여 서버** hello 드롭 다운 목록 및 클릭에서 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![사용자 권한 부여][api-management-user-authorization-save]

## <span data-ttu-id="56dd0-152"><a name="step3"></a>Hello 개발자 포털에서에서 hello OAuth 2.0 사용자 권한 부여를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="56dd0-153">OAuth 2.0 권한 부여 서버를 구성 하 고 API toouse 해당 서버를 구성 했으면 toohello 개발자 포털을 이동 하는 API를 호출 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="56dd0-154">클릭 **개발자 포털** hello 맨 위 오른쪽 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-154">Click **Developer portal** in hello top right menu.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="56dd0-156">클릭 **Api** hello 상단 메뉴 및 선택 **에코 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="56dd0-158">구성 하는 하나의 API가 있는 경우 표시 tooyour 계정 Api를 클릭 한 다음 이동 직접 해당 API에 대 한 toohello 작업.</span><span class="sxs-lookup"><span data-stu-id="56dd0-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="56dd0-159">선택 hello **리소스 가져오기** 작업을 클릭 하 여 **콘솔을 열고**, 선택한 후 **인증 코드** hello 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![콘솔 시작][api-management-open-console]

<span data-ttu-id="56dd0-161">때 **인증 코드** 은 선택 하면 팝업 창이 hello OAuth 2.0 공급자의 hello 로그인 폼으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="56dd0-162">이 예에서 hello 로그인 폼은 Azure Active Directory에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="56dd0-163">팝업을 사용 하는 경우 tooenable을 묻는 메시지가 표시 됩니다. 사용 안 함 hello 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="56dd0-164">사용 하도록 설정한 후 선택 **인증 코드** 다시 고 hello 로그인 폼이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![로그인][api-management-oauth2-signin]

<span data-ttu-id="56dd0-166">로그인 하면 hello **요청 헤더** 채워집니다는 `Authorization : Bearer` hello 요청에 권한을 부여 하는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![요청 헤더 토큰][api-management-request-header-token]

<span data-ttu-id="56dd0-168">이 시점에서 매개 변수를 남은 hello에 대 한 hello 원하는 값을 구성한 hello 요청을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="56dd0-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56dd0-169">Next steps</span></span>
<span data-ttu-id="56dd0-170">OAuth 2.0 및 API 관리를 사용 하는 방법에 대 한 자세한 내용은 참조 hello 다음 비디오 및 함께 제공 된 [문서](api-management-howto-protect-backend-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56dd0-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

