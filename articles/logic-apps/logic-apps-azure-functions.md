---
title: "Azure 기능을 사용 하 여 Azure 논리 앱에 대 한 코드 aaaCustom | Microsoft Docs"
description: "Azure Functions를 사용하여 Azure Logic Apps에 대한 사용자 지정 코드 만들기 및 실행"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="63891-103">Azure Functions를 통해 Logic Apps에 대한 사용자 지정 코드 추가 및 실행</span><span class="sxs-lookup"><span data-stu-id="63891-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="63891-104">C# 또는 논리 앱에서 node.js의 사용자 지정 코드 조각을 toorun Azure 기능을 통해 사용자 지정 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63891-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="63891-105">[Azure Functions](../azure-functions/functions-overview.md)는 Microsoft Azure에서 서버 없는 계산을 제공하고 다음과 같은 태스크를 수행하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="63891-106">고급 서식 지정 또는 논리 앱에서 필드 계산</span><span class="sxs-lookup"><span data-stu-id="63891-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="63891-107">워크플로에서 계산을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="63891-108">C# 또는 node.js에서 지원 되는 함수로 hello 논리 앱 기능을 확장</span><span class="sxs-lookup"><span data-stu-id="63891-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="63891-109">Logic Apps에 대한 사용자 지정 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="63891-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="63891-110">Hello에서 hello 함수 Azure 포털에는 함수를 만드는 것이 좋습니다 **제네릭 Webhook-노드** 또는 **제네릭 Webhook-C#** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="63891-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="63891-111">hello 결과 자동으로 채워진 서식 파일을 만들고 허용 `application/json` 논리 앱에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="63891-112">이러한 서식 파일에서 만든 함수는 자동으로 검색 및 논리 응용 프로그램 디자이너에서 hello에 표시 **내 영역에서 Azure 함수입니다.**</span><span class="sxs-lookup"><span data-stu-id="63891-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="63891-113">Hello hello에 Azure 포털에서에서 **통합** 창 함수에 대 한 서식 파일에 표시할지를 **모드** 도**Webhook** 및 **Webhook유형** 너무 설정**일반 JSON**합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="63891-114">Webhook 함수 요청을 수락 및 통해 hello 메서드에 전달 된 `data` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="63891-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="63891-115">와 같은 점 표기법을 사용 하 여 페이로드 hello 속성에 액세스할 수 있습니다 `data.function-name`합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="63891-116">예를 들어 날짜 문자열에는 DateTime 값으로 변환 하는 간단한 JavaScript 함수를 다음 예제는 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63891-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="63891-117">논리 앱에서 Azure Functions 호출</span><span class="sxs-lookup"><span data-stu-id="63891-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="63891-118">해당 구독 및 toocall 논리가 응용 프로그램 디자이너에서 선택 hello 함수 toolist hello 컨테이너 클릭 hello **작업** 메뉴에서을 선택에서 **내 영역에서 Azure 함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="63891-119">Hello 함수를 선택 하 고 나면 됩니다 toospecify 입력된 페이로드 개체를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="63891-120">이 개체는 hello 메시지를 논리 앱 보냅니다 toohello 함수 hello를 JSON 개체 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="63891-121">예를 들어 hello에 toopass 원하는 **마지막으로 수정한 날짜** 날짜는 Salesforce 트리거에서 hello 함수 페이로드가이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63891-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![마지막으로 수정한 날짜][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="63891-123">함수에서 논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="63891-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="63891-124">함수 내에서 논리 앱을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63891-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="63891-125">[호출 가능 끝점인 논리 앱](logic-apps-http-endpoint.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63891-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="63891-126">수동 트리거가 있는 논리 앱을 만드는 다음에서 내부 함수를 생성 toohello 논리 앱을 전송 하는 것이 원하는 hello 페이로드를 사용한 HTTP POST toohello 수동 트리거 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="63891-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="63891-127">Logic App Designer에서 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="63891-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="63891-128">Node.js webhook 함수 hello 디자이너에서 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63891-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="63891-129">먼저 **내 영역의 Azure Functions** 를 선택하고 함수에 대한 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="63891-130">Hello에서 toocreate 하나 컨테이너를 아직 없는 경우 해야 [Azure 함수 포털](https://functions.azure.com/signin)합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="63891-131">그런 다음 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-131">Then select **Create New**.</span></span>  

<span data-ttu-id="63891-132">toogenerate toocompute, hello 데이터를 기반으로 템플릿의 함수로 toopass를 계획 하는 hello 컨텍스트 개체를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="63891-133">이 개체는 JSON 개체여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-133">This object must be a JSON object.</span></span> <span data-ttu-id="63891-134">예를 들어 hello 파일 내용에서 FTP 작업에서 전달 하는 경우 hello 컨텍스트 페이로드가이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63891-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![상황에 맞는 페이로드][2]

> [!NOTE]
> <span data-ttu-id="63891-136">이 개체를 문자열로 캐스팅 되지 않은, toohello JSON 페이로드 hello 콘텐츠 직접 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63891-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="63891-137">그러나 hello 개체 JSON 토큰 (즉, 문자열 또는 JSON 개체/배열은) 없는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="63891-138">toocast hello 개체를 문자열로 hello이 문서의 첫 번째 그림에 나와 있는 것 처럼 따옴표를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="63891-139">hello 디자이너에는 다음 인라인을 만들 수는 함수 템플릿을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="63891-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="63891-140">변수 미리 hello 함수로 toopass를 계획 하는 hello 상황에 따라 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63891-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
