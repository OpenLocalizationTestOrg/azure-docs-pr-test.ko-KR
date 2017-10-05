---
title: "Azure Active Directory 및 API Management로 Web API 백 엔드 보호 | Microsoft Docs"
description: "Azure Active Directory 및 API 관리로 Web API 백 엔드를 보호하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="0a754-103">Azure Active Directory 및 API 관리로 Web API 백 엔드를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="0a754-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="0a754-104">다음 비디오에서는 Web API 백 엔드 빌드 및 Azure Active Directory 및 API 관리로 OAuth 2.0 프로토콜을 사용하여 보호하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="0a754-105">이 문서에서는 비디오로 해당 단계에 대한 개요 및 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="0a754-106">이 24분 비디오에서는 다음을 수행할 수 있는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="0a754-107">Web API 백 엔드 빌드 및 AAD로 보안 유지 - 1시 30분에 시작</span><span class="sxs-lookup"><span data-stu-id="0a754-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="0a754-108">API를 API 관리로 가져오기 - 7시 10분에 시작</span><span class="sxs-lookup"><span data-stu-id="0a754-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="0a754-109">API를 호출하도록 개발자 포털 구성 - 9시 9분에 시작</span><span class="sxs-lookup"><span data-stu-id="0a754-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="0a754-110">API를 호출하도록 데스크톱 응용 프로그램 구성 - 18시 8분에 시작</span><span class="sxs-lookup"><span data-stu-id="0a754-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="0a754-111">미리 요청 권한을 부여하도록 JWT 유효성 검사 정책 구성 - 20시 47분에 시작</span><span class="sxs-lookup"><span data-stu-id="0a754-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="0a754-112">Azure AD 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="0a754-112">Create an Azure AD directory</span></span>
<span data-ttu-id="0a754-113">Azure Active Directory를 사용하여 Web API 백 엔드를 보호하려면 먼저 AAD 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="0a754-114">이 비디오에서는 **APIMDemo** 라는 테넌트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="0a754-115">AAD 테넌트를 만들려면 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인하고 **새로 만들기**->**App Services**->**Active Directory**->**디렉터리**->**사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="0a754-117">이 예에서 **APIMDemo**라는 디렉터리는 **DemoAPIM.onmicrosoft.com**이라는 기본 도메인 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="0a754-118">이 디렉터리는 비디오 전체에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="0a754-120">Azure Active Directory로 보안이 유지된 Web API 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0a754-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="0a754-121">이 단계에서는 Web API 백 엔드는 Visual Studio 2013을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="0a754-122">이 단계의 비디오는 1분 30초에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="0a754-123">Visual Studio에서 Web API 백 엔드 프로젝트를 만들려면 **파일**->**새로 만들기**->**프로젝트**를 클릭하고 **웹** 템플릿 목록에서 **ASP.NET 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="0a754-124">이 비디오에서 프로젝트의 이름은 **APIMAADDemo**입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="0a754-125">**확인** 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="0a754-127">**템플릿 목록 선택**에서 **Web API**를 클릭하여 Web API 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="0a754-128">Azure 디렉터리의 인증을 구성하려면 **인증 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![새 프로젝트][api-management-new-project]

<span data-ttu-id="0a754-130">**조직 계정**을 클릭하고 AAD 테넌트의 **도메인**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="0a754-131">이 예에서 도메인은 **DemoAPIM.onmicrosoft.com**입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="0a754-132">디렉터리의 도메인은 디렉터리의 **도메인** 탭에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![도메인][api-management-aad-domains]

<span data-ttu-id="0a754-134">**인증 변경** 대화 상자에서 원하는 설정을 구성하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![인증 변경][api-management-change-authentication]

<span data-ttu-id="0a754-136">**확인** 을 클릭하면 Visual Studio는 Azure AD 디렉터리로 응용 프로그램을 등록하려고 하며 Visual Studio에서 로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="0a754-137">디렉터리에 대한 관리 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-137">Sign in using an administrative account for your directory.</span></span>

![Visual Studio에 로그인][api-management-sign-in-vidual-studio]

<span data-ttu-id="0a754-139">Azure Web API로 이 프로젝트를 구성하려면 **클라우드에서 호스트** 상자를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![새 프로젝트][api-management-new-project-cloud]

<span data-ttu-id="0a754-141">Azure에 로그인하라는 메시지가 표시될 수 있으며, 다음 웹앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![구성][api-management-configure-web-app]

<span data-ttu-id="0a754-143">이 예에서는 **APIMAADDemo**라는 새 **App Service 계획**이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="0a754-144">**확인** 을 클릭하여 웹앱을 구성하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="0a754-145">Web API 프로젝트에 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-145">Add the code to the Web API project</span></span>
<span data-ttu-id="0a754-146">비디오의 다음 단계는 Web API 프로젝트에 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="0a754-147">이 단계는 4분 35초에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-147">This step starts at 4:35.</span></span>

<span data-ttu-id="0a754-148">이 예에서 Web API는 모델과 컨트롤러를 사용하여 기본 계산기 서비스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="0a754-149">서비스에 대한 모델을 추가하려면 **솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="0a754-150">클래스의 이름을 `CalcInput` 로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="0a754-151">다음 `using` 명령문을 `CalcInput.cs` 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="0a754-152">생성된 클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="0a754-153">**솔루션 탐색기**에서 **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 **추가**->**컨트롤러**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="0a754-154">**Web API 2 컨트롤러 - 비어 있음**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="0a754-155">컨트롤러 이름으로 **CalcController**를 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![컨트롤러 추가][api-management-add-controller]

<span data-ttu-id="0a754-157">다음 `using` 명령문을 `CalcController.cs` 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="0a754-158">생성된 컨트롤러를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="0a754-159">이 코드는 기본 계산기 API의 `Add`, `Subtract`, `Multiply` 및 `Divide` 작업을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="0a754-160">**F6** 를 눌러 솔루션을 빌드하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="0a754-161">Azure에 프로젝트 게시</span><span class="sxs-lookup"><span data-stu-id="0a754-161">Publish the project to Azure</span></span>
<span data-ttu-id="0a754-162">이 단계에서 Visual Studio 프로젝트는 Azure에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="0a754-163">이 단계의 비디오는 5분 45초에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="0a754-164">프로젝트를 Azure에 게시하려면 Visual Studio에서 **APIMAADDemo** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="0a754-165">**웹 게시** 대화 상자에서 기본 설정을 유지하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![웹 게시][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="0a754-167">Azure AD 백 엔드 서비스 응용 프로그램에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="0a754-168">백 엔드 서비스에 대한 새 응용 프로그램은 Web API 프로젝트의 구성 및 게시 프로세스의 일부로 Azure AD 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="0a754-169">6분 13초에 시작하는 비디오의 이 단계에서는 Web API 백 엔드에 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![응용 프로그램][api-management-aad-backend-app]

<span data-ttu-id="0a754-171">필요한 권한을 구성하려면 응용 프로그램의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="0a754-172">**구성** 탭으로 이동하고 **다른 응용 프로그램에 권한 부여** 섹션으로 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="0a754-173">**Windows** **Azure Active Directory** 옆의 **응용 프로그램 사용 권한** 드롭다운을 클릭하고 **디렉터리 데이터 읽기** 상자를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![권한 추가][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="0a754-175">**Windows** **Azure Active Directory**가 다른 응용 프로그램에 대한 사용 권한에 나열되지 않으면 **응용 프로그램 추가**를 클릭하고 목록에서 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="0a754-176">Azure AD 응용 프로그램이 API 관리 개발자 포털에 대해 구성된 경우, 다음 단계에서 사용하도록 **앱 ID URI** 를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![앱 ID URI][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="0a754-178">Web API를 API 관리로 가져오기</span><span class="sxs-lookup"><span data-stu-id="0a754-178">Import the Web API into API Management</span></span>
<span data-ttu-id="0a754-179">API는 Azure Portal을 통해 액세스할 수 있는 API 게시자 포털에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="0a754-180">이 위치로 이동하려면 API Management 서비스의 도구 모음에서 **게시자 포털**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0a754-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="0a754-181">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [첫 번째 API Management][Manage your first API] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a754-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="0a754-183">작업을 [수동으로 API에 추가](api-management-howto-add-operations.md)하거나 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="0a754-184">이 비디오에서는 작업을 6분 40초부터 Swagger 형식으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="0a754-185">다음 내용을 포함한 `calcapi.json` 이라는 파일을 만들고 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="0a754-186">`host` 특성이 Web API 백 엔드를 가리키는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="0a754-187">이 예에서는 `"host": "apimaaddemo.azurewebsites.net"` 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="0a754-188">계산기 API를 가져오려면 왼쪽의 **API Management** 메뉴에서 **API**를 클릭한 다음 **API 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![API 가져오기 단추][api-management-import-api]

<span data-ttu-id="0a754-190">다음 단계를 수행하여 계산기 API를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="0a754-191">**파일에서**를 클릭하고 저장한 `calculator.json` 파일로 이동한 다음 **Swagger** 라디오 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="0a754-192">**웹 API URL 접미사** 텍스트 상자에 **calc**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="0a754-193">**제품(선택 사항)** 상자를 클릭하고 **시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="0a754-194">**저장** 을 클릭하여 API를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-194">Click **Save** to import the API.</span></span>

![새 API 추가][api-management-import-new-api]

<span data-ttu-id="0a754-196">API를 가져오면 API에 대한 요약 페이지가 게시자 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="0a754-197">개발자 포털에서 API 호출 실패</span><span class="sxs-lookup"><span data-stu-id="0a754-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="0a754-198">이 시점에서 API를 API 관리로 가져오지만, 백 엔드 서비스는 Azure AD 인증으로 보호되어야 하기 때문에 개발자 포털에서 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="0a754-199">다음 단계를 통해 7분 40초부터 시작되는 비디오에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="0a754-200">게시자 포털의 오른쪽 위에 있는 메뉴에서 **개발자 포털** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="0a754-202">**API**를 클릭하고 **계산기** API를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-202">Click **APIs** and click the **Calculator** API.</span></span>

![개발자 포털][api-management-dev-portal-apis]

<span data-ttu-id="0a754-204">**사용해 보세요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-204">Click **Try it**.</span></span>

![시도][api-management-dev-portal-try-it]

<span data-ttu-id="0a754-206">**보내기**를 클릭하여 **401 권한 없음**의 응답 상태를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![보내기][api-management-dev-portal-send-401]

<span data-ttu-id="0a754-208">백 엔드 API는 Azure Active Directory로 보호되기 때문에 요청이 인증되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="0a754-209">API를 성공적으로 호출하기 전에 개발자 포털은 OAuth 2.0을 사용하여 개발자에게 권한을 부여하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="0a754-210">이 프로세스는 다음 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="0a754-211">AAD 응용 프로그램으로 개발자 포털 등록</span><span class="sxs-lookup"><span data-stu-id="0a754-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="0a754-212">개발자가 OAuth 2.0을 사용하여 권한을 부여하도록 개발자 포털을 구성하는 첫 번째 단계는 AAD 응용 프로그램으로 개발자 포털을 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="0a754-213">8분 27초에 시작되는 비디오에서 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="0a754-214">이 비디오의 첫 번째 단계에서 Azure AD 테넌트로 이동하고, 이 예제 **APIMDemo**에서 **응용 프로그램** 탭 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![새 응용 프로그램][api-management-aad-new-application-devportal]

<span data-ttu-id="0a754-216">**추가** 단추를 클릭하여 새 Azure Active Directory 응용 프로그램을 만들고 **내 조직에서 개발 중인 응용 프로그램 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![새 응용 프로그램][api-management-new-aad-application-menu]

<span data-ttu-id="0a754-218">**웹 응용 프로그램 및/또는 Web API**를 선택하고 이름을 입력한 후 다음 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="0a754-219">이 예에서는 **APIMDeveloperPortal** 이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-219">In this example **APIMDeveloperPortal** is used.</span></span>

![새 응용 프로그램][api-management-aad-new-application-devportal-1]

<span data-ttu-id="0a754-221">**로그인 URL**로 API Management 서비스의 URL을 입력하고 `/signin`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="0a754-222">이 예에서는 `https://contoso5.portal.azure-api.net/signin` 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="0a754-223">**앱 ID URL**로 API Management 서비스의 URL을 입력하고 일부 고유 문자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="0a754-224">원하는 문자를 사용할 수 있으며 이 예에서는 `https://contoso5.portal.azure-api.net/dp`이(가) 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="0a754-225">원하는 **앱 속성**이 구성되면, 확인 표시를 클릭하여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![새 응용 프로그램][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="0a754-227">API 관리 OAuth 2.0 권한 부여 서버 구성</span><span class="sxs-lookup"><span data-stu-id="0a754-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="0a754-228">다음 단계는 API 관리에서의 OAuth 2.0 권한 부여 서버 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="0a754-229">이 단계는 9분 43초에 시작되는 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="0a754-230">왼쪽의 API Management 메뉴에서 **보안**을 클릭하고 **OAuth 2.0**을 클릭한 다음 **권한 부여 서버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server]

<span data-ttu-id="0a754-232">**이름** 필드에 이름을 입력하고 원하는 경우 **설명** 필드에 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="0a754-233">이러한 필드는 API 관리 서비스 인스턴스 내에서 OAuth 2.0 권한 부여 서버를 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="0a754-234">이 예에서 **권한 부여 서버 데모** 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="0a754-235">나중에 API에 대한 인증으로 사용되도록 OAuth 2.0 서버를 지정하면 이 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="0a754-236">**클라이언트 등록 페이지 URL**로 `http://localhost`와 같은 자리 표시자 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="0a754-237">**클라이언트 등록 페이지 URL** 은 사용자가 계정의 사용자 관리를 지원하는 OAuth 2.0 공급자에 대한 계정을 만들고 구성하는 데 사용할 수 있는 페이지를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="0a754-238">이 예에서 자리 표시자를 사용하도록 사용자는 자신의 계정을 만들거나 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-1]

<span data-ttu-id="0a754-240">그런 다음 **권한 부여 끝점 URL** 및**토큰 끝점 URL**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![권한 부여 서버][api-management-add-authorization-server-1a]

<span data-ttu-id="0a754-242">이 값은 개발자 포털에 대해 만든 AAD 응용 프로그램의 **앱 끝점** 페이지에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="0a754-243">끝점에 액세스하려면 AAD 응용 프로그램에 대한 **구성** 탭으로 이동하고 **끝점 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![응용 프로그램][api-management-aad-devportal-application]

![끝점 보기][api-management-aad-view-endpoints]

<span data-ttu-id="0a754-246">**OAuth 2.0 권한 부여 끝점**을 복사하여 **권한 부여 끝점 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-2]

<span data-ttu-id="0a754-248">**OAuth 2.0 토큰 끝점**을 복사하여 **토큰 끝점 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-2a]

<span data-ttu-id="0a754-250">토큰 끝점에 붙여넣기 외에도 **리소스**라는 추가 본문 매개 변수를 추가하고 값으로 Visual Studio 프로젝트를 게시할 때 만들어진 백 엔드 서비스에 대한 AAD 응용 프로그램에서 **앱 ID URI**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![앱 ID URI][api-management-aad-sso-uri]

<span data-ttu-id="0a754-252">다음으로 클라이언트 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-252">Next, specify the client credentials.</span></span> <span data-ttu-id="0a754-253">액세스할 리소스의 자격 증명이며,이 경우 개발자 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![클라이언트 자격 증명][api-management-client-credentials]

<span data-ttu-id="0a754-255">**클라이언트 ID**를 가져오려면 개발자 포털에 대한 AAD 응용 프로그램의 **구성** 탭으로 이동하여 **클라이언트 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="0a754-256">**클라이언트 암호**를 가져오려면, **키** 섹션의 **기간 선택** 드롭다운을 클릭하고 간격을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="0a754-257">이 예제에서는 1년을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-257">In this example 1 year is used.</span></span>

![클라이언트 ID][api-management-aad-client-id]

<span data-ttu-id="0a754-259">**저장** 을 클릭하여 구성을 저장하고 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0a754-260">이 키를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-260">Make a note of this key.</span></span> <span data-ttu-id="0a754-261">Azure Active Directory 구성 창을 닫으면 키를 다시 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="0a754-262">키를 클립보드에 복사하고, 게시자 포털로 다시 전환하고 키를 **클라이언트 암호** 텍스트 상자에 붙여 넣은 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![권한 부여 서버 추가][api-management-add-authorization-server-3]

<span data-ttu-id="0a754-264">클라이언트 자격 증명 바로 다음이 인증 코드 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="0a754-265">이 권한 부여 코드를 복사하고 Azure AD 개발자 포털 응용 프로그램 구성 페이지로 다시 전환하여 권한 부여를 **회신 URL** 필드에 붙여 넣고 **저장**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![회신 URL][api-management-aad-reply-url]

<span data-ttu-id="0a754-267">개발자 포털 AAD 응용 프로그램에 대한 권한 구성이 다음 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="0a754-268">**응용 프로그램 사용 권한**을 클릭하고 **디렉터리 데이터 읽기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="0a754-269">**저장**을 클릭하여 이 변경 내용을 저장한 다음 **응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![권한 추가][api-management-add-devportal-permissions]

<span data-ttu-id="0a754-271">검색 아이콘을 클릭하고 형식**APIM**을 시작 상자에 입력하고, **APIMAADDemo**를 선택하고 확인 표시를 클릭하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![권한 추가][api-management-aad-add-app-permissions]

<span data-ttu-id="0a754-273">**APIMAADDemo**에 대해 **권한 위임**을 클릭하고 **APIMAADDemo 액세스** 확인란을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="0a754-274">이렇게 하면 개발자 포털 응용 프로그램이 백 엔드 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-274">This allows the developer portal application to access the backend service.</span></span>

![권한 추가][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="0a754-276">계산기 API에 대해 OAuth 2.0 사용자 권한 부여 사용</span><span class="sxs-lookup"><span data-stu-id="0a754-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="0a754-277">이제 OAuth 2.0 서버가 구성되었으므로 API에 대한 보안 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="0a754-278">이 단계는 14분 30초에 시작되는 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="0a754-279">왼쪽 메뉴에서 **API**를 클릭하고 **계산기**를 클릭하여 해당 설정을 보고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![계산기 API][api-management-calc-api]

<span data-ttu-id="0a754-281">**보안** 탭으로 이동하고 **OAuth 2.0** 확인란을 선택한 다음, 원하는 권한 부여 서버를 **권한 부여 서버** 드롭다운에서 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![계산기 API][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="0a754-283">개발자 포털에서 계산기 API를 성공적으로 호출</span><span class="sxs-lookup"><span data-stu-id="0a754-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="0a754-284">이제 OAuth 2.0 권한 부여가 API에서 구성되었으므로, 개발자 센터에서 해당 작업을 성공적으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="0a754-285">이 단계는 15분에 시작되는 비디오에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="0a754-286">개발자 포털에서 계산기 서비스의 **두 개의 정수 추가**로 다시 이동하여 **사용해 보세요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="0a754-287">방금 추가한 권한 부여 서버에 해당하는 **권한 부여** 섹션의 새 항목을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![계산기 API][api-management-calc-authorization-server]

<span data-ttu-id="0a754-289">권한 부여 드롭다운 목록에서 **권한 부여 코드** 를 선택하고 사용할 계정 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="0a754-290">이미 이 계정으로 로그인한 경우 메시지가 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-290">If you are already signed in with the account you may not be prompted.</span></span>

![계산기 API][api-management-devportal-authorization-code]

<span data-ttu-id="0a754-292">**보내기**를 클릭하고 **200 확인**의 **응답 상태** 및 응답 내용에 대한 작업의 결과를 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![계산기 API][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="0a754-294">API를 호출하도록 데스크톱 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="0a754-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="0a754-295">비디오의 다음 절차는 16분 30초부터 시작하며 API를 호출하는 간단한 데스크톱 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="0a754-296">Azure AD에서 데스크톱 응용 프로그램을 등록하고 디렉터리와 백 엔드 서비스에 액세스 권한을 부여하는 것이 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="0a754-297">18분 25초에 계산기 API에 대한 작업을 호출하는 데스크톱 응용 프로그램의 데모가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="0a754-298">미리 요청 권한을 부여하도록 JWT 유효성 검사 정책 구성</span><span class="sxs-lookup"><span data-stu-id="0a754-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="0a754-299">이 비디오에서 최종 절차는 20분 48초에 시작하며 [JWT의 유효성 검사](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) 정책을 사용하여 들어오는 각 요청의 액세스 토큰의 유효성을 검사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="0a754-300">요청의 유효성을 JWT 정책으로 검사하지 않은 경우, 요청은 API 관리로 차단되며 백 엔드를 따라 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="0a754-301">이 정책 구성 및 사용에 대한 다른 데모는 [클라우드 표지 에피소드 177: 추가 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) 을 참고하여 13분 50초로 빨리 감기합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="0a754-302">15분으로 빨리 감기하여 정책 편집기에 구성된 정책을 본 다음 18분 50초로 빨리 감기하여 필수 권한 부여 토큰 포함 및 제외 모두의 경우로 개발자 포털에서 작업 호출의 데모를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a754-303">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a754-303">Next steps</span></span>
* <span data-ttu-id="0a754-304">API 관리에 대한 추가 [비디오](https://azure.microsoft.com/documentation/videos/index/?services=api-management) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a754-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="0a754-305">백 엔드 서비스를 보호하는 다른 방법은 [상호 인증서 인증](api-management-howto-mutual-certificates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a754-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
