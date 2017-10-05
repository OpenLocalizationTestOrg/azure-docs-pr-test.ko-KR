---
title: "Azure IoT에 Raspberry Pi(C) 연결 - 단원 1: 앱 배포 | Microsoft Docs"
description: "GitHub에서 샘플 C 응용 프로그램과, Raspberry Pi 3 보드에 이 응용 프로그램을 배포하기 위한 gulp를 복제합니다. 이 샘플 응용 프로그램은 보드에 연결된 LED를 2초마다 깜박이게 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Raspberry Pi LED 깜박임, Raspberry Pi를 통한 LED 깜박임"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>깜박임 응용 프로그램 만들기 및 배포
## <a name="what-you-will-do"></a>수행할 사항
GitHub에서 샘플 C 응용 프로그램을 복제하고 gulp 도구를 사용하여 Raspberry Pi 3에 샘플 응용 프로그램을 배포합니다. 샘플 응용 프로그램은 보드에 연결된 LED를 2초마다 깜박이게 합니다. 문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* Pi에 관한 네트워킹 정보를 검색하기 위해 `device-discover-cli` 도구 사용 방법.
* Pi에서 샘플 응용 프로그램을 배포하고 실행하는 방법.
* Pi에서 원격으로 실행되는 응용 프로그램을 배포하고 디버깅하는 방법.

## <a name="what-you-need"></a>필요한 항목
다음 작업을 성공적으로 완료해야 합니다.

* [장치 구성](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [도구 얻기](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a>Pi의 IP 주소 및 호스트 이름 가져오기
macOS 또는 Ubuntu의 터미널이나 Windows에서 명령 프롬프트를 열고 다음 명령을 실행합니다.

```bash
devdisco list --eth
```

출력은 다음과 유사해야 합니다.

![장치 검색](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Pi의 `IP address` 및 `hostname`을 기록해 둡니다. 이 정보는 이 문서의 뒤 부분에서 필요합니다.

> [!NOTE]
> Pi가 컴퓨터와 같은 네트워크에 연결되어 있어야 합니다. 예를 들어 컴퓨터는 무선 네트워크, Pi는 유선 네트워크에 연결되었다면 devdisco 출력에 IP 주소가 표시되지 않을 수 있습니다.

## <a name="open-the-sample-application"></a>샘플 응용 프로그램 열기
샘플 응용 프로그램을 열려면 다음 단계를 따릅니다.

1. 다음 명령을 실행하여 GitHub에서 샘플 리포지토리를 복제합니다.
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. 다음 명령을 실행하여 Visual Studio Code에서 샘플 응용 프로그램을 엽니다.
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Repo 구조](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

`app` 하위 폴더의 `main.c` 파일은 LED 제어 코드가 담긴 핵심 원본 파일입니다.

### <a name="install-application-dependencies"></a>응용 프로그램 종속성 설치
다음 명령을 실행하여 샘플 응용 프로그램에 필요한 라이브러리 및 기타 모듈을 설치합니다.

```bash
npm install
```

## <a name="configure-the-device-connection"></a>장치 연결 구성
장치 연결을 구성하려면 다음 단계를 따릅니다.

1. 다음 명령을 실행하여 장치 구성 파일을 생성합니다.
   
   ```bash
   gulp init
   ```
   
   구성 파일 `config-raspberrypi.json`에는 Pi에 로그인하는 데 사용하는 사용자 자격 증명이 포함됩니다. 사용자 자격 증명의 유출을 방지하기 위해 구성 파일은 컴퓨터 홈 폴더의 `.iot-hub-getting-started` 하위 폴더에 생성됩니다.

2. 다음 명령을 실행하여 Visual Studio Code에서 장치 구성 파일을 엽니다.
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. 자리 표시자 `[device hostname or IP address]`를 앞서 "Pi의 IP 주소 및 호스트 이름 가져오기"에서 확보한 IP 주소 또는 호스트 이름과 바꿉니다.
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> Raspberry Pi에 연결할 때 사용자 이름과 암호 대신 SSH 키를 사용할 수 있습니다. 사용 하 여 키를 생성 해야 하며이 작업을 수행 하기 위해 **붙여넣으세요** 및 **@ ssh-복사-id pi\<장치 주소\>**합니다.
>
> Windows의 경우 이러한 명령은 **Git Bash**에서 사용할 수 있습니다.
>
> MacOS의 경우 **brew install ssh-copy-id**를 실행해야 합니다.
>
> 키를 Raspberry Pi에 업로드한 후, **config-raspberrypi.json**에서 **device_password**를 **device_key_path** 속성으로 바꿉니다.
>
> 업데이트된 줄은 다음과 같이 표시되어야 합니다.
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

축하합니다. Pi의 첫 번째 샘플 응용 프로그램을 만들었습니다.

## <a name="deploy-and-run-the-sample-application"></a>샘플 응용 프로그램 배포 및 실행
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a>Pi에 Azure IoT Hub SDK를 설치합니다.
다음 명령을 실행하여 Azure Linux Hub SDK를 Pi에 설치합니다.

```bash
gulp install-tools
```

이 태스크를 처음 실행 시 완료하려면 몇 분의 시간이 소요될 수 있습니다.

### <a name="deploy-and-run-the-sample-app"></a>샘플 앱 배포 및 실행
다음 명령을 실행하여 샘플 응용 프로그램을 배포하고 실행합니다.

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>앱 작동 확인
샘플 응용 프로그램은 LED를 20번 깜박인 후 자동으로 종료됩니다. Led가 깜박이지 않으면 [문제 해결 가이드](iot-hub-raspberry-pi-kit-c-troubleshooting.md)에서 일반적인 문제에 대한솔루션을 참조하세요.
![LED 깜박임](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>요약
Pi 작동에 필요한 도구를 설치했으며 LED를 깜박이게 하는 샘플 응용 프로그램을 Pi에 배포했습니다. 이제 메시지 송수신을 위해 Azure IoT Hub에 Pi를 연결하는 다른 샘플 응용 프로그램을 만들고, 배포하고, 실행할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[Azure 도구 얻기](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

