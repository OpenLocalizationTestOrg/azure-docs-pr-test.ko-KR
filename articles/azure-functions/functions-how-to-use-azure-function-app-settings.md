---
title: "Azure Functions 앱 설정 구성 | Microsoft Docs"
description: "Azure 함수 앱 설정을 구성하는 방법에 알아봅니다."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="16dd5-103">Azure Portal에서 함수 앱을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="16dd5-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="16dd5-104">Azure Functions에서 함수 앱은 개별 함수에 대한 실행 컨텍스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="16dd5-105">함수 앱 동작은 지정된 함수 앱에서 호스트하는 모든 함수에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="16dd5-106">이 항목에서는 Azure Portal에서 함수 앱을 구성 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="16dd5-107">시작하려면 [Azure Portal](http://portal.azure.com)로 이동한 후 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="16dd5-108">포털 맨 위에 있는 검색 표시줄에 함수 앱의 이름을 입력하고 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="16dd5-109">함수 앱을 선택하면 다음 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-109">After selecting your function app, you see the following page:</span></span>

![Azure Portal의 함수 앱 개요](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="16dd5-111"><a name="manage-app-service-settings"></a>함수 앱 설정 탭</span><span class="sxs-lookup"><span data-stu-id="16dd5-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Azure Portal의 함수 앱 개요](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="16dd5-113">**설정** 탭에서는 함수 앱에서 사용되는 Functions 런타임 버전을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="16dd5-114">이 탭에서는 또한 함수 앱에서 호스트하는 모든 함수에 대한 HTTP 액세스를 제한하는 데 사용되는 호스트 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="16dd5-115">Functions는 소비 호스팅 및 App Service 호스팅 계획을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="16dd5-116">자세한 내용은 [Azure Functions에 대한 올바른 서비스 계획 선택](functions-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="16dd5-117">소비 계획에서 더 나은 예측 가능성을 얻기 위해 Functions는 일일 사용 할당량(기가바이트 초)을 설정하여 플랫폼 사용을 제한할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="16dd5-118">일일 사용 할당량에 도달하면 함수 앱이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="16dd5-119">사용 할당량에 도달하여 중지한 함수 앱은 일일 사용 할당량을 설정할 때와 같은 컨텍스트에서 다시 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="16dd5-120">대금 청구에 대한 자세한 내용은 [Azure Functions 가격 책정 페이지](http://azure.microsoft.com/pricing/details/functions/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="16dd5-121">플랫폼 기능 탭</span><span class="sxs-lookup"><span data-stu-id="16dd5-121">Platform features tab</span></span>

![함수 응용 프로그램 플랫폼 기능 탭](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="16dd5-123">함수 앱은 Azure App Service 플랫폼에서 실행되고 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="16dd5-124">따라서 함수 앱은 Azure의 핵심 웹 호스팅 플랫폼 기능 대부분에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="16dd5-125">**플랫폼 기능** 탭에서는 함수 앱에서 사용할 수 있는 App Service 플랫폼의 많은 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="16dd5-126">함수 앱이 소비 호스팅 계획에서 실행될 때 모든 App Service 기능을 사용할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="16dd5-127">이 항목의 나머지 부분에서는 Functions에 유용한 Azure Portal의 다음과 같은 App Service 기능을 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="16dd5-128">App Service 편집기</span><span class="sxs-lookup"><span data-stu-id="16dd5-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="16dd5-129">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="16dd5-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="16dd5-130">Console</span><span class="sxs-lookup"><span data-stu-id="16dd5-130">Console</span></span>](#console)
+ [<span data-ttu-id="16dd5-131">고급 도구(Kudu)</span><span class="sxs-lookup"><span data-stu-id="16dd5-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="16dd5-132">배포 옵션</span><span class="sxs-lookup"><span data-stu-id="16dd5-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="16dd5-133">CORS</span><span class="sxs-lookup"><span data-stu-id="16dd5-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="16dd5-134">인증</span><span class="sxs-lookup"><span data-stu-id="16dd5-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="16dd5-135">API 정의</span><span class="sxs-lookup"><span data-stu-id="16dd5-135">API definition</span></span>](#swagger)

<span data-ttu-id="16dd5-136">App Service 설정을 사용하는 방법에 대한 자세한 내용은 [Azure App Service 설정 구성](../app-service-web/web-sites-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="16dd5-137"><a name="editor"></a>App Service 편집기</span><span class="sxs-lookup"><span data-stu-id="16dd5-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![함수 앱 App Service 편집기](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="16dd5-139">App Service 편집기는 JSON 구성 파일과 코드 파일을 둘 다 수정하는 데 사용할 수 있는 포털 내 고급 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="16dd5-140">이 옵션을 선택하면 기본 편집기와 함께 별도의 브라우저 탭이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="16dd5-141">이를 통해 Git 리포지토리와 통합하고 코드를 실행 및 디버깅하며 함수 앱 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="16dd5-142">이 편집기는 기본 함수 앱 블레이드와 비교할 때 함수에 대해 고급 개발 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![App Service 편집기](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="16dd5-144"><a name="settings"></a>응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="16dd5-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![함수 앱 응용 프로그램 설정](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="16dd5-146">App Service **응용 프로그램 설정** 블레이드에서 프레임워크 버전, 원격 디버깅, 앱 설정 및 연결 문자열을 구성 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="16dd5-147">다른 Azure 및 타사 서비스에 함수 앱을 통합할 경우 이 블레이드에서 해당 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![응용 프로그램 설정 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="16dd5-149"><a name="console"></a>콘솔</span><span class="sxs-lookup"><span data-stu-id="16dd5-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Azure Portal의 함수 앱 콘솔](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="16dd5-151">포털 내 콘솔은 명령줄에서 함수 앱과 상호 작용하려는 경우에 이상적인 개발자 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="16dd5-152">일반적인 명령에는 배치 파일 및 스크립트 실행과 함께 디렉터리 및 파일의 생성 및 탐색이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![함수 앱 콘솔](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="16dd5-154"><a name="kudu"></a>고급 도구(Kudu)</span><span class="sxs-lookup"><span data-stu-id="16dd5-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Azure Portal의 함수 앱 Kudu](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="16dd5-156">App Service용 고급 도구(Kudu라고도 함)를 사용하면 함수 앱의 고급 관리 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="16dd5-157">Kudu에서 시스템 정보, 앱 설정, 환경 변수, 사이트 확장, HTTP 헤더 및 서버 변수를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="16dd5-158">`https://<myfunctionapp>.scm.azurewebsites.net/`과 같은 함수 앱에 대한 SCM 끝점으로 이동하여 **Kudu**를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Kudu 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="16dd5-160"><a name="deployment">배포 옵션</span><span class="sxs-lookup"><span data-stu-id="16dd5-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Azure Portal의 함수 앱 배포 옵션](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="16dd5-162">Functions를 사용하면 로컬 컴퓨터에서 함수 코드를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="16dd5-163">그런 다음 Azure에 로컬 함수 앱 프로젝트를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="16dd5-164">기존 FTP 업로드 외에도 Functions를 사용하면 GitHub, VSTS, Dropbox, Bitbucket 등과 같은 인기 있는 연속 통합 솔루션을 사용하여 함수 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="16dd5-165">자세한 내용은 [Azure Functions에 대한 연속 배포](functions-continuous-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="16dd5-166">FTP 또는 로컬 Git을 사용하여 수동으로 업로드하려면 [배포 자격 증명을 구성](functions-continuous-deployment.md#credentials)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="16dd5-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="16dd5-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Azure Portal의 함수 앱 CORS](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="16dd5-169">서비스의 악의적인 코드 실행을 방지하기 위해 App Service는 외부 원본의 함수 앱에 대한 호출을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="16dd5-170">Functions는 CORS(원본 간 리소스 공유)를 지원하여 함수가 원격 요청을 수락할 수 있는 허용 원본을 나타내는 “허용 목록"을 정의할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![함수 앱 CORS 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="16dd5-172"><a name="auth"></a>인증</span><span class="sxs-lookup"><span data-stu-id="16dd5-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Azure Portal의 함수 앱 인증](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="16dd5-174">함수가 HTTP 트리거를 사용하는 경우 먼저 호출이 인증되도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="16dd5-175">App Service는 Facebook, Microsoft 및 Twitter 같은 소셜 공급자를 사용하는 Azure Active Directory 인증 및 로그인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="16dd5-176">특정 인증 공급자를 구성하는 방법에 대한 자세한 내용은 [Azure App Service 인증 개요](../app-service/app-service-authentication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![함수 앱에 대한 인증 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="16dd5-178"><a name="swagger"></a>API 정의</span><span class="sxs-lookup"><span data-stu-id="16dd5-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Azure Portal의 함수 앱 API swagger 정의](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="16dd5-180">Functions는 클라이언트가 HTTP에서 트리거한 함수를 더 쉽게 사용할 수 있도록 하는 Swagger를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="16dd5-181">Swagger를 사용하는 API 정의를 만드는 방법에 대한 자세한 내용은 [Azure에서 API 앱, ASP.NET 및 Swagger 시작](../app-service-api/app-service-api-dotnet-get-started.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="16dd5-182">또한 Functions 프록시를 사용하여 여러 함수에 대해 단일 API 화면을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16dd5-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="16dd5-183">자세한 내용은 [Azure Functions 프록시 사용](functions-proxies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16dd5-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![함수 앱 API 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="16dd5-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16dd5-185">Next steps</span></span>

+ [<span data-ttu-id="16dd5-186">Azure App Service 설정 구성</span><span class="sxs-lookup"><span data-stu-id="16dd5-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="16dd5-187">Azure Functions에 대한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="16dd5-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



