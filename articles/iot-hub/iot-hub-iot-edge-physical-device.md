---
title: "물리적 장치에서 Azure IoT Edge 사용 | Microsoft Docs"
description: "Texas Instruments SensorTag 장치를 사용하여 Raspberry Pi 3에서 실행되는 IoT Edge 게이트웨이를 통해 IoT Hub로 데이터를 전송하는 방법입니다. 이 게이트웨이는 Azure IoT Edge를 사용하여 빌드됩니다."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a>Raspberry Pi에 Azure IoT Edge를 사용하여 IoT Hub에 장치-클라우드 메시지 전달

[Bluetooth 저에너지 샘플][lnk-ble-samplecode]의 이 연습에서는 [Azure IoT Edge][lnk-sdk]를 사용하여 다음을 수행하는 방법을 보여줍니다.

* 물리적 장치에서 IoT Hub로 장치-클라우드 원격 분석을 전달합니다.
* IoT Hub에서 물리적 장치로 명령을 라우팅합니다.

이 연습에서는 다음 내용을 다룹니다.

* **아키텍처**: Bluetooth 저에너지 샘플에 대한 중요한 아키텍처 정보입니다.
* **빌드 및 실행**: 샘플을 빌드하고 실행하는 데 필요한 단계입니다.

## <a name="architecture"></a>아키텍처

이 연습은 Raspbian Linux를 실행하는 Raspberry Pi 3에서 IoT Edge 게이트웨이를 빌드하고 실행하는 방법을 보여줍니다. 게이트웨이는 IoT Edge를 사용하여 빌드됩니다. 이 샘플은 Texas Instruments SensorTag BLE(Bluetooth 저에너지) 장치를 사용하여 온도 데이터를 수집합니다.

IoT Edge 게이트웨이를 실행하면 다음 작업이 수행됩니다.

* BLE(Bluetooth 저에너지) 프로토콜을 사용하여 SensorTag 장치에 연결합니다.
* HTTP 프로토콜을 사용하여 IoT Hub에 연결합니다.
* SensorTag 장치에서 IoT Hub로 원격 분석을 전달합니다.
* IoT Hub에서 SensorTag 장치로 명령을 라우팅합니다.

게이트웨이에는 다음과 같은 IoT Edge 모듈이 포함됩니다.

* *BLE 모듈* - BLE 장치와 연결되며, 장치에서 온도 데이터를 수신하고 장치로 명령을 보냅니다.
* *BLE 클라우드-장치 모듈* - *BLE 모듈*에 대한 BLE 지침으로 IoT Hub에서 전송된 JSON 메시지를 변환합니다.
* *로거 모듈* - 모든 게이트웨이 메시지를 로컬 파일에 기록합니다.
* *ID 매핑 모듈* - BLE 장치 MAC 주소 및 Azure IoT Hub 장치 ID 간을 변환합니다.
* *IoT Hub 모듈* - IoT hub에 원격 분석 데이터를 업로드하고 IoT hub에서 장치 명령을 수신합니다.
* *BLE 프린터 모듈* - BLE 장치의 원격 분석을 해석하고 형식이 지정된 데이터를 콘솔에 출력하여 문제 해결 및 디버깅을 사용하도록 설정합니다.

### <a name="how-data-flows-through-the-gateway"></a>게이트웨이를 통해 데이터가 흐르는 방식

다음 블록 다이어그램에서는 원격 분석 업로드 데이터 흐름 파이프라인을 보여 줍니다.

![원격 분석 업로드 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

원격 분석 항목이 BLE 장치에서 IoT Hub로 이동하면서 진행되는 단계는 다음과 같습니다.

1. BLE 장치가 온도 샘플을 생성한 후 Bluetooth를 통해 게이트웨이의 BLE 모듈로 보냅니다.
1. BLE 모듈이 샘플을 수신한 후 장치의 MAC 주소와 함께 broker에 게시합니다.
1. ID 매핑 모듈이 이 메시지를 선택하고 내부 표를 사용하여 장치의 MAC 주소를 IoT Hub 장치 ID로 변환합니다. IoT Hub 장치 ID는 장치 ID와 장치 키로 구성됩니다.
1. ID 매핑 모듈은 온도 샘플 데이터, 장치의 MAC 주소, 장치 ID 및 장치 키가 포함된 새 메시지를 게시합니다.
1. IoT Hub 모듈은 새 메시지(ID 매핑 모듈에 의해 생성)를 수신한 후 IoT Hub에 게시합니다.
1. 로거 모듈이 broker의 모든 메시지를 로컬 파일에 기록합니다.

다음 블록 다이어그램에서는 장치 명령 데이터 흐름 파이프라인을 보여 줍니다.

![장치 명령 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. IoT Hub 모듈은 새로운 명령 메시지에 대한 IoT Hub를 주기적으로 폴링합니다.
1. IoT Hub 모듈은 새 명령 메시지를 받으면 broke에 게시합니다.
1. ID 매핑 모듈은 명령 메시지를 선택하고 내부 표를 사용하여 IoT Hub 장치 ID를 장치 MAC 주소로 변환합니다. 그런 다음 메시지의 속성 맵에 대상 장치의 MAC 주소가 포함된 새 메시지를 게시합니다.
1. BLE 클라우드-장치 모듈은 이 메시지를 선택해 BLE 모듈에 적합한 BLE 명령으로 변환합니다. 그런 다음 새 메시지를 게시합니다.
1. BLE 모듈은 이 메시지를 선택하고 BLE 장치와 통신하여 I/O 명령을 실행합니다.
1. 로거 모듈이 broker의 모든 메시지를 디스크 파일에 기록합니다.

## <a name="prerequisites"></a>필수 조건

이 자습서를 완료하려면 활성 Azure 구독이 필요합니다.

> [!NOTE]
> 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.

Raspberry Pi의 명령줄에 원격으로 액세스할 수 있도록 데스크톱 컴퓨터에 SSH 클라이언트가 필요합니다.

- Windows에서는 SSH 클라이언트를 포함하지 않습니다. [PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.
- 대부분의 Linux 배포판 및 Mac OS는 명령줄 SSH 유틸리티를 포함합니다. 자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.

## <a name="prepare-your-hardware"></a>하드웨어 준비

이 자습서에서는 사용자가 Raspbian을 실행하는 Raspberry Pi 3 에 연결된 [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) 장치를 사용한다고 가정합니다.

### <a name="install-raspbian"></a>Raspbian 설치

다음 옵션 중 하나를 사용하여 Raspbian을 Raspberry Pi 3 장치에 설치할 수 있습니다.

* 최신 버전의 Raspbian을 설치하려면 [NOOBS][lnk-noobs] 그래픽 사용자 인터페이스를 사용합니다.
* 최신 Raspbian 운영 체제 이미지를 수동으로 [다운로드][lnk-raspbian]하고 SD 카드에 씁니다.

### <a name="sign-in-and-access-the-terminal"></a>터미널 로그인 및 액세스

Raspberry Pi의 터미널 환경에 액세스하는 두 가지 옵션이 있습니다.

* 키보드 및 모니터가 Raspberry Pi에 연결된 경우 Raspbian GUI를 사용하여 터미널 창에 액세스할 수 있습니다.

* 데스크톱 컴퓨터에서 SSH를 사용하여 Raspberry Pi의 명령줄에 액세스합니다.

#### <a name="use-a-terminal-window-in-the-gui"></a>GUI에서 터미널 창 사용

Raspbian에 대한 기본 자격 증명은 사용자 이름 **pi** 및 암호 **raspberry**입니다. GUI의 작업 표시줄에서 모니터 모양의 아이콘을 사용하여 **터미널** 유틸리티를 시작할 수 있습니다.

#### <a name="sign-in-with-ssh"></a>SSH를 사용하여 로그인

Raspberry Pi에 명령줄 액세스를 위해 SSH를 사용할 수 있습니다. [SSH(Secure Shell)][lnk-pi-ssh] 문서에서는 Raspberry Pi에서 SSH를 구성하는 방법 및 [Windows][lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]에서 연결하는 방법을 설명합니다.

사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.

### <a name="install-bluez-537"></a>BlueZ 5.37 설치

BLE 모듈은 BlueZ 스택을 통해 Bluetooth 하드웨어와 통신합니다. 모듈이 제대로 작동하려면 BlueZ 버전 5.37이 필요합니다. 다음 지침은 올바른 BlueZ 버전이 설치되어 있는지 확인합니다.

1. 현재 Bluetooth 디먼을 중지합니다.

    ```sh
    sudo systemctl stop bluetooth
    ```

1. BlueZ 종속성을 설치합니다.

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. bluez.org에서 BlueZ 소스 코드를 다운로드합니다.

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. 소스 코드 압축을 풉니다.

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. 디렉터리를 새로 생성된 폴더로 변경합니다.

    ```sh
    cd bluez-5.37
    ```

1. 빌드할 BlueZ 코드를 구성합니다.

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. BlueZ를 빌드합니다.

    ```sh
    make
    ```

1. 빌드가 완료되면 BlueZ를 설치합니다.

    ```sh
    sudo make install
    ```

1. `/lib/systemd/system/bluetooth.service` 파일에서 새로운 Bluetooth 디먼을 가리키도록 Bluetooth에 대한 systemd 서비스 구성을 변경합니다. 'ExecStart' 줄을 다음 텍스트로 바꿉니다.

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a>Raspberry Pi 3 장치에서 SensorTag 장치로 연결 설정

이 샘플을 실행하기 전에 Raspberry Pi 3이 SensorTag 장치에 연결할 수 있는지 확인해야 합니다.

1. `rfkill` 유틸리티가 설치되어 있는지 확인합니다.

    ```sh
    sudo apt-get install rfkill
    ```

1. Raspberry Pi 3에서 Bluetooth를 차단 해제하고 버전 번호가 **5.37**인지 확인합니다.

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. 대화형 Bluetooth 셸을 시작하려면 Bluetooth 서비스를 시작하고 **bluetoothctl** 명령을 실행합니다.

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. **power on** 명령을 입력하여 bluetooth 컨트롤러에 전원을 공급합니다. 명령은 다음과 비슷한 출력을 반환합니다.

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. 대화형 Bluetooth 셸에서 **scan on** 명령을 입력하여 Bluetooth 장치를 검색합니다. 명령은 다음과 비슷한 출력을 반환합니다.

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. 작은 단추(녹색 표시등이 깜박거림)를 눌러 SensorTag 장치를 검색 가능하게 합니다. Raspberry Pi 3은 SensorTag 장치를 검색해야 합니다.

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    이 예제에서는 SensorTag 장치의 MAC 주소가 **A0:E6:F8:B5:F6:00**이라는 것을 확인할 수 있습니다.

1. **scan off** 명령을 입력하여 스캔을 해제합니다.

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. **connect \<MAC 주소\>**를 입력하고 MAC 주소를 사용하여 SensorTag 장치에 연결합니다. 다음 샘플 출력은 명확히 하기 위해 축약형으로 표시됩니다.

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > **list-attributes** 명령을 사용하여 장치의 GATT 특성을 다시 나열할 수 있습니다.

1. 이제 **disconnect** 명령을 사용하여 장치에서 연결을 끊은 다음 **quit** 명령을 사용하여 Bluetooth 셸을 끝낼 수 있습니다.

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

이제 Raspberry Pi 3에서 BLE IoT Edge 샘플을 실행할 준비가 되었습니다.

## <a name="run-the-iot-edge-ble-sample"></a>IoT Edge BLE 샘플 실행

IoT Edge BLE 샘플을 실행하려면 다음 세 가지 작업을 완료해야 합니다.

* IoT Hub에서 두 개의 샘플 장치를 구성합니다.
* Raspberry Pi 3 장치에서 IoT Edge를 빌드합니다.
* Raspberry Pi 3 장치에서 BLE 샘플을 구성하고 실행합니다.

작성할 때 IoT Edge는 Linux에서 실행되는 게이트웨이의 BLE 모듈만 지원합니다.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>IoT Hub에서 두 개의 샘플 장치 구성

* Azure 구독에서 [IoT Hub를 만듭니다][lnk-create-hub]. 이 연습을 완료하려면 허브 이름이 필요합니다. 계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.
* **SensorTag_01**이라는 장치 하나를 IoT hub에 추가하고 해당 ID와 장치 키를 적어둡니다. [장치 Explorer 또는 iothub-explorer][lnk-explorer-tools] 도구를 사용하여 이전 단계에서 만든 IoT Hub에 장치를 추가하고 해당 키를 검색할 수 있습니다. 게이트웨이를 구성할 때 이 장치를 SensorTag 장치에 매핑합니다.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Raspberry Pi 3에서 Azure IoT Edge 빌드

Azure IoT Edge에 대한 종속성을 설치합니다.

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

다음 명령을 사용하여 IoT Edge 및 모든 하위 모듈을 홈 디렉터리로 복제합니다.

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Raspberry Pi 3에 IoT Edge 리포지토리의 전체 복사본이 있는 경우 다음 명령을 사용하여 SDK가 포함된 폴더에서 빌드할 수 있습니다.

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a>Raspberry Pi 3에서 BLE 샘플 구성 및 실행

샘플을 부트스트랩하고 실행하려면 게이트웨이에서 참여하는 각 IoT Edge 모듈을 구성해야 합니다. 이 구성은 JSON 파일에 제공되며 참여하는 5가지 IoT Edge 모듈을 모두 구성해야 합니다. 리포지토리에는 구성 파일을 직접 작성하기 위한 시작 지점으로 사용할 수 있는 **gateway\_sample.json**이라는 샘플 JSON 파일이 있습니다. 이 파일은 IoT Edge 리포지토리의 로컬 복사본에 있는 **samples/ble_gateway/src** 폴더에 있습니다.

다음 섹션에서는 BLE 샘플에 대해 이 구성 파일을 편집하는 방법을 설명하고 IoT Edge 리포지토리가 Raspberry Pi 3의 **/home/pi/iot-edge/** 폴더에 있다고 가정합니다. 리포지토리가 다른 위치에 있으면 그에 맞게 경로를 조정합니다.

#### <a name="logger-configuration"></a>로거 구성

게이트웨이 리포지토리가 **/home/pi/iot-edge/** 폴더에 있다고 가정하고 다음과 같이 로거 모듈을 구성합니다.

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>BLE 모듈 구성

BLE 장치에 대한 샘플 구성에서는 Texas Instruments SensorTag 장치를 가정합니다. GATT 주변 기기로 작동할 수 있는 모든 표준 BLE 장치가 작동되어야 하지만 GATT 특성 ID 및 데이터를 업데이트해야 할 수도 있습니다. SensorTag 장치의 MAC 주소를 추가합니다.

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

SensorTag 장치를 사용하지 않는 경우 BLE 장치에 대한 설명서를 검토하여 GATT 특성 ID 및 데이터 값을 업데이트해야 하는지 여부를 결정합니다.

#### <a name="iot-hub-module"></a>IoT Hub 모듈

IoT Hub의 이름을 추가합니다. 일반적으로 접미사 값은 **azure-devices.net**입니다.

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>ID 매핑 모듈 구성

SensorTag 장치의 MAC 주소와 IoT Hub에 추가된 **SensorTag_01** 장치의 장치 ID 및 키를 추가합니다.

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>BLE 프린터 모듈 구성

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>BLEC2D 모듈 구성

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>라우팅 구성

다음 구성은 IoT Edge 모듈 간에 다음과 같은 라우팅을 보장합니다.

* **로거** 모듈은 모든 메시지를 수신하고 기록합니다.
* **SensorTag** 모듈은 **매핑** 및 **BLE 프린터** 모듈 둘 다에 메시지를 보냅니다.
* **매핑** 모듈은 IoT Hub 보내질 메시지를 **IoTHub** 모듈에 보냅니다.
* **IoTHub** 모듈은 메시지를 **매핑** 모듈로 돌려 보냅니다.
* **mapping** 모듈은 메시지를 **BLEC2D** 모듈에 보냅니다.
* **BLEC2D** 모듈은 메시지를 **Sensor Tag** 모듈로 돌려 보냅니다.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

샘플을 실행하려면 JSON 구성 파일에 대한 경로를 매개 변수로 **ble\_gateway** binary에 전달합니다. 다음 명령은 **gateway_sample.json** 구성 파일을 사용하고 있다고 가정합니다. Raspberry Pi의 **iot-edge** 폴더에서 이 명령을 실행합니다.

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

샘플을 실행하기 전에 SensorTag 장치에 있는 작은 단추를 눌러 검색을 가능하게 만들어야 할 수 있습니다.

샘플을 실행할 경우 [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 [iothub-explorer](https://github.com/Azure/iothub-explorer) 도구를 사용하여 SensorTag 장치에서 IoT Edge 게이트웨이가 전달하는 메시지를 모니터링할 수 있습니다. 예를 들어 iothub-explorer를 사용하면 다음 명령으로 장치-클라우드 메시지를 모니터링할 수 있습니다.

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>클라우드-장치 메시지 보내기

또한 BLE 모듈은 IoT Hub에서 장치로 명령을 보내도록 지원합니다. [장치 Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 [iothub-explorer](https://github.com/Azure/iothub-explorer) 도구를 사용하여 BLE 게이트웨이 모듈이 BLE 장치에 전달하는 JSON 메시지를 보낼 수 있습니다.

Texas Instruments SensorTag 장치를 사용하는 경우 IoT Hub에서 명령을 보내서 빨간색 LED, 녹색 LED 또는 버저를 켤 수 있습니다. IoT Hub에서 명령을 보내기 전에 먼저 다음 두 JSON 메시지를 순서대로 보냅니다. 그런 다음 원하는 명령을 보내서 표시등 또는 버저를 켭니다.

1. 모든 LED 및 버저 다시 설정(끄기):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. I/O를 '원격'으로 구성:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

이제 다음 명령을 보내서 SensorTag 장치에서 표시등 또는 버저를 켤 수 있습니다.

* 빨간색 LED 켜기:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* 녹색 LED 켜기:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* 버저 켜기:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>다음 단계

IoT Edge와 코드 예제 실험에 대해 더욱 심도 있게 이해하고 싶다면 다음 개발자 자습서 및 리소스를 참고하세요.

* [Azure IoT Edge][lnk-sdk]

IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.

* [IoT Hub 개발자 가이드][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
