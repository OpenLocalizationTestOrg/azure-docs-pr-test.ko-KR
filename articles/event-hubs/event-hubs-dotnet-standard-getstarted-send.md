---
title: "이벤트 허브 표준.NET을 사용 하 여 aaaSend 이벤트 tooAzure | Microsoft Docs"
description: "표준.NET의 이벤트를 tooEvent 허브 전송 시작"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="128aa-103">표준.NET에서 tooAzure 이벤트 허브 메시지를 보내기 시작.</span><span class="sxs-lookup"><span data-stu-id="128aa-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="128aa-104">이 샘플은 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="128aa-105">이 자습서에서는 toowrite 세트를 전송 하는.NET Core 콘솔 응용 프로그램 tooan 이벤트 허브를 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="128aa-106">Hello를 실행할 수 있습니다 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 솔루션으로-, 대체 hello `EhConnectionString` 및 `EhEntityPath` 이벤트 허브 값이 포함 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="128aa-107">참고할 수 또는 hello에서에서 단계를이 자습서 toocreate 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="128aa-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="128aa-108">Prerequisites</span></span>

* <span data-ttu-id="128aa-109">[Microsoft Visual Studio 2015 또는 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="128aa-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="128aa-110">hello의에서 예제가 자습서에서는 Visual Studio 2017 하지만 Visual Studio 2015 에서도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="128aa-111">[.NET Core Visual Studio 2015 또는 2017 도구](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="128aa-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="128aa-112">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="128aa-112">An Azure subscription.</span></span>
* <span data-ttu-id="128aa-113">이벤트 허브 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="128aa-113">An event hub namespace.</span></span>

<span data-ttu-id="128aa-114">toosend 메시지 tooan 이벤트 허브 toowrite Visual Studio는 C# 콘솔 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="128aa-115">Event Hubs 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="128aa-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="128aa-116">hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate hello 이벤트 허브 유형에 대 한 네임 스페이스 및 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="128aa-117">toocreate 네임 스페이스 및 이벤트 허브 절차에 따라 hello에 [이 여기서](event-hubs-create.md), 다음 단계를 수행 하는 hello 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="128aa-118">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="128aa-118">Create a console application</span></span>

<span data-ttu-id="128aa-119">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-119">Start Visual Studio.</span></span> <span data-ttu-id="128aa-120">Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="128aa-121">.NET Core 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-121">Create a .NET Core console application.</span></span>

![새 프로젝트][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="128aa-123">Hello 이벤트 허브 NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="128aa-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="128aa-124">Hello 추가 [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) 다음이 단계를 수행 하 여.NET 표준 라이브러리 NuGet 패키지 tooyour 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="128aa-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="128aa-125">Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="128aa-126">Hello 클릭 **찾아보기** 누른 "Microsoft.Azure.EventHubs" 및 선택 hello에 대 한 검색 **Microsoft.Azure.EventHubs** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="128aa-127">클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="128aa-128">일부 코드 toosend 메시지 toohello 이벤트 허브를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="128aa-129">Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="128aa-130">상수 toohello 추가 `Program` hello 이벤트 허브 연결 문자열 및 엔터티 경로 (개별 이벤트 허브 이름)에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="128aa-131">Hello 적절 한 값을 hello 이벤트 허브를 만들 때 대괄호의 hello 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="128aa-132">라는 새 메서드 추가 `MainAsync` toohello `Program` 클래스 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="128aa-133">라는 새 메서드 추가 `SendMessagesToEventHub` toohello `Program` 클래스 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="128aa-134">다음 코드 toohello hello 추가 `Main` hello에 대 한 메서드 `Program` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="128aa-135">Program.cs는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="128aa-136">Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="128aa-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="128aa-137">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-137">Congratulations!</span></span> <span data-ttu-id="128aa-138">이제 메시지 tooan 이벤트 허브를 보냈을.</span><span class="sxs-lookup"><span data-stu-id="128aa-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="128aa-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="128aa-139">Next steps</span></span>
<span data-ttu-id="128aa-140">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="128aa-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="128aa-141">Event Hubs에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="128aa-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="128aa-142">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="128aa-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="128aa-143">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="128aa-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="128aa-144">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="128aa-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
