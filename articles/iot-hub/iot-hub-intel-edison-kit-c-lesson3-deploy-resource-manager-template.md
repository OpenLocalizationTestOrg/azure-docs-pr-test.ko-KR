---
title: "Connect Intel Edison (C) tooAzure IoT-3 단원: 함수 앱 만들기 | Microsoft Docs"
description: "hello Azure 함수 앱 tooAzure IoT 허브 이벤트를 수신 하 고, 들어오는 메시지를 처리, tooAzure 테이블 저장소에 기록 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 저장 된 데이터에에서 데이터를 저장할 iot 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ef045ec2f44fe379a5e6c777d1bfb97de8b965a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Azure 함수 앱 및 Azure Storage 계정 만들기
[Azure 기능](../../articles/azure-functions/functions-overview.md) 쉽게 실행 하기 위한 솔루션은 *함수* (코드의 작은 조각) hello 클라우드에서 합니다. Azure 함수 응용 프로그램 호스트 hello Azure에서 함수를 실행 합니다.

## <a name="what-will-you-do"></a>수행할 내용
Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 Azure 저장소 계정 및 Azure 함수 응용 프로그램. hello Azure 함수 앱 tooAzure IoT 허브 이벤트를 수신 하 고, 들어오는 메시지를 처리, tooAzure 테이블 저장소에 기록 합니다. hello 저장소 계정을 읽는 데 사용 됩니다 hello Azure 테이블에서 메시지의 복사본을 유지 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-will-you-learn"></a>학습할 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 toouse [Azure 리소스 관리자](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure 리소스입니다.
* Toouse Azure 응용 프로그램 tooprocess IoT 허브 메시지 작동 방법과 Azure 테이블 저장소에서 tooa 테이블 작성.

## <a name="what-do-you-need"></a>필요한 내용
다음을 완료해야 합니다.
- [Intel Edison 시작][get-started-with-your-intel-edison]
- [Azure IoT Hub 만들기][create-your-azure-iot-hub]

## <a name="open-hello-sample-app"></a>열기 hello 샘플 응용 프로그램
Visual Studio Code에서 hello 다음 명령을 실행 하 여 hello 샘플 프로젝트를 엽니다.

```bash
cd Lesson3
code .
```

![Repo 구조][repo-structure]

* hello에 hello 파일 `app` 하위 폴더는 hello 키 원본 파일입니다. 이 소스 파일 hello 코드 toosend 20 배 tooyour IoT 허브 및 깜박임 hello LED 각 메시지에 대 한 보내는 메시지를 포함 합니다.
* hello `arm-template.json` 파일은 Azure 저장소 계정 및 Azure 함수 응용 프로그램을 포함 하는 hello Azure 리소스 관리자 템플릿.
* hello `arm-template-param.json` 파일은 hello 구성 파일에서 hello Azure 리소스 관리자 템플릿을 사용 합니다.
* hello `ReceiveDeviceMessages` 하위 폴더는 hello Azure 함수에 대 한 hello Node.js 코드를 포함 합니다.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager 템플릿 구성 및 Azure에서 리소스 만들기
업데이트 hello `arm-template-param.json` Visual Studio 코드 파일.

![Azure Resource Manager 템플릿 매개 변수][arm-template-parameters]

* **[your IoT Hub name]**을 [IoT Hub를 만들고 Intel Edison을 등록][created-your-iot-hub-and-registered-intel-edison]할 때 지정한 **{my hub name}**으로 바꿉니다.
* **[새 리소스에 대한 문자열 접두사]**를 원하는 접두사로 대체합니다. hello 접두사 hello 해당 리소스 이름은 전역적으로 고유 tooavoid 충돌을 확인 합니다. 대시 또는 hello 접두사의 초기 수는 사용 하지 마십시오.

Hello를 업데이트 한 후 `arm-template-param.json` 파일, hello 다음 명령을 실행 하 여 hello 리소스 tooAzure 배포:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

이러한 리소스 약 5 분 toocreate 걸립니다. Hello 리소스 만들기 진행 중에서 상태인 동안에 다음 toohello 아티클에서 이동할 수 있습니다.

## <a name="summary"></a>요약
Azure 함수 앱 tooprocess IoT 허브 메시지 생성 및 Azure 저장소 계정 toostore 이러한 메시지입니다. 이제 배포 하 고 Edison에 hello 샘플 toosend 장치-클라우드 메시지를 실행할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[샘플 응용 프로그램 toosend 장치-클라우드 메시지에 Intel Edison 실행][send-device-to-cloud-messages]합니다.
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md