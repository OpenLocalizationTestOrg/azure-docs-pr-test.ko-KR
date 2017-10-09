---
title: "aaaIntroduction tooStream 분석 | Microsoft Docs"
description: "스트림 분석에서 실시간 스트리밍 데이터 hello 인터넷 IoT (사물)를에서 분석 하는 데 도움이 되는 관리 되는 서비스에 알아봅니다."
keywords: "analytics as a service, 관리 서비스, 스트림 처리, 스트림 분석, 스트림 분석이란"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>Stream Analytics란 무엇인가요?

Azure Stream Analytics는 스트리밍 데이터에 대한 실시간 분석 계산 작업을 설정할 수 있는 완전히 관리되는 이벤트 처리 엔진입니다. 장치, 센서, 웹 사이트, 소셜 미디어 피드, 응용 프로그램, 인프라 시스템 등의 hello 데이터를 가져올 수 있습니다. 

## <a name="what-can-i-do-with-stream-analytics"></a>Stream Analytics으로 무엇을 할 수 있나요?

스트림 분석 tooexamine 대용량의 데이터 흐름에서 장치 또는 프로세스를 사용 하 여 hello 데이터 스트림, 정보를 추출 하 고, 패턴, 추세 및 관계를 찾습니다. Hello 데이터에 포함 된 내용에 따라, 응용 프로그램 작업 수행할 수 있습니다. 예를 들어 수 경고를 생성, 자동화 워크플로를 시작, 피드 정보 tooa 보고 Power BI와 같은 도구 또는 향후 조사에 대 한 데이터를 저장 합니다. 

예제:

* 금융 서비스 회사에서 제공된 개인화된 실시간 주식 거래 분석 및 알림
* 트랜잭션 데이터 검사를 통한 실시간 사기 감지 
* 데이터와 ID 보호 서비스
* 물리적 개체에 포함된 센서와 작동기에 의해 생성된 데이터의 분석(사물 인터넷 또는 IoT)
* 웹 클릭 동향 분석
* 시간 프레임 내에서 사용자 환경이 저하된 경우 경고를 발생하는 고객 관계 관리(CRM) 응용 프로그램

## <a name="how-does-stream-analytics-work"></a>Stream Analytics는 어떻게 작동합니까?

이 다이어그램에 어떻게 데이터는 수집 된, 분석 하 고, 프레젠테이션 또는 동작에 대 한 전송 보여 주는 hello 스트림 분석 파이프라인을 보여 줍니다. 

![Stream Analytics 파이프라인](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Stream Analytics는 스트리밍 데이터의 원본으로 시작합니다. hello 데이터는 Azure 이벤트 허브 또는 IoT 허브를 사용 하는 장치에서 Azure에 ingested 수 있습니다. Azure Blob 저장소와 같은 데이터 저장소에서 끌어올 수도 hello 데이터를 사용할 수 있습니다. 

스트림 분석을 만들 tooexamine hello 스트림 *작업* hello 데이터에서 온 것인지를 지정 하는 합니다. hello 작업 지정을 *변환*&mdash;어떻게 toolook 데이터, 패턴 또는 관계에 대 한 합니다. 이 작업의 경우 Stream Analytics는 일정 시간 동안 스트리밍 데이터를 필터링, 정렬, 집계 및 조인할 수 있도록 SQL 방식 쿼리 언어를 지원합니다.

마지막으로, hello 작업 출력 toosend hello 변환 된 데이터를 지정합니다. 이 기능을 사용 하면 분석 한 어떤 toodo 응답 toohello 정보에서 제어할 수 있습니다. 예를 들어 응답 tooanalysis에서 수행할 수 있습니다.

* 장치의 설정을 명령 toochange를 보냅니다. 
* 그 결과에 따라 작업을 수행 하는 프로세스에 의해 모니터링 되는 데이터 tooa 큐를 보냅니다. 
* 보고에 대 한 tooa Power BI 대시보드에 데이터를 보냅니다.
* 데이터 레이크 저장소, SQL Server 데이터베이스 또는 Azure Blob 또는 테이블 저장소와 같은 데이터 toostorage를 보냅니다.

작업이 실행되는 동안 모니터링하고 초당 몇 개의 이벤트를 처리할지 조정할 수 있습니다. 문제 해결을 위한 진단 로그를 생성하는 작업도 할 수 있습니다.

## <a name="key-capabilities-and-benefits"></a>주요 기능 및 이점

스트림 분석은 설계 된 toobe 쉽게 toouse, 크기 및 경제적이 고 유연 하 고 확장 가능한 tooany 작업입니다.

### <a name="connectivity-toomany-inputs-and-outputs"></a>연결 toomany 입 / 출력

스트림 분석 직접 연결 너무[Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 및 [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) 스트림 수집 및 hello에 대 한 [Azure Blob 저장소 서비스](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest 기록 데이터입니다. 이벤트 허브에서 데이터를 가져오는 경우 Stream Analytics를 다른 데이터 원본 및 처리 엔진과 결합할 수 있습니다.

작업 입력은 참조 데이터(정적 또는 느리게 변하는 데이터)를 포함할 수도 있습니다. 스트리밍 데이터 toothis 참조 데이터 tooperform 조회 작업 hello를 조인할 수 데이터베이스 쿼리를 사용 하 여 동일한 방식으로 합니다.

여러 방향으로 Stream Analytics 작업 출력을 라우팅합니다. Azure 저장소 blob 또는 테이블, Azure SQL DB, Azure 데이터 레이크 저장소 또는 Azure Cosmos DB 같은 toostorage를 작성할 수 있습니다. 여기에서 Azure HDInsight를 통해 일괄 처리 분석에 대 한 hello 데이터 이동할 수 있습니다. 이벤트 허브, Azure Service Bus 항목 또는 큐와 같은 다른 프로세스에 의해 소비에 대 한 hello 출력 tooanother 서비스를 보낼 수 있습니다. 시각화에 대 한 hello 출력 tooPower BI 보낼 수 있습니다.

### <a name="ease-of-use"></a>사용 편의성

단순 하 고 선언적 사용 toodefine 변환 [Stream Analytics 쿼리 언어](https://msdn.microsoft.com/library/azure/dn834998.aspx) 프로그램 고급 분석을 만들 수 있는 합니다. hello 쿼리 언어는 스트리밍 데이터를 입력으로 사용 합니다. 필터 및 정렬 hello 데이터 값을 집계, 계산을 수행, 데이터 (데이터 내에서 스트림 또는 tooreference), 조인 및 지리 공간 함수를 사용 하 여 다음 할 수 있습니다. IntelliSense 및 구문 검사를 사용 하 여 쿼리 hello 포털에서 편집할 수 있으며 hello 라이브 스트림에서 추출할 수 있는 샘플 데이터를 사용 하 여 쿼리를 테스트할 수 있습니다.

### <a name="extensible-query-language"></a>확장 가능한 쿼리 언어

정의 하 고 추가 함수를 호출 하 여 hello 쿼리 언어의 hello 기능을 확장할 수 있습니다. Azure 기계 학습 솔루션의 Azure 기계 학습 서비스 tootake 장점은 hello에 함수 호출을 정의할 수 있습니다. 스트림 분석 쿼리 일부로 tooperform 복잡 한 계산 순서에에서 JavaScript 사용자 정의 함수 (Udf)를 통합할 수 있습니다.

### <a name="scalability"></a>확장성

스트림 분석 too1 GB의 초당 들어오는 데이터를 처리할 수 있습니다. 와 통합 [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 및 [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) 작업 tooingest 수백만 두 번째 기능은 당 이벤트의 연결 된 장치, clickstreams, 및 로그 파일 tooname에서 몇 가지 있습니다. 이벤트 허브의 hello 파티션 기능을 사용 논리 단계 계산을 분할할 수 있습니다, tooincrease 확장성 분할 각각 hello 기능 toobe 추가 합니다.

### <a name="low-cost"></a>저렴한 비용

클라우드 서비스, 스트림 분석 비용 효율적인 시작 하나요 최적화 toolet 크기는입니다. 스트리밍 단위 사용 및 hello 금액 hello 시스템에 의해 처리 되는 데이터에 따라 작업을 진행 하면서 지불 합니다. 사용 현황 처리 된 이벤트의 hello 볼륨에 따라 파생 있고 스트림 분석 작업 hello 클러스터 toohandle 내에서 프로 비전 hello 양의 계산 합니다.

### <a name="reliability-quick-recovery-and-repeatability"></a>안정성, 빠른 복구 및 반복성

Hello 클라우드에서 관리 되는 서비스로, 스트림 분석 데이터 손실을 방지할 하 고 비즈니스 연속성을 제공 합니다. 오류가 발생 한 경우 hello 서비스는 기본 제공 복구 기능을 제공 합니다. Toointernally hello 기능 상태를 유지 하 고 hello 서비스 가능한 tooarchive 이벤트 하 고 항상 hello 동일한 결과 얻는 hello 이후 처리를 다시 적용 하는 반복 가능한 결과 제공 합니다. 이 시간에 다시 toogo 수 있고 근본 원인 분석, 가상 분석을 수행할 때 계산을 조사 합니다.

## <a name="next-steps"></a>다음 단계

* [IoT 장치의 입력 및 쿼리로 시험](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md)하여 시작합니다.
* 빌드는 [종단 간 스트림 분석 솔루션](stream-analytics-real-time-fraud-detection.md) 사기성 호출에 대 한 메타 데이터 toolook 전화를 검사 하 합니다.
* 와 같은 고유한 개념 및 hello 스트림 분석에 대 한 SQL 방식 쿼리 언어에 대 한 자세한 내용은 [window 함수](stream-analytics-window-functions.md)합니다.
* 너무 방법에 대해 알아봅니다[스트림 분석 작업의 크기를 조정](stream-analytics-scale-jobs.md)합니다. 
* 너무 방법에 대해 알아봅니다[Azure 기계 학습 및 스트림 분석 통합](stream-analytics-machine-learning-integration-tutorial.md)합니다.
* Hello에 tooyour 스트림 분석 질문 답변을 찾을 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)합니다.

