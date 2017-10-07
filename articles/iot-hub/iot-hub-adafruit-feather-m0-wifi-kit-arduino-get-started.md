---
title: "M0 toocloud: 페더 M0 WiFi tooAzure IoT 허브 연결 | Microsoft Docs"
description: "자세한 내용은 방법 tooset 및이 자습서에서는 Adafruit 페더 M0 WiFi tooAzure IoT Hub toosend 데이터 toohello Azure 클라우드 플랫폼을 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Adafruit 페더 M0 WiFi tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280, Feather M0 WiFi 및 IoT Hub 간의 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

이 자습서에서는 먼저 Arduino 보드와 작업의 hello 기본 사항을 학습 합니다. 그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.

## <a name="what-you-do"></a>수행할 작업

만들면 Adafruit 페더 M0 WiFi tooan IoT 허브를 연결 합니다. 다음는 BME280에서 M0 WiFi toocollect hello 온도 및 습도 데이터에는 예제 응용 프로그램을 실행 합니다. 마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.


## <a name="what-you-learn"></a>학습 내용

* 어떻게 toocreate IoT hub 페더 M0 WiFi에 대 한 장치를 등록 하 고
* 어떻게 tooconnect 페더 M0 WiFi hello 센서와 사용자의 컴퓨터
* 어떻게 페더 M0 WiFi에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터
* Toosend 센서 데이터 tooyour IoT 허브를 hello 하는 방법

## <a name="what-you-need"></a>필요한 항목

![hello 자습서에 필요한 부품](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete 페더 M0 WiFi 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.

* hello 페더 M0 WiFi 보드
* 마이크로 USB tooType A USB 케이블

Hello 개발 환경에 대 한 작업을 수행 해야 합니다.

* 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
* Windows 또는 Ubuntu를 실행하는 Mac 또는 PC
* 페더 M0 WiFi tooconnect에 대 한 무선 네트워크입니다.
* 인터넷 연결 toodownload hello 구성 도구입니다.
* [Arduino IDE](https://www.arduino.cc/en/main/software) 버전 1.6.8 이상 이전 버전 hello Azure IoT Hub 라이브러리와 함께 작동 하지 않습니다.

센서를 설정 하지 않은 경우 hello 다음 항목은 선택적입니다. 시뮬레이션 된 센서 데이터를 사용 하 여 hello 옵션도 제공 합니다.

* BME280 온도 및 습도 센서
* 실험용 회로판
* M/M 점퍼 와이어

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>페더 M0 WiFi hello 센서 및 컴퓨터를 사용 하 여 연결
이 섹션에서는 hello 센서 tooyour 보드를 연결합니다. 그런 다음 나중에 사용할 장치 tooyour 컴퓨터에 연결할 수도 있습니다.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>DHT22 온도 및 습도 센서 tooFeather M0 WiFi에 연결

Hello breadboard 및 점퍼 와이어 toomake hello 연결을 사용 합니다. 센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.

![연결 참조](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


센서 핀에 대 한 다음 배선 hello를 사용 합니다.


| 시작(센서)           | 끝(보드)            | 케이블 색   |
| -----------------------  | ---------------------- | ------------: |
| VDD(27A 핀)            | 3V(3A 핀)            | 빨간색 케이블     |
| GND(29A 핀)            | GND(6A 핀)           | 검은색 케이블   |
| SCK(30A 핀)            | SCK(12A 핀)          | 노란색 케이블  |
| SDO(31A 핀)            | MI(14A 핀)           | 흰색 케이블   |
| SDI(32A 핀)            | M0(13A 핀)           | 파란색 케이블    |
| CS(33A 핀)             | GPIO 5(15J 핀)       | 주황색 케이블  |

자세한 내용은 [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all)(Adafruit BME280 습도 + 기압 + 온도 센서 혁신 세션) 및 [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts)(Adafruit Feather M0 WiFi 핀 배열)를 참조하세요.



이제 Feather M0 WiFi를 작동 센서와 연결해야 합니다.

![DHT22를 Feather Huzzah와 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>페더 M0 WiFi tooyour 컴퓨터 연결

표시 된 것 처럼 hello 마이크로 USB tooType USB 케이블 tooconnect 페더 M0 WiFi tooyour 컴퓨터를 사용 합니다.

![페더 Huzzah tooyour 컴퓨터 연결](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>직렬 포트 권한 추가(Ubuntu만 해당)

Ubuntu를 사용 하는 경우 했는지 확인 hello 권한을 toooperate에 hello USB 포트의 페더 M0 WiFi 합니다. tooadd 직렬 포트 사용 권한을 다음이 단계를 따르십시오.


1. 터미널 hello 다음 명령을 실행 합니다.

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Hello 다음 출력 중 하나를 가져오는:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Hello 출력 알 수 있듯이 `uucp` 또는 `dialout` hello USB 포트 hello 그룹 소유자 이름입니다.

2. tooadd hello 사용자 toohello 그룹, hello 다음 명령을 실행 합니다.

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   Hello 그룹 소유자 이름 hello 이전 단계에서 가져온 `<group-owner-name>`합니다. Ubuntu 사용자 이름은 `<username>`입니다.

3. Hello 변경 tooappear에 대 한 로그 Ubuntu 아웃 한 다음 다시 로그인 합니다.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>센서 데이터를 수집 하 고 tooyour IoT hub 보내기

이 섹션에서는 Feather M0 WiFi에서 샘플 응용 프로그램을 배포하고 실행합니다. hello 샘플 응용 프로그램을 사용 하면 hello 페더 M0 WiFi에 led가 깜박입니다. 그런 다음 hello 온도 보냅니다 및 IoT 허브에서 hello BME280 센서 tooyour 습도 데이터 수집 합니다.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>GitHub에서 hello 샘플 응용 프로그램을 가져오고 hello Arduino IDE를 준비 합니다.

hello 샘플 응용 프로그램은 GitHub에서 호스트 됩니다. GitHub에서 hello 샘플 응용 프로그램을 포함 하는 hello 샘플 리포지토리를 복제 합니다. tooclone hello 샘플 리포지토리 다음이 단계를 수행 합니다.

1. 명령 프롬프트 또는 터미널 창을 엽니다.

2. 저장 된 hello 샘플 응용 프로그램 toobe 저장할 tooa 폴더를 이동 합니다.
3. Hello 다음 명령을 실행 합니다.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Hello Arduino IDE에서에서 페더 M0 WiFi에 대 한 hello 패키지 설치

1. Hello 샘플 응용 프로그램 저장 된 hello 폴더를 엽니다.

2. Hello Arduino IDE의에서 hello 응용 프로그램 폴더에 hello app.ino 파일을 엽니다.

   ![Arduino IDE에서 열린 hello 샘플 응용 프로그램](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. 클릭 **파일** > **기본 설정** (Windows/Linux) 또는 **Arduino** > **기본 설정** (Mac) 및 복사 하 고 hello에 아래 hello 링크 붙여넣기 **보드 관리자 Url을 추가로** hello Arduino IDE 기본 설정 옵션입니다.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. 클릭 **도구** > **보드** > **보드 관리자**, hello를 설치한 다음 `Arduino SAMD Boards` 버전 `1.6.2` 이상. 

1. 그런 다음 같은 창 hello, 설치 `Adafruit SAMD Boards` tooadd hello 보드 파일 정의 패키지 합니다.

   ![hello esp8266 패키지가 설치 되어](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. **도구** > **보드** > **Adafruit M0 WiFi**를 클릭합니다.

5. 드라이버를 설치합니다(Windows만 해당). 페더 M0 WiFi에 연결 하는 경우에 드라이버 tooinstall을 할 수 있습니다. 클릭 [hello 웹 페이지에서 다운로드 링크 hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello 드라이버 설치 합니다. 원하는 hello 단계 tooinstall hello 드라이버를 따릅니다.

### <a name="install-necessary-libraries"></a>필요한 라이브러리 설치

1. Hello Arduino IDE, 클릭 **스케치** > **라이브러리 포함** > **관리 라이브러리**합니다.

2. 다음 라이브러리 이름을 하나씩 hello에 대 한 검색입니다. 검색한 각 라이브러리에 대해 **설치**를 클릭합니다.

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. 수동으로 `Adafruit_WINC1500`을 설치합니다. 너무 이동[이 웹 사이트](https://github.com/adafruit/Adafruit_WINC1500) 클릭 **클론 또는 다운로드** > **zip 파일 다운로드**합니다. 프로그램 Arduino IDE에서 이동 하 여 너무**스케치** > **라이브러리 포함** > **.zip 라이브러리 추가** hello zip 파일을 추가 합니다.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>실제 BME280 센서 없는 경우 hello 샘플 응용 프로그램을 사용 하 여

실제 BME280 센서를 설정 하지 않은 경우 hello 샘플 응용 프로그램 데이터를 온도 및 습도 시뮬레이션할 수 있습니다. tooset hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 다음이 단계를 따르십시오.

1. 열기 hello `config.h` hello에 대 한 파일 `app` 폴더입니다.

2. 다음 코드 줄을 hello를 찾아 hello 값에서 변경 `false` 너무`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 구성 합니다.](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Hello 파일을 저장 `Control-s`합니다.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Hello 샘플 응용 프로그램 tooFeather M0 WiFi 배포

1. Hello Arduino IDE, 클릭 **도구** > **포트**, 페더 M0 WiFi에 대 한 hello 직렬 포트를 클릭 하 고 있습니다.

2. 클릭 **스케치** > **업로드** toobuild hello 샘플 응용 프로그램 tooFeather M0 WiFi를 배포 합니다.

### <a name="enter-your-credentials"></a>자격 증명 입력

Hello 업로드 성공적으로 완료 되 면 이러한 단계 tooenter 자격 증명를 따릅니다.

1. Hello Arduino IDE, 클릭 **도구** > **직렬 모니터**합니다.

2. Hello 직렬 모니터 창의 hello 오른쪽 아래에서 선택 **줄 닫는** hello 왼쪽 hello 드롭 다운 목록에서.
3. 선택 **115200 보드** hello 드롭 다운 목록에서 오른쪽 hello 합니다.
4. Hello 위쪽에 hello 입력된 상자에 hello 인 경우 다음 정보를 입력 한 클릭 tooprovide 요청 **보낼**:

   * Wi-Fi SSID
   * Wi-Fi 암호
   * 장치 연결 문자열

> [!Note]
> hello 자격 증명 정보는 hello 페더 M0 WiFi EEPROM에에서 저장 됩니다. Hello 페더 M0 WiFi 보드에 hello reset 단추를 누르면 hello 샘플 응용 프로그램 묻는 tooerase hello 정보입니다. 입력 `Y` tooerase hello 정보입니다. Tooprovide hello 정보를 두 번째로 묻는 합니다.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Hello 예제 응용 프로그램이 성공적으로 실행 되 고 있는지 확인 하십시오.

표시 되 면 hello 다음 hello 직렬 모니터 창에서 출력 hello 페더 M0 WiFi hello 샘플 응용 프로그램의 led가 깜박입니다.이 성공적으로 실행 되 고:

![Arduino IDE의 최종 출력](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>다음 단계

페더 M0 WiFi tooyour IoT 허브를 연결 하 고 캡처한 hello 센서 데이터 tooyour IoT 허브를 전송 했습니다. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

