---
title: "Azure Event Hubs 샘플 | Microsoft Docs"
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
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="c7b95-103">Event Hubs 샘플</span><span class="sxs-lookup"><span data-stu-id="c7b95-103">Event Hubs samples</span></span> 

<span data-ttu-id="c7b95-104">Azure Event Hubs 샘플 집합은 [Azure Event Hubs](/azure/event-hubs/)의 주요 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="c7b95-105">이 문서는 사용할 수 있는 샘플 각각을 링크를 사용하여 범주화하고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="c7b95-106">이 문서가 작성되었을 때 Event Hubs 샘플은 다음 여러 위치에 배치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="c7b95-107">MSDN 개발자 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="c7b95-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="c7b95-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="c7b95-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="c7b95-109">다른 버전의 .NET Framework에 대한 자세한 내용은 [프레임워크 및 대상](/dotnet/articles/standard/frameworks)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7b95-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="c7b95-110">시간이 지남에 따라 더 많은 샘플이 추가될 예정이므로 업데이트가 있는지 자주 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c7b95-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="c7b95-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="c7b95-111">.NET Standard</span></span>

<span data-ttu-id="c7b95-112">다음 샘플은 [.NET Standard 라이브러리](/dotnet/articles/standard/library)에 대해 [Event Hubs 클라이언트](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md)를 사용하여 이벤트를 송수신하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="c7b95-113">이벤트 보내기</span><span class="sxs-lookup"><span data-stu-id="c7b95-113">Send events</span></span> 

<span data-ttu-id="c7b95-114">[전송 시작](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 샘플은 이벤트 허브로 이벤트를 전송하는 .NET Core 콘솔 응용 프로그램을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="c7b95-115">이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="c7b95-115">Receive events</span></span> 

<span data-ttu-id="c7b95-116">[이벤트 프로세서 호스트를 사용하여 수신 시작](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 샘플은 이벤트 프로세서 호스트를 사용하여 이벤트 허브에서 메시지를 수신하는 .NET Core 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="c7b95-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c7b95-117">.NET Framework</span></span>   

<span data-ttu-id="c7b95-118">이러한 샘플은 [.NET Framework 라이브러리](/dotnet/framework/index)를 대상으로 하는 Azure Event Hubs의 기타 다양한 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="c7b95-119">수신된 이벤트를 사용자에게 알림</span><span class="sxs-lookup"><span data-stu-id="c7b95-119">Notify users of events received</span></span>

<span data-ttu-id="c7b95-120">[AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) 샘플은 센서 또는 다른 시스템으로부터 받은 데이터를 사용자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="c7b95-121">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="c7b95-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="c7b95-122">[Event Hubs 시작](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) 샘플은 이벤트 허브를 만드는 방법, 이벤트 허브로 이벤트를 전송하는 방법, [이벤트 프로세서 호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)를 사용하여 이벤트를 소비하는 방법 등 Event Hubs의 기본 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="c7b95-123">이벤트 처리 확장</span><span class="sxs-lookup"><span data-stu-id="c7b95-123">Scale out event processing</span></span> 

<span data-ttu-id="c7b95-124">[이벤트 처리 확장](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) 샘플은 [이벤트 프로세서 호스트](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)를 사용하여 Event Hubs 스트림 사용 워크로드를 분산하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="c7b95-125">또한 이벤트 스트림을 관리하도록 **EventProcessor** 및 **EventProcessorFactory** 개체를 구현하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="c7b95-126">SQL의 데이터를 이벤트 허브로 끌어오기</span><span class="sxs-lookup"><span data-stu-id="c7b95-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="c7b95-127">[SQL 데이터 끌어오기](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) 샘플은 SQL 테이블의 데이터를 끌어와 이벤트 허브에 푸시하여 다운스트림 분석 응용 프로그램에 대한 입력으로 사용하도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="c7b95-128">웹 데이터를 이벤트 허브로 끌어오기</span><span class="sxs-lookup"><span data-stu-id="c7b95-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="c7b95-129">[웹에서 데이터 가져오기](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) 샘플은 공용 피드의 데이터(예: 교통 부서의 트래픽 정보 피드)를 끌어와 이벤트 허브로 푸시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b95-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7b95-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7b95-130">Next steps</span></span>

<span data-ttu-id="c7b95-131">다음 링크에서 .NET Framework 버전에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c7b95-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="c7b95-132">Frameworks 및 대상</span><span class="sxs-lookup"><span data-stu-id="c7b95-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="c7b95-133">.NET Framework 4.6 및 4.5</span><span class="sxs-lookup"><span data-stu-id="c7b95-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="c7b95-134">Event Hubs에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7b95-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="c7b95-135">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="c7b95-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="c7b95-136">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="c7b95-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="c7b95-137">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="c7b95-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)