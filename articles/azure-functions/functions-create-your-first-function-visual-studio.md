---
title: "Visual Studio를 사용 하 여 Azure에서 첫 번째 작동 aaaCreate | Microsoft Docs"
description: "만들고 Visual Studio에 대 한 Azure 기능 도구를 사용 하 여 간단한 HTTP 트리거된 함수 tooAzure 게시 합니다."
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
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="68ca6-104">Visual Studio를 사용하여 첫 번째 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="68ca6-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="68ca6-105">Azure 기능을 사용 하면 toofirst VM을 만들거나 웹 응용 프로그램을 게시 하지 않고도 서버가 없는 환경에서 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="68ca6-106">이 항목에서는 방법을 toouse toocreate Azure 함수에 대 한 Visual Studio 2017 도구 hello 함수 및 테스트 "hello world" 로컬로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="68ca6-107">Hello 함수 코드 tooAzure 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="68ca6-108">이러한 도구는 이후 버전 또는 Visual Studio 2017 15.3, 버전의에서 hello Azure 개발 작업의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Visual Studio 프로젝트의 Azure Functions 코드](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="68ca6-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="68ca6-110">Prerequisites</span></span>

<span data-ttu-id="68ca6-111">toocomplete이 자습서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="68ca6-112">[Visual Studio 2017 버전 15.3](https://www.visualstudio.com/vs/preview/), hello를 포함 하 여 **Azure 개발** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Visual Studio 2017 hello Azure 개발 작업이 포함 된 설치](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="68ca6-114">를 설치 하거나 tooVisual Studio 2017 15.3 버전을 업그레이드 한 후 Azure 함수에 대 한 toomanually 업데이트 hello Visual Studio 2017 도구 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="68ca6-115">Hello 도구 hello에서 업데이트할 수 있습니다 **도구** 메뉴 아래 **확장명 및 업데이트 중...**   >  **업데이트** > **Visual Studio 마켓플레이스** > **Azure 함수 및 웹 작업이 도구**  >  **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="68ca6-116">Visual Studio에서 Azure Functions 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="68ca6-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="68ca6-117">Hello 프로젝트를 만든 첫 번째 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="68ca6-118">Hello 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="68ca6-118">Create hello function</span></span>

1. <span data-ttu-id="68ca6-119">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="68ca6-120">**Azure 함수**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="68ca6-121">**HttpTrigger**를 선택하고, **함수 이름**을 입력하고, **익명**에 대한 **액세스 권한**을 선택하고, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="68ca6-122">만든 hello 함수는 모든 클라이언트에서 HTTP 요청에 의해 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![새 Azure 함수 만들기](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="68ca6-124">코드 파일을 함수 코드를 구현 하는 클래스를 포함 하는 tooyour 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="68ca6-125">이 코드는 이름 값을 수신한 후 다시 에코하는 템플릿을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="68ca6-126">hello **FunctionName** 특성 설정 hello 함수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="68ca6-127">hello **HttpTrigger** 특성 hello 함수를 트리거하는 hello 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![함수 코드 파일](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="68ca6-129">이제 HTTP에서 트리거한 함수를 만들었으므로 로컬 컴퓨터에서 해당 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="68ca6-130">로컬로 테스트 hello 함수</span><span class="sxs-lookup"><span data-stu-id="68ca6-130">Test hello function locally</span></span>

<span data-ttu-id="68ca6-131">Azure Functions Core 도구를 사용하면 로컬 개발 컴퓨터에서 Azure Functions 프로젝트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="68ca6-132">이러한 도구는 Visual Studio에서 함수를 시작할 처음으로 hello 메시지 표시 tooinstall 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="68ca6-133">tootest 함수를 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-133">tootest your function, press F5.</span></span> <span data-ttu-id="68ca6-134">메시지가 표시 되 면 Visual Studio toodownload의 hello 요청을 받을 하 고 Azure 함수 코어 (CLI) 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="68ca6-135">방화벽 예외를 tooenable hello 도구는 HTTP 요청을 처리할 수 있도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="68ca6-136">Hello Azure 함수 런타임에서 함수의 hello URL 복사를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Azure 로컬 런타임](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="68ca6-138">Hello HTTP 요청에 대 한 hello URL을 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="68ca6-139">쿼리 문자열 hello 추가 `&name=<yourname>` toothis URL hello 요청을 실행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="68ca6-140">hello 다음 hello 브라우저 toohello 로컬 GET 요청에 hello 함수에서 반환 된 hello 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Hello 브라우저에서 localhost 응답 함수](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="68ca6-142">디버깅, toostop 클릭 hello **중지** hello Visual Studio 도구 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="68ca6-143">Hello 함수 로컬 컴퓨터에서 제대로 실행 되는지 확인 한 후에 시간 toopublish hello 프로젝트 tooAzure 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="68ca6-144">Hello 프로젝트 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="68ca6-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="68ca6-145">프로젝트를 게시하려면 먼저 Azure 구독에 함수 앱이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="68ca6-146">Visual Studio에서 직접 함수 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="68ca6-147">Azure에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="68ca6-147">Test your function in Azure</span></span>

1. <span data-ttu-id="68ca6-148">Hello 게시 프로필 페이지에서 hello hello 함수 응용 프로그램의 기준 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="68ca6-149">Hello 대체 `localhost:port` hello 새 기준 URL 사용 하 여 로컬로 hello 함수를 테스트할 때 사용 하는 hello URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="68ca6-150">이전 처럼 있는지 tooappend hello 쿼리 문자열을 확인 `&name=<yourname>` toothis URL hello 요청을 실행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="68ca6-151">HTTP를 호출 하는 hello URL 트리거할 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="68ca6-152">Hello HTTP 요청에 대 한 새 URL이 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="68ca6-153">hello 다음 hello 브라우저 toohello 원격 GET 요청에 hello 함수에서 반환 된 hello 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Hello 브라우저에서 응답 함수](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="68ca6-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68ca6-155">Next steps</span></span>

<span data-ttu-id="68ca6-156">Visual Studio는 C# toocreate 함수 앱 간단한 HTTP 트리거된 함수와 함께 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="68ca6-157">toolearn 어떻게 tooconfigure 프로젝트 toosupport 다른 종류의 트리거 및 바인딩 참조 hello [로컬 개발에 대 한 구성 hello 프로젝트](functions-develop-vs.md#configure-the-project-for-local-development) 섹션 [Azure 함수 Tools for Visual Studio](functions-develop-vs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="68ca6-158">로컬 테스트 및 hello Azure 함수 핵심 도구를 사용 하 여 디버깅에 대해 자세히 toolearn 참조 [코드 및 테스트 Azure 함수 로컬로](functions-run-local.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="68ca6-159">.NET 클래스 라이브러리 기능 개발에 대 한 더 toolearn 참조 [Azure 함수와 함께 사용 하 여.NET 클래스 라이브러리](functions-dotnet-class-library.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68ca6-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

