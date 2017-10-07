---
title: "Azure IoT Hub 장치 트윈스 (Java) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toouse Azure IoT Hub 장치 트윈스 tooadd 태그를 삽입 하 고 IoT Hub 쿼리를 사용 합니다. Hello Azure IoT 장치 SDK를 사용 하 여 Java tooimplement hello 장치 응용 프로그램 및 Java tooimplement hello 태그를 추가 하 고 hello IoT Hub 쿼리를 실행 하는 서비스 응용 프로그램에 대 한 Azure IoT 서비스 SDK hello에 대 한 합니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>장치 쌍 시작(Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

이 자습서에서는 다음 두 개의 Java 콘솔 앱을 만듭니다.

* **add-tags-query**, 태그를 추가하고 장치 쌍을 쿼리하는 Java 백 엔드 앱입니다.
* **시뮬레이션 된 장치**, 하는 연결 되도록 tooyour IoT hub 및 보고서의 연결 상태를 보고 속성을 사용 하 여 Java 장치 응용 프로그램입니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk](iot-hub-devguide-sdks.md) toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.

toocomplete 해야이 자습서에서는:

* 최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Toocreate hello 장치 id를 프로그래밍 방식으로 선호 하는 경우 hello의 hello 해당 섹션을 읽어 [Java를 사용 하 여 장치 tooyour IoT 허브 연결](iot-hub-java-java-getstarted.md#create-a-device-identity) 문서.

## <a name="create-hello-service-app"></a>Hello 서비스 앱 만들기

IoT 허브에서 태그 toohello 장치로 이중 연결 된 메타 데이터 위치를 추가 하는 Java 응용 프로그램을 만들면이 섹션에서는 **myDeviceId**합니다. 먼저 hello 앱 hello, 미국에에서 있는 장치에 대 한 한 다음 보고 셀룰러 네트워크에 연결 하는 장치에 대 한 IoT hub를 쿼리 합니다.

1. 개발 컴퓨터에서 `iot-java-twin-getstarted`라는 빈 폴더를 만듭니다.

1. Hello에 `iot-java-twin-getstarted` 폴더 라는 Maven 프로젝트를 만들 **태그 추가-쿼리** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 긴 단일 명령입니다.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 명령 프롬프트에서 이동 toohello `add-tags-query` 폴더입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `add-tags-query` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드. 이 종속성 하면 toouse hello **iot 서비스 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > 최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.

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

1. 저장 후 닫기 hello `pom.xml` 파일입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `add-tags-query\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. Hello 다음 추가 **가져올** 문 toohello 파일:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. 클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다. 대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. 업데이트 hello **주** 메서드 서명 tooinclude hello 다음 `throws` 절:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. 다음 코드 toohello hello 추가 **주** 메서드 toocreate hello **DeviceTwin** 및 **DeviceTwinDevice** 개체입니다. hello **DeviceTwin** IoT hub와 hello 통신을 처리 하는 개체입니다. hello **DeviceTwinDevice** 개체의 속성 및 태그가 hello 장치로 이중을 나타냅니다.

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Hello 다음 추가 `try/catch` toohello 차단 **주** 메서드:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. tooupdate hello **지역** 및 **공장** 프로그램 장치로 이중에 장치로 이중 태그 추가 hello에서 코드 다음 hello `try` 블록:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. IoT 허브에서 tooquery hello 장치 트윈스 추가 코드 toohello 다음 hello `try` 후 hello 이전 단계에서 추가한 hello 코드 블록입니다. hello 코드는 두 개의 쿼리를 실행합니다. 각 쿼리는 최대 100대의 장치를 반환합니다.

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. 저장 후 닫기 hello `add-tags-query\src\main\java\com\mycompany\app\App.java` 파일

1. Hello 빌드 **태그 추가-쿼리** 응용 프로그램 오류 수정 하십시오. 명령 프롬프트에서 이동 toohello `add-tags-query` 폴더 및 다음 명령이 실행된 hello:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>장치 앱 만들기

이 섹션에서는 tooIoT 허브 전송 되는 보고 된 속성 값을 설정 하 여 Java 콘솔 응용 프로그램을 만들 수 있습니다.

1. Hello에 `iot-java-twin-getstarted` 폴더 라는 Maven 프로젝트를 만들 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 긴 단일 명령입니다.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 명령 프롬프트에서 이동 toohello `simulated-device` 폴더입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `simulated-device` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드. 이 종속성 하면 toouse hello **iot 장치 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > 최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.

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

1. 저장 후 닫기 hello `pom.xml` 파일입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.

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
    ```

    이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다. 현재 toouse 장치로 이중 기능 hello MQTT 프로토콜을 사용 해야 합니다.

1. 다음 코드 toohello hello 추가 **주** 메서드:
    * IoT Hub와 장치 클라이언트 toocommunicate를 만듭니다.
    * 만들기는 **장치** toostore hello 장치로 이중 속성 개체입니다.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. 다음 코드 toohello hello 추가 **주** 메서드 toocreate는 **connectivityType** 속성을 보고 하 고 tooIoT 허브 보내기:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. 추가 코드 toohello의 끝 다음 hello hello **주** 메서드. Hello에 대 한 대기 **Enter** 키 hello 장치로 이중 작업의 IoT Hub tooreport hello 상태에 대 한 시간을 허용 합니다.

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. 저장 후 닫기 hello `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. Hello 빌드 **시뮬레이션 된 장치** 응용 프로그램 오류 수정 하십시오. 명령 프롬프트에서 이동 toohello `simulated-device` 폴더 및 다음 명령이 실행된 hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hello 앱 실행

준비 toorun hello 콘솔 응용 프로그램입니다.

1. Hello에 명령 프롬프트에서 `add-tags-query` hello 명령 toorun hello 다음를 실행 하는 폴더 **태그 추가-쿼리** 서비스 응용 프로그램:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 tooupdate 값 태그를 지정 하 여 장치 쿼리 실행](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Hello를 볼 수 있습니다 **공장** 및 **지역** 태그가 toohello 장치로 이중을 추가 합니다. hello 첫 번째 쿼리에서 장치를 반환 하지만 hello 둘째 하지 않습니다.

1. Hello에 명령 프롬프트에서 `simulated-device` hello 명령 tooadd hello 다음를 실행 하는 폴더 **connectivityType** 속성 toohello 장치로 이중 보고:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello를 추가 하는 장치 클라이언트 hello * * connectivityType * * 속성을 보고 합니다.](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. Hello에 명령 프롬프트에서 `add-tags-query` hello 명령 toorun hello 다음를 실행 하는 폴더 **태그 추가-쿼리** 응용 프로그램 서비스를 두 번째로:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 tooupdate 값 태그를 지정 하 여 장치 쿼리 실행](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    이제 장치 hello 전송한 **connectivityType** 속성 tooIoT 허브 hello 두 번째 쿼리에서 장치를 반납 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 백 엔드 앱에서 태그로 장치 메타 데이터를 추가 하 고 hello 장치로 이중에 장치 앱 tooreport 장치 연결 정보를 작성 합니다. 또한 tooquery hello IoT Hub SQL 방식 쿼리 언어를 사용 하 여 장치로 이중 정보 hello 하는 방법을 배웠습니다.

사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:

* Hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작](iot-hub-java-java-getstarted.md) 자습서입니다.
* Hello로 장치를 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬 설정)를 제어할 [직접 메서드를 사용 하 여](iot-hub-java-java-direct-methods.md) 자습서입니다.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
