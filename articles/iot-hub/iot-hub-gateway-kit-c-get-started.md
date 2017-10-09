---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 시작 | Microsoft Docs"
description: "IoT 게이트웨이 시작 키트 시작, Azure IoT 허브를 만들고, SensorTag 및 게이트웨이 toohello IoT 허브 연결"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 게이트웨이 시작, azure iot 허브 hello iot toolkit, 사물 인터넷"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>SensorTag를 사용하여 IoT Gateway 시작 키트 시작

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [시뮬레이션된 장치](iot-hub-gateway-kit-c-sim-get-started.md)

이 자습서에서는 학습 hello의 기본적인 사용 하 여 시작 [IoT 게이트웨이 시작 키트](https://aka.ms/gateway-kit)합니다. Intel NUC 바람 강 Linux 및 hello 실행 중인 작업은 [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main)합니다. Tooseamleesly Azure IoT 허브를 사용 하 여 장치 toohello 클라우드를 연결 하는 방법을 설명 합니다.

***
**아직 키트가 없나요?:** [여기](https://aka.ms/gateway-kit)를 클릭합니다. **SensorTag가 없나요?:** [시뮬레이트된 장치로 시작하거나](iot-hub-gateway-kit-c-sim-get-started.md) [SensorTag를 구입합니다.](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>단원 1: NUC 구성
![단원 1 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

Hello Azure IoT 게이트웨이로 키트에서에서 Intel NUC (다음 단위의 컴퓨팅)를 설정 하면이 단원에서는 NUC에 hello Azure IoT 가장자리 패키지를 설치 하 고 샘플 앱 tooverify hello 게이트웨이 기능을 실행 합니다.

*예상 시간 toocomplete: 15 분*

너무 이동[IoT 게이트웨이로 Intel NUC 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>단원 2: IoT Hub 만들기
![단원 2 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

이 단원에서는 호스트 컴퓨터에 hello 도구와 소프트웨어를 설치 하면 합니다. 그런 다음 무료 Azure 계정, Azure IoT hub를 프로 비전 만들고 hello IoT 허브에서 첫 번째 장치를 만들고 합니다.

이 단원을 시작하기 전에 1단원을 완료합니다.

### <a name="get-hello-tools"></a>Hello 도구 가져오기
호스트 컴퓨터에 hello 도구와 소프트웨어를 설치 합니다.

*예상 시간 toocomplete: 20 분*

너무 이동[hello 도구 가져오기](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>IoT Hub 만들기 및 장치 등록
리소스 그룹을 만들고 첫 번째 Azure IoT 허브를 프로 비전 hello Azure CLI를 사용 하 여 첫 번째 장치 toohello IoT 허브를 추가 합니다.

*예상 시간 toocomplete: 10 분*

너무 이동[IoT hub를 만들고 장치를 등록 합니다.](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>3단원: SensorTag에서 메시지 수신 및 IoT Hub에서 메시지 읽기
이 단원에서는 스크립트 tooautomate hello 구성 및 배포용 샘플 응용 프로그램의 실행 게이트웨이를 사용 합니다. 이러한 응용 프로그램 모듈 tooaggregate 및 변환에 데이터의 컬렉션을 사용 하 여, 처리 명령, 또는 임의 개수의 관련된 작업을 수행 합니다. 모듈은 메시지 브로커를 통해 서로 통신합니다. hello 샘플 응용 프로그램에는 배포용 모듈과 IoT 허브 모듈에 있습니다. hello 배포용 모듈 배포용 SensorTag에서 데이터를 받습니다. 안녕 IoT 허브 모듈 패키지 hello 데이터 수신 및 Azure IoT 가장자리 tooyour IoT hub 제공 hello 게이트웨이 프레임 워크를 통해 보냅니다.

![단원 3 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>구성 하 고 hello 배포용 샘플 응용 프로그램 실행
SensorTag와 게이트웨이 간의 hello 연결을 설정 합니다. 그런 다음 hello 구성을 완료 하 고 hello 배포용 샘플 응용 프로그램을 실행 합니다.

*예상 시간 toocomplete: 15 분*

너무 이동[구성 및 실행된 hello 배포용 샘플 앱](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>IoT Hub에서 메시지 읽기
샘플에서 코드를 실행할 호스트 컴퓨터 tooread 메시지 IoT 허브에서 합니다.

*예상 시간 toocomplete: 15 분*

너무 이동[IoT 허브에서 메시지 읽기](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>4 단원: tooAzure 테이블 저장소 메시지 저장
IoT hub에서 들어오는 메시지를 가져오고 tooAzure 테이블 저장소에 기록 하는 Azure 함수 응용 프로그램을 만듭니다.

![단원 4 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Azure 함수 앱 및 Azure Storage 계정 만들기
Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 Azure 저장소 계정 및 Azure 함수 응용 프로그램.

*예상 시간 toocomplete: 10 분*

너무 이동[Azure 함수 앱 및 Azure 저장소 계정 만들기](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Azure Table Storage에 유지되는 메시지 읽기
TooAzure 테이블 저장소에 작성 된 것 처럼 hello 게이트웨이-클라우드 메시지를 모니터링 합니다.

*예상 시간 toocomplete: 5 분*

너무 이동[Azure 테이블 저장소에서 읽은 메시지 지속](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)합니다.

## <a name="troubleshooting"></a>문제 해결
Hello에 솔루션에 대 한 hello 단원 중 문제 수 있으면 확인 [문제 해결](iot-hub-gateway-kit-c-troubleshooting.md) 문서.

## <a name="explore-more"></a>자세히 살펴보기
Hello 방문 [Intel IoT 게이트웨이 키트 개발자 영역](http://software.intel.com/iot/microsoft-azure) toolearn 더 합니다.
