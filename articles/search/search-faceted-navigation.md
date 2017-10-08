---
title: "Azure 검색의 aaaHow tooimplement 패싯 탐색 | Microsoft Docs"
description: "Azure 검색에서는 Microsoft Azure에서 호스팅되는 클라우드 검색 서비스와 통합 되는 패싯 탐색 tooapplications를 추가 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>어떻게 Azure 검색의 tooimplement 패싯 탐색
패싯 탐색은 검색 응용 프로그램에서 자기 주도형 드릴다운 탐색을 제공하는 필터링 메커니즘입니다. hello 용어 '패싯 탐색' 친숙 하 고 있지만 아마도 사용 하기 전에. 다음 예제와 hello, 패싯 탐색은 hello 4 가지 범주가 사용 toofilter 결과 불과합니다.

 ![Azure Search 작업 포털 데모][1]

패싯 탐색은 대체 항목 지점 toosearch입니다. 제공 편리한 대체 tootyping 복잡 한 검색 식 직접 합니다. 패싯을 사용하면 원하는 항목을 쉽게 찾을 수 있으며 항상 결과를 얻을 수 있습니다. 개발자는 패싯 검색 모음을 탐색 하기 위한 가장 유용한 검색 조건을 hello를 노출할 수 있습니다. 온라인 소매 응용 프로그램에서는 종종 브랜드, 부서(어린이 신발), 크기, 가격, 인기도 및 등급에 대한 패싯 탐색이 작성됩니다. 

패싯 탐색의 구현은 검색 기술에 따라 다릅니다. Azure Search에서는 이전에 스키마에서 특성을 지정한 필드를 사용하여 쿼리 시 패싯 탐색이 작성됩니다.

-   응용 프로그램 빌드, 쿼리를 보내야 하는 hello 쿼리에서 *패싯 쿼리 매개 변수* tooget hello 사용할 수 있는 패싯 필터 값 해당 문서에 대 한 결과 집합입니다.

-   tooactually 자르기 hello 문서 결과 집합, hello 응용 프로그램에도 적용 해야는 `$filter` 식입니다.

응용 프로그램 개발에서 쿼리를 생성 하는 코드 작성 hello 대량의 hello 작업을 구성 합니다. 대부분 패싯 탐색에서 예상 하는 hello 응용 프로그램 동작의 범위를 정의 하 고 패싯 결과 대 한 개수를 가져오는 대 한 기본 제공 지원을 비롯 하 여 hello 서비스에 의해 제공 됩니다. hello 서비스도 수행할 수 있는 실제 기본값 다루기 탐색 구조를 방지 합니다. 

## <a name="sample-code-and-demo"></a>샘플 코드 및 데모
이 문서에서는 구직 검색 포털을 예로 사용합니다. hello 예제는 ASP.NET MVC 응용 프로그램으로 구현 됩니다.

-   참조 및 hello 작업 데모 온라인에서 테스트 [Azure 검색 작업 포털 데모](http://azjobsdemo.azurewebsites.net/)합니다.

-   Hello에서 hello 코드 다운로드 [GitHub의 Azure 샘플 리포지토리](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)합니다.

## <a name="get-started"></a>시작
을 사용 하는 새로운 toosearch 개발 hello 가장 좋은 방법은 toothink 패싯 탐색의 경우 자체 방향이 지정 된 검색에 대 한 hello 가능성을 표시 합니다. 패싯 탐색은 포인트 클릭 동작을 통해 검색 결과의 범위를 신속하게 좁히는 데 사용되는 미리 정의된 필터를 기반으로 하는 드릴다운 검색 환경에 일종입니다. 

### <a name="interaction-model"></a>상호 작용 모델

hello 검색 패싯 탐색의 경우 반복적으로 하겠습니다를 일련의 쿼리 응답 toouser 작업에 펼치려면를 이해 하 여 시작 합니다.

hello 시작 지점에는 일반적으로 hello 주변에 배치 하는 패싯 탐색을 제공 하는 응용 프로그램 페이지입니다. 패싯 탐색은 각 값에 대한 확인란 또는 클릭할 수 있는 텍스트가 포함된 트리 구조인 경우가 많습니다. 

1. 전송 tooAzure 검색 쿼리는 하나 이상의 패싯 쿼리 매개 변수를 통해 hello 패싯 탐색 구조를 지정 합니다. 예를 들어 hello 쿼리 포함 될 수 있습니다 `facet=Rating`, 등을 사용는 `:values` 또는 `:sort` 옵션 toofurther hello 프레젠테이션 구체화 합니다.
2. hello 프레젠테이션 계층 hello 요청에 지정 된 hello 패싯을 사용 하 여 패싯 탐색을 제공 하는 검색 페이지를 렌더링 합니다.
3. 등급이 4 이상이 인 제품만 표시 해야 하는 "4" tooindicate 클릭 등급을 포함 하는 패싯 탐색 구조를 지정 합니다. 
4. 응답으로 hello 응용 프로그램 포함 하는 쿼리를 보냅니다.`$filter=Rating ge 4` 
5. hello 프레젠테이션 계층 업데이트 hello 페이지 hello 새 조건을 충족 하는 해당 항목을 포함 하는 축소 된 결과 집합을 보여 주는 (이 경우 제품 등급 4 이상).

패싯은 쿼리 매개 변수이지만 쿼리 입력과 혼동해서는 안 됩니다. 쿼리의 선택 조건으로 사용되지 않습니다. 대신, 이라고 패싯 쿼리 매개 변수 다시 hello 응답에 제공 된 입력 toohello 탐색 구조. 각 패싯 쿼리 매개 변수에 제공한 Azure 검색 문서는 각 패싯 값에 대 한 hello 부분 결과에 평가 합니다.

공지 hello `$filter` 4 단계에서 합니다. hello 필터는 패싯 탐색의 중요 한 측면입니다. 패싯 및 필터는 hello API에서에서 관련이, 하려는 두 toodeliver hello 경험을 해야 합니다. 

### <a name="app-design-pattern"></a>앱 디자인 패턴

응용 프로그램 코드에서 hello 방법은 toouse 패싯 쿼리 매개 변수 tooreturn hello 패싯 탐색 구조와 함께 패싯 결과 $filter 식입니다.  hello 필터 식 핸들 hello는 hello 패싯 값에는 이벤트를 클릭 합니다. Hello 간주할 `$filter` hello 코드 숨김 hello 실제 트리밍으로 검색 결과의 식 toohello 프레젠테이션 계층을 반환 합니다. 색 패싯을 매개 변수로 받아을 통해 구현 됩니다 빨간색 hello 색을 클릭 하는 `$filter` 선택 항목에는 빨간색의 색만 식입니다. 

### <a name="query-basics"></a>쿼리 기본 사항

Azure 검색에서는 하나 이상의 쿼리 매개 변수를 통해 요청이 지정됩니다(각 매개 변수에 대한 설명은 [문서 검색](http://msdn.microsoft.com/library/azure/dn798927.aspx) 참조). Hello 쿼리 매개 변수 모두가 필요 하지만 쿼리 toobe 유효 하려면에서 하나 이상 있어야 합니다.

전체 자릿수, 이해 하는 hello 관련이 없는 적중 아웃 toofilter 기능을 통해 얻습니다 이러한 식 중 하나 이상이:

-   **search=**  
    이 매개 변수 값 hello hello 검색 식을 구성합니다. 단일 텍스트 조각 또는 여러 항 및 연산자를 포함하는 복잡한 검색 식일 수 있습니다. Hello 서버에서 검색 식 결과에 반환 용어 일치에 대 한 hello 인덱스의 검색 가능 필드를 쿼리 하는 전체 텍스트 검색에 사용 됩니다. 설정한 경우 `search` hello 전체 인덱스 toonull, 쿼리 실행 됩니다 (즉, `search=*`). Hello의 다른 요소와 같은 쿼리 되는,이 `$filter` hello 반환 되는 문서에 영향을 주는 주요 요소는 점수 매기기 프로필, 또는 `($filter`) 어떤 순서로 (`scoringProfile` 또는 `$orderby`).

-   **$filter=**  
    필터는 특정 문서 특성의 hello 값을 기반으로 하는 검색 결과의 hello 크기 제한에 대 한 강력한 메커니즘입니다. A `$filter` 를 먼저 평가 hello 사용 가능한 값과 각 값에 대 한 해당 수를 생성 하는 패싯 논리 이어서

복잡 한 검색 식에는 hello 쿼리의 hello 성능이 저하 됩니다. 가능한 경우 제대로 생성 된 필터 식을 tooincrease 정밀도 사용 및 쿼리 성능을 향상 시킵니다.

toobetter 보다 정밀 하 게 필터를 추가 하는 방법을 이해, 필터 식을 포함 하는 복잡 한 검색 식 tooone 비교 합니다.

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

두 쿼리는 유효 하지만 hello 둘째 더 우수 비-적합 하지 않습니다 시애틀에 주차 된 찾고 있는 경우.
-   hello 첫 번째 쿼리는 이름, 설명 및 검색 가능한 데이터가 포함 된 다른 모든 필드와 같은 문자열 필드에 언급 되지 않은 되거나 언급 되 해당 특정 단어에 의존 합니다.
-   hello 두 번째 쿼리는 구조화 된 데이터에서 일치 하는 정확한 찾은 가능성이 toobe 더욱 정확 하 게 됩니다.

패싯 탐색이 포함된 응용 프로그램에서는 패싯 탐색 구조에 대한 각 사용자 작업이 수행된 후 검색 결과 범위를 좁혀야 합니다. toonarrow 결과 필터 식을 사용 합니다.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>패싯 탐색 앱 구축
Hello 검색 요청을 작성 하는 응용 프로그램 코드에서 Azure 검색을 사용 하 여 패싯 탐색을 구현 합니다. 이전에 정의 된 스키마의 요소를 의존 하는 hello 패싯 탐색 합니다.

검색 인덱스에 미리 정의 된 hello `Facetable [true|false]` 특성을 인덱싱하거나 tooenable 선택한 필드에 설정, 패싯 탐색 구조에서 사용 되는 사용 하지 않도록 설정 합니다. `"Facetable" = true`가 아니면 패싯 탐색에서 필드를 사용할 수 없습니다.

코드에서 프레젠테이션 계층 hello hello 사용자 환경을 제공합니다. 상자 hello hello 패싯 탐색 hello 레이블, 값, 확인란, hello count 등의 구성 요소를 나열 해야 합니다. hello Azure 검색 REST API는 플랫폼과 별 관계가, 모든 언어 및 플랫폼을 사용 합니다. hello 중요 한 점은 tooinclude UI 요소를 지 원하는 증분 새로 고침, 업데이트 된 UI 상태와 각 추가 패싯을 선택 합니다. 

쿼리 시간에 응용 프로그램 코드를 포함 하는 요청 만듭니다 `facet=[string]`, hello 필드 toofacet에서 제공 하는 요청 매개 변수입니다. `&facet=color&facet=category&facet=rating`과 같이 각 패싯을 앰퍼샌드(&) 문자로 구분하여 여러 패싯을 쿼리에 지정할 수 있습니다.

응용 프로그램 코드 구성도 해야는 `$filter` 식 toohandle hello 패싯 탐색 창에서 이벤트를 클릭 합니다. A `$filter` hello 검색 결과 hello 패싯 값을 사용 하 여 필터 조건으로 감소 합니다.

Azure 검색 업데이트 toohello 패싯 탐색 구조와 함께 입력 하는 하나 이상의 조건에 따른 hello 검색 결과 반환 합니다. Azure 검색에서 패싯 탐색은 패싯 값과 각 값에 대해 발견된 결과 수로 이루어진 단일 수준 구성입니다.

Hello 다음 섹션, 방법 자세히 보기 걸릴 toobuild 각 부분입니다.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Hello 인덱스를 작성
이 인덱스 특성을 통해 hello 인덱스에서 필드 별로으로 패싯 사용 됨: `"Facetable": true`합니다.  
패싯 탐색에 사용할 수 있는 모든 필드 형식은 기본적으로 `Facetable` 입니다. 이러한 필드 형식에는 `Edm.String`, `Edm.DateTimeOffset`, 모든 hello 숫자 필드 형식 및 (기본적으로, 모든 필드 유형에 제외 하 고 facetable `Edm.GeographyPoint`, 패싯 탐색에 사용할 수 없습니다). 

인덱스를 작성할 때 패싯 탐색에 대 한 가장 좋은 방법은 꺼져 tooexplicitly turn 패싯 패싯으로 사용 하면 안 되는 필드에 있습니다.  특히, ID 또는 제품 이름, 같은 단일 항목 값에 대 한 문자열 필드 설정할지 너무`"Facetable": false` tooprevent 패싯 탐색에 사용 하 여 자신의 실수로 (및 비효율적인). 패싯 접속이 필요 없는 해제 하면 hello 인덱스의 hello 크기를 작게 유지 하는 데 도움이 되 고 일반적으로 성능이 향상 됩니다.

다음은 몇 가지 특성 tooreduce hello 크기로 잘린 hello 작업 포털 데모 샘플 앱에 대 한 hello 스키마의 일부입니다.

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Hello 샘플 스키마에서 볼 수 있듯이 `Facetable` ID 값과 같은 패싯으로 사용 하면 안 되는 문자열 필드에 꺼져 있습니다. 패싯 접속이 필요 없는 해제 하면 hello 인덱스의 hello 크기를 작게 유지 하는 데 도움이 되 고 일반적으로 성능이 향상 됩니다.

> [!TIP]
> 모범 사례로, 각 필드에 대 한 인덱스 특성의 hello 전체 집합을 포함 합니다. 하지만 `Facetable` 각 특성 얻을 수 있습니다 각 스키마 의사 결정의 hello 의미를 통해 의도적으로 설정 하는 거의 모든 필드에는 기본적으로 설정 됩니다. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Hello 데이터 검사
데이터의 품질 hello 하 되는 대로 hello 패싯 탐색 구조를 구체화 여부에 직접적인 영향을 미칩니다. Hello 쉽게를 생성할 수 있다는 필터 tooreduce hello 결과 집합에도 영향을 줍니다.

각 문서에 대 한 값을 포함 해야 toofacet 브랜드 또는 가격을 하려는 경우 *BrandName* 및 *ProductPrice* 유효 하 고 생산성 필터 옵션을 일관 되 합니다.

에 대 한 어떤 tooscrub의 몇 가지 미리 알림은 다음과 같습니다.

* Toofacet 하 여 원하는 모든 필드에 대 한 자문해 값 자체 방향이 지정 된 검색의 필터와 적합 한을 포함 합니다. hello 값 짧고 설명적 충분히 고유한 toooffer 경쟁 옵션 중 하나를 지우기 선택 해야 합니다.
* 맞춤법 오류 또는 거의 일치하는 값. 경우 hello 색 필드에 따라 패싯 모두를 선택 하는, 색 및 필드 값에서 패싯을 포함 주황색 및 Ornage (맞춤법 오류).
* 대/소문자가 혼합된 텍스트도 패싯 탐색에서 나타날 수 있습니다. 예를 들어 orange와 Orange가 두 가지 값으로 표시됩니다. 
* 단일 및 복수 버전의 hello 동일한 값 각각에 대해 별도 패싯에 발생할 수 있습니다.

상상할 수 있듯이 성실 hello 데이터 준비는 효과적인 패싯 탐색의 필수 요소입니다.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Hello UI 빌드
Hello 프레젠테이션 계층에서 다시 작업할 수 그렇지 않은 경우 누락 될 수 있습니다 하 고 어떤 기능에 필수적인 toohello을 이해 하는 요구 사항을 클릭 하면 도움말 검색 환경을 합니다.

패싯 탐색 측면에서 웹 또는 응용 프로그램 페이지 hello 패싯 탐색 구조를 표시, hello 페이지에서 사용자 입력을 검색 및 변경 하는 hello 요소를 삽입 합니다. 

AJAX 웹 응용 프로그램에서는 일반적으로 증분 변경 내용을 toorefresh 수 있기 때문에 hello 프레젠테이션 계층에 사용 됩니다. ASP.NET MVC 또는 HTTP를 통해 tooan Azure 검색 서비스에 연결할 수 있는 다른 시각화 플랫폼을 사용할 수도 있습니다. hello 샘플 응용 프로그램에서 참조 된이 문서 hello **Azure 검색 작업 포털 데모** – toobe ASP.NET MVC 응용 프로그램에 발생 합니다.

Hello 샘플에서 패싯 탐색 hello 검색 결과 페이지에 포함 됩니다. 다음 예제에서는 hello에서 가져온 hello `index.cshtml` 패싯 탐색 hello 검색에 표시 하기 위한 표시 hello 정적 HTML 구조 hello 샘플 응용 프로그램의 파일 결과 페이지입니다. 패싯 목록이 hello 작성 하거나 검색 용어를 제출 또는 선택 하거나 패싯의 선택을 취소 하면 동적으로 다시 작성 합니다.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

다음 코드 조각에서 hello hello `index.cshtml` 페이지 hello HTML toodisplay hello 첫 번째 패싯, 직함을 동적으로 작성 합니다. 유사한 기능을 동적으로 hello에 대 한 HTML hello 패싯 지정할 합니다. 각 패싯 레이블과 hello 해당 패싯 결과 대 한 항목 수를 표시 하는 개수에 있습니다.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Hello 검색 결과 페이지를 디자인할 때 tooadd 패싯을 지우기 위한 메커니즘을 기억 합니다. 확인란을 추가 하는 경우 tooclear hello 필터링 하는 방법을 쉽게 확인할 수 있습니다. 다른 레이아웃에는 이동 경로 탐색 패턴 또는 다른 창의적인 방법이 필요할 수 있습니다. 예를 들어 hello 작업 검색 포털 샘플 응용 프로그램에서에서 클릭할 수 있는 hello `[X]` 선택한 패싯 tooclear hello 패싯 후 합니다.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Hello 쿼리 작성
쿼리 작성을 위한 작성 하는 hello 코드 tooformulate 요청을 사용 하는 모든 부분의 검색 식, 패싯, 필터, 점수 매기기 프로필 – 모든 항목을 포함 하 여 올바른 쿼리를 지정 해야 합니다. 이 섹션에서는 패싯 필요한 경우 쿼리 및 패싯 toodeliver와 필터는 사용 하는 방법에 축소 된 탐색 결과 집합입니다.

패싯은 이 샘플 응용 프로그램의 필수 요소입니다. hello 포털 데모 작업에서에서 hello 검색 환경 패싯 탐색 및 필터 기반으로 설계 되었습니다. 패싯 탐색 hello 페이지의 hello 두드러진 배치의 중요성을 보여 줍니다. 

예로 것이 좋습니다 toobegin 경우가 많습니다. 다음 예제에서는 hello에서 가져온 hello `JobsSearch.cs` 파일을 빌드 비즈니스 제목, 위치, 게시 유형 및 최소 급여에 따라 만드는 패싯 탐색 요청 합니다. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

패싯 쿼리 매개 변수가 설정 되어 tooa 필드 고 hello 데이터 형식에 따라 추가로 매개 변수화 할 수를 포함 하는 쉼표로 구분 된 목록으로 `count:<integer>`, `sort:<>`, `interval:<integer>`, 및 `values:<list>`합니다. 값 목록은 범위를 설정할 때 숫자 데이터에 대해 지원됩니다. 자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) 을 참조하세요.

응용 프로그램에 의해 공식화 hello 요청, 면 함께 필터 toonarrow hello 문서 집합을 후보 패싯 값 선택 항목을 아래로 작성 해야 합니다. 패싯 탐색 자전거 저장소에 대 한 단서 tooquestions와 같은 제공 *사용할 수 있는 어떤 색, 제조업체 및 자전거 유형의?*합니다. 필터링은 *이 가격대의 빨간색 산악용 자전거는 무엇입니까?*와 같은 질문에 답변합니다. 만 빨간색 제품 표시할지, "Red" tooindicate를 클릭할 때 hello 다음 쿼리 hello 응용 프로그램이 포함 되어 보낼 `$filter=Color eq ‘Red’`합니다.

다음 코드 조각에서 hello hello `JobsSearch.cs` 페이지 hello 비즈니스 제목 패싯의 값을 선택할 경우 선택한 hello 비즈니스 제목 toohello 필터를 추가 합니다.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>팁 및 모범 사례

### <a name="indexing-tips"></a>인덱싱 팁
**검색 상자를 사용하지 않을 경우 인덱스 효율성 향상**

응용 프로그램 패싯 탐색에 독점적으로 사용 하는 경우 (즉, 없음 검색 상자)로 hello 필드를 표시할 수 있습니다 `searchable=false`, `facetable=true` tooproduce 인덱스를 더욱 간결 하 합니다. 또한 인덱싱 전체 패싯 값이 없는 단어 잘림 또는 다중 단어 값의 hello 구성 요소 부분의 인덱싱에 대해서만 발생 합니다.

**패싯으로 사용할 수 있는 필드 지정**

해당 hello 회수 hello 인덱스의 스키마는 패싯으로 사용할 수 있는 toouse 있는 필드를 결정 합니다. Hello 쿼리 필드 facetable로 가정 하 고 여는 필드 toofacet를 지정 합니다. 패싯이 hello 필드 hello 레이블 아래에 표시 되는 hello 값을 제공 합니다. 

각 레이블에 아래에 표시 되는 hello 값 hello 인덱스에서 검색 됩니다. 예를 들어 hello 패싯 필드는 *색*, hello 추가 필터링에 사용할 수 있는 값이 됩니다 hello-해당 필드에 대 한 빨간색, 검정, 등입니다.

숫자 및 날짜/시간 값에만, 명시적으로 값을 설정할 수 hello 패싯 필드 (예를 들어 `facet=Rating,values:1|2|3|4|5`). 이러한 필드 형식 toosimplify hello 분리 패싯 결과의 연속 범위 (숫자 값 이나 전체 기간에 따라 범위 중 하나)에 값 목록을 허용 됩니다. 

**기본적으로 한 수준의 패싯 탐색만 유지 가능** 

계층 구조에서 패싯 중첩은 직접 지원되지 않습니다. 기본적으로 Azure Search의 패싯 탐색은 하나의 필터 수준만 지원합니다. 그러나 해결 방법이 있습니다. `Collection(Edm.String)` 의 계층적 패싯 구조를 계층당 하나의 항목으로 인코딩할 수 있습니다. 이 해결 방법을 구현 하는 것은이 문서의 hello 다루지 않습니다. 

### <a name="querying-tips"></a>쿼리 팁
**필드의 유효성 검사**

신뢰할 수 없는 사용자 입력에 따라 동적으로 패싯의 hello 목록을 작성 하는 경우 hello hello 패싯 필드 이름이 유효한 지 확인 합니다. 또는 중 하나를 사용 하 여 Url 작성 시 hello 이름을 이스케이프 `Uri.EscapeDataString()` .NET 또는 선택한 플랫폼에서 동일한 hello에 있습니다.

### <a name="filtering-tips"></a>필터링 팁
**필터로 검색 정확도 향상**

필터를 사용합니다. 에 의존 하는 경우 검색 식만 단독으로 형태소 분석 문서 toobe 공격자는 hello 정확한 패싯 값이 해당 필드 중 하나에 없는 반환 합니다.

**필터로 검색 성능 향상**

필터는 hello 문서 집합을 후보 검색에 대 한 범위를 좁힐 하 고 순위에서 제외 합니다. 대량의 문서 집합이 있는 경우 엄선된 패싯 드릴다운을 사용하면 때로는 성능을 크게 향상시킬 수 있습니다.
  
**패싯 필드에 hello만 필터링**

패싯 드릴 다운에 일반적으로 원하는 tooonly 모든 검색 가능한 필드에서 아무 곳 이나 하지 hello 패싯 값이 특정 (패싯) 필드에 포함 된 문서를 포함 합니다. 필터를 추가 하 여 일치 하는 값에 대 한 hello 패싯 필드에만 서비스 toosearch hello hello 대상 필드에 도움이 되도록 합니다.

**추가 필터로 패싯 결과 자르기**

패싯 결과 패싯 용어와 일치 하는 hello 검색 결과는 문서입니다. 다음 예제에 대 한 검색 결과에서 hello에 *클라우드 컴퓨팅*, 254 항목 있습니다 *내부 사양* 콘텐츠 형식으로. 항목은 상호 배타적이지 않을 수 있습니다. 항목 필터 둘 모두의 hello 조건에 부합 하는 경우에 각각에서 계산 됩니다. 이러한 중복이 가능에 패싯 `Collection(Edm.String)` 필드는 종종 tooimplement 문서 태그를 사용 합니다.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

일반적으로 패싯 결과는 너무 큰 일관 되 게, 더 추가 하는 것이 좋습니다 찾을 필터링 toogive 사용자 hello 검색을 축소 하는 옵션이 더 합니다.

### <a name="tips-about-result-count"></a>결과 개수에 대한 팁

**Hello 패싯 탐색 창에서 항목 hello 수 제한**

Hello 탐색 트리의 각 패싯 필드에 대 한 기본 제한이 10 개의 값을 있습니다. 이 기본 탐색 구조에 대 한 때문에 합리적 hello 값 목록 tooa 관리 하기 쉬운 크기로 유지 합니다. 값 toocount 할당 하 여 hello 기본값을 재정의할 수 있습니다.

* `&facet=city,count:5`패싯 결과적으로 hello 처음 5 개 도시만 hello 최상위 결과 반환 되도록 지정 합니다. 검색 용어가 "공항"이고 일치 항목이 32개인 샘플 쿼리를 생각해 보세요. Hello 쿼리를 지정 하는 경우 `&facet=city,count:5`hello 검색 결과에서 대부분의 문서에 포함 된 hello로 처음 다섯 개의 고유한 도시의 hello hello 패싯 결과 필요 합니다.

공지 hello 패싯 결과 구별 검색 결과. 검색 결과 hello 쿼리와 일치 하는 모든 hello 문서입니다. 패싯 결과 각 패싯 값에 일치 하는 hello 됩니다. Hello 예제 검색 결과는 hello 패싯 분류 목록 (예에서 5)에 없는 도시 이름을 포함 합니다. 패싯 탐색을 통해 필터링된 결과는 사용자가 패싯을 지우거나 City 이외의 다른 패싯을 선택한 경우에 표시됩니다. 

> [!NOTE]
> 두 가지 이상의 형식이 있을 때 `count`를 설명하면 혼동을 일으킬 수 있습니다. hello 다음 표에서 제공 Azure 검색 API, 예제 코드 및 설명서 hello 용어 사용 방법에 대 한 간단한 요약 합니다. 

* `@colorFacet.count`<br/>
  프레젠테이션 코드 hello 패싯을 사용 하는 toodisplay hello 수가 패싯 결과에서 count 매개 변수를 표시 됩니다. 패싯 결과 개수 hello hello 패싯 용어 또는 범위에서 일치 하는 문서 수를 나타냅니다.
* `&facet=City,count:12`<br/>
  패싯 쿼리에서 count tooa 값을 설정할 수 있습니다.  hello 기본값은 10, 하지만 위쪽 또는 아래쪽에 설정할 수 있습니다. 설정 `count:12` 가져옵니다 문서 수에 따라 패싯 결과에서 상위 12 일치 하는 hello 합니다.
* "`@odata.count`"<br/>
  Hello 쿼리 응답에이 값 hello hello 검색 결과에 일치 하는 항목 수를 나타냅니다. 평균적으로 인해 hello 검색 단어와 일치 하는 항목의 toohello 존재 결합 하는 모든 패싯 결과의 hello 합계 보다 큽니다. 되었지만 패싯 값 일치 항목이 없습니다.

**패싯 결과의 개수 가져오기**

필터 tooa 패싯 쿼리를 추가 하면 tooretain hello 패싯 문 할 수 있습니다 (예를 들어 `facet=Rating&$filter=Rating ge 4`). 기술적으로 패싯 = 등급 필요 하지 않습니다 되지만 4 이상에 hello 등급에 대 한 패싯 값 수를 반환 지속적으로 업데이트 합니다. 예를 들어, "4"을 클릭 하 고 hello 쿼리에 포함 된 필터 크거나 너무 "4", 개수 반환 됩니다에 대 한 각 등급을 4 이상.  

**정확한 수의 패싯을 가져오는지 확인**

특정 상황에서는 경우가 패싯 수가 hello 결과 집합을 일치 하지 않으므로 (참조 [Azure 검색 (포럼 게시물)의 패싯 탐색](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

패싯 개수 toohello 분할 아키텍처 인해 정확 하 게 취소할 수 있습니다. 모든 검색 인덱스에 여러 분할 영역이 하 고 각 분할 결과 단일 구조로 결합 되는 문서 수에 따라 상위 n 개 면 hello를 보고 합니다. 분할 된 데이터베이스 일부가 여러 개의 일치 하는 값을 다른 사용자가 보다 적은 반면 일부 패싯 값이 누락 되었습니다 또는 아래 횟수가 계산 hello 결과에 알 수 있습니다.

Hello 수를 인위적으로 않아서 여 주위 사용할 수 있지만이 문제는 현재이 문제를 발생 하는 경우 언제 든 지 변경할 수 없습니다,:<number> 큰 숫자 tooenforce tooa 전체 각 분할에서 보고 합니다. 경우 수의 값을 hello: 보다 크거나 같은 toohello 숫자인 hello 필드의 고유 값의 정확한 결과 보장 됩니다. 그러나 문서 수가 많은 경우에는 성능이 저하되므로 이 옵션을 신중하게 사용해야 합니다.

### <a name="user-interface-tips"></a>사용자 인터페이스 팁
**패싯 탐색의 각 필드에 대한 레이블 추가**

레이블이 hello HTML 또는 폼에 일반적으로 정의 됩니다 (`index.cshtml` hello 예제 응용 프로그램에서). Azure Search에는 패싯 탐색 레이블 또는 다른 메타데이터에 사용할 수 있는 API가 없습니다.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>범위를 기준으로 필터링
값 범위에 대한 패싯은 일반적인 검색 응용 프로그램 요구 사항입니다. 범위는 숫자 데이터 및 DateTime 값에 대해 지원됩니다. 각 접근 방법에 대한 자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)을 참조하세요.

Azure 검색에서는 범위를 계산하는 두 가지 방법을 제공하여 범위 생성을 간소화합니다. 두 방법에 대 한 Azure 검색 hello 제공 된 hello 입력이 주어진 적절 한 범위를 만듭니다. 예를 들어 10|20|30 범위 값을 지정한 경우 0-10, 10-20, 20-30 범위가 자동으로 만들어집니다. 비어 있는 간격을 응용 프로그램에서 선택적으로 제거할 수도 있습니다. 

**Hello 간격 매개 변수를 사용 하는 접근 방식 1:**  
$10 단위로, tooset 가격 면을 지정 합니다.`&facet=price,interval:10`

**방법 2: 값 목록 사용**  
숫자 데이터의 경우 값 목록을 사용할 수 있습니다.  에 대 한 hello 패싯 범위를 고려는 `listPrice` 필드를 다음과 같이 렌더링 합니다.

  ![샘플 값 목록][5]

패싯 범위 hello hello 스크린 샷 앞에서 같은 toospecify 값 목록을 사용 합니다.

    facet=listPrice,values:10|25|100|500|1000|2500

각 범위는 시작점, 끝점으로 hello 목록에서 값으로 0을 사용 하 고 hello 이전 범위 toocreate 불연속 간격 잘린 후에 작성 됩니다. Azure Search는 이러한 작업을 패싯 탐색의 일부로 수행합니다. 각 간격의 구조를 지정 toowrite 코드가 없는 합니다.

### <a name="build-a-filter-for-a-range"></a>범위에 대한 필터 작성
선택한 범위에 따라 toofilter 문서 hello를 사용할 수 있습니다 `"ge"` 및 `"lt"` hello 범위의 hello 끝점을 정의 하는 두 부분으로 구성 식에서 연산자를 필터링 합니다. 예를 들어 선택한 경우 hello에 대 한 범위 10-25는 `listPrice` 필드가, hello 필터 잘립니다 `$filter=listPrice ge 10 and listPrice lt 25`합니다. Hello 필터 식을 사용 하 여 hello 샘플 코드에서 **priceFrom** 및 **priceTo** tooset hello 끝점 매개 변수입니다. 

  ![값 범위 쿼리][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>거리를 기준으로 필터링
일반적인 toosee 저장소나 restaurant, 근접 tooyour 현재 위치에 따라 대상을 선택 하는 데 도움이 되도록 필터링 합니다. 이 유형의 필터는 패싯 탐색처럼 보일 수 있지만 단순한 필터입니다. 특별히 이와 같은 특정 디자인 문제에 대한 구현 조언을 구하는 경우 이 점에 주의해야 합니다.

Azure Search에는 **geo.distance** 및 **geo.intersects**라는 두 개의 지리 공간 함수가 있습니다.

* hello **geo.distance** 함수 두 점 사이의 hello 거리 킬로미터 단위로 반환 합니다. 1 포인트 필드 이며 다른 하나는 hello 필터의 일부분으로 전달 되는 상수입니다. 
* hello **geo.intersects** 함수 해당된 지점이 특정된 다각형 내에 있으면 true를 반환 합니다. hello 포인트 필드 이며 hello 다각형 hello 필터의 일부분으로 전달 하는 좌표 상수 목록으로 지정 됩니다.

필터 예제는 [OData 식 구문(Azure 검색)](http://msdn.microsoft.com/library/azure/dn798921.aspx)에서 확인할 수 있습니다.

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Hello 데모를 시도 하십시오.
hello Azure 검색 작업 포털 데모가이 문서에서 참조 하는 hello 예제가 포함 되어 있습니다.

-   참조 및 hello 작업 데모 온라인에서 테스트 [Azure 검색 작업 포털 데모](http://azjobsdemo.azurewebsites.net/)합니다.

-   Hello에서 hello 코드 다운로드 [GitHub의 Azure 샘플 리포지토리](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)합니다.

검색 결과 사용할 때는 변경 쿼리 생성에 대 한 hello URL 살펴보십시오. 각 항목을 선택할 때이 응용 프로그램 tooappend 패싯 toohello URI에 발생 합니다.

1. hello 데모 응용 프로그램의 toouse hello 매핑 기능 hello에서 Bing 지도 키 가져오기 [Bing Maps 개발자 센터](https://www.bingmapsportal.com/)합니다. Hello에 기존 키 hello에 붙여넣습니다 `index.cshtml` 페이지. hello `BingApiKey` hello에서 설정 `Web.config` 파일 사용 되지 않습니다. 

2. Hello 응용 프로그램을 실행 합니다. Hello 선택적 둘러보기 걸리거나 hello 대화 상자를 닫습니다.
   
3. "분석가"와 같은 검색 용어를 입력 하 고 hello 검색 아이콘을 클릭 합니다. hello 쿼리가 신속 하 게 실행 됩니다.
   
   패싯 탐색 구조 hello 검색 결과 함께 반환 됩니다. Hello 검색 결과 페이지 hello 패싯 탐색 구조에 대 한 각 패싯 결과 수를 포함합니다. 패싯을 선택하지 않았으므로 일치하는 모든 결과가 반환됩니다.
   
   ![패싯을 선택하기 전의 검색 결과][11]

4. 직함, 위치 또는 최소 급여를 클릭합니다. 패싯 hello 초기 검색 시 null 되었지만 더 이상 일치 하는 항목의 hello 검색 결과 값을 사용 하는 대로 잘립니다.
   
   ![패싯을 선택한 후의 검색 결과][12]

5. tooclear hello 패싯 쿼리 다른 쿼리 동작을 시도할 수 있도록 클릭 hello `[X]` hello 패싯 tooclear hello 패싯을 선택 합니다.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>자세한 정보
[Azure Search 심층 정보](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410)를 살펴보세요. 에 45:25는 데모는 방법에 tooimplement 패싯 합니다.

패싯 탐색에 대 한 디자인 원칙에 더 많은 정보에 대 한 링크를 따라 hello를 것이 좋습니다.

* [패싯 검색을 위한 디자인](http://www.uie.com/articles/faceted_search/)
* [디자인 패턴: 패싯 탐색](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

