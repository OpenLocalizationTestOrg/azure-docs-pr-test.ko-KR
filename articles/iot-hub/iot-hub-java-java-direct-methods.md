---
title: "Azure IoT Hub aaaUse 직접 메서드 (Java) | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub는 메서드를 전달 합니다. Hello Azure IoT 장치 SDK를 사용 하 여 Java tooimplement 직접적인 방법 및 hello Java tooimplement hello 직접 메서드를 호출 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK 포함 하는 시뮬레이션 된 장치 앱에 대 한 합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>직접 메서드 사용(Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

이 자습서에서는 다음 두 개의 Java 콘솔 앱을 만듭니다.

* **직접-메서드 호출**, hello 시뮬레이션 된 장치 응용 프로그램의 메서드를 호출 하 고 hello 응답을 표시 하는 Java 백 엔드 앱.
* **시뮬레이션 된 장치**, tooyour IoT hub를 만들면 hello 장치 id를 사용 하 여 연결 하는 장치를 시뮬레이션 하는 Java 응용 프로그램입니다. 이 응용 프로그램 응답 toohello hello 백 엔드에서 직접 호출 합니다.

> [!NOTE]
> 장치 및 백 엔드 솔루션에서 응용 프로그램 toorun toobuild를 사용할 수 있는 Sdk hello에 대 한 정보를 참조 하십시오. [Azure IoT Sdk][lnk-hub-sdks]합니다.

toocomplete 해야이 자습서에서는:

* Java SE 8. <br/> [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 Windows 또는 Linux에서이 자습서에 대 한 Java tooinstall 합니다.
* Maven 3.  <br/> [개발 환경을 준비] [ lnk-dev-setup] 설명 방법을 tooinstall [Maven] [ lnk-maven] Windows 또는 Linux에서이 자습서에 대 한 합니다.
* [Node.js 버전 0.10.0 이상](http://nodejs.org)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기

이 섹션에서는 응답 tooa 메서드 끝 hello 솔루션 다시에서 호출 하 여 Java 콘솔 응용 프로그램을 만들 수 있습니다.

1. iot-java-direct-method라는 빈 폴더를 만듭니다.

1. Hello java 직접 메서드 iot 폴더에서 만들 라는 Maven 프로젝트 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 다음 명령을 hello은 단일, 긴 명령입니다.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 명령 프롬프트 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.

1. 텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 시뮬레이션 된 장치 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드. 이 종속성 있습니다 toouse hello iot 장치 클라이언트에서에서 패키지를 IoT hub와 사용자 응용 프로그램 toocommunicate 수 있습니다.

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > 최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-device-search]합니다.

1. Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드. 이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. 저장 하 고 hello pom.xml 파일을 닫습니다.

1. 텍스트 편집기를 사용 하 여 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.

1. Hello 다음 추가 **가져올** 문 toohello 파일:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. 클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다. 교체 `{youriothubname}` 을 IoT 허브 이름으로, 및 `{yourdevicekey}` hello에 생성 된 hello 장치 키 값을 가진 *장치 id를 만드는* 섹션:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다. 현재 toouse 직접 hello MQTT 프로토콜을 사용 해야 하는 방법입니다.

1. 상태 코드 tooyour IoT 허브를 tooreturn hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. hello 솔루션 백 엔드 toohandle hello 직접 메서드 호출 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. toocreate는 **DeviceClient** 직접 메서드 호출에 대 한 수신 대기 하 고, 추가 **주** 메서드 toohello **앱** 클래스:

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. 저장 후 닫기 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일

1. Hello 빌드 **시뮬레이션 된 장치** 응용 프로그램 오류 수정 하십시오. 명령 프롬프트에서 다음 명령이 실행된 hello 및 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>장치에서 직접 메서드 호출

이 섹션에서는 직접 메서드를 호출 하 고 다음 hello 응답을 표시 하는 Java 콘솔 앱을 만듭니다. 이 콘솔 응용 프로그램 tooyour IoT Hub tooinvoke hello에 대 한 직접 메서드를 연결합니다.

1. Hello java 직접 메서드 iot 폴더에서 만들 라는 Maven 프로젝트 **-직접-메서드 호출** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 다음 명령을 hello은 단일, 긴 명령입니다.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 명령 프롬프트 toohello-직접-메서드 호출 폴더를 이동 합니다.

1. 텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello-직접-메서드 호출 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드. 이 종속성 있습니다 toouse hello iot 서비스 클라이언트에서에서 패키지를 IoT hub와 사용자 응용 프로그램 toocommunicate 수 있습니다.

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > 최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-service-search]합니다.

1. Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드. 이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. 저장 하 고 hello pom.xml 파일을 닫습니다.

1. 텍스트 편집기를 사용 하 여 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 파일을 엽니다.

1. Hello 다음 추가 **가져올** 문 toohello 파일:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. 클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다. 대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. hello 시뮬레이션 된 장치에서 tooinvoke hello 메서드 추가 코드 toohello 다음 hello **주** 메서드:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. 저장 후 닫기 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 파일

1. Hello 빌드 **-직접-메서드 호출** 응용 프로그램 오류 수정 하십시오. 명령 프롬프트 toohello-직접-메서드 호출 폴더 및 다음 명령이 실행된 hello를 이동 합니다.

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hello 앱 실행

준비 toorun hello 콘솔 응용 프로그램입니다.

1. Hello 시뮬레이션 된 장치 폴더에서 명령 프롬프트에서 다음 명령을 toobegin IoT 허브에서 메서드 호출을 수신 대기 하는 hello를 실행 합니다.

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub에 장치 앱 toolisten 직접 메서드 호출에 대 한 시뮬레이션 된][8]

1. Hello-직접-메서드 호출 폴더에 명령 프롬프트에서 다음 명령을 toocall hello 메서드가 장치에서 실행 시뮬레이션 IoT 허브에서:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 toocall 직접적인 방법][7]

1. hello 시뮬레이션 된 장치 응답 toohello 직접 메서드를 호출 합니다.

    ![Java IoT Hub 시뮬레이션 된 장치 응용 프로그램 응답 toohello 직접 메서드 호출][9]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 tooreact toomethods hello 클라우드 호출한 사용 했습니다. 또한 hello 장치에 대 한 메서드를 호출 하 고 hello 장치에서 hello 응답을 표시 하는 응용 프로그램을 만들었습니다.

tooexplore IoT 시나리오도 참조 [여러 장치에서 작업을 예약][lnk-devguide-jobs]합니다.

toolearn tooextend IoT 솔루션 및 일정 메서드를 여러 장치에서 호출 하는 방법 참조 hello [일정 및 브로드캐스트 작업] [ lnk-tutorial-jobs] 자습서입니다.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
