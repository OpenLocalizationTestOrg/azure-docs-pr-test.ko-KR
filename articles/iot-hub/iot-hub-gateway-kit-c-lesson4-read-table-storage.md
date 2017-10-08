---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 4: 테이블 저장소 | Microsoft Docs"
description: "Intel NUC tooyour IoT 허브에서 메시지를 저장 하 고 tooAzure 테이블 저장소에 쓰는 hello 클라우드에서 읽어 주시기 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드에서 데이터 검색, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Azure Table Storage에 유지되는 메시지 읽기

## <a name="what-you-will-do"></a>수행할 사항

- 보내는 메시지 tooyour IoT hub 게이트웨이에 hello 게이트웨이 샘플 응용 프로그램을 실행 합니다.
- 그런 다음 Azure 테이블 저장소에 호스트 컴퓨터 tooread hello 메시지에 예제 코드를 실행 합니다. 

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

어떻게 toouse hello gulp Azure 테이블 저장소 도구 toorun hello 샘플 코드 tooread 메시지입니다.

## <a name="what-you-need"></a>필요한 항목

성공적으로 포함 해야 다음 작업 hello 수행:

- [Hello Azure 함수 앱 및 hello Azure 저장소 계정을 만든](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)합니다.
- [Hello 게이트웨이 샘플 응용 프로그램 실행](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)합니다.
- [IoT Hub에서 메시지 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="get-your-azure-storage-connection-strings"></a>Azure Storage 연결 문자열 가져오기

이 단원의 초반부에 Azure Storage 계정을 성공적으로 만들었습니다. 실행할 명령을 수행 하는 hello hello Azure 저장소 계정의 tooget hello 연결 문자열:

* 모든 저장소 계정을 나열합니다.

```bash
az storage account list -g iot-gateway --query [].name
```

* Azure Storage 연결 문자열을 가져옵니다.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Iot 게이트웨이 사용 하 여의 hello 값으로 `{resource group name}` hello 값 2 단원에서에서 변경 되지 않은 경우.

## <a name="configure-hello-device-connection"></a>Hello 장치 연결 구성

업데이트 hello `config-azure.json` hello 호스트 컴퓨터에서 실행 되는 hello 샘플 코드는 Azure 테이블 저장소에 메시지를 읽을 수 있도록 파일입니다. tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.

1. 장치 구성 파일 열기 hello `config-azure.json` hello 다음 명령을 실행 하 여:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![구성](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. 대체 `[Azure storage connection string]` 가져온 Azure 저장소 연결 문자열 hello로 합니다.

   `[IoT hub connection string]`은 3단원의 [Azure IoT Hub에서 메시기 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) 섹션에서 이미 바꿨어야 합니다.

## <a name="read-messages-in-your-azure-table-storage"></a>Azure Table Storage에서 메시지 읽기

Hello 게이트웨이 샘플 응용 프로그램을 실행 하 고 다음 명령을 hello 하 여 Azure 테이블 저장소 메시지 읽기:

```bash
gulp run --table-storage
```

IoT hub 새 메시지가 도착 하는 경우 Azure 테이블 저장소에 Azure 함수 응용 프로그램 toosave 메시지를 트리거합니다.
hello `gulp run` 명령은 메시지 tooyour IoT 허브에서 전송 하는 게이트웨이 샘플 응용 프로그램을 실행 합니다. 와 `table-storage` 매개 변수에 생성 Azure 테이블 저장소에 메시지를 저장 하는 자식 프로세스 tooreceive hello 합니다.

hello 메시지를 보내는 지 모든에 즉시 표시 hello 같은 콘솔 창에는 수신 호스트 컴퓨터를 hello 합니다. hello 예제 응용 프로그램 인스턴스는 40 초 후에 자동으로 종료 됩니다.

   ![gulp 읽기](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>요약

Azure 함수 응용 프로그램에서 저장 된 Azure 테이블 저장소에 hello 샘플 코드 tooread hello 메시지를 실행 했습니다.
