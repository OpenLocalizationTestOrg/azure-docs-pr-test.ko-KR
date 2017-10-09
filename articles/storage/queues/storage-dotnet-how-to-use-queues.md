---
title: ".NET을 사용 하 여 Azure 큐 저장소 시작 aaaGet | Microsoft Docs"
description: "Azure 큐는 응용 프로그램 구성 요소 간에 안정적인 비동기 메시징을 제공합니다. 클라우드 하지 메시징 사용 하면 응용 프로그램 구성 요소 tooscale 독립적으로 합니다."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>.NET을 사용하여 Azure 큐 저장소 시작
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>개요
Azure 큐 저장소는 응용 프로그램 구성 요소 간에 클라우드 메시징을 제공합니다. 규모를 고려하여 응용 프로그램을 디자인할 때는 응용 프로그램 구성 요소를 개별적으로 확장할 수 있도록 각 구성 요소를 분리하는 경우가 많습니다. 큐 저장소는 클라우드 hello hello 데스크톱, 온-프레미스 서버 또는 모바일 장치에서에서 실행 되는 여부를 비동기 메시징 응용 프로그램 구성 요소 간의 통신을 제공 합니다. 큐 저장소는 또한 비동기 작업 관리와 프로세스 워크플로 작성을 지원합니다.

### <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서에서는 Azure 큐 저장소를 사용 하 여 몇 가지 일반적인 시나리오에 대 한.NET toowrite 코드 하는 방법을 보여 줍니다. 여기서 다루는 시나리오에는 큐 만들기 및 삭제, 큐 메시지 추가, 읽기 및 삭제가 포함됩니다.

**예상 시간 toocomplete:** 45 분

**필수 구성 요소**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [.NET용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [.NET용 Azure 구성 관리자](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure 저장소 계정](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>지시문을 사용하여 추가
Hello 다음 추가 `using` 지시문 toohello 맨 hello `Program.cs` 파일:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Hello 연결 문자열을 구문 분석
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Hello 큐 서비스 클라이언트 만들기
hello **CloudQueueClient** 클래스를 사용 하면 있습니다 tooretrieve 큐 큐 저장소에 저장 합니다. 한 가지 방법은 toocreate hello 서비스 클라이언트는 다음과 같습니다.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
이제 준비 toowrite 코드에서 데이터를 읽고 tooQueue 저장소 데이터를 기록 하는 합니다.

## <a name="create-a-queue"></a>큐 만들기
이 예에서는 어떻게 toocreate 아직 없는 경우 큐:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>큐에 메시지 삽입
tooinsert를 기존 큐에 메시지를 먼저 새로 만들려면 **CloudQueueMessage**합니다. 그런 다음 호출 하는 hello **AddMessage** 메서드. **CloudQueueMessage**는 문자열(UTF-8 형식) 또는 **바이트** 배열에서 만들 수 있습니다. 코드 (존재 하지 않는) 하는 경우 큐를 만듦 및 삽입 hello 메시지 'Hello World' 다음과 같습니다.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>Hello 다음 메시지 피킹
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **PeekMessage** 메서드.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>대기 중인된 메시지의 hello 내용을 변경합니다
메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다. 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello 작업 작업의 상태를 사용할 수 있습니다. 코드 다음 hello hello 큐 메시지를 새 내용으로 업데이트 하 고 집합 hello 가시성 제한 시간 tooextend 다른 60 초입니다. 이 hello 메시지와 관련 된 작업의 hello 상태를 저장 하 고 hello 클라이언트 hello 메시지에서 작업 하는 다른 분 toocontinue를 제공 합니다. 부터 hello toohardware 또는 소프트웨어 오류로 인해 실패 하면 처리 단계를 통해 toostart 필요 없이 큐의 메시지에이 기술을 tootrack multi-step 워크플로 사용할 수 있습니다. 일반적으로는 다시 시도 횟수를 보관할 때 하 고 메시지를 다시 시도 하는 경우 hello 이상  *n*  시간,는 삭제 합니다. 이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>Hello 다음 메시지 큐에서 제거
다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다. 호출 하는 경우 **GetMessage**, 큐에 있는 hello 다음 메시지를 가져옵니다. 반환 된 메시지 **GetMessage** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. 기본적으로, 이 메시지는 30초간 표시되지 않습니다. toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **DeleteMessage**합니다. 이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다. 코드 호출 **DeleteMessage** 직후 hello 메시지를 처리 합니다.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>일반적인 큐 저장소 API와 함께 Async-Await 패턴 사용
이 예에서는 일반 큐 저장소 Api Async Await toouse hello 패턴 하는 방법을 보여 줍니다. hello 샘플 hello에 표시 된 대로 각 메서드를 제공 하는 hello hello 비동기 버전을 호출 *비동기* 각 방법의 접미사입니다. 비동기 메서드를 사용 하면 비동기 hello-await 패턴 hello 호출이 완료 될 때까지 로컬 실행을 일시 중단 합니다. 이 동작 hello 현재 스레드 toodo 성능 병목 현상을 방지 하 고 있는 다른 작업을 통해 응용 프로그램의 전체적인 응답성 hello 합니다. 사용 하 여 대 한 자세한 내용은 hello.net에서 Await 비동기 패턴에 대 한 참조 [Async 및 Await (C# 및 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>큐에서 메시지를 제거하는 추가 옵션 활용
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.
첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다. 둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다. hello 다음 코드 예제에서는 **GetMessages** 메서드 tooget 20 메시지 한 번 호출에서 합니다. 그런 다음에 **foreach** 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다. 5 분 해당 hello 참고 hello에서 모든 메시지에 대 한 시작 시간이, 하므로 5 분 이후 경과한 hello 호출 너무 나면**GetMessages**, 모든 메시지는 삭제 되지 않았으므로 다시 표시 됩니다.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>Hello 큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. **FetchAttributes** 메서드 hello 메시지 수를 포함 하 여 hello 큐 특성을 검색 하기 위해 hello 큐 서비스를 요청 합니다. hello **ApproximateMessageCount** 속성에서 검색 하는 hello 마지막 값을 반환 된 **FetchAttributes** hello 큐 서비스를 호출 하지 않고 메서드.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>큐 삭제
toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 된 **삭제** hello 큐 개체에서 메서드.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>다음 단계
큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.

* 사용 가능한 Api에 대 한 자세한 내용은 hello 큐 서비스 참조 설명서를 봅니다.
  * [Storage Client Library for .NET 참조](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [REST API 참조](http://msdn.microsoft.com/library/azure/dd179355)
* Toosimplify hello 코드 작성 방법에 대해 알아봅니다 hello를 사용 하 여 Azure 저장소와 toowork [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md)합니다.
* Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.
  * [.NET을 사용 하 여 Azure 테이블 저장소 시작](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore 구조화 된 데이터입니다.
  * [.NET을 사용 하 여 Azure Blob 저장소 시작](../blobs/storage-dotnet-how-to-use-blobs.md) toostore 구조화 되지 않은 데이터입니다.
  * [.NET (C#)를 사용 하 여 데이터베이스 tooSQL 연결](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore 관계형 데이터입니다.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
