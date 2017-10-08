---
title: "Connect Arduino (C) tooAzure IoT-3 단원: 샘플을 실행 | Microsoft Docs"
description: "배포 하 여 샘플 응용 프로그램 tooAdafruit 페더 M0 WiFi tooyour IoT hub 메시지를 보내고 hello led가 깜박이를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 클라우드 서비스 arduino toocloud 데이터 보내기"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>샘플 응용 프로그램 toosend 장치-클라우드 메시지 실행
## <a name="what-you-will-do"></a>수행할 사항
이 문서에서는 보여 toodeploy 및 프로그램 Adafruit 페더 M0 WiFi Arduino에서 샘플 응용 프로그램 실행을 해당 보내는 메시지 tooyour IoT 허브 보드 어떻게 합니다.

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
하면 toouse hello 도구 toodeploy gulp 하 고 Arduino 보드에 hello 샘플 Arduino 응용 프로그램을 실행 하는 방법에 대해 설명 합니다.

## <a name="what-you-need"></a>필요한 항목
* 이 작업을 시작 하기 전에 성공적으로 완료 해야 [메시지 Azure 함수 응용 프로그램 및 저장소 계정 tooprocess와 저장소 IoT 허브를 만들][process-and-store-iot-hub-messages]합니다.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IoT Hub 및 장치 연결 문자열 가져오기
장치 연결 문자열 hello 사용 되는 tooconnect Arduino 보드 tooyour IoT 허브는 합니다. hello IoT 허브 연결 문자열은 프로그램 Arduino 나타내는 IoT 허브 toohello 장치 id 보드 hello IoT 허브에서 사용 되는 tooconnect입니다.

* Hello 다음 Azure CLI 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.

```bash
az iot hub list -g iot-sample --query [].name
```

사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.

* Hello 다음 Azure CLI 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`IoT 허브를 만들고 Arduino 보드를 등록 하는 때를 지정 하는 hello 이름이입니다.

* Hello 다음 명령을 실행 하 여 hello 장치 연결 문자열을 가져옵니다.

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

사용 하 여 `mym0wifi` 의 hello 값으로 `{device id}` hello 값을 변경 되지 않은 경우.
## <a name="configure-hello-device-connection"></a>Hello 장치 연결 구성
tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.

1. Hello hello 장치 검색 cli 사용 하 여 hello 장치의 직렬 포트를 가져옵니다.

   ```bash
   devdisco list --usb
   ```

   Toohello 다음과 유사한 출력을 확인 및 Arduino 보드에 대 한 hello usb COM 포트를 찾을 해야 하면:

   ![장치 검색][device-discovery]

2. 파일 열기 hello `config.json` 단원 폴더 hello와의 COM 포트 번호를 발견 하는 hello hello 값을 추가 합니다.

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Windows 플랫폼에서 hello COM 포트에 대 한 형식이 지므로 hello의 `COM1, COM2, ...`합니다. macOS 또는 Ubuntu에서는 `/dev/`로 시작합니다.

3. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. 장치 구성 파일 열기 hello `config-arduino.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. Hello 바꾸기 작업을 수행 하는 hello 확인 `config-arduino.json` 파일:

   * 대체 **[Wi-fi SSID]** toohello 인터넷 연결에 Wi-fi SSID로 합니다.
   * **[Wi-Fi password]**를 사용자의 Wi-Fi 암호로 바꿉니다. Wi-fi 암호 필요 하지 않은 경우 hello 문자열을 제거 합니다.
   * 대체 **[IoT 장치 연결 문자열]** hello로 `device connection string` 얻을 수 있습니다.
   * 대체 **[IoT 허브 연결 문자열]** hello로 `iot hub connection string` 얻을 수 있습니다.

   > [!NOTE]
   > 이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다. 그대로 유지합니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 Arduino 보드에 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> hello 기본 gulp 작업 실행 `install-tools` 및 `run` 순차적으로 작업 합니다. 때 있습니다 [hello 깜박임 앱 배포][deployed-the-blink-app]를 개별적으로 이러한 작업을 실행 합니다.

## <a name="verify-that-hello-sample-application-works"></a>Hello 샘플 응용 프로그램이 작동 하는지 확인 하십시오.
Hello GPIO #0 온보드 led가 깜박입니다.이 2 초 마다 표시 됩니다. Hello led가 깜박입니다 때마다 hello 샘플 응용 프로그램 메시지 tooyour IoT hub를 보내고 해당 hello 메시지에 전송 되었습니다. IoT hub tooyour 확인 합니다. 또한 hello IoT hub에서 수신 된 각 메시지는 hello 콘솔 창에 인쇄 됩니다. 샘플 응용 프로그램 hello 20 개의 메시지를 보낸 후 자동으로 종료 합니다.

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>요약
배포 되었으며 Arduino 보드 toosend 장치-클라우드 메시지 tooyour IoT 허브에서 hello 새 깜박임 샘플 응용 프로그램을 실행 합니다. 이제 toohello 저장소 계정에 작성 된 것 처럼 메시지를 모니터링 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Storage에 유지되는 메시지 읽기][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md