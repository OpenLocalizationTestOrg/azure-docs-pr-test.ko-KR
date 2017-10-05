---
title: "펌웨어 업데이트를 지원하도록 C를 사용하여 Azure IoT Suite에 Raspberry Pi 연결 | Microsoft Docs"
description: "Raspberry Pi 3 및 Azure IoT Suite에 Microsoft Azure IoT 스타터 키트를 사용합니다. C를 사용하여 Raspberry Pi를 원격 모니터링 솔루션에 연결하고, 센서의 원격 분석을 클라우드로 전송하고, 원격 펌웨어 업데이트를 수행합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: f36f6512bb30e4b109b1bd1c3cdab10300f4edc9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="43f21-104">Raspberry Pi 3를 원격 모니터링 솔루션에 연결하고 C를 사용하여 원격 펌웨어 업데이트를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="43f21-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="43f21-105">이 자습서에서는 Raspberry Pi 3에 대해 Microsoft Azure IoT 스타터 키트를 사용하여 다음을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="43f21-106">클라우드와 통신할 수 있는 온도 및 습도 판독기를 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="43f21-107">원격 펌웨어 업데이트를 설정하고 수행하여 Raspberry Pi에서 클라이언트 응용 프로그램을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="43f21-108">이 자습서에서는 다음을 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-108">The tutorial uses:</span></span>

* <span data-ttu-id="43f21-109">Raspbian OS, C 프로그래밍 언어 및 C용 Microsoft Azure IoT SDK를 사용하여 샘플 장치를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
* <span data-ttu-id="43f21-110">클라우드 기반 백 엔드로 미리 구성된 IoT Suite 원격 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="43f21-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="43f21-111">개요</span><span class="sxs-lookup"><span data-stu-id="43f21-111">Overview</span></span>

<span data-ttu-id="43f21-112">이 자습서에서는 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-112">In this tutorial, you complete the following steps:</span></span>

* <span data-ttu-id="43f21-113">Azure 구독에서 미리 구성된 원격 모니터링 솔루션의 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="43f21-114">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="43f21-115">사용자 컴퓨터 및 원격 모니터링 솔루션과 통신하도록 장치 및 센서를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
* <span data-ttu-id="43f21-116">샘플 장치 코드를 업데이트하여 원격 모니터링 솔루션에 연결하고 솔루션 대시보드에서 볼 수 있는 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
* <span data-ttu-id="43f21-117">샘플 장치 코드를 사용하여 클라이언트 응용 프로그램을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="43f21-118">원격 모니터링 솔루션은 Azure 구독에서 Azure 서비스 집합을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="43f21-119">배포는 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="43f21-120">불필요한 Azure 사용료가 부과되지 않도록 하려면 배포가 완료된 후 azureiotsuite.com에서 미리 구성된 솔루션 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="43f21-121">미리 구성된 솔루션이 다시 필요하면 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="43f21-122">원격 모니터링 솔루션이 실행되는 동안 소비를 감소하는 방법에 대한 자세한 내용은 [데모 목적으로 미리 구성된 Azure IoT Suite 솔루션 구성][lnk-demo-config]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f21-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="43f21-123">샘플 다운로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="43f21-123">Download and configure the sample</span></span>

<span data-ttu-id="43f21-124">이제 Raspberry Pi에서 원격 모니터링 클라이언트 응용 프로그램을 다운로드하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="43f21-125">리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="43f21-125">Clone the repositories</span></span>

<span data-ttu-id="43f21-126">아직 해당 작업을 수행하지 않은 경우 Pi에서 다음 명령을 실행하여 필요한 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="43f21-127">장치 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="43f21-127">Update the device connection string</span></span>

<span data-ttu-id="43f21-128">다음 명령을 사용하여 **nano** 편집기에서 샘플 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-128">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="43f21-129">자리 표시자 값을 이 자습서를 시작할 때 만들어 저장한 장치 ID 및 IoT Hub 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="43f21-130">완료되면 deviceinfo 파일 내용이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-130">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="43f21-131">변경 내용을 저장하고(**Ctrl-O**, **Enter**) 편집기를 종료합니다(**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="43f21-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="43f21-132">샘플 빌드</span><span class="sxs-lookup"><span data-stu-id="43f21-132">Build the sample</span></span>

<span data-ttu-id="43f21-133">아직 해당 작업을 수행하지 않은 경우 Raspberry Pi의 터미널에서 다음 명령을 실행하여 C용 Microsoft Azure IoT 장치 SDK의 필수 구성 요소 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="43f21-134">이제 Raspberry Pi에서 샘플 솔루션을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-134">You can now build the sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="43f21-135">이제 Raspberry Pi에서 샘플 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-135">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="43f21-136">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-136">Enter the command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="43f21-137">다음 샘플 출력은 Raspberry Pi의 명령 프롬프트에 표시되는 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Raspberry Pi 앱의 출력][img-raspberry-output]

<span data-ttu-id="43f21-139">**Ctrl+C**를 눌러 언제든지 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-139">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="43f21-140">솔루션 대시보드에서 **장치**를 클릭하여 **장치** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="43f21-141">**장치 목록**에서 Raspberry Pi를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-141">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="43f21-142">그런 다음 **메서드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-142">Then choose **Methods**:</span></span>

    ![대시보드에서 장치 나열][img-list-devices]

1. <span data-ttu-id="43f21-144">**메서드 호출** 페이지의 **메서드** 드롭다운에서 **InitiateFirmwareUpdate**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="43f21-145">**FWPackageURI** 필드에 합니다 **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="43f21-146">이 보관 파일에는 펌웨어 버전 2.0 구현이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-146">This archive file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="43f21-147">**InvokeMethod**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="43f21-148">Raspberry Pi의 앱은 솔루션 대시보드로 승인 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="43f21-149">그런 다음 새 버전의 펌웨어를 다운로드하여 펌웨어 업데이트 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-149">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![메서드 기록 표시][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="43f21-151">펌웨어 업데이트 프로세스 확인</span><span class="sxs-lookup"><span data-stu-id="43f21-151">Observe the firmware update process</span></span>

<span data-ttu-id="43f21-152">장치에서 실행될 때, 솔루션 대시보드에서 보고된 속성을 검토하여 펌웨어 업데이트 프로세스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="43f21-153">Raspberry Pi에서 업데이트 프로세스의 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-153">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![업데이트 진행률 표시][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="43f21-155">업데이트가 완료되면 원격 모니터링 앱이 자동으로 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-155">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="43f21-156">`ps -ef` 명령을 사용하여 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-156">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="43f21-157">프로세스를 종료하려면 프로세스 ID와 함께 `kill` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-157">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="43f21-158">장치에서 보고하는 펌웨어 업데이트의 상태를 솔루션 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="43f21-159">다음 스크린샷은 각 업데이트 프로세스 단계의 상태 및 기간과 새로운 펌웨어 버전을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![작업 상태 보기][img-job-status]

    <span data-ttu-id="43f21-161">대시보드를 다시 이동하여 장치가 펌웨어 업데이트 후에도 계속 원격 분석을 보내는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="43f21-162">Azure 계정에서 원격 모니터링 솔루션을 실행하는 경우 실행하는 동안 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="43f21-163">원격 모니터링 솔루션이 실행되는 동안 소비를 감소하는 방법에 대한 자세한 내용은 [데모 목적으로 미리 구성된 Azure IoT Suite 솔루션 구성][lnk-demo-config]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43f21-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="43f21-164">사용을 마친 경우 Azure 계정에서 미리 구성된 솔루션을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="43f21-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43f21-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43f21-165">Next steps</span></span>

<span data-ttu-id="43f21-166">Azure IoT에 대한 추가 샘플 및 설명서를 보려면 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="43f21-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md