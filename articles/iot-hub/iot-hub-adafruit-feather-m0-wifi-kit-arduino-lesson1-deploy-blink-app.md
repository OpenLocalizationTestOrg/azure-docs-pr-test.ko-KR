---
title: "Arduino tooAzure IoT-1과 연결: 앱 배포 | Microsoft Docs"
description: "GitHub에서 hello 샘플 Arduino 응용 프로그램을 복제 하 고이 응용 프로그램 tooyour Adafruit 페더 M0 WiFi gulp toodeploy를 실행 합니다. 이 샘플 응용 프로그램을 깜박일 hello GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 프로젝트, arduino led 깜박임, arduino led 깜박임 코드, arduino 깜박임 프로그램, arduino 깜박임 예제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>만들기 및 hello 깜박임 응용 프로그램 배포
## <a name="what-you-will-do"></a>수행할 사항
GitHub에서 hello 샘플 Arduino 응용 프로그램을 복제 하 고 hello gulp 도구 toodeploy hello 샘플 응용 프로그램 tooyour Adafruit 페더 M0 WiFi Arduino 보드를 사용 합니다. hello 샘플 응용 프로그램을 깜박일 hello barod에 GPIO #13 인해 2 초 마다 발생 했습니다.

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting-page]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
* 어떻게 toodeploy 및 실행된 hello 샘플 Arduino 보드에 응용 프로그램입니다.

## <a name="what-you-need"></a>필요한 항목
성공적으로 완료 해야 다음 작업 hello:

* [장치 구성][configure-your-device]
* [Hello 도구 가져오기][get-the-tools]

## <a name="open-hello-sample-application"></a>열기 hello 샘플 응용 프로그램
tooopen hello 샘플 응용 프로그램, 다음이 단계를 수행 합니다.

1. Hello 다음 명령을 실행 하 여 GitHub에서 hello 샘플 리포지토리를 복제 합니다.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Repo 구조][repo-structure]

hello `app.ino` hello에 대 한 파일 `app` 하위 폴더는 hello 코드 toocontrol hello LED가 있는 hello 키 원본 파일입니다.

### <a name="install-application-dependencies"></a>응용 프로그램 종속성 설치
Hello 라이브러리 및 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램에 필요한 다른 모듈을 설치 합니다.

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Hello 장치 연결 구성
tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.

1. Hello hello 장치 검색 cli 사용 하 여 hello 장치의 직렬 포트를 가져옵니다.

   ```bash
   devdisco list --usb
   ```

   Toohello 다음과 유사한 출력을 보고 Arduino 보드에 대 한 hello usb COM 포트를 찾을 해야: ![장치 검색][device-discovery]

2. 파일 열기 hello `config.json` 단원 폴더 hello와의 COM 포트 번호를 발견 하는 hello hello 값을 추가 합니다.

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Windows 플랫폼에서 hello COM 포트에 대 한 형식이 지므로 hello의 `COM1, COM2, ...`합니다. macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Arduino 보드에 대 한 필요한 hello 도구 설치

Hello 다음 명령을 실행 하 여 Arduino 보드에 대 한 hello Azure IoT 허브 SDK를 설치 합니다.

```bash
gulp install-tools
```

이 작업은 네트워크 연결에 따라 시간이 오래 toocomplete, 걸릴 수 있습니다.

> [!NOTE]
> Hello gulp 작업을 실행할 때 Arduino IDE 인스턴스 실행을 끝낸 후: `install-tools`, `run`합니다.

### <a name="deploy-and-run-hello-sample-app"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Hello 앱 작동 확인
Hello led가 깜박입니다.이 표시 되지 않으면 참조 hello [문제 해결 가이드] [ troubleshooting-page] toocommon 문제 해결 방법에 대 한 합니다.

![LED 깜박임][led-blinking]

## <a name="summary"></a>요약
필요한 hello 도구 toowork Arduino 보드와 함께 설치 하 고는 샘플 응용 프로그램 tooyour Arduino 보드 tooblink hello LED를 배포 합니다. 있습니다 수 이제 만들고, 배포, 및 Arduino 보드 tooAzure toosend IoT 허브를 연결 하는 또 다른 샘플 응용 프로그램을 실행 하 고 메시지를 수신 합니다.

## <a name="next-steps"></a>다음 단계
[Hello Azure 도구 가져오기][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md