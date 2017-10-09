---
title: "표준.NET을 사용 하 여 Azure 이벤트 허브에서 aaaReceive 이벤트 | Microsoft Docs"
description: "표준.NET에서 EventProcessorHost hello로 메시지를 받기 시작."
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
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="54b51-103">표준.NET의 이벤트 프로세서 호스트 hello로 메시지를 받기 시작.</span><span class="sxs-lookup"><span data-stu-id="54b51-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="54b51-104">이 샘플은 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="54b51-105">이 자습서에서는 어떻게 toowrite.NET Core 콘솔 사용 하 여 이벤트 허브에서 메시지를 수신 하는 응용 프로그램 **EventProcessorHost**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="54b51-106">Hello를 실행할 수 있습니다 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 솔루션으로-, 대체 문자열 hello 이벤트 허브 및 저장소 계정 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="54b51-107">참고할 수 또는 hello에서에서 단계를이 자습서 toocreate 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54b51-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54b51-108">Prerequisites</span></span>

* <span data-ttu-id="54b51-109">[Microsoft Visual Studio 2015 또는 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="54b51-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="54b51-110">hello의에서 예제가 자습서에서는 Visual Studio 2017 하지만 Visual Studio 2015 에서도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="54b51-111">[.NET Core Visual Studio 2015 또는 2017 도구](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="54b51-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="54b51-112">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="54b51-112">An Azure subscription.</span></span>
* <span data-ttu-id="54b51-113">Azure Event Hubs 네임스페이스.</span><span class="sxs-lookup"><span data-stu-id="54b51-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="54b51-114">Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="54b51-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="54b51-115">Event Hubs 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="54b51-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="54b51-116">hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate hello 이벤트 허브에 대 한 네임 스페이스를 입력 하 고 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="54b51-117">toocreate 네임 스페이스 및 이벤트 허브 hello 절차에 따라 [이 여기서](event-hubs-create.md), 다음 단계를 수행 하는 hello 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="54b51-118">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="54b51-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="54b51-119">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="54b51-120">Hello hello 포털의 왼쪽된 탐색 창에서 클릭 **새로**, 클릭 **저장소**, 클릭 하 고 **저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="54b51-121">저장소 계정 블레이드에서 hello hello 필드에 내용을 입력 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![저장소 계정 만들기][1]

4. <span data-ttu-id="54b51-123">Hello를 본 후 **배포 성공** 메시지에서 새 저장소 계정 hello의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="54b51-124">Hello에 **Essentials** 블레이드에서 클릭 **Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="54b51-125">Hello 때 **Blob 서비스** 블레이드를 열고, 클릭 **+ 컨테이너** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="54b51-126">Hello 컨테이너 이름을 입력 한 다음 hello 닫습니다 **Blob 서비스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="54b51-127">클릭 **선택키가** hello 왼쪽된 블레이드 및 복사 hello의 이름에 hello 저장소 컨테이너, hello 저장소 계정과의 hello 값 **key1**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="54b51-128">이러한 값 tooNotepad 또는 일부 다른 임시 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="54b51-129">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="54b51-129">Create a console application</span></span>

<span data-ttu-id="54b51-130">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-130">Start Visual Studio.</span></span> <span data-ttu-id="54b51-131">Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="54b51-132">.NET Core 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-132">Create a .NET Core console application.</span></span>

![새 프로젝트][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="54b51-134">Hello 이벤트 허브 NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="54b51-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="54b51-135">Hello 추가 [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) 및 [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) 다음이 단계를 수행 하 여.NET 표준 라이브러리 NuGet 패키지 tooyour 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="54b51-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="54b51-136">Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="54b51-137">Hello 클릭 **찾아보기** 누른 "Microsoft.Azure.EventHubs" 및 선택 hello에 대 한 검색 **Microsoft.Azure.EventHubs** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="54b51-138">클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="54b51-139">1과 2 단계를 반복 하 여 hello 설치 **Microsoft.Azure.EventHubs.Processor** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="54b51-140">Hello IEventProcessor 인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="54b51-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="54b51-141">솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 프로젝트에서에서 클릭 **추가**, 클릭 하 고 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="54b51-142">Hello 새 클래스 이름을 **SimpleEventProcessor**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="54b51-143">Hello SimpleEventProcessor.cs 파일을 열고 hello 다음 추가 `using` hello 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="54b51-144">구현 hello `IEventProcessor` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="54b51-145">Hello의 전체 내용을 hello 대체 `SimpleEventProcessor` 코드 다음 hello 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="54b51-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="54b51-146">Hello SimpleEventProcessor 클래스 tooreceive 메시지를 사용 하는 주 콘솔 메서드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="54b51-147">Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="54b51-148">상수 toohello 추가 `Program` hello 이벤트 허브 연결 문자열, 이벤트 허브 이름, 저장소 계정 컨테이너 이름, 저장소 계정 이름과 저장소 계정 키에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="54b51-149">코드 다음, 해당 값과 함께 hello 자리 표시자를 대체 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="54b51-150">라는 새 메서드 추가 `MainAsync` toohello `Program` 클래스 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="54b51-151">다음 줄의 코드 toohello hello 추가 `Main` 메서드:</span><span class="sxs-lookup"><span data-stu-id="54b51-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="54b51-152">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="54b51-153">Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="54b51-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="54b51-154">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-154">Congratulations!</span></span> <span data-ttu-id="54b51-155">이벤트 프로세서 호스트 hello를 사용 하 여 이벤트 허브에서 메시지를 받은 있을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54b51-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54b51-156">Next steps</span></span>
<span data-ttu-id="54b51-157">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b51-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="54b51-158">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="54b51-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="54b51-159">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="54b51-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="54b51-160">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="54b51-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
