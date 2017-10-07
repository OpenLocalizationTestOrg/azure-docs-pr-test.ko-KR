---
featureFlags: usabilla
title: "연결 라스베리 Pi (노드) tooAzure IoT-3 단원: 테이블 저장소 | Microsoft Docs"
description: "Tooyour Azure 테이블 저장소에 작성 된 것 처럼 hello 장치-클라우드 메시지를 모니터링 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "클라우드에서 데이터 검색, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3c2c8086d3561b7603e18ed00492fcaa0593b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Azure Storage에 유지되는 메시지 읽기
## <a name="what-you-will-do"></a>수행할 사항
Hello 메시지로 라스베리 Pi 3 tooyour IoT 허브에서 보낸 모니터 hello 장치-클라우드 메시지 tooyour Azure 테이블 저장소에 기록 됩니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 Azure 테이블 저장소에 toouse hello gulp 메시지 읽기 작업 tooread 메시지 유지 하는 방법을 배웁니다.

## <a name="what-you-need"></a>필요한 항목
이 프로세스를 시작 하기 전에 성공적으로 완료 해야 [라스베리 Pi 3에서 hello Azure 깜박임 샘플 응용 프로그램을 실행](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)합니다.

## <a name="read-new-messages-from-your-storage-account"></a>저장소 계정에서 새 메시지 읽어오기
Hello 이전 문서 원주율 샘플 응용 프로그램을 실행 합니다. hello 샘플 응용 프로그램 메시지 tooyour Azure IoT 허브를 전송 합니다. tooyour IoT hub를 전송 하는 hello 메시지 hello Azure 함수 앱을 통해 Azure 테이블 저장소에 저장 됩니다. Azure 테이블 저장소에서 hello Azure 저장소 연결 문자열 tooread 메시지 해야합니다.

Azure 테이블 저장소에 저장 된 tooread 메시지는 다음이 단계를 따르십시오.

1. Hello 다음 명령을 실행 하 여 hello 연결 문자열을 가져옵니다.

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   hello 첫 번째 명령은 검색 hello `storage name` hello 두 번째 명령은 tooget hello 연결 문자열에 사용 되는 합니다. 사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.
2. 구성 파일 열기 hello `config-raspberrypi.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. 대체 `[Azure storage connection string]` 1 단계에서 가져온 hello 연결 문자열을 사용 합니다.
4. Hello 저장 `config-raspberrypi.json` 파일입니다.
5. 메시지를 다시 보내고 hello 다음 명령을 실행 하 여 Azure 테이블 저장소에서 읽기:
   
   ```bash
   gulp run --read-storage
   ```
   
   hello Azure 테이블 저장소에서 읽기에 대 한 논리는 hello `azure-table.js` 파일입니다.
   
    ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a>요약
성공적으로 hello 클라우드에서 Pi tooyour IoT 허브를 연결 하 고 hello 깜박임 샘플 응용 프로그램 toosend 장치-클라우드 메시지를 사용 했습니다. 또한 hello Azure 함수 앱 toostore 들어오는 IoT 허브 메시지 tooyour Azure 테이블 저장소를 사용 합니다. 이제 IoT 허브 tooPi에서 클라우드-장치 메시지를 보낼 수 있습니다.

## <a name="next-steps"></a>다음 단계
[Hello 샘플 응용 프로그램 tooreceive 클라우드-장치 메시지를 실행 합니다.](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

