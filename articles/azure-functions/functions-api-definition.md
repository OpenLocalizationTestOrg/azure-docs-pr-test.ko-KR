---
title: "Azure 함수에서 메타 데이터 aaaOpenAPI | Microsoft Docs"
description: "Azure Functions에서 OpenAPI 지원 개요"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a><span data-ttu-id="5f43a-103">Azure Functions에서 OpenAPI 2.0 메타데이터 지원(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="5f43a-103">OpenAPI 2.0 metadata support in Azure Functions (preview)</span></span>
<span data-ttu-id="5f43a-104">OpenAPI 2.0 (Swagger 이전의) Azure 함수에서 메타 데이터 지원을 함수 앱 내 toowrite OpenAPI 2.0 정의 사용할 수 있는 미리 보기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-104">OpenAPI 2.0 (formerly Swagger) metadata support in Azure Functions is a preview feature that you can use toowrite an OpenAPI 2.0 definition inside a function app.</span></span> <span data-ttu-id="5f43a-105">그런 다음 hello 함수 앱을 사용 하 여 해당 파일을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-105">You can then host that file by using hello function app.</span></span>

<span data-ttu-id="5f43a-106">[메타 데이터 OpenAPI](http://swagger.io/) 다른 소프트웨어의 다양 한에서 REST API toobe를 호스트 하는 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-106">[OpenAPI metadata](http://swagger.io/) allows a function that's hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="5f43a-107">이 소프트웨어 PowerApps 및 hello와 같은 Microsoft 제품에는 [Azure 앱 서비스의 API 앱 기능](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), 타사 개발자 도구와 같은 [우체부](https://www.getpostman.com/docs/importing_swagger), 및 [많은 추가 패키지](http://swagger.io/tools/).</span><span class="sxs-lookup"><span data-stu-id="5f43a-107">This software includes Microsoft offerings like PowerApps and hello [API Apps feature of Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), third-party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
><span data-ttu-id="5f43a-108">Hello로 시작 하는 것이 좋습니다 [시작 자습서](./functions-api-definition-getting-started.md) 특정 기능에 대 한 자세한 문서 toolearn toothis를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-108">We recommend starting with hello [getting started tutorial](./functions-api-definition-getting-started.md) and then returning toothis document toolearn more about specific features.</span></span>

## <span data-ttu-id="5f43a-109"><a name="enable"></a>OpenAPI 정의 지원 사용</span><span class="sxs-lookup"><span data-stu-id="5f43a-109"><a name="enable"></a>Enable OpenAPI definition support</span></span>
<span data-ttu-id="5f43a-110">Hello에서 모든 OpenAPI 설정을 구성할 수 있습니다 **API 정의** 함수 응용 프로그램의 페이지 **플랫폼 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-110">You can configure all OpenAPI settings on hello **API Definition** page in your function app's **Platform features**.</span></span>

<span data-ttu-id="5f43a-111">호스팅된 OpenAPI 정의와 퀵 스타트 정의의 tooenable hello 생성 설정 **API 정의 소스** 너무**함수 (미리 보기)**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-111">tooenable hello generation of a hosted OpenAPI definition and a quickstart definition, set **API definition source** too**Function (Preview)**.</span></span> <span data-ttu-id="5f43a-112">**외부 URL** 함수 toouse 사용 하면 다른 곳에서 호스트에 OpenAPI 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-112">**External URL** allows your function toouse an OpenAPI definition that's hosted elsewhere.</span></span>

## <span data-ttu-id="5f43a-113"><a name="generate-definition"></a>함수의 메타데이터에서 Swagger 구조 생성</span><span class="sxs-lookup"><span data-stu-id="5f43a-113"><a name="generate-definition"></a>Generate a Swagger skeleton from your function's metadata</span></span>
<span data-ttu-id="5f43a-114">템플릿을 사용하면 첫 번째 OpenAPI 정의 작성을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-114">A template can help you start writing your first OpenAPI definition.</span></span> <span data-ttu-id="5f43a-115">hello 정의 템플릿 기능 각 HTTP 트리거 함수에 대 한 hello function.json 파일에 모든 hello 메타 데이터를 사용 하 여 스파스 OpenAPI 정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-115">hello definition template feature creates a sparse OpenAPI definition by using all hello metadata in hello function.json file for each of your HTTP trigger functions.</span></span> <span data-ttu-id="5f43a-116">Hello에서 API에 대 한 자세한 내용은에서 toofill을 매핑해야 합니다 [OpenAPI 사양](http://swagger.io/specification/), 요청 및 응답 템플릿과 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-116">You'll need toofill in more information about your API from hello [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.</span></span>

<span data-ttu-id="5f43a-117">단계별 지침은 hello [시작 자습서](./functions-api-definition-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-117">For step-by-step instructions, see hello [getting started tutorial](./functions-api-definition-getting-started.md).</span></span>

### <span data-ttu-id="5f43a-118"><a name="templates"></a>사용 가능한 템플릿</span><span class="sxs-lookup"><span data-stu-id="5f43a-118"><a name="templates"></a>Available templates</span></span>

|<span data-ttu-id="5f43a-119">이름</span><span class="sxs-lookup"><span data-stu-id="5f43a-119">Name</span></span>| <span data-ttu-id="5f43a-120">설명</span><span class="sxs-lookup"><span data-stu-id="5f43a-120">Description</span></span> |
|:-----|:-----|
|<span data-ttu-id="5f43a-121">생성된 정의</span><span class="sxs-lookup"><span data-stu-id="5f43a-121">Generated Definition</span></span>|<span data-ttu-id="5f43a-122">Hello 함수 기존 메타 데이터에서 유추할 수 있는 정보의 hello 최대한 사용 하는 OpenAPI 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-122">An OpenAPI definition with hello maximum amount of information that can be inferred from hello function's existing metadata.</span></span>|

### <span data-ttu-id="5f43a-123"><a name="quickstart-details"></a>생성 된 hello 정의에 포함 된 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="5f43a-123"><a name="quickstart-details"></a>Included metadata in hello generated definition</span></span>

<span data-ttu-id="5f43a-124">hello 테이블 나타내는 다음 Azure 포털 설정 및 해당 데이터에 function.json hello를 생성 하는 매핑된 toohello Swagger 구조를 그대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-124">hello following table represents hello Azure portal settings and corresponding data in function.json as it is mapped toohello generated Swagger skeleton.</span></span>

|<span data-ttu-id="5f43a-125">Swagger.json</span><span class="sxs-lookup"><span data-stu-id="5f43a-125">Swagger.json</span></span>|<span data-ttu-id="5f43a-126">포털 UI</span><span class="sxs-lookup"><span data-stu-id="5f43a-126">Portal UI</span></span>|<span data-ttu-id="5f43a-127">Function.json</span><span class="sxs-lookup"><span data-stu-id="5f43a-127">Function.json</span></span>|
|:----|:-----|:-----|
|[<span data-ttu-id="5f43a-128">호스트</span><span class="sxs-lookup"><span data-stu-id="5f43a-128">Host</span></span>](http://swagger.io/specification/#fixed-fields-15)|<span data-ttu-id="5f43a-129">**함수 앱 설정** > **App Service 설정** > **개요** > **URL**</span><span class="sxs-lookup"><span data-stu-id="5f43a-129">**Function app settings** > **App Service settings** > **Overview** > **URL**</span></span>|<span data-ttu-id="5f43a-130">*없음*</span><span class="sxs-lookup"><span data-stu-id="5f43a-130">*Not present*</span></span>
|[<span data-ttu-id="5f43a-131">경로</span><span class="sxs-lookup"><span data-stu-id="5f43a-131">Paths</span></span>](http://swagger.io/specification/#paths-object-29)|<span data-ttu-id="5f43a-132">**통합** > **선택한 HTTP 메서드**</span><span class="sxs-lookup"><span data-stu-id="5f43a-132">**Integrate** > **Selected HTTP methods**</span></span>|<span data-ttu-id="5f43a-133">바인딩: 경로</span><span class="sxs-lookup"><span data-stu-id="5f43a-133">Bindings: Route</span></span>
|[<span data-ttu-id="5f43a-134">경로 항목</span><span class="sxs-lookup"><span data-stu-id="5f43a-134">Path Item</span></span>](http://swagger.io/specification/#path-item-object-32)|<span data-ttu-id="5f43a-135">**통합** > **경로 템플릿**</span><span class="sxs-lookup"><span data-stu-id="5f43a-135">**Integrate** > **Route template**</span></span>|<span data-ttu-id="5f43a-136">바인딩: 메서드</span><span class="sxs-lookup"><span data-stu-id="5f43a-136">Bindings: Methods</span></span>
|[<span data-ttu-id="5f43a-137">보안</span><span class="sxs-lookup"><span data-stu-id="5f43a-137">Security</span></span>](http://swagger.io/specification/#security-scheme-object-112)|<span data-ttu-id="5f43a-138">**키**</span><span class="sxs-lookup"><span data-stu-id="5f43a-138">**Keys**</span></span>|<span data-ttu-id="5f43a-139">*없음*</span><span class="sxs-lookup"><span data-stu-id="5f43a-139">*Not present*</span></span>|
|<span data-ttu-id="5f43a-140">operationID*</span><span class="sxs-lookup"><span data-stu-id="5f43a-140">operationID*</span></span>|<span data-ttu-id="5f43a-141">**경로 + 허용되는 동사**</span><span class="sxs-lookup"><span data-stu-id="5f43a-141">**Route + Allowed verbs**</span></span>|<span data-ttu-id="5f43a-142">경로 + 허용 동사</span><span class="sxs-lookup"><span data-stu-id="5f43a-142">Route + Allowed Verbs</span></span>|

<span data-ttu-id="5f43a-143">\*hello 작업 ID가 PowerApps 및 흐름 통합에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-143">\*hello operation ID is required only for integrating with PowerApps and Flow.</span></span>
> [!NOTE]
> <span data-ttu-id="5f43a-144">hello x-ms-요약 확장 논리 앱, PowerApps, 및 흐름에 표시 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-144">hello x-ms-summary extension provides a display name in Logic Apps, PowerApps, and Flow.</span></span>
>
> <span data-ttu-id="5f43a-145">toolearn 더 참조 [powerapps Swagger 정의 사용자 지정](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-145">toolearn more, see [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span></span>

## <span data-ttu-id="5f43a-146"><a name="CICD"></a>CI/CD tooset API 정의 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5f43a-146"><a name="CICD"></a>Use CI/CD tooset an API definition</span></span>

 <span data-ttu-id="5f43a-147">API 소스 제어 toomodify를 소스 제어에서 API 정의 사용 하기 전에 정의 hello 포털의 호스팅을 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-147">You must enable API definition hosting in hello portal before you enable source control toomodify your API definition from source control.</span></span> <span data-ttu-id="5f43a-148">다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-148">Follow these instructions:</span></span>

1. <span data-ttu-id="5f43a-149">너무 찾아보기**API 정의 (미리 보기)** 함수 응용 프로그램 설정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-149">Browse too**API Definition (preview)** in your function app settings.</span></span>
  1. <span data-ttu-id="5f43a-150">설정 **API 정의 소스** 너무**함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-150">Set **API definition source** too**Function**.</span></span>
  1. <span data-ttu-id="5f43a-151">클릭 **생성 API 정의 템플릿** 차례로 **저장** toocreate 나중에 수정에 대 한 템플릿 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-151">Click **Generate API definition template** and then **Save** toocreate a template definition for modifying later.</span></span>
  1. <span data-ttu-id="5f43a-152">API 정의 URL 및 키를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-152">Note your API definition URL and key.</span></span>
1. <span data-ttu-id="5f43a-153">[CI/CD(연속 통합/연속 배포)를 설정합니다](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span><span class="sxs-lookup"><span data-stu-id="5f43a-153">[Set up continuous integration/continuous deployment (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span></span>
2. <span data-ttu-id="5f43a-154">\site\wwwroot\.azurefunctions\swagger\swagger.json의 원본 제어에서 swagger.json을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-154">Modify swagger.json in source control at \site\wwwroot\.azurefunctions\swagger\swagger.json.</span></span>

<span data-ttu-id="5f43a-155">이제 저장소에서 tooswagger.json hello API 정의 URL에서 함수 응용 프로그램에서 호스팅되는 변경 내용 및에서 적어 둔 키 1.c를 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-155">Now, changes tooswagger.json in your repository are hosted by your function app at hello API definition URL and key that you noted in step 1.c.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f43a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f43a-156">Next steps</span></span>
* <span data-ttu-id="5f43a-157">[시작 자습서](functions-api-definition-getting-started.md) -</span><span class="sxs-lookup"><span data-stu-id="5f43a-157">[Getting started tutorial](functions-api-definition-getting-started.md).</span></span> <span data-ttu-id="5f43a-158">이 연습에서는 toosee 작업에 있는 OpenAPI 정의 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="5f43a-158">Try our walkthrough toosee an OpenAPI definition in action.</span></span>
* <span data-ttu-id="5f43a-159">[Azure Functions GitHub 리포지토리](https://github.com/Azure/Azure-Functions/) -</span><span class="sxs-lookup"><span data-stu-id="5f43a-159">[Azure Functions GitHub repository](https://github.com/Azure/Azure-Functions/).</span></span> <span data-ttu-id="5f43a-160">체크 아웃 hello 함수 리포지토리 toogive us hello API 정의 지원 미리 보기에 대 한 피드백 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-160">Check out hello Functions repository toogive us feedback on hello API definition support preview.</span></span> <span data-ttu-id="5f43a-161">업데이트 toosee 원하는 모든 항목에 대 한 GitHub 문제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-161">Make a GitHub issue for anything you want toosee updated.</span></span>
* <span data-ttu-id="5f43a-162">[Azure Functions 개발자 참조](functions-reference.md) -</span><span class="sxs-lookup"><span data-stu-id="5f43a-162">[Azure Functions developer reference](functions-reference.md).</span></span> <span data-ttu-id="5f43a-163">함수 코딩과 트리거 및 바인딩 정의에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f43a-163">Learn about coding functions and defining triggers and bindings.</span></span>
