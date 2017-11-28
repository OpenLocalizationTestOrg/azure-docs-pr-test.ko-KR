---
title: "Azure IoT Hub (Java) aaaGet 시작 | Microsoft Docs"
description: "Toosend 장치-클라우드 tooAzure IoT Sdk를 사용 하 여 Java에 대 한 IoT Hub를 메시지 하는 방법을 알아봅니다. 시뮬레이션 된 장치 및 서비스 응용 프로그램 tooregister 장치, 메시지를 보낼 만들고 IoT 허브에서 메시지를 읽은 합니다."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="d1d04-104">Java를 사용 하 여 장치 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="d1d04-105">이 자습서의 hello 끝 세 개의 Java 콘솔 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="d1d04-106">**장치 만들기-id**, 장치 id를 만드는 연결 된 보안 키 tooconnect 장치 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="d1d04-107">**읽기-d2c-송신 된 메시지**, 장치 앱에서 보낸 hello 원격 분석을 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="d1d04-108">**시뮬레이션 된 장치**, 이전에 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하 고 MQTT 프로토콜 hello 하 여 모든 두 번째 원격 분석 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d04-109">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 앱 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="d1d04-110">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="d1d04-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d1d04-111">최신 hello [Java SE 개발 키트 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="d1d04-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="d1d04-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="d1d04-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="d1d04-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="d1d04-113">An active Azure account.</span></span> <span data-ttu-id="d1d04-114">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="d1d04-115">마지막 단계로 hello 적어 **기본 키** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="d1d04-116">클릭 **끝점** 및 hello **이벤트** 기본 제공 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="d1d04-117">Hello에 **속성** 블레이드를 기록해 둡니다 hello **이벤트 허브와 호환 가능한 이름** 및 hello **호환 이벤트 허브 끝점** 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="d1d04-118">**read-d2c-messages** 앱을 만들 때 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Azure Portal IoT Hub 메시징 블레이드][6]

<span data-ttu-id="d1d04-120">IoT Hub를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-120">You have now created your IoT hub.</span></span> <span data-ttu-id="d1d04-121">해야 hello IoT Hub 호스트 이름, IoT 허브 연결 문자열, IoT 허브에 대 한 기본 키, 이벤트 허브와 호환 가능한 이름 및 이벤트 허브 호환 끝점 toocomplete이이 자습서를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="d1d04-122">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="d1d04-122">Create a device identity</span></span>
<span data-ttu-id="d1d04-123">이 섹션에서는 hello id 레지스트리에 IoT 허브에서에서 장치 id를 작성 하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="d1d04-124">장치 id 레지스트리에 hello에 항목이 없는 경우 tooIoT 허브를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="d1d04-125">자세한 내용은 참조 hello **Id 레지스트리에** hello 섹션 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d1d04-126">이 콘솔 응용 프로그램을 실행 하면 고유한 장치 ID를 생성 및 메시지 tooIoT 허브를 키 장치-클라우드 보낼 때 장치가 tooidentify 자체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="d1d04-127">iot-java-get-started라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="d1d04-128">Hello iot-java-get 시작 폴더에서 라는 Maven 프로젝트를 만듭니다 **장치 만들기-id** hello 다음 명령 프롬프트에서 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="d1d04-129">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="d1d04-130">명령 프롬프트 toohello 장치 만들기-id 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="d1d04-131">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 장치 만들기-id 폴더에 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d1d04-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="d1d04-132">이 종속성 패키지를 통해 있습니다 toouse hello iot 서비스 클라이언트 응용 프로그램에서:</span><span class="sxs-lookup"><span data-stu-id="d1d04-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d1d04-133">최신 버전의 hello 확인할 수 있습니다 **iot 서비스 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-service-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="d1d04-134">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="d1d04-135">텍스트 편집기를 사용 하 여 hello create-device-identity\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="d1d04-136">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="d1d04-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="d1d04-137">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스를 대체 **{yourhubconnectionstring}** hello로 값에 명시 된 이전 버전:</span><span class="sxs-lookup"><span data-stu-id="d1d04-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="d1d04-138">Hello의 hello 서명을 수정 **주** 메서드 tooinclude 예외를 다음과 같이 hello:</span><span class="sxs-lookup"><span data-stu-id="d1d04-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="d1d04-139">Hello hello의 hello 본문으로 코드를 다음 추가 **주** 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1d04-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="d1d04-140">이 코드는 IoT Hub ID 레지스트리에 *javadevice* 라는 장치를 만듭니다(없는 경우).</span><span class="sxs-lookup"><span data-stu-id="d1d04-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="d1d04-141">다음 hello 장치 ID와 키 나중에 필요를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="d1d04-142">저장 하 고 hello App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="d1d04-143">toobuild hello **장치 만들기-id** Maven에서 사용 하 여 앱 hello 다음 hello 장치 만들기-id 폴더에 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="d1d04-144">toorun hello **장치 만들기-id** Maven에서 사용 하 여 앱 hello 다음 hello 장치 만들기-id 폴더에 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="d1d04-145">Hello 메모 **장치 ID** 및 **장치 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="d1d04-146">이 값이 필요 하면 이러한 나중 tooIoT 장치로 허브를 연결 하는 앱을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="d1d04-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d04-147">IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d1d04-148">장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d1d04-149">앱은 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="d1d04-150">자세한 내용은 참조 hello [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="d1d04-151">장치-클라우드 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="d1d04-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="d1d04-152">이 섹션에서는 IoT Hub에서 장치-클라우드 메시지를 읽는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="d1d04-153">IoT hub를 노출 한 [이벤트 허브][lnk-event-hubs-overview]-호환 되는 끝점 tooenable tooread 장치-클라우드 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="d1d04-154">단순 tookeep 항목을이 자습서에서는 처리량이 높은 배포에 적합 하지 않은 기본 판독기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="d1d04-155">hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서에서는 배율로 tooprocess 장치-클라우드 메시지 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="d1d04-156">hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] 자습서 tooprocess 이벤트 허브에서 메시지를 하 고는 적용 가능한 toohello IoT 허브 이벤트 허브 호환 되지 않는 끝점 하는 방법에 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d04-157">hello 항상 장치-클라우드 메시지 도착 읽기에 대 한 이벤트 허브 호환 끝점 hello AMQP 프로토콜이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="d1d04-158">Hello에서 만든 hello iot-java-get 시작 폴더에 *장치 id를 만드는* 섹션, 호출 Maven 프로젝트 만들기 **읽기-d2c-송신 된 메시지** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="d1d04-159">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="d1d04-160">명령 프롬프트 toohello 읽기-d2c-송신 된 메시지 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="d1d04-161">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 메시지 d2c-읽기-폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d1d04-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="d1d04-162">이 종속성 toouse hello eventhubs 클라이언트 패키지를 하면 앱 tooread hello 호환 이벤트 허브 끝점에서의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="d1d04-163">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="d1d04-164">텍스트 편집기를 사용 하 여 hello read-d2c-messages\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="d1d04-165">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="d1d04-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="d1d04-166">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="d1d04-167">대체 **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, 및 **{youreventhubcompatiblename}** hello 값이 이전에 기록한:</span><span class="sxs-lookup"><span data-stu-id="d1d04-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="d1d04-168">Hello 다음 추가 **receiveMessages** 메서드 toohello **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="d1d04-169">이 메서드는 만듭니다는 **EventHubClient** tooconnect toohello 호환 이벤트 허브 끝점 인스턴스 선택한 비동기적으로 만듭니다는 **PartitionReceiver** 인스턴스 tooread 이벤트 허브에서 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="d1d04-170">지속적으로 루프를 실행 하 고 hello 앱이 종료 될 때까지 hello 메시지 세부 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="d1d04-171">이 메서드는 읽을 수 있도록 hello 수신기만 보낸 메시지 tooIoT 허브를 실행 하는 hello 수신기가 시작 되 면 hello 수신기를 만들 때 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="d1d04-172">이 방법은 hello 메시지의 현재 집합을 볼 수 있도록 테스트 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="d1d04-173">프로덕션 환경에서 코드 있어야-자세한 정보에 대 한 모든 hello 메시지를 처리 하도록 확인을 참조 하세요 hello [어떻게 tooprocess IoT Hub 장치-클라우드 메시지] [ lnk-process-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="d1d04-174">Hello의 hello 서명을 수정 **주** 메서드 tooinclude 예외를 다음과 같이 hello:</span><span class="sxs-lookup"><span data-stu-id="d1d04-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="d1d04-175">다음 코드 toohello hello 추가 **주** hello에 대 한 메서드 **앱** 클래스.</span><span class="sxs-lookup"><span data-stu-id="d1d04-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="d1d04-176">이 코드에서는 두 hello **EventHubClient** 및 **PartitionReceiver** 인스턴스를 사용 하면 tooclose hello 앱 메시지 처리를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="d1d04-177">이 코드는 hello F1 (무료) 계층에 있는 IoT 허브를 만든 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="d1d04-178">무료 IoT Hub에는 "0" 및 "1"이라는 두 개의 파티션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="d1d04-179">저장 하 고 hello App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="d1d04-180">toobuild hello **읽기-d2c-송신 된 메시지** Maven에서 사용 하 여 앱 hello 다음 hello 메시지 d2c-읽기-폴더에 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="d1d04-181">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d1d04-181">Create a device app</span></span>
<span data-ttu-id="d1d04-182">이 섹션에서는 tooan IoT hub 장치-클라우드 메시지를 전송 하는 장치를 시뮬레이션 하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="d1d04-183">Hello에서 만든 hello iot-java-get 시작 폴더에 *장치 id를 만드는* 섹션, 호출 Maven 프로젝트 만들기 **시뮬레이션 된 장치** hello 다음 명령 프롬프트에서 명령을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="d1d04-184">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="d1d04-185">명령 프롬프트 toohello 시뮬레이션 된 장치 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="d1d04-186">텍스트 편집기를 사용 하 여 hello pom.xml 파일 hello 시뮬레이션 된 장치 폴더에서 열고 추가 종속성 toohello 다음 hello **종속성** 노드.</span><span class="sxs-lookup"><span data-stu-id="d1d04-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="d1d04-187">이 종속성 있습니다 toouse hello iothub java 클라이언트에서에서 패키지를 하면 앱 toocommunicate IoT 허브와 tooserialize Java 개체 tooJSON 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d1d04-188">최신 버전의 hello 확인할 수 있습니다 **iot 장치 클라이언트** 를 사용 하 여 [Maven 검색][lnk-maven-device-search]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="d1d04-189">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="d1d04-190">텍스트 편집기를 사용 하 여 hello simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="d1d04-191">Hello 다음 추가 **가져올** 문 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="d1d04-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="d1d04-192">클래스 수준 변수 toohello 다음 hello 추가 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="d1d04-193">교체 **{youriothubname}** 을 IoT 허브 이름으로, 및 **{yourdevicekey}** hello에 생성 된 hello 장치 키 값을 가진 *장치 id를 만드는* 섹션:</span><span class="sxs-lookup"><span data-stu-id="d1d04-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="d1d04-194">이 샘플 응용 프로그램 hello를 사용 하 여 **프로토콜** 를 인스턴스화할 때 변수는 **DeviceClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="d1d04-195">IoT Hub와 hello MQTT, AMQP 또는 HTTP 프로토콜 toocommunicate 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="d1d04-196">중첩 된 hello 다음 추가 **TelemetryDataPoint** hello 내부 클래스 **앱** toospecify hello 원격 분석 데이터 tooyour IoT 허브를 전송 하는 사용자 장치 클래스:</span><span class="sxs-lookup"><span data-stu-id="d1d04-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="d1d04-197">중첩 된 hello 다음 추가 **EventCallback** hello 내부 클래스 **앱** 클래스 toodisplay hello 승인 상태 hello IoT 허브는 hello 장치 응용 프로그램에서 메시지를 처리할 때를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="d1d04-198">이 메서드도 hello 메시지 처리 되 면 hello 응용 프로그램의 주 스레드에서를 hello에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="d1d04-199">중첩 된 hello 다음 추가 **MessageSender** hello 내부 클래스 **앱** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="d1d04-200">hello **실행** 이 클래스의 메서드와 샘플 원격 분석 데이터 toosend tooyour IoT 허브를 생성 하 고 hello 다음 메시지를 보내기 전에 승인을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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

    <span data-ttu-id="d1d04-201">이 메서드는 1 초 hello IoT hub hello 이전 메시지를 승인한 후 새 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="d1d04-202">hello 메시지 hello deviceId 가진 JSON 직렬화 된 개체가 포함 하 고 숫자 toosimulate 온도 센서 및 습도 센서를 임의로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="d1d04-203">Hello 대체 **주** 스레드 toosend 장치-클라우드 메시지 tooyour IoT 허브를 만드는 코드를 다음 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="d1d04-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="d1d04-204">저장 하 고 hello App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="d1d04-205">toobuild hello **시뮬레이션 된 장치** Maven에서 사용 하 여 앱 hello 다음 hello 시뮬레이션 된 장치 폴더에서 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="d1d04-206">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d1d04-207">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="d1d04-208">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="d1d04-208">Run hello apps</span></span>

<span data-ttu-id="d1d04-209">준비 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d1d04-210">Hello 읽기 d2c 폴더에 명령 프롬프트에서 다음 명령 toobegin IoT 허브에서 첫 번째 파티션에 hello를 모니터링 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Java IoT 허브 서비스 응용 프로그램 toomonitor 장치-클라우드 메시지][7]

2. <span data-ttu-id="d1d04-212">Hello 시뮬레이션 된 장치 폴더에서 명령 프롬프트에서 다음 원격 분석 데이터 tooyour IoT 허브를 보내는 명령 toobegin hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Java IoT Hub 장치 앱 toosend 장치-클라우드 메시지][8]

3. <span data-ttu-id="d1d04-214">hello **사용량** hello에 바둑판식으로 배열 [Azure 포털] [ lnk-portal] 표시 hello 보낸 메시지 toohello IoT 허브의 수:</span><span class="sxs-lookup"><span data-stu-id="d1d04-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure 포털 사용량 타일 보여 주는 수가 전송 된 메시지 tooIoT 허브][43]

## <a name="next-steps"></a><span data-ttu-id="d1d04-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1d04-216">Next steps</span></span>
<span data-ttu-id="d1d04-217">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d1d04-218">이 장치 identity tooenable hello 장치 앱 toosend 장치-클라우드 메시지 toohello IoT 허브를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="d1d04-219">또한 hello IoT 허브에서 수신 하는 hello 메시지를 표시 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="d1d04-220">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d1d04-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d1d04-221">[장치 연결][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="d1d04-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="d1d04-222">[장치 관리 시작][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="d1d04-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="d1d04-223">[Azure IoT Hub 시작][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="d1d04-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="d1d04-224">toolearn tooextend 배율 사용할 때 IoT 솔루션 및 프로세스 장치-클라우드 메시지를 확인 하려면 어떻게 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d04-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
