---
title: "Azure IoT Hub 장치-클라우드 메시지 (Java) aaaProcess | Microsoft Docs"
description: "어떻게 tooprocess 라우팅 규칙 및 사용자 지정 끝점 toodispatch를 사용 하 여 IoT Hub 장치-클라우드 메시지 tooother 백 엔드 서비스 메시지입니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="16508-103">IoT Hub 장치-클라우드 메시지 처리(Java)</span><span class="sxs-lookup"><span data-stu-id="16508-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="16508-104">Azure IoT Hub는 수백만의 장치와 솔루션 백 엔드 간에서 안정적이고 안전한 양방향 통신이 가능하도록 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="16508-105">다른 자습서 ([IoT 허브 시작] 및 [IoT Hub와 클라우드-장치 메시지를 보낼][lnk-c2d]) 기본 장치-클라우드 및 클라우드-장치 toouse hello 하는 방법을 보여 줍니다 IoT Hub의 메시징 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="16508-106">Hello에 표시 된 hello 코드를 기반으로 한이 자습서 [IoT 허브 시작] 자습서 toouse tooprocess 장치-클라우드 메시지를 라우팅하는 확장 가능한 방식으로 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="16508-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="16508-107">hello 자습서 hello 솔루션에서 즉각적인 동작이 필요한 tooprocess 메시지 끝을 백업 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="16508-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="16508-108">예를 들어 장치는 CRM 시스템으로의 티켓 삽입을 트리거하는 경보 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="16508-109">이와 반대로 데이터 요소 메시지는 단순히 분석 엔진으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="16508-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="16508-110">예를 들어 온도 원격 분석은 향후 분석을 위해 저장 toobe 하는 장치에서 데이터 요소의 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="16508-111">이 자습서의 hello 끝 세 Java 콘솔 응용 프로그램 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="16508-112">**시뮬레이션 된 장치**, hello에서 만든 hello 응용 프로그램의 수정된 된 버전 [IoT 허브 시작] 자습서 1 초 마다 데이터 요소 장치-클라우드 메시지를 보냅니다 및 대화형 장치-클라우드 메시지 마다 10 시간 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="16508-113">이 응용 프로그램 IoT Hub와 AMQP 프로토콜 toocommunicate hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="16508-114">**읽기-d2c-송신 된 메시지** 장치 앱에서 보낸 hello 원격 분석 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16508-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="16508-115">**중요 한 큐 읽기** hello hello 서비스 버스 연결 된 큐 toohello IoT 허브에서에서 중요 한 메시지 큐에 넣고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="16508-116">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 JavaScript 포함)에 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="16508-117">어떻게 tooreplace hello 장치가이 자습서에서는 실제 장치에 대 한 지침은 tooconnect 장치 tooan IoT Hub hello를 참조 하는 방법 및 [Azure IoT 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="16508-118">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="16508-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="16508-119">전체 작업 버전의 hello [IoT 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="16508-120">최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="16508-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="16508-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="16508-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="16508-122">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="16508-122">An active Azure account.</span></span> <span data-ttu-id="16508-123">(계정이 없는 경우 몇 분 만에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="16508-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="16508-124">[Azure Storage] 및 [Azure Service Bus]에 대한 기본 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="16508-125">장치 앱에서 대화형 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="16508-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="16508-126">Hello 장치 hello에서 만든 응용 프로그램을 수정이 섹션에서는 [IoT 허브 시작] 자습서 toooccasionally 즉시 처리를 필요로 하는 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="16508-127">텍스트 편집기 tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="16508-128">이 파일에 포함 hello에 대 한 hello 코드 **시뮬레이션 된 장치** hello에서 만든 응용 [IoT 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="16508-129">Hello 대체 **MessageSender** 코드 다음 hello 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="16508-129">Replace hello **MessageSender** class with hello following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="16508-130">이 메서드는 임의로 hello 속성 추가 `"level": "critical"` toomessages hello 응용 프로그램 백 엔드 하 여 즉각적인 동작이 필요한 메시지를 시뮬레이트하는 hello 장치에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="16508-131">해당 IoT 허브는 hello 메시지 toohello 적절 한 메시지 대상 라우팅할 수 있도록 hello 응용 프로그램 hello 메시지 속성에서이 정보 대신 hello 메시지 본문에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="16508-132">콜드 경로 toohello 실행 부하 과다 경로 여기에 표시 된 예에서는 또한 처리를 포함 하는 다양 한 시나리오에 대 한 메시지 속성 tooroute 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="16508-133">저장 하 고 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16508-134">이 자습서는 간단한 hello 위해서 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="16508-135">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 지 수 백오프 같은 다시 시도 정책을 구현 해야 [일시적인 오류 처리]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="16508-136">toobuild hello **시뮬레이션 된 장치** Maven에서 사용 하 여 앱 hello 다음 hello 시뮬레이션 된 장치 폴더에서 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="16508-137">큐 tooyour IoT 허브 및 경로 메시지 tooit 추가</span><span class="sxs-lookup"><span data-stu-id="16508-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="16508-138">서비스 버스 큐를 만들이 섹션에서는 tooyour IoT 허브를 연결 및 hello 메시지에서 속성의 hello 존재 여부에 따라 IoT 허브 toosend 메시지 toohello 큐를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="16508-139">서비스 버스 큐에서 메시지를 tooprocess 방법에 대 한 자세한 내용은 참조 [큐 작업 시작][lnk-sb-queues-java]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="16508-140">[큐 시작][lnk-sb-queues-java]에서 설명한 대로 Service Bus 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16508-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="16508-141">Hello 네임 스페이스와 큐 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="16508-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="16508-142">에 Azure 포털 hello IoT 허브를 열고 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![IoT Hub의 끝점][30]

3. <span data-ttu-id="16508-144">Hello에 **끝점** 블레이드에서 클릭 **추가** 에 hello 상위 tooadd 큐 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="16508-145">이름 hello 끝점 **CriticalQueue** 드롭다운 tooselect hello를 사용 하 여 **서비스 버스 큐**, 큐 상주 하는 서비스 버스 네임 스페이스 hello 및 hello 큐의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="16508-146">완료 되 면 클릭 **저장** hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-146">When you are done, click **Save** at hello bottom.</span></span>

    ![끝점 추가][31]

4. <span data-ttu-id="16508-148">이제 IoT Hub에서 **경로**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="16508-149">클릭 **추가** toohello 방금 하면 큐 메시지를 라우팅하는 라우팅 규칙을 추가 하는 hello 블레이드 toocreate hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="16508-150">선택 **DeviceTelemetry** hello 데이터 원본으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="16508-151">입력 `level="critical"` hello 조건으로 사용자 지정 끝점으로 라우팅 규칙 끝점 hello로 방금 추가한 hello 큐를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="16508-152">완료 되 면 클릭 **저장** hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-152">When you are done, click **Save** at hello bottom.</span></span>

    ![경로 추가][32]

    <span data-ttu-id="16508-154">대체 경로 hello 너무 설정 되어 있는지 확인**ON**합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="16508-155">이 설정은 IoT hub의 hello 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![대체(fallback) 경로][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="16508-157">(선택 사항) Hello 큐 끝점에서 읽기</span><span class="sxs-lookup"><span data-stu-id="16508-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="16508-158">Hello 지침에 따라 hello 큐 끝점에서 hello 메시지를 읽고 필요에 따라 [큐 작업 시작][lnk-sb-queues-java]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="16508-159">이름 hello 앱 **중요 큐 읽기**합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="16508-160">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="16508-160">Run hello applications</span></span>

<span data-ttu-id="16508-161">이제 모르는 준비 toorun hello 세 개의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="16508-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="16508-162">toorun hello **읽기-d2c-송신 된 메시지** 응용 프로그램 또는 셸 명령 프롬프트에서 toohello 읽기 d2c 폴더를 이동 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![read-d2c-messages 실행][readd2c]

2. <span data-ttu-id="16508-164">toorun hello **중요 큐 읽기** 응용 프로그램 또는 셸 명령 프롬프트에서 toohello 읽기 중요 큐 폴더를 이동 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![read-critical-messages 실행][readqueue]

3. <span data-ttu-id="16508-166">toorun hello **시뮬레이션 된 장치** 응용 프로그램 또는 셸 명령 프롬프트에서 toohello 시뮬레이션 된 장치 폴더를 이동 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![simulated-device 실행][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="16508-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16508-168">Next steps</span></span>

<span data-ttu-id="16508-169">이 자습서에서는 tooreliably IoT 허브의 hello 메시지 라우팅 기능을 사용 하 여 장치-클라우드 메시지를 디스패치 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="16508-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="16508-170">hello [IoT Hub와 toosend 클라우드-장치 메시지 방법을] [ lnk-c2d] toosend 솔루션 백 엔드에서 tooyour 장치 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="16508-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="16508-171">IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite][lnk-suite]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="16508-172">IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="16508-173">IoT Hub에 메시지 라우팅에 대 한 더 toolearn 참조 [IoT Hub와 메시지를 주고받을][lnk-devguide-messaging]합니다.</span><span class="sxs-lookup"><span data-stu-id="16508-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[IoT 허브 개발자 가이드]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[IoT 허브 시작]: iot-hub-java-java-getstarted.md
[Azure IoT 개발자 센터]: https://azure.microsoft.com/develop/iot
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
