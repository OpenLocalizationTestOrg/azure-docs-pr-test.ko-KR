---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 1: NUC 설정 | Microsoft Docs"
description: "센서와 Azure IoT Hub toocollect 센서 정보 사이의 IoT 게이트웨이로 Intel NUC toowork를 설정 하 고 tooIoT 허브 전송 됩니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "iot 게이트웨이, intel nuc, nuc 컴퓨터, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Intel NUC를 IoT 게이트웨이로 설정

## <a name="what-you-will-do"></a>수행할 사항

- Intel NUC를 IoT 게이트웨이로 설정합니다.
- Intel NUC에 hello Azure IoT 가장자리 패키지를 설치 합니다.
- Intel NUC tooverify hello 게이트웨이 기능에는 "hello_world" 예제 응용 프로그램을 실행 합니다.
문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

이 단원에서는 다음 내용을 배웁니다.

- 어떻게 tooconnect Intel NUC 주변 장치를 합니다.
- 어떻게 사용 하 여 Intel NUC tooinstall 및 업데이트 hello 필요한 패키지가 hello 스마트 패키지 관리자.
- 어떻게 toorun hello_world"hello" 예제 응용 프로그램 tooverify hello 게이트웨이 기능 합니다.

## <a name="what-you-need"></a>필요한 항목

- Intel IoT 게이트웨이 소프트웨어 제품군 hello로 Intel NUC 키트 DE3815TYKE (바람 강 Linux * 7.0.0.13) 사전 설치 합니다.
- 이더넷 케이블
- 키보드
- HDMI 또는 VGA 케이블
- HDMI 또는 VGA 포트가 있는 모니터

![게이트웨이 키트](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC hello 주변 장치를 사용 하 여 연결

아래 hello 이미지는 다양 한 주변 장치에 연결 하는 Intel NUC의 예:

1. 연결 된 tooa 키보드입니다.
2. Toohello 모니터 vga 또는 HDMI 케이블을 연결합니다.
3. 연결 된 tooa 유선 이더넷 케이블을 통해 네트워크입니다.
4. 연결 된 toohello 전원 공급 장치 전원 케이블을 사용 합니다.

![Intel NUC tooperipherals 연결](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>호스트 컴퓨터를 통해 SSH (보안 셸)에서 toohello Intel NUC 시스템에 연결

여기 NUC 장치의 키보드 및 모니터 tooget hello IP 주소가 필요합니다. Hello IP를 이미 알고 있는 경우 주소를이 섹션의 3 toostep를 건너뛸 수 있습니다.

1. Intel NUC hello 시스템에서 전원 단추 hello 및 로그를 키를 누르면으로 설정 됩니다.

   hello 기본 사용자 이름과 암호는 모두 `root`합니다.

2. Hello를 실행 하 여 NUC의 hello IP 주소를 가져올 `ifconfig` 명령입니다. 이 단계는 hello NUC 장치에서 수행 됩니다.

   Hello 명령 출력의 예를 들면 다음과 같습니다.

   ![NUC IP를 보여주는 ifconfig 출력](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   이 예제에서는 값 뒤에 오는 hello `inet addr:` 호스트 컴퓨터 tooIntel NUC에서 원격으로 tooconnect를 계획할 때 필요한 hello IP 주소입니다.

3. Hello 호스트 컴퓨터 tooconnect tooIntel NUC에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.

   - Windows용 [PuTTY](http://www.putty.org/)
   - hello에 SSH 클라이언트 Ubuntu 또는 macOS입니다.

   호스트 컴퓨터와에서 Intel NUC에 더 효율적이 고 생산적인 toooperate 것합니다. Hello hello IP 주소, 사용자 이름 및 암호를 필요한 SSH 클라이언트를 통해 tooconnect hello NUC 합니다. MacOS에 hello 예제 사용 하 여 SSH 클라이언트가입니다.
   ![MacOS에서 실행되는 SSH 클라이언트](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Hello Azure IoT 가장자리 패키지 설치

hello Azure IoT 가장자리 패키지 hello SDK의 hello 미리 컴파일된 이진 파일 및 해당 종속성을 포함합니다. 이러한 이진 파일은 Azure IoT 가장자리, Azure IoT SDK hello 및 hello 해당 도구입니다. 또한 hello 패키지 hello 게이트웨이 기능을 사용 하는 toovalidate "hello_world" 샘플 응용 프로그램을 포함 합니다. IoT 가장자리가 hello 게이트웨이의 hello 핵심 부분입니다. tooinstall hello 패키지에서 다음이 단계를 수행 합니다.

1. Hello 명령을 터미널 창에서 다음을 실행 하 여 hello IoT 클라우드 저장소를 추가 합니다.

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   hello `rpm` imports hello rpm 키 명령입니다. hello `smart channel` 명령은 hello rpm 채널 toohello 스마트 패키지 관리자를 추가 합니다. Hello를 실행 하기 전에 `smart update` 같은 출력이 표시 명령을 아래 합니다.

   ![rpm 및 스마트 채널 명령 출력](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Hello 다음 명령을 실행 하 여 hello 패키지를 설치 합니다.

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`hello hello 패키지 이름이입니다. hello `smart install` 명령에 사용 되는 tooinstall hello 패키지입니다.

   Hello 패키지를 설치한 후 Intel NUC 예상된 toowork 게이트웨이로 됩니다.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Hello Azure IoT 가장자리 "hello_world" 샘플 응용 프로그램 실행

너무 이동`azureiotgatewaysdk/samples` hello 샘플 "hello_world" 샘플 응용 프로그램을 실행 합니다. 이 샘플 응용 프로그램에서 hello 한 게이트웨이 만듭니다 `hello_world.json` 파일을 5 초 마다 hello hello Azure IoT 가장자리 아키텍처 toolog hello world 메시지 tooa 파일의 기본 구성 요소를 사용 합니다.

Hello 다음 명령을 실행 하 여 hello 샘플 "hello_world" 샘플 응용 프로그램을 실행할 수 있습니다.

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

샘플 응용 프로그램 hello hello 다음과 같이 hello 게이트웨이 기능이 제대로 작동 하는 경우 출력을 생성 합니다.

![응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.

## <a name="summary"></a>요약

축하합니다. 게이트웨이로 Intel NUC 설정을 완료했습니다. 준비가 이제 toomove 호스트 컴퓨터를 다음 단원에서는 tooset toohello에 Azure IoT hub를 만들고 Azure IoT 허브 논리적 장치를 등록 합니다.

## <a name="next-steps"></a>다음 단계
[호스트 컴퓨터 및 Azure IoT Hub 준비](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
