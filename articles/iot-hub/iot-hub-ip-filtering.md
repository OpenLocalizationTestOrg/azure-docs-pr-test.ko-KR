---
title: "aaaAzure IoT 허브 IP 연결 필터 | Microsoft Docs"
description: "특정 IP에서 tooblock 연결 필터링 toouse IP 해결 하는 방법을 tooyour Azure IoT 허브에 대 한 합니다. 개별 또는 IP 주소 범위에서 연결을 차단할 수 있습니다."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>IP 필터 사용

보안은 Azure IoT Hub를 기반으로 하는 모든 IoT 솔루션의 중요한 측면입니다. Tooexplicitly 필요한 경우에 따라 보안 구성의 일부로 장치 연결할 수는 hello IP 주소를 지정 합니다. hello _IP 필터_ 거부 하거나 특정 IPv4 주소에서 트래픽을 받아들이고에 대 한 tooconfigure 규칙 기능을 사용 합니다.

## <a name="when-toouse"></a>때 toouse

특정 IP 주소에 대 한 유용한 tooblock hello IoT Hub 끝점을 되었을 때에 두 개의 특정 사용 사례:

- IoT Hub가 지정된 범위의 IP 주소에서 오는 트래픽만 수신하고 그 밖의 트래픽은 거부합니다. IoT 허브를 사용 하는 예를 들어 [Azure Express 경로] toocreate IoT hub와 온-프레미스 인프라 간에 개인 연결 합니다.
- IoT 허브 관리자에 게 의심 스러운 것으로 확인 된 IP 주소에서 tooreject 트래픽이 필요 합니다.

## <a name="how-filter-rules-are-applied"></a>필터 규칙이 적용되는 방식

hello IP 필터 규칙 hello IoT 허브 서비스 수준에서 적용 됩니다. 따라서 hello IP 필터 규칙 tooall 연결 장치 및 모든 지원 되는 프로토콜을 사용 하 여 백 엔드 응용 프로그램에서 적용 됩니다.

IoT Hub의 거부 IP 규칙에 일치하는 IP 주소에서 오는 모든 연결 시도는 권한 없음 401 상태 코드 및 설명을 수신합니다. hello 응답 메시지는 hello IP 규칙을 언급 하지 않습니다.

## <a name="default-setting"></a>기본 설정

기본적으로 hello **IP 필터** IoT 허브에 대 한 hello 포털에서 표는 비어 있습니다. 이러한 기본 설정은 허브가 모든 IP 주소의 연결을 수락한다는 것을 의미합니다. 이 기본 설정은 hello 0.0.0.0/0 IP 주소 범위를 허용 하는 해당 tooa 규칙입니다.

![IoT Hub 기본 IP 필터 설정][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>IP 필터 규칙 추가 또는 편집

IP 필터 규칙을 추가 하는 경우에 다음 값에는 hello에 대 한 표시 됩니다.

- **IP 필터 규칙 이름** 하 too128 자를 고유한, 대/소문자 구분, 영숫자 문자열 이어야 합니다. Hello ASCII 7 비트 영숫자 문자만 더하기 `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` 허용 됩니다.
- 선택 된 **거부** 또는 **수락** hello로 **동작** hello IP 필터 규칙에 대 한 합니다.
- 단일 IPv4 주소 또는 CIDR 표기법으로 IP 주소 블록을 제공합니다. 예를 들어 CIDR 표기법 192.168.100.0/22 나타냅니다 hello 1024 IPv4 주소에서 192.168.100.0이 고 too192.168.103.255 합니다.

![IP 필터 규칙 tooan IoT hub 추가][img-ip-filter-add-rule]

Hello 규칙을 저장 하면 해당 hello 업데이트 진행에서 됨을 알리는 경고가 표시 됩니다.

![IP 필터 규칙 저장에 대한 알림][img-ip-filter-save-new-rule]

hello **추가** hello 최대 10 개의 IP 필터 규칙에 도달 하면 옵션은 사용할 수 없습니다.

Hello 규칙을 포함 하는 hello 행을 두 번 클릭 하 여 기존 규칙을 편집할 수 있습니다.

> [!NOTE]
> 거부 된 IP 주소는 다른 Azure 서비스 (예: Azure Stream Analytics, Azure 가상 컴퓨터 또는 hello 포털에서 장치 탐색기 hello) hello IoT 허브와 상호 작용에서 방지할 수 있습니다.

> [!WARNING]
> IoT hub에서 Azure 스트림 분석 (ASA) tooread 메시지를 사용 하 여 IP 필터링이 활성화 된 경우 hello ASA 연결 문자열에에서 hello 이벤트 허브 호환 이름과 IoT Hub 끝점을 사용 합니다.

## <a name="delete-an-ip-filter-rule"></a>IP 필터 규칙 삭제

toodelete IP 필터 규칙에 hello 그리드에서 하나 이상의 규칙 선택 **삭제**합니다.

![IoT Hub IP 필터 규칙 삭제][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>IP 필터 규칙 평가

IP 필터 규칙 순서에 적용 되 고 hello hello hello IP 주소를 일치 하는 항목을 결정 하는 첫 번째 규칙 적용 하거나 작업을 취소 합니다.

예를 들어 hello 범위 192.168.100.0/22에서 tooaccept 주소가 다른 모든 항목을 거부 하는 경우 hello 그리드에서 첫 번째 규칙 hello 주소 범위 192.168.100.0/22 hello를 사용 해야 합니다. 다음 규칙 hello hello 범위 0.0.0.0/0을 사용 하 여 모든 주소를 거부 해야 합니다.

Hello 점 세 개 세로 hello 시작 되는 행을 클릭 하 고 끌어서를 사용 하 여 hello 표에에서는 IP 필터 규칙의 hello 순서를 변경 하 고 삭제할 수 있습니다.

toosave 새 IP 필터링 규칙 순서를 클릭 **저장**합니다.

![IoT 허브 IP 필터 규칙의 hello 순서 변경][img-ip-filter-rule-order]

## <a name="next-steps"></a>다음 단계

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

- [작업 모니터링][lnk-monitor]
- [IoT Hub 메트릭][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express 경로]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md