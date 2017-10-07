---
title: "aaaGetting Azure 함수에서 OpenAPI 메타 데이터와 시작 됨 | Microsoft Docs"
description: "Azure Functions에서 OpenAPI 지원 시작"
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
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="4405e-103">함수 앱에서 OpenAPI 2.0(Swagger) 만들기(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="4405e-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="4405e-104">이 문서는 hello Azure 함수에서 호스트 되는 간단한 API에 대 한 OpenAPI 정의 만드는 방법을 단계별로 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="4405e-105">OpenAPI(Swagger)란?</span><span class="sxs-lookup"><span data-stu-id="4405e-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="4405e-106">[Swagger 메타 데이터](http://swagger.io/) hello 기능을 정의 하는 파일 및 이며, 운영 모드의 API 호스팅하는 다양 한 다른 소프트웨어에서 사용 하는 REST API toobe 함수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="4405e-107">Microsoft 제공 사항 PowerApps 같은 및 [API 앱](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), 3rd 파티 개발자와 같은 도구 뿐만 아니라 [우체부](https://www.getpostman.com/docs/importing_swagger) 및 [많은 추가 패키지](http://swagger.io/tools/) 과 함께 사용 된 프로그램 API toobe 수는 Swagger 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="4405e-108"><a name="prepare-function"></a>간단한 API가 포함된 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="4405e-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="4405e-109">OpenAPI 정의 toocreate 먼저 필요 toocreate 단순 API 사용 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="4405e-110">함수는 앱에서 호스트 되는 API를 이미 있는 경우에 직선 toohello 다음 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="4405e-111">새로운 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="4405e-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="4405e-112">[Azure Portal](https://portal.azure.com) > `+ New` > “함수 앱” 검색</span><span class="sxs-lookup"><span data-stu-id="4405e-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="4405e-113">사용자의 새 함수 앱 내에서 새 HTTP 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="4405e-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="4405e-114">함수는 매우 간단한 REST API를 정의하는 코드로 미리 채워져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="4405e-115">쿼리 매개 변수로 또는 hello 본문에 toohello 함수를 전달 하는 모든 문자열 "Hello {입력}"로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="4405e-116">Toohello 이동 `Integrate` 새 HTTP 트리거 함수의 탭</span><span class="sxs-lookup"><span data-stu-id="4405e-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="4405e-117">설정/해제 `Allowed HTTP methods` 너무`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="4405e-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="4405e-118">`Selected HTTP methods`에서 POST를 제외한 모든 동사를 선택 취소합니다</span><span class="sxs-lookup"><span data-stu-id="4405e-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="4405e-119">![선택된 HTTP 메서드](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="4405e-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="4405e-120">이 단계는 나중에 API 정의를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="4405e-121"><a name="enable"></a>API 정의 지원을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4405e-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="4405e-122">너무 이동`your function name` > `Platform Features` > `API Definition`
![정의 탭](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="4405e-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="4405e-123">설정 `API Definition Source` 너무`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="4405e-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="4405e-124">이 단계에서는 끝점 toohost OpenAPI 파일로 된 인라인 사본 hello 함수 응용 프로그램 도메인에서 등 함수 응용 프로그램에 대 한 OpenAPI 옵션 집합이 [OpenAPI 편집기](http://editor.swagger.io), 및 퀵 스타트 정의 생성기입니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="4405e-125">![사용 가능한 정의](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="4405e-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="4405e-126"><a name="create-definition"></a>템플릿에서 API 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="4405e-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="4405e-127">`Generate API Definition template`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="4405e-128">이 단계는 HTTP 트리거 함수에 대 한 함수 앱을 검색 하 고 functions.json toogenerate OpenAPI 문서에서에서 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="4405e-129">작업 개체를 너무 추가`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="4405e-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="4405e-130">hello 퀵 스타트 OpenAPI 문서는 전체 OpenAPI doc의 개요입니다. 더 많은 메타 데이터 toobe 응답 템플릿 작업 개체와 같은 전체 OpenAPI 정의 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="4405e-131">hello 샘플 작업 개체 아래에 생성/사용 섹션, 매개 변수 개체 및 응답 개체 채워진 스타일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="4405e-132">x-ms-summary는 논리 앱, 흐름, PowerApps에 표시 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="4405e-133">체크 아웃 [powerapps Swagger 정의 사용자 지정](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="4405e-134">클릭 `save` toosave 변경 내용을 ![템플릿 정의 추가](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="4405e-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="4405e-135"><a name="use-definition"></a>API 정의 사용</span><span class="sxs-lookup"><span data-stu-id="4405e-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="4405e-136">복사 프로그램 `API definition URL` 원시 OpenAPI 문서에 새 브라우저 탭 tooview 붙여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="4405e-137">테스트와 해당 URL을 사용 하 여 통합을 위한 도구는 OpenAPI 문서 tooany 번호를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="4405e-138">많은 Azure 리소스가 수 tooautomatically 가져오기 OpenAPI 문서를 사용 하 여 hello 함수 응용 프로그램 설정에 저장 되는 API 정의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="4405e-139">Hello의 일부로 `Function` API 정의 소스 url을 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="4405e-140"><a name="test-definition"></a>API 정의 Swagger UI tootest hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4405e-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="4405e-141">내장 hello API 정의 편집기의 toohello UI 뷰에서 기본 제공 도구 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="4405e-142">API 키를 추가 하 고 다음 hello를 사용 하 여 `Try this operation` 각 방법에 따라 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="4405e-143">hello 도구는 사용자의 API 정의 tooformat hello 요청을 사용 하 고 성공 응답 정의 정확한 지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="4405e-144">단계:</span><span class="sxs-lookup"><span data-stu-id="4405e-144">Steps:</span></span>

1. <span data-ttu-id="4405e-145">함수 API 키 복사</span><span class="sxs-lookup"><span data-stu-id="4405e-145">Copy your function API key</span></span>
    1. <span data-ttu-id="4405e-146">HTTP 트리거 함수에서 hello API 키를 찾을 수 `function name` > `Keys` > `Function Keys` 
   ![기능 키](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="4405e-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="4405e-147">Toohello 이동 `API Definition` 페이지.</span><span class="sxs-lookup"><span data-stu-id="4405e-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="4405e-148">클릭 `Authenticate` hello 위쪽 함수 API 키 toohello 보안 개체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="4405e-149">![OpenAPI 키](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="4405e-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="4405e-150">`/api/yourfunctionroute` > `POST`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="4405e-151">클릭 `Try it out` 이름 tootest 입력</span><span class="sxs-lookup"><span data-stu-id="4405e-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="4405e-152">`Pretty`
![API 정의 테스트](./media/functions-api-definition-getting-started/definitionTest.png)에서 SUCCESS 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4405e-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4405e-153">Next steps</span></span>
* [<span data-ttu-id="4405e-154">Functions 개요의 OpenAPI 정의</span><span class="sxs-lookup"><span data-stu-id="4405e-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="4405e-155">Hello OpenAPI 지원에 대 한 자세한 정보에 대 한 전체 설명서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="4405e-156">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="4405e-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="4405e-157">함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="4405e-158">Azure Functions GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="4405e-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="4405e-159">체크 아웃 hello 함수 GitHub toogive us hello API 정의 지원 미리 보기에 대 한 피드백!</span><span class="sxs-lookup"><span data-stu-id="4405e-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="4405e-160">업데이트 toosee 원하는 모든 항목에 대 한 GitHub 문제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4405e-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
