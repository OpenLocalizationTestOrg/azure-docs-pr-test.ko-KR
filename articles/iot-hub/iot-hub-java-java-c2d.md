---
title: "Azure IoT Hub(Java)를 사용한 클라우드-장치 메시지 | Microsoft Docs"
description: "Java용 Azure IoT SDK를 사용하여 Azure IoT Hub에서 장치로 클라우드-장치 메시지를 보내는 방법입니다. 클라우드-장치 메시지를 받는 시뮬레이트된 장치 앱을 수정하고 클라우드-장치 메시지를 보내는 백 엔드 앱을 수정합니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: f5e3ac46f4d144b12e2ab7fcfb456665ff6cc68f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="9f22e-104">IoT Hub(Java)를 사용하여 클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="9f22e-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="9f22e-105">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="9f22e-106">[IoT Hub 시작하기] 자습서에서는 IoT Hub를 만들고 그 안에 장치 ID를 프로비전하고 장치-클라우드 메시지를 보내는 시뮬레이션된 장치 앱을 코딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-106">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="9f22e-107">이 자습서는 [IoT Hub 시작하기]를 토대로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="9f22e-108">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-108">It shows you how to:</span></span>

* <span data-ttu-id="9f22e-109">솔루션 백 엔드에서 IoT Hub를 통해 클라우드-장치 메시지를 단일 장치로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-109">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="9f22e-110">장치에서 클라우드-장치 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="9f22e-111">솔루션 백 엔드에서, IoT Hub에서 장치로 보낸 메시지에 대한 배달 확인(*피드백*)을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="9f22e-112">클라우드-장치 메시지에 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-112">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="9f22e-113">이 자습서의 끝 부분에서는 다음 두 개의 Java 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-113">At the end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="9f22e-114">**simulated-device**는 [IoT Hub 시작하기]에서 만든 앱의 수정된 버전으로서 IoT Hub에 연결하고 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-114">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="9f22e-115">**send-c2d-messages**는 IoT Hub를 통해 시뮬레이션된 장치 앱에 클라우드-장치 메시지를 보낸 다음 배달 승인을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-115">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="9f22e-116">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="9f22e-117">이 자습서의 코드 및 일반적으로 Azure IoT Hub에 장치를 연결하는 방법에 대한 단계별 지침은 [Azure IoT 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f22e-117">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="9f22e-118">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="9f22e-119">[IoT Hub 시작](iot-hub-java-java-getstarted.md) 또는 [IoT Hub 장치-클라우드 메시지 처리](iot-hub-java-java-process-d2c.md) 자습서의 전체 작업 버전.</span><span class="sxs-lookup"><span data-stu-id="9f22e-119">A complete working version of the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="9f22e-120">최신 [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="9f22e-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="9f22e-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="9f22e-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="9f22e-122">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="9f22e-122">An active Azure account.</span></span> <span data-ttu-id="9f22e-123">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="9f22e-124">시뮬레이션된 장치 앱에서 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="9f22e-124">Receive messages in the simulated device app</span></span>

<span data-ttu-id="9f22e-125">이 섹션에서는 [IoT Hub 시작하기]에서 만든 시뮬레이션된 장치 앱을 수정하여 IoT Hub로부터 클라우드-장치 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-125">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="9f22e-126">텍스트 편집기를 사용하여 simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-126">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="9f22e-127">**App** 클래스 안에 중첩 클래스로 다음과 같은 **MessageCallback** 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-127">Add the following **MessageCallback** class as a nested class inside the **App** class.</span></span> <span data-ttu-id="9f22e-128">장치가 IoT Hub에서 메시지를 받을 때 **execute** 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-128">The **execute** method is invoked when the device receives a message from IoT Hub.</span></span> <span data-ttu-id="9f22e-129">이 예제에서 장치는 항상 IoT Hub에 메시지를 완료했음을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-129">In this example, the device always notifies the IoT hub that it has completed the message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="9f22e-130">다음과 같이 클라이언트를 열기 전에 **main** 메서드를 수정하여 **AppMessageCallback** 인스턴스를 만들고 **setMessageCallback** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-130">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="9f22e-131">전송으로 MQTT 또는 AMQP 대신 HTTP을 사용하는 경우 **DeviceClient** 인스턴스는 IoT Hub의 메시지를 자주(25분 미만 간격으로) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-131">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="9f22e-132">MQTT, AMQP 및 HTTP 지원과 IoT Hub 제한 간의 차이점에 대한 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub developer guide - C2D]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f22e-132">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="9f22e-133">Maven을 사용하여 **simulated-device** 앱을 빌드하려면 simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-133">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="9f22e-134">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="9f22e-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="9f22e-135">이 섹션에서는 클라우드-장치 메시지를 시뮬레이트된 장치 앱으로 보내는 Java 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-135">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="9f22e-136">[IoT Hub 시작하기] 자습서에서 추가한 장치의 장치 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-136">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="9f22e-137">[Azure Portal]에서 찾을 수 있는 IoT Hub에 대한 연결 문자열도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-137">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="9f22e-138">명령 프롬프트에서 다음 명령을 사용하여 **send-c2d-messages**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-138">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="9f22e-139">이 명령은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="9f22e-140">명령 프롬프트에서 새 send-c2d-messages 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-140">At your command prompt, navigate to the new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="9f22e-141">텍스트 편집기를 사용하여 send-c2d-messages 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-141">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="9f22e-142">의존성을 추가하면 IoT Hub 서비스와 통신하기 위해 응용 프로그램에서 **iothub-java-service-client** 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-142">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="9f22e-143">[Maven 검색][lnk-maven-service-search]을 사용하여 **iot-service-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-143">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="9f22e-144">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-144">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="9f22e-145">텍스트 편집기를 사용하여 send-c2d-messages\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-145">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="9f22e-146">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-146">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="9f22e-147">**App** 클래스에 다음 클래스 수준 변수를 추가하고 **{yourhubconnectionstring}** 및 **{yourdeviceid}**를 앞에서 기록해둔 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-147">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="9f22e-148">**main** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-148">Replace the **main** method with the following code.</span></span> <span data-ttu-id="9f22e-149">이 코드는 IoT hub에 연결하고 장치에 메시지를 보낸 다음 장치가 메시지를 수신하고 처리했다는 승인을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-149">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="9f22e-150">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="9f22e-151">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 재시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="9f22e-152">Maven을 사용하여 **simulated-device** 앱을 빌드하려면 simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-152">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="9f22e-153">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9f22e-153">Run the applications</span></span>

<span data-ttu-id="9f22e-154">이제 응용 프로그램을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="9f22e-155">simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub에 원격 분석 데이터 전송을 시작하고 사용자의 허브에서 보낸 클라우드-장치 메시지를 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![시뮬레이션된 장치 앱 실행][img-simulated-device]

2. <span data-ttu-id="9f22e-157">명령 프롬프트의 send-c2d-messages 폴더에서 다음 명령을 실행하여 클라우드-장치 메시지를 보내고 피드백 승인을 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![명령을 실행하여 클라우드-장치 메시지 보내기][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="9f22e-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f22e-159">Next steps</span></span>

<span data-ttu-id="9f22e-160">이 자습서에서 클라우드-장치 메시지를 보내고 받는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9f22e-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="9f22e-161">IoT Hub를 사용하는 전체 종단 간 솔루션의 예를 보려면 [Azure IoT Suite]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f22e-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="9f22e-162">IoT Hub를 사용하여 솔루션을 개발하는 방법에 대한 자세한 내용은 [IoT Hub 개발자 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f22e-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

<span data-ttu-id="9f22e-163">[IoT Hub 시작하기]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="9f22e-163">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="9f22e-164">[IoT Hub 개발자 가이드]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="9f22e-164">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="9f22e-165">[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="9f22e-165">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
<span data-ttu-id="9f22e-166">[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="9f22e-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="9f22e-167">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9f22e-167">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="9f22e-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="9f22e-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22