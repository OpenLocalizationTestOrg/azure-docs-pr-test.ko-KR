---
title: "aaaRaspberry Pi toocloud (C)-라스베리 Pi 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 방법을 toosetup 하 고이 자습서에서는 라스베리 Pi toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 라스베리 Pi tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot 라즈베리 라즈베리 pi pi iot 허브 라즈베리 pi 송신 데이터 toocloud 라즈베리 pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>라스베리 Pi tooAzure IoT Hub (C) 연결

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

이 자습서에서는 먼저 라스베리 Pi Raspbian를 실행 하는 작업의 hello 기본 사항 학습 합니다. 그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다. Windows 10 IoT Core 샘플에 대 한 이동 toohello [Windows 개발자 센터](http://www.windowsondevices.com/)합니다.

아직 키트가 없으세요? [Raspberry Pi 온라인 시뮬레이터](iot-hub-raspberry-pi-web-simulator-get-started.md)를 사용해 보세요. 또는 새 키트를 [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 구입합니다.

## <a name="what-you-do"></a>수행할 작업

* IoT Hub를 만듭니다.
* IoT Hub에 Pi용 장치를 등록합니다.
* Raspberry Pi를 설치합니다.
* Pi toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.

만들면 라스베리 Pi tooan IoT 허브를 연결 합니다. 다음 BME280 센서에서 Pi toocollect 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다. 마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.

## <a name="what-you-learn"></a>학습 내용

* 어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다.
* 어떻게 tooconnect BME280 센서와 Pi 합니다.
* 어떻게 Pi에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.
* 어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.

## <a name="what-you-need"></a>필요한 항목

![필요한 항목](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* hello 라스베리 Pi 2 또는 라스베리 Pi 3 보드 합니다.
* 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
* 모니터, USB 키보드 및 마우스 tooPi 연결 하는 합니다.
* Windows 또는 Linux를 실행하는 Mac 또는 PC.
* 인터넷 연결.
* 16GB 이상의 microSD 카드.
* USB SD 어댑터 또는 microSD 카드 tooburn hello에 운영 체제 이미지 hello microSD 카드입니다.
* Hello 6 피트 마이크로 USB 케이블을 5 v 2 amp 전원 공급 장치.

hello 다음 항목은 선택 사항:

* 조립된 Adafruit BME280 온도, 압력 및 습도 센서.
* 실험용 회로판
* F/M 점퍼 와이어 6개.
* 확산형 10mm LED.


> [!NOTE] 
Hello 코드 샘플 지원 센서 데이터를 시뮬레이션 하기 때문에 이러한 항목은 선택 사항입니다.


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Raspberry Pi 설치

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Pi에 대 한 hello Raspbian 운영 체제를 설치 합니다.

Hello microSD 카드 hello Raspbian 이미지의 설치를 준비 합니다.

1. Raspbian을 다운로드합니다.
   1. [Desktop Raspbian 제시 다운로드](https://www.raspberrypi.org/downloads/raspbian/) (hello.zip 파일).
   1. Hello Raspbian 이미지 tooa 컴퓨터의 폴더에 추출 합니다.
1. Raspbian toohello microSD 카드를 설치 합니다.
   1. [다운로드 및 설치 hello Etcher SD 카드 버너 유틸리티](https://etcher.io/)합니다.
   1. Etcher를 실행 하 고 1 단계에서 압축을 푼 hello Raspbian 이미지를 선택 합니다.
   1. Hello microSD 카드 드라이브를 선택 합니다. Etcher 선택 했을 수 이미 hello 올바른 드라이브 참고 합니다.
   1. 플래시 tooinstall Raspbian toohello microSD 카드를 클릭 합니다.
   1. 설치가 완료 되 면 hello microSD 카드를 컴퓨터에서 제거 합니다. 되므로 안전 tooremove hello microSD 카드 직접 Etcher를 꺼냅니다. 자동으로 또는 완료 되 면 hello microSD 카드 탑재 해제 합니다.
   1. Pi에 hello microSD 카드를 삽입 합니다.

### <a name="enable-ssh-and-spi"></a>SSH 및 SPI를 사용하도록 설정

1. Pi toohello 모니터, 키보드 및 마우스 연결 Pi 시작한 다음 Raspbian 사용 하 여 로그인 `pi` hello. 사용자 이름 및 `raspberry` hello 암호와 합니다.
1. Hello 라즈베리 아이콘 클릭 > **기본 설정** > **라스베리 Pi 구성**합니다.

   ![hello Raspbian 기본 설정 메뉴](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Hello에 **인터페이스** 탭, 설정 **SPI** 및 **SSH** 너무**사용**, 클릭 하 고 **확인**합니다. 없습니다 실제 센서 고 시뮬레이션 toouse 센서 데이터를 하는 경우이 단계는 선택 사항입니다.

   ![Raspberry Pi에서 SPI 및 SSH를 사용하도록 설정](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH 및 SPI에서 더 많은 참조 문서를 찾을 수 있습니다 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 및 [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)합니다.

### <a name="connect-hello-sensor-toopi"></a>Hello 센서 tooPi 연결

사용 하 여 hello breadboard 및 점퍼 와이어 tooconnect LED 및 BME280 tooPi 다음과 같습니다. Hello 센서가 없는 경우 [이 섹션을 건너뛸](#connect-pi-to-the-network)합니다.

![hello 라스베리 Pi 및 센서 연결](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

hello BME280 센서 온도 및 습도 데이터를 수집할 수 있습니다. 및 장치 및 hello 클라우드 간의 통신 이면 hello led가 깜박입니다. 

센서 핀에 대 한 다음 배선 hello를 사용 합니다.

| 시작(센서 및 LED)     | 끝(보드)            | 케이블 색   |
| -----------------------  | ---------------------- | ------------: |
| LED VDD(5G 핀)         | GPIO 4(7 핀)         | 흰색 케이블   |
| LED GND(6G 핀)         | GND(6 핀)            | 검은색 케이블   |
| VDD(18F 핀)            | 3.3V PWR(17 핀)      | 흰색 케이블   |
| GND(20F 핀)            | GND(20 핀)           | 검은색 케이블   |
| SCK(21F 핀)            | SPI0 SCLK(23 핀)     | 주황색 케이블  |
| SDO(22F 핀)            | SPI0 MISO(21 핀)     | 노란색 케이블  |
| SDI(23F 핀)            | SPI0 MOSI(19 핀)     | 녹색 케이블   |
| CS(24F 핀)             | SPI0 CS(24 핀)       | 파란색 케이블    |

Tooview 클릭 [라스베리 Pi 2 & 3 Pin 매핑](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) 참조할 수 있도록 합니다.

성공적으로 연결한 후 BME280 tooyour 라스베리 Pi와 같은 이미지 아래 이어야 합니다.

![Pi와 BME280 연결](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello 네트워크에 연결

Pi hello 마이크로 USB 케이블 및 hello 전원 공급 장치를 사용 하 여 설정 합니다. 사용 하 여 hello 이더넷 케이블 tooconnect Pi tooyour 유선 네트워크 또는 hello에 따라 [hello 라스베리 Pi Foundation의에서 지침에 따라](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 무선 네트워크입니다. Tootake hello 메모 필요 하면 Pi에 대 한 toohello 성공적으로 연결 된 네트워크를 수행한 후 [프로그램 Pi의 IP 주소](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)합니다.

![연결 된 toowired 네트워크](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>Pi에서 샘플 응용 프로그램 실행

### <a name="install-hello-prerequisite-packages"></a>Hello 필수 구성 요소 패키지를 설치 합니다.

1. Hello 호스트 컴퓨터 tooconnect tooyour 라스베리 Pi에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.
   
   **Windows 사용자**
   1. Windows용 [PuTTY](http://www.putty.org/)를 다운로드 및 설치합니다. 
   1. Hello 호스트 이름 (또는 IP 주소)에 Pi 섹션의 hello IP 주소를 복사 하 고 SSH hello 연결 유형으로 선택 합니다.
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac 및 Ubuntu 사용자**
   
   Ubuntu 또는 macOS에 SSH 클라이언트를 기본 제공 하는 hello를 사용 합니다. Toorun 해야 `ssh pi@<ip address of pi>` tooconnect SSH 통해 Pi 합니다.
   > [!NOTE] 
   hello 기본 사용자 이름은 `pi` , hello 암호도 `raspberry`합니다.

1. C 및 Cmake hello 다음 명령을 실행 하 여 hello hello Microsoft Azure IoT 장치 SDK에 대 한 필수 구성 요소 패키지를 설치 합니다.

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Hello 샘플 응용 프로그램 구성

1. Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 복제 합니다.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Config 파일](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   이 파일에는 사용자가 구성할 수 있는 두 개의 매크로가 있습니다. hello 먼저 하나는 `INTERVAL`, toocloud 전송 하는 두 개의 메시지 간의 hello 시간 간격 (밀리초)을 정의 하는 합니다. 두 번째 식 hello `SIMULATED_DATA`, 값은 부울 값 여부 toouse 센서 데이터를 시뮬레이션 하는 여부입니다.

   경우 있습니다 **hello 센서 없는**설정 hello `SIMULATED_DATA` 너무 값`1` toomake hello 샘플 응용 프로그램을 만들고 시뮬레이션된 센서 데이터를 사용 합니다.

1. Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.

### <a name="build-and-run-hello-sample-application"></a>빌드 및 hello 샘플 응용 프로그램 실행

1. Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 빌드하십시오.

   ```bash
   cmake . && make
   ```
   ![빌드 출력](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   하면 복사-붙여넣기 hello 장치 연결 문자열 hello 작은따옴표에 있는지 확인 합니다.


Hello 다음 출력에서는 hello 센서 데이터와 hello 전송 된 메시지를 tooyour IoT 허브는 표시 됩니다.

![출력-라스베리 Pi tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>다음 단계

샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다. 라스베리 Pi가 보냈음을 tooyour IoT 허브 또는 송신 메시지 tooyour 라스베리 Pi는 명령줄 인터페이스에서 toosee hello 메시지 참조 hello [iothub 탐색기 자습서와 함께 메시징 관리 클라우드 장치](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)합니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
