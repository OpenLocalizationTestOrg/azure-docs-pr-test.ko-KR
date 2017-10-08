---
title: "IoT 게이트웨이 tooconnect 장치 tooAzure IoT Hub aaaUse | Microsoft Docs"
description: "Toouse IoT 게이트웨이 tooconnect TI SensorTag으로 Intel NUC 및 송신 센서 데이터 tooAzure IoT Hub hello에서 클라우드 방식에 대해 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 게이트웨이 장치 toocloud 연결"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>IoT 게이트웨이 tooconnect 작업 toohello 클라우드 SensorTag tooAzure IoT 허브를 사용 하 여

> [!NOTE]
> 이 자습서를 시작하기 전에 먼저 [Intel NUC를 IoT 게이트웨이로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)을 완료해야 합니다. [IoT 게이트웨이로 Intel NUC 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), IoT 게이트웨이로 hello Intel NUC 장치를 설정 합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

배웁니다 어떻게 toouse IoT 게이트웨이 tooconnect 텍사스 기기 SensorTag (CC2650STK) tooAzure IoT 허브입니다. hello IoT 게이트웨이 온도 보내고 SensorTag tooAzure IoT 허브에서 hello 습도 데이터 수집 합니다.

## <a name="what-you-will-do"></a>수행할 사항

- IoT Hub를 만듭니다.
- SensorTag hello에 대 한 hello IoT hub에 장치를 등록 합니다.
- Hello IoT 게이트웨이와 hello SensorTag 간 hello 연결을 사용 하도록 설정 합니다.
- 배포용 샘플 응용 프로그램 toosend SensorTag 데이터 tooyour IoT 허브를 실행 합니다.

## <a name="what-you-need"></a>필요한 항목

- [Intel NUC를 IoT 게이트웨이로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) 자습서를 완료하여 Intel NUC를 IoT 게이트웨이로 설정.
- * 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
- 호스트 컴퓨터에서 실행되는 SSH 클라이언트 - Windows의 경우 PuTTY를 사용하는 것이 좋습니다. Linux와 macOS의 경우 이미 SSH 클라이언트와 함께 제공됩니다.
- hello IP 주소 및 hello SSH 클라이언트에서 hello 사용자 이름 및 암호 tooaccess hello 게이트웨이 제공 합니다.
- 인터넷 연결.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> 여기서 SensorTag용 새 장치 등록

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Hello IoT 게이트웨이와 hello SensorTag 간 hello 연결을 사용 하도록 설정

이 단원의 태스크를 수행 하는 hello를 수행할 수 있습니다.

- Bluetooth 연결에 대 한 hello SensorTag의 hello MAC 주소를 가져옵니다.
- Hello IoT 게이트웨이 toohello SensorTag에서에서 Bluetooth 연결을 시작 합니다.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Bluetooth 연결에 대 한 hello SensorTag의 hello MAC 주소 가져오기

1. Hello 호스트 컴퓨터에서 hello SSH 클라이언트를 실행 하 고 toohello IoT 게이트웨이 연결 합니다.
1. Bluetooth hello 다음 명령을 실행 하 여 차단을 해제 합니다.

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Hello IoT 게이트웨이에서 hello Bluetooth 서비스를 시작 하 고 다음 명령을 실행 하 여 Bluetooth hello Bluetooth 셸 tooconfigure를 입력 합니다.

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. 실행 하 여 hello Bluetooth 컨트롤러에서 전원 다음 Bluetooth 셸 hello에서 명령을 hello:

   ```bash
   power on
   ```

   ![hello Bluetooth 컨트롤러 bluetoothctl IoT 게이트웨이 hello에 대 한 전원](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Hello 다음 명령을 실행 하 여 주변 Bluetooth 장치에 대 한 검색을 시작 합니다.

   ```bash
   scan on
   ```

   ![bluetoothctl을 사용하여 주변의 Bluetooth 장치 검색](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Hello SensorTag 단추 쌍으로 연결 하는 hello 키를 누릅니다. hello SensorTag 깜박입니다에서 hello 녹색 LED.
1. Bluetooth 셸 hello에 hello SensorTag가 표시 됩니다. Hello hello SensorTag의 MAC 주소를 기록해 둡니다. 이 예에서 hello hello SensorTag의 MAC 주소는 `24:71:89:C0:7F:82`합니다.
1. Hello 다음 명령을 실행 하 여 hello 검사를 해제 합니다.

   ```bash
   scan off
   ```

   ![bluetoothctl을 사용하여 주변의 Bluetooth 장치 검색 중지](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Bluetooth 연결 hello IoT 게이트웨이 toohello SensorTag에서 시작

1. Toohello SensorTag hello 다음 명령을 실행 하 여 연결 합니다.

   ```bash
   connect <MAC address>
   ```

   ![Toohello SensorTag bluetoothctl를 사용 하 여 연결](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Hello SensorTag 끊고 hello 다음 명령을 실행 하 여 hello Bluetooth 셸 종료:

   ```bash
   disconnect
   exit
   ```

   ![Hello SensorTag bluetoothctl와에서 연결 끊기](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

성공적으로 SensorTag hello와 hello IoT 게이트웨이 간의 hello 연결 사용 설정 되어 있습니다.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>배포용 샘플 응용 프로그램 toosend SensorTag 데이터 tooyour IoT 허브를 실행 합니다.

hello Bluetooth 낮은 에너지 (배포용) 샘플 응용 프로그램은 Azure IoT 가장자리에서 제공 됩니다. hello 샘플 응용 프로그램에는 배포용 연결에서 데이터를 수집 및 hello 데이터 tooyou IoT 허브를 보냅니다. toorun hello 샘플 응용 프로그램을 해야합니다.

1. Hello 샘플 응용 프로그램을 구성 합니다.
1. Hello IoT 게이트웨이에서 hello 샘플 응용 프로그램을 실행 합니다.

### <a name="configure-hello-sample-application"></a>Hello 샘플 응용 프로그램 구성

1. Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램의 toohello 폴더를 이동 합니다.

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.

   ```bash
   vi ble_gateway.json
   ```

1. Hello 구성 파일에 다음 값에는 hello를 입력 합니다.

   **IoTHubName**: IoT 허브의 hello 이름입니다.

   **IoTHubSuffix**: 가져오기 IoTHubSuffix hello 기본 키의 hello 장치 연결 문자열의 아래쪽에 표시 된 것입니다. Hello hello 장치 연결 문자열의 기본 키를 가져올 하지 IoT 허브 연결 문자열의 기본 키를 hello 하 확인 합니다. hello 장치 연결 문자열의 기본 키 hello hello 형식으로 되어 `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`합니다.

   **전송**: hello 기본값은 `amqp`합니다. 이 값 transpotation 중 hello 프로토콜을 보여 줍니다. `http`, `amqp` 또는 `mqtt`입니다.

   **macAddress**: hello hello 아래로 기록해둔 SensorTag의 MAC 주소입니다.

   **deviceID**: hello 장치의 IoT 허브에서 만든 ID입니다.

   **deviceKey**: hello hello 장치 연결 문자열의 기본 키입니다.

   ![Hello 배포용 샘플 응용 프로그램의 전체 hello 구성 파일](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. 키를 눌러 `ESC` 유형과 `:wq` toosave hello 파일입니다.

### <a name="run-hello-sample-application"></a>Hello 샘플 응용 프로그램 실행

1. SensorTag 켜져 있는지 hello를 확인 합니다.
1. Hello 다음 명령을 실행 합니다.

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>다음 단계

[IoT 게이트웨이를 사용하여 Azure IoT Edge를 통해 센서 데이터 변환](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
