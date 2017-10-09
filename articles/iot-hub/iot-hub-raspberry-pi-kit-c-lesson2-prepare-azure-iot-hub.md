---
title: "Connect Raspberry Pi (C) tooAzure IoT-2 단원: 장치를 등록 | Microsoft Docs"
description: "리소스 그룹을 만들고 Azure IoT hub를 만들 hello Azure CLI를 사용 하 여 hello Azure IoT 허브에서 Pi를 등록 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Raspberry Pi 클라우드, Pi 클라우드 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>IoT Hub 만들기 및 Raspberry Pi 3 등록
## <a name="what-you-will-do"></a>수행할 사항
* 리소스 그룹을 만듭니다.
* Hello 리소스 그룹에 Azure IoT 허브를 만듭니다.
* Hello Azure CLI (명령줄 인터페이스 Azure)를 사용 하 여 라스베리 Pi 3 toohello Azure IoT 허브를 추가 합니다.

Hello Azure CLI tooadd Pi tooyour IoT 허브를 사용 하는 경우 hello 서비스는 hello 서비스와 tooauthenticate Pi에 대 한 키를 생성 합니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-raspberry-pi-kit-c-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
이 문서에서는 다음에 대해 알아봅니다.
* 어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.
* 어떻게 toocreate Pi에 대 한 IoT hub에서 장치 id입니다.

## <a name="what-you-need"></a>필요한 항목
* Azure 계정.
* Mac 또는 hello Azure CLI 설치 된 Windows 컴퓨터

## <a name="create-your-iot-hub"></a>IoT Hub 만들기
Azure IoT Hub를 사용하면 수백만 개의 IoT 자산을 연결, 모니터링 및 관리할 수 있습니다. toocreate IoT 허브를 다음이 단계를 수행 합니다.

1. Hello 다음 명령을 실행 하 여 Azure 계정 tooyour에 로그인 합니다.

   ```bash
   az login
   ```

   로그인이 완료되면 사용 가능한 구독이 모두 나열됩니다.

2. Hello 기본 구독 hello 다음 명령을 실행 하 여 toouse 되도록 설정 합니다.

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`hello의 hello 출력에서 찾을 수 `az login` 또는 hello `az account list` 명령입니다.

3. Hello 다음 명령을 실행 하 여 hello 공급자를 등록 합니다. 리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다. Hello 공급자 제공 hello Azure 리소스를 배포 하기 전에 hello 공급자를 등록 해야 합니다.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. 리소스 그룹 만들기 라는 iot 샘플 hello 미국 서 부 지역에 hello 다음 명령을 실행 하 여:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`리소스 그룹을 만들면 hello 위치가입니다. 다른 위치 toouse을 원하는 경우 실행할 수 있습니다 `az account list-locations -o table` toosee 모든 hello Azure에서는 지원 되는 위치입니다.
 
5. Hello 다음 명령을 실행 하 여 hello iot 샘플 리소스 그룹에는 IoT 허브를 만듭니다.

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   기본적으로 hello 도구 hello 무료 가격 책정 계층에는 IoT 허브를 만듭니다. 자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.

> [!NOTE]
> IoT hub의 hello 이름 전역적으로 고유 해야 합니다. Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.

## <a name="register-pi-in-your-iot-hub"></a>IoT Hub에 Pi 등록
메시지 tooyour IoT hub를 보내고 IoT 허브에서 메시지를 수신 하는 각 장치는 고유 ID에 등록 되어야 합니다.

다음 명령을 실행하여 허브에 Pi를 등록합니다.

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a>요약
IoT Hub를 만들고 IoT Hub에 장치 ID로 Pi를 등록했습니다. Toosend Pi tooyour IoT 허브에서 메시지를 어떻게 준비 toolearn 것입니다.

## <a name="next-steps"></a>다음 단계
[Azure 저장소 계정 tooprocess와 저장소 IoT hub 및 Azure 함수 응용 프로그램 메시지를 만들](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)합니다.

