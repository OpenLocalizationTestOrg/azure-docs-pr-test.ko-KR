---
title: "Azure Queue Storage 및 Visual Studio 연결 서비스 시작(ASP.NET) | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 저장소 계정에 연결한 후 Visual Studio ASP.NET 프로젝트에서 Azure Queue Storage 사용을 시작하는 방법입니다."
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
ms.openlocfilehash: 4687e5dfce72583728068c176d86d100313badf6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="b1549-103">Azure Queue Storage 및 Visual Studio 연결 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b1549-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="b1549-104">개요</span><span class="sxs-lookup"><span data-stu-id="b1549-104">Overview</span></span>

<span data-ttu-id="b1549-105">Azure Queue Storage는 응용 프로그램 구성 요소 간에 클라우드 메시징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="b1549-106">규모를 고려하여 응용 프로그램을 디자인할 때는 응용 프로그램 구성 요소를 개별적으로 확장할 수 있도록 각 구성 요소를 분리하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="b1549-107">큐 저장소는 클라우드, 데스크톱, 온-프레미스 서버 또는 모바일 장치에서 실행 중인지와 관계 없이 응용 프로그램 구성 요소 간에 통신을 위한 비동기 메시징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="b1549-108">큐 저장소는 또한 비동기 작업 관리와 프로세스 워크플로 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="b1549-109">이 자습서에서는 Azure Queue Storage 항목을 사용하여 몇 가지 일반적인 시나리오에 대한 ASP.NET 코드를 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="b1549-110">이러한 시나리오는 Azure 큐 작성, 큐 메시지 추가, 수정, 읽기 및 제거와 같은 일반적인 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="b1549-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b1549-111">Prerequisites</span></span>

* [<span data-ttu-id="b1549-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b1549-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="b1549-113">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="b1549-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="b1549-114">MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="b1549-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="b1549-115">**솔루션 탐색기**에서 **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->컨트롤러**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![ASP.NET MVC 앱에 컨트롤러 추가](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="b1549-117">**스캐폴드 추가** 대화 상자에서 **MVC 5 컨트롤러 - 비어 있음**을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="b1549-119">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 *QueuesController*로 설정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![MVC 컨트롤러 이름 지정](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="b1549-121">다음 *using* 지시문을 `QueuesController.cs` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="b1549-122">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="b1549-122">Create a queue</span></span>

<span data-ttu-id="b1549-123">다음 단계에서는 큐를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b1549-124">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment) 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b1549-125">`QueuesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="b1549-126">**ActionResult**를 반환하는 **CreateQueue**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b1549-127">**CreateQueue** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b1549-128">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="b1549-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b1549-129">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="b1549-130">원하는 큐 이름에 대한 참조를 나타내는 **CloudQueue** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="b1549-131">**CloudQueueClient.GetQueueReference** 메서드는 큐 저장소에 대한 요청을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="b1549-132">큐가 있는지 여부에 관계없이 참조가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b1549-133">큐가 아직 없으면 **CloudQueue.CreateIfNotExists** 메서드를 호출하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="b1549-134">큐가 없는 경우 큐가 성공적으로 생성되면 **CloudQueue.CreateIfNotExists** 메서드는 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="b1549-135">그렇지 않으면 **false**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="b1549-136">**ViewBag**을 큐의 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="b1549-137">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **큐**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b1549-138">**보기 추가** 대화 상자에서 보기 이름으로 **CreateQueue**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="b1549-139">`CreateQueue.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="b1549-140">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b1549-141">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="b1549-142">응용 프로그램을 실행하고 **큐 만들기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![큐 만들기](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="b1549-144">앞에서 언급했듯이 큐가 없고 만들어진 경우에만 **CloudQueue.CreateIfNotExists** 메서드에서 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="b1549-145">따라서 큐가 있을 때 앱을 실행하면 메서드에서 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="b1549-146">앱을 여러 번 실행하려면 앱을 다시 실행하기 전에 큐를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="b1549-147">**CloudQueue.Delete** 메서드를 통해 큐 삭제를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="b1549-148">또한 [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 [Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 큐를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="b1549-149">큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="b1549-149">Add a message to a queue</span></span>

<span data-ttu-id="b1549-150">[큐를 만든](#create-a-queue) 후 해당 큐에 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="b1549-151">이 섹션에서는 큐 *test-queue*에 메시지를 추가하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b1549-152">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment) 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b1549-153">`QueuesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b1549-154">**ActionResult**를 반환하는 **AddMessage**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b1549-155">**AddMessage** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b1549-156">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="b1549-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b1549-157">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b1549-158">큐에 대한 참조를 나타내는 **CloudQueueContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b1549-159">큐에 추가할 메시지를 나타내는 **CloudQueueMessage** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="b1549-160">**CloudQueueMessage** 개체는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="b1549-161">**CloudQueue.AddMessage** 메서드를 호출하여 큐에 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="b1549-162">보기에 표시하기 위한 몇 가지 **ViewBag** 속성을 만들고 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="b1549-163">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **큐**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b1549-164">**보기 추가** 대화 상자에서 보기 이름으로 **AddMessage**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="b1549-165">`AddMessage.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="b1549-166">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b1549-167">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="b1549-168">응용 프로그램을 실행하고 **메시지 추가**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![메시지 추가](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="b1549-170">두 개의 섹션 - [메시지를 제거하지 않고 큐에서 읽기](#read-a-message-from-a-queue-without-removing-it) 및 [큐에서 메시지 읽기 및 제거](#read-and-remove-a-message-from-a-queue) - 큐에서 메시지를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="b1549-171">메시지를 제거하지 않고 큐에서 읽기</span><span class="sxs-lookup"><span data-stu-id="b1549-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="b1549-172">이 섹션에서는 대기 중인 메시지를 미리 확인하는 방법을 설명합니다(첫 번째 메시지를 제거하지 않고 읽음).</span><span class="sxs-lookup"><span data-stu-id="b1549-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="b1549-173">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment) 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b1549-174">`QueuesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b1549-175">**ActionResult**를 반환하는 **PeekMessage**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b1549-176">**PeekMessage** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b1549-177">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="b1549-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b1549-178">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b1549-179">큐에 대한 참조를 나타내는 **CloudQueueContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b1549-180">**CloudQueue.PeekMessage** 메서드를 호출하여 큐에서 메시지를 제거하지 않고도 큐의 첫 번째 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="b1549-181">읽힌 큐 이름 및 메시지의 두 값으로 **ViewBag**을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="b1549-182">**CloudQueueMessage** 개체는 개체의 값을 가져오기 위해 두 개의 속성(**CloudQueueMessage.AsBytes** 및 **CloudQueueMessage.AsString**)을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="b1549-183">**AsString**(이 예제에서 사용)은 문자열을 반환하는 반면 **AsBytes**는 바이트 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="b1549-184">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **큐**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b1549-185">**보기 추가** 대화 상자에서 보기 이름으로 **PeekMessage**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="b1549-186">`PeekMessage.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="b1549-187">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b1549-188">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="b1549-189">응용 프로그램을 실행하고 **메시지 보기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![메시지 보기](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="b1549-191">큐에서 메시지 읽기 및 제거</span><span class="sxs-lookup"><span data-stu-id="b1549-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="b1549-192">이 섹션에서는 큐에서 메시지를 읽고 제거하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="b1549-193">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment) 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b1549-194">`QueuesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b1549-195">**ActionResult**를 반환하는 **ReadMessage**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b1549-196">**ReadMessage** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b1549-197">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="b1549-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b1549-198">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b1549-199">큐에 대한 참조를 나타내는 **CloudQueueContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b1549-200">**CloudQueue.GetMessage** 메서드를 호출하여 큐의 첫 번째 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="b1549-201">**CloudQueue.GetMessage** 메서드는 메시지를 읽는 다른 코드에 해당 메시지가 30초(기본값) 동안 보이지 않도록 하여 사용자가 메시지를 처리하는 동안 다른 코드가 메시지를 수정하거나 삭제할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="b1549-202">메시지가 보이지 않는 기간을 변경하려면 **CloudQueue.GetMessage** 메서드에 전달되는 **visibilityTimeout** 매개 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="b1549-203">**CloudQueueMessage.Delete** 메서드를 호출하여 큐에서 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="b1549-204">**ViewBag**을 삭제된 메시지로 업데이트하고 큐의 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="b1549-205">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **큐**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b1549-206">**보기 추가** 대화 상자에서 보기 이름으로 **ReadMessage**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="b1549-207">`ReadMessage.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="b1549-208">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b1549-209">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="b1549-210">응용 프로그램을 실행하고 **메시지 읽기/삭제**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![메시지 읽기 및 삭제](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="b1549-212">큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="b1549-212">Get the queue length</span></span>

<span data-ttu-id="b1549-213">이 섹션에서는 큐 길이(메시지 수)를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b1549-214">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment) 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b1549-215">`QueuesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b1549-216">**ActionResult**를 반환하는 **GetQueueLength**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b1549-217">**ReadMessage** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b1549-218">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="b1549-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b1549-219">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b1549-220">큐에 대한 참조를 나타내는 **CloudQueueContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b1549-221">**CloudQueue.FetchAttributes** 메서드를 호출하여 큐의 특성(길이 포함)을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="b1549-222">**CloudQueue.ApproximateMessageCount** 속성에 액세스하여 큐의 길이를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="b1549-223">**ViewBag**을 큐의 이름으로 업데이트하고 해당 길이를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="b1549-224">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **큐**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b1549-225">**보기 추가** 대화 상자에서 보기 이름으로 **GetQueueLength**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="b1549-226">`GetQueueLengthMessage.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="b1549-227">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b1549-228">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="b1549-229">응용 프로그램을 실행하고 **큐 길이 가져오기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![큐 길이 가져오기](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="b1549-231">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="b1549-231">Delete a queue</span></span>
<span data-ttu-id="b1549-232">이 섹션에서는 큐를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b1549-233">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment) 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b1549-234">`QueuesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b1549-235">**ActionResult**를 반환하는 **DeleteQueue**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b1549-236">**DeleteQueue** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b1549-237">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="b1549-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b1549-238">큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b1549-239">큐에 대한 참조를 나타내는 **CloudQueueContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b1549-240">**CloudQueue.Delete** 메서드를 호출하여 **CloudQueue** 개체로 나타내는 큐를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="b1549-241">**ViewBag**을 큐의 이름으로 업데이트하고 해당 길이를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="b1549-242">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **큐**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b1549-243">**보기 추가** 대화 상자에서 보기 이름으로 **DeleteQueue**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="b1549-244">`DeleteQueue.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="b1549-245">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b1549-246">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="b1549-247">응용 프로그램을 실행하고 **큐 길이 가져오기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1549-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![큐 삭제](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="b1549-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1549-249">Next steps</span></span>
<span data-ttu-id="b1549-250">Azure에 데이터를 저장하기 위한 추가 옵션에 대한 자세한 내용은 추가 기능 가이드를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b1549-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="b1549-251">Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b1549-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="b1549-252">Azure 테이블 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b1549-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
