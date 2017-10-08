---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 2: 장치 등록 | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, 사물 인터넷 클라우드, azure iot hub 장치 만들기, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Azure IoT Hub 만들기 및 장치 등록

## <a name="what-you-will-do"></a>수행할 사항

- 리소스 그룹 만들기
- 첫 번째 IoT Hub 만들기
- Hello Azure CLI를 사용 하 여 IoT hub에 장치를 등록 합니다. 

IoT hub에서 장치를 등록할 때 hello Azure IoT 허브 서비스는 hello 서비스와 장치 toouse tooauthenticate 프로그램에 대 한 키를 생성 합니다. 

문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

이 단원에서는 다음 내용을 배웁니다.

- 어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.
- 어떻게 tooregister IoT hub에서 장치.

## <a name="what-you-need"></a>필요한 항목

- 활성 Azure 구독. Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.
- Hello Azure CLI 설치 되어 있어야 합니다.

## <a name="create-an-iot-hub"></a>IoT Hub 만들기

IoT hub toocreate 다음이 단계를 따르십시오.

1. Hello 다음 명령을 실행 하 여 Azure 계정 tooyour에 로그인 합니다.

   ```bash
   az login
   ```

   로그인하면 사용 가능한 구독이 모두 나열됩니다.

2. Hello 기본 hello 다음 명령을 실행 하 여 toouse 되도록 Azure 구독을 설정 합니다.

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`hello의 hello 출력에서 찾을 수 `az login` 또는 hello `az account list` 명령입니다.

3. Hello 다음 명령을 실행 하 여 hello 공급자를 등록 합니다. 리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다. Hello 공급자 제공 hello Azure 리소스를 배포 하기 전에 hello 공급자를 등록 해야 합니다.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. 명명 된 리소스 그룹 만들기 `iot-gateway` hello 다음 명령을 실행 하 여 hello 미국 서 부 지역에 있습니다.

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`리소스 그룹을 만들면 hello 위치가입니다. 다른 위치 toouse을 원하는 경우 실행할 수 있습니다 `az account list-locations -o table` toosee 모든 hello Azure에서는 지원 되는 위치입니다.

5. Hello에서 IoT hub를 만들 `iot-gateway` hello 다음 명령을 실행 하 여 리소스 그룹:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

기본적으로 hello 도구 hello 무료 가격 책정 계층에는 IoT 허브를 만듭니다. 자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.

> [!NOTE]
> IoT hub의 hello 이름 전역적으로 고유 해야 합니다. Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.

## <a name="register-your-device-in-your-iot-hub"></a>IoT Hub에 장치 등록

메시지 tooyour IoT hub를 보내고 IoT 허브에서 메시지를 수신 하는 각 장치는 고유 ID에 등록 되어야 합니다.
다음 명령을 실행하여 IoT Hub에 장치를 등록합니다.

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>요약

IoT Hub를 만들고 IoT Hub에 장치 ID로 논리적 장치를 등록했습니다. Tooconfigure 및 물리적 장치 tooyour IoT 허브 hello에서에서 실행 되는 게이트웨이 샘플 응용 프로그램 toosend 데이터의 클라우드 준비 toolearn 것입니다.

## <a name="next-steps"></a>다음 단계
[BLE 샘플 앱 구성 및 실행](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)