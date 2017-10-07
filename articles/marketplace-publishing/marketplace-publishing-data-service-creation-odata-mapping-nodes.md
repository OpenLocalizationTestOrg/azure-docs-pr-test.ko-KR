---
title: "aaaGuide toocreating 마켓플레이스 hello에 대 한 데이터 서비스 | Microsoft Docs"
description: "Toocreate, 인증 하 고에 대 한 데이터 서비스를 배포 하는 방법의 자세한 지침은 hello Azure Marketplace에서 구입 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>기존 웹 서비스 tooOData CSDL 통해 매핑하기 위한 hello 노드 스키마 이해
> [!IMPORTANT]
> **현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.** SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다. IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.
>
>

이 문서는 OData 프로토콜 tooCSDL 매핑하기 위한 hello 노드 구조를 명확 하 게 하는 데 도움이 됩니다. Hello 노드 구조는 잘 toonote 된 형식의 XML이 유용 합니다. 따라서 OData 매핑을 설계할 때 루트, 부모 및 자식 스키마를 적용할 수 있습니다.

## <a name="ignored-elements"></a>무시되는 요소
hello 다음은 hello 높은 수준의 CSDL 요소 (XML 노드) toobe hello hello 웹 서비스의 메타 데이터를 가져오는 동안 hello Azure 마켓플레이스 백 엔드에서 사용 하는 것입니다. 이러한 요소가 있더라도 무시됩니다.

| 요소 | 범위 |
| --- | --- |
| Using 요소 |hello 노드, 하위 노드 및 모든 특성 |
| Documentation 요소 |hello 노드, 하위 노드 및 모든 특성 |
| ComplexType |hello 노드, 하위 노드 및 모든 특성 |
| Association 요소 |hello 노드, 하위 노드 및 모든 특성 |
| 확장 속성 |hello 노드, 하위 노드 및 모든 특성 |
| EntityContainer |Hello 다음 특성이 무시 됩니다. 전용: *확장* 및 *AssociationSet* |
| 스키마 |Hello 다음 특성이 무시 됩니다. 전용: *Namespace* |
| FunctionImport |Hello 다음 특성이 무시 됩니다. 전용: *모드* (ln의 기본값은 간주) |
| EntityType |Hello 다음 하위 노드는 무시 되므로: *키* 및 *PropertyRef* |

hello 다음 hello 변경 (추가 및 요소를 무시) toohello 자세히 다양 한 CSDL XML 노드를 설명합니다.

## <a name="functionimport-node"></a>FunctionImport 노드
FunctionImport 노드 서비스 toohello 최종 사용자를 노출 하는 한 개의 URL을 (진입점)를 나타냅니다. hello 노드 hello URL 주소를 지정 방법을, 어떤 매개 변수는 사용 가능한 toohello 최종 사용자 및 이러한 매개 변수에 제공 되는 방법을 설명 하는 수 있습니다.

이 노드에 대한 세부 정보는 [여기][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx)에서 확인할 수 있습니다.

hello 다음은 hello 추가 특성 (또는 추가 tooattributes) hello FunctionImport 노드가 노출 하는:

**d:BaseUri** -노출된 tooMarketplace 있는 hello REST 리소스에 대 한 hello URI 템플릿입니다. 마켓플레이스는 hello REST 웹 서비스에 대 한 hello 템플릿 tooconstruct 쿼리를 사용합니다. hello URI 템플릿을 여기서 parameterName는 hello hello 매개 변수 이름을 {parameterName}의 hello 형태로 hello 매개 변수에 대 한 자리 표시자를 포함 합니다. 예: apiVersion={apiVersion}.
매개 변수는 URI 매개 변수 또는 hello URI 경로의 일부로 tooappear를 허용 됩니다. Hello 경로에 hello 모양의 hello 경우에는 항상 필수 (표시할 수 없습니다. nullable로). *예제:* `d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**이름** -hello의 hello 이름을 가져온 함수가 있습니다.  없습니다 hello CSDL에서에서 정의 된 다른 이름으로 같은 hello 수 있습니다.  예: Name="GetModelUsageFile"

**EntitySet** *(선택 사항)* -hello 함수 엔터티 형식의 컬렉션, hello hello 값을 반환 하는 경우 **EntitySet** hello 엔터티 집합 toowhich hello 컬렉션이 속한 이어야 합니다. 그렇지 않으면 hello **EntitySet** 특성을 사용할 수 없습니다. *예제:* `EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(선택 사항)* -hello URI에서 반환 되는 요소의 hello 유형을 지정 합니다.  Hello 함수는 값을 반환 하지 않는 경우에이 특성을 사용 하지 마십시오. hello 다음은 지원 되는 hello 형식입니다.

* **Collection(<Entity type name>)**: 정의된 엔터티 유형 컬렉션을 지정합니다. hello 이름이 hello EntityType 노드의 hello Name 특성에 있습니다. 예: Collection(WXC.HourlyResult)
* **원시 (<mime type>)**: 원시 문서/blob toohello 사용자 반환 되는 지정 합니다. 예: Raw(image/jpeg) 기타 예:

  * ReturnType="Raw(text/plain)"
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*

**d:Paging** -페이징 hello REST 리소스에서 처리 하는 방법을 지정 합니다. hello 값 중괄호 분기 내에서 사용 되는 매개 변수, 예: 페이지 {$page} = & itemsperpage = {$size} hello 사용 가능한 옵션은:

* **None:** 페이징을 사용할 수 없습니다.
* **Skip:** 논리적 “skip” 및 “take”(위)를 통해 페이징이 표현됩니다. Skip 반환 hello 다음 N 요소는 다음을 수행 하십시오 M 개 요소를 통해 이동 됩니다. 매개 변수 값: $skip
* **Take:** Take hello 다음 n 개 요소를 반환 합니다. 매개 변수 값: $take
* **PageSize:** 논리적 페이지 및 크기(페이지당 항목 수)를 통해 페이징이 표현됩니다. 페이지 반환 되는 hello 현재 페이지를 나타냅니다. 매개 변수 값: $page
* **크기:** 크기는 각 페이지에 대해 반환 되는 항목의 hello 수를 나타냅니다. 매개 변수 값: $size

**d:AllowedHttpMethods** *(선택 사항)* -hello REST 리소스는 동사를 처리 하는 지정 합니다. 또한 지정 된 승인 된 동사 toohello 제한 값입니다.  기본값은 POST입니다.  *예:* `d:AllowedHttpMethods="GET"` 사용할 수 있는 hello 옵션:

* **GET:** 일반적으로 사용 되는 tooreturn 데이터
* **게시물:** 일반적으로 사용 되는 새 데이터 tooinsert
* **PUT:** 일반적으로 사용 되는 tooupdate 데이터
* **삭제:** toodelete 데이터 사용

Hello FunctionImport 노드 내에서 추가 하위 노드 (hello CSDL 설명서에서 다루지 않음)를.

**d:RequestBody** *(선택 사항)* -hello 요청 본문은 요청 hello 사용 되는 tooindicate 전송 본문 toobe 필요 합니다. Hello 요청 본문 내에서 매개 변수를 지정할 수 있습니다. 매개 변수는 중괄호 안에 표현됩니다(예: {parameterName}). 이러한 매개 변수는 매핑되지 않은 hello 본문에 사용자 입력 hello에서 toohello 콘텐츠 공급자의 서비스를 전송 합니다. hello requestBody 요소에 httpMethod 이름 가진 특성이 있습니다. 두 값을 허용 하는 hello 특성:

* **게시물:** 경우 hello 요청에 HTTP POST 사용
* **GET:** hello 요청은 HTTP GET 사용

    예제:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces** 및 **d:Namespace** -이 노드 hello hello 함수 가져오기 (URI 끝점)에서 반환 되는 XML에에서 정의 된 hello 네임 스페이스에 설명 합니다. hello hello 백 엔드 서비스에 의해 반환 되는 XML에 반환 되는 네임 스페이스 toodifferentiate hello 콘텐츠 개수에 관계 없이 포함 될 수 있습니다. **이러한 네임 스페이스의 d:Map 또는 d:Match XPath 쿼리에서 사용 하는 경우 모든 나열 된 toobe가 필요 합니다.** hello d:Namespaces 노드 d:Namespace 노드 집합/목록이 포함 되어 있습니다. 각각의 hello 백 엔드 서비스 응답에 사용 되는 하나의 네임 스페이스를 나열 합니다. hello 다음은 hello d:Namespace 노드의 hello 특성입니다.

* **d:Prefix:** hello XML 결과 hello 서비스에서 반환 된 f:FirstName, f는 hello 접두사 f:LastName 예:와 같이 hello 네임 스페이스 접두사를 hello 합니다.
* **d:Uri:** hello hello 결과 문서에 사용 된 hello 네임 스페이스의 전체 URI입니다. Hello 값을 나타내는 해당 hello 접두사는 해결된 tooat 런타임.

**d:ErrorHandling** *(선택 사항)* - 이 노드는 오류 처리 조건을 포함합니다. 각 hello 조건이 hello 콘텐츠 공급자의 서비스에 의해 반환 되는 hello 결과 대해 유효성이 검사 됩니다. 조건을 HTTP 오류 코드를 제안 하는 hello와 일치 하는 경우 오류 메시지가 toohello 최종 사용자를 반환 됩니다.

**d:ErrorHandling** *(선택 사항)* 및 **d:Condition** *(선택 사항)* -hello 결과 반환한이 선택 되어 있는 한 가지 조건을 보유 하는 조건 노드 hello 콘텐츠 공급자의 서비스입니다. hello는 다음과 같은 hello **필요한** 특성:

* **d:Match:** hello 콘텐츠 공급자에는 지정 된 노드/값이 있는지 여부를 확인 하는 XPath 식의 XML을 출력 합니다. hello XPath hello 출력에 대해 실행 되 고 hello 조건이 일치 항목이 나 false 그렇지 않으면 true를 반환 해야 합니다.
* **d:HttpStatusCode:** hello hello 사례 hello 조건 일치에 마켓플레이스에서 반환 되어야 하는 HTTP 상태 코드입니다. 마켓플레이스 signalizes HTTP 상태 코드를 통해 오류 toohello 사용자입니다. HTTP 상태 코드의 목록은 http://en.wikipedia.org/wiki/HTTP_status_code에서 제공됩니다.
* **d:ErrorMessage:** – hello HTTP 상태 코드를 사용 하는 반환 된 toohello 최종 사용자는 hello 오류 메시지입니다. 기밀 정보가 포함되지 않은 친숙한 오류 메시지여야 합니다.

**d:Title** *(선택 사항)* -hello 제목 hello 함수를 설명할 수 있습니다. hello 제목 hello 값은에서 제공 됩니다.

* hello 선택적 지도 특성 (xpath) hello에 대 한 응답 toofind hello 제목 hello 서비스 요청에서 반환 되는 위치를 지정 합니다.
* -또는-hello 제목 hello 노드의 값으로 지정 합니다.

**d:Rights** *(선택 사항)* -hello hello 함수 연관 된 권한 (예: 저작권). hello 권한에 대 한 hello 값은에서 제공 됩니다.

* hello 선택적 지도 특성 (xpath) hello에 대 한 응답 toofind hello 권한 hello 서비스 요청에서 반환 되는 위치를 지정 합니다.
* -또는-hello 권한 hello 노드의 값으로 지정 합니다.

**d:Description** *(선택 사항)* -간단한 hello 함수에 대 한 설명입니다. hello 설명에 대 한 hello 값은에서 제공 됩니다.

* hello 선택적 지도 특성 (xpath) hello에 대 한 응답 toofind hello 설명 hello 서비스 요청에서 반환 되는 위치를 지정 합니다.
* -또는-hello 설명이 hello 노드의 값으로 지정 합니다.

**d:EmitSelfLink** - *위의 "반환된 데이터를 통해 '페이징'에 대한 FunctionImport" 예를 참조하세요.*

**d:EncodeParameterValue** -선택적 확장 tooOData

**d:QueryResourceCost** -선택적 확장 tooOData

**d:Map** -선택적 확장 tooOData

**d:Headers** -선택적 확장 tooOData

**d:Headers** -선택적 확장 tooOData

**d:Value** -선택적 확장 tooOData

**d:HttpStatusCode** -선택적 확장 tooOData

**d:ErrorMessage** -선택적 확장 tooOData

## <a name="parameter-node"></a>매개 변수 노드
이 노드가 나타내는 hello URI 서식 파일의 일부로 노출 되는 하나의 매개 변수 / hello FunctionImport 노드에 지정 된 본문을 요청 합니다.

Hello "매개 변수 요소" 노드에 대 한 매우 유용한 정보 문서 페이지에서 찾을 수 있으며 [여기](http://msdn.microsoft.com/library/ee473431.aspx) (사용 하 여 hello **기타 버전** 드롭다운 tooselect 필요한 tooview hello 설명서 하는 경우 다른 버전). *예제:* `<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| 매개 변수 특성 | 필수 여부 | 값 |
| --- | --- | --- |
| 이름 |예 |hello hello 매개 변수의 이름입니다. 대/소문자를 구분합니다.  Hello BaseUri 대/소문자와 일치 합니다. **예제:** `<Property Name="IsDormant" Type="Byte" />` |
| 형식 |예 |hello 매개 변수 형식입니다. hello 값 이어야 합니다는 **EDMSimpleType** 또는 hello 모델의 hello 범위 내에 있는 복합 형식입니다. 자세한 내용은 “지원되는 6가지 매개 변수/속성 유형”을 참조하세요.  (대/소문자를 구분합니다. 첫 번째 문자는 대문자, 나머지는 소문자입니다.)  또한 [개념적 모델 형식(CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx)도 참조하세요. **예제:** `<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |아니요 |****, Out 또는 InOut hello 매개 변수는 입력, 출력 또는 입력/출력 매개 변수 인지에 따라 합니다. (Azure 마켓플레이스에서는 "IN"만 사용할 수 있습니다.) **예제:** `<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |아니요 |hello 최대 허용 길이인 hello 매개 변수입니다. **예제:** `<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| 자릿수 |아니요 |hello 매개 변수는 hello 전체 자릿수입니다. **예제:** `<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| 확장 |아니요 |hello 소수 hello 매개 변수입니다. **예제:** `<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

hello 다음은 toohello CSDL 사양에 추가 된 hello 특성입니다.

| 매개 변수 특성 | 설명 |
| --- | --- |
| **d:Regex** *(선택 사항)* |Regex 문을 hello 매개 변수에 대 한 toovalidate hello 입력된 값을 사용 합니다. Hello 입력된 값에는 hello 문을 hello 값과 일치 하지 않는 경우 거부 됩니다. 이렇게 하면 toospecify도의 가능한 값을 집합 예: ^ [0-9] +? $ tooonly 번호를 허용 합니다. **예:** `<Parameter Name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters" d:SampleValues="George |
| **d:Enum** *(선택 사항)* |Hello 매개 변수에 대 한 유효한 값 목록을 구분 하는 파이프 합니다. hello 값의 hello 형식 toomatch hello 정의 된 유형의 hello 매개 변수를 필요합니다. 예: `english |
| **d: Nullable** *(선택 사항)* |매개 변수가 null일 수 있는지 여부를 정의할 수 있습니다. hello 기본값은: true. 그러나 hello URI 템플릿에 hello 경로의 일부로 노출 되는 매개 변수는 null 일 수 없습니다. Hello 특성이 toofalse-이러한 매개 변수에 대해 설정 되 면 hello 사용자 입력은 무시 됩니다. **예제:** `<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(선택 사항)* |Hello UI에서에서 참고 toohello 클라이언트로 예제 값 toodisplay 합니다.  수 즉, 파이프를 사용 하 여 여러 값이 구분 tooadd 목록 '는 |

## <a name="entitytype-node"></a>EntityType 노드
이 노드는 마켓플레이스 toohello 최종 사용자 로부터 반환 되는 hello 형식 중 하나를 나타냅니다. 또한 toohello 최종 사용자에 반환 되는 hello 콘텐츠 공급자의 서비스 toohello 값에 의해 반환 되는 hello 출력에서 hello 매핑을 포함 합니다.

이 노드에 대 한 세부 정보에서 발견 되 [여기](http://msdn.microsoft.com/library/bb399206.aspx) (사용 하 여 hello **기타 버전** 드롭다운 tooselect 필요한 tooview hello 설명서 하는 경우 다른 버전입니다.)

| 특성 이름 | 필수 여부 | 값 |
| --- | --- | --- |
| 이름 |예 |hello 엔터티 형식의 hello 이름입니다. **예제:** `<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |아니요 |hello 정의 되는 hello 엔터티 형식의 기본 형식입니다. 다른 엔터티 형식의 hello 이름입니다. **예제:** `<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

hello 다음은 toohello CSDL 사양에 추가 된 hello 특성입니다.

**d:Map** -hello 서비스 출력에 대해 실행 되는 XPath 식입니다. hello 여기 된다고 가정해 ATOM 피드 처럼 hello 서비스 출력을 반복 하는 요소 집합을 포함 반복 되는 항목 노드 집합이 있습니다. 이러한 반복 노드는 하나의 레코드를 포함합니다. 개별 레코드에 대 한 hello 값을 포함 하는 hello 콘텐츠 공급자의 서비스 결과의 개별 반복 노드에 hello에 지정 된 toopoint hello XPath는입니다. Hello 서비스에서 출력 예:

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

각 hello 모음 노드는 hello 반복 hello의 노드에서 출력 및 hello toohello 최종 사용자에 반환 되는 실제 콘텐츠를 포함 하기 때문에 XPath 식 hello /foo/bar 것입니다.

**Key** - 이 특성은 마켓플레이스에서 무시됩니다. 일반적으로 REST 기반 웹 서비스는 기본 키를 노출하지 않습니다.

## <a name="property-node"></a>속성 노드
이 노드는 hello 레코드의 한 속성을 포함합니다.

이 노드에 대 한 세부 정보에서 발견 되 [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (사용 하 여 hello **기타 버전** 드롭다운 tooselect 필요한 tooview hello 설명서 하는 경우 다른 버전입니다.) *예제:* `<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| 특성 이름 | 필수 | 값 |
| --- | --- | --- |
| 이름 |예 |hello 속성의 hello 이름입니다. |
| 형식 |예 |hello 형식 hello 속성 값입니다. hello 속성 값 형식 이어야 합니다는 **EDMSimpleType** 또는 hello 모델의 범위 내에 있는 복합 형식 (정규화 된 이름으로 표시 됨). 자세한 내용은 개념적 모델 유형(CSDL)을 참조하세요. |
| Nullable |아니요 |**True 이면** (기본값 hello) 또는 **False** hello 속성이 null 값을 가질 수 있는지 여부에 따라 합니다. 참고: hello CSDL 버전으로 표시 hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) 네임 스페이스, 복합 형식 속성은 Nullable = "False"입니다. |
| DefaultValue |아니요 |hello hello 속성의 기본 값입니다. |
| MaxLength |아니요 |hello hello 속성 값의 최대 길이입니다. |
| FixedLength |아니요 |**True 이면** 또는 **False** fiexed 길이 문자열로 hello 속성 값은 저장 하는 여부에 따라 합니다. |
| 자릿수 |아니요 |Hello 숫자 값의 자릿수 tooretain toohello 최대 수를 의미합니다. |
| 확장 |아니요 |Hello 숫자 값에서 소수 자릿수 tooretain의 최대 수입니다. |
| Unicode |아니요 |**True 이면** 또는 **False** hello 속성 값 수 있는지 여부에 따라 유니코드 문자열로 저장 합니다. |
| Collation |아니요 |Hello 시퀀스 toobe hello 데이터 원본에 사용 되는 데이터 정렬 지정 하는 문자열입니다. |
| ConcurrencyMode |아니요 |**None** (기본값 hello) 또는 **Fixed**합니다. Hello 값이 너무 설정**Fixed**, 낙관적 동시성 검사에 hello 속성 값이 사용 됩니다. |

hello 다음 toohello CSDL 사양에 추가 된 hello 추가 특성은입니다.

**d:Map** -hello 서비스에 대해 실행 되는 XPath 식을 출력 및 hello 출력의 한 속성을 추출 합니다. 지정 된 XPath hello hello EntityType 노드의 XPath에서 선택 된 노드를 반복 하는 상대 toohello입니다. 정적 리소스를 포함 하 여 각 hello에는 절대 XPath tooallow 출력 hello에 원래 서비스 출력 되지만 각 hello OData의에서 hello 행에 있는 것은 발견 된 저작권 정보 예를 들어 같은 노드 가능한 toospecify 이기도 출력입니다. Hello 서비스에서 예제:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

여기에 XPath 식을 hello hello 콘텐츠 공급자의 서비스에서./bar/baz0 tooget hello baz0 노드 것입니다.

**d:CharMaxLength** -문자열 유형에 대 한 hello 최대 길이 지정할 수 있습니다. DataService CSDL 예를 참조하세요.

**d:IsPrimaryKey** -hello 열 hello 테이블/뷰의 기본 키 hello 인지 여부를 나타냅니다. DataService CSDL 예를 참조하세요.

**d:isExposed** -hello 테이블 스키마가 노출 하는 경우 결정 (일반적으로 true). DataService CSDL 예를 참조하세요.

**d:IsView** *(선택 사항)* - 테이블이 아닌 보기를 기반으로 할 경우 true입니다.  DataService CSDL 예를 참조하세요.

**d:Tableschema** - DataService CSDL 예를 참조하세요.

**d:ColumnName** -hello hello 테이블/뷰의 hello 열 이름입니다.  DataService CSDL 예를 참조하세요.

**d:IsReturned** -는 hello hello 서비스 값 toohello 클라이언트에이 통해 노출 하는 경우를 결정 하는 부울 값입니다.  DataService CSDL 예를 참조하세요.

**d:IsQueryable** -는 hello hello 열 데이터베이스 쿼리에서 사용할 수 있는지 여부를 나타내는 Boolean입니다.   DataService CSDL 예를 참조하세요.

**d:OrdinalPosition** -는 hello 열의 숫자의 위치, x, hello 테이블이 나 hello 뷰의 모양 여기서 x는 hello 테이블의 열 수가 1 toohello에서 합니다.  DataService CSDL 예를 참조하세요.

**d:DatabaseDataType** -hello 데이터베이스, 즉, SQL 데이터 형식에에서 대 한 hello 열의 hello 데이터 형식이 있습니다. DataService CSDL 예를 참조하세요.

## <a name="supported-parametersproperty-types"></a>지원되는 매개 변수/속성 유형
hello 다음은 매개 변수 및 속성에 대 한 지원 hello 형식입니다. (대/소문자 구분)

| 기본 유형 | 설명 |
| --- | --- |
| Null |값이 hello 없음을 나타냅니다. |
| Boolean |Hello 이진 값 논리의 수학적 개념을 나타냅니다. |
| Byte |부호 없는 8비트 정수 값 |
| DateTime |값 A.D. 1753 년 1 월 1 일 12시: 00 자정에서 날짜 및 시간을 나타냅니다. 서 기 9999 년 12 월 오후 11시 59분: 59를 통해 |
| 10진수 |고정 전체 자릿수와 소수 자릿수를 사용하여 숫자 값을 나타냅니다. 이 형식에서 + 10 사이의 숫자 값을 설명할 수 ^255 + 1 toopositive 10 ^-255 1 |
| Double |약 ±2.23e-308부터 ±1.79e+308 사이의 값을 표시할 수 있는 15자리의 부동 소수점 숫자를 나타냅니다. **10 진수를 사용 하 여 tooExel 내보내기 문제 기한** |
| 단일 |약 ±1.18e-38부터 ±3.40e+38 사이의 값을 표시할 수 있는 7자리의 부동 소수점 숫자를 나타냅니다. |
| Guid |16바이트(128비트) 고유 식별자 값을 나타냅니다. |
| Int16 |부호 있는 16비트 정수 값을 나타냅니다. |
| Int32 |부호 있는 32비트 정수 값을 나타냅니다. |
| Int64 |부호 있는 64비트 정수 값을 나타냅니다. |
| String |고정 또는 가변 길이 문자 데이터를 나타냅니다. |

## <a name="see-also"></a>참고 항목
* 이 문서를 읽을 전반적인 OData 매핑 프로세스 및 목적을 이해에서 하려는 경우 hello [데이터 서비스 OData 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview 정의 구조체 및 지침입니다.
* 예를 검토 하려는 경우이 문서를 읽어 보세요. [데이터 서비스 OData 매핑 예제](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee 샘플 코드와 코드 구문 및 컨텍스트를 이해 합니다.
* 이 문서를 참조 데이터 서비스 toohello Azure 마켓플레이스에서 게시에 대 한 경로 지정 하는 tooreturn toohello [데이터 서비스에 대 한 게시 가이드](marketplace-publishing-data-service-creation.md)합니다.
