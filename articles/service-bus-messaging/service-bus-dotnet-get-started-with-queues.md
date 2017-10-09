---
title: "Azure 서비스 버스 큐 aaaGet 시작 | Microsoft Docs"
description: "Service Bus 메시징 큐를 사용하는 C# 콘솔 응용 프로그램을 작성합니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="b08e2-103">Service Bus 큐 시작</span><span class="sxs-lookup"><span data-stu-id="b08e2-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="b08e2-104">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="b08e2-104">What will be accomplished</span></span>
<span data-ttu-id="b08e2-105">이 자습서에서는 hello 다음 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="b08e2-106">Hello Azure 포털을 사용 하 여 서비스 버스 네임 스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="b08e2-107">Hello Azure 포털을 사용 하 여 서비스 버스 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="b08e2-108">콘솔 응용 프로그램 toosend 메시지를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="b08e2-109">콘솔 응용 프로그램 tooreceive hello hello 이전 단계에서 전송 된 메시지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b08e2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b08e2-110">Prerequisites</span></span>
1. <span data-ttu-id="b08e2-111">[Visual Studio 2015 이상](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b08e2-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="b08e2-112">이 자습서의 hello 예제에서는 Visual Studio 2017를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="b08e2-113">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="b08e2-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="b08e2-114">1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b08e2-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="b08e2-115">서비스 버스 메시징 네임 스페이스를 이미 만든 경우 점프 toohello [hello Azure 포털을 사용 하 여 큐를 만들](#2-create-a-queue-using-the-azure-portal) 섹션.</span><span class="sxs-lookup"><span data-stu-id="b08e2-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="b08e2-116">2. Hello Azure 포털을 사용 하 여 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="b08e2-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="b08e2-117">이미 서비스 버스 큐를 만든 경우 점프 toohello [송신 메시지 toohello 큐](#3-send-messages-to-the-queue) 섹션.</span><span class="sxs-lookup"><span data-stu-id="b08e2-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="b08e2-118">3. 송신 메시지 toohello 큐</span><span class="sxs-lookup"><span data-stu-id="b08e2-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="b08e2-119">Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램을 작성 했습니다 toosend 메시지 toohello 큐</span><span class="sxs-lookup"><span data-stu-id="b08e2-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="b08e2-120">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b08e2-120">Create a console application</span></span>

<span data-ttu-id="b08e2-121">Visual Studio를 시작하고 **콘솔 앱(.NET Framework)** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="b08e2-122">Hello Service Bus NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="b08e2-123">Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b08e2-124">Hello 클릭 **찾아보기** 탭에서 검색할 **Microsoft Azure 서비스 버스**를 선택한 후 hello **WindowsAzure.ServiceBus** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="b08e2-125">클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![NuGet 패키지 선택][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="b08e2-127">일부 코드 toosend 메시지 toohello 큐 쓰기</span><span class="sxs-lookup"><span data-stu-id="b08e2-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="b08e2-128">Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="b08e2-129">다음 코드 toohello hello 추가 `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b08e2-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="b08e2-130">집합 hello `connectionString` 변수 toohello 연결 문자열 hello 네임 스페이스를 만들 때 가져온 마우스 설정 `queueName` hello 큐를 만들 때 사용한 toohello 큐 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="b08e2-131">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-131">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="b08e2-132">Hello 프로그램을 실행 하 고 Azure 포털 hello 확인: hello 네임 스페이스에 큐의 hello 이름을 클릭 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="b08e2-133">hello 큐 **Essentials** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="b08e2-134">해당 hello 확인 **근무 중인 메시지 수** 값은 이제 1 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="b08e2-135">Hello 메시지를 검색 하지 않고 hello 보낸 사람 응용 프로그램을 실행할 때마다가이 값 1 씩 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="b08e2-136">또한 참고 hello hello queue의 현재 크기 증가 각 시간 hello 응용 프로그램을 메시지 toohello 큐를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![메시지 크기][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="b08e2-138">4. Hello 큐에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="b08e2-139">방금 전송 받은 tooreceive hello 메시지 새 콘솔 응용 프로그램을 만들고 유사한 toohello 이전 보낸 사람 응용 프로그램 참조 toohello Service Bus NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="b08e2-140">Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="b08e2-141">다음 코드 toohello hello 추가 `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b08e2-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="b08e2-142">집합 hello `connectionString` hello 네임 스페이스를 만들 때를 설정 하는 변수 toohello 연결 문자열 `queueName` hello 큐를 만들 때 사용한 toohello 큐 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="b08e2-143">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-143">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="b08e2-144">Hello 프로그램을 실행 하 고 hello 포털을 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="b08e2-145">해당 hello 확인 **근무 중인 메시지 수** 및 **현재** 값은 이제 0입니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![큐 길이][queue-message-receive]

<span data-ttu-id="b08e2-147">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-147">Congratulations!</span></span> <span data-ttu-id="b08e2-148">이제 큐를 만들고 메시지를 보내고 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b08e2-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b08e2-149">Next steps</span></span>

<span data-ttu-id="b08e2-150">체크 아웃 우리의 [샘플 GitHub 리포지토리](https://github.com/Azure/azure-service-bus/tree/master/samples) hello 보다 고급 서비스 버스 메시징 기능 중 일부를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08e2-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
