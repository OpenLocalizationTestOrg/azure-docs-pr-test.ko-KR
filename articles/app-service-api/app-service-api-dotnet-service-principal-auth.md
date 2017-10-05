---
title: "Azure App Service의 API 앱에 대한 서비스 주체 인증 | Microsoft Docs"
description: "서비스 간 시나리오에 대해 Azure 앱 서비스에서 API 앱을 보호하는 방법에 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 95653287546bbe358111ed16af0c30a53caff2b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="13bba-103">Azure 앱 서비스의 API 앱에 대한 서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="13bba-103">Service principal authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="13bba-104">개요</span><span class="sxs-lookup"><span data-stu-id="13bba-104">Overview</span></span>
<span data-ttu-id="13bba-105">이 문서에서는 API 앱에 대한 *내부* 액세스를 위해 앱 서비스 인증을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-105">This article explains how to use App Service authentication for *internal* access to API apps.</span></span> <span data-ttu-id="13bba-106">내부 시나리오에는 사용자 고유의 응용 프로그램 코드에 의해서만 사용되도록 한 API 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-106">An internal scenario is where you have an API app that you want to be consumable only by your own application code.</span></span> <span data-ttu-id="13bba-107">앱 서비스에서 이 시나리오를 구현하는 가장 좋은 방법은 호출된 API 앱을 보호하기 위해 Azure AD를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-107">The recommended way to implement this scenario in App Service is to use Azure AD to protect the called API app.</span></span> <span data-ttu-id="13bba-108">응용 프로그램 ID(서비스 주체) 자격 증명을 제공하여 Azure AD에서 가져온 전달자 토큰으로 보호된 API 앱을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-108">You call the protected API app with a bearer token that you get from Azure AD by providing application identity (service principal) credentials.</span></span> <span data-ttu-id="13bba-109">Azure AD를 사용하는 대안은 **Azure 앱 서비스 인증 개요** 의 [서비스 간 인증](../app-service/app-service-authentication-overview.md#service-to-service-authentication)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-109">For alternatives to using Azure AD, see the **Service-to-service authentication** section of the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md#service-to-service-authentication).</span></span>

<span data-ttu-id="13bba-110">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-110">In this article, you'll learn:</span></span>

* <span data-ttu-id="13bba-111">Azure AD(Azure Active Directory)를 사용하여 인증되지 않은 액세스로부터 API 앱을 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="13bba-111">How to use Azure Active Directory (Azure AD) to protect an API app from unauthenticated access.</span></span>
* <span data-ttu-id="13bba-112">Azure AD 서비스 주체(앱 ID) 자격 증명을 사용하여 API 앱, 웹앱 또는 모바일 앱의 보호된 API 앱을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="13bba-112">How to consume a protected API app from an API app, web app, or mobile app by using Azure AD service principal (app identity) credentials.</span></span> <span data-ttu-id="13bba-113">논리 앱에서 사용하는 방법에 대한 자세한 내용은 [논리 앱으로 App Service에서 호스트되는 사용자 지정 API 사용](../logic-apps/logic-apps-custom-hosted-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-113">For information about how to consume from a logic app, see [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>
* <span data-ttu-id="13bba-114">로그온된 사용자가 보호된 API 앱을 브라우저에서 호출할 수 없도록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-114">How to make sure that the protected API app can't be called from a browser by logged on users.</span></span>
* <span data-ttu-id="13bba-115">특정 Azure AD 서비스 주체만이 보호된 API 앱을 호출할 수 있도록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-115">How to make sure that the protected API app can only be called by a specific Azure AD service principal.</span></span>

<span data-ttu-id="13bba-116">이 문서에는 두 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-116">The article contains two sections:</span></span>

* <span data-ttu-id="13bba-117">[Azure 앱 서비스에서 서비스 주체 인증을 구성하는 방법](#authconfig) 섹션에서는 API 앱에 인증을 구성하는 방법 및 보호된 API 앱을 사용하는 방법을 일반적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-117">The [How to configure service principal authentication in Azure App Service](#authconfig) section explains in general how to configure authentication for any API app, and how to consume the protected API app.</span></span> <span data-ttu-id="13bba-118">이 섹션은 .NET, Node.js 및 Java를 포함하여 앱 서비스에서 지원되는 모든 프레임워크에 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-118">This section applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="13bba-119">[.NET 시작 자습서 계속](#tutorialstart) 으로 시작하는 자습서는 앱 서비스에서 실행되는 .NET 샘플 응용 프로그램에 대해 "내부 액세스" 시나리오를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-119">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the tutorial guides you through configuring an "internal access" scenario for a .NET sample application running in App Service.</span></span> 

## <span data-ttu-id="13bba-120"><a id="authconfig"></a> Azure 앱 서비스에서 서비스 주체 인증을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="13bba-120"><a id="authconfig"></a> How to configure service principal authentication in Azure App Service</span></span>
<span data-ttu-id="13bba-121">이 섹션에서는 모든 API 앱에 적용되는 일반적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-121">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="13bba-122">수행 목록 .NET 샘플 응용 프로그램에 특정한 단계는 [.NET API 앱 자습서 시리즈 계속](#tutorialstart)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-122">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET API Apps tutorial series](#tutorialstart).</span></span>

1. <span data-ttu-id="13bba-123">[Azure Portal](https://portal.azure.com/)에서 보호할 API 앱의 **설정** 블레이드로 이동한 후 **기능** 섹션을 찾고 **인증/권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-123">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, and then find the **Features** section and click **Authentication/ Authorization**.</span></span>
   
    ![Azure 포털에서 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="13bba-125">**인증/권한 부여** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-125">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="13bba-126">**요청이 인증되지 않은 경우에 수행할 동작** 드롭다운 목록에서 **Azure Active Directory를 사용하여 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-126">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory** .</span></span>
4. <span data-ttu-id="13bba-127">**인증 공급자**에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-127">Under **Authentication Providers**, select **Azure Active Directory**.</span></span>
   
    ![Azure 포털에서 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="13bba-129">**Azure Active Directory 설정** 블레이드를 구성하여 새 Azure AD 응용 프로그램을 만들거나 또는 이미 기존 Azure AD 응용 프로그램이 있는 경우 해당 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-129">Configure the **Azure Active Directory Settings** blade to create a new Azure AD application, or use an existing Azure AD application if you already have one that you want to use.</span></span>
   
    <span data-ttu-id="13bba-130">내부 시나리오는 일반적으로 API 앱을 호출하는 API 앱을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-130">Internal scenarios typically involve an API app calling an API app.</span></span> <span data-ttu-id="13bba-131">각 API 앱 또는 하나의 Azure AD 응용 프로그램에 분리된 AD 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-131">You can use separate Azure AD applications for each API app or just one Azure AD application.</span></span>
   
    <span data-ttu-id="13bba-132">이 블레이드에서 자세한 지침은 [Azure Active Directory 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-132">For detailed instructions on this blade, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
6. <span data-ttu-id="13bba-133">인증 공급자 구성 블레이드를 마치면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-133">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
7. <span data-ttu-id="13bba-134">**인증/권한 부여** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-134">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

<span data-ttu-id="13bba-136">이 작업이 완료되면 앱 서비스는 구성된 Azure AD 테넌트에 있는 호출자의 요청만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-136">When this is done, App Service only allows requests from callers in the configured Azure AD tenant.</span></span> <span data-ttu-id="13bba-137">보호된 API 앱에 인증 또는 권한 부여 코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-137">No authentication or authorization code is required in the protected API app.</span></span> <span data-ttu-id="13bba-138">전달자 토큰은 HTTP 헤더에서 흔히 사용되는 클레임과 함께 API 앱에 전달되면, 서비스 주체와 같은 특정 호출자의 요청을 확인하기 위해 코드의 해당 정보를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-138">The bearer token is passed to the API app along with commonly used claims in HTTP headers, and you can read that information in code to validate that requests are from a particular caller, such as a service principal.</span></span>

<span data-ttu-id="13bba-139">인증 기능은 .NET, Node.js, Java 등 앱 서비스가 지원하는 모든 언어에 동일한 방법으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-139">This authentication functionality works the same way for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

#### <a name="how-to-consume-the-protected-api-app"></a><span data-ttu-id="13bba-140">보호된 API 앱을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="13bba-140">How to consume the protected API app</span></span>
<span data-ttu-id="13bba-141">호출자는 API 호출로 Azure AD 전달자 토큰을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-141">The caller must provide an Azure AD bearer token with API calls.</span></span> <span data-ttu-id="13bba-142">서비스 주체 자격 증명을 사용하여 전달자 토큰을 가져오려면 호출자는 Active Directory 인증 라이브러리([.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) 또는 [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)용 ADAL)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-142">To get a bearer token using service principal credentials, the caller uses Active Directory Authentication Library (ADAL for [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), or [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)).</span></span> <span data-ttu-id="13bba-143">토큰을 가져오려면 ADAL을 호출하는 코드는 ADAL에 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-143">To get a token, the code that calls ADAL provides to ADAL the following information:</span></span>

* <span data-ttu-id="13bba-144">Azure AD 테넌트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-144">The name of your Azure AD tenant.</span></span>
* <span data-ttu-id="13bba-145">Azure AD 앱의 클라이언트 ID 및 클라이언트 암호(앱 키)는 호출자와 연관되었습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-145">The client ID and client secret (app key) of the Azure AD app associated with the caller.</span></span>
* <span data-ttu-id="13bba-146">Azure AD 응용 프로그램의 클라이언트 ID는 보호된 API 앱과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-146">The client ID of the Azure AD application associated with the protected API app.</span></span> <span data-ttu-id="13bba-147">(Azure AD 응용 프로그램을 하나만 사용한 경우 호출자에 대한 클라이언트 ID와 동일합니다.)</span><span class="sxs-lookup"><span data-stu-id="13bba-147">(If just one Azure AD application is used, this is the same client ID as the one for the caller.)</span></span>

<span data-ttu-id="13bba-148">이러한 값은 [Azure 클래식 포털](https://manage.windowsazure.com/)의 Azure AD 페이지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-148">These values are available in the Azure AD pages of the [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="13bba-149">토큰을 획득하면 호출자는 토큰을 권한 부여 헤더에 HTTP 요청으로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-149">Once the token has been acquired, the caller includes it with HTTP requests in the Authorization header.</span></span>  <span data-ttu-id="13bba-150">앱 서비스는 토큰의 유효성을 검사하고 요청이 보호된 API 앱에 도달하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-150">App Service validates the token and allows the requests to reach the protected API app.</span></span>

#### <a name="how-to-protect-the-api-app-from-access-by-users-in-the-same-tenant"></a><span data-ttu-id="13bba-151">동일한 테넌트의 사용자가 API 앱을 액세스로부터 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="13bba-151">How to protect the API app from access by users in the same tenant</span></span>
<span data-ttu-id="13bba-152">동일한 테넌트의 사용자에 대한 전달자 토큰은 보호된 API 앱에 대해 유효하다고 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-152">Bearer tokens for users in the same tenant are considered valid for the protected API app.</span></span>  <span data-ttu-id="13bba-153">서비스 주체만이 보호된 API 앱을 호출할 수 있도록 하려는 경우 보호된 API 앱에 코드를 추가하여 토큰으로부터 다음과 같은 클레임의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-153">If you want to ensure that only a service principal can call the protected API app, add code in the protected API app to validate the following claims from the token:</span></span>

* <span data-ttu-id="13bba-154">`appid` 는 호출자와 관련된 Azure AD 응용 프로그램의 클라이언트 ID여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-154">`appid` should be the client ID of the Azure AD application that is associated with the caller.</span></span> 
* <span data-ttu-id="13bba-155">`oid`(`objectidentifier`)는 호출자의 서비스 주체 ID여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-155">`oid` (`objectidentifier`) should be the service principal ID of the caller.</span></span> 

<span data-ttu-id="13bba-156">앱 서비스는 X-MS-CLIENT-PRINCIPAL-ID 헤더에 있는 `objectidentifier` 클레임을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-156">App Service also provides the `objectidentifier` claim in the X-MS-CLIENT-PRINCIPAL-ID header.</span></span>

### <a name="how-to-protect-the-api-app-from-browser-access"></a><span data-ttu-id="13bba-157">브라우저 액세스로부터 API 앱을 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="13bba-157">How to protect the API app from browser access</span></span>
<span data-ttu-id="13bba-158">보호된 API 앱의 코드에서 클레임의 유효성을 검사하지 않은 경우 및 보호된 API 앱에 별도의 Azure AD 응용 프로그램을 사용하는 경우 Azure AD 응용 프로그램의 회신 URL이 API 앱의 기본 URL과 동일하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-158">If you don't validate claims in code in the protected API app, and if you use a separate Azure AD application for the protected API app, make sure that the Azure AD application's Reply URL is not the same as the API app's base URL.</span></span> <span data-ttu-id="13bba-159">회신 URL이 직접 보호된 API 앱을 가리키는 경우 동일한 Azure AD 테넌트의 사용자는 API 앱을 찾고 로그온한 다음 성공적으로 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-159">If the Reply URL points directly to the protected API app, a user in the same Azure AD tenant could browse to the API app, log on, and successfully call the API.</span></span>

## <span data-ttu-id="13bba-160"><a id="tutorialstart"></a> .NET API 앱 자습서 시리즈 계속</span><span class="sxs-lookup"><span data-stu-id="13bba-160"><a id="tutorialstart"></a> Continuing the .NET API Apps tutorial series</span></span>
<span data-ttu-id="13bba-161">API 앱에 Node.js 또는 Java 자습서 시리즈를 수행 중인 경우 [다음 단계](#next-steps) 섹션으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-161">If you are following the Node.js or Java tutorial series for API apps, skip to the [Next steps](#next-steps) section.</span></span> 

<span data-ttu-id="13bba-162">이 문서의 나머지 부분에서는 API 앱에 .NET API 앱 자습서 시리즈를 계속하며 [사용자 인증 자습서](app-service-api-dotnet-user-principal-auth.md) 를 완료하고 사용자 인증을 사용하여 Azure에서 실행하는 샘플 응용 프로그램이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-162">The remainder of this article continues the .NET API Apps tutorial series and assumes that you have completed the [user authentication tutorial](app-service-api-dotnet-user-principal-auth.md) and have the sample application running in Azure with user authentication enabled.</span></span>

## <a name="set-up-authentication-in-azure"></a><span data-ttu-id="13bba-163">Azure에서 인증 설정</span><span class="sxs-lookup"><span data-stu-id="13bba-163">Set up authentication in Azure</span></span>
<span data-ttu-id="13bba-164">이 섹션에서는 앱 서비스를 구성하므로 데이터 계층 API 앱이 도달하도록 허용하는 HTTP 요청만이 유효한 Azure AD 전달자 토큰을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-164">In this section you configure App Service so that the only HTTP requests it allows to reach the data tier API app are the ones that have valid Azure AD bearer tokens.</span></span> 

<span data-ttu-id="13bba-165">다음 섹션에서는 데이터 계층 API 앱을 구성하여 Azure AD에 응용 프로그램 자격 증명을 보내고 전달자 토큰을 다시 가져오며 해당 전달자 토큰을 중간 계층 API 앱에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-165">In the following section, you configure the middle tier API app to send application credentials to Azure AD, get back a bearer token, and send the bearer token to the data tier API app.</span></span> <span data-ttu-id="13bba-166">이 프로세스는 다이어그램에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-166">This process is illustrated in the diagram.</span></span>

![서비스 인증 다이어그램](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

<span data-ttu-id="13bba-168">자습서의 지침을 수행하는 동안 문제가 발생하는 경우 자습서 끝부분의 [문제 해결](#troubleshooting) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-168">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

1. <span data-ttu-id="13bba-169">[Azure Portal](https://portal.azure.com/)에서 ToDoListDataAPI(데이터 계층) API 앱에 만든 API 앱의 **설정** 블레이드로 이동한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-169">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListDataAPI (data tier) API app, and then click **Settings**.</span></span>
2. <span data-ttu-id="13bba-170">**설정** 블레이드의 **기능** 섹션을 찾고 **인증/권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-170">In the **Settings** blade, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure 포털에서 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. <span data-ttu-id="13bba-172">**인증/권한 부여** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-172">In the **Authentication / Authorization** blade, click **On**.</span></span>
4. <span data-ttu-id="13bba-173">**요청이 인증되지 않은 경우에 수행할 동작** 드롭다운 목록에서 **Azure Active Directory를 사용하여 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-173">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="13bba-174">앱 서비스를 발생시켜서 인증된 요청이 API 앱에 도달하도록 하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-174">This is the setting that causes App Service to ensure that only authenticated requests reach the API app.</span></span> <span data-ttu-id="13bba-175">유효한 전달자 토큰을 가진 요청의 경우 앱 서비스는 API 앱에 따라 토큰을 전달하고 해당 정보를 코드에 보다 쉽게 사용할 수 있도록 하는 자주 사용된 클레임으로 HTTP 헤더를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-175">For requests that have valid bearer tokens, App Service passes the tokens along to the API app and populates HTTP headers with commonly used claims to make that information more easily available to your code.</span></span>
5. <span data-ttu-id="13bba-176">**인증 공급자** 아래에서 **Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-176">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure 포털에서 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. <span data-ttu-id="13bba-178">**Azure Active Directory 설정** 블레이드에서 **Express**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-178">In the **Azure Active Directory Settings** blade, click **Express**.</span></span>
   
    <span data-ttu-id="13bba-179">**Express** 옵션을 사용하면 Azure는 Azure AD [테넌트](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)에서 자동으로 AAD 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-179">With the **Express** option Azure can automatically create an AAD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="13bba-180">자동으로 모든 Azure 계정에 하나씩 있기 때문에 테넌트를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-180">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
7. <span data-ttu-id="13bba-181">**관리 모드**에서 아직 선택하지 않은 경우 **새 AD 앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-181">Under **Management mode**, click **Create New AD App** if it isn't already selected.</span></span>
   
    <span data-ttu-id="13bba-182">포털이 **앱 만들기** 입력 상자에 기본값을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-182">The portal plugs the **Create App** input box with a default value.</span></span> <span data-ttu-id="13bba-183">기본적으로 Azure AD 응용 프로그램의 이름은 API 앱과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-183">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="13bba-184">원하는 경우 다른 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-184">If you prefer, you can enter a different name.</span></span>
   
    ![Azure AD 설정](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    <span data-ttu-id="13bba-186">**참고**: 대신 API 앱 및 보호된 API 앱을 호출하기 위해 단일 Azure AD 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-186">**Note**: As an alternative, you could use a single Azure AD application for both the calling API app and the protected API app.</span></span> <span data-ttu-id="13bba-187">해당 대안을 선택한 경우 앞의 사용자 인증 자습서에서 Azure AD 응용 프로그램을 이미 만들었기 때문에 **새 AD 앱 만들기** 옵션은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-187">If you chose that alternative, you would not need the **Create New AD App** option here because you already created an Azure AD application earlier in the user authentication tutorial.</span></span> <span data-ttu-id="13bba-188">이 자습서에서는 API 앱 및 보호된 API 앱을 호출하기 위해 별도의 Azure AD 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-188">For this tutorial, you'll use separate Azure AD applications for the calling API app and the protected API app.</span></span>
8. <span data-ttu-id="13bba-189">**앱 만들기** 입력 상자에 있는 값을 기록해 둡니다. 나중에 Azure 클래식 포털에서 이 AAD 응용 프로그램을 찾아 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-189">Make a note of the value that is in the **Create App** input box; you'll look up this AAD application in the Azure classic portal later.</span></span>
9. <span data-ttu-id="13bba-190">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-190">Click **OK**.</span></span>
10. <span data-ttu-id="13bba-191">**인증/권한 부여** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-191">In the **Authentication / Authorization** blade, click **Save**.</span></span>
    
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    <span data-ttu-id="13bba-193">App Service는 자동으로 API 앱의 URL로 설정된 **로그온 URL** 및 **회신 URL**을 사용하여 Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-193">App Service creates an Azure Active Directory application with **Sign-on URL** and **Reply URL** automatically set to the URL of your API app.</span></span> <span data-ttu-id="13bba-194">두 번째 값을 사용하면 AAD 테넌트의 사용자가 API 앱에 로그인하고 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-194">The latter value enables users in your AAD tenant to log in and access the API app.</span></span>

### <a name="verify-that-the-api-app-is-protected"></a><span data-ttu-id="13bba-195">API 앱이 보호되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-195">Verify that the API app is protected</span></span>
1. <span data-ttu-id="13bba-196">브라우저에서 API 앱의 URL로 이동: Azure Portal에서 **API 앱** 블레이드에서 **URL** 아래 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-196">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span> 
   
    <span data-ttu-id="13bba-197">인증되지 않은 요청은 API 앱에 도달할 수 없으므로 로그인 화면으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-197">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span> 
   
    <span data-ttu-id="13bba-198">브라우저가 Swagger UI로 이동하면 브라우저에서 이미 로그온했을 수 있습니다. 이 경우 InPrivate 또는 Incognito 창을 열고 Swagger UI URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-198">If your browser does go to the Swagger UI, your browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the Swagger UI URL.</span></span>
2. <span data-ttu-id="13bba-199">AAD 테넌트의 사용자 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-199">Log in with credentials of a user in your AAD tenant.</span></span>
   
   <span data-ttu-id="13bba-200">로그온하면 "만들기 성공" 페이지가 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-200">When you're logged on, the "successfully created" page appears in the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a><span data-ttu-id="13bba-201">ToDoListAPI 프로젝트를 구성하여 Azure AD 토큰 획득 및 전송</span><span class="sxs-lookup"><span data-stu-id="13bba-201">Configure the ToDoListAPI project to acquire and send the Azure AD token</span></span>
<span data-ttu-id="13bba-202">이 섹션에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-202">In this section you do the following tasks:</span></span>

* <span data-ttu-id="13bba-203">Azure AD 응용 프로그램 자격 증명을 사용하는 중간 계층 API 앱에서 코드를 추가하여 토큰을 획득하고 데이터 계층 API 앱에 HTTP 요청으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-203">Add code in the middle tier API app that uses Azure AD application credentials to acquire a token and send it with HTTP requests to the data tier API app.</span></span>
* <span data-ttu-id="13bba-204">Azure AD에서 필요한 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-204">Get the credentials you need from Azure AD.</span></span>
* <span data-ttu-id="13bba-205">중간 계층 API 앱의 Azure 앱 서비스 런타임 환경 설정에 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-205">Enter the credentials into Azure App Service runtime environment settings in the middle tier API app.</span></span> 

### <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a><span data-ttu-id="13bba-206">ToDoListAPI 프로젝트를 구성하여 Azure AD 토큰 획득 및 전송</span><span class="sxs-lookup"><span data-stu-id="13bba-206">Configure the ToDoListAPI project to acquire and send the Azure AD token</span></span>
<span data-ttu-id="13bba-207">Visual Studio의 ToDoListAPI 프로젝트에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-207">Make the following changes in the ToDoListAPI project in Visual Studio.</span></span>

1. <span data-ttu-id="13bba-208">*ServicePrincipal.cs* 파일의 모든 코드에 달린 주석을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-208">Uncomment all of the code in the *ServicePrincipal.cs* file.</span></span>
   
    <span data-ttu-id="13bba-209">Azure AD 전달자 토큰을 획득하기 위해 .NET용 ADAL을 사용하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-209">This is the code that uses ADAL for .NET to acquire the Azure AD bearer token.</span></span>  <span data-ttu-id="13bba-210">나중에 Azure 런타임 환경에서 설정할 몇 가지 구성 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-210">It uses several configuration values that you'll set in the Azure runtime environment later.</span></span> <span data-ttu-id="13bba-211">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-211">Here's the code:</span></span> 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    <span data-ttu-id="13bba-212">**참고:** 이 코드는 .NET NuGet 패키지(Microsoft.IdentityModel.Clients.ActiveDirectory)에 ADAL이 필요하며 이는 프로젝트에 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-212">**Note:** This code requires the ADAL for .NET NuGet package (Microsoft.IdentityModel.Clients.ActiveDirectory), which is already installed in the project.</span></span> <span data-ttu-id="13bba-213">처음부터 이 프로젝트를 만들 때 이 패키지를 설치해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-213">If you were creating this project from scratch, you would have to install this package.</span></span> <span data-ttu-id="13bba-214">이 패키지는 API 앱 new-project 템플릿에서 자동으로 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-214">This package is not automatically installed by the API app new-project template.</span></span>
2. <span data-ttu-id="13bba-215">*Controllers/ToDoListController*에서 인증 헤더의 HTTP 요청에 토큰을 추가하는 `NewDataAPIClient` 메서드에서 코드의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-215">In *Controllers/ToDoListController*, uncomment the code in the `NewDataAPIClient` method that adds the token to HTTP requests in the authorization header.</span></span>
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. <span data-ttu-id="13bba-216">ToDoListAPI 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="13bba-216">Deploy the ToDoListAPI project.</span></span> <span data-ttu-id="13bba-217">(프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **게시 > 게시**를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="13bba-217">(Right-click the project, then click **Publish > Publish**.)</span></span>
   
    <span data-ttu-id="13bba-218">Visual Studio가 프로젝트를 배포하고 웹앱의 기본 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-218">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="13bba-219">일반적으로 브라우저에서 Web API 기본 URL로 이동하려고 하는 403 오류 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-219">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
4. <span data-ttu-id="13bba-220">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-220">Close the browser.</span></span>

### <a name="get-azure-ad-configuration-values"></a><span data-ttu-id="13bba-221">Azure AD 구성 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="13bba-221">Get Azure AD configuration values</span></span>
1. <span data-ttu-id="13bba-222">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **Azure Active Directory**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-222">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
2. <span data-ttu-id="13bba-223">**디렉터리** 탭에서 AAD 테넌트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-223">On the **Directory** tab, click your AAD tenant.</span></span>
3. <span data-ttu-id="13bba-224">**응용 프로그램 > 회사 소유 응용 프로그램**을 클릭한 다음 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-224">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
4. <span data-ttu-id="13bba-225">응용 프로그램 목록에서 ToDoListDataAPI(데이터 계층) API 앱에 대한 인증을 활성화할 때 만들어진 응용 프로그램의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-225">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for the ToDoListDataAPI (data tier) API app.</span></span>
5. <span data-ttu-id="13bba-226">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-226">Click the **Configure** tab.</span></span>
6. <span data-ttu-id="13bba-227">**클라이언트 ID** 값을 복사하여 나중에 가져올 수 있는 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-227">Copy the **Client ID** value and save it someplace you can get it from later.</span></span> 
7. <span data-ttu-id="13bba-228">Azure 클래식 포털에서 **회사가 보유한 응용 프로그램**목록으로 다시 돌아가 중간 계층 ToDoListAPI API 앱에 대해 만든 AAD 응용 프로그램을 클릭합니다(이 자습서에서 만든 것이 아닌 이전 자습서에서 만든 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="13bba-228">In the Azure classic portal go back to the list of **Applications my company owns**, and click the AAD application that you created for the middle tier ToDoListAPI API app (the one you created in the previous tutorial, not the one you created in this tutorial).</span></span>
8. <span data-ttu-id="13bba-229">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-229">Click the **Configure** tab.</span></span>
9. <span data-ttu-id="13bba-230">**클라이언트 ID** 값을 복사하여 나중에 가져올 수 있는 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-230">Copy the **Client ID** value and save it someplace you can get it from later.</span></span>
10. <span data-ttu-id="13bba-231">**키** 아래의 **기간 선택** 드롭다운 목록에서 **1년**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-231">Under **keys**, select **1 year** from the **Select duration** drop-down list.</span></span>
11. <span data-ttu-id="13bba-232">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-232">Click **Save**.</span></span>
    
     ![앱 키 생성](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. <span data-ttu-id="13bba-234">키 값을 복사하여 나중에 가져올 수 있는 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-234">Copy the key value and save it someplace you can get it from later.</span></span>
    
     ![새 앱 키 복사](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-the-middle-tier-api-apps-runtime-environment"></a><span data-ttu-id="13bba-236">중간 계층 API 앱의 런타임 환경에서 Azure AD 설정 구성</span><span class="sxs-lookup"><span data-stu-id="13bba-236">Configure Azure AD settings in the middle tier API app's runtime environment</span></span>
1. <span data-ttu-id="13bba-237">[Azure 포털](https://portal.azure.com/)로 이동한 다음 TodoListAPI(중간 계층) 프로젝트를 호스팅하는 API 앱에 대한 **API 앱** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-237">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that hosts the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="13bba-238">**설정 > 응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-238">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="13bba-239">**앱 설정** 섹션에서 다음 키와 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-239">In the **App settings** section, add the following keys and values:</span></span>
   
   | <span data-ttu-id="13bba-240">**키**</span><span class="sxs-lookup"><span data-stu-id="13bba-240">**Key**</span></span> | <span data-ttu-id="13bba-241">ida:Authority</span><span class="sxs-lookup"><span data-stu-id="13bba-241">ida:Authority</span></span> |
   | --- | --- |
   | <span data-ttu-id="13bba-242">**값**</span><span class="sxs-lookup"><span data-stu-id="13bba-242">**Value**</span></span> |<span data-ttu-id="13bba-243">https://login.microsoftonline.com/{Azure AD 테넌트 이름}</span><span class="sxs-lookup"><span data-stu-id="13bba-243">https://login.microsoftonline.com/{your Azure AD tenant name}</span></span> |
   | <span data-ttu-id="13bba-244">**예제**</span><span class="sxs-lookup"><span data-stu-id="13bba-244">**Example**</span></span> |<span data-ttu-id="13bba-245">https://login.microsoftonline.com/contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="13bba-245">https://login.microsoftonline.com/contoso.onmicrosoft.com</span></span> |
   
   | <span data-ttu-id="13bba-246">**키**</span><span class="sxs-lookup"><span data-stu-id="13bba-246">**Key**</span></span> | <span data-ttu-id="13bba-247">ida:ClientId</span><span class="sxs-lookup"><span data-stu-id="13bba-247">ida:ClientId</span></span> |
   | --- | --- |
   | <span data-ttu-id="13bba-248">**값**</span><span class="sxs-lookup"><span data-stu-id="13bba-248">**Value**</span></span> |<span data-ttu-id="13bba-249">호출하는 응용 프로그램(중간 계층 - ToDoListAPI)의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="13bba-249">Client ID of the calling application (middle tier - ToDoListAPI)</span></span> |
   | <span data-ttu-id="13bba-250">**예제**</span><span class="sxs-lookup"><span data-stu-id="13bba-250">**Example**</span></span> |<span data-ttu-id="13bba-251">960adec2-b74a-484a-960adec2-b74a-484a</span><span class="sxs-lookup"><span data-stu-id="13bba-251">960adec2-b74a-484a-960adec2-b74a-484a</span></span> |
   
   | <span data-ttu-id="13bba-252">**키**</span><span class="sxs-lookup"><span data-stu-id="13bba-252">**Key**</span></span> | <span data-ttu-id="13bba-253">ida:ClientSecret</span><span class="sxs-lookup"><span data-stu-id="13bba-253">ida:ClientSecret</span></span> |
   | --- | --- |
   | <span data-ttu-id="13bba-254">**값**</span><span class="sxs-lookup"><span data-stu-id="13bba-254">**Value**</span></span> |<span data-ttu-id="13bba-255">호출하는 응용 프로그램의 앱 키(중간 계층 - ToDoListAPI)</span><span class="sxs-lookup"><span data-stu-id="13bba-255">App key of the calling application (middle tier - ToDoListAPI)</span></span> |
   | <span data-ttu-id="13bba-256">**예제**</span><span class="sxs-lookup"><span data-stu-id="13bba-256">**Example**</span></span> |<span data-ttu-id="13bba-257">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span><span class="sxs-lookup"><span data-stu-id="13bba-257">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span></span> |
   
   | <span data-ttu-id="13bba-258">**키**</span><span class="sxs-lookup"><span data-stu-id="13bba-258">**Key**</span></span> | <span data-ttu-id="13bba-259">ida:Resource</span><span class="sxs-lookup"><span data-stu-id="13bba-259">ida:Resource</span></span> |
   | --- | --- |
   | <span data-ttu-id="13bba-260">**값**</span><span class="sxs-lookup"><span data-stu-id="13bba-260">**Value**</span></span> |<span data-ttu-id="13bba-261">호출되는 응용 프로그램(중간 계층 - ToDoListDataAPI)의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="13bba-261">Client ID of the called application (data tier - ToDoListDataAPI)</span></span> |
   | <span data-ttu-id="13bba-262">**예제**</span><span class="sxs-lookup"><span data-stu-id="13bba-262">**Example**</span></span> |<span data-ttu-id="13bba-263">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span><span class="sxs-lookup"><span data-stu-id="13bba-263">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span></span> |
   
    <span data-ttu-id="13bba-264">**참고**: `ida:Resource`의 경우 **앱 ID URI**가 아닌 호출된 응용 프로그램의 **클라이언트 ID**를 사용해야 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-264">**Note**: For `ida:Resource`, make sure you use the called application's **client ID** and not its **App ID URI**.</span></span>
   
    <span data-ttu-id="13bba-265">이 자습서에서는 중간 계층 및 데이터 계층에 대해 구분된 Azure AD 응용 프로그램을 사용하므로 `ida:ClientId` 및 `ida:Resource`가 서로 다른 값입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-265">`ida:ClientId` and `ida:Resource` are different values for this tutorial because you're using separate Azure AD applicaations for the middle tier and data tier.</span></span> <span data-ttu-id="13bba-266">API 앱 및 보호된 API 앱을 호출하기 위해 단일 Azure AD 응용 프로그램을 사용하는 경우 `ida:ClientId` 및 `ida:Resource` 모두에서 동일한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-266">If you were using a single Azure AD application for the calling API app and the protected API app, you would use the same value in both `ida:ClientId` and `ida:Resource`.</span></span>
   
    <span data-ttu-id="13bba-267">코드는 ConfigurationManager를 사용하여 이러한 값을 가져오므로 프로젝트의 Web.config 파일 또는 Azure 런타임 환경에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-267">The code uses ConfigurationManager to get these values, so they could be stored in the project's Web.config file or in the Azure runtime environment.</span></span> <span data-ttu-id="13bba-268">Azure 앱 서비스에서 ASP.NET 응용 프로그램을 실행하는 동안 환경 설정은 Web.config에서 설정을 자동으로 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-268">While an ASP.NET application is running in Azure App Service, environment settings automatically override settings from Web.config.</span></span> <span data-ttu-id="13bba-269">환경 설정은 일반적으로 [Web.config 파일에 비해 중요한 정보를 저장하는 더 안전한 방법](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-269">Environment settings are generally a [more secure way to store sensitive information compared to a Web.config file](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>
4. <span data-ttu-id="13bba-270">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-270">Click **Save**.</span></span>
   
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-the-application"></a><span data-ttu-id="13bba-272">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="13bba-272">Test the application</span></span>
1. <span data-ttu-id="13bba-273">브라우저에서 AngularJS 프런트 엔드 웹앱의 HTTPS URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-273">In a browser go to the HTTPS URL of the AngularJS front end web app.</span></span>
2. <span data-ttu-id="13bba-274">**할 일 목록** 탭을 클릭하고 Azure AD 테넌트의 사용자에 대한 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-274">Click the **To Do List** tab and log in with credentials for a user in your Azure AD tenant.</span></span> 
3. <span data-ttu-id="13bba-275">응용 프로그램이 작동하고 있는지 확인하려면 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-275">Add to-do items to verify that the application is working.</span></span>
   
    ![할 일 목록 페이지](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    <span data-ttu-id="13bba-277">응용 프로그램이 예상 대로 작동하지 않으면 Azure 포털에 입력한 모든 설정을 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-277">If the application doesn't work as expected, double-check all of the settings you entered in the Azure portal.</span></span> <span data-ttu-id="13bba-278">모든 설정이 올바르다고 나타나는 경우 이 자습서의 뒷부분에서 [문제 해결](#troubleshooting) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-278">If all of the settings appear to be correct, see the [Troubleshooting](#troubleshooting) section later in this tutorial.</span></span>

## <a name="protect-the-api-app-from-browser-access"></a><span data-ttu-id="13bba-279">브라우저 액세스로부터 API 앱 보호</span><span class="sxs-lookup"><span data-stu-id="13bba-279">Protect the API app from browser access</span></span>
<span data-ttu-id="13bba-280">이 자습서의 경우 ToDoListDataAPI(데이터 계층) API 앱에 대한 별도의 Azure AD 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-280">For this tutorial you created a separate Azure AD application for the ToDoListDataAPI (data tier) API app.</span></span> <span data-ttu-id="13bba-281">알고 있는 것처럼 앱 서비스가 AAD 응용 프로그램을 만들 때 사용자가 브라우저에서 API 앱의 URL로 이동한 후 로그인하도록 하는 방식으로 AAD 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-281">As you've seen, when App Service creates an AAD application, it configures the AAD application in a way that enables a user to go to the API app's URL in a browser and log on.</span></span> <span data-ttu-id="13bba-282">즉, 서비스 주체뿐만 아니라 Azure AD 테넌트의 최종 사용자도 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-282">That means it's possible for an end user in your Azure AD tenant, not just a service principal, to access the API.</span></span> 

<span data-ttu-id="13bba-283">보호된 API 앱에서 코드를 작성하지 않고 브라우저가 액세스하는 것을 방지하려면 AAD 응용 프로그램에서 **회신 URL** 을 변경하여 API 앱의 기본 URL을 다르게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-283">If you want to prevent browser access without writing any code in the protected API app, you can change the **Reply URL** in the AAD application so that it's different from the API app's base URL.</span></span> 

### <a name="disable-browser-access"></a><span data-ttu-id="13bba-284">브라우저 액세스 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="13bba-284">Disable browser access</span></span>
1. <span data-ttu-id="13bba-285">TodoListService에 대해 만든 AAD 응용 프로그램에 대한 클래식 포털 **구성** 탭에서 **회신 URL** 필드의 값을 변경하여 API 앱의 URL이 아닌 유효한 URL이 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-285">In the classic portal's **Configure** tab for the AAD application that was created for the TodoListService, change the value in the **Reply URL** field so that it is a valid URL but not the API app's URL.</span></span>
2. <span data-ttu-id="13bba-286">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-286">Click **Save**.</span></span>

### <a name="verify-browser-access-no-longer-works"></a><span data-ttu-id="13bba-287">브라우저 액세스가 더 이상 작동하지 않는지 확인</span><span class="sxs-lookup"><span data-stu-id="13bba-287">Verify browser access no longer works</span></span>
<span data-ttu-id="13bba-288">개별 사용자의 자격 증명으로 로그온하여 브라우저에서 API 앱 URL로 이동할 수 있다는 것을 이전에 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-288">Earlier you verified that you can go to the API app URL from a browser by logging on with an individual user's credentials.</span></span> <span data-ttu-id="13bba-289">이 섹션에서 더 이상 가능하지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-289">In this section, you verify that this is no longer possible.</span></span> 

1. <span data-ttu-id="13bba-290">새 브라우저 창에서 API 앱의 URL로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-290">In a new browser window, go to the URL of the API app again.</span></span>
2. <span data-ttu-id="13bba-291">이렇게 하라는 메시지가 표시되면 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-291">Log in when prompted to do so.</span></span>
3. <span data-ttu-id="13bba-292">로그인에 성공하지만 오류 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-292">Login succeeds but leads to an error page.</span></span>
   
    <span data-ttu-id="13bba-293">AAD 앱을 구성하여 AAD 테넌트의 사용자가 브라우저에서 API에 로그인하고 액세스할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-293">You've configured the AAD app so that users in the AAD tenant cannot log in and access the API from a browser.</span></span> <span data-ttu-id="13bba-294">서비스 주체 토큰을 사용하여 API 앱에 계속 액세스할 수 있으며 이는 웹앱의 URL로 이동하고 할 일 항목을 더 추가하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-294">You can still access the API app by using a service principal token, which you can verify by going to the web app's URL and adding more to-do items.</span></span>

## <a name="restrict-access-to-a-particular-service-principal"></a><span data-ttu-id="13bba-295">특정 서비스 주체에 대한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="13bba-295">Restrict access to a particular service principal</span></span>
<span data-ttu-id="13bba-296">지금은 Azure AD 테넌트의 사용자 또는 서비스 주체에 대한 토큰을 얻을 수 있는 모든 호출자가 TodoListDataAPI(데이터 계층) API 앱을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-296">Right now, any caller that can get a token for a user or service principal in your Azure AD tenant can call the TodoListDataAPI (data tier) API app.</span></span> <span data-ttu-id="13bba-297">데이터 계층 API 앱이 TodoListAPI(중간 계층) API 앱 및 특정 서비스 주체에서만 호출을 허용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-297">You might want to make sure that the data tier API app only accepts calls from the TodoListAPI (middle tier) API app, and only from a particular service principal.</span></span> 

<span data-ttu-id="13bba-298">들어오는 호출에서 `appid` 및 `objectidentifier` 클레임의 유효성을 검사하는 코드를 추가하여 이러한 제한을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-298">You can add these restrictions by adding code to validate the `appid` and `objectidentifier` claims on incoming calls.</span></span>

<span data-ttu-id="13bba-299">이 자습서의 경우 컨트롤러 작업에서 직접 앱 ID 및 서비스 주체 ID의 유효성을 검사하는 코드를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-299">For this tutorial you put the code that validates app ID and service principal ID directly in your controller actions.</span></span>  <span data-ttu-id="13bba-300">대안은 사용자 지정 `Authorize` 특성을 사용하거나 시작 시퀀스(예: OWIN 미들웨어)에서 이 유효성 검사를 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-300">Alternatives are to use a custom `Authorize` attribute or to do this validation in your startup sequences (e.g. OWIN middleware).</span></span> <span data-ttu-id="13bba-301">두 번째 방법의 예제는 [이 샘플 응용 프로그램](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-301">For an example of the latter, see [this sample application](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs).</span></span> 

<span data-ttu-id="13bba-302">TodoListDataAPI 프로젝트를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-302">Make the following changes to the TodoListDataAPI project.</span></span>

1. <span data-ttu-id="13bba-303">*Controllers/TodoListController.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-303">Open the *Controllers/TodoListController.cs* file.</span></span>
2. <span data-ttu-id="13bba-304">`trustedCallerClientId` 및 `trustedCallerServicePrincipalId`를 설정하는 줄의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-304">Uncomment the lines that set `trustedCallerClientId` and `trustedCallerServicePrincipalId`.</span></span>
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. <span data-ttu-id="13bba-305">CheckCallerId 메서드에서 코드의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-305">Uncomment the code in the CheckCallerId method.</span></span> <span data-ttu-id="13bba-306">이 메서드는 컨트롤러에서 모든 작업 메서드의 시작 부분에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-306">This method is called at the start of every action method in the controller.</span></span> 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The appID or service principal ID is not the expected value." });
            }
        }
4. <span data-ttu-id="13bba-307">새 Azure 앱 서비스에 ToDoListDataAPI 프로젝트를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-307">Redeploy the ToDoListDataAPI project to Azure App Service.</span></span>
5. <span data-ttu-id="13bba-308">브라우저에서 AngularJS 프런트 엔드 웹앱의 HTTPS URL로 이동하고 홈 페이지에서 **할 일 목록** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-308">In your browser, go to the AngularJS front end web app's HTTPS URL, and in the home page click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="13bba-309">백 엔드에 대한 호출이 실패하기 때문에 응용 프로그램이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-309">The application doesn't work because calls to the back end are failing.</span></span> <span data-ttu-id="13bba-310">새 코드는 실제 appid 및 objectidentifier를 검사하지만 확인할 올바른 값이 아직 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-310">The new code is checking actual appid and objectidentifier but it doesn't yet have the correct values to check them against.</span></span> <span data-ttu-id="13bba-311">브라우저 개발자 도구 콘솔은 서버가 HTTP 401 오류를 반환하고 있는지를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-311">The browser Developer Tools Console reports that the server is returning an HTTP 401 error.</span></span>
   
    ![개발자 도구 콘솔의 오류](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    <span data-ttu-id="13bba-313">다음 단계에서 예상 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-313">In the following steps you configure the expected values.</span></span>
6. <span data-ttu-id="13bba-314">Azure AD PowerShell을 사용하여 TodoListWebApp 프로젝트에 대해 만든 Azure AD 응용 프로그램에 대한 서비스 주체의 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-314">Using Azure AD PowerShell, get the value of the service principal for the Azure AD application that you created for the TodoListWebApp project.</span></span>
   
    <span data-ttu-id="13bba-315">a.</span><span class="sxs-lookup"><span data-stu-id="13bba-315">a.</span></span> <span data-ttu-id="13bba-316">Azure PowerShell을 설치하고 구독에 연결하는 방법에 대한 지침은 [Azure Resource Manager로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-316">For instructions on how to install Azure PowerShell and connect to your subscription, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
   
    <span data-ttu-id="13bba-317">b.</span><span class="sxs-lookup"><span data-stu-id="13bba-317">b.</span></span> <span data-ttu-id="13bba-318">서비스 주체의 목록을 가져오려면 `Login-AzureRmAccount` 명령 및 `Get-AzureRmADServicePrincipal` 명령을 차례로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-318">To get a list of service principals, execute the `Login-AzureRmAccount` command and then the `Get-AzureRmADServicePrincipal` command.</span></span>
   
    <span data-ttu-id="13bba-319">c.</span><span class="sxs-lookup"><span data-stu-id="13bba-319">c.</span></span> <span data-ttu-id="13bba-320">TodoListAPI 응용 프로그램의 서비스 주체에 대한 objectid를 찾고 나중에 복사할 수 있는 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-320">Find the objectid for the service principal of the TodoListAPI application, and save it in a location you can copy from later.</span></span>
7. <span data-ttu-id="13bba-321">Azure 포털에서 ToDoList.API 프로젝트를 배포한 API 앱에 대한 API 앱 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-321">In the Azure portal, navigate to the API app blade for the API app that you deployed the ToDoListDataAPI project to.</span></span>
8. <span data-ttu-id="13bba-322">**설정 > 응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-322">Click **Settings > Application settings**.</span></span>
9. <span data-ttu-id="13bba-323">**앱 설정** 섹션에서 다음 키와 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-323">In the **App settings** section, add the following keys and values:</span></span>
   
   | <span data-ttu-id="13bba-324">**키**</span><span class="sxs-lookup"><span data-stu-id="13bba-324">**Key**</span></span> | <span data-ttu-id="13bba-325">todo:TrustedCallerServicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="13bba-325">todo:TrustedCallerServicePrincipalId</span></span> |
   | --- | --- |
   | <span data-ttu-id="13bba-326">**값**</span><span class="sxs-lookup"><span data-stu-id="13bba-326">**Value**</span></span> |<span data-ttu-id="13bba-327">호출하는 응용 프로그램의 서비스 주체 ID</span><span class="sxs-lookup"><span data-stu-id="13bba-327">Service principal id of calling application</span></span> |
   | <span data-ttu-id="13bba-328">**예제**</span><span class="sxs-lookup"><span data-stu-id="13bba-328">**Example**</span></span> |<span data-ttu-id="13bba-329">4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072</span><span class="sxs-lookup"><span data-stu-id="13bba-329">4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072</span></span> |
   
   | <span data-ttu-id="13bba-330">**키**</span><span class="sxs-lookup"><span data-stu-id="13bba-330">**Key**</span></span> | <span data-ttu-id="13bba-331">todo:TrustedCallerClientId</span><span class="sxs-lookup"><span data-stu-id="13bba-331">todo:TrustedCallerClientId</span></span> |
   | --- | --- |
   | <span data-ttu-id="13bba-332">**값**</span><span class="sxs-lookup"><span data-stu-id="13bba-332">**Value**</span></span> |<span data-ttu-id="13bba-333">TodoListAPI Azure AD 응용 프로그램에서 복사한 호출하는 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="13bba-333">Client ID of calling application - copied from the TodoListAPI Azure AD application</span></span> |
   | <span data-ttu-id="13bba-334">**예제**</span><span class="sxs-lookup"><span data-stu-id="13bba-334">**Example**</span></span> |<span data-ttu-id="13bba-335">960adec2-b74a-484a-960adec2-b74a-484a</span><span class="sxs-lookup"><span data-stu-id="13bba-335">960adec2-b74a-484a-960adec2-b74a-484a</span></span> |
10. <span data-ttu-id="13bba-336">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-336">Click **Save**.</span></span>
    
     ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. <span data-ttu-id="13bba-338">브라우저에서 웹앱의 URL로 돌아가서 홈 페이지에서 **할 일 목록** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-338">In your browser, return to the web app's URL, and in the home page click the **To Do List** tab.</span></span>
    
     <span data-ttu-id="13bba-339">신뢰할 수 있는 호출자의 앱 ID 및 서비스 주체 ID가 예상된 값이기 때문에 이번에는 응용 프로그램이 예상 대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-339">This time the application works as expected because the trusted caller app ID and service principal ID are the expected values.</span></span>
    
     ![할 일 목록 페이지](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="13bba-341">처음부터 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="13bba-341">Building the projects from scratch</span></span>
<span data-ttu-id="13bba-342">**Azure API 앱** 프로젝트 템플릿을 사용하고 기본 Values 컨트롤러를 ToDoList 컨트롤러로 대체하여 두 개의 웹 API 프로젝트가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-342">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> <span data-ttu-id="13bba-343">ToDoListAPI 프로젝트에서 Azure AD 서비스 주체 토큰을 확보하기 위해 [.NET 용 ADAL(Active Directory 인증 라이브러리)](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet 패키지가 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-343">For acquiring Azure AD service principal tokens in the ToDoListAPI project, the [Active Directory Authentication Library (ADAL) for .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet package was installed.</span></span>

<span data-ttu-id="13bba-344">ToDoListAngular와 같은 Web API 백 엔드를 통한 AngularJS 단일 페이지 응용 프로그램을 만드는 방법에 대한 내용은 [Hands On Lab: ASP.NET Web API 및 Angular.js를 통해 SPA(단일 페이지 응용 프로그램) 빌드](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-344">For information about how to  create an AngularJS single-page application with a Web API back end like ToDoListAngular, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="13bba-345">Azure AD 인증 코드를 추가하는 방법에 대한 정보는 [Azure AD로 AngularJS 단일 페이지 앱 보안](../active-directory/active-directory-devquickstarts-angular.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-345">For information about how to add Azure AD authentication code, see [Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="13bba-346">문제 해결</span><span class="sxs-lookup"><span data-stu-id="13bba-346">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="13bba-347">ToDoListAPI(중간 계층) 및 ToDoListDataAPI(데이터 계층)를 혼동하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-347">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="13bba-348">예를 들어 이 자습서에서는 데이터 계층 API 앱에 인증을 추가하지만 **앱 키는 중간 계층 API 앱에 대해 만든 Azure AD 응용 프로그램에서 가져와야**합니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-348">For example, in this tutorial you add authentication to the data tier API app, **but the app key must come from the Azure AD application that you created for the middle tier API app**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13bba-349">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13bba-349">Next steps</span></span>
<span data-ttu-id="13bba-350">이 자습서는 API 앱 시리즈의 마지막 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-350">This is the last tutorial in the API Apps series.</span></span> 

<span data-ttu-id="13bba-351">Azure Active Directory에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-351">For more information about Azure Active Directory, see the following resources.</span></span>

* [<span data-ttu-id="13bba-352">Azure AD 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="13bba-352">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="13bba-353">Azure AD 시나리오</span><span class="sxs-lookup"><span data-stu-id="13bba-353">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="13bba-354">Azure AD 샘플</span><span class="sxs-lookup"><span data-stu-id="13bba-354">Azure AD samples</span></span>](http://aka.ms/aadsamples)
  
    <span data-ttu-id="13bba-355">[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) 샘플은 이 자습서에 표시된 것과 비슷하지만, 앱 서비스 인증을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13bba-355">The [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) sample is similar to what is shown in this tutorial, but without using App Service authentication.</span></span>

<span data-ttu-id="13bba-356">Visual Studio를 사용하거나 [원본 제어 시스템](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)에서 [배포를 자동화](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)하여 API 앱에 Visual Studio를 배포하는 다른 방법에 대한 정보는 [Azure App Service 앱을 배포하는 방법](../app-service-web/web-sites-deploy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13bba-356">For information about other ways to deploy Visual Studio projects to API apps, by using Visual Studio or by [automating deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) from a [source control system](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), see [How to deploy an Azure App Service app](../app-service-web/web-sites-deploy.md).</span></span>

