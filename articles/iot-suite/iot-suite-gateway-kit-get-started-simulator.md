---
title: "게이트웨이 tooAzure Intel NUC를 사용 하 여 IoT Suite aaaConnect | Microsoft Docs"
description: "Hello Microsoft IoT 상용 게이트웨이 키트 및 hello 원격 모니터링 미리 구성 된 솔루션을 사용 합니다. Azure IoT 가장자리 게이트웨이 tooconnect toohello 원격 모니터링 솔루션을 사용 하 여 hello 시뮬레이션 된 원격 분석 toohello 클라우드 보내고 toomethods hello 솔루션 대시보드에서 호출에 응답 합니다."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="849c8-104">미리 구성 된 솔루션을 모니터링 하 고 원격 Azure IoT 가장자리 게이트웨이 toohello 사용자를 연결 하 고 시뮬레이트된 원격 분석</span><span class="sxs-lookup"><span data-stu-id="849c8-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="849c8-105">이 자습서에서는 toouse Azure IoT 가장자리 toosimulate 온도 및 습도 데이터 toosend toohello 원격 모니터링 솔루션 미리 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="849c8-106">hello 자습서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-106">hello tutorial uses:</span></span>

- <span data-ttu-id="849c8-107">Azure IoT 가장자리 tooimplement 샘플 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="849c8-108">hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="849c8-109">개요</span><span class="sxs-lookup"><span data-stu-id="849c8-109">Overview</span></span>

<span data-ttu-id="849c8-110">이 자습서의 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="849c8-111">Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="849c8-112">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="849c8-113">컴퓨터 및 원격 모니터링 솔루션 hello와는 Intel NUC 게이트웨이 장치 toocommunicate를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="849c8-114">Hello IoT 가장자리 게이트웨이 toosend 시뮬레이션 hello 솔루션 대시보드에서 볼 수 있는 원격 분석을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="849c8-115">원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="849c8-116">hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="849c8-117">종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="849c8-118">미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="849c8-119">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="849c8-120">두 번째 장치 등 장치 ID를 사용 하 여 이전 단계 tooadd hello 반복 **device02**합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="849c8-121">hello 샘플 hello 게이트웨이 toohello 원격 모니터링 솔루션에 두 개의 시뮬레이션 된 장치에서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="849c8-122">사용자 지정 IoT 지 모듈 hello 빌드</span><span class="sxs-lookup"><span data-stu-id="849c8-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="849c8-123">이제 hello 사용자 지정 IoT 가장자리 수 있는 모듈을 hello 게이트웨이 toosend 메시지 toohello 원격 모니터링 솔루션을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="849c8-124">게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="849c8-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="849c8-125">다음 명령을 hello를 사용 하 여 GitHub에서 사용자 지정 IoT 가장자리 모듈 hello에 대 한 hello 소스 코드를 다운로드:</span><span class="sxs-lookup"><span data-stu-id="849c8-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="849c8-126">다음 명령 hello를 사용 하 여 hello 사용자 지정 IoT 가장자리 모듈 빌드:</span><span class="sxs-lookup"><span data-stu-id="849c8-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="849c8-127">hello 빌드 스크립트는 hello libsimulator.so 사용자 지정 IoT 지 모듈 hello 빌드 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="849c8-128">구성 하 고 hello IoT 지 게이트웨이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="849c8-129">이제 hello IoT 가장자리 게이트웨이 toosend 시뮬레이션 된 원격 분석 tooyour 원격 모니터링 대시보드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="849c8-130">게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="849c8-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="849c8-131">이 자습서를 사용 하 여 hello 표준 `vi` Intel NUC hello에 대 한 텍스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="849c8-132">사용 하지 않은 경우 `vi` 앞,와 같은 있는 소개 자습서를 완료 해야 [Unix-hello vi 편집기 자습서] [ lnk-vi-tutorial] toofamiliarize이이 편집기와 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="849c8-133">또는 보다 사용자 친화적인 hello를 설치할 수 [nano](https://www.nano-editor.org/) hello 명령을 사용 하 여 편집기 `smart install nano -y`합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="849c8-134">Hello에 샘플 구성 파일을 열고 hello **vi** hello 다음 명령을 사용 하 여 편집기:</span><span class="sxs-lookup"><span data-stu-id="849c8-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="849c8-135">위의 hello IoTHub 모듈에 대 한 hello 구성에서 삼각형 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="849c8-136">Hello 만들고 hello에 저장 된 IoT 허브 정보를 사용 하 여 값이이 자습서의 시작 hello 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="849c8-137">hello 값 IoTHubName에 대 한 다음과 같은 **yourrmsolution37e08**, IoTSuffix hello 값이 일반적으로 **azure devices.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="849c8-138">Hello를 다음 hello 매핑 모듈에 대 한 hello 구성에 있는 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

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

<span data-ttu-id="849c8-139">Hello 대체 **deviceID** 및 **deviceKey** hello Id 및 키 hello 원격 모니터링 솔루션에서 이전에 만든 hello 두 장치에 대 한 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="849c8-140">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-140">Save your changes.</span></span>

<span data-ttu-id="849c8-141">이제 hello IoT 지 게이트웨이 수행 하는 hello를 사용 하 여 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="849c8-142">hello 게이트웨이 Intel NUC hello에 시작 되며, 시뮬레이션 된 원격 분석 toohello 원격 모니터링 솔루션을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![IoT Edge 게이트웨이는 시뮬레이션된 원격 분석을 생성합니다.][img-simulated telemetry]

<span data-ttu-id="849c8-144">키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="849c8-145">Hello 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="849c8-145">View hello telemetry</span></span>

<span data-ttu-id="849c8-146">이제 hello IoT 지 게이트웨이 시뮬레이션 된 원격 분석 toohello 원격 모니터링 솔루션을 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="849c8-147">Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="849c8-148">Toohello 솔루션 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="849c8-149">Hello 게이트웨이 hello에서에서 구성한 hello 두 장치 중 하나를 선택 **장치 tooView** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="849c8-150">hello 게이트웨이 장치에서 원격 분석 hello hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![시뮬레이션 된 hello 게이트웨이 장치에서 원격 분석 표시][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="849c8-152">Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="849c8-153">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="849c8-154">사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="849c8-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="849c8-155">Next steps</span></span>

<span data-ttu-id="849c8-156">Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="849c8-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started