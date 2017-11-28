---
title: "Azure Functions에서 SendGrid를 사용하는 방법 | Microsoft Docs"
description: "Azure Functions에서 SendGrid를 사용하는 방법을 보여 줍니다."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="86ea2-103">Azure Functions에서 SendGrid를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="86ea2-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="86ea2-104">SendGrid 개요</span><span class="sxs-lookup"><span data-stu-id="86ea2-104">SendGrid Overview</span></span>

<span data-ttu-id="86ea2-105">Azure Functions는 함수에서 몇 줄의 코드와 SendGrid 계정으로 전자 메일 메시지를 보낼 수 있도록 SendGrid 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="86ea2-106">Azure Function의 SendGrid API를 사용하려면 [SendGrid 계정](http://SendGrid.com)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="86ea2-107">또한 SendGrid API 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="86ea2-108">SendGrid 계정에 로그인하고 **설정**을 클릭한 다음 **API 키**를 클릭하여 API 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="86ea2-109">이후 단계에서 사용되므로 이 키를 사용 가능한 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="86ea2-110">이제 Azure Function 앱을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="86ea2-111">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="86ea2-111">Create an Azure Function app</span></span> 

<span data-ttu-id="86ea2-112">Azure Function Appls는 하나 이상의 Azure Functions에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="86ea2-113">Azure Functions는 함수일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="86ea2-114">각 Azure Function은 함수 실행을 야기하는 이벤트에 해당하는 하나의 트리거에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="86ea2-115">각 함수는 임의 개수의 입력 또는 출력 바인딩을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="86ea2-116">바인딩은 함수에서 사용할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="86ea2-117">SendGrid는 전자 메일을 보내는 데 사용할 수 있는 출력 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="86ea2-118">Azure Portal에 로그인하고 [Azure Function 앱을 만들거나](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) 기존 함수 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="86ea2-119">Azure Function을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-119">Create an Azure function.</span></span> <span data-ttu-id="86ea2-120">간단한 작업을 위해 수동 트리거 및 C#을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Azure Function 만들기](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="86ea2-122">Azure Function 앱에서 사용할 SendGrid 구성</span><span class="sxs-lookup"><span data-stu-id="86ea2-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="86ea2-123">함수에서 사용할 수 있게 SendGrid API 키를 앱 설정으로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="86ea2-124">ApiKey 필드는 실제 SendGrid API 키가 아니지만 정의하는 앱 설정은 실제 API 키를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="86ea2-125">이러한 방식으로 키를 저장하면 소스 코드 제어에 체크인될 수 있는 코드 또는 파일에서 분리되므로 보안에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="86ea2-126">함수 앱의 **응용 프로그램 설정**에서 **AppSettings**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Azure Function 만들기](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="86ea2-128">SendGrid 출력 바인딩 구성</span><span class="sxs-lookup"><span data-stu-id="86ea2-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="86ea2-129">SendGrid는 Azure Function 출력 바인딩으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="86ea2-130">SendGrid 출력 바인딩을 만들려면</span><span class="sxs-lookup"><span data-stu-id="86ea2-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="86ea2-131">Azure Portal에서 함수의 **통합** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="86ea2-132">**새 출력**을 클릭하여 SendGrid 출력 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="86ea2-133">**API 키** 및 **메시지 매개 변수 이름** 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="86ea2-134">원할 경우 지금 다른 속성을 입력하거나 코드를 대신 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="86ea2-135">이러한 설정은 기본값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-135">These settings can be used as defaults.</span></span>

 ![SendGrid 출력 바인딩 구성](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="86ea2-137">함수에 바인딩을 추가하면 함수 폴더에 **function.json**이라는 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="86ea2-138">이 파일에는 Azure Function의 **통합** 탭에서 볼 수 있는 것과 동일한 모든 정보가 Json 형식으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="86ea2-139">**ApiKey**, **메시지** 및 **보낸 사람** 필드를 설정하면 **function.json** 파일에 다음 항목이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="86ea2-140">원할 경우 이 파일을 직접 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="86ea2-141">이제 함수 앱 및 함수를 만들고 구성했으므로 전자 메일을 보내는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="86ea2-142">전자 메일을 만들어 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="86ea2-142">Write code that creates and sends email</span></span>

<span data-ttu-id="86ea2-143">SendGrid API에는 전자 메일을 만들어 보내는 데 필요한 모든 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="86ea2-144">함수의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-144">Replace the code in the function with the following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change to email of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="86ea2-145">첫 번째 줄에는 SendGrid 어셈블리를 참조하는 ```#r``` 지시문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="86ea2-146">그 후에는 ```using``` 문을 사용하여 해당 네임스페이스의 개체에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="86ea2-147">코드에서 SendGrid API로부터 전자 메일을 구성하는 ```Mail```, ```Personalization``` 및 ```Content``` 개체 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="86ea2-148">메시지를 반환하는 경우 SendGrid가 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="86ea2-149">함수의 서명에도 ```message```라는 ```Mail``` 형식의 추가 출력 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="86ea2-150">입력 및 출력 바인딩 모두 코드에서 함수 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="86ea2-151">**테스트**를 클릭하고 메시지를 **요청 본문** 필드에 입력한 후 **실행** 단추를 클릭하여 코드를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![코드 테스트](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="86ea2-153">전자 메일을 검토하여 SendGrid에서 전자 메일을 보냈는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="86ea2-154">1단계의 코드에서 주소로 이동한 후 **요청 본문**의 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86ea2-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86ea2-155">Next steps</span></span>
<span data-ttu-id="86ea2-156">이 문서에서는 SendGrid 서비스를 사용하여 전자 메일을 만들고 전송하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="86ea2-157">앱에서 Azure Functions를 사용하는 방법에 대해 자세히 알아보려면 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86ea2-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="86ea2-158">[Azure Functions에 대한 모범 사례](functions-best-practices.md) Azure Functions를 만들 때 사용할 몇 가지 모범 사례를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="86ea2-159">[Azure Functions 개발자 참조](functions-reference.md) 함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="86ea2-160">[Azure Functions 테스트](functions-test-a-function.md) 함수를 테스트하는 다양한 도구와 기법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86ea2-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>