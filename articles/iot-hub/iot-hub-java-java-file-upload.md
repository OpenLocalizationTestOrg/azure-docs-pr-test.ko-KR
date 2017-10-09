---
title: "장치 tooAzure Java와 함께 IoT 허브에서에서 aaaUpload 파일 | Microsoft Docs"
description: "어떻게 tooupload Java 용 Azure IoT 장치 SDK를 사용 하 여 장치 toohello 클라우드에서 파일입니다. 업로드된 파일은 Azure Storage blob 컨테이너에 저장됩니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>IoT Hub와 장치 toohello 클라우드에서 파일 업로드

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Hello에 hello 코드에 기반 하는이 자습서 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-java-java-c2d.md) 자습서 tooshow 있습니다 어떻게 toouse hello [IoT 허브의 업로드 기능 파일](iot-hub-devguide-file-upload.md) tooupload 파일 너무[ Azure blob 저장소](../storage/index.md)합니다. 표시 하는 hello 자습서에:

- 파일을 업로드하기 위한 Azure blob URI를 장치에 안전하게 제공합니다.
- 앱 백 엔드에서 IoT Hub 파일 업로드 알림 tootrigger 처리 hello 파일 hello를 사용 합니다.

hello [IoT 허브 시작](iot-hub-java-java-getstarted.md) 및 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-java-java-c2d.md) hello 장치-클라우드 및 클라우드-장치 메시징의 기본 기능 IoT Hub를 보여 주는 자습서입니다. hello [프로세스 장치-클라우드 메시지](iot-hub-java-java-process-d2c.md) 자습서에서는 Azure blob 저장소에 양방향 tooreliably 저장소 장치-클라우드 메시지를 설명 합니다. 그러나 일부 시나리오에서는 장치가 IoT Hub 수락 하는 hello 상대적으로 작은 하는 장치-클라우드 메시지에 보낼 hello 데이터 쉽게 매핑할 수 없습니다. 예:

* 이미지가 포함된 대형 파일
* 비디오
* 자주 샘플링되는 진동 데이터
* 특정 형태의 전처리된 데이터

이러한 파일은 일반적으로 일괄 처리와 같은 도구를 사용 하 여 hello 클라우드에서 [Azure Data Factory](../data-factory/index.md) 또는 hello [Hadoop](../hdinsight/index.md) 스택 합니다. 장치에서 tooupland 파일 필요할 때 IoT 허브의 안정성 및 보안 hello 여전히 사용할 수 있습니다.

이 자습서의 hello 끝에 두 개의 Java 콘솔 응용 프로그램 실행합니다.

* **시뮬레이션 된 장치**, hello [IoT Hub와 송신 클라우드-장치 메시지] 자습서에서 만든 hello 응용 프로그램의 수정된 된 버전입니다. 이 앱이 IoT 허브에서 제공 하는 SAS URI를 사용 하 여 파일 toostorage를 업로드 합니다.
* **read-file-upload-notification** - IoT Hub에서 파일 업로드 알림을 받습니다.

> [!NOTE]
> IoT Hub는 Azure IoT 장치 SDK를 통해 많은 장치 플랫폼 및 언어(C, .NET 및 Javascript 포함)를 지원합니다. Toohello 참조 [Azure IoT 개발자 센터] 방법에 대 한 단계별 지침에 대 한 tooconnect 프로그램 장치 tooAzure IoT 허브입니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>장치 앱에서 파일 업로드

이 섹션에서는 hello 장치 응용 프로그램에서 만든 수정 하면 [IoT Hub와 클라우드-장치 메시지를 보낼](iot-hub-java-java-c2d.md) tooupload 파일 tooIoT 허브입니다.

1. 이미지 파일 toohello 복사 `simulated-device` 폴더 이름을 바꿉니다 `myimage.png`합니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. Hello 변수 선언 toohello 추가 **앱** 클래스:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess 업로드 상태 콜백 메시지를 파일, hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload 이미지 tooIoT 허브 메서드 toohello 다음 hello 추가 **앱** 클래스 tooupload tooIoT 허브 이미지:

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. Hello 수정 **주** 메서드 toocall hello **uploadFile** hello 다음 코드 조각에에서 나와 있는 것 처럼 메서드:

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. 사용 하 여 hello 다음 명령은 toobuild hello **시뮬레이션 된 장치** 응용 프로그램 및 오류를 확인 합니다.

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>파일 업로드 알림 수신

이 섹션에서는 IoT Hub에서 파일 업로드 알림 메시지를 수신하는 Java 콘솔 앱을 만듭니다.

Hello 필요한 **iothubowner** 이 여기서 IoT Hub toocomplete에 대 한 연결 문자열입니다. Hello에서 hello 연결 문자열을 찾을 수 있습니다 [Azure 포털](https://portal.azure.com/) hello에 **공유 액세스 정책** 블레이드입니다.

1. 라는 Maven 프로젝트 만들기 **파일 업로드 알림 읽기** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다. 이 명령은 긴 단일 명령입니다.

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. 명령 프롬프트에서 새 toohello 이동 `read-file-upload-notification` 폴더입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `read-file-upload-notification` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드. Toouse hello hello 종속성을 추가 하면 **java 서비스 클라이언트 iothub** IoT 허브 서비스와 응용 프로그램 toocommunicate 프로그램에서 패키지:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > 최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.

1. 저장 후 닫기 hello `pom.xml` 파일입니다.

1. Hello를 열고 텍스트 편집기를 사용 하 여 `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. Hello 다음 추가 **가져올** 문 toohello 파일:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. 클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. hello 파일 업로드 toohello 콘솔에 대 한 정보 tooprint hello 다음 추가 클래스 toohello 중첩 **앱** 클래스:

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. 파일 업로드 알림을 수신 하는 toostart hello 스레드 추가 코드 toohello 다음 hello **주** 메서드:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. 저장 후 닫기 hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` 파일입니다.

1. 사용 하 여 hello 다음 명령은 toobuild hello **파일 업로드 알림 읽기** 응용 프로그램 및 오류를 확인 합니다.

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행

이제 준비 toorun hello 응용 프로그램 됩니다.

Hello에서 명령 프롬프트에서 `read-file-upload-notification` 폴더를 hello 다음 명령을 실행 합니다.

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Hello에서 명령 프롬프트에서 `simulated-device` 폴더를 hello 다음 명령을 실행 합니다.

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

hello 다음 스크린 샷에서 hello 출력을에서 보여 줍니다 hello **시뮬레이션 된 장치** 앱:

![simulated-device 앱의 출력](media/iot-hub-java-java-upload/simulated-device.png)

hello 다음 스크린 샷에서 hello 출력을에서 보여 줍니다 hello **파일 업로드 알림 읽기** 앱:

![read-file-upload-notification 앱의 출력](media/iot-hub-java-java-upload/read-file-upload-notification.png)

구성한 hello 저장소 컨테이너에서 hello 포털 tooview hello 업로드 파일을 사용할 수 있습니다.

![업로드된 파일](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 toouse hello 파일에서 IoT Hub toosimplify 파일 업로드 장치에서의 기능을 업로드 하는 방법을 배웠습니다. 다음 문서는 hello로 tooexplore IoT 허브 기능 및 시나리오를 진행할 수 있습니다.

* [프로그래밍 방식으로 IoT Hub 만들기][lnk-create-hub]
* [소개 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


