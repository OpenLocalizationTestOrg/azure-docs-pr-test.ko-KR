---
title: "Azure IoT 가장자리를 사용 하 여 물리적 장치 aaaUse | Microsoft Docs"
description: "어떻게 toouse 라스베리 Pi 3 장치에서 실행 중인 IoT 지 게이트웨이 통해 텍사스 기기 SensorTag 장치 toosend 데이터 tooan IoT 허브입니다. hello 게이트웨이 Azure IoT 가장자리를 사용 하 여 만들어집니다."
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Azure IoT 가장자리 라스베리 Pi tooforward 장치-클라우드 메시지 tooIoT 허브에서 사용 하 여

이 연습에서는 hello의 [Bluetooth 낮은 에너지 샘플] [ lnk-ble-samplecode] 방법을 보여주는 toouse [Azure IoT 가장자리] [ lnk-sdk] 에:

* 실제 장치에서 장치-클라우드 원격 분석 tooIoT 허브를 전달 합니다.
* IoT Hub tooa 물리적 장치에서 명령 경로입니다.

이 연습에서는 다음 내용을 다룹니다.

* **아키텍처**: hello Bluetooth 낮은 에너지 샘플에 대 한 중요 한 아키텍처 정보입니다.
* **빌드 및 실행**: hello 단계 필요한 toobuild 및 실행된 hello 샘플.

## <a name="architecture"></a>아키텍처

hello 연습 toobuild 및 라스베리 Pi 3에서 IoT 지 게이트웨이 실행 하는 실행 방법을 Raspbian Linux 보여 줍니다. hello 게이트웨이 IoT 가장자리를 사용 하 여 만들어집니다. hello 샘플 텍사스 기기 SensorTag Bluetooth 낮은 에너지 (배포용) 장치 toocollect 온도 데이터를 사용합니다.

Hello IoT 지 게이트웨이 실행 하는 경우 해당:

* Hello Bluetooth 낮은 에너지 (배포용) 프로토콜을 사용 하 여 tooa SensorTag 장치를 연결 합니다.
* TooIoT 허브 연결 hello HTTP 프로토콜을 사용 합니다.
* Hello SensorTag 장치 tooIoT 허브에서에서 원격 분석을 전달합니다.
* IoT Hub toohello SensorTag 장치에서 명령을 라우팅합니다.

hello 게이트웨이 모듈 IoT 가장자리를 따라 hello를 포함 되어 있습니다.

* A *배포용 모듈* hello 장치와 송신 명령 toohello 장치에서 배포용 장치 tooreceive 온도 데이터와 교류 하 합니다.
* A *배포용 클라우드 toodevice 모듈* hello에 대 한 지침 배포용으로 IoT 허브에서 보낸 JSON 메시지를 변환 하는 *배포용 모듈*합니다.
* A *로 거 모듈* 모든 게이트웨이 메시지 tooa 로컬 파일을 기록 하 합니다.
* *ID 매핑 모듈* - BLE 장치 MAC 주소 및 Azure IoT Hub 장치 ID 간을 변환합니다.
* *IoT 허브 모듈* 원격 분석 데이터 tooan IoT 허브를 업로드 하 고 IoT 허브에서 장치 명령을 수신 합니다.
* A *배포용 프린터 모듈* hello 배포용 장치에서 원격 분석을 해석 하 고 형식이 지정 된 데이터 toohello 콘솔 tooenable 문제 해결 및 디버깅 출력입니다.

### <a name="how-data-flows-through-hello-gateway"></a>Hello 게이트웨이 통해 데이터 흐름

블록 다이어그램을 다음 hello hello 원격 분석 업로드 데이터 흐름 파이프라인을 보여 줍니다.

![원격 분석 업로드 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

원격 분석의 항목 사용 배포용 장치 tooIoT에서 이동 하는 hello 단계 허브가 같습니다.

1. hello 배포용 장치 온도 샘플에서는 오류가 발생 하 고 hello 게이트웨이에 Bluetooth toohello 배포용 모듈을 통해 보냅니다.
1. hello 배포용 모듈 hello 샘플 받아 toohello 브로커 hello 장치의 hello MAC 주소와 함께 게시 합니다.
1. hello 인식 매핑 모듈이이 메시지를 선택 하 고 IoT Hub 장치 id를 내부 테이블 tootranslate hello hello 장치의 MAC 주소를 사용 합니다. IoT Hub 장치 ID는 장치 ID와 장치 키로 구성됩니다.
1. hello 인식 매핑 모듈 hello 온도 예제 데이터, hello 장치, hello 장치 ID 및 hello 장치 키의 hello MAC 주소를 포함 하는 새 메시지를 게시 합니다.
1. hello IoT 허브 모듈 (hello 인식 매핑 모듈에서 생성)이 새 메시지를 받아 tooIoT 허브 게시 합니다.
1. hello로 거 모듈 hello 브로커 tooa 로컬 파일에서 모든 메시지를 기록합니다.

블록 다이어그램을 다음 hello hello 장치 명령 데이터 흐름 파이프라인을 보여 줍니다.

![장치 명령 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. IoT Hub 모듈 주기적으로 폴링하여 hello hello 새 명령 메시지에 대 한 IoT hub 합니다.
1. IoT Hub 모듈 hello 새 명령 메시지를 받으면 게시 것 toohello 브로커 합니다.
1. hello 인식 매핑 모듈 hello 명령 메시지를 선택 하 고 내부 테이블 tootranslate hello IoT Hub 장치 ID tooa 장치 MAC 주소를 사용 합니다. 그런 다음 hello 메시지의 hello 속성 맵에서 hello 대상 장치의 hello MAC 주소를 포함 하는 새 메시지를 게시 합니다.
1. hello 배포용 클라우드-장치 모듈이이 메시지를 선택 하 고 hello hello 배포용 모듈에 대 한 적절 한 배포용 명령으로 변환 합니다. 그런 다음 새 메시지를 게시합니다.
1. hello 배포용 모듈이이 메시지를 선택 하 고 hello 배포용 장치와 통신 하 여 hello I/O 명령을 실행 합니다.
1. hello로 거 모듈 hello 브로커 tooa 디스크 파일에서 모든 메시지를 기록합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.

> [!NOTE]
> 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.

사용자 데스크톱 컴퓨터 tooenable 있습니다 tooremotely 액세스 hello 명령줄로 라스베리 Pi hello에에 SSH 클라이언트를 있어야 합니다.

- Windows에서는 SSH 클라이언트를 포함하지 않습니다. [PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.
- 대부분의 Linux 배포판 및 Mac OS 명령줄 SSH 유틸리티 hello를 포함합니다. 자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.

## <a name="prepare-your-hardware"></a>하드웨어 준비

이 자습서에서는 사용 하는 가정는 [텍사스 기기 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) 장치가 연결 tooa 라스베리 Pi 3 Raspbian를 실행 합니다.

### <a name="install-raspbian"></a>Raspbian 설치

Hello 옵션 tooinstall Raspbian 라스베리 Pi 3 장치에서 다음 중 하나를 사용할 수 있습니다.

* tooinstall hello 최신 버전의 Raspbian 사용 하 여 hello [NOOBS] [ lnk-noobs] 그래픽 사용자 인터페이스입니다.
* 수동으로 [다운로드] [ lnk-raspbian] hello Raspbian 운영 체제 tooan SD 카드의 hello 최신 이미지를 작성 합니다.

### <a name="sign-in-and-access-hello-terminal"></a>로그인 및 액세스 hello 터미널

환경을 사용 하는 두 가지 옵션 tooaccess 터미널 라스베리 원주율:

* 키보드 연결된 tooyour 라스베리 Pi를 모니터링 하는 경우에 hello Raspbian GUI tooaccess 터미널 윈도우를 사용할 수 있습니다.

* 액세스 hello 명령줄 데스크톱 컴퓨터의 SSH를 사용 하 여 라스베리 원주율입니다.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Hello GUI에서에서 터미널 윈도우를 사용 하 여

Raspbian에 대 한 hello 기본 자격 증명이 username **pi** 및 암호 **라스베리**합니다. Hello GUI에에서 hello 작업 표시줄에서 hello를 시작할 수 있습니다 **터미널** hello 모양의 아이콘을 모니터를 사용 하 여 유틸리티입니다.

#### <a name="sign-in-with-ssh"></a>SSH를 사용하여 로그인

명령줄 액세스 tooyour 라스베리 Pi에 대 한 SSH를 사용할 수 있습니다. hello 문서 [SSH (보안 셸)] [ lnk-pi-ssh] 설명 방법을 tooconfigure 라스베리 Pi와의 SSH 방법과에서 tooconnect [Windows] [ lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]합니다.

사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.

### <a name="install-bluez-537"></a>BlueZ 5.37 설치

hello 배포용 모듈 hello BlueZ 스택을 통해 toohello Bluetooth 하드웨어와 통신 합니다. 5.37 BlueZ의 버전에 필요한 hello 모듈 toowork 올바르게 합니다. 이러한 지침은 hello BlueZ의 올바른 버전이 설치 되어 있는지 확인 합니다.

1. 현재 bluetooth 데몬 hello를 중지 합니다.

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Hello BlueZ 종속성을 설치 합니다.

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Bluez.org에서 hello BlueZ 소스 코드를 다운로드 하세요.

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Hello 소스 코드를 압축을 풉니다.

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. 디렉터리 toohello 새로 만든 폴더를 변경 합니다.

    ```sh
    cd bluez-5.37
    ```

1. Hello BlueZ 코드 toobe 구축을 구성 합니다.

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

1. Bluetooth hello 파일에서 새 bluetooth 데몬이 toohello 하는 것을 나타내는 되므로 systemd 서비스 구성 변경 `/lib/systemd/system/bluetooth.service`합니다. Hello 'ExecStart' 줄을 텍스트 다음 hello로 바꿉니다.

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>라스베리 Pi 3 장치에서 연결 toohello SensorTag 장치 사용

실행 중인 hello 샘플 하기 전에 tooverify 라스베리 Pi 3 toohello SensorTag 장치를 연결할 수 있도록 해야 합니다.

1. Hello 확인 `rfkill` 유틸리티를 설치 합니다.

    ```sh
    sudo apt-get install rfkill
    ```

1. Hello 라스베리 Pi 3에서 bluetooth를 차단을 해제 하 고 hello 버전 번호가 인지 확인 **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. tooenter hello 대화형 bluetooth 셸 hello bluetooth 서비스 시작 및 실행 hello **bluetoothctl** 명령:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Hello 명령을 입력 **전원 켜기** toopower hello bluetooth 컨트롤러를 합니다. hello 명령은 유사한 toohello 다음을 출력을 반환합니다.

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. Hello 대화형 bluetooth 셸에서 hello 명령을 입력 **검색 시 검색** tooscan bluetooth 장치에 대 한 합니다. hello 명령은 유사한 toohello 다음을 출력을 반환합니다.

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Hello 작은 단추 (녹색 led가 깜박입니다 hello)를 눌러 hello SensorTag 장치 검색 가능 하 게 합니다. hello 라스베리 Pi 3 hello SensorTag 장치를 검색 해야 합니다.

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    이 예제에서는 해당 hello hello 장치가 SensorTag의 MAC 주소를 확인할 수 있습니다 **A0:E6:F8:B5:F6:00**합니다.

1. Hello를 입력 하 여 검색 기능을 해제 **오프 스캔** 명령:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. MAC 주소를 사용 하 여 입력 하 여 tooyour SensorTag 장치 연결 **연결 \<MAC 주소\>**합니다. 다음 샘플 출력 hello은 쉽게 구별할 수 있도록 약어:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > Hello를 사용 하 여 다시 hello 장치의 hello GATT 특성을 나열할 수 있습니다 **특성 목록** 명령입니다.

1. Hello를 사용 하 여 hello 장치에서 연결을 끊을 이제 수 **연결 끊기** 명령을 클릭 한 다음 종료 hello를 사용 하 여 hello bluetooth 셸에서 **종료** 명령:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

이 든 이제 준비 toorun hello 배포용 IoT 가장자리 샘플 라스베리 Pi 3입니다.

## <a name="run-hello-iot-edge-ble-sample"></a>Hello IoT 가장자리 배포용 샘플 실행

toorun hello IoT 가장자리 배포용 샘플 toocomplete 세 가지 작업이 필요합니다.

* IoT Hub에서 두 개의 샘플 장치를 구성합니다.
* Raspberry Pi 3 장치에서 IoT Edge를 빌드합니다.
* 구성 하 고 라스베리 Pi 3 장치에서 hello 배포용 샘플을 실행 합니다.

작성 hello 시 IoT 가장자리 Linux에서 실행 중인 게이트웨이의 배포용 모듈만 지원 합니다.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>IoT Hub에서 두 개의 샘플 장치 구성

* [IoT 허브를 만듭니다.] [ lnk-create-hub] Azure 구독에 필요한 허브 toocomplete의 hello 이름을이 연습 합니다. 계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.
* 라는 하나의 장치 추가 **SensorTag_01** tooyour IoT hub id와 장치 키을 기록 합니다. Hello를 사용할 수 있습니다 [장치 탐색기 또는 iothub 탐색기] [ lnk-explorer-tools] tooadd 키 tooretrieve hello 이전 단계에서 만든이 장치 toohello IoT 허브 도구입니다. Hello 게이트웨이 구성 하는 경우이 장치 toohello SensorTag 장치를 매핑합니다.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Raspberry Pi 3에서 Azure IoT Edge 빌드

Azure IoT Edge에 대한 종속성을 설치합니다.

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

사용 하 여 hello 다음 tooclone IoT Edge 및 모든 하위 모듈 tooyour 홈 디렉터리 명령:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

라스베리 Pi 3에 hello IoT 가장자리 저장소의 전체 복사본을 있을 때 hello hello SDK를 포함 하는 hello 폴더에서 다음 명령을 사용 하 여 빌드할 수 있습니다.

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>구성 하 고 라스베리 Pi 3에서 hello 배포용 샘플을 실행 합니다.

toobootstrap 및 실행된 hello 샘플 hello 게이트웨이 참여 하는 각 IoT 지 모듈을 구성 해야 합니다. 이 구성은 JSON 파일에 제공되며 참여하는 5가지 IoT Edge 모듈을 모두 구성해야 합니다. Hello 저장소 호출 중인 샘플 JSON 파일 **게이트웨이\_sample.json** hello 구성 파일을 직접 작성의 시작 지점으로 사용할 수 있습니다. 이 파일은 hello에 **샘플/ble_gateway/src** hello IoT 가장자리 저장소의 로컬 복사본에 있는 폴더입니다.

hello 다음 섹션에서는 어떻게이 구성은 hello 배포용 샘플에 대 한 파일을 해당 hello IoT 가장자리 리포지토리 가정 tooedit의에서 설명 hello **/home/pi/iot-edge /** 라스베리 Pi 3에는 폴더입니다. Hello 리포지토리는 다른 위치를 hello 경로 적절 하 게 조정 합니다.

#### <a name="logger-configuration"></a>로거 구성

Hello 게이트웨이 저장소 hello에 있는 것으로 가정 **/home/pi/iot-edge /** 폴더를 다음과 같이 hello로 거 모듈을 구성 합니다.

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

hello 배포용 장치에 대 한 샘플 구성 hello 텍사스 기기 SensorTag 장치를 가정합니다. 주변는 GATT 작동 해야 하지만 tooupdate hello GATT 특성 Id 및 데이터를 할 수 있습니다으로 작동할 수 있는 모든 표준 배포용 장치입니다. SensorTag 장치의 hello MAC 주소를 추가 합니다.

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

SensorTag 장치를 사용 하지 않는 경우 tooupdate hello GATT 특성 Id 및 데이터 값을 필요한 지 배포용 장치 toodetermine에 대 한 hello 설명서를 검토 합니다.

#### <a name="iot-hub-module"></a>IoT Hub 모듈

IoT Hub의 hello 이름을 추가 합니다. 일반적으로 hello 접미사 값은 **azure devices.net**:

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

SensorTag 장치 및 hello 장치 ID 및 키의 hello의 hello MAC 주소를 추가 **SensorTag_01** tooyour IoT 허브를 추가 하는 장치:

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

hello 다음 구성을 사용 하면 hello 다음 IoT 가장자리 모듈 간의 라우팅:

* hello **로 거** 모듈 수신 하 고 모든 메시지를 기록 합니다.
* hello **SensorTag** 모듈 tooboth hello 메시지를 보내는 **매핑** 및 **배포용 프린터** 모듈입니다.
* hello **매핑** 모듈 보내는 메시지 toohello **IoTHub** 모듈 toobe tooyour IoT Hub를 전송 합니다.
* hello **IoTHub** 모듈 toohello 회신 메시지를 보내는 **매핑** 모듈입니다.
* hello **매핑** 모듈 보내는 메시지 toohello **BLEC2D** 모듈입니다.
* hello **BLEC2D** 모듈 toohello 회신 메시지를 보내는 **센서 태그** 모듈입니다.

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

매개 변수 toohello 패스 hello 경로 toohello JSON 구성 파일 toorun hello 샘플 **배포용\_게이트웨이** 이진입니다. hello 다음 명령을 사용 하 고 가정 hello **gateway_sample.json** 구성 파일입니다. Hello에서이 명령을 실행 **iot 가장자리** hello 라스베리 Pi의 폴더:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Toopress 야 hello 작은 단추 hello SensorTag 장치 toomake 검색 가능한 것 hello 샘플을 실행 하기 전에.

Hello 샘플을 실행 하면 hello를 사용할 수 있습니다 [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 hello [iothub 탐색기](https://github.com/Azure/iothub-explorer) 도구 toomonitor hello 메시지 hello hello SensorTag 장치에서 IoT 지 게이트웨이 전달 합니다. 예를 들어 iothub 탐색기를 사용 하 여 다음 명령을 hello를 사용 하 여 장치-클라우드 메시지 모니터링할 수 있습니다.

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>클라우드-장치 메시지 보내기

hello 배포용 모듈에는 또한 IoT Hub toohello 장치에서 보내는 명령을 지원합니다. Hello를 사용할 수 있습니다 [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 hello [iothub 탐색기](https://github.com/Azure/iothub-explorer) 도구 toosend JSON 메시지 해당 hello 배포용 게이트웨이 모듈 toohello 배포용 장치에 전달 합니다.

Hello 텍사스 기기 SensorTag 장치를 사용 하는 경우 켤 수 있습니다 hello 빨간색 LED, 녹색 LED 또는 버저 IoT 허브에서 명령을 전송 하 여 합니다. IoT 허브에서 명령에 보내기 전에 먼저 hello 다음 순서 대로 두 개의 JSON 메시지를 보냅니다. 그런 다음 hello 명령 tooturn hello lights 또는 버저에 보낼 수 있습니다.

1. (해제) 하는 모든 Led 형식 및 hello 버저 다시 설정 하십시오.

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

이제 hello 나오는 명령 tooturn hello lights 또는 hello SensorTag 장치에서 버저에 보낼 수 있습니다.

* Hello 빨간색 LED를 켭니다.

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Hello 녹색 LED를 켭니다.

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Hello 버저를 설정 합니다.

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>다음 단계

원하는 toogain IoT 가장자리에 대 한 자세한 하 고 몇 가지 코드 예제를 시험해 방문 hello 다음 개발자 자습서 및 리소스:

* [Azure IoT Edge][lnk-sdk]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

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
