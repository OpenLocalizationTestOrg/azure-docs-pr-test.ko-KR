---
title: "aaaDevelop 미디어 서비스로 Azure 함수"
description: "이 항목에서는 방법을 사용 하 여 미디어 서비스와 Azure 기능을 개발 하는 toostart hello Azure 포털을 보여줍니다."
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
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="5786f-103">Media Services에서 Azure Functions 개발</span><span class="sxs-lookup"><span data-stu-id="5786f-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="5786f-104">이 항목에서는 tooget 미디어 서비스를 사용 하는 Azure 함수를 만드는 것부터 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="5786f-105">이 항목에 정의 된 Azure 함수 hello 라는 저장소 계정 컨테이너 모니터링 **입력** 새 MP4 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="5786f-106">Hello 저장소 컨테이너에 파일은 삭제 되 면 hello blob 트리거 hello 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="5786f-107">원하는 tooexplore Azure 미디어 서비스를 사용 하는 기존 Azure 함수를 배포 하는 경우 체크 아웃 [미디어 서비스 Azure 함수](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="5786f-108">이 저장소는 미디어 서비스 tooshow 워크플로 관련된 tooingesting 직접 blob 저장소에서 인코딩, 콘텐츠를 쓸 롤백할 tooblob 저장소 콘텐츠를 사용 하는 예제를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="5786f-109">또한 toomonitor Webhook 및 Azure 큐를 통해 알림을 작업 하는 방법의 예도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="5786f-110">Hello에 hello 예제에 따라 함수를 개발 [미디어 서비스 Azure 함수](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="5786f-111">toodeploy hello 함수, 키를 눌러 hello **tooAzure 배포** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5786f-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5786f-112">Prerequisites</span></span>

- <span data-ttu-id="5786f-113">첫 번째 함수를 만들기 전에 toohave 활성 Azure 계정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="5786f-114">Azure 계정이 아직 없는 경우 [체험 계정을 사용](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="5786f-115">설명 된 대로 AMS 계정을 Azure 미디어 서비스 (AMS) 계정에 작업을 수행 하거나 미디어 서비스에서 보낸 tooevents 수신 대기 하는 toocreate Azure 함수를 사용 하도록 하려는 경우 만든 [여기](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="5786f-116">이해 [어떻게 toouse Azure 함수](../azure-functions/functions-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="5786f-117">또한 다음을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-117">Also, review:</span></span>
    - [<span data-ttu-id="5786f-118">Azure Functions HTTP 및 웹후크 바인딩</span><span class="sxs-lookup"><span data-stu-id="5786f-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="5786f-119">어떻게 tooconfigure Azure 함수 앱 설정</span><span class="sxs-lookup"><span data-stu-id="5786f-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="5786f-120">고려 사항</span><span class="sxs-lookup"><span data-stu-id="5786f-120">Considerations</span></span>

-  <span data-ttu-id="5786f-121">Hello 소비 계획으로 실행 하는 azure 함수를 제한 하는 5 분 시간 초과 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="5786f-122">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5786f-122">Create a function app</span></span>

1. <span data-ttu-id="5786f-123">Toohello 이동 [Azure 포털](http://portal.azure.com) 및 Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="5786f-124">[여기](../azure-functions/functions-create-function-app-portal.md)에 설명한 대로 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="5786f-125">Hello에 지정 하는 저장소 계정을 **StorageConnection** hello 환경 변수 여야 합니다 (hello 다음 단계 참조) 응용 프로그램으로 같은 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="5786f-126">함수 앱 구성 설정</span><span class="sxs-lookup"><span data-stu-id="5786f-126">Configure function app settings</span></span>

<span data-ttu-id="5786f-127">미디어 서비스 기능을 개발, 때는 함수 전체에서 사용할 수 있는 편리한 tooadd 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="5786f-128">tooconfigure 앱 설정 hello 앱 설정 구성 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="5786f-129">자세한 내용은 참조 [어떻게 tooconfigure Azure 함수 앱 설정](../azure-functions/functions-how-to-use-azure-function-app-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="5786f-130">예:</span><span class="sxs-lookup"><span data-stu-id="5786f-130">For example:</span></span>

![설정](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="5786f-132">앱 설정에서 환경 변수를 다음 hello 있다고 가정 하 고이 문서에 정의 된 hello 함수:</span><span class="sxs-lookup"><span data-stu-id="5786f-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="5786f-133">**AMSAccount**: *AMS 계정 이름*(예: testams)</span><span class="sxs-lookup"><span data-stu-id="5786f-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="5786f-134">**AMSKey**: *AMS 계정 키*(예: IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="5786f-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="5786f-135">**MediaServicesStorageAccountName**: *저장소 계정 이름*(예: testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="5786f-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="5786f-136">**MediaServicesStorageAccountKey**: *저장소 계정 키*(예: xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX = =)</span><span class="sxs-lookup"><span data-stu-id="5786f-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="5786f-137">**StorageConnection**: *저장소 연결*(예: DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX = = =)</span><span class="sxs-lookup"><span data-stu-id="5786f-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="5786f-138">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="5786f-138">Create a function</span></span>

<span data-ttu-id="5786f-139">함수 앱을 배포하면 **App Services** Azure Functions에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="5786f-140">함수 앱을 선택하고 **새 함수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="5786f-141">Hello 선택 **C#** 언어 및 **데이터 처리** 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="5786f-142">**BlobTrigger** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="5786f-143">이 함수를 hello로 blob은 업로드 될 때마다 트리거되어 **입력** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="5786f-144">hello **입력** hello에 이름이 지정 된 **경로**, hello 다음 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![업로드](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="5786f-146">선택 하 고 나면 **BlobTrigger**, 몇 가지 더 많은 컨트롤이 hello 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![업로드](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="5786f-148">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="5786f-149">파일</span><span class="sxs-lookup"><span data-stu-id="5786f-149">Files</span></span>

<span data-ttu-id="5786f-150">Azure Function은 이 섹션에 설명된 코드 파일 및 기타 파일과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="5786f-151">기본적으로 함수는 **function.json** 및 **run.csx**(C#) 파일과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="5786f-152">Tooadd 해야는 **project.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="5786f-153">hello이이 단원의 나머지 부분에서는 이러한 파일에 대 한 hello 정의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-153">hello rest of this section shows hello definitions for these files.</span></span>

![업로드](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="5786f-155">function.json</span><span class="sxs-lookup"><span data-stu-id="5786f-155">function.json</span></span>

<span data-ttu-id="5786f-156">hello function.json 파일 hello 함수 바인딩 및 기타 구성 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="5786f-157">hello 런타임은이 파일 toodetermine hello 이벤트 toomonitor 및 toopass 데이터를 한 반환 데이터에서 실행이 작동 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="5786f-158">자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](../azure-functions/functions-reference.md#function-code)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5786f-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="5786f-159">집합 hello **비활성화** 속성 너무**true** tooprevent hello 함수 실행 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="5786f-160">**function.json** 파일의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="5786f-161">project.json</span><span class="sxs-lookup"><span data-stu-id="5786f-161">project.json</span></span>

<span data-ttu-id="5786f-162">hello project.json 파일 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="5786f-163">예로 **project.json** hello 필요한.NET Azure 미디어 서비스를 포함 하는 파일에서 Nuget 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="5786f-164">hello 버전 번호가 변경 된다는 최신 업데이트로 toohello 패키지 hello 가장 최신 버전을 확인 해야 하므로 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="5786f-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="5786f-165">run.csx</span></span>

<span data-ttu-id="5786f-166">함수에 대 한 hello C# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="5786f-167">hello 함수 아래에 정의 된 모니터가 라는 저장소 계정 컨테이너 **입력** (즉 hello 경로에 지정 된 항목) 새 MP4 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="5786f-168">Hello 저장소 컨테이너에 파일은 삭제 되 면 hello blob 트리거 hello 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="5786f-169">이 섹션에 정의 된 hello 예제</span><span class="sxs-lookup"><span data-stu-id="5786f-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="5786f-170">tooingest를 미디어 서비스 자산 (AMS 자산으로 blob를 복사) 하 여 계정 하는 방법 및</span><span class="sxs-lookup"><span data-stu-id="5786f-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="5786f-171">어떻게 toosubmit 미디어 인코더 표준의 "적응 스트리밍"를 사용 하는 인코딩 작업을 미리 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="5786f-172">Hello 실제 시나리오에서는 가장 가능성이 높은 tootrack 작업 진행 상황을 다음 인코딩된 자산을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="5786f-173">자세한 내용은 참조 [사용 하 여 Azure Webhook toomonitor 미디어 서비스 작업 알림](media-services-dotnet-check-job-progress-with-webhooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="5786f-174">더 많은 예제는 [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5786f-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="5786f-175">함수를 정의했으면 **저장 및 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
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

        // Get hello destination asset container reference
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

        // Get hold of hello destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="5786f-176">함수 테스트</span><span class="sxs-lookup"><span data-stu-id="5786f-176">Test your function</span></span>

<span data-ttu-id="5786f-177">tootest tooupload hello로 MP4 파일 필요한 함수를 **입력** hello 연결 문자열에 지정 하는 hello 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="5786f-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5786f-178">Next step</span></span>

<span data-ttu-id="5786f-179">이 시점에서 미디어 서비스 응용 프로그램을 개발 하는 준비 toostart 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="5786f-180">자세한 내용과 전체 샘플/의 Azure 기능 및 논리 앱을 사용 하 여 Azure 미디어 서비스 toocreate 사용자 지정 콘텐츠 제작 워크플로 사용 하 여 솔루션에 대 한 참조 hello [GitHub에 미디어 서비스.NET 함수 통합 샘플](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="5786f-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="5786f-181">참고: [사용 하 여 Azure Webhook toomonitor 미디어 서비스.NET을 사용 하 여 알림 작업](media-services-dotnet-check-job-progress-with-webhooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5786f-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="5786f-182">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="5786f-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5786f-183">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5786f-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

