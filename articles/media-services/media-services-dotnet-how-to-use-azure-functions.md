---
title: "Media Services에서 Azure Functions 개발"
description: "이 항목에서는 Azure Portal을 사용하여 Media Services에서 Azure Functions를 개발하기 시작하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="59046-103">Media Services에서 Azure Functions 개발</span><span class="sxs-lookup"><span data-stu-id="59046-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="59046-104">이 항목에서는 Media Services를 사용하는 Azure Functions를 만들기 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59046-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="59046-105">이 항목에 정의된 Azure Function은 새 MP4 파일에 대한 저장소 계정 컨테이너 **input**을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="59046-106">저장소 컨테이너에서 파일이 삭제되면 blob 트리거가 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="59046-107">Azure Media Services를 사용하는 기존 Azure Functions를 탐색하고 배포하려는 경우 [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="59046-108">이 리포지토리는 Blob Storage에서 직접 콘텐츠를 수집하고 Blob Storage에 콘텐츠를 인코딩 및 작성하는 데 관련된 워크플로를 표시하는 데 Media Services를 사용하는 예제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="59046-109">또한 WebHooks 및 Azure 큐를 통해 작업 알림을 모니터링하는 방법의 예도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="59046-110">[Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) 리포지토리의 예제를 기반으로 함수를 개발할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="59046-111">함수를 배포하려면 **Azure에 배포** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="59046-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59046-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="59046-112">Prerequisites</span></span>

- <span data-ttu-id="59046-113">첫 번째 함수를 만들기 전에 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="59046-114">Azure 계정이 아직 없는 경우 [체험 계정을 사용](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="59046-115">AMS(Azure Media Services) 계정에서 작업을 수행하거나 Media Services에서 보낸 이벤트를 수신 대기하는 Azure Functions를 만들려는 경우 [여기](media-services-portal-create-account.md)에 설명한 대로 AMS 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="59046-116">[Azure Functions를 사용하는 방법](../azure-functions/functions-overview.md)을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="59046-117">또한 다음을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-117">Also, review:</span></span>
    - [<span data-ttu-id="59046-118">Azure Functions HTTP 및 웹후크 바인딩</span><span class="sxs-lookup"><span data-stu-id="59046-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="59046-119">Azure 함수 앱 설정을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="59046-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="59046-120">고려 사항</span><span class="sxs-lookup"><span data-stu-id="59046-120">Considerations</span></span>

-  <span data-ttu-id="59046-121">소비 계획에서 실행되는 Azure Functions의 시간 초과 제한은 5분입니다.</span><span class="sxs-lookup"><span data-stu-id="59046-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="59046-122">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="59046-122">Create a function app</span></span>

1. <span data-ttu-id="59046-123">[Azure Portal](http://portal.azure.com) 로 이동하여 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="59046-124">[여기](../azure-functions/functions-create-function-app-portal.md)에 설명한 대로 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59046-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="59046-125">**StorageConnection** 환경 변수에 지정(다음 단계 참조)한 저장소 계정은 앱과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="59046-126">함수 앱 구성 설정</span><span class="sxs-lookup"><span data-stu-id="59046-126">Configure function app settings</span></span>

<span data-ttu-id="59046-127">Media Services 함수를 개발하는 경우 함수 전체에서 사용할 환경 변수를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="59046-128">앱 설정을 구성하려면 앱 설정 구성 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="59046-129">자세한 내용은 [Azure 함수 앱 설정을 구성하는 방법](../azure-functions/functions-how-to-use-azure-function-app-settings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="59046-130">예:</span><span class="sxs-lookup"><span data-stu-id="59046-130">For example:</span></span>

![설정](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="59046-132">이 문서에 정의된 함수는 앱 설정에 다음 환경 변수가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="59046-133">**AMSAccount**: *AMS 계정 이름*(예: testams)</span><span class="sxs-lookup"><span data-stu-id="59046-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="59046-134">**AMSKey**: *AMS 계정 키*(예: IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="59046-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="59046-135">**MediaServicesStorageAccountName**: *저장소 계정 이름*(예: testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="59046-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="59046-136">**MediaServicesStorageAccountKey**: *저장소 계정 키*(예: xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX = =)</span><span class="sxs-lookup"><span data-stu-id="59046-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="59046-137">**StorageConnection**: *저장소 연결*(예: DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX = = =)</span><span class="sxs-lookup"><span data-stu-id="59046-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="59046-138">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="59046-138">Create a function</span></span>

<span data-ttu-id="59046-139">함수 앱을 배포하면 **App Services** Azure Functions에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="59046-140">함수 앱을 선택하고 **새 함수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="59046-141">**C#** 언어 및 **데이터 처리** 시나리오를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="59046-142">**BlobTrigger** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="59046-143">이 함수는 Blob이 **input** 컨테이너에 업로드될 때마다 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="59046-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="59046-144">**input** 이름은 다음 단계에서 **Path**에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="59046-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![업로드](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="59046-146">**BlobTrigger**를 선택하면 페이지에 몇 가지 추가 컨트롤이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59046-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![업로드](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="59046-148">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="59046-149">파일</span><span class="sxs-lookup"><span data-stu-id="59046-149">Files</span></span>

<span data-ttu-id="59046-150">Azure Function은 이 섹션에 설명된 코드 파일 및 기타 파일과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="59046-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="59046-151">기본적으로 함수는 **function.json** 및 **run.csx**(C#) 파일과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="59046-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="59046-152">**project.json** 파일을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="59046-153">이 섹션의 나머지 부분에서는 이러한 파일의 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59046-153">The rest of this section shows the definitions for these files.</span></span>

![업로드](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="59046-155">function.json</span><span class="sxs-lookup"><span data-stu-id="59046-155">function.json</span></span>

<span data-ttu-id="59046-156">function.json 파일은 함수 바인딩 및 기타 구성 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="59046-157">런타임은 이 파일을 사용하여 모니터링할 이벤트와 함수 실행에서 데이터를 전달하고 반환하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="59046-158">자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](../azure-functions/functions-reference.md#function-code)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="59046-159">함수가 실행되지 않도록 **disabled** 속성을 **true**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="59046-160">**function.json** 파일의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="59046-161">project.json</span><span class="sxs-lookup"><span data-stu-id="59046-161">project.json</span></span>

<span data-ttu-id="59046-162">project.json 파일은 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="59046-163">다음은 Nuget의 필수 .NET Azure Media Services 패키지를 포함하는 **project.json** 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="59046-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="59046-164">버전 번호가 패키지의 최신 업데이트로 변경되므로 가장 최근 버전을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="59046-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="59046-165">run.csx</span></span>

<span data-ttu-id="59046-166">함수에 대한 C# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="59046-166">This is the C# code for your function.</span></span>  <span data-ttu-id="59046-167">아래 정의된 함수는 새 MP4 파일에 대한 저장소 계정 컨테이너 **input**(경로에 지정됨)을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="59046-168">저장소 컨테이너에서 파일이 삭제되면 blob 트리거가 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="59046-169">이 섹션에 정의된 예제는 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59046-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="59046-170">AMS 자산에 blob을 복사하여 Media Services 계정에 자산을 수집하는 방법</span><span class="sxs-lookup"><span data-stu-id="59046-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="59046-171">Media Encoder Standard의 "적응 스트리밍" 사전 설정을 사용하는 인코딩 작업을 제출하는 방법</span><span class="sxs-lookup"><span data-stu-id="59046-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="59046-172">실제 시나리오에서는 작업 진행률을 추적한 다음 인코딩된 자산을 게시할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="59046-173">자세한 내용은 [Azure 웹후크를 사용하여 Media Services 작업 알림 모니터링](media-services-dotnet-check-job-progress-with-webhooks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="59046-174">더 많은 예제는 [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="59046-175">함수를 정의했으면 **저장 및 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="59046-176">함수 테스트</span><span class="sxs-lookup"><span data-stu-id="59046-176">Test your function</span></span>

<span data-ttu-id="59046-177">함수를 테스트하려면 연결 문자열에 지정한 저장소 계정의 **input** 컨테이너에 MP4 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59046-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="59046-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59046-178">Next step</span></span>

<span data-ttu-id="59046-179">이제 미디어 서비스 응용 프로그램 개발을 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59046-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="59046-180">Azure Media Services에서 Azure Functions 및 Logic Apps를 사용하여 사용자 지정 콘텐츠 만들기 워크플로를 만드는 방법에 대한 자세한 내용 및 전체 샘플/솔루션은 [GitHub의 Media Services .NET 함수 통합 샘플](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="59046-181">또한 [Azure 웹후크를 사용하여 .NET으로 Media Services 작업 알림 모니터링](media-services-dotnet-check-job-progress-with-webhooks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59046-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="59046-182">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="59046-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="59046-183">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="59046-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

