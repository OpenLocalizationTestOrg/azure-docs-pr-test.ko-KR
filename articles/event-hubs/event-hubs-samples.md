---
title: "이벤트 허브 샘플 aaaAzure | Microsoft Docs"
description: "Azure Event Hubs 샘플"
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
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="16d6a-103">Event Hubs 샘플</span><span class="sxs-lookup"><span data-stu-id="16d6a-103">Event Hubs samples</span></span> 

<span data-ttu-id="16d6a-104">hello Azure 이벤트 허브 샘플 집합을 보여 줍니다의 주요 기능 [Azure 이벤트 허브](/azure/event-hubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="16d6a-105">이 문서 분류 하 고 hello 예제 링크 tooeach 함께 사용할 수에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="16d6a-106">이 문서 작성 hello 시 이벤트 허브 샘플은 여러 다른 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="16d6a-107">MSDN 개발자 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="16d6a-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="16d6a-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="16d6a-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="16d6a-109">서로 다른 버전의.NET Framework hello에 대 한 자세한 내용은 참조 [프레임 워크 및 대상](/dotnet/articles/standard/frameworks)합니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="16d6a-110">시간이 지남에 따라 더 많은 샘플이 추가될 예정이므로 업데이트가 있는지 자주 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="16d6a-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="16d6a-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="16d6a-111">.NET Standard</span></span>

<span data-ttu-id="16d6a-112">hello 다음 샘플을 보여 줍니다 방법을 toosend hello를 사용 하 여 이벤트를 수신 하 고 [이벤트 허브 클라이언트](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) hello에 대 한 [.NET 표준 라이브러리](/dotnet/articles/standard/library)합니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="16d6a-113">이벤트 보내기</span><span class="sxs-lookup"><span data-stu-id="16d6a-113">Send events</span></span> 

<span data-ttu-id="16d6a-114">hello [보내기 시작](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 샘플 toowrite.NET Core 콘솔 이벤트 tooan 이벤트 허브를 전송 하는 응용 프로그램 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="16d6a-115">이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="16d6a-115">Receive events</span></span> 

<span data-ttu-id="16d6a-116">hello [이벤트 프로세서 호스트 hello로 받기 시작](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 샘플은 이벤트 프로세서 호스트 hello를 사용 하 여 이벤트 허브에서 메시지를 수신 하는.NET Core 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="16d6a-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="16d6a-117">.NET Framework</span></span>   

<span data-ttu-id="16d6a-118">이러한 샘플 hello를 대상으로 지정 되는 Azure 이벤트 허브의 다른 다양 한 기능을 보여 줍니다. [.NET Framework 라이브러리](/dotnet/framework/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="16d6a-119">수신된 이벤트를 사용자에게 알림</span><span class="sxs-lookup"><span data-stu-id="16d6a-119">Notify users of events received</span></span>

<span data-ttu-id="16d6a-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) 샘플 센서 또는 다른 시스템에서 받은 데이터의 사용자에 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="16d6a-121">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="16d6a-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="16d6a-122">hello [이벤트 허브 시작](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) 샘플 어떻게 toocreate 이벤트 허브 이벤트 tooan 이벤트 허브 보내고 사용할 hello를 사용 하 여 이벤트 등 이벤트 허브의 hello 기본 기능을 보여 줍니다. [이벤트프로세서호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="16d6a-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="16d6a-123">이벤트 처리 확장</span><span class="sxs-lookup"><span data-stu-id="16d6a-123">Scale out event processing</span></span> 

<span data-ttu-id="16d6a-124">hello [이벤트 처리 확장](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) 샘플 방법을 toouse hello [이벤트 프로세서 호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello 작업의 이벤트 허브 스트림 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="16d6a-125">표시 방법을 tooimplement hello **EventProcessor** 및 **EventProcessorFactory** 개체 toomanage hello 이벤트 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="16d6a-126">SQL의 데이터를 이벤트 허브로 끌어오기</span><span class="sxs-lookup"><span data-stu-id="16d6a-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="16d6a-127">hello [SQL 끌어오는 데이터](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) 샘플은 방법을 보여 줍니다 toopull 데이터를 SQL 테이블 tooan 이벤트 허브를 다운스트림 분석 응용 프로그램에 대 한 입력으로 toouse 밀어 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="16d6a-128">웹 데이터를 이벤트 허브로 끌어오기</span><span class="sxs-lookup"><span data-stu-id="16d6a-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="16d6a-129">hello [hello 웹에서 데이터를 가져올](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) 샘플은 방법을 보여 줍니다 public에서 toopull 데이터 피드 (예: 부서의 운송의 트래픽 정보 피드 hello) tooan 이벤트 허브를 밀어 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16d6a-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16d6a-130">Next steps</span></span>

<span data-ttu-id="16d6a-131">자세한 정보.NET Framework 버전에 대 한 링크를 따라 hello를 방문 하 여:</span><span class="sxs-lookup"><span data-stu-id="16d6a-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="16d6a-132">Frameworks 및 대상</span><span class="sxs-lookup"><span data-stu-id="16d6a-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="16d6a-133">.NET Framework 4.6 및 4.5</span><span class="sxs-lookup"><span data-stu-id="16d6a-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="16d6a-134">Hello 문서 다음에 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16d6a-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="16d6a-135">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="16d6a-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="16d6a-136">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="16d6a-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="16d6a-137">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="16d6a-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)