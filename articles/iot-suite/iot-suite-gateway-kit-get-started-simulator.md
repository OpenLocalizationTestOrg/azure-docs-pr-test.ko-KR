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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>미리 구성 된 솔루션을 모니터링 하 고 원격 Azure IoT 가장자리 게이트웨이 toohello 사용자를 연결 하 고 시뮬레이트된 원격 분석

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

이 자습서에서는 toouse Azure IoT 가장자리 toosimulate 온도 및 습도 데이터 toosend toohello 원격 모니터링 솔루션 미리 구성 되어 있습니다. hello 자습서를 사용합니다.

- Azure IoT 가장자리 tooimplement 샘플 게이트웨이 합니다.
- hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.

## <a name="overview"></a>개요

이 자습서의 단계를 수행 하는 hello를 완료 합니다.

- Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다. 이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.
- 컴퓨터 및 원격 모니터링 솔루션 hello와는 Intel NUC 게이트웨이 장치 toocommunicate를 설정 합니다.
- Hello IoT 가장자리 게이트웨이 toosend 시뮬레이션 hello 솔루션 대시보드에서 볼 수 있는 원격 분석을 구성 합니다.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> 원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다. hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다. 종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다. 미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

두 번째 장치 등 장치 ID를 사용 하 여 이전 단계 tooadd hello 반복 **device02**합니다. hello 샘플 hello 게이트웨이 toohello 원격 모니터링 솔루션에 두 개의 시뮬레이션 된 장치에서 데이터를 보냅니다.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

hello 빌드 스크립트는 hello libsimulator.so 사용자 지정 IoT 지 모듈 hello 빌드 폴더에 배치합니다.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>구성 하 고 hello IoT 지 게이트웨이 실행 합니다.

이제 hello IoT 가장자리 게이트웨이 toosend 시뮬레이션 된 원격 분석 tooyour 원격 모니터링 대시보드를 구성할 수 있습니다. 게이트웨이 및 IoT Edge 모듈을 구성하는 방법에 대한 자세한 내용은 [Azure IoT Edge 개념][lnk-gateway-concepts]을 참조하세요.

> [!TIP]
> 이 자습서를 사용 하 여 hello 표준 `vi` Intel NUC hello에 대 한 텍스트 편집기입니다. 사용 하지 않은 경우 `vi` 앞,와 같은 있는 소개 자습서를 완료 해야 [Unix-hello vi 편집기 자습서] [ lnk-vi-tutorial] toofamiliarize이이 편집기와 직접 합니다. 또는 보다 사용자 친화적인 hello를 설치할 수 [nano](https://www.nano-editor.org/) hello 명령을 사용 하 여 편집기 `smart install nano -y`합니다.

Hello에 샘플 구성 파일을 열고 hello **vi** hello 다음 명령을 사용 하 여 편집기:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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

Hello 대체 **deviceID** 및 **deviceKey** hello Id 및 키 hello 원격 모니터링 솔루션에서 이전에 만든 hello 두 장치에 대 한 자리 표시자입니다.

변경 내용을 저장합니다.

이제 hello IoT 지 게이트웨이 수행 하는 hello를 사용 하 여 명령을 실행할 수 있습니다.

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

hello 게이트웨이 Intel NUC hello에 시작 되며, 시뮬레이션 된 원격 분석 toohello 원격 모니터링 솔루션을 보냅니다.

![IoT Edge 게이트웨이는 시뮬레이션된 원격 분석을 생성합니다.][img-simulated telemetry]

키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.

## <a name="view-hello-telemetry"></a>Hello 원격 분석 보기

이제 hello IoT 지 게이트웨이 시뮬레이션 된 원격 분석 toohello 원격 모니터링 솔루션을 보내는 중입니다. Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다.

- Toohello 솔루션 대시보드를 탐색 합니다.
- Hello 게이트웨이 hello에서에서 구성한 hello 두 장치 중 하나를 선택 **장치 tooView** 드롭다운입니다.
- hello 게이트웨이 장치에서 원격 분석 hello hello 대시보드에 표시 됩니다.

![시뮬레이션 된 hello 게이트웨이 장치에서 원격 분석 표시][img-telemetry-display]

> [!WARNING]
> Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다. 사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.

## <a name="next-steps"></a>다음 단계

Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started