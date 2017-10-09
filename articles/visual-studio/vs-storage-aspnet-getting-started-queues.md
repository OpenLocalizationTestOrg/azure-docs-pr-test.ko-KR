---
title: "Visual Studio 연결 된 서비스 (ASP.NET) 및 Azure 큐 저장소 시작: aaaGet | Microsoft Docs"
description: "Visual Studio에서 ASP.NET 프로젝트를 Azure 큐 저장소를 사용 하 여 Visual Studio 연결 된 서비스를 사용 하 여 tooa 저장소 계정을 연결한 후 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="6a29c-103">Azure Queue Storage 및 Visual Studio 연결 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6a29c-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6a29c-104">개요</span><span class="sxs-lookup"><span data-stu-id="6a29c-104">Overview</span></span>

<span data-ttu-id="6a29c-105">Azure Queue Storage는 응용 프로그램 구성 요소 간에 클라우드 메시징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="6a29c-106">규모를 고려하여 응용 프로그램을 디자인할 때는 응용 프로그램 구성 요소를 개별적으로 확장할 수 있도록 각 구성 요소를 분리하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="6a29c-107">큐 저장소는 클라우드 hello hello 데스크톱, 온-프레미스 서버 또는 모바일 장치에서에서 실행 되는 여부를 비동기 메시징 응용 프로그램 구성 요소 간의 통신을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="6a29c-108">큐 저장소는 또한 비동기 작업 관리와 프로세스 워크플로 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="6a29c-109">이 자습서에서는 Azure 큐 저장소 엔터티를 사용 하 여 몇 가지 일반적인 시나리오에 대 한 ASP.NET toowrite 코드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="6a29c-110">이러한 시나리오는 Azure 큐 작성, 큐 메시지 추가, 수정, 읽기 및 제거와 같은 일반적인 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="6a29c-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6a29c-111">Prerequisites</span></span>

* [<span data-ttu-id="6a29c-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a29c-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="6a29c-113">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="6a29c-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="6a29c-114">MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="6a29c-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="6a29c-115">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **컨트롤러**, hello 상황에 맞는 메뉴에서 **추가-컨트롤러 >**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![컨트롤러 tooan ASP.NET MVC 응용 프로그램 추가](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="6a29c-117">Hello에 **추가 스 캐 폴드** 대화 상자에서 **MVC 5 컨트롤러-비어 있지**, 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="6a29c-119">Hello에 **컨트롤러 추가** 대화 상자에서 이름 hello 컨트롤러 *QueuesController*를 선택 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Hello MVC 컨트롤러 이름](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="6a29c-121">Hello 다음 추가 *를 사용 하 여* 지시문 toohello `QueuesController.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="6a29c-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="6a29c-122">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="6a29c-122">Create a queue</span></span>

<span data-ttu-id="6a29c-123">hello 아래 단계에 설명 방법을 toocreate 큐:</span><span class="sxs-lookup"><span data-stu-id="6a29c-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6a29c-124">이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6a29c-125">열기 hello `QueuesController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="6a29c-126">**ActionResult**를 반환하는 **CreateQueue**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6a29c-127">Hello 내 **CreateQueue** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a29c-128">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="6a29c-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6a29c-129">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="6a29c-130">가져오기는 **CloudQueue** 참조 toohello 원하는 큐 이름을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="6a29c-131">hello **CloudQueueClient.GetQueueReference** 메서드 큐 저장소에 대 한 요청을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="6a29c-132">hello 큐가 여부 hello 참조가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6a29c-133">Hello 호출 **CloudQueue.CreateIfNotExists** 메서드 toocreate hello 큐 아직 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="6a29c-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="6a29c-134">hello **CloudQueue.CreateIfNotExists** 메서드 반환 **true** hello 대기열 존재 하지 않는 하 고 성공적으로 생성 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="6a29c-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="6a29c-135">그렇지 않으면 **false**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="6a29c-136">업데이트 hello **ViewBag** hello 큐의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="6a29c-137">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="6a29c-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6a29c-138">Hello에 **뷰 추가** 대화 상자에서 입력 **CreateQueue** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6a29c-139">열기 `CreateQueue.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="6a29c-140">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6a29c-141">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6a29c-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="6a29c-142">Hello 응용 프로그램을 실행 하 고 선택 **만들기 큐** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="6a29c-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![큐 만들기](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="6a29c-144">앞에서 설명한 대로 hello **CloudQueue.CreateIfNotExists** 메서드 반환 **true** hello 큐 존재 하지 않는 있고 만들어지는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="6a29c-145">따라서 hello 큐가 있는 경우 hello 앱을 실행 하면 hello 메서드는 반환 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="6a29c-146">toorun hello 앱 여러 번 삭제 해야 hello 큐 hello 응용 프로그램을 다시 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="6a29c-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="6a29c-147">Hello 통해 hello 큐 삭제를 수행할 수 있습니다 **CloudQueue.Delete** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6a29c-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="6a29c-148">Hello를 사용 하 여 hello 큐를 삭제할 수도 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 hello [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="6a29c-149">메시지 tooa 큐 추가</span><span class="sxs-lookup"><span data-stu-id="6a29c-149">Add a message tooa queue</span></span>

<span data-ttu-id="6a29c-150">한 후 [큐를 만든](#create-a-queue), toothat 큐 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="6a29c-151">이 섹션에서는 메시지 tooa 큐를 추가 하는 과정에서는 *큐 테스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6a29c-152">이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6a29c-153">열기 hello `QueuesController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6a29c-154">**ActionResult**를 반환하는 **AddMessage**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6a29c-155">Hello 내 **AddMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a29c-156">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="6a29c-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6a29c-157">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6a29c-158">가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6a29c-159">Hello 만들기 **CloudQueueMessage** tooadd toohello 큐 hello 메시지를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="6a29c-160">**CloudQueueMessage** 개체는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="6a29c-161">Hello 호출 **CloudQueue.AddMessage** 메서드 tooadd hello 방식과 toohello 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="6a29c-162">만들고 몇 가지 설정 **ViewBag** hello 보기에 표시 하기 위한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="6a29c-163">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="6a29c-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6a29c-164">Hello에 **뷰 추가** 대화 상자에서 입력 **AddMessage** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6a29c-165">열기 `AddMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="6a29c-166">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6a29c-167">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6a29c-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="6a29c-168">Hello 응용 프로그램을 실행 하 고 선택 **추가 메시지** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="6a29c-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![메시지 추가](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="6a29c-170">두 개의 섹션-hello [제거 하지 않고 큐에서 메시지를 읽으려면](#read-a-message-from-a-queue-without-removing-it) 및 [읽기 및 큐에서 메시지 제거](#read-and-remove-a-message-from-a-queue) -tooread 큐에서 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="6a29c-171">메시지를 제거하지 않고 큐에서 읽기</span><span class="sxs-lookup"><span data-stu-id="6a29c-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="6a29c-172">이 섹션에서는 어떻게 toopeek 큐에 대기 중인 메시지 (제거 하지 않고 첫 번째 메시지 읽기 hello).</span><span class="sxs-lookup"><span data-stu-id="6a29c-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="6a29c-173">이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6a29c-174">열기 hello `QueuesController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6a29c-175">**ActionResult**를 반환하는 **PeekMessage**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6a29c-176">Hello 내 **PeekMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a29c-177">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="6a29c-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6a29c-178">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6a29c-179">가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6a29c-180">Hello 호출 **CloudQueue.PeekMessage** 메서드 tooread hello hello 큐에서 제거 하지 않고 hello 큐의 첫 번째 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="6a29c-181">업데이트 hello **ViewBag** 두 값이 포함: hello 큐 이름 및 hello 메시지를 읽었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="6a29c-182">hello **CloudQueueMessage** 개체 hello 개체의 값을 가져오기 위한 두 가지 속성을 노출: **CloudQueueMessage.AsBytes** 및 **CloudQueueMessage.AsString**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="6a29c-183">**AsString**(이 예제에서 사용)은 문자열을 반환하는 반면 **AsBytes**는 바이트 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="6a29c-184">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="6a29c-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6a29c-185">Hello에 **뷰 추가** 대화 상자에서 입력 **PeekMessage** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6a29c-186">열기 `PeekMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="6a29c-187">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6a29c-188">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6a29c-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="6a29c-189">Hello 응용 프로그램을 실행 하 고 선택 **Peek 메시지** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="6a29c-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![메시지 보기](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="6a29c-191">큐에서 메시지 읽기 및 제거</span><span class="sxs-lookup"><span data-stu-id="6a29c-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="6a29c-192">이 섹션에서는 설명 어떻게 tooread 큐에서 메시지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="6a29c-193">이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6a29c-194">열기 hello `QueuesController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6a29c-195">**ActionResult**를 반환하는 **ReadMessage**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6a29c-196">Hello 내 **ReadMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a29c-197">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="6a29c-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6a29c-198">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6a29c-199">가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6a29c-200">Hello 호출 **CloudQueue.GetMessage** 메서드 tooread hello hello 큐의 첫 번째 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="6a29c-201">hello **CloudQueue.GetMessage** 메서드 hello 메시지 보이지 않는 기본적으로 30 초 tooany에 대 한 다른 코드 수정 하거나 사용자 처리 하는 동안 hello 메시지를 삭제할 수 있도록 메시지를 읽고 다른 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="6a29c-202">toochange hello 양의 시간 hello 메시지 보이지 않으면, hello 수정 **visibilityTimeout** toohello 전달 되는 매개 변수 **CloudQueue.GetMessage** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6a29c-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="6a29c-203">Hello 호출 **CloudQueueMessage.Delete** hello 큐에서 메서드 toodelete hello 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="6a29c-204">업데이트 hello **ViewBag** hello로 메시지를 삭제 하 고 hello hello 큐의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="6a29c-205">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="6a29c-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6a29c-206">Hello에 **뷰 추가** 대화 상자에서 입력 **ReadMessage** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6a29c-207">열기 `ReadMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="6a29c-208">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6a29c-209">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6a29c-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="6a29c-210">Hello 응용 프로그램을 실행 하 고 선택 **읽기/삭제 메시지** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="6a29c-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![메시지 읽기 및 삭제](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="6a29c-212">Hello 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a29c-212">Get hello queue length</span></span>

<span data-ttu-id="6a29c-213">이 섹션에서는 tooget 큐 길이 (메시지 수) hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6a29c-214">이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6a29c-215">열기 hello `QueuesController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6a29c-216">**ActionResult**를 반환하는 **GetQueueLength**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6a29c-217">Hello 내 **ReadMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a29c-218">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="6a29c-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6a29c-219">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6a29c-220">가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6a29c-221">Hello 호출 **CloudQueue.FetchAttributes** 메서드 tooretrieve hello 큐의 특성 (길이 포함).</span><span class="sxs-lookup"><span data-stu-id="6a29c-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="6a29c-222">액세스 hello **CloudQueue.ApproximateMessageCount** 속성 tooget hello 큐 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="6a29c-223">업데이트 hello **ViewBag** hello 큐 길이 hello 이름을 사용해 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="6a29c-224">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="6a29c-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6a29c-225">Hello에 **뷰 추가** 대화 상자에서 입력 **GetQueueLength** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6a29c-226">열기 `GetQueueLengthMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="6a29c-227">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6a29c-228">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6a29c-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="6a29c-229">Hello 응용 프로그램을 실행 하 고 선택 **큐 길이 가져오기** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="6a29c-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![큐 길이 가져오기](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="6a29c-231">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="6a29c-231">Delete a queue</span></span>
<span data-ttu-id="6a29c-232">이 섹션에서는 어떻게 toodelete 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6a29c-233">이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6a29c-234">열기 hello `QueuesController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="6a29c-235">**ActionResult**를 반환하는 **DeleteQueue**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="6a29c-236">Hello 내 **DeleteQueue** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6a29c-237">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="6a29c-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="6a29c-238">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="6a29c-239">가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="6a29c-240">Hello 호출 **CloudQueue.Delete** hello가 나타내는 메서드 toodelete hello 큐 **CloudQueue** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="6a29c-241">업데이트 hello **ViewBag** hello 큐 길이 hello 이름을 사용해 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="6a29c-242">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="6a29c-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6a29c-243">Hello에 **뷰 추가** 대화 상자에서 입력 **DeleteQueue** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="6a29c-244">열기 `DeleteQueue.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="6a29c-245">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6a29c-246">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6a29c-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="6a29c-247">Hello 응용 프로그램을 실행 하 고 선택 **큐 길이 가져오기** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="6a29c-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![큐 삭제](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="6a29c-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a29c-249">Next steps</span></span>
<span data-ttu-id="6a29c-250">Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6a29c-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="6a29c-251">Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6a29c-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="6a29c-252">Azure 테이블 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6a29c-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
