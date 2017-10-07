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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="6496f-104">장치 쌍 시작(Java)</span><span class="sxs-lookup"><span data-stu-id="6496f-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="6496f-105">이 자습서에서는 다음 두 개의 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="6496f-106">**add-tags-query**, 태그를 추가하고 장치 쌍을 쿼리하는 Java 백 엔드 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="6496f-107">**시뮬레이션 된 장치**, 하는 연결 되도록 tooyour IoT hub 및 보고서의 연결 상태를 보고 속성을 사용 하 여 Java 장치 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="6496f-108">hello 문서 [Azure IoT Sdk](iot-hub-devguide-sdks.md) toobuild를 사용할 수 있는, Azure IoT Sdk hello에 대 한 정보를 제공 장치와 백 엔드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="6496f-109">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="6496f-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="6496f-110">최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="6496f-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="6496f-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="6496f-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="6496f-112">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="6496f-112">An active Azure account.</span></span> <span data-ttu-id="6496f-113">계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="6496f-114">Toocreate hello 장치 id를 프로그래밍 방식으로 선호 하는 경우 hello의 hello 해당 섹션을 읽어 [Java를 사용 하 여 장치 tooyour IoT 허브 연결](iot-hub-java-java-getstarted.md#create-a-device-identity) 문서.</span><span class="sxs-lookup"><span data-stu-id="6496f-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="6496f-115">Hello 서비스 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6496f-115">Create hello service app</span></span>

<span data-ttu-id="6496f-116">IoT 허브에서 태그 toohello 장치로 이중 연결 된 메타 데이터 위치를 추가 하는 Java 응용 프로그램을 만들면이 섹션에서는 **myDeviceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="6496f-117">먼저 hello 앱 hello, 미국에에서 있는 장치에 대 한 한 다음 보고 셀룰러 네트워크에 연결 하는 장치에 대 한 IoT hub를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="6496f-118">개발 컴퓨터에서 `iot-java-twin-getstarted`라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="6496f-119">Hello에 `iot-java-twin-getstarted` 폴더 라는 Maven 프로젝트를 만들 **태그 추가-쿼리** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="6496f-120">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="6496f-121">명령 프롬프트에서 이동 toohello `add-tags-query` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="6496f-122">Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `add-tags-query` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="6496f-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="6496f-123">이 종속성 하면 toouse hello **iot 서비스 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="6496f-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6496f-124">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="6496f-125">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="6496f-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="6496f-126">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="6496f-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="6496f-127">저장 후 닫기 hello `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="6496f-128">Hello를 열고 텍스트 편집기를 사용 하 여 `add-tags-query\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="6496f-129">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="6496f-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="6496f-130">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="6496f-131">대체 `{youriothubconnectionstring}` hello에서 기록한 IoT 허브 연결 문자열로 *IoT 허브를 만듭니다.* 섹션:</span><span class="sxs-lookup"><span data-stu-id="6496f-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="6496f-132">업데이트 hello **주** 메서드 서명 tooinclude hello 다음 `throws` 절:</span><span class="sxs-lookup"><span data-stu-id="6496f-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="6496f-133">다음 코드 toohello hello 추가 **주** 메서드 toocreate hello **DeviceTwin** 및 **DeviceTwinDevice** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="6496f-134">hello **DeviceTwin** IoT hub와 hello 통신을 처리 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="6496f-135">hello **DeviceTwinDevice** 개체의 속성 및 태그가 hello 장치로 이중을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="6496f-136">Hello 다음 추가 `try/catch` toohello 차단 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="6496f-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="6496f-137">tooupdate hello **지역** 및 **공장** 프로그램 장치로 이중에 장치로 이중 태그 추가 hello에서 코드 다음 hello `try` 블록:</span><span class="sxs-lookup"><span data-stu-id="6496f-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="6496f-138">IoT 허브에서 tooquery hello 장치 트윈스 추가 코드 toohello 다음 hello `try` 후 hello 이전 단계에서 추가한 hello 코드 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="6496f-139">hello 코드는 두 개의 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-139">hello code runs two queries.</span></span> <span data-ttu-id="6496f-140">각 쿼리는 최대 100대의 장치를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="6496f-141">저장 후 닫기 hello `add-tags-query\src\main\java\com\mycompany\app\App.java` 파일</span><span class="sxs-lookup"><span data-stu-id="6496f-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="6496f-142">Hello 빌드 **태그 추가-쿼리** 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6496f-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="6496f-143">명령 프롬프트에서 이동 toohello `add-tags-query` 폴더 및 다음 명령이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="6496f-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="6496f-144">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6496f-144">Create a device app</span></span>

<span data-ttu-id="6496f-145">이 섹션에서는 tooIoT 허브 전송 되는 보고 된 속성 값을 설정 하 여 Java 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="6496f-146">Hello에 `iot-java-twin-getstarted` 폴더 라는 Maven 프로젝트를 만들 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="6496f-147">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="6496f-148">명령 프롬프트에서 이동 toohello `simulated-device` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="6496f-149">Hello를 열고 텍스트 편집기를 사용 하 여 `pom.xml` hello에 대 한 파일 `simulated-device` 폴더 hello 종속성 toohello 다음 추가 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="6496f-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="6496f-150">이 종속성 하면 toouse hello **iot 장치 클라이언트** IoT hub와 앱 toocommunicate 프로그램에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="6496f-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6496f-151">최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="6496f-152">Hello 다음 추가 **빌드** hello 후 노드 **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="6496f-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="6496f-153">이 구성은 지시 Maven toouse Java 1.8 toobuild hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="6496f-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="6496f-154">저장 후 닫기 hello `pom.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="6496f-155">Hello를 열고 텍스트 편집기를 사용 하 여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="6496f-156">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="6496f-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="6496f-157">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="6496f-158">교체 `{youriothubname}` 을 IoT 허브 이름으로, 및 `{yourdevicekey}` hello에 생성 된 hello 장치 키 값을 가진 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="6496f-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="6496f-159">이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="6496f-160">현재 toouse 장치로 이중 기능 hello MQTT 프로토콜을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="6496f-161">다음 코드 toohello hello 추가 **주** 메서드:</span><span class="sxs-lookup"><span data-stu-id="6496f-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="6496f-162">IoT Hub와 장치 클라이언트 toocommunicate를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="6496f-163">만들기는 **장치** toostore hello 장치로 이중 속성 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="6496f-164">다음 코드 toohello hello 추가 **주** 메서드 toocreate는 **connectivityType** 속성을 보고 하 고 tooIoT 허브 보내기:</span><span class="sxs-lookup"><span data-stu-id="6496f-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="6496f-165">추가 코드 toohello의 끝 다음 hello hello **주** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6496f-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="6496f-166">Hello에 대 한 대기 **Enter** 키 hello 장치로 이중 작업의 IoT Hub tooreport hello 상태에 대 한 시간을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="6496f-167">저장 후 닫기 hello `simulated-device\src\main\java\com\mycompany\app\App.java` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="6496f-168">Hello 빌드 **시뮬레이션 된 장치** 응용 프로그램 오류 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6496f-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="6496f-169">명령 프롬프트에서 이동 toohello `simulated-device` 폴더 및 다음 명령이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="6496f-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="6496f-170">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="6496f-170">Run hello apps</span></span>

<span data-ttu-id="6496f-171">준비 toorun hello 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="6496f-172">Hello에 명령 프롬프트에서 `add-tags-query` hello 명령 toorun hello 다음를 실행 하는 폴더 **태그 추가-쿼리** 서비스 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="6496f-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 tooupdate 값 태그를 지정 하 여 장치 쿼리 실행](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="6496f-174">Hello를 볼 수 있습니다 **공장** 및 **지역** 태그가 toohello 장치로 이중을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="6496f-175">hello 첫 번째 쿼리에서 장치를 반환 하지만 hello 둘째 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="6496f-176">Hello에 명령 프롬프트에서 `simulated-device` hello 명령 tooadd hello 다음를 실행 하는 폴더 **connectivityType** 속성 toohello 장치로 이중 보고:</span><span class="sxs-lookup"><span data-stu-id="6496f-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello를 추가 하는 장치 클라이언트 hello * * connectivityType * * 속성을 보고 합니다.](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="6496f-178">Hello에 명령 프롬프트에서 `add-tags-query` hello 명령 toorun hello 다음를 실행 하는 폴더 **태그 추가-쿼리** 응용 프로그램 서비스를 두 번째로:</span><span class="sxs-lookup"><span data-stu-id="6496f-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 허브 서비스 응용 프로그램 tooupdate 값 태그를 지정 하 여 장치 쿼리 실행](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="6496f-180">이제 장치 hello 전송한 **connectivityType** 속성 tooIoT 허브 hello 두 번째 쿼리에서 장치를 반납 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6496f-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6496f-181">Next steps</span></span>

<span data-ttu-id="6496f-182">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="6496f-183">백 엔드 앱에서 태그로 장치 메타 데이터를 추가 하 고 hello 장치로 이중에 장치 앱 tooreport 장치 연결 정보를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="6496f-184">또한 tooquery hello IoT Hub SQL 방식 쿼리 언어를 사용 하 여 장치로 이중 정보 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="6496f-185">사용 하 여 hello 리소스 toolearn을 어떻게 수행 하려면:</span><span class="sxs-lookup"><span data-stu-id="6496f-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="6496f-186">Hello 사용 하 여 장치에서 원격 분석 전송 [IoT 허브 시작](iot-hub-java-java-getstarted.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="6496f-187">Hello로 장치를 대화형으로 (예: 사용자 제어 응용 프로그램에서 팬 설정)를 제어할 [직접 메서드를 사용 하 여](iot-hub-java-java-direct-methods.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="6496f-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
