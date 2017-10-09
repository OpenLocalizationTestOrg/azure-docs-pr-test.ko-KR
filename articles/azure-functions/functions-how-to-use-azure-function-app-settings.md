---
title: "aaaConfigure Azure 함수 앱 설정 | Microsoft Docs"
description: "Tooconfigure Azure 응용 프로그램 설정을 어떻게 작동 하는지 알아봅니다."
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
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="3cd2c-103">어떻게 toomanage hello Azure 포털에서에서 함수 앱</span><span class="sxs-lookup"><span data-stu-id="3cd2c-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="3cd2c-104">Azure 함수는 함수 앱 개별 함수에 대 한 hello 실행 컨텍스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="3cd2c-105">앱 동작 함수는 지정된 함수 응용 프로그램에서 호스트 tooall 함수를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="3cd2c-106">이 항목에서는 설명 방법을 tooconfigure 함수 hello Azure 포털에서에서 앱을 관리 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="3cd2c-107">toobegin, 이동 toohello [Azure 포털](http://portal.azure.com) tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="3cd2c-108">Hello 포털의 hello 위쪽 hello 검색 표시줄에 함수 응용 프로그램의 hello 이름을 입력 하 고 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="3cd2c-109">함수에서 사용 하는 앱을 선택한 후 다음 페이지 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-109">After selecting your function app, you see hello following page:</span></span>

![Hello Azure 포털에서에서 응용 프로그램 개요 함수](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="3cd2c-111"><a name="manage-app-service-settings"></a>함수 앱 설정 탭</span><span class="sxs-lookup"><span data-stu-id="3cd2c-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![함수 hello Azure 포털에서에서 응용 프로그램 개요입니다.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="3cd2c-113">hello **설정을** 탭은 함수 응용 프로그램에서 사용 하는 hello 함수 런타임 버전을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="3cd2c-114">이기도 hello 호스트 사용 되는 키 toorestrict HTTP 액세스 tooall 함수 hello 함수 앱에서 호스트를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="3cd2c-115">Functions는 소비 호스팅 및 App Service 호스팅 계획을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="3cd2c-116">자세한 내용은 참조 [Azure 함수에 대 한 hello 올바른 서비스 계획 선택](functions-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="3cd2c-117">Hello 소비 계획에서 더 나은 예측 가능성에 대 한 함수 기가바이트 초에서 일별 사용 할당량을 설정 하 여 플랫폼 사용을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="3cd2c-118">Hello 일일 사용량 할당량에 도달 하면 hello 함수 앱이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="3cd2c-119">할당량을 소비 하는 hello 도달의 결과로 중지 함수 앱 hello에서 다시 설정할 수 있습니다 동일한 컨텍스트에서 매일 할당량을 소비 하는 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="3cd2c-120">Hello 참조 [가격 책정 페이지 Azure 함수](http://azure.microsoft.com/pricing/details/functions/) 청구에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="3cd2c-121">플랫폼 기능 탭</span><span class="sxs-lookup"><span data-stu-id="3cd2c-121">Platform features tab</span></span>

![함수 응용 프로그램 플랫폼 기능 탭](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="3cd2c-123">기능 앱을 실행 하 고 hello Azure 앱 서비스 플랫폼으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="3cd2c-124">따라서 기능 앱 Azure의 핵심 웹 호스팅 플랫폼의 hello 기능 액세스 toomost이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="3cd2c-125">hello **플랫폼 기능** 탭에 액세스할 수 있는 권한을 hello hello 함수 앱에서 사용할 수 있는 응용 프로그램 s 서비스 플랫폼의 많은 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="3cd2c-126">Hello 소비 호스팅 계획에 함수 응용 프로그램을 실행 합니다. 앱 서비스 기능을 일부만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="3cd2c-127">이 항목의 hello 나머지 부분에 중점을 두고 같은 hello에 대 한 앱 서비스 기능 hello 함수에 대 한 유용한 Azure 포털:</span><span class="sxs-lookup"><span data-stu-id="3cd2c-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="3cd2c-128">App Service 편집기</span><span class="sxs-lookup"><span data-stu-id="3cd2c-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="3cd2c-129">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="3cd2c-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="3cd2c-130">Console</span><span class="sxs-lookup"><span data-stu-id="3cd2c-130">Console</span></span>](#console)
+ [<span data-ttu-id="3cd2c-131">고급 도구(Kudu)</span><span class="sxs-lookup"><span data-stu-id="3cd2c-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="3cd2c-132">배포 옵션</span><span class="sxs-lookup"><span data-stu-id="3cd2c-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="3cd2c-133">CORS</span><span class="sxs-lookup"><span data-stu-id="3cd2c-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="3cd2c-134">인증</span><span class="sxs-lookup"><span data-stu-id="3cd2c-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="3cd2c-135">API 정의</span><span class="sxs-lookup"><span data-stu-id="3cd2c-135">API definition</span></span>](#swagger)

<span data-ttu-id="3cd2c-136">방법에 대 한 자세한 내용은 응용 프로그램 서비스 설정 사용 하 여 toowork 참조 [Azure 앱 서비스 설정 구성](../app-service-web/web-sites-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="3cd2c-137"><a name="editor"></a>App Service 편집기</span><span class="sxs-lookup"><span data-stu-id="3cd2c-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![함수 앱 App Service 편집기](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="3cd2c-139">앱 서비스 편집기 hello toomodify JSON 구성 파일 및 코드 파일을 동일 하 게 사용할 수 있는 고급 포털에서 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="3cd2c-140">이 옵션을 선택하면 기본 편집기와 함께 별도의 브라우저 탭이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="3cd2c-141">이 hello Git 리포지토리, 실행 및 디버그 코드 toointegrate 수 있고 함수 응용 프로그램 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="3cd2c-142">이 편집기에는 hello 기본 함수 앱 블레이드와 비교 하 여 함수에 대 한 향상 된 개발 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![hello 응용 프로그램 서비스 편집기](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="3cd2c-144"><a name="settings"></a>응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="3cd2c-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![함수 앱 응용 프로그램 설정](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="3cd2c-146">앱 서비스 hello **응용 프로그램 설정** 블레이드는 구성 하 고 프레임 워크 버전, 원격 디버깅, 앱 설정 및 연결 문자열을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="3cd2c-147">다른 Azure 및 타사 서비스에 함수 앱을 통합할 경우 이 블레이드에서 해당 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![응용 프로그램 설정 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="3cd2c-149"><a name="console"></a>콘솔</span><span class="sxs-lookup"><span data-stu-id="3cd2c-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Hello Azure 포털에서에서 응용 프로그램 콘솔 함수](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="3cd2c-151">포털에서 콘솔 hello 함수 앱 toointeract hello 명령줄에서 선호 하는 경우 이상적인 개발자 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="3cd2c-152">일반적인 명령에는 배치 파일 및 스크립트 실행과 함께 디렉터리 및 파일의 생성 및 탐색이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![함수 앱 콘솔](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="3cd2c-154"><a name="kudu"></a>고급 도구(Kudu)</span><span class="sxs-lookup"><span data-stu-id="3cd2c-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Hello Azure 포털에서에서 응용 프로그램 Kudu 함수](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="3cd2c-156">hello 응용 프로그램 서비스 (Kudu이 라고도 함)에 대 한 고급 도구 액세스할 tooadvanced 함수 응용 프로그램의 관리 기능.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="3cd2c-157">Kudu에서 시스템 정보, 앱 설정, 환경 변수, 사이트 확장, HTTP 헤더 및 서버 변수를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="3cd2c-158">시작할 수도 있습니다 **Kudu** 함수 앱에 대 한 SCM 끝점과 toohello 같은 탐색 하 여`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="3cd2c-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Kudu 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="3cd2c-160"><a name="deployment">배포 옵션</span><span class="sxs-lookup"><span data-stu-id="3cd2c-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Hello Azure 포털에서에서 앱 배포 옵션 함수](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="3cd2c-162">Functions를 사용하면 로컬 컴퓨터에서 함수 코드를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="3cd2c-163">그런 다음 사용자 로컬 함수 응용 프로그램 프로젝트 tooAzure 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="3cd2c-164">또한 tootraditional FTP 업로드 함수 배포할 수 있습니다 GitHub, VSTS, Dropbox, Bitbucket 등과 같은 인기 있는 연속 통합 솔루션을 사용 하 여 함수 앱.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="3cd2c-165">자세한 내용은 [Azure Functions에 대한 연속 배포](functions-continuous-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="3cd2c-166">로컬 Git 또는 FTP를 사용 하 여 수동으로 tooupload도 해야 [배포 자격 증명 구성](functions-continuous-deployment.md#credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="3cd2c-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="3cd2c-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Hello Azure 포털에서에서 응용 프로그램 CORS 함수](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="3cd2c-169">서비스에서 tooprevent 악의적인 코드 실행, 앱 서비스 블록 tooyour 기능 앱 외부 원본에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="3cd2c-170">함수는 크로스-원본 자원 공유 (CORS) toolet "의 허용 목록을" origin 함수 원격 요청을 수락할 수 있는 허용 된 정의 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![함수 앱 CORS 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="3cd2c-172"><a name="auth"></a>인증</span><span class="sxs-lookup"><span data-stu-id="3cd2c-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Hello Azure 포털에서에서 응용 프로그램 인증 함수](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="3cd2c-174">함수는 HTTP 트리거를 사용 해야 호출 toofirst 인증 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="3cd2c-175">App Service는 Facebook, Microsoft 및 Twitter 같은 소셜 공급자를 사용하는 Azure Active Directory 인증 및 로그인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="3cd2c-176">특정 인증 공급자를 구성하는 방법에 대한 자세한 내용은 [Azure App Service 인증 개요](../app-service/app-service-authentication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![함수 앱에 대한 인증 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="3cd2c-178"><a name="swagger"></a>API 정의</span><span class="sxs-lookup"><span data-stu-id="3cd2c-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![응용 프로그램 API 함수 swagger 정의 hello Azure 포털에](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="3cd2c-180">함수 지원 Swagger tooallow 클라이언트 toomore HTTP 트리거되는 함수를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="3cd2c-181">Swagger를 사용하는 API 정의를 만드는 방법에 대한 자세한 내용은 [Azure에서 API 앱, ASP.NET 및 Swagger 시작](../app-service-api/app-service-api-dotnet-get-started.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="3cd2c-182">또한 여러 개의 함수에 대 한 함수 프록시 toodefine 단일 API 화면을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="3cd2c-183">자세한 내용은 [Azure Functions 프록시 사용](functions-proxies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cd2c-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![함수 앱 API 구성](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="3cd2c-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cd2c-185">Next steps</span></span>

+ [<span data-ttu-id="3cd2c-186">Azure App Service 설정 구성</span><span class="sxs-lookup"><span data-stu-id="3cd2c-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="3cd2c-187">Azure Functions에 대한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="3cd2c-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



