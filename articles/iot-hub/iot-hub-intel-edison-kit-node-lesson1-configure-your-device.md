---
title: "Intel Edison (노드) tooAzure IoT-1과 연결: 장치 구성 | Microsoft Docs"
description: "처음 사용을 위한 Intel Edison을 구성합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "설정, arduino arduino toopc, 설치 arduino, arduino 보드 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Intel Edison 구성
## <a name="what-you-will-do"></a>수행할 사항
Hello 보드, 위로 전원을 어셈블하는 방법으로 처음에 대 한 Intel Edison를 구성 하 고 구성 도구 tooyour 데스크톱 OS tooflash 설치 Edison의 펌웨어 해당 암호를 설정 하 고 연결 tooWi-Fi. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.

* Tooassemble Edison 보드 어떻게을 켭니다.
* Tooflash Edison 펌웨어 암호를 설정 하 고 Wi-fi 연결 방법

## <a name="what-you-need"></a>필요한 항목
toocomplete Intel Edison 시작 키트에서 파트를 수행 하는 hello 해야이 작업을이 수행 합니다.

* Intel® Edison 모듈
* Arduino 확장 보드
* 모든 공백 막대 또는 나사 hello 패키징, 나사 두 toofasten hello 모듈 toohello 확장 보드 등의 나사와 플라스틱 스페이서 4 집합에에서 포함 합니다.
* 마이크로 B tooType A USB 케이블
* DC(직류) 전원 공급 장치 전원 공급 장치 정격은 다음과 같아야 합니다.
  - 7-15V DC
  - 1500mA 이상
  - hello 센터/내부 pin hello 양수 극의 hello 전원 공급 장치가 있어야 합니다.

  ![시작 키트의 항목](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

다음 항목도 필요합니다.

* Windows, Mac 또는 Linux를 실행하는 컴퓨터 
* Edison tooconnect에 대 한 무선 연결 합니다.
* 인터넷 연결 toodownload 구성 도구입니다.

## <a name="assemble-your-board"></a>보드 조립

이 섹션 단계 tooattach Intel® Edison 모듈 tooyour 확장 보드를 포함합니다.

1. Hello 확장 보드에 hello 나사 hello 모듈에 hello 허점 만나려고 프로그램 확장 보드에 흰색 hello 개요 내의 hello Intel® Edison 모듈을 배치 합니다.

2. Hello 단어 바로 아래 hello 모듈을 누르면 `What will you make?` 간단히 생각 될 때까지 합니다.

   ![보드 2 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Hello 두 (hello 패키지에 포함 됨) 하는 16 진수 너트 toosecure hello 모듈 toohello 확장 보드를 사용 합니다.

   ![보드 3 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Hello 확장 보드에 네 개의 모퉁이 구멍 hello 중 하나에 나사를 삽입 합니다. 비틀 및 hello 나사에 흰색 hello 플라스틱 스페이서 중 하나를 강화 합니다.

   ![보드 4 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. 반복에 대 한 다른 3 개의 모퉁이 스페이서 hello 합니다.

   ![보드 5 조립](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

이제 보드가 조립됩니다.

   ![조립된 보드](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Edison 전원 켜기

1. Hello 전원 공급 장치에 연결 합니다.

   ![전원 공급 장치 꽂기](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. (DS1 hello Arduino * 확장 보드에 표시) 녹색 led가 켜지 고 켜져 해야 합니다.

3. Hello 보드 toofinish 부팅에 대 일 분 기다립니다.

   > [!NOTE]
   > DC 전원 공급 장치가 하면 전원 hello 보드 USB 포트를 통해 계속 됩니다. 자세한 내용은 `Connect Edison tooyour computer` 섹션을 참조하세요. 이러한 방식으로 보드를 켜면 보드에서 예기치 않은 동작이 나타날 수 있습니다. 이러한 현상은 Wi-Fi 또는 구동 모터를 사용할 때 더욱 두드러집니다.

## <a name="connect-edison-tooyour-computer"></a>Edison tooyour 컴퓨터 연결

1. Edison 장치 모드는 hello 두 마이크로 USB 포트에 대 한 hello 마이크로 스위치를 설정/해제 합니다. 장치 모드와 호스트 모드 간 차이점에 대해서는 [여기](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)를 참조하세요.

   ![Hello 마이크로 스위치를 설정/해제](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Hello 상위 마이크로 USB 포트에 hello 마이크로 USB 케이블을 연결 합니다.

   ![위쪽 마이크로 USB 포트](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. 플러그를 컴퓨터에 USB 케이블의 다른 쪽 끝을 hello 합니다.

   ![컴퓨터 USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

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

축하합니다. Edison 구성을 마쳤습니다.

## <a name="summary"></a>요약
이 문서에서는 tooassemble를 Edison 보드 hello, 해당 펌웨어, 설정 암호 플래시 및 구성 도구를 사용 하 여 tooWi-Fi 연결 방법을 배웠습니다. Note 해당 hello LED가 켜 아직 하지 않습니다. hello 다음 작업은 tooinstall hello 필요한 도구 및 Edison에서 샘플 응용 프로그램을 실행 하는 준비 과정에서 소프트웨어.

## <a name="next-steps"></a>다음 단계
[Hello 도구 가져오기][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md