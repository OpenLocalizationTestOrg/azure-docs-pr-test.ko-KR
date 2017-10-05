---
title: "Java에서 Queue Storage를 사용하는 방법 | Microsoft Docs"
description: "Azure 큐 서비스를 사용하여 큐를 작성 및 삭제하고 메시지를 삽입하고 가져오고 삭제하는 방법을 알아봅니다. 샘플은 Java로 작성되었습니다."
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
ms.openlocfilehash: a56b345c5efb4ce9c8ee2da91b798d09d44e42be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="8cc83-104">Java에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="8cc83-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="8cc83-105">개요</span><span class="sxs-lookup"><span data-stu-id="8cc83-105">Overview</span></span>
<span data-ttu-id="8cc83-106">이 가이드에서는 Azure 큐 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="8cc83-107">샘플은 Java로 작성되었으며 [Java용 Azure Storage SDK][Azure Storage SDK for Java](영문)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="8cc83-108">여기서 다루는 시나리오에는 큐 **만들기** 및 **삭제**뿐만 아니라 큐 메시지 **삽입**, **보기**, **가져오기** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="8cc83-109">큐에 대한 자세한 내용은 [다음 단계](#Next-Steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cc83-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="8cc83-110">SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="8cc83-111">자세한 내용은 [Android용 Azure Storage SDK][Azure Storage SDK for Android]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cc83-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="8cc83-112">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8cc83-112">Create a Java application</span></span>
<span data-ttu-id="8cc83-113">이 가이드에서는 Java 응용 프로그램 내에서 로컬로 실행할 수 있거나 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="8cc83-114">그러려면 JDK(Java Development Kit)를 설치하고 Azure 구독에서 Azure 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="8cc83-115">그러고 나면 개발 시스템에서 GitHub의 [Java용 Azure Storage SDK][Azure Storage SDK for Java] 리포지토리에 있는 최소 요구 사항과 종속성을 충족하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="8cc83-116">시스템에서 해당 요구 사항을 충족하는 경우에는 리포지토리에서 시스템의 Java용 Azure Storage Library를 다운로드 및 설치하기 위한 지침을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="8cc83-117">작업을 완료하고 나면 이 문서의 예를 사용하는 Java 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="8cc83-118">큐 저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="8cc83-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="8cc83-119">Azure 저장소 API를 사용하여 큐에 액세스하려는 Java 파일의 맨 위에 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="8cc83-120">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="8cc83-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="8cc83-121">Azure 저장소 클라이언트는 저장소 연결 문자열을 사용하여 데이터 관리 서비스에 액세스하기 위한 끝점 및 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8cc83-122">클라이언트 응용 프로그램에서 실행할 경우 *AccountName*과 *AccountKey* 값에 대해 [Azure Portal](https://portal.azure.com)에 나열된 저장소 계정의 이름과 기본 액세스 키를 사용하여 다음 형식의 저장소 연결 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8cc83-123">이 예제는 정적 필드가 연결 문자열을 포함할 수 있도록 선언하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="8cc83-124">Microsoft Azure의 역할 내에서 실행되는 응용 프로그램에서는 이 문자열이 서비스 구성 파일 *ServiceConfiguration.cscfg*에 저장될 수 있고, **RoleEnvironment.getConfigurationSettings** 메서드 호출을 통해 이 문자열에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="8cc83-125">다음은 서비스 구성 파일에서 이름이 **StorageConnectionString** 인 *설정* 요소에서 연결 문자열을 가져오는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="8cc83-126">다음 샘플에서는 저장소 연결 문자열을 가져오기 위해 위의 두 메서드 중 하나를 사용한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="8cc83-127">방법: 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="8cc83-127">How to: Create a queue</span></span>
<span data-ttu-id="8cc83-128">**CloudQueueClient** 개체를 통해 큐에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="8cc83-129">다음 코드는 **CloudQueueClient** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="8cc83-130">(참고: **loudStorageAccount** 개체를 만들 수 있는 방법이 더 있습니다. 자세한 내용은 [Azure 저장소 클라이언트 SDK 참조]에서 **CloudStorageAccount**를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="8cc83-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="8cc83-131">**CloudQueueClient** 개체를 사용하여 사용할 큐에 대한 참조를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="8cc83-132">큐가 없는 경우 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="8cc83-133">큐에 메시지 추가 방법</span><span class="sxs-lookup"><span data-stu-id="8cc83-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="8cc83-134">기존 큐에 메시지를 삽입하려면 먼저 새 **CloudQueueMessage**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="8cc83-135">그런 다음, **addMessage** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="8cc83-136">**CloudQueueMessage** 는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="8cc83-137">다음은 큐가 없는 경우 새로 만들고 "Hello, World" 메시지를 삽입하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="8cc83-138">방법: 다음 메시지 보기</span><span class="sxs-lookup"><span data-stu-id="8cc83-138">How to: Peek at the next message</span></span>
<span data-ttu-id="8cc83-139">큐에서 메시지를 제거하지 않고도 **peekMessage**를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="8cc83-140">방법: 대기 중인 메시지의 콘텐츠 변경</span><span class="sxs-lookup"><span data-stu-id="8cc83-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="8cc83-141">큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="8cc83-142">메시지가 작업을 나타내는 경우 이 기능을 사용하여 작업의 상태를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="8cc83-143">다음 코드는 큐 메시지를 새로운 콘텐츠로 업데이트하고 표시 제한 시간이 60초 더 늘어나도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="8cc83-144">그러면 메시지와 연결된 작업의 상태가 저장되고 클라이언트에서 메시지에 대한 작업을 계속할 수 있는 시간이 1분 더 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="8cc83-145">이 기술을 사용하여 처리 단계가 하드웨어 또는 소프트웨어 오류로 인해 실패하는 경우 처음부터 시작하지 않고도 큐 메시지에 대한 여러 단계의 워크플로를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="8cc83-146">일반적으로 재시도 횟수도 유지하고, 메시지가 *n*번 이상 다시 시도되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="8cc83-147">이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="8cc83-148">다음 코드 샘플에서는 메시지 큐를 검색하여 내용에서 "Hello, World"와 일치하는 최초의 메시지를 찾고 메시지 내용을 수정한 후 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="8cc83-149">한편 다음 코드 샘플에서는 큐에서 처음으로 보이는 메시지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="8cc83-150">방법: 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="8cc83-150">How to: Get the queue length</span></span>
<span data-ttu-id="8cc83-151">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="8cc83-152">**downloadAttributes** 메서드는 큐에 있는 메시지 수를 포함한 일부 현재 값을 큐 서비스에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="8cc83-153">큐 서비스가 요청에 응답한 후 메시지가 추가되거나 제거될 수 있으므로 이 메시지 수는 근사치일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="8cc83-154">**getApproximateMessageCount** 메서드는 큐 서비스를 호출하지 않고도 **downloadAttributes**를 호출하여 검색된 마지막 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="8cc83-155">큐에서 다음 메시지를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="8cc83-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="8cc83-156">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="8cc83-157">**retrieveMessage**를 호출하면 큐에서 다음 메시지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="8cc83-158">**retrieveMessage** 에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="8cc83-159">기본적으로, 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="8cc83-160">큐에서 메시지 제거를 완료하려면 **deleteMessage**도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="8cc83-161">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="8cc83-162">코드는 메시지가 처리된 직후에 **deleteMessage** 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="8cc83-163">큐에서 메시지를 제거하는 추가 옵션</span><span class="sxs-lookup"><span data-stu-id="8cc83-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="8cc83-164">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="8cc83-165">먼저, 메시지의 배치(최대 32개)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="8cc83-166">두 번째로, 표시하지 않는 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="8cc83-167">다음 코드 예제는 **retrieveMessages** 메서드를 사용하여 한 번 호출에 20개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="8cc83-168">그런 다음 **for** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="8cc83-169">또한 각 메시지에 대해 표시하지 않는 제한 시간을 5분(300초)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="8cc83-170">5분은 모든 메시지에 대해 동시에 시작되므로, **retrieveMessages**에 대한 호출 이후로 5분이 지나고 나면 삭제되지 않은 모든 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="8cc83-171">큐 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="8cc83-171">How to: List the queues</span></span>
<span data-ttu-id="8cc83-172">현재 큐의 목록을 가져오려면 **CloudQueue** 개체의 컬렉션을 반환하는 **CloudQueueClient.listQueues()** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="8cc83-173">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="8cc83-173">How to: Delete a queue</span></span>
<span data-ttu-id="8cc83-174">큐 및 해당 큐의 모든 메시지를 삭제하려면 **CloudQueue** 개체의 **deleteIfExists** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc83-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="8cc83-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8cc83-175">Next steps</span></span>
<span data-ttu-id="8cc83-176">이제 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀 더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8cc83-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="8cc83-177">[Java용 Azure Storage SDK][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="8cc83-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="8cc83-178">[Azure 저장소 클라이언트 SDK 참조][Azure 저장소 클라이언트 SDK 참조]</span><span class="sxs-lookup"><span data-stu-id="8cc83-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="8cc83-179">[Azure Storage 서비스 REST API][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="8cc83-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="8cc83-180">[Azure Storage 팀 블로그][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="8cc83-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 저장소 클라이언트 SDK 참조]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
