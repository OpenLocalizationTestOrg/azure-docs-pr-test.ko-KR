---
title: ".NET Standard를 사용하여 Azure Event Hubs에서 이벤트 수신 | Microsoft Docs"
description: ".NET Standard에서 EventProcessorHost를 사용하여 메시지 수신 시작"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="a86aa-103">.NET Standard에서 이벤트 프로세서 호스트를 사용하여 메시지 수신 시작</span><span class="sxs-lookup"><span data-stu-id="a86aa-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="a86aa-104">이 샘플은 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="a86aa-105">이 자습서는 **EventProcessorHost**를 사용하여 이벤트 허브에서 메시지를 수신하는 .NET Core 콘솔 응용 프로그램을 작성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="a86aa-106">문자열을 사용자의 이벤트 허브 및 저장소 계정 값으로 바꾸어 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 솔루션을 있는 그대로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="a86aa-107">또는 이 자습서의 단계를 수행하여 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a86aa-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a86aa-108">Prerequisites</span></span>

* <span data-ttu-id="a86aa-109">[Microsoft Visual Studio 2015 또는 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a86aa-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="a86aa-110">이 자습서의 예제에서는 Visual Studio 2017을 사용하지만 Visual Studio 2015도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="a86aa-111">[.NET Core Visual Studio 2015 또는 2017 도구](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="a86aa-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="a86aa-112">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a86aa-112">An Azure subscription.</span></span>
* <span data-ttu-id="a86aa-113">Azure Event Hubs 네임스페이스.</span><span class="sxs-lookup"><span data-stu-id="a86aa-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="a86aa-114">Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="a86aa-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="a86aa-115">Event Hubs 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="a86aa-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="a86aa-116">1단계에서는 [Azure Portal](https://portal.azure.com)을 사용하여 Event Hubs 형식의 네임스페이스를 만들고 응용 프로그램이 이벤트 허브와 통신하는 데 필요한 관리 자격 증명을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="a86aa-117">네임스페이스 및 이벤트 허브를 만들려면 [이 문서](event-hubs-create.md)의 절차에 따라 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a86aa-118">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a86aa-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="a86aa-119">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="a86aa-120">포털의 왼쪽 탐색 창에서 **새로 만들기**, **저장소**, **저장소 계정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="a86aa-121">저장소 계정 블레이드에서 필드를 완성한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![저장소 계정 만들기][1]

4. <span data-ttu-id="a86aa-123">**배포 성공** 메시지가 나타나면 새 저장소 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="a86aa-124">**Essentials** 블레이드에서 **Blob**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="a86aa-125">**Blob service** 블레이드가 열리면 맨 위의 **+ 컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="a86aa-126">컨테이너 이름을 지정한 다음 **Blob service** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="a86aa-127">왼쪽 블레이드에서 **선택키**를 클릭하고 저장소 컨테이너 이름, 저장소 계정 및 **key1** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="a86aa-128">메모장이나 기타 다른 위치에 임시로 이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="a86aa-129">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a86aa-129">Create a console application</span></span>

<span data-ttu-id="a86aa-130">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-130">Start Visual Studio.</span></span> <span data-ttu-id="a86aa-131">**파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="a86aa-132">.NET Core 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-132">Create a .NET Core console application.</span></span>

![새 프로젝트][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="a86aa-134">Event Hubs NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a86aa-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="a86aa-135">다음 단계에 따라 [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) 및 [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET 표준 라이브러리 NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="a86aa-136">마우스 오른쪽 단추로 새롭게 만든 프로젝트를 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a86aa-137">**찾아보기** 탭을 클릭한 다음 "Microsoft.Azure.EventHubs"를 검색하고 **Microsoft.Azure.EventHubs** 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="a86aa-138">**설치** 를 클릭하여 설치를 완료한 후 이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="a86aa-139">1단계와 2단계를 반복하고 **Microsoft.Azure.EventHubs.Processor** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="a86aa-140">IEventProcessor 인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="a86aa-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="a86aa-141">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="a86aa-142">새 클래스 이름을 **SimpleEventProcessor**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="a86aa-143">SimpleEventProcessor.cs 파일을 열고 다음 `using` 문을 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="a86aa-144">`IEventProcessor` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="a86aa-145">`SimpleEventProcessor` 클래스의 전체 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="a86aa-146">SimpleEventProcessor 클래스를 사용하여 메시지를 수신하는 기본 콘솔 메서드 작성</span><span class="sxs-lookup"><span data-stu-id="a86aa-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="a86aa-147">Program.cs 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="a86aa-148">이벤트 허브 연결 문자열, 이벤트 허브 이름, 저장소 계정 컨테이너 이름, 저장소 계정 이름, 저장소 계정 키의 `Program` 클래스에 상수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="a86aa-149">자리 표시자를 해당 값으로 바꾸어 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="a86aa-150">다음과 같이 `MainAsync`라는 새 메서드를 `Program` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="a86aa-151">`Main` 메서드에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="a86aa-152">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-152">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="a86aa-153">프로그램을 실행하고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="a86aa-154">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-154">Congratulations!</span></span> <span data-ttu-id="a86aa-155">이제 이벤트 프로세서 호스트를 사용하여 이벤트 허브에서 메시지를 수신했습니다.</span><span class="sxs-lookup"><span data-stu-id="a86aa-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86aa-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a86aa-156">Next steps</span></span>
<span data-ttu-id="a86aa-157">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a86aa-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a86aa-158">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="a86aa-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a86aa-159">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="a86aa-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a86aa-160">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="a86aa-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
