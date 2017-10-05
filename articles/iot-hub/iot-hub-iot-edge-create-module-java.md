---
title: "Java를 사용하여 Azure IoT Edge 모듈 만들기 | Microsoft Docs"
description: "이 자습서에서는 최신 Azure IoT Edge Maven 패키지를 사용하여 BLE 데이터 변환기 모듈을 작성하는 방법을 소개합니다."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: 0c430272225d79737baec2be15ed7c93991cdeac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="5236b-103">Java를 사용하여 Azure IoT Edge 모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="5236b-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="5236b-104">이 자습서는 Java에서 Azure IoT Edge에 대한 모듈을 빌드하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="5236b-105">이 자습서에서는 최신 Azure IoT Edge Maven 패키지를 사용하여 환경 설정 및 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 데이터 변환기 모듈을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-105">In this tutorial, we will walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5236b-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5236b-106">Prerequisites</span></span>

<span data-ttu-id="5236b-107">이 섹션에서는 IoT Edge 모듈 개발을 위한 환경을 설정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="5236b-108">*64비트 Windows* 및 *64비트 Linux(Ubuntu/Debian 8)* 운영 체제 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="5236b-109">다음과 같은 소프트웨어가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-109">The following software is required:</span></span>

* <span data-ttu-id="5236b-110">[Git 클라이언트](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="5236b-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="5236b-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="5236b-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="5236b-112">[Maven](https://maven.apache.org/install.html)</span><span class="sxs-lookup"><span data-stu-id="5236b-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="5236b-113">명령줄 터미널 창을 열고 다음 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-113">Open a command-line terminal window and clone the following repository:</span></span>

1. <span data-ttu-id="5236b-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="5236b-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="5236b-115">전체 아키텍처</span><span class="sxs-lookup"><span data-stu-id="5236b-115">Overall architecture</span></span>

<span data-ttu-id="5236b-116">Azure IoT Edge 플랫폼은 [Von Neumann 아키텍처](https://en.wikipedia.org/wiki/Von_Neumann_architecture)를 중요하게 채택합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-116">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="5236b-117">전체 Azure IoT Edge 아키텍처는 입력을 처리하고 출력을 생성하는 시스템이며 각 개별 모듈은 아주 작은 입력-출력 하위 시스템이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-117">Which means that the entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="5236b-118">이 자습서에서는 다음 두 개의 모듈을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-118">In this tutorial, we will introduce the following two modules:</span></span>

1. <span data-ttu-id="5236b-119">시뮬레이션된 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 신호를 수신하여 형식이 지정된 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지로 변환하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="5236b-120">수신한 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지를 인쇄하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-120">A module which prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="5236b-121">다음 이미지는 이 프로젝트에 대한 일반적인 종단 간 데이터 흐름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-121">The following image displays the typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="5236b-122">![3개의 모듈 간의 데이터 흐름](media/iot-hub-iot-edge-create-module/dataflow.png "입력: 시뮬레이션된 BLE 모듈, 프로세서: 변환기 모듈, 출력: 프린터 모듈")</span><span class="sxs-lookup"><span data-stu-id="5236b-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="5236b-123">코드 이해</span><span class="sxs-lookup"><span data-stu-id="5236b-123">Understanding the code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="5236b-124">Maven 프로젝트 구조</span><span class="sxs-lookup"><span data-stu-id="5236b-124">Maven project structure</span></span>

<span data-ttu-id="5236b-125">Azure IoT Edge 패키지는 Maven을 기반으로 하므로 `pom.xml` 파일을 포함하는 일반적인 Maven 프로젝트 구조를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-125">Since Azure IoT Edge packages are based on Maven, we need to create a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="5236b-126">POM은 `com.microsoft.azure.gateway.gateway-module-base` 패키지에서 상속합니다. 이는 런타임 이진 파일, 게이트웨이 구성 파일 경로 및 실행 동작을 포함하는 모듈 프로젝트에서 필요한 모든 종속성을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-126">The POM inherits from the `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of the dependencies needed by a module project which includes the runtime binaries, the gateway configuration file path, and the execution behavior.</span></span> <span data-ttu-id="5236b-127">이를 통해 많은 시간을 절약할 수 있고, 수백 개의 코드 줄을 반복하여 쓰고 다시 쓸 필요가 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-127">This saves us lots of time and eliminate the need to write and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="5236b-128">다음 코드 조각에 나와 있는 것처럼 모듈에서 사용할 구성 파일의 필수 종속성/플러그 인 및 이름을 선언하여 pom.xml 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-128">We need to update the pom.xml file by declaring the required dependencies/plugins and the name of the configuration file to be used by our module as shown in the following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set the filename of the Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="5236b-129">Azure IoT Edge 모듈에 대한 기본적인 이해</span><span class="sxs-lookup"><span data-stu-id="5236b-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="5236b-130">Azure IoT Edge 모듈을 입력을 수신하고, 처리하며, 출력을 생성하는 작업을 수행하는 데이터 프로세서로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="5236b-131">입력은 하드웨어(예: 동작 탐지기)의 데이터, 다른 모듈의 메시지 또는 그밖에 무엇(예: 타이머에 의해 정기적으로 생성된 난수)이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-131">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="5236b-132">출력은 입력과 유사하게, 하드웨어 동작(예: 깜박이는 LED), 다른 모듈로 보내는 메시지 또는 그밖에 무엇(예: 콘솔에 인쇄)을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-132">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="5236b-133">모듈은 `com.microsoft.azure.gateway.messaging.Message` 클래스를 사용하여 서로 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="5236b-134">`Message`의 **콘텐츠**는 사용자가 선호하는 모든 종류의 데이터를 표시할 수 있는 바이트 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-134">The **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="5236b-135">**속성**은 `Message`에서 사용할 수 있으며 단순히 문자열-문자열 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-135">**Properties** are also available in the `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="5236b-136">**속성**을 HTTP 요청의 헤더 또는 파일의 메타데이터로 생각할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-136">You may think of **Properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="5236b-137">Java에서 Azure IoT Edge 모듈을 개발하려면 `com.microsoft.azure.gateway.core.GatewayModule`에서 상속하는 새 모듈 클래스를 만들고, 필수 추상 메서드 `receive()` 및 `destroy()`를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-137">In order to develop an Azure IoT Edge module in Java, you need to create a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement the required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="5236b-138">이 시점에서 선택적 `start()` 또는 `create()` 메서드를 구현하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-138">At this point, you may also choose to implement the optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="5236b-139">다음 코드 조각은 Azure IoT Edge 모듈을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-139">The following code snippet shows you how to get started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let the GatewayModule do the dirty work of initialization. It's also
       a good time to parse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire the resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time to release all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic to process the input message. This method is required. */
    // ...
    /* Use publish() method to do the output. You are
       allowed to publish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="5236b-140">변환기 모듈</span><span class="sxs-lookup"><span data-stu-id="5236b-140">Converter module</span></span>

| <span data-ttu-id="5236b-141">입력</span><span class="sxs-lookup"><span data-stu-id="5236b-141">Input</span></span>                    | <span data-ttu-id="5236b-142">프로세서</span><span class="sxs-lookup"><span data-stu-id="5236b-142">Processor</span></span>                              | <span data-ttu-id="5236b-143">출력</span><span class="sxs-lookup"><span data-stu-id="5236b-143">Output</span></span>                 | <span data-ttu-id="5236b-144">원본 파일</span><span class="sxs-lookup"><span data-stu-id="5236b-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="5236b-145">온도 데이터 메시지</span><span class="sxs-lookup"><span data-stu-id="5236b-145">Temperature data message</span></span> | <span data-ttu-id="5236b-146">새 JSON 메시지의 구문 분석 및 생성</span><span class="sxs-lookup"><span data-stu-id="5236b-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="5236b-147">JSON 메시지 구조</span><span class="sxs-lookup"><span data-stu-id="5236b-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="5236b-148">이 모듈은 일반적인 Azure IoT Edge 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="5236b-149">다른 모듈에서 온도 메시지를 수락하고(하드웨어 모듈 또는 이 경우 시뮬레이션된 BLE 모듈), 구조적 JSON 메시지로 온도 메시지를 정규화합니다(메시지 ID 첨부, 온도 경고를 트리거해야 하는지 여부의 속성 설정 등 포함).</span><span class="sxs-lookup"><span data-stu-id="5236b-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="5236b-150">프린터 모듈</span><span class="sxs-lookup"><span data-stu-id="5236b-150">Printer module</span></span>

| <span data-ttu-id="5236b-151">입력</span><span class="sxs-lookup"><span data-stu-id="5236b-151">Input</span></span>                          | <span data-ttu-id="5236b-152">프로세서</span><span class="sxs-lookup"><span data-stu-id="5236b-152">Processor</span></span> | <span data-ttu-id="5236b-153">출력</span><span class="sxs-lookup"><span data-stu-id="5236b-153">Output</span></span>                     | <span data-ttu-id="5236b-154">원본 파일</span><span class="sxs-lookup"><span data-stu-id="5236b-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="5236b-155">다른 모듈의 모든 메시지</span><span class="sxs-lookup"><span data-stu-id="5236b-155">Any message from other modules</span></span> | <span data-ttu-id="5236b-156">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5236b-156">N/A</span></span>       | <span data-ttu-id="5236b-157">콘솔에 메시지 로그</span><span class="sxs-lookup"><span data-stu-id="5236b-157">Log the message to console</span></span> | `PrinterModule.java` |

<span data-ttu-id="5236b-158">이는 간단하고 설명이 따로 필요 없으며, 수신한 메시지를 터미널 창으로 출력하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-158">This is a simple, self-explanatory, module which outputs the received messages to the terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="5236b-159">Azure IoT Edge 구성</span><span class="sxs-lookup"><span data-stu-id="5236b-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="5236b-160">모듈을 실행하기 전 마지막 단계는 Azure IoT Edge를 구성하고 모듈 간 연결을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-160">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="5236b-161">첫 번째로, 나중에 섹션에서 자체 `name`에 의해 참조될 수 있는 Java 로더를 선언해야 합니다(Azure IoT Edge가 다른 언어의 로더를 지원하기 때문).</span><span class="sxs-lookup"><span data-stu-id="5236b-161">First we need to declare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="5236b-162">로더를 선언하고 나면, 모듈도 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-162">Once we have declared our loaders, we will also need to declare our modules as well.</span></span> <span data-ttu-id="5236b-163">로더 선언과 마찬가지로 모듈도 `name` 특성에 의해 참조될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-163">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="5236b-164">모듈을 선언할 때 각 모듈에 대해 사용해야 하는 로더(앞서 정의한 것 중 하나여야 함) 및 진입점(모듈의 정규화된 클래스 이름이어야 함)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-164">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="5236b-165">`simulated_device` 모듈은 Azure IoT Edge 코어 런타임 패키지에 포함되는 네이티브 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-165">The `simulated_device` module is a native module which is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="5236b-166">`args`를 JSON 파일에 `null`인 경우라도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-166">You should always include `args` in the JSON file even if it is `null`.</span></span>

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="5236b-167">구성 마지막에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-167">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="5236b-168">각 연결은 `source` 및 `sink`로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="5236b-169">미리 정의된 모듈을 모두 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="5236b-170">`source` 모듈의 출력 메시지는 `sink` 모듈의 입력으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-170">The output message of `source` module will be forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="5236b-171">모듈 실행</span><span class="sxs-lookup"><span data-stu-id="5236b-171">Running the modules</span></span>

<span data-ttu-id="5236b-172">`mvn package`를 사용하여 모든 항목을 `target/` 폴더에 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-172">Use `mvn package` to build everything into the `target/` folder.</span></span> <span data-ttu-id="5236b-173">`mvn clean package`도 클린 빌드에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="5236b-174">`mvn exec:exec`를 사용하여 Azure IoT Edge를 실행하고, 온도 데이터와 모든 속성이 고정된 속도로 콘솔에 인쇄되는 것을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-174">Use `mvn exec:exec` to run the Azure IoT Edge and you should observe that the temperature data and all the properties are printed to the console at a fixed rate.</span></span>

<span data-ttu-id="5236b-175">응용 프로그램을 종료하려면 `<Enter>` 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-175">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5236b-176">Ctrl + C를 사용하여 IoT Edge 게이트웨이 응용 프로그램을 종료하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-176">It is not recommended to use Ctrl + C to terminate the IoT Edge gateway application.</span></span> <span data-ttu-id="5236b-177">이는 프로세스를 비정상적으로 종료할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5236b-177">As this may cause the process to terminate abnormally.</span></span>

