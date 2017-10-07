---
title: "aaaDeep을 심층적으로 자동차를 움직일 상태를 예측 하 고 습관-Azure | Microsoft Docs"
description: "습관 지원 하 고 차량 상태에 대해 Cortana 인텔리전스 toogain 실시간 및 예측 insights hello 기능을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>자동차를 움직일 원격 분석 분석 솔루션 플레이 북: hello 솔루션으로 심층 분석
이 **메뉴** 이 플레이 북의 toohello 섹션 링크: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

이 섹션으로 드릴 다운 각 hello 솔루션 아키텍처 지침 및 사용자 지정에 대 한 포인터에에서 표시 된 hello 단계입니다. 

## <a name="data-sources"></a>데이터 원본
hello 솔루션에서는 두 개의 서로 다른 데이터 소스를 사용합니다.

* **시뮬레이션된 차량 신호 및 진단 데이터 집합** 및 
* **차량 카탈로그**

차량 텔레매틱스 시뮬레이터가 이 솔루션의 일부로 포함되어 있습니다. 진단 정보를 내보냅니다 하 고 해당 toohello 상태 hello 차량와 시간에서 지정된 된 지점에서 패턴을 구동 toohello에 알립니다. 클릭 [차량 전자 통신 정보 시뮬레이터](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **차량 전자 통신 정보 시뮬레이터 Visual Studio 솔루션** 요구 사항에 따라 사용자 지정 합니다. hello 차량 카탈로그 VIN toomodel 매핑 사용 하 여 참조 데이터 집합을 포함합니다.

![차량 텔레매틱스 시뮬레이터](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*그림 1 – 차량 텔레매틱스 시뮬레이터*

Hello 다음 스키마를 포함 하는 JSON 형식의 데이터 집합입니다.

| 열 | 설명 | 값 |
| --- | --- | --- |
| VIN |임의로 생성된 차량 식별 번호 |10,000개의 임의로 생성된 차량 식별 번호의 마스터 목록에서 가져옵니다. |
| 외부 온도 |hello 차량 운전는 온도 외부 hello |0-100까지의 임의로 생성된 번호 |
| 엔진 온도 |hello 차량 hello 엔진 온도 |0-500까지의 임의로 생성된 번호 |
| 속도 |hello 엔진 속도 hello에 자동차를 움직일 제어 |0-100까지의 임의로 생성된 번호 |
| 연료 |hello 자동차의 연료 수준 hello |0-100까지의 임의로 생성된 번호(연료 수준 비율을 나타냄) |
| 엔진 오일 |hello 차량 hello 엔진 석유 수준 |0-100까지의 임의로 생성된 번호(엔진 오일 수준 비율을 나타냄) |
| 타이어 압력 |hello 차량 hello tire 압력 |0-50까지의 임의로 생성된 번호(타이어 압력 수준 비율을 나타냄) |
| 주행 기록계 |hello 차량 주행 기록 계 읽기 hello |0-200000까지의 임의로 생성된 번호 |
| Accelerator_pedal_position |hello 차량 hello 가속기 페달 위치 |0-100까지의 임의로 생성된 번호(가속기 수준 비율을 나타냄) |
| Parking_brake_status |Hello 차량 파킹 되었는지 여부를 나타냅니다. |True 또는 False |
| Headlamp_status |Hello headlamp 위치가에 여부를 나타냅니다. |True 또는 False |
| Brake_pedal_status |Hello 브레이크 페달을 눌렀는지 여부를 나타냅니다. |True 또는 False |
| Transmission_gear_position |hello 차량 hello 전송 기어 위치 |상태: 1단, 2단, 3단, 4단, 5단, 6단, 7단, 8단 |
| Ignition_status |실행 중이거나 중지 된 hello 차량 인지를 나타냅니다. |True 또는 False |
| Windshield_wiper_status |Hello 차량의 바람막이 wiper 설정 여부를 나타냅니다. |True 또는 False |
| ABS |ABS의 작동 여부를 나타냅니다. |True 또는 False |
| Timestamp |hello 데이터 요소를 만들 때 timestamp 안녕 |Date |
| City |hello 차량 hello 위치 |이 솔루션의 경우 4개 도시: 벨뷰, 레드몬드, 사마미시, 시애틀 |

참조 데이터 집합을 모델 hello 차량 VIN toohello 모델 매핑을 포함합니다. 

| VIN | 모델 |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |세단 |
| 8J0U8XCPRGW4Z3NQE |하이브리드 |
| WORG68Z2PLTNZDBI7 |가족용 승용차 |
| JTHMYHQTEPP4WBMRN |세단 |
| W9FTHG27LZN1YWO0Y |하이브리드 |
| MHTP9N792PHK08WJM |가족용 승용차 |
| EI4QXI2AXVQQING4I |세단 |
| 5KKR2VB4WHQH97PF8 |하이브리드 |
| W9NSZ423XZHAONYXB |가족용 승용차 |
| 26WJSGHX4MA5ROHNL |컨버터블 |
| GHLUB6ONKMOSI7E77 |스테이션 웨건 |
| 9C2RHVRVLMEJDBXLP |경차 |
| BRNHVMZOUJ6EOCP32 |소형 SUV |
| VCYVW0WUZNBTM594J |스포츠카 |
| HNVCE6YFZSA5M82NY |중형 SUV |
| 4R30FOR7NUOBL05GJ |스테이션 웨건 |
| WYNIIY42VKV6OQS1J |대형 SUV |
| 8Y5QKG27QET1RBK7I |대형 SUV |
| DF6OX2WSRA6511BVG |쿠페 |
| Z2EOZWZBXAEW3E60T |세단 |
| M4TV6IEALD5QDS3IR |하이브리드 |
| VHRA1Y2TGTA84F00H |가족용 승용차 |
| R0JAUHT1L1R3BIKI0 |세단 |
| 9230C202Z60XX84AU |하이브리드 |
| T8DNDN5UDCWL7M72H |가족용 승용차 |
| 4WPYRUZII5YV7YA42 |세단 |
| D1ZVY26UV2BFGHZNO |하이브리드 |
| XUF99EW9OIQOMV7Q7 |가족용 승용차 |
| 8OMCL3LGI7XNCC21U |컨버터블 |
| ……. | |

### <a name="references"></a>참조
[차량 텔레매틱스 시뮬레이터 Visual Studio 솔루션](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/)

[Azure 데이터 팩터리](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>수집
Azure 이벤트 허브, 스트림 분석 및 데이터 팩터리의의 조합은 사용된 tooingest hello 차량 신호를 hello 진단 이벤트 및 실시간 분석을 일괄 처리 및 합니다. 이러한 구성 요소가 모두 생성 및 hello 솔루션 배포의 일부로 구성 됩니다. 

### <a name="real-time-analysis"></a>실시간 분석
hello hello 차량 전자 통신 정보 시뮬레이터에 의해 생성 된 이벤트 게시 된 이벤트 허브 SDK hello toohello 이벤트 허브를 사용 하 여 합니다. hello 스트림 분석 작업 hello 이벤트 허브에서에서 이러한 이벤트를 수집 하 고 프로세스의 실시간으로 tooanalyze hello 차량 상태 데이터를 hello 합니다. 

![이벤트 허브 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*그림 4 - 이벤트 허브 대시보드*

![데이터를 처리 중인 Stream Analytics 작업](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*그림 5 - 데이터를 처리 중인 Stream Analytics 작업*

hello 스트림 분석 작업입니다.

* hello 이벤트 허브에서에서 데이터를 수집합니다. 
* hello 참조 데이터 toomap hello 차량 VIN toohello 해당 모델을 사용 하 여 연결을 수행합니다. 
* 충분한 일괄 분석을 위해 Azure Blob Storage에 유지 

hello 다음 스트림 분석 쿼리는 Azure blob 저장소로 사용 되는 toopersist hello 데이터입니다. 

![데이터 수집을 위한 Stream Analytics 작업 쿼리](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*그림 6 - 데이터 수집을 위한 Stream Analytics 작업 쿼리*

### <a name="batch-analysis"></a>일괄 분석
또한 더욱 충분한 일괄 분석을 위해 시뮬레이션된 차량 신호와 진단 데이터 집합의 추가 볼륨을 생성합니다. 이 필수 tooensure 일괄 처리에 대 한 적절 한 대표 데이터 볼륨입니다. 이 작업을 위해 사용 하 여 "PrepareSampleDataPipeline" hello Azure Data Factory 워크플로 toogenerate에 이름이 지정 된 파이프라인 시뮬레이션 된 차량 신호 및 진단 데이터 집합에 1 년 동안의 합니다. 클릭 [Data Factory 사용자 지정 활동](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello DotNet 활동을 사용자 지정 하는 데이터 팩터리. 사용자 지정을 위한 Visual Studio 솔루션 요구 사항에 따라 합니다. 

![일괄 처리 워크플로를 위한 샘플 데이터 준비](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*그림 7 - 일괄 처리 워크플로를 위한 샘플 데이터 준비*

hello 파이프라인의 사용자 지정 ADF.Net 구성 됩니다. 작업을 여기에 표시 합니다.

![PrepareSampleDataPipeline 작업](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*그림 8 - PrepareSampleDataPipeline*

Hello 파이프라인 성공적으로 실행 되 고 1 년 분량의 시뮬레이션 된 차량 신호 및 진단 "RawCarEventsTable" dataset "준비" 표시는 데이터는 생성 됩니다. Hello 다음을 참조 폴더 및 hello "connectedcar" 컨테이너 아래에서 저장소 계정에서 만든 파일:

![PrepareSampleDataPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*그림 9 - PrepareSampleDataPipeline 출력*

### <a name="references"></a>참조
[스트림 수집을 위한 Azure 이벤트 허브 SDK](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Azure Data Factory 데이터 이동 기능](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet 작업](../data-factory/data-factory-use-custom-activities.md)

[샘플 데이터 준비를 위한 Azure 데이터 팩터리 DotNet 작업 Visual Studio 솔루션](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>데이터 집합을 분할 hello
hello 원시 반 구조화 된 차량 신호 및 진단 데이터 집합을 YEAR/MONTH 형식 hello 데이터 준비 단계에서 분할 됩니다. 다음 hello 첫 번째 계정으로 blob 하나 계정 toohello에서 장애 조치를 사용 하 여 확장 가능한 장기 저장소 꽉 차면 및 보다 효율적인 쿼리를 승격이 분할 합니다. 

>[!NOTE] 
>Hello 솔루션의이 단계는 적용 가능한 유일한 toobatch 처리 합니다.

입력 및 출력 데이터 데이터 관리:

* hello **출력 데이터** (레이블이 *PartitionedCarEventsTable*) toobe로 유지 되는 오랜 시간에 대 한 hello 기본 / "rawest" 형식의 "데이터 레이크" hello 고객의에서 데이터입니다. 
* hello **입력 데이터** toothis 파이프라인은 일반적으로 무시 hello 출력 데이터의 충실도 toohello 입력-(분할) 보다 잘 후속 사용 하기 위해 방금 저장 됩니다.

![자동차 이벤트 분할 워크플로](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*그림 10 - 자동차 이벤트 분할 워크플로*

hello 원시 데이터에서 "PartitionCarEventsPipeline" HDInsight Hive 활동을 사용 하 여 분할 됩니다. 1 년에 대해 1 단계에서 생성 된 hello 예제 데이터는 YEAR/MONTH로 분할 되므로 hello 파티션은 연도의 매월 (총 12 파티션)에 대 한 사용 되는 toogenerate 차량 신호 및 진단 데이터는입니다. 

![PartitionCarEventsPipeline 작업](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*그림 11 - PartitionCarEventsPipeline*

***PartitionConnectedCarEvents 하이브 스크립트***

hello "partitioncarevents.hql" 이라는 다음 하이브 스크립트 분할에 사용 있고는 hello 다운로드 zip의 hello "\demo\src\connectedcar\scripts" 폴더에 있습니다. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.

![분할된 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*그림 12 - 분할된 출력*

hello 데이터 액세스에 최적화 된 이제는, 좀 더 관리 및 toogain 풍부한 일괄 처리 insights 추가 처리할 준비가 됩니다. 

## <a name="data-analysis"></a>데이터 분석
이 섹션에서는 Azure 스트림 분석 toocombine, Azure 기계 학습, Azure 데이터 팩터리 및 풍부한에 대 한 Azure HDInsight의 고급 표시 분석 차량 상태 및 구동 습관입니다. 다음과 같은 세 개의 하위 섹션이 있습니다.

1. **기계 학습**:이 하위 섹션에서는 유지 관리 및 차량 회수 toosafety 문제 때문에 필요한 서비스 필요한이 솔루션 toopredict 수단을 사용 했습니다 hello 비정상 탐지 실험에 대해 설명 합니다.
2. **실시간 분석**:이 하위 섹션에 대 한 hello 실시간 분석 hello 기계 학습 작업 활용 및 hello 스트림 분석 쿼리 언어를 사용 하 여 사용자 지정 응용 프로그램을 사용 하 여 실시간으로에서 실험 하는 정보를 포함 합니다.
3. **분석을 일괄 처리**:이 하위 섹션 hello Azure HDInsight 및 Azure 데이터 팩터리에서 병원 Azure 기계 학습을 사용 하 여 hello 일괄 처리 데이터를 처리 하 고 변환에 대 한 정보를 포함 합니다.

### <a name="machine-learning"></a>Machine Learning
우리의 목적은 유지 관리 또는 특정 heath 통계에 따라 회수 필요한 toopredict hello 수단입니다. Hello를 다음 가정을 만듭니다.

* Hello 다음 세 가지 조건 중 하나에 해당할 경우 hello 차량 필요 **유지 관리 서비스**:
  
  * 타이어 압력이 낮음
  * 엔진 오일 수준이 낮음
  * 엔진 온도가 높음
* Hello 다음 조건 중 하나에 해당할 경우에 hello 차량 있을 수는 **안전 문제** 필요 **회수**:
  
  * 엔진 온도가 높지만 외부 온도는 낮음
  * 엔진 온도가 낮지만 외부 온도는 높음

Hello 이전 요구 사항에 따라, 만들어져 차량 유지 관리 검색 및 차량 회수 검색에 대 한 두 개의 별도 모델 toodetect 예외. 이러한 두 모델 hello 기본 제공 보안 주체 PCA (주성분 분석) 알고리즘 이상 탐지에 사용 됩니다. 

**유지 관리 감지 모델**

각 조건에 맞는-tire 압력, 엔진 석유 또는 엔진 온도-세 표시기 중 하나 hello 유지 관리 탐지 모델은 비정상 상태를 보고 합니다. 따라서 필요 tooconsider hello 모델 작성에 이러한 세 개의 변수입니다. Azure 기계 학습에서의 실험에서 처음 사용 하 여는 **데이터 집합의 열 선택** 모듈 tooextract 이러한 세 개의 변수입니다. 그런 다음 hello PCA 기반 비정상 검색 모듈 toobuild hello 이상 탐지 모델을 사용합니다. 

주 구성 요소 분석 PCA ()가 적용 된 toofeature 선택, 분류 및 변칙 검색 될 수 있는 기계 학습의 인정 받는 기술입니다. PCA는 가능하면 상관된 변수가 포함된 사례 집합을 주성분이라는 값 집합으로 변환합니다. PCA 기반 모델링의 hello 핵심 아이디어는 기능 및 예외 보다 쉽게 식별할 수 있도록 차원 하위 공간으로 tooproject 데이터입니다.

새로운 각 입력에는 너무 탐지 모델 hello에 대 한 hello 비정상 탐지기 hello 고유 벡터에 프로젝션으로 먼저 계산 하 고 계산 hello 표준화 재구성 오류. 이 정규화 된 오류는 hello 비정상 점수입니다. 더 높은 hello 오류 hello hello 더 비정상적인 hello 인스턴스가합니다. 

검색 문제를 유지 관리 하는 hello 각 레코드 좌표 tire 압력과 엔진 석유 엔진 온도에 정의 된 3 차원 공간에서 지점으로 간주할 수 있습니다. toocapture 이러한 비정상 PCA를 사용 하 여 2 차원 공간 hello hello 3 차원 공간에서 원래 데이터를 프로젝션 할 수 있습니다. 따라서 hello 매개 변수 수가 구성 요소 toouse PCA toobe 2에서에서 설정합니다. 이 매개 변수는 PCA 기반 이상 감지를 적용하는 데 중요한 역할을 합니다. PCA를 사용하여 데이터를 표현하면 이러한 이상을 보다 쉽게 식별할 수 있습니다.

**이상 탐지 모델 회수** hello 회수 이상 탐지 모델을 사용 하 여 hello 데이터 집합과 PCA 기반 비정상 열 선택 비슷한 방법으로 검색 모듈입니다. 처음 세 개의 변수-엔진 온도, 외부 기온, 기 속도-hello를 사용 하 여 추출할 특히 **데이터 집합의 열 선택** 모듈입니다. 또한 hello 속도 포함 변수 hello 엔진 온도 일반적으로 이므로 toohello 속도 상관 관계가 지정 된 합니다. 그런 다음 PCA 기반 비정상 검색 모듈 tooproject hello 데이터를 사용 하 여 hello 3 차원 공간에서으로 2 차원 공간입니다. 충족 하는 hello 회수 조건을 이루어지며 하므로 hello 차량 회수 엔진 온도 및 외부 온도 부정적인 높은 상호 연결 하는 경우. PCA 기반 비정상 검색 알고리즘을 사용 하 여 우리 PCA를 수행한 후 hello 변칙을 캡처할 수 있습니다. 

두 모델을 학습할 때 유지 관리 또는 회수 hello 입력된 데이터 tootrain hello PCA 기반 비정상 검색 모델으로 요구 하지 않는 toouse 일반 데이터 필요 합니다. Hello 실험 점수 매기기, 유지 관리 또는 회수 hello 차량 필요 여부 hello 학습 된 비정상 검색 모델 toodetect을 사용 합니다. 

### <a name="real-time-analysis"></a>실시간 분석
스트림 분석 SQL 쿼리를 수행 하는 hello 사용 되는 모든 tooget hello 평균 hello 차량 속도, 연료 수준, 엔진 온도, 주행 기록 계 읽기, 타이어 압력, 엔진 석유 수준 및 다른 사용자와 같은 중요 한 차량 매개 변수입니다. hello 평균은 사용 되는 toodetect 예외 경고를 발생 하 고 확인 후 toodemographics로 서로 연결 하 고 특정 지역에서 작동 하는 자동차의 전반적인 상태 조건 hello 합니다. 

![실시간 처리를 위한 Stream Analytics 쿼리](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*그림 13 - 실시간 처리를 위한 Stream Analytics 쿼리*

모든 hello 평균 3 초 TumblingWindow에 대해 계산 됩니다. 이 경우 중복되지 않는 연속적인 시간 간격이 필요하므로 TubmlingWindow를 사용합니다. 

Azure 스트림 분석에서 모든 hello "Windowing" 기능에 대해 자세히 toolearn 클릭 [창 작업 (Azure 스트림 분석)](https://msdn.microsoft.com/library/azure/dn835019.aspx)합니다.

**실시간 예측**

응용 프로그램은 실제 시간에서 hello 솔루션 toooperationalize hello 기계 학습 모델의 일부로 포함 합니다. 이 응용 프로그램 "RealTimeDashboardApp" 라는 만들어지고 hello 솔루션 배포의 일부로 구성 됩니다. hello 응용 프로그램에서는 hello 다음을 수행합니다.

1. 여기서 스트림 분석은 이벤트를 게시 hello 패턴에서 지속적으로 tooan 이벤트 허브 인스턴스를 수신 대기 합니다. ![스트림 분석 쿼리 hello 데이터 게시를 위한](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *그림 14-hello 데이터 tooan 게시에 대 한 스트림 분석 쿼리 출력 이벤트 허브 인스턴스* 
2. 이 응용 프로그램이 수신하는 모든 이벤트에 대해 다음을 수행합니다. 
   
   * 시스템 학습 요청-응답 점수 매기기 (RR) 끝점을 사용 하 여 hello 데이터를 처리 합니다. hello RR 끝점 hello 배포의 일부로 자동으로 게시 됩니다.
   * hello RR 출력은 hello 푸시 Api를 사용 하 여 게시 된 tooa Power BI 데이터 집합입니다.

이 패턴을 볼 toointegrate hello 실시간 분석 흐름에 따라 비즈니스 줄 (lob 기간 업무) 응용 프로그램 경고, 알림 및 메시징 등의 시나리오에 적용 가능한 tooscenarios 이기도 합니다.

클릭 [RealtimeDashboardApp 다운로드](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio 솔루션에 대 한 사용자 지정 합니다. 

**tooexecute hello 실시간 대시보드 응용 프로그램**
1. 로컬로 추출 및 저장 ![RealtimeDashboardApp 폴더](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *그림 16 - RealtimeDashboardApp 폴더*  
2. Hello RealtimeDashboardApp.exe 응용 프로그램 실행
3. 유효한 Power BI 자격 증명을 제공하고 로그인한 후 동의를 클릭합니다. ![실시간 대시보드 응용 프로그램 로그인 tooPower 비교 BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![실시간 대시보드 응용 프로그램 로그인 tooPower BI 마침](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*그림 17-RealtimeDashboardApp: 로그인 tooPower BI*

>[!NOTE] 
>Tooflush hello Power BI 데이터 집합을 원하는 경우 hello RealtimeDashboardApp hello "flushdata" 매개 변수를 실행 합니다. 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>일괄 분석
hello 목적은 tooshow Contoso 모터 어떻게 활용 hello Azure 계산 기능 tooharness 빅 데이터 toogain 풍부한 인 사이트에 운전 패턴, 사용량 동작 및 차량 상태입니다. 이를 통해 다음이 가능합니다.

* 운전 습관 및 연료 효율적인 구동 동작에 통찰력을 제공 하 여 더 저렴 하 게 하는 hello 고객 환경 개선
* 고객 및 구동 패턴 toogovern 비즈니스 의사 결정의 사전 확인 하 고 hello를 가장 잘 클래스 제품 및 서비스에 제공

이 솔루션에서는 다음 메트릭을 hello 대상으로 합니다.

1. **전체 업그레이드 동작을 구동**: hello hello 모델, 위치, 구동 조건 및 구동 적극적인 패턴에 대 한 hello 연도 toogain 통찰력의 시간 추세를 식별 합니다. Contoso Motors는 마케팅 캠페인, 주행에 새롭게 개인 설정된 기능 및 사용 현황에 따른 보험에 이를 활용할 수 있습니다.
2. **효율적인 구동 동작 연료**: hello hello 모델, 위치, 구동 조건 및 연료 효율적인 구동 패턴에 대 한 hello 연도 toogain 통찰력 시간의 추세를 식별 합니다. Contoso 모터 이러한 insights를 사용 마케팅 캠페인, 새로운 기능을 구동 하 고 보고 하는 사전 toohello 드라이버에 대 한 유효 및 환경 친숙 한 구동 습관 비용입니다. 
3. **모델을 회수**: 회수 hello 변칙 검색 기계 학습 실험 작업 활용 하 여 필요한 모델 식별

이러한 메트릭의 각 hello 세부 정보를 살펴보겠습니다.

**공격적인 주행 패턴**

hello 차량 신호를 분할 하 고 진단 데이터는 처리 하이브 toodetermine hello 모델, 위치, 자동차를 사용 하 여 "AggresiveDrivingPatternPipeline" 라는 hello 파이프라인에서 구동 조건 및 다른 매개 변수를 보여 주는 적극적인 구동 패턴입니다.

![적극적인 구동 패턴 워크플로](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
 *그림 18 - 적극적인 구동 패턴 워크플로*


***공격적인 주행 패턴 하이브 쿼리***

hello 라는 "aggresivedriving.hql" 적극적인 구동 조건 패턴 분석에 사용 된 Hive 스크립트는 hello 다운로드 zip의 "\demo\src\connectedcar\scripts" 폴더에 있습니다. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


자동차의 전송 기어 위치, 브레이크 페달 상태 및 속도 toodetect 무모/적극적인 브레이크 빠른 속도로 패턴에 따라 동작을 구동의 hello 조합을 사용 합니다. 

Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.

![AggressiveDrivingPatternPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*그림 19 - AggressiveDrivingPatternPipeline 출력*

**연료 효율이 좋은 주행 패턴**

hello 차량 신호를 분할 하 고 진단 데이터는 "FuelEfficientDrivingPatternPipeline" 라는 hello 파이프라인에서 처리 됩니다. 하이브 사용 되는 toodetermine hello 모델, 위치, 자동차를 움직일, 운전 환경 및 연료 효율적인 구동 패턴을 제공 하는 기타 속성도입니다.

![연료 효율이 좋은 주행 패턴](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*그림 20 - 연료 효율이 좋은 주행 패턴 워크플로*

***연료 효율이 좋은 주행 패턴 하이브 쿼리***

hello 라는 "fuelefficientdriving.hql" 적극적인 구동 조건 패턴 분석에 사용 된 Hive 스크립트는 hello 다운로드 zip의 "\demo\src\connectedcar\scripts" 폴더에 있습니다. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


자동차의 전송 기어 위치, 페달 브레이크 상태, 속도 및 가속기 페달 위치 toodetect 연료 브레이크, 가속에 기반 하 여 효율적인 구동 동작 hello 조합을 사용 하 고 패턴 속도입니다. 

Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.

![FuelEfficientDrivingPatternPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*그림 21 - FuelEfficientDrivingPatternPipeline 출력*

**회수 예측**

hello 기계 학습 실험은 프로 비전 및 hello 솔루션 배포의 일부로 웹 서비스로 게시 합니다. hello 일괄 처리 끝점을 점수 매기기 데이터 팩터리에 연결 된 서비스로 등록 하 고 데이터 팩터리 일괄 처리 점수 매기기 활동을 사용 하 여 병원이 워크플로의 활용 하 고 있습니다.

![Machine Learning 끝점](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*그림 22 - Data Factory의 연결된 서비스로 등록된 Machine Learning 끝점*

hello 등록 된 연결 된 서비스에에서 사용 됩니다 hello 이상 탐지 모델을 사용 하 여 hello DetectAnomalyPipeline tooscore hello 데이터. 

![Data Factory에서 Machine Learning 일괄 처리 점수 매기기 활동](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*그림 23 – Data Factory에서 Azure Machine Learning 일괄 처리 점수 매기기 활동* 

웹 서비스를 평가 하는 hello 일괄 처리와 병원 될 수 있도록 데이터 준비에 대 한이 파이프라인에서 수행 하는 몇 가지 단계가 있습니다. 

![회수가 필요한 차량을 예측하기 위한 DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*그림 24 - 회수가 필요한 차량을 예측하기 위한 DetectAnomalyPipeline* 

***변칙 검색 Hive 쿼리***

Hello 점수 매기기가 완료 되 면 사용 되는 tooprocess 및 비정상을 확률 점수로 0.60 이상의 hello 모델에 의해 분류 되는 집계 hello 데이터 HDInsight 활동은.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.

![DetectAnomalyPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*그림 25 – DetectAnomalyPipeline 출력*

## <a name="publish"></a>게시

### <a name="real-time-analysis"></a>실시간 분석
Hello Stream Analytics 작업에서 hello 쿼리 중 하나 게시 hello 이벤트 tooan 출력 이벤트 허브 인스턴스. 

![스트림 분석 작업이 게시 tooan 출력 이벤트 허브 인스턴스](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*그림 26-스트림 분석 작업 게시 tooan 출력 이벤트 허브 인스턴스*

![스트림 분석 쿼리 toopublish toohello 출력 이벤트 허브 인스턴스](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*그림 27-스트림 분석 쿼리 toopublish toohello 출력 이벤트 허브 인스턴스*

이 이벤트 스트림의 RealTimeDashboardApp hello 솔루션에 포함 된 hello에서 사용 됩니다. 이 응용 프로그램 실시간 점수 매기기에 대 한 hello 컴퓨터 학습 요청-응답 웹 서비스를 활용 하며 hello 결과 데이터 tooa Power BI 데이터 집합에 사용 하기 위해 게시 합니다. 

### <a name="batch-analysis"></a>일괄 분석
hello hello 일괄 처리 및 실시간 처리 결과가 소비에 대 한 게시 된 toohello Azure SQL 데이터베이스 테이블입니다. hello Azure SQL Server, 데이터베이스 및 테이블 hello hello 설치 스크립트의 일부로 자동으로 만들어집니다. 

![결과 처리 하는 일괄 처리 복사 toodata 마트 워크플로](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*그림 28-일괄 처리 결과 복사 toodata 마트 워크플로*

![스트림 분석 작업이 toodata 마트 게시](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*그림 29-스트림 분석 작업 toodata 마트 게시*

![Stream Analytics 작업에서 데이터 마트 설정](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*그림 30 - Stream Analytics 작업에서 데이터 마트 설정*

## <a name="consume"></a>사용
Power BI는 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다. 

Hello Power BI 보고서 및 대시보드 hello 설정에 대 한 자세한 내용은 여기를 클릭 합니다. hello 최종 대시보드는 다음과 같습니다.

![Power BI 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*그림 31 - Power BI 대시보드*

## <a name="summary"></a>요약
이 문서에는 hello 차량 원격 분석 분석 솔루션의 자세한 드릴 다운 합니다. 예측 및 동작과 함께 실시간 및 일괄 분석을 위한 람다 아키텍처 패턴을 설명합니다. 이 패턴 tooa 다양 한 범위의 실행 부하 과다 경로 (실시간)를 필요로 하는 사용 사례를 적용 및 콜드 경로 (일괄 처리) 분석 합니다. 

