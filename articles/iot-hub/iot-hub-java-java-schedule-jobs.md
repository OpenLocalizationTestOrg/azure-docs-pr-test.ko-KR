---
title: "Azure IoT Hub (Java)와 aaaSchedule 작업 | Microsoft Docs"
description: "Azure IoT Hub tooschedule tooinvoke 직접적인 방법 작업 방법과 여러 장치에서 원하는 속성을 설정 합니다. Hello Azure IoT 장치 SDK를 사용 하 여 Java tooimplement hello 시뮬레이션 된 장치 앱과 hello Java tooimplement 서비스 응용 프로그램 toorun hello 작업에 대 한 Azure IoT 서비스 SDK에 대 한 합니다."
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>작업 예약 및 브로드캐스트(Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

수백만 개의 장치로 업데이트 하는 Azure IoT Hub tooschedule 및 추적 작업을 사용 합니다. 작업을 사용하여 다음을 수행합니다.

* desired 속성 업데이트
* tags 업데이트
* 직접 메서드 호출

작업이 다음이 작업 중 하나를 래핑하고 트랙 hello 일련의 장치에 대 한 실행. 장치로 이중 쿼리 hello hello 작업에 대해 실행 되는 장치 집합을 정의 합니다. 예를 들어 백 엔드 응용 프로그램 hello 장치를 다시 부팅 하는 장치 10, 000에서 작업 tooinvoke 직접 메서드를 사용할 수 있습니다. 장치로 이중 쿼리로 hello 일련의 장치를 지정 하 고 hello 작업 toorun 이후 시간에 예약 합니다. 각 hello 장치로 작업 추적 진행 상황 hello 수신 하 고 hello 재부팅 직접 메서드를 실행 합니다.

이러한 기능의 각각에 대해 자세히 toolearn 참조:

* 장치 쌍 및 속성: [장치 쌍 시작](iot-hub-java-java-twin-getstarted.md)
* 직접 메서드: [IoT Hub 개발자 가이드 - 직접 메서드](iot-hub-devguide-direct-methods.md) 및 [자습서: 직접 메서드 사용](iot-hub-java-java-direct-methods.md)

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* **lockDoor**라는 직접 메서드를 구현하는 장치 앱을 만듭니다. hello 장치 앱 hello 백 엔드 응용 프로그램에서 원하는 속성 변경 내용을 수신합니다.
* 백 엔드 앱을 만드는 작업 toocall hello 만들기 **lockDoor** 여러 장치에서 직접적인 방법입니다. 다른 작업이 toomultiple 장치를 업데이트 하는 원하는 속성을 보냅니다.

이 자습서의 hello 끝에 콘솔 장치 java 응용 프로그램 및 java 콘솔 백 엔드 응용 프로그램

**시뮬레이션 된 장치** tooyour IoT 허브를 연결 하는, 구현 hello **lockDoor** 메서드와 핸들 필요한 속성 변경 내용을 전송 합니다.

**작업 예약** 작업 toocall hello를 사용 하는 **lockDoor** 원하는 여러 장치에서 속성을 직접 메서드와 업데이트 hello 장치로 이중 합니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk](iot-hub-devguide-sdks.md) toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 조건

toocomplete 해야이 자습서에서는:

* 최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Toocreate hello 장치 id를 프로그래밍 방식으로 선호 하는 경우 hello의 hello 해당 섹션을 읽어 [Java를 사용 하 여 장치 tooyour IoT 허브 연결](iot-hub-java-java-getstarted.md#create-a-device-identity) 문서. Hello를 사용할 수도 있습니다 [iothub 탐색기](https://github.com/Azure/iothub-explorer) 도구 tooadd 장치 tooyour IoT 허브입니다.

## <a name="create-hello-service-app"></a>Hello 서비스 앱 만들기

이 섹션에서는 작업을 통해 다음을 수행하는 Java 콘솔 앱을 만듭니다.

* Hello 호출 **lockDoor** 여러 장치에서 직접적인 방법입니다.
* 원하는 속성 toomultiple 장치를 보냅니다.

toocreate hello 앱:

1. 개발 컴퓨터에서 `iot-java-schedule-jobs`라는 빈 폴더를 만듭니다.

1. Hello에 `iot-java-schedule-jobs` 폴더 라는 Maven 프로젝트를 만들 **작업 예약** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 긴 단일 명령입니다.

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 명령 프롬프트에서 이동 toohello `schedule-jobs` 폴더입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `schedule-jobs` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드. 이 종속성 하면 toouse hello **iot 서비스 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:

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

1. Hello를 열고 텍스트 편집기를 사용 하 여 `schedule-jobs\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. Hello 다음 추가 **가져올** 문 toohello 파일:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. 클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다. 대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Hello 메서드 toohello 다음 추가 **앱** 클래스 tooschedule 작업 tooupdate hello **건물** 및 **Floor** 원하는 hello 장치로 이중의 속성:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. 작업 toocall hello tooschedule **lockDoor** 메서드를 다음 메서드 toohello hello 추가 **앱** 클래스:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor 작업을 추가 메서드 toohello 다음 hello **앱** 클래스:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. 를 실행 하는 hello 작업의 hello 세부 정보에 대 한 tooquery hello 다음 메서드를 추가 합니다.

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. 업데이트 hello **주** 메서드 서명 tooinclude hello 다음 `throws` 절:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun 및 모니터 두 가지 작업은 순차적으로 hello 코드 toohello 다음 추가 **주** 메서드:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. 저장 후 닫기 hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` 파일

1. Hello 빌드 **작업 예약** 응용 프로그램 오류 수정 하십시오. 명령 프롬프트에서 이동 toohello `schedule-jobs` 폴더 및 다음 명령이 실행된 hello:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>장치 앱 만들기

이 섹션에서는 Java 콘솔 앱을 핸들 hello IoT Hub와 구현 hello 직접 메서드 호출에서 전송 되는 원하는 속성을 만듭니다.

1. Hello에 `iot-java-schedule-jobs` 폴더 라는 Maven 프로젝트를 만들 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 긴 단일 명령입니다.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다. 현재 toouse 장치로 이중 기능 hello MQTT 프로토콜을 사용 해야 합니다.

1. tooprint 장치로 이중 알림 toohello 콘솔에서 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint 메서드 알림 toohello 직접 콘솔에서 hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. IoT 허브에서 직접 메서드 호출 toohandle hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. 업데이트 hello **주** 메서드 서명 tooinclude hello 다음 `throws` 절:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. 다음 코드 toohello hello 추가 **주** 메서드:
    * IoT Hub와 장치 클라이언트 toocommunicate를 만듭니다.
    * 만들기는 **장치** toostore hello 장치로 이중 속성 개체입니다.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. toostart hello 장치 클라이언트 서비스를 추가할 코드 toohello 다음 hello **주** 메서드:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. hello 사용자 toopress hello에 대 한 toowait **Enter** 종료 하기 전에 키에 추가 코드 toohello의 끝 다음 hello hello **주** 메서드:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. 저장 후 닫기 hello `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. Hello 빌드 **시뮬레이션 된 장치** 응용 프로그램 오류 수정 하십시오. 명령 프롬프트에서 이동 toohello `simulated-device` 폴더 및 다음 명령이 실행된 hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Hello 앱 실행

준비 toorun hello 콘솔 응용 프로그램입니다.

1. Hello에서 명령 프롬프트에서 `simulated-device` hello 원하는 속성 변경 및 직접 메서드 호출에 대 한 수신 대기 하는 명령 toostart hello 장치 앱을 따라를 실행 하는 폴더:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello 장치 클라이언트 시작](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. Hello에 명령 프롬프트에서 `schedule-jobs` hello 명령 toorun hello 다음를 실행 하는 폴더 **작업 예약** 앱 toorun 두 개의 작업 서비스입니다. hello hello 원하는 속성 값을 먼저 설정, 두 번째 호출 hello hello 직접적인 방법:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub 서비스 앱에서 두 개의 작업을 작성함](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. hello 장치 앱 hello 원하는 속성을 변경 하 고 hello 직접 메서드 호출을 처리합니다.

    ![장치 클라이언트 hello 응답 toohello 변경 내용](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 두 개의 작업 toorun 백 엔드 응용 프로그램을 만들었습니다. hello ल ी 원하는 속성 값, 직접 메서드를 호출 하는 hello 두 번째 작업을 설정 합니다.

사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:

* Hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작](iot-hub-java-java-getstarted.md) 자습서입니다.
* Hello로 장치를 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬 설정)를 제어할 [직접 메서드를 사용 하 여](iot-hub-java-java-direct-methods.md) 자습서입니다.
