---
title: "HTTP를 통해 끝점과 통신 - Azure Logic Apps | Microsoft Docs"
description: "HTTP를 통해 끝점과 통신할 수 있는 Logic Apps 만들기"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="2d958-103">HTTP 동작 시작</span><span class="sxs-lookup"><span data-stu-id="2d958-103">Get started with the HTTP action</span></span>

<span data-ttu-id="2d958-104">HTTP 작업을 사용하여 조직에 대한 워크플로를 확장하고 HTTP를 통해 끝점과 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="2d958-105">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-105">You can:</span></span>

* <span data-ttu-id="2d958-106">관리하는 웹 사이트가 중단되면 활성화되는(트리거) 논리 앱 워크플로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="2d958-107">HTTP를 통해 모든 끝점과 통신하여 다른 서비스로 워크플로를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="2d958-108">논리 앱에서 HTTP 동작 사용을 시작하려면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d958-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="2d958-109">HTTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="2d958-109">Use the HTTP trigger</span></span>
<span data-ttu-id="2d958-110">트리거는 논리 앱에서 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="2d958-111">[트리거에 대해 자세히 알아보세요](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d958-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="2d958-112">논리 앱 디자이너에서 HTTP 트리거를 설정하는 방법의 예제 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="2d958-113">논리 앱에 HTTP 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="2d958-114">폴링할 HTTP 끝점에 대한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="2d958-115">폴링할 빈도에 대해 되풀이 간격을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="2d958-116">이제 각 검사 중에 반환된 모든 콘텐츠에 대해 논리 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP 트리거](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="2d958-118">HTTP 트리거 작동 방식</span><span class="sxs-lookup"><span data-stu-id="2d958-118">How the HTTP trigger works</span></span>

<span data-ttu-id="2d958-119">HTTP 트리거는 되풀이 간격에 따라 HTTP 끝점에 대한 호출을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="2d958-120">기본적으로 300 미만의 모든 HTTP 응답 코드에서 논리 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="2d958-121">논리 앱을 실행할지 여부를 지정하려면 코드 보기에서 논리 앱을 편집하고 HTTP 호출 이후에 평가되는 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="2d958-122">다음은 반환된 상태 코드가 `400`보다 크거나 같을 때마다 발생하는 HTTP 트리거의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="2d958-123">HTTP 트리거 매개 변수에 대한 전체 세부 정보는 [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="2d958-124">HTTP 동작 사용</span><span class="sxs-lookup"><span data-stu-id="2d958-124">Use the HTTP action</span></span>

<span data-ttu-id="2d958-125">동작은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="2d958-126">[작업에 대해 자세히 알아봅니다.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2d958-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="2d958-127">**다음 단계** > **동작 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="2d958-128">동작 검색 상자에 **http**를 입력하여 HTTP 동작을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![HTTP 동작 선택](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="2d958-130">HTTP 호출에 대한 모든 필수 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-130">Add any required parameters for the HTTP call.</span></span>
   
    ![HTTP 동작 완료](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="2d958-132">디자이너 도구 모음에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="2d958-133">논리 앱이 저장되면서 동시에 게시(활성화)됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="2d958-134">HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="2d958-134">HTTP trigger</span></span>
<span data-ttu-id="2d958-135">여기에는 이 커넥터가 지원하는 트리거에 대한 세부 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="2d958-136">HTTP 커넥터에는 1개의 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="2d958-137">트리거</span><span class="sxs-lookup"><span data-stu-id="2d958-137">Trigger</span></span> | <span data-ttu-id="2d958-138">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d958-139">http</span><span class="sxs-lookup"><span data-stu-id="2d958-139">HTTP</span></span> |<span data-ttu-id="2d958-140">HTTP 호출을 수행하고 응답 콘텐츠를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="2d958-141">HTTP 동작</span><span class="sxs-lookup"><span data-stu-id="2d958-141">HTTP action</span></span>
<span data-ttu-id="2d958-142">여기에는 이 커넥터가 지원하는 동작에 대한 세부 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="2d958-143">HTTP 커넥터에는 1개의 가능한 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="2d958-144">작업</span><span class="sxs-lookup"><span data-stu-id="2d958-144">Action</span></span> | <span data-ttu-id="2d958-145">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d958-146">http</span><span class="sxs-lookup"><span data-stu-id="2d958-146">HTTP</span></span> |<span data-ttu-id="2d958-147">HTTP 호출을 수행하고 응답 콘텐츠를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="2d958-148">HTTP 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2d958-148">HTTP details</span></span>
<span data-ttu-id="2d958-149">다음 표에서는 동작의 필수 및 선택적 입력 필드와 함께 동작 사용과 연관된 해당 출력 세부 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="2d958-150">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="2d958-150">HTTP request</span></span>
<span data-ttu-id="2d958-151">HTTP 아웃바운드 요청을 하는 동작에 대한 입력 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="2d958-152">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="2d958-153">표시 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-153">Display name</span></span> | <span data-ttu-id="2d958-154">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-154">Property name</span></span> | <span data-ttu-id="2d958-155">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d958-156">Method*</span><span class="sxs-lookup"><span data-stu-id="2d958-156">Method*</span></span> |<span data-ttu-id="2d958-157">메서드</span><span class="sxs-lookup"><span data-stu-id="2d958-157">method</span></span> |<span data-ttu-id="2d958-158">사용할 HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="2d958-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="2d958-159">URI*</span><span class="sxs-lookup"><span data-stu-id="2d958-159">URI*</span></span> |<span data-ttu-id="2d958-160">uri</span><span class="sxs-lookup"><span data-stu-id="2d958-160">uri</span></span> |<span data-ttu-id="2d958-161">HTTP 요청에 대한 URI</span><span class="sxs-lookup"><span data-stu-id="2d958-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="2d958-162">헤더</span><span class="sxs-lookup"><span data-stu-id="2d958-162">Headers</span></span> |<span data-ttu-id="2d958-163">헤더</span><span class="sxs-lookup"><span data-stu-id="2d958-163">headers</span></span> |<span data-ttu-id="2d958-164">포함할 HTTP 헤더의 JSON 개체</span><span class="sxs-lookup"><span data-stu-id="2d958-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="2d958-165">본문</span><span class="sxs-lookup"><span data-stu-id="2d958-165">Body</span></span> |<span data-ttu-id="2d958-166">본문</span><span class="sxs-lookup"><span data-stu-id="2d958-166">body</span></span> |<span data-ttu-id="2d958-167">HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="2d958-167">The HTTP request body</span></span> |
| <span data-ttu-id="2d958-168">인증</span><span class="sxs-lookup"><span data-stu-id="2d958-168">Authentication</span></span> |<span data-ttu-id="2d958-169">인증</span><span class="sxs-lookup"><span data-stu-id="2d958-169">authentication</span></span> |<span data-ttu-id="2d958-170">[인증](#authentication) 섹션의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2d958-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="2d958-171">출력 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2d958-171">Output details</span></span>
<span data-ttu-id="2d958-172">HTTP 요청에 대한 출력 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="2d958-173">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-173">Property name</span></span> | <span data-ttu-id="2d958-174">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="2d958-174">Data type</span></span> | <span data-ttu-id="2d958-175">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d958-176">headers</span><span class="sxs-lookup"><span data-stu-id="2d958-176">Headers</span></span> |<span data-ttu-id="2d958-177">object</span><span class="sxs-lookup"><span data-stu-id="2d958-177">object</span></span> |<span data-ttu-id="2d958-178">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="2d958-178">Response headers</span></span> |
| <span data-ttu-id="2d958-179">본문</span><span class="sxs-lookup"><span data-stu-id="2d958-179">Body</span></span> |<span data-ttu-id="2d958-180">object</span><span class="sxs-lookup"><span data-stu-id="2d958-180">object</span></span> |<span data-ttu-id="2d958-181">응답 개체</span><span class="sxs-lookup"><span data-stu-id="2d958-181">Response object</span></span> |
| <span data-ttu-id="2d958-182">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d958-182">Status Code</span></span> |<span data-ttu-id="2d958-183">int</span><span class="sxs-lookup"><span data-stu-id="2d958-183">int</span></span> |<span data-ttu-id="2d958-184">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d958-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="2d958-185">인증</span><span class="sxs-lookup"><span data-stu-id="2d958-185">Authentication</span></span>
<span data-ttu-id="2d958-186">Logic Apps 기능을 사용하면 HTTP 끝점에 대해 다른 유형의 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="2d958-187">이 인증은 HTTP, **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)** 및 **[HTTP 웹후크](connectors-native-webhook.md)** 커넥터와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="2d958-188">다음 인증 유형은 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="2d958-189">기본 인증</span><span class="sxs-lookup"><span data-stu-id="2d958-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="2d958-190">클라이언트 인증서 인증</span><span class="sxs-lookup"><span data-stu-id="2d958-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="2d958-191">Azure AD(Azure Active Directory) OAuth 인증</span><span class="sxs-lookup"><span data-stu-id="2d958-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="2d958-192">기본 인증</span><span class="sxs-lookup"><span data-stu-id="2d958-192">Basic authentication</span></span>

<span data-ttu-id="2d958-193">기본 인증 개체는 기본 인증에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="2d958-194">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="2d958-195">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-195">Property name</span></span> | <span data-ttu-id="2d958-196">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="2d958-196">Data type</span></span> | <span data-ttu-id="2d958-197">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d958-198">형식*</span><span class="sxs-lookup"><span data-stu-id="2d958-198">Type*</span></span> |<span data-ttu-id="2d958-199">type</span><span class="sxs-lookup"><span data-stu-id="2d958-199">type</span></span> |<span data-ttu-id="2d958-200">인증 유형(기본 인증의 경우 `Basic` 이어야 함)</span><span class="sxs-lookup"><span data-stu-id="2d958-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="2d958-201">사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="2d958-201">Username*</span></span> |<span data-ttu-id="2d958-202">username</span><span class="sxs-lookup"><span data-stu-id="2d958-202">username</span></span> |<span data-ttu-id="2d958-203">인증할 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-203">User name to authenticate</span></span> |
| <span data-ttu-id="2d958-204">암호*</span><span class="sxs-lookup"><span data-stu-id="2d958-204">Password*</span></span> |<span data-ttu-id="2d958-205">password</span><span class="sxs-lookup"><span data-stu-id="2d958-205">password</span></span> |<span data-ttu-id="2d958-206">인증하기 위한 암호</span><span class="sxs-lookup"><span data-stu-id="2d958-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="2d958-207">정의에서 검색할 수 없는 암호를 사용하려는 경우 `securestring` 매개 변수 및 `@parameters()` 
> [워크플로 정의 함수](http://aka.ms/logicappdocs)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="2d958-208">예:</span><span class="sxs-lookup"><span data-stu-id="2d958-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="2d958-209">클라이언트 인증서 인증</span><span class="sxs-lookup"><span data-stu-id="2d958-209">Client certificate authentication</span></span>

<span data-ttu-id="2d958-210">다음 인증 개체는 클라이언트 인증서 인증에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="2d958-211">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="2d958-212">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-212">Property name</span></span> | <span data-ttu-id="2d958-213">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="2d958-213">Data type</span></span> | <span data-ttu-id="2d958-214">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d958-215">형식*</span><span class="sxs-lookup"><span data-stu-id="2d958-215">Type*</span></span> |<span data-ttu-id="2d958-216">type</span><span class="sxs-lookup"><span data-stu-id="2d958-216">type</span></span> |<span data-ttu-id="2d958-217">인증 유형(SSL 클라이언트 인증서의 경우 `ClientCertificate` 여야 함)</span><span class="sxs-lookup"><span data-stu-id="2d958-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="2d958-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="2d958-218">PFX*</span></span> |<span data-ttu-id="2d958-219">pfx</span><span class="sxs-lookup"><span data-stu-id="2d958-219">pfx</span></span> |<span data-ttu-id="2d958-220">PFX(개인 정보 교환) 파일의 Base64로 인코딩된 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="2d958-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="2d958-221">암호*</span><span class="sxs-lookup"><span data-stu-id="2d958-221">Password*</span></span> |<span data-ttu-id="2d958-222">password</span><span class="sxs-lookup"><span data-stu-id="2d958-222">password</span></span> |<span data-ttu-id="2d958-223">PFX 파일에 액세스하기 위한 암호</span><span class="sxs-lookup"><span data-stu-id="2d958-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="2d958-224">논리 앱을 저장한 후 정의에서 읽을 수 없는 매개 변수를 사용하려면 `securestring` 매개 변수 및 `@parameters()` 
> [워크플로 정의 함수](http://aka.ms/logicappdocs)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="2d958-225">예:</span><span class="sxs-lookup"><span data-stu-id="2d958-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="2d958-226">Azure AD OAuth 인증</span><span class="sxs-lookup"><span data-stu-id="2d958-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="2d958-227">다음 인증 개체는 Azure AD OAuth 인증에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="2d958-228">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="2d958-229">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2d958-229">Property name</span></span> | <span data-ttu-id="2d958-230">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="2d958-230">Data type</span></span> | <span data-ttu-id="2d958-231">설명</span><span class="sxs-lookup"><span data-stu-id="2d958-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d958-232">형식*</span><span class="sxs-lookup"><span data-stu-id="2d958-232">Type*</span></span> |<span data-ttu-id="2d958-233">type</span><span class="sxs-lookup"><span data-stu-id="2d958-233">type</span></span> |<span data-ttu-id="2d958-234">인증 유형(Azure AD OAuth의 경우 `ActiveDirectoryOAuth` 여야 함)</span><span class="sxs-lookup"><span data-stu-id="2d958-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="2d958-235">테넌트*</span><span class="sxs-lookup"><span data-stu-id="2d958-235">Tenant*</span></span> |<span data-ttu-id="2d958-236">tenant</span><span class="sxs-lookup"><span data-stu-id="2d958-236">tenant</span></span> |<span data-ttu-id="2d958-237">Azure AD 테넌트의 테넌트 식별자</span><span class="sxs-lookup"><span data-stu-id="2d958-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="2d958-238">대상*</span><span class="sxs-lookup"><span data-stu-id="2d958-238">Audience*</span></span> |<span data-ttu-id="2d958-239">audience</span><span class="sxs-lookup"><span data-stu-id="2d958-239">audience</span></span> |<span data-ttu-id="2d958-240">사용 권한을 요청하는 리소스.</span><span class="sxs-lookup"><span data-stu-id="2d958-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="2d958-241">예: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="2d958-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="2d958-242">클라이언트 ID*</span><span class="sxs-lookup"><span data-stu-id="2d958-242">Client ID*</span></span> |<span data-ttu-id="2d958-243">clientId</span><span class="sxs-lookup"><span data-stu-id="2d958-243">clientId</span></span> |<span data-ttu-id="2d958-244">Azure AD 응용 프로그램의 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="2d958-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="2d958-245">암호*</span><span class="sxs-lookup"><span data-stu-id="2d958-245">Secret*</span></span> |<span data-ttu-id="2d958-246">secret</span><span class="sxs-lookup"><span data-stu-id="2d958-246">secret</span></span> |<span data-ttu-id="2d958-247">토큰을 요청하는 클라이언트의 암호</span><span class="sxs-lookup"><span data-stu-id="2d958-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="2d958-248">`securestring` 매개 변수 및 `@parameters()` [워크플로 정의 함수](http://aka.ms/logicappdocs)를 사용하면 저장한 후 정의에서 읽을 수 없는 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="2d958-249">예:</span><span class="sxs-lookup"><span data-stu-id="2d958-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="2d958-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d958-250">Next steps</span></span>
<span data-ttu-id="2d958-251">이제 플랫폼을 사용해 보고 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d958-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="2d958-252">[API 목록](apis-list.md)에서 논리 앱의 사용 가능한 다른 커넥터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d958-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

