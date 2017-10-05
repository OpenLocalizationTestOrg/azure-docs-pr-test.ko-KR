---
title: "Intel NUC를 사용하여 Azure IoT Suite에 게이트웨이 연결 | Microsoft Docs"
description: "미리 구성된 원격 모니터링 솔루션 및 Microsoft IoT 상용 게이트웨이 키트를 사용합니다. Azure IoT Edge 게이트웨이를 사용하여 원격 모니터링 솔루션에 연결하고, 시뮬레이션된 원격 분석을 클라우드로 전송하고, 솔루션 대시보드에서 호출된 메서드에 응답합니다."
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
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="86a3d-104">미리 구성된 원격 모니터링 솔루션에 Azure IoT Edge 게이트웨이 연결 및 시뮬레이션된 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="86a3d-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="86a3d-105">이 자습서에서는 Azure IoT Edge를 사용하여 미리 구성된 원격 모니터링 솔루션으로 전송할 온도 및 습도 데이터를 시뮬레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="86a3d-106">이 자습서에서는 다음을 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-106">The tutorial uses:</span></span>

- <span data-ttu-id="86a3d-107">샘플 게이트웨이를 구현하는 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="86a3d-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="86a3d-108">클라우드 기반 백 엔드로 미리 구성된 IoT Suite 원격 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="86a3d-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="86a3d-109">개요</span><span class="sxs-lookup"><span data-stu-id="86a3d-109">Overview</span></span>

<span data-ttu-id="86a3d-110">이 자습서에서는 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="86a3d-111">Azure 구독에서 미리 구성된 원격 모니터링 솔루션의 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="86a3d-112">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="86a3d-113">사용자 컴퓨터 및 원격 모니터링 솔루션과 통신하도록 Intel NUC 게이트웨이 장치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="86a3d-114">솔루션 대시보드에서 볼 수 있는 시뮬레이션된 원격 분석을 보내도록 IoT Edge 게이트웨이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="86a3d-115">원격 모니터링 솔루션은 Azure 구독에서 Azure 서비스 집합을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="86a3d-116">배포는 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="86a3d-117">불필요한 Azure 사용료가 부과되지 않도록 하려면 배포가 완료된 후 azureiotsuite.com에서 미리 구성된 솔루션 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="86a3d-118">미리 구성된 솔루션이 다시 필요하면 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="86a3d-119">원격 모니터링 솔루션이 실행되는 동안 소비를 감소하는 방법에 대한 자세한 내용은 [데모 목적으로 미리 구성된 Azure IoT Suite 솔루션 구성][lnk-demo-config]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86a3d-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="86a3d-120">**device02**와 같은 장치 ID를 사용하여 두 번째 장치를 추가하기 위해 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="86a3d-121">샘플은 게이트웨이의 시뮬레이션된 두 개의 장치에서 원격 모니터링 솔루션으로 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="86a3d-122">사용자 지정 IoT Edge 모듈 빌드</span><span class="sxs-lookup"><span data-stu-id="86a3d-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="86a3d-123">게이트웨이가 원격 모니터링 솔루션에 메시지를 보낼 수 있도록 사용자 지정 IoT Edge 모듈을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="86a3d-124">게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86a3d-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="86a3d-125">다음 명령을 사용하여 GitHub에서 사용자 지정 IoT Edge 모듈의 소스 코드를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="86a3d-126">다음 명령을 사용하여 사용자 지정 IoT Edge 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="86a3d-127">빌드 스크립트는 빌드 폴더에 사용자 지정 IoT Edge 모듈인 libsimulator.so를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="86a3d-128">IoT Edge 게이트웨이 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="86a3d-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="86a3d-129">이제 원격 모니터링 대시보드에 시뮬레이션된 원격 분석을 보내도록 IoT Edge 게이트웨이를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="86a3d-130">게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86a3d-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="86a3d-131">이 자습서에서는 Intel NUC에서 표준 `vi` 텍스트 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="86a3d-132">이전에 `vi`를 사용하지 않은 경우 [Unix - vi 편집기 자습서][lnk-vi-tutorial]와 같은 입문용 자습서를 완료하여 이 편집기에 익숙해져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="86a3d-133">또는 `smart install nano -y` 명령을 사용하여 보다 친숙한 [nano](https://www.nano-editor.org/) 편집기를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="86a3d-134">다음 명령을 사용하여 **vi** 편집기에서 샘플 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="86a3d-135">IoT Hub 모듈에 대한 구성에서 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="86a3d-136">자리 표시자 값을 이 자습서를 시작할 때 만들어 저장한 IoT Hub 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="86a3d-137">IoTHubName의 값은 **yourrmsolution37e08**이고 IoTSuffix의 값은 대개 **azure-devices.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="86a3d-138">매핑 모듈에 대한 구성에서 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-138">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="86a3d-139">**deviceID** 및 **deviceKey** 자리 표시자를 원격 모니터링 솔루션에서 이전에 만든 두 개의 장치에 대한 ID 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="86a3d-140">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-140">Save your changes.</span></span>

<span data-ttu-id="86a3d-141">이제 다음 명령을 사용하여 IoT Edge 게이트웨이를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="86a3d-142">게이트웨이는 Intel NUC에서 시작하고 원격 모니터링 솔루션에 시뮬레이션된 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![IoT Edge 게이트웨이는 시뮬레이션된 원격 분석을 생성합니다.][img-simulated telemetry]

<span data-ttu-id="86a3d-144">**Ctrl+C**를 눌러 언제든지 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="86a3d-145">원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="86a3d-145">View the telemetry</span></span>

<span data-ttu-id="86a3d-146">이제 IoT Edge 게이트웨이는 시뮬레이션된 원격 분석을 원격 모니터링 솔루션으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="86a3d-147">솔루션 대시보드에서 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="86a3d-148">솔루션 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="86a3d-149">**장치 보기** 드롭다운에서 게이트웨이에 구성한 두 개의 장치 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="86a3d-150">게이트웨이 장치의 원격 분석은 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![시뮬레이션된 게이트웨이 장치에서 원격 분석 표시][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="86a3d-152">Azure 계정에서 원격 모니터링 솔루션을 실행하는 경우 실행하는 동안 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="86a3d-153">원격 모니터링 솔루션이 실행되는 동안 소비를 감소하는 방법에 대한 자세한 내용은 [데모 목적으로 미리 구성된 Azure IoT Suite 솔루션 구성][lnk-demo-config]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86a3d-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="86a3d-154">사용을 마친 경우 Azure 계정에서 미리 구성된 솔루션을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="86a3d-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a3d-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86a3d-155">Next steps</span></span>

<span data-ttu-id="86a3d-156">Azure IoT에 대한 추가 샘플 및 설명서를 보려면 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="86a3d-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started