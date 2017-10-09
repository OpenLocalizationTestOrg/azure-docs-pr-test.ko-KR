---
title: "Azure 논리 앱-HTTP 통해 모든 끝점과 aaaCommunicate | Microsoft Docs"
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
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="8226e-103">HTTP 동작 hello로 시작</span><span class="sxs-lookup"><span data-stu-id="8226e-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="8226e-104">HTTP 동작 hello로 워크플로 확장 하 여 조직에 대 한 수 있으며 tooany 끝점 HTTP를 통해 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="8226e-105">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-105">You can:</span></span>

* <span data-ttu-id="8226e-106">관리하는 웹 사이트가 중단되면 활성화되는(트리거) 논리 앱 워크플로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="8226e-107">통신할 끝점 tooany HTTP tooextend 워크플로 다른 서비스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="8226e-108">tooget hello HTTP 작업을 사용 하 여 논리 앱에서 시작 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="8226e-109">Hello HTTP 트리거를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8226e-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="8226e-110">트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="8226e-111">[트리거에 대해 자세히 알아보세요.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8226e-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="8226e-112">다음은 시퀀스 tooset HTTP hello hello 논리가 응용 프로그램 디자이너에서에서 트리거하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="8226e-113">논리 앱에 hello HTTP 트리거를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="8226e-114">Toopoll hello HTTP 끝점에 대 한 hello 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="8226e-115">폴링 간격에 hello 되풀이 간격을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="8226e-116">각 검사 하는 동안 반환 되는 모든 콘텐츠로 hello 논리 앱 이제 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP 트리거](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="8226e-118">Hello HTTP 트리거 작동 방식</span><span class="sxs-lookup"><span data-stu-id="8226e-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="8226e-119">hello HTTP 트리거 되풀이 간격 호출 tooHTTP 끝점을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="8226e-120">기본적으로 300 보다 낮은 모든 HTTP 응답 코드는 논리 앱 toorun을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="8226e-121">toospecify hello 논리 앱 발생 시켜야 하는지 여부를는 hello 논리 앱 코드 보기에서 편집을 HTTP 호출 hello 후 확인 하는 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="8226e-122">다음은 상태 코드 보다 크면 또는 값이 너무 hello 반환 되 면 발생 하는 HTTP 트리거의 예`400`합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

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

<span data-ttu-id="8226e-123">Hello HTTP 트리거 매개 변수에 대 한 자세한 세부 정보는에서 사용할 수 있는 [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="8226e-124">Hello HTTP 작업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8226e-124">Use hello HTTP action</span></span>

<span data-ttu-id="8226e-125">동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="8226e-126">[작업에 대해 자세히 알아봅니다.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8226e-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="8226e-127">**다음 단계** > **동작 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="8226e-128">Hello 동작 검색 상자에 입력 **http** toolist hello HTTP 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Hello HTTP 작업을 선택](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="8226e-130">Hello HTTP 호출에 대 한 필수 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![전체 hello HTTP 동작](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="8226e-132">Hello 디자이너 도구 모음에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="8226e-133">논리 앱을 저장 하 고 hello에 (활성화) 게시 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="8226e-134">HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="8226e-134">HTTP trigger</span></span>
<span data-ttu-id="8226e-135">이 커넥터가 지 원하는 hello 트리거에 대 한 hello 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="8226e-136">HTTP 커넥터 hello에 하나의 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="8226e-137">트리거</span><span class="sxs-lookup"><span data-stu-id="8226e-137">Trigger</span></span> | <span data-ttu-id="8226e-138">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8226e-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="8226e-139">HTTP</span></span> |<span data-ttu-id="8226e-140">HTTP 호출을 실행 하 고 hello 응답 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="8226e-141">HTTP 동작</span><span class="sxs-lookup"><span data-stu-id="8226e-141">HTTP action</span></span>
<span data-ttu-id="8226e-142">이 커넥터가 지 원하는 hello 동작에 대 한 hello 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="8226e-143">HTTP 커넥터 hello에 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="8226e-144">동작</span><span class="sxs-lookup"><span data-stu-id="8226e-144">Action</span></span> | <span data-ttu-id="8226e-145">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8226e-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="8226e-146">HTTP</span></span> |<span data-ttu-id="8226e-147">HTTP 호출을 실행 하 고 hello 응답 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="8226e-148">HTTP 세부 정보</span><span class="sxs-lookup"><span data-stu-id="8226e-148">HTTP details</span></span>
<span data-ttu-id="8226e-149">hello 다음 표에서 필요한 hello 및 hello 작업과 hello 동작을 사용 하 여 연관 된 hello 해당 하는 출력 정보에 대 한 선택적 입력된 필드.</span><span class="sxs-lookup"><span data-stu-id="8226e-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="8226e-150">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="8226e-150">HTTP request</span></span>
<span data-ttu-id="8226e-151">hello 다음은 아웃 바운드 HTTP 요청을 낮추는 hello 동작에 대 한 입력된 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="8226e-152">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="8226e-153">표시 이름</span><span class="sxs-lookup"><span data-stu-id="8226e-153">Display name</span></span> | <span data-ttu-id="8226e-154">속성 이름</span><span class="sxs-lookup"><span data-stu-id="8226e-154">Property name</span></span> | <span data-ttu-id="8226e-155">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8226e-156">Method*</span><span class="sxs-lookup"><span data-stu-id="8226e-156">Method*</span></span> |<span data-ttu-id="8226e-157">메서드</span><span class="sxs-lookup"><span data-stu-id="8226e-157">method</span></span> |<span data-ttu-id="8226e-158">hello HTTP 동사 toouse</span><span class="sxs-lookup"><span data-stu-id="8226e-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="8226e-159">URI*</span><span class="sxs-lookup"><span data-stu-id="8226e-159">URI*</span></span> |<span data-ttu-id="8226e-160">uri</span><span class="sxs-lookup"><span data-stu-id="8226e-160">uri</span></span> |<span data-ttu-id="8226e-161">hello HTTP 요청에 대 한 hello URI</span><span class="sxs-lookup"><span data-stu-id="8226e-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="8226e-162">헤더</span><span class="sxs-lookup"><span data-stu-id="8226e-162">Headers</span></span> |<span data-ttu-id="8226e-163">headers</span><span class="sxs-lookup"><span data-stu-id="8226e-163">headers</span></span> |<span data-ttu-id="8226e-164">HTTP 헤더 tooinclude의 JSON 개체</span><span class="sxs-lookup"><span data-stu-id="8226e-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="8226e-165">body</span><span class="sxs-lookup"><span data-stu-id="8226e-165">Body</span></span> |<span data-ttu-id="8226e-166">body</span><span class="sxs-lookup"><span data-stu-id="8226e-166">body</span></span> |<span data-ttu-id="8226e-167">hello HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="8226e-167">hello HTTP request body</span></span> |
| <span data-ttu-id="8226e-168">인증</span><span class="sxs-lookup"><span data-stu-id="8226e-168">Authentication</span></span> |<span data-ttu-id="8226e-169">인증</span><span class="sxs-lookup"><span data-stu-id="8226e-169">authentication</span></span> |<span data-ttu-id="8226e-170">Hello에 대 한 세부 정보 [인증](#authentication) 섹션</span><span class="sxs-lookup"><span data-stu-id="8226e-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="8226e-171">출력 세부 정보</span><span class="sxs-lookup"><span data-stu-id="8226e-171">Output details</span></span>
<span data-ttu-id="8226e-172">hello 다음은 hello HTTP 응답에 대 한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="8226e-173">속성 이름</span><span class="sxs-lookup"><span data-stu-id="8226e-173">Property name</span></span> | <span data-ttu-id="8226e-174">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8226e-174">Data type</span></span> | <span data-ttu-id="8226e-175">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8226e-176">headers</span><span class="sxs-lookup"><span data-stu-id="8226e-176">Headers</span></span> |<span data-ttu-id="8226e-177">object</span><span class="sxs-lookup"><span data-stu-id="8226e-177">object</span></span> |<span data-ttu-id="8226e-178">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="8226e-178">Response headers</span></span> |
| <span data-ttu-id="8226e-179">본문</span><span class="sxs-lookup"><span data-stu-id="8226e-179">Body</span></span> |<span data-ttu-id="8226e-180">object</span><span class="sxs-lookup"><span data-stu-id="8226e-180">object</span></span> |<span data-ttu-id="8226e-181">응답 개체</span><span class="sxs-lookup"><span data-stu-id="8226e-181">Response object</span></span> |
| <span data-ttu-id="8226e-182">상태 코드</span><span class="sxs-lookup"><span data-stu-id="8226e-182">Status Code</span></span> |<span data-ttu-id="8226e-183">int</span><span class="sxs-lookup"><span data-stu-id="8226e-183">int</span></span> |<span data-ttu-id="8226e-184">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="8226e-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="8226e-185">인증</span><span class="sxs-lookup"><span data-stu-id="8226e-185">Authentication</span></span>
<span data-ttu-id="8226e-186">hello 논리 앱 기능 toouse 서로 다른 유형의 HTTP 끝점에 대해 인증 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="8226e-187">이 인증을 사용 하 여 hello로 **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, 및  **[HTTP Webhook](connectors-native-webhook.md)**  커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="8226e-188">hello 인증 유형만 구성할 수는:</span><span class="sxs-lookup"><span data-stu-id="8226e-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="8226e-189">기본 인증</span><span class="sxs-lookup"><span data-stu-id="8226e-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="8226e-190">클라이언트 인증서 인증</span><span class="sxs-lookup"><span data-stu-id="8226e-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="8226e-191">Azure AD(Azure Active Directory) OAuth 인증</span><span class="sxs-lookup"><span data-stu-id="8226e-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="8226e-192">기본 인증</span><span class="sxs-lookup"><span data-stu-id="8226e-192">Basic authentication</span></span>

<span data-ttu-id="8226e-193">기본 인증을 위한 인증 개체를 다음 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="8226e-194">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="8226e-195">속성 이름</span><span class="sxs-lookup"><span data-stu-id="8226e-195">Property name</span></span> | <span data-ttu-id="8226e-196">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8226e-196">Data type</span></span> | <span data-ttu-id="8226e-197">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8226e-198">형식*</span><span class="sxs-lookup"><span data-stu-id="8226e-198">Type*</span></span> |<span data-ttu-id="8226e-199">type</span><span class="sxs-lookup"><span data-stu-id="8226e-199">type</span></span> |<span data-ttu-id="8226e-200">인증 유형(기본 인증의 경우 `Basic` 이어야 함)</span><span class="sxs-lookup"><span data-stu-id="8226e-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="8226e-201">사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="8226e-201">Username*</span></span> |<span data-ttu-id="8226e-202">username</span><span class="sxs-lookup"><span data-stu-id="8226e-202">username</span></span> |<span data-ttu-id="8226e-203">사용자 이름 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="8226e-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="8226e-204">암호*</span><span class="sxs-lookup"><span data-stu-id="8226e-204">Password*</span></span> |<span data-ttu-id="8226e-205">암호</span><span class="sxs-lookup"><span data-stu-id="8226e-205">password</span></span> |<span data-ttu-id="8226e-206">암호 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="8226e-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="8226e-207">Toouse hello 정의에서 검색할 수 없는 암호 사용을 `securestring` 매개 변수 및 hello `@parameters()`  
>  [워크플로 정의 함수의](http://aka.ms/logicappdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="8226e-208">예:</span><span class="sxs-lookup"><span data-stu-id="8226e-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="8226e-209">클라이언트 인증서 인증</span><span class="sxs-lookup"><span data-stu-id="8226e-209">Client certificate authentication</span></span>

<span data-ttu-id="8226e-210">hello 다음 인증 개체에 필요한 클라이언트 인증서 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="8226e-211">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="8226e-212">속성 이름</span><span class="sxs-lookup"><span data-stu-id="8226e-212">Property name</span></span> | <span data-ttu-id="8226e-213">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8226e-213">Data type</span></span> | <span data-ttu-id="8226e-214">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8226e-215">형식*</span><span class="sxs-lookup"><span data-stu-id="8226e-215">Type*</span></span> |<span data-ttu-id="8226e-216">type</span><span class="sxs-lookup"><span data-stu-id="8226e-216">type</span></span> |<span data-ttu-id="8226e-217">인증 유형 hello (있어야 `ClientCertificate` SSL 클라이언트 인증서에 대 한)</span><span class="sxs-lookup"><span data-stu-id="8226e-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="8226e-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="8226e-218">PFX*</span></span> |<span data-ttu-id="8226e-219">pfx</span><span class="sxs-lookup"><span data-stu-id="8226e-219">pfx</span></span> |<span data-ttu-id="8226e-220">hello hello 개인 정보 교환 (PFX) 파일의 내용을 Base64 인코딩</span><span class="sxs-lookup"><span data-stu-id="8226e-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="8226e-221">암호*</span><span class="sxs-lookup"><span data-stu-id="8226e-221">Password*</span></span> |<span data-ttu-id="8226e-222">암호</span><span class="sxs-lookup"><span data-stu-id="8226e-222">password</span></span> |<span data-ttu-id="8226e-223">hello 암호 tooaccess hello PFX 파일</span><span class="sxs-lookup"><span data-stu-id="8226e-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="8226e-224">사용할 수는 매개 변수는 hello 정의 hello 논리 앱을 저장 한 후에 읽을 수 없는 되지 않을 toouse는 `securestring` 매개 변수 및 hello `@parameters()`  
>  [워크플로 정의 함수의](http://aka.ms/logicappdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="8226e-225">예:</span><span class="sxs-lookup"><span data-stu-id="8226e-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="8226e-226">Azure AD OAuth 인증</span><span class="sxs-lookup"><span data-stu-id="8226e-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="8226e-227">Azure AD OAuth 인증을 위한 인증 개체를 다음 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="8226e-228">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="8226e-229">속성 이름</span><span class="sxs-lookup"><span data-stu-id="8226e-229">Property name</span></span> | <span data-ttu-id="8226e-230">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8226e-230">Data type</span></span> | <span data-ttu-id="8226e-231">설명</span><span class="sxs-lookup"><span data-stu-id="8226e-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8226e-232">형식*</span><span class="sxs-lookup"><span data-stu-id="8226e-232">Type*</span></span> |<span data-ttu-id="8226e-233">type</span><span class="sxs-lookup"><span data-stu-id="8226e-233">type</span></span> |<span data-ttu-id="8226e-234">인증 유형 hello (있어야 `ActiveDirectoryOAuth` Azure AD OAuth 용)</span><span class="sxs-lookup"><span data-stu-id="8226e-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="8226e-235">테넌트*</span><span class="sxs-lookup"><span data-stu-id="8226e-235">Tenant*</span></span> |<span data-ttu-id="8226e-236">tenant</span><span class="sxs-lookup"><span data-stu-id="8226e-236">tenant</span></span> |<span data-ttu-id="8226e-237">hello Azure AD 테 넌 트에 대 한 hello 테 넌 트 식별자</span><span class="sxs-lookup"><span data-stu-id="8226e-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="8226e-238">대상*</span><span class="sxs-lookup"><span data-stu-id="8226e-238">Audience*</span></span> |<span data-ttu-id="8226e-239">audience</span><span class="sxs-lookup"><span data-stu-id="8226e-239">audience</span></span> |<span data-ttu-id="8226e-240">권한 부여 toouse를 요청 하는 hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="8226e-241">예: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="8226e-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="8226e-242">클라이언트 ID*</span><span class="sxs-lookup"><span data-stu-id="8226e-242">Client ID*</span></span> |<span data-ttu-id="8226e-243">clientId</span><span class="sxs-lookup"><span data-stu-id="8226e-243">clientId</span></span> |<span data-ttu-id="8226e-244">hello hello Azure AD 응용 프로그램에 대 한 클라이언트 식별자</span><span class="sxs-lookup"><span data-stu-id="8226e-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="8226e-245">암호*</span><span class="sxs-lookup"><span data-stu-id="8226e-245">Secret*</span></span> |<span data-ttu-id="8226e-246">secret</span><span class="sxs-lookup"><span data-stu-id="8226e-246">secret</span></span> |<span data-ttu-id="8226e-247">hello 토큰을 요청 하는 hello 클라이언트의 hello 암호</span><span class="sxs-lookup"><span data-stu-id="8226e-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="8226e-248">사용할 수는 `securestring` 매개 변수 및 hello `@parameters()` [워크플로 정의 함수의](http://aka.ms/logicappdocs) toouse 매개 변수를 저장 한 후 hello 정의에서 쉽게 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="8226e-249">예:</span><span class="sxs-lookup"><span data-stu-id="8226e-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="8226e-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8226e-250">Next steps</span></span>
<span data-ttu-id="8226e-251">이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="8226e-252">탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8226e-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

