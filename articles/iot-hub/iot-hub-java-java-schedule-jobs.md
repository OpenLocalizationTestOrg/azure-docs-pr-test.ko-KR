---
title: "Azure IoT Hub(Java)를 사용하여 작업 예약 | Microsoft 문서"
description: "여러 장치에서 직접 메서드를 호출하여 Azure IoT Hub 작업을 예약하고 원하는 속성을 설정하는 방법을 설명합니다. Java용 Azure IoT 장치 SDK를 사용하여 시뮬레이션된 장치 앱을 구현하고 Java용 Azure IoT 서비스 SDK를 사용하여 작업을 실행하는 서비스 앱을 구현합니다."
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
ms.openlocfilehash: 003a548ef2da2921a699df1aa9f7aee366d341ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="00f49-104">작업 예약 및 브로드캐스트(Java)</span><span class="sxs-lookup"><span data-stu-id="00f49-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="00f49-105">Azure IoT Hub를 사용하여 수백만 대의 장치를 업데이트하는 작업을 예약하고 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="00f49-106">작업을 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-106">Use jobs to:</span></span>

* <span data-ttu-id="00f49-107">desired 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="00f49-107">Update desired properties</span></span>
* <span data-ttu-id="00f49-108">tags 업데이트</span><span class="sxs-lookup"><span data-stu-id="00f49-108">Update tags</span></span>
* <span data-ttu-id="00f49-109">직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="00f49-109">Invoke direct methods</span></span>

<span data-ttu-id="00f49-110">작업(job)은 이러한 작업(action) 중 하나를 래핑하고 장치 집합에 대한 실행을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="00f49-111">장치 쌍 쿼리에서는 작업 실행 대상인 장치 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="00f49-112">예를 들어 백 엔드 앱은 작업(job)을 사용하여 10,000대 장치에 대해 장치를 재부팅하는 직접 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="00f49-113">장치 쌍 쿼리로 장치 집합을 지정하고 향후 실행될 작업(job)을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="00f49-114">작업(job)은 해당하는 각 장치에서 재부팅 직접 메서드를 수신 및 실행할 때 진행 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="00f49-115">이러한 각 기능에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00f49-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="00f49-116">장치 쌍 및 속성: [장치 쌍 시작](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="00f49-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="00f49-117">직접 메서드: [IoT Hub 개발자 가이드 - 직접 메서드](iot-hub-devguide-direct-methods.md) 및 [자습서: 직접 메서드 사용](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="00f49-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="00f49-118">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="00f49-119">**lockDoor**라는 직접 메서드를 구현하는 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="00f49-120">또한 이 장치 앱은 백 엔드 앱에서 원하는 속성 변경 내용을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="00f49-121">여러 장치에 대해 **lockDoor** 직접 메서드를 호출하는 작업을 만드는 백 엔드 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="00f49-122">다른 작업이 여러 장치로 원하는 속성 업데이트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="00f49-123">이 자습서를 마치면 다음과 같은 java 콘솔 장치 앱과 java 콘솔 백 엔드 앱이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="00f49-124">**simulated-device**: IoT Hub에 연결되고, **lockDoor** 직접 메서드를 구현하고, 원하는 속성 변경 내용을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="00f49-125">**schedule-jobs** 작업을 사용하여 **lockDoor** 직접 메서드를 호출하고 여러 장치에서 장치 쌍의 원하는 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="00f49-126">[Azure IoT SDK](iot-hub-devguide-sdks.md) 문서는 장치 및 백 엔드 앱을 빌드하는 데 사용할 수 있는 Azure IoT SDK에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00f49-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00f49-127">Prerequisites</span></span>

<span data-ttu-id="00f49-128">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="00f49-129">최신 [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="00f49-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="00f49-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="00f49-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="00f49-131">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="00f49-131">An active Azure account.</span></span> <span data-ttu-id="00f49-132">계정이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="00f49-133">프로그래밍 방식으로 장치 ID를 만들려면 [Java를 사용하여 IoT 허브에 장치 연결](iot-hub-java-java-getstarted.md#create-a-device-identity) 문서의 해당 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00f49-133">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="00f49-134">[iothub-explorer](https://github.com/Azure/iothub-explorer) 도구를 사용하여 IoT Hub에 장치를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-134">You can also use the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="00f49-135">서비스 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="00f49-135">Create the service app</span></span>

<span data-ttu-id="00f49-136">이 섹션에서는 작업을 통해 다음을 수행하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="00f49-137">여러 장치에서 **lockDoor** 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="00f49-137">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="00f49-138">여러 장치로 원하는 속성 전송</span><span class="sxs-lookup"><span data-stu-id="00f49-138">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="00f49-139">앱을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-139">To create the app:</span></span>

1. <span data-ttu-id="00f49-140">개발 컴퓨터에서 `iot-java-schedule-jobs`라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="00f49-141">`iot-java-schedule-jobs` 폴더에서 명령 프롬프트를 통해 다음 명령을 사용하여 **schedule-jobs**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-141">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="00f49-142">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="00f49-143">명령 프롬프트에서 `schedule-jobs` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-143">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="00f49-144">텍스트 편집기를 사용하여 `schedule-jobs` 폴더에서 `pom.xml` 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-144">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="00f49-145">이러한 종속성을 통해 IoT Hub와 통신하도록 앱에서 **iot-service-client** 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-145">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="00f49-146">[Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)을 사용하여 **iot-service-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-146">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="00f49-147">**종속성** 노드 뒤에 다음 **빌드** 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-147">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="00f49-148">이 구성에서는 Maven에 Java 1.8을 사용하여 앱을 빌드하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-148">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="00f49-149">`pom.xml` 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="00f49-150">텍스트 편집기를 사용하여 `schedule-jobs\src\main\java\com\mycompany\app\App.java` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-150">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="00f49-151">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-151">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="00f49-152">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-152">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="00f49-153">`{youriothubconnectionstring}`은 *IoT Hub 만들기* 섹션에서 기록한 IoT Hub 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="00f49-154">**App** 클래스에 다음 메서드를 추가하여 장치 쌍에서 원하는 속성 **Building** 및 **Floor**를 업데이트하는 작업을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-154">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
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

1. <span data-ttu-id="00f49-155">**lockDoor** 메서드를 호출하는 작업을 예약하려면 **App** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-155">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
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

1. <span data-ttu-id="00f49-156">작업을 모니터링하려면 **App** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-156">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
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

1. <span data-ttu-id="00f49-157">실행한 작업의 세부 정보를 쿼리하려면 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-157">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="00f49-158">다음 `throws` 절을 포함하도록 **main** 메서드 서명을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-158">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="00f49-159">두 작업을 순서대로 실행하고 모니터링하려면 **main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-159">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
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

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="00f49-160">`schedule-jobs\src\main\java\com\mycompany\app\App.java` 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-160">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="00f49-161">**schedule-jobs** 앱을 빌드하고 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-161">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="00f49-162">명령 프롬프트에서 `schedule-jobs` 폴더로 이동하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-162">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="00f49-163">장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="00f49-163">Create a device app</span></span>

<span data-ttu-id="00f49-164">이 섹션에서는 IoT Hub에서 전송한 원하는 속성을 처리하고 직접 메서드 호출을 구현하는 Java 콘솔 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-164">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="00f49-165">명령 프롬프트에서 다음 명령을 사용하여 `iot-java-schedule-jobs` 폴더에 **simulated-device**라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-165">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="00f49-166">긴 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="00f49-167">명령 프롬프트에서 `simulated-device` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-167">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="00f49-168">텍스트 편집기를 사용하여 `simulated-device` 폴더에서 `pom.xml` 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-168">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="00f49-169">이러한 종속성을 통해 IoT 허브와 통신하도록 앱에서 **iot-device-client** 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-169">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="00f49-170">[Maven 검색](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)을 사용하여 **iot-device-client**의 최신 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-170">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="00f49-171">**종속성** 노드 뒤에 다음 **빌드** 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-171">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="00f49-172">이 구성에서는 Maven에 Java 1.8을 사용하여 앱을 빌드하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-172">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="00f49-173">`pom.xml` 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-173">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="00f49-174">텍스트 편집기를 사용하여 `simulated-device\src\main\java\com\mycompany\app\App.java` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-174">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="00f49-175">파일에 다음 **import** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-175">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="00f49-176">다음 클래스 수준 변수를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-176">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="00f49-177">`{youriothubname}`을 IoT 허브 이름으로 바꾸고 `{yourdevicekey}`를 *장치 ID 만들기* 섹션에서 만든 장치 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="00f49-178">이 샘플 앱은 **DeviceClient** 개체를 인스턴스화할 때 **프로토콜** 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-178">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="00f49-179">현재, 장치 쌍 기능을 사용하려면 MQTT 프로토콜을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-179">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="00f49-180">콘솔에 장치 쌍 알림을 인쇄하려면 다음 중첩 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-180">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="00f49-181">콘솔에 직접 메서드 알림을 인쇄하려면 다음 중첩 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-181">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="00f49-182">IoT Hub로부터의 직접 메서드 호출을 처리하려면 다음 중첩 클래스를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-182">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="00f49-183">다음 `throws` 절을 포함하도록 **main** 메서드 서명을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-183">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="00f49-184">**main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-184">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="00f49-185">IoT Hub와 통신하는 장치 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-185">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="00f49-186">**Device** 개체를 만들어 장치 쌍 속성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-186">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="00f49-187">장치 클라이언트 서비스를 시작하려면 다음 코드를 **main** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-187">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
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

1. <span data-ttu-id="00f49-188">종료하기 전에 사용자가 **Enter** 키를 누를 때까지 대기하려면 다음 코드를 **main** 메서드 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-188">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="00f49-189">`simulated-device\src\main\java\com\mycompany\app\App.java` 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-189">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="00f49-190">**simulated-device** 앱을 빌드하고 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-190">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="00f49-191">명령 프롬프트에서 `simulated-device` 폴더로 이동하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-191">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="00f49-192">앱 실행</span><span class="sxs-lookup"><span data-stu-id="00f49-192">Run the apps</span></span>

<span data-ttu-id="00f49-193">이제 콘솔 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-193">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="00f49-194">명령 프롬프트의 `simulated-device` 폴더에서 다음 명령을 실행하여 원하는 속성 변경 내용과 직접 메서드 호출을 수신 대기하도록 장치 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-194">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![장치 클라이언트 시작](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="00f49-196">명령 프롬프트의 `schedule-jobs` 폴더에서 다음 명령을 실행하여 **schedule-jobs** 서비스 앱을 실행해 두 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-196">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="00f49-197">첫 번째 작업에서는 원하는 속성 값을 설정하고 두 번째 작업에서는 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-197">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub 서비스 앱에서 두 개의 작업을 작성함](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="00f49-199">장치 앱이 원하는 속성 변경 및 직접 메서드 호출을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-199">The device app handles the desired property change and the direct method call:</span></span>

    ![장치 클라이언트에 변경 내용에 응답함](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="00f49-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00f49-201">Next steps</span></span>

<span data-ttu-id="00f49-202">이 자습서에서는 Azure Portal에서 새 IoT Hub를 구성한 다음, IoT Hub의 ID 레지스트리에서 장치 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-202">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="00f49-203">그리고 두 작업을 실행하는 백 엔드 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-203">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="00f49-204">첫 번째 작업은 원하는 속성 값을 설정했으며 두 번째 작업은 직접 메서드를 호출했습니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-204">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="00f49-205">아래와 같이 실행할 방법을 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00f49-205">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="00f49-206">[IoT Hub 시작](iot-hub-java-java-getstarted.md) 자습서를 참조하여 장치에서 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-206">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="00f49-207">[직접 메서드 사용](iot-hub-java-java-direct-methods.md) 자습서를 참조하여 대화형으로(예: 사용자 제어 앱에서 팬 작동) 장치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="00f49-207">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
