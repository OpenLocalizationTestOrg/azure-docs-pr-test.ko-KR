---
title: "Java를 사용하여 Azure Event Hubs에서 이벤트 수신 | Microsoft Docs"
description: "Java를 사용하여 Event Hubs에서 수신 시작"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="cf750-103">Java를 사용하여 Azure Event Hubs에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="cf750-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="cf750-104">소개</span><span class="sxs-lookup"><span data-stu-id="cf750-104">Introduction</span></span>
<span data-ttu-id="cf750-105">Event Hubs는 연결된 장치와 응용 프로그램에서 생성되는 엄청난 양의 데이터를 처리 및 분석할 수 있도록 초당 수백만 개의 이벤트를 수용할 수 있는 확장성이 뛰어난 수집 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="cf750-106">이벤트 허브로 수집된 데이터는 실시간 분석 공급자나 저장소 클러스터를 사용하여 변환하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="cf750-107">자세한 내용은 [이벤트 허브 개요][Event Hubs overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf750-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="cf750-108">이 자습서에서는 Java로 작성된 콘솔 응용 프로그램을 사용하여 이벤트 허브로 이벤트를 수신하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf750-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cf750-109">Prerequisites</span></span>

<span data-ttu-id="cf750-110">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="cf750-111">Java 개발 환경.</span><span class="sxs-lookup"><span data-stu-id="cf750-111">A Java development environment.</span></span> <span data-ttu-id="cf750-112">이 자습서에서는 [Eclipse](https://www.eclipse.org/)를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="cf750-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="cf750-113">An active Azure account.</span></span> <br/><span data-ttu-id="cf750-114">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="cf750-115">자세한 내용은 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 무료 체험</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf750-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="cf750-116">Java에서 EventProcessorHost를 사용하여 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="cf750-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="cf750-117">**EventProcessorHost**는 영구적 검사점을 관리하여 Event Hubs의 이벤트 수신을 간소화하고 이러한 Event Hubs에서 병렬 수신하는 Java 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="cf750-118">EventProcessorHost를 사용하면 다른 노드에 호스트된 경우라도 여러 수신기 간에 이벤트를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="cf750-119">이 예제에서는 단일 수신기에 대해 EventProcessorHost를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="cf750-120">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cf750-120">Create a storage account</span></span>
<span data-ttu-id="cf750-121">EventProcessorHost를 사용하려면 [Azure Storage 계정][Azure Storage account]이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="cf750-122">[Azure Portal][Azure portal]에 로그온하고 화면 왼쪽에서 **+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="cf750-123">**저장소**를 클릭한 다음 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="cf750-124">**저장소 계정 만들기** 블레이드에서 저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="cf750-125">필드의 나머지 부분을 입력하고 원하는 지역을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="cf750-126">새로 만든 저장소 계정을 클릭한 후 **액세스 키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="cf750-127">이 자습서에서 나중에 사용할 기본 액세스 키를 임시 위치로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="cf750-128">EventProcessor 호스트를 사용하여 Java 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="cf750-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="cf750-129">Event Hubs에 대한 Java 클라이언트 라이브러리는 [Maven 중앙 리포지토리][Maven Package]의 Maven 프로젝트에 사용할 수 있으며 Maven 프로젝트 파일 내의 다음 종속성 선언을 사용하여 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="cf750-130">다양한 유형의 빌드 환경을 위해, [Maven 중앙 리포지토리][Maven Package] 또는 [GitHub의 릴리스 배포 지점](https://github.com/Azure/azure-event-hubs/releases)에서 최근에 릴리스된 JAR 파일을 명시적으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="cf750-131">다음 샘플에서는 먼저 즐겨 찾는 Java 개발 환경에서 콘솔/셸 응용 프로그램에 대한 새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="cf750-132">클래스는 `ErrorNotificationHandler`라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="cf750-133">다음 코드를 사용하여 `EventProcessor`(이)라는 클래스를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="cf750-134">다음 코드를 사용하여 `EventProcessorSample`이라는 클래스를 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter to stop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="cf750-135">다음 필드를 이벤트 허브 및 저장소 계정을 만들 때 사용한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="cf750-136">이 자습서에서는 EventProcessorHost의 단일 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="cf750-137">처리량을 늘리려면 EventProcessorHost의 여러 인스턴스를 개별 컴퓨터에서 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="cf750-138">그러면 중복성도 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-138">This provides redundancy as well.</span></span> <span data-ttu-id="cf750-139">이러한 경우 다양한 인스턴스가 자동으로 서로 조정하여 수신된 이벤트의 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="cf750-140">여러 수신기가 각각 이벤트를 *모두* 처리하도록 하려면 **ConsumerGroup** 개념을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="cf750-141">서로 다른 컴퓨터에서 이벤트를 수신하는 경우 EventProcessorHost 인스턴스의 이름을 해당 인스턴스가 배포된 컴퓨터 또는 역할을 기준으로 지정하면 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf750-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cf750-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf750-142">Next steps</span></span>
<span data-ttu-id="cf750-143">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf750-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="cf750-144">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="cf750-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="cf750-145">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="cf750-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="cf750-146">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="cf750-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
