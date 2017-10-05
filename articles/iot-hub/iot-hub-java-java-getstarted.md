---
title: "Azure IoT Hub 시작(Java) | Microsoft Docs"
description: "Java용 IoT SDK를 사용하여 Azure IoT Hub에 장치-클라우드 메시지를 보내는 방법을 알아봅니다. 시뮬레이션된 장치 및 서비스 앱을 만들어서 장치를 등록하고 메시지를 전송하고 IoT Hub의 메시지를 읽습니다."
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
ms.openlocfilehash: 707356a49970bcd76a55ee1b8a6fbddf6a6ba390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a><span data-ttu-id="73f33-104">Java를 사용하여 IoT Hub에 장치 연결</span><span class="sxs-lookup"><span data-stu-id="73f33-104">Connect your device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="73f33-105">이 자습서의 끝 부분에서 다음의 세 가지 Java 콘솔 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="73f33-106">**create-device-identity**는 장치 ID 및 연결된 보안 키를 만들어 장치 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-106">**create-device-identity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="73f33-107">**read-d2c-messages**는 장치 앱에서 보낸 원격 분석을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-107">**read-d2c-messages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="73f33-108">**simulated-device**는 앞에서 만든 장치 ID로 IoT Hub에 연결하고 MQTT 프로토콜을 사용하여 매초마다 원격 분석 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="73f33-109">[Azure IoT SDKs][lnk-hub-sdks] 문서는 장치와 솔루션 백 엔드에서 실행하기 위해 두 앱을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 관한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>

<span data-ttu-id="73f33-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="73f33-111">최신 [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="73f33-111">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="73f33-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="73f33-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="73f33-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="73f33-113">An active Azure account.</span></span> <span data-ttu-id="73f33-114">계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="73f33-115">마지막 단계로 **기본 키** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-115">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="73f33-116">그런 다음 **끝점** 및 **이벤트** 기본 제공 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-116">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="73f33-117">**속성** 블레이드에서 **Event Hub 호환 이름** 및 **Event Hub 호환 끝점** 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-117">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="73f33-118">**read-d2c-messages** 앱을 만들 때 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Azure Portal IoT Hub 메시징 블레이드][6]

<span data-ttu-id="73f33-120">IoT Hub를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-120">You have now created your IoT hub.</span></span> <span data-ttu-id="73f33-121">이 자습서를 완료하는 데 필요한 IoT Hub 호스트 이름, IoT Hub 연결 문자열, IoT Hub 기본 키, Event Hub 호환 이름 및 Event Hub 호환 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-121">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="73f33-122">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="73f33-122">Create a device identity</span></span>
<span data-ttu-id="73f33-123">이 섹션에서는 IoT Hub의 ID 레지스트리에서 장치 ID를 만드는 Java 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-123">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="73f33-124">ID 레지스트리에 항목이 없는 경우 장치를 IoT Hub에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-124">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="73f33-125">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]의 **ID 레지스트리** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73f33-125">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="73f33-126">이 콘솔 앱을 실행하면 장치-클라우드 메시지를 IoT Hub로 보낼 때 장치가 자체적으로 ID를 식별하는 데 사용할 수 있는 고유한 장치 ID와 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-126">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="73f33-127">iot-java-get-started라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="73f33-128">명령 프롬프트에서 다음 명령을 사용하여 iot-java-get-started 폴더에 **create-device-identity**라는 새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-128">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="73f33-129">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="73f33-130">명령 프롬프트에서 create-device-identity 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-130">At your command prompt, navigate to the create-device-identity folder.</span></span>

3. <span data-ttu-id="73f33-131">텍스트 편집기를 사용하여 create-device-identity 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-131">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="73f33-132">이러한 종속성으로 인해 앱에서 iot-service-client 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-132">This dependency enables you to use the iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="73f33-133">[Maven 검색][lnk-maven-service-search]을 사용하여 **iot-service-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-133">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="73f33-134">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-134">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="73f33-135">텍스트 편집기를 사용하여 create-device-identity\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-135">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="73f33-136">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-136">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="73f33-137">**App** 클래스에 다음 클래스 수준 변수를 추가하고 **{yourhubconnectionstring}**를 앞에서 기록해둔 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-137">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="73f33-138">**main** 메서드의 서명을 수정하여 다음과 같은 예외를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-138">Modify the signature of the **main** method to include the exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="73f33-139">**main** 메서드의 본문으로 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-139">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="73f33-140">이 코드는 IoT Hub ID 레지스트리에 *javadevice* 라는 장치를 만듭니다(없는 경우).</span><span class="sxs-lookup"><span data-stu-id="73f33-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="73f33-141">그런 다음 나중에 필요한 장치 ID와 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-141">It then displays the device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
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
      // If the device already exists.
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

10. <span data-ttu-id="73f33-142">App.java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-142">Save and close the App.java file.</span></span>

11. <span data-ttu-id="73f33-143">Maven을 사용하여 **create-device-identity** 앱을 빌드하려면 create-device-identity 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-143">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="73f33-144">Maven을 사용하여 **create-device-identity** 앱을 실행하려면 create-device-identity 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-144">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="73f33-145">**장치 ID**와 **장치 키**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-145">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="73f33-146">나중에 장치로 IoT Hub에 연결하는 앱을 만들 때 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-146">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="73f33-147">IoT Hub ID 레지스트리는 장치 ID만 저장하여 IoT Hub에 보안 액세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-147">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="73f33-148">보안 자격 증명으로 사용하기 위해 장치 ID 및 키와 개별 장치에 대해 액세스하지 못하도록 설정할 수 있는 사용/사용 안 함 플래그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-148">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="73f33-149">앱이 다른 장치별 메타데이터를 저장해야 할 경우 앱별 저장소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-149">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="73f33-150">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73f33-150">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="73f33-151">장치-클라우드 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="73f33-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="73f33-152">이 섹션에서는 IoT Hub에서 장치-클라우드 메시지를 읽는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="73f33-153">IoT Hub가 [Event Hub][lnk-event-hubs-overview] 호환 끝점을 노출하여 장치-클라우드 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="73f33-154">작업을 단순화하기 위해 이 자습서에서는 처리량이 높은 배포용이 아닌 기본적인 판독기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-154">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="73f33-155">[장치-클라우드 메시지 처리][lnk-process-d2c-tutorial] 자습서는 대량의 장치-클라우드 메시지를 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-155">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="73f33-156">[Event Hubs 시작][lnk-eventhubs-tutorial] 자습서는 Event Hubs의 메시지를 처리하는 방법에 대해 추가 정보를 제공하며 IoT Hub Event Hub 호환 끝점에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-156">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="73f33-157">장치-클라우드 메시지를 읽는 Event Hub와 호환 가능한 끝점은 항상 AMQP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-157">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="73f33-158">*장치 ID 만들기* 섹션에서 만든 iot-java-get-started 폴더의 명령 프롬프트에서 다음 명령을 사용하여 **read-d2c-messages**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-158">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="73f33-159">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="73f33-160">명령 프롬프트에서 read-d2c-messages 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-160">At your command prompt, navigate to the read-d2c-messages folder.</span></span>

3. <span data-ttu-id="73f33-161">텍스트 편집기를 사용하여 read-d2c-messages 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-161">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="73f33-162">이러한 종속성을 통해 앱에서 eventhubs-client 패키지를 사용하여 Event Hub 호환 끝점에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-162">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="73f33-163">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-163">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="73f33-164">텍스트 편집기를 사용하여 read-d2c-messages\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-164">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="73f33-165">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-165">Add the following **import** statements to the file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="73f33-166">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-166">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="73f33-167">**{youriothubkey}**, **{youreventhubcompatibleendpoint}** 및 **{youreventhubcompatiblename}**을 앞에서 기록해둔 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="73f33-168">다음 **receiveMessages** 메서드를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-168">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="73f33-169">이 메서드는 **EventHubClient** 인스턴스를 만들어 Event Hub 호환 끝점에 연결하고 **PartitionReceiver** 인스턴스를 비동기식으로 만들어 Event Hub 파티션에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-169">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="73f33-170">계속해서 반복하고 앱이 종료될 때까지 메시지 세부 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-170">It loops continuously and prints the message details until the app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
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
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="73f33-171">이 메서드는 수신기를 만들 때 필터를 사용하여 수신기는 수신기 실행이 시작된 후 IoT Hub에 전송된 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-171">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="73f33-172">이 방법은 테스트 환경에서 현재 메시지 집합을 볼 수 있어 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-172">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="73f33-173">프로덕션 환경에서는 코드가 모든 메시지를 처리하는지 확인해야 합니다. 자세한 내용은 [IoT Hub 장치-클라우드 메시지 처리 방법][lnk-process-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73f33-173">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="73f33-174">**main** 메서드의 서명을 수정하여 다음과 같은 예외를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-174">Modify the signature of the **main** method to include the exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="73f33-175">**App** 클래스의 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-175">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="73f33-176">이 코드에서는 **EventHubClient** 및 **PartitionReceiver**라는 두 개의 인스턴스를 만들고 메시지 처리를 완료할 때 앱을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-176">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
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
    > <span data-ttu-id="73f33-177">이 코드는 F1(무료) 계층에서 IoT Hub를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-177">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="73f33-178">무료 IoT Hub에는 "0" 및 "1"이라는 두 개의 파티션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="73f33-179">App.java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-179">Save and close the App.java file.</span></span>

12. <span data-ttu-id="73f33-180">Maven을 사용하여 **read-d2c-messages** 앱을 빌드하려면 read-d2c-messages 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-180">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="73f33-181">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="73f33-181">Create a device app</span></span>
<span data-ttu-id="73f33-182">이 섹션에서는 IoT Hub로 장치-클라우드 메시지를 전송하는 장치를 시뮬레이션하는 Java 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="73f33-183">*장치 ID 만들기* 섹션에서 만든 iot-java-get-started 폴더의 명령 프롬프트에서 다음 명령을 사용하여 **simulated-device**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-183">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="73f33-184">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="73f33-185">명령 프롬프트에서 simulated-device 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-185">At your command prompt, navigate to the simulated-device folder.</span></span>

3. <span data-ttu-id="73f33-186">텍스트 편집기를 사용하여 simulated-device 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-186">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="73f33-187">이러한 종속성을 통해 IoT Hub와 통신하고 JSON으로 Java 개체를 직렬화하도록 앱에서 iothub-java-client 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-187">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>

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
    > <span data-ttu-id="73f33-188">[Maven 검색][lnk-maven-device-search]을 사용하여 **iot-device-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-188">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="73f33-189">pom.xml 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-189">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="73f33-190">텍스트 편집기를 사용하여 simulated-device\src\main\java\com\mycompany\app\App.java 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-190">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="73f33-191">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-191">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="73f33-192">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-192">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="73f33-193">**{youriothubname}**을 IoT Hub 이름으로 바꾸고 **{yourdevicekey}**를 *장치 ID 만들기* 섹션에서 만든 장치 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="73f33-194">이 샘플 앱은 **DeviceClient** 개체를 인스턴스화할 때 **프로토콜** 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-194">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="73f33-195">MQTT, AMQP 또는 HTTP 프로토콜을 사용하여 IoT Hub와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-195">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>

8. <span data-ttu-id="73f33-196">다음의 중첩된 **TelemetryDataPoint** 클래스를 **App** 클래스 안에 추가하여 장치가 IoT Hub에 전송한 원격 분석 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-196">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>

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
9. <span data-ttu-id="73f33-197">다음의 중첩된 **EventCallback** 클래스를 **App** 클래스 안에 추가하여 장치 앱의 메시지를 처리할 때 IoT Hub가 반환하는 확인 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-197">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the device app.</span></span> <span data-ttu-id="73f33-198">이 메서드는 또한 메시지가 처리되면 앱에서 메인 스레드를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-198">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="73f33-199">다음의 중첩된 **MessageSender** 클래스를 **App** 클래스 안에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-199">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="73f33-200">이 클래스의 **run** 메서드는 IoT Hub에 전송할 샘플 원격 분석 데이터를 생성하고 다음 메시지를 전송하기 전에 확인을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-200">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>

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

    <span data-ttu-id="73f33-201">이 메서드는 IoT Hub에서 이전 메시지를 확인하고 1초 후 새 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-201">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="73f33-202">메시지에는 장치 ID가 있는 JSON 직렬화된 개체와 온도 센서 및 습도 센서를 시뮬레이션하기 위해 임의로 생성된 숫자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-202">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="73f33-203">**main** 메서드를 장치-클라우드 메시지를 사용자의 IoT Hub로 전송하는 스레드를 만드는 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-203">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="73f33-204">App.java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-204">Save and close the App.java file.</span></span>

13. <span data-ttu-id="73f33-205">Maven을 사용하여 **simulated-device** 앱을 빌드하려면 simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-205">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="73f33-206">간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-206">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="73f33-207">프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리][lnk-transient-faults]에서 제시한 대로 다시 시도 정책(예: 지수 백오프)을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="73f33-208">앱 실행</span><span class="sxs-lookup"><span data-stu-id="73f33-208">Run the apps</span></span>

<span data-ttu-id="73f33-209">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-209">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="73f33-210">read-d2c 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub에서 첫 번째 파티션의 모니터링을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-210">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![장치-클라우드 메시지를 모니터링하는 Java IoT Hub 서비스 앱][7]

2. <span data-ttu-id="73f33-212">simulated-device 폴더의 명령 프롬프트에서 다음 명령을 실행하여 IoT Hub에 원격 분석 데이터 전송을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-212">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![장치-클라우드 메시지를 전송하는 Java IoT Hub 장치 앱][8]

3. <span data-ttu-id="73f33-214">[Azure Portal][lnk-portal]의 **사용량** 타일에 IoT Hub로 전송된 메시지 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-214">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![IoT Hub에 전송된 메시지의 수를 보여주는 Azure Portal 사용량 타일][43]

## <a name="next-steps"></a><span data-ttu-id="73f33-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73f33-216">Next steps</span></span>
<span data-ttu-id="73f33-217">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-217">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="73f33-218">이 장치 ID를 사용하여 장치-클라우드 메시지를 IoT Hub로 보내기 위해 장치 앱을 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-218">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="73f33-219">IoT Hub에서 받은 메시지를 표시하는 앱도 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="73f33-219">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="73f33-220">계속해서 IoT Hub을 시작하고 다른 IoT 시나리오를 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73f33-220">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="73f33-221">[장치 연결][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="73f33-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="73f33-222">[장치 관리 시작][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="73f33-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="73f33-223">[Azure IoT Hub 시작][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="73f33-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="73f33-224">IoT 솔루션을 확장하고 대량의 장치-클라우드 메시지를 처리하는 방법을 알아보려면 [장치-클라우드 메시지 처리][lnk-process-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73f33-224">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
