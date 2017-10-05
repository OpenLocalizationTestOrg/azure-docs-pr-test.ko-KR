---
title: "Visual Studio를 사용하여 Azure에서 첫 번째 함수 만들기 | Microsoft Docs"
description: "Azure Functions Tools for Visual Studio를 사용하여 간단하고 HTTP에서 트리거한 함수를 Azure에 만들고 게시합니다."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "Azure 함수, 함수, 이벤트 처리, 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="a0ed2-104">Visual Studio를 사용하여 첫 번째 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="a0ed2-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="a0ed2-105">Azure Functions를 사용하면 먼저 VM을 만들거나 웹 응용 프로그램을 게시하지 않고도 서버를 사용하지 않는 환경에서 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="a0ed2-106">이 항목에서는 Visual Studio 2017 tools for Azure Functions를 사용하여 로컬에서 "hello world" 함수를 만들고 테스트하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="a0ed2-107">그런 다음 함수 코드를 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="a0ed2-108">이러한 도구는 Visual Studio 2017 버전 15.3 이상에서 Azure 개발 워크로드의 일부로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Visual Studio 프로젝트의 Azure Functions 코드](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="a0ed2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a0ed2-110">Prerequisites</span></span>

<span data-ttu-id="a0ed2-111">이 자습서를 완료하려면 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="a0ed2-112">[Visual Studio 2017 버전 15.3](https://www.visualstudio.com/vs/preview/)(**Azure 개발** 워크로드 포함)</span><span class="sxs-lookup"><span data-stu-id="a0ed2-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![Azure 개발 워크로드를 통한 Visual Studio 2017 설치](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="a0ed2-114">Visual Studio 2017 버전 15.3을 설치하거나 업그레이드한 후 Visual Studio 2017 tools for Azure Functions를 수동으로 업데이트해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="a0ed2-115">**확장 및 업데이트...** > **업데이트** > **Visual Studio Marketplace** > **Azure Functions 및 Web Jobs Tools** > **업데이트** 아래의 **도구** 메뉴에서 도구를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="a0ed2-116">Visual Studio에서 Azure Functions 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a0ed2-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="a0ed2-117">이제 프로젝트를 만들었으므로 첫 번째 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="a0ed2-118">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="a0ed2-118">Create the function</span></span>

1. <span data-ttu-id="a0ed2-119">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="a0ed2-120">**Azure 함수**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="a0ed2-121">**HttpTrigger**를 선택하고, **함수 이름**을 입력하고, **익명**에 대한 **액세스 권한**을 선택하고, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="a0ed2-122">만든 함수는 모든 클라이언트의 HTTP 요청으로 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![새 Azure 함수 만들기](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="a0ed2-124">함수 코드를 구현하는 클래스가 들어 있는 프로젝트에 코드 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="a0ed2-125">이 코드는 이름 값을 수신한 후 다시 에코하는 템플릿을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="a0ed2-126">**FunctionName** 특성은 함수의 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="a0ed2-127">**HttpTrigger** 특성은 함수를 트리거하는 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![함수 코드 파일](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="a0ed2-129">이제 HTTP에서 트리거한 함수를 만들었으므로 로컬 컴퓨터에서 해당 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="a0ed2-130">로컬에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="a0ed2-130">Test the function locally</span></span>

<span data-ttu-id="a0ed2-131">Azure Functions Core 도구를 사용하면 로컬 개발 컴퓨터에서 Azure Functions 프로젝트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="a0ed2-132">Visual Studio에서 처음으로 함수를 시작할 때 이 도구를 설치하도록 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="a0ed2-133">함수를 테스트하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-133">To test your function, press F5.</span></span> <span data-ttu-id="a0ed2-134">메시지가 표시되면 Visual Studio에서 Azure Functions Core(CLI) 도구를 다운로드하여 설치하도록 요구하는 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="a0ed2-135">또한 도구에서 HTTP 요청을 처리할 수 있도록 방화벽 예외를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="a0ed2-136">Azure Functions 런타임 출력에서 함수의 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Azure 로컬 런타임](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="a0ed2-138">HTTP 요청에 대한 URL을 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="a0ed2-139">이 URL에 쿼리 문자열 `&name=<yourname>`을 추가하고 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="a0ed2-140">다음은 함수에서 반환된 로컬 GET 요청에 대한 브라우저의 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![브라우저의 localhost 함수 응답](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="a0ed2-142">디버깅을 중지하려면 Visual Studio 도구 모음에서 **중지** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="a0ed2-143">함수가 로컬 컴퓨터에서 제대로 실행되는지 확인한 후에 해당 프로젝트를 Azure에 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="a0ed2-144">Azure에 프로젝트 게시</span><span class="sxs-lookup"><span data-stu-id="a0ed2-144">Publish the project to Azure</span></span>

<span data-ttu-id="a0ed2-145">프로젝트를 게시하려면 먼저 Azure 구독에 함수 앱이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="a0ed2-146">Visual Studio에서 직접 함수 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="a0ed2-147">Azure에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="a0ed2-147">Test your function in Azure</span></span>

1. <span data-ttu-id="a0ed2-148">게시 프로필 페이지에서 함수 앱의 기준 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="a0ed2-149">로컬에서 함수를 테스트할 때 사용한 URL의 `localhost:port` 부분을 새 기준 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="a0ed2-150">이전처럼 이 URL에 `&name=<yourname>` 쿼리 문자열을 추가하고 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="a0ed2-151">HTTP에서 트리거한 함수를 호출하는 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="a0ed2-152">HTTP 요청에 대한 이러한 새 URL을 브라우저의 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="a0ed2-153">다음은 함수에서 반환된 원격 GET 요청에 대한 브라우저의 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![브라우저의 함수 응답](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="a0ed2-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0ed2-155">Next steps</span></span>

<span data-ttu-id="a0ed2-156">Visual Studio를 사용하여 간단하고 HTTP에서 트리거한 함수가 있는 C# 함수 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="a0ed2-157">다른 종류의 트리거 및 바인딩을 지원하도록 프로젝트를 구성하는 방법은 [Visual Studio용 Azure Functions 도구](functions-develop-vs.md#configure-the-project-for-local-development)의 [로컬 개발에 대한 프로젝트 구성](functions-develop-vs.md) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="a0ed2-158">Azure Functions Core 도구를 사용하여 로컬에서 테스트하고 디버그하는 방법에 대한 자세한 내용은 [Azure Functions를 로컬로 코딩 및 테스트하는 방법](functions-run-local.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="a0ed2-159">.NET 클래스 라이브러리로 기능을 개발하는 방법에 대해 자세히 알아보려면 [Azure Functions에서 .NET 클래스 라이브러리 사용](functions-dotnet-class-library.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0ed2-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

