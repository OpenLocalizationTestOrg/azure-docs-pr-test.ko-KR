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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>미리 구성 된 솔루션을 모니터링 하 고 원격 Azure IoT 가장자리 게이트웨이 toohello 사용자를 연결 하 고는 SensorTag에서 원격 분석 전송

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

이 자습서에서는 toouse SensorTag 장치 toohello 원격 모니터링에서 Azure IoT 가장자리 toosend 온도 및 습도 데이터 미리 솔루션을 구성 하는 방법을 보여 줍니다. hello SensorTag Bluetooth를 사용 하 여 toohello Intel NUC 게이트웨이 연결 합니다. hello 자습서를 사용합니다.

- Azure IoT 가장자리 tooimplement 샘플 게이트웨이 합니다.
- hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.

## <a name="overview"></a>개요

이 자습서의 단계를 수행 하는 hello를 완료 합니다.

- Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다. 이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.
- 컴퓨터 및 원격 모니터링 솔루션 hello와는 Intel NUC 게이트웨이 장치 toocommunicate를 설정 합니다.
- SensorTag 장치에서 Intel NUC 게이트웨이 tooreceive 원격 분석을 설정 하 고 보낼 toohello 원격 대시보드를 모니터링 합니다.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments BLE SensorTag][lnk-sensortag] 이 자습서는 hello SensorTag 장치에서 Bluetooth를 통해 원격 분석 데이터를 검색합니다.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> 원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다. hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다. 종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다. 미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Bluetooth 연결 구성

Hello Intel NUC tooenable hello SensorTag 장치 tooconnect에서 Bluetooth를 구성 하 고 원격 분석 합니다.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Hello SensorTag hello MAC 주소를 찾을

1. Intel NUC hello에 hello 셸에서 hello 명령 toounblock hello Bluetooth 서비스를 실행 합니다.

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. 실행된 hello 다음 Intel NUC hello에서 toostart hello Bluetooth 서비스 명령과 hello Bluetooth 셸 입력:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Hello 명령 toopower hello Bluetooth 컨트롤러에서 다음을 실행 합니다.

    ```bash
    power on
    ```

    메시지가 나타나면 hello 컨트롤러를 설정 하면 **성공에 전원 변경**합니다.

1. 다음 근처의 Bluetooth 장치에 대 한 명령 tooscan hello를 실행 합니다.

    ```bash
    scan on
    ```

1. 키를 눌러 hello 전원 단추를 hello SensorTag toomake 검색 가능한 것입니다. hello 녹색 led가 깜박입니다.

1. Hello 셸에서 메시지가 나타나면 해당 hello 컨트롤러가 SensorTag hello를 검색, hello hello 장치의 MAC 주소를 기록 합니다. hello MAC 주소 처럼 보이는 **A0:E6:F8:B5:F6:00**합니다. Hello 게이트웨이 구성할 때 hello 자습서의 뒷부분에 나오는 hello MAC 주소가 필요 합니다.

1. Bluetooth 검색 해제 명령을 tooturn 다음 hello를 실행 합니다.

    ```bash
    scan off
    ```

1. Hello 명령 tooverify toohello SensorTag 장치를 연결할 수 있는지 다음을 실행 합니다.

    ```bash
    connect <SensorTag MAC address>
    ```

    성공적으로 연결 하는 경우 hello 셸 hello 메시지를 표시 하는 **성공적으로 연결** hello SensorTag 장치에 대 한 정보를 인쇄 합니다. 연결할 수 없는 경우 SensorTag 켜져 여전히 hello를 확인 합니다.

1. 이제 hello SensorTag에서에서 분리 하 고 hello Bluetooth 셸 hello 다음 명령을 실행 하 여 종료할 수 있습니다.

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>사용자 지정 IoT 지 모듈 hello 빌드

이제 hello 사용자 지정 IoT 가장자리 수 있는 모듈을 hello 게이트웨이 toosend 메시지 toohello 원격 모니터링 솔루션을 빌드할 수 있습니다. 게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.

다음 명령을 hello를 사용 하 여 GitHub에서 사용자 지정 IoT 가장자리 모듈 hello에 대 한 hello 소스 코드를 다운로드:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

다음 명령 hello를 사용 하 여 hello 사용자 지정 IoT 가장자리 모듈 빌드:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

hello 빌드 스크립트는 hello libsensor2remotemonitoring.so 사용자 지정 IoT 지 모듈 hello 빌드 폴더에 배치합니다.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>구성 하 고 hello IoT 지 게이트웨이 실행 합니다.

이제 프로그램 SensorTag 장치 tooyour 모니터링 대시보드 원격에서 hello IoT 가장자리 게이트웨이 toosend 원격 분석을 구성할 수 있습니다. 게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.

> [!TIP]
> 이 자습서를 사용 하 여 hello 표준 `vi` Intel NUC hello에 대 한 텍스트 편집기입니다. 사용 하지 않은 경우 `vi` 앞,와 같은 있는 소개 자습서를 완료 해야 [Unix-hello vi 편집기 자습서] [ lnk-vi-tutorial] toofamiliarize이이 편집기와 직접 합니다. 또는 보다 사용자 친화적인 hello를 설치할 수 [nano](https://www.nano-editor.org/) hello 명령을 사용 하 여 편집기 `smart install nano -y`합니다.

Hello에 샘플 구성 파일을 열고 hello **vi** hello 다음 명령을 사용 하 여 편집기:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

위의 hello IoTHub 모듈에 대 한 hello 구성에서 삼각형 hello를 찾습니다.

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Hello 만들고 hello에 저장 된 IoT 허브 정보를 사용 하 여 값이이 자습서의 시작 hello 자리 표시자를 대체 합니다. hello 값 IoTHubName에 대 한 다음과 같은 **yourrmsolution37e08**, IoTSuffix hello 값이 일반적으로 **azure devices.net**합니다.

Hello를 다음 hello 매핑 모듈에 대 한 hello 구성에 있는 줄을 찾습니다.

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Hello 대체 **macAddress** hello 앞에서 설명 된 프로그램 SensorTag의 MAC 주소가 있는 자리 표시자입니다. Hello 대체 **deviceID** 및 **deviceKey** hello Id 및 키 hello 원격 모니터링 솔루션에서 이전에 만든 hello 두 장치에 대 한 자리 표시자입니다.

위의 hello SensorTag 모듈에 대 한 hello 구성에서 삼각형 hello를 찾습니다.

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Hello 대체 **장치\_mac\_주소** hello 앞에서 설명 된 프로그램 SensorTag의 MAC 주소가 있는 자리 표시자입니다.

변경 내용을 저장합니다.

이제 다음 명령 hello를 사용 하 여 hello 게이트웨이 실행할 수 있습니다.

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

hello IoT 지 게이트웨이 hello Intel NUC에서 시작 하 고 hello SensorTag toohello 원격 모니터링 솔루션에서에서 원격 분석을 보냅니다.

![IoT 지 게이트웨이 hello SensorTag에서에서 원격 분석 전송][img-telemetry]

키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.

## <a name="view-hello-telemetry"></a>Hello 원격 분석 보기

이제 hello 게이트웨이 hello SensorTag 장치 toohello 원격 모니터링 솔루션에서에서 원격 분석을 보내는 것입니다. Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다. Hello 솔루션 대시보드에서 hello 게이트웨이 통해 명령을 tooyour SensorTag 장치를 보낼 수도 있습니다.

- Toohello 솔루션 대시보드를 탐색 합니다.
- Hello에 SensorTag hello 나타내는 hello 게이트웨이에서 구성 선택 hello 장치 **장치 tooView** 드롭다운입니다.
- hello SensorTag 장치에서 원격 분석 hello hello 대시보드에 표시 됩니다.

![Hello SensorTag 장치에서 원격 분석 표시][img-telemetry-display]

> [!WARNING]
> Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다. 사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.


## <a name="next-steps"></a>다음 단계

Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started