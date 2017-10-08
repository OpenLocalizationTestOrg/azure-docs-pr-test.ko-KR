---
title: "iothub 탐색기와 메시징 aaaManage Azure IoT Hub 클라우드 장치 | Microsoft Docs"
description: "Toouse iothub 탐색기 CLI 도구 toomonitor 장치 toocloud (D2C) 메시지 hello 및 Azure IoT Hub에서 클라우드 toodevice (C2D) 메시지를 보낼 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iothub 탐색기, 메시징, 클라우드 장치 iot 허브 클라우드 toodevice 클라우드 toodevice 메시징"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Iothub 탐색기 toosend를 사용 하 고 사용자의 장치 및 IoT Hub 간에 메시지 송수신

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer)에는 IoT Hub를 더 쉽게 관리할 수 있는 몇 가지 명령이 있습니다. 이 자습서는 방법에 대해 toouse iothub 탐색기 toosend 및 IoT 허브와 장치 간에 메시지를 수신 합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

배웁니다 어떻게 toouse iothub 탐색기 toomonitor 장치-클라우드 메시지와 toosend 클라우드-장치 메시지입니다. 장치-클라우드 메시지에는 장치를 수집 하 고 다음 tooyour IoT 허브를 보냅니다 센서 데이터가 될 수 있습니다. 클라우드-장치 메시지 명령을 IoT hub 보내는 연결 된 tooyour 장치가 LED tooyour 장치 tooblink는 될 수 있습니다.

## <a name="what-you-will-do"></a>수행할 사항

- Iothub 탐색기 toomonitor 장치-클라우드 메시지를 사용 합니다.
- Iothub 탐색기 toosend 클라우드-장치 메시지를 사용 합니다.

## <a name="what-you-need"></a>필요한 항목

- 자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.
  - 활성 Azure 구독.
  - 구독 중인 Azure IoT Hub
  - 메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.
- iothub-explorer ([Install iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>장치-클라우드 메시지 모니터링

toomonitor 전송 된 메시지를 장치 tooyour IoT 허브에서 다음이 단계를 따르십시오.

1. 콘솔 창을 엽니다.
1. Hello 다음 명령을 실행 합니다.

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > IoT Hub에서 `<device-id>`과 `<IoTHubConnectionString>`을 가져옵니다. 확인 hello 이전 자습서 작업을 완료 했습니다. Toouse 시도할 수 있습니다 또는 `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` 있으면 `HostName`, `SharedAccessKeyName` 및 `SharedAccessKey`합니다.

## <a name="send-cloud-to-device-messages"></a>클라우드-장치 메시지 보내기

toosend 메시지가 IoT hub tooyour 장치에서 다음이 단계를 따르십시오.

1. 콘솔 창을 엽니다.
1. Hello 다음 명령을 실행 하 여 IoT 허브에서 세션을 시작 합니다.

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Hello 다음 명령을 실행 하 여 메시지 tooyour 장치 보내기:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

hello 명령 하는 연결 된 tooyour 장치 고 hello 메시지 tooyour 장치 전송 hello led가 깜박입니다.

> [!Note]
> Hello 메시지를 받을 때 별도 ack 명령 백 tooyour IoT 허브는 hello 장치 toosend 필요가 없습니다.

## <a name="next-steps"></a>다음 단계

Toomonitor 장치-클라우드 메시지 하 고 IoT 장치와 Azure IoT Hub 간의 클라우드-장치 메시지를 송신 하는 방법을 배웠습니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
