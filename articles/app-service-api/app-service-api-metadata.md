---
title: "API 검색 및 코드 생성에 대한 App Service API 앱 메타데이터 | Microsoft Docs"
description: "Azure 앱 서비스에서 API 앱이 Swagger 메타데이터를 사용하여 API 검색 및 코드 생성을 용이하게 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 800bb9df9b957bec2c80abb3edefbaf354b549ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a><span data-ttu-id="66bde-103">API 검색 및 코드 생성에 대한 앱 서비스 API 앱 메타데이터</span><span class="sxs-lookup"><span data-stu-id="66bde-103">App Service API Apps metadata for API discovery and code generation</span></span>
<span data-ttu-id="66bde-104">[Swagger 2.0](http://swagger.io/) API 메타데이터에 대한 지원은 앱 서비스 API 앱에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-104">Support for [Swagger 2.0](http://swagger.io/) API metadata is built into App Service API Apps.</span></span> <span data-ttu-id="66bde-105">Swagger를 사용할 필요는 없지만 사용하면 검색 및 소비를 쉽게 만드는 API 앱 기능의 장점을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-105">You don't have to use Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier.</span></span>   

## <a name="swagger-endpoint"></a><span data-ttu-id="66bde-106">Swagger 끝점</span><span class="sxs-lookup"><span data-stu-id="66bde-106">Swagger endpoint</span></span>
<span data-ttu-id="66bde-107">API 앱의 속성에서 API 앱에 Swagger 2.0 JSON 메타데이터를 제공하는 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-107">You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of the API app.</span></span> <span data-ttu-id="66bde-108">끝점은 API 앱의 기본 URL 또는 절대 URL에 상대적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-108">The endpoint can be relative to the base URL of the API app or an absolute URL.</span></span> <span data-ttu-id="66bde-109">절대 URL은 API 앱 외부를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-109">Absolute URLs can point outside the API app.</span></span> 

<span data-ttu-id="66bde-110">많은 다운스트림 클라이언트(예: Visual Studio 코드 생성 및 PowerApps "API 추가" 흐름)인 URL은 공개적으로 액세스할 수 있어야 합니다.(사용자 또는 서비스 인증으로 보호되지 않음)</span><span class="sxs-lookup"><span data-stu-id="66bde-110">Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), the URL must be publicly accessible (not protected by user or service authentication).</span></span> <span data-ttu-id="66bde-111">즉, 앱 서비스 인증을 사용하고 자체 앱 내에서 API 정의를 노출하려는 경우 익명 트래픽을 허용하는 인증 옵션을 사용하여 API에 도달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-111">This means that if you're using App Service authentication and want to expose the API definition from within your app itself, you need to use authentication option that allows anonymous traffic to reach your API.</span></span> <span data-ttu-id="66bde-112">자세한 내용은 [App Service API 앱에 대한 인증 및 권한 부여](app-service-api-authentication.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66bde-112">For more information, see [Authentication and authorization for App Service API Apps](app-service-api-authentication.md).</span></span>

### <a name="portal-blade"></a><span data-ttu-id="66bde-113">포털 블레이드</span><span class="sxs-lookup"><span data-stu-id="66bde-113">Portal blade</span></span>
<span data-ttu-id="66bde-114">[Azure 포털](https://portal.azure.com/) 에서 끝점 URL은 **API 정의** 블레이드에서 확인하고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-114">In the [Azure portal](https://portal.azure.com/) the endpoint URL can be seen and changed on the **API Definition** blade.</span></span>

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a><span data-ttu-id="66bde-115">Azure 리소스 관리자 속성</span><span class="sxs-lookup"><span data-stu-id="66bde-115">Azure Resource Manager property</span></span>
<span data-ttu-id="66bde-116">또한 [Azure PowerShell](/powershell/azureps-cmdlets-docs)과 [Azure CLI](../cli-install-nodejs.md) 등 명령줄 도구의 [리소스 탐색기](https://resources.azure.com/) 또는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-authoring-templates.md)을 사용하여 API 앱에 대한 API 정의 URL을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-116">You can also configure the API definition URL for an API app by using [Resource Explorer](https://resources.azure.com/) or [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="66bde-117">**리소스 탐색기**에서 **구독 > {your subscription} > resourceGroups > {your resource group} > 공급자 > Microsoft.Web > 사이트 > {your site} > 구성 > 웹**으로 이동하면 `apiDefinition` 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-117">In **Resource Explorer**, go to **subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Web > sites > {your site} > config > web**, and you'll see the `apiDefinition` property:</span></span>

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

<span data-ttu-id="66bde-118">`apiDefinition` 속성을 설정하는 Azure Resource Manager 템플릿의 예를 보려면 [To-Do List 응용 프로그램 예제에 있는 azuredeploy.json 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-118">For an example of an Azure Resource Manager template that sets the `apiDefinition` property, open the [azuredeploy.json file in the To-Do List sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="66bde-119">위에 표시된 JSON 샘플과 같은 템플릿 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-119">Find the section of the template that looks like the JSON sample shown above.</span></span>

### <a name="default-value"></a><span data-ttu-id="66bde-120">기본값</span><span class="sxs-lookup"><span data-stu-id="66bde-120">Default value</span></span>
<span data-ttu-id="66bde-121">Visual Studio를 사용하여 API 앱을 만들 때 API 정의 끝점은 API 앱 및 `/swagger/docs/v1`의 기본 URL로 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-121">When you use Visual Studio to create an API app, the API definition endpoint is automatically set to the base URL of the API app plus `/swagger/docs/v1`.</span></span> <span data-ttu-id="66bde-122">[Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 패키지가 ASP.NET Web API 프로젝트에 대해 동적으로 생성된 Swagger 메타데이터를 사용하기 위해 사용하는 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-122">This is the default URL that the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package uses to serve dynamically generated Swagger metadata for an ASP.NET Web API project.</span></span> 

## <a name="code-generation"></a><span data-ttu-id="66bde-123">코드 생성</span><span class="sxs-lookup"><span data-stu-id="66bde-123">Code generation</span></span>
<span data-ttu-id="66bde-124">Azure API 앱에 Swagger를 통합하는 이점 중 하나는 자동 코드 생성입니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-124">One of the benefits of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="66bde-125">생성된 클라이언트 클래스는 API 앱을 호출하는 코드를 더욱 쉽게 작성하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-125">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="66bde-126">Visual Studio를 사용하거나 명령줄에서 API 앱에 대한 클라이언트 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-126">You can generate client code for an API app by using Visual Studio or from the command line.</span></span> <span data-ttu-id="66bde-127">Visual Studio에서 ASP.NET Web API 프로젝트에 클라이언트 클래스를 생성하는 방법에 대한 정보는 [API 앱 및 ASP.NET 시작](app-service-api-dotnet-get-started.md#codegen)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66bde-127">For information about how to generate client classes in Visual Studio for an ASP.NET Web API project, see [Get started with API Apps and ASP.NET](app-service-api-dotnet-get-started.md#codegen).</span></span> <span data-ttu-id="66bde-128">지원되는 모든 언어에 대한 명령줄에서 수행하는 방법에 대한 내용은 GitHub.com에서 [Azure/autorest](https://github.com/azure/autorest) 리포지토리의 추가 정보 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66bde-128">For information about how to do it from the command line for all supported languages, see the readme file of the [Azure/autorest](https://github.com/azure/autorest) repository on GitHub.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66bde-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66bde-129">Next steps</span></span>
<span data-ttu-id="66bde-130">API 앱을 만들고 배포하며 소비하는 과정을 안내하는 단계별 자습서는 [Azure 앱 서비스에서 API 앱 시작](app-service-api-dotnet-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66bde-130">For a step-by-step tutorial that guides you through creating, deploying, and consuming an API app, see [Get started with API Apps in Azure App Service](app-service-api-dotnet-get-started.md).</span></span>

<span data-ttu-id="66bde-131">API 앱과 함께 Azure API 관리를 사용하는 경우 Swagger 메타데이터를 사용하여 API를 API 관리로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bde-131">If you use Azure API Management with API Apps, you can use Swagger metadata to import your API into API Management.</span></span> <span data-ttu-id="66bde-132">자세한 내용은 [Azure API 관리에서 작업과 함께 API의 정의를 가져오는 방법](../api-management/api-management-howto-import-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66bde-132">For more information, see [How to import the definition of an API with operations in Azure API Management](../api-management/api-management-howto-import-api.md).</span></span> 

