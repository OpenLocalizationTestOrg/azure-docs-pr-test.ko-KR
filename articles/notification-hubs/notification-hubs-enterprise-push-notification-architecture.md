---
title: "알림 허브 - 엔터프라이즈 푸시 아키텍처"
description: "엔터프라이즈 환경에서 Azure 알림 허브 사용에 대한 지침"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="7e35d-103">엔터프라이즈 푸시 아키텍처 지침</span><span class="sxs-lookup"><span data-stu-id="7e35d-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="7e35d-104">오늘날 기업에서는 최종 사용자(외부)를 위해 또는 직원(내부)을 위해 모바일 응용 프로그램을 만드는 일이 점점 많아지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="7e35d-105">기업은 가동 중인 기존 백엔드 시스템이 모바일 응용 프로그램 아키텍처에 통합되어야 하는 메인프레임 또는 일부 LoB 응용 프로그램이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="7e35d-106">이 가이드에서는 일반적인 시나리오에 사용 가능한 솔루션을 권장하는 이 통합을 가장 잘 수행할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="7e35d-107">백엔드 시스템에서 관심 이벤트가 발생하는 경우 해당 모바일 응용 프로그램을 통해 사용자에게 푸시 알림을 보내기 위한 일반적인 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="7e35d-108">예:</span><span class="sxs-lookup"><span data-stu-id="7e35d-108">E.g.</span></span> <span data-ttu-id="7e35d-109">자신의 iPhone에 해당 은행의 뱅킹 앱을 가지고 있는 은행 고객은 자신의 계정에서 일정 금액 이상이 인출되었을 때 알림을 받고 싶어합니다. 또한 재무부서에서 일하며 자신의 Windows Phone에 예산 승인 앱을 가지고 있는 직원은 요청이 승인되었을 때 알림을 받고 싶어하는 인트라넷 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="7e35d-110">은행 계좌 또는 승인 처리는 사용자에 게 푸시를 초기화해야 하는 일부 백엔드 시스템에서 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="7e35d-111">이벤트가 알림을 트리거할 때 같은 종류의 논리를 모두 동일하게 빌드하여 푸시를 구현해야 하는 여러 백엔드 시스템 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="7e35d-112">여기에서는 여러 백엔드 시스템을 단일 푸시 시스템에 함께 통합할 때의 복잡성을 설명합니다. 최종 사용자는 다양한 알림을 구독했을 수 있고 여기에는 여러 모바일 응용 프로그램이 있을 수도 있습니다. 예를 들어, 인트라넷 모바일 앱의 경우 특정 모바일 응용 프로그램이 그러한 여러 백엔드 시스템에서 알림을 받기를 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="7e35d-113">백엔드 시스템은 푸시 의미론/기술을 모르거나 알고 있어야 합니다. 그래서 일반적인 솔루션은 전통적으로 모든 관심 이벤트의 백엔드 시스템을 폴링한 구성 요소를 소개했으며 클라이언트에 푸시 메시지를 전송하는 역할을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="7e35d-114">여기에서는 확장 가능한 솔루션을 만드는 동안 복잡성을 줄일 수 있는 [Azure Service Bus - 항목/구독 모델]을 사용하는 보다 나은 해결책에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="7e35d-115">이는 일반 솔루션 아키텍처입니다(여러 모바일 앱으로 일반화되었지만 모바일 앱이 하나뿐일 경우 동일하게 적용할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="7e35d-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="7e35d-116">아키텍처</span><span class="sxs-lookup"><span data-stu-id="7e35d-116">Architecture</span></span>
![][1]

<span data-ttu-id="7e35d-117">이 아키텍처 다이어그램의 핵심 부분은 항목/구독 프로그래밍 모델(자세한 내용은 [Service Bus Pub/Sub 프로그래밍]참조)을 제공하는 Azure 서비스 버스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="7e35d-118">이 경우에 받는 사람인 모바일 백엔드(일반적으로 모바일 앱에 푸시를 시작할 [Azure 모바일 서비스])는 백엔드 시스템에서 직접 메시지를 수신하지 않지만 [Azure Service Bus]에서 제공하는 대신 중간 추상화 계층을 가지고 있기 때문에 모바일 백엔드가 하나 이상의 백엔드 시스템에서 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="7e35d-119">각각의 백엔드 시스템(예: 계정, HR, 재정)에 대해 서비스 버스 항목을 만들어야 하며 기본적으로 메시지를 푸시 알림으로 보내기 시작할 관심 "항목"입니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="7e35d-120">백엔드 시스템은 이러한 항목에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="7e35d-121">모바일 백엔드는 서비스 버스 구독을 만들어 이러한 항목을 하나 이상 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="7e35d-122">이를 통해 모바일 백엔드가 해당 백엔드 시스템에서 알림을 받도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="7e35d-123">모바일 백엔드는 계속 해당 구독에서 메시지를 수신하고 메시지가 도착하는 즉시 다시 해당 알림 허브에 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="7e35d-124">그런 다음 알림 허브는 마침내 메시지를 모바일 앱으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="7e35d-125">주요 구성 요소를 요약하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="7e35d-126">백엔드 시스템(LoB/레거시 시스템)</span><span class="sxs-lookup"><span data-stu-id="7e35d-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="7e35d-127">서비스 버스 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="7e35d-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="7e35d-128">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="7e35d-128">Sends Message</span></span>
2. <span data-ttu-id="7e35d-129">모바일 백엔드</span><span class="sxs-lookup"><span data-stu-id="7e35d-129">Mobile backend</span></span>
   * <span data-ttu-id="7e35d-130">서비스 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="7e35d-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="7e35d-131">메시지 받기(백엔드 시스템에서)</span><span class="sxs-lookup"><span data-stu-id="7e35d-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="7e35d-132">클라이언트에 알림 보내기(Azure 알림 허브를 통해)</span><span class="sxs-lookup"><span data-stu-id="7e35d-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="7e35d-133">모바일 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="7e35d-133">Mobile Application</span></span>
   * <span data-ttu-id="7e35d-134">알림 수신 및 표시</span><span class="sxs-lookup"><span data-stu-id="7e35d-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="7e35d-135">이점:</span><span class="sxs-lookup"><span data-stu-id="7e35d-135">Benefits:</span></span>
1. <span data-ttu-id="7e35d-136">수신자(알림 허브를 통한 모바일 앱/서비스)와 발신자(백엔드 시스템) 사이를 분리하면 최소한의 변경 내용을 가진 추가 백엔드 시스템을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="7e35d-137">이렇게 하면 하나 이상의 백엔드 시스템에서 이벤트를 받을 수 있는 여러 모바일 앱 시나리오를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="7e35d-138">샘플:</span><span class="sxs-lookup"><span data-stu-id="7e35d-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7e35d-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7e35d-139">Prerequisites</span></span>
<span data-ttu-id="7e35d-140">개념뿐만 아니라 일반적인 만들기 및 구성 단계에 익숙해지려면 다음 자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="7e35d-141">[Service Bus Pub/Sub 프로그래밍] - [Service Bus 항목/구독]으로 작업하는 세부 사항, 항목/구독을 포함하는 네임스페이스를 만드는 방법 및 메시지를 송신 및 수신하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="7e35d-142">[알림 허브 - Windows 유니버설 자습서] - Windows 스토어 앱을 설정하고 알림 허브를 사용하여 등록한 다음 알림을 수신하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="7e35d-143">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="7e35d-143">Sample code</span></span>
<span data-ttu-id="7e35d-144">전체 샘플 코드는 [알림 허브 샘플]에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="7e35d-145">세 가지 구성 요소로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-145">It is split into three components:</span></span>

1. <span data-ttu-id="7e35d-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="7e35d-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="7e35d-147">a.</span><span class="sxs-lookup"><span data-stu-id="7e35d-147">a.</span></span> <span data-ttu-id="7e35d-148">이 프로젝트는 *WindowsAzure.ServiceBus* Nuget 패키지를 사용하며 [Service Bus Pub/Sub 프로그래밍]을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="7e35d-149">b.</span><span class="sxs-lookup"><span data-stu-id="7e35d-149">b.</span></span> <span data-ttu-id="7e35d-150">모바일 앱으로 메시지를 전달하기 시작하는 LoB 시스템을 시뮬레이션하기 위한 간단한 C# 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="7e35d-151">c.</span><span class="sxs-lookup"><span data-stu-id="7e35d-151">c.</span></span> <span data-ttu-id="7e35d-152">`CreateTopic` 은 메시지를 보낼 서비스 버스 항목을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="7e35d-153">d.</span><span class="sxs-lookup"><span data-stu-id="7e35d-153">d.</span></span> <span data-ttu-id="7e35d-154">`SendMessage` 는 이 서비스 버스 항목으로 메시지를 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="7e35d-155">여기서는 샘플 목적으로 항목에 임의 메시지 집합을 정기적으로 한 번 보내보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="7e35d-156">일반적으로 이벤트가 발생하면 메시지를 보내는 백엔드 시스템이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="7e35d-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="7e35d-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="7e35d-158">a.</span><span class="sxs-lookup"><span data-stu-id="7e35d-158">a.</span></span> <span data-ttu-id="7e35d-159">이 프로젝트는 *WindowsAzure.ServiceBus* 및 *Microsoft.Web.WebJobs.Publish* Nuget 패키지를 사용하며 [Service Bus Pub/Sub 프로그래밍]을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="7e35d-160">b.</span><span class="sxs-lookup"><span data-stu-id="7e35d-160">b.</span></span> <span data-ttu-id="7e35d-161">[Azure WebJob]으로 실행해야 하는 또 다른 C# 콘솔 앱입니다. LoB/백엔드 시스템에서 메시지를 지속적으로 수신하려면 이를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="7e35d-162">모바일 백엔드의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="7e35d-163">c.</span><span class="sxs-lookup"><span data-stu-id="7e35d-163">c.</span></span> <span data-ttu-id="7e35d-164">`CreateSubscription` 은 백엔드 시스템이 메시지를 보내는 항목에 대한 서비스 버스 구독을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="7e35d-165">비즈니스 시나리오에 따라 이 구성 요소는 해당 항목에 대한 하나 이상의 구독을 만듭니다(예: 일부는 HR 시스템에서, 일부는 재무 시스템 등에서 메시지를 수신할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="7e35d-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="7e35d-166">d.</span><span class="sxs-lookup"><span data-stu-id="7e35d-166">d.</span></span> <span data-ttu-id="7e35d-167">ReceiveMessageAndSendNotification은 해당 구독을 사용하여 항목에서 메시지를 보내는 데 사용되며 읽기에 성공한 경우 Azure 알림 허브를 사용하여 모바일 앱으로 보낼 알림(샘플 시나리오의 경우 Windows 네이티브 토스트 알림)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="7e35d-168">e.</span><span class="sxs-lookup"><span data-stu-id="7e35d-168">e.</span></span> <span data-ttu-id="7e35d-169">이를 **WebJob**으로 게시하려면 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **WebJob으로 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="7e35d-170">f.</span><span class="sxs-lookup"><span data-stu-id="7e35d-170">f.</span></span> <span data-ttu-id="7e35d-171">게시 프로필을 선택한 후 Azure 웹 사이트가 없는 경우 이 WebJob을 호스트할 새 Azure 웹 사이트를 만들고, 웹 사이트가 있는 경우 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="7e35d-172">g.</span><span class="sxs-lookup"><span data-stu-id="7e35d-172">g.</span></span> <span data-ttu-id="7e35d-173">[Azure 클래식 포털] 에 로그인할 때 다음과 같은 단계를 거쳐야 하기 때문에 작업이 "계속 실행"되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="7e35d-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="7e35d-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="7e35d-175">a.</span><span class="sxs-lookup"><span data-stu-id="7e35d-175">a.</span></span> <span data-ttu-id="7e35d-176">모바일 백엔드의 일부로 실행 중인 WebJob에서 토스트 알림을 수신하여 이를 표시하는 Windows 스토어 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="7e35d-177">[알림 허브 - Windows 유니버설 자습서]를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="7e35d-178">b.</span><span class="sxs-lookup"><span data-stu-id="7e35d-178">b.</span></span> <span data-ttu-id="7e35d-179">응용 프로그램이 토스트 알림을 받을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="7e35d-180">c.</span><span class="sxs-lookup"><span data-stu-id="7e35d-180">c.</span></span> <span data-ttu-id="7e35d-181">앱 시작 시 다음 Notification Hubs 등록 코드가 호출되었는지 확인합니다(*HubName* 및 *DefaultListenSharedAccessSignature* 교체 후).</span><span class="sxs-lookup"><span data-stu-id="7e35d-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="7e35d-182">샘플 실행:</span><span class="sxs-lookup"><span data-stu-id="7e35d-182">Running sample:</span></span>
1. <span data-ttu-id="7e35d-183">WebJob이 성공적으로 실행 중이고 "계속 실행"되도록 예약되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="7e35d-184">**EnterprisePushMobileApp** 을 실행하면 Windows 스토어 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="7e35d-185">**EnterprisePushBackendSystem** 콘솔 응용 프로그램을 실행하면 LoB 백엔드를 시뮬레이션 하고 메시지를 보내기 시작하기 때문에 다음과 같이 나타나는 토스트 알림이 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="7e35d-186">원래 메시지는 웹 작업의 서비스 버스 구독에서 모니터링하는 서비스 버스 항목으로 전송되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="7e35d-187">메시지가 수신되면 알림이 생성되어 모바일 앱으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="7e35d-188">사용자의 웹 작업에 대한 [Azure 클래식 포털] 의 로그 링크로 이동하면 WebJob 로그를 통해 처리 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e35d-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="7e35d-189">[알림 허브 샘플]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="7e35d-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="7e35d-190">[Azure 모바일 서비스]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="7e35d-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="7e35d-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="7e35d-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="7e35d-192">[Service Bus Pub/Sub 프로그래밍]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="7e35d-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="7e35d-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="7e35d-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="7e35d-194">[알림 허브 - Windows 유니버설 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="7e35d-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="7e35d-195">[Azure 클래식 포털]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="7e35d-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
