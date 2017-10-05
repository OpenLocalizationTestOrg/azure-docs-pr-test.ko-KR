---
title: ".NET Framework를 사용하여 Azure Event Hubs에서 이벤트 수신 | Microsoft Docs"
description: ".NET Framework를 사용하여 Azure Event Hubs에서 이벤트를 수신하려면 이 자습서를 따르세요."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 581af52b3264b1a7c57315c65d5385a372308c27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="6fd3e-103">.NET Framework를 사용하여 Azure Event Hubs에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="6fd3e-103">Receive events from Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="6fd3e-104">소개</span><span class="sxs-lookup"><span data-stu-id="6fd3e-104">Introduction</span></span>

<span data-ttu-id="6fd3e-105">이벤트 허브는 연결된 장치 및 응용 프로그램에서 많은 양의 이벤트 데이터(원격 분석)를 처리하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="6fd3e-106">이벤트 허브에 데이터를 수집한 후 저장소 클러스터를 사용하여 데이터를 저장하거나 실시간 분석 공급자를 사용하여 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="6fd3e-107">이 대규모 이벤트 수집 및 처리 기능은 IoT(사물 인터넷)를 포함하여 최신 응용 프로그램 아키텍처의 핵심 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="6fd3e-108">이 자습서에서는 **[이벤트 프로세서 호스트][EventProcessorHost]**를 사용하여 Event Hub에서 메시지를 수신하는 .NET Framework 콘솔 응용 프로그램을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-108">This tutorial shows how to write a .NET Framework console application that receives messages from an event hub using the **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="6fd3e-109">.NET Framework를 사용하여 이벤트를 전송하려면 [.NET Framework를 사용하여 Azure Event Hubs로 이벤트 전송](event-hubs-dotnet-framework-getstarted-send.md) 문서를 참조하거나 목차 왼쪽에서 해당하는 전송 언어를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-109">To send events using the .NET Framework, see the [Send events to Azure Event Hubs using the .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click the appropriate sending language in the left-hand table of contents.</span></span>

<span data-ttu-id="6fd3e-110">[이벤트 프로세서 호스트][EventProcessorHost]는 영구적 검사점을 관리하여 Event Hubs의 이벤트 수신을 간소화하고 이러한 Event Hubs에서 병렬 수신하는 .NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-110">The [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="6fd3e-111">[이벤트 프로세서 호스트][Event Processor Host]를 사용하면 다른 노드에 호스트된 수신기를 비롯한 여러 수신기 간에 이벤트를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-111">Using the [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="6fd3e-112">이 예제에서는 단일 수신기에 대해 [이벤트 프로세서 호스트][EventProcessorHost]를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-112">This example shows how to use the [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="6fd3e-113">[확장된 이벤트 처리][Scale out Event Processing with Event Hubs] 샘플에서는 여러 수신기에서 [이벤트 프로세서 호스트][EventProcessorHost]를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-113">The [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how to use the [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fd3e-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6fd3e-114">Prerequisites</span></span>

<span data-ttu-id="6fd3e-115">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-115">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="6fd3e-116">[Microsoft Visual Studio 2015 이상](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="6fd3e-117">이 자습서의 스크린샷에서는 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-117">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="6fd3e-118">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-118">An active Azure account.</span></span> <span data-ttu-id="6fd3e-119">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="6fd3e-120">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="6fd3e-121">Event Hubs 네임스페이스 및 Event Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="6fd3e-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="6fd3e-122">첫 번째 단계에서는 [Azure Portal](https://portal.azure.com)을 사용하여 Event Hubs 형식의 네임스페이스를 만들고 응용 프로그램에서 Event Hub와 통신하는 데 필요한 관리 자격 증명을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-122">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="6fd3e-123">네임스페이스 및 Event Hub를 만들려면 [이 문서](event-hubs-create.md)의 프로시저를 따른 후 이 자습서의 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-123">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="6fd3e-124">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="6fd3e-124">Create an Azure Storage account</span></span>

<span data-ttu-id="6fd3e-125">[이벤트 프로세서 호스트][EventProcessorHost]를 사용하려면 [Azure Storage 계정][Azure Storage account]이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-125">To use the [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="6fd3e-126">[Azure Portal][Azure portal]에 로그온하고 화면 왼쪽 위에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-126">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
2. <span data-ttu-id="6fd3e-127">**저장소**를 클릭한 다음 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="6fd3e-128">**저장소 계정 만들기** 블레이드에서 저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-128">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="6fd3e-129">리소스를 만들 Azure 구독, 리소스 그룹 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-129">Choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="6fd3e-130">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="6fd3e-131">저장소 계정 목록에서 새로 만든 저장소 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-131">In the list of storage accounts, click the newly created storage account.</span></span>
5. <span data-ttu-id="6fd3e-132">저장소 계정 블레이드에서 **선택키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-132">In the storage account blade, click **Access keys**.</span></span> <span data-ttu-id="6fd3e-133">이 자습서에서 나중에 **key1** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-133">Copy the value of **key1** to use later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="6fd3e-134">수신기 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-134">Create a receiver console application</span></span>

1. <span data-ttu-id="6fd3e-135">Visual Studio에서 **콘솔 응용 프로그램** 프로젝트 템플릿을 사용하여 Visual C# 데스크톱 응용 프로그램 프로젝트를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-135">In Visual Studio, create a new Visual C# Desktop App project using the **Console  Application** project template.</span></span> <span data-ttu-id="6fd3e-136">프로젝트 이름을 **Receiver**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-136">Name the project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="6fd3e-137">솔루션 탐색기에서 **Receiver** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **솔루션에 대한 NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-137">In Solution Explorer, right-click the **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="6fd3e-138">**찾아보기** 탭을 클릭한 다음 `Microsoft Azure Service Bus Event Hub - EventProcessorHost`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-138">Click the **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="6fd3e-139">**설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-139">Click **Install**, and accept the terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="6fd3e-140">Visual Studio는 [Azure 서비스 버스 이벤트 허브 - EventProcessorHost NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost)에 대한 참조 및 해당하는 모든 종속성을 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-140">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="6fd3e-141">**Receiver** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-141">Right-click the **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="6fd3e-142">새 클래스의 이름을 **SimpleEventProcessor**로 지정하고 **추가**를 클릭하여 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-142">Name the new class **SimpleEventProcessor**, and then click **Add** to create the class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="6fd3e-143">SimpleEventProcessor.cs 파일의 맨 위에 다음 구문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-143">Add the following statements at the top of the SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="6fd3e-144">그런 다음 다음 코드를 클래스의 본문으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-144">Then, substitute the following code for the body of the class:</span></span>
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  <span data-ttu-id="6fd3e-145">이 클래스는 Event Hub에서 받는 이벤트를 처리하기 위해 **EventProcessorHost**에 의해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-145">This class is called by the **EventProcessorHost** to process events received from the event hub.</span></span> <span data-ttu-id="6fd3e-146">`SimpleEventProcessor` 클래스는 초시계를 사용하여 **EventProcessorHost** 컨텍스트에서 검사점 메서드를 주기적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-146">The `SimpleEventProcessor` class uses a stopwatch to periodically call the checkpoint method on the **EventProcessorHost** context.</span></span> <span data-ttu-id="6fd3e-147">이 처리로 인해 수신기가 다시 시작되는 경우 5분 이하의 처리 작업은 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-147">This processing ensures that, if the receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="6fd3e-148">**Program** 클래스에서 파일 맨 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-148">In the **Program** class, add the following `using` statement at the top of the file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="6fd3e-149">그런 다음 `Program` 클래스의 `Main` 메서드를 다음 코드로 바꾸고 이전에 저장한 Event Hub 이름 및 네임스페이스 수준 연결 문자열과 이전 섹션에서 복사한 저장소 계정 및 키를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-149">Then, replace the `Main` method in the `Program` class with the following code, substituting the event hub name and the namespace-level connection string that you saved previously, and the storage account and key that you copied in the previous sections.</span></span> 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key to stop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="6fd3e-150">프로그램을 실행하고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-150">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="6fd3e-151">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-151">Congratulations!</span></span> <span data-ttu-id="6fd3e-152">이제 이벤트 프로세서 호스트를 사용하여 Event Hub에서 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-152">You have now received messages from an event hub using the Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="6fd3e-153">이 자습서에서는 [EventProcessorHost][EventProcessorHost]의 단일 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="6fd3e-154">처리량을 늘리려면 [EventProcessorHost][EventProcessorHost]의 여러 인스턴스를 실행하는 것이 좋습니다. [확장된 이벤트 처리][확장된 이벤트 처리] 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-154">To increase throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in the [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="6fd3e-155">이러한 경우 다양한 인스턴스가 자동으로 서로 조정되어 수신된 이벤트의 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-155">In those cases, the various instances automatically coordinate with each other to load balance the received events.</span></span> <span data-ttu-id="6fd3e-156">여러 수신기가 각각 이벤트를 *모두* 처리하도록 하려면 **ConsumerGroup** 개념을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-156">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="6fd3e-157">서로 다른 컴퓨터에서 이벤트를 수신하는 경우 [EventProcessorHost][EventProcessorHost] 인스턴스의 이름을 해당 인스턴스가 배포된 컴퓨터 또는 역할을 기준으로 지정하면 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-157">When receiving events from different machines, it might be useful to specify names for [EventProcessorHost][EventProcessorHost] instances based on the machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="6fd3e-158">이러한 항목에 대한 자세한 내용은 [Event Hubs 개요][Event Hubs overview] 및 [Event Hubs 프로그래밍 가이드][Event Hubs Programming Guide] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-158">For more information about these topics, see the [Event Hubs overview][Event Hubs overview] and the [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6fd3e-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6fd3e-159">Next steps</span></span>

<span data-ttu-id="6fd3e-160">이제 Event Hub를 만들고 데이터를 보내고 받는 작업 중인 응용 프로그램을 구축했으므로 다음 링크를 방문하여 더 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting the following links:</span></span>

* <span data-ttu-id="6fd3e-161">[이벤트 프로세서 호스트][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="6fd3e-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="6fd3e-162">[Event Hubs 개요][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="6fd3e-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="6fd3e-163">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="6fd3e-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
