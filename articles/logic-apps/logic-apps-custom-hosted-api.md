---
title: "Azure Logic Apps에 대한 웹 API 및 REST API 배포, 호출 및 인증 | Microsoft Docs"
description: "Azure Logic Apps를 사용하여 시스템 통합을 위한 워크플로에서 웹 API 및 REST API를 배포, 인증 및 호출합니다."
keywords: "웹 API, REST API, 커넥터, 워크플로, 시스템 통합, 인증"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="9a6ca-104">사용자 지정 앱 API를 논리 앱용 커넥터로 배포, 호출 및 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="9a6ca-105">논리 앱 워크플로에서 사용할 동작이나 트리거를 제공하는 [사용자 지정 API를 만든](./logic-apps-create-api-app.md) 후에는 API를 호출하기 전에 먼저 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="9a6ca-106">그리고 논리 앱에서 API를 호출할 수 있지만 최상의 환경을 위해 API 작업 및 매개 변수를 설명하는 [Swagger 메타데이터](http://swagger.io/specification/)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="9a6ca-107">이 Swagger 파일을 사용하면 API가 더 잘 작동하고 논리 앱과 더 쉽게 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="9a6ca-108">API를 [웹앱](../app-service-web/app-service-web-overview.md)으로 배포할 수 있지만 [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md)으로 배포하는 것이 좋습니다. 이렇게 하면 클라우드에서 API를 빌드, 호스팅 및 사용할 때 작업을 더 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="9a6ca-109">API에서 코드를 변경할 필요가 없이 API 앱에 코드를 배포하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="9a6ca-110">API 호스팅을 위한 가장 쉽고, 확장성 있는, 최상의 방법 중 하나를 제공하는 PaaS(Platform-as-a-Service) 제품인 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에서 API를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="9a6ca-111">논리 앱에서 API로의 호출을 인증하려면 코드를 업데이트할 필요가 없이 Azure Portal에서 Azure Active Directory를 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="9a6ca-112">또는 API 코드를 통해 인증을 요구하고 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="9a6ca-113">API를 웹앱 또는 API 앱으로 배포</span><span class="sxs-lookup"><span data-stu-id="9a6ca-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="9a6ca-114">논리 앱에서 사용자 지정 API를 호출하려면 먼저 API를 웹앱 또는 API 앱으로 Azure App Service에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="9a6ca-115">또한 Logic App Designer에서 Swagger 문서를 읽을 수 있게 하려면 API 정의 속성을 설정하고 웹앱 또는 API 앱에 대해 [CORS(원본 간 리소스 공유)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig)를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="9a6ca-116">Azure Portal에서 웹앱 또는 API 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="9a6ca-117">열린 블레이드의 **API** 아래에서 **API 정의**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="9a6ca-118">**API 정의 위치**를 swagger.json 파일의 URL로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="9a6ca-119">일반적으로 URL은 `https://{name}.azurewebsites.net/swagger/docs/v1)` 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![사용자 지정 API를 위한 Swagger 파일에 연결](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="9a6ca-121">**API** 아래에서 **CORS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="9a6ca-122">**허용된 원본**에 대한 CORS 정책을 **'*'**(모두 허용)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="9a6ca-123">이 설정은 Logic App Designer의 요청을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-123">This setting permits requests from Logic App Designer.</span></span>

   ![Logic App Designer에서 사용자 지정 API로의 요청 허용](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="9a6ca-125">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="9a6ca-126">ASP.NET 웹 API에 대한 Swagger 메타데이터 추가</span><span class="sxs-lookup"><span data-stu-id="9a6ca-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="9a6ca-127">Azure App Service에 ASP.NET 웹 API 배포</span><span class="sxs-lookup"><span data-stu-id="9a6ca-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="9a6ca-128">논리 앱 워크플로에서 사용자 지정 API 호출</span><span class="sxs-lookup"><span data-stu-id="9a6ca-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="9a6ca-129">API 정의 속성과 CORS를 설정한 후에는 사용자 지정 API의 트리거 및 동작은 논리 앱 워크플로에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="9a6ca-130">Swagger URL이 있는 웹 사이트를 보려면 Logic Apps Designer에서 구독 웹 사이트를 찾아보면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="9a6ca-131">Swagger 문서를 가리켜 사용할 수 있는 동작과 입력을 보려면 [HTTP + Swagger 동작](../connectors/connectors-native-http-swagger.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="9a6ca-132">Swagger 문서가 없거나 공개되지 않는 API를 포함하여 모든 API를 호출하려면 언제든지 [HTTP 동작](../connectors/connectors-native-http.md)을 사용하여 요청을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="9a6ca-133">사용자 지정 API에 대한 호출 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="9a6ca-134">다음과 같은 방법으로 사용자 지정 API에 대한 호출을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="9a6ca-135">[코드 변경 없음](#no-code) - Azure Portal을 통해 [Azure AD(Azure Active Directory)](../active-directory/active-directory-whatis.md)로 API를 보호하므로 코드를 업데이트하거나 API를 다시 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9a6ca-136">기본적으로 Azure Portal에서 설정하는 Azure AD 인증은 세분화된 권한 부여를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9a6ca-137">예를 들어 이 인증을 통해 특정 사용자 또는 앱이 아니라 특정 테넌트에 대한 API를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="9a6ca-138">[API 코드 업데이트](#update-code) - 코드를 통해 [인증서 인증](#certificate), [기본 인증](#basic) 또는 [Azure AD 인증](#azure-ad-code)을 적용하여 API를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="9a6ca-139">코드를 변경하지 않고 API에 대한 호출 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="9a6ca-140">이 방법의 일반적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="9a6ca-141">두 개의 [Azure AD(Azure Active Directory) 응용 프로그램 ID](../app-service-api/app-service-api-dotnet-service-principal-auth.md)를 만듭니다. 하나는 논리 앱용이고 다른 하나는 웹앱용(또는 API 앱용)입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="9a6ca-142">API에 대한 호출을 인증하려면 논리 앱의 Azure AD 응용 프로그램 ID와 연결된 [서비스 주체](../app-service-api/app-service-api-dotnet-service-principal-auth.md)의 자격 증명(클라이언트 ID 및 비밀)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="9a6ca-143">논리 앱 정의에 응용 프로그램 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="9a6ca-144">1부: 논리 앱의 Azure AD 응용 프로그램 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="9a6ca-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="9a6ca-145">논리 앱은 이 Azure AD 응용 프로그램 ID를 사용하여 Azure AD에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="9a6ca-146">디렉터리에 대해 이 ID를 한 번만 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="9a6ca-147">예를 들어 논리 앱마다 고유한 ID를 만들 수 있더라도 모든 논리 앱에 대해 동일한 ID를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="9a6ca-148">Azure Portal, [Azure 클래식 포털](#app-identity-logic-classic) 또는 [PowerShell](#powershell)을 사용하여 이러한 ID를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="9a6ca-149">**Azure Portal에서 논리 앱에 대한 응용 프로그램 ID 만들기**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="9a6ca-150">[Azure Portal](https://portal.azure.com "https://portal.azure.com")에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="9a6ca-151">웹앱 또는 API 앱과 동일한 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="9a6ca-152">디렉터리를 전환하려면 프로필을 클릭하고 다른 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="9a6ca-153">또는 **개요** > **디렉터리 전환**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="9a6ca-154">디렉터리 메뉴의 **관리** 아래에서 **앱 등록** > **새 응용 프로그램 등록**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="9a6ca-155">기본적으로 앱 등록 목록에는 디렉터리의 모든 앱 등록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="9a6ca-156">앱 등록만 보려면 검색 상자 옆에 있는 **내 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![새 앱 등록 만들기](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="9a6ca-158">응용 프로그램 ID의 이름을 지정하고, **응용 프로그램 종류**를 **웹앱/API**로 설정하며, **로그인 URL**의 도메인으로 형식이 지정된 고유 문자열을 제공하고, **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![응용 프로그램 ID의 이름 및 로그인 URL 제공](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="9a6ca-160">논리 앱에 대해 만든 응용 프로그램 ID가 이제 앱 등록 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![논리 앱의 응용 프로그램 ID](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="9a6ca-162">앱 등록 목록에서 새 응용 프로그램 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="9a6ca-163">3부에서 논리 앱에 대한 "클라이언트 ID"로 사용할 **응용 프로그램 ID**를 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![논리 앱의 응용 프로그램 ID 복사 및 저장](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="9a6ca-165">응용 프로그램 ID 설정이 표시되지 않으면 **설정** 또는 **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="9a6ca-166">**API 액세스** 아래에서 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="9a6ca-167">**설명** 아래에서 키의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="9a6ca-168">**만료** 아래에서 키의 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="9a6ca-169">만드는 키는 논리 앱에 대한 응용 프로그램 ID의 "비밀" 또는 암호 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![논리 앱 ID의 키 만들기](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="9a6ca-171">도구 모음에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="9a6ca-172">이제 **값** 아래에서 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="9a6ca-173">키 블레이드를 떠날 때 키가 숨겨지므로 나중에 사용할 수 있도록 **키를 복사하여 저장해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="9a6ca-174">3부에서 논리 앱을 구성할 때 이 키를 "비밀" 또는 암호로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![나중을 위한 키 복사 및 저장](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="9a6ca-176">**Azure 클래식 포털에서 논리 앱의 응용 프로그램 ID 만들기**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="9a6ca-177">Azure 클래식 포털에서 [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="9a6ca-178">웹앱 또는 API 앱에 사용하는 것과 동일한 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="9a6ca-179">**응용 프로그램** 탭의 페이지 아래쪽에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="9a6ca-180">응용 프로그램 ID의 이름을 지정하고 **다음**(오른쪽 화살표)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="9a6ca-181">**앱 속성** 아래에서 **로그인 URL** 및 **앱 ID URI**에 대한 도메인으로 형식이 지정된 고유 문자열을 제공하고 **완료**를 선택합니다(확인 표시).</span><span class="sxs-lookup"><span data-stu-id="9a6ca-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="9a6ca-182">**구성** 탭에서 3부에서 사용할 논리 앱의 **클라이언트 ID**를 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="9a6ca-183">**키** 아래에서 **기간 선택** 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="9a6ca-184">키의 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-184">Select a duration for your key.</span></span>

   <span data-ttu-id="9a6ca-185">만드는 키는 논리 앱에 대한 응용 프로그램 ID의 "비밀" 또는 암호 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="9a6ca-186">페이지 아래쪽에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="9a6ca-187">몇 초 정도 기다려야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="9a6ca-188">**키** 아래에서 현재 표시된 키를 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="9a6ca-189">3부에서 논리 앱을 구성할 때 이 키를 "비밀" 또는 암호로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="9a6ca-190">자세한 내용은 [Azure Active Directory 로그인을 사용하도록 App Service 응용 프로그램을 구성하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="9a6ca-191">**PowerShell에서 논리 앱의 응용 프로그램 ID 만들기**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="9a6ca-192">PowerShell과 함께 Azure Resource Manager를 통해 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="9a6ca-193">PowerShell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="9a6ca-194">사용한 **테넌트 ID**(Azure AD 테넌트의 GUID), **응용 프로그램 ID** 및 암호를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="9a6ca-195">자세한 내용은 [PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="9a6ca-196">2부: 웹앱 또는 API 앱의 Azure AD 응용 프로그램 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="9a6ca-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="9a6ca-197">웹앱 또는 API 앱이 이미 배포된 경우 Azure Portal에서 인증을 설정하고 응용 프로그램 ID를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="9a6ca-198">그렇지 않으면 [Azure Resource Manager 템플릿으로 배포할 때 인증을 설정](#authen-deploy)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="9a6ca-199">**Azure Portal에서 배포된 앱의 응용 프로그램 ID 만들기 및 인증 설정**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="9a6ca-200">[Azure Portal](https://portal.azure.com "https://portal.azure.com")에서 웹앱 또는 API 앱을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="9a6ca-201">**설정**에서 **인증/권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="9a6ca-202">**App Service 인증** 아래에서 인증을 **설정**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="9a6ca-203">**인증 공급자** 아래에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![인증 설정](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="9a6ca-205">이제 다음과 같이 웹앱 또는 API 앱의 응용 프로그램 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="9a6ca-206">**Azure Active Directory 설정** 블레이드에서 **관리 모드**를 **기본**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="9a6ca-207">**새 AD 앱 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="9a6ca-208">응용 프로그램 ID의 이름을 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![웹앱 또는 API 앱의 응용 프로그램 ID 만들기](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="9a6ca-210">**인증/권한 부여** 블레이드에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="9a6ca-211">이제 웹앱 또는 API 앱과 연결된 응용 프로그램 ID에 대한 클라이언트 ID 및 테넌트 ID를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="9a6ca-212">이러한 ID는 3부에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="9a6ca-213">따라서 Azure Portal 또는 [Azure 클래식 포털](#find-id-classic)에 대해 이러한 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="9a6ca-214">**Azure Portal에서 웹앱 또는 API 앱에 대한 응용 프로그램 ID의 클라이언트 ID 및 테넌트 ID 찾기**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="9a6ca-215">**인증 공급자** 아래에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   !["Azure Active Directory"를 선택합니다.](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="9a6ca-217">**Azure Active Directory 설정** 블레이드에서 **관리 모드**를 **고급**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="9a6ca-218">**클라이언트 ID**를 복사하고 3부에서 사용할 해당 GUID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="9a6ca-219">**클라이언트 ID** 및 **발급자 URL**이 표시되지 않으면 Azure Portal을 새로 고치고 1단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="9a6ca-220">**발급자 URL** 아래에서 3부에서 사용할 GUID만 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="9a6ca-221">필요한 경우 웹앱 또는 API 앱의 배포 템플릿에서 이 GUID를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="9a6ca-222">이 GUID는 특정 테넌트의 GUID("테넌트 ID")이며 `https://sts.windows.net/{GUID}` URL에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="9a6ca-223">변경 내용을 저장하지 않고 **Azure Active Directory 설정** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="9a6ca-224">**Azure 클래식 포털에서 웹앱 또는 API 앱에 대한 응용 프로그램 ID의 클라이언트 ID 및 테넌트 ID 찾기**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="9a6ca-225">Azure 클래식 포털에서 [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="9a6ca-226">웹앱 또는 API 앱에 사용할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="9a6ca-227">**검색** 상자에서 웹앱 또는 API 앱의 응용 프로그램 ID를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="9a6ca-228">**구성** 탭에서 **클라이언트 ID**를 복사하고 3부에서 사용할 해당 GUID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="9a6ca-229">클라이언트 ID를 가져온 후 **구성** 탭 아래쪽에서 **끝점 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="9a6ca-230">**페더레이션 메타데이터 문서**의 URL을 복사하고 해당 URL을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="9a6ca-231">열린 메타데이터 문서에서 `https://sts.windows.net/{GUID}` 형식의 **entityID** 특성이 있는 루트 **EntityDescriptor ID** 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="9a6ca-232">이 특성의 GUID는 특정 테넌트의 GUID(테넌트 ID)입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="9a6ca-233">테넌트 ID를 복사하고, 3부에서 사용할 뿐만 아니라 필요한 경우 웹앱 또는 API 앱의 배포 템플릿에서도 사용할 해당 ID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="9a6ca-234">자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="9a6ca-235">Azure App Service의 API 앱에 대한 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="9a6ca-236">Azure 앱 서비스의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="9a6ca-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="9a6ca-237">**Azure Resource Manager 템플릿으로 배포할 때 인증 설정**</span><span class="sxs-lookup"><span data-stu-id="9a6ca-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="9a6ca-238">논리 앱의 앱 ID와 다른 웹앱 또는 API 앱의 Azure AD 응용 프로그램 ID도 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="9a6ca-239">응용 프로그램 ID를 만들려면 Azure Portal에 대해 2부의 이전 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="9a6ca-240">1부의 단계를 수행할 수도 있지만 **로그인 URL** 및 **앱 ID URI**에 대한 웹앱 또는 API 앱의 실제 `https://{URL}`을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="9a6ca-241">이러한 단계에서 앱의 배포 템플릿 및 3부에서 사용할 클라이언트 ID와 테넌트 ID를 모두 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="9a6ca-242">웹앱 또는 API 앱의 Azure AD 응용 프로그램 ID를 만들 때는 PowerShell 대신 Azure Portal 또는 Azure 클래식 포털을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="9a6ca-243">PowerShell commandlet은 웹 사이트에 사용자가 로그인하는 데 필요한 권한을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="9a6ca-244">클라이언트 ID와 테넌트 ID를 가져온 후에는 이러한 ID를 웹앱 또는 API 앱의 하위 리소스로 배포 템플릿에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="9a6ca-245">Azure Active Directory 인증과 함께 빈 웹앱과 논리 앱을 자동으로 배포하려면 [여기에서 전체 템플릿을 보거나](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json) 아래의 **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="9a6ca-246">[![Azure에 배포](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9a6ca-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="9a6ca-247">3부: 논리 앱의 권한 부여 섹션 채우기</span><span class="sxs-lookup"><span data-stu-id="9a6ca-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="9a6ca-248">이전 템플릿에는 이 권한 부여 섹션이 설정되어 있지만, 논리 앱을 직접 작성하는 경우 전체 권한 부여 섹션을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="9a6ca-249">코드 보기에서 논리 앱 정의를 열고 **HTTP** 동작 섹션으로 이동하여 **권한 부여** 섹션을 찾아 다음 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="9a6ca-250">요소</span><span class="sxs-lookup"><span data-stu-id="9a6ca-250">Element</span></span> | <span data-ttu-id="9a6ca-251">설명</span><span class="sxs-lookup"><span data-stu-id="9a6ca-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9a6ca-252">tenant</span><span class="sxs-lookup"><span data-stu-id="9a6ca-252">tenant</span></span> |<span data-ttu-id="9a6ca-253">Azure AD 테넌트의 GUID</span><span class="sxs-lookup"><span data-stu-id="9a6ca-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="9a6ca-254">audience</span><span class="sxs-lookup"><span data-stu-id="9a6ca-254">audience</span></span> |<span data-ttu-id="9a6ca-255">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-255">Required.</span></span> <span data-ttu-id="9a6ca-256">액세스하려는 대상 리소스의 GUID, 즉 웹앱 또는 API 앱에 대한 응용 프로그램 ID의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="9a6ca-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="9a6ca-257">clientId</span><span class="sxs-lookup"><span data-stu-id="9a6ca-257">clientId</span></span> |<span data-ttu-id="9a6ca-258">액세스를 요청하는 클라이언트의 GUID, 즉 논리 앱에 대한 응용 프로그램 ID의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="9a6ca-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="9a6ca-259">secret</span><span class="sxs-lookup"><span data-stu-id="9a6ca-259">secret</span></span> |<span data-ttu-id="9a6ca-260">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-260">Required.</span></span> <span data-ttu-id="9a6ca-261">액세스 토큰을 요청하는 클라이언트에 대한 응용 프로그램 ID의 키 또는 암호</span><span class="sxs-lookup"><span data-stu-id="9a6ca-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="9a6ca-262">type</span><span class="sxs-lookup"><span data-stu-id="9a6ca-262">type</span></span> |<span data-ttu-id="9a6ca-263">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-263">The authentication type.</span></span> <span data-ttu-id="9a6ca-264">ActiveDirectoryOAuth 인증의 경우 이 값은 `ActiveDirectoryOAuth`입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="9a6ca-265">예:</span><span class="sxs-lookup"><span data-stu-id="9a6ca-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="9a6ca-266">코드를 통한 API 호출 보호</span><span class="sxs-lookup"><span data-stu-id="9a6ca-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="9a6ca-267">인증서 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-267">Certificate authentication</span></span>

<span data-ttu-id="9a6ca-268">논리 앱에서 웹앱 또는 API 앱으로 들어오는 요청의 유효성을 검사하기 위해 클라이언트 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="9a6ca-269">코드를 설정하려면 [TLS 상호 인증을 구성하는 방법](../app-service-web/app-service-web-configure-tls-mutual-auth.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="9a6ca-270">**권한 부여** 섹션에서 다음 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="9a6ca-271">요소</span><span class="sxs-lookup"><span data-stu-id="9a6ca-271">Element</span></span> | <span data-ttu-id="9a6ca-272">설명</span><span class="sxs-lookup"><span data-stu-id="9a6ca-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9a6ca-273">type</span><span class="sxs-lookup"><span data-stu-id="9a6ca-273">type</span></span> |<span data-ttu-id="9a6ca-274">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-274">Required.</span></span> <span data-ttu-id="9a6ca-275">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-275">The authentication type.</span></span> <span data-ttu-id="9a6ca-276">SSL 클라이언트 인증서의 경우 이 값은 `ClientCertificate`여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="9a6ca-277">password</span><span class="sxs-lookup"><span data-stu-id="9a6ca-277">password</span></span> |<span data-ttu-id="9a6ca-278">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-278">Required.</span></span> <span data-ttu-id="9a6ca-279">클라이언트 인증서(PFX 파일)에 액세스하기 위한 암호</span><span class="sxs-lookup"><span data-stu-id="9a6ca-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="9a6ca-280">pfx</span><span class="sxs-lookup"><span data-stu-id="9a6ca-280">pfx</span></span> |<span data-ttu-id="9a6ca-281">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-281">Required.</span></span> <span data-ttu-id="9a6ca-282">클라이언트 인증서(PFX 파일)의 Base64로 인코딩된 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="9a6ca-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="9a6ca-283">기본 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-283">Basic authentication</span></span>

<span data-ttu-id="9a6ca-284">논리 앱에서 웹앱 또는 API 앱으로 들어오는 요청의 유효성을 검사하기 위해 사용자 이름 및 암호와 같은 기본 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="9a6ca-285">기본 인증은 일반적인 패턴이며, 웹앱 또는 API 앱을 빌드하는 데 사용되는 언어에서 이 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="9a6ca-286">**권한 부여** 섹션에서 다음 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="9a6ca-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="9a6ca-288">요소</span><span class="sxs-lookup"><span data-stu-id="9a6ca-288">Element</span></span> | <span data-ttu-id="9a6ca-289">설명</span><span class="sxs-lookup"><span data-stu-id="9a6ca-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9a6ca-290">type</span><span class="sxs-lookup"><span data-stu-id="9a6ca-290">type</span></span> |<span data-ttu-id="9a6ca-291">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-291">Required.</span></span> <span data-ttu-id="9a6ca-292">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-292">The authentication type.</span></span> <span data-ttu-id="9a6ca-293">기본 인증의 경우 값은 `Basic`이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="9a6ca-294">username</span><span class="sxs-lookup"><span data-stu-id="9a6ca-294">username</span></span> |<span data-ttu-id="9a6ca-295">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-295">Required.</span></span> <span data-ttu-id="9a6ca-296">인증을 위한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-296">The username for authentication</span></span> |
| <span data-ttu-id="9a6ca-297">password</span><span class="sxs-lookup"><span data-stu-id="9a6ca-297">password</span></span> |<span data-ttu-id="9a6ca-298">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-298">Required.</span></span> <span data-ttu-id="9a6ca-299">인증을 위한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="9a6ca-300">코드를 통한 Azure Active Directory 인증</span><span class="sxs-lookup"><span data-stu-id="9a6ca-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="9a6ca-301">기본적으로 Azure Portal에서 설정하는 Azure AD 인증은 세분화된 권한 부여를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9a6ca-302">예를 들어 이 인증을 통해 특정 사용자 또는 앱이 아니라 특정 테넌트에 대한 API를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="9a6ca-303">코드를 통해 논리 앱에 대한 API 액세스를 제한하려면 JWT(JSON Web Token)가 포함된 헤더를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="9a6ca-304">호출자의 ID를 확인하고 일치하지 않는 요청을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="9a6ca-305">Azure Portal을 사용하지 않고 자신의 코드에서 이 인증을 완전히 구현하려면 [Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증](../app-service-web/web-sites-authentication-authorization.md)하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="9a6ca-306">논리 앱의 응용 프로그램 ID를 만들고 해당 ID를 사용하여 API를 호출하려면 이전 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6ca-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a6ca-307">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a6ca-307">Next steps</span></span>

* [<span data-ttu-id="9a6ca-308">진단 로그 및 경고를 사용하여 논리 앱 성능 확인</span><span class="sxs-lookup"><span data-stu-id="9a6ca-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)