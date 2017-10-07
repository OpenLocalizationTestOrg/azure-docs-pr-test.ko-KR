---
title: "Azure 데이터 팩터리에서 aaaFile 및 압축 형식 | Microsoft Docs"
description: "Azure Data Factory에서 지 원하는 hello 파일 형식에 알아봅니다."
keywords: "Blob 데이터, Azure Blob 복사"
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Azure Data Factory에서 지원하는 파일 및 압축 형식
*이 항목은 다음 커넥터 toohello 적용 됩니다.: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure 데이터 레이크 저장소](data-factory-azure-datalake-connector.md), [파일 시스템](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), 및 [SFTP](data-factory-sftp-connector.md)합니다.*

Azure Data Factory hello 다음 파일 형식 유형을 지원 합니다.

* [텍스트 형식](#text-format)
* [JSON 형식](#json-format)
* [Avro 형식](#avro-format)
* [ORC 형식](#orc-format)
* [Parquet 형식](#parquet-format)

## <a name="text-format"></a>텍스트 형식
텍스트 파일에서 tooread를 싶거나 tooa 텍스트 파일 쓰기 설정 hello `type` hello에 대 한 속성 `format` hello 데이터 집합의 섹션 너무**TextFormat**합니다. Hello 다음을 지정할 수도 있습니다 **선택적** hello에 대 한 속성 `format` 섹션. 참조 [TextFormat 예제](#textformat-example) 방법에 대 한 섹션 tooconfigure 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| columnDelimiter |hello 문자는 파일에 tooseparate 열을 사용 합니다. 데이터의 확률이 높습니다 않은 드문 인쇄할 수 없는 char 존재 toouse를 고려할 수 있습니다. 예를 들어 헤딩의 시작(SOH)을 나타내는 "\u0001"을 지정합니다. |문자는 하나만 사용할 수 있습니다. hello **기본** 값은 **쉼표 (',')**합니다. <br/><br/>유니코드 문자를 toouse 너무 참조[유니코드 문자](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget에 해당 하는 코드를 hello 합니다. |아니요 |
| rowDelimiter |hello 문자는 파일에 tooseparate 행을 사용 합니다. |문자는 하나만 사용할 수 있습니다. hello **기본** 값은 hello 읽기의 다음 값 중 하나: **["\r\n", "\r", "\n"]** 및 **"\r\n"** 쓰기입니다. |아니요 |
| escapeChar |입력된 파일의 hello 내용 tooescape 열 구분 기호를 사용 하는 hello 특수 문자입니다. <br/><br/>한 테이블에 대해 escapeChar 및 quoteChar을 둘 다 지정할 수는 없습니다. |문자는 하나만 사용할 수 있습니다. 기본값은 없습니다. <br/><br/>예: 쉼표 있는 경우 (', ') toohave hello 쉼표 문자 hello 텍스트에는 원하는 수 있지만 hello 열 구분 기호 (예: "Hello, world"), '$' hello 이스케이프 문자로 정의 하 고 문자열을 사용할 수 "Hello$, world" hello 소스에서 합니다. |아니요 |
| quoteChar |hello 문자 tooquote는 문자열 값을 사용 합니다. hello 열 및 행 구분 기호 hello 인용 문자 내 hello 문자열 값의 일부분으로 간주 됩니다. 이 속성은 적용 가능한 tooboth 입력 및 데이터 집합을 출력 합니다.<br/><br/>한 테이블에 대해 escapeChar 및 quoteChar을 둘 다 지정할 수는 없습니다. |문자는 하나만 사용할 수 있습니다. 기본값은 없습니다. <br/><br/>예를 들어, 쉼표가 있는 경우 (', ') hello 열 구분 기호 있지만 hello 텍스트에 쉼표 문자 toohave 원하는 만큼 (예: < Hello, world >), 정의할 수 있습니다 "(큰따옴표) hello 인용 문자 및 문자열 hello를 사용 하 여"Hello, world"hello 소스에서 합니다. |아니요 |
| nullValue |하나 이상의 문자 toorepresent null 값을 사용합니다. |하나 이상의 문자입니다. hello **기본** 값은 **"\N" 및 "NULL"** 읽기 및 **"\N"** 쓰기입니다. |아니요 |
| encodingName |Hello 인코딩 이름을 지정 합니다. |유효한 인코딩 이름입니다. [Encoding.EncodingName 속성](https://msdn.microsoft.com/library/system.text.encoding.aspx)을 참조하세요. windows-1250 또는 shift_jis 등을 예로 들 수 있습니다. hello **기본** 값은 **u t F-8**합니다. |아니요 |
| firstRowAsHeader |Tooconsider 첫 번째 행을 머리글로 hello 있는지 여부를 지정 합니다. 입력 데이터 집합의 경우 Data Factory는 첫 번째 행을 머리글로 읽습니다. 출력 데이터 집합의 경우에는 첫 번째 행을 머리글로 씁니다. <br/><br/>샘플 시나리오의 경우 [`firstRowAsHeader` 및 `skipLineCount` 사용 시나리오](#scenarios-for-using-firstrowasheader-and-skiplinecount)를 참조하세요. |True<br/><b>False(기본값)</b> |아니요 |
| skipLineCount |입력된 파일에서 데이터를 읽을 때 행 tooskip hello 수를 나타냅니다. SkipLineCount과 firstRowAsHeader 모두 지정 된 경우 hello 줄은 먼저 건너뜁니다 고 hello 헤더 정보 hello 입력된 파일에서 읽은 다음 합니다. <br/><br/>샘플 시나리오의 경우 [`firstRowAsHeader` 및 `skipLineCount` 사용 시나리오](#scenarios-for-using-firstrowasheader-and-skiplinecount)를 참조하세요. |Integer |아니요 |
| treatEmptyAsNull |Tootreat null 또는 빈 문자열을 null로 최대값 여부를 지정 합니다. 입력된 파일에서 데이터를 읽고 있습니다. |**True(기본값)**<br/>False |아니요 |

### <a name="textformat-example"></a>TextFormat 예제
다음 데이터 집합에 대 한 JSON 정의 hello, 일부 hello 선택적 속성 지정 됩니다.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse는 `escapeChar` 대신 `quoteChar`, 대체 hello 줄을 `quoteChar` 에서는 escapeChar 다음 hello로:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>FirstRowAsHeader 및 skipLineCount 사용 시나리오
* 파일이 아닌 소스 tooa 텍스트 파일에서 복사 하 고 hello 스키마 메타 데이터가 포함 된 헤더 줄 tooadd ु (예: SQL 스키마). 지정 `firstRowAsHeader` 이 시나리오에 대 한 hello 출력 데이터 집합에 완전 하 게 합니다.
* 헤더 줄 tooa 비파일 싱크를 포함 하는 텍스트 파일에서 복사 하는 및 줄 toodrop 있을 것입니다. 지정 `firstRowAsHeader` hello 입력된 데이터 집합의 완전 하 게 합니다.
* 텍스트 파일에서 복사 하는 및 tooskip 없는 데이터 나 헤더 정보가 포함 된 hello 시작 부분에 몇 줄을 선택 합니다. 지정 `skipLineCount` tooindicate hello 개수의 줄 toobe 건너뛰도록 합니다. Hello 파일의 나머지 부분은 hello 포함 헤더 줄을 지정할 수도 있습니다 `firstRowAsHeader`합니다. 두 `skipLineCount` 및 `firstRowAsHeader` hello 줄은 먼저 건너뜁니다 고 hello 헤더 정보 hello 입력된 파일에서 읽은 다음 지정 된

## <a name="json-format"></a>JSON 형식
너무**로 JSON 파일 가져오기/내보내기-Azure Cosmos DB에서 /으로**, hello 참조 [가져오기/내보내기 JSON 문서](data-factory-azure-documentdb-connector.md#importexport-json-documents) 섹션 [/Azure Cosmos DB에서 데이터를 이동](data-factory-azure-documentdb-connector.md) 문서.

Tooparse hello JSON 파일 또는 JSON 형식으로 hello 데이터를 쓸 경우 설정 hello `type` hello에 대 한 속성 `format` 너무 섹션**JsonFormat**합니다. Hello 다음을 지정할 수도 있습니다 **선택적** hello에 대 한 속성 `format` 섹션. 참조 [JsonFormat 예제](#jsonformat-example) 방법에 대 한 섹션 tooconfigure 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| filePattern |각 JSON 파일에 저장 된 데이터의 hello 패턴을 나타냅니다. 사용 가능한 값은 **setOfObjects** 및 **arrayOfObjects**이고 hello **기본** 값은 **setOfObjects**합니다. 이러한 패턴에 대한 자세한 내용은 [JSON 파일 패턴](#json-file-patterns) 섹션을 참조하세요. |아니요 |
| jsonNodeReference | Tooiterate을 배열 내에서 hello 개체에서 데이터를 추출 하는 경우 필드 hello로 동일한 패턴을 해당 배열의 hello JSON 경로 지정 합니다. 이 속성은 JSON 파일에서 데이터를 복사할 때만 지원됩니다. | 아니요 |
| jsonPathDefinition | 각 열 매핑에 대 한 hello JSON 경로 식 (소문자로 시작)를 사용자 지정 된 열 이름으로 지정 합니다. 이 속성은 JSON 파일에서 데이터를 복사할 때만 지원되며 개체 또는 배열에서 데이터를 추출할 수 있습니다. <br/><br/> 루트 개체에서 필드에 대 한 루트 $;로 시작 필드에서 선택한 hello 배열 내에 대 한 `jsonNodeReference` 속성을 hello 배열 요소에서 시작 합니다. 참조 [JsonFormat 예제](#jsonformat-example) 방법에 대 한 섹션 tooconfigure 합니다. | 아니요 |
| encodingName |Hello 인코딩 이름을 지정 합니다. 유효한 인코딩 이름 목록은 hello, 참조: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) 속성입니다. 예: windows-1250 또는 shift_jis hello **기본** 값은: **u t F-8**합니다. |아니요 |
| nestingSeparator |문자는 사용 되는 tooseparate 중첩 수준입니다. hello 기본값은 '.' (점)입니다. |아니요 |

### <a name="json-file-patterns"></a>JSON 파일 패턴

복사 작업에는 hello JSON 파일의 패턴을 따르는 구문 분석할 수 있습니다.

- **유형 I: setOfObjects**

    각 파일에 단일 개체 또는 줄로 구분된/연결된 여러 개체가 포함되어 있습니다. 출력 데이터 집합에서 이 옵션을 선택하는 경우 복사 활동에서는 줄마다 개체가 하나씩 포함된(각 개체가 줄로 구분된) JSON 파일 하나를 생성합니다.

    * **단일 개체 JSON 예제**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **줄로 구분된 JSON 예제**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **연결된 JSON 예제**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **유형 II: arrayOfObjects**

    각 파일에 개체 배열이 포함됩니다.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>JsonFormat 예제

**사례 1: JSON 파일에서 데이터 복사**

Hello 두 개의 샘플 JSON 파일에서 데이터를 복사 하는 경우 다음을 참조 하십시오. 일반적인 포인트 toonote hello:

**샘플 1: 개체 및 배열에서 데이터 추출**

이 샘플에서는 하나의 루트 JSON 개체는 테이블 형식 결과의 toosingle 레코드 매핑합니다 예상 합니다. 콘텐츠를 다음 hello로 JSON 파일을 가정해 봅니다.  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
및 원하는 toocopy 개체 및 배열 둘 다에서 데이터를 추출 하 여 포맷 hello 다음에 Azure SQL 테이블에:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

hello 입력된 데이터 집합을 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의). 더 구체적으로 살펴보면 다음과 같습니다.

- `structure`섹션은 tootabular 데이터를 변환 하는 동안 사용자 지정 하는 hello 열 이름 및 hello 해당 데이터 형식을 정의 합니다. 이 섹션은 **선택적** toodo 열 매핑이 필요 하지 않는 한 합니다. 참조 [원본 데이터 집합 열 toodestination 데이터 집합 열 매핑](data-factory-map-columns.md) 자세한 내용은 섹션.
- `jsonPathDefinition`여기서 tooextract hello 데이터를 나타내는 각 열에 대 한 hello JSON 경로 지정 합니다. 사용할 수 배열의 데이터 toocopy **배열 [x] 지 원하는** hello xth 개체의 속성을 지정 하는 hello tooextract 값 צ ְ ײ  **배열 [*] 지 원하는** toofind 이러한 속성을 포함 하는 개체 로부터 hello 값입니다.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**예제 2: 교차 적용 hello 배열에서 동일한 패턴을 사용 하 여 여러 개체**

이 샘플에서는 테이블 형식 결과에서 여러 레코드로 tootransform 하나의 루트 JSON 개체를 예상 합니다. 콘텐츠를 다음 hello로 JSON 파일을 가정해 봅니다.  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
및 hello hello 배열 내에서 데이터를 병합 하 여 포맷 hello 다음에 Azure SQL 테이블에 toocopy을 크로스 조인 공용 루트 정보 hello로:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

hello 입력된 데이터 집합을 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의). 더 구체적으로 살펴보면 다음과 같습니다.

- `structure`섹션은 tootabular 데이터를 변환 하는 동안 사용자 지정 하는 hello 열 이름 및 hello 해당 데이터 형식을 정의 합니다. 이 섹션은 **선택적** toodo 열 매핑이 필요 하지 않는 한 합니다. 참조 [원본 데이터 집합 열 toodestination 데이터 집합 열 매핑](data-factory-map-columns.md) 자세한 내용은 섹션.
- `jsonNodeReference`hello에서 같은 패턴을 사용 하 여 hello 개체에서 데이터를 tooiterate 및 추출 나타냅니다 **배열** orderlines 합니다.
- `jsonPathDefinition`여기서 tooextract hello 데이터를 나타내는 각 열에 대 한 hello JSON 경로 지정 합니다. 이 예제에서는 "ordernumber", "orderdate" 및 "city"가 루트 개체에서 "$" 하지 않고 hello 배열 요소에서 파생 된 경로로 정의 되지만 "order_pd" 및 "order_price" "$."로 시작 하는 JSON 경로.

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**포인트 다음 참고 hello:**

* 경우 hello `structure` 및 `jsonPathDefinition` 정의 되어 있지 않은 hello Data Factory 데이터 집합에 hello 복사 작업에서 hello hello 첫 번째 개체에서 스키마 및 병합 된 hello 전체 개체를 검색 합니다.
* Hello JSON 입력 배열에 있는 경우 기본적으로 hello 복사 활동 hello 전체 배열 값을 문자열로 변환 합니다. 사용 하 여 tooextract 데이터를 선택할 수 있습니다 `jsonNodeReference` 및/또는 `jsonPathDefinition`에서 지정 하 여 건너뛸 또는 `jsonPathDefinition`합니다.
* 가 중복 이름에 같은 수준 hello, hello 복사 작업은 마지막 hello를 선택 합니다.
* 속성 이름은 대/소문자를 구분합니다. 이름은 같지만 대/소문자가 다른 두 속성은 별도의 두 속성으로 간주됩니다.

**사례 2: 데이터 tooJSON 파일 쓰기**

다음 표에 SQL 데이터베이스의 hello 가정해 봅니다.

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

및 각 레코드에 대해이 원하는 toowrite tooa JSON 개체 형식에 따라 hello:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

hello 출력 데이터 집합으로 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의). 보다 구체적으로, `structure` 대상 파일에 사용자 지정 하는 hello 속성 이름을 정의 하는 섹션 `nestingSeparator` (기본값은 ".")는 hello 이름에서 사용 되는 tooidentify hello 중첩 계층입니다. 이 섹션은 **선택적** toochange hello 속성 이름을 원본 열 이름과 비교 하거나 hello 속성 중 일부를 중첩 하지 않는 한 합니다.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>AVRO 형식
Tooparse hello Avro 파일 또는 Avro 형식에서 hello 데이터를 작성 하는 경우 설정 hello `format` `type` 속성 너무**AvroFormat**합니다. Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성. 예제:

```json
"format":
{
    "type": "AvroFormat",
}
```

toouse Hive 테이블에서 Avro 형식으로 참조할 수 있습니다 너무[Apache Hive 자습서](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)합니다.

포인트 다음 참고 hello:  

* [복합 데이터 형식](http://avro.apache.org/docs/current/spec.html#schema_complex)은 지원되지 않습니다(레코드, 열거형, 배열, 매핑, 공용 구조체 및 고정).

## <a name="orc-format"></a>ORC 형식
Tooparse hello ORC 파일 형식 ORC hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**OrcFormat**합니다. Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성. 예제:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> ORC 파일을 복사 하지는 **으로-는** 온-프레미스와 클라우드 사이 데이터 저장소, tooinstall hello 8 JRE (Java Runtime Environment) 게이트웨이 컴퓨터에 필요 합니다. 64비트 게이트웨이에는 64비트 JRE가 필요하고 32비트 게이트웨이에는 32비트 JRE가 필요합니다. [여기서](http://go.microsoft.com/fwlink/?LinkId=808605)두 버전이 모두 제공됩니다. 적절 한 hello를 선택 합니다.
>
>

포인트 다음 참고 hello:

* 복합 데이터 형식(구조체, 맵, 목록, 공용 구조체)은 지원되지 않습니다.
* ORC 파일에는 3개의 [압축 관련 옵션](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)(NONE, ZLIB, SNAPPY)이 있습니다. Data Factory에서는 이러한 압축 형식으로 된 데이터를 ORC 파일에서 읽을 수 있습니다. Hello 압축을 사용 하 여 코덱은 hello 메타 데이터 tooread hello 데이터입니다. 그러나 tooan ORC 파일을 작성할 때 데이터 팩터리 선택 ZLIB, ORC에 대 한 hello 기본값 합니다. 현재,이 없는 옵션 toooverride이이 동작 합니다.

## <a name="parquet-format"></a>Parquet 형식
Tooparse hello Parquet 파일 형식 Parquet hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**ParquetFormat**합니다. Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성. 예제:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Parquet 파일을 복사 하지는 **으로-는** 온-프레미스와 클라우드 사이 데이터 저장소, tooinstall hello 8 JRE (Java Runtime Environment) 게이트웨이 컴퓨터에 필요 합니다. 64비트 게이트웨이에는 64비트 JRE가 필요하고 32비트 게이트웨이에는 32비트 JRE가 필요합니다. [여기서](http://go.microsoft.com/fwlink/?LinkId=808605)두 버전이 모두 제공됩니다. 적절 한 hello를 선택 합니다.
>
>

포인트 다음 참고 hello:

* 복합 데이터 형식(MAP, LIST)은 지원되지 않습니다.
* Parquet 파일에 다음 압축 관련 옵션 hello: NONE, SNAPPY, GZIP, 및 LZO 합니다. Data Factory에서는 이러한 압축 형식으로 된 데이터를 ORC 파일에서 읽을 수 있습니다. Hello 압축 코덱 hello 메타 데이터 tooread hello 데이터에 사용합니다. 그러나 tooa Parquet 파일을 작성할 때 데이터 팩터리 선택 SNAPPY, Parquet 형식에 대 한 hello 기본값입니다. 현재,이 없는 옵션 toooverride이이 동작 합니다.

## <a name="compression-support"></a>압축 지원
큰 데이터 집합을 처리하면 I/O 및 네트워크 병목 현상이 발생할 수 있습니다. 따라서 압축된 데이터 저장소에 수 hello 네트워크를 통해 데이터 전송 속도 및 디스크 공간을 절약 뿐만 아니라 표시할 수도 빅 데이터 처리 성능이 크게 향상 되었습니다. 현재 압축은 Azure Blob 또는 온-프레미스 파일 시스템과 같은 파일 기반 데이터 저장소에 대해 지원됩니다.  

데이터 집합을 사용 하 여 hello에 대 한 toospecify 압축 **압축** hello 다음 예제와 같이 hello 데이터 집합 JSON의에서 속성:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Hello 샘플 데이터 집합 복사 작업의 hello 출력으로 사용, 가정 hello 복사 활동 압축 hello 최적의 비율을 사용 하 여 GZIP 코덱을 사용 하 여 데이터를 출력 하 고 hello Azure Blob 저장소에서에서 pagecounts.csv.gz 라는 파일에 압축 hello 데이터를 작성 합니다.

> [!NOTE]
> 데이터 hello에 대 한 압축 설정이 지원 되지 않습니다 **AvroFormat**, **OrcFormat**, 또는 **ParquetFormat**합니다. 이러한 형식의 파일을 읽을 때 데이터 팩터리 검색 하 고 hello 메타 데이터에 hello 압축 코덱을 사용 합니다. Data Factory toofiles 이러한 형식의 작성할 때 해당 형식에 대 한 기본 압축 코덱 hello를 선택 합니다. 예를 들어 OrcFormat에 대해 ZLIB를 사용하고 ParquetFormat에 대해 SNAPPY를 사용합니다.   

hello **압축** 섹션에 다음 두 가지 속성이 있습니다.  

* **형식:** 될 수 있는 hello 압축 코덱을 **GZIP**, **Deflate**, **BZIP2**, 또는 **ZipDeflate**합니다.  
* **수준:** 될 수 있는 hello 압축률 **최적** 또는 **fastest 이면**합니다.

  * **가장 빠른:** hello 결과 파일 최적으로 압축 되지 않은 경우에 hello 압축 작업을 최대한 빨리 완료 해야 합니다.
  * **최적의**: hello 압축 작업 최적으로 압축 hello 연산이 더 긴 시간 toocomplete 하는 경우에 합니다.

    자세한 내용은 [압축 수준](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) 항목을 참조하세요.

지정 하는 경우 `compression` 입력된 데이터 집합 JSON의에서 hello 파이프라인 hello 소스에서 압축 된 데이터를 읽을 수 속성과 hello 복사 작업 출력 데이터 집합 JSON에에서 hello 속성을 지정 하는 경우 압축 된 데이터 toohello 대상을 작성할 수 있습니다. 다음은 몇 가지 샘플 시나리오입니다.

* Azure blob에서 데이터 읽기 GZIP 압축, 압축을 풀고 결과 데이터 tooan Azure SQL 데이터베이스를 작성 합니다. Hello 입력된 hello로 Azure Blob 데이터 집합을 정의할 `compression` `type` GZIP으로 JSON 속성입니다.
* 온-프레미스 파일 시스템에서 일반 텍스트 파일에서 데이터 읽기, GZip 형식을 사용 하 여 압축 및 압축 hello 데이터 tooan Azure blob를 작성 합니다. Hello로 출력 Azure Blob 데이터 집합 정의 `compression` `type` GZip으로 JSON 속성입니다.
* FTP 서버에서.zip 파일 읽기, 내부 tooget hello 파일 압축을 풀고 Azure 데이터 레이크 저장소로 해당 파일을 배치 합니다. Hello로 입력된 FTP 데이터 집합 정의 `compression` `type` ZipDeflate로 JSON 속성입니다.
* Azure blob에서 GZIP 압축 데이터 읽기, 압축을 풀어, BZIP2를 사용 하 여 압축 및 결과 데이터 tooan Azure blob에 쓰기 Hello Azure Blob 된 입력된 데이터 집합 정의 `compression` `type` tooGZIP를 설정 하 고 출력 데이터 집합을 hello `compression` `type` tooBZIP2이 경우에 설정 합니다.   


## <a name="next-steps"></a>다음 단계
Azure Data Factory에서 지원 되는 파일 기반 데이터 저장소에 대 한 아티클을 다음 hello 참조:

- [Azure Blob Storage](data-factory-azure-blob-connector.md)
- [Azure 데이터 레이크 저장소](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [파일 시스템](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
