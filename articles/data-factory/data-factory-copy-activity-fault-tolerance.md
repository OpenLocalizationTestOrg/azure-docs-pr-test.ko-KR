---
title: "aaaAdd 내결함성 Azure 데이터 팩터리 복사 작업에서 호환 되지 않는 행을 건너뛰는 여 | Microsoft Docs"
description: "어떻게 tooadd 내결함성 Azure 데이터 팩터리 복사 작업에 복사 하는 동안 호환 되지 않는 행을 건너뛰는 여 알아봅니다"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>호환되지 않는 행을 건너뛰어 복사 작업에 내결함성 추가

Azure Data Factory [복사 작업](data-factory-data-movement-activities.md) 원본 및 싱크 데이터 저장소 간에 데이터를 복사 하는 경우 두 가지 방법으로 toohandle 호환 되지 않는 행을 제공 합니다.

- 중단 하 고 hello 복사 실패 작업에서 데이터가 호환 되지 않는 경우에 (기본 동작) 발생 했습니다.
- Toocopy 계속 내결함성 추가 호환 되지 않는 데이터 행을 건너뛰는 hello 데이터의 모든 합니다. 또한 Azure Blob 저장소에 hello 호환 되지 않는 행을 기록할 수 있습니다. 다음 검사 hello 실패에 대 한 hello 로그 toolearn hello 원인, hello 데이터 원본에 대해 hello 데이터를 수정 하 고 수 hello 복사 작업을 다시 시도 하십시오.

## <a name="supported-scenarios"></a>지원되는 시나리오
복사 작업은 호환되지 않는 데이터의 검색, 건너뛰기 및 로깅에 대한 다음 세 가지 시나리오를 지원합니다.

- **Hello 원본 데이터 형식과 hello 싱크 네이티브 형식 간의 비 호환성**

    예: Blob 저장소 tooa SQL에서에서 CSV 파일에서 데이터 복사 데이터베이스 세 개 포함 하는 스키마 정의로 **INT** 유형 열입니다. 와 같은 숫자 데이터를 포함 하는 CSV 파일 행 hello `123,456,789` 성공적으로 복사 됩니다 toohello 싱크 저장소입니다. 그러나 같은 숫자가 아닌 값을 포함 하는 행을 hello `123,456,abc` 호환 되지 않음으로 감지 하 고는 건너뜁니다.

- **Hello hello 원본 및 싱크 hello 사이 열 수가 일치 하지 않습니다.**

    예: 6 개의 열이 포함 된 스키마 정의와 함께 데이터베이스에서 Blob 저장소 tooa SQL CSV 파일에서 데이터를 복사 합니다. hello 6 개의 열이 포함 된 행은 CSV 파일 복사 성공적으로 toohello 싱크 저장소. hello CSV 파일 행 수를 늘리거나 6 개 미만의 열이 포함 된 호환 되지 않는 것으로 확인 된 및 생략 됩니다.

- **기본 키 위반 tooa 관계형 데이터베이스에 쓸 때**

    예: SQL server tooa SQL 데이터베이스에서 데이터를 복사 합니다. Hello 싱크 SQL 데이터베이스에 기본 키가 정의 하지만 이러한 기본 키 hello 원본 SQL server에서 정의 됩니다. hello 원본에 존재 하는 hello 중복 행 복사 toohello 싱크 일 수 없습니다. 복사 활동 hello 싱크 hello 원본 데이터의 첫 번째 행 hello만 복사합니다. hello 중복 hello 기본 키 값을 포함 하는 후속 소스 행 호환 되지 않는 것으로 검색 되 고은 건너뜁니다.

## <a name="configuration"></a>구성
hello 다음 예에서는 hello 복사 작업에서 호환 되지 않는 행을 건너뛰는 JSON 정의 tooconfigure.

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | 복사 중 호환되지 않는 행을 건너뛸지 여부를 설정합니다. | True<br/>False(기본값) | 아니요 |
| **redirectIncompatibleRowSettings** | 될 수 있는 속성의 그룹이 toolog hello 호환 되지 않는 행을 할 때 지정 합니다. | &nbsp; | 아니요 |
| **linkedServiceName** | hello는 hello 건너뛴 행이 포함 된 Azure 저장소 toostore hello 로그의 서비스를 연결 합니다. | hello 이름은 [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) 또는 [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) toouse toostore hello 로그 파일을 사용 하지 않겠다고 toohello 저장소 인스턴스가 참조 하는 서비스를 연결 합니다. | 아니요 |
| **path** | hello 경로 hello를 포함 하는 hello 로그 파일의 행을 건너뜁니다. | Hello toouse toolog hello 호환 되지 않는 데이터를 지정 하는 Blob 저장소 경로 지정 합니다. 경로 제공 하지 않으면 hello 서비스 사용자에 대 한 컨테이너를 만듭니다. | 아니요 |

## <a name="monitoring"></a>모니터링
Hello 복사 작업 실행이 완료 되 면 hello hello 보고서는 모니터링 섹션의에서 건너뛴된 행 수를 확인할 수 있습니다.

![건너뛰는 호환되지 않는 행 모니터링](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Toolog hello 호환 되지 않는 행을 구성 하는 경우에이 경로에 hello 로그 파일을 찾을 수 있습니다: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` hello 로그 파일에 해당 하는 hello 행 파악 하 고 hello 비 호환성의 근본 원인을 hello 합니다.

Hello 원래 데이터와 해당 오류 hello hello 파일에 기록 됩니다. Hello 로그 파일 콘텐츠의 예는 다음과 같습니다.
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>다음 단계
Azure 데이터 팩터리 복사 작업에 대해 자세히 toolearn 참조 [복사 작업을 사용 하 여 데이터를 이동](data-factory-data-movement-activities.md)합니다.
