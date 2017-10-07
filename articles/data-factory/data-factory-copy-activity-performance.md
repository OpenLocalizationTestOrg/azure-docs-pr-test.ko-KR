---
title: "aaaCopy 활동 성능 및 조정 가이드 | Microsoft Docs"
description: "복사 작업을 사용 하면 Azure Data Factory에서 데이터 이동의 hello 성능에 영향을 주는 주요 요인에 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>복사 작업 성능 및 조정 가이드
Azure Data Factory 복사 작업은 최고 수준의 보안, 안정성 및 고성능 데이터 로드 솔루션을 제공합니다. 그 테라바이트의 데이터의 수만 toocopy 매일 풍부한 다양 한 클라우드의 있으며 온-프레미스 데이터 저장소 합니다. 로드 성능을 함으로써 빠른 데이터는 핵심 tooensure hello 코어 "빅 데이터" 문제에 초점을 맞출 수 있습니다: 고급 분석 솔루션을 빌드하고 깊은 통찰력 제공 하는 모든 데이터에서 가져오는 합니다.

Azure 데이터 저장소 및 데이터 웨어하우스 솔루션에서 엔터프라이즈급의 집합을 제공 하 고 복사 작업 경험을 쉽게 tooconfigure 및 설정을 로드 고도로 최적화 된 데이터를 제공 합니다. 단일 복사 작업 만을 사용하여 다음을 수행할 수 있습니다.

* **1.2Gbps** 속도로 **Azure SQL Data Warehouse**에 데이터 로드 - 사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.
* **1.0 Gbps** 속도로 **Azure Blob 저장소**에 데이터 로드
* **1.0 Gbps** 속도로 **Azure Data Lake Store**에 데이터 로드

이 문서에서는 다음을 설명합니다.

* [성능 참조 번호](#performance-reference) 프로젝트; 지원 되는 원본 및 싱크 데이터 저장소 toohelp에 대 한 계획
* 확장 시킬 수 있는 기능을 비롯 한 다양 한 시나리오에서 복사 처리량 hello [데이터 이동을 단위 클라우드](#cloud-data-movement-units), [복사 병렬](#parallel-copy), 및 [복사본을 스테이징](#staged-copy);
* [성능 지침 튜닝](#performance-tuning-steps) tootune hello 성능과 hello 주요 요인을 영향을 줄 수 있는 성능을 복사 하는 방법에 있습니다.

> [!NOTE]
> 복사 작업에 대해 전반적으로 잘 알지 못하는 경우, 이 문서를 읽기 전에 [복사 작업을 사용하여 데이터 이동](data-factory-data-movement-activities.md)을 참조하세요.
>

## <a name="performance-reference"></a>성능 참조

참조로 아래 테이블 수를 보여 줍니다 hello 복사 처리량 MBps 사내 테스트에 원본 및 싱크 쌍을 지정 하는 hello에 대 한 합니다. 비교를 위해 [클라우드 데이터 이동 단위](#cloud-data-movement-units) 또는 [데이터 관리 게이트웨이 확장성](data-factory-data-management-gateway-high-availability-scalability.md)(여러 게이트웨이 노드)의 다른 설정이 어떻게 복사 성능에 도움이 되는지도 설명합니다.

![성능 매트릭스](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**포인트 toonote:**
* 처리량 hello 다음 수식을 사용 하 여 계산 됩니다. [소스에서 읽은 데이터의 크기] / [복사 작업 실행 기간이] 합니다.
* hello 표에 hello 성능 참조 번호를 사용 하 여 측정 된 [TPC H](http://www.tpc.org/tpch/) 실행 하는 단일 복사 활동에서 데이터 집합입니다.
* Hello에는 Azure 데이터 저장소, hello 원본과 싱크가 동일한 Azure 지역에 있습니다.
* 온-프레미스와 클라우드 간의 하이브리드 복사에 대 한 데이터 저장소, 게이트웨이 노드마다 사양 아래 hello 온-프레미스 데이터 저장소와 별도로 했던 컴퓨터에서 실행 되었습니다. 단일 활동 게이트웨이, 실행 중인 경우 hello 복사 작업 hello 테스트 컴퓨터의 CPU, 메모리 또는 네트워크 대역폭의 작은 부분만 사용 합니다. [데이터 관리 게이트웨이에 대한 고려 사항](#considerations-for-data-management-gateway)에서 자세히 알아보세요.
    <table>
    <tr>
        <td>CPU</td>
        <td>32 코어 2.20GHz Intel Xeon E5-2660 v2</td>
    </tr>
    <tr>
        <td>메모리</td>
        <td>128GB</td>
    </tr>
    <tr>
        <td>네트워크</td>
        <td>인터넷 인터페이스: 10Gbps. 인트라넷 인터페이스: 40Gbps</td>
    </tr>
    </table>


> [!TIP]
> 보다 더 큰 데이터 이동을 단위로 (DMUs) hello 활용 하 여 더 높은 처리량을 얻을 수 있는 32 클라우드-클라우드 복사 작업 실행에 대 한 최대 DMUs 기본 합니다. 예를 들어 100개 DMU를 사용하면 **1.0GBps** 속도로 Azure Blob에서 Azure Data Lake Store로 데이터 복사를 수행할 수 있습니다. Hello 참조 [데이터 이동을 단위 클라우드](#cloud-data-movement-units) 섹션이 기능 및 hello에 대 한 세부 정보에 대 한 시나리오를 지원 합니다. 연락처 [Azure 지원](https://azure.microsoft.com/support/) toorequest 자세한 DMUs 합니다.

## <a name="parallel-copy"></a>병렬 복사
Hello에서 데이터 원본 또는 데이터 toohello 대상 쓰기를 읽을 수 **복사 작업 실행 내에서 병렬로**합니다. 이 기능은 복사 작업의 처리량 hello를 향상 되 고 toomove 데이터 hello 시간 줄어듭니다.

이 설정은 hello와에서는 다르며 **동시성** hello 활동 정의에서 속성입니다. hello **동시성** hello 수를 결정 하는 속성 **동시 복사 작업 실행** 각기 다른 활동이 windows에서 tooprocess 데이터 (2 AM too3 AM 3 AM too4 AM, 1 AM too2 AM, 등). 이 기능은 기록 로드를 수행하는 경우 유용합니다. hello 병렬 복사 기능이 적용 tooa **단일 작업 실행**합니다.

샘플 시나리오를 살펴 보겠습니다. 다음 예제는 hello, 지난 hello에서 여러 분할 영역 toobe 처리 필요 합니다. Data Factory는 각 조각에 대한 복사 작업(작업 실행) 인스턴스를 하나 실행합니다.

* hello 첫 번째 작업 창에서 데이터 조각을 hello (1 AM too2 AM) = = > 1을 실행 하는 활동
* hello 두 번째 활동 창에서 데이터 조각을 hello (2 AM too3 AM) = = > 작업 2를 실행 합니다.
* hello 두 번째 활동 창에서 데이터 조각을 hello (3 AM too4 AM) = = > 3을 실행 하는 활동

방식으로 계속됩니다.

이 예제에서는 hello **동시성** 값이 설정 too2, **1을 실행 하는 활동** 및 **2를 실행 하는 활동** 두 개의 작업 창에서 데이터를 복사 **동시에**  tooimprove 데이터 이동 성능입니다. 그러나 여러 개의 파일에 연결 되어 있으면 1을 실행 하는 작업과 hello 데이터 이동 서비스 파일 복사 hello 소스 toohello 대상 한 파일에서 한 번에 합니다.

### <a name="cloud-data-movement-units"></a>클라우드 데이터 이동 단위
A **클라우드 데이터 이동 단위 (DMU)** hello 우위 (CPU, 메모리 및 네트워크 리소스 할당의 조합) Data Factory에 단일 단위를 나타내는 측정값입니다. 클라우드-클라우드 복사 작업에 DMU를 사용할 수 있으며 하이브리드 복사에는 사용할 수 없습니다.

기본적으로 데이터 팩터리는 단일 클라우드 DMU tooperform 단일 복사 작업 실행을 사용 합니다. toooverride이이 기본값 hello에 대 한 값을 지정 **cloudDataMovementUnits** 속성을 다음과 같이 합니다. 에 대 한 내용은 hello 수준 성능 향상의 특정 복사본 원본과 싱크에 대 한 더 많은 단위를 구성할 때 표시 될 수 있습니다 참조 hello [성능 참조](#performance-reference)합니다.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
hello **허용 되는 값** hello에 대 한 **cloudDataMovementUnits** 속성은 1 (기본값), 2, 4, 8, 16, 32입니다. hello **실제 수가 클라우드 DMUs** 데이터 패턴에 따라 hello 구성 값을 보다 작은 같은 tooor은 런타임에 사용 하 여 hello 복사 작업입니다.

> [!NOTE]
> 더 높은 처리량을 위해 더 많은 클라우드 DMU가 필요하면 [Azure 지원](https://azure.microsoft.com/support/)에 문의하시기 바랍니다. 8의 설정 및 이상이 현재 경우에만 작동 하면 **Blob 저장소/데이터 레이크 저장소/Amazon S3/클라우드 FTP/클라우드 SFTP tooBlob/데이터 레이크 저장소/Azure의 저장소에서 여러 파일을 복사 합니다. SQL 데이터베이스**합니다.
>

### <a name="parallelcopies"></a>parallelCopies
Hello를 사용할 수 있습니다 **parallelCopies** 속성 tooindicate hello 병렬 처리를 복사 작업 toouse 되도록 합니다. 이 속성의 hello 소스에서 읽은 병렬로 tooyour 싱크 데이터 저장소를 쓸 수 있는 복사 작업에서 스레드 최대 수로 생각할 수 있습니다.

각 복사 작업 실행에 대 한 데이터 팩터리의 hello 원본 데이터 저장소와 toohello 대상 데이터 저장소에서 toouse toocopy 데이터를 복사 하는 병렬의 hello 수를 결정 합니다. 병렬 복사본을 사용 하 여 hello 기본 수는 원본 및 싱크의 사용 중인 hello 유형에 따라 다릅니다.  

| 원본 및 싱크 | 서비스에 의해 결정되는 기본 병렬 복사 개수 |
| --- | --- |
| 파일 기반 저장소 간에 데이터 복사(Blob 저장소, Data Lake Store, Amazon S3, 온-프레미스 파일 시스템, 온-프레미스 HDFS) |1에서 32 사이. 두 개의 클라우드 데이터 저장소 간에 사용 되는 toocopy 데이터 hello 파일 및 클라우드 데이터 이동 단위 (DMUs) hello 수의 hello 크기에 따라 결정 또는 hello 물리적 구성의 환영 온-프레미스 데이터 저장소에서 (toocopy 데이터 tooor 하이브리드 복사본에 사용 되는 게이트웨이 컴퓨터 ). |
| 데이터 복사 **tooAzure 테이블 저장소를 저장 하는 모든 원본 데이터** |4 |
| 기타 모든 원본 및 싱크 쌍 |1 |

일반적으로 기본 동작 hello를 제공 해야 hello 최상의 처리량입니다. 그러나 toocontrol hello 로드 컴퓨터에서 해당 호스트 데이터 저장소 또는 복사 성능을 얻으려면 tootune, toooverride hello 기본값을 선택 하 고 hello에 대 한 값을 지정 될 수 있습니다 **parallelCopies** 속성입니다. hello 값 1과 32 (둘 다 포함) 사이 여야 합니다. 런타임 시 hello 최상의 성능을 위해 복사 작업을 사용 값 보다 작거나 같은 설정 하는 toohello 값.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
포인트 toonote:

* 파일 기반 저장소 간에 데이터를 복사할 때 hello **parallelCopies** hello 파일 수준에서 병렬 처리 수준 hello를 결정 합니다. 단일 파일 내 hello 청크 했을 때 아래 자동으로 있으며이 뷰어는 지정 된 소스 데이터 저장소에 대 한 toouse hello 가장 적합 한 청크 크기는 병렬 및 직교 tooparallelCopies에 tooload 데이터를 입력 합니다. 런타임 시 hello 복사 작업에 대 한 데이터 이동 서비스 사용 hello 요소가 있는 파일의 hello 수 뿐인 병렬 복사본 hello 실제 수입니다. Hello 복사 동작이 경우 **mergeFile**, 복사 작업 병렬 처리 수준 파일을 사용할 수 없습니다.
* Hello에 대 한 값을 지정 하는 경우 **parallelCopies** 속성에는 하이브리드 복사본 경우 원본 및 싱크 데이터 저장소 및 toogateway hello 부하 증가 고려 합니다. 이런 경우가 특히 있는 경우 여러 활동 또는 hello의 동시 실행에 대해 실행 되는 동일한 활동 hello 동일한 데이터 저장소입니다. Hello 데이터 저장소 또는 게이트웨이 hello 부하로 가득 채워가 발견 한 경우 저하 hello **parallelCopies** 값 toorelieve hello 로드 합니다.
* Hello 데이터 이동 서비스는 hello 무시는 파일 기반 파일 기반 toostores 되지 않는 저장소에서 데이터를 복사할 때 **parallelCopies** 속성입니다. 병렬 처리를 지정하더라도 이 경우에는 적용되지 않습니다.

> [!NOTE]
> 데이터 관리 게이트웨이 버전 1.11 이상이 toouse hello를 사용 해야 **parallelCopies** 하이브리드 복사를 수행 하는 경우 기능을 합니다.
>
>

toobetter 사용 하 여 이러한 두 속성 및 tooenhance 데이터 이동을 처리량 hello를 참조 하십시오 [사용 사례 샘플](#case-study-use-parallel-copy)합니다. Tooconfigure 않아도 **parallelCopies** tootake 활용 hello 기본 동작입니다. 구성을 수행하고 **parallelCopies**가 너무 작은 경우 여러 클라우드 DMU가 완전히 활용되지 않을 수 있습니다.  

### <a name="billing-impact"></a>청구 영향
있기 **중요** hello 복사 작업의 hello 총 시간을 기준으로 요금이 청구 되므로 tooremember 합니다. 복사 작업 사용 경우 tootake 1 시간 한 클라우드 단위와 4 명의 클라우드 단위를 15 분 정도 걸리며 이제, hello 전반적인 청구서 남아 거의 hello 동일 합니다. 예를 들어 4개의 클라우드 단위를 사용합니다. hello 첫 번째 클라우드 단위 데 10 분, hello 두 번째 식, 10 분 hello 세 번째, 5 분, 5 분에 실행 한 복사 작업에 모두 네 번째 hello 합니다. Hello 총 복사본 (데이터 이동) 시간, 즉 10 + 10 + 5 + 5 = 30 분에 대 한 요금이 청구 됩니다. **parallelCopies**의 사용은 청구에 영향을 주지 않습니다.

## <a name="staged-copy"></a>준비된 복사
원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사 하면 준비 중간 저장소로 toouse Blob 저장소를 선택할 수 있습니다. 준비를 비활성화 하는 hello 특히 유용 합니다.

1. **PolyBase 통해 SQL 데이터 웨어하우스로 tooingest 데이터에서 다양 한 데이터 저장소를 원하는**합니다. SQL 데이터 웨어하우스 SQL 데이터 웨어하우스로 처리량이 높은 메커니즘 tooload 많은 양의 데이터도 PolyBase를 사용합니다. 그러나 hello 원본 데이터는 Blob 저장소에 있어야 합니다. 않으며 추가 조건을 충족 해야 합니다. Blob 저장소가 아닌 데이터 저장소에서 데이터를 로드하는 경우 중간 준비 Blob 저장소를 통해 데이터 복사를 활성화할 수 있습니다. 이 경우 데이터 팩터리의 hello 필요한 데이터 변환을 tooensure PolyBase의 hello 요구 사항을 충족 하는지를 수행 합니다. 그런 다음 SQL 데이터 웨어하우스로 PolyBase tooload 데이터를 사용합니다. 자세한 내용은 참조 하십시오. [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse)합니다. 사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.
2. **시간이 걸리는 경우에 따라 하이브리드 데이터 이동 (즉, 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 toocopy) 느린 네트워크 연결을 통해 tooperform**합니다. tooimprove 성능 hello 온-프레미스 데이터를 짧은 시간 toomove 데이터 toohello 준비 데이터 hello 클라우드에 저장을 가지도록 압축할 수 있습니다. 그런 다음 hello 대상 데이터 저장소에 로드 하기 전에 저장소를 준비 하는 hello에 hello 데이터 압축을 해제할 수 있습니다.
3. **Tooopen 포트 이외의 포트 80 및 포트 443을 하려면 방화벽에서 기업 IT 정책 때문에 않으려는**합니다. 예를 들어 온-프레미스 데이터 저장소 tooan Azure SQL 데이터베이스 싱크 또는 Azure SQL 데이터 웨어하우스 싱크에에서 데이터를 복사할 때 tooactivate 아웃 바운드 TCP 통신 포트 1433에서 Windows 방화벽 hello와 회사 방화벽에 대 한 필요 합니다. 이 시나리오에서는 활용 hello 게이트웨이 toofirst 복사본 데이터 tooa Blob 저장소 준비 인스턴스 HTTP 또는 HTTPS를 통한 포트 443에서. 그런 다음 Blob 저장소 준비에서 SQL 데이터베이스 또는 SQL 데이터 웨어하우스를 hello 데이터를 로드 합니다. 이 흐름에서 tooenable 포트 1433 필요는 없습니다.

### <a name="how-staged-copy-works"></a>준비 복사의 작동 방법
첫 번째 hello 데이터가 데이터 저장소를 준비 하는 hello 원본 데이터 저장소 toohello에서 복사 됩니다 hello 준비 기능을 활성화 하면 (bring 직접). 다음으로 hello 데이터는 데이터 저장소 toohello 싱크 데이터 저장소를 준비 하는 hello에서 복사 됩니다. Data Factory 수에 대 한 2 단계 흐름 hello를 자동으로 관리 합니다. 데이터 팩터리는 또한 hello 데이터 이동이 완료 한 후 저장소를 준비 하는 hello에서 임시 데이터를 정리 합니다.

게이트웨이 hello 클라우드 복사 시나리오 (소스와 싱크 데이터 저장소는 hello 클라우드에서)에서 사용 되지 않습니다. 데이터 팩터리 서비스 hello hello 복사 작업을 수행 합니다.

![준비 복사: 클라우드 시나리오](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

Hello 하이브리드 복사 시나리오에서 (소스는 온-프레미스 및 싱크는 hello 클라우드에서) hello 게이트웨이 tooa 준비 데이터 저장소를 저장 하는 hello 원본 데이터에서 데이터를 이동 합니다. 데이터 팩터리 서비스에서 데이터를 준비 하는 hello 데이터 저장 toohello 싱크 데이터 저장소를 이동 합니다. 클라우드 데이터 저장소 tooan에서 데이터 복사 온-프레미스도 스테이징을 통한 데이터 저장소가 되돌릴 hello 흐름에 따라 지원 됩니다.

![준비 복사: 하이브리드 시나리오](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

데이터 이동을 준비 저장소를 사용 하 여을 활성화 하면 데이터 tooan 중간 또는 데이터 저장소를 준비를 저장 하 고는 중간에서 데이터를 이동 하기 전에 다음 압축을 풀 hello 원본에서 데이터를 이동 하기 전에 압축 hello 데이터 toobe 것인지 여부를 지정할 수 있습니다 또는 준비 데이터 저장소 toohello 싱크 데이터 저장소입니다.

현재는 준비 저장소를 사용하여 두 온-프레미스 데이터 저장소 간에 데이터를 복사할 수 없습니다. 곧 사용할 수 있는 옵션 toobe이 예정입니다.

### <a name="configuration"></a>구성
Hello 구성 **enableStaging** 대상 데이터 저장소에 로드 하기 전에 Blob 저장소에 미리 준비 하는 hello 데이터 toobe 것인지 toospecify 복사 작업에서에서 설정 합니다. 설정 하는 경우 **enableStaging** tooTRUE, hello 다음 표에 나열 된 hello 추가 속성을 지정 합니다. 가 없는 하나 toocreate Azure 저장소에 있어야 하거나 저장소 공유 액세스 서명 연결 된 서비스 준비에 대 한 합니다.

| 속성 | 설명 | 기본값 | 필수 |
| --- | --- | --- | --- |
| **enableStaging** |저장소 준비는 중간 통해 toocopy 데이터 있는지 여부를 지정 합니다. |False |아니요 |
| **linkedServiceName** |hello 이름을 지정는 [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) 또는 [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) 연결 된 서비스를 중간 준비 저장소로 사용 하는 저장소의 toohello 인스턴스 참조입니다. <br/><br/> PolyBase 통해 SQL 데이터 웨어하우스에 대 한 공유 액세스 서명 tooload 데이터 저장소를 사용할 수 없습니다. 다른 모든 시나리오에서는 사용할 수 있습니다. |해당 없음 |예, **enableStaging** tooTRUE 설정 |
| **path** |Hello toocontain hello 준비 된 데이터를 지정 하는 Blob 저장소 경로 지정 합니다. 경로 제공 하지 않으면 hello 서비스 컨테이너 toostore 임시 데이터를 만듭니다. <br/><br/> 공유 액세스 서명을 사용 하 여 저장소를 사용 하거나 특정 위치에 임시 데이터 toobe를 필요로 하는 경우에 경로 지정 합니다. |해당 없음 |아니요 |
| **enableCompression** |복사한 toohello 대상 되기 전에 데이터를 압축할지 여부를 지정 합니다. 이 설정은 hello 전송 되는 데이터 양이 줄어듭니다. |False |아니요 |

Hello 테이블 앞에서 설명 하는 hello 속성이 있는 복사 작업에 대 한 샘플 정의 다음과 같습니다.

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>청구 영향
복사 기간 및 복사 유형의 두 단계에 따라 요금이 청구됩니다.

* 사용 하는 경우 준비를 하는 클라우드 복사 (클라우드 데이터 저장소 tooanother 클라우드 데이터 저장소에서 데이터를 복사) 하는 동안 요금이 부과 됩니다 [클라우드 복사 단가] x [1 단계와 2 단계에 대 한 복사 기간 sum] hello 합니다.
* 사용 하는 경우 준비를 하는 하이브리드 복사 (온-프레미스 데이터 저장소 tooa 클라우드 데이터 저장소에서 데이터를 복사) 하는 동안 요금이 부과 됩니다 [하이브리드 복사 기간]에 대 한 [하이브리드 복사 단가] x [클라우드 복사 기간] + x [클라우드 복사 단가].

## <a name="performance-tuning-steps"></a>성능 튜닝 단계
수행 하는 다음이 단계 tootune hello 성능 복사 작업을 사용 하 여 데이터 팩터리 서비스에 유지 하는 것이 좋습니다.

1. **기초 설정**. Hello 개발 단계 대표 데이터 샘플에 대 한 복사 작업을 사용 하 여 파이프라인을 테스트 합니다. Hello Data Factory를 사용할 수 있습니다 [모델을 조각화](data-factory-scheduling-and-execution.md) toolimit hello 양의 데이터를 사용 합니다.

   Hello를 사용 하 여 실행 시간 및 성능 특징을 수집 **모니터링 및 관리 응용 프로그램**합니다. Data Factory 홈페이지에서 **모니터 및 관리**를 선택합니다. Hello 트리 뷰에서 선택 hello **출력 데이터 집합**합니다. Hello에 **활동 창** 목록 hello 복사 작업 실행을 선택 합니다. **활동 창** hello 복사 된 hello 데이터 크기 및 hello 복사 작업 기간을 나열 합니다. hello 처리량에 나열 된 **활동 창 탐색기**합니다. toolearn hello 앱에 대 한 참조 [모니터 및 관리를 사용 하 여 Azure 데이터 팩터리 파이프라인 hello 모니터링 및 관리 응용 프로그램](data-factory-monitor-manage-app.md)합니다.

   ![작업 실행 세부 정보](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Hello 문서의 뒷부분에 나오는 hello 성능과 사용자 시나리오 tooCopy 활동의 구성을 비교할 수 있습니다 [성능 참조](#performance-reference) 이 테스트에서 합니다.
2. **성능 진단 및 최적화**. Hello 성능을 관찰 하기 하지 않는 사용자의 예상을 충족 하는 경우 성능 병목 현상을 tooidentify 해야 합니다. 그런 다음 성능 tooremove 최적화 하거나 병목 현상의 hello 효과 줄이십시오. 성능 진단에 대 한 자세한 내용은이 문서의 hello 범위를 벗어납니다. 하지만 다음은 몇 가지 일반적인 고려 사항:

   * 성능 기능:
     * [병렬 복사](#parallel-copy)
     * [클라우드 데이터 이동 단위](#cloud-data-movement-units)
     * [준비된 복사](#staged-copy)
     * [데이터 관리 게이트웨이 확장성](data-factory-data-management-gateway-high-availability-scalability.md)
   * [데이터 관리 게이트웨이](#considerations-for-data-management-gateway)
   * [원본](#considerations-for-the-source)
   * [싱크](#considerations-for-the-sink)
   * [직렬화 및 역직렬화](#considerations-for-serialization-and-deserialization)
   * [압축](#considerations-for-compression)
   * [열 매핑](#considerations-for-column-mapping)
   * [기타 고려 사항](#other-considerations)
3. **Hello 구성 tooyour 전체 데이터 집합 확장**합니다. Hello 실행 결과 성능 만족 하는 경우 hello 정의 확장 하 고 파이프라인 활성 기간 toocover 전체 데이터 집합 수 있습니다.

## <a name="considerations-for-data-management-gateway"></a>데이터 관리 게이트웨이에 대한 고려 사항
**게이트웨이 설치**: 전용된 컴퓨터 toohost 데이터 관리 게이트웨이 사용 하는 것이 좋습니다. [데이터 관리 게이트웨이에 대한 고려 사항](data-factory-data-management-gateway.md#considerations-for-using-gateway)을 참조하세요.  

**게이트웨이 모니터링 및 위쪽/확장**: 하나 이상의 게이트웨이 노드가 포함 된 단일 논리 게이트웨이 여러 복사 작업을 사용할 수 있습니다 hello에서 실행 이와 동시에 합니다. 정선 hello hello Azure 포털에에서 대 한 제한 및를 실행 하는 동시 작업 수 참조 된 게이트웨이 컴퓨터에서 리소스 사용률 (CPU, 메모리, network(in/out) 등)의 거의 실시간으로 스냅숏을 볼 수 있습니다 [hello 포털모니터게이트웨이](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). 많은 수의 동시 복사본 활동을 실행 또는 많은 양의 데이터 toocopy 하이브리드 데이터 이동을에 많이 필요한 경우 너무 하십시오[수직 또는 수평 확장 게이트웨이](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) 따라서 toobetter로 리소스를 활용 하거나 tooprovision 더 많은 리소스 tooempower 복사 합니다. 

## <a name="considerations-for-hello-source"></a>Hello 소스에 대 한 고려 사항
### <a name="general"></a>일반
데이터 저장소를 기본 해당 hello 또는에 대해 실행 되는 다른 워크 로드 초과 하지 않고 확인 해야 합니다.

Microsoft 데이터 저장소에 대 한 참조 [모니터링 및 튜닝 항목](#performance-reference) 특정 toodata 저장소 및 성능 특성을 저장, 응답 시간을 최소화 및 처리량을 최대화 데이터를 이해 하는 도움말은입니다.

사용 하 여 Blob 저장소 tooSQL 데이터 웨어하우스에서에서 데이터를 복사 하는 경우 고려 **PolyBase** tooboost 성능입니다. 참조 [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) 대 한 자세한 내용은 합니다. 사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.

### <a name="file-based-data-stores"></a>파일 기반 데이터 저장소
*(Blob 저장소, Data Lake Store, Amazon S3, 온-프레미스 파일 시스템, 온-프레미스 HDFS 포함)*

* **평균 파일 크기 및 파일 개수**: 복사 작업은 데이터를 한 번에 하나씩 전송합니다. 와 같은 양의 데이터 toobe 이동 hello, hello 전반적인 처리량이 낮습니다 hello 데이터 각 파일에 대 한 toohello 부트스트랩 단계 인해 몇 개의 큰 파일 대신 작은 많은 파일의 구성 된 경우. 따라서 가능 하면 결합 작은 파일 더 큰 파일 toogain 처리량을 더 합니다.
* **파일 형식 및 압축**: 자세한 방법으로 tooimprove 성능에 대 한 참조 hello [serialization 및 deserialization에 대 한 고려 사항](#considerations-for-serialization-and-deserialization) 및 [압축에 대 한 고려 사항](#considerations-for-compression) 섹션입니다.
* Hello에 대 한 **온-프레미스 파일 시스템** 시나리오는 **데이터 관리 게이트웨이** 는 hello 참조 필요한 [데이터 관리 게이트웨이에 대 한 고려 사항](#considerations-for-data-management-gateway) 섹션.

### <a name="relational-data-stores"></a>관계형 데이터 저장소
*(SQL Database, SQL Data Warehouse, Amazon Redshift, SQL Server 데이터베이스, Oracle, MySQL, DB2, Teradata, Sybase, PostgreSQL 데이터베이스 등 포함)*

* **데이터 패턴**: 테이블 스키마는 복사본 처리량에 영향을 줍니다. 행 크기가 크면 작은 행 크기 보다 더 나은 성능을 제공, toocopy hello 동일한 양의 데이터입니다. hello 이유는 해당 hello 데이터베이스 적은 수의 행을 포함 하는 데이터의 더 적은 일괄 처리를 보다 효율적으로 검색할 수 있습니다.
* **쿼리 또는 저장된 프로시저**: hello 쿼리 또는 hello 복사 활동 소스 toofetch 데이터에서 보다 효율적으로 지정 하는 저장된 프로시저의 hello 논리를 최적화 합니다.
* 에 대 한 **온-프레미스 관계형 데이터베이스**, SQL Server 및 Oracle hello를 사용 해야 **데이터 관리 게이트웨이**, hello 참조 [데이터 관리 게이트웨이에대한고려사항](#considerations-on-data-management-gateway) 섹션.

## <a name="considerations-for-hello-sink"></a>Hello 싱크에 대 한 고려 사항
### <a name="general"></a>일반
데이터 저장소를 기본 해당 hello 또는에 대해 실행 되는 다른 워크 로드 초과 하지 않고 확인 해야 합니다.

Microsoft 데이터 저장소에 대 한 참조 너무[모니터링 및 튜닝 항목](#performance-reference) 하는 특정 toodata 저장소입니다. 이러한 항목에는 데이터 저장소 성능 특징과 toominimize 적당 한 시간 방법을 이해 하 고 처리량을 최대화 데 도움이 됩니다.

데이터를 복사 하는 경우 **Blob 저장소** 너무**SQL 데이터 웨어하우스**를 사용 하는 것이 좋습니다 **PolyBase** tooboost 성능입니다. 참조 [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) 대 한 자세한 내용은 합니다. 사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.

### <a name="file-based-data-stores"></a>파일 기반 데이터 저장소
*(Blob 저장소, Data Lake Store, Amazon S3, 온-프레미스 파일 시스템, 온-프레미스 HDFS 포함)*

* **복사 동작**: 다른 파일 기반 데이터 저장소에서 데이터를 복사할 경우 복사 작업 세 가지 옵션이 hello 통해 **copyBehavior** 속성입니다. 계층 구조를 유지하고 평면화하며 파일을 병합합니다. 유지 또는 계층 구조를 평면화에 거의 없거나 전혀 없이 성능 오버 헤드가 되지만 파일 병합 성능 오버 헤드 tooincrease 됩니다.
* **파일 형식 및 압축**: 참조 hello [serialization 및 deserialization에 대 한 고려 사항](#considerations-for-serialization-and-deserialization) 및 [압축에 대 한 고려 사항](#considerations-for-compression) 자세한 방법으로 tooimprove 성능에 대 한 섹션 .
* **Blob 저장소**: 현재 Blob 저장소는 최적화된 데이터 전송 및 처리량에 대해서만 블록 Blob를 지원합니다.
* 에 대 한 **온-프레미스 파일 시스템** hello 사용 해야 하는 시나리오 **데이터 관리 게이트웨이**, hello 참조 [데이터 관리 게이트웨이에 대 한 고려 사항](#considerations-for-data-management-gateway) 섹션.

### <a name="relational-data-stores"></a>관계형 데이터 저장소
*(SQL Database, SQL Data Warehouse, SQL Server 데이터베이스 및 Oracle 데이터베이스 포함)*

* **복사 동작**: hello 속성의 설정에 따라 **sqlSink**, 복사 작업 다양 한 방식에서 toohello 대상 데이터베이스 데이터를 씁니다.
  * 기본적으로 hello 데이터 이동 서비스 사용의 hello 대량 복사 API tooinsert 데이터 추가 모드를 제공 하는 최상의 성능을 hello 합니다.
  * Hello 싱크에서 저장된 프로시저를 구성 하는 경우 hello 데이터베이스 대량 로드를 대신 한 번에 한 행씩 hello 데이터를 적용 합니다. 성능이 크게 저하됩니다. 데이터 집합을 해당 하는 경우에 큰 경우 toousing hello 전환 고려 **sqlWriterCleanupScript** 속성입니다.
  * Hello를 구성 하는 경우 **sqlWriterCleanupScript** 각 복사 작업에 대 한 속성을 실행 하 고 hello 서비스 트리거 hello 스크립트를 hello 대량 복사 API tooinsert hello 데이터를 사용 합니다. 예를 들어 toooverwrite hello 최신 데이터가 포함 된 전체 테이블을 hello를 hello 원본의 hello 새 데이터를 대량 로드 하기 전에 모든 레코드를 삭제 하는 스크립트 toofirst을 지정할 수 있습니다.
* **데이터 패턴 및 배치 크기**:
  * 테이블 스키마는 복사본 처리량에 영향을 줍니다. toocopy hello 동일한 양의 데이터, 행 크기가 크면 하면 작은 행 크기 보다 더 나은 성능을 hello 데이터베이스 데이터의 더 적은 일괄 처리를 보다 효율적으로 커밋할 수 때문에 있습니다.
  * 복사 작업은 일련의 배치로 데이터를 삽입합니다. Hello를 사용 하 여 일괄 처리의 행 수가 hello를 설정할 수 있습니다 **writeBatchSize** 속성입니다. 데이터에 작은 행이 hello를 설정할 수 있습니다 **writeBatchSize** 일괄 처리 오버 헤드가 더 높은 처리량을 높은 값 toobenefit 사용 하 여 속성입니다. 데이터의 hello 행 크기가 큰 경우 주의 해야 늘리면 **writeBatchSize**합니다. 값이 크면 tooa 복사에 실패 했습니다. hello 데이터베이스 오버 로드 하 여 발생할 수 있습니다.
* 에 대 한 **온-프레미스 관계형 데이터베이스** SQL Server, Oracle, hello를 사용 해야 하는 등의 **데이터 관리 게이트웨이**, hello 참조 [데이터 관리 게이트웨이에대한고려사항](#considerations-for-data-management-gateway) 섹션.

### <a name="nosql-stores"></a>NoSQL 저장소
*(테이블 저장소 및 Azure Cosmos DB 포함)*

* **테이블 저장소**:
  * **파티션**: 크게 데이터 toointerleaved 파티션 작성 하면 성능이 저하 됩니다. Hello 데이터 삽입 되도록 효율적으로 하나의 파티션으로 서로 파티션 키에 따라 원본 데이터를 정렬 하거나 hello 논리 toowrite hello 데이터 tooa 단일 파티션에 조정 합니다.
* **Azure Cosmos DB**의 경우:
  * **일괄 처리 크기**: hello **writeBatchSize** 속성 toohello Azure Cosmos DB 서비스 toocreate 문서 hello 병렬 요청 수를 설정 합니다. 늘리면 성능 향상을 기대할 수 있는 **writeBatchSize** 더 많은 병렬 요청 tooAzure Cosmos DB 전송 되기 때문에 있습니다. 그러나 tooAzure Cosmos DB를 쓸 때의 제한에 대 한 감시 (hello 오류 메시지는 "요청 빈도가 높습니다."). 다양 한 요인 으로부터 대상 컬렉션의 인덱싱 정책을 hello 및 문서 크기를 비롯 하 여 hello hello 문서에서 용어 수가 제한 발생할 수 있습니다. 복사 처리량이 늘어나며 tooachieve, 예를 들어 S3 더 나은 모음을 사용 하는 것이 좋습니다.

## <a name="considerations-for-serialization-and-deserialization"></a>직렬화 및 역직렬화에 대한 고려 사항
입력 데이터 집합 또는 출력 데이터 집합이 파일인 경우 직렬화 및 역직렬화가 발생할 수 있습니다. 복사 작업에서 지원하는 파일 형식에 대한 세부 정보는 [지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.

**복사 동작**:

* 파일 기반 데이터 저장소 간에 파일 복사:
  * 입력 및 출력 데이터 집합 둘 다 동일 또는 없고의 파일 형식 설정, 데이터 이동 서비스 hello hello 하는 경우 모든 serialization 또는 deserialization을 수행 하지 않고 이진 복사본을 실행 합니다. 어떤 hello 원본 및 싱크 파일 형식 설정은 서로 다릅니다는 더 높은 처리량 비교 toohello 시나리오를 표시 됩니다.
  * 때 입력 하 고 출력 데이터 집합이 두 유일한 hello 인코딩 및 텍스트 형식에는 형식이 다르면, hello 데이터 이동 서비스에만 인코딩 변환을 수행 합니다. 모든 serialization을 수행 하지 및 몇 가지 성능 오버 헤드를 발생 시키는 deserialization tooa 이진 복사를 비교 합니다.
  * 입력 및 출력 데이터 집합 둘 다가 다른 파일 형식 또는 구분 기호 등의 다양 한 구성 데이터 이동 서비스 hello 경우 역직렬화 원본 데이터 toostream, 변환 및 다음 지정한 hello 출력 형식으로 serialize 합니다. 이 작업을 훨씬 더 상당한 성능 오버 헤드의 결과로 tooother 시나리오를 비교합니다.
* 없는 파일 기반 (예: 파일 기반 저장소 tooa 관계형 저장소)에서 데이터 저장소에서 파일을 복사할 때 hello serialization 또는 deserialization 단계는 필요 합니다. 이 단계로 상당한 성능 오버헤드가 발생합니다.

**파일 형식**: 선택한 hello 파일 형식에는 복사 성능이 영향을 줄 수 있습니다. 예를 들어 Avro는 데이터를 사용하여 메타데이터를 저장하는 간단한 이진 형식입니다. 한 폭넓은 지원을 hello Hadoop 에코 시스템을 처리 하 고 쿼리를 포함 합니다. 그러나 Avro는 serialization 및 deserialization, 낮은 복사 처리량 결과적 tootext 형식 비교에 대 한 더 비쌉니다. Hello 전체적 처리 흐름 전체에서 파일 형식을 선택을 하십시오. 시작 양식 hello 데이터에 저장 됩니다, 그리고 데이터 저장소 또는 toobe; 외부 시스템에서 추출 된 원본 저장소, 분석 처리 및 쿼리;에 대 한 hello 가장 적절 한 형식 및 어떤 형식으로 보고 및 시각화 도구에 대 한 데이터 마트에 hello 데이터를 내보냅니다. 경우에 따라 변수가 스니핑 하는 파일 형식 읽기 및 쓰기 성능 수에 적합 한 선택 고려할 때 hello 전체 분석 프로세스입니다.

## <a name="considerations-for-compression"></a>압축에 대한 고려 사항
파일이 입력 또는 출력 데이터 집합을 사용 하는 경우 toohello 대상 데이터를 쓸 때 복사 작업 tooperform 압축 하거나 압축을 설정할 수 있습니다. 압축을 선택할 때 입력/출력(I/O) 및 CPU 간에 균형을 유지합니다. 계산 리소스의 추가 비용 hello 데이터를 압축 합니다. 대신에, 네트워크 I/O 및 저장소는 감소합니다. 데이터에 따라 전체 복사 처리량이 향상되는 것을 볼 수 있습니다.

**코덱**: 복사 작업에서는 gzip, bzip2 및 Deflate 압축 형식을 지원합니다. Azure HDInsight에서는 처리를 위해 세 가지 형식을 모두 사용할 수 있습니다. 압축 코덱에는 각각 장점이 있습니다. 예를 들어, bzip2 hello 가장 낮은 복사 처리량을 갖지만 처리를 위해 나눌 수 있으므로 bzip2로 hello 최적의 하이브 쿼리 성능을 얻습니다. Gzip hello 분산 된 가장 옵션을 사용 되며 사용은 가장 자주 hello 합니다. 종단 간 시나리오에 가장 적합 한 hello 코덱을 선택 합니다.

**수준**: 각 압축 코덱의 경우 빠른 압축 및 최적 압축이라는 두 옵션 중에서 선택할 수 있습니다. hello 빠른 압축된 옵션 hello 데이터 압축을 최대한 빨리 hello 결과 파일 최적으로 압축 되지 않은 경우에 합니다. hello 최적으로 압축 된 압축 하는 데 더 많은 시간이 소비 옵션과 아주 적은 양의 데이터를 생성 합니다. 케이스에 전체 더 나은 성능을 제공 하는 두 옵션 toosee를 테스트할 수 있습니다.

**고려 사항**: toocopy 많은 양의 데이터를 온-프레미스 저장소와 hello 클라우드 간에 중간 blob 저장소를 사용 하 여 압축 된 것이 좋습니다. 중간 저장소를 사용 하 여 회사 네트워크와 Azure 서비스의 hello 대역폭 hello 제한 요소가 있고 hello 데이터 집합 입력 및 출력 데이터는 압축 되지 않은 형식 모두 toobe 설정 하려는 경우 유용 합니다. 보다 자세히, 단일 복사 작업을 두 개의 복사 작업으로 나눌 수 있습니다. hello 첫 번째 복사 활동에서 복사본 hello 소스 tooan 중간 또는 압축 된 형태로에 blob를 준비 합니다. hello 두 번째 복사본 활동 스테이징에서 hello 압축 데이터를 복사한 다음 toohello 싱크를 쓰는 동안 압축을 풉니다.

## <a name="considerations-for-column-mapping"></a>열 매핑에 대한 고려 사항
Hello를 설정할 수 있습니다 **columnMappings** 모든 복사 작업 toomap 또는 hello의 하위 집합에서 속성 열 toohello 출력 열을 입력 합니다. Hello 데이터 이동 서비스는 hello 소스에서 hello 데이터를 읽고, 후 hello 데이터 toohello 싱크를 쓰기 전에 tooperform 열 매핑을 hello 데이터에 필요 합니다. 이 추가 처리는 복사 처리량을 감소시킵니다.

원본 데이터 저장소 쿼리 가능한 경우, 예를 들어 SQL 데이터베이스 또는 SQL Server와 같은 관계형 저장소 또는 테이블 저장소 또는 Azure Cosmos DB와 같은 NoSQL 저장소가 경우 밀어넣으려고 hello 열 필터링 및 논리 toohello 다시 정렬을 **쿼리**  열 매핑을 사용 하는 대신 속성입니다. 이러한 방식으로 hello 프로젝션 hello 데이터 이동 서비스 읽는 것이 훨씬 더 효율적 hello 원본 데이터에서 데이터를 저장 하는 동안 발생 합니다.

## <a name="other-considerations"></a>기타 고려 사항
크기 조정 하는 경우 hello toocopy 대형 이면 조정할 수 있습니다 사용할 데이터를 사용 하 여 비즈니스 논리 toofurther 파티션 hello 데이터 hello 데이터 팩터리의 조각화 메커니즘 작업을 수행 합니다. 그런 다음 복사 작업 toorun 더 자주 실행 하는 각 복사 작업에 대 한 tooreduce hello 데이터 크기를 예약 합니다.

사용할 데이터 집합 및 데이터 팩터리의 tooconnector toohello 필요한 복사 작업 hello 수에 대해 주의 동일한 데이터에 저장할 hello 동일 시간. 많은 동시 복사 작업 수 데이터 저장소 제한 및 toodegraded 성능 리드, 내부 재시도 작업을 복사 하 고 경우에 따라 실행 실패 합니다.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>샘플 시나리오: 온-프레미스 SQL Server tooBlob 저장소에서 복사
**시나리오**: 파이프라인 toocopy 데이터는 온-프레미스 SQL Server tooBlob 저장소를 CSV 형식에서 만들어집니다. toomake 복사 작업을 더 빠르게 hello, bzip2 형식으로 hello CSV 파일을 압축 해야 합니다.

**테스트 및 분석**: 복사 작업의 hello 처리량은 2 개 미만인 MBps hello 성능 벤치 마크 보다 훨씬 느립니다입니다.

**성능 분석 및 튜닝**: tootroubleshoot hello 성능 문제, hello 데이터는 처리 하 고 이동 하는 방법에 대해 살펴보겠습니다.

1. **데이터 읽기**: 게이트웨이 서버는 연결 tooSQL 열리고 보냅니다 hello 쿼리 합니다. SQL Server hello 데이터 스트림 tooGateway hello 인트라넷을 통해 전송 하 여 응답 합니다.
2. **직렬화 하 고 데이터를 압축**: 게이트웨이 hello 데이터 스트림 tooCSV 형식으로 serialize 하 고 압축 데이터 tooa bzip2 스트림을 hello 합니다.
3. **데이터 쓰기**: 게이트웨이 hello bzip2 스트림 tooBlob 저장소 hello 인터넷을 통해 업로드 합니다.

볼 수 있듯이 되는 hello 데이터 처리 및 스트리밍 순차적으로 이동: SQL Server > LAN > 게이트웨이 > WAN > Blob 저장소입니다. **hello 전반적인 성능에 의해 제어 되므로 hello 최소 처리량 hello 파이프라인에서**합니다.

![데이터 흐름](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

하나 이상의 요소를 다음 hello hello 성능 병목 현상이 발생할 수 있습니다.

* **원본**: SQL Server 자체가 과도한 로드로 인해 처리량이 낮아집니다.
* **데이터 관리 게이트웨이**:
  * **LAN**: 게이트웨이 hello SQL Server 컴퓨터에 크게 못 미치는 있고 낮은 대역폭 연결 되어 있습니다.
  * **게이트웨이**: 게이트웨이 작업을 수행 하는 부하 제한 사항 tooperform hello에 도달 했습니다.
    * **Serialization**: hello 데이터 스트림 tooCSV를 직렬화 하는 작업 형식에는 처리량이 저하 됩니다.
    * **압축**: 느린 압축 코덱을 선택했습니다(예: Core i7 2.8MBps의 bzip2).
  * **WAN**: hello 회사 네트워크와 Azure 서비스 간의 hello 대역폭은 낮은 (예를 들어 T1 = 1,544 kbps; T 2 = 6312 kbps)입니다.
* **싱크**: Blob 저장소의 처리량이 낮습니다. (이 시나리오에서는 해당 SLA가 최소 60MBps를 보장하므로 가능성이 없습니다.)

이 경우 bzip2 데이터 압축 hello 전체 파이프라인 저하 될 수 있습니다. Tooa gzip 압축 코덱 전환이 병목을 쉬워질 수 있습니다.

## <a name="sample-scenarios-use-parallel-copy"></a>샘플 시나리오: 병렬 복사본 사용
**시나리오 i:** hello 온-프레미스 파일 시스템 tooBlob 저장소에서 1, 000 1MB 파일을 복사 합니다.

**분석 및 성능 조정**: 예를 들어, 쿼드 코어 컴퓨터에서 게이트웨이 설치한 경우 데이터 팩터리의 파일을 사용 하 16 병렬 복사본 toomove hello 파일 시스템 tooBlob 저장소에서 동시에 합니다. 이 병렬 실행 결과, 높은 처리량이 발생합니다. 도 지정 하면 hello 병렬 복사본 수입니다. 다수의 작은 파일을 복사하는 경우, 병렬 복사는 리소스를 보다 효과적으로 활용하여 처리량을 급격히 향상시키는 데 유용합니다.

![시나리오 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**시나리오 II**: Blob 저장소 tooData Lake 저장소 분석에서에서 500 m B의 20 blob를 복사한 다음 성능을 조정 합니다.

**분석 및 성능 조정**:이 시나리오에서는 데이터 팩터리의 hello에서에서 데이터를 복사 Blob 저장소 tooData Lake 저장소 단일 복사본을 사용 하 여 (**parallelCopies** too1 설정) 및 단일 클라우드 데이터 이동 단위입니다. hello 처리량을 관찰 하기는 hello에 설명 된 닫기 toothat [성능 참조 섹션](#performance-reference)합니다.   

![시나리오 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**시나리오 III**: 개별 파일 크기는 수십 MB를 초과하며 총 볼륨은 큽니다.

**분석 및 성능 켜는**: 증가 **parallelCopies** 단일 클라우드 DMU hello 리소스 제한 되어 있으므로 복사 성능이 향상 될 하지 않습니다. 대신 지정 해야 더 많은 클라우드 DMUs tooget 더 많은 리소스 tooperform hello 데이터 이동 합니다. Hello에 대 한 값을 지정 하지 않으면 **parallelCopies** 속성입니다. Data Factory 수에 대 한 hello 병렬 처리를 처리합니다. 이렇게 설정 하면 **cloudDataMovementUnits** too4, 대의 처리량 4 번 발생 합니다.

![시나리오 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>참조
성능 모니터링 및 지원 hello 데이터 저장소의 일부에 대 한 참조를 튜닝 다음과 같습니다.

* Azure Storage(Blob 저장소 및 테이블 저장소 포함): [Azure Storage 확장성 목표](../storage/common/storage-scalability-targets.md) 및 [Azure Storage 성능 및 확장성 검사 목록](../storage/common/storage-performance-checklist.md)
* Azure SQL 데이터베이스: 있습니다 수 [hello 성능을 모니터링](../sql-database/sql-database-single-database-monitor.md) hello 데이터베이스 트랜잭션 단위 (DTU) 비율을 확인 하 고
* Azure SQL Data Warehouse: 해당 기능은 DWU(데이터 웨어하우스 단위)로 측정됩니다. [Azure SQL Data Warehouse의 계산 능력 관리(개요)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)를 참조하세요.
* Azure Cosmos DB: [Azure Cosmos DB의 성능 수준](../documentdb/documentdb-performance-levels.md)
* 온-프레미스 SQL Server: [성능에 대한 모니터링 및 튜닝](https://msdn.microsoft.com/library/ms189081.aspx)
* 온-프레미스 파일 서버: [파일 서버에 대한 성능 튜닝](https://msdn.microsoft.com/library/dn567661.aspx)
