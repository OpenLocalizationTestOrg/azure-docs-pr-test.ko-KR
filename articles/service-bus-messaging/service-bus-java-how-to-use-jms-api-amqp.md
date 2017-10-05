---
title: "Java Service Bus API와 함께 AMQP 1.0을 사용하는 방법 | Microsoft Docs"
description: "Azure 서비스 버스 및 AMQP(Advanced Message Queuing Protocol) 1.0과 함께 JMS(Java Message Service)를 사용하는 방법."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="d4331-103">서비스 버스 및 AMQP 1.0과 함께 JMS(Java Message Service) API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d4331-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="d4331-104">AMQP(Advanced Message Queuing Protocol) 1.0은 강력한 크로스 플랫폼 메시징 응용 프로그램을 빌드하는 데 사용할 수 있는 효율성과 안정성이 뛰어난 유선 수준 메시징 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="d4331-105">서비스 버스에서 AMQP 1.0이 지원되므로 효율적인 이진 프로토콜을 사용하여 다양한 플랫폼에서 큐 및 게시/구독 조정된 메시징 기능을 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="d4331-106">뿐만 아니라 여러 언어, 프레임워크 및 운영 체제가 혼합되어 사용된 구성 요소로 이루어진 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="d4331-107">이 문서에서는 널리 사용되는 JMS(Java Message Service) API 표준을 통해 Java 응용 프로그램에서 Service Bus 메시징 기능(큐 및 게시/구독 토픽)을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="d4331-108">Service Bus .NET API를 사용하여 동일한 작업을 수행하는 방법을 설명하는 [동반 문서](service-bus-amqp-dotnet.md)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="d4331-109">AMQP 1.0을 사용한 플랫폼 간 메시징에 대해 알아보려면 이 두 가지 가이드를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="d4331-110">서비스 버스 시작</span><span class="sxs-lookup"><span data-stu-id="d4331-110">Get started with Service Bus</span></span>
<span data-ttu-id="d4331-111">이 가이드에서는 사용자가 **queue1**이라는 큐가 포함된 Service Bus 네임스페이스를 이미 가지고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="d4331-112">가지고 있지 않은 사용자는 [Azure Portal](https://portal.azure.com)을 사용하여 [네임스페이스와 큐를 만들](service-bus-create-namespace-portal.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d4331-113">Service Bus 네임스페이스와 큐를 만드는 방법에 대한 자세한 내용은 [Service Bus 큐 시작](service-bus-dotnet-get-started-with-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4331-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d4331-114">분할된 큐 및 토픽은 또한 AMQP를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="d4331-115">자세한 내용은 [분할된 메시징 엔터티](service-bus-partitioning.md) 및 [Service Bus 분할 큐 및 토픽을 위한 AMQP 1.0 지원](service-bus-partitioned-queues-and-topics-amqp-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4331-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="d4331-116">AMQP 1.0 JMS 클라이언트 라이브러리 다운로드</span><span class="sxs-lookup"><span data-stu-id="d4331-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="d4331-117">최신 버전의 Apache Qpid JMS AMQP 1.0 클라이언트 라이브러리를 다운로드할 위치에 대한 자세한 내용은 [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4331-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="d4331-118">서비스 버스를 사용하여 JMS 응용 프로그램을 빌드 및 실행할 때 Apache Qpid JMS AMQP 1.0 배포 보관에 포함된 다음 JAR 파일 4개를 Java CLASSPATH에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="d4331-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="d4331-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="d4331-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="d4331-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="d4331-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="d4331-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="d4331-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="d4331-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="d4331-123">Java 응용 프로그램 코딩</span><span class="sxs-lookup"><span data-stu-id="d4331-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="d4331-124">JNDI(Java Naming and Directory Interface)</span><span class="sxs-lookup"><span data-stu-id="d4331-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="d4331-125">JMS는 JNDI(Java Naming and Directory Interface)를 사용하여 논리적 이름과 물리적 이름 간에 구분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="d4331-126">JNDI를 사용하여 두 유형의 JMS 개체인 ConnectionFactory와 Destination을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="d4331-127">JNDI는 다양한 디렉터리 서비스를 연결할 수 있는 공급자 모델을 사용하여 이름 확인 책임을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="d4331-128">Apache Qpid JMS AMQP 1.0 라이브러리에는 다음 형식의 속성 파일을 사용하여 구성된 간단한 속성 파일 기반 JNDI 공급자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="d4331-129">ConnectionFactory 구성</span><span class="sxs-lookup"><span data-stu-id="d4331-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="d4331-130">Qpid 속성 파일 JNDI 공급자에서 **ConnectionFactory**를 정의하는 데 사용되는 항목의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="d4331-131">여기서 **[jndi_name]** 및 **[ConnectionURL]**의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="d4331-132">**[jndi_name]**: ConnectionFactory의 논리적 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="d4331-133">JNDI IntialContext.lookup() 메서드를 사용하여 Java 응용 프로그램에서 확인되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="d4331-134">**[ConnectionURL]**: AMQP broker에 필요한 정보를 JMS 라이브러리에 제공하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="d4331-135">**ConnectionURL**의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="d4331-136">여기서 **[namespace]**, **[SASPolicyName]** 및 **[SASPolicyKey]**의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="d4331-137">**[namespace]**: Service Bus 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="d4331-138">**[SASPolicyName]**: 큐 공유 액세스 서명 정책 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="d4331-139">**[SASPolicyKey]**: 큐 공유 액세스 서명 정책 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="d4331-140">수동으로 암호를 URL 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="d4331-141">유용한 URL 인코딩 유틸리티는 [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="d4331-142">destination 구성</span><span class="sxs-lookup"><span data-stu-id="d4331-142">Configure destinations</span></span>
<span data-ttu-id="d4331-143">Qpid 속성 파일 JNDI 공급자에서 destination을 정의하는 데 사용되는 항목의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="d4331-144">또는</span><span class="sxs-lookup"><span data-stu-id="d4331-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="d4331-145">여기서 **[jndi\_name]**과 **[physical\_name]**의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="d4331-146">**[jndi_name]**: 대상의 논리적 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="d4331-147">JNDI IntialContext.lookup() 메서드를 사용하여 Java 응용 프로그램에서 확인되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="d4331-148">**[physical_name]**: 응용 프로그램이 메시지를 보내거나 받는 Service Bus 엔터티의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="d4331-149">서비스 버스 토픽 구독에서 받는 경우 JNDI에 지정된 물리적 이름은 토픽 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="d4331-150">구독 이름은 JMS 응용 프로그램 코드에서 지속형 구독을 만들 때 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="d4331-151">[Service Bus AMQP 1.0 개발자 가이드](service-bus-amqp-dotnet.md)에서는 JMS의 Service Bus 토픽 작업에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="d4331-152">JMS 응용 프로그램 작성</span><span class="sxs-lookup"><span data-stu-id="d4331-152">Write the JMS application</span></span>
<span data-ttu-id="d4331-153">서비스 버스와 함께 JMS를 사용할 때 필요한 특별한 API 또는 옵션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="d4331-154">하지만 나중에 다룰 몇 가지 제한은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="d4331-155">JMS 응용 프로그램과 마찬가지로 **ConnectionFactory** 및 대상을 확인하려면 먼저 JNDI 환경의 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="d4331-156">JNDI InitialContext 구성</span><span class="sxs-lookup"><span data-stu-id="d4331-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="d4331-157">JNDI 환경은 구성 정보 해시 테이블을 javax.naming.InitialContext 클래스의 생성자에 전달하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="d4331-158">해시 테이블의 두 가지 필수 요소는 초기 컨텍스트 팩터리의 클래스 이름과 공급자 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="d4331-159">다음 코드는 **servicebus.properties**라는 속성 파일과 함께 Qpid 속성 파일 기반 JNDI 공급자를 사용하도록 JNDI 환경을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="d4331-160">서비스 버스 큐를 사용하는 간단한 JMS 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d4331-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="d4331-161">다음 예제 프로그램은 JNDI 논리적 이름이 QUEUE인 서비스 버스 큐에 JMS TextMessages를 보내고 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="d4331-162">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d4331-162">Run the application</span></span>
<span data-ttu-id="d4331-163">응용 프로그램을 실행하면 양식의 출력이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="d4331-164">JMS와 .NET 간의 크로스 플랫폼 메시징</span><span class="sxs-lookup"><span data-stu-id="d4331-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="d4331-165">이 가이드에서는 JMS를 사용하여 서비스 버스로 메시지를 보내고 받는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="d4331-166">그러나 AMQP 1.0의 주요 이점 중 하나는 다른 언어로 작성된 구성 요소로 응용 프로그램을 빌드하여 안정적이며 완전히 신뢰할 수 있는 상태로 메시지를 교환할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="d4331-167">위에서 설명한 샘플 JMS 응용 프로그램 및 동반 문서([AMQP 1.0을 사용하여 .NET에서 Service Bus 사용](service-bus-amqp-dotnet.md))에서 제공하는 유사한 .NET 응용 프로그램을 사용하여 .NET과 Java 간에 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="d4331-168">Service Bus 및 AMQP 1.0을 사용하는 크로스 플랫폼 메시징에 대한 자세한 내용은 이 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4331-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="d4331-169">JMS에서 .NET으로</span><span class="sxs-lookup"><span data-stu-id="d4331-169">JMS to .NET</span></span>
<span data-ttu-id="d4331-170">JMS에서 .NET으로의 메시징을 시연하려면:</span><span class="sxs-lookup"><span data-stu-id="d4331-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="d4331-171">명령줄 인수 없이 .NET 샘플 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="d4331-172">"sendonly" 명령줄 인수로 Java 샘플 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="d4331-173">이 모드에서는 응용 프로그램이 큐에서 메시지를 받지 않고 보내기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="d4331-174">Java 응용 프로그램 콘솔에서 **Enter** 키를 몇 번 누릅니다. 그러면 메시지가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="d4331-175">.NET 응용 프로그램에서 이러한 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="d4331-176">JMS 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="d4331-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="d4331-177">.NET 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="d4331-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="d4331-178">.NET에서 JMS로</span><span class="sxs-lookup"><span data-stu-id="d4331-178">.NET to JMS</span></span>
<span data-ttu-id="d4331-179">.NET에서 JMS로의 메시징을 시연하려면:</span><span class="sxs-lookup"><span data-stu-id="d4331-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="d4331-180">"sendonly" 명령줄 인수로 .NET 샘플 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="d4331-181">이 모드에서는 응용 프로그램이 큐에서 메시지를 받지 않고 보내기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="d4331-182">명령줄 인수 없이 Java 샘플 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="d4331-183">.NET 응용 프로그램 콘솔에서 **Enter** 키를 몇 번 누릅니다. 그러면 메시지가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="d4331-184">Java 응용 프로그램에서 이러한 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="d4331-185">.NET 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="d4331-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="d4331-186">JMS 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="d4331-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="d4331-187">지원되지 않는 기능 및 제한</span><span class="sxs-lookup"><span data-stu-id="d4331-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="d4331-188">서비스 버스와 함께 JMS over AMQP 1.0을 사용하는 경우 다음과 같은 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="d4331-189">**세션**당 하나의 **MessageProducer** 또는 **MessageConsumer**만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="d4331-190">응용 프로그램에서 **MessageProducers** 또는 **MessageConsumers**를 여러 개 만들어야 하는 경우 각 항목에 대한 전용 **세션**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="d4331-191">휘발성 토픽 구독은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="d4331-192">**MessageSelectors**는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="d4331-193">예를 들어, 임시 대상인 **TemporaryQueue**, **TemporaryTopic**과 이러한 대상을 사용하는 **QueueRequestor** 및 **TopicRequestor** API는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="d4331-194">트랜잭션 처리된 세션과 분산 트랜잭션은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="d4331-195">요약</span><span class="sxs-lookup"><span data-stu-id="d4331-195">Summary</span></span>
<span data-ttu-id="d4331-196">이 방법 가이드에서는 널리 사용되는 JMS API 및 AMQP 1.0을 통해 Java에서 Service Bus 조정된 메시징 기능(큐 및 게시/구독 토픽)에 액세스하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="d4331-197">.NET, C, Python, PHP 등의 다른 언어에서도 Service Bus AMQP 1.0을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="d4331-198">이러한 언어로 빌드한 구성 요소는 서비스 버스의 AMQP 1.0 지원을 사용하여 안정적이며 완전히 신뢰할 수 있는 상태로 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4331-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4331-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4331-199">Next steps</span></span>
* [<span data-ttu-id="d4331-200">Azure Service Bus의 AMQP 1.0 지원</span><span class="sxs-lookup"><span data-stu-id="d4331-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="d4331-201">Service Bus .NET API와 함께 AMQP 1.0을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d4331-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="d4331-202">Service Bus AMQP 1.0 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="d4331-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="d4331-203">Service Bus 큐 시작</span><span class="sxs-lookup"><span data-stu-id="d4331-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="d4331-204">Java 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="d4331-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

