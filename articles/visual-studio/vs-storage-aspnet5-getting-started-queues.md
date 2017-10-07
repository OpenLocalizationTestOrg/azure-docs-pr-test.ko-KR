---
title: "큐 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (ASP.NET Core) | Microsoft Docs"
description: "Visual Studio에서 ASP.NET Core 프로젝트를 Azure 큐 저장소를 사용 하 여 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 90c1ebcb6a2eac6bc4f6b69133bdf3135d359a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Queue Storage 및 Visual Studio 연결 서비스 시작(ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요
이 문서에서는 tooget 시작 hello Visual Studio를 사용 하 여 ASP.NET Core 프로젝트에 Azure 저장소 계정을 참조 하거나 만든 후 Visual Studio에서 Azure 큐 저장소를 사용 하는 방법을 설명 **연결 된 서비스 추가** 대화 상자. hello **연결 된 서비스 추가** 작업 프로젝트에 hello 적절 한 NuGet 패키지 tooaccess Azure 저장소를 설치 하 고 계정에 대 한 hello 저장소 tooyour 프로젝트 구성 파일 hello 연결 문자열을 추가 합니다.

Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다. 단일 큐 메시지 크기가 too64 킬로바이트 (KB)를 가능 하 고 큐 수많은 메시지 저장소 계정의 toohello 총 용량 한계를 포함할 수 있습니다.

시작 tooget, 먼저 toocreate Azure 큐 저장소 계정에 있습니다. 방식을 보여줍니다 toocreate 코드에서 큐입니다. 또한 보여줍니다 tooperform basic 추가, 수정, 읽기, 및 큐의 메시지를 제거 하는 등의 작업을 대기 하는 방법입니다. hello 샘플은 C로 작성 된\# 하 고.NET 용 hello Azure 저장소 클라이언트 라이브러리를 사용 합니다. ASP.NET에 대한 자세한 내용은 [ASP.NET(영문)](http://www.asp.net)을 참조하세요.

**참고:** hello에서 ASP.NET Core tooAzure 저장소 호출을 수행 하는 Api의 일부는 비동기 작업입니다. 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요. 아래 hello 코드는 비동기 프로그래밍 메서드를 사용 하 되 고 가정 합니다.

* 큐를 프로그래밍 방식으로 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](../storage/queues/storage-dotnet-how-to-use-queues.md) 을 참조하세요.
* Azure 저장소에 대한 일반적인 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/) 를 참조하세요.
* Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/) 를 참조하세요.
* ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net) 을 참조하세요.

## <a name="access-queues-in-code"></a>코드에서 큐 액세스
tooinclude hello 다음 필요한 ASP.NET Core 프로젝트에서 tooaccess 큐, Azure 큐 저장소에 액세스 하는 항목 tooany C# 소스 파일.

1. 이러한 hello C# 파일의 hello 위쪽 hello 네임 스페이스 선언을 포함 **를 사용 하 여** 문.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다. 사용 하 여 hello tooget 코드를 다음 저장소 연결 문자열 및 hello Azure 서비스 구성에서 저장소 계정 정보 hello 합니다.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. 가져오기는 **CloudQueueClient** 개체 저장소 계정의 tooreference hello 큐 개체입니다.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. 가져오기는 **CloudQueue** tooreference 특정 큐 개체입니다.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**참고:** hello 다음 샘플에서에서 코드 hello 코드 앞에 위의 hello를 모두 사용 합니다.

### <a name="create-a-queue-in-code"></a>코드에서 큐 만들기
코드에서 Azure 큐 toocreate hello 추가 호출 너무**CreateIfNotExistsAsync**합니다.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>메시지 tooa 큐 추가
tooinsert를 기존 큐에 메시지를 새로 만듭니다. **CloudQueueMessage** 개체가, 다음 호출 hello **AddMessageAsync** 메서드.

**CloudQueueMessage** 개체는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.

'Hello World' hello 메시지를 삽입 하는 예제는 다음과 같습니다.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>큐의 메시지 읽기
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **PeekMessageAsync** 메서드.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>큐의 메시지 읽기 및 제거
이 코드에서는 2단계를 거쳐 큐에서 메시지를 제거할 수 있습니다.

1. 호출 **GetMessageAsync** tooget hello 다음 메시지는 큐에 있습니다. 반환 된 메시지 **GetMessageAsync** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. 기본적으로, 이 메시지는 30초간 표시되지 않습니다.
2. hello 메시지 호출 hello 큐에서 제거 toofinish **DeleteMessageAsync**합니다.

이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다. hello 다음 호출 코드 **DeleteMessageAsync** 직후 hello 메시지를 처리 합니다.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>큐에서 메시지를 제거하는 추가 옵션 활용
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.
첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다. 둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다. hello 다음 코드 예제에서는 **GetMessages** 메서드 tooget 20 메시지 한 번 호출에서 합니다. 그런 다음에 **foreach** 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 too5 분을 설정합니다. 모든에 대해 5 분 시작 hello 메시지 hello에 동일 하므로 hello 호출 후 5 분 너무 성공한 시간**GetMessages**, 삭제 되지 않았으므로 되는 모든 메시지를 다시 표시 됩니다.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Hello 큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. **FetchAttributes** 메서드 hello 메시지 수를 포함 하 여 hello 큐 특성을 검색 하기 위해 hello 큐 서비스를 요청 합니다. hello **ApproximateMethodCount** 속성에서 검색 하는 hello 마지막 값을 반환 된 **FetchAttributes** hello 큐 서비스를 호출 하지 않고 메서드.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>일반적인 큐 Api Async Await hello 패턴 사용
이 예제에서는 toouse 일반 큐 Api와 패턴 Async Await hello 하는 방법을 보여 줍니다. hello 샘플 호출 hello 비동기 버전의 각각 hello 메서드를 제공 합니다. 각 방법의 hello 비동기 후 수정 하 여이 볼 수 있습니다. 비동기 메서드를 사용 하면 hello Async Await 패턴 hello 호출이 완료 될 때까지 로컬 실행을 일시 중단 합니다. 이 동작 hello 현재 스레드 toodo 성능 병목 현상을 방지 하 고 있는 다른 작업을 통해 응용 프로그램의 전체적인 응답성 hello 합니다. 사용 하 여 대 한 자세한 내용은.net에서 비동기 Await 패턴 hello, 참조 [Async 및 Await (C# 및 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a>큐 삭제
toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 된 **삭제** hello 큐 개체에서 메서드.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>다음 단계
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

