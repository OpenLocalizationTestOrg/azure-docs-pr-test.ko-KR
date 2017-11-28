---
title: "Azure IoT Hub (Java)와 aaaCloud-장치 메시지 | Microsoft Docs"
description: "어떻게 toosend 클라우드-장치 메시지 tooa 장치 hello Azure IoT Sdk를 사용 하 여 Java 용 Azure IoT 허브에서 설정 합니다. 시뮬레이션 된 장치 앱 tooreceive 클라우드-장치 메시지를 수정 하 고 백 엔드 응용 프로그램 toosend hello 클라우드-장치 메시지를 수정 합니다."
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
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="39a74-104">IoT Hub(Java)를 사용하여 클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="39a74-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="39a74-105">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="39a74-106">hello [IoT 허브 시작] toocreate IoT hub, 장치 id를 프로 비전 하 고 장치-클라우드 메시지를 보내는 시뮬레이션 된 장치 앱을 코딩 하는 방법을 보여 주는 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="39a74-107">이 자습서는 [IoT 허브 시작]를 토대로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="39a74-108">이 항목에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-108">It shows you how to:</span></span>

* <span data-ttu-id="39a74-109">솔루션 백 엔드에서 IoT 허브를 통해 tooa 단일 장치를 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="39a74-110">장치에서 클라우드-장치 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="39a74-111">솔루션 백 엔드에서 배달 확인 요청 (*피드백*) IoT 허브에서 메시지 보내는 tooa 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="39a74-112">Hello에서 클라우드-장치 메시지에서 자세한 정보를 찾을 수 있습니다 [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="39a74-113">이 자습서의 hello 끝에 두 개의 Java 콘솔 응용 프로그램 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="39a74-114">**시뮬레이션 된 장치**, 수정 된 버전에서 만든 hello 앱의 [IoT 허브 시작], tooyour IoT 허브를 연결 하 고 클라우드-장치 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="39a74-115">**메시지를 보내며-c2d**는 IoT 허브를 통해 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 앱을 보내고 해당 배달 승인을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="39a74-116">IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="39a74-117">에 대 한 단계별 지침은 tooconnect 장치 toothis 자습서의 코드 및 일반적으로 tooAzure IoT Hub를 확인 하려면 어떻게 hello [Azure IoT 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="39a74-118">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="39a74-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="39a74-119">전체 작업 버전의 hello [IoT 허브 시작](iot-hub-java-java-getstarted.md) 또는 [프로세스 IoT Hub 장치-클라우드 메시지](iot-hub-java-java-process-d2c.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="39a74-120">최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="39a74-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="39a74-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="39a74-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="39a74-122">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="39a74-122">An active Azure account.</span></span> <span data-ttu-id="39a74-123">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="39a74-124">Hello 시뮬레이션 된 장치 응용 프로그램에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="39a74-125">Hello 시뮬레이션 된 장치 응용 프로그램에서 만든이 섹션에서 수정 [IoT 허브 시작] hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="39a74-126">텍스트 편집기를 사용 하 여 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="39a74-127">Hello 다음 추가 **MessageCallback** hello 안에 중첩 된 클래스와 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="39a74-128">hello **실행** hello 장치 IoT 허브에서 메시지를 받을 때 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="39a74-129">이 예제에서는 hello 장치 항상에 게 알리는 hello IoT hub hello 메시지 완료 되었음을:</span><span class="sxs-lookup"><span data-stu-id="39a74-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="39a74-130">Hello 수정 **주** 메서드 toocreate는 **AppMessageCallback** 인스턴스와 호출 hello **setMessageCallback** 메서드를 다음과 같이 hello 클라이언트 열리기 전에:</span><span class="sxs-lookup"><span data-stu-id="39a74-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="39a74-131">MQTT 또는 AMQP 대신 hello 전송으로 HTTP를 사용 하는 경우 hello **DeviceClient** 인스턴스 IoT 허브에 자주 사용 (모든 25 분 내)에서 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="39a74-132">Hello 차이 MQTT, AMQP 및 HTTP 지원 및 IoT Hub 제한에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="39a74-133">toobuild hello **시뮬레이션 된 장치** Maven에서 사용 하 여 앱 hello 다음 hello 시뮬레이션 된 장치 폴더에서 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="39a74-134">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="39a74-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="39a74-135">이 섹션에서는 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 응용 프로그램에서 전송 하 여 Java 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="39a74-136">Hello에 추가 하는 hello 장치의 장치 ID hello 필요 [IoT 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="39a74-137">또한 hello에서 찾을 수 있는 허브에 대 한 연결 문자열 IoT Hub를 hello 필요 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="39a74-138">라는 Maven 프로젝트 만들기 **c2d 보냄** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="39a74-139">이 명령은 긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="39a74-140">명령 프롬프트 toohello 새 메시지를 보내며-c2d 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="39a74-141">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 메시지를 보내며-c2d 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="39a74-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="39a74-142">Toouse hello hello 종속성을 추가 하면 **java 서비스 클라이언트 iothub** IoT 허브 서비스와 응용 프로그램 toocommunicate 프로그램에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="39a74-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="39a74-143">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-service-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="39a74-144">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="39a74-145">텍스트 편집기를 사용 하 여 hello send-c2d-messages\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="39a74-146">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="39a74-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="39a74-147">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스를 대체 **{yourhubconnectionstring}** 및 **{yourdeviceid}** hello로 값에 명시 된 이전 버전:</span><span class="sxs-lookup"><span data-stu-id="39a74-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="39a74-148">Hello 대체 **주** 메서드 코드 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="39a74-149">이 코드 tooyour IoT 허브를 연결 하 고 보내는 메시지 tooyour 장치를 해당 hello 장치 수신 및 처리 된 hello 메시지를 승인 후 대기.</span><span class="sxs-lookup"><span data-stu-id="39a74-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
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
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
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
    > <span data-ttu-id="39a74-150">간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="39a74-151">프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="39a74-152">toobuild hello **시뮬레이션 된 장치** Maven에서 사용 하 여 앱 hello 다음 hello 시뮬레이션 된 장치 폴더에서 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="39a74-153">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="39a74-153">Run hello applications</span></span>

<span data-ttu-id="39a74-154">준비 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="39a74-155">Hello 시뮬레이션 된 장치 폴더에서 명령 프롬프트에서 다음 원격 분석 tooyour IoT 허브 및 허브에서 보낸 클라우드-장치 메시지에 대 한 toolisten 보내는 명령 toobegin hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Hello 시뮬레이션 된 장치 앱 실행][img-simulated-device]

2. <span data-ttu-id="39a74-157">클라우드-장치 메시지와 대기 피드백 승인에 대 한 hello 메시지를 보내며-c2d 폴더에 명령 프롬프트에서 다음 명령 toosend hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Hello 명령 toosend hello 클라우드-장치 메시지를 실행 합니다.][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="39a74-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39a74-159">Next steps</span></span>

<span data-ttu-id="39a74-160">이 자습서에서는 방법에 대해 배웠습니다 toosend 및 클라우드-장치 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="39a74-161">IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="39a74-162">IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.</span><span class="sxs-lookup"><span data-stu-id="39a74-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[IoT 허브 시작]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT 허브 개발자 가이드]: iot-hub-devguide.md
[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure 포털]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22