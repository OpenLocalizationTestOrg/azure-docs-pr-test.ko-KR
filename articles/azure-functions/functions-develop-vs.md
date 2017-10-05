---
title: "Visual Studio를 사용하여 Azure Functions 개발 | Microsoft Docs"
description: "Azure Functions Tools for Visual Studio 2017을 사용하여 Azure Functions를 개발하고 테스트하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="c62bf-103">Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c62bf-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="c62bf-104">Azure Functions Tools for Visual Studio 2017은 C# 함수를 Azure에 개발, 테스트 및 배포할 수 있는 Visual Studio에 대한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="c62bf-105">Azure Functions을 처음으로 접하는 경우라면 [Azure Functions 소개](functions-overview.md)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="c62bf-106">Azure Functions 도구는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="c62bf-107">로컬 개발 컴퓨터에서 함수를 편집, 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="c62bf-108">Azure에 직접 Azure Functions 프로젝트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="c62bf-109">바인딩 정의에 대한 별도 function.json을 유지하는 대신 WebJobs 특성을 사용하여 함수 바인딩을 C# 코드에 직접 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="c62bf-110">미리 컴파일된 C# 함수를 개발하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="c62bf-111">미리 컴파일된 함수는 C# 스크립트 기반 함수보다 더 뛰어난 콜드 부팅 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="c62bf-112">Visual Studio 개발의 모든 이점을 누리면서 C#에서 함수를 코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="c62bf-113">이 토픽에서는 Azure Functions Tools for Visual Studio 2017을 사용하여 C#에서 함수를 개발하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="c62bf-114">또한 .NET 어셈블리로 Azure에 프로젝트를 게시하는 방법도 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c62bf-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c62bf-115">Prerequisites</span></span>

<span data-ttu-id="c62bf-116">Azure Functions 도구는 [Visual Studio 2017 버전 15.3](https://www.visualstudio.com/vs/) 이상에서 Azure 개발 워크로드의 일부로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="c62bf-117">Visual Studio 2017 버전 15.3 설치에 **Azure 개발** 워크로드가 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Azure 개발 워크로드를 통한 Visual Studio 2017 설치](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="c62bf-119">함수를 만들고 배포하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="c62bf-120">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c62bf-120">An active Azure subscription.</span></span> <span data-ttu-id="c62bf-121">Azure 구독이 아직 없는 경우 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="c62bf-122">Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="c62bf-122">An Azure Storage account.</span></span> <span data-ttu-id="c62bf-123">저장소 계정을 만들려면 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="c62bf-124">Azure Functions 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c62bf-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="c62bf-125">로컬 개발에 대한 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="c62bf-125">Configure the project for local development</span></span>

<span data-ttu-id="c62bf-126">Azure Functions 템플릿을 사용하여 새 프로젝트를 만들 때 다음 파일이 포함된 빈 C# 프로젝트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="c62bf-127">**host.json**: 함수 호스트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="c62bf-128">이러한 설정은 로컬 및 Azure에서 실행할 때 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="c62bf-129">자세한 내용은 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="c62bf-130">**local.settings.json**: 함수를 로컬로 실행할 때 사용되는 설정을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="c62bf-131">이러한 설정은 Azure에서 사용되지 않으며, [Azure Functions 핵심 도구](functions-run-local.md)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="c62bf-132">이 파일을 사용하여 연결 문자열과 같은 설정을 다른 Azure 서비스에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="c62bf-133">프로젝트에서 함수에 필요한 각 연결에 대한 **값** 배열에 새 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="c62bf-134">자세한 내용은 Azure Functions 핵심 도구 토픽의 [로컬 설정 파일](functions-run-local.md#local-settings-file)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="c62bf-135">함수 런타임에서 Azure Storage 계정을 내부적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="c62bf-136">HTTP 및 웹후크 이외의 모든 트리거 형식을 위해 **Values.AzureWebJobsStorage** 키를 유효한 Azure Storage 계정 연결 문자열에 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="c62bf-137">저장소 계정 연결 문자열을 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="c62bf-138">Visual Studio에서 **클라우드 탐색기**를 열고 **저장소 계정** > **저장소 계정**을 확장한 후 **속성**을 선택하고 **기본 연결 문자열** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="c62bf-139">사용자 프로젝트에서 local.settings.json 프로젝트 파일을 열고 **AzureWebJobsStorage** 키의 값을 복사한 연결 문자열로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="c62bf-140">이전 단계를 반복하여 사용자의 함수에 필요한 다른 연결에 대한 **값** 배열에 고유 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="c62bf-141">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="c62bf-141">Create a function</span></span>

<span data-ttu-id="c62bf-142">미리 컴파일된 함수에서 함수에 사용된 바인딩은 코드에 특성을 적용함에 따라 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="c62bf-143">Azure Functions 도구를 사용하여 제공된 템플릿에서 함수를 만들 때 이러한 특성이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="c62bf-144">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="c62bf-145">**Azure Function**을 선택하고 클래스에 사용할 **이름**을 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="c62bf-146">사용자의 트리거를 선택하고, 바인딩 속성을 설정한 후, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="c62bf-147">다음 예제에서는 Queue Storage 트리거 함수를 만들 때 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="c62bf-148">local.settings.json 파일에 정의된 **QueueStorage**라고 명명된 연결 문자열 키가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="c62bf-149">새로 추가된 클래스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-149">Examine the newly added class.</span></span> <span data-ttu-id="c62bf-150">**FunctionName** 특성으로 보이는 정적 **실행** 메서드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="c62bf-151">이 특성은 메서드가 함수에 대한 진입점임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="c62bf-152">예를 들어 다음 C# 클래스는 기본 Queue Storage 트리거 함수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

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
 
    <span data-ttu-id="c62bf-153">바인딩 고유 특성은 진입점 메서드에 적용되는 각 바인딩 매개 변수에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="c62bf-154">특성은 매개 변수로 바인딩 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="c62bf-155">이전 예제에서 첫 매개 변수는 큐 트리거 함수를 나타내는 **QueueTrigger** 특성이 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="c62bf-156">큐 이름 및 연결 문자열 설정 이름은 매개 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="c62bf-157">테스팅 함수</span><span class="sxs-lookup"><span data-stu-id="c62bf-157">Testing functions</span></span>

<span data-ttu-id="c62bf-158">Azure Functions Core 도구를 사용하면 로컬 개발 컴퓨터에서 Azure Functions 프로젝트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="c62bf-159">Visual Studio에서 처음으로 함수를 시작할 때 이 도구를 설치하도록 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="c62bf-160">함수를 테스트하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-160">To test your function, press F5.</span></span> <span data-ttu-id="c62bf-161">메시지가 표시되면 Visual Studio에서 Azure Functions Core(CLI) 도구를 다운로드하여 설치하도록 요구하는 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="c62bf-162">또한 도구에서 HTTP 요청을 처리할 수 있도록 방화벽 예외를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="c62bf-163">실행 중인 프로젝트와 함께 배포된 함수를 테스트할 때 코드를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="c62bf-164">자세한 내용은 [Azure Functions에서 코드를 테스트하기 위한 전략](functions-test-a-function.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="c62bf-165">디버그 모드에서 실행할 때 중단점이 예상대로 Visual Studio에서 적중됩니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="c62bf-166">큐 트리거 함수를 테스트하는 방법에 대한 예제는 [큐 트리거 함수 빠른 시작 자습서](functions-create-storage-queue-triggered-function.md#test-the-function)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="c62bf-167">Azure Functions 핵심 도구 사용에 대한 자세한 내용은 [Azure Functions를 로컬로 코딩 및 테스트](functions-run-local.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="c62bf-168">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="c62bf-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="c62bf-169">local.settings.json에서 추가한 모든 설정을 Azure의 함수 앱에도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="c62bf-170">이러한 설정은 자동으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-170">These settings are not added automatically.</span></span> <span data-ttu-id="c62bf-171">다음 방법 중 하나로 필요한 설정을 함수 앱에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="c62bf-172">[Azure Portal 사용](functions-how-to-use-azure-function-app-settings.md#settings)</span><span class="sxs-lookup"><span data-stu-id="c62bf-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="c62bf-173">[`--publish-local-settings` Azure Functions 핵심 도구의 게시 옵션](functions-run-local.md#publish) 사용</span><span class="sxs-lookup"><span data-stu-id="c62bf-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="c62bf-174">[Azure CLI 사용](/cli/azure/functionapp/config/appsettings#set)</span><span class="sxs-lookup"><span data-stu-id="c62bf-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c62bf-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c62bf-175">Next steps</span></span>

<span data-ttu-id="c62bf-176">Azure Functions 도구에 대한 자세한 내용은 [Azure Functions에 대한 Visual Studio 2017 도구](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) 블로그 게시물의 일반적인 질문 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="c62bf-177">Azure Functions 핵심 도구에 대한 자세한 내용은 [Azure Functions를 로컬로 코딩 및 테스트](functions-run-local.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="c62bf-178">.NET 클래스 라이브러리로 기능을 개발하는 방법에 대해 자세히 알아보려면 [Azure Functions에서 .NET 클래스 라이브러리 사용](functions-dotnet-class-library.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c62bf-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="c62bf-179">이 항목에서는 특성을 사용하여 Azure Functions에서 지원하는 다양한 유형의 바인딩을 선언하는 방법의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c62bf-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
