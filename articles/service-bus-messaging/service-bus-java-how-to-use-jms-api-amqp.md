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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="0c218-103">어떻게 toouse hello 메시지 JMS (Java Service) API와 서비스 버스에서 AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="0c218-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="0c218-104">hello 고급 메시지 큐 (AMQP Protocol) 1.0은는 효율적이 고 신뢰할 수 있는 유선 수준 메시징 프로토콜 toobuild 강력한 크로스 플랫폼 메시징 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="0c218-105">사용할 수 있는 수단 hello 큐 및 게시/구독 조정 된 메시징 기능 효율적인 이진 프로토콜을 사용 하 여 플랫폼의 범위에서 서비스 버스에서 AMQP 1.0을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="0c218-106">뿐만 아니라 여러 언어, 프레임워크 및 운영 체제가 혼합되어 사용된 구성 요소로 이루어진 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="0c218-107">이 문서에서는 toouse 서비스 버스 메시징 기능 (큐 및 게시/구독 항목)를 사용 하 여 Java 응용 프로그램에서 인기 있는 서비스 JMS (Java Message) 표준 API hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="0c218-108">한 [관련 문서](service-bus-amqp-dotnet.md) toodo hello hello 서비스 버스.NET API를 사용 하 여 동일한 방법을 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="0c218-109">AMQP 1.0을 사용 하 여 플랫폼 간 메시징에 대 한 이러한 두 가이드 함께 toolearn를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="0c218-110">서비스 버스 시작</span><span class="sxs-lookup"><span data-stu-id="0c218-110">Get started with Service Bus</span></span>
<span data-ttu-id="0c218-111">이 가이드에서는 사용자가 **queue1**이라는 큐가 포함된 Service Bus 네임스페이스를 이미 가지고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="0c218-112">그렇지 않고 경우 할 수 있습니다 [hello 네임 스페이스를 만들고 큐](service-bus-create-namespace-portal.md) hello를 사용 하 여 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c218-113">Toocreate 서비스 버스 네임 스페이스, 큐의 참조 하는 방법에 대 한 자세한 내용은 [서비스 버스 큐 시작](service-bus-dotnet-get-started-with-queues.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0c218-114">분할된 큐 및 토픽은 또한 AMQP를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="0c218-115">자세한 내용은 [분할된 메시징 엔터티](service-bus-partitioning.md) 및 [Service Bus 분할 큐 및 토픽을 위한 AMQP 1.0 지원](service-bus-partitioned-queues-and-topics-amqp-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c218-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="0c218-116">Hello AMQP 1.0 JMS 클라이언트 라이브러리 다운로드</span><span class="sxs-lookup"><span data-stu-id="0c218-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="0c218-117">여기서 toodownload hello hello Apache Qpid JMS AMQP 1.0 클라이언트 라이브러리의 최신 버전에 대 한 내용은 방문 [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="0c218-118">서비스 버스를 통해 JMS 응용 프로그램을 실행할 때 hello Apache Qpid JMS AMQP 1.0 배포 보관 toohello Java CLASSPATH에서에서 네 개의 JAR 파일을 다음 hello를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="0c218-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="0c218-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="0c218-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="0c218-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="0c218-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="0c218-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="0c218-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="0c218-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="0c218-123">Java 응용 프로그램 코딩</span><span class="sxs-lookup"><span data-stu-id="0c218-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="0c218-124">JNDI(Java Naming and Directory Interface)</span><span class="sxs-lookup"><span data-stu-id="0c218-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="0c218-125">JMS는 hello Java Naming and Directory 인터페이스 (JNDI) toocreate 논리적 이름과 실제 이름을 구분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="0c218-126">JNDI를 사용하여 두 유형의 JMS 개체인 ConnectionFactory와 Destination을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="0c218-127">JNDI는 공급자 모델을 다른 디렉터리 서비스 toohandle 이름 확인 작업을 연결할 수 있습니다를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="0c218-128">hello Apache Qpid JMS AMQP 1.0 라이브러리는 간단한 속성와 함께 제공 hello 다음의 속성 파일을 사용 하 여 구성 된 파일 기반 JNDI 공급자 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="0c218-129">ConnectionFactory hello 구성</span><span class="sxs-lookup"><span data-stu-id="0c218-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="0c218-130">사용 되는 항목 toodefine hello는 **ConnectionFactory** 에서 hello Qpid 속성 파일 JNDI 공급자는 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="0c218-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="0c218-131">여기서 **[jndi_name]** 및 **[ConnectionURL]** hello 의미를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="0c218-132">**[jndi_name]** : hello hello ConnectionFactory의 논리적 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="0c218-133">이 hello 이름 hello JNDI intialcontext.lookup () 메서드를 사용 하 여 hello Java 응용 프로그램에서 해결 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="0c218-134">**[ConnectionURL]** : Hello 정보로 hello JMS 라이브러리를 제공 하는 URL toohello AMQP 브로커 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="0c218-135">hello 형식의 hello **ConnectionURL** 는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="0c218-136">여기서 **[namespace]**, **[SASPolicyName]** 및 **[SASPolicyKey]** hello 따라 의미 있는:</span><span class="sxs-lookup"><span data-stu-id="0c218-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="0c218-137">**[namespace]** : hello 서비스 버스 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="0c218-138">**[SASPolicyName]** : hello 큐 공유 액세스 서명 정책 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="0c218-139">**[SASPolicyKey]** : hello 큐 공유 액세스 서명 정책 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="0c218-140">수동으로 URL로 인코드할 hello 암호 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="0c218-141">유용한 URL 인코딩 유틸리티는 [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="0c218-142">destination 구성</span><span class="sxs-lookup"><span data-stu-id="0c218-142">Configure destinations</span></span>
<span data-ttu-id="0c218-143">형식에 따라 hello hello Qpid 속성 파일 JNDI 공급자에서 대상이 사용 되는 항목 toodefine hello:</span><span class="sxs-lookup"><span data-stu-id="0c218-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="0c218-144">또는</span><span class="sxs-lookup"><span data-stu-id="0c218-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="0c218-145">여기서 **[jndi\_이름]** 및 **[물리적\_이름]** hello 따라 의미 있는:</span><span class="sxs-lookup"><span data-stu-id="0c218-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="0c218-146">**[jndi_name]** : hello hello 대상의 논리적 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="0c218-147">이 hello 이름 hello JNDI intialcontext.lookup () 메서드를 사용 하 여 hello Java 응용 프로그램에서 해결 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="0c218-148">**[physical_name]** : hello 서비스 버스 엔터티 toowhich hello 응용 프로그램의 hello 이름 보내거나 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="0c218-149">서비스 버스 항목 구독에서를 받을 때 JNDI에 지정 된 hello 물리적 이름에는 hello 항목의 hello 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="0c218-150">hello 구독 이름은 JMS 응용 프로그램 코드 hello에서 hello 지속적인 구독을 만들 때 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="0c218-151">hello [서비스 버스 AMQP 1.0 개발자 가이드](service-bus-amqp-dotnet.md) 작업 JMS에서 서비스 버스 항목에 자세한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="0c218-152">Hello JMS 응용 프로그램 작성</span><span class="sxs-lookup"><span data-stu-id="0c218-152">Write hello JMS application</span></span>
<span data-ttu-id="0c218-153">서비스 버스와 함께 JMS를 사용할 때 필요한 특별한 API 또는 옵션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="0c218-154">하지만 나중에 다룰 몇 가지 제한은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="0c218-155">모든 JMS 응용 프로그램에서는 hello 필요한 것은 toobe 수 tooresolve hello JNDI 환경의 구성을 **ConnectionFactory** 및 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="0c218-156">JNDI InitialContext hello 구성</span><span class="sxs-lookup"><span data-stu-id="0c218-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="0c218-157">hello JNDI 환경 구성 정보의 hashtable hello hello javax.naming.InitialContext 클래스 생성자에 전달 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="0c218-158">hello 해시 테이블에 있는 두 개의 필수 요소 hello hello 초기 컨텍스트 팩터리 hello 클래스 이름과 hello 공급자 URL 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="0c218-159">hello 다음 코드를 보여 줍니다 tooconfigure hello JNDI 환경 toouse hello Qpid 속성 파일 이름이 속성 파일 JNDI 공급자에 기반 하는 방법을 **servicebus.properties**합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="0c218-160">서비스 버스 큐를 사용하는 간단한 JMS 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0c218-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="0c218-161">hello 다음 예제 프로그램 JMS TextMessages tooa 서비스 버스 큐 hello JNDI 큐의 논리적 이름으로 보내고 다시 hello 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="0c218-162">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="0c218-162">Run hello application</span></span>
<span data-ttu-id="0c218-163">Hello 응용 프로그램을 실행 hello 폼의 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="0c218-164">JMS와 .NET 간의 크로스 플랫폼 메시징</span><span class="sxs-lookup"><span data-stu-id="0c218-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="0c218-165">이 가이드 방법을 배웠습니다 toosend 메시지 tooand JMS를 사용 하 여 서비스 버스에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="0c218-166">그러나 hello AMQP 1.0의 주요 이점 중 하나 안정적이 고를 완전 하 게 교환 되는 메시지와 다른 언어로 작성 된 구성 요소에서 작성 된 응용 프로그램 toobe 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="0c218-167">위에서 설명한 hello 샘플 JMS 응용 프로그램과 관련 문서에서 가져온 유사한.NET 응용 프로그램을 사용 하 여 [AMQP 1.0과 함께.NET에서 서비스 버스를 사용 하 여](service-bus-amqp-dotnet.md),.NET 및 Java 간에 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="0c218-168">서비스 버스에서 AMQP 1.0을 사용 하 여 메시징 플랫폼의 hello 세부 정보에 대 한 자세한 내용은이 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="0c218-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="0c218-169">JMS too.NET</span></span>
<span data-ttu-id="0c218-170">toodemonstrate JMS too.NET 메시징:</span><span class="sxs-lookup"><span data-stu-id="0c218-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="0c218-171">명령줄 인수 없이 hello.NET 예제 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="0c218-172">Hello "sendonly" 명령줄 인수로 hello Java 예제 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="0c218-173">이 모드에서는 hello 응용 프로그램 hello 큐에서 메시지를 받지 것입니다만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="0c218-174">키를 눌러 **Enter** 를 몇 번 hello Java 응용 프로그램 콘솔에서 발생 메시지 toobe 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="0c218-175">이러한 메시지는 hello.NET 응용 프로그램에서 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="0c218-176">JMS 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="0c218-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="0c218-177">.NET 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="0c218-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="0c218-178">.NET tooJMS</span><span class="sxs-lookup"><span data-stu-id="0c218-178">.NET tooJMS</span></span>
<span data-ttu-id="0c218-179">toodemonstrate.NET tooJMS 메시징:</span><span class="sxs-lookup"><span data-stu-id="0c218-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="0c218-180">Hello "sendonly" 명령줄 인수로 hello.NET 예제 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="0c218-181">이 모드에서는 hello 응용 프로그램 hello 큐에서 메시지를 받지 것입니다만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="0c218-182">명령줄 인수 없이 hello Java 예제 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="0c218-183">키를 눌러 **Enter** 를 몇 번 hello.NET 응용 프로그램 콘솔에서 발생 메시지 toobe 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="0c218-184">이러한 메시지는 hello Java 응용 프로그램에서 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="0c218-185">.NET 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="0c218-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="0c218-186">JMS 응용 프로그램의 출력</span><span class="sxs-lookup"><span data-stu-id="0c218-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="0c218-187">지원되지 않는 기능 및 제한</span><span class="sxs-lookup"><span data-stu-id="0c218-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="0c218-188">제한 사항에 따라 hello 즉 Service bus AMQP 1.0을 통해 JMS를 사용 하는 경우 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="0c218-189">**세션**당 하나의 **MessageProducer** 또는 **MessageConsumer**만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="0c218-190">Toocreate 해야 할 경우 여러 **MessageProducers** 또는 **MessageConsumers** 응용 프로그램을 만들 전용 **세션** 채 각 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="0c218-191">휘발성 토픽 구독은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="0c218-192">**MessageSelectors**는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="0c218-193">임시 대상을; 예를 들어 **TemporaryQueue**, **TemporaryTopic** 현재 지원 되지 않는, hello 함께 **QueueRequestor** 및 **TopicRequestor**을 사용 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="0c218-194">트랜잭션 처리된 세션과 분산 트랜잭션은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="0c218-195">요약</span><span class="sxs-lookup"><span data-stu-id="0c218-195">Summary</span></span>
<span data-ttu-id="0c218-196">이 방법 tooguide 인기 있는 JMS API 및 AMQP 1.0 toouse 서비스 버스 조정 된 메시징 기능 (큐 및 게시/구독 항목)에서 Java를 사용 하 여 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="0c218-197">.NET, C, Python, PHP 등의 다른 언어에서도 Service Bus AMQP 1.0을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="0c218-198">이러한 다른 언어를 사용 하 여 구축 된 구성 요소를 서비스 버스에서 AMQP 1.0 hello 지원을 사용 하 여 완전 하 게 하 고 안정적으로 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c218-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c218-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c218-199">Next steps</span></span>
* [<span data-ttu-id="0c218-200">Azure Service Bus의 AMQP 1.0 지원</span><span class="sxs-lookup"><span data-stu-id="0c218-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="0c218-201">AMQP 1.0 toouse와 서비스 버스.NET API hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0c218-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="0c218-202">Service Bus AMQP 1.0 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="0c218-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="0c218-203">Service Bus 큐 시작</span><span class="sxs-lookup"><span data-stu-id="0c218-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="0c218-204">Java 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="0c218-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

