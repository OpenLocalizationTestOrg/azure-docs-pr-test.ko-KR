---
title: "OMS 로그 분석의 뷰 디자이너에 대 한 참조 aaaTile | Microsoft Docs"
description: "로그 분석의 뷰 디자이너 toocreate 사용자 지정을 사용 하면 hello OMS 리포지토리에 데이터의 각기 다른 시각화를 포함 하는 hello OMS 콘솔에서 뷰. 이 문서는 각각 hello 사용자 지정 보기에서 사용할 수 있는 toouse 타일에 대 한 hello 설정의 참조를 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Log Analytics 뷰 디자이너 타일 참조
로그 분석의 뷰 디자이너 hello toocreate 사용자 지정을 사용 하면 hello OMS 리포지토리에 데이터의 각기 다른 시각화를 포함 하는 hello OMS 콘솔에서 뷰. 이 문서는 각각 hello 사용자 지정 보기에서 사용할 수 있는 toouse 타일에 대 한 hello 설정의 참조를 제공 합니다.

뷰 디자이너에 적용할 수 있는 다른 문서는 다음과 같습니다.

* [뷰 디자이너](log-analytics-view-designer.md) -hello 디자이너 보기와 만들기 및 사용자 지정 보기를 편집 하기 위한 절차의 개요.
* [시각화 파트 참조](log-analytics-view-designer-parts.md) -참조 각 hello에 대 한 hello 설정의 사용자 지정 보기에서 사용할 수 있는 toouse 바둑판식으로 표시 합니다.

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), hello 모든 보기에서 쿼리를 작성 해야 하는 다음 [새로운 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856078)합니다.  작업 영역 hello를 업그레이드 하기 전에 생성 된 모든 뷰 automtically 변환 됩니다.

hello 다음 표에 hello 서로 다른 유형의 타일이 hello 뷰 디자이너에서에서 사용할 수 있습니다.  아래 hello 섹션에는 세부 정보 및 해당 속성에서 각 타일 유형에 대해 설명합니다.

| 타일 | 설명 |
|:--- |:--- |
| [Number](#number-tile) |한 쿼리의 레코드 수를 보여 주는 1개의 단일 숫자 |
| [2개 숫자](#two-numbers-tile) |서로 다른 두 쿼리의 레코드 수를 보여 주는 2개의 단일 숫자입니다. |
| [도넛](#donut-tile) |도넛형 차트 hello 센터의 요약 값이 있는 쿼리를 기반으로 합니다. |
| [꺾은선형 차트 및 설명선](#line-chart-amp-callout-tile) |쿼리 기반 꺾은선형 차트 및 요약 값이 있는 설명선입니다. |
| [꺾은선형 차트](#line-chart-tile) |쿼리 기반 꺾은선형 차트입니다. |
| [2개 타임 라인](#two-timelines-tile) |각각 별도의 쿼리에 기반하는 두 계열이 있는 세로 막대형 차트입니다. |

## <a name="number-tile"></a>1개 숫자 타일
hello **번호** hello 로그 쿼리 및 레이블을에서 레코드 수를 표시 하는 단일 숫자 타일에 표시 됩니다.

![1개 숫자 타일](media/log-analytics-view-designer/tile-number.png)

| 설정 | 설명 |
|:--- |:--- |
| 이름 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 설명 |텍스트 toodisplay hello 타일 이름입니다. |
| **타일** | |
| 범례 |Hello 값에서 텍스트 toodisplay 합니다. |
| 쿼리 |Toorun를 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| **고급** |**> 데이터 흐름 확인** |
| 사용 |데이터 흐름 확인 hello 타일에 대해 사용 하도록 설정 해야 하는 경우 선택 합니다.  이 데이터 hello 타일에 대해 사용할 수 없는 경우 대체 메시지를 제공 합니다.  일반적으로 사용 되는 tooprovide 메시지 hello 임시 기간 때 hello 보기를 설치 하 고 사용할 수 있는 데이터 원본입니다. |
| 쿼리 |Hello 보기에 대 한 데이터가 있으면 toorun toocheck를 쿼리 합니다.  Hello 쿼리 결과가 없으면 메시지가 hello 주 쿼리에서 hello 값 대신 표시 됩니다. |
| Message |메시지 toodisplay hello 데이터 흐름 확인 쿼리 없는 데이터를 반환 합니다.  메시지를 제공하지 않을 경우 *평가 수행 중*이라는 메시지가 표시됩니다. |


## <a name="two-numbers-tile"></a>2개 숫자 타일
hello **두 개의 번호** 각각에 대해 두 개의 다른 로그 쿼리 및 레이블을 레코드의 hello 개수를 보여 주는 두 개의 숫자 타일에 표시 됩니다.

![2개 숫자 타일](media/log-analytics-view-designer/tile-two-numbers.png)

| 설정 | 설명 |
|:--- |:--- |
| 이름 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 설명 |텍스트 toodisplay hello 타일 이름입니다. |
| **첫 번째 타일** | |
| 범례 |Hello 값에서 텍스트 toodisplay 합니다. |
| 쿼리 |Toorun를 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| **두 번째 타일** | |
| 범례 |Hello 값에서 텍스트 toodisplay 합니다. |
| 쿼리 |Toorun를 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| **고급** |**> 데이터 흐름 확인** |
| 사용 |데이터 흐름 확인 hello 타일에 대해 사용 하도록 설정 해야 하는 경우 선택 합니다.  이 데이터 hello 타일에 대해 사용할 수 없는 경우 대체 메시지를 제공 합니다.  일반적으로 사용 되는 tooprovide 메시지 hello 임시 기간 때 hello 보기를 설치 하 고 사용할 수 있는 데이터 원본입니다. |
| 쿼리 |Hello 보기에 대 한 데이터가 있으면 toorun toocheck를 쿼리 합니다.  Hello 쿼리 결과가 없으면 메시지가 hello 주 쿼리에서 hello 값 대신 표시 됩니다. |
| Message |메시지 toodisplay hello 데이터 흐름 확인 쿼리 없는 데이터를 반환 합니다.  메시지를 제공하지 않을 경우 *평가 수행 중*이라는 메시지가 표시됩니다. |


## <a name="donut-tile"></a>도넛형 타일
hello **도넛** 로그 쿼리의 값 열에서 요약 하 여 단일 숫자 타일에 표시 됩니다.  hello 도넛 hello 상위 3 개 레코드의 결과 그래픽으로 표시합니다.

![도넛형 타일](media/log-analytics-view-designer/tile-donut.png)

| 설정 | 설명 |
|:--- |:--- |
| 이름 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 설명 |텍스트 toodisplay hello 타일 이름입니다. |
| **도넛** | |
| 쿼리 |Toorun 도넛 hello에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  Hello를 사용 하는 쿼리는 일반적으로 **측정값** 키워드 toosummarize 결과입니다. |
| **도넛** |**> 중앙** |
| 텍스트 |Hello 도넛 내 hello 값에서 텍스트 toodisplay 합니다. |
| 작업 |hello 값 속성 toosummarize tooa 단일 값에 대 한 hello 작업 tooperform 합니다.<br><br>-합계: hello 속성 값을 사용 하 여 모든 레코드의 hello 값을 추가 합니다.<br>-비율: hello 속성 값 비교 toohello이 있는 레코드에서 hello 합계 값의 비율 합계 값의 모든 레코드. |
| 중앙에 사용되는 결과 값 연산 |필요에 따라 클릭 하 여 하나 이상의 값 tooadd 더하기 기호를 hello 합니다.  hello hello 쿼리 결과 제한 toorecords hello 속성 값이 지정 됩니다.  값이 없으면 추가 되 면 모든 레코드 보다는 hello 쿼리에 포함 합니다. |
| **도넛** |**> 추가 옵션** |
| 색 |hello 색 toodisplay 각 hello에 대 한 상위 3 개의 속성입니다.  특정 속성 값에 대 한 toospecify 대체 색을 원하는 경우 고급 색 매핑을 사용 합니다. |
| 고급 색 매핑 |특정 속성 값의 색을 표시합니다.  지정한 hello 값에는 상위 3 hello 경우 hello 대체 색 hello 표준 색 대신 표시 됩니다.  Hello 속성에 없는 경우 최상위 3 hello 다음 hello 색 표시 되지 않습니다. |
| **고급** |**> 데이터 흐름 확인** |
| 사용 |데이터 흐름 확인 hello 타일에 대해 사용 하도록 설정 해야 하는 경우 선택 합니다.  이 데이터 hello 타일에 대해 사용할 수 없는 경우 대체 메시지를 제공 합니다.  일반적으로 사용 되는 tooprovide 메시지 hello 임시 기간 때 hello 보기를 설치 하 고 사용할 수 있는 데이터 원본입니다. |
| 쿼리 |Hello 보기에 대 한 데이터가 있으면 toorun toocheck를 쿼리 합니다.  Hello 쿼리 결과가 없으면 메시지가 hello 주 쿼리에서 hello 값 대신 표시 됩니다. |
| Message |메시지 toodisplay hello 데이터 흐름 확인 쿼리 없는 데이터를 반환 합니다.  메시지를 제공하지 않을 경우 *평가 수행 중*이라는 메시지가 표시됩니다. |


## <a name="line-chart-tile"></a>꺾은선형 차트 타일
hello **꺾은선형 차트** 타일 시간에 따라 로그 쿼리에서 여러 계열와는 꺾은선형 차트를 표시 합니다.  

![꺾은선형 차트 및 설명선 타일](media/log-analytics-view-designer/tile-line-chart.png)

| 설정 | 설명 |
|:--- |:--- |
| 이름 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 설명 |텍스트 toodisplay hello 타일 이름입니다. |
| **꺾은선형 차트** | |
| 쿼리 |Toorun hello 꺾은선형 차트에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  Hello를 사용 하는 쿼리는 일반적으로 **측정값** 키워드 toosummarize 결과입니다.  Hello 쿼리 hello를 사용 하는 경우 **간격** 키워드 다음 hello hello 차트의 x 축이 시간 간격을 사용 합니다.  Hello 쿼리 hello 포함 되어 있지 않으면 **간격** hello x 축에 대 한 키워드 다음 시간별 간격이 사용 됩니다. |
| **꺾은선형 차트** |**> Y축** |
| 로그 눈금 간격 사용 |Toouse hello y 축에 대 한 로그 눈금 간격을 선택 합니다. |
| Units |Hello 쿼리에서 반환 된 hello 값에 대 한 hello 단위를 지정 합니다.  이 정보는 사용 되는 toodisplay 레이블을 hello 값 형식을 나타내는 hello 차트와 필요에 따라 hello 값 변환에 대 한 합니다.  hello **단위 형식** hello 단위의 hello 범주를 지정 하 고 hello 정의 **현재 단위 형식** 사용할 수 있는 값입니다.  값을 선택 하는 경우 **변환할** hello에서 hello 숫자 값은 변환 된 후 **현재 단위** toohello 입력 **변환할** 유형입니다. |
| 사용자 지정 레이블 |Hello 단위 형식에 대 한 hello Y 축 다음 toohello 레이블에 대 한 텍스트 toodisplay 합니다.  레이블이 없으면 지정 된 경우 hello 단위 형식에만 표시 됩니다. |
| **고급** |**> 데이터 흐름 확인** |
| 사용 |데이터 흐름 확인 hello 타일에 대해 사용 하도록 설정 해야 하는 경우 선택 합니다.  이 데이터 hello 타일에 대해 사용할 수 없는 경우 대체 메시지를 제공 합니다.  일반적으로 사용 되는 tooprovide 메시지 hello 임시 기간 때 hello 보기를 설치 하 고 사용할 수 있는 데이터 원본입니다. |
| 쿼리 |Hello 보기에 대 한 데이터가 있으면 toorun toocheck를 쿼리 합니다.  Hello 쿼리 결과가 없으면 메시지가 hello 주 쿼리에서 hello 값 대신 표시 됩니다. |
| Message |메시지 toodisplay hello 데이터 흐름 확인 쿼리 없는 데이터를 반환 합니다.  메시지를 제공하지 않을 경우 *평가 수행 중*이라는 메시지가 표시됩니다. |


## <a name="line-chart--callout-tile"></a>꺾은선형 차트 및 설명선 타일
hello **차트 & 설명선 선** 타일 설명선 요약된 된 값을 가지는 시간에 따른 로그 쿼리에서 여러 계열와는 꺾은선형 차트를 표시 합니다.  

![꺾은선형 차트 및 설명선 타일](media/log-analytics-view-designer/tile-line-chart-callout.png)

| 설정 | 설명 |
|:--- |:--- |
| 이름 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 설명 |텍스트 toodisplay hello 타일 이름입니다. |
| **꺾은선형 차트** | |
| 쿼리 |Toorun hello 꺾은선형 차트에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  Hello를 사용 하는 쿼리는 일반적으로 **측정값** 키워드 toosummarize 결과입니다.  Hello 쿼리 hello를 사용 하는 경우 **간격** 키워드 다음 hello hello 차트의 x 축이 시간 간격을 사용 합니다.  Hello 쿼리 hello 포함 되어 있지 않으면 **간격** hello x 축에 대 한 키워드 다음 시간별 간격이 사용 됩니다. |
| **꺾은선형 차트** |**> 설명선** |
| 설명선 제목 |제목 텍스트 toodisplay hello 설명선 값을 초과 합니다. |
| 계열 이름 |Hello 설명선 값에 대 한 계열 toouse hello에 대 한 속성 값입니다.  계열이 없습니다 제공 경우 hello 쿼리에서 모든 레코드가 사용 됩니다. |
| 작업 |hello hello 값 속성 toosummarize tooa 단일 값에 설명선 hello에 대 한 작업 tooperform 합니다.<br>모든 레코드의 hello 값의 평균: 평균입니다.<br><br>-C o u: hello 쿼리에서 반환 된 모든 레코드의 수입니다.<br>-Hello 차트에 포함 하는 hello 마지막 간격에서 마지막 샘플: 값입니다.<br>-Hello 차트에 포함 하는 hello 간격 최대: 최대 값입니다.<br>-최소: hello 간격 hello 차트에 포함 된 최소 값입니다.<br>모든 레코드의 hello 값의 합계: 합입니다. |
| **꺾은선형 차트** |**> Y축** |
| 로그 눈금 간격 사용 |Toouse hello y 축에 대 한 로그 눈금 간격을 선택 합니다. |
| Units |Hello 쿼리에서 반환 된 hello 값에 대 한 hello 단위를 지정 합니다.  이 정보는 사용 되는 toodisplay 레이블을 hello 값 형식을 나타내는 hello 차트와 필요에 따라 hello 값 변환에 대 한 합니다.  hello **단위 형식** hello 단위의 hello 범주를 지정 하 고 hello 정의 **현재 단위 형식** 사용할 수 있는 값입니다.  값을 선택 하는 경우 **변환할** hello에서 hello 숫자 값은 변환 된 후 **현재 단위** toohello 입력 **변환할** 유형입니다. |
| 사용자 지정 레이블 |Hello 단위 형식에 대 한 hello Y 축 다음 toohello 레이블에 대 한 텍스트 toodisplay 합니다.  레이블이 없으면 지정 된 경우 hello 단위 형식에만 표시 됩니다. |
| **고급** |**> 데이터 흐름 확인** |
| 사용 |데이터 흐름 확인 hello 타일에 대해 사용 하도록 설정 해야 하는 경우 선택 합니다.  이 데이터 hello 타일에 대해 사용할 수 없는 경우 대체 메시지를 제공 합니다.  일반적으로 사용 되는 tooprovide 메시지 hello 임시 기간 때 hello 보기를 설치 하 고 사용할 수 있는 데이터 원본입니다. |
| 쿼리 |Hello 보기에 대 한 데이터가 있으면 toorun toocheck를 쿼리 합니다.  Hello 쿼리 결과가 없으면 메시지가 hello 주 쿼리에서 hello 값 대신 표시 됩니다. |
| Message |메시지 toodisplay hello 데이터 흐름 확인 쿼리 없는 데이터를 반환 합니다.  메시지를 제공하지 않을 경우 *평가 수행 중*이라는 메시지가 표시됩니다. |


## <a name="two-timelines-tile"></a>2개 타임 라인 타일
hello **두 개의 일정이** 타일으로 세로 막대형 차트는 시간에 따라 두 로그 쿼리의 hello 결과 표시 됩니다.  계열 각각의 설명선이 표시됩니다.  

![2개 타임 라인 타일](media/log-analytics-view-designer/tile-two-timelines.png)

| 설정 | 설명 |
|:--- |:--- |
| 이름 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 설명 |텍스트 toodisplay hello 타일 이름입니다. |
| 첫 번째 차트 | |
| 범례 |Hello 첫 번째 계열에 대 한 hello 설명선 아래 텍스트 toodisplay 합니다. |
| 색 |Toouse hello 열 hello 첫 번째 계열에 대 한 색입니다. |
| 차트 쿼리 |Toorun hello 첫 번째 계열에 대 한 쿼리 합니다.  각 시간 간격에 대해 레코드의 hello 수의 hello 수 hello 차트 열에 의해 표현 됩니다. |
| 작업 |hello hello 값 속성 toosummarize tooa 단일 값에 설명선 hello에 대 한 작업 tooperform 합니다.<br><br>모든 레코드의 hello 값의 평균: 평균입니다.<br>-C o u: hello 쿼리에서 반환 된 모든 레코드의 수입니다.<br>-Hello 차트에 포함 하는 hello 마지막 간격에서 마지막 샘플: 값입니다.<br>-Hello 차트에 포함 하는 hello 간격 최대: 최대 값입니다. |
| **두 번째 차트** | |
| 범례 |Hello 두 번째 계열에 대 한 hello 설명선 아래 텍스트 toodisplay 합니다. |
| 색 |Toouse hello 열 hello 두 번째 계열에 대 한 색입니다. |
| 차트 쿼리 |Toorun hello 두 번째 계열에 대 한 쿼리 합니다.  각 시간 간격에 대해 레코드의 hello 수의 hello 수 hello 차트 열에 의해 표현 됩니다. |
| 작업 |hello hello 값 속성 toosummarize tooa 단일 값에 설명선 hello에 대 한 작업 tooperform 합니다.<br><br>모든 레코드의 hello 값의 평균: 평균입니다.<br>-C o u: hello 쿼리에서 반환 된 모든 레코드의 수입니다.<br>-Hello 차트에 포함 하는 hello 마지막 간격에서 마지막 샘플: 값입니다.<br>-Hello 차트에 포함 하는 hello 간격 최대: 최대 값입니다. |
| **고급** |**> 데이터 흐름 확인** |
| 사용 |데이터 흐름 확인 hello 타일에 대해 사용 하도록 설정 해야 하는 경우 선택 합니다.  이 데이터 hello 타일에 대해 사용할 수 없는 경우 대체 메시지를 제공 합니다.  일반적으로 사용 되는 tooprovide 메시지 hello 임시 기간 때 hello 보기를 설치 하 고 사용할 수 있는 데이터 원본입니다. |
| 쿼리 |Hello 보기에 대 한 데이터가 있으면 toorun toocheck를 쿼리 합니다.  Hello 쿼리 결과가 없으면 메시지가 hello 주 쿼리에서 hello 값 대신 표시 됩니다. |
| Message |메시지 toodisplay hello 데이터 흐름 확인 쿼리 없는 데이터를 반환 합니다.  메시지를 제공하지 않을 경우 *평가 수행 중*이라는 메시지가 표시됩니다. |


## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) 타일의 toosupport hello 쿼리 합니다.
* 추가 [시각화 부분](log-analytics-view-designer-parts.md) tooyour 사용자 지정 보기.
