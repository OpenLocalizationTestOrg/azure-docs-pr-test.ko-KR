---
title: "Connect Arduino (C) tooAzure IoT-1 단원: 장치 구성 | Microsoft Docs"
description: "처음 사용 시 Adafruit Feather M0 WiFi를 구성합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "설정, arduino arduino toopc, 설치 arduino, arduino 보드 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>장치 구성
## <a name="what-you-will-do"></a>수행할 사항
처음 사용 하기 위해 Adafruit 페더 M0 WiFi Arduino 보드를 구동 하는 hello 보드 어셈블하는 방법으로 구성 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)합니다.

## <a name="what-you-need"></a>필요한 항목
toocomplete hello Adafruit 페더 M0 WiFi 시작 키트에 대 한 부분을 다음 해야이 작업의 경우:

* hello Adafruit 페더 M0 WiFi 보드
* 마이크로 B tooType A USB 케이블

![키트][kit]

다음 항목도 필요합니다.

* Windows, Mac 또는 Linux를 실행하는 컴퓨터 
* Arduino 보드 tooconnect 프로그램에 대 한 무선 연결 합니다.
* 인터넷 연결 toodownload 구성 도구입니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* 어떻게 tooassemble Arduino 보드 및 전원 것 다음 hello에 대해 학습 합니다.
* 어떻게 ubuntu tooadd 직렬 포트 사용 권한.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Arduino 보드 tooyour 컴퓨터 연결

1. Hello 상위 마이크로 USB 포트에 hello 마이크로 USB 케이블을 연결 합니다.

   ![위쪽 마이크로 USB 포트][top-micro-usb-port]

2. 플러그를 컴퓨터에 USB 케이블의 다른 쪽 끝을 hello 합니다.

   ![컴퓨터 USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Ubuntu에서 직렬 포트 권한 추가

Windows 또는 macOS를 사용하는 경우 이 섹션을 건너뛸 수 있습니다. Ubuntu, hello hello 일반 linux 사용자에 게 Arduino 보드의 hello USB 포트에 사용 권한을 toooperate hello 있는지 단계 toomake 다음이 필요 합니다.

1. 이제 터미널에서 일반 사용자로 다음을 수행합니다.

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   다음과 비슷한 결과가 표시됩니다.

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   다른 숫자를 "0" hello 없거나 항목이 여러 개 반환 될 수 있습니다. 필요한 hello 첫 번째 사례 hello 데이터는 `uucp`, 둘째는 hello에 `dialout`, hello 파일의 hello 그룹 소유자 인 합니다.

2. 사용자 toohello toohello 그룹을 추가 합니다.

   ```bash
   sudo usermod -a -G group-name username
   ```

   여기서 `group-name` 는 hello 첫 번째 단계에서 찾은 hello 데이터 및 `username` 은 linux 사용자 이름입니다.

3. 이 변경 tootake 효과 및 전체 hello 설정에 대 한 다시 toolog에 및를 해야 합니다.

## <a name="summary"></a>요약
이 문서에서 배운 어떻게 tooconfigure Arduino 보드 합니다. hello 다음 작업은 tooinstall hello 필요한 도구 및 Arduino 보드에는 예제 응용 프로그램을 실행 하기 위한 준비 과정에서 소프트웨어.

![하드웨어는 준비되었습니다.][hardware-is-ready]

## <a name="next-steps"></a>다음 단계
[Hello 도구 가져오기][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md