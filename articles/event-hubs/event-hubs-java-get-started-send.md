---
title: "이벤트 허브 aaaSend 이벤트 tooAzure Java를 사용 하 여 | Microsoft Docs"
description: "Java를 사용 하 여 tooEvent 허브 전송 시작"
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
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a>Java를 사용 하 여 tooAzure 이벤트 허브 이벤트를 전송 합니다.

## <a name="introduction"></a>소개
이벤트 허브는 수백만 개의 초당 응용 프로그램 tooprocess 활성화 이벤트를 수집 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있는 확장성이 높은 수집 시스템. 이벤트 허브로 수집된 데이터는 실시간 분석 공급자나 저장소 클러스터를 사용하여 변환하고 저장할 수 있습니다.

자세한 내용은 참조 hello [이벤트 허브 개요][Event Hubs overview]합니다.

이 자습서에서는 어떻게 toosend 이벤트 tooan 이벤트 허브는 콘솔 응용 프로그램에서 Java 사용 하 여 합니다. hello Java 이벤트 프로세서 호스트 라이브러리를 사용 하 여 tooreceive 이벤트 참조 [이 문서](event-hubs-java-get-started-receive-eph.md), 또는 hello hello 내용의 왼쪽 테이블에서 적절 한 받는 언어를 선택 합니다.

에 순서 toocomplete이이 자습서에서는 해야 하는 다음 hello:

* Java 개발 환경. 이 자습서에서는 [Eclipse](https://www.eclipse.org/)를 사용한다고 가정합니다.
* 활성 Azure 계정. <br/>계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다. 자세한 내용은 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 무료 체험</a>을 참조하세요.

## <a name="send-messages-tooevent-hubs"></a>TooEvent 허브 메시지 보내기
hello 이벤트 허브에 대 한 Java 클라이언트 라이브러리는 hello에서 Maven 프로젝트에서 사용할 수 있는 [Maven 중앙 리포지토리에](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)합니다. Maven 프로젝트 파일 안에 종속성 선언 뒤 hello를 사용 하 여이 라이브러리를 참조할 수 있습니다.    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

빌드 환경, 다양 한 유형의 얻을 수 있습니다 명시적으로 릴리스된 최신 hello JAR 파일에서 hello [Maven 중앙 리포지토리에](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)합니다.  

단순 이벤트 게시자에 대 한 hello 가져올 *com.microsoft.azure.eventhubs* hello 이벤트 허브 클라이언트 클래스 및 hello에 대 한 패키지 *com.microsoft.azure.servicebus* 등 유틸리티 클래스에 대 한 패키지 hello Azure 서비스 버스 메시징 클라이언트와 공유 되는 일반적인 예외 

다음 예제는 hello에 대 한 먼저 즐겨 찾는 Java 개발 환경에서 콘솔/셸 응용 프로그램에 대 한 새 Maven 프로젝트를 만듭니다. Hello 클래스 이름을 `Send`합니다.     

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

Hello 네임 스페이스 및 이벤트 허브 이름을 hello 이벤트 허브를 만들 때 사용 되는 hello 값으로 대체 합니다.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

그런 다음, 문자열을 UTF-8 바이트 인코딩으로 전환하여 단일 이벤트를 만듭니다. 그런 다음 새 이벤트 허브 클라이언트 인스턴스를 hello 연결 문자열에서 만들고 hello 메시지를 보냅니다.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [EventProcessorHost hello를 사용 하 여 이벤트를 수신 합니다.](event-hubs-java-get-started-receive-eph.md)
* [Event Hubs 개요][Event Hubs overview]
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md