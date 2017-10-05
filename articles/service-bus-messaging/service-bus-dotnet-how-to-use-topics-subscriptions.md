---
title: "Azure Service Bus 항목 및 구독 시작 | Microsoft Docs"
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
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="a1cbf-103">Service Bus 큐 항목 시작</span><span class="sxs-lookup"><span data-stu-id="a1cbf-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="a1cbf-104">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="a1cbf-104">What will be accomplished</span></span>

<span data-ttu-id="a1cbf-105">이 자습서에서 다루는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="a1cbf-106">Azure Portal을 사용하여 Service Bus 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="a1cbf-107">Azure Portal을 사용하여 Service Bus 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="a1cbf-108">Azure Portal을 사용하여 해당 항목에 Service Bus 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="a1cbf-109">메시지를 항목으로 보내는 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="a1cbf-110">구독으로부터 해당 메시지를 받을 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1cbf-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a1cbf-111">Prerequisites</span></span>

1. <span data-ttu-id="a1cbf-112">[Visual Studio 2015 이상](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a1cbf-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="a1cbf-113">이 자습서의 예제에서는 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="a1cbf-114">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="a1cbf-115">1. Azure Portal을 사용하여 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a1cbf-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="a1cbf-116">Service Bus 메시징 네임스페이스를 이미 만든 경우 [Azure Portal을 사용하여 큐 만들기](#2-create-a-topic-using-the-azure-portal) 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="a1cbf-117">2. Azure Portal을 사용하여 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="a1cbf-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="a1cbf-118">[Azure Portal][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="a1cbf-119">포털의 왼쪽 탐색 창에서 **Service Bus**(**Service Bus**가 표시되지 않으면 **더 많은 서비스** 클릭)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="a1cbf-120">항목을 만들려는 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="a1cbf-121">네임스페이스 개요 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-121">The namespace overview blade appears:</span></span>
   
    ![토픽 만들기][createtopic1]
4. <span data-ttu-id="a1cbf-123">**Service Bus 네임스페이스** 블레이드에서 **항목**을 선택한 다음 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![항목 선택][createtopic2]
5. <span data-ttu-id="a1cbf-125">항목의 이름을 입력하고 **분할 사용** 옵션을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="a1cbf-126">다른 옵션은 기본값 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-126">Leave the other options with their default values.</span></span>
   
    ![새로 만들기 선택][createtopic3]
6. <span data-ttu-id="a1cbf-128">블레이드 하단에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="a1cbf-129">3. 항목에 대한 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="a1cbf-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="a1cbf-130">포털 리소스 창에서 1단계에서 만든 네임스페이스를 클릭한 다음 2단계에서 만든 항목의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="a1cbf-131">개요 창 위에서 **구독** 옆에 있는 더하기 기호를 클릭하여 이 항목에 대한 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![구독 만들기][createtopic4]

3. <span data-ttu-id="a1cbf-133">구독의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-133">Enter a name for the subscription.</span></span> <span data-ttu-id="a1cbf-134">다른 옵션은 기본값 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="a1cbf-135">4. 토픽에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="a1cbf-135">4. Send messages to the topic</span></span>

<span data-ttu-id="a1cbf-136">항목에 메시지를 보내려면 Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="a1cbf-137">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a1cbf-137">Create a console application</span></span>

<span data-ttu-id="a1cbf-138">Visual Studio를 시작하고 **콘솔 앱(.NET Framework)** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="a1cbf-139">Service Bus NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a1cbf-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="a1cbf-140">마우스 오른쪽 단추로 새롭게 만든 프로젝트를 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a1cbf-141">**찾아보기** 탭을 클릭하고 **Microsoft Azure Service Bus**를 검색한 다음 **WindowsAzure.ServiceBus** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="a1cbf-142">**설치**를 클릭하여 설치를 완료한 후 이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![NuGet 패키지 선택][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="a1cbf-144">항목에 메시지를 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="a1cbf-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="a1cbf-145">Program.cs 파일 위쪽에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="a1cbf-146">`Main` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a1cbf-147">`connectionString` 변수는 네임스페이스를 만들 때 가져온 연결 문자열에 설정하고, `topicName`은 항목을 만들 때 사용된 이름에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a1cbf-148">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="a1cbf-149">프로그램을 실행하고 Azure Portal을 확인합니다. 네임스페이스 **개요** 블레이드에서 항목 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="a1cbf-150">항목 **Essentials** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="a1cbf-151">블레이드 맨 아래 가까이 나열된 구독에서 각 구독에 대한 **메시지 수** 값이 이제 1임을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="a1cbf-152">메시지를 검색하지 않고 보낸 사람 응용 프로그램을 실행할 때마다(다음 섹션에서 설명) 이 값이 1씩 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="a1cbf-153">또한 앱이 항목/구독에 메시지를 추가할 때마다 항목의 현재 크기는 **Essentials** 블레이드에 있는 **현재** 값을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![메시지 크기][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="a1cbf-155">5. 구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="a1cbf-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="a1cbf-156">방금 보낸 메시지를 받으려면 새 콘솔 응용 프로그램을 만들고 이전의 보낸 사람 응용 프로그램과 유사한 Service Bus NuGet 패키지에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="a1cbf-157">Program.cs 파일 위쪽에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="a1cbf-158">`Main` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a1cbf-159">`connectionString` 변수는 네임스페이스를 만들 때 가져온 연결 문자열에 설정하고, `topicName`은 항목을 만들 때 사용된 이름에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a1cbf-160">Program.cs 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="a1cbf-161">프로그램을 실행하고 포털을 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="a1cbf-162">**메시지 수**와 **현재** 값이 이제 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![항목 길이][topic-message-receive]

<span data-ttu-id="a1cbf-164">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-164">Congratulations!</span></span> <span data-ttu-id="a1cbf-165">이제 토픽 및 구독을 만들고, 메시지를 보내고 해당 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1cbf-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1cbf-166">Next steps</span></span>

<span data-ttu-id="a1cbf-167">Service Bus 메시징의 많은 고급 기능 중 일부를 보여 주는 [샘플이 있는 GitHub 리포지토리](https://github.com/Azure/azure-service-bus/tree/master/samples)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cbf-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

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
