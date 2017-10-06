---
title: "Azure Active Directory 및 API 관리 웹 API 백 엔드 aaaProtect | Microsoft Docs"
description: "자세한 내용은 방법 tooprotect을 웹 API 백 엔드 Azure Active Directory 및 API 관리 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="810f2-103">어떻게 tooprotect을 웹 API 백 엔드 Azure Active Directory 및 API 관리</span><span class="sxs-lookup"><span data-stu-id="810f2-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="810f2-104">비디오 표시 방법을 따르는 hello toobuild 웹 API 백 엔드 고 OAuth 2.0 프로토콜을 사용 하 여 Azure Active Directory 및 API 관리를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="810f2-105">Hello 비디오에서 단계 hello에 대 한 추가 정보 및이 문서 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="810f2-106">이 24분 비디오에서는 다음을 수행할 수 있는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="810f2-107">Web API 백 엔드 빌드 및 AAD로 보안 유지 - 1시 30분에 시작</span><span class="sxs-lookup"><span data-stu-id="810f2-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="810f2-108">API 관리-7시 10분부터 hello API 가져오기</span><span class="sxs-lookup"><span data-stu-id="810f2-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="810f2-109">Hello 개발자 포털 toocall hello API-9시 09분부터 구성</span><span class="sxs-lookup"><span data-stu-id="810f2-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="810f2-110">데스크톱 응용 프로그램 toocall hello API-18시 08분에서 시작 구성</span><span class="sxs-lookup"><span data-stu-id="810f2-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="810f2-111">JWT 유효성 검사 정책 toopre 구성-요청 수-20시 47분부터 권한 부여</span><span class="sxs-lookup"><span data-stu-id="810f2-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="810f2-112">Azure AD 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="810f2-112">Create an Azure AD directory</span></span>
<span data-ttu-id="810f2-113">웹 API 있어야 하는 Azure Active Directory를 사용 하 여 백업 toosecure는 AAD 테 넌 트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="810f2-114">이 비디오에서는 **APIMDemo** 라는 테넌트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="810f2-115">AAD 테 넌 트가 toocreate 로그인 toohello [Azure 클래식 포털](https://manage.windowsazure.com) 클릭 **새로**->**응용 프로그램 서비스**->**Active 디렉터리**->**디렉터리**->**사용자 지정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="810f2-117">이 예에서 **APIMDemo**라는 디렉터리는 **DemoAPIM.onmicrosoft.com**이라는 기본 도메인 이름으로 만들어집니다. 이 디렉터리는 hello 비디오 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="810f2-119">Azure Active Directory로 보안이 유지된 Web API 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="810f2-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="810f2-120">이 단계에서는 Web API 백 엔드는 Visual Studio 2013을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="810f2-121">Hello 비디오의이 단계 1시 30분부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="810f2-122">Visual Studio에서 toocreate 웹 API 백 엔드 프로젝트 **파일**->**새로**->**프로젝트**, 선택 **ASP.NET 웹 응용 프로그램** hello에서 **웹** 템플릿 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="810f2-123">이 비디오 hello 프로젝트 이름은 **APIMAADDemo**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="810f2-124">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="810f2-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="810f2-126">클릭 **웹 API** hello에서 **템플릿 목록 선택** toocreate 웹 API 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="810f2-127">Azure Directory 인증 tooconfigure 클릭 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![새 프로젝트][api-management-new-project]

<span data-ttu-id="810f2-129">클릭 **조직 계정**, hello 지정 **도메인** AAD 테 넌 트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="810f2-130">이 예제에서는 hello 도메인은 **DemoAPIM.onmicrosoft.com**. hello에서 디렉터리의 hello 도메인을 가져올 수 있습니다 **도메인** 디렉터리의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![도메인][api-management-aad-domains]

<span data-ttu-id="810f2-132">Hello에서 원하는 hello 설정을 구성 **인증 변경** 대화 상자와 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![인증 변경][api-management-change-authentication]

<span data-ttu-id="810f2-134">클릭할 때 **확인** Visual Studio는 tooregister Azure AD 디렉터리와 응용 프로그램 변수와 Visual Studio에서의 증명된 toosign 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="810f2-135">디렉터리에 대한 관리 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-135">Sign in using an administrative account for your directory.</span></span>

![TooVisual Studio에 로그인][api-management-sign-in-vidual-studio]

<span data-ttu-id="810f2-137">tooconfigure Azure 웹 API 검사 hello로이 프로젝트에 대 한 상자 **hello 클라우드의 호스트에에서** 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![새 프로젝트][api-management-new-project-cloud]

<span data-ttu-id="810f2-139">TooAzure에서 증명된 toosign 수 및 다음 hello 웹 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![구성][api-management-configure-web-app]

<span data-ttu-id="810f2-141">이 예에서는 **APIMAADDemo**라는 새 **App Service 계획**이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="810f2-142">클릭 **확인** tooconfigure hello 웹 앱을 hello 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="810f2-143">Hello 코드 toohello 웹 API 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="810f2-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="810f2-144">hello hello 비디오의 다음 단계는 hello 코드 toohello 웹 API 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="810f2-145">이 단계는 4분 35초에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-145">This step starts at 4:35.</span></span>

<span data-ttu-id="810f2-146">이 예에서 웹 API hello 모델과 컨트롤러를 사용 하 여 기본 계산기 서비스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="810f2-147">hello 서비스에 대 한 tooadd hello 모델 마우스 오른쪽 단추로 클릭 **모델** 에 **솔루션 탐색기** 선택 **추가**, **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="810f2-148">Hello 클래스 이름을 `CalcInput` 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="810f2-149">Hello 다음 추가 `using` 문 toohello 맨 hello `CalcInput.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="810f2-150">Replace hello 코드 다음 hello를 사용 하 여 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="810f2-151">**솔루션 탐색기**에서 **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 **추가**->**컨트롤러**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="810f2-152">**Web API 2 컨트롤러 - 비어 있음**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="810f2-153">형식 **CalcController** hello 컨트롤러에 대 한 이름을 지정 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![컨트롤러 추가][api-management-add-controller]

<span data-ttu-id="810f2-155">Hello 다음 추가 `using` 문 toohello 맨 hello `CalcController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="810f2-156">Replace hello 코드 다음 hello를 사용 하 여 컨트롤러 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="810f2-157">이 코드 구현 hello `Add`, `Subtract`, `Multiply`, 및 `Divide` hello 기본 계산기 API의 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="810f2-158">키를 눌러 **F6** toobuild hello 솔루션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="810f2-159">Hello 프로젝트 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="810f2-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="810f2-160">이 단계 hello Visual Studio 프로젝트는 게시 된 tooAzure입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="810f2-161">이 단계를 hello 비디오 5시 45분에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="810f2-162">toopublish 프로젝트 tooAzure hello, hello를 마우스 오른쪽 단추로 클릭 **APIMAADDemo** Visual Studio에서 프로젝트를 마우스 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="810f2-163">Hello hello 기본 설정을 유지 **웹 게시** 대화 상자와 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![웹 게시][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="810f2-165">Azure AD toohello 백 엔드 서비스 응용 프로그램 사용 권한 부여</span><span class="sxs-lookup"><span data-stu-id="810f2-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="810f2-166">Hello 백 엔드 서비스에 대 한 새 응용 프로그램 부분 hello 구성 및 게시 프로세스의 웹 API 프로젝트에 Azure AD 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="810f2-167">Hello 비디오의이 단계에서는 6시 13분부터 권한은 부여 toohello 웹 API 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![응용 프로그램][api-management-aad-backend-app]

<span data-ttu-id="810f2-169">Hello 응용 프로그램 tooconfigure hello 필요한 사용 권한 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="810f2-170">Toohello 이동 **구성** 탭과 toohello 아래로 스크롤하여 **tooother 응용 프로그램 사용 권한** 섹션.</span><span class="sxs-lookup"><span data-stu-id="810f2-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="810f2-171">Hello 클릭 **응용 프로그램 사용 권한** 옆에 있는 드롭 다운 **Windows** **Azure Active Directory**에 대 한 hello 확인란 **디렉터리데이터읽기**를 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![권한 추가][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="810f2-173">경우 **Windows** **Azure Active Directory** 가 나타나지 않으면 tooother 응용 프로그램 사용 권한 아래에서 클릭 **응용 프로그램을 추가** hello 목록에서 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="810f2-174">Hello 메모 **앱 Id URI** hello API 관리 개발자 포털에 대 한 Azure AD 응용 프로그램 구성 된 경우 이후 단계에서 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![앱 ID URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="810f2-176">가져오기 hello API 관리에 웹 API</span><span class="sxs-lookup"><span data-stu-id="810f2-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="810f2-177">Api는 hello Azure 포털을 통해 액세스할 수 있는 hello API 게시자 포털에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="810f2-178">tooreach, 클릭 **게시자 포털** API 관리 서비스의 hello 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="810f2-179">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [첫 번째 API 관리] [ Manage your first API] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="810f2-181">작업 수 [tooAPIs를 수동으로 추가](api-management-howto-add-operations.md), 가져왔거나 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="810f2-182">이 비디오에서는 작업을 6분 40초부터 Swagger 형식으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="810f2-183">라는 파일을 만들어 `calcapi.json` 와 콘텐츠를 따르고 tooyour 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="810f2-184">해당 hello 확인 `host` 특성 tooyour 웹 API 백 엔드를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="810f2-185">이 예에서는 `"host": "apimaaddemo.azurewebsites.net"` 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="810f2-186">tooimport hello 계산기 API 클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **가져오기 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![API 가져오기 단추][api-management-import-api]

<span data-ttu-id="810f2-188">Hello 단계 tooconfigure hello 계산기 API 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="810f2-189">클릭 **파일에서**, toohello 찾아보기 `calculator.json` 파일을 저장 하 고 hello 클릭 **Swagger** 라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="810f2-190">형식 **calc** hello에 **웹 API URL 접미사** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="810f2-191">Hello에 클릭 **(선택 사항) 제품** 확인란을 선택한 **스타터**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="810f2-192">클릭 **저장** tooimport hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-192">Click **Save** tooimport hello API.</span></span>

![새 API 추가][api-management-import-new-api]

<span data-ttu-id="810f2-194">가져온 hello API는 hello hello API에 대 한 요약 페이지에에서 표시 됩니다 hello 게시자 포털.</span><span class="sxs-lookup"><span data-stu-id="810f2-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="810f2-195">Hello 개발자 포털에서 실패 한 hello API를 호출</span><span class="sxs-lookup"><span data-stu-id="810f2-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="810f2-196">이 시점에서 hello API API 관리에 가져온 하지만 없습니다 아직에서 호출할 수 성공적으로 hello 개발자 포털 hello 백 엔드 서비스는 Azure AD 인증으로 보호 되어야 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="810f2-197">이 단계를 수행 하는 hello를 사용 하 여 7시 40분에서 시작 하는 hello 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="810f2-198">클릭 **개발자 포털** hello 게시자 포털의 상단 오른쪽 면 hello에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="810f2-200">클릭 **Api** hello 클릭 **계산기** API입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-200">Click **APIs** and click hello **Calculator** API.</span></span>

![개발자 포털][api-management-dev-portal-apis]

<span data-ttu-id="810f2-202">**사용해 보세요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-202">Click **Try it**.</span></span>

![시도][api-management-dev-portal-try-it]

<span data-ttu-id="810f2-204">클릭 **보낼** 의 hello 응답 상태를 확인 하 고 **401 권한 없음**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![보내기][api-management-dev-portal-send-401]

<span data-ttu-id="810f2-206">hello 백 엔드 API은 Azure Active Directory로 보호 되어 hello 요청이 인증 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="810f2-207">성공적으로 hello API를 호출 하기 전에 hello 개발자 포털 구성된 tooauthorize 개발자가 OAuth 2.0을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="810f2-208">이 프로세스는 hello 다음 섹션에에서 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="810f2-209">Hello 개발자 포털 AAD 응용 프로그램으로 등록</span><span class="sxs-lookup"><span data-stu-id="810f2-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="810f2-210">OAuth 2.0을 사용 하 여 hello 개발자 포털 tooauthorize 개발자 구성 hello 첫 번째 단계는 AAD 응용 프로그램으로 tooregister hello 개발자 포털을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="810f2-211">이 8:27 hello 비디오에서에서 시작 하는 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="810f2-212">이 예에서이 비디오의 hello 첫 번째 단계에서 toohello Azure AD 테 넌 트 탐색 **APIMDemo** toohello 이동 **응용 프로그램** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![새 응용 프로그램][api-management-aad-new-application-devportal]

<span data-ttu-id="810f2-214">Hello 클릭 **추가** toocreate 새 Azure Active Directory 응용 프로그램 단추 선택한 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![새 응용 프로그램][api-management-new-aad-application-menu]

<span data-ttu-id="810f2-216">선택 **웹 응용 프로그램 및/또는 Web API**는 이름을 입력 하 고 hello 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="810f2-217">이 예에서는 **APIMDeveloperPortal** 이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-217">In this example **APIMDeveloperPortal** is used.</span></span>

![새 응용 프로그램][api-management-aad-new-application-devportal-1]

<span data-ttu-id="810f2-219">에 대 한 **로그온 URL** API 관리 서비스의 hello URL을 입력 하 고 추가 `/signin`합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="810f2-220">이 예에서는 `https://contoso5.portal.azure-api.net/signin` 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="810f2-221">에 대 한 **앱 Id URL** API 관리 서비스의 hello URL을 입력 하 고 몇 가지 고유한 문자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="810f2-222">원하는 문자를 사용할 수 있으며 이 예에서는 `https://contoso5.portal.azure-api.net/dp`이(가) 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="810f2-223">Hello 필요한 경우 **앱 속성** 됩니다 구성 hello 확인 표시가 toocreate hello 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![새 응용 프로그램][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="810f2-225">API 관리 OAuth 2.0 권한 부여 서버 구성</span><span class="sxs-lookup"><span data-stu-id="810f2-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="810f2-226">hello 다음 단계는 tooconfigure API 관리에서 OAuth 2.0 권한 부여 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="810f2-227">이 단계를 hello 9:43 일에서 시작 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="810f2-228">클릭 **보안** hello 왼쪽에 hello API 관리 메뉴에서 클릭 **OAuth 2.0**, 클릭 하 고 **추가 권한 부여** 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server]

<span data-ttu-id="810f2-230">Hello에는 이름 및 선택적 설명을 입력 **이름** 및 **설명** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="810f2-231">이러한 필드는 hello API 관리 서비스 인스턴스 내에서 사용 되는 tooidentify hello OAuth 2.0 권한 부여 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="810f2-232">이 예에서 **권한 부여 서버 데모** 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="810f2-233">나중에 API에 대 한 인증에 사용 되는 OAuth 2.0 서버 toobe를 지정할 때이 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="810f2-234">Hello에 대 한 **클라이언트 등록 페이지 URL** 같은 자리 표시자 값을 입력 `http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="810f2-235">hello **클라이언트 등록 페이지 URL** toohello 페이지가 사용 하는 지점 toocreate를 사용 하 여를 업데이트 하 고 계정의 사용자 관리를 지 원하는 OAuth 2.0 공급자에 대 한 자신의 계정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="810f2-236">이 예에서 자리 표시자를 사용하도록 사용자는 자신의 계정을 만들거나 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-1]

<span data-ttu-id="810f2-238">그런 다음 **권한 부여 끝점 URL** 및**토큰 끝점 URL**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![권한 부여 서버][api-management-add-authorization-server-1a]

<span data-ttu-id="810f2-240">Hello에서 이러한 값을 검색할 수 **앱 끝점** hello hello 개발자 포털에 대해 생성 되는 AAD 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="810f2-241">tooaccess hello 끝점 이동 toohello **구성** hello AAD 응용 프로그램에 대 한 탭을 클릭 **끝점 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![응용 프로그램][api-management-aad-devportal-application]

![끝점 보기][api-management-aad-view-endpoints]

<span data-ttu-id="810f2-244">복사 hello **OAuth 2.0 권한 부여 끝점** hello에 붙여 넣습니다 **권한 부여 끝점 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-2]

<span data-ttu-id="810f2-246">복사 hello **OAuth 2.0 토큰 끝점** hello에 붙여 넣습니다 **끝점 URL 토큰** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-2a]

<span data-ttu-id="810f2-248">Hello 토큰 끝점에 toopasting 라는 추가 본문 매개 변수를 추가 하는 또한 **리소스** hello 값에 대 한 hello를 사용 하 여 **앱 Id URI** hello hello 백 엔드 서비스는 AAD 응용 프로그램에서 hello Visual Studio 프로젝트를 게시할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![앱 ID URI][api-management-aad-sso-uri]

<span data-ttu-id="810f2-250">다음으로 hello 클라이언트 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="810f2-251">원하는 hello 리소스에 대 한 자격 증명 hello 이들은 tooaccess,이 경우 개발자 포털을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![클라이언트 자격 증명][api-management-client-credentials]

<span data-ttu-id="810f2-253">tooget hello **클라이언트 Id**, toohello 이동 **구성** hello hello 개발자 포털 및 복사 hello에 대 한 AAD 응용 프로그램의 탭 **클라이언트 Id**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="810f2-254">tooget hello **클라이언트 암호** hello 클릭 **기간 선택** 드롭 다운 hello **키** 섹션 고 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="810f2-255">이 예제에서는 1년을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-255">In this example 1 year is used.</span></span>

![클라이언트 ID][api-management-aad-client-id]

<span data-ttu-id="810f2-257">클릭 **저장** toosave hello 구성 및 표시 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="810f2-258">이 키를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-258">Make a note of this key.</span></span> <span data-ttu-id="810f2-259">Hello Azure Active Directory 구성 창을 닫으면 되 면 hello 키를 다시 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="810f2-260">Hello 키 toohello 클립보드로 복사, 스위치 백 toohello 게시자 포털 hello에 hello 키를 붙여 **클라이언트 암호** 입력란을 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-3]

<span data-ttu-id="810f2-262">바로 뒤에 따라오는 hello 클라이언트 자격 증명은 인증 코드 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="810f2-263">이 권한 부여 코드를 복사 하 고 스위치 백 tooyour Azure AD 개발자 포털 응용 프로그램 페이지 및 hello 인증 부여 hello에 붙여 **회신 URL** 필드를 클릭 **저장** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![회신 URL][api-management-aad-reply-url]

<span data-ttu-id="810f2-265">hello 다음 단계는 hello 개발자 포털 AAD 응용 프로그램에 대 한 tooconfigure hello 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="810f2-266">클릭 **응용 프로그램 사용 권한** hello 상자를 선택 하 고 **디렉터리 데이터 읽기**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="810f2-267">클릭 **저장** toosave 변경 하 고 클릭이 **응용 프로그램을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![권한 추가][api-management-add-devportal-permissions]

<span data-ttu-id="810f2-269">Hello 검색 아이콘을 클릭 형식 **APIM** hello에 선택 상자 부터는 **APIMAADDemo**, hello 확인 표시가 toosave를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![권한 추가][api-management-aad-add-app-permissions]

<span data-ttu-id="810f2-271">클릭 **위임 된 권한** 에 대 한 **APIMAADDemo** hello 상자를 선택 하 고 **액세스 APIMAADDemo**를 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="810f2-272">이렇게 하면 hello 개발자 포털 응용 프로그램 tooaccess hello 백 엔드 서비스.</span><span class="sxs-lookup"><span data-stu-id="810f2-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![권한 추가][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="810f2-274">Hello 계산기 API에 대 한 OAuth 2.0 사용자 권한 부여를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="810f2-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="810f2-275">Hello OAuth 2.0 서버를 구성 하는 이제 API에 대 한 hello 보안 설정에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="810f2-276">이 단계를 hello 14시 30분부터 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="810f2-277">클릭 **Api** 에서 왼쪽된 메뉴 hello 하 고 클릭 **계산기** tooview 하 고 해당 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![계산기 API][api-management-calc-api]

<span data-ttu-id="810f2-279">Toohello 이동 **보안** 탭에서 확인 hello **OAuth 2.0** 확인란을 선택 하는 hello 원하는 권한 부여 서버 hello에서 **권한 부여 서버** 드롭 다운 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![계산기 API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="810f2-281">Hello 개발자 포털에서 hello 계산기 API를 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="810f2-282">Hello API에 hello OAuth 2.0 권한 부여가 구성 된 했으므로 hello 개발자 센터에서 해당 작업을 성공적으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="810f2-283">이 단계를 hello 15시 시작 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="810f2-284">뒤로 toohello 이동 **정수 두 개를 추가** hello 개발자 포털에서 hello 계산기 서비스의 작동 **실습**합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="810f2-285">참고 hello hello에 새 항목이 **권한 부여** 방금 추가한 해당 toohello 권한 부여 서버 섹션.</span><span class="sxs-lookup"><span data-stu-id="810f2-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![계산기 API][api-management-calc-authorization-server]

<span data-ttu-id="810f2-287">선택 **인증 코드** hello 권한 부여 드롭다운 목록에서에서 나열 하 고 hello 계정 toouse의 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="810f2-288">Hello 계정을 사용 하 여 이미 로그인 한 경우에 사용자에 메시지가 나타나지 않을.</span><span class="sxs-lookup"><span data-stu-id="810f2-288">If you are already signed in with hello account you may not be prompted.</span></span>

![계산기 API][api-management-devportal-authorization-code]

<span data-ttu-id="810f2-290">클릭 **보낼** 및 참고 hello **응답 상태** 의 **200 확인** 및 hello 응답 콘텐츠 hello 연산의 hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![계산기 API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="810f2-292">데스크톱 응용 프로그램 toocall hello API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="810f2-293">hello hello 비디오의 다음 절차는 16시 30분부터 시작 하 고 간단한 데스크톱 응용 프로그램 toocall hello API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="810f2-294">hello 첫 번째 단계는 tooregister hello 데스크톱 응용 프로그램에서 Azure AD는 하 고 액세스 toohello 디렉터리와 toohello 백 엔드 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="810f2-295">18:25 hello 데스크톱 응용 프로그램 호출 hello 계산기 API에 대 한 작업의 데모가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="810f2-296">JWT 유효성 검사 정책 toopre 구성-요청 권한 부여</span><span class="sxs-lookup"><span data-stu-id="810f2-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="810f2-297">hello hello 비디오에서 마지막 절차에서 시작 20시 48분을 표시 하는 toouse hello [JWT의 유효성을 검사](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) 정책 toopre-들어오는 각 요청의 hello 액세스 토큰을 확인 하 여 요청 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="810f2-298">Hello 요청 hello 정책 JWT의 유효성을 검사 하 여 검증 되지 않은 경우 hello 요청 API 관리에 의해 액세스가 차단 되 고 toohello 백 엔드를 따라 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="810f2-299">다른 구성 하 고이 정책을 사용 하 여 데모를 보려면을 참조 하십시오. [클라우드 포괄 에피소드 177: 더욱 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too13:50 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="810f2-300">Hello 정책 편집기에 구성 된 toosee hello 정책이 too15:00를 빨리 감기 및 too18:50 모두와 사용 하지 않는 hello hello 개발자 포털에서 호출 하는 작업의 데모에 대 한 권한 부여 토큰을 필요로 하는 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="810f2-301">다음 단계</span><span class="sxs-lookup"><span data-stu-id="810f2-301">Next steps</span></span>
* <span data-ttu-id="810f2-302">API 관리에 대한 추가 [비디오](https://azure.microsoft.com/documentation/videos/index/?services=api-management) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="810f2-303">다른 방법으로 toosecure에 대 한 백 엔드 서비스에서 참조 [상호 인증서 인증](api-management-howto-mutual-certificates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="810f2-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
