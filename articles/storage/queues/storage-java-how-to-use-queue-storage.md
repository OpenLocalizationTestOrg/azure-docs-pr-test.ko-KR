---
title: "Java에서 큐 저장소 aaaHow toouse | Microsoft Docs"
description: "방법 toouse hello Azure 큐 서비스 toocreate 및 큐 삭제 및 삽입, 및 메시지 삭제에 대해 알아봅니다. 샘플은 Java로 작성되었습니다."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 297f89c9d21a38d2b4a5f4346f66f59f9d487010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a>어떻게 toouse Java에서 큐 저장소
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>개요
이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 큐 저장소 서비스에 표시 됩니다. hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Java 용 Azure 저장소 SDK][Azure Storage SDK for Java]합니다. hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만드는** 및 **삭제** 큐입니다. 큐에 대 한 자세한 내용은 참조 hello [다음 단계](#Next-Steps) 섹션.

SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다. 자세한 내용은 참조 hello [Android 용 Azure 저장소 SDK][Azure Storage SDK for Android]합니다.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Java 응용 프로그램 만들기
이 가이드에서는 Java 응용 프로그램 내에서 로컬로 실행할 수 있거나 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.

toodo tooinstall, 나오는 Java Development Kit (JDK) hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다. 그렇게 않은 후에 hello 최소 요구 사항 및 종속성 hello에 나열 되어 있는 개발 시스템 맞는 tooverify 해야 합니다 [Java 용 Azure 저장소 SDK] [ Azure Storage SDK for Java] GitHub의 리포지토리 합니다. 시스템에 이러한 요구 사항을 충족 하는 경우 다운로드 하 고 해당 리포지토리 로부터 시스템에 hello Java 용 Azure 저장소 라이브러리를 설치 하기 위한 hello 지침을 따를 수 있습니다. 이러한 작업을 완료 되 면이 문서의 hello 예제를 사용 하는 Java 응용 프로그램 수 toocreate 됩니다.

## <a name="configure-your-application-tooaccess-queue-storage"></a>응용 프로그램 tooaccess 큐 저장소를 구성 합니다.
Hello toouse Azure 저장소 Api tooaccess 큐 저장할 hello Java 파일 맨 문을 toohello 가져오기 뒤에 추가 합니다.

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다. 형식에 따라, 사용자의 저장소 계정 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 입력 하 고 hello에 나열 된 hello 저장소 계정의 기본 액세스 키를 hello 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다. 이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Microsoft Azure에서 역할 내에서 실행 하는 응용 프로그램을이 문자열 hello 서비스 구성 파일에 저장 될 수 *ServiceConfiguration.cscfg*, 호출 toohello로 액세스할 수 있습니다 및  **RoleEnvironment.getConfigurationSettings** 메서드. Hello 연결 문자열에서 가져오는의 예로 **설정** 라는 요소 *StorageConnectionString* hello 서비스 구성 파일에:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.

## <a name="how-to-create-a-queue"></a>방법: 큐 만들기
**CloudQueueClient** 개체를 통해 큐에 대한 참조 개체를 가져올 수 있습니다. hello 다음 코드에서는 **CloudQueueClient** 개체입니다. (참고: 추가 방법을 알아볼 toocreate는 **CloudStorageAccount** 개체, 자세한 내용은 참조 **CloudStorageAccount** hello에 [Azure 저장소 클라이언트 SDK 참조].)

사용 하 여 hello **CloudQueueClient** tooget toouse 원하는 참조 toohello 큐 개체입니다. 존재 하지 않는 경우 hello 큐를 만들 수 있습니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a>방법: 메시지 tooa 큐 추가
tooinsert를 기존 큐에 메시지를 먼저 새로 만들려면 **CloudQueueMessage**합니다. 그런 다음 호출 하는 hello **addMessage** 메서드. **CloudQueueMessage** 는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다. 코드 (존재 하지 않는) 하는 경우 큐를 만듦 및 삽입 hello 메시지 "Hello, World" 다음과 같습니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a>방법: hello 다음 메시지 피킹
호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peekMessage**합니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>방법: 대기 중인된 메시지의 hello 내용을 변경
메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다. Hello 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello hello 작업 작업의 상태를 사용할 수 있습니다. 코드 다음 hello hello 큐 메시지를 새 내용으로 업데이트 하 고 집합 hello 가시성 제한 시간 tooextend 다른 60 초입니다. 이 hello 메시지와 관련 된 작업의 hello 상태를 저장 하 고 hello 클라이언트 hello 메시지에서 작업 하는 다른 분 toocontinue를 제공 합니다. 부터 hello toohardware 또는 소프트웨어 오류로 인해 실패 하면 처리 단계를 통해 toostart 필요 없이 큐의 메시지에이 기술을 tootrack multi-step 워크플로 사용할 수 있습니다. 일반적으로는 다시 시도 횟수를 보관할 때 하 고 메시지를 다시 시도 하는 경우 hello 이상  *n*  시간,는 삭제 합니다. 이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.

hello 다음 hello 메시지 큐를 통해 샘플 검색 코드에서 hello 메시지 콘텐츠를 수정 및 종료 한 다음 "Hello, World" hello 콘텐츠에 대 한 일치 하는 hello 첫 번째 메시지를 찾습니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

또는 hello 다음 코드 샘플 메시지를 업데이트 방금 hello 첫 번째 표시 hello 큐에 있습니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a>방법: hello 큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. hello **downloadAttributes** 큐에 있는 메시지의 수를 포함 하 메서드 몇 가지 현재 값에 대 한 hello 큐 서비스를 요청 합니다. 메시지를 추가 또는 큐 서비스 hello tooyour 요청 응답 한 후 제거 될 수 있으므로 hello count 대략적인 값만입니다. hello **getApproximateMessageCount** 너무 hello 호출에 의해 검색 된 hello 마지막 값을 반환 하는 메서드**downloadAttributes**, hello 큐 서비스를 호출 하지 않고 있습니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a>방법: hello 다음 메시지를 큐에서 제거
다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다. 호출 하는 경우 **retrieveMessage**, 큐에 있는 hello 다음 메시지를 가져옵니다. 반환 된 메시지 **retrieveMessage** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. 기본적으로, 이 메시지는 30초간 표시되지 않습니다. toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **deleteMessage**합니다. 이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다. 코드 호출 **deleteMessage** 직후 hello 메시지를 처리 합니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a>큐에서 메시지를 제거하는 추가 옵션
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다. 첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다. 둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다.

hello 다음 코드 예제에서는 hello **retrieveMessages** 메서드 tooget 20 메시지 한 번 호출에서 합니다. 그런 다음 **for** 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분 (300 초)을 설정합니다. 동일한 hello에 해당 hello 5 모두에 대 한 시작 시간 (분) 참고 메시지 시간, 5 분 이후 경과한 hello 호출 너무 때**retrieveMessages**, 모든 메시지는 삭제 되지 않았으므로 다시 표시 됩니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a>방법: hello 큐 나열
호출 hello hello 현재 큐 목록 tooobtain **CloudQueueClient.listQueues()** 메서드의 컬렉션을 반환 합니다 **CloudQueue** 개체입니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a>방법: 큐 삭제
toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 hello **deleteIfExists** 메서드 hello **CloudQueue** 개체입니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>다음 단계
큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.

* [Java용 Azure Storage SDK][Azure Storage SDK for Java]
* [Azure 저장소 클라이언트 SDK 참조][Azure 저장소 클라이언트 SDK 참조]
* [Azure Storage 서비스 REST API][Azure Storage Services REST API]
* [Azure Storage 팀 블로그][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 저장소 클라이언트 SDK 참조]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
