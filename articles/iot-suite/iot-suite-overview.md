---
title: "aaaMicrosoft Azure IoT Suite 개요 | Microsoft Docs"
description: "Azure IoT Suite 가지 미리 구성 된 솔루션 toocollect의 인터넷을 배달 하는 방법의 개요를 분석 및 데이터를 저장, 시각화를 제공 및 다른 시스템과 통합 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Azure IoT Suite의 개요

hello Azure 인터넷 IoT (사물) 서비스의 다양 한 범위의 기능을 제공 합니다. 이러한 엔터프라이즈급 서비스를 사용하면 다음과 같은 작업을 할 수 있습니다.

* 장치에서 데이터 수집
* 동작 내 데이터 스트림 분석
* 큰 데이터 집합 저장 및 쿼리
* 실시간 및 기록 데이터 시각화
* 백 오피스 시스템과 통합
* 장치 관리

toodeliver 이러한 기능, Azure IoT Suite 패키지으로 사용자 지정 확장을 사용 하 여 여러 Azure 서비스 함께 *솔루션 미리 구성 된*합니다. 이러한 미리 구성 된 솔루션은 tooreduce hello 시간 IoT 솔루션 toodeliver 수행 하는 데 도움이 되는 일반적인 IoT 솔루션 패턴의 기본 구현입니다. Hello를 사용 하 여 [IoT 소프트웨어 개발 키트][lnk-sdks]를 사용자 지정할 수 있으며 이러한 솔루션 toomeet 사용자의 요구 사항을 확장할 수 있습니다. 또한 새로운 IoT 솔루션을 개발할 때 이러한 솔루션을 예제 또는 템플릿으로 사용할 수도 있습니다.

hello 다음 비디오에서는 소개 tooAzure IoT Suite:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Azure IoT Suite에서 Azure IoT 서비스
미리 구성 하는 hello 솔루션은 일반적으로 서비스를 수행 하는 hello 사용:

* 코어 tooAzure IoT Suite는 hello [Azure IoT Hub] [ lnk-iot-hub] 서비스입니다. 이 서비스는 hello 장치-클라우드 및 클라우드 다른 키 IoT Suite 서비스 hello 메시징 기능을 클라우드-장치 및 게이트웨이 toohello hello 처럼 동작 합니다. hello 서비스 tooreceive 메시지 배율 사용할 때 장치를 사용 하면 및 tooyour 장치 명령을 보냅니다. hello 서비스 하면 수도 너무[장치를 관리 하][lnk-device-management]합니다. 예를 들어, 구성 컴퓨터를 다시 부팅 하거나 하나 이상의 장치 연결 된 toohello 허브에서 공장 재설정을 수행할 수 있습니다.
* [Azure Stream Analytics][lnk-asa]는 모션 내 데이터 분석을 제공합니다. 서비스 tooprocess 들어오는 원격 분석을 사용 하 여 IoT Suite, 집계를 수행 하 고 이벤트 검색 합니다. 또한 미리 구성 하는 hello 솔루션 스트림 분석 tooprocess 정보 메시지 장치에서 메타 데이터 또는 명령 응답 등의 데이터를 포함 하는 사용 합니다. hello 솔루션 사용 하 여 장치에서 스트림 분석 tooprocess hello 메시지 및 tooother 서비스 해당 메시지를 제공 합니다.
* [Azure 저장소] [ lnk-azure-storage] 및 [Azure Cosmos DB] [ lnk-document-db] hello 데이터 저장소 기능을 제공 합니다. hello 미리 구성 된 솔루션을 사용 하 고 toomake blob 저장소 toostore 원격 분석에 사용할 수 있게 합니다. hello Cosmos DB toostore 장치 메타 데이터를 사용 하 여 솔루션과 hello 솔루션의 hello 장치 관리 기능을 사용 하도록 설정 합니다.
* [Azure 웹 앱] [ lnk-web-apps] 및 [Microsoft Power BI] [ lnk-power-bi] hello 데이터 시각화 기능을 제공 합니다. Power BI의 hello 유연성을 사용 하면 tooquickly IoT Suite 데이터를 사용 하는 사용자 고유의 대화형 대시보드를 작성 합니다.

일반적인 IoT 솔루션의 hello 아키텍처의 개요를 참조 하십시오. [Microsoft Azure 및 인터넷 IoT (사물) hello][iot-suite-what-is-azure-iot]합니다.

## <a name="preconfigured-solutions"></a>미리 구성된 솔루션

IoT Suite 미리 구성 된 솔루션에 포함 된 해당 있습니다 tooquickly 시작 설정 및 일반적인 IoT 시나리오와 같은 hello tooexplore:

* 원격 모니터링
* 예측 유지 관리
* 연결된 공장

이러한 솔루션 tooyour Azure 구독을 배포 하 고 완전 한 종단 간 IoT 시나리오를 실행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

IoT Suite 수행할 수 있는 란 무엇 이며 해당 기본 구성 요소에 대 한 개요를가지고 학습할 수 있는 미리 구성 하는 hello 솔루션 IoT Suite에 대 한 자세한 정보. 자세한 내용은 참조 [솔루션 미리 구성 된 Azure IoT hello 무엇 인가요?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
