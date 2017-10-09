---
title: "Azure 검색에 대 한 쿼리 예제 aaaLucene | Microsoft Docs"
description: "Lucene은 유사 항목 검색, 근접 검색, 용어 상승, 정규식 검색 및 와일드카드 검색에 대해 구문을 쿼리합니다."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Lucene은 Azure 검색에서 퀴리를 만들기 위해 구문 예제를 쿼리합니다.
Azure 검색에 대 한 쿼리를 구성할 때 hello 기본값 중 하나를 사용할 수 있습니다 [단순 쿼리 구문을](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) hello 방법 [Azure 검색에서 쿼리 파서 Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)합니다. hello Lucene 쿼리 파서 필드 범위 쿼리에, 유사 항목 검색, 근접 검색, 용어 승격 정규식 검색과 같은 보다 복잡 한 쿼리 구문을 지원 합니다.

이 문서에서는 hello 전체 구문을 사용 하 여 사용 가능한 쿼리 작업을 보여 주는 예제를 단계별로 실행할 수 있습니다.

## <a name="viewing-hello-examples-in-jsfiddle"></a>Hello 예제 JSFiddle에서 보기

이 문서의 hello 예제 모두에 미리 로드 된 검색 인덱스에 대해 실행 되는 실행 가능한 쿼리 [JSFiddle](https://jsfiddle.net), 스크립트 및 HTML을 테스트 하기 위한 온라인 코드 편집기. 

toorun를 마우스 오른쪽 단추로 클릭 hello 쿼리 예제 Url tooopen JSFiddle 별도 브라우저 창에서.

> [!NOTE]
> hello 다음 예제에서는 활용 하 여 hello에서 제공 하는 데이터 집합에 따라 사용 가능한 작업으로 구성 된 검색 인덱스 [City의 뉴욕 방식인 개방형 데이터](https://nycopendata.socrata.com/) 이니셔티브입니다. 이 데이터는 최신 또는 완료로 간주되어서는 안 됩니다. hello 인덱스 Microsoft에서 제공 하는 샌드박스 서비스 켜져 있습니다. 불필요 한 Azure 구독 또는 Azure 검색 tootry 이러한 쿼리 합니다.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Tooinvoke 전체 Lucene 구문 분석 하는 방법

Hello를 지정 하는 모든이 문서의 예제 hello **queryType = 전체** Lucene 쿼리 파서 hello에 의해 처리 그 hello 전체 구문을 나타내는 매개 변수를 검색 합니다. 

**예제 1** --쿼리 조각 tooopen 새 브라우저에서 페이지에서 다음 마우스 오른쪽 단추 클릭 hello JSFiddle 로드 및 실행 hello 쿼리:

* [&queryType=full&search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

Hello 새 브라우저 창에서 hello JavaScript 소스 및 HTML 출력은 나란히 표시 합니다. 전체 쿼리 (뿐 아니라 hello 조각 hello 링크에 나와 있는 것 처럼)를 참조 하는 hello 스크립트. hello 전체 쿼리는 각 예제에 대 한 hello Url에 표시 됩니다. 

이 쿼리는 뉴욕시 작업 인덱스(샌드박스 서비스에 로드된 nycjobs)에서 문서를 반환합니다. 말해 hello 쿼리 비즈니스 타이틀만 반환 되도록 지정 합니다. hello 전체 기본 쿼리는 다음과 같습니다.

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

hello **searchFields** 매개 변수는 hello 검색 toojust hello 비즈니스 제목 필드를 제한 합니다. hello **queryType** 너무 설정**전체**,이 쿼리에 대 한 Azure 검색 toouse hello Lucene 쿼리 파서 게 지시 합니다.

> [!NOTE]
> 쿼리 처리에 대한 배경 정보를 보려면 [Azure Search에서 전체 텍스트 검색의 작동 방식](search-lucene-query-architecture.md)을 참조하세요. 검색 매개 변수에 대한 자세한 내용은 [Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)(문서 검색(Azure Search 서비스 REST API))를 참조하세요.
>

### <a name="fielded-query-operation"></a>필드 지정 쿼리 작업
지정 하 여이 문서의 hello 예제를 수정할 수는 **fieldname:searchterm** 생성 toodefine 여기서 hello 필드는 단일 단어 고 hello 검색 단어는 또한 한 단어 또는 구를, 한 쿼리 작업 경우에 따라의 부울 연산자 사용. Hello 다음 몇 가지 예입니다.

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

이 경우 두 개의 서로 다른 도시 hello 위치 필드에 대 한 검색에 하나의 항목으로 평가 하는 두 문자열 toobe 하려는 경우 있는지 tooput 따옴표로 묶인 여러 문자열을 수 있습니다. 또한 hello 연산자와 NOT 표시 된 대로 대문자로 표시를 위해 및 and가 있습니다.

에 지정 된 hello 필드 **fieldname:searchterm** 검색 가능한 필드 여야 합니다. 필드 정의에서 인덱스 특성이 사용되는 방법에 대한 자세한 내용은 [인덱스 만들기(Azure 검색 서비스 REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) 를 참조하세요.

**예제 2** -마우스 오른쪽 단추로 클릭 hello 다음 코드 조각 hello로 비즈니스 타이틀에 대 한 검색 용어를 수석 하지만 하지 신참이 쿼리를 쿼리 합니다.

* [&queryType=full&search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>유사 항목 검색 예제
유사 항목 검색은 용어에서 구조가 유사한 일치 항목을 찾습니다. [Lucene 문서](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html)에 따라 유사 항목 검색은 [다메라우-레펜슈타인(Damerau-Levenshtein) 거리](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance)에 기반합니다.

유사 항목 검색 toodo hello 물결표 추가 "~" 기호는 선택적 매개 변수, 0, 2 사이의 hello 편집 거리를 지정 하는 값이 포함 된 한 단어 hello 끝입니다. 예를 들어, "blue~" 또는 "blue~1"은 blue, blues 및 glue를 반환합니다.

**예제 3** -마우스 오른쪽 단추 클릭 hello 다음 코드 조각을 쿼리 합니다. 이 쿼리는 hello 용어 연결 (여기서 것 철자가)를 사용 하 여 작업에 대 한 검색:

* [&queryType=full&search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> 형태소 분석 또는 단어의 기본형 찾기를 기대하는 경우에는 놀랄 수 있겠지만 유사 항목 쿼리는 [분석](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis)되지 않습니다. 어휘 분석은 완전한 용어(용어 쿼리 또는 구 쿼리)에만 수행됩니다. 불완전 한 조건 (접두사 쿼리, 와일드 카드 쿼리, regex 쿼리, 유사 항목 쿼리) 쿼리 유형은 추가 됩니다 직접 toohello 쿼리 트리 hello 분석 단계를 무시 합니다. hello 불완전 한 쿼리 용어에 수행 하는 변환 에서만 소문자로 변환 합니다.
>

## <a name="proximity-search-example"></a>근접 검색 예제
근접 검색에는 문서에서 서로 가까이 있는 toofind 사용 되는 용어입니다. 물결표 삽입 "~" 구의 hello 끝 기호 뒤 hello 단어 hello 근접 단어 경계를 만들 수 있습니다. 예를 들어 "호텔 공항" ~ 5 문서에서 서로 5 개 단어 내의 공항 및 hello 용어 호텔을 찾을 수 있습니다.

**예 4** -hello 쿼리를 마우스 오른쪽 단추로 클릭 합니다. 둘 이상의 단어로 구분 hello 단어 "수석 분석가"와 함께 작업에 대 한 검색:

* [&queryType=full&search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**예 5** -hello 용어 "수석 분석가" 사이 hello 단어를 제거 하는 다시 시도 합니다.

* [&queryType=full&search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>용어 상승 예제
Tooranking hello를 포함 하는 경우 더 높은 문서에는 단어 hello 용어를 포함 하지 않는 상대 toodocuments 승격 된 참조 용어를 승격 합니다. 이것은 평가 프로필은 특정 용어가 아닌 특정 필드를 상승시킨다는 점에서 평가 프로필과는 다릅니다. hello 다음 예제에서는 사용 하면 hello 차이 보여 줍니다.

점수 매기기 프로필 증폭을 같은 특정 필드에 일치 하는 것이 좋습니다. **장르** hello musicstoreindex 예제에서입니다. 용어 승격 검색어 다른 항목 보다 더 높은 특정 사용된 toofurther 향상 될 수 있습니다. 예를 들어 "록 ^2 전자" hello에 hello 검색 용어를 포함 하는 문서를 상승 됩니다 **장르** hello 인덱스의 검색 가능한 다른 필드 보다 높은 필드입니다. 또한 hello 검색어 "록"를 포함 하는 문서 순위를 지정할 hello 보다 높은 "전자" hello 용어 부스트 값 (2)으로 인해 다른 검색어입니다.

용어를 사용 하 여 hello 캐럿 a tooboost "^"를 상승 계수 (숫자) 검색 하는 hello 용어의 hello 끝에 있는 기호입니다. hello 높은 hello 상승 계수 hello 관련성이 hello 용어 상대 tooother 검색어 됩니다. 기본적으로 hello 상승 계수는 1입니다. Hello 상승 계수는 양수 여야 합니다 (예: 0.2) 1 보다 작은 수 있습니다.

**예 6** -hello 쿼리를 마우스 오른쪽 단추로 클릭 합니다. Hello 단어 단어 컴퓨터와 분석가와 결과가 아직 hello 결과의 hello 위쪽 분석가 작업은 참조 म "컴퓨터 분석가"와 함께 작업을 검색 합니다.

* [&queryType=full&search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**예 7** -다시 시도, 두 단어 모두 존재 하지 않는 경우 hello 용어 분석가 통해 hello 용어 컴퓨터와 결과이 시간을 향상 시키는 합니다.

* [&queryType=full&search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>정규식 예제
정규식 검색 간에 슬래시 "/"에 문서화 된 hello로 hello 내용에 따라 일치 사항을 찾습니다. [RegExp 클래스](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html)합니다.

**예 8** -hello 쿼리를 마우스 오른쪽 단추로 클릭 합니다. Hello 용어 수석 또는 Junior과 함께 작업을 검색 합니다.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

이 예제에 대 한 hello URL hello 페이지에서 제대로 렌더링 되지 않습니다. 이 문제를 해결 아래 hello URL 복사한 hello 브라우저 URL 주소에 붙여 넣습니다.`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>와일드카드 검색 예제
일반적으로 다중(\*) 또는 단일(?) 문자 와일드카드 검색에 인식된 구문을 사용할 수 있습니다. Note hello Lucene 쿼리 파서 구를 하지 단일 용어와 이러한 기호의 hello 사용을 지원 합니다.

**예 9** -hello 쿼리를 마우스 오른쪽 단추로 클릭 합니다. Hello 접두사 'prog' hello 용어 프로그래밍 및 그 안에 프로그래머 비즈니스 제목을 포함을 포함 하는 작업을 검색 합니다.

* [&queryType=full&$select=business_title&search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

검색의 첫 문자로 * 또는 ? 검색의 첫 번째 문자로 hello 기호입니다.

## <a name="next-steps"></a>다음 단계
코드에서 hello Lucene 쿼리 파서를 지정 하십시오. hello 링크를 따라 검색 tooset.NET 및 REST API hello에 대 한 쿼리 하는 방법을 설명 합니다. hello 링크가 문서 toospecify hello에서 배운 tooapply에 해야 hello 기본 간단한 구문을 사용 하 여 **queryType**합니다.

* [Hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 쿼리 합니다.](search-query-dotnet.md)
* [Hello REST API를 사용 하 여 Azure 검색 인덱스를 쿼리 합니다.](search-query-rest-api.md)

## <a name="see-also"></a>참고 항목

 [Azure Search의 전체 텍스트 검색 작동 방식](search-lucene-query-architecture.md)