---
title: "연결 Intel Edison (노드) tooAzure IoT-3 단원: 메시지를 보낼 | Microsoft Docs"
description: "배포 하 여 샘플 응용 프로그램 tooIntel Edison tooyour IoT hub 메시지를 보내고 hello led가 깜박이를 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 클라우드 서비스 arduino toocloud 데이터 보내기"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>샘플 응용 프로그램 toosend 장치-클라우드 메시지 실행
## <a name="what-you-will-do"></a>수행할 사항
Toodeploy 및 전송 하는 Intel Edison에서 실행을 예제 응용 프로그램 메시지 tooyour IoT hub 방법을 표시이 문서 됩니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
Toouse hello 도구 toodeploy gulp 하는 방법에 대해 알아봅니다 쿼리하고 Edison에 hello 샘플 C 응용 프로그램을 실행 합니다.

## <a name="what-you-need"></a>필요한 항목
* 이 작업을 시작 하기 전에 성공적으로 완료 해야 [메시지 Azure 함수 응용 프로그램 및 저장소 계정 tooprocess와 저장소 IoT 허브를 만들][process-and-store-iot-hub-messages]합니다.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IoT Hub 및 장치 연결 문자열 가져오기
hello 장치 연결 문자열은 사용한 tooconnect Edison tooyour IoT 허브입니다. hello IoT 허브 연결 문자열은 사용한 tooconnect Edison hello IoT 허브를 표시 하 여 IoT 허브 toohello 장치 id입니다.

* Hello 다음 Azure CLI 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.

```bash
az iot hub list -g iot-sample --query [].name
```

사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.

* Hello 다음 Azure CLI 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`IoT hub를 생성 하 고 Edison 등록 지정한 hello 이름이입니다.

* Hello 다음 명령을 실행 하 여 hello 장치 연결 문자열을 가져옵니다.

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

사용 하 여 `myinteledison` 의 hello 값으로 `{device id}` hello 값을 변경 되지 않은 경우.

## <a name="configure-hello-device-connection"></a>Hello 장치 연결 구성
1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.

   ```bash
   npm install
   gulp init
   ```

2. 장치 구성 파일 열기 hello `config-edison.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. Hello 바꾸기 작업을 수행 하는 hello 확인 `config-edison.json` 파일:

   * 대체 **[장치 호스트 이름 또는 IP 주소]** hello 장치 IP 주소 장치를 구성 했을 때를 표시 합니다.
   * 대체 **[IoT 장치 연결 문자열]** hello로 `device connection string` 얻을 수 있습니다.
   * 대체 **[IoT 허브 연결 문자열]** hello로 `iot hub connection string` 얻을 수 있습니다.

   > [!NOTE]
   > 이 문서에서는 `azure_storage_connection_string`이 필요하지 않습니다. 그대로 유지합니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 및 실행 hello 샘플 응용 프로그램 Edison hello 다음 명령을 실행 하 여:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Hello 샘플 응용 프로그램이 작동 하는지 확인 하십시오.
연결 된 tooEdison 2 초 마다 깜박입니다.이 hello LED 표시 되어야 합니다. Hello led가 깜박입니다 때마다 hello 샘플 응용 프로그램 메시지 tooyour IoT hub를 보내고 해당 hello 메시지에 전송 되었습니다. IoT hub tooyour 확인 합니다. 또한 hello IoT hub에서 수신 된 각 메시지는 hello 콘솔 창에 인쇄 됩니다. 샘플 응용 프로그램 hello 20 개의 메시지를 보낸 후 자동으로 종료 합니다.

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>요약
배포 되었으며 toosend 장치-클라우드 메시지 tooyour IoT 허브에서 Edison hello 새 깜박임 샘플 응용 프로그램을 실행 합니다. 이제 toohello 저장소 계정에 작성 된 것 처럼 메시지를 모니터링 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Storage에 유지되는 메시지 읽기][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md