---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 시작 | Microsoft Docs"
description: "IoT 게이트웨이 시작 키트 시작, Azure IoT 허브를 만들고, 게이트웨이 toohello IoT 허브 연결"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 게이트웨이 시작, azure iot 허브 hello iot toolkit, 사물 인터넷"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>시뮬레이트된 장치에서 IoT Gateway 시작 키트 시작

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [시뮬레이션된 장치](iot-hub-gateway-kit-c-sim-get-started.md)

이 자습서에서는 학습 hello의 기본적인 사용 하 여 시작 [IoT 게이트웨이 시작 키트](https://aka.ms/gateway-kit)합니다. Wind River Linux를 실행하는 Intel NUC로 작업하게 됩니다. Tooseamleesly Azure IoT 허브를 사용 하 여 장치 toohello 클라우드를 연결 하는 방법을 설명 합니다.

***
**아직 키트가 없나요?:** [여기](https://aka.ms/gateway-kit)를 클릭합니다.
***

## <a name="lesson-1-configure-your-nuc"></a>단원 1: NUC 구성
![단원 1 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

Hello Azure IoT 게이트웨이로 키트에서에서 Intel NUC (다음 단위의 컴퓨팅)를 설정 하면이 단원에서는 NUC에 hello Azure IoT 가장자리 패키지를 설치 하 고 샘플 앱 tooverify hello 게이트웨이 기능을 실행 합니다.

*예상 시간 toocomplete: 15 분*

너무 이동[IoT 게이트웨이로 Intel NUC 설정](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>단원 2: IoT Hub 만들기
![단원 2 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

이 단원에서는 호스트 컴퓨터에 hello 도구와 소프트웨어를 설치 하면 합니다. 그런 다음 무료 Azure 계정, Azure IoT hub를 프로 비전 만들고 hello IoT 허브에서 첫 번째 장치를 만들고 합니다.

이 단원을 시작하기 전에 1단원을 완료합니다.

### <a name="get-hello-tools"></a>Hello 도구 가져오기
호스트 컴퓨터에 hello 도구와 소프트웨어를 설치 합니다.

*예상 시간 toocomplete: 20 분*

너무 이동[hello 도구 가져오기](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>IoT Hub 만들기 및 장치 등록
리소스 그룹을 만들고 첫 번째 Azure IoT 허브를 프로 비전 hello Azure CLI를 사용 하 여 첫 번째 장치 toohello IoT 허브를 추가 합니다.

*예상 시간 toocomplete: 10 분*

너무 이동[IoT hub를 만들고 장치를 등록 합니다.](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>3 단원: hello 시뮬레이션 된 장치에서 메시지를 수신 및 IoT 허브에서 메시지 읽기
이 단원에서는 스크립트 tooautomate hello 구성 및 시뮬레이션 된 장치 앱의 실행 게이트웨이를 사용 합니다. hello 시뮬레이션 된 장치 앱 샘플 온도 데이터를 생성 하 고 tooan IoT 허브 모듈 보냅니다. 안녕 IoT 허브 모듈 패키지 hello 데이터 수신 및 Azure IoT 가장자리 tooyour IoT hub 제공 hello 게이트웨이 프레임 워크를 통해 보냅니다.

![단원 3 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>시뮬레이트된 장치 구성 및 실행
Hello 샘플 코드를 준비 합니다. 다음 구성 하 고 hello 시뮬레이션 된 장치에 대 한 샘플 응용 프로그램을 실행 합니다.

*예상 시간 toocomplete: 15 분*

너무 이동[실행 시뮬레이션된 된 장치 및 구성](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>IoT Hub에서 메시지 읽기
IoT 허브에서 호스트 컴퓨터 tooread hello 메시지에 예제 코드를 실행 합니다.

*예상 시간 toocomplete: 15 분*

너무 이동[IoT 허브에서 메시지 읽기](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>4 단원: tooAzure 테이블 저장소 메시지 저장
IoT hub에서 들어오는 메시지를 가져오고 tooAzure 테이블 저장소에 기록 하는 Azure 함수 응용 프로그램을 만듭니다.

![단원 4 종단간 다이어그램](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Azure 함수 앱 및 Azure Storage 계정 만들기
Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 Azure 저장소 계정 및 Azure 함수 응용 프로그램.

*예상 시간 toocomplete: 10 분*

너무 이동[Azure 함수 앱 및 Azure 저장소 계정 만들기](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Azure Table Storage에 유지되는 메시지 읽기
TooAzure 테이블 저장소에 작성 된 것 처럼 hello 게이트웨이-클라우드 메시지를 모니터링 합니다.

*예상 시간 toocomplete: 5 분*

너무 이동[Azure 테이블 저장소에서 읽은 메시지 지속](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md)합니다.

## <a name="troubleshooting"></a>문제 해결
Hello에 솔루션에 대 한 hello 단원 중 문제 수 있으면 확인 [문제 해결](iot-hub-gateway-kit-c-sim-troubleshooting.md) 문서.

## <a name="explore-more"></a>자세히 살펴보기
Hello 방문 [Intel IoT 게이트웨이 키트 개발자 영역](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn 더 합니다.
