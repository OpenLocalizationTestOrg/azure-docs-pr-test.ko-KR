---
title: "를 호출 하 고 Azure 논리 앱에 대 한 웹 Api 및 REST Api를 인증 하는 aaaDeploy, | Microsoft Docs"
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
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="d7c50-104">사용자 지정 앱 API를 논리 앱용 커넥터로 배포, 호출 및 인증</span><span class="sxs-lookup"><span data-stu-id="d7c50-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="d7c50-105">후 [사용자 지정 Api 만들기](./logic-apps-create-api-app.md) 앱 워크플로 작업 또는 트리거 toouse 논리에서 제공 하는, Api를 호출 하기 전에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="d7c50-106">최상의 환경을 hello에 대 한 논리 앱에서 모든 API를 호출할 수, 있지만 추가 [Swagger 메타 데이터](http://swagger.io/specification/) API의 작업 및 매개 변수를 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="d7c50-107">이 Swagger 파일을 사용하면 API가 더 잘 작동하고 논리 앱과 더 쉽게 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="d7c50-108">사용자 Api로 배포할 수 있습니다 [웹 앱](../app-service-web/app-service-web-overview.md),으로 Api를 배포 하는 것이 좋습니다. [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md)는 수 작업을 손쉽게 수행할 빌드, 호스팅 및 hello 클라우드 및 온-프레미스 Api를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d7c50-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="d7c50-109">Toochange 모든 코드에에서 없는 Api-방금 코드 tooan API 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="d7c50-110">Api에서 호스트할 수 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)는 플랫폼으로-서비스 (PaaS) API 호스팅을 위한 제공 하는 hello 가장 쉽고 가장 확장성이 뛰어난 방법 중 하나를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="d7c50-111">논리 앱 tooyour Api에서에서 tooauthenticate 호출을 설정할 수 있습니다 Azure Active directory hello에 Azure 포털 코드 tooupdate 쓸 필요.</span><span class="sxs-lookup"><span data-stu-id="d7c50-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="d7c50-112">또는 API 코드를 통해 인증을 요구하고 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="d7c50-113">API를 웹앱 또는 API 앱으로 배포</span><span class="sxs-lookup"><span data-stu-id="d7c50-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="d7c50-114">논리 앱에서 사용자 지정 API를 호출할 수 있습니다, 전에 웹 앱 또는 앱 서비스 API 앱 tooAzure로 API를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="d7c50-115">또한 toomake hello 논리가 응용 프로그램 디자이너에서 읽을 수 있는 Swagger 문서 hello API 정의 속성을 설정 하 고 설정 [크로스-원본 자원 공유 (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) 웹 응용 프로그램 또는 API 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="d7c50-116">Hello Azure 포털에서에서 웹 앱 또는 API 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="d7c50-117">아래에서 열리면 hello 블레이드에서 **API**, 선택 **API 정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="d7c50-118">집합 hello **API 정의 위치** swagger.json 파일에 대 한 toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="d7c50-119">일반적으로 hello URL이이 형식으로 나타납니다.`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="d7c50-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![사용자 지정 API에 대 한 링크 tooSwagger 파일](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="d7c50-121">**API** 아래에서 **CORS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="d7c50-122">설정에 대 한 CORS 정책을 hello **origin 허용** 너무**'*'** (모두 허용).</span><span class="sxs-lookup"><span data-stu-id="d7c50-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="d7c50-123">이 설정은 Logic App Designer의 요청을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-123">This setting permits requests from Logic App Designer.</span></span>

   ![응용 프로그램 디자이너 논리 tooyour 사용자 지정 API에서 요청을 허용 합니다.](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="d7c50-125">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7c50-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="d7c50-126">ASP.NET 웹 API에 대한 Swagger 메타데이터 추가</span><span class="sxs-lookup"><span data-stu-id="d7c50-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="d7c50-127">ASP.NET 웹 Api tooAzure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="d7c50-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="d7c50-128">논리 앱 워크플로에서 사용자 지정 API 호출</span><span class="sxs-lookup"><span data-stu-id="d7c50-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="d7c50-129">Hello API 정의 속성과 CORS 설정한 후 사용자 지정 API 트리거 및 작업에서 논리 앱 워크플로 tooinclude에 대 한 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="d7c50-130">tooview hello 웹 사이트의 Swagger Url이 있는 경우 hello 논리 앱 디자이너에에서 웹 사이트 구독을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="d7c50-131">hello를 사용 하 여 tooview 사용 가능한 작업 및 Swagger 문서를 가리키는 방법으로 입력 [HTTP + Swagger 동작](../connectors/connectors-native-http-swagger.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="d7c50-132">toocall 하거나 Swagger 문서를 노출 하는 Api를 포함 하 여 모든 API hello로 요청을 만들고 항상 [HTTP 동작](../connectors/connectors-native-http.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="d7c50-133">호출 tooyour 사용자 지정 API를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="d7c50-134">다음과 같은이 방법으로 tooyour 사용자 지정 API 호출을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="d7c50-135">[코드 변경 없이](#no-code):에서 API 보호 [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) hello Azure 포털을 통해 하므로 없습니다 tooupdate 코드 했거나 API를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d7c50-136">기본적으로 hello Azure 포털에서에서 켜면 hello Azure AD 인증 세분화 된 권한 부여를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="d7c50-137">예를 들어 특정 테 넌 트, 사용자가 아닌 tooa 특정 사용자 또는 앱이이 인증 API toojust를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="d7c50-138">[API 코드 업데이트](#update-code) - 코드를 통해 [인증서 인증](#certificate), [기본 인증](#basic) 또는 [Azure AD 인증](#azure-ad-code)을 적용하여 API를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="d7c50-139">코드를 변경 하지 않고 호출 tooyour API 인증</span><span class="sxs-lookup"><span data-stu-id="d7c50-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="d7c50-140">이 메서드에 대 한 hello 일반적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="d7c50-141">두 개의 [Azure AD(Azure Active Directory) 응용 프로그램 ID](../app-service-api/app-service-api-dotnet-service-principal-auth.md)를 만듭니다. 하나는 논리 앱용이고 다른 하나는 웹앱용(또는 API 앱용)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="d7c50-142">tooauthenticate 호출 tooyour API hello 자격 증명 (클라이언트 ID 및 암호)를 사용 하 여 hello에 대 한 [서비스 사용자](../app-service-api/app-service-api-dotnet-service-principal-auth.md) 연관 된 hello 논리 앱에 대 한 Azure AD 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="d7c50-143">논리 앱 정의에 hello 응용 프로그램 Id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="d7c50-144">1부: 논리 앱의 Azure AD 응용 프로그램 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="d7c50-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="d7c50-145">논리 앱이 Azure AD 응용 프로그램 identity tooauthenticate를 Azure AD 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="d7c50-146">이 id tooset 디렉터리에 대해 한 번만 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="d7c50-147">예를 들어 선택할 수 있습니다 각 논리 앱에 대 한 고유 id를 만들 수 있지만 toouse hello 모든 논리 앱에 동일한 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="d7c50-148">Hello Azure 포털에서에서 이러한 id를 설정할 수 있습니다 [Azure 클래식 포털](#app-identity-logic-classic), 사용 또는 [PowerShell](#powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="d7c50-149">**논리 앱에 대 한 응용 프로그램 id hello hello Azure 포털에서 만들기**</span><span class="sxs-lookup"><span data-stu-id="d7c50-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="d7c50-150">Hello에 [Azure 포털](https://portal.azure.com "https://portal.azure.com"), 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="d7c50-151">Hello에 인지 확인 웹 응용 프로그램 또는 API 앱과 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="d7c50-152">tooswitch 디렉터리 사용자 프로필을 클릭 하 고 다른 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="d7c50-153">또는 **개요** > **디렉터리 전환**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="d7c50-154">Hello 디렉터리 메뉴 아래 **관리**, 선택 **앱 등록** > **새 응용 프로그램 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="d7c50-155">기본적으로 hello 응용 프로그램 등록 목록 디렉터리의 모든 응용 프로그램 등록을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="d7c50-156">사용자 응용 프로그램 등록만 다음 toohello 검색 상자 선택 tooview **My apps**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![새 앱 등록 만들기](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="d7c50-158">이름을 응용 프로그램 id를 제공 하 고, 유지 **응용 프로그램 종류** 도**웹 응용 프로그램 / API**, 고유한 제공에 대 한 도메인으로 형식이 지정 된 문자열 **로그온 URL**, 선택 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![응용 프로그램 ID의 이름 및 로그인 URL 제공](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="d7c50-160">새로 만든 논리 앱에 대 한 hello 응용 프로그램 id hello 응용 프로그램 등록 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![논리 앱의 응용 프로그램 ID](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="d7c50-162">Hello 앱 등록 목록에 새 응용 프로그램 id를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="d7c50-163">복사 하 고 hello 저장 **응용 프로그램 ID** toouse 3 부에서는 논리 앱에 대 한 "클라이언트 ID" hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![논리 앱의 응용 프로그램 ID 복사 및 저장](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="d7c50-165">응용 프로그램 ID 설정이 표시되지 않으면 **설정** 또는 **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="d7c50-166">**API 액세스** 아래에서 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="d7c50-167">**설명** 아래에서 키의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="d7c50-168">**만료** 아래에서 키의 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="d7c50-169">사용자가 만드는 hello 키 hello 응용 프로그램 id "보안" 기간 또는 암호 논리 앱에 대 한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![논리 앱 ID의 키 만들기](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="d7c50-171">Hello 도구 모음에서 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="d7c50-172">이제 **값** 아래에서 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="d7c50-173">**있는지 toocopy 하 고 키를 저장할** 나중에 사용할 hello 키 숨겨져 있기 때문에 두면 hello 키 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="d7c50-174">3 부에서는 논리 앱을 구성할 때 "보안" 또는 암호 hello 대로이 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![나중을 위한 키 복사 및 저장](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="d7c50-176">**논리 앱에 대 한 응용 프로그램 id hello hello Azure 클래식 포털에서 만들기**</span><span class="sxs-lookup"><span data-stu-id="d7c50-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="d7c50-177">Hello Azure 클래식 포털에서 선택 [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="d7c50-178">선택 hello 웹 응용 프로그램 또는 API 응용 프로그램에 사용 되는 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="d7c50-179">Hello에 **응용 프로그램** 탭에서 선택 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="d7c50-180">응용 프로그램 ID의 이름을 지정하고 **다음**(오른쪽 화살표)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="d7c50-181">**앱 속성** 아래에서 **로그인 URL** 및 **앱 ID URI**에 대한 도메인으로 형식이 지정된 고유 문자열을 제공하고 **완료**를 선택합니다(확인 표시).</span><span class="sxs-lookup"><span data-stu-id="d7c50-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="d7c50-182">Hello에 **구성** 탭, 복사 및 저장 hello **클라이언트 ID** 3 부에서는 논리 앱 toouse 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="d7c50-183">아래 **키**개방형 hello **기간 선택** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="d7c50-184">키의 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-184">Select a duration for your key.</span></span>

   <span data-ttu-id="d7c50-185">사용자가 만드는 hello 키 hello 응용 프로그램 id "보안" 기간 또는 암호 논리 앱에 대 한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="d7c50-186">Hello 페이지의 hello 맨 아래에 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="d7c50-187">Toowait 몇 초 정도 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="d7c50-188">아래 **키**toocopy 있는지를 확인 하 고 이제 나타나는 hello 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="d7c50-189">3 부에서는 논리 앱을 구성할 때 "보안" 또는 암호 hello 대로이 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="d7c50-190">자세한 내용은 자세한 방법을 너무 [앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인 구성](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="d7c50-191">**PowerShell에서 논리 앱에 대 한 hello 응용 프로그램 id 만들기**</span><span class="sxs-lookup"><span data-stu-id="d7c50-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="d7c50-192">PowerShell과 함께 Azure Resource Manager를 통해 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="d7c50-193">PowerShell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="d7c50-194">있는지 toocopy hello 확인 **테 넌 트 ID** (GUID)를 사용 하 여 Azure AD 테 넌 트에 대 한 hello **응용 프로그램 ID**, 및 hello 사용한 암호를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="d7c50-195">자세한 내용은 자세한 방법을 너무 [PowerShell tooaccess 리소스 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="d7c50-196">2부: 웹앱 또는 API 앱의 Azure AD 응용 프로그램 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="d7c50-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="d7c50-197">웹 앱 또는 API 앱은 이미 배포 된 경우 인증을 설정 하 고 hello 응용 프로그램 id hello Azure 포털에서에서 만든 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="d7c50-198">그렇지 않으면 [Azure Resource Manager 템플릿으로 배포할 때 인증을 설정](#authen-deploy)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="d7c50-199">**Hello 응용 프로그램 id를 만들고 hello 배포 된 앱 용 Azure 포털에서에서 인증 설정**</span><span class="sxs-lookup"><span data-stu-id="d7c50-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="d7c50-200">Hello에 [Azure 포털](https://portal.azure.com "https://portal.azure.com")찾아 웹 응용 프로그램 또는 API 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="d7c50-201">**설정**에서 **인증/권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="d7c50-202">**App Service 인증** 아래에서 인증을 **설정**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="d7c50-203">**인증 공급자** 아래에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![인증 설정](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="d7c50-205">이제 다음과 같이 웹앱 또는 API 앱의 응용 프로그램 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="d7c50-206">Hello에 **Azure Active Directory 설정** 설정 블레이드에서 **관리 모드** 너무**Express**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="d7c50-207">**새 AD 앱 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="d7c50-208">응용 프로그램 ID의 이름을 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![웹앱 또는 API 앱의 응용 프로그램 ID 만들기](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="d7c50-210">Hello에 **인증 / 권한 부여 블레이드**, 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="d7c50-211">이제 hello 클라이언트 ID를 찾아 웹 앱 또는 API 앱와 관련 된 hello 응용 프로그램 id에 대 한 테 넌 트 ID 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="d7c50-212">이러한 ID는 3부에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="d7c50-213">따라서 hello Azure 포털에 대해 다음이 단계를 계속 또는 [Azure 클래식 포털](#find-id-classic)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="d7c50-214">**응용 프로그램 id의 클라이언트 ID를 찾아 웹 응용 프로그램 또는 hello Azure 포털에서에서 API 앱에 대 한 테 넌 트 ID**</span><span class="sxs-lookup"><span data-stu-id="d7c50-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="d7c50-215">**인증 공급자** 아래에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   !["Azure Active Directory"를 선택합니다.](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="d7c50-217">Hello에 **Azure Active Directory 설정** 설정 블레이드에서 **관리 모드** 너무**고급**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="d7c50-218">복사 hello **클라이언트 ID**, 파트 3에서 사용 하기 위해 해당 GUID를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="d7c50-219">경우 **클라이언트 ID** 및 **발급자 Url** 표시, hello Azure 포털을 새로 고쳐 보세요 및 1 단계를 반복 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="d7c50-220">아래 **발급자 Url**, 복사 및 저장 방금 hello GUID 파트 3에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="d7c50-221">필요한 경우 웹앱 또는 API 앱의 배포 템플릿에서 이 GUID를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="d7c50-222">이 GUID는 특정 테넌트의 GUID("테넌트 ID")이며 `https://sts.windows.net/{GUID}` URL에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="d7c50-223">변경 내용을 저장 하지 않고 닫습니다 hello **Azure Active Directory 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="d7c50-224">**응용 프로그램 id의 클라이언트 ID를 찾아 웹 응용 프로그램 또는 hello Azure 클래식 포털에서에서 API 앱에 대 한 테 넌 트 ID**</span><span class="sxs-lookup"><span data-stu-id="d7c50-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="d7c50-225">Hello Azure 클래식 포털에서 선택 [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="d7c50-226">웹 앱 또는 API 응용 프로그램에 사용 하는 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="d7c50-227">Hello에 **검색** 상자, 찾아 웹 응용 프로그램 또는 API 앱에 대 한 hello 응용 프로그램 id를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="d7c50-228">Hello에 **구성** 탭, 복사 hello **클라이언트 ID**, 파트 3에서 사용 하기 위해 해당 GUID를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="d7c50-229">Hello hello 맨 아래에 hello 클라이언트 ID를 가져온 후 **구성** 탭에서 선택 **끝점 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="d7c50-230">Hello URL을 복사 **페더레이션 메타 데이터 문서**, toothat URL를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="d7c50-231">열리면 hello 메타 데이터 문서에 hello 루트를 찾을 **EntityDescriptor ID** 요소를 한 **entityID** 이러한 형식 특성:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="d7c50-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="d7c50-232">이 특성에 GUID hello은 특정 테 넌 트의 GUID (테 넌 트 ID)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="d7c50-233">Hello 테 넌 트 ID를 복사 하 고 필요한 경우 해당 ID를 사용 하기 위해 파트 3 및 웹 응용 프로그램 또는 API 응용 프로그램의 배포 템플릿에 toouse 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="d7c50-234">자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7c50-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="d7c50-235">Azure App Service의 API 앱에 대한 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d7c50-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="d7c50-236">Azure 앱 서비스의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="d7c50-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="d7c50-237">**Azure Resource Manager 템플릿으로 배포할 때 인증 설정**</span><span class="sxs-lookup"><span data-stu-id="d7c50-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="d7c50-238">논리 앱에 대 한 hello 응용 프로그램 id에서 웹 앱 또는 다른 API 앱에 대 한 Azure AD 응용 프로그램 id를 만들 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="d7c50-239">toocreate hello 응용 프로그램 id, 이전에 따라 hello 2 부의에서 Azure 포털 hello에 대 한 단계.</span><span class="sxs-lookup"><span data-stu-id="d7c50-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="d7c50-240">또한 1 부의에서 hello 단계를 수행 수 있지만 웹 앱 또는 API 응용 프로그램의 실제 있는지 toouse 확인 `https://{URL}` 에 대 한 **로그온 URL** 및 **앱 ID URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="d7c50-241">다음이 단계에서 있는 toosave hello 클라이언트 ID 및 앱의 배포 서식 파일에 사용할 및 파트 3에 대 한 테 넌 트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c50-242">웹 앱 또는 API 앱에 대 한 hello Azure AD 응용 프로그램 id를 만들 때 PowerShell 대신 hello Azure 포털 또는 Azure 클래식 포털을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="d7c50-243">hello PowerShell commandlet toosign 사용자 웹 사이트에 필요한 hello 권한을 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="d7c50-244">Hello 클라이언트 ID 및 테 넌 트 ID를 얻은 후 웹 응용 프로그램 또는 배포 서식 파일에서 API 앱 subresource로 이러한 Id를 포함:</span><span class="sxs-lookup"><span data-stu-id="d7c50-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="d7c50-245">tooautomatically 빈 웹 앱 및 Azure Active Directory 인증을 함께 논리 앱 배포 [hello 전체 템플릿 보기 여기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), 하거나 클릭 **tooAzure 배포** 여기:</span><span class="sxs-lookup"><span data-stu-id="d7c50-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="d7c50-246">[![TooAzure 배포](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d7c50-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="d7c50-247">3 부: hello Authorization 섹션 논리 앱에서 채우기</span><span class="sxs-lookup"><span data-stu-id="d7c50-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="d7c50-248">hello 이전 서식 파일에 이미 설정, 권한 부여 절이 있지만 hello 논리 앱을 직접 제작 하는 경우 hello 전체 권한 부여 섹션도 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="d7c50-249">논리 앱 정의 이동 toohello 코드 뷰에서 엽니다 **HTTP** 작업 섹션, 찾기 hello **권한 부여** 섹션을이 줄을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="d7c50-250">요소</span><span class="sxs-lookup"><span data-stu-id="d7c50-250">Element</span></span> | <span data-ttu-id="d7c50-251">설명</span><span class="sxs-lookup"><span data-stu-id="d7c50-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="d7c50-252">tenant</span><span class="sxs-lookup"><span data-stu-id="d7c50-252">tenant</span></span> |<span data-ttu-id="d7c50-253">hello Azure AD 테 넌 트에 대 한 hello GUID</span><span class="sxs-lookup"><span data-stu-id="d7c50-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="d7c50-254">audience</span><span class="sxs-lookup"><span data-stu-id="d7c50-254">audience</span></span> |<span data-ttu-id="d7c50-255">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-255">Required.</span></span> <span data-ttu-id="d7c50-256">tooaccess-웹 응용 프로그램 또는 API 앱에 대 한 응용 프로그램 id hello에서에서 hello 클라이언트 ID를 지정 하는 hello 대상 리소스에 대 한 hello GUID</span><span class="sxs-lookup"><span data-stu-id="d7c50-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="d7c50-257">clientId</span><span class="sxs-lookup"><span data-stu-id="d7c50-257">clientId</span></span> |<span data-ttu-id="d7c50-258">액세스-hello 클라이언트 ID 논리 앱에 대 한 hello 응용 프로그램 id에서 요청 하는 hello 클라이언트에 대 한 hello GUID</span><span class="sxs-lookup"><span data-stu-id="d7c50-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="d7c50-259">secret</span><span class="sxs-lookup"><span data-stu-id="d7c50-259">secret</span></span> |<span data-ttu-id="d7c50-260">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-260">Required.</span></span> <span data-ttu-id="d7c50-261">hello 키 또는 암호가 hello 액세스 토큰을 요청 하는 hello 클라이언트에 대 한 hello 응용 프로그램 id에서</span><span class="sxs-lookup"><span data-stu-id="d7c50-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="d7c50-262">type</span><span class="sxs-lookup"><span data-stu-id="d7c50-262">type</span></span> |<span data-ttu-id="d7c50-263">hello 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-263">hello authentication type.</span></span> <span data-ttu-id="d7c50-264">ActiveDirectoryOAuth 인증 hello 값은 `ActiveDirectoryOAuth`합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="d7c50-265">예:</span><span class="sxs-lookup"><span data-stu-id="d7c50-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="d7c50-266">코드를 통한 API 호출 보호</span><span class="sxs-lookup"><span data-stu-id="d7c50-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="d7c50-267">인증서 인증</span><span class="sxs-lookup"><span data-stu-id="d7c50-267">Certificate authentication</span></span>

<span data-ttu-id="d7c50-268">논리 앱 tooyour 웹 앱 또는 API 앱에서 toovalidate hello의 들어오는 요청을 클라이언트 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="d7c50-269">프로그램 코드를 tooset 알아봅니다 [어떻게 tooconfigure TLS 상호 인증](../app-service-web/app-service-web-configure-tls-mutual-auth.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="d7c50-270">Hello에 **권한 부여** 섹션에서이 줄을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="d7c50-271">요소</span><span class="sxs-lookup"><span data-stu-id="d7c50-271">Element</span></span> | <span data-ttu-id="d7c50-272">설명</span><span class="sxs-lookup"><span data-stu-id="d7c50-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="d7c50-273">type</span><span class="sxs-lookup"><span data-stu-id="d7c50-273">type</span></span> |<span data-ttu-id="d7c50-274">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-274">Required.</span></span> <span data-ttu-id="d7c50-275">hello 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-275">hello authentication type.</span></span> <span data-ttu-id="d7c50-276">SSL 클라이언트 인증서에 대 한 hello 값 이어야 합니다 `ClientCertificate`합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="d7c50-277">암호</span><span class="sxs-lookup"><span data-stu-id="d7c50-277">password</span></span> |<span data-ttu-id="d7c50-278">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-278">Required.</span></span> <span data-ttu-id="d7c50-279">hello 클라이언트 인증서 (PFX 파일)에 액세스 하기 위한 hello 암호</span><span class="sxs-lookup"><span data-stu-id="d7c50-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="d7c50-280">pfx</span><span class="sxs-lookup"><span data-stu-id="d7c50-280">pfx</span></span> |<span data-ttu-id="d7c50-281">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-281">Required.</span></span> <span data-ttu-id="d7c50-282">Hello 클라이언트 인증서 (PFX 파일)의 Base64 인코딩 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="d7c50-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="d7c50-283">기본 인증</span><span class="sxs-lookup"><span data-stu-id="d7c50-283">Basic authentication</span></span>

<span data-ttu-id="d7c50-284">toovalidate 논리 앱 tooyour 웹 앱 또는 API 앱에서 들어오는 요청을 사용자 이름 및 암호와 같은 기본 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="d7c50-285">기본 인증은 일반적인 패턴 및 웹 앱 또는 API 앱이이 인증에 사용 되는 언어 toobuild 모든를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="d7c50-286">Hello에 **권한 부여** 섹션에서이 줄을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="d7c50-287">`{"type": "basic", "username": "username", "password": "password"}`</span><span class="sxs-lookup"><span data-stu-id="d7c50-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="d7c50-288">요소</span><span class="sxs-lookup"><span data-stu-id="d7c50-288">Element</span></span> | <span data-ttu-id="d7c50-289">설명</span><span class="sxs-lookup"><span data-stu-id="d7c50-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7c50-290">type</span><span class="sxs-lookup"><span data-stu-id="d7c50-290">type</span></span> |<span data-ttu-id="d7c50-291">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-291">Required.</span></span> <span data-ttu-id="d7c50-292">hello 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-292">hello authentication type.</span></span> <span data-ttu-id="d7c50-293">기본 인증에 대 한 hello 값 이어야 합니다 `Basic`합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="d7c50-294">username</span><span class="sxs-lookup"><span data-stu-id="d7c50-294">username</span></span> |<span data-ttu-id="d7c50-295">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-295">Required.</span></span> <span data-ttu-id="d7c50-296">인증에 대 한 hello 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="d7c50-296">hello username for authentication</span></span> |
| <span data-ttu-id="d7c50-297">암호</span><span class="sxs-lookup"><span data-stu-id="d7c50-297">password</span></span> |<span data-ttu-id="d7c50-298">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-298">Required.</span></span> <span data-ttu-id="d7c50-299">인증에 대 한 hello 암호</span><span class="sxs-lookup"><span data-stu-id="d7c50-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="d7c50-300">코드를 통한 Azure Active Directory 인증</span><span class="sxs-lookup"><span data-stu-id="d7c50-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="d7c50-301">기본적으로 hello Azure 포털에서에서 켜면 hello Azure AD 인증 세분화 된 권한 부여를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="d7c50-302">예를 들어 특정 테 넌 트, 사용자가 아닌 tooa 특정 사용자 또는 앱이이 인증 API toojust를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="d7c50-303">코드를 통해 toorestrict API 액세스 tooyour 논리 앱 hello 포함 된 헤더를 hello JSON 웹 토큰 (JWT)을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="d7c50-304">Hello 호출자의 id를 확인 하 고 일치 하지 않는 요청을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="d7c50-305">계속 tooimplement 완전히 프로그램 코드 및 하지 사용 하 여 hello Azure 포털에서이 인증에 알아봅니다 너무 어떻게 [Azure 응용 프로그램에서 온-프레미스 Active Directory를 사용 하 여 인증](../app-service-web/web-sites-authentication-authorization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="d7c50-306">논리 앱에 대 한 응용 프로그램 id toocreate identity toocall 해당 API를 사용 하 고, hello 이전 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7c50-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7c50-307">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7c50-307">Next steps</span></span>

* [<span data-ttu-id="d7c50-308">진단 로그 및 경고를 사용하여 논리 앱 성능 확인</span><span class="sxs-lookup"><span data-stu-id="d7c50-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)