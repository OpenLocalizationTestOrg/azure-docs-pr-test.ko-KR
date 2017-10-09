---
title: "aaaCall, 트리거 또는 중첩 된 HTTP 끝점-Azure 논리 앱 워크플로 | Microsoft Docs"
description: "Azure 논리 앱에 대 한 HTTP 끝점 toocall, 트리거 또는 중첩 워크플로를 설정 합니다."
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
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="f1ba7-104">Logic Apps의 HTTP 끝점을 통해 워크플로 호출, 트리거 또는 중첩</span><span class="sxs-lookup"><span data-stu-id="f1ba7-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="f1ba7-105">URL을 통해 Logic Apps를 트리거 또는 호출할 수 있도록 동기식 HTTP 끝점을 기본적으로 논리 앱에 트리거로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="f1ba7-106">또한 호출 가능 끝점의 패턴을 사용하여 Logic Apps에서 워크플로를 중첩할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="f1ba7-107">toocreate HTTP 끝점 논리 앱 들어오는 요청을 받을 수 있도록 이러한 트리거 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="f1ba7-108">요청</span><span class="sxs-lookup"><span data-stu-id="f1ba7-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="f1ba7-109">API 연결 웹후크</span><span class="sxs-lookup"><span data-stu-id="f1ba7-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="f1ba7-110">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="f1ba7-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="f1ba7-111">Hello를 사용 하는 예제 있지만 **요청** 트리거를 사용할 수 있습니다의 hello HTTP 트리거를 나열 하 고 모든 원칙 동일 하 게 toohello 다른 트리거 형식을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="f1ba7-112">논리 앱을 위해 HTTP 끝점 설정</span><span class="sxs-lookup"><span data-stu-id="f1ba7-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="f1ba7-113">HTTP 끝점을 toocreate 들어오는 요청을 받을 수 있는 트리거를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="f1ba7-114">Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="f1ba7-115">Tooyour 논리 앱을 이동 하 고 논리 응용 프로그램 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="f1ba7-116">논리 앱이 들어오는 요청을 받을 수 있도록 하는 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="f1ba7-117">예를 들어 hello 추가 **요청** 트리거 tooyour 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="f1ba7-118">아래 **요청 본문이 JSON 스키마**, hello 트리거 tooreceive 예상 하는 hello 페이로드 (데이터)에 대 한 JSON 스키마를 선택적으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="f1ba7-119">hello 디자이너 tooconsume, parse 및 워크플로 통해 hello 트리거에서 패스 데이터 논리 앱 사용할 수는 토큰을 생성 하는 것에 대 한이 스키마를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="f1ba7-120">[JSON 스키마에서 생성된 토큰](#generated-tokens)에 관한 추가 정보.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="f1ba7-121">예를 들어 hello 디자이너에 표시 하는 hello 스키마를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-121">For this example, enter hello schema shown in hello designer:</span></span>

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

    ![Hello 요청 동작 추가][1]

    > [!TIP]
    > 
    > <span data-ttu-id="f1ba7-123">와 같은 도구에서 샘플 JSON 페이로드에 대 한 스키마를 생성할 수 있습니다 [jsonschema.net](http://jsonschema.net/), 또는 hello **요청** 선택 하 여 트리거 **사용 샘플 페이로드 toogenerate 스키마**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="f1ba7-124">샘플 페이로드를 입력하고 **완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="f1ba7-125">예를 들어 다음 샘플 페이로드는:</span><span class="sxs-lookup"><span data-stu-id="f1ba7-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="f1ba7-126">다음 스키마를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="f1ba7-127">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-127">Save your logic app.</span></span> <span data-ttu-id="f1ba7-128">**HTTP POST toothis URL**, 생성 된 콜백 URL이 예제에서와 같이 이제 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![끝점에 대해 생성된 콜백 URL](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="f1ba7-130">이 URL 인증에 사용 되는 hello 쿼리 매개 변수에서 공유 액세스 서명 (SAS) 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="f1ba7-131">또한 hello Azure 포털에서에서 논리 앱 개요에서 hello HTTP 끝점 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="f1ba7-132">**트리거 기록** 아래에서 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-132">Under **Trigger History**, select your trigger:</span></span>

    ![Azure Portal에서 HTTP 끝점 URL 가져오기][2]

    <span data-ttu-id="f1ba7-134">또는이 호출 하 여 hello URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="f1ba7-135">트리거에 대 한 hello HTTP 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="f1ba7-136">기본적으로 hello **요청** 트리거 HTTP POST 요청을 하는데 다른 HTTP 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="f1ba7-137">메서드 유형을 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="f1ba7-138">**요청** 트리거에서 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="f1ba7-139">열기 hello **메서드** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-139">Open hello **Method** list.</span></span> <span data-ttu-id="f1ba7-140">이 예의 경우 **GET**을 선택하면 HTTP 끝점의 URL을 나중에 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f1ba7-141">다른 HTTP 메서드를 선택하거나 사용자의 고유한 논리 앱에 대한 사용자 지정 메서드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![HTTP 메서드 변경](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="f1ba7-143">HTTP 끝점 URL을 통해 매개 변수 허용</span><span class="sxs-lookup"><span data-stu-id="f1ba7-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="f1ba7-144">HTTP 끝점 URL tooaccept 매개 변수를 사용 하도록 하려는 경우 사용자 트리거의 상대 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="f1ba7-145">**요청** 트리거에서 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="f1ba7-146">아래 **메서드**, 요청 toouse hello HTTP 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="f1ba7-147">이 예에서는 선택 hello **가져오기** 메서드를 아직 없는 경우, HTTP 끝점의 URL을 테스트할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f1ba7-148">트리거에 대한 상대 경로를 지정하는 경우 트리거에 대한 HTTP 메서드도 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="f1ba7-149">아래 **상대 경로**, 예를 들어 URL 허용 해야 하는 hello 매개 변수에 대 한 상대 경로 hello 지정 `customers/{customerID}`합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Hello HTTP 메서드 및 매개 변수에 대 한 상대 경로 지정 합니다.](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="f1ba7-151">toouse hello 매개 변수를 추가 **응답** tooyour 논리 앱 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="f1ba7-152">(트리거 아래에서 **새 단계** > **작업 추가** > **응답**을 선택)</span><span class="sxs-lookup"><span data-stu-id="f1ba7-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="f1ba7-153">사용자의 응답에 **본문**, trigger의 상대 경로에 지정 된 hello 매개 변수에 대 한 hello 토큰을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="f1ba7-154">예를 들어 tooreturn `Hello {customerID}`, 업데이트 응답의 **본문** 와 `Hello {customerID token}`합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="f1ba7-155">hello 동적 콘텐츠 목록을 표시 하 고 hello를 표시 해야 `customerID` tooselect 있습니다에 대 한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Tooresponse 본문 매개 변수 추가](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="f1ba7-157">**본문**은 다음 예와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-157">Your **Body** should look like this example:</span></span>

    ![매개 변수 포함 응답 본문](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="f1ba7-159">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-159">Save your logic app.</span></span> 

    <span data-ttu-id="f1ba7-160">HTTP 끝점 URL 포함 hello 상대 경로 지금 예:</span><span class="sxs-lookup"><span data-stu-id="f1ba7-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="f1ba7-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="f1ba7-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="f1ba7-162">다른 브라우저 창에 업데이트 된 URL을 hello 있지만 대체할 HTTP 끝점, 복사 및 붙여넣기 tootest `{customerID}` 와 `123456`, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="f1ba7-163">브라우저에 다음 텍스트가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="f1ba7-164">논리 앱에 대한 JSON 스키마에서 생성된 토큰</span><span class="sxs-lookup"><span data-stu-id="f1ba7-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="f1ba7-165">JSON 스키마를 제공 하 여 **요청** 트리거, hello 논리가 응용 프로그램 디자이너에서 토큰을 생성 속성에 대 한 해당 스키마에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="f1ba7-166">논리 앱 워크플로를 통해 데이터를 전달하는 데 해당 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="f1ba7-167">예를 들어 hello를 추가 하는 경우 `title` 및 `name` 속성 tooyour JSON 스키마 토큰과 이후 워크플로 단계에서 사용 가능한 toouse 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="f1ba7-168">Hello 완전 한 JSON 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="f1ba7-169">Logic Apps에 대한 중첩 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="f1ba7-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="f1ba7-170">요청을 받을 수 있는 다른 논리 앱을 추가하여 Logic Apps에서 워크플로를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="f1ba7-171">tooinclude 이러한 논리 앱 추가 hello **Azure 논리 앱-선택 논리 앱 워크플로** tooyour 트리거 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="f1ba7-172">그런 다음 자격이 있는 Logic Apps 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-172">You can then select from eligible logic apps.</span></span>

![다른 논리 앱 추가](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="f1ba7-174">HTTP 끝점을 통해 Logic Apps 호출 또는 트리거</span><span class="sxs-lookup"><span data-stu-id="f1ba7-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="f1ba7-175">HTTP 끝점을 만든 후를 통해 응용 프로그램 논리를 트리거할 수 있습니다는 `POST` 메서드 toohello 전체 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="f1ba7-176">Logic Apps는 직접 액세스 끝점에 대한 기본 제공 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="f1ba7-177">들어오는 요청의 콘텐츠 참조</span><span class="sxs-lookup"><span data-stu-id="f1ba7-177">Reference content from an incoming request</span></span>

<span data-ttu-id="f1ba7-178">Hello 콘텐츠의 종류를 `application/json`, hello 들어오는 요청에서 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="f1ba7-179">그렇지 않은 경우 콘텐츠는 tooother Api를 전달할 수 있습니다를 하나의 이진으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="f1ba7-180">tooreference hello 워크플로 내에 콘텐츠를 해당 콘텐츠를 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="f1ba7-181">예를 들어, 전달 하는 경우 `application/xml` 콘텐츠를 사용할 수 있습니다 `@xpath()` 에서 XPath 추출에 대 한 또는 `@json()` XML tooJSON 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="f1ba7-182">[콘텐츠 형식 사용](../logic-apps/logic-apps-content-type.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="f1ba7-183">들어오는 요청에서 출력 tooget hello hello를 사용할 수 있습니다 `@triggerOutputs()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="f1ba7-184">이 예제에서는 같은 hello 출력 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="f1ba7-185">tooaccess hello `body` 속성 특히 있습니다 사용할 수 hello `@triggerBody()` 바로 가기 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="f1ba7-186">Toorequests 응답</span><span class="sxs-lookup"><span data-stu-id="f1ba7-186">Respond toorequests</span></span>

<span data-ttu-id="f1ba7-187">Toorespond toocertain 요청 콘텐츠 toohello 호출자에 게 반환 하 여 논리 앱을 시작 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="f1ba7-188">hello tooconstruct hello 상태 코드, 헤더 및 응답 본문을 사용할 수 있습니다 **응답** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="f1ba7-189">이 작업은 워크플로의 hello 끝 뿐 아니라 논리 앱에서 아무 곳 이나 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="f1ba7-190">논리 앱이 포함 되지 않은 경우는 **응답**, hello HTTP 끝점 응답 *즉시* 와 **202 수락 됨** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="f1ba7-191">또한 응답에 대 한 hello 원래 요청 tooget hello, hello 응답에 필요한 모든 단계 완료 해야 hello 내 [요청 시간 제한](./logic-apps-limits-and-config.md) hello 중첩된 논리 앱 워크플로 호출 하지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="f1ba7-192">Hello 들어오는 요청 제한 시간이 초과 되며 hello HTTP 응답을 수신이 시간 동안 응답이 없는 경우 **408 클라이언트 시간 제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="f1ba7-193">중첩 된 논리 앱에 대 한 hello 부모 논리 앱에 대 한 응답 시간을 필요에 관계 없이 완료 될 때까지 toowait를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="f1ba7-194">Hello 응답 생성</span><span class="sxs-lookup"><span data-stu-id="f1ba7-194">Construct hello response</span></span>

<span data-ttu-id="f1ba7-195">Hello 응답 본문에 둘 이상의 헤더 및 모든 종류의 콘텐츠를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="f1ba7-196">우리의 예제 응답 hello 헤더 지정 hello 응답의 콘텐츠 형식은 `application/json`합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="f1ba7-197">hello 본문에 포함 하 고 `title` 및 `name`hello에 대 한 이전에 업데이트 된 hello JSON 스키마에 따라 **요청** 트리거.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![HTTP 응답 작업][3]

<span data-ttu-id="f1ba7-199">응답 속성:</span><span class="sxs-lookup"><span data-stu-id="f1ba7-199">Responses have these properties:</span></span>

| <span data-ttu-id="f1ba7-200">속성</span><span class="sxs-lookup"><span data-stu-id="f1ba7-200">Property</span></span> | <span data-ttu-id="f1ba7-201">설명</span><span class="sxs-lookup"><span data-stu-id="f1ba7-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1ba7-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="f1ba7-202">statusCode</span></span> |<span data-ttu-id="f1ba7-203">응답 toohello 들어오는 요청에 대 한 hello HTTP 상태 코드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="f1ba7-204">이 코드는 2xx, 4xx 또는 5xx로 시작하는 모든 유효한 상태 코드가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="f1ba7-205">하지만 3xx 상태 코드는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="f1ba7-206">headers</span><span class="sxs-lookup"><span data-stu-id="f1ba7-206">headers</span></span> |<span data-ttu-id="f1ba7-207">Hello에 대 한 응답 헤더 tooinclude 개수에 관계 없이 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="f1ba7-208">body</span><span class="sxs-lookup"><span data-stu-id="f1ba7-208">body</span></span> |<span data-ttu-id="f1ba7-209">문자열, JSON 개체 또는 이전 단계에서 참조한 이진 콘텐츠일 수도 있는 본문 개체를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="f1ba7-210">다음은 hello에 대 한 이제 처럼 보이지만 어떤 hello JSON 스키마 **응답** 동작:</span><span class="sxs-lookup"><span data-stu-id="f1ba7-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="f1ba7-211">논리 앱 hello 논리가 응용 프로그램 디자이너에 대 한 tooview hello 전체 JSON 정의 선택 **코드 뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="f1ba7-212">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="f1ba7-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="f1ba7-213">Q: URL 보안이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f1ba7-213">Q: What about URL security?</span></span>

<span data-ttu-id="f1ba7-214">A: Azure는 공유 액세스 서명(SAS)을 사용하여 논리 앱 콜백 URL을 안전하게 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="f1ba7-215">이 서명은 쿼리 매개 변수로 전달되고 논리 앱이 시작하기 전에 유효성이 검사되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="f1ba7-216">Azure 논리 앱, hello 트리거 이름 및 hello 작업을 수행 하는 비밀 키의 고유 조합을 사용 하 여 hello 서명을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="f1ba7-217">따라서은 사용자가 액세스 toohello 비밀 논리 응용 프로그램 키, 하지 않는 한 유효한 서명을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f1ba7-218">프로덕션 환경과 보안 시스템에서는 권장 하지 하기 때문에 hello 브라우저에서 직접 논리 앱을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="f1ba7-219">공유 액세스 키 hello hello URL에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="f1ba7-220">여러 논리 앱 고객 tooshared 도메인 인해 콘텐츠 보안 정책을 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="f1ba7-221">Q: HTTP 끝점을 추가로 구성할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f1ba7-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="f1ba7-222">A: 예, HTTP 끝점은 [**API Management**](../api-management/api-management-key-concepts.md)를 통해 고급 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="f1ba7-223">이 서비스는 또한 hello 기능을 제공 하면 tooconsistently 논리 앱을 포함 하 여 모든 Api 관리에 대 한 하 고, 사용자 지정 도메인 이름을 설정 하 고, 인증 방법의 자세한 등에 사용 예:</span><span class="sxs-lookup"><span data-stu-id="f1ba7-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="f1ba7-224">Hello 요청 방법 변경</span><span class="sxs-lookup"><span data-stu-id="f1ba7-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="f1ba7-225">Hello 요청의 hello URL 세그먼트를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="f1ba7-226">Hello에서 API 관리 도메인 설정 [Azure 포털](https://portal.azure.com/ "Azure 포털")</span><span class="sxs-lookup"><span data-stu-id="f1ba7-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="f1ba7-227">기본 인증에 대 한 정책 toocheck 설정</span><span class="sxs-lookup"><span data-stu-id="f1ba7-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="f1ba7-228">Q: hello 스키마 hello 2014 년 12 월 1 일 미리 보기에서 마이그레이션할 때 변경?</span><span class="sxs-lookup"><span data-stu-id="f1ba7-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="f1ba7-229">A: 다음은 이러한 변경 내용에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="f1ba7-230">2014 년 12 월 1 일 미리 보기</span><span class="sxs-lookup"><span data-stu-id="f1ba7-230">December 1, 2014 preview</span></span> | <span data-ttu-id="f1ba7-231">2016년 6월 1일</span><span class="sxs-lookup"><span data-stu-id="f1ba7-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="f1ba7-232">**HTTP 수신기** API 앱 클릭</span><span class="sxs-lookup"><span data-stu-id="f1ba7-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="f1ba7-233">**수동 트리거** 클릭(API 앱 필요 없음)</span><span class="sxs-lookup"><span data-stu-id="f1ba7-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="f1ba7-234">HTTP 수신기 설정 "*자동으로 응답 보내기*"</span><span class="sxs-lookup"><span data-stu-id="f1ba7-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="f1ba7-235">포함 된 **응답** 동작 또는 hello 워크플로 정의에 없는</span><span class="sxs-lookup"><span data-stu-id="f1ba7-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="f1ba7-236">기본 또는 OAuth 인증 구성</span><span class="sxs-lookup"><span data-stu-id="f1ba7-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="f1ba7-237">API Management를 통해</span><span class="sxs-lookup"><span data-stu-id="f1ba7-237">via API Management</span></span> |
| <span data-ttu-id="f1ba7-238">HTTP 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="f1ba7-238">Configure HTTP method</span></span> |<span data-ttu-id="f1ba7-239">**고급 옵션 표시** 아래에서 HTTP 메서드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="f1ba7-240">상대 경로 구성</span><span class="sxs-lookup"><span data-stu-id="f1ba7-240">Configure relative path</span></span> |<span data-ttu-id="f1ba7-241">**고급 옵션 표시** 아래에서 상대 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="f1ba7-242">통해 참조 hello 들어오는 본문`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="f1ba7-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="f1ba7-243">`@triggerOutputs().body`을 통해 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="f1ba7-244">**HTTP 응답을 보냅니다** hello HTTP 수신기에 대 한 작업</span><span class="sxs-lookup"><span data-stu-id="f1ba7-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="f1ba7-245">클릭 **응답 tooHTTP 요청** (API 앱 필요)</span><span class="sxs-lookup"><span data-stu-id="f1ba7-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="f1ba7-246">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="f1ba7-246">Get help</span></span>

<span data-ttu-id="f1ba7-247">tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="f1ba7-248">Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1ba7-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1ba7-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1ba7-249">Next steps</span></span>

* [<span data-ttu-id="f1ba7-250">작성자 논리 앱 정의</span><span class="sxs-lookup"><span data-stu-id="f1ba7-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="f1ba7-251">오류 및 예외 처리</span><span class="sxs-lookup"><span data-stu-id="f1ba7-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
