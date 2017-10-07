---
title: "aaaIntel Edison toocloud (C)-Intel Edison 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 방법을 toosetup 하 고이 자습서에서는 Intel Edison toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 Intel Edison tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot intel edison, intel edison iot 허브, intel edison 보낼 데이터 toocloud, intel edison toocloud"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a>Intel Edison tooAzure IoT Hub (C) 연결

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

이 자습서에서는 먼저 Intel Edison 작업할 hello 기본 사항 학습 합니다. 그런 다음 배웁니다 tooseamlessly 장치 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다.

아직 키트가 없으세요? [여기](https://azure.microsoft.com/develop/iot/starter-kits)에서 시작하세요.

## <a name="what-you-do"></a>수행할 작업

* Intel Edison 및 Grove 모듈을 설정합니다.
* IoT Hub를 만듭니다.
* IoT Hub에 Edison용 장치를 등록합니다.
* Edison toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.

Intel Edison tooan IoT hub를 만들면를 연결 합니다. 다음 예제 응용 프로그램에서에서를 실행 Edison toocollect 온도 및 습도 데이터 나무숲을 조성 온도 센서 합니다. 마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.

## <a name="what-you-learn"></a>학습 내용

* 어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다.
* 어떻게 나무숲을 조성 온도 센서와 Edison tooconnect 합니다.
* 어떻게 Edison에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.
* 어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.

## <a name="what-you-need"></a>필요한 항목

![필요한 항목](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* hello Intel Edison 보드
* Arduino 확장 보드
* 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
* Windows 또는 Linux를 실행하는 Mac 또는 PC
* 인터넷 연결.
* 마이크로 B tooType A USB 케이블
* DC(직류) 전원 공급 장치 전원 공급 장치 정격은 다음과 같아야 합니다.
  - 7-15V DC
  - 1500mA 이상
  - hello 센터/내부 pin hello 양수 극의 hello 전원 공급 장치가 있어야 합니다.

hello 다음 항목은 선택 사항:

* Grove Base Shield V2
* Grove - 온도 센서
* Grove 케이블
* 모든 공백 막대 또는 나사 hello 패키징, 나사 두 toofasten hello 모듈 toohello 확장 보드 등의 나사와 플라스틱 스페이서 4 집합에에서 포함 합니다.

> [!NOTE] 
Hello 코드 샘플 지원 센서 데이터를 시뮬레이션 하기 때문에 이러한 항목은 선택 사항입니다.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Intel Edison 설정

### <a name="assemble-your-board"></a>보드 조립

이 섹션 단계 tooattach Intel® Edison 모듈 tooyour 확장 보드를 포함합니다.

1. Hello 확장 보드에 hello 나사 hello 모듈에 hello 허점 만나려고 프로그램 확장 보드에 흰색 hello 개요 내의 hello Intel® Edison 모듈을 배치 합니다.

2. Hello 단어 바로 아래 hello 모듈을 누르면 `What will you make?` 간단히 생각 될 때까지 합니다.

   ![보드 2 조립](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. Hello 두 (hello 패키지에 포함 됨) 하는 16 진수 너트 toosecure hello 모듈 toohello 확장 보드를 사용 합니다.

   ![보드 3 조립](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. Hello 확장 보드에 네 개의 모퉁이 구멍 hello 중 하나에 나사를 삽입 합니다. 비틀 및 hello 나사에 흰색 hello 플라스틱 스페이서 중 하나를 강화 합니다.

   ![보드 4 조립](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. 반복에 대 한 다른 3 개의 모퉁이 스페이서 hello 합니다.

   ![보드 5 조립](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

이제 보드가 조립됩니다.

   ![조립된 보드](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>연결 나무숲을 조성 자료 방패 hello 및 hello 온도 센서

1. Hello 나무숲을 조성 자료 방패 tooyour 보드에 배치 합니다. 모든 핀이 보드에 꽂혀 있는지 확인합니다.
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. Hello 나무숲을 조성 자료 방패에 나무숲을 사용 하 여 나무숲을 조성 케이블 tooconnect 조성 온도 센서 **A0** 포트입니다.

   ![Tootemperature 센서 연결](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison 및 센서 연결](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

이제 센서가 준비되었습니다.

### <a name="power-up-edison"></a>Edison 전원 켜기

1. Hello 전원 공급 장치에 연결 합니다.

   ![전원 공급 장치 꽂기](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. (DS1 hello Arduino * 확장 보드에 표시) 녹색 led가 켜지 고 켜져 해야 합니다.

3. Hello 보드 toofinish 부팅에 대 일 분 기다립니다.

   > [!NOTE]
   > DC 전원 공급 장치가 하면 전원 hello 보드 USB 포트를 통해 계속 됩니다. 자세한 내용은 `Connect Edison tooyour computer` 섹션을 참조하세요. 이러한 방식으로 보드를 켜면 보드에서 예기치 않은 동작이 나타날 수 있습니다. 이러한 현상은 Wi-Fi 또는 구동 모터를 사용할 때 더욱 두드러집니다.

### <a name="connect-edison-tooyour-computer"></a>Edison tooyour 컴퓨터 연결

1. Edison 장치 모드는 hello 두 마이크로 USB 포트에 대 한 hello 마이크로 스위치를 설정/해제 합니다. 장치 모드와 호스트 모드 간 차이점에 대해서는 [여기](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)를 참조하세요.

   ![Hello 마이크로 스위치를 설정/해제](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. Hello 상위 마이크로 USB 포트에 hello 마이크로 USB 케이블을 연결 합니다.

   ![위쪽 마이크로 USB 포트](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. 플러그를 컴퓨터에 USB 케이블의 다른 쪽 끝을 hello 합니다.

   ![컴퓨터 USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. 컴퓨터에 새 장치를 탑재(컴퓨터에 SD 카드를 꽂는 것과 매우 유사함)할 때 보드가 완전히 초기화된다는 것을 알 수 있습니다.

## <a name="download-and-run-hello-configuration-tool"></a>다운로드 하 고 hello 구성 도구를 실행 합니다.
Hello 최신 구성 도구에서 가져올 [이 링크](https://software.intel.com/en-us/iot/hardware/edison/downloads) hello 아래에 나열 `Installers` 제목입니다. Hello 도구를 실행 하 고에 따라 해당 화면에 나타나는 지침, 필요한 경우 다음을 클릭

### <a name="flash-firmware"></a>펌웨어 플래시
1. Hello에 `Set up options` 페이지 `Flash Firmware`합니다.
2. 보드에 hello 이미지 tooflash hello 다음 중 하나를 수행 하 여 선택 합니다.
   - 보드 hello 최신 펌웨어 이미지와 Intel에서 사용할 수 있는 선택 toodownload 및 플래시 `Download hello latest image version xxxx`합니다.
   - tooflash 이미 컴퓨터에 저장 한 이미지와 함께 보드 선택 `Select hello local image`합니다. Tooflash tooyour 게시판 tooand 선택 hello 이미지를 찾습니다.
3. hello 설치 도구 tooflash 보드를 시도 합니다. hello 전체 깜박이 프로세스는 too10 분 정도 걸릴 수 있습니다.

### <a name="set-password"></a>암호 설정
1. Hello에 `Set up options` 페이지 `Enable Security`합니다.
2. Intel® Edison 보드에 대한 사용자 지정 이름을 설정할 수 있습니다. 선택 사항입니다.
3. 보드에 대한 암호를 입력한 후 `Set password`를 클릭합니다.
4. 나중에 사용 되는 hello 암호를 표시 합니다.

### <a name="connect-wi-fi"></a>Wi-Fi 연결
1. Hello에 `Set up options` 페이지 `Connect Wi-Fi`합니다. 사용 가능한 Wi-fi 네트워크에 대 한 컴퓨터 검색으로 tooone 분을 대기 합니다.
2. Hello에서 `Detected Networks` 드롭 다운 목록에서 네트워크를 선택 합니다.
3. Hello에서 `Security` 드롭 다운 목록, 선택 hello 네트워크의 보안 종류입니다.
4. 로그인 및 암호 정보를 입력한 다음 `Configure Wi-Fi`를 클릭합니다.
5. Hello 아래로 나중에 사용 되는 IP 주소를 표시 합니다.

> [!NOTE]
> Edison 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다. Edison tooyour hello IP 주소를 사용 하 여 연결 하는 컴퓨터입니다.

   ![Tootemperature 센서 연결](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

축하합니다. Edison 구성을 마쳤습니다.

## <a name="run-a-sample-application-on-intel-edison"></a>Intel Edison에 샘플 응용 프로그램 실행

### <a name="prepare-hello-azure-iot-device-sdk"></a>Azure IoT 장치 SDK hello 준비

1. Hello 호스트 컴퓨터 tooconnect tooyour Intel Edison에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다. hello IP 주소가 hello 구성 도구에서 고 hello 암호는 hello 하나 해당 도구에서 설정 했습니다.
    - Windows용 [PuTTY](http://www.putty.org/)
    - Ubuntu 또는 macOS에서 기본 제공 SSH 클라이언트 hello (실행 `ssh root@"hello IP address"`).

2. Hello 샘플 클라이언트 응용 프로그램 tooyour 장치를 복제 합니다. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. 다음 명령 toobuild Azure IoT SDK 다음 toohello 리포지토리 폴더 toorun hello 탐색

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a>Hello 샘플 응용 프로그램 구성

1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.

   ```bash
   nano config.h
   ```

   ![Config 파일](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   이 파일에는 사용자가 구성할 수 있는 두 개의 매크로가 있습니다. hello 먼저 하나는 `INTERVAL`, toocloud 전송 하는 두 개의 메시지 간의 hello 시간 간격을 정의 하는 합니다. 두 번째 식 hello `SIMULATED_DATA`, 값은 부울 값 여부 toouse 센서 데이터를 시뮬레이션 하는 여부입니다.

   경우 있습니다 **hello 센서 없는**설정 hello `SIMULATED_DATA` 너무 값`1` toomake hello 샘플 응용 프로그램을 만들고 시뮬레이션된 센서 데이터를 사용 합니다.

2. Control-O > Enter > Control-X를 눌러 저장하고 종료합니다.

### <a name="build-and-run-hello-sample-application"></a>빌드 및 hello 샘플 응용 프로그램 실행

1. Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 빌드하십시오.

   ```bash
   cmake . && make
   ```
   ![빌드 출력](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   하면 복사-붙여넣기 hello 장치 연결 문자열 hello 작은따옴표에 있는지 확인 합니다.

Hello 다음 출력에서는 hello 센서 데이터와 hello 전송 된 메시지를 tooyour IoT 허브는 표시 됩니다.

![출력-Intel Edison tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a>다음 단계

샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
