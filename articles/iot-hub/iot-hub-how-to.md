---
title: "IoT 허브 어떻게 aaaAzure 너무 | Microsoft Docs"
description: "개발자가 사용 하는 방법 hello 다양 한 IoT Hub 기능?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: d9c6e25bb332704dee4327bcdc361a299c064130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-iot-hub"></a>어떻게 toouse Azure IoT 허브

다양 한 옵션 toolearn toodevelop hello IoT 허브에 대 한 서비스 하는 방법을 사용할 수 있습니다.

* IoT Hub의 hello 기능을 자세히 설명 하는 hello 개념 문서를 읽습니다.
* IoT Hub의 다양 한 기능 hello를 포괄 하는 hello 자습서 중 하나를 수행 합니다.

## <a name="developer-guide"></a>개발자 가이드

개발자는 hello에서 IoT Hub에 대 한 자세한 개념적 지침을 읽을 수 있습니다 [개발자 가이드][lnk-devguide]합니다. 이 가이드에는 다음이 포함됩니다.

* 자세한 설명 하는 데 도움이 toolearn 어떻게 모든 IoT Hub 기능의 toouse 해당 합니다.
* 방법에 대 한 지침 toochoose 때 여러 옵션을 사용할 수 있습니다.

## <a name="tutorials"></a>자습서

실무 연습을 통해 작업 하 여 특정 IoT 허브 기능에 대 한 toolearn를 선호 하는 경우의 몇 가지 자습서 toochoose가 있습니다. 대부분의 자습서는 여러 프로그래밍 언어로 제공됩니다. 이 자습서는 다음을 포함합니다.

- [경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리][lnk-routes-tutorial]. 이 자습서에서는 toouse IoT Hub 라우팅 규칙 방식 toodispatch 장치-클라우드 메시지를 쉽게, 구성 기반 방식으로 보여 줍니다.

- [IoT Hub를 사용하여 클라우드-장치 메시지 보내기][lnk-c2d-tutorial]. 이 자습서 IoT 허브를 통해 toosend 클라우드-장치 메시지 하는 방법을 보여 줍니다 및 장치에서 클라우드-장치 메시지를 수신 합니다.

- [IoT Hub와 toohello 클라우드 장치에서에서 파일을 업로드][lnk-upload-tutorial]합니다. 이 자습서에서는 toouse hello 파일에서 IoT Hub의 기능을 업로드 하는 방법을 보여 줍니다.

- [장치 쌍 시작][lnk-twin-tutorial]. 이 자습서에는 toodevice 트윈스, 보고 된 속성, 원하는 속성 및 태그 소개합니다. 장치 장치 트윈스 toosynchronize 값을 사용합니다.

- [직접 메서드 사용][lnk-methods-tutorial]. 이 자습서 toouse 메서드를 직접 하는 방법을 보여 줍니다. 시뮬레이션 된 장치에서 직접적인 방법에 대 한 처리기를 추가 하 고 hello IoT 허브에서 직접 메서드를 호출 합니다.

- [장치 관리 시작][lnk-dm-tutorial]. 이 자습서 트윈스 및 직접 메서드와 같은 toouse 키 장치 관리 기능 하는 방법을 보여 줍니다. 이러한 기능 tooremotely 재부팅 시뮬레이션 된 장치를 사용합니다.

- [원하는 속성 tooconfigure 장치를 사용 하 여][lnk-properties-tutorial]합니다. 이 자습서에서는 toouse hello 장치로 이중 원하는 하 고 속성을 보고 하는 방법, tooremotely 장치를 구성 합니다.

- [장치 사용 작업 tooinitiate 장치 펌웨어 업데이트][lnk-jobs-tutorial]합니다. 이 자습서 트윈스 및 직접 메서드와 같은 toouse 키 장치 관리 기능 하는 방법을 보여 줍니다. 배웁니다 어떻게 toouse 이러한 기능 tooremotely 장치의 펌웨어를 업데이트 합니다.

- [작업 예약 및 브로드캐스트][lnk-schedule-tutorial]. 이 자습서에서는 어떻게 toouse 필요한 속성 및 메서드를 직접 toointeract 장치가 여러 개일 예약 된 시간입니다.

## <a name="next-steps"></a>다음 단계

toolearn hello IoT 허브 서비스에 대 한 자세한 참조 hello [개발자 가이드][lnk-devguide]합니다.

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md