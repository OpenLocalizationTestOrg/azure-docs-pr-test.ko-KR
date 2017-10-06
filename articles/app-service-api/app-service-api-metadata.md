---
title: "aaaApp 서비스 API 앱 메타 데이터 API 검색 및 코드 생성에 대 한 | Microsoft Docs"
description: "Azure 앱 서비스에서 API 앱 Swagger 메타 데이터 API toofacilitate 검색 및 코드 생성을 사용 하는 방법에 대해 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a><span data-ttu-id="188da-103">API 검색 및 코드 생성에 대한 앱 서비스 API 앱 메타데이터</span><span class="sxs-lookup"><span data-stu-id="188da-103">App Service API Apps metadata for API discovery and code generation</span></span>
<span data-ttu-id="188da-104">[Swagger 2.0](http://swagger.io/) API 메타데이터에 대한 지원은 앱 서비스 API 앱에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="188da-104">Support for [Swagger 2.0](http://swagger.io/) API metadata is built into App Service API Apps.</span></span> <span data-ttu-id="188da-105">Swagger, toouse 필요는 없지만 사용 않는 쉽게 검색 하 고 사용할 수 있게 하는 API 앱 기능을 활용 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="188da-105">You don't have toouse Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier.</span></span>   

## <a name="swagger-endpoint"></a><span data-ttu-id="188da-106">Swagger 끝점</span><span class="sxs-lookup"><span data-stu-id="188da-106">Swagger endpoint</span></span>
<span data-ttu-id="188da-107">Hello API 응용 프로그램의 속성에서 API 앱에 대 한 Swagger 2.0 JSON 메타 데이터를 제공 하는 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="188da-107">You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of hello API app.</span></span> <span data-ttu-id="188da-108">절대 URL 또는 hello API 응용 프로그램의 기준 URL을 상대 toohello hello 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="188da-108">hello endpoint can be relative toohello base URL of hello API app or an absolute URL.</span></span> <span data-ttu-id="188da-109">절대 Url hello API 앱 외부 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="188da-109">Absolute URLs can point outside hello API app.</span></span> 

<span data-ttu-id="188da-110">많은 다운스트림 클라이언트 (예: Visual Studio 코드 생성 및 PowerApps "API 추가" 흐름) hello URL 이어야 합니다 공개적으로 액세스할 수 있는 (사용자 또는 서비스 인증으로 보호 되지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="188da-110">Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), hello URL must be publicly accessible (not protected by user or service authentication).</span></span> <span data-ttu-id="188da-111">이 앱 서비스 인증을 사용 하는 자체 응용 프로그램 내에서 tooexpose hello API 정의 사용할 경우 할 toouse 인증 하는 옵션을 익명 트래픽 tooreach API 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-111">This means that if you're using App Service authentication and want tooexpose hello API definition from within your app itself, you need toouse authentication option that allows anonymous traffic tooreach your API.</span></span> <span data-ttu-id="188da-112">자세한 내용은 [App Service API 앱에 대한 인증 및 권한 부여](app-service-api-authentication.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="188da-112">For more information, see [Authentication and authorization for App Service API Apps](app-service-api-authentication.md).</span></span>

### <a name="portal-blade"></a><span data-ttu-id="188da-113">포털 블레이드</span><span class="sxs-lookup"><span data-stu-id="188da-113">Portal blade</span></span>
<span data-ttu-id="188da-114">Hello에 [Azure 포털](https://portal.azure.com/) 끝점 URL을 볼 hello에서 변경 하 고 hello **API 정의** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="188da-114">In hello [Azure portal](https://portal.azure.com/) hello endpoint URL can be seen and changed on hello **API Definition** blade.</span></span>

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a><span data-ttu-id="188da-115">Azure 리소스 관리자 속성</span><span class="sxs-lookup"><span data-stu-id="188da-115">Azure Resource Manager property</span></span>
<span data-ttu-id="188da-116">사용 하 여 API 앱에 대 한 hello API 정의 URL을 구성할 수도 있습니다 [리소스 탐색기](https://resources.azure.com/) 또는 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md) 와 같은 명령줄 도구에서 [Azure PowerShell](/powershell/azureps-cmdlets-docs)및 hello [Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-116">You can also configure hello API definition URL for an API app by using [Resource Explorer](https://resources.azure.com/) or [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="188da-117">**리소스 탐색기**, 너무 이동**구독 > {구독} > resourceGroups > {리소스 그룹} > 공급자 > Microsoft.Web > 사이트 > {사이트} > 구성 > 웹**, hello 보면 `apiDefinition` 속성:</span><span class="sxs-lookup"><span data-stu-id="188da-117">In **Resource Explorer**, go too**subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Web > sites > {your site} > config > web**, and you'll see hello `apiDefinition` property:</span></span>

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

<span data-ttu-id="188da-118">Hello를 설정 하는 Azure 리소스 관리자 템플릿에 대 한 예제 `apiDefinition` 속성을 열고 hello [hello 할 작업 목록 샘플 응용 프로그램에서에서 azuredeploy.json 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-118">For an example of an Azure Resource Manager template that sets hello `apiDefinition` property, open hello [azuredeploy.json file in hello To-Do List sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="188da-119">위에 표시 된 hello JSON 예제 처럼 보이는 hello 템플릿의 hello 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="188da-119">Find hello section of hello template that looks like hello JSON sample shown above.</span></span>

### <a name="default-value"></a><span data-ttu-id="188da-120">기본값</span><span class="sxs-lookup"><span data-stu-id="188da-120">Default value</span></span>
<span data-ttu-id="188da-121">Visual Studio toocreate API 앱을 사용 하 여 hello API 정의 끝점이 자동으로 설정 됩니다 toohello 더하기 hello API 응용 프로그램의 기준 URL `/swagger/docs/v1`합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-121">When you use Visual Studio toocreate an API app, hello API definition endpoint is automatically set toohello base URL of hello API app plus `/swagger/docs/v1`.</span></span> <span data-ttu-id="188da-122">이 hello 기본 URL 해당 hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 패키지는 ASP.NET Web API 프로젝트에 대 한 동적으로 생성 된 tooserve Swagger 메타 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-122">This is hello default URL that hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package uses tooserve dynamically generated Swagger metadata for an ASP.NET Web API project.</span></span> 

## <a name="code-generation"></a><span data-ttu-id="188da-123">코드 생성</span><span class="sxs-lookup"><span data-stu-id="188da-123">Code generation</span></span>
<span data-ttu-id="188da-124">Swagger Azure API 앱에 통합 hello 이점 중 하나는 자동 코드 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="188da-124">One of hello benefits of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="188da-125">생성 된 클라이언트 클래스는 API 앱을 호출 하는 보다 쉽게 toowrite 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="188da-125">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="188da-126">Hello 명령줄에서 또는 Visual Studio를 사용 하 여 API 앱에 대 한 클라이언트 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="188da-126">You can generate client code for an API app by using Visual Studio or from hello command line.</span></span> <span data-ttu-id="188da-127">Toogenerate 클라이언트 Visual Studio에서 ASP.NET 웹 API 프로젝트에 대 한 클래스 하는 방법에 대 한 정보를 참조 하십시오. [API 앱 및 ASP.NET 시작](app-service-api-dotnet-get-started.md#codegen)합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-127">For information about how toogenerate client classes in Visual Studio for an ASP.NET Web API project, see [Get started with API Apps and ASP.NET](app-service-api-dotnet-get-started.md#codegen).</span></span> <span data-ttu-id="188da-128">어떻게 toodo hello 명령에서 줄에 대 한 지원 되는 모든 언어에 대 한 내용은 hello의 hello readme 파일을 참조 하십시오. [Azure/autorest](https://github.com/azure/autorest) GitHub.com에 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-128">For information about how toodo it from hello command line for all supported languages, see hello readme file of hello [Azure/autorest](https://github.com/azure/autorest) repository on GitHub.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="188da-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="188da-129">Next steps</span></span>
<span data-ttu-id="188da-130">API 앱을 만들고 배포하며 소비하는 과정을 안내하는 단계별 자습서는 [Azure 앱 서비스에서 API 앱 시작](app-service-api-dotnet-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="188da-130">For a step-by-step tutorial that guides you through creating, deploying, and consuming an API app, see [Get started with API Apps in Azure App Service](app-service-api-dotnet-get-started.md).</span></span>

<span data-ttu-id="188da-131">API 앱과 Azure API 관리를 사용 하는 경우 사용할 수 있습니다 Swagger 메타 데이터 tooimport API API 관리에.</span><span class="sxs-lookup"><span data-stu-id="188da-131">If you use Azure API Management with API Apps, you can use Swagger metadata tooimport your API into API Management.</span></span> <span data-ttu-id="188da-132">자세한 내용은 참조 [어떻게 tooimport hello Azure API 관리에서 작업을 사용 하는 API의 정의](../api-management/api-management-howto-import-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="188da-132">For more information, see [How tooimport hello definition of an API with operations in Azure API Management](../api-management/api-management-howto-import-api.md).</span></span> 

