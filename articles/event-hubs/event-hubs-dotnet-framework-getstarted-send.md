---
title: ".NET Framework hello aaaSend tooAzure 이벤트 허브 사용 하 여 이벤트 | Microsoft Docs"
description: ".NET Framework hello를 사용 하 여 tooEvent 허브 이벤트를 전송 합니다. 시작."
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="9d18b-103">.NET Framework hello를 사용 하 여 tooAzure 이벤트 허브 이벤트를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="9d18b-104">소개</span><span class="sxs-lookup"><span data-stu-id="9d18b-104">Introduction</span></span>

<span data-ttu-id="9d18b-105">이벤트 허브는 연결된 장치 및 응용 프로그램에서 많은 양의 이벤트 데이터(원격 분석)를 처리하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="9d18b-106">이벤트 허브로 데이터를 수집한 후 저장소 클러스터를 사용 하 여 hello 데이터를 저장할 수도 있고 실시간 분석 공급자를 사용 하 여 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="9d18b-107">이 대규모 이벤트 수집 및 처리 기능은 hello 인터넷 IoT (사물)를 포함 하 여 최신 응용 프로그램 아키텍처의 핵심 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="9d18b-108">이 자습서에서는 어떻게 toouse hello [Azure 포털](https://portal.azure.com) toocreate 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="9d18b-109">또한 toosend 이벤트 tooan 이벤트 허브로 작성 된 C# 사용 하 여 콘솔 응용 프로그램을 사용 하 여.NET Framework hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="9d18b-110">.NET Framework hello를 사용 하 여 tooreceive 이벤트 참조 hello [hello.NET Framework를 사용 하 여 이벤트를 수신](event-hubs-dotnet-framework-getstarted-receive-eph.md) , 문서 또는 hello hello 내용의 왼쪽 테이블에서 적절 한 받는 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="9d18b-111">toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="9d18b-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="9d18b-112">[Microsoft Visual Studio 2015 이상](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="9d18b-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="9d18b-113">이 자습서에서는 hello 스크린 샷 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="9d18b-114">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="9d18b-114">An active Azure account.</span></span> <span data-ttu-id="9d18b-115">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="9d18b-116">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d18b-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="9d18b-117">Event Hubs 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="9d18b-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="9d18b-118">hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate의 네임 스페이스는 이벤트 허브를 입력 하 고 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="9d18b-119">toocreate 네임 스페이스 및 이벤트 허브 hello 절차에 따라 [이 여기서](event-hubs-create.md), 다음 hello이이 자습서에서는 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="9d18b-120">보낸 사람 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9d18b-120">Create a sender console application</span></span>

<span data-ttu-id="9d18b-121">이 섹션에서는 이벤트 tooyour 이벤트 허브를 전송 하는 Windows 콘솔 앱을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="9d18b-122">Visual Studio에서 hello를 사용 하 여 새 Visual C# 데스크톱 앱 프로젝트를 만듭니다 **콘솔 응용 프로그램** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="9d18b-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="9d18b-123">이름 hello 프로젝트 **보낸 사람**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="9d18b-124">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **보낸 사람** 프로젝트를 마우스 클릭 **솔루션에 대 한 NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="9d18b-125">Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="9d18b-126">클릭 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="9d18b-127">Visual Studio 다운로드, 설치 및 추가 참조 toohello [Azure 서비스 버스 라이브러리 NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="9d18b-128">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="9d18b-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="9d18b-129">다음 필드 toohello hello 추가 **프로그램** 클래스를 이전에 저장 하는 hello 네임 스페이스 수준 연결 문자열 및 hello 이전 섹션에서 만든 hello 이벤트 허브 hello 이름의 hello 자리 표시자 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="9d18b-130">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="9d18b-130">Add hello following method toohello **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="9d18b-131">이 메서드는 200 ms 지연 된 이벤트 tooyour 이벤트 허브를 지속적으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="9d18b-132">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="9d18b-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="9d18b-133">Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9d18b-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="9d18b-134">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-134">Congratulations!</span></span> <span data-ttu-id="9d18b-135">이제 메시지 tooan 이벤트 허브를 보냈을.</span><span class="sxs-lookup"><span data-stu-id="9d18b-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d18b-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d18b-136">Next steps</span></span>
<span data-ttu-id="9d18b-137">이벤트 허브를 만들고 데이터를 전송 하는 작업 중인 응용 프로그램을 작성할 했으므로 toohello 다음 시나리오에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="9d18b-138">이벤트 프로세서 호스트 hello를 사용 하 여 이벤트를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d18b-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="9d18b-139">이벤트 프로세서 호스트 참조</span><span class="sxs-lookup"><span data-stu-id="9d18b-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="9d18b-140">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="9d18b-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

