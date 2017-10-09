---
title: "게이트웨이 tooAzure Intel NUC를 사용 하 여 IoT Suite aaaConnect | Microsoft Docs"
description: "Hello Microsoft IoT 상용 게이트웨이 키트 및 hello 원격 모니터링 미리 구성 된 솔루션을 사용 합니다. Hello Azure IoT 가장자리 게이트웨이 tooenable SensorTag 장치 tooconnect toohello 원격 모니터링 솔루션을 사용 하 고 원격 분석 toohello 클라우드 보내고 hello 솔루션 대시보드에서 호출 toomethods 알림에 응답 합니다."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="3e4ae-104">미리 구성 된 솔루션을 모니터링 하 고 원격 Azure IoT 가장자리 게이트웨이 toohello 사용자를 연결 하 고는 SensorTag에서 원격 분석 전송</span><span class="sxs-lookup"><span data-stu-id="3e4ae-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="3e4ae-105">이 자습서에서는 toouse SensorTag 장치 toohello 원격 모니터링에서 Azure IoT 가장자리 toosend 온도 및 습도 데이터 미리 솔루션을 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="3e4ae-106">hello SensorTag Bluetooth를 사용 하 여 toohello Intel NUC 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="3e4ae-107">hello 자습서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-107">hello tutorial uses:</span></span>

- <span data-ttu-id="3e4ae-108">Azure IoT 가장자리 tooimplement 샘플 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="3e4ae-109">hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="3e4ae-110">개요</span><span class="sxs-lookup"><span data-stu-id="3e4ae-110">Overview</span></span>

<span data-ttu-id="3e4ae-111">이 자습서의 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="3e4ae-112">Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="3e4ae-113">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="3e4ae-114">컴퓨터 및 원격 모니터링 솔루션 hello와는 Intel NUC 게이트웨이 장치 toocommunicate를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="3e4ae-115">SensorTag 장치에서 Intel NUC 게이트웨이 tooreceive 원격 분석을 설정 하 고 보낼 toohello 원격 대시보드를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="3e4ae-116">[Texas Instruments BLE SensorTag][lnk-sensortag]</span><span class="sxs-lookup"><span data-stu-id="3e4ae-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="3e4ae-117">이 자습서는 hello SensorTag 장치에서 Bluetooth를 통해 원격 분석 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="3e4ae-118">원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="3e4ae-119">hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="3e4ae-120">종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="3e4ae-121">미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="3e4ae-122">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="3e4ae-123">Bluetooth 연결 구성</span><span class="sxs-lookup"><span data-stu-id="3e4ae-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="3e4ae-124">Hello Intel NUC tooenable hello SensorTag 장치 tooconnect에서 Bluetooth를 구성 하 고 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="3e4ae-125">Hello SensorTag hello MAC 주소를 찾을</span><span class="sxs-lookup"><span data-stu-id="3e4ae-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="3e4ae-126">Intel NUC hello에 hello 셸에서 hello 명령 toounblock hello Bluetooth 서비스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="3e4ae-127">실행된 hello 다음 Intel NUC hello에서 toostart hello Bluetooth 서비스 명령과 hello Bluetooth 셸 입력:</span><span class="sxs-lookup"><span data-stu-id="3e4ae-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="3e4ae-128">Hello 명령 toopower hello Bluetooth 컨트롤러에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="3e4ae-129">메시지가 나타나면 hello 컨트롤러를 설정 하면 **성공에 전원 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="3e4ae-130">다음 근처의 Bluetooth 장치에 대 한 명령 tooscan hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="3e4ae-131">키를 눌러 hello 전원 단추를 hello SensorTag toomake 검색 가능한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="3e4ae-132">hello 녹색 led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="3e4ae-133">Hello 셸에서 메시지가 나타나면 해당 hello 컨트롤러가 SensorTag hello를 검색, hello hello 장치의 MAC 주소를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="3e4ae-134">hello MAC 주소 처럼 보이는 **A0:E6:F8:B5:F6:00**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="3e4ae-135">Hello 게이트웨이 구성할 때 hello 자습서의 뒷부분에 나오는 hello MAC 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="3e4ae-136">Bluetooth 검색 해제 명령을 tooturn 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="3e4ae-137">Hello 명령 tooverify toohello SensorTag 장치를 연결할 수 있는지 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="3e4ae-138">성공적으로 연결 하는 경우 hello 셸 hello 메시지를 표시 하는 **성공적으로 연결** hello SensorTag 장치에 대 한 정보를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="3e4ae-139">연결할 수 없는 경우 SensorTag 켜져 여전히 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="3e4ae-140">이제 hello SensorTag에서에서 분리 하 고 hello Bluetooth 셸 hello 다음 명령을 실행 하 여 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="3e4ae-141">사용자 지정 IoT 지 모듈 hello 빌드</span><span class="sxs-lookup"><span data-stu-id="3e4ae-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="3e4ae-142">이제 hello 사용자 지정 IoT 가장자리 수 있는 모듈을 hello 게이트웨이 toosend 메시지 toohello 원격 모니터링 솔루션을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="3e4ae-143">게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="3e4ae-144">다음 명령을 hello를 사용 하 여 GitHub에서 사용자 지정 IoT 가장자리 모듈 hello에 대 한 hello 소스 코드를 다운로드:</span><span class="sxs-lookup"><span data-stu-id="3e4ae-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="3e4ae-145">다음 명령 hello를 사용 하 여 hello 사용자 지정 IoT 가장자리 모듈 빌드:</span><span class="sxs-lookup"><span data-stu-id="3e4ae-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="3e4ae-146">hello 빌드 스크립트는 hello libsensor2remotemonitoring.so 사용자 지정 IoT 지 모듈 hello 빌드 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="3e4ae-147">구성 하 고 hello IoT 지 게이트웨이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="3e4ae-148">이제 프로그램 SensorTag 장치 tooyour 모니터링 대시보드 원격에서 hello IoT 가장자리 게이트웨이 toosend 원격 분석을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="3e4ae-149">게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="3e4ae-150">이 자습서를 사용 하 여 hello 표준 `vi` Intel NUC hello에 대 한 텍스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="3e4ae-151">사용 하지 않은 경우 `vi` 앞,와 같은 있는 소개 자습서를 완료 해야 [Unix-hello vi 편집기 자습서] [ lnk-vi-tutorial] toofamiliarize이이 편집기와 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="3e4ae-152">또는 보다 사용자 친화적인 hello를 설치할 수 [nano](https://www.nano-editor.org/) hello 명령을 사용 하 여 편집기 `smart install nano -y`합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="3e4ae-153">Hello에 샘플 구성 파일을 열고 hello **vi** hello 다음 명령을 사용 하 여 편집기:</span><span class="sxs-lookup"><span data-stu-id="3e4ae-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="3e4ae-154">위의 hello IoTHub 모듈에 대 한 hello 구성에서 삼각형 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="3e4ae-155">Hello 만들고 hello에 저장 된 IoT 허브 정보를 사용 하 여 값이이 자습서의 시작 hello 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="3e4ae-156">hello 값 IoTHubName에 대 한 다음과 같은 **yourrmsolution37e08**, IoTSuffix hello 값이 일반적으로 **azure devices.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="3e4ae-157">Hello를 다음 hello 매핑 모듈에 대 한 hello 구성에 있는 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="3e4ae-158">Hello 대체 **macAddress** hello 앞에서 설명 된 프로그램 SensorTag의 MAC 주소가 있는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="3e4ae-159">Hello 대체 **deviceID** 및 **deviceKey** hello Id 및 키 hello 원격 모니터링 솔루션에서 이전에 만든 hello 두 장치에 대 한 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="3e4ae-160">위의 hello SensorTag 모듈에 대 한 hello 구성에서 삼각형 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="3e4ae-161">Hello 대체 **장치\_mac\_주소** hello 앞에서 설명 된 프로그램 SensorTag의 MAC 주소가 있는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="3e4ae-162">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-162">Save your changes.</span></span>

<span data-ttu-id="3e4ae-163">이제 다음 명령 hello를 사용 하 여 hello 게이트웨이 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="3e4ae-164">hello IoT 지 게이트웨이 hello Intel NUC에서 시작 하 고 hello SensorTag toohello 원격 모니터링 솔루션에서에서 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![IoT 지 게이트웨이 hello SensorTag에서에서 원격 분석 전송][img-telemetry]

<span data-ttu-id="3e4ae-166">키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="3e4ae-167">Hello 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="3e4ae-167">View hello telemetry</span></span>

<span data-ttu-id="3e4ae-168">이제 hello 게이트웨이 hello SensorTag 장치 toohello 원격 모니터링 솔루션에서에서 원격 분석을 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="3e4ae-169">Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="3e4ae-170">Hello 솔루션 대시보드에서 hello 게이트웨이 통해 명령을 tooyour SensorTag 장치를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="3e4ae-171">Toohello 솔루션 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="3e4ae-172">Hello에 SensorTag hello 나타내는 hello 게이트웨이에서 구성 선택 hello 장치 **장치 tooView** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="3e4ae-173">hello SensorTag 장치에서 원격 분석 hello hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Hello SensorTag 장치에서 원격 분석 표시][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="3e4ae-175">Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="3e4ae-176">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="3e4ae-177">사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3e4ae-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e4ae-178">Next steps</span></span>

<span data-ttu-id="3e4ae-179">Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4ae-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started