---
title: "Azure 검색 인덱서의 aaaField 매핑"
description: "Azure 검색 인덱서 필드 매핑 tooaccount 필드 이름 및 데이터 표현의 차이 대 한 구성"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Azure Search 인덱서의 필드 매핑
Azure 검색 인덱서를 사용할 경우 가끔에서 찾을 수 있습니다 직접 경우 입력된 데이터의 대상 인덱스 hello 스키마 일치 매우 하지 않습니다. 이러한 경우에 사용할 수 있습니다 **필드 매핑** tootransform hello로 데이터 적용할 셰이프.

필드 매핑이 유용한 일부 상황:

* 데이터 원본에 `_id`필드가 있지만 Azure 검색이 밑줄로 시작하는 필드 이름을 허용하지 않습니다. 필드 매핑을 너무 "의 이름을 바꾸면" 필드 수 있습니다.
* Hello를 사용 하 여 hello의 필드를 여러 인덱싱할 toopopulate 원하는 tooapply 다른 분석기 toothose 필드 하려고 하기 때문에 동일한 데이터 원본 데이터의 예입니다. 필드 매핑을 사용하여 데이터 원본 필드를 "분기"할 수 있습니다.
* TooBase64 필요한 인코딩 또는 디코딩할 데이터입니다. 필드 매핑은 Base64 인코딩 및 디코딩에 대한 함수를 포함한 여러 **매핑 함수**를 지원합니다.   

## <a name="setting-up-field-mappings"></a>필드 매핑 설정
Hello를 사용 하 여 새 인덱서를 만들 때 필드 매핑을 추가할 수 있습니다 [인덱서 만들기](https://msdn.microsoft.com/library/azure/dn946899.aspx) API입니다. Hello를 사용 하 여 인덱싱 인덱서에서 필드 매핑을 관리할 수 있습니다 [업데이트 인덱서](https://msdn.microsoft.com/library/azure/dn946892.aspx) API입니다.

필드 매핑은 3개의 부분으로 구성됩니다.

1. `sourceFieldName`은(는) 데이터 원본의 필드를 나타냅니다. 이 속성은 필수입니다.
2. 선택 사항 `targetFieldName`은(는) 검색 인덱스의 필드를 나타냅니다. 생략 하면 hello hello 데이터 원본의 이름과 동일한 이름을 사용 됩니다.
3. 선택 사항 `mappingFunction`은(는) 미리 정의된 여러 함수 중 하나를 사용하여 데이터를 변환할 수 있습니다. 함수의 전체 목록은 hello [아래](#mappingFunctions)합니다.

필드 매핑 toohello 추가 `fieldMappings` hello 인덱서 정의에 배열입니다.

예를 들어 필드 이름의 차이를 수용하는 방법은 다음과 같습니다.

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

인덱서는 여러 필드 매핑을 포함할 수 있습니다. 예를 들어 필드를 "분기"할 수 있는 방법은 다음과 같습니다.

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Azure 검색에서 필드 매핑을 대/소문자 비구분 비교 tooresolve hello 필드와 함수 이름을 사용합니다. (없는 tooget 모든 hello 대/소문자 오른쪽), 편리 하지만 데이터 소스 나 인덱스에 대/소문자만 다른 필드를 가질 수 없음을 의미 합니다.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>필드 매핑 함수
이러한 함수는 현재 지원됩니다.

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
수행 *URL 안전한* 입력 문자열 hello의 Base64 인코딩입니다. Hello 입력 u t F-8로 인코딩된 있다고 가정 합니다.

#### <a name="sample-use-case"></a>샘플 사용 사례
만 URL 지원 문자 (해야 하기 때문에 고객 수 tooaddress hello 문서 예를 들어 hello 조회 API를 사용 하 여)는 Azure 검색 문서 키에 나타날 수 있습니다. 데이터 URL 안전 하지 않은 문자 포함 되 고 toouse 원하는 것 toopopulate 검색 인덱스의 키 필드를이 함수를 사용 합니다.   

#### <a name="example"></a>예제
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Hello 입력된 문자열의 Base64 디코딩을 수행 합니다. hello 입력 가정 tooa *URL 안전한* Base64 인코딩 문자열입니다.

#### <a name="sample-use-case"></a>샘플 사용 사례
Blob 사용자 지정 메타데이터 값은 ASCII 인코딩되어야 합니다. Blob의 사용자 지정 메타 데이터에 Base64 인코딩 toorepresent 임의의 유니코드 문자열을 사용할 수 있습니다. 그러나 의미 있는 toomake 검색을 사용할 수 있습니다이 함수 tooturn hello로 인코딩된 데이터 다시 "일반" 문자열로 검색 인덱스를 채울 때.  

#### <a name="example"></a>예제
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Hello를 사용 하는 문자열 필드 구분 기호 및 선택 hello 토큰에서 지정 된 분할 hello hello 결과 분할의 지정한 위치입니다.

예를 들어 hello 입력이 `Jane Doe`, hello `delimiter` 은 `" "`위에 공백을 hello 및 `position` 가 0 이면 hello 결과 `Jane`경우 hello `position` 1 이면 hello 결과 `Doe`합니다. Hello 위치는 존재 하지 않는 tooa 토큰을 참조 하는 경우 오류가 반환 됩니다.

#### <a name="sample-use-case"></a>샘플 사용 사례
데이터 원본에는 `PersonName` 필드 tooindex 원하는 두 개의 별도 `FirstName` 및 `LastName` 필드입니다. 이 함수 toosplit hello 구분 기호를 hello 대로 hello 공백 문자를 사용 하 여 입력을 사용할 수 있습니다.

#### <a name="parameters"></a>매개 변수
* `delimiter`: 입력된 문자열 hello를 분할 하는 경우 hello 구분 기호로 문자열 toouse 합니다.
* `position`: 정수 hello 토큰 toopick hello 입력 문자열의 0부터 시작 위치 분할 됩니다.    

#### <a name="example"></a>예제
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
문자열로 서식이 문자열의 JSON 배열을 toopopulate 사용된 될 수 있는 문자열 배열로 변환은 `Collection(Edm.String)` hello 인덱스의 필드입니다.

예를 들어 hello 입력 문자열은 `["red", "white", "blue"]`, 다음 형식의 hello 대상 필드 `Collection(Edm.String)` hello 3 값으로 채울 수 `red`, `white` 및 `blue`합니다. JSON 문자열 배열로 구문 분석할 수 없는 입력 값의 경우 오류가 반환됩니다.

#### <a name="sample-use-case"></a>샘플 사용 사례
Azure SQL 데이터베이스 자연스럽 게 너무 매핑되는 기본 제공 데이터 형식이 없는`Collection(Edm.String)` Azure 검색의 필드입니다. toopopulate 문자열 컬렉션 필드 JSON 문자열 배열로 원본 데이터 형식과이 함수를 사용 합니다.

#### <a name="example"></a>예제
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Azure Search 개선 지원
기능 또는 향상 된 기능에 대 한 아이디어를 설정한 경우에 게 연락 하세요에 toous 우리의 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search/)합니다.
