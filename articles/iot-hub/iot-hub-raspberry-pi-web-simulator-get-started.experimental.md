---
title: "aaaSimulated 라스베리 Pi toocloud (Node.js)-라스베리 Pi 연결 웹 시뮬레이터 tooAzure IoT 허브 | Microsoft Docs"
description: "Azure 클라우드 라스베리 Pi toosend 데이터 toohello에 대 한 라스베리 Pi 웹 시뮬레이터 tooAzure IoT 허브를 연결 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "라즈베리 pi 시뮬레이터, azure iot 라즈베리 pi 라즈베리 pi iot 허브 라즈베리 pi toocloud 라즈베리 pi toocloud 데이터 보내기"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>라스베리 Pi 온라인 시뮬레이터 tooAzure IoT Hub (Node.js) 연결

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

이 자습서에서는 먼저 온라인 시뮬레이터 라스베리 Pi와 작업의 hello 기본 사항을 학습 합니다. 그런 다음 배웁니다 tooseamlessly hello Pi 시뮬레이터 toohello 클라우드를 사용 하 여 연결 하는 방법을 [Azure IoT Hub](iot-hub-what-is-iot-hub.md)합니다. 

물리적 장치를 설정한 경우 방문 [라스베리 Pi 연결 tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget 시작 합니다. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>수행할 작업

* 온라인 시뮬레이터 라스베리 Pi의 hello 기본 사항에 알아봅니다.
* IoT Hub를 만듭니다.
* IoT Hub에 Pi용 장치를 등록합니다.
* Pi 시뮬레이션 toosend 센서 데이터 tooyour IoT 허브에서 샘플 응용 프로그램을 실행 합니다.

만들면 시뮬레이션된 라스베리 Pi tooan IoT 허브를 연결 합니다. 그런 다음 hello 시뮬레이터 toogenerate 센서 데이터로 샘플 응용 프로그램을 실행 합니다. 마지막으로 hello 센서 데이터 tooyour IoT 허브를 보냅니다.

## <a name="what-you-learn"></a>학습 내용

* 어떻게 toocreate Azure IoT hub 가져오고, 새로운 장치 연결 문자열입니다. Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
* 어떻게 라스베리 Pi 온라인 시뮬레이터와 toowork 합니다.
* 어떻게 toosend 센서 데이터 tooyour IoT 허브입니다.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Raspberry Pi 웹 시뮬레이터 개요

Hello 단추 toolaunch 라스베리 Pi 온라인 시뮬레이터를 클릭 합니다.

> [!div class="button"]
[Raspberry Pi 시뮬레이터 시작](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Hello 웹 시뮬레이터에 있는 세 가지 영역이 있습니다.
* 어셈블리-hello 기본 회로 영역은 Pi BME280 센서 및 LED와 연결 되도록 합니다. 미리 보기 버전에서 hello 영역 잠겨 있으므로 현재 사용자 지정을 수행할 수 없습니다.
* 영역-라스베리 Pi와 함께 toocode에 대 한 온라인 코드 편집기를 코딩 합니다. hello 기본 샘플 응용 프로그램 BME280 센서에서 toocollect 센서 데이터를 사용 하면 고 tooyour Azure IoT Hub를 보냅니다. hello 응용 프로그램은 실제 Pi 장치 완벽 하 게 호환 됩니다. 
* 통합된 콘솔 창-코드의 hello 출력을 표시합니다. 이 창의 hello 위쪽에 세 개의 단추가 있습니다.
   * **실행** -hello 영역 코딩에서 hello 응용 프로그램을 실행 합니다.
   * **다시 설정** -재설정 hello 영역 toohello 기본 샘플 응용 프로그램을 코딩 합니다.
   * **접기/확장** -hello toofold 확장/있습니다 hello 콘솔 창에 대 한 쪽에 있는 단추 오른쪽에 있습니다.

> [!NOTE] 
hello 라스베리 Pi 웹 시뮬레이터 미리 보기 버전에서 제공 되었습니다. Toohear 같은 hello에 음성을 [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator)합니다. hello 소스 코드는 public으로 [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator)합니다.

![Pi 온라인 시뮬레이터 개요](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Pi 웹 시뮬레이터에서 샘플 응용 프로그램 실행

1. 영역을 코딩에서 hello 기본 샘플 응용 프로그램에서 작업 하는 있는지를 확인 합니다. Azure IoT 허브 장치 연결 문자열 hello 줄 15의 hello 자리 표시자를 바꿉니다.
   ![Hello 장치 연결 문자열을 바꾸기](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. 클릭 **실행** 또는 형식 `npm start` toorun hello 응용 프로그램입니다.


다음 hello hello 센서 데이터와 tooyour IoT 허브 전송 되는 hello 메시지를 표시 하는 출력 표시 되어야 ![출력-라스베리 Pi tooyour IoT 허브에서 보낸 센서 데이터](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>다음 단계

샘플 응용 프로그램 toocollect 센서 데이터를 실행 하 고이 정보를 tooyour IoT 허브를 보냅니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
