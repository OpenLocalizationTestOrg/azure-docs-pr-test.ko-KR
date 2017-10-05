---
title: "Java를 사용하여 Azure Event Hubs로 이벤트 전송 | Microsoft Docs"
description: "Java를 사용하여 Event Hubs로 전송 시작"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b31771001989e20b88bc8d7bca1afceb58ec197c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="107ee-103">Java를 사용하여 Azure Event Hubs로 이벤트 전송</span><span class="sxs-lookup"><span data-stu-id="107ee-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="107ee-104">소개</span><span class="sxs-lookup"><span data-stu-id="107ee-104">Introduction</span></span>
<span data-ttu-id="107ee-105">Event Hubs는 연결된 장치와 응용 프로그램에서 생성되는 엄청난 양의 데이터를 처리 및 분석할 수 있도록 초당 수백만 개의 이벤트를 수용할 수 있는 확장성이 뛰어난 수집 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="107ee-106">이벤트 허브로 수집된 데이터는 실시간 분석 공급자나 저장소 클러스터를 사용하여 변환하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="107ee-107">자세한 내용은 [이벤트 허브 개요][Event Hubs overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="107ee-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="107ee-108">이 자습서에서는 Java 언어의 콘솔 응용 프로그램을 사용하여 이벤트 허브로 이벤트를 전송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="107ee-109">Java 이벤트 프로세스 호스트 라이브러리를 사용하여 이벤트를 수신하려면 [이 문서](event-hubs-java-get-started-receive-eph.md)를 참조하거나 목차 왼쪽에서 해당하는 수신 언어를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="107ee-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="107ee-111">Java 개발 환경.</span><span class="sxs-lookup"><span data-stu-id="107ee-111">A Java development environment.</span></span> <span data-ttu-id="107ee-112">이 자습서에서는 [Eclipse](https://www.eclipse.org/)를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="107ee-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="107ee-113">An active Azure account.</span></span> <br/><span data-ttu-id="107ee-114">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="107ee-115">자세한 내용은 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 무료 체험</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="107ee-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="107ee-116">이벤트 허브에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="107ee-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="107ee-117">Event Hubs에 대한 Java 클라이언트 라이브러리는 [Maven 중앙 리포지토리](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)에서 Maven 프로젝트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="107ee-118">Maven 프로젝트 파일 안에 다음 종속성 선언을 사용하여 이 라이브러리를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-118">You can reference this library using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="107ee-119">다양한 형식의 빌드 환경을 위해, [Maven 중앙 리포지토리](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)에서 최근에 릴리스된 JAR 파일을 명시적으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-119">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="107ee-120">단순 이벤트 게시자의 경우 이벤트 허브 클라이언트 클래스에 대한 *com.microsoft.azure.eventhubs* 패키지와 유틸리티 클래스(예: Azure Service Bus 메시징 클라이언트와 공유되는 일반적인 예외)에 대한 *com.microsoft.azure.servicebus* 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-120">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="107ee-121">다음 샘플에서는 먼저 즐겨 찾는 Java 개발 환경에서 콘솔/셸 응용 프로그램에 대한 새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-121">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="107ee-122">클래스 `Send` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-122">Name the class `Send`.</span></span>     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

<span data-ttu-id="107ee-123">네임스페이스 및 이벤트 허브 이름을 이벤트 허브를 만들 때 사용한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-123">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="107ee-124">그런 다음, 문자열을 UTF-8 바이트 인코딩으로 전환하여 단일 이벤트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="107ee-125">그런 다음, 연결 문자열에서 새 Event Hubs 클라이언트 인스턴스를 만들고 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="107ee-125">Then, create a new Event Hubs client instance from the connection string and send the message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="107ee-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="107ee-126">Next steps</span></span>
<span data-ttu-id="107ee-127">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="107ee-127">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="107ee-128">를 사용하여 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="107ee-128">Receive events using the EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="107ee-129">[Event Hubs 개요][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="107ee-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="107ee-130">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="107ee-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="107ee-131">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="107ee-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md