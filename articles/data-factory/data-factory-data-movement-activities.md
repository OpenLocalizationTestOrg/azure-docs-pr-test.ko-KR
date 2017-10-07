---
title: "복사 작업을 사용 하 여 aaaMove 데이터 | Microsoft Docs"
description: "Data Factory 파이프라인에서 데이터를 이동하는 방법(클라우드 저장소 간/온-프레미스 저장소와 클라우드 저장소 간에 데이터 마이그레이션)에 대해 알아봅니다. 또한 복사 활동을 사용하는 방법을 살펴봅니다."
keywords: "데이터 복사, 데이터 이동, 데이터 마이그레이션, 데이터 전송"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>복사 활동을 사용하여 데이터 이동
## <a name="overview"></a>개요
Azure Data Factory에서 온-프레미스와 클라우드 간 toocopy 데이터 복사 작업을 사용할 수 있습니다 데이터 저장소입니다. Hello 데이터 복사 된 후 추가 변환 하 고 수 분석 합니다. 또한 business intelligence (BI) 및 응용 프로그램 소비에 대 한 복사 작업 toopublish 변환 및 분석 결과 사용할 수 있습니다.

![복사 활동의 역할](media/data-factory-data-movement-activities/copy-activity.png)

복사 활동은 안전성, 안전성, 확장성이 뛰어나며 [전 세계에서 사용 가능한 서비스](#global)를 통해 제공됩니다. 이 문서는 Data Factory 및 복사 작업에서 데이터 이동에 대한 세부 정보를 제공합니다.

먼저 두 개의 클라우드 데이터 저장소 간, 그리고 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 이루어지는 데이터 마이그레이션 방식에 대해 살펴보겠습니다.

> [!NOTE]
> 활동에 대 한 toolearn 일반적으로 참조 [이해 파이프라인 및 활동](data-factory-create-pipelines.md)합니다.
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>두 클라우드 데이터 저장소 간의 데이터 복사
소스와 싱크 데이터 저장소 hello 클라우드의 경우 복사 작업은 hello 소스 toohello 싱크에서 같은 단계 toocopy 데이터가 hello 설명 합니다. 복사 작업을 구동 하는 hello 서비스:

1. Hello 원본 데이터 저장소에서 데이터를 읽습니다.
2. 직렬화/역직렬화, 압축/압축 해제, 열 매핑 및 형식 변환을 수행합니다. Hello 입력된 데이터 집합, 출력 데이터 집합 및 복사 작업의 hello 구성에 따라 이러한 작업을 수행 합니다.
3. 데이터 toohello 대상 데이터 저장소를 씁니다.

hello 서비스는 hello 최적의 지역 tooperform hello 데이터 이동을 자동으로 선택 합니다. 이 영역은 일반적으로 hello 한 가장 가까운 toohello 싱크 데이터 저장소입니다.

![클라우드 간 복사](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간 데이터 복사
온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 toosecurely 이동 데이터가 온-프레미스 컴퓨터에 데이터 관리 게이트웨이 설치 합니다. 데이터 관리 게이트웨이는 하이브리드 데이터 이동 및 처리를 수행할 수 있도록 하는 에이전트입니다. Hello hello 데이터 저장소에서 자체 하므로 동일한 컴퓨터 또는 저장 toohello 데이터 액세스를 가진 별도 컴퓨터에 설치할 수 있습니다.

이 시나리오에서는 데이터 관리 게이트웨이 hello serialization/deserialization, 압축/압축 풀기, 열 매핑를 실행 하 고 형식 변환 합니다. 데이터는 hello Azure 데이터 팩터리 서비스를 통해 전달 되지 않습니다. 대신, 데이터 관리 게이트웨이 hello 데이터 toohello 대상 저장소를 직접 작성합니다.

![온-프레미스 및 클라우드 간 복사](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

데이터 이동에 대한 소개와 연습은 [온-프레미스 및 클라우드 데이터 저장소 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요. 이 에이전트에 대한 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 를 참조하세요.

데이터를 이동할 수도 있습니다 / toosupported 데이터를 저장 하는 데이터 관리 게이트웨이 사용 하 여 Azure IaaS 가상 컴퓨터 (Vm)에서 호스팅됩니다. 이 경우에 데이터 관리 게이트웨이 설치할 수 있습니다 hello 데이터 저장소 자체에서 또는 저장 toohello 데이터 액세스를 가진 별도 VM에서 동일한 VM hello 합니다.

## <a name="supported-data-stores-and-formats"></a>지원되는 데이터 저장소 및 형식
복사 활동 Data Factory에는 원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사합니다. 데이터 팩터리 hello 다음 데이터 저장소를 지원 합니다. 데이터 소스에서 tooany 싱크를 작성할 수 있습니다. 데이터 저장소 toolearn 방법을 클릭 해당 저장소에서 데이터 tooand toocopy 합니다.

> [!NOTE] 
> Toomove 데이터 복사 작업을 지원 하지 않는 데이터 저장소에서 필요한 경우 사용 된 **사용자 지정 활동** 를 데이터 복사/이동 하기 위한 사용자 논리로 데이터 팩터리에서 합니다. 사용자 지정 활동을 만들고 사용하는 방법에 대한 자세한 내용은 [Azure Data Factory 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md)을 참조하세요.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 데이터 저장소와 * 온-프레미스 될 수 있습니다 또는 Azure IaaS에서 고 tooinstall 있어야 하며 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 에-프레미스/Azure IaaS 컴퓨터에 있습니다.

### <a name="supported-file-formats"></a>지원 파일 형식
복사 작업에도 사용할 수 있습니다**파일을 다음으로 복사-은** 두 파일 기반 데이터 저장소 간의 hello를 건너뛸 수 있습니다 [섹션 서식을](data-factory-create-datasets.md) 에 모두 hello 입력 및 출력 데이터 집합의 정의 합니다. hello 데이터가 모든 직렬화/역직렬화 하지 않고 효율적으로 복사 됩니다.

복사 활동도에서 읽고 씁니다 toofiles 지정 된 형식으로: **텍스트, JSON, Avro, ORC, 및 Parquet**, 및 압축 코덱 **GZip, Deflate, BZip2 및 ZipDeflate** 지원 됩니다. 자세한 내용은 [지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.

수행할 수는 예를 들어 hello 다음 활동을 복사 합니다.

* 온-프레미스 SQL Server에서 데이터를 복사한 ORC 형식에서 tooAzure 데이터 레이크 저장소를 작성 합니다.
* 온-프레미스 파일 시스템에서 텍스트 (CSV) 형식에서 파일을 복사 하 고 Avro 형식에서 tooAzure Blob를 작성 합니다.
* 온-프레미스 파일 시스템에서 압축 된 파일을 복사 하 고 압축을 푸는 다음 tooAzure 데이터 레이크 저장소를 배치 합니다.
* Azure Blob에서 GZip 압축 된 텍스트 (CSV) 형식으로 데이터를 복사 하 고 tooAzure SQL 데이터베이스를 작성 합니다.

## <a name="global"></a>전역적으로 사용 가능한 데이터 이동
Azure 데이터 팩터리는 hello 미국 서 부, 미국 동부 및 북부 유럽 지역 에서만 사용할 수 있습니다. 그러나 복사 작업을 구동 하는 hello 서비스는 hello에서 전체적으로 사용할 수 있는 영역 및 지역입니다. hello 전체적으로 사용 가능한 토폴로지는 일반적으로 지역 간 홉을 방지 하는 효율적인 데이터 이동이 되도록 합니다. 지역별 Data Factory 및 데이터 이동 기능 사용 가능 여부는 [지역별 서비스](https://azure.microsoft.com/regions/#services) 를 참조하세요.

### <a name="copy-data-between-cloud-data-stores"></a>클라우드 데이터 저장소 간의 데이터 복사
데이터 팩터리 서비스 배포를 사용 하 여 hello에 가장 가까운 toohello 싱크가 hello 영역의 hello 클라우드 데이터 저장소를 원본 및 싱크를 같은 지리 toomove hello 데이터입니다. Toohello 다음 매핑에 대 한 표를 참조 하십시오.

| Hello 대상 데이터 저장소의 지리적 위치 | Hello 대상 데이터 저장소의 지역 | 데이터 이동에 사용되는 지역 |
|:--- |:--- |:--- |
| 미국 | 미국 동부 | 미국 동부 |
| &nbsp; | 미국 동부 2 | 미국 동부 2 |
| &nbsp; | 미국 중부 | 미국 중부 |
| &nbsp; | 미국 중북부 | 미국 중북부 |
| &nbsp; | 미국 중남부 | 미국 중남부 |
| &nbsp; | 미국 중서부 | 미국 중서부 |
| &nbsp; | 미국 서부 | 미국 서부 |
| &nbsp; | 미국 서부 2 | 미국 서부 |
| 캐나다 | 캐나다 동부 | 캐나다 중부 |
| &nbsp; | 캐나다 중부 | 캐나다 중부 |
| 브라질 | 브라질 남부 | 브라질 남부 |
| 유럽 | 북유럽 | 북유럽 |
| &nbsp; | 서유럽 | 서유럽 |
| 영국 | 영국 서부 | 영국 남부 |
| &nbsp; | 영국 남부 | 영국 남부 |
| 아시아 태평양 | 동남아시아 | 동남아시아 |
| &nbsp; | 동아시아 | 동남아시아 |
| 오스트레일리아 | 오스트레일리아 동부 | 오스트레일리아 동부 |
| &nbsp; | 오스트레일리아 남동부 | 오스트레일리아 남동부 |
| 일본 | 일본 동부 | 일본 동부 |
| &nbsp; | 일본 서부 | 일본 동부 |
| 인도 | 인도 중부 | 인도 중부 |
| &nbsp; | 인도 서부 | 인도 중부 |
| &nbsp; | 인도 남부 | 인도 중부 |

또는 나타낼 수 있습니다 명시적으로 지정 하 여 tooperform hello 복사본을 사용 하는 데이터 팩터리 서비스 toobe의 hello 영역 `executionLocation` 복사 작업에서 속성 `typeProperties`합니다. 이 속성에 대한 지원되는 값은 위의 **데이터 이동에 사용되는 지역** 열에 나열됩니다. 데이터를 거칩니다 해당 지역의 hello 유선으로 복사 하는 동안 note 합니다. 예를 들어 Azure 간의 toocopy 저장 한국를 지정할 수 있습니다 `"executionLocation": "Japan East"` 일본 영역을 통해 tooroute (참조 [JSON 샘플](#by-using-json-scripts) 참조로).

> [!NOTE]
> Hello 대상 데이터 저장소의 hello 영역 앞의 목록에 없거나 또는 검색할 수 없는 경우, 기본적으로 복사 작업은 대체 지역을 통하지 않고 하지 않으면 실패 하는 경우 `executionLocation` 지정 됩니다. 지원 되는 hello 지역 목록 시간에 따라 확장 됩니다.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간 데이터 복사
온-프레미스 또는 Azure Virtual Machines/IaaS와 클라우드 저장소 간에 데이터를 복사할 때 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 는 온-프레미스 컴퓨터 또는 Virtual Machines에서 데이터 이동을 수행합니다. hello를 사용 하지 않는 한 hello 데이터 hello 클라우드에서 hello 서비스를 통해 이동 하지 않는 [복사본을 스테이징](data-factory-copy-activity-performance.md#staged-copy) 기능입니다. 이 경우 데이터 hello 싱크 데이터 저장소에 기록 되기 전에 Azure Blob 저장소를 준비 하는 hello 통해 전송 됩니다.

## <a name="create-a-pipeline-with-copy-activity"></a>복사 활동을 포함하는 파이프라인 만들기
두 가지 방법을 통해 복사 활동을 포함하는 파이프라인을 만들 수 있습니다.

### <a name="by-using-hello-copy-wizard"></a>Hello 복사 마법사를 사용 하 여
데이터 팩터리 복사 마법사 hello toocreate 파이프라인 복사 작업을 수 있습니다. 이 파이프라인에서 지원 되는 소스 toodestinations toocopy 데이터를 사용 하면 *JSON을 작성 하지 않고도* 연결 된 서비스, 데이터 집합 및 파이프라인에 대 한 정의입니다. 참조 [데이터 팩터리 복사 마법사](data-factory-copy-wizard.md) hello 마법사에 대 한 세부 정보에 대 한 합니다.  

### <a name="by-using-json-scripts"></a>JSON 스크립트 사용
(사용 하 여 복사 작업)는 파이프라인에 대 한 hello Azure 포털, Visual Studio 또는 Azure PowerShell toocreate JSON 정의에서 데이터 팩터리 편집기를 사용할 수 있습니다. 그런 다음 데이터 팩터리에서 toocreate hello 파이프라인 것 것을 배포할 수 있습니다. 단계별 지침이 포함된 자습서는 [자습서: Azure Data Factory 파이프라인에서 복사 활동 사용](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 을 참조하세요.    

이름, 설명, 입력/출력 테이블, 정책 등의 JSON 속성은 모든 형식의 활동에 사용할 수 있습니다. Hello에서 사용할 수 있는 속성 `typeProperties` hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.

복사 작업에 대 한 hello `typeProperties` 섹션 hello 유형의 원본에 따라 다르며 싱크 합니다. Hello에는 원본/싱크 클릭 [원본 및 싱크를 지원](#supported-data-stores-and-formats) 해당 데이터 저장소에 대 한 복사 작업을 지원 합니다. 형식 속성에 대 한 섹션 toolearn 합니다.

샘플 JSON 정의는 다음과 같습니다.

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
hello에 정의 된 hello 일정 출력 데이터 집합 결정 hello 활동 실행 하는 경우 (예: **매일**와 빈도 **일**, 및 간격으로 **1**). hello 활동에서에서 데이터를 복사 된 입력된 데이터 집합 (**소스**) tooan 출력 데이터 집합 (**싱크**).

둘 이상의 입력된 데이터 집합 tooCopy 활동을 지정할 수 있습니다. 서로 hello 활동이 실행 되기 전에 사용 되는 tooverify hello 종속성입니다. 그러나 hello 첫 번째 데이터 집합의 hello 데이터만 복사 toohello 대상 데이터입니다. 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.  

## <a name="performance-and-tuning"></a>성능 및 튜닝
Hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 설명 하는 Azure Data Factory에서 데이터 이동 (복사 작업)의 hello 성능에 영향을 주는 주요 요인입니다. 또한 내부 테스트 중에 성능을 관찰 된 hello를 나열 하 고 복사 작업의 다양 한 방법으로 toooptimize hello 성능에 설명 합니다.

## <a name="fault-tolerance"></a>내결함성
데이터 및 반환 오류 복사 복사 작업은 중지 하는 기본적으로 원본 및 싱크; 간에 호환 되지 않는 데이터를 발견 하면 tooskip 및 로그 hello 호환 되지 않는 행과 복사본만 명시적으로 구성할 수도 있지만 이러한 호환 되는 데이터 toomake hello 복사가 했습니다. Hello 참조 [복사 활동 내결함성](data-factory-copy-activity-fault-tolerance.md) 자세한 세부 정보.

## <a name="security-considerations"></a>보안 고려 사항
Hello 참조 [보안 고려 사항](data-factory-data-movement-security-considerations.md), Azure Data Factory에서 데이터 이동 서비스를 있는지 toosecure 데이터를 사용 하는 보안 인프라를 설명 하는 합니다.

## <a name="scheduling-and-sequential-copy"></a>예약 및 순차 복사
Data Factory에서 예약 및 실행이 작동하는 방식에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md) 을 참조하세요. 것은 가능한 toorun 여러 복사 작업 차례로 정렬/순차적 방식으로 합니다. Hello 참조 [순차적으로 복사](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) 섹션.

## <a name="type-conversions"></a>형식 변환
다른 데이터 저장소에는 서로 다른 네이티브 형식 시스템이 있습니다. 복사 작업에는 2 단계 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.

1. 네이티브 소스 형식 tooa.NET 형식에서 변환 합니다.
2. .NET 형식 tooa 네이티브 싱크 형식에서 변환 합니다.

데이터 저장소에 대 한 네이티브 형식 시스템 tooa.NET 유형에 서 hello 매핑 hello 각 데이터 저장소 문서입니다. (Hello hello 특정 링크를 클릭 [데이터 저장소를 지원](#supported-data-stores) 테이블). 복사 활동 hello 오른쪽 변환을 수행 되도록 테이블을 만드는 동안 이러한 매핑 toodetermine 적절 한 형식을 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* toolearn hello 더 복사 작업에 대 한 참조 [Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
* 온-프레미스 데이터 저장소 tooa 클라우드 데이터 저장소에서 데이터를 이동 하는 방법에 대 한 toolearn 참조 [온-프레미스 toocloud 데이터 저장소에서 데이터를 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다.
