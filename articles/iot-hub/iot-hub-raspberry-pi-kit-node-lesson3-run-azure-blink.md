---
title: "연결 라스베리 Pi (노드) tooAzure IoT-3 단원: 샘플을 실행 | Microsoft Docs"
description: "배포 하 여 샘플 응용 프로그램 tooRaspberry tooyour IoT hub 메시지를 보내고 hello led가 깜박이 Pi 3을 실행 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "깜박임 LED 클라우드 Pi, 클라우드에서 LED 깜빡이기"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>샘플 응용 프로그램 toosend 장치-클라우드 메시지 실행
## <a name="what-you-will-do"></a>수행할 사항
Toodeploy 및 보내는 라스베리 Pi 3에서 실행을 예제 응용 프로그램 메시지 tooyour IoT hub 방법을 표시이 문서 됩니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
하면 toouse hello 도구 toodeploy gulp 하 고 원주율 hello 샘플 Node.js 응용 프로그램을 실행 하는 방법에 대해 설명 합니다.

## <a name="what-you-need"></a>필요한 항목
* 이 작업을 시작 하기 전에 성공적으로 완료 해야 [메시지 Azure 함수 응용 프로그램 및 저장소 계정 tooprocess와 저장소 IoT 허브를 만들](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)합니다.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>IoT Hub 및 장치 연결 문자열 가져오기
장치 연결 문자열 hello Pi tooconnect tooyour IoT 허브에서 사용 됩니다. IoT 허브 연결 문자열 hello tooconnect tooyour IoT 허브는 사용할 수 있는 IoT 허브 toomanage hello 장치에 사용 되는 tooconnect toohello id 레지스트리에입니다. 

* Hello 다음 Azure CLI 명령을 실행 하 여 리소스 그룹에서 모든 IoT 허브를 나열 합니다.

```bash
az iot hub list -g iot-sample --query [].name
```

사용 하 여 `iot-sample` 의 hello 값으로 `{resource group name}` hello 값을 변경 되지 않은 경우.

* Hello 다음 Azure CLI 명령을 실행 하 여 hello IoT 허브 연결 문자열을 가져옵니다.

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`IoT hub를 생성 하 고 Pi 등록 지정한 hello 이름이입니다.

* Hello 다음 명령을 실행 하 여 hello 장치 연결 문자열을 가져옵니다.

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

사용 하 여 `myraspberrypi` 의 hello 값으로 `{device id}` hello 값을 변경 되지 않은 경우.

## <a name="configure-hello-device-connection"></a>Hello 장치 연결 구성
1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.
   
   ```bash
   npm install
   gulp init
   ```
2. 장치 구성 파일 열기 hello `config-raspberrypi.json` hello 다음 명령을 실행 하 여 Visual Studio Code에서:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Hello 바꾸기 작업을 수행 하는 hello 확인 `config-raspberrypi.json` 파일:
   
   * 대체 **[장치 호스트 이름 또는 IP 주소]** 에서 가져온 hello 장치 IP 주소 또는 호스트 이름으로 `device-discovery-cli` 또는 장치를 구성할 때 상속 hello 값을 사용 합니다.
   * 대체 **[IoT 장치 연결 문자열]** hello로 `device connection string` 얻을 수 있습니다.
   * 대체 **[IoT 허브 연결 문자열]** hello로 `iot hub connection string` 얻을 수 있습니다.

업데이트 hello `config-raspberrypi.json` hello 샘플 응용 프로그램에서 컴퓨터를 배포할 수 있도록 파일입니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 원주율 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Hello 샘플 응용 프로그램이 작동 하는지 확인 하십시오.
연결 된 tooPi 2 초 마다 깜박입니다.이 hello LED 표시 되어야 합니다. Hello led가 깜박입니다 때마다 hello 샘플 응용 프로그램 메시지 tooyour IoT hub를 보내고 해당 hello 메시지에 전송 되었습니다. IoT hub tooyour 확인 합니다. 또한 hello IoT hub에서 수신 된 각 메시지는 hello 콘솔 창에 인쇄 됩니다. 샘플 응용 프로그램 hello 20 개의 메시지를 보낸 후 자동으로 종료 합니다.

![보낸 메시지와 수신한 메시지가 있는 샘플 응용 프로그램](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>요약
배포 되었으며 Pi toosend 장치-클라우드 메시지 tooyour IoT 허브에서 hello 새 깜박임 샘플 응용 프로그램을 실행 합니다. 이제 toohello 저장소 계정에 작성 된 것 처럼 메시지를 모니터링할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[Azure Storage에 유지되는 메시지 읽기](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

