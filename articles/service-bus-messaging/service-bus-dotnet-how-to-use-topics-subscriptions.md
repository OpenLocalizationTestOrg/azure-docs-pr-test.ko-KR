---
title: "Azure Service Bus 항목 및 구독을 시작 하는 aaaGet | Microsoft Docs"
description: "Service Bus 메시징 항목 및 구독을 사용하는 C# 콘솔 응용 프로그램을 작성합니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="cce34-103">Service Bus 큐 항목 시작</span><span class="sxs-lookup"><span data-stu-id="cce34-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="cce34-104">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="cce34-104">What will be accomplished</span></span>

<span data-ttu-id="cce34-105">이 자습서에서는 hello 다음 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="cce34-106">Hello Azure 포털을 사용 하 여 서비스 버스 네임 스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="cce34-107">Hello Azure 포털을 사용 하 여 서비스 버스 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="cce34-108">Hello Azure 포털을 사용 하 여 서비스 버스 구독 toothat 주제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="cce34-109">콘솔 응용 프로그램 toosend 메시지 toohello 도움말 항목을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="cce34-110">Hello 구독에서 콘솔 응용 프로그램 tooreceive 해당 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cce34-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cce34-111">Prerequisites</span></span>

1. <span data-ttu-id="cce34-112">[Visual Studio 2015 이상](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="cce34-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="cce34-113">이 자습서의 hello 예제에서는 Visual Studio 2017를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="cce34-114">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="cce34-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="cce34-115">1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="cce34-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="cce34-116">이미 서비스 버스 메시징 네임 스페이스를 만든 경우 점프 toohello [hello Azure 포털을 사용 하 여 항목을 만들](#2-create-a-topic-using-the-azure-portal) 섹션.</span><span class="sxs-lookup"><span data-stu-id="cce34-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="cce34-117">2. Hello Azure 포털을 사용 하 여 주제를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="cce34-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="cce34-118">Toohello 로그온 [Azure 포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="cce34-119">Hello hello 포털의 왼쪽된 탐색 창에서 클릭 **서비스 버스** (표시 되지 않으면 **서비스 버스**, 클릭 **더 많은 서비스**).</span><span class="sxs-lookup"><span data-stu-id="cce34-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="cce34-120">Hello 네임 스페이스를 원하는 toocreate hello 항목을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="cce34-121">hello 네임 스페이스 개요 블레이드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-121">hello namespace overview blade appears:</span></span>
   
    ![토픽 만들기][createtopic1]
4. <span data-ttu-id="cce34-123">Hello에 **서비스 버스 네임 스페이스** 블레이드에서 클릭 **항목**, 클릭 **추가 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![항목 선택][createtopic2]
5. <span data-ttu-id="cce34-125">Hello 항목에 대 한 이름을 입력 하 고 hello의 선택을 취소 **분할을 사용 하도록 설정** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="cce34-126">Hello와 해당 기본값이 다른 옵션을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-126">Leave hello other options with their default values.</span></span>
   
    ![새로 만들기 선택][createtopic3]
6. <span data-ttu-id="cce34-128">Hello 블레이드의 hello 아래쪽 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="cce34-129">3. 구독 toohello 주제 만들기</span><span class="sxs-lookup"><span data-stu-id="cce34-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="cce34-130">Hello 포털 리소스 창에서 1 단계에서 만든 hello 네임 스페이스를 클릭 한 다음 2 단계에서 만든 hello 항목의 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="cce34-131">Hello 개요 창의 hello top hello 클릭 더한 다음 너무 서명**구독** tooadd 구독 toothis 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![구독 만들기][createtopic4]

3. <span data-ttu-id="cce34-133">Hello 구독에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="cce34-134">Hello와 해당 기본값이 다른 옵션을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="cce34-135">4. Toohello 부분 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="cce34-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="cce34-136">Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램을 작성할 toosend 메시지 toohello 항목 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="cce34-137">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cce34-137">Create a console application</span></span>

<span data-ttu-id="cce34-138">Visual Studio를 시작하고 **콘솔 앱(.NET Framework)** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="cce34-139">Hello Service Bus NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="cce34-140">Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="cce34-141">Hello 클릭 **찾아보기** 탭에서 검색할 **Microsoft Azure 서비스 버스**를 선택한 후 hello **WindowsAzure.ServiceBus** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="cce34-142">클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![NuGet 패키지 선택][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="cce34-144">일부 코드 toosend 메시지 toohello 항목 작성</span><span class="sxs-lookup"><span data-stu-id="cce34-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="cce34-145">Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="cce34-146">다음 코드 toohello hello 추가 `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cce34-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="cce34-147">집합 hello `connectionString` 변수 toohello 연결 문자열 hello 네임 스페이스를 만들 때 가져온 마우스 설정 `topicName` hello 항목을 만들 때 사용한 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="cce34-148">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-148">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="cce34-149">Hello 프로그램을 실행 하 고 Azure 포털 hello 확인: hello hello 네임 스페이스의 항목 이름을 클릭 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="cce34-150">hello 항목 **Essentials** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="cce34-151">Hello 아래 근처의 hello 블레이드 나열 된 hello 구독, 해당 hello 알 수 있듯이 **메시지 수** 값이 각 구독 1 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="cce34-152">Hello 메시지 (hello 다음 섹션에서 설명) 검색 하지 않고 hello 보낸 사람 응용 프로그램을 실행할 때마다,이 값이 1 씩 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="cce34-153">또한 hello 항목 증가 hello의 해당 hello 현재 크기를 확인 **현재** hello에 대 한 값 **Essentials** 블레이드 될 때마다 hello 앱 메시지 toohello 항목/구독을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![메시지 크기][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="cce34-155">5. Hello 구독에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="cce34-156">tooreceive hello 메시지 또는 메시지 방금 전송 받은 새 콘솔 응용 프로그램을 만들고 참조 toohello Service Bus NuGet 패키지를 유사한 toohello 이전 보낸 사람 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="cce34-157">Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="cce34-158">다음 코드 toohello hello 추가 `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cce34-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="cce34-159">집합 hello `connectionString` 변수 toohello 연결 문자열을 설정 하 고 hello 네임 스페이스를 만들 때 가져온 `topicName` hello 항목을 만들 때 사용한 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="cce34-160">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-160">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. <span data-ttu-id="cce34-161">Hello 프로그램을 실행 하 고 hello 포털을 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="cce34-162">해당 hello 확인 **메시지 수** 및 **현재** 값은 이제 0입니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![항목 길이][topic-message-receive]

<span data-ttu-id="cce34-164">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-164">Congratulations!</span></span> <span data-ttu-id="cce34-165">이제 토픽 및 구독을 만들고, 메시지를 보내고 해당 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cce34-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cce34-166">Next steps</span></span>

<span data-ttu-id="cce34-167">체크 아웃 우리의 [샘플 GitHub 리포지토리](https://github.com/Azure/azure-service-bus/tree/master/samples) hello 보다 고급 서비스 버스 메시징 기능 중 일부를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce34-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
