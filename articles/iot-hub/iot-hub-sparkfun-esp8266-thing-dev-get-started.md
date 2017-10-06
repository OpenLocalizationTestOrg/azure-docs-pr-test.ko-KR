---
title: "aaaESP8266 toocloud-연결 Sparkfun ESP8266 일 Dev tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup이 자습서에서에 대 한 IoT Hub Sparkfun ESP8266 일 Dev tooAzure toosend 데이터 toohello Azure 클라우드 플랫폼을 연결 하 고 있습니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Sparkfun ESP8266 일 Dev tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, Thing Dev 및 IoT Hub 간 연결](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>수행할 사항

만들려는 Sparkfun ESP8266 일 Dev tooan IoT 허브를 연결 합니다. 다음 DHT22 센서에서 샘플 응용 프로그램 ESP8266 toocollect 온도 및 습도 데이터에 대해 실행 합니다. 마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.

> [!NOTE]
> 이러한 단계 tooconnect 다른 ESP8266 보드를 사용 하는 경우 여전히 따라 수 것 tooyour IoT 허브입니다. Hello ESP8266 보드를 사용 하는, 따라 tooreconfigure hello를 할 수 있습니다 `LED_PIN`합니다. 예를 들어 ESP8266 AI Thinker에서를 사용 하는 경우 변경할 수 있습니다에서 `0` 너무`2`합니다. 아직 키트가 없나요? [여기](http://azure.com/iotstarterkits)를 클릭하세요.

## <a name="what-you-will-learn"></a>알아볼 내용

* 어떻게 toocreate IoT hub 일 개발에 대 한 장치를 등록 하 고
* 어떻게 tooconnect 일 Dev hello 센서와 사용자의 컴퓨터.
* 방법 항목 개발에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터
* 어떻게 toosend hello 센서 데이터 tooyour IoT 허브입니다.

## <a name="what-you-will-need"></a>필요한 사항

![hello 자습서에 필요한 부품](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete 일 개발자 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.

* hello Sparkfun ESP8266 일 Dev 보드 합니다.
* 마이크로 USB tooType A USB 케이블

개발 환경에 대 한 hello 다음 구성 요소도 필요.

* 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
* Windows 또는 Ubuntu가 실행되는 Mac 또는 PC
* 무선 네트워크에 Sparkfun ESP8266 일 Dev tooconnect에 대 한 합니다.
* 인터넷 연결 toodownload hello 구성 도구입니다.
* [Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 버전 이상, 이전 버전 hello AzureIoT 라이브러리와 함께 작동 하지 것입니다.

hello 다음 항목은 선택적 요소는 센서 없는 경우. 시뮬레이션 된 센서 데이터를 사용 하 여 hello 옵션이 있습니다.

* Adafruit DHT22 온도 및 습도 센서
* 실험용 회로판
* M/M 점퍼 와이어

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>ESP8266 일 Dev hello 센서 및 컴퓨터를 사용 하 여 연결

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>DHT22 온도 및 습도 센서 연결 tooESP8266 일 개발

다음과 같이 hello breadboard 및 점퍼 와이어 toomake hello 연결을 사용 합니다. 센서가 없는 경우 시뮬레이션된 센서 데이터를 사용할 수 있으므로 이 섹션을 건너뜁니다.

![연결 참조](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

센서 핀에 대 한 hello 배선 다음 사용 합니다.

| 시작(센서)           | 끝(보드)           | 케이블 색   |
| -----------------------  | ---------------------- | ------------: |
| VDD(27F 핀)            | 3V(8A 핀)           | 빨간색 케이블     |
| 데이터(28F 핀)           | GPIO 2(9A 핀)       | 흰색 케이블    |
| GND(30F 핀)            | GND(7J 핀)          | 검은색 케이블   |


- 자세한 내용은 [DHT22 센서 설정](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf)(영문) 및 [Sparkfun ESP8266 Thing Dev 사양](https://www.sparkfun.com/products/13711)(영문)을 참조하세요.

이제 Sparkfun ESP8266 Thing Dev를 작동 센서와 연결해야 합니다.

![dht22와 ESP8266 Thing Dev 연결](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Sparkfun ESP8266 일 Dev tooyour 컴퓨터 연결

다음과 같이 hello 마이크로 USB tooType USB 케이블 tooconnect Sparkfun ESP8266 일 Dev tooyour 컴퓨터를 사용 합니다.

![페더 huzzah tooyour 컴퓨터 연결](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>직렬 포트 권한 추가 – Ubuntu만

Ubuntu를 사용 하는 경우 일반 사용자에 hello 권한을 toooperate에 hello USB 포트의 Sparkfun ESP8266 일 개발 있는지 확인 다음이 단계를 수행 하는 일반 사용자에 대 한 tooadd 직렬 포트 사용 권한:

1. Hello 다음 터미널에서 명령을 실행 합니다.

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Hello 다음 출력 중 하나를 가져오는:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Hello 출력 `uucp` 또는 `dialout` 즉 hello 소유자의 그룹 이름을 hello USB 포트입니다.

1. Hello 다음 명령을 실행 하 여 hello 사용자 toohello 그룹을 추가 합니다.

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`hello 이전 단계에서는 가져온 hello 그룹 소유자 이름입니다. `<username>`은 Ubuntu 사용자 이름입니다.

1. 로그 아웃 Ubuntu 하 한이 다시 로그인 tootake 효과 변경 하는 hello에 대 한 키를 누릅니다.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>센서 데이터를 수집 하 고 tooyour IoT hub 보내기

이 섹션에서는 Sparkfun ESP8266 Thing Dev에 대한 샘플 응용 프로그램을 배포하고 실행합니다. hello 샘플 응용 프로그램 hello Sparkfun ESP8266 작업 개발자의 led가 깜박입니다 hello 온도 보냅니다 및 IoT 허브에서 hello DHT22 센서 tooyour 습도 데이터 수집 합니다.

### <a name="get-hello-sample-application-from-github"></a>GitHub에서 hello 샘플 응용 프로그램 가져오기

hello 샘플 응용 프로그램은 GitHub에서 호스트 됩니다. GitHub에서 hello 샘플 응용 프로그램을 포함 하는 hello 샘플 리포지토리를 복제 합니다. tooclone hello 샘플 리포지토리 다음이 단계를 수행 합니다.

1. 명령 프롬프트 또는 터미널 창을 엽니다.
1. 저장 된 hello 샘플 응용 프로그램 toobe 저장할 tooa 폴더를 이동 합니다.
1. Hello 다음 명령을 실행 합니다.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Arduino IDE에서 Sparkfun ESP8266 일 dev hello 패키지를 설치 합니다.

1. Hello 샘플 응용 프로그램 저장 된 hello 폴더를 엽니다.
1. Arduino IDE에서 hello 응용 프로그램 폴더에서 hello app.ino 파일을 엽니다.

   ![arduino ide에서 열린 hello 샘플 응용 프로그램](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. Hello Arduino IDE, 클릭 **파일** > **기본 설정**합니다.
1. Hello에 **기본 설정** 대화 상자에서 hello 아이콘 다음 toohello 클릭 **보드 관리자 Url을 추가로** 입력란.
1. Hello 팝업 창에 hello url을 입력 한 다음 클릭 **확인**합니다.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![arduino ide tooa 패키지 url 지정](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. Hello에 **Preference** 대화 상자를 클릭 **확인**합니다.
1. **도구** > **보드** > **보드 관리자**를 클릭한 후 esp8266을 검색합니다.
   ESP8266 버전 2.2.0 이상을 설치해야 합니다.

   ![hello esp8266 패키지가 설치 되어](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. **도구** > **보드** > **Sparkfun ESP8266 Thing Dev**를 클릭합니다.

### <a name="install-necessary-libraries"></a>필요한 라이브러리 설치

1. Hello Arduino IDE, 클릭 **스케치** > **라이브러리 포함** > **관리 라이브러리**합니다.
1. 다음 라이브러리 이름을 하나씩 hello에 대 한 검색입니다. 각 찾았으면 hello 라이브러리에 대 한 클릭 **설치**합니다.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>실제 DHT22 센서가 없나요?

실제 DHT22 센서 없는 경우 hello 샘플 응용 프로그램 데이터를 온도 및 습도 시뮬레이션할 수 있습니다. tooenable hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터는 다음이 단계를 따르십시오.

1. 열기 hello `config.h` hello에 대 한 파일 `app` 폴더입니다.
1. 다음 코드 줄을 hello를 찾아 hello 값에서 변경 `false` 너무`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![hello 샘플 응용 프로그램 toouse 시뮬레이션 데이터를 구성 합니다.](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. `Control-s`로 저장합니다.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Hello 샘플 응용 프로그램 tooSparkfun ESP8266 일 개발 배포

1. Hello Arduino IDE, 클릭 **도구** > **포트**, Sparkfun ESP8266 일 개발 hello 직렬 포트를 클릭 한 다음
1. 클릭 **스케치** > **업로드** toobuild hello 샘플 응용 프로그램 tooSparkfun ESP8266 일 장치 배포

> [!Note]
> MacOS를 사용 하는 경우 아마도 hello 메시지를 업로드 하는 동안 다음을 볼 수 있습니다. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Ternimal 창을 열고이 문제를 작업 toosolve 아래 완료 하십시오.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>자격 증명 입력

Hello 업로드 성공적으로 완료 되 면 hello 단계 tooenter 자격 증명를 따릅니다.

1. Hello Arduino IDE, 클릭 **도구** > **직렬 모니터**합니다.
1. Hello 직렬 모니터 창에서 hello 오른쪽 아래 모서리에 hello 두 드롭 다운 목록을 확인 합니다.
1. 선택 **줄 닫는** hello 왼쪽된 드롭다운 목록에 대 한 합니다.
1. 선택 **115200 보드** hello 오른쪽 드롭다운 목록에 대 한 합니다.
1. Hello 직렬 모니터 창의 hello 위쪽에 있는 입력된 상자 hello에에서 hello tooprovide 요청 하는 경우 다음 정보를 입력, 클릭 하 고 **보낼**합니다.
   * Wi-Fi SSID
   * Wi-Fi 암호
   * 장치 연결 문자열

> [!Note]
> hello 자격 증명 정보는 hello EEPROM의 Sparkfun ESP8266 일 장치에 저장 Hello Sparkfun ESP8266 일 Dev 보드에 hello reset 단추를 누르면 hello 샘플 응용 프로그램 묻는 경우 tooerase hello 정보입니다. 입력 `Y` toohave hello 정보를 삭제 하 고 라는 tooprovide hello 정보를 다시 표시 됩니다.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Hello 샘플 응용 프로그램을 성공적으로 실행 되는지 확인 합니다.

표시 되 면 hello 다음 hello 직렬 모니터 창에서 출력 및 hello Sparkfun ESP8266 일 개발, hello 샘플 응용 프로그램의 led가 깜박입니다.이 성공적으로 실행 됩니다.

![arduino ide에서 최종 출력](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>다음 단계

Sparkfun ESP8266 일 Dev tooyour IoT 허브를 연결 하 고 캡처한 hello 센서 데이터 tooyour IoT 허브를 전송 했습니다. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
