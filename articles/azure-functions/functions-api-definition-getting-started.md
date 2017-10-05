---
title: "Azure Functions에서 OpenAPI 메타데이터 시작 | Microsoft Docs"
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
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="36d86-103">함수 앱에서 OpenAPI 2.0(Swagger) 만들기(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="36d86-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="36d86-104">이 문서는 Azure Functions에서 호스팅되는 간단한 API에 대해 OpenAPI 정의를 만드는 단계별 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="36d86-105">OpenAPI(Swagger)란?</span><span class="sxs-lookup"><span data-stu-id="36d86-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="36d86-106">[Swagger 메타데이터](http://swagger.io/)는 API의 기능 및 작동 모드를 정의하고 기타 다양한 소프트웨어에서 REST API를 호스팅하는 함수를 사용할 수 있도록 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="36d86-107">PowerApps, [API 앱](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), [Postman](https://www.getpostman.com/docs/importing_swagger) 등의 타사 개발자 도구와 [기타 다양한 패키지](http://swagger.io/tools/)에서 Swagger 정의로 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="36d86-108"><a name="prepare-function"></a>간단한 API가 포함된 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="36d86-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="36d86-109">OpenAPI 정의를 만들기 위해 간단한 API가 포함된 함수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="36d86-110">이미 함수 앱에서 API를 호스팅하고 있는 경우 바로 다음 섹션으로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="36d86-111">새로운 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="36d86-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="36d86-112">[Azure Portal](https://portal.azure.com) > `+ New` > “함수 앱” 검색</span><span class="sxs-lookup"><span data-stu-id="36d86-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="36d86-113">사용자의 새 함수 앱 내에서 새 HTTP 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="36d86-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="36d86-114">함수는 매우 간단한 REST API를 정의하는 코드로 미리 채워져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="36d86-115">함수에 쿼리 매개 변수로 전달되거나 본문에 있는 모든 문자열은 “Hello {input}”로 반환됩니다</span><span class="sxs-lookup"><span data-stu-id="36d86-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="36d86-116">새 HTTP 트리거 함수의 `Integrate` 탭으로 이동</span><span class="sxs-lookup"><span data-stu-id="36d86-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="36d86-117">`Allowed HTTP methods`를 `Selected methods`로 전환</span><span class="sxs-lookup"><span data-stu-id="36d86-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="36d86-118">`Selected HTTP methods`에서 POST를 제외한 모든 동사를 선택 취소합니다</span><span class="sxs-lookup"><span data-stu-id="36d86-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="36d86-119">![선택된 HTTP 메서드](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="36d86-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="36d86-120">이 단계는 나중에 API 정의를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="36d86-121"><a name="enable"></a>API 정의 지원을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="36d86-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="36d86-122">로 이동 `your function name`  >  `Platform Features`  >  `API Definition` 
 ![정의 탭](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="36d86-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="36d86-123">`API Definition Source`를 `Function (preview)`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="36d86-124">이 단계에서는 함수 앱의 도메인에서 OpenAPI 파일을 호스팅하는 끝점, [OpenAPI 편집기](http://editor.swagger.io)의 인라인 복사, 빠른 시작 정의 생성기를 포함하여 함수 앱의 OpenAPI 옵션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="36d86-125">![사용 가능한 정의](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="36d86-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="36d86-126"><a name="create-definition"></a>템플릿에서 API 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="36d86-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="36d86-127">`Generate API Definition template`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="36d86-128">이 단계에서는 함수 앱에서 HTTP 트리거 함수가 있는지 검색하고 functions.json에서 해당 정보를 사용하여 OpenAPI 문서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="36d86-129">`paths: /api/yourfunctionroute post:`에 작업 개체 추가</span><span class="sxs-lookup"><span data-stu-id="36d86-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="36d86-130">빠른 시작 OpenAPI 문서는 전체 OpenAPI 문서의 요약본입니다. 여기서 작업 개체, 응답 템플릿 등 더 많은 메타데이터가 전체 OpenApI 정의여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="36d86-131">아래의 샘플 작업은 생산/소비 섹션, 매개 변수 개체, 응답 개체가 채워져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="36d86-132">x-ms-summary는 논리 앱, 흐름, PowerApps에 표시 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="36d86-133">자세히 알아보려면 [PowerApps에 대한 Swagger 정의 사용자 지정](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="36d86-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="36d86-134">변경 사항을 저장하려면 `save`를 클릭합니다 ![템플릿 정의 추가](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="36d86-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="36d86-135"><a name="use-definition"></a>API 정의 사용</span><span class="sxs-lookup"><span data-stu-id="36d86-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="36d86-136">원시 OpenAPI 문서를 보려면 `API definition URL`을 복사한 다음 새 브라우저 탭에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="36d86-137">OpenAPI 문서를 도구로 가져와 해당 URL을 사용하는 테스트 및 통합에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="36d86-138">대부분의 Azure 리소스는 함수 응용 프로그램 설정에 저장된 API 정의 URL을 사용하여 OpenAPI 문서를 자동으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="36d86-139">해당 URL은 `Function` API 정의 원본의 일부로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="36d86-140"><a name="test-definition"></a>Swagger UI를 사용하여 API 정의 테스트</span><span class="sxs-lookup"><span data-stu-id="36d86-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="36d86-141">임베디드 API 정의 편집기의 UI 보기에 테스트 도구가 포함되어 있스니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="36d86-142">각자의 API 키를 추가한 다음 각 메서드 아래에 있는 `Try this operation` 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="36d86-143">이 도구는 API 정의를 사용하여 요청 형식을 지정합니다. 성공적 응답은 정의가 올바르다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="36d86-144">단계:</span><span class="sxs-lookup"><span data-stu-id="36d86-144">Steps:</span></span>

1. <span data-ttu-id="36d86-145">함수 API 키 복사</span><span class="sxs-lookup"><span data-stu-id="36d86-145">Copy your function API key</span></span>
    1. <span data-ttu-id="36d86-146">HTTP 트리거 함수에서 API 키를 찾을 수 `function name` > `Keys` > `Function Keys` 
   ![기능 키](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="36d86-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="36d86-147">`API Definition` 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="36d86-148">`Authenticate`를 클릭하고 맨 위 보안 개체에 함수 API 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="36d86-149">![OpenAPI 키](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="36d86-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="36d86-150">`/api/yourfunctionroute` > `POST`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="36d86-151">`Try it out`을 클릭한 다음 테스트할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="36d86-152">`Pretty`
![API 정의 테스트](./media/functions-api-definition-getting-started/definitionTest.png)에서 SUCCESS 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="36d86-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36d86-153">Next steps</span></span>
* [<span data-ttu-id="36d86-154">Functions 개요의 OpenAPI 정의</span><span class="sxs-lookup"><span data-stu-id="36d86-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="36d86-155">OpenAPI 지원에 대한 자세한 내용은 전체 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36d86-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="36d86-156">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="36d86-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="36d86-157">함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="36d86-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="36d86-158">Azure Functions GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="36d86-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="36d86-159">API 정의 지원 미리 보기에 대한 의견을 보내려면 Functions GitHub를 확인하세요!</span><span class="sxs-lookup"><span data-stu-id="36d86-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="36d86-160">업데이트 정보를 확인하려는 항목에 대해 GitHub 문제를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="36d86-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
