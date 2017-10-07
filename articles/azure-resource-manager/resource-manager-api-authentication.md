---
title: "aaaAzure Active Directory 인증 및 리소스 관리자 | Microsoft Docs"
description: "개발자 가이드 tooauthentication hello Azure 리소스 관리자 API 및 Azure Active Directory와 응용 프로그램 통합 다른 Azure 구독에 대 한 합니다."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a><span data-ttu-id="aa197-103">리소스 관리자 API 인증 tooaccess 구독 사용</span><span class="sxs-lookup"><span data-stu-id="aa197-103">Use Resource Manager authentication API tooaccess subscriptions</span></span>
## <a name="introduction"></a><span data-ttu-id="aa197-104">소개</span><span class="sxs-lookup"><span data-stu-id="aa197-104">Introduction</span></span>
<span data-ttu-id="aa197-105">소프트웨어 개발자에 게 toocreate 고객의 Azure 리소스를 관리 하는 응용 프로그램의 경우와 tooauthenticate hello Azure 리소스 관리자 Api 및 액세스 tooresources 다른 구독에 대 한 권한을 얻는 방법을이 항목에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-105">If you are a software developer who needs toocreate an app that manages customer's Azure resources, this topic shows you how tooauthenticate with hello Azure Resource Manager APIs and gain access tooresources in other subscriptions.</span></span>

<span data-ttu-id="aa197-106">앱 hello 여러 가지 방법으로 리소스 관리자 Api에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-106">Your app can access hello Resource Manager APIs in couple of ways:</span></span>

1. <span data-ttu-id="aa197-107">**사용자 + 앱 액세스**: 로그인한 사용자를 대신하여 리소스에 액세스하는 앱.</span><span class="sxs-lookup"><span data-stu-id="aa197-107">**User + app access**: for apps that access resources on behalf of a signed-in user.</span></span> <span data-ttu-id="aa197-108">이 방법은 웹앱 및 명령줄 도구 등 Azure 리소스의 "대화형 관리"만 처리하는 앱에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-108">This approach works for apps, such as web apps and command-line tools, that deal with only "interactive management" of Azure resources.</span></span>
2. <span data-ttu-id="aa197-109">**앱 전용 액세스**: 디먼 서비스 및 예약된 작업을 실행하는 앱.</span><span class="sxs-lookup"><span data-stu-id="aa197-109">**App-only access**: for apps that run daemon services and scheduled jobs.</span></span> <span data-ttu-id="aa197-110">hello 응용 프로그램 id toohello 리소스에 직접 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-110">hello app's identity is granted direct access toohello resources.</span></span> <span data-ttu-id="aa197-111">이 방법은 장기 헤드리스 (무인된) 액세스 tooAzure 해야 하는 앱에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-111">This approach works for apps that need long-term headless (unattended) access tooAzure.</span></span>

<span data-ttu-id="aa197-112">이 항목에서는 단계별 지침 toocreate 두 가지 권한 부여 방식은 사용 하는 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="aa197-112">This topic provides step-by-step instructions toocreate an app that employs both these authorization methods.</span></span> <span data-ttu-id="aa197-113">REST API 또는 C# 사용 tooperform 각 단계 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-113">It shows how tooperform each step with REST API or C#.</span></span> <span data-ttu-id="aa197-114">ASP.NET MVC 응용 프로그램을 완료 하는 hello에서 제공 됩니다. [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-114">hello complete ASP.NET MVC application is available at [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).</span></span>

## <a name="what-hello-web-app-does"></a><span data-ttu-id="aa197-115">어떤 hello 웹 앱은</span><span class="sxs-lookup"><span data-stu-id="aa197-115">What hello web app does</span></span>
<span data-ttu-id="aa197-116">hello 웹 앱:</span><span class="sxs-lookup"><span data-stu-id="aa197-116">hello web app:</span></span>

1. <span data-ttu-id="aa197-117">Azure 사용자를 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-117">Signs-in an Azure user.</span></span>
2. <span data-ttu-id="aa197-118">사용자 toogrant hello 웹 응용 프로그램 액세스 tooResource 관리자에 게 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-118">Asks user toogrant hello web app access tooResource Manager.</span></span>
3. <span data-ttu-id="aa197-119">Resource Manager에 액세스하기 위한 사용자 + 앱 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-119">Gets user + app access token for accessing Resource Manager.</span></span>
4. <span data-ttu-id="aa197-120">Hello 앱 장기 액세스 toohello 구독을 제공 하는 hello 구독에서 리소스 관리자 (3 단계)에서 토큰 toocall 및 할당 hello 앱 서비스 주 tooa 역할을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-120">Uses token (from step 3) toocall Resource Manager and assign hello app's service principal tooa role in hello subscription, which gives hello app long-term access toohello subscription.</span></span>
5. <span data-ttu-id="aa197-121">앱 전용 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-121">Gets app-only access token.</span></span>
6. <span data-ttu-id="aa197-122">리소스 관리자를 통해 hello 구독에서 (5 단계)에서 토큰 toomanage 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-122">Uses token (from step 5) toomanage resources in hello subscription through Resource Manager.</span></span>

<span data-ttu-id="aa197-123">Hello 웹 응용 프로그램의 hello 종단 간 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-123">Here's hello end-to-end flow of hello web application.</span></span>

![Resource Manager 인증 흐름](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

<span data-ttu-id="aa197-125">Hello 구독 id를 제공 하는 사용자로 toouse hello 구독에 대 한 원하는:</span><span class="sxs-lookup"><span data-stu-id="aa197-125">As a user, you provide hello subscription id for hello subscription you want toouse:</span></span>

![구독 ID 제공](./media/resource-manager-api-authentication/sample-ux-1.png)

<span data-ttu-id="aa197-127">로그인 하기 위한 계정 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-127">Select hello account toouse for logging in.</span></span>

![계정 선택](./media/resource-manager-api-authentication/sample-ux-2.png)

<span data-ttu-id="aa197-129">자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-129">Provide your credentials.</span></span>

![자격 증명 제공](./media/resource-manager-api-authentication/sample-ux-3.png)

<span data-ttu-id="aa197-131">Azure 구독을 hello 앱 액세스 tooyour에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-131">Grant hello app access tooyour Azure subscriptions:</span></span>

![액세스 권한 부여](./media/resource-manager-api-authentication/sample-ux-4.png)

<span data-ttu-id="aa197-133">연결된 구독을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-133">Manage your connected subscriptions:</span></span>

![구독 연결](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a><span data-ttu-id="aa197-135">응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="aa197-135">Register application</span></span>
<span data-ttu-id="aa197-136">코딩을 시작하기 전에 Azure Active Directory(AD)를 사용하여 웹앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-136">Before you start coding, register your web app with Azure Active Directory (AD).</span></span> <span data-ttu-id="aa197-137">앱 등록을 hello Azure AD에서 앱에 대 한 중앙 id를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-137">hello app registration creates a central identity for your app in Azure AD.</span></span> <span data-ttu-id="aa197-138">응용 프로그램 tooauthenticate 및 액세스 Azure 리소스 관리자 Api를 사용 하도록 OAuth 클라이언트 ID, 회신 Url과 자격 증명와 같은 응용 프로그램에 대 한 기본 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-138">It holds basic information about your application like OAuth Client ID, Reply URLs, and credentials that your application uses tooauthenticate and access Azure Resource Manager APIs.</span></span> <span data-ttu-id="aa197-139">또한 hello 앱 등록 응용 프로그램에 필요한 hello 사용자를 대신 하 여 Microsoft Api에 액세스할 때 사용 권한이 위임 다양 한 hello를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-139">hello app registration also records hello various delegated permissions that your application needs when accessing Microsoft APIs on behalf of hello user.</span></span>

<span data-ttu-id="aa197-140">앱에서 다른 구독에 액세스하므로 다중 테넌트 응용 프로그램으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-140">Because your app accesses other subscription, you must configure it as a multi-tenant application.</span></span> <span data-ttu-id="aa197-141">toopass 유효성 검사를 Azure Active Directory와 연결 된 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-141">toopass validation, provide a domain associated with your Azure Active Directory.</span></span> <span data-ttu-id="aa197-142">Azure Active Directory, toohello 로그인와 연결 된 toosee hello 도메인 [클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-142">toosee hello domains associated with your Azure Active Directory, log in toohello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="aa197-143">Azure Active Directory를 선택한 다음 **도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-143">Select your Azure Active Directory and then select **Domains**.</span></span>

<span data-ttu-id="aa197-144">다음 예제는 hello tooregister Azure PowerShell을 사용 하 여 앱을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-144">hello following example shows how tooregister hello app by using Azure PowerShell.</span></span> <span data-ttu-id="aa197-145">Hello 최신 버전 (2016 년 8 월)의 Azure PowerShell이 명령 toowork에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-145">You must have hello latest version (August 2016) of Azure PowerShell for this command toowork.</span></span>

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

<span data-ttu-id="aa197-146">AD 응용 프로그램 hello로 toolog hello 응용 프로그램 id와 암호 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-146">toolog in as hello AD application, you need hello application id and password.</span></span> <span data-ttu-id="aa197-147">사용 하 여 hello 이전 명령에서 반환 되는 toosee hello 응용 프로그램 id:</span><span class="sxs-lookup"><span data-stu-id="aa197-147">toosee hello application id that is returned from hello previous command, use:</span></span>

    $app.ApplicationId

<span data-ttu-id="aa197-148">다음 예제는 hello tooregister Azure CLI를 사용 하 여 앱을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-148">hello following example shows how tooregister hello app by using Azure CLI.</span></span>

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

<span data-ttu-id="aa197-149">hello 결과 hello hello 응용 프로그램으로 인증할 때 필요한 AppId를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-149">hello results include hello AppId, which you need when authenticating as hello application.</span></span>

### <a name="optional-configuration---certificate-credential"></a><span data-ttu-id="aa197-150">선택적 구성 - 인증서 자격 증명</span><span class="sxs-lookup"><span data-stu-id="aa197-150">Optional configuration - certificate credential</span></span>
<span data-ttu-id="aa197-151">또한 azure AD 응용 프로그램을 위한 인증서 자격 증명을 지원 합니다: 자체 서명 된 인증서 만들기, hello 개인 키를 유지 하 고 hello 공개 키 tooyour Azure AD 응용 프로그램 등록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-151">Azure AD also supports certificate credentials for applications: you create a self-signed cert, keep hello private key, and add hello public key tooyour Azure AD application registration.</span></span> <span data-ttu-id="aa197-152">인증을 위해 응용 프로그램에서 사용자의 개인 키를 사용 하 여 서명 하는 AD와 Azure AD 작은 페이로드 tooAzure 등록 hello 공개 키를 사용 하 여 hello 서명의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-152">For authentication, your application sends a small payload tooAzure AD signed using your private key, and Azure AD validates hello signature using hello public key that you registered.</span></span>

<span data-ttu-id="aa197-153">인증서와 함께 AD 응용 프로그램을 만드는 방법은 참조 [toocreate Azure PowerShell을 사용 하 여 서비스 사용자 tooaccess 리소스](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) 또는 [서비스 주체를 사용 하 여 Azure CLI toocreate tooaccess 리소스](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).</span><span class="sxs-lookup"><span data-stu-id="aa197-153">For information about creating an AD app with a certificate, see [Use Azure PowerShell toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) or [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).</span></span>

## <a name="get-tenant-id-from-subscription-id"></a><span data-ttu-id="aa197-154">구독 ID에서 테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-154">Get tenant id from subscription id</span></span>
<span data-ttu-id="aa197-155">toorequest 토큰을 사용 하는 toocall 리소스 관리자 일 수 있는 응용 프로그램 tooknow hello Azure 구독을 호스팅하는 hello Azure AD 테 넌 트의 테 넌 트 ID를 hello에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-155">toorequest a token that can be used toocall Resource Manager, your application needs tooknow hello tenant ID of hello Azure AD tenant that hosts hello Azure subscription.</span></span> <span data-ttu-id="aa197-156">대부분의 경우 사용자는 자신의 구독 ID를 알고 있지만 Azure Active Directory에 대한 테넌트 ID는 모를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-156">Most likely, your users know their subscription ids, but they might not know their tenant ids for Azure Active Directory.</span></span> <span data-ttu-id="aa197-157">tooget hello 구독 id에 대 한 hello 사용자에 게 확인 hello 사용자의 테 넌 트 id입니다. Hello 구독에 대 한 요청을 보낼 경우 해당 구독 id를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-157">tooget hello user's tenant id, ask hello user for hello subscription id. Provide that subscription id when sending a request about hello subscription:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

<span data-ttu-id="aa197-158">hello 요청 하지만 때문에 실패 hello 사용자가 아직 로그인 하지 않은 hello 응답에서 hello 테 넌 트 id를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-158">hello request fails because hello user has not logged in yet, but you can retrieve hello tenant id from hello response.</span></span> <span data-ttu-id="aa197-159">해당 예외에 대 한 hello 응답 헤더 값에서 hello 테 넌 트 id 검색 **Www-authenticate**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-159">In that exception, retrieve hello tenant id from hello response header value for **WWW-Authenticate**.</span></span> <span data-ttu-id="aa197-160">Hello에이 구현을 참조 [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) 메서드.</span><span class="sxs-lookup"><span data-stu-id="aa197-160">You see this implementation in hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) method.</span></span>

## <a name="get-user--app-access-token"></a><span data-ttu-id="aa197-161">사용자 + 앱 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-161">Get user + app access token</span></span>
<span data-ttu-id="aa197-162">응용 프로그램 hello 사용자 tooAzure는 OAuth 2.0 권한 부여 요청-tooauthenticate hello 사용자의 자격 증명으로 AD 리디렉션하고 인증 코드 가져오기 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-162">Your application redirects hello user tooAzure AD with an OAuth 2.0 Authorize Request - tooauthenticate hello user's credentials and get back an authorization code.</span></span> <span data-ttu-id="aa197-163">응용 프로그램 리소스 관리자에 대 한 hello 권한 부여 코드 tooget 액세스 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-163">Your application uses hello authorization code tooget an access token for Resource Manager.</span></span> <span data-ttu-id="aa197-164">hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) 메서드 hello 권한 부여 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-164">hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) method creates hello authorization request.</span></span>

<span data-ttu-id="aa197-165">이 항목에서는 hello REST API 요청 tooauthenticate hello 사용자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-165">This topic shows hello REST API requests tooauthenticate hello user.</span></span> <span data-ttu-id="aa197-166">코드에 도우미 라이브러리 tooperform 인증도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-166">You can also use helper libraries tooperform authentication in your code.</span></span> <span data-ttu-id="aa197-167">이러한 라이브러리에 대한 자세한 내용은 [Azure Active Directory 인증 라이브러리](../active-directory/active-directory-authentication-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa197-167">For more information about these libraries, see [Azure Active Directory Authentication Libraries](../active-directory/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="aa197-168">응용 프로그램에서 ID 관리를 통합하는 지침은 [Azure Active Directory 개발자 가이드](../active-directory/active-directory-developers-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa197-168">For guidance on integrating identity management in an application, see [Azure Active Directory developer's guide](../active-directory/active-directory-developers-guide.md).</span></span>

### <a name="auth-request-oauth-20"></a><span data-ttu-id="aa197-169">인증 요청(OAuth 2.0)</span><span class="sxs-lookup"><span data-stu-id="aa197-169">Auth request (OAuth 2.0)</span></span>
<span data-ttu-id="aa197-170">Open ID 연결/oauth 2.0 권한 부여 요청 toohello Azure AD 권한 부여 끝점을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-170">Issue an Open ID Connect/OAuth2.0 Authorize Request toohello Azure AD Authorize endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

<span data-ttu-id="aa197-171">이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [인증 코드 요청](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-171">hello query string parameters that are available for this request are described in hello [request an authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) topic.</span></span>

<span data-ttu-id="aa197-172">hello 방법을 예제와 다음 toorequest oauth 2.0 권한 부여:</span><span class="sxs-lookup"><span data-stu-id="aa197-172">hello following example shows how toorequest OAuth2.0 authorization:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

<span data-ttu-id="aa197-173">Azure AD hello 사용자를 인증 하 고 필요한 경우 hello 사용자 toogrant 권한 toohello 응용 프로그램을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-173">Azure AD authenticates hello user, and, if necessary, asks hello user toogrant permission toohello app.</span></span> <span data-ttu-id="aa197-174">Hello 권한 부여 코드 toohello 응용 프로그램의 회신 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-174">It returns hello authorization code toohello Reply URL of your application.</span></span> <span data-ttu-id="aa197-175">Hello에 따라 response_mode를, 어느 보냅니다 다시 hello 데이터 게시 데이터 또는 쿼리 문자열에 Azure AD가 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-175">Depending on hello requested response_mode, Azure AD either sends back hello data in query string or as post data.</span></span>

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a><span data-ttu-id="aa197-176">인증 요청(Open ID Connect)</span><span class="sxs-lookup"><span data-stu-id="aa197-176">Auth request (Open ID Connect)</span></span>
<span data-ttu-id="aa197-177">뿐만 아니라 hello 사용자를 대신 하 여 Azure 리소스 관리자 tooaccess 원하는 하지만 tooyour 응용 프로그램을 통해 Azure AD 계정을 사용 하 여 hello 사용자 toosign 통해서도으로 Open ID 연결 권한 부여 요청을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-177">If you not only wish tooaccess Azure Resource Manager on behalf of hello user, but also allow hello user toosign in tooyour application using their Azure AD account, issue an Open ID Connect Authorize Request.</span></span> <span data-ttu-id="aa197-178">Open ID Connect와 함께 응용 프로그램 앱 toosign hello 사용자에 사용할 수 있는 Azure AD에서는 id_token을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-178">With Open ID Connect, your application also receives an id_token from Azure AD that your app can use toosign in hello user.</span></span>

<span data-ttu-id="aa197-179">이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [hello 로그인 요청 보내기](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-179">hello query string parameters that are available for this request are described in hello [Send hello sign-in request](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) topic.</span></span>

<span data-ttu-id="aa197-180">Open ID Connect 요청 예제:</span><span class="sxs-lookup"><span data-stu-id="aa197-180">An example Open ID Connect request is:</span></span>

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

<span data-ttu-id="aa197-181">Azure AD hello 사용자를 인증 하 고 필요한 경우 hello 사용자 toogrant 권한 toohello 응용 프로그램을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-181">Azure AD authenticates hello user, and, if necessary, asks hello user toogrant permission toohello app.</span></span> <span data-ttu-id="aa197-182">Hello 권한 부여 코드 toohello 응용 프로그램의 회신 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-182">It returns hello authorization code toohello Reply URL of your application.</span></span> <span data-ttu-id="aa197-183">Hello에 따라 response_mode를, 어느 보냅니다 다시 hello 데이터 게시 데이터 또는 쿼리 문자열에 Azure AD가 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-183">Depending on hello requested response_mode, Azure AD either sends back hello data in query string or as post data.</span></span>

<span data-ttu-id="aa197-184">Open ID Connect 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="aa197-184">An example Open ID Connect response is:</span></span>

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a><span data-ttu-id="aa197-185">토큰 요청(OAuth2.0 코드 부여 흐름)</span><span class="sxs-lookup"><span data-stu-id="aa197-185">Token request (OAuth2.0 Code Grant Flow)</span></span>
<span data-ttu-id="aa197-186">이제 응용 프로그램이 Azure AD에서 인증 코드 hello 받은 경우 시간 tooget hello 액세스 토큰에 대 한 Azure 리소스 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-186">Now that your application has received hello authorization code from Azure AD, it is time tooget hello access token for Azure Resource Manager.</span></span>  <span data-ttu-id="aa197-187">Oauth 2.0 코드 부여 토큰 요청 toohello Azure AD 토큰 끝점을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-187">Post an OAuth2.0 Code Grant Token Request toohello Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="aa197-188">이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [hello 인증 코드를 사용 하 여](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-188">hello query string parameters that are available for this request are described in hello [use hello authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) topic.</span></span>

<span data-ttu-id="aa197-189">다음 예제는 hello 암호 자격 증명을 가진 코드 부여 토큰에 대 한 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-189">hello following example shows a request for code grant token with password credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="aa197-190">자격 증명 인증서를 사용할 때 JSON 웹 토큰 (JWT) 및 기호 (RSA SHA256) hello 응용 프로그램의 인증서 자격 증명의 개인 키를 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-190">When working with certificate credentials, create a JSON Web Token (JWT) and sign (RSA SHA256) using hello private key of your application's certificate credential.</span></span> <span data-ttu-id="aa197-191">hello hello 토큰에 대 한 클레임 형식에 표시 되어 [JWT 토큰 클레임](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-191">hello claim types for hello token are shown in [JWT token claims](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims).</span></span> <span data-ttu-id="aa197-192">참조를 위해 참조 hello [Active Directory 인증 라이브러리 (.NET) 코드](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign 클라이언트 어설션 JWT 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-192">For reference, see hello [Active Directory Auth Library (.NET) code](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign Client Assertion JWT tokens.</span></span>

<span data-ttu-id="aa197-193">Hello 참조 [Open ID 연결 사양](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) 클라이언트 인증에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-193">See hello [Open ID Connect spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) for details on client authentication.</span></span>

<span data-ttu-id="aa197-194">다음 예제는 hello 인증서 자격 증명 코드 부여 토큰에 대 한 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-194">hello following example shows a request for code grant token with certificate credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

<span data-ttu-id="aa197-195">코드 부여 토큰에 대한 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="aa197-195">An example response for code grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a><span data-ttu-id="aa197-196">코드 부여 토큰 응답 처리</span><span class="sxs-lookup"><span data-stu-id="aa197-196">Handle code grant token response</span></span>
<span data-ttu-id="aa197-197">성공적인 토큰 응답 Azure 리소스 관리자에 대 한 액세스 토큰 hello (사용자 + 응용 프로그램)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-197">A successful token response contains hello (user + app) access token for Azure Resource Manager.</span></span> <span data-ttu-id="aa197-198">응용 프로그램에서이 액세스 토큰 tooaccess 리소스 관리자 hello 사용자 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-198">Your application uses this access token tooaccess Resource Manager on behalf of hello user.</span></span> <span data-ttu-id="aa197-199">hello Azure AD에서 발급 하는 액세스 토큰의 수명은 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-199">hello lifetime of access tokens issued by Azure AD is one hour.</span></span> <span data-ttu-id="aa197-200">웹 응용 프로그램 toorenew hello (사용자 + 응용 프로그램) 액세스 토큰이 필요 함을 가능성이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-200">It is unlikely that your web application needs toorenew hello (user + app) access token.</span></span> <span data-ttu-id="aa197-201">Toorenew hello 액세스 토큰을 해야 하는 경우 응용 프로그램 hello 토큰 응답에서 부여 하는 hello 새로 고침 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-201">If it needs toorenew hello access token, use hello refresh token that your application receives in hello token response.</span></span> <span data-ttu-id="aa197-202">Oauth 2.0 토큰 요청 toohello Azure AD 토큰 끝점을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-202">Post an OAuth2.0 Token Request toohello Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="aa197-203">hello 매개 변수 toouse hello 새로 고침 요청에 설명 되어 있음 [hello 액세스 토큰 새로 고침](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-203">hello parameters toouse with hello refresh request are described in [refreshing hello access token](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).</span></span>

<span data-ttu-id="aa197-204">hello 다음 보여 주는 예제 toouse hello 새로 고침 하는 토큰:</span><span class="sxs-lookup"><span data-stu-id="aa197-204">hello following example shows how toouse hello refresh token:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="aa197-205">새로 고침 토큰이 사용 되는 tooget 새 액세스 토큰에 대 한 Azure 리소스 관리자를 사용할 수 있지만 응용 프로그램에서 오프 라인 액세스에 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-205">Although refresh tokens can be used tooget new access tokens for Azure Resource Manager, they are not suitable for offline access by your application.</span></span> <span data-ttu-id="aa197-206">hello 새로 고침 토큰 수명을 제한 되며 새로 고침 토큰은 바인딩된 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-206">hello refresh tokens lifetime is limited, and refresh tokens are bound toohello user.</span></span> <span data-ttu-id="aa197-207">Hello 사용자가 조직 hello를 hello 새로 고침 토큰을 사용 하 여 hello 응용 프로그램 액세스를 잃습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-207">If hello user leaves hello organization, hello application using hello refresh token loses access.</span></span> <span data-ttu-id="aa197-208">이 방법을 사용 되는 응용 프로그램에 적합 하지 팀 toomanage 하 여 Azure 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-208">This approach isn't suitable for applications that are used by teams toomanage their Azure resources.</span></span>

## <a name="check-if-user-can-assign-access-toosubscription"></a><span data-ttu-id="aa197-209">사용자 액세스 toosubscription 할당할 수 확인</span><span class="sxs-lookup"><span data-stu-id="aa197-209">Check if user can assign access toosubscription</span></span>
<span data-ttu-id="aa197-210">이제 응용 프로그램에 hello 사용자 대신 토큰 tooaccess Azure 리소스 관리자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-210">Your application now has a token tooaccess Azure Resource Manager on behalf of hello user.</span></span> <span data-ttu-id="aa197-211">hello 다음 단계는 tooconnect 앱 toohello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-211">hello next step is tooconnect your app toohello subscription.</span></span> <span data-ttu-id="aa197-212">에 연결한 후 앱 hello 사용자를 사용할 수 없는 경우에 해당 구독을 관리할 수 (장기 오프 라인 액세스).</span><span class="sxs-lookup"><span data-stu-id="aa197-212">After connecting, your app can manage those subscriptions even when hello user isn't present (long-term offline access).</span></span>

<span data-ttu-id="aa197-213">각 구독 tooconnect 호출 hello [목록 사용 권한 리소스 관리자](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine hello 사용자의 hello 구독에 대 한 액세스 관리 권한이 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="aa197-213">For each subscription tooconnect, call hello [Resource Manager list permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine whether hello user has access management rights for hello subscription.</span></span>

<span data-ttu-id="aa197-214">hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) 메서드 hello ASP.NET MVC 샘플 응용 프로그램의이 호출을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-214">hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) method of hello ASP.NET MVC sample app implements this call.</span></span>

<span data-ttu-id="aa197-215">hello 방법을 예제와 다음 toorequest 구독에 대 한 사용자의 권한을 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-215">hello following example shows how toorequest a user's permissions on a subscription.</span></span> <span data-ttu-id="aa197-216">83cfe939-2402-4581-b761-4f59b0a041e4은 hello id hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-216">83cfe939-2402-4581-b761-4f59b0a041e4 is hello id of hello subscription.</span></span>

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

<span data-ttu-id="aa197-217">구독에 대 한 hello 응답 tooget 사용자의 권한의 예는.</span><span class="sxs-lookup"><span data-stu-id="aa197-217">An example of hello response tooget user's permissions on subscription is:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

<span data-ttu-id="aa197-218">hello 권한을 API 여러 사용 권한을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-218">hello permissions API returns multiple permissions.</span></span> <span data-ttu-id="aa197-219">각 사용 권한은 허용되는 작업(actions) 및 허용되지 않는 작업(notactions)으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-219">Each permission consists of allowed actions (actions) and disallowed actions (notactions).</span></span> <span data-ttu-id="aa197-220">작업에 대 한 사용 권한의 작업 목록 허용 hello 있고 hello 사용자가 없거나 해당 권한의 hello notactions 목록의 tooperform 해당 작업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-220">If an action is present in hello allowed actions list of any permission and not present in hello notactions list of that permission, hello user is allowed tooperform that action.</span></span> <span data-ttu-id="aa197-221">**microsoft.authorization/roleassignments/write** hello 동작 하는 액세스 관리 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-221">**microsoft.authorization/roleassignments/write** is hello action that that grants access management rights.</span></span> <span data-ttu-id="aa197-222">응용 프로그램 hello 작업 및 각 사용 권한의 notactions에서이 동작 문자열에 정규식 일치에 대 한 사용 권한 결과 toolook hello 구문 분석 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-222">Your application must parse hello permissions result toolook for a regex match on this action string in hello actions and notactions of each permission.</span></span>

## <a name="get-app-only-access-token"></a><span data-ttu-id="aa197-223">앱 전용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-223">Get app-only access token</span></span>
<span data-ttu-id="aa197-224">이제 알 수 hello 사용자 액세스 toohello Azure 구독을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-224">Now, you know if hello user can assign access toohello Azure subscription.</span></span> <span data-ttu-id="aa197-225">hello 다음 단계는.</span><span class="sxs-lookup"><span data-stu-id="aa197-225">hello next steps are:</span></span>

1. <span data-ttu-id="aa197-226">Hello 적절 한 RBAC 역할 tooyour 응용 프로그램의 id hello 구독에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-226">Assign hello appropriate RBAC role tooyour application's identity on hello subscription.</span></span>
2. <span data-ttu-id="aa197-227">Hello 구독에 대 한 사용 권한의 hello 응용 프로그램의 쿼리를 통해 또는 응용 프로그램 전용 토큰을 사용 하 여 리소스 관리자에 액세스 하 여 hello 액세스 할당의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-227">Validate hello access assignment by querying for hello Application's permission on hello subscription or by accessing Resource Manager using app-only token.</span></span>
3. <span data-ttu-id="aa197-228">Hello hello 구독의 id를 유지 하면 응용 프로그램 "연결 된 구독" 데이터 구조의-레코드 hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-228">Record hello connection in your applications "connected subscriptions" data structure - persisting hello id of hello subscription.</span></span>

<span data-ttu-id="aa197-229">Hello 첫 번째 단계에서 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-229">Let's look closer at hello first step.</span></span> <span data-ttu-id="aa197-230">tooassign hello 적절 한 RBAC 역할 toohello 응용 프로그램의 id를 있습니다 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-230">tooassign hello appropriate RBAC role toohello application's identity, you must determine:</span></span>

* <span data-ttu-id="aa197-231">hello 사용자의 Azure Active Directory에서 응용 프로그램의 id의 hello 개체 id</span><span class="sxs-lookup"><span data-stu-id="aa197-231">hello object id of your application's identity in hello user's Azure Active Directory</span></span>
* <span data-ttu-id="aa197-232">응용 프로그램에 필요한 hello 구독에 대해 hello RBAC 역할의 hello 식별자</span><span class="sxs-lookup"><span data-stu-id="aa197-232">hello identifier of hello RBAC role that your application requires on hello subscription</span></span>

<span data-ttu-id="aa197-233">응용 프로그램이 Azure AD에서 사용자를 인증할 때 응용 프로그램에 대한 서비스 주체 개체가 해당 Azure AD에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-233">When your application authenticates a user from an Azure AD, it creates a service principal object for your application in that Azure AD.</span></span> <span data-ttu-id="aa197-234">Azure는 RBAC 역할 toobe 할당 한 Azure 리소스에 대 한 직접 액세스 toocorresponding 응용 프로그램 toogrant tooservice 주체 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-234">Azure allows RBAC roles toobe assigned tooservice principals toogrant direct access toocorresponding applications on Azure resources.</span></span> <span data-ttu-id="aa197-235">이 작업을 정확 하 게 toodo 했는데도 기능.</span><span class="sxs-lookup"><span data-stu-id="aa197-235">This action is exactly what we wish toodo.</span></span> <span data-ttu-id="aa197-236">쿼리 hello Azure AD Graph API toodetermine hello 식별자 hello 로그인 한 사용자의 응용 프로그램의 hello 서비스 사용자의 Azure AD의입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-236">Query hello Azure AD Graph API toodetermine hello identifier of hello service principal of your application in hello signed-in user's Azure AD.</span></span>

<span data-ttu-id="aa197-237">액세스 토큰에 대 한 Azure 리소스 관리자와 하면 새 액세스 토큰 toocall hello Azure AD Graph API를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-237">You only have an access token for Azure Resource Manager - you need a new access token toocall hello Azure AD Graph API.</span></span> <span data-ttu-id="aa197-238">Azure AD에서 모든 응용 프로그램에 권한이 tooquery 서비스 사용자 개체는 자체 응용 프로그램 전용 액세스 토큰은 충분 한 있으므로.</span><span class="sxs-lookup"><span data-stu-id="aa197-238">Every application in Azure AD has permission tooquery its own service principal object, so an app-only access token is sufficient.</span></span>

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a><span data-ttu-id="aa197-239">Azure AD Graph API에 대한 응용 프로그램 전용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-239">Get app-only access token for Azure AD Graph API</span></span>
<span data-ttu-id="aa197-240">tooauthenticate 앱과 get 토큰 tooAzure AD Graph API 발급 한 클라이언트 자격 증명 부여 oauth 2.0 흐름 토큰 요청 tooAzure AD 토큰 끝점 (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/토큰**).</span><span class="sxs-lookup"><span data-stu-id="aa197-240">tooauthenticate your app and get a token tooAzure AD Graph API, issue a Client Credential Grant OAuth2.0 flow token request tooAzure AD token endpoint (**https://login.microsoftonline.com/{directory_domain_name}/OAuth2/Token**).</span></span>

<span data-ttu-id="aa197-241">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) ASP.net MVC 샘플 응용 앱 전용 액세스를 사용 하 여 Graph API에 대 한 토큰을 가져옵니다 hello 방식의.NET에 대 한 Active Directory 인증 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-241">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) method of hello ASP.net MVC sample application gets an app-only access token for Graph API using hello Active Directory Authentication Library for .NET.</span></span>

<span data-ttu-id="aa197-242">이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [액세스 토큰 요청](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-242">hello query string parameters that are available for this request are described in hello [Request an Access Token](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) topic.</span></span>

<span data-ttu-id="aa197-243">클라이언트 자격 증명 부여 토큰에 대한 요청 예제:</span><span class="sxs-lookup"><span data-stu-id="aa197-243">An example request for client credential grant token:</span></span>

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

<span data-ttu-id="aa197-244">클라이언트 자격 증명 부여 토큰에 대한 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="aa197-244">An example response for client credential grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a><span data-ttu-id="aa197-245">사용자 Azure AD에서 응용 프로그램 서비스 주체의 ObjectId 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-245">Get ObjectId of application service principal in user Azure AD</span></span>
<span data-ttu-id="aa197-246">이제 hello 앱 전용 액세스 토큰 tooquery hello를 사용 하 여 [서비스 사용자를 Azure AD 그래프](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API toodetermine hello hello 디렉터리에 hello 응용 프로그램의 서비스 사용자의 개체 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-246">Now, use hello app-only access token tooquery hello [Azure AD Graph Service Principals](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API toodetermine hello Object Id of hello application's service principal in hello directory.</span></span>

<span data-ttu-id="aa197-247">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) 메서드 hello ASP.net MVC 샘플 응용 프로그램의이 호출을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-247">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) method of hello ASP.net MVC sample application implements this call.</span></span>

<span data-ttu-id="aa197-248">hello 방법을 예제와 다음 toorequest 응용 프로그램의 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-248">hello following example shows how toorequest an application's service principal.</span></span> <span data-ttu-id="aa197-249">a0448380-c346-4f9f-b897-c18733de9394는 hello 응용 프로그램의 hello 클라이언트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-249">a0448380-c346-4f9f-b897-c18733de9394 is hello client id of hello application.</span></span>

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

<span data-ttu-id="aa197-250">hello 다음 보여 주는 예제 응용 프로그램의 서비스에 대 한 응답 toohello 요청 주</span><span class="sxs-lookup"><span data-stu-id="aa197-250">hello following example shows a response toohello request for an application's service principal</span></span>

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a><span data-ttu-id="aa197-251">Azure RBAC 역할 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-251">Get Azure RBAC role identifier</span></span>
<span data-ttu-id="aa197-252">tooassign hello 적절 한 RBAC 역할 tooyour 서비스 사용자, hello Azure RBAC 역할의 hello 식별자를 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-252">tooassign hello appropriate RBAC role tooyour service principal, you must determine hello identifier of hello Azure RBAC role.</span></span>

<span data-ttu-id="aa197-253">hello RBAC에 대해 올바른 역할 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="aa197-253">hello right RBAC role for your application:</span></span>

* <span data-ttu-id="aa197-254">응용 프로그램 변경 하지 않고 hello 구독을 모니터링 하는 경우에 hello 구독에 대해 판독기 권한만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-254">If your application only monitors hello subscription, without making any changes, it requires only reader permissions on hello subscription.</span></span> <span data-ttu-id="aa197-255">Hello 할당 **판독기** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-255">Assign hello **Reader** role.</span></span>
* <span data-ttu-id="aa197-256">응용 프로그램에 Azure hello 구독을 만들기/수정/삭제 하는 엔터티를 관리 하는 경우 hello 참가자 권한 중 하나가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-256">If your application manages Azure hello subscription, creating/modifying/deleting entities, it requires one of hello contributor permissions.</span></span>
  * <span data-ttu-id="aa197-257">특정 유형의 리소스를 toomanage 할당 hello 리소스별 참가자 역할 (가상 컴퓨터 참가자, 가상 네트워크 참가자, 저장소 계정 참가자 등)</span><span class="sxs-lookup"><span data-stu-id="aa197-257">toomanage a particular type of resource, assign hello resource-specific contributor roles (Virtual Machine Contributor, Virtual Network Contributor, Storage Account Contributor, etc.)</span></span>
  * <span data-ttu-id="aa197-258">toomanage 모든 리소스 종류, 할당 hello **참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-258">toomanage any resource type, assign hello **Contributor** role.</span></span>

<span data-ttu-id="aa197-259">응용 프로그램에 대 한 역할 할당 hello 표시 toousers 이므로 선택 hello 최소 필수 권한.</span><span class="sxs-lookup"><span data-stu-id="aa197-259">hello role assignment for your application is visible toousers, so select hello least-required privilege.</span></span>

<span data-ttu-id="aa197-260">Hello 호출 [리소스 관리자 역할 정의 API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) 모든 Azure RBAC 역할 및 검색 반복 hello 결과 toofind hello toolist 이름으로 역할 정의 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-260">Call hello [Resource Manager role definition API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist all Azure RBAC roles and search then iterate over hello result toofind hello desired role definition by name.</span></span>

<span data-ttu-id="aa197-261">hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) 메서드 hello ASP.net MVC 샘플 응용 프로그램의이 호출을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-261">hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) method of hello ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="aa197-262">hello 다음 요청 예제와 방법을 tooget Azure RBAC 역할 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-262">hello following request example shows how tooget Azure RBAC role identifier.</span></span> <span data-ttu-id="aa197-263">09cbd307-aa71-4aca-b346-5f253e6e3ebb은 hello id hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-263">09cbd307-aa71-4aca-b346-5f253e6e3ebb is hello id of hello subscription.</span></span>

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

<span data-ttu-id="aa197-264">hello 응답 형식에 따라 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-264">hello response is in hello following format:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

<span data-ttu-id="aa197-265">Toocall 필요 하지 않습니다이 API는 지속적으로.</span><span class="sxs-lookup"><span data-stu-id="aa197-265">You do not need toocall this API on an ongoing basis.</span></span> <span data-ttu-id="aa197-266">확인 한 후 hello 역할 정의의 잘 알려진 GUID hello,으로 hello 역할 정의 id를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-266">Once you've determined hello well-known GUID of hello role definition, you can construct hello role definition id as:</span></span>

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

<span data-ttu-id="aa197-267">다음은 자주 사용 되는 기본 제공 역할의 hello 잘 알려진 guid가입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-267">Here are hello well-known guids of commonly used built-in roles:</span></span>

| <span data-ttu-id="aa197-268">역할</span><span class="sxs-lookup"><span data-stu-id="aa197-268">Role</span></span> | <span data-ttu-id="aa197-269">Guid</span><span class="sxs-lookup"><span data-stu-id="aa197-269">Guid</span></span> |
| --- | --- |
| <span data-ttu-id="aa197-270">독자</span><span class="sxs-lookup"><span data-stu-id="aa197-270">Reader</span></span> |<span data-ttu-id="aa197-271">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="aa197-271">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |
| <span data-ttu-id="aa197-272">참가자</span><span class="sxs-lookup"><span data-stu-id="aa197-272">Contributor</span></span> |<span data-ttu-id="aa197-273">b24988ac-6180-42a0-ab88-20f7382dd24c</span><span class="sxs-lookup"><span data-stu-id="aa197-273">b24988ac-6180-42a0-ab88-20f7382dd24c</span></span> |
| <span data-ttu-id="aa197-274">가상 컴퓨터 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-274">Virtual Machine Contributor</span></span> |<span data-ttu-id="aa197-275">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span><span class="sxs-lookup"><span data-stu-id="aa197-275">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span></span> |
| <span data-ttu-id="aa197-276">가상 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-276">Virtual Network Contributor</span></span> |<span data-ttu-id="aa197-277">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span><span class="sxs-lookup"><span data-stu-id="aa197-277">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span></span> |
| <span data-ttu-id="aa197-278">저장소 계정 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-278">Storage Account Contributor</span></span> |<span data-ttu-id="aa197-279">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span><span class="sxs-lookup"><span data-stu-id="aa197-279">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span></span> |
| <span data-ttu-id="aa197-280">웹 사이트 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-280">Website Contributor</span></span> |<span data-ttu-id="aa197-281">de139f84-1756-47ae-9be6-808fbbe84772</span><span class="sxs-lookup"><span data-stu-id="aa197-281">de139f84-1756-47ae-9be6-808fbbe84772</span></span> |
| <span data-ttu-id="aa197-282">웹 계획 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-282">Web Plan Contributor</span></span> |<span data-ttu-id="aa197-283">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span><span class="sxs-lookup"><span data-stu-id="aa197-283">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span></span> |
| <span data-ttu-id="aa197-284">SQL Server 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-284">SQL Server Contributor</span></span> |<span data-ttu-id="aa197-285">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span><span class="sxs-lookup"><span data-stu-id="aa197-285">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span></span> |
| <span data-ttu-id="aa197-286">SQL DB 참여자</span><span class="sxs-lookup"><span data-stu-id="aa197-286">SQL DB Contributor</span></span> |<span data-ttu-id="aa197-287">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span><span class="sxs-lookup"><span data-stu-id="aa197-287">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span></span> |

### <a name="assign-rbac-role-tooapplication"></a><span data-ttu-id="aa197-288">RBAC 역할 tooapplication 할당</span><span class="sxs-lookup"><span data-stu-id="aa197-288">Assign RBAC role tooapplication</span></span>
<span data-ttu-id="aa197-289">Hello를 사용 하 여 tooassign hello 적절 한 RBAC 역할 tooyour 서비스 사용자를 원하는 대로 [리소스 관리자 역할 할당을 만들](https://docs.microsoft.com/rest/api/authorization/roleassignments) API입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-289">You have everything you need tooassign hello appropriate RBAC role tooyour service principal by using hello [Resource Manager create role assignment](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.</span></span>

<span data-ttu-id="aa197-290">hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) 메서드 hello ASP.net MVC 샘플 응용 프로그램의이 호출을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-290">hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) method of hello ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="aa197-291">예제 요청 tooassign RBAC 역할 tooapplication의:</span><span class="sxs-lookup"><span data-stu-id="aa197-291">An example request tooassign RBAC role tooapplication:</span></span>

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

<span data-ttu-id="aa197-292">Hello 요청에 다음 값에는 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-292">In hello request, hello following values are used:</span></span>

| <span data-ttu-id="aa197-293">Guid</span><span class="sxs-lookup"><span data-stu-id="aa197-293">Guid</span></span> | <span data-ttu-id="aa197-294">설명</span><span class="sxs-lookup"><span data-stu-id="aa197-294">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa197-295">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span><span class="sxs-lookup"><span data-stu-id="aa197-295">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span></span> |<span data-ttu-id="aa197-296">hello 구독의 hello id</span><span class="sxs-lookup"><span data-stu-id="aa197-296">hello id of hello subscription</span></span> |
| <span data-ttu-id="aa197-297">c3097b31-7309-4c59-b4e3-770f8406bad2</span><span class="sxs-lookup"><span data-stu-id="aa197-297">c3097b31-7309-4c59-b4e3-770f8406bad2</span></span> |<span data-ttu-id="aa197-298">hello 응용 프로그램의 hello 서비스 사용자의 hello 개체 id</span><span class="sxs-lookup"><span data-stu-id="aa197-298">hello object id of hello service principal of hello application</span></span> |
| <span data-ttu-id="aa197-299">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="aa197-299">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |<span data-ttu-id="aa197-300">hello 읽기 역할의 hello id</span><span class="sxs-lookup"><span data-stu-id="aa197-300">hello id of hello reader role</span></span> |
| <span data-ttu-id="aa197-301">4f87261d-2816-465d-8311-70a27558df4c</span><span class="sxs-lookup"><span data-stu-id="aa197-301">4f87261d-2816-465d-8311-70a27558df4c</span></span> |<span data-ttu-id="aa197-302">만든 hello 새 역할 할당에 대 한 새 guid</span><span class="sxs-lookup"><span data-stu-id="aa197-302">a new guid created for hello new role assignment</span></span> |

<span data-ttu-id="aa197-303">hello 응답 형식에 따라 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-303">hello response is in hello following format:</span></span>

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a><span data-ttu-id="aa197-304">Azure Resource Manager에 대한 응용 프로그램 전용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-304">Get app-only access token for Azure Resource Manager</span></span>
<span data-ttu-id="aa197-305">toovalidate hello 구독에서 해당 앱은 필요한 hello 액세스할, 응용 프로그램 전용 토큰을 사용 하 여 hello 구독에서 테스트 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-305">toovalidate that app has hello desired access on hello subscription, perform a test task on hello subscription using an app-only token.</span></span>

<span data-ttu-id="aa197-306">응용 프로그램 전용 액세스 토큰을 tooget 섹션에서 지침에 따라 [Azure AD Graph API에 대 한 앱 전용 액세스 토큰 가져오기](#app-azure-ad-graph), hello 리소스 매개 변수에 대 한 다른 값으로:</span><span class="sxs-lookup"><span data-stu-id="aa197-306">tooget an app-only access token, follow instructions from section [Get app-only access token for Azure AD Graph API](#app-azure-ad-graph), with a different value for hello resource parameter:</span></span>

    https://management.core.windows.net/

<span data-ttu-id="aa197-307">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) ASP.NET MVC 샘플 응용 앱 전용 액세스를 사용 하 여 Azure 리소스 관리자에 대 한 토큰을 가져옵니다 hello 방식의.net에 대 한 Active Directory 인증 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-307">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of hello ASP.NET MVC sample application gets an app-only access token for Azure Resource Manager using hello Active Directory Authentication Library for .net.</span></span>

#### <a name="get-applications-permissions-on-subscription"></a><span data-ttu-id="aa197-308">구독에 대한 응용 프로그램의 권한 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa197-308">Get Application's Permissions on Subscription</span></span>
<span data-ttu-id="aa197-309">Azure 구독에 대 한 액세스를 원하는 응용 프로그램에 hello toocheck, hello를 호출할 수도 있습니다 [리소스 관리자 사용 권한을](https://docs.microsoft.com/rest/api/authorization/permissions) API입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-309">toocheck that your application has hello desired access on an Azure subscription, you may also call hello [Resource Manager Permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API.</span></span> <span data-ttu-id="aa197-310">이 방법은 비슷한 toohow hello 사용자에 게 hello 구독에 대 한 액세스 관리 권한이 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-310">This approach is similar toohow you determined whether hello user has Access Management rights for hello subscription.</span></span> <span data-ttu-id="aa197-311">그러나이 이번에는 hello 이전 단계에서 받은 hello 응용 프로그램 전용 액세스 토큰으로 hello 권한을 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-311">However, this time, call hello permissions API with hello app-only access token that you received in hello previous step.</span></span>

<span data-ttu-id="aa197-312">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) 메서드 hello ASP.NET MVC 샘플 응용 프로그램의이 호출을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-312">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of hello ASP.NET MVC sample app implements this call.</span></span>

## <a name="manage-connected-subscriptions"></a><span data-ttu-id="aa197-313">연결된 구독 관리</span><span class="sxs-lookup"><span data-stu-id="aa197-313">Manage connected subscriptions</span></span>
<span data-ttu-id="aa197-314">적절 한 RBAC 역할 hello hello 구독에서 tooyour 응용 프로그램의 서비스 사용자에 게 할당 되 면 응용 프로그램 수 유지 모니터링/관리 Azure 리소스 관리자에 대 한 앱 전용 액세스 토큰을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-314">When hello appropriate RBAC role is assigned tooyour application's service principal on hello subscription, your application can keep monitoring/managing it using app-only access tokens for Azure Resource Manager.</span></span>

<span data-ttu-id="aa197-315">구독 소유자 hello 클래식 포털 또는 명령줄 도구, 응용 프로그램을 사용 하 여 응용 프로그램의 역할 할당을 제거 하는 경우 더 이상 수 tooaccess 해당 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-315">If a subscription owner removes your application's role assignment using hello classic portal or command-line tools, your application is no longer able tooaccess that subscription.</span></span> <span data-ttu-id="aa197-316">이 경우 hello 구독과 hello 연결 hello 응용 프로그램 외부에서 손상 되었습니다 hello 사용자에 게 알리는 하 고 hello 연결 옵션 너무 "복구"으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-316">In that case, you should notify hello user that hello connection with hello subscription was severed from outside hello application and give them an option too"repair" hello connection.</span></span> <span data-ttu-id="aa197-317">"복구" 다시 오프 라인으로 삭제 된 hello 역할 할당을 만들면가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-317">"Repair" would simply re-create hello role assignment that was deleted offline.</span></span>

<span data-ttu-id="aa197-318">Hello 사용자 tooconnect 구독 tooyour 응용 프로그램을 사용 하도록 설정한 것 처럼 너무 hello 사용자 toodisconnect 구독 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-318">Just as you enabled hello user tooconnect subscriptions tooyour application, you must allow hello user toodisconnect subscriptions too.</span></span> <span data-ttu-id="aa197-319">액세스 관리의 관점에서 hello 응용 프로그램의 서비스 사용자에 미치는 hello 구독 hello 역할 할당을 제거 하는 수단을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-319">From an access management point of view, disconnect means removing hello role assignment that hello application's service principal has on hello subscription.</span></span> <span data-ttu-id="aa197-320">필요에 따라 hello 구독에 대 한 hello 응용 프로그램의 모든 상태는 너무 제거 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-320">Optionally, any state in hello application for hello subscription might be removed too.</span></span>
<span data-ttu-id="aa197-321">Hello 구독에 대 한 액세스 관리 권한 가진 사용자만 수 toodisconnect hello 구독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-321">Only users with access management permission on hello subscription are able toodisconnect hello subscription.</span></span>

<span data-ttu-id="aa197-322">hello [RevokeRoleFromServicePrincipalOnSubscription 메서드](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) 샘플 응용 프로그램의 ASP.net MVC hello이이 호출을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-322">hello [RevokeRoleFromServicePrincipalOnSubscription method](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) of hello ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="aa197-323">이와 같이 사용자는 이제 응용 프로그램을 사용하여 쉽게 Azure 구독을 연결 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa197-323">That's it - users can now easily connect and manage their Azure subscriptions with your application.</span></span>
