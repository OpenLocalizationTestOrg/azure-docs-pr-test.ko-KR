---
title: "연결 라스베리 Pi (노드) tooAzure IoT-1 단원: 장치 구성 | Microsoft Docs"
description: "처음 사용 하기 위해 라스베리 Pi 3 구성 하 고 hello Raspbian OS, hello 라스베리 Pi 하드웨어에 최적화 된 무료 운영 체제를 설치 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "raspbian 다운로드, 설치 raspbian은 tooinstall raspbian raspbian 설치 라즈베리 pi 설치 raspbian 라즈베리 pi 설치 라즈베리 os pi sd 카드 라즈베리 설치 pi 연결 연결 tooraspberry pi 라즈베리 pi 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>장치 구성
## <a name="what-you-will-do"></a>수행할 사항
Pi를 처음 사용 하기 위해 구성 하 고 hello Raspbian 운영 체제를 설치 합니다. Raspbian는 가능한 운영 체제 hello 라스베리 Pi 하드웨어에 대해 최적화 된입니다. Hello에서 솔루션을 검색할 수 있는 문제가 있는 경우 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* 어떻게 tooinstall 원주율 Raspbian 합니다.
* 어떻게 USB 케이블을 사용 하 여 toopower Pi 합니다.
* 어떻게 tooconnect Pi toohello 이더넷 케이블 또는 무선 네트워크를 사용 하 여 네트워크입니다.
* Tooadd LED toohello breadboard 어떻게 tooPi 연결 합니다.

## <a name="what-you-will-need"></a>필요한 사항
toocomplete 라스베리 Pi 3 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.

* hello 라스베리 Pi 3 보드
* hello 16GB microSD 카드
* hello 6 피트 마이크로 USB 케이블 hello 5 v 2 amp 전원 공급 장치
* hello breadboard
* 커넥터 와이어
* 560옴 저항기
* 확산형 10mm LED
* hello 이더넷 케이블

![시작 키트의 항목](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

다음 항목도 필요합니다.

* 에 Pi tooconnect에 대 한 유선 또는 무선 연결 합니다.
* USB SD 어댑터 또는 miniSD 카드 tooburn hello에 운영 체제 이미지 hello microSD 카드입니다.
* Windows, Mac 또는 Linux를 실행하는 컴퓨터  hello 컴퓨터가 hello microSD 카드에 사용 되는 tooinstall Raspbian 있습니다.
* 인터넷 연결 toodownload 필요한 도구와 소프트웨어 hello 합니다.

## <a name="install-raspbian-on-hello-microsd-card"></a>Raspbian hello microSD 카드에 설치
Hello microSD 카드 hello Raspbian 이미지의 설치를 준비 합니다.

1. Raspbian을 다운로드합니다.
   1. [다운로드](https://www.raspberrypi.org/downloads/raspbian/) hello.zip 파일에 대 한 픽셀을 Raspbian 제시 합니다.
   2. Hello Raspbian 이미지 tooa 컴퓨터의 폴더에 추출 합니다.
2. Raspbian toohello microSD 카드를 설치 합니다.
   1. [다운로드](https://www.etcher.io) hello Etcher SD 카드 버너 유틸리티 하 여 설치 합니다.
   2. Etcher를 실행 하 고 1 단계에서 압축을 푼 hello Raspbian 이미지를 선택 합니다.
   3. Hello microSD 카드 드라이브를 선택 합니다.
      Etcher 선택 했을 수 이미 hello 올바른 드라이브 참고 합니다.
   4. 클릭 **플래시** tooinstall Raspbian toohello microSD 카드입니다.
   5. 설치가 완료 되 면 hello microSD 카드를 컴퓨터에서 제거 합니다.
      되므로 안전 tooremove hello microSD 카드 직접 Etcher를 꺼냅니다. 자동으로 또는 완료 되 면 hello microSD 카드 탑재 해제 합니다.
   6. Pi에 hello microSD 카드를 삽입 합니다.

![Hello SD 카드를 삽입 합니다.](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Pi 켜기
Pi hello 마이크로 USB 케이블 및 hello 전원 공급 장치를 사용 하 여 설정 합니다.

![켜기](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> 최소 hello 키트의 중요 한 toouse hello 전원 공급 장치는 프로그램 라스베리에 충분 한 전력 toowork 올바르게 있는지 2A toomake 합니다.

## <a name="enable-ssh"></a>SSH 사용
Hello 2016 년 11 월 릴리스를 기준으로 Raspbian 기본적으로 사용 하지 않도록 설정 하는 hello SSH 서버를 있습니다. Tooenable 필요한 것 수동으로 합니다. Toohello 참조할 수 있습니다 [공식 지침](https://www.raspberrypi.org/documentation/remote-access/ssh/) 하거나 모니터를 연결 하 고 이동 너무**기본 설정-> 라스베리 Pi 구성** tooenable SSH 합니다.

## <a name="connect-raspberry-pi-3-toohello-network"></a>라스베리 Pi 3 toohello 네트워크에 연결
Pi tooa 유선 네트워크 또는 tooa 무선 네트워크를 연결할 수 있습니다. Pi 사용자 컴퓨터와 동일한 네트워크 연결된 toohello 인지 확인 합니다. 예를 들어 컴퓨터에 연결 되어 있는지를 전환 동일한는 Pi toohello를 연결할 수 있습니다.

### <a name="connect-tooa-wired-network"></a>Tooa 유선 네트워크 연결
Hello 이더넷 케이블 tooconnect Pi tooyour 유선 네트워크를 사용 합니다. hello Pi에서 두 개의 Led 설정 hello 연결 합니다.

![이더넷 케이블을 사용하여 연결](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Tooa 무선 네트워크 연결
Hello에 따라 [지침](https://www.raspberrypi.org/learning/software-guide/wifi/) hello 라스베리 Pi Foundation tooconnect Pi tooyour 무선 네트워크에서 합니다. 이러한 지침을 사용 해야 하는 모니터 및 키보드 tooPi toofirst 연결 합니다.

## <a name="connect-hello-led-toopi"></a>Hello LED tooPi 연결
toocomplete이 작업을 사용 하 여 hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)및 LED, hello 저항기 hello 커넥터 와이어 hello 합니다. Toohello 연결 [범용 입/출력](https://www.raspberrypi.org/documentation/usage/gpio/) Pi의 포트 (GPIO).

![실험용 회로판, LED 및 저항기](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Hello 짧은 다리 hello LED의 너무 연결**GPIO GND (Pin 6)**합니다.
2. Hello hello 저항기의 LED tooone 레그의 긴 레그 hello를 연결 합니다.
3. 연결의 hello 저항기 다른 레그 너무 hello**GPIO 4 (Pin 7)**합니다.

Note는 hello LED 극성이 중요 합니다. 이 극성 설정은 일반적으로 활성(낮음)이라고 합니다.

![핀아웃](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

축하합니다. Pi 구성을 마쳤습니다.

## <a name="summary"></a>요약
이 문서에서 배운 Raspbian, Pi tooa 네트워크 연결을 설치 하 고 연결 하는 LED tooPi tooconfigure Pi 하는 방법입니다. Note 해당 hello LED가 켜 아직 하지 않습니다. hello 다음 작업은 tooinstall hello 필요한 도구 및 Pi에서 샘플 응용 프로그램을 실행 하는 준비 과정에서 소프트웨어.

![하드웨어는 준비되었습니다.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>다음 단계
[Hello 도구 가져오기](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

