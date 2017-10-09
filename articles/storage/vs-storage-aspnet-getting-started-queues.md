---
title: "Visual Studio 연결 된 서비스 (ASP.NET) 및 Azure 큐 저장소 시작: aaaGet | Microsoft Docs"
description: "Visual Studio에서 ASP.NET 프로젝트를 Azure 큐 저장소를 사용 하 여 Visual Studio 연결 된 서비스를 사용 하 여 tooa 저장소 계정을 연결한 후 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Azure Queue Storage 및 Visual Studio 연결 서비스 시작(ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요

Azure Queue Storage는 응용 프로그램 구성 요소 간에 클라우드 메시징을 제공합니다. 규모를 고려하여 응용 프로그램을 디자인할 때는 응용 프로그램 구성 요소를 개별적으로 확장할 수 있도록 각 구성 요소를 분리하는 경우가 많습니다. 큐 저장소는 클라우드 hello hello 데스크톱, 온-프레미스 서버 또는 모바일 장치에서에서 실행 되는 여부를 비동기 메시징 응용 프로그램 구성 요소 간의 통신을 제공 합니다. 큐 저장소는 또한 비동기 작업 관리와 프로세스 워크플로 작성을 지원합니다.

이 자습서에서는 Azure 큐 저장소 엔터티를 사용 하 여 몇 가지 일반적인 시나리오에 대 한 ASP.NET toowrite 코드 하는 방법을 보여 줍니다. 이러한 시나리오는 Azure 큐 작성, 큐 메시지 추가, 수정, 읽기 및 제거와 같은 일반적인 작업을 포함합니다.

##<a name="prerequisites"></a>필수 조건

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>MVC 컨트롤러 만들기 

1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **컨트롤러**, hello 상황에 맞는 메뉴에서 **추가-컨트롤러 >**합니다.

    ![컨트롤러 tooan ASP.NET MVC 응용 프로그램 추가](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. Hello에 **추가 스 캐 폴드** 대화 상자에서 **MVC 5 컨트롤러-비어 있지**, 선택한 **추가**합니다.

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. Hello에 **컨트롤러 추가** 대화 상자에서 이름 hello 컨트롤러 *QueuesController*를 선택 하 고 **추가**합니다.

    ![Hello MVC 컨트롤러 이름](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Hello 다음 추가 *를 사용 하 여* 지시문 toohello `QueuesController.cs` 파일:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>큐 만들기

hello 아래 단계에 설명 방법을 toocreate 큐:

> [!NOTE]
> 
> 이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `QueuesController.cs` 파일입니다. 

1. **ActionResult**를 반환하는 **CreateQueue**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **CreateQueue** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. 가져오기는 **CloudQueue** 참조 toohello 원하는 큐 이름을 나타내는 개체입니다. hello **CloudQueueClient.GetQueueReference** 메서드 큐 저장소에 대 한 요청을 만들지 않습니다. hello 큐가 여부 hello 참조가 반환 됩니다. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hello 호출 **CloudQueue.CreateIfNotExists** 메서드 toocreate hello 큐 아직 존재 하지 않는 경우. hello **CloudQueue.CreateIfNotExists** 메서드 반환 **true** hello 대기열 존재 하지 않는 하 고 성공적으로 생성 되는 경우. 그렇지 않으면 **false**가 반환됩니다.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. 업데이트 hello **ViewBag** hello 큐의 hello 이름을 사용 합니다.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **CreateQueue** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `CreateQueue.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **만들기 큐** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![큐 만들기](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    앞에서 설명한 대로 hello **CloudQueue.CreateIfNotExists** 메서드 반환 **true** hello 큐 존재 하지 않는 있고 만들어지는 경우에 합니다. 따라서 hello 큐가 있는 경우 hello 앱을 실행 하면 hello 메서드는 반환 **false**합니다. toorun hello 앱 여러 번 삭제 해야 hello 큐 hello 응용 프로그램을 다시 실행 하기 전에. Hello 통해 hello 큐 삭제를 수행할 수 있습니다 **CloudQueue.Delete** 메서드. Hello를 사용 하 여 hello 큐를 삭제할 수도 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 hello [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.  

## <a name="add-a-message-tooa-queue"></a>메시지 tooa 큐 추가

한 후 [큐를 만든](#create-a-queue), toothat 큐 메시지를 추가할 수 있습니다. 이 섹션에서는 메시지 tooa 큐를 추가 하는 과정에서는 *큐 테스트*합니다. 

> [!NOTE]
> 
> 이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `QueuesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **AddMessage**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **AddMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hello 만들기 **CloudQueueMessage** tooadd toohello 큐 hello 메시지를 나타내는 개체입니다. **CloudQueueMessage** 개체는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Hello 호출 **CloudQueue.AddMessage** 메서드 tooadd hello 방식과 toohello 큐입니다.

    ```csharp
    queue.AddMessage(message);
    ```

1. 만들고 몇 가지 설정 **ViewBag** hello 보기에 표시 하기 위한 속성입니다.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **AddMessage** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `AddMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **추가 메시지** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![메시지 추가](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

두 개의 섹션-hello [제거 하지 않고 큐에서 메시지를 읽으려면](#read-a-message-from-a-queue-without-removing-it) 및 [읽기 및 큐에서 메시지 제거](#read-and-remove-a-message-from-a-queue) -tooread 큐에서 메시지 하는 방법을 보여 줍니다.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>메시지를 제거하지 않고 큐에서 읽기

이 섹션에서는 어떻게 toopeek 큐에 대기 중인 메시지 (제거 하지 않고 첫 번째 메시지 읽기 hello).  

> [!NOTE]
> 
> 이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `QueuesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **PeekMessage**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **PeekMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hello 호출 **CloudQueue.PeekMessage** 메서드 tooread hello hello 큐에서 제거 하지 않고 hello 큐의 첫 번째 메시지입니다. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. 업데이트 hello **ViewBag** 두 값이 포함: hello 큐 이름 및 hello 메시지를 읽었습니다. hello **CloudQueueMessage** 개체 hello 개체의 값을 가져오기 위한 두 가지 속성을 노출: **CloudQueueMessage.AsBytes** 및 **CloudQueueMessage.AsString**합니다. **AsString**(이 예제에서 사용)은 문자열을 반환하는 반면 **AsBytes**는 바이트 배열을 반환합니다.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **PeekMessage** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `PeekMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

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

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **Peek 메시지** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![메시지 보기](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>큐에서 메시지 읽기 및 제거

이 섹션에서는 설명 어떻게 tooread 큐에서 메시지를 제거 합니다.   

> [!NOTE]
> 
> 이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `QueuesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **ReadMessage**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **ReadMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hello 호출 **CloudQueue.GetMessage** 메서드 tooread hello hello 큐의 첫 번째 메시지입니다. hello **CloudQueue.GetMessage** 메서드 hello 메시지 보이지 않는 기본적으로 30 초 tooany에 대 한 다른 코드 수정 하거나 사용자 처리 하는 동안 hello 메시지를 삭제할 수 있도록 메시지를 읽고 다른 코드를 만듭니다. toochange hello 양의 시간 hello 메시지 보이지 않으면, hello 수정 **visibilityTimeout** toohello 전달 되는 매개 변수 **CloudQueue.GetMessage** 메서드.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Hello 호출 **CloudQueueMessage.Delete** hello 큐에서 메서드 toodelete hello 메시지입니다.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. 업데이트 hello **ViewBag** hello로 메시지를 삭제 하 고 hello hello 큐의 이름입니다.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **ReadMessage** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `ReadMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

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

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **읽기/삭제 메시지** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![메시지 읽기 및 삭제](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Hello 큐 길이 가져오기

이 섹션에서는 tooget 큐 길이 (메시지 수) hello 하는 방법을 보여 줍니다. 

> [!NOTE]
> 
> 이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `QueuesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **GetQueueLength**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **ReadMessage** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hello 호출 **CloudQueue.FetchAttributes** 메서드 tooretrieve hello 큐의 특성 (길이 포함). 

    ```csharp
    queue.FetchAttributes();
    ```

6. 액세스 hello **CloudQueue.ApproximateMessageCount** 속성 tooget hello 큐 길이입니다.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. 업데이트 hello **ViewBag** hello 큐 길이 hello 이름을 사용해 합니다.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **GetQueueLength** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `GetQueueLengthMessage.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **큐 길이 가져오기** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![큐 길이 가져오기](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>큐 삭제
이 섹션에서는 어떻게 toodelete 큐입니다. 

> [!NOTE]
> 
> 이 섹션에서는 hello 단계를 완료 한 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `QueuesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **DeleteQueue**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **DeleteQueue** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 큐 서비스 클라이언트를 나타내는 **CloudQueueClient** 개체를 나타냅니다.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 가져오기는 **CloudQueueContainer** 참조 toohello 큐를 나타내는 개체입니다. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hello 호출 **CloudQueue.Delete** hello가 나타내는 메서드 toodelete hello 큐 **CloudQueue** 개체입니다.

    ```csharp
    queue.Delete();
    ```

1. 업데이트 hello **ViewBag** hello 큐 길이 hello 이름을 사용해 합니다.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **큐**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **DeleteQueue** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `DeleteQueue.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **큐 길이 가져오기** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![큐 삭제](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>다음 단계
Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.

  * [Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Azure 테이블 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
