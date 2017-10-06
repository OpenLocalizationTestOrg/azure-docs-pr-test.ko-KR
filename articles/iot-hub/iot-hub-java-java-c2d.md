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
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>IoT Hub(Java)를 사용하여 클라우드-장치 메시지 보내기
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다. hello [IoT 허브 시작] toocreate IoT hub, 장치 id를 프로 비전 하 고 장치-클라우드 메시지를 보내는 시뮬레이션 된 장치 앱을 코딩 하는 방법을 보여 주는 자습서입니다.

이 자습서는 [IoT 허브 시작]를 토대로 작성되었습니다. 이 항목에서는 다음 방법을 설명합니다.

* 솔루션 백 엔드에서 IoT 허브를 통해 tooa 단일 장치를 클라우드-장치 메시지를 보냅니다.
* 장치에서 클라우드-장치 메시지를 받습니다.
* 솔루션 백 엔드에서 배달 확인 요청 (*피드백*) IoT 허브에서 메시지 보내는 tooa 장치에 대 한 합니다.

Hello에서 클라우드-장치 메시지에서 자세한 정보를 찾을 수 있습니다 [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.

이 자습서의 hello 끝에 두 개의 Java 콘솔 응용 프로그램 실행합니다.

* **시뮬레이션 된 장치**, 수정 된 버전에서 만든 hello 앱의 [IoT 허브 시작], tooyour IoT 허브를 연결 하 고 클라우드-장치 메시지를 수신 합니다.
* **메시지를 보내며-c2d**는 IoT 허브를 통해 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 앱을 보내고 해당 배달 승인을 받습니다.

> [!NOTE]
> IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다. 에 대 한 단계별 지침은 tooconnect 장치 toothis 자습서의 코드 및 일반적으로 tooAzure IoT Hub를 확인 하려면 어떻게 hello [Azure IoT 개발자 센터]합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 전체 작업 버전의 hello [IoT 허브 시작](iot-hub-java-java-getstarted.md) 또는 [프로세스 IoT Hub 장치-클라우드 메시지](iot-hub-java-java-process-d2c.md) 자습서입니다.
* 최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

## <a name="receive-messages-in-hello-simulated-device-app"></a>Hello 시뮬레이션 된 장치 응용 프로그램에서 메시지를 수신 합니다.

Hello 시뮬레이션 된 장치 응용 프로그램에서 만든이 섹션에서 수정 [IoT 허브 시작] hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.

1. 텍스트 편집기를 사용 하 여 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.

2. Hello 다음 추가 **MessageCallback** hello 안에 중첩 된 클래스와 **앱** 클래스입니다. hello **실행** hello 장치 IoT 허브에서 메시지를 받을 때 메서드가 호출 됩니다. 이 예제에서는 hello 장치 항상에 게 알리는 hello IoT hub hello 메시지 완료 되었음을:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Hello 수정 **주** 메서드 toocreate는 **AppMessageCallback** 인스턴스와 호출 hello **setMessageCallback** 메서드를 다음과 같이 hello 클라이언트 열리기 전에:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > MQTT 또는 AMQP 대신 hello 전송으로 HTTP를 사용 하는 경우 hello **DeviceClient** 인스턴스 IoT 허브에 자주 사용 (모든 25 분 내)에서 메시지를 확인 합니다. Hello 차이 MQTT, AMQP 및 HTTP 지원 및 IoT Hub 제한에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.

4. toobuild hello **시뮬레이션 된 장치** Maven에서 사용 하 여 앱 hello 다음 hello 시뮬레이션 된 장치 폴더에서 hello 명령 프롬프트에서 명령을 실행 합니다.

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>클라우드-장치 메시지 보내기

이 섹션에서는 클라우드-장치 메시지 toohello 시뮬레이션 된 장치 응용 프로그램에서 전송 하 여 Java 콘솔 응용 프로그램을 만들 수 있습니다. Hello에 추가 하는 hello 장치의 장치 ID hello 필요 [IoT 허브 시작] 자습서입니다. 또한 hello에서 찾을 수 있는 허브에 대 한 연결 문자열 IoT Hub를 hello 필요 [Azure 포털]합니다.

1. 라는 Maven 프로젝트 만들기 **c2d 보냄** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 이 명령은 긴 단일 명령입니다.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. 명령 프롬프트 toohello 새 메시지를 보내며-c2d 폴더를 이동 합니다.

3. 텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 메시지를 보내며-c2d 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드. Toouse hello hello 종속성을 추가 하면 **java 서비스 클라이언트 iothub** IoT 허브 서비스와 응용 프로그램 toocommunicate 프로그램에서 패키지:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > 최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-service-search]합니다.

4. 저장 하 고 hello pom.xml 파일을 닫습니다.

5. 텍스트 편집기를 사용 하 여 hello send-c2d-messages\src\main\java\com\mycompany\app\App.java 파일을 엽니다.

6. Hello 다음 추가 **가져올** 문 toohello 파일:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. 클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스를 대체 **{yourhubconnectionstring}** 및 **{yourdeviceid}** hello로 값에 명시 된 이전 버전:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Hello 대체 **주** 메서드 코드 다음 hello로 합니다. 이 코드 tooyour IoT 허브를 연결 하 고 보내는 메시지 tooyour 장치를 해당 hello 장치 수신 및 처리 된 hello 메시지를 승인 후 대기.
   
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
    > 간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.


9. toobuild hello **시뮬레이션 된 장치** Maven에서 사용 하 여 앱 hello 다음 hello 시뮬레이션 된 장치 폴더에서 hello 명령 프롬프트에서 명령을 실행 합니다.

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행

준비 toorun hello 응용 프로그램입니다.

1. Hello 시뮬레이션 된 장치 폴더에서 명령 프롬프트에서 다음 원격 분석 tooyour IoT 허브 및 허브에서 보낸 클라우드-장치 메시지에 대 한 toolisten 보내는 명령 toobegin hello를 실행 합니다.

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Hello 시뮬레이션 된 장치 앱 실행][img-simulated-device]

2. 클라우드-장치 메시지와 대기 피드백 승인에 대 한 hello 메시지를 보내며-c2d 폴더에 명령 프롬프트에서 다음 명령 toosend hello를 실행 합니다.

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Hello 명령 toosend hello 클라우드-장치 메시지를 실행 합니다.][img-send-command]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 방법에 대해 배웠습니다 toosend 및 클라우드-장치 메시지를 수신 합니다. 

IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite]합니다.

IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.

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