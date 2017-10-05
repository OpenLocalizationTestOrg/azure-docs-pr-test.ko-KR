---
title: "Azure Active Directory 인증 및 Resource Manager | Microsoft Docs"
description: "앱을 다른 Azure 구독과 통합하기 위한 Azure Resource Manager API 및 Azure Active Directory를 사용한 권한 부여 개발자 가이드."
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
ms.openlocfilehash: 7830dc4774652f4d108e98660dce3bcea7b32d05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-resource-manager-authentication-api-to-access-subscriptions"></a><span data-ttu-id="4f419-103">Resource Manager 인증 API를 사용하여 구독에 액세스</span><span class="sxs-lookup"><span data-stu-id="4f419-103">Use Resource Manager authentication API to access subscriptions</span></span>
## <a name="introduction"></a><span data-ttu-id="4f419-104">소개</span><span class="sxs-lookup"><span data-stu-id="4f419-104">Introduction</span></span>
<span data-ttu-id="4f419-105">고객의 Azure 리소스를 관리하는 앱을 만들어야 하는 소프트웨어 개발자의 경우 이 항목은 Azure Resource Manager API를 사용하여 인증하고 다른 구독에 있는 리소스에 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-105">If you are a software developer who needs to create an app that manages customer's Azure resources, this topic shows you how to authenticate with the Azure Resource Manager APIs and gain access to resources in other subscriptions.</span></span>

<span data-ttu-id="4f419-106">앱에서 두 가지 방법으로 Resource Manager API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-106">Your app can access the Resource Manager APIs in couple of ways:</span></span>

1. <span data-ttu-id="4f419-107">**사용자 + 앱 액세스**: 로그인한 사용자를 대신하여 리소스에 액세스하는 앱.</span><span class="sxs-lookup"><span data-stu-id="4f419-107">**User + app access**: for apps that access resources on behalf of a signed-in user.</span></span> <span data-ttu-id="4f419-108">이 방법은 웹앱 및 명령줄 도구 등 Azure 리소스의 "대화형 관리"만 처리하는 앱에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-108">This approach works for apps, such as web apps and command-line tools, that deal with only "interactive management" of Azure resources.</span></span>
2. <span data-ttu-id="4f419-109">**앱 전용 액세스**: 디먼 서비스 및 예약된 작업을 실행하는 앱.</span><span class="sxs-lookup"><span data-stu-id="4f419-109">**App-only access**: for apps that run daemon services and scheduled jobs.</span></span> <span data-ttu-id="4f419-110">리소스에 대한 직접 액세스 권한을 앱의 ID에 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-110">The app's identity is granted direct access to the resources.</span></span> <span data-ttu-id="4f419-111">이 방법은 Azure에 대한 장기적인 헤드리스 액세스(자동)가 필요한 앱에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-111">This approach works for apps that need long-term headless (unattended) access to Azure.</span></span>

<span data-ttu-id="4f419-112">이 항목에서는 이러한 권한 부여 방법을 모두 채택하는 앱을 만드는 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-112">This topic provides step-by-step instructions to create an app that employs both these authorization methods.</span></span> <span data-ttu-id="4f419-113">REST API 또는 C#을 사용하여 각 단계를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-113">It shows how to perform each step with REST API or C#.</span></span> <span data-ttu-id="4f419-114">전체 ASP.NET MVC 응용 프로그램은 [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-114">The complete ASP.NET MVC application is available at [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).</span></span>

## <a name="what-the-web-app-does"></a><span data-ttu-id="4f419-115">웹앱이 수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="4f419-115">What the web app does</span></span>
<span data-ttu-id="4f419-116">웹앱:</span><span class="sxs-lookup"><span data-stu-id="4f419-116">The web app:</span></span>

1. <span data-ttu-id="4f419-117">Azure 사용자를 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-117">Signs-in an Azure user.</span></span>
2. <span data-ttu-id="4f419-118">사용자에게 Resource Manager에 대한 웹앱 액세스 권한을 부여하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-118">Asks user to grant the web app access to Resource Manager.</span></span>
3. <span data-ttu-id="4f419-119">Resource Manager에 액세스하기 위한 사용자 + 앱 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-119">Gets user + app access token for accessing Resource Manager.</span></span>
4. <span data-ttu-id="4f419-120">토큰(3단계)을 사용하여 Resource Manager를 호출하고 앱의 서비스 주체를 구독에 있는 역할에 할당합니다. 그러면 앱에 구독에 대한 장기적인 액세스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-120">Uses token (from step 3) to call Resource Manager and assign the app's service principal to a role in the subscription, which gives the app long-term access to the subscription.</span></span>
5. <span data-ttu-id="4f419-121">앱 전용 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-121">Gets app-only access token.</span></span>
6. <span data-ttu-id="4f419-122">토큰(5단계)을 사용하여 Resource Manager를 통해 구독에 있는 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-122">Uses token (from step 5) to manage resources in the subscription through Resource Manager.</span></span>

<span data-ttu-id="4f419-123">다음은 웹 응용 프로그램의 종단 간 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-123">Here's the end-to-end flow of the web application.</span></span>

![Resource Manager 인증 흐름](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

<span data-ttu-id="4f419-125">사용자는 사용하려는 구독에 대한 구독 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-125">As a user, you provide the subscription id for the subscription you want to use:</span></span>

![구독 ID 제공](./media/resource-manager-api-authentication/sample-ux-1.png)

<span data-ttu-id="4f419-127">로그인에 사용할 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-127">Select the account to use for logging in.</span></span>

![계정 선택](./media/resource-manager-api-authentication/sample-ux-2.png)

<span data-ttu-id="4f419-129">자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-129">Provide your credentials.</span></span>

![자격 증명 제공](./media/resource-manager-api-authentication/sample-ux-3.png)

<span data-ttu-id="4f419-131">Azure 구독에 대한 앱 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-131">Grant the app access to your Azure subscriptions:</span></span>

![액세스 권한 부여](./media/resource-manager-api-authentication/sample-ux-4.png)

<span data-ttu-id="4f419-133">연결된 구독을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-133">Manage your connected subscriptions:</span></span>

![구독 연결](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a><span data-ttu-id="4f419-135">응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="4f419-135">Register application</span></span>
<span data-ttu-id="4f419-136">코딩을 시작하기 전에 Azure Active Directory(AD)를 사용하여 웹앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-136">Before you start coding, register your web app with Azure Active Directory (AD).</span></span> <span data-ttu-id="4f419-137">앱 등록은 Azure AD의 사용자 앱에 대한 중앙 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-137">The app registration creates a central identity for your app in Azure AD.</span></span> <span data-ttu-id="4f419-138">이는 응용 프로그램이 Azure Resource Manager API를 인증하고 액세스하는 데 사용하는 OAuth 클라이언트 ID, 회신 URL 및 자격 증명 등 응용 프로그램에 관한 기본 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-138">It holds basic information about your application like OAuth Client ID, Reply URLs, and credentials that your application uses to authenticate and access Azure Resource Manager APIs.</span></span> <span data-ttu-id="4f419-139">또한 앱 등록은 응용 프로그램이 사용자를 대신하여 Microsoft API에 액세스할 때 필요한 여러 가지 위임된 권한을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-139">The app registration also records the various delegated permissions that your application needs when accessing Microsoft APIs on behalf of the user.</span></span>

<span data-ttu-id="4f419-140">앱에서 다른 구독에 액세스하므로 다중 테넌트 응용 프로그램으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-140">Because your app accesses other subscription, you must configure it as a multi-tenant application.</span></span> <span data-ttu-id="4f419-141">유효성 검사를 통과하려면 Azure Active Directory와 연결된 도메인을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="4f419-141">To pass validation, provide a domain associated with your Azure Active Directory.</span></span> <span data-ttu-id="4f419-142">Azure Active Directory와 연결된 도메인을 보려면 [클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-142">To see the domains associated with your Azure Active Directory, log in to the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="4f419-143">Azure Active Directory를 선택한 다음 **도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-143">Select your Azure Active Directory and then select **Domains**.</span></span>

<span data-ttu-id="4f419-144">다음 예에서는 Azure PowerShell을 사용하여 앱을 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-144">The following example shows how to register the app by using Azure PowerShell.</span></span> <span data-ttu-id="4f419-145">이 명령이 작동하려면 최신 버전(2016년 8월)의 Azure PowerShell이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-145">You must have the latest version (August 2016) of Azure PowerShell for this command to work.</span></span>

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

<span data-ttu-id="4f419-146">AD 응용 프로그램으로 로그인하려면 응용 프로그램 ID 및 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-146">To log in as the AD application, you need the application id and password.</span></span> <span data-ttu-id="4f419-147">이전 명령에서 반환된 응용 프로그램 ID를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-147">To see the application id that is returned from the previous command, use:</span></span>

    $app.ApplicationId

<span data-ttu-id="4f419-148">다음 예에서는 Azure CLI를 사용하여 앱을 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-148">The following example shows how to register the app by using Azure CLI.</span></span>

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

<span data-ttu-id="4f419-149">결과에는 응용 프로그램으로 인증을 수행할 때 필요한 AppId가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-149">The results include the AppId, which you need when authenticating as the application.</span></span>

### <a name="optional-configuration---certificate-credential"></a><span data-ttu-id="4f419-150">선택적 구성 - 인증서 자격 증명</span><span class="sxs-lookup"><span data-stu-id="4f419-150">Optional configuration - certificate credential</span></span>
<span data-ttu-id="4f419-151">또한 Azure AD는 응용 프로그램에 대한 인증서 자격 증명을 지원합니다. 즉, 자체 서명된 인증서를 만들고 개인 키를 유지하고 Azure AD 응용 프로그램 등록에 공개 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-151">Azure AD also supports certificate credentials for applications: you create a self-signed cert, keep the private key, and add the public key to your Azure AD application registration.</span></span> <span data-ttu-id="4f419-152">인증을 위해 응용 프로그램이 개인 키를 사용하여서명한 Azure AD에 작은 페이로드를 보내면 Azure AD가 등록된 공개 키를 사용하여 서명의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-152">For authentication, your application sends a small payload to Azure AD signed using your private key, and Azure AD validates the signature using the public key that you registered.</span></span>

<span data-ttu-id="4f419-153">인증서를 사용하여 AD 앱을 만드는 방법에 대한 자세한 내용은 [Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) 또는 [Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f419-153">For information about creating an AD app with a certificate, see [Use Azure PowerShell to create a service principal to access resources](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) or [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).</span></span>

## <a name="get-tenant-id-from-subscription-id"></a><span data-ttu-id="4f419-154">구독 ID에서 테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-154">Get tenant id from subscription id</span></span>
<span data-ttu-id="4f419-155">Resource Manager를 호출하는 데 사용할 수 있는 토큰을 요청하기 위해서는 응용 프로그램이 Azure 구독을 호스트하는 Azure AD 테넌트의 테넌트 ID를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-155">To request a token that can be used to call Resource Manager, your application needs to know the tenant ID of the Azure AD tenant that hosts the Azure subscription.</span></span> <span data-ttu-id="4f419-156">대부분의 경우 사용자는 자신의 구독 ID를 알고 있지만 Azure Active Directory에 대한 테넌트 ID는 모를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-156">Most likely, your users know their subscription ids, but they might not know their tenant ids for Azure Active Directory.</span></span> <span data-ttu-id="4f419-157">사용자의 테넌트 ID를 얻으려면 사용자에게 구독 ID를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-157">To get the user's tenant id, ask the user for the subscription id.</span></span> <span data-ttu-id="4f419-158">구독에 대한 요청을 보낼 때 이 구독 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-158">Provide that subscription id when sending a request about the subscription:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

<span data-ttu-id="4f419-159">사용자가 아직 로그인하지 않았으므로 요청은 실패하지만 응답에서 테넌트 ID를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-159">The request fails because the user has not logged in yet, but you can retrieve the tenant id from the response.</span></span> <span data-ttu-id="4f419-160">이 예외에서 **WWW-Authenticate**에 대한 응답 헤더 값에서 테넌트 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-160">In that exception, retrieve the tenant id from the response header value for **WWW-Authenticate**.</span></span> <span data-ttu-id="4f419-161">이 구현은 [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) 메서드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-161">You see this implementation in the [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) method.</span></span>

## <a name="get-user--app-access-token"></a><span data-ttu-id="4f419-162">사용자 + 앱 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-162">Get user + app access token</span></span>
<span data-ttu-id="4f419-163">응용 프로그램이 OAuth 2.0 권한 부여 요청을 사용하여 사용자를 Azure AD로 리디렉션하여 사용자의 자격 증명을 인증하고 권한 부여 코드를 돌려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-163">Your application redirects the user to Azure AD with an OAuth 2.0 Authorize Request - to authenticate the user's credentials and get back an authorization code.</span></span> <span data-ttu-id="4f419-164">응용 프로그램은 권한 부여 코드를 사용하여 Resource Manager에 대한 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-164">Your application uses the authorization code to get an access token for Resource Manager.</span></span> <span data-ttu-id="4f419-165">[ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) 메서드는 권한 부여 요청을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-165">The [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) method creates the authorization request.</span></span>

<span data-ttu-id="4f419-166">이 항목은 사용자를 인증하는 REST API 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-166">This topic shows the REST API requests to authenticate the user.</span></span> <span data-ttu-id="4f419-167">또한 코드에서 인증을 수행하도록 도우미 라이브러리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-167">You can also use helper libraries to perform authentication in your code.</span></span> <span data-ttu-id="4f419-168">이러한 라이브러리에 대한 자세한 내용은 [Azure Active Directory 인증 라이브러리](../active-directory/active-directory-authentication-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f419-168">For more information about these libraries, see [Azure Active Directory Authentication Libraries](../active-directory/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="4f419-169">응용 프로그램에서 ID 관리를 통합하는 지침은 [Azure Active Directory 개발자 가이드](../active-directory/active-directory-developers-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f419-169">For guidance on integrating identity management in an application, see [Azure Active Directory developer's guide](../active-directory/active-directory-developers-guide.md).</span></span>

### <a name="auth-request-oauth-20"></a><span data-ttu-id="4f419-170">인증 요청(OAuth 2.0)</span><span class="sxs-lookup"><span data-stu-id="4f419-170">Auth request (OAuth 2.0)</span></span>
<span data-ttu-id="4f419-171">Azure AD 권한 부여 끝점에 대한 Open ID Connect/OAuth2.0 권한 부여 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-171">Issue an Open ID Connect/OAuth2.0 Authorize Request to the Azure AD Authorize endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

<span data-ttu-id="4f419-172">이 요청에 사용할 수 있는 쿼리 문자열 매개 변수는 [인증 코드 요청](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-172">The query string parameters that are available for this request are described in the [request an authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) topic.</span></span>

<span data-ttu-id="4f419-173">다음 예제에서는 OAuth2.0 권한 부여를 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-173">The following example shows how to request OAuth2.0 authorization:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

<span data-ttu-id="4f419-174">Azure AD는 사용자를 인증하고 필요한 경우 사용자에게 앱 사용 권한 부여를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-174">Azure AD authenticates the user, and, if necessary, asks the user to grant permission to the app.</span></span> <span data-ttu-id="4f419-175">그러면 응용 프로그램의 회신 URL에 인증 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-175">It returns the authorization code to the Reply URL of your application.</span></span> <span data-ttu-id="4f419-176">요청한 response_mode에 따라 Azure AD는 쿼리 문자열에 데이터를 다시 보내거나 데이터를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-176">Depending on the requested response_mode, Azure AD either sends back the data in query string or as post data.</span></span>

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a><span data-ttu-id="4f419-177">인증 요청(Open ID Connect)</span><span class="sxs-lookup"><span data-stu-id="4f419-177">Auth request (Open ID Connect)</span></span>
<span data-ttu-id="4f419-178">사용자를 대신하여 Azure Resource Manager에 액세스할 뿐만 아니라 사용자가 자신의 Azure AD 계정을 사용하여 응용 프로그램에 로그인할 수 있도록 하려면 Open ID Connect 권한 부여 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-178">If you not only wish to access Azure Resource Manager on behalf of the user, but also allow the user to sign in to your application using their Azure AD account, issue an Open ID Connect Authorize Request.</span></span> <span data-ttu-id="4f419-179">또한 Open ID Connect를 사용하면 응용 프로그램이 Azure AD로부터 앱에서 사용자를 로그인하는 데 사용할 수 있는 id_token을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-179">With Open ID Connect, your application also receives an id_token from Azure AD that your app can use to sign in the user.</span></span>

<span data-ttu-id="4f419-180">이 요청에 사용할 수 있는 쿼리 문자열 매개 변수는 [로그인 요청 보내기](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-180">The query string parameters that are available for this request are described in the [Send the sign-in request](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) topic.</span></span>

<span data-ttu-id="4f419-181">Open ID Connect 요청 예제:</span><span class="sxs-lookup"><span data-stu-id="4f419-181">An example Open ID Connect request is:</span></span>

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

<span data-ttu-id="4f419-182">Azure AD는 사용자를 인증하고 필요한 경우 사용자에게 앱 사용 권한 부여를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-182">Azure AD authenticates the user, and, if necessary, asks the user to grant permission to the app.</span></span> <span data-ttu-id="4f419-183">그러면 응용 프로그램의 회신 URL에 인증 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-183">It returns the authorization code to the Reply URL of your application.</span></span> <span data-ttu-id="4f419-184">요청한 response_mode에 따라 Azure AD는 쿼리 문자열에 데이터를 다시 보내거나 데이터를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-184">Depending on the requested response_mode, Azure AD either sends back the data in query string or as post data.</span></span>

<span data-ttu-id="4f419-185">Open ID Connect 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="4f419-185">An example Open ID Connect response is:</span></span>

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a><span data-ttu-id="4f419-186">토큰 요청(OAuth2.0 코드 부여 흐름)</span><span class="sxs-lookup"><span data-stu-id="4f419-186">Token request (OAuth2.0 Code Grant Flow)</span></span>
<span data-ttu-id="4f419-187">이제 응용 프로그램이 Azure AD에서 권한 부여 코드를 수신했으므로 Azure Resource Manager에 대한 토큰을 가져올 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-187">Now that your application has received the authorization code from Azure AD, it is time to get the access token for Azure Resource Manager.</span></span>  <span data-ttu-id="4f419-188">OAuth2.0 코드 부여 토큰 요청을 Azure AD 토큰 끝점에 게시:</span><span class="sxs-lookup"><span data-stu-id="4f419-188">Post an OAuth2.0 Code Grant Token Request to the Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="4f419-189">이 요청에 사용할 수 있는 쿼리 문자열 매개 변수는 [인증 코드 사용](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-189">The query string parameters that are available for this request are described in the [use the authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) topic.</span></span>

<span data-ttu-id="4f419-190">다음 예제에서는 암호 자격 증명을 사용하여 코드 부여 토큰에 대한 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-190">The following example shows a request for code grant token with password credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="4f419-191">인증서 자격 증명을 사용하여 작업할 때 JSON 웹 토큰(JWT)을 만들고 응용 프로그램의 인증서 자격 증명의 개인 키를 사용하여 서명합니다(RSA SHA256).</span><span class="sxs-lookup"><span data-stu-id="4f419-191">When working with certificate credentials, create a JSON Web Token (JWT) and sign (RSA SHA256) using the private key of your application's certificate credential.</span></span> <span data-ttu-id="4f419-192">토큰에 대한 클레임 형식은 [JWT 토큰 클레임](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims)에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-192">The claim types for the token are shown in [JWT token claims](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims).</span></span> <span data-ttu-id="4f419-193">참고로 클라이언트 어설션 JWT 토큰에 서명하는 방법은 [Active Directory 인증 라이브러리(.NET) 코드](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f419-193">For reference, see the [Active Directory Auth Library (.NET) code](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) to sign Client Assertion JWT tokens.</span></span>

<span data-ttu-id="4f419-194">클라이언트 인증에 대한 자세한 내용은 [Open ID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f419-194">See the [Open ID Connect spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) for details on client authentication.</span></span>

<span data-ttu-id="4f419-195">다음 예제에서는 인증서 자격 증명을 사용하여 코드 부여 토큰에 대한 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-195">The following example shows a request for code grant token with certificate credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

<span data-ttu-id="4f419-196">코드 부여 토큰에 대한 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="4f419-196">An example response for code grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a><span data-ttu-id="4f419-197">코드 부여 토큰 응답 처리</span><span class="sxs-lookup"><span data-stu-id="4f419-197">Handle code grant token response</span></span>
<span data-ttu-id="4f419-198">성공적인 토큰 응답은 Azure Resource Manager에 대한(사용자 + 앱) 액세스 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-198">A successful token response contains the (user + app) access token for Azure Resource Manager.</span></span> <span data-ttu-id="4f419-199">응용 프로그램은 이 액세스 토큰을 사용하여 사용자를 대신해 Resource Manager에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-199">Your application uses this access token to access Resource Manager on behalf of the user.</span></span> <span data-ttu-id="4f419-200">Azure AD에서 발급하는 액세스 토큰의 수명은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-200">The lifetime of access tokens issued by Azure AD is one hour.</span></span> <span data-ttu-id="4f419-201">웹 응용 프로그램이(사용자 + 앱) 액세스 토큰을 갱신해야 할 가능성은 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-201">It is unlikely that your web application needs to renew the (user + app) access token.</span></span> <span data-ttu-id="4f419-202">액세스 토큰을 갱신해야 한다면 응용 프로그램이 토큰 응답에서 받는 새로 고침 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-202">If it needs to renew the access token, use the refresh token that your application receives in the token response.</span></span> <span data-ttu-id="4f419-203">OAuth2.0 토큰 요청을 Azure AD 토큰 끝점에 게시:</span><span class="sxs-lookup"><span data-stu-id="4f419-203">Post an OAuth2.0 Token Request to the Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="4f419-204">새로 고침 요청에 사용할 매개 변수는 [액세스 토큰 새로 고침](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-204">The parameters to use with the refresh request are described in [refreshing the access token](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).</span></span>

<span data-ttu-id="4f419-205">다음 예제에서는 새로 고침 토큰을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-205">The following example shows how to use the refresh token:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="4f419-206">새로 고침 토큰을 사용하여 Azure Resource Manager에 대한 새 액세스 토큰을 가져올 수 있지만 이는 응용 프로그램에 의한 오프라인 액세스에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-206">Although refresh tokens can be used to get new access tokens for Azure Resource Manager, they are not suitable for offline access by your application.</span></span> <span data-ttu-id="4f419-207">새로 고침 토큰 수명은 제한되어 있고 새로 고침 토큰은 사용자에게 바인딩되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-207">The refresh tokens lifetime is limited, and refresh tokens are bound to the user.</span></span> <span data-ttu-id="4f419-208">사용자가 조직을 떠나면 새로 고침 토큰을 사용하는 응용 프로그램은 액세스 권한을 잃게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-208">If the user leaves the organization, the application using the refresh token loses access.</span></span> <span data-ttu-id="4f419-209">이 방법은 Azure 리소스를 관리하는 팀이 사용하는 응용 프로그램에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-209">This approach isn't suitable for applications that are used by teams to manage their Azure resources.</span></span>

## <a name="check-if-user-can-assign-access-to-subscription"></a><span data-ttu-id="4f419-210">사용자가 구독에 액세스를 할당할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="4f419-210">Check if user can assign access to subscription</span></span>
<span data-ttu-id="4f419-211">응용 프로그램은 이제 사용자를 대신하여 Azure Resource Manager에 액세스하기 위한 토큰을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-211">Your application now has a token to access Azure Resource Manager on behalf of the user.</span></span> <span data-ttu-id="4f419-212">다음 단계에서는 앱을 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-212">The next step is to connect your app to the subscription.</span></span> <span data-ttu-id="4f419-213">연결되면 앱은 사용자가 없어도(장기 오프라인 액세스) 해당 구독을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-213">After connecting, your app can manage those subscriptions even when the user isn't present (long-term offline access).</span></span>

<span data-ttu-id="4f419-214">연결할 각 구독에 대해 [Resource Manager 목록 권한](https://docs.microsoft.com/rest/api/authorization/permissions) API를 호출하여 사용자가 구독에 대한 액세스 관리 권한을 가지고 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-214">For each subscription to connect, call the [Resource Manager list permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API to determine whether the user has access management rights for the subscription.</span></span>

<span data-ttu-id="4f419-215">ASP.NET MVC 샘플 앱의 [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) 메서드가 이 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-215">The [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) method of the ASP.NET MVC sample app implements this call.</span></span>

<span data-ttu-id="4f419-216">다음 예제에서는 구독에 대한 사용자의 권한을 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-216">The following example shows how to request a user's permissions on a subscription.</span></span> <span data-ttu-id="4f419-217">83cfe939-2402-4581-b761-4f59b0a041e4는 구독의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-217">83cfe939-2402-4581-b761-4f59b0a041e4 is the id of the subscription.</span></span>

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

<span data-ttu-id="4f419-218">구독에 대한 사용자의 권한을 가져오기 위한 응답 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-218">An example of the response to get user's permissions on subscription is:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

<span data-ttu-id="4f419-219">사용 권한 API가 여러 사용 권한을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-219">The permissions API returns multiple permissions.</span></span> <span data-ttu-id="4f419-220">각 사용 권한은 허용되는 작업(actions) 및 허용되지 않는 작업(notactions)으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-220">Each permission consists of allowed actions (actions) and disallowed actions (notactions).</span></span> <span data-ttu-id="4f419-221">작업이 사용 권한의 허용되는 actions 목록에 있고 해당 권한의 notactions 목록에 없는 경우, 사용자는 해당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-221">If an action is present in the allowed actions list of any permission and not present in the notactions list of that permission, the user is allowed to perform that action.</span></span> <span data-ttu-id="4f419-222">**microsoft.authorization/roleassignments/write** 는 액세스 관리 권한을 부여하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-222">**microsoft.authorization/roleassignments/write** is the action that that grants access management rights.</span></span> <span data-ttu-id="4f419-223">응용 프로그램은 사용 권한 결과를 구문 분석하여 각 권한의 actions 및 notactions에서 이 작업 문자열에 대한 정규식 일치(regex match)를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-223">Your application must parse the permissions result to look for a regex match on this action string in the actions and notactions of each permission.</span></span>

## <a name="get-app-only-access-token"></a><span data-ttu-id="4f419-224">앱 전용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-224">Get app-only access token</span></span>
<span data-ttu-id="4f419-225">이제 사용자가 Azure 구독에 액세스 권한을 할당할 수 있는지 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-225">Now, you know if the user can assign access to the Azure subscription.</span></span> <span data-ttu-id="4f419-226">다음 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-226">The next steps are:</span></span>

1. <span data-ttu-id="4f419-227">구독에 대한 응용 프로그램의 ID에 대해 적절한 RBAC 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-227">Assign the appropriate RBAC role to your application's identity on the subscription.</span></span>
2. <span data-ttu-id="4f419-228">구독에 대한 응용 프로그램의 사용 권한을 쿼리하거나 응용 프로그램 전용 토큰을 사용해 Resource Manager에 액세스하여 액세스 할당의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-228">Validate the access assignment by querying for the Application's permission on the subscription or by accessing Resource Manager using app-only token.</span></span>
3. <span data-ttu-id="4f419-229">응용 프로그램의 "연결된 구독" 데이터 구조에 연결을 기록하여 구독의 ID를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-229">Record the connection in your applications "connected subscriptions" data structure - persisting the id of the subscription.</span></span>

<span data-ttu-id="4f419-230">첫 번째 단계를 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-230">Let's look closer at the first step.</span></span> <span data-ttu-id="4f419-231">응용 프로그램의 ID에 적절한 RBAC 역할을 할당하려면 다음을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-231">To assign the appropriate RBAC role to the application's identity, you must determine:</span></span>

* <span data-ttu-id="4f419-232">사용자의 Azure Active Directory에서 응용 프로그램의 ID의 개체 ID</span><span class="sxs-lookup"><span data-stu-id="4f419-232">The object id of your application's identity in the user's Azure Active Directory</span></span>
* <span data-ttu-id="4f419-233">응용 프로그램이 구독에 대해 요구하는 RBAC 역할의 ID</span><span class="sxs-lookup"><span data-stu-id="4f419-233">The identifier of the RBAC role that your application requires on the subscription</span></span>

<span data-ttu-id="4f419-234">응용 프로그램이 Azure AD에서 사용자를 인증할 때 응용 프로그램에 대한 서비스 주체 개체가 해당 Azure AD에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-234">When your application authenticates a user from an Azure AD, it creates a service principal object for your application in that Azure AD.</span></span> <span data-ttu-id="4f419-235">Azure는 RBAC 역할을 서비스 주체에 할당하여 Azure 리소스에 대한 직접 액세스 권한을 해당 응용 프로그램에 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-235">Azure allows RBAC roles to be assigned to service principals to grant direct access to corresponding applications on Azure resources.</span></span> <span data-ttu-id="4f419-236">이 작업이 바로 원했던 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-236">This action is exactly what we wish to do.</span></span> <span data-ttu-id="4f419-237">Azure AD Graph API를 쿼리하여 로그인한 사용자의 Azure AD에서 응용 프로그램의 서비스 주체의 ID를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-237">Query the Azure AD Graph API to determine the identifier of the service principal of your application in the signed-in user's Azure AD.</span></span>

<span data-ttu-id="4f419-238">사용자는 Azure Resource Manager에 대한 액세스 토큰만 가지고 있으므로 Azure AD Graph API를 호출하려면 새 액세스 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-238">You only have an access token for Azure Resource Manager - you need a new access token to call the Azure AD Graph API.</span></span> <span data-ttu-id="4f419-239">Azure AD의 모든 응용 프로그램은 서비스 주체 개체를 직접 쿼리하는 권한을 가지고 있으므로 앱 전용 액세스 토큰이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-239">Every application in Azure AD has permission to query its own service principal object, so an app-only access token is sufficient.</span></span>

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a><span data-ttu-id="4f419-240">Azure AD Graph API에 대한 응용 프로그램 전용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-240">Get app-only access token for Azure AD Graph API</span></span>
<span data-ttu-id="4f419-241">앱을 인증하고 Azure AD Graph API에 대한 토큰을 가져오려면 Azure AD 토큰 끝점(**https://login.microsoftonline.com/{directory_domain_name}/OAuth2/Token**)에 대한 클라이언트 자격 증명 부여 OAuth2.0 흐름 토큰 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-241">To authenticate your app and get a token to Azure AD Graph API, issue a Client Credential Grant OAuth2.0 flow token request to Azure AD token endpoint (**https://login.microsoftonline.com/{directory_domain_name}/OAuth2/Token**).</span></span>

<span data-ttu-id="4f419-242">ASP.net MVC 샘플 응용 프로그램의 [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) 메서드는 Active Directory Authentication Library for .NET을 사용하여 Graph API에 대한 앱 전용 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-242">The [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) method of the ASP.net MVC sample application gets an app-only access token for Graph API using the Active Directory Authentication Library for .NET.</span></span>

<span data-ttu-id="4f419-243">이 요청에 사용할 수 있는 쿼리 문자열 매개 변수는 [액세스 토큰 요청](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-243">The query string parameters that are available for this request are described in the [Request an Access Token](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) topic.</span></span>

<span data-ttu-id="4f419-244">클라이언트 자격 증명 부여 토큰에 대한 요청 예제:</span><span class="sxs-lookup"><span data-stu-id="4f419-244">An example request for client credential grant token:</span></span>

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

<span data-ttu-id="4f419-245">클라이언트 자격 증명 부여 토큰에 대한 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="4f419-245">An example response for client credential grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a><span data-ttu-id="4f419-246">사용자 Azure AD에서 응용 프로그램 서비스 주체의 ObjectId 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-246">Get ObjectId of application service principal in user Azure AD</span></span>
<span data-ttu-id="4f419-247">이제 응용 프로그램 전용 액세스 토큰을 사용하여 [Azure AD Graph 서비스 주체](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API를 쿼리하여 디렉터리에 있는 응용 프로그램의 서비스 주체의 개체 ID를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-247">Now, use the app-only access token to query the [Azure AD Graph Service Principals](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API to determine the Object Id of the application's service principal in the directory.</span></span>

<span data-ttu-id="4f419-248">ASP.net MVC 샘플 응용 프로그램의 [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) 메서드가 이 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-248">The [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) method of the ASP.net MVC sample application implements this call.</span></span>

<span data-ttu-id="4f419-249">다음 예제에서는 응용 프로그램의 서비스 주체를 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-249">The following example shows how to request an application's service principal.</span></span> <span data-ttu-id="4f419-250">a0448380-c346-4f9f-b897-c18733de9394는 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-250">a0448380-c346-4f9f-b897-c18733de9394 is the client id of the application.</span></span>

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

<span data-ttu-id="4f419-251">다음 예제에서는 응용 프로그램의 서비스 주체 요청에 대한 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-251">The following example shows a response to the request for an application's service principal</span></span>

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow the application to access CloudSense on behalf of the signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow the application to access CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a><span data-ttu-id="4f419-252">Azure RBAC 역할 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-252">Get Azure RBAC role identifier</span></span>
<span data-ttu-id="4f419-253">서비스 주체에 적절한 RBAC 역할을 할당하려면 Azure RBAC 역할의 ID를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-253">To assign the appropriate RBAC role to your service principal, you must determine the identifier of the Azure RBAC role.</span></span>

<span data-ttu-id="4f419-254">응용 프로그램에 대한 올바른 RBAC 역할:</span><span class="sxs-lookup"><span data-stu-id="4f419-254">The right RBAC role for your application:</span></span>

* <span data-ttu-id="4f419-255">응용 프로그램이 구독을 변경하지 않고 모니터링만 한다면 구독에 대한 독자 권한만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-255">If your application only monitors the subscription, without making any changes, it requires only reader permissions on the subscription.</span></span> <span data-ttu-id="4f419-256">**독자** 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-256">Assign the **Reader** role.</span></span>
* <span data-ttu-id="4f419-257">응용 프로그램이 Azure 구독을 관리하는 경우(엔터티 만들기/수정/삭제) 참가자 권한 중 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-257">If your application manages Azure the subscription, creating/modifying/deleting entities, it requires one of the contributor permissions.</span></span>
  * <span data-ttu-id="4f419-258">특정 유형의 리소스를 관리하려면 리소스별 참가자 역할(가상 컴퓨터 참가자, Virtual Network 참가자, 저장소 계정 참가자 등)을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-258">To manage a particular type of resource, assign the resource-specific contributor roles (Virtual Machine Contributor, Virtual Network Contributor, Storage Account Contributor, etc.)</span></span>
  * <span data-ttu-id="4f419-259">모든 리소스 유형을 관리하려면 **참가자** 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-259">To manage any resource type, assign the **Contributor** role.</span></span>

<span data-ttu-id="4f419-260">응용 프로그램에 대한 역할 할당은 사용자가 볼 수 있으므로 필요한 최소 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-260">The role assignment for your application is visible to users, so select the least-required privilege.</span></span>

<span data-ttu-id="4f419-261">[Resource Manager 역할 정의 API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) 를 호출하여 모든 Azure RBAC 역할을 나열하고 검색한 다음, 결과에 대해 이를 반복 실행하여 이름에 의해 원하는 역할 정의를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-261">Call the [Resource Manager role definition API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) to list all Azure RBAC roles and search then iterate over the result to find the desired role definition by name.</span></span>

<span data-ttu-id="4f419-262">ASP.net MVC 샘플 앱의 [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) 메서드가 이 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-262">The [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) method of the ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="4f419-263">다음 요청 예제는 Azure RBAC 역할 ID를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-263">The following request example shows how to get Azure RBAC role identifier.</span></span> <span data-ttu-id="4f419-264">09cbd307-aa71-4aca-b346-5f253e6e3ebb는 구독의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-264">09cbd307-aa71-4aca-b346-5f253e6e3ebb is the id of the subscription.</span></span>

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

<span data-ttu-id="4f419-265">응답은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-265">The response is in the following format:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access to them.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access to them.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

<span data-ttu-id="4f419-266">이 API를 수시로 호출할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-266">You do not need to call this API on an ongoing basis.</span></span> <span data-ttu-id="4f419-267">역할 정의의 잘 알려진 GUID를 결정한 후 다음과 같이 역할 정의 ID를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-267">Once you've determined the well-known GUID of the role definition, you can construct the role definition id as:</span></span>

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

<span data-ttu-id="4f419-268">다음은 널리 사용되는 기본 제공 역할의 잘 알려진 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-268">Here are the well-known guids of commonly used built-in roles:</span></span>

| <span data-ttu-id="4f419-269">역할</span><span class="sxs-lookup"><span data-stu-id="4f419-269">Role</span></span> | <span data-ttu-id="4f419-270">Guid</span><span class="sxs-lookup"><span data-stu-id="4f419-270">Guid</span></span> |
| --- | --- |
| <span data-ttu-id="4f419-271">독자</span><span class="sxs-lookup"><span data-stu-id="4f419-271">Reader</span></span> |<span data-ttu-id="4f419-272">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="4f419-272">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |
| <span data-ttu-id="4f419-273">참가자</span><span class="sxs-lookup"><span data-stu-id="4f419-273">Contributor</span></span> |<span data-ttu-id="4f419-274">b24988ac-6180-42a0-ab88-20f7382dd24c</span><span class="sxs-lookup"><span data-stu-id="4f419-274">b24988ac-6180-42a0-ab88-20f7382dd24c</span></span> |
| <span data-ttu-id="4f419-275">가상 컴퓨터 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-275">Virtual Machine Contributor</span></span> |<span data-ttu-id="4f419-276">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span><span class="sxs-lookup"><span data-stu-id="4f419-276">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span></span> |
| <span data-ttu-id="4f419-277">가상 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-277">Virtual Network Contributor</span></span> |<span data-ttu-id="4f419-278">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span><span class="sxs-lookup"><span data-stu-id="4f419-278">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span></span> |
| <span data-ttu-id="4f419-279">저장소 계정 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-279">Storage Account Contributor</span></span> |<span data-ttu-id="4f419-280">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span><span class="sxs-lookup"><span data-stu-id="4f419-280">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span></span> |
| <span data-ttu-id="4f419-281">웹 사이트 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-281">Website Contributor</span></span> |<span data-ttu-id="4f419-282">de139f84-1756-47ae-9be6-808fbbe84772</span><span class="sxs-lookup"><span data-stu-id="4f419-282">de139f84-1756-47ae-9be6-808fbbe84772</span></span> |
| <span data-ttu-id="4f419-283">웹 계획 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-283">Web Plan Contributor</span></span> |<span data-ttu-id="4f419-284">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span><span class="sxs-lookup"><span data-stu-id="4f419-284">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span></span> |
| <span data-ttu-id="4f419-285">SQL Server 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-285">SQL Server Contributor</span></span> |<span data-ttu-id="4f419-286">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span><span class="sxs-lookup"><span data-stu-id="4f419-286">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span></span> |
| <span data-ttu-id="4f419-287">SQL DB 참여자</span><span class="sxs-lookup"><span data-stu-id="4f419-287">SQL DB Contributor</span></span> |<span data-ttu-id="4f419-288">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span><span class="sxs-lookup"><span data-stu-id="4f419-288">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span></span> |

### <a name="assign-rbac-role-to-application"></a><span data-ttu-id="4f419-289">응용 프로그램에 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="4f419-289">Assign RBAC role to application</span></span>
<span data-ttu-id="4f419-290">응용 프로그램의 [Resource Manager 역할 할당 만들기](https://docs.microsoft.com/rest/api/authorization/roleassignments) API를 사용하여 서비스 주체에 적절한 RBAC 역할을 할당하기 위해 필요한 모든 것을 가졌습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-290">You have everything you need to assign the appropriate RBAC role to your service principal by using the [Resource Manager create role assignment](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.</span></span>

<span data-ttu-id="4f419-291">ASP.net MVC 샘플 앱의 [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) 메서드가 이 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-291">The [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) method of the ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="4f419-292">응용 프로그램에 RBAC 역할을 할당하는 요청 예제:</span><span class="sxs-lookup"><span data-stu-id="4f419-292">An example request to assign RBAC role to application:</span></span>

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

<span data-ttu-id="4f419-293">요청에 다음과 같은 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-293">In the request, the following values are used:</span></span>

| <span data-ttu-id="4f419-294">Guid</span><span class="sxs-lookup"><span data-stu-id="4f419-294">Guid</span></span> | <span data-ttu-id="4f419-295">설명</span><span class="sxs-lookup"><span data-stu-id="4f419-295">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f419-296">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span><span class="sxs-lookup"><span data-stu-id="4f419-296">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span></span> |<span data-ttu-id="4f419-297">구독의 ID</span><span class="sxs-lookup"><span data-stu-id="4f419-297">the id of the subscription</span></span> |
| <span data-ttu-id="4f419-298">c3097b31-7309-4c59-b4e3-770f8406bad2</span><span class="sxs-lookup"><span data-stu-id="4f419-298">c3097b31-7309-4c59-b4e3-770f8406bad2</span></span> |<span data-ttu-id="4f419-299">응용 프로그램의 서비스 주체의 개체 ID</span><span class="sxs-lookup"><span data-stu-id="4f419-299">the object id of the service principal of the application</span></span> |
| <span data-ttu-id="4f419-300">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="4f419-300">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |<span data-ttu-id="4f419-301">독자 역할의 ID</span><span class="sxs-lookup"><span data-stu-id="4f419-301">the id of the reader role</span></span> |
| <span data-ttu-id="4f419-302">4f87261d-2816-465d-8311-70a27558df4c</span><span class="sxs-lookup"><span data-stu-id="4f419-302">4f87261d-2816-465d-8311-70a27558df4c</span></span> |<span data-ttu-id="4f419-303">새 역할 할당에 대해 만든 새 GUID</span><span class="sxs-lookup"><span data-stu-id="4f419-303">a new guid created for the new role assignment</span></span> |

<span data-ttu-id="4f419-304">응답은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-304">The response is in the following format:</span></span>

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a><span data-ttu-id="4f419-305">Azure Resource Manager에 대한 응용 프로그램 전용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-305">Get app-only access token for Azure Resource Manager</span></span>
<span data-ttu-id="4f419-306">앱에 구독에 대해 원하는 액세스 권한이 있는지 확인하려면 앱 전용 토큰을 사용하여 구독에서 테스트 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-306">To validate that app has the desired access on the subscription, perform a test task on the subscription using an app-only token.</span></span>

<span data-ttu-id="4f419-307">리소스 매개 변수에 대해 서로 다른 값을 사용하여 앱 전용 액세스 토큰을 가져오려면 [Azure AD Graph API에 대한 응용 프로그램 전용 액세스 토큰 가져오기](#app-azure-ad-graph)섹션의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-307">To get an app-only access token, follow instructions from section [Get app-only access token for Azure AD Graph API](#app-azure-ad-graph), with a different value for the resource parameter:</span></span>

    https://management.core.windows.net/

<span data-ttu-id="4f419-308">ASP.NET MVC 샘플 응용 프로그램의 [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) 메서드는 Active Directory Authentication Library for .net을 사용하여 Azure Resource Manager에 대한 응용 프로그램 전용 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-308">The [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of the ASP.NET MVC sample application gets an app-only access token for Azure Resource Manager using the Active Directory Authentication Library for .net.</span></span>

#### <a name="get-applications-permissions-on-subscription"></a><span data-ttu-id="4f419-309">구독에 대한 응용 프로그램의 권한 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f419-309">Get Application's Permissions on Subscription</span></span>
<span data-ttu-id="4f419-310">응용 프로그램이 Azure 구독에 대해 원하는 액세스 권한을 가지고 있는지 확인하기 위해 [Resource Manager 사용 권한](https://docs.microsoft.com/rest/api/authorization/permissions) API를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-310">To check that your application has the desired access on an Azure subscription, you may also call the [Resource Manager Permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API.</span></span> <span data-ttu-id="4f419-311">이 방법은 사용자가 구독에 대해 액세스 관리 권한을 가지고 있는지 여부를 결정하는 방법과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-311">This approach is similar to how you determined whether the user has Access Management rights for the subscription.</span></span> <span data-ttu-id="4f419-312">그러나 이번에는 이전 단계에서 수신한 앱 전용 액세스 토큰을 사용하여 사용 권한 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-312">However, this time, call the permissions API with the app-only access token that you received in the previous step.</span></span>

<span data-ttu-id="4f419-313">ASP.NET MVC 샘플 앱의 [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) 메서드가 이 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-313">The [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of the ASP.NET MVC sample app implements this call.</span></span>

## <a name="manage-connected-subscriptions"></a><span data-ttu-id="4f419-314">연결된 구독 관리</span><span class="sxs-lookup"><span data-stu-id="4f419-314">Manage connected subscriptions</span></span>
<span data-ttu-id="4f419-315">구독에 대해 응용 프로그램의 서비스 주체에 적절한 RBAC 역할이 할당된 경우 응용 프로그램은 Azure Resource Manager에 대한 응용 프로그램 전용 액세스 토큰을 사용하여 해당 역할에 대한 모니터링/관리를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-315">When the appropriate RBAC role is assigned to your application's service principal on the subscription, your application can keep monitoring/managing it using app-only access tokens for Azure Resource Manager.</span></span>

<span data-ttu-id="4f419-316">구독 소유자가 클래식 포털 또는 명령줄 도구를 사용하여 응용 프로그램의 역할 할당을 제거하는 경우 응용 프로그램은 더 이상 해당 구독에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-316">If a subscription owner removes your application's role assignment using the classic portal or command-line tools, your application is no longer able to access that subscription.</span></span> <span data-ttu-id="4f419-317">이 경우 사용자에게 구독과의 연결이 응용 프로그램 외부에서 끊어졌음을 알리고 연결을 "복구"하는 옵션을 사용자에게 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-317">In that case, you should notify the user that the connection with the subscription was severed from outside the application and give them an option to "repair" the connection.</span></span> <span data-ttu-id="4f419-318">여기서 "복구"는 오프라인 상태에서 삭제된 역할 할당을 다시 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-318">"Repair" would simply re-create the role assignment that was deleted offline.</span></span>

<span data-ttu-id="4f419-319">사용자가 응용 프로그램에 대한 자신의 구독을 연결할 수 있도록 하는 것과 마찬가지로 사용자가 구독의 연결을 끊는 것도 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-319">Just as you enabled the user to connect subscriptions to your application, you must allow the user to disconnect subscriptions too.</span></span> <span data-ttu-id="4f419-320">액세스 관리 관점에서 연결 끊기란 응용 프로그램의 서비스 주체가 구독에 대해 가지고 있는 역할 할당을 제거하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-320">From an access management point of view, disconnect means removing the role assignment that the application's service principal has on the subscription.</span></span> <span data-ttu-id="4f419-321">필요에 따라 구독에 대한 응용 프로그램의 상태도 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-321">Optionally, any state in the application for the subscription might be removed too.</span></span>
<span data-ttu-id="4f419-322">구독에 대한 액세스 관리 권한을 가진 사용자만이 구독의 연결을 끊을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-322">Only users with access management permission on the subscription are able to disconnect the subscription.</span></span>

<span data-ttu-id="4f419-323">ASP.net MVC 샘플 앱의 [RevokeRoleFromServicePrincipalOnSubscription 메서드](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) 가 이 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-323">The [RevokeRoleFromServicePrincipalOnSubscription method](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) of the ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="4f419-324">이와 같이 사용자는 이제 응용 프로그램을 사용하여 쉽게 Azure 구독을 연결 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f419-324">That's it - users can now easily connect and manage their Azure subscriptions with your application.</span></span>
