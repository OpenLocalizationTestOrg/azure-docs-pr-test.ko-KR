## <a name="specifying-structure-definition-for-rectangular-datasets"></a>사각형 데이터 집합의 구조 정의 지정
hello hello 데이터 집합 JSON의에서 구조 섹션은는 **선택적** 사각형 테이블 (테이블 행 및 열)에 대 한 섹션 및 hello 테이블의 열 컬렉션을 포함 합니다. 형식 변환에 대 한 형식 정보를 제공 하거나 또는 열 매핑을 수행 하는 hello 구조 섹션을 사용 합니다. hello 다음 섹션에서는이 기능을 자세히 설명 합니다. 

각 열에는 다음과 같은 속성 hello 포함 됩니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| name |Hello 열의 이름입니다. |예 |
| type |Hello 열의 데이터 형식입니다. 형식 정보를 지정해야 할 시기에 대한 자세한 내용은 아래의 형식 변환 섹션을 참조하세요. |아니요 |
| culture |.NET 기반 유형을 지정 하 고.NET 형식이 Datetime 또는 Datetimeoffset 사용 되는 문화권 toobe입니다. 기본값은 "en-us"입니다. |아니요 |
| format |사용 유형을 지정 하 고.NET 형식이 Datetime 또는 Datetimeoffset 문자열 toobe 서식을 지정 합니다. |아니요 |

hello 다음 샘플 섹션을 보여 줍니다 hello 구조 JSON 세 열 사용자 id, 이름 및 lastlogindate이 있는 테이블에 대 한 합니다.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

시기에 대 한 지침을 따르는 hello를 사용 하 여 하십시오 tooinclude "구조" 정보 및 hello에 어떤 tooinclude **구조** 섹션.

* **구조화 된 데이터 원본에 대 한** 자체 (원본) SQL Server, Oracle, Azure 테이블 등과 같은 특정 열 매핑을 수행 하려는 경우에 hello "구조" 섹션을 지정 해야 hello 데이터와 함께 데이터 스키마 및 형식 정보를 저장 하는 싱크 및 이름을 toospecific 열은 원본 열을 hello (열 매핑 섹션 아래에서 세부 정보 참조) 동일 하지 않습니다. 
  
    위에서 설명 했 듯이 hello 형식 정보 "구조" 섹션에서 선택 사항입니다. 구조화 된 원본에 대 한 형식 정보를 이미 사용할 수 있는 hello 데이터 저장소에 데이터 집합 정의의 일부로, 따라서를 포함 하지 않아야 형식 정보 hello "구조" 섹션을 포함 않는 경우.
* **읽은 데이터 원본 (특히 Azure blob)에 스키마에 대 한** hello 데이터와 스키마 또는 형식 정보를 저장 하지 않고 toostore 데이터를 선택할 수 있습니다. 이러한 유형의 데이터 원본에 대 한 hello 2의 경우 다음에 "structure"를 포함 해야 합니다.
  * Toodo 열 매핑을 사용 하는 것이 좋습니다.
  * 복사 작업에서 소스 hello 데이터 집합을 사용 하는 경우 "구조"에 유형 정보를 제공할 수 있습니다 및 데이터 팩터리의 hello 싱크에 대 한 변환 toonative 형식에 대 한이 형식 정보를 사용 합니다. 참조 [Azure Blob에서 데이터 tooand 이동](../articles/data-factory/data-factory-azure-blob-connector.md) 대 한 자세한 내용은 문서.

### <a name="supported-net-based-types"></a>지원되는 .NET 기반 형식
데이터 팩터리의 지원 hello CLS 규격.NET 다음 Azure blob와 같은 읽기 데이터 원본에 대 한 스키마에 대 한 "구조"에 유형 정보를 제공 하는 데 형식 값을 기반으로 합니다.

* Int16
* Int32 
* Int64
* Single
* Double
* DECIMAL
* Byte[]
* Bool
* 문자열 
* Guid
* Datetime
* Datetimeoffset
* Timespan 

Datetime 및 Datetimeoffset에 대 한 "culture" & "format" 문자열 toofacilitate의 구문 분석 사용자 지정 날짜/시간 문자열을 선택적으로 지정할 수 있습니다. 아래의 형식 변환 샘플을 참조하세요.

