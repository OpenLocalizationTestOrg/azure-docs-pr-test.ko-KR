---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 3: 메시지 읽기 | Microsoft Docs"
description: "IoT 허브에서 호스트 컴퓨터 tooread hello 메시지에 예제 코드를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 데이터 수집, iot 클라우드 서비스, iot 데이터의 데이터"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>IoT Hub에서 메시지 읽기

## <a name="what-you-will-do"></a>수행할 사항

- 샘플에서 코드를 실행할 호스트 컴퓨터 tooread 메시지 IoT 허브에서 합니다.

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

어떻게 toouse hello gulp IoT 허브에서 도구 tooread 메시지입니다.

## <a name="what-you-need"></a>필요한 항목

- hello 시뮬레이션 된 장치 샘플에서 [구성 및 실행 하는 시뮬레이션 된 장치 클라우드 샘플 응용 프로그램 업로드](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)합니다.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IoT Hub 및 장치 연결 문자열 가져오기

hello 장치 연결 문자열은 시뮬레이션 된 장치 tooconnect tooyour IoT 허브에서 사용 됩니다. IoT 허브 연결 문자열 hello tooconnect tooyour IoT 허브는 사용할 수 있는 IoT 허브 toomanage hello 장치에 사용 되는 tooconnect toohello id 레지스트리에입니다.

- Hello 다음 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   사용 하 여 `iot-gateway` 의 hello 값으로 `{resource group name}` 변경 하지 않은 경우.
- Hello 다음 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`2 단원에서에서 지정한 hello 이름이입니다.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Hello 샘플 코드에 대 한 hello 장치 연결을 구성 합니다.

IoT 허브와 장치 연결 구성을 업데이트 `config-azure.json` hello 다음 단계를 수행 하 여:

1. 열기 `config-azure.json` hello 다음 콘솔 창에서 명령을 실행 하 여 Visual Studio Code에서:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Hello 바꾸기 작업을 수행 하는 hello 확인 `config-azure.json` 파일:

   ![config azure의 스크린 샷](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   대체 `[IoT hub connection string]` IoT 허브 연결 문자열 hello로 합니다.

## <a name="read-messages-from-your-iot-hub"></a>IoT Hub에서 메시지 읽기

Hello 시뮬레이션 된 장치에 대 한 샘플 응용 프로그램을 실행 하 고 다음 명령을 hello에서 IoT Hub 메시지를 읽을:

```bash
gulp run --iot-hub
```

hello 명령은 메시지 tooyour IoT hub 2 초 마다 전송 하는 hello 응용 프로그램을 실행 합니다. 또한 자식 프로세스 tooreceive hello 메시지를 생성합니다.

hello 메시지를 보내는 지 모든에 즉시 표시 hello 같은 콘솔 창에는 수신 호스트 컴퓨터를 hello 합니다. hello 응용 프로그램에 40 초 후에 종료 됩니다.

![보낸 메시지와 수신한 메시지가 있는 시뮬레이트된 샘플 응용 프로그램](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>요약

성공적으로 시뮬레이션 된 장치와 hello 샘플 응용 프로그램 toosend 데이터 tooyour IoT 허브를 실행 했습니다. IoT hub tooyour 보낸 hello 메시지 읽은 수 있습니다.

## <a name="next-steps"></a>다음 단계
[Azure 함수 앱 및 Azure Storage 계정 만들기](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


