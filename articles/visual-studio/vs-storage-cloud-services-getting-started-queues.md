---
title: "큐 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (클라우드 서비스) | Microsoft Docs"
description: "Tooget 시작 서비스에 연결 된 Visual Studio를 사용 하 여 tooa 저장소 계정을 연결 후 Visual Studio에서 클라우드 서비스 프로젝트에서 Azure 큐 저장소를 사용 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(클라우드 서비스 프로젝트)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요
이 문서에서는 tooget 시작 hello Visual Studio를 사용 하 여 클라우드 서비스 프로젝트에서 Azure 저장소 계정을 참조 하거나 만든 후 Visual Studio에서 Azure 큐 저장소를 사용 하는 방법을 설명 **연결 된 서비스 추가** 대화 상자 .

방식을 보여줍니다 toocreate 코드에서 큐입니다. 또한 보여줍니다 tooperform basic 추가, 수정, 읽기 및 큐 메시지를 제거 하는 등의 작업을 대기 하는 방법입니다. hello 샘플 C# 코드에서 작성 되 고 hello를 사용 하 여 [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/dn261237.aspx)합니다.

hello **연결 된 서비스 추가** 작업 프로젝트에 hello 적절 한 NuGet 패키지 tooaccess Azure 저장소를 설치 하 고 계정에 대 한 hello 저장소 tooyour 프로젝트 구성 파일 hello 연결 문자열을 추가 합니다.

* 코드에서 큐를 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](../storage/queues/storage-dotnet-how-to-use-queues.md) 을 참조하세요.
* Azure 저장소에 대한 일반적인 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/) 를 참조하세요.
* Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/) 를 참조하세요.
* ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net) 을 참조하세요.

Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다. 단일 큐 메시지의 크기 (kb) too64 될 수 있습니다 및 큐 수많은 메시지 저장소 계정의 toohello 총 용량 한계를 포함할 수 있습니다.

## <a name="access-queues-in-code"></a>코드에서 큐 액세스
Visual Studio 클라우드 서비스 프로젝트에서 tooaccess 큐 해야 tooinclude hello 다음 Azure 큐 저장소에 액세스 하는 항목 tooany C# 소스 파일.

1. 이러한 hello C# 파일의 hello 위쪽 hello 네임 스페이스 선언을 포함 **를 사용 하 여** 문.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다. 사용 하 여 hello tooget 코드를 다음 저장소 연결 문자열 및 hello Azure 서비스 구성에서 저장소 계정 정보 hello 합니다.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. 가져오기는 **CloudQueueClient** 개체 저장소 계정의 tooreference hello 큐 개체입니다.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. 가져오기는 **CloudQueue** tooreference 특정 큐 개체입니다.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**참고:** hello 다음 샘플에서에서 코드 hello 코드 앞에 위의 hello를 모두 사용 합니다.

## <a name="create-a-queue-in-code"></a>코드에서 큐 만들기
코드에서 toocreate hello 큐 추가 호출 너무**경고는 CreateIfNotExists**합니다.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>메시지 tooa 큐 추가
tooinsert를 기존 큐에 메시지를 새로 만듭니다. **CloudQueueMessage** 개체가, 다음 호출 hello **AddMessage** 메서드.

**CloudQueueMessage** 개체는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.

'Hello World' hello 메시지를 삽입 하는 예제는 다음과 같습니다.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>큐의 메시지 읽기
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **PeekMessage** 메서드.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>큐의 메시지 읽기 및 제거
이 코드에서는 2단계를 거쳐 큐에서 메시지를 제거할 수 있습니다.

1. 호출 **GetMessage** tooget hello 다음 메시지는 큐에 있습니다. 반환 된 메시지 **GetMessage** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. 기본적으로, 이 메시지는 30초간 표시되지 않습니다.
2. hello 메시지 호출 hello 큐에서 제거 toofinish **DeleteMessage**합니다.

이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다. hello 다음 호출 코드 **DeleteMessage** 직후 hello 메시지를 처리 합니다.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Tooprocess 추가 옵션을 사용 하 고 큐의 메시지를 제거 합니다.
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.

* 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다.
* 각 메시지를 처리 하는 작은 시간 toofully 또는 코드를 자세히 허용 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다. hello 다음 코드 예제에서는 **GetMessages** 메서드 tooget 20 메시지 한 번 호출에서 합니다. 그런 다음에 **foreach** 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다. 5 분 해당 hello 참고 hello에서 모든 메시지에 대 한 시작 시간이, 하므로 5 분 이후 경과한 hello 호출 너무 나면**GetMessages**, 모든 메시지는 삭제 되지 않았으므로 다시 표시 됩니다.

예를 들면 다음과 같습니다.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Hello 큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. **FetchAttributes** 메서드 hello 메시지 수를 포함 하 여 hello 큐 특성을 검색 하기 위해 hello 큐 서비스를 요청 합니다. hello **ApproximateMethodCount** 속성에서 검색 하는 hello 마지막 값을 반환 된 **FetchAttributes** hello 큐 서비스를 호출 하지 않고 메서드.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>일반적인 Azure 큐 Api hello Async Await 패턴 사용
이 예에서는 일반적인 Azure 큐 Api와 Async Await toouse hello 패턴을 사용 방법을 보여 줍니다. 각 메서드를 제공 하는 hello hello 비동기 버전을 호출 하는 hello 샘플, hello가 볼 수 있습니다이 **비동기** 각 방법의 이후 수정 합니다. 비동기 메서드의 경우에 사용 되는 hello 비동기-await 패턴 hello 호출이 완료 될 때까지 로컬 실행을 일시 중단 합니다. 이 동작 hello 현재 스레드 toodo 성능 병목 현상을 방지 하 고 있는 다른 작업을 통해 응용 프로그램의 전체적인 응답성 hello 합니다. 사용 하 여 대 한 자세한 내용은 hello.net에서 Await 비동기 패턴에 대 한 참조 [Async 및 Await (C# 및 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a>큐 삭제
큐와 모든 hello 메시지에 포함 된, 호출 hello toodelete **삭제** hello 큐 개체에서 메서드.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>다음 단계
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

