---
title: "OMS 로그 분석의 aaaRegular 식 로그 검색 | Microsoft Docs"
description: "로그 분석 로그 검색 toohello 필터 hello 결과 tooa 정규식에 따라 hello RegEx 키워드를 사용할 수 있습니다.  이 문서에서는 몇 가지 예제와 함께 이러한 식에 대 한 hello 구문을 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>로그 분석에 정규식 toofilter를 사용 하 여 로그 검색

[로그 검색](log-analytics-log-searches.md) hello 로그 분석 저장소에서 tooextract 정보를 허용 합니다.  [필터 식](log-analytics-search-reference.md#filter-expressions) toospecific 조건에 따라 hello 검색 toofilter hello 결과 허용 합니다.  hello **RegEx** toospecify이이 필터에 대 한 정규식 키워드를 사용 합니다.  

이 문서에서는 로그 분석에서 사용 하는 hello 정규식 구문에 자세히 설명 합니다.

> [!NOTE]
> 검색 가능한 필드가 있는 RegEx만 사용할 수 있습니다.  검색 가능한 필드에 대한 자세한 내용은 [Log Analytics에서 로그 검색을 사용하여 데이터 찾기](log-analytics-log-searches.md#use-additional-filters)에서 **필드 형식**을 참조하세요.


## <a name="regex-keyword"></a>RegEx 키워드

다음 구문 toouse hello 사용 하 여 hello **RegEx** 로그 검색에는 키워드입니다.  사용할 수 있습니다이 문서 toodetermine hello 구문에서 자체 정규식 hello의 다른 섹션 hello 합니다.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

형식의 toouse 정규식 tooreturn 경고를 기록 하는 예를 들어 *경고* 또는 *오류*, 로그 검색을 수행 하는 hello를 사용 합니다.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>부분 일치
참고 hello 정규식 hello hello 속성의 전체 텍스트를 일치 해야 합니다.  부분 일치는 레코드를 반환하지 않습니다.  예를 들어 srv01.contoso.com 라는 컴퓨터에서 tooreturn 레코드를 시도 하는 경우 로그 검색을 수행 하는 hello는 **하지** 레코드를 반환 합니다.

    Computer=RegEx("srv..")

즉, hello 이름의 첫 번째 부분 hello만 hello 정규식과 일치 합니다.  hello 다음 두 개의 로그 검색 레코드가이 컴퓨터에서 때문에 반환 됩니다 hello 전체 이름 일치 합니다.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>문자
다른 문자를 지정합니다.

| 문자 | 설명 | 예 | 샘플 일치 |
|:--|:--|:--|:--|
| a | Hello 문자의 하나 발생 합니다. | Computer=RegEx("srv01.contoso.com") | srv01.contoso.com |
| 을 참조하세요. | 단일 문자입니다. | Computer=RegEx("srv...contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| a? | Hello 문자의 0 개 또는 1 발생 합니다. | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>srv01.contoso.com |
| a* | Hello 문자의 0 개 이상의 발생 합니다. | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Hello 문자의 하나 이상 찾습니다. | Computer=RegEx("srv01+.contoso.com") | srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Hello 대괄호로 한 문자 일치 | Computer=RegEx("srv0[123].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [*a*-*z*] | Hello 범위에 단일 문자를 찾습니다.  여러 범위를 포함할 수 있습니다. | Computer=RegEx("srv0[1-3].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Hello hello 대괄호로 둘러싸인 문자 중 | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^*a*-*z*] | Hello 범위에 있는 hello 문자의 없음입니다. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | 숫자의 범위와 일치합니다. | Computer=RegEx("srv[01-03].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| @ | 문자의 문자열입니다. | Computer=RegEx("srv@.contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>여러 문자를 발견합니다.
특정 문자를 여러 번 발견했음을 나타냅니다.

| 문자 | 설명 | 예 | 샘플 일치 |
|:--|:--|:--|:--|
| a{n} |  *n*hello 문자가 한 번 발생 합니다. | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*또는 hello 문자 이상 찾습니다. | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*너무*m* hello 문자가 한 번 발생 합니다. | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>논리 식
여러 값에서 선택합니다.

| 문자 | 설명 | 예 | 샘플 일치 |
|:--|:--|:--|:--|
| &#124; | 논리 OR.  두 식 중 하나가 일치하는 경우 결과를 반환합니다. | Type=Alert AlertSeverity=RegEx("Warning&#124;Error") | Warning<br>오류 |
| & | 논리 AND.  두 식이 모두 일치하는 경우 결과를 반환합니다. | EventData=regex("(Security.\*&.\*success.\*)") | 보안 감사 성공 |


## <a name="literals"></a>리터럴
특수 문자 tooliteral 문자 변환 합니다.  와 같은 기능 tooregular 식을 제공 하는 문자를 포함 하는이?-\*^\[\]{}\(\)+\|. & 합니다.

| 문자 | 설명 | 예 | 샘플 일치 |
|:--|:--|:--|:--|
| \\ | 리터럴는 특수 문자 tooa를 변환합니다. | Status_CF=\\[Error\\]@<br>Status_CF=Error\\-@ | [오류]파일을 찾을 수 없습니다.<br>오류-파일을 찾을 수 없습니다. |


## <a name="next-steps"></a>다음 단계

* 익숙해질 목적으로 [검색 로그](log-analytics-log-searches.md) tooview hello 로그 분석 저장소에서 데이터를 분석 하 고 있습니다.
