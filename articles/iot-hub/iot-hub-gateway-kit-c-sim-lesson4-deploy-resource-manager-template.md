---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 4: 메시지 저장 | Microsoft Docs"
description: "Intel NUC tooyour IoT 허브에서 메시지를 저장 하 고 tooAzure 테이블 저장소에 쓰는 hello 클라우드에서 읽어 주시기 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 저장 된 데이터에에서 데이터를 저장할 iot 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Azure 함수 앱 및 저장소 계정 만들기

Azure 기능을 쉽게 실행 하기 위한 솔루션 _함수_ (코드의 작은 조각) hello 클라우드에서 합니다. Azure 함수 응용 프로그램 호스트 hello Azure에서 함수를 실행 합니다. 

## <a name="what-you-will-do"></a>수행할 사항

- Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 Azure 저장소 계정 및 Azure 함수 응용 프로그램. hello Azure 함수 앱 tooAzure IoT 허브 이벤트를 수신 하 고, 들어오는 메시지를 처리, tooAzure 테이블 저장소에 기록 합니다.

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.


## <a name="what-you-will-learn"></a>알아볼 내용

이 단원에서는 다음 내용을 배웁니다.

- 어떻게 toouse Azure 리소스 관리자 toodeploy Azure 리소스입니다.
- Toouse Azure 응용 프로그램 tooprocess IoT Hub 메시지 작동 방법과 Azure 테이블 저장소에서 tooa 테이블 작성.

## <a name="what-you-need"></a>필요한 항목

성공적으로 완료 해야 hello 이전 단원:

- [1단원: Intel NUC를 IoT Gateway로 설정](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [2단원: 호스트 컴퓨터 및 Azure IoT Hub 준비](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [3 단원: hello 시뮬레이션 된 장치에서 메시지를 수신 및 IoT 허브에서 메시지 읽기](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>샘플 앱 열기

Tooyour 이동 `iot-hub-c-intel-nuc-gateway-getting-started` 리포지토리 폴더, initialize hello 구성 파일 및 hello 다음 명령을 실행 하 여 Visual Studio Code에서 연 다음 hello 샘플 프로젝트:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Repo 구조](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- hello `arm-template.json` 파일은 Azure 저장소 계정 및 Azure 함수 응용 프로그램을 포함 하는 hello Azure 리소스 관리자 템플릿.
- hello `arm-template-param.json` 파일은 hello 구성 파일에서 hello Azure 리소스 관리자 템플릿을 사용 합니다.
- hello `ReceiveDeviceMessages` 하위 폴더는 hello Azure 함수에 대 한 hello Node.js 코드를 포함 합니다.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager 템플릿 구성 및 Azure에서 리소스 만들기

업데이트 hello `arm-template-param.json` Visual Studio 코드 파일.

![ARM 템플릿 JSON](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- `[your IoT Hub name]`을 단원 2에서 지정했던 `{my hub name}`으로 바꿉니다.

Hello를 업데이트 한 후 `arm-template-param.json` 파일, hello 다음 명령을 실행 하 여 hello 리소스 tooAzure 배포:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

사용 하 여 `iot-gateway` 의 hello 값으로 `{resource group name}` hello 값 2 단원에서에서 변경 되지 않은 경우.

## <a name="summary"></a>요약

Azure 함수 앱 tooprocess IoT 허브 메시지 생성 및 Azure 저장소 계정 toostore 이러한 메시지입니다. 이제 게이트웨이 tooyour IoT 허브에서 보낸 메시지를 읽을 수 있습니다.

## <a name="next-steps"></a>다음 단계
[Azure Storage에 유지되는 메시지를 읽습니다](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).
