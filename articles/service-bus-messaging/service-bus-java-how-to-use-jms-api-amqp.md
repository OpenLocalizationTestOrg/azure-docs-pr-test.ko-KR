---
title: "Java 서비스 버스 API hello로 aaaHow toouse AMQP 1.0 | Microsoft Docs"
description: "어떻게 toouse hello 서비스 JMS (Java Message) Azure 서비스 버스와 메시지 큐 Protodol AMQP (Advanced) 1.0입니다."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>어떻게 toouse hello 메시지 JMS (Java Service) API와 서비스 버스에서 AMQP 1.0
hello 고급 메시지 큐 (AMQP Protocol) 1.0은는 효율적이 고 신뢰할 수 있는 유선 수준 메시징 프로토콜 toobuild 강력한 크로스 플랫폼 메시징 응용 프로그램을 사용할 수 있습니다.

사용할 수 있는 수단 hello 큐 및 게시/구독 조정 된 메시징 기능 효율적인 이진 프로토콜을 사용 하 여 플랫폼의 범위에서 서비스 버스에서 AMQP 1.0을 지원 합니다. 뿐만 아니라 여러 언어, 프레임워크 및 운영 체제가 혼합되어 사용된 구성 요소로 이루어진 응용 프로그램을 만들 수 있습니다.

이 문서에서는 toouse 서비스 버스 메시징 기능 (큐 및 게시/구독 항목)를 사용 하 여 Java 응용 프로그램에서 인기 있는 서비스 JMS (Java Message) 표준 API hello 하는 방법을 설명 합니다. 한 [관련 문서](service-bus-amqp-dotnet.md) toodo hello hello 서비스 버스.NET API를 사용 하 여 동일한 방법을 설명 하는 합니다. AMQP 1.0을 사용 하 여 플랫폼 간 메시징에 대 한 이러한 두 가이드 함께 toolearn를 사용할 수 있습니다.

## <a name="get-started-with-service-bus"></a>서비스 버스 시작
이 가이드에서는 사용자가 **queue1**이라는 큐가 포함된 Service Bus 네임스페이스를 이미 가지고 있다고 가정합니다. 그렇지 않고 경우 할 수 있습니다 [hello 네임 스페이스를 만들고 큐](service-bus-create-namespace-portal.md) hello를 사용 하 여 [Azure 포털](https://portal.azure.com)합니다. Toocreate 서비스 버스 네임 스페이스, 큐의 참조 하는 방법에 대 한 자세한 내용은 [서비스 버스 큐 시작](service-bus-dotnet-get-started-with-queues.md)합니다.

> [!NOTE]
> 분할된 큐 및 토픽은 또한 AMQP를 지원합니다. 자세한 내용은 [분할된 메시징 엔터티](service-bus-partitioning.md) 및 [Service Bus 분할 큐 및 토픽을 위한 AMQP 1.0 지원](service-bus-partitioned-queues-and-topics-amqp-overview.md)을 참조하세요.
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Hello AMQP 1.0 JMS 클라이언트 라이브러리 다운로드
여기서 toodownload hello hello Apache Qpid JMS AMQP 1.0 클라이언트 라이브러리의 최신 버전에 대 한 내용은 방문 [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html)합니다.

서비스 버스를 통해 JMS 응용 프로그램을 실행할 때 hello Apache Qpid JMS AMQP 1.0 배포 보관 toohello Java CLASSPATH에서에서 네 개의 JAR 파일을 다음 hello를 추가 해야 합니다.

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>Java 응용 프로그램 코딩
### <a name="java-naming-and-directory-interface-jndi"></a>JNDI(Java Naming and Directory Interface)
JMS는 hello Java Naming and Directory 인터페이스 (JNDI) toocreate 논리적 이름과 실제 이름을 구분을 사용합니다. JNDI를 사용하여 두 유형의 JMS 개체인 ConnectionFactory와 Destination을 확인합니다. JNDI는 공급자 모델을 다른 디렉터리 서비스 toohandle 이름 확인 작업을 연결할 수 있습니다를 사용 합니다. hello Apache Qpid JMS AMQP 1.0 라이브러리는 간단한 속성와 함께 제공 hello 다음의 속성 파일을 사용 하 여 구성 된 파일 기반 JNDI 공급자 서식을 지정 합니다.

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>ConnectionFactory hello 구성
사용 되는 항목 toodefine hello는 **ConnectionFactory** 에서 hello Qpid 속성 파일 JNDI 공급자는 형식에 따라 hello:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

여기서 **[jndi_name]** 및 **[ConnectionURL]** hello 의미를 수행 했습니다.

* **[jndi_name]** : hello hello ConnectionFactory의 논리적 이름입니다. 이 hello 이름 hello JNDI intialcontext.lookup () 메서드를 사용 하 여 hello Java 응용 프로그램에서 해결 될 것입니다.
* **[ConnectionURL]** : Hello 정보로 hello JMS 라이브러리를 제공 하는 URL toohello AMQP 브로커 필요 합니다.

hello 형식의 hello **ConnectionURL** 는 다음과 같습니다.

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
여기서 **[namespace]**, **[SASPolicyName]** 및 **[SASPolicyKey]** hello 따라 의미 있는:

* **[namespace]** : hello 서비스 버스 네임 스페이스입니다.
* **[SASPolicyName]** : hello 큐 공유 액세스 서명 정책 이름입니다.
* **[SASPolicyKey]** : hello 큐 공유 액세스 서명 정책 키입니다.

> [!NOTE]
> 수동으로 URL로 인코드할 hello 암호 실행 해야 합니다. 유용한 URL 인코딩 유틸리티는 [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp)에서 사용할 수 있습니다.
> 
> 

#### <a name="configure-destinations"></a>destination 구성
형식에 따라 hello hello Qpid 속성 파일 JNDI 공급자에서 대상이 사용 되는 항목 toodefine hello:

```
queue.[jndi_name] = [physical_name]
```

또는

```
topic.[jndi_name] = [physical_name]
```

여기서 **[jndi\_이름]** 및 **[물리적\_이름]** hello 따라 의미 있는:

* **[jndi_name]** : hello hello 대상의 논리적 이름입니다. 이 hello 이름 hello JNDI intialcontext.lookup () 메서드를 사용 하 여 hello Java 응용 프로그램에서 해결 될 것입니다.
* **[physical_name]** : hello 서비스 버스 엔터티 toowhich hello 응용 프로그램의 hello 이름 보내거나 메시지를 수신 합니다.

> [!NOTE]
> 서비스 버스 항목 구독에서를 받을 때 JNDI에 지정 된 hello 물리적 이름에는 hello 항목의 hello 이름 이어야 합니다. hello 구독 이름은 JMS 응용 프로그램 코드 hello에서 hello 지속적인 구독을 만들 때 제공 됩니다. hello [서비스 버스 AMQP 1.0 개발자 가이드](service-bus-amqp-dotnet.md) 작업 JMS에서 서비스 버스 항목에 자세한 세부 정보를 제공 합니다.
> 
> 

### <a name="write-hello-jms-application"></a>Hello JMS 응용 프로그램 작성
서비스 버스와 함께 JMS를 사용할 때 필요한 특별한 API 또는 옵션은 없습니다. 하지만 나중에 다룰 몇 가지 제한은 있습니다. 모든 JMS 응용 프로그램에서는 hello 필요한 것은 toobe 수 tooresolve hello JNDI 환경의 구성을 **ConnectionFactory** 및 대상입니다.

#### <a name="configure-hello-jndi-initialcontext"></a>JNDI InitialContext hello 구성
hello JNDI 환경 구성 정보의 hashtable hello hello javax.naming.InitialContext 클래스 생성자에 전달 하 여 구성 됩니다. hello 해시 테이블에 있는 두 개의 필수 요소 hello hello 초기 컨텍스트 팩터리 hello 클래스 이름과 hello 공급자 URL 됩니다. hello 다음 코드를 보여 줍니다 tooconfigure hello JNDI 환경 toouse hello Qpid 속성 파일 이름이 속성 파일 JNDI 공급자에 기반 하는 방법을 **servicebus.properties**합니다.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>서비스 버스 큐를 사용하는 간단한 JMS 응용 프로그램
hello 다음 예제 프로그램 JMS TextMessages tooa 서비스 버스 큐 hello JNDI 큐의 논리적 이름으로 보내고 다시 hello 메시지를 수신 합니다.

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>Hello 응용 프로그램 실행
Hello 응용 프로그램을 실행 hello 폼의 출력을 생성 합니다.

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>JMS와 .NET 간의 크로스 플랫폼 메시징
이 가이드 방법을 배웠습니다 toosend 메시지 tooand JMS를 사용 하 여 서비스 버스에서 수신 합니다. 그러나 hello AMQP 1.0의 주요 이점 중 하나 안정적이 고를 완전 하 게 교환 되는 메시지와 다른 언어로 작성 된 구성 요소에서 작성 된 응용 프로그램 toobe 수 있다는 것입니다.

위에서 설명한 hello 샘플 JMS 응용 프로그램과 관련 문서에서 가져온 유사한.NET 응용 프로그램을 사용 하 여 [AMQP 1.0과 함께.NET에서 서비스 버스를 사용 하 여](service-bus-amqp-dotnet.md),.NET 및 Java 간에 메시지를 교환할 수 있습니다. 서비스 버스에서 AMQP 1.0을 사용 하 여 메시징 플랫폼의 hello 세부 정보에 대 한 자세한 내용은이 문서를 참조 합니다.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET 메시징:

* 명령줄 인수 없이 hello.NET 예제 응용 프로그램을 시작 합니다.
* Hello "sendonly" 명령줄 인수로 hello Java 예제 응용 프로그램을 시작 합니다. 이 모드에서는 hello 응용 프로그램 hello 큐에서 메시지를 받지 것입니다만 전송 합니다.
* 키를 눌러 **Enter** 를 몇 번 hello Java 응용 프로그램 콘솔에서 발생 메시지 toobe 전송 합니다.
* 이러한 메시지는 hello.NET 응용 프로그램에서 수신 됩니다.

#### <a name="output-from-jms-application"></a>JMS 응용 프로그램의 출력
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>.NET 응용 프로그램의 출력
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET tooJMS
toodemonstrate.NET tooJMS 메시징:

* Hello "sendonly" 명령줄 인수로 hello.NET 예제 응용 프로그램을 시작 합니다. 이 모드에서는 hello 응용 프로그램 hello 큐에서 메시지를 받지 것입니다만 전송 합니다.
* 명령줄 인수 없이 hello Java 예제 응용 프로그램을 시작 합니다.
* 키를 눌러 **Enter** 를 몇 번 hello.NET 응용 프로그램 콘솔에서 발생 메시지 toobe 전송 합니다.
* 이러한 메시지는 hello Java 응용 프로그램에서 수신 됩니다.

#### <a name="output-from-net-application"></a>.NET 응용 프로그램의 출력
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>JMS 응용 프로그램의 출력
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>지원되지 않는 기능 및 제한
제한 사항에 따라 hello 즉 Service bus AMQP 1.0을 통해 JMS를 사용 하는 경우 존재 합니다.

* **세션**당 하나의 **MessageProducer** 또는 **MessageConsumer**만 허용됩니다. Toocreate 해야 할 경우 여러 **MessageProducers** 또는 **MessageConsumers** 응용 프로그램을 만들 전용 **세션** 채 각 항목에 대 한 합니다.
* 휘발성 토픽 구독은 현재 지원되지 않습니다.
* **MessageSelectors**는 현재 지원되지 않습니다.
* 임시 대상을; 예를 들어 **TemporaryQueue**, **TemporaryTopic** 현재 지원 되지 않는, hello 함께 **QueueRequestor** 및 **TopicRequestor**을 사용 하는 Api입니다.
* 트랜잭션 처리된 세션과 분산 트랜잭션은 지원되지 않습니다.

## <a name="summary"></a>요약
이 방법 tooguide 인기 있는 JMS API 및 AMQP 1.0 toouse 서비스 버스 조정 된 메시징 기능 (큐 및 게시/구독 항목)에서 Java를 사용 하 여 hello 하는 방법을 배웠습니다.

.NET, C, Python, PHP 등의 다른 언어에서도 Service Bus AMQP 1.0을 사용할 수 있습니다. 이러한 다른 언어를 사용 하 여 구축 된 구성 요소를 서비스 버스에서 AMQP 1.0 hello 지원을 사용 하 여 완전 하 게 하 고 안정적으로 메시지를 교환할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Azure Service Bus의 AMQP 1.0 지원](service-bus-amqp-overview.md)
* [AMQP 1.0 toouse와 서비스 버스.NET API hello 하는 방법](service-bus-dotnet-advanced-message-queuing.md)
* [Service Bus AMQP 1.0 개발자 가이드](service-bus-amqp-dotnet.md)
* [Service Bus 큐 시작](service-bus-dotnet-get-started-with-queues.md)
* [Java 개발자 센터](https://azure.microsoft.com/develop/java/)

