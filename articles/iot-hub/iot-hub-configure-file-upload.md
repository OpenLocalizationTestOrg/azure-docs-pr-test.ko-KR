---
title: "aaaUse hello Azure 포털 tooconfigure 파일 업로드 | Microsoft Docs"
description: "Toouse hello Azure 포털 tooconfigure 방법 IoT 허브 tooenable 파일에 연결 된 장치에서 업로드 합니다. Hello 대상 Azure 저장소 계정을 구성 하는 방법에 대 한 정보가 포함 됩니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>IoT Hub 파일 업로드 hello Azure 포털을 사용 하 여 구성

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>파일 업로드

toouse hello [IoT 허브에서 파일을 업로드 기능][lnk-upload], 허브와 Azure 저장소 계정을 연결 해야 합니다. 선택 **파일 업로드** toodisplay 수정 하는 hello IoT 허브에 대 한 파일 업로드 속성의 목록입니다.

![IoT Hub 파일 보기 업로드 hello 포털에서 설정][13]

**저장소 컨테이너**: 사용 하 여 hello Azure 포털 tooselect IoT Hub와 현재 Azure 구독 tooassociate 프로그램의 Azure 저장소 계정에서 blob 컨테이너입니다. 경우 필요에 따라 만들 수 있습니다는 Azure 저장소 계정에 hello **저장소 계정은** 블레이드 및 blob 컨테이너에서 hello **컨테이너** 블레이드입니다. IoT Hub 때 자동으로 생성 SAS Uri toouse 장치에 대 한 쓰기 권한 toothis blob 컨테이너로 파일을 업로드 합니다.

![Hello 포털에서 파일 업로드에 대 한 저장소 컨테이너 보기][14]

**업로드 된 파일에 대 한 알림을 수신**: hello 토글을 통해 파일 업로드 알림을 설정 하거나 해제 합니다.

**SAS TTL**:이 설정은-time-to-live의 SAS Uri IoT 허브에서 toohello 장치를 반환 하는 hello hello입니다. 기본적으로 tooone 시간 설정 되지만 사용자 지정 된 tooother 값을 사용할 수도 hello 슬라이더 합니다.

**파일 설정을 기본 TTL 알림**: hello time-to-live 만료 되기 전에 파일 업로드 알림입니다. Tooone 일은 기본적으로 설정 되지만 사용자 지정 된 tooother 값을 사용할 수도 hello 슬라이더 합니다.

**알림 최대 배달 횟수 파일**: hello 횟수입니다. IoT Hub 시도 toodeliver 파일 업로드 알림 hello 합니다. Too10 기본적으로 설정 되지만 사용자 지정 된 tooother 값을 사용할 수도 hello 슬라이더 합니다.

![IoT Hub 파일 업로드 hello 포털에서 구성][15]

## <a name="next-steps"></a>다음 단계

IoT Hub hello 파일 업로드 기능에 대 한 자세한 내용은 참조 [장치에서 파일을 업로드] [ lnk-upload] hello IoT 허브 개발자 가이드에서에서.

이러한 링크 toolearn Azure IoT Hub를 관리 하는 방법에 대 한 자세한를 수행 합니다.

* [IoT 장치 대량 관리][lnk-bulk]
* [IoT Hub 메트릭][lnk-metrics]
* [작업 모니터링][lnk-monitor]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]
* [Hello 접지에서 IoT 솔루션 보안][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
