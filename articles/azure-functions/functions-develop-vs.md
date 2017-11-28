---
title: "Visual Studio를 사용 하 여 Azure 함수 aaaDevelop | Microsoft Docs"
description: "자세한 내용은 방법 Visual Studio 2017에 대 한 Azure 기능 도구를 사용 하 여 Azure 함수 toodevelop 및 테스트 합니다."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="26c96-103">Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26c96-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="26c96-104">Visual Studio 2017 용 azure 기능 도구는 개발, 테스트 및 C# 기능 tooAzure 배포할 수 있는 Visual Studio에 대 한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions tooAzure.</span></span> <span data-ttu-id="26c96-105">첫 번째 환경과 Azure 함수 이면에서 자세히 알아볼 수 있습니다 [소개 tooAzure 함수](functions-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-105">If this is your first experience with Azure Functions, you can learn more at [An introduction tooAzure Functions](functions-overview.md).</span></span>

<span data-ttu-id="26c96-106">hello를 Azure 함수 도구 hello를 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-106">hello Azure Functions Tools provides hello following benefits:</span></span> 

* <span data-ttu-id="26c96-107">로컬 개발 컴퓨터에서 함수를 편집, 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="26c96-108">게시 Azure 함수 프로젝트 tooAzure 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-108">Publish your Azure Functions project directly tooAzure.</span></span> 
* <span data-ttu-id="26c96-109">WebJobs 특성 toodeclare 함수 바인딩이 hello 바인딩 정의 대 한 별도 function.json 유지 하는 대신 C# 코드에서 직접 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-109">Use WebJobs attributes toodeclare function bindings directly in hello C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="26c96-110">미리 컴파일된 C# 함수를 개발하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="26c96-111">미리 컴파일된 함수는 C# 스크립트 기반 함수보다 더 뛰어난 콜드 부팅 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="26c96-112">C#에서 함수를 모두 Visual Studio 개발 hello 활용 하는 동안 코드.</span><span class="sxs-lookup"><span data-stu-id="26c96-112">Code your functions in C# while having all of hello benefits of Visual Studio development.</span></span> 

<span data-ttu-id="26c96-113">이 항목에서는 방법을 toouse hello Azure 함수 도구 Visual Studio 2017 toodevelop에 대 한 C#에서 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-113">This topic shows you how toouse hello Azure Functions Tools for Visual Studio 2017 toodevelop your functions in C#.</span></span> <span data-ttu-id="26c96-114">또한 학습 방법을 toopublish.NET 어셈블리와 프로젝트 tooAzure 프로그램.</span><span class="sxs-lookup"><span data-stu-id="26c96-114">You also learn how toopublish your project tooAzure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26c96-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="26c96-115">Prerequisites</span></span>

<span data-ttu-id="26c96-116">기능 도구를 azure의 hello Azure 개발 작업에 포함 된 [Visual Studio 2017 버전 15.3](https://www.visualstudio.com/vs/), 또는 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-116">Azure Functions Tools is included in hello Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="26c96-117">Hello 포함 되어 있는지 확인 **Azure 개발** Visual Studio 2017 15.3 버전 설치에는 작업:</span><span class="sxs-lookup"><span data-stu-id="26c96-117">Make sure you include hello **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Visual Studio 2017 hello Azure 개발 작업이 포함 된 설치](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="26c96-119">toocreate 함수 배포도 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-119">toocreate and deploy functions, you also need:</span></span>

* <span data-ttu-id="26c96-120">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="26c96-120">An active Azure subscription.</span></span> <span data-ttu-id="26c96-121">Azure 구독이 아직 없는 경우 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="26c96-122">Azure Storage 계정.</span><span class="sxs-lookup"><span data-stu-id="26c96-122">An Azure Storage account.</span></span> <span data-ttu-id="26c96-123">저장소 계정 toocreate 참조 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-123">toocreate a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="26c96-124">Azure Functions 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="26c96-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a><span data-ttu-id="26c96-125">로컬 개발에 대 한 hello 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="26c96-125">Configure hello project for local development</span></span>

<span data-ttu-id="26c96-126">Hello Azure 함수 템플릿을 사용 하 여 새 프로젝트를 만들 때 빈 C# 프로젝트 hello 다음 파일이 포함 된 가져오기:</span><span class="sxs-lookup"><span data-stu-id="26c96-126">When you create a new project using hello Azure Functions template, you get an empty C# project that contains hello following files:</span></span>

* <span data-ttu-id="26c96-127">**host.json**: 함수 호스트를 hello 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-127">**host.json**: Lets you configure hello Functions host.</span></span> <span data-ttu-id="26c96-128">이러한 설정은 로컬 및 Azure에서 실행할 때 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="26c96-129">자세한 내용은 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26c96-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="26c96-130">**local.settings.json**: 함수를 로컬로 실행할 때 사용되는 설정을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="26c96-131">이러한 설정은 Azure에서 사용 되지 않습니다, hello에 사용 되는 [Azure 함수 핵심 도구](functions-run-local.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-131">These settings are not used by Azure, they are used by hello [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="26c96-132">연결 문자열 tooother Azure 같은 파일 toospecify 설정이이 사용 하 여 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-132">Use this file toospecify settings, such as connection strings tooother Azure services.</span></span> <span data-ttu-id="26c96-133">새 키 toohello 추가 **값** 프로젝트에서 함수에 필요한 각 연결에 대 한 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-133">Add a new key toohello **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="26c96-134">자세한 내용은 참조 [로컬 설정 파일](functions-run-local.md#local-settings-file) hello Azure 함수 핵심 도구 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in hello Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="26c96-135">hello 함수 런타임에서 Azure 저장소 계정을 내부적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-135">hello Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="26c96-136">HTTP 및 webhook 이외의 종류를 트리거할 모든 hello 설정 해야 **Values.AzureWebJobsStorage** tooa 유효한 Azure 저장소 계정 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-136">For all trigger types other than HTTP and webhooks, you must set hello **Values.AzureWebJobsStorage** key tooa valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="26c96-137">tooset hello 저장소 계정 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="26c96-137">tooset hello storage account connection string:</span></span>

1. <span data-ttu-id="26c96-138">Visual Studio에서 열고 **클라우드 탐색기**를 확장 하 고 **저장소 계정** > **저장소 계정**을 선택한 후 **속성**및 복사 hello **기본 연결 문자열** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy hello **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="26c96-139">프로젝트를 hello local.settings.json 프로젝트 파일을 열고 hello의 hello 값 설정 **AzureWebJobsStorage** 복사한 toohello 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-139">In your project, open hello local.settings.json project file and set hello value of hello **AzureWebJobsStorage** key toohello connection string you copied.</span></span>

3. <span data-ttu-id="26c96-140">Hello 이전 단계 tooadd 고유 키 toohello 반복 **값** 함수에 필요한 다른 연결에 대 한 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-140">Repeat hello previous step tooadd unique keys toohello **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="26c96-141">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="26c96-141">Create a function</span></span>

<span data-ttu-id="26c96-142">미리 컴파일된 함수 hello 함수에 의해 사용 되는 hello 바인딩은 hello 코드의 특성을 적용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-142">In pre-compiled functions, hello bindings used by hello function are defined by applying attributes in hello code.</span></span> <span data-ttu-id="26c96-143">Hello Azure 함수 도구 toocreate hello 제공 된 템플릿에서 함수를 사용 하면 이러한 특성을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-143">When you use hello Azure Functions Tools toocreate your functions from hello provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="26c96-144">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="26c96-145">선택 **Azure 함수**, 입력 **이름** hello 클래스 및 클릭에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-145">Select **Azure Function**, type a **Name** for hello class, and click **Add**.</span></span>

2. <span data-ttu-id="26c96-146">사용자의 트리거를 선택 하 고, hello 바인딩 속성을 설정, 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-146">Choose your trigger, set hello binding properties, and click **Create**.</span></span> <span data-ttu-id="26c96-147">hello 다음 예제에서는 hello 설정이 트리거되면 큐 저장소를 만드는 함수</span><span class="sxs-lookup"><span data-stu-id="26c96-147">hello following example shows hello settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="26c96-148">명명 된 연결 문자열 키 **QueueStorage** 가 제공 된 hello local.settings.json 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-148">A connection string key named **QueueStorage** is supplied, which is defined in hello local.settings.json file.</span></span> 
 
3. <span data-ttu-id="26c96-149">검사 hello 새로 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-149">Examine hello newly added class.</span></span> <span data-ttu-id="26c96-150">정적 참조 **실행** hello 특성을 사용 하는 메서드를 **FunctionName** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-150">You see a static **Run** method, that is attributed with hello **FunctionName** attribute.</span></span> <span data-ttu-id="26c96-151">이 특성 hello 메서드가 hello hello 함수에 대 한 진입점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-151">This attribute indicates that hello method is hello entry point for hello function.</span></span> 

    <span data-ttu-id="26c96-152">예를 들어 hello C# 클래스를 다음 기본 큐 트리거되는 저장소 함수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-152">For example, hello following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="26c96-153">바인딩 고유 특성은 적용 된 tooeach 바인딩 제공 된 매개 변수가 toohello 진입점 메서드.</span><span class="sxs-lookup"><span data-stu-id="26c96-153">A binding-specific attribute is applied tooeach binding parameter supplied toohello entry point method.</span></span> <span data-ttu-id="26c96-154">매개 변수로 hello 바인딩 정보를 사용 하는 hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-154">hello attribute takes hello binding information as parameters.</span></span> <span data-ttu-id="26c96-155">이전 예 hello hello 첫 번째 매개 변수는 한 **QueueTrigger** 트리거한 큐 함수를 나타내는 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-155">In hello previous example, hello first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="26c96-156">hello 큐 이름 및 연결 문자열 설정 이름 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-156">hello queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="26c96-157">테스팅 함수</span><span class="sxs-lookup"><span data-stu-id="26c96-157">Testing functions</span></span>

<span data-ttu-id="26c96-158">Azure Functions Core 도구를 사용하면 로컬 개발 컴퓨터에서 Azure Functions 프로젝트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="26c96-159">이러한 도구는 Visual Studio에서 함수를 시작할 처음으로 hello 메시지 표시 tooinstall 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-159">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="26c96-160">tootest 함수를 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-160">tootest your function, press F5.</span></span> <span data-ttu-id="26c96-161">메시지가 표시 되 면 Visual Studio toodownload의 hello 요청을 받을 하 고 Azure 함수 코어 (CLI) 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-161">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="26c96-162">방화벽 예외를 tooenable hello 도구는 HTTP 요청을 처리할 수 있도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-162">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

<span data-ttu-id="26c96-163">실행 하는 hello 프로젝트에서 배포 된 함수를 테스트할 때 코드를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-163">With hello project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="26c96-164">자세한 내용은 [Azure Functions에서 코드를 테스트하기 위한 전략](functions-test-a-function.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26c96-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="26c96-165">디버그 모드에서 실행할 때 중단점이 예상대로 Visual Studio에서 적중됩니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="26c96-166">큐 tootest 함수를 실행 하는 방법의 예를 들어 참조 hello [트리거한 큐 함수 빠른 시작 자습서](functions-create-storage-queue-triggered-function.md#test-the-function)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-166">For an example of how tootest a queue triggered function, see hello [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="26c96-167">hello Azure 함수 핵심 도구 사용에 대 한 더 toolearn 참조 [코드 및 Azure 함수 로컬로 테스트](functions-run-local.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-167">toolearn more about using hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-tooazure"></a><span data-ttu-id="26c96-168">TooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="26c96-168">Publish tooAzure</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="26c96-169">Hello local.settings.json에서 추가한 모든 설정도 추가 해야 toohello 함수 앱 Azure에서.</span><span class="sxs-lookup"><span data-stu-id="26c96-169">Any settings you added in hello local.settings.json must be also added toohello function app in Azure.</span></span> <span data-ttu-id="26c96-170">이러한 설정은 자동으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-170">These settings are not added automatically.</span></span> <span data-ttu-id="26c96-171">다음이 방법 중 하나에 필요한 설정을 tooyour 함수 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-171">You can add required settings tooyour function app in one of these ways:</span></span>
>
>* <span data-ttu-id="26c96-172">[Azure 포털 hello를 사용 하 여](functions-how-to-use-azure-function-app-settings.md#settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-172">[Using hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="26c96-173">[Hello를 사용 하 여 `--publish-local-settings` hello Azure 함수 핵심 도구에서에서 게시 옵션](functions-run-local.md#publish)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-173">[Using hello `--publish-local-settings` publish option in hello Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="26c96-174">[Azure CLI hello를 사용 하 여](/cli/azure/functionapp/config/appsettings#set)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-174">[Using hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="26c96-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26c96-175">Next steps</span></span>

<span data-ttu-id="26c96-176">Azure 함수 도구에 대 한 자세한 내용은 참조에 대 한 일반적인 질문 섹션의 hello hello [Azure 함수에 대 한 Visual Studio 2017 도구](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-176">For more information about Azure Functions Tools, see hello Common Questions section of hello [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="26c96-177">hello Azure 함수 핵심 도구에 대해 자세히 toolearn 참조 [코드 및 Azure 함수 로컬로 테스트](functions-run-local.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-177">toolearn more about hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="26c96-178">.NET 클래스 라이브러리 기능 개발에 대 한 더 toolearn 참조 [Azure 함수와 함께 사용 하 여.NET 클래스 라이브러리](functions-dotnet-class-library.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-178">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="26c96-179">이 항목에서는 toouse 특성 toodeclare 다양 한 유형의 Azure 함수에서 지 원하는 바인딩 hello 하는 방법의 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26c96-179">This topic also provides examples of how toouse attributes toodeclare hello various types of bindings supported by Azure Functions.</span></span>    
