---
title: "HTTP 끝점을 통해 워크플로 호출, 트리거 또는 중첩 - Azure Logic Apps | Microsoft 문서"
description: "Azure Logic Apps에 대해 워크플로를 호출, 트리거 또는 중첩하기 위해 HTTP 끝점 설정"
services: logic-apps
keywords: "워크플로, HTTP 끝점"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="ec687-104">Logic Apps의 HTTP 끝점을 통해 워크플로 호출, 트리거 또는 중첩</span><span class="sxs-lookup"><span data-stu-id="ec687-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="ec687-105">URL을 통해 Logic Apps를 트리거 또는 호출할 수 있도록 동기식 HTTP 끝점을 기본적으로 논리 앱에 트리거로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="ec687-106">또한 호출 가능 끝점의 패턴을 사용하여 Logic Apps에서 워크플로를 중첩할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="ec687-107">HTTP 끝점을 만들려면 Logic Apps가 들어오는 요청을 받을 수 있도록 이러한 트리거를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="ec687-108">요청</span><span class="sxs-lookup"><span data-stu-id="ec687-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="ec687-109">API 연결 웹후크</span><span class="sxs-lookup"><span data-stu-id="ec687-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="ec687-110">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="ec687-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="ec687-111">이 예제에서는 **요청** 트리거를 사용하지만 나열된 어떤 HTTP 트리거도 사용할 수 있으며, 모든 원칙은 다른 트리거 유형에 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="ec687-112">논리 앱을 위해 HTTP 끝점 설정</span><span class="sxs-lookup"><span data-stu-id="ec687-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="ec687-113">HTTP 끝점을 만들려면 들어오는 요청을 받을 수 있는 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="ec687-114">[Azure Portal](https://portal.azure.com "Azure Portal")에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="ec687-115">논리 앱으로 이동하고 논리 앱 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="ec687-116">논리 앱이 들어오는 요청을 받을 수 있도록 하는 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="ec687-117">예를 들어, 논리 앱에 **요청** 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="ec687-118">필요에 따라 **요청 본문 JSON 스키마**에서 트리거가 받을 것으로 예상하는 페이로드(데이터)에 대해 JSON 스키마를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="ec687-119">설계자는 워크플로를 통해 논리 앱이 트리거에서 데이터를 소비, 구문 분석 및 전달하는 데 사용할 수 있는 토큰을 생성하는 데 이 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="ec687-120">[JSON 스키마에서 생성된 토큰](#generated-tokens)에 관한 추가 정보.</span><span class="sxs-lookup"><span data-stu-id="ec687-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="ec687-121">이 예의 경우 디자이너에 표시된 스키마를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![요청 작업 추가][1]

    > [!TIP]
    > 
    > <span data-ttu-id="ec687-123">[jsonschema.net](http://jsonschema.net/) 같은 도구에서, 또는 **샘플 페이로드를 사용하여 스키마 생성**을 선택하여 **요청** 트리거에서 샘플 JSON 페이로드에 대한 스키마를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="ec687-124">샘플 페이로드를 입력하고 **완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="ec687-125">예를 들어 다음 샘플 페이로드는:</span><span class="sxs-lookup"><span data-stu-id="ec687-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="ec687-126">다음 스키마를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="ec687-127">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-127">Save your logic app.</span></span> <span data-ttu-id="ec687-128">**이 URL의 HTTP POST** 아래에서 이제 다음 예와 같은 생성된 콜백 URL을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![끝점에 대해 생성된 콜백 URL](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="ec687-130">이 URL은 인증에 사용하는 쿼리 매개 변수에 공유 액세스 서명(SAS) 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="ec687-131">Azure Portal의 논리 앱 개요에서 HTTP 끝점 URL을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="ec687-132">**트리거 기록** 아래에서 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-132">Under **Trigger History**, select your trigger:</span></span>

    ![Azure Portal에서 HTTP 끝점 URL 가져오기][2]

    <span data-ttu-id="ec687-134">또는 다음을 호출하여 URL을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="ec687-135">트리거를 위한 HTTP 메서드 변경</span><span class="sxs-lookup"><span data-stu-id="ec687-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="ec687-136">기본적으로 **요청** 트리거는 HTTP POST 요청을 예상하지만 다른 HTTP 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec687-137">메서드 유형을 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="ec687-138">**요청** 트리거에서 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="ec687-139">**메서드** 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-139">Open the **Method** list.</span></span> <span data-ttu-id="ec687-140">이 예의 경우 **GET**을 선택하면 HTTP 끝점의 URL을 나중에 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec687-141">다른 HTTP 메서드를 선택하거나 사용자의 고유한 논리 앱에 대한 사용자 지정 메서드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![HTTP 메서드 변경](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="ec687-143">HTTP 끝점 URL을 통해 매개 변수 허용</span><span class="sxs-lookup"><span data-stu-id="ec687-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="ec687-144">HTTP 끝점 URL이 매개 변수를 허용하도록 하려면 트리거의 상대 경로를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="ec687-145">**요청** 트리거에서 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="ec687-146">**메서드** 아래에서 요청에 사용할 HTTP 메서드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="ec687-147">이 예의 경우 아직 선택하지 않은 경우 **GET** 메서드를 선택하여 HTTP 끝점의 URL을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ec687-148">트리거에 대한 상대 경로를 지정하는 경우 트리거에 대한 HTTP 메서드도 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="ec687-149">**상대 경로** 아래에서 URL이 허용해야 하는 매개 변수에 대한 상대 경로를 지정합니다. 예: `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="ec687-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![HTTP 메서드 및 매개 변수에 대한 상대 경로 지정](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="ec687-151">매개 변수를 사용하려면 논리 앱에 **응답** 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="ec687-152">(트리거 아래에서 **새 단계** > **작업 추가** > **응답**을 선택)</span><span class="sxs-lookup"><span data-stu-id="ec687-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="ec687-153">응답의 **본문**에 트리거의 상대 경로에 지정한 매개 변수의 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="ec687-154">예를 들어 `Hello {customerID}`로 돌아가려면 응답의 **본문**을 `Hello {customerID token}`로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="ec687-155">동적 콘텐츠 목록 표시를 표시 된 `customerID` 토큰을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![응답 본문에 매개 변수 추가](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="ec687-157">**본문**은 다음 예와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-157">Your **Body** should look like this example:</span></span>

    ![매개 변수 포함 응답 본문](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="ec687-159">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-159">Save your logic app.</span></span> 

    <span data-ttu-id="ec687-160">HTTP 끝점 URL은 이제 다음 예와 같은 상대 경로를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="ec687-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="ec687-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="ec687-162">HTTP 끝점을 테스트하려면 업데이트된 URL을 복사하여 다른 브라우저 창에 붙여넣되, `{customerID}`을 `123456`로 바꾸고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="ec687-163">브라우저에 다음 텍스트가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="ec687-164">논리 앱에 대한 JSON 스키마에서 생성된 토큰</span><span class="sxs-lookup"><span data-stu-id="ec687-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="ec687-165">**요청** 트리거에 JSON 스키마를 제공하면 논리 앱 디자이너가 이 스키마의 속성에 대한 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="ec687-166">논리 앱 워크플로를 통해 데이터를 전달하는 데 해당 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="ec687-167">이 예의 경우 JSON 스키마에 `title` 및 `name` 속성을 추가하면 해당 토큰은 이제 이후 워크플로 단계에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="ec687-168">다음은 완료된 JSON 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="ec687-169">Logic Apps에 대한 중첩 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="ec687-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="ec687-170">요청을 받을 수 있는 다른 논리 앱을 추가하여 Logic Apps에서 워크플로를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="ec687-171">이러한 논리 앱을 포함하려면 **Azure Logic Apps - 논리 앱 워크플로 선택** 작업을 트리거에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="ec687-172">그런 다음 자격이 있는 Logic Apps 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-172">You can then select from eligible logic apps.</span></span>

![다른 논리 앱 추가](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="ec687-174">HTTP 끝점을 통해 Logic Apps 호출 또는 트리거</span><span class="sxs-lookup"><span data-stu-id="ec687-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="ec687-175">HTTP 끝점을 만든 후 `POST` 메서드를 통해 논리 앱을 전체 URL로 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="ec687-176">Logic Apps는 직접 액세스 끝점에 대한 기본 제공 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="ec687-177">들어오는 요청의 콘텐츠 참조</span><span class="sxs-lookup"><span data-stu-id="ec687-177">Reference content from an incoming request</span></span>

<span data-ttu-id="ec687-178">콘텐츠의 형식이 `application/json`이면 들어오는 요청의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="ec687-179">그렇지 않으면 콘텐츠는 다른 API에 전달할 수 있는 단일 이진 단위로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="ec687-180">워크플로 내에서 이 콘텐츠를 참조하려면 해당 콘텐츠를 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="ec687-181">예를 들어 `application/xml` 콘텐츠를 전달하는 경우 `@xpath()`를 사용하여 XPath 추출을 수행하거나 `@json()`를 사용하여 XML을 JSON으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="ec687-182">[콘텐츠 형식 사용](../logic-apps/logic-apps-content-type.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="ec687-183">들어오는 요청에서 출력을 가져오려면 `@triggerOutputs()` 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="ec687-184">출력은 다음 예제와 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="ec687-185">특히 `@triggerBody()` 속성에 액세스하기 위해 `body` 바로 가기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="ec687-186">요청에 응답</span><span class="sxs-lookup"><span data-stu-id="ec687-186">Respond to requests</span></span>

<span data-ttu-id="ec687-187">콘텐츠를 호출자에게 반환하여 논리 앱을 시작하는 특정 요청에 응답하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="ec687-188">응답에 대한 상태 코드, 헤더 및 본문을 생성하려면 **응답** 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="ec687-189">이 작업은 워크플로의 끝뿐만 아니라 논리 앱의 어디서나 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="ec687-190">논리 앱에 **응답**이 포함되지 않은 경우 HTTP 끝점은 **202 수락됨** 상태로 *즉시* 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="ec687-191">또한 워크플로를 중첩 논리 앱으로 호출하지 않은 한 원래 요청에서 응답을 가져오려면 응답에 필요한 모든 단계를 [요청 시간 제한](./logic-apps-limits-and-config.md) 이내에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="ec687-192">이 시간 제한 내에 도달하는 응답 작업이 없으면 들어오는 요청은 시간 초과되어 **408 클라이언트 시간 제한** HTTP 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="ec687-193">중첩 논리 앱의 경우 부모 논리 앱은 필요한 시간에 관계없이 응답이 완료될 때까지 계속 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="ec687-194">응답 생성</span><span class="sxs-lookup"><span data-stu-id="ec687-194">Construct the response</span></span>

<span data-ttu-id="ec687-195">응답 본문에 둘 이상의 헤더 및 임의 형식의 콘텐츠를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="ec687-196">이 예제 응답의 경우 헤더는 응답의 콘텐츠 형식이 `application/json`인 것으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="ec687-197">그리고 본문은 **요청** 트리거에 대해 이전에 업데이트된 JSON 스키마에 따라 `title` 및 `name`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![HTTP 응답 작업][3]

<span data-ttu-id="ec687-199">응답 속성:</span><span class="sxs-lookup"><span data-stu-id="ec687-199">Responses have these properties:</span></span>

| <span data-ttu-id="ec687-200">속성</span><span class="sxs-lookup"><span data-stu-id="ec687-200">Property</span></span> | <span data-ttu-id="ec687-201">설명</span><span class="sxs-lookup"><span data-stu-id="ec687-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec687-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="ec687-202">statusCode</span></span> |<span data-ttu-id="ec687-203">들어오는 요청에 응답하는 HTTP 상태 코드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="ec687-204">이 코드는 2xx, 4xx 또는 5xx로 시작하는 모든 유효한 상태 코드가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="ec687-205">하지만 3xx 상태 코드는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="ec687-206">headers</span><span class="sxs-lookup"><span data-stu-id="ec687-206">headers</span></span> |<span data-ttu-id="ec687-207">응답에 포함될 헤더의 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="ec687-208">body</span><span class="sxs-lookup"><span data-stu-id="ec687-208">body</span></span> |<span data-ttu-id="ec687-209">문자열, JSON 개체 또는 이전 단계에서 참조한 이진 콘텐츠일 수도 있는 본문 개체를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="ec687-210">**응답** 작업에 대한 JSON 스키마는 이제 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="ec687-211">논리 앱에 대한 전체 JSON 정의를 보려면 논리 앱 디자이너에서 **코드 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="ec687-212">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="ec687-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="ec687-213">Q: URL 보안이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ec687-213">Q: What about URL security?</span></span>

<span data-ttu-id="ec687-214">A: Azure는 공유 액세스 서명(SAS)을 사용하여 논리 앱 콜백 URL을 안전하게 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="ec687-215">이 서명은 쿼리 매개 변수로 전달되고 논리 앱이 시작하기 전에 유효성이 검사되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="ec687-216">Azure는 논리 앱, 트리거 이름 및 수행되는 작업 별로 비밀 키의 고유한 조합을 사용하여 서명을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="ec687-217">따라서 사용자가 비밀 논리 앱 키에 액세스하지 않으면 유효한 서명을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ec687-218">프로덕션 및 보안 시스템의 경우 다음과 같은 이유로 논리 앱을 브라우저에서 직접 호출하는 것을 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="ec687-219">URL에 공유 액세스 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="ec687-220">논리 앱 고객 간에 공유 도메인으로 인해 보안 콘텐츠 정책을 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="ec687-221">Q: HTTP 끝점을 추가로 구성할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ec687-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="ec687-222">A: 예, HTTP 끝점은 [**API Management**](../api-management/api-management-key-concepts.md)를 통해 고급 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="ec687-223">또한 이 서비스는 Logic Apps를 포함한 모든 API를 일관성 있게 관리하고 사용자 지정 도메인 이름을 설정하고 다음과 같은 더 많은 인증 방법을 사용하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="ec687-224">요청 메서드 변경</span><span class="sxs-lookup"><span data-stu-id="ec687-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="ec687-225">요청의 URL 세그먼트 변경</span><span class="sxs-lookup"><span data-stu-id="ec687-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="ec687-226">[Azure Portal](https://portal.azure.com/ "Azure Portal")에서 API Management 도메인 설정</span><span class="sxs-lookup"><span data-stu-id="ec687-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="ec687-227">기본 인증을 확인하는 정책 설정</span><span class="sxs-lookup"><span data-stu-id="ec687-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="ec687-228">Q: 스키마가 2014년 12월 1일 마이그레이션되었을 때 미리 보기가 어떻게 변경되었습니까?</span><span class="sxs-lookup"><span data-stu-id="ec687-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="ec687-229">A: 다음은 이러한 변경 내용에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="ec687-230">2014 년 12 월 1 일 미리 보기</span><span class="sxs-lookup"><span data-stu-id="ec687-230">December 1, 2014 preview</span></span> | <span data-ttu-id="ec687-231">2016년 6월 1일</span><span class="sxs-lookup"><span data-stu-id="ec687-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="ec687-232">**HTTP 수신기** API 앱 클릭</span><span class="sxs-lookup"><span data-stu-id="ec687-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="ec687-233">**수동 트리거** 클릭(API 앱 필요 없음)</span><span class="sxs-lookup"><span data-stu-id="ec687-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="ec687-234">HTTP 수신기 설정 "*자동으로 응답 보내기*"</span><span class="sxs-lookup"><span data-stu-id="ec687-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="ec687-235">**응답** 작업 포함 또는 워크플로 정의에 없음</span><span class="sxs-lookup"><span data-stu-id="ec687-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="ec687-236">기본 또는 OAuth 인증 구성</span><span class="sxs-lookup"><span data-stu-id="ec687-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="ec687-237">API Management를 통해</span><span class="sxs-lookup"><span data-stu-id="ec687-237">via API Management</span></span> |
| <span data-ttu-id="ec687-238">HTTP 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="ec687-238">Configure HTTP method</span></span> |<span data-ttu-id="ec687-239">**고급 옵션 표시** 아래에서 HTTP 메서드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="ec687-240">상대 경로 구성</span><span class="sxs-lookup"><span data-stu-id="ec687-240">Configure relative path</span></span> |<span data-ttu-id="ec687-241">**고급 옵션 표시** 아래에서 상대 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="ec687-242">`@triggerOutputs().body.Content`을 통해 들어오는 본문을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="ec687-243">`@triggerOutputs().body`을 통해 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ec687-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="ec687-244">**HTTP 응답 보내기** 작업</span><span class="sxs-lookup"><span data-stu-id="ec687-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="ec687-245">**HTTP 요청에 응답** 클릭(API 앱 필요 없음)</span><span class="sxs-lookup"><span data-stu-id="ec687-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="ec687-246">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="ec687-246">Get help</span></span>

<span data-ttu-id="ec687-247">질문하고, 질문에 답변하고, 다른 Azure Logic Apps 사용자가 어떤 일을 하는지 알아보려면 [Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ec687-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="ec687-248">Azure Logic Apps 및 커넥터 개선에 도움을 주려면 [Azure Logic Apps 사용자 의견 사이트](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="ec687-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec687-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec687-249">Next steps</span></span>

* [<span data-ttu-id="ec687-250">작성자 논리 앱 정의</span><span class="sxs-lookup"><span data-stu-id="ec687-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="ec687-251">오류 및 예외 처리</span><span class="sxs-lookup"><span data-stu-id="ec687-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
