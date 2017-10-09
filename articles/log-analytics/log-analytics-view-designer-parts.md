---
title: "OMS 로그 분석의 뷰 디자이너에 대 한 참조 aaaPart | Microsoft Docs"
description: "로그 분석의 뷰 디자이너 toocreate 사용자 지정을 사용 하면 hello OMS 리포지토리에 데이터의 각기 다른 시각화를 포함 하는 hello OMS 콘솔에서 뷰. 이 문서는 각각 hello 시각화 부분 사용자 지정 보기에서 사용할 수 있는 toouse hello 설정의 참조를 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Log Analytics 뷰 디자이너 시각화 요소 참조
로그 분석의 뷰 디자이너 hello toocreate 사용자 지정 보기를 hello OMS 콘솔에서 hello OMS 리포지토리에서 데이터의 각기 다른 시각화를 포함 하는 있습니다. 이 문서는 각각 hello 시각화 부분 사용자 지정 보기에서 사용할 수 있는 toouse hello 설정의 참조를 제공 합니다.

뷰 디자이너에 적용할 수 있는 다른 문서는 다음과 같습니다.

* [뷰 디자이너](log-analytics-view-designer.md) -hello 디자이너 보기와 만들기 및 사용자 지정 보기를 편집 하기 위한 절차의 개요.
* [참조 바둑판식으로 배열](log-analytics-view-designer-tiles.md) -참조 각 hello에 대 한 hello 설정의 사용자 지정 보기에서 사용할 수 있는 toouse 바둑판식으로 표시 합니다.

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), hello 모든 보기에서 쿼리를 작성 해야 하는 다음 [새로운 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856078)합니다.  작업 영역 hello를 업그레이드 하기 전에 생성 된 모든 뷰 automtically 변환 됩니다.

hello 다음 표에 hello 서로 다른 유형의 타일이 hello 뷰 디자이너에서에서 사용할 수 있습니다.  아래 hello 섹션에는 세부 정보 및 해당 속성에서 각 타일 유형에 대해 설명합니다.

| 보기 유형 | 설명 |
|:--- |:--- |
| [쿼리 목록](#list-of-queries-part) |로그 검색 쿼리 목록을 표시합니다.  hello 사용자 그 결과 각 쿼리 toodisplay에 클릭 수 있습니다. |
| [1개 숫자 및 목록](#number-amp-list-part) |머리글에서 로그 검색 쿼리에서 레코드 수를 보여 주는 숫자 하나를 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다. |
| [2개 숫자 및 목록](#two-numbers-amp-list-part) |머리글에서 로그 검색 쿼리에서 레코드 수를 보여 주는 숫자 둘을 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다. |
| [도넛형 차트 및 목록](#donut-amp-list-part) |머리글에서 로그 쿼리의 값 열로부터 요약된 숫자 하나를 표시합니다.  hello 도넛 hello 상위 3 개 레코드의 결과 그래픽으로 표시합니다. |
| [2개 타임 라인 및 목록](#two-timelines-amp-list-part) |로그 쿼리의 값 열에서 요약 된 헤더 세로 막대형 차트는 단일 숫자를 표시 하는 콜아웃이 시간이 경과 하는 두 개의 로그 쿼리의 hello 결과 표시 합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다. |
| [정보](#information-part) |머리글에서 정적 텍스트와 선택적 링크를 표시합니다.  목록에서 정적 텍스트 및 제목을 포함한 항목을 하나 이상 표시합니다. |
| [꺾은선형 차트, 설명선 및 목록](#line-chart-callout-amp-list-part) |머리글에서 로그 쿼리의 여러 시계열 및 요약된 값이 있는 설명선을 포함한 꺾은선형 차트를 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다. |
| [꺾은선형 차트 및 목록](#line-chart-amp-list-part) |머리글에서 로그 쿼리의 여러 시계열이 있는 꺾은선형 차트를 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다. |
| [꺾은선형 차트 요소 스택](#stack-of-line-charts-part) |로그 쿼리의 여러 시계열이 있는 별도의 꺾은선형 차트 3개를 표시합니다. |

## <a name="list-of-queries-part"></a>쿼리 목록 요소
로그 검색 쿼리 목록을 표시합니다.  hello 사용자 그 결과 각 쿼리 toodisplay에 클릭 수 있습니다.  hello 보기는 기본적으로 단일 쿼리를 포함 되며 클릭할 수 있는 **+ 쿼리** tooadd 추가 쿼리 합니다.

![쿼리 목록 보기](media/log-analytics-view-designer/view-list-queries.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 제목 |Hello 보기의 hello 위쪽 toodisplay 텍스트입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 미리 선택된 필터 |쉼표로 구분 된 hello 왼쪽된 필터 창에서 속성 tooinclude의 목록 hello 사용자가 쿼리를 선택 합니다. |
| 렌더링 모드 |초기 보기 hello 쿼리를 선택할 때 표시 됩니다.  hello 사용자 hello 쿼리를 연 후 사용 가능한 모든 뷰를 선택할 수 있습니다. |
| **쿼리** | |
| 검색 쿼리 |Toorun를 쿼리 합니다. |
| 친숙한 이름 |Hello 쿼리 toodisplay toohello 사용자의 설명이 포함 된 이름입니다. |

## <a name="number--list-part"></a>1개 숫자 및 목록 요소
머리글에서 로그 검색 쿼리에서 레코드 수를 보여 주는 숫자 하나를 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다.

![쿼리 목록 보기](media/log-analytics-view-designer/view-number-list.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |Hello 보기의 hello 위쪽 toodisplay 텍스트입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| 아이콘 사용 |Toohave hello 아이콘 표시를 선택 합니다. |
| **제목** | |
| 범례 |Hello 헤더의 hello 위쪽 toodisplay 텍스트입니다. |
| 쿼리 |Toorun hello 헤더에 대 한 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| **목록** | |
| 쿼리 |Toorun hello 목록에 대 한 쿼리 합니다.  hello에 대 한 처음 두 속성 hello 첫 번째 10 결과 표시 하는 hello에 기록 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  막대는 hello 상대 hello 숫자 열 값에 따라 자동으로 생성 됩니다.<br><br>Hello 목록의 hello 쿼리 toosort hello 레코드가 hello 정렬 명령을 사용 합니다.  hello 사용자가 클릭할 수 참조 모든 toorun hello 쿼리하고 모든 레코드를 반환 합니다. |
| 그래프 숨기기 |Toodisable hello 그래프 toohello 오른쪽의 hello 숫자 열을 선택 합니다. |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 색 |Hello 막대나 스파크 라인의 색입니다. |
| 이름 및 값 구분 기호 |여러 값으로 tooparse hello text 속성을 원하는 경우 단일 문자 구분 기호  자세한 내용은 [일반 설정](#name-value-separator)을 참조하세요. |
| 탐색 쿼리 |Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  자세한 내용은 [일반 설정](#navigation-query)을 참조하세요. |
| **목록** |**> 열 제목** |
| 이름 |Hello 위쪽 hello hello 목록의 첫 번째 열에 텍스트 toodisplay 합니다. |
| 값 |Hello 위쪽 hello hello 목록의 두 번째 열에 텍스트 toodisplay 합니다. |
| **목록** |**> 임계값** |
| 임계값 사용 |Tooenable 임계값을 선택 합니다.  자세한 내용은 [일반 설정](#thresholds)을 참조하세요. |

## <a name="two-numbers--list-part"></a>2개 숫자 및 목록 요소
머리글에서 로그 검색 쿼리에서 레코드 수를 보여 주는 숫자 둘을 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다.

![2개 숫자 및 목록 보기](media/log-analytics-view-designer/view-two-numbers-list.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |Hello 보기의 hello 위쪽 toodisplay 텍스트입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| 아이콘 사용 |Toohave hello 아이콘 표시를 선택 합니다. |
| **제목** | |
| 범례 |Hello 헤더의 hello 위쪽 toodisplay 텍스트입니다. |
| 쿼리 |Toorun hello 헤더에 대 한 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| **목록** | |
| 쿼리 |Toorun hello 목록에 대 한 쿼리 합니다.  hello에 대 한 처음 두 속성 hello 첫 번째 10 결과 표시 하는 hello에 기록 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  막대는 hello 상대 hello 숫자 열 값에 따라 자동으로 생성 됩니다.<br><br>Hello 목록의 hello 쿼리 toosort hello 레코드가 hello 정렬 명령을 사용 합니다.  hello 사용자가 클릭할 수 참조 모든 toorun hello 쿼리하고 모든 레코드를 반환 합니다. |
| 그래프 숨기기 |Toodisable hello 그래프 toohello 오른쪽의 hello 숫자 열을 선택 합니다. |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 색 |Hello 막대나 스파크 라인의 색입니다. |
| 작업 |Hello 스파크 라인에 대 한 작업 tooperform 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 이름 및 값 구분 기호 |여러 값으로 tooparse hello text 속성을 원하는 경우 단일 문자 구분 기호  자세한 내용은 [일반 설정](#name-value-separator)을 참조하세요. |
| 탐색 쿼리 |Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  자세한 내용은 [일반 설정](#navigation-query)을 참조하세요. |
| **목록** |**> 열 제목** |
| 이름 |Hello 위쪽 hello hello 목록의 첫 번째 열에 텍스트 toodisplay 합니다. |
| 값 |Hello 위쪽 hello hello 목록의 두 번째 열에 텍스트 toodisplay 합니다. |
| **목록** |**> 임계값** |
| 임계값 사용 |Tooenable 임계값을 선택 합니다.  자세한 내용은 [일반 설정](#thresholds)을 참조하세요. |

## <a name="donut--list-part"></a>도넛형 차트 및 목록 요소
머리글에서 로그 쿼리의 값 열로부터 요약된 숫자 하나를 표시합니다.  hello 도넛 hello 상위 3 개 레코드의 결과 그래픽으로 표시합니다.

![도넛형 차트 및 목록 보기](media/log-analytics-view-designer/view-donut-list.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| 아이콘 사용 |Toohave hello 아이콘 표시를 선택 합니다. |
| **머리글** | |
| 제목 |Hello 헤더의 hello 위쪽 toodisplay 텍스트입니다. |
| 부제 |Hello hello 헤더의 hello 위에 제목 아래 텍스트 toodisplay 합니다. |
| **도넛** | |
| 쿼리 |Toorun 도넛 hello에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다. |
| **도넛** |**> 중앙** |
| 텍스트 |Hello 도넛 내 hello 값에서 텍스트 toodisplay 합니다. |
| 작업 |hello 값 속성 toosummarize tooa 단일 값에 대 한 hello 작업 tooperform 합니다.<br><br>-합계: hello 값의 모든 레코드를 추가 합니다.<br>-비율: 백분율의 hello 값으로 반환 되는 hello 레코드 **센터 운영에 사용 되는 값을 결과** toohello hello 쿼리의 레코드 요약 합니다. |
| 중앙에 사용되는 결과 값 연산 |필요에 따라 클릭 하 여 하나 이상의 값 tooadd 더하기 기호를 hello 합니다.  hello hello 쿼리 결과 제한 toorecords hello 속성 값이 지정 됩니다.  값이 없으면 추가 되 면 hello 쿼리에서 모든 레코드가 포함 됩니다. |
| **추가 옵션** |**> 색** |
| 색 1<br>색 2<br>색 3 |각 hello hello 도넛에 표시 된 hello 값의 hello 색을 선택 합니다. |
| **추가 옵션** |**> 고급 색 매핑** |
| 필드 값 |필드 toodisplay의 형식 hello 이름을 hello 도넛에 포함 된 경우에 다른 색으로 합니다. |
| 색 |Hello 고유 필드에 대 한 hello 색을 선택 합니다. |
| **목록** | |
| 쿼리 |Toorun hello 목록에 대 한 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| 그래프 숨기기 |Toodisable hello 그래프 toohello 오른쪽의 hello 숫자 열을 선택 합니다. |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 색 |Hello 막대나 스파크 라인의 색입니다. |
| 작업 |Hello 스파크 라인에 대 한 작업 tooperform 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 이름 및 값 구분 기호 |여러 값으로 tooparse hello text 속성을 원하는 경우 단일 문자 구분 기호  자세한 내용은 [일반 설정](#name-value-separator)을 참조하세요. |
| 탐색 쿼리 |Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  자세한 내용은 [일반 설정](#navigation-query)을 참조하세요. |
| **목록** |**> 열 제목** |
| 이름 |Hello 위쪽 hello hello 목록의 첫 번째 열에 텍스트 toodisplay 합니다. |
| 값 |Hello 위쪽 hello hello 목록의 두 번째 열에 텍스트 toodisplay 합니다. |
| **목록** |**> 임계값** |
| 임계값 사용 |Tooenable 임계값을 선택 합니다.  자세한 내용은 [일반 설정](#thresholds)을 참조하세요. |

## <a name="two-timelines--list-part"></a>2개 타임 라인 및 목록 요소
로그 쿼리의 값 열에서 요약 된 헤더 세로 막대형 차트는 단일 숫자를 표시 하는 콜아웃이 시간이 경과 하는 두 개의 로그 쿼리의 hello 결과 표시 합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다.

![2개 타임 라인 및 목록 보기](media/log-analytics-view-designer/view-two-timelines-list.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| 아이콘 사용 |Toohave hello 아이콘 표시를 선택 합니다. |
| **첫 번째 차트<br>두 번째 차트** | |
| 범례 |Hello 첫 번째 계열에 대 한 hello 설명선 아래 텍스트 toodisplay 합니다. |
| 색 |Toouse hello 계열의 hello 열에 대 한 색입니다. |
| 쿼리 |Toorun hello 첫 번째 계열에 대 한 쿼리 합니다.  각 시간 간격에 대해 레코드의 hello 수의 hello 수 hello 차트 열에 의해 표현 됩니다. |
| 작업 |hello hello 값 속성 toosummarize tooa 단일 값에 설명선 hello에 대 한 작업 tooperform 합니다.<br><br>모든 레코드의 hello 값의 합계: 합입니다.<br>모든 레코드의 hello 값의 평균: 평균입니다.<br>-Hello 차트에 포함 하는 hello 마지막 간격에서 마지막 샘플: 값입니다.<br>-첫 번째 샘플: hello 첫 번째 간격 hello 차트에 포함 된 값입니다.<br>-C o u: hello 쿼리에서 반환 된 모든 레코드의 수입니다. |
| **목록** | |
| 쿼리 |Toorun hello 목록에 대 한 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| 그래프 숨기기 |Toodisable hello 그래프 toohello 오른쪽의 hello 숫자 열을 선택 합니다. |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 색 |Hello 막대나 스파크 라인의 색입니다. |
| 작업 |Hello 스파크 라인에 대 한 작업 tooperform 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 탐색 쿼리 |Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  자세한 내용은 [일반 설정](#navigation-query)을 참조하세요. |
| **목록** |**> 열 제목** |
| 이름 |Hello 위쪽 hello hello 목록의 첫 번째 열에 텍스트 toodisplay 합니다. |
| 값 |Hello 위쪽 hello hello 목록의 두 번째 열에 텍스트 toodisplay 합니다. |
| **목록** |**> 임계값** |
| 임계값 사용 |Tooenable 임계값을 선택 합니다.  자세한 내용은 [일반 설정](#thresholds)을 참조하세요. |

## <a name="information-part"></a>정보 요소
머리글에서 정적 텍스트와 선택적 링크를 표시합니다.  목록에서 정적 텍스트 및 제목을 포함한 항목을 하나 이상 표시합니다.

![정보 보기](media/log-analytics-view-designer/view-information.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 색 |Hello 헤더에 대 한 배경색입니다. |
| **머리글** | |
| 이미지 |Hello 머리글에 이미지 파일 toodisplay 합니다. |
| 레이블 |텍스트 toodisplay hello 헤더에 있습니다. |
| **머리글** |**> 링크** |
| 레이블 |링크 텍스트입니다. |
| Url |링크에 적용되는 Url입니다. |
| **정보 항목** | |
| 제목 |각 항목의 제목에 대 한 텍스트 toodisplay 합니다. |
| Content |각 항목에 대 한 텍스트 toodisplay 합니다. |

## <a name="line-chart-callout--list-part"></a>꺾은선형 차트, 설명선 및 목록 요소
머리글에서 로그 쿼리의 여러 시계열 및 요약된 값이 있는 설명선을 포함한 꺾은선형 차트를 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다.

![꺾은선형 차트, 설명선 및 목록 보기](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| 아이콘 사용 |Toohave hello 아이콘 표시를 선택 합니다. |
| **머리글** | |
| 제목 |Hello 헤더의 hello 위쪽 toodisplay 텍스트입니다. |
| 부제 |Hello hello 헤더의 hello 위에 제목 아래 텍스트 toodisplay 합니다. |
| **꺾은선형 차트** | |
| 쿼리 |Toorun hello 꺾은선형 차트에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  Hello를 사용 하는 쿼리는 일반적으로 **측정값** 키워드 toosummarize 결과입니다.  Hello 쿼리 hello를 사용 하는 경우 **간격** 키워드 다음 hello hello 차트의 x 축이 시간 간격을 사용 합니다.  Hello 쿼리 hello 포함 되어 있지 않으면 **간격** hello x 축에 대 한 키워드 다음 시간별 간격이 사용 됩니다. |
| **꺾은선형 차트** |**> 설명선** |
| 설명선 제목 |텍스트 toodisplay hello 설명선 값을 초과 합니다. |
| 계열 이름 |Hello 설명선 값에 대 한 계열 toouse hello에 대 한 속성 값입니다.  계열이 없습니다 제공 경우 hello 쿼리에서 모든 레코드가 사용 됩니다. |
| 작업 |hello hello 값 속성 toosummarize tooa 단일 값에 설명선 hello에 대 한 작업 tooperform 합니다.<br><br>모든 레코드의 hello 값의 평균: 평균입니다.<br>-C o u hello 쿼리에서 반환 된 모든 레코드 수입니다.<br>-Hello 차트에 포함 하는 hello 마지막 간격에서 마지막 샘플: 값입니다.<br>-Hello 차트에 포함 하는 hello 간격 최대: 최대 값입니다.<br>-최소: hello 간격 hello 차트에 포함 된 최소 값입니다.<br>모든 레코드의 hello 값의 합계: 합입니다. |
| **꺾은선형 차트** |**> Y축** |
| 로그 눈금 간격 사용 |Toouse hello y 축에 대 한 로그 눈금 간격을 선택 합니다. |
| Units |Hello 쿼리에서 반환 된 hello 값에 대 한 hello 단위를 지정 합니다.  이 정보는 사용 되는 toodisplay 레이블을 hello 값 형식을 나타내는 hello 차트와 필요에 따라 hello 값 변환에 대 한 합니다.  hello 단위 형식 hello 단위의 hello 범주를 지정 하 고 사용할 수 있는 hello 현재 단위 형식 값을 정의 합니다.  Convert toothen hello 숫자의 값을 선택 하는 경우 값은 hello 현재 단위 형식 toohello Convert tootype에서 변환 됩니다. |
| 사용자 지정 레이블 |Hello 단위 형식에 대 한 hello Y 축 다음 toohello 레이블에 대 한 텍스트 toodisplay 합니다.  레이블이 없으면 지정 된 경우 hello 단위 형식에만 표시 됩니다. |
| **목록** | |
| 쿼리 |Toorun hello 목록에 대 한 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| 그래프 숨기기 |Toodisable hello 그래프 toohello 오른쪽의 hello 숫자 열을 선택 합니다. |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 색 |Hello 막대나 스파크 라인의 색입니다. |
| 작업 |Hello 스파크 라인에 대 한 작업 tooperform 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 이름 및 값 구분 기호 |여러 값으로 tooparse hello text 속성을 원하는 경우 단일 문자 구분 기호  자세한 내용은 [일반 설정](#name-value-separator)을 참조하세요. |
| 탐색 쿼리 |Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  자세한 내용은 [일반 설정](#navigation-query)을 참조하세요. |
| **목록** |**> 열 제목** |
| 이름 |Hello 위쪽 hello hello 목록의 첫 번째 열에 텍스트 toodisplay 합니다. |
| 값 |Hello 위쪽 hello hello 목록의 두 번째 열에 텍스트 toodisplay 합니다. |
| **목록** |**> 임계값** |
| 임계값 사용 |Tooenable 임계값을 선택 합니다.  자세한 내용은 [일반 설정](#thresholds)을 참조하세요. |

## <a name="line-chart--list-part"></a>꺾은선형 차트 및 목록 요소
머리글에서 로그 쿼리의 여러 시계열이 있는 꺾은선형 차트를 표시합니다.  시간이 지남에 따라 변경 내용 또는 숫자 열 hello 상대 값을 나타내는 그래프를 hello 상위 10 개의 쿼리 결과 목록에 표시 됩니다.

![꺾은선형 차트 및 목록 보기](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| 아이콘 사용 |Toohave hello 아이콘 표시를 선택 합니다. |
| **머리글** | |
| 제목 |Hello 헤더의 hello 위쪽 toodisplay 텍스트입니다. |
| 부제 |Hello hello 헤더의 hello 위에 제목 아래 텍스트 toodisplay 합니다. |
| **꺾은선형 차트** | |
| 쿼리 |Toorun hello 꺾은선형 차트에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  Hello를 사용 하는 쿼리는 일반적으로 **측정값** 키워드 toosummarize 결과입니다.  Hello 쿼리 hello를 사용 하는 경우 **간격** 키워드 다음 hello hello 차트의 x 축이 시간 간격을 사용 합니다.  Hello 쿼리 hello 포함 되어 있지 않으면 **간격** hello x 축에 대 한 키워드 다음 시간별 간격이 사용 됩니다. |
| **꺾은선형 차트** |**> Y축** |
| 로그 눈금 간격 사용 |Toouse hello y 축에 대 한 로그 눈금 간격을 선택 합니다. |
| Units |Hello 쿼리에서 반환 된 hello 값에 대 한 hello 단위를 지정 합니다.  이 정보는 사용 되는 toodisplay 레이블을 hello 값 형식을 나타내는 hello 차트와 필요에 따라 hello 값 변환에 대 한 합니다.  hello 단위 형식 hello 단위의 hello 범주를 지정 하 고 사용할 수 있는 hello 현재 단위 형식 값을 정의 합니다.  Convert toothen hello 숫자의 값을 선택 하는 경우 값은 hello 현재 단위 형식 toohello Convert tootype에서 변환 됩니다. |
| 사용자 지정 레이블 |Hello 단위 형식에 대 한 hello Y 축 다음 toohello 레이블에 대 한 텍스트 toodisplay 합니다.  레이블이 없으면 지정 된 경우 hello 단위 형식에만 표시 됩니다. |
| **목록** | |
| 쿼리 |Toorun hello 목록에 대 한 쿼리 합니다.  hello 개수 hello hello 쿼리에서 반환 된 레코드 수가 표시 됩니다. |
| 그래프 숨기기 |Toodisable hello 그래프 toohello 오른쪽의 hello 숫자 열을 선택 합니다. |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 색 |Hello 막대나 스파크 라인의 색입니다. |
| 작업 |Hello 스파크 라인에 대 한 작업 tooperform 합니다.  자세한 내용은 [일반 설정](#sparklines)을 참조하세요. |
| 이름 및 값 구분 기호 |여러 값으로 tooparse hello text 속성을 원하는 경우 단일 문자 구분 기호  자세한 내용은 [일반 설정](#name-value-separator)을 참조하세요. |
| 탐색 쿼리 |Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  자세한 내용은 [일반 설정](#navigation-query)을 참조하세요. |
| **목록** |**> 열 제목** |
| 이름 |Hello 위쪽 hello hello 목록의 첫 번째 열에 텍스트 toodisplay 합니다. |
| 값 |Hello 위쪽 hello hello 목록의 두 번째 열에 텍스트 toodisplay 합니다. |
| **목록** |**> 임계값** |
| 임계값 사용 |Tooenable 임계값을 선택 합니다.  자세한 내용은 [일반 설정](#thresholds)을 참조하세요. |

## <a name="stack-of-line-charts-part"></a>꺾은선형 차트 요소 스택
로그 쿼리의 여러 시계열이 있는 별도의 꺾은선형 차트 3개를 표시합니다.

![꺾은선형 차트 스택](media/log-analytics-view-designer/view-stack-line-charts.png)

| 설정 | 설명 |
|:--- |:--- |
| **일반** | |
| 그룹 제목 |텍스트 toodisplay hello 위쪽 hello에 바둑판식으로 배열입니다. |
| 새 그룹 |Hello 현재 보기에서 시작 하는 hello 뷰에서 toocreate 새 그룹을 선택 합니다. |
| 아이콘 |이미지 파일 toodisplay 다음 toohello 결과 hello 헤더에서입니다. |
| **차트 1<br>차트 2<br>차트 3** |**> 머리글** |
| 제목 |Hello 차트의 hello 위쪽 toodisplay 텍스트입니다. |
| 부제 |Hello hello 위쪽 hello 차트의 제목 아래에서 텍스트 toodisplay 합니다. |
| **차트 1<br>차트 2<br>차트 3** |**꺾은선형 차트** |
| 쿼리 |Toorun hello 꺾은선형 차트에 대 한 쿼리 합니다.  첫 번째 속성 hello 속성 이어야 합니다. 텍스트 값과 hello 두 번째 숫자 값입니다.  Hello를 사용 하는 쿼리는 일반적으로 **측정값** 키워드 toosummarize 결과입니다.  Hello 쿼리 hello를 사용 하는 경우 **간격** 키워드 다음 hello hello 차트의 x 축이 시간 간격을 사용 합니다.  Hello 쿼리 hello 포함 되어 있지 않으면 **간격** hello x 축에 대 한 키워드 다음 시간별 간격이 사용 됩니다. |
| **차트** |**> Y축** |
| 로그 눈금 간격 사용 |Toouse hello y 축에 대 한 로그 눈금 간격을 선택 합니다. |
| Units |Hello 쿼리에서 반환 된 hello 값에 대 한 hello 단위를 지정 합니다.  이 정보는 사용 되는 toodisplay 레이블을 hello 값 형식을 나타내는 hello 차트와 필요에 따라 hello 값 변환에 대 한 합니다.  hello 단위 형식 hello 단위의 hello 범주를 지정 하 고 사용할 수 있는 hello 현재 단위 형식 값을 정의 합니다.  Convert toothen hello 숫자의 값을 선택 하는 경우 값은 hello 현재 단위 형식 toohello Convert tootype에서 변환 됩니다. |
| 사용자 지정 레이블 |Hello 단위 형식에 대 한 hello Y 축 다음 toohello 레이블에 대 한 텍스트 toodisplay 합니다.  레이블이 없으면 지정 된 경우 hello 단위 형식에만 표시 됩니다. |

## <a name="common-settings"></a>일반 설정
다음 섹션 hello 설정을 공통 tooseveral 시각화 부분을 설명 합니다.

### <a name="name-value-separator">이름 및 값 구분 기호</a>
단일 문자 구분 기호 tooparse hello text 속성 목록 쿼리에서 여러 값으로 하려는 경우입니다.  구분 기호를 지정 하는 경우 각 필드 구분 하 여 hello 동일에 대 한 이름을 제공할 수 있습니다 hello 이름 상자에 구분 기호입니다.

예를 들어 *Redmond-Building 41* 및 *Redmond-Building12*와 같은 값을 포함한 *위치*라는 속성이 있습니다.  지정할 수 있습니다-hello 이름 및 값 구분 기호에 대 한 및 *시 건물이* hello 이름에 대 한 합니다.  이렇게 하면 각 값을 *City*와 *Building*이라는 두 속성으로 구문 분석합니다.

### <a name="navigation-query">탐색 쿼리</a>
Hello hello 목록에서 항목을 선택 하는 경우 toorun를 쿼리 합니다.  사용 하 여 *{선택한 항목}* hello 사용자가 선택한 항목에 대 한 tooinclude hello 구문입니다.

예를 들어 경우 hello 쿼리 이라는 열이 포함 *컴퓨터* hello 탐색 쿼리가 *{선택한 항목을 (를)*와 같은 쿼리 *컴퓨터 = "MyComputer"* 때 실행 hello 사용자 컴퓨터를 선택 합니다.  Hello 탐색 쿼리가 *유형 = {선택한 항목을 (를) 이벤트* hello 쿼리 한 다음 *유형 = 이벤트 컴퓨터 = "MyComputer"* 실행 합니다.

### <a name="sparklines">스파크라인</a>
스파크 라인은 시간이 지남에 따라 목록 항목의 hello 값을 보여 주는 작은 꺾은선형 차트입니다.  목록이 있는 시각화 파트를 toodisplay 가로줄로 나눠진 나타내는 hello 숫자 열의 상대 값 또는 시간에 따른 해당 값을 나타내는 스파크 라인을 선택할 수 있습니다.

다음 표에서 hello 스파크 라인에 대 한 hello 설정을 설명 합니다.

| 설정 | 설명 |
|:--- |:--- |
| 스파크라인 사용 |대신 가로 막대 toodisplay 스파크 라인을 선택 합니다. |
| 작업 |스파크 라인을 사용할 경우 이것이 hello 스파크 라인에 대 한 hello 목록 toocalculate hello 값의 각 속성에 hello 작업 tooperform입니다.<br><br>-마지막 샘플: hello 시간 간격 동안 hello 계열에 대 한 마지막 값입니다.<br>-최대: hello 시간 간격 동안 hello 계열에 대 한 최대 값입니다.<br>-최소: hello 시간 간격 동안 hello 계열에 대 한 최소 값입니다.<br>Hello 시간 간격 동안 hello 계열에 대 한 값의 합계: 합입니다.<br>-요약: 사용 하 여 hello hello 헤더에 hello 쿼리 측정값 명령과 동일 합니다. |

### <a name="thresholds">임계값</a>
임계값을 특정 값을 초과 하거나 특정 범위 내에 있는 항목의 빠른 시각적 표시기를 제공 하는 목록에서 색이 지정 된 아이콘 다음 tooeach 항목 toodisplay를 허용 합니다.  예를 들어 오류 값을 초과 하는 경우에 사용 가능한 값, hello 값이 경고를 나타내는 범위 내에서 노랑 및 빨강 항목에 대 한 녹색 아이콘을 표시할 수 있습니다.

부분적으로 임계값을 사용하려면 하나 이상의 임계값을 지정해야 합니다.  항목의 hello 값이 임계값 보다 크고 hello 다음 임계값 보다 낮은 경우 해당 색이 사용 됩니다.  Hello 항목 다음 가장 높은 임계값 보다 큰 경우 해당 색이 설정 됩니다.   

각 임계값 집합에 값이 **기본값**인 임계값 하나가 있습니다.  다른 값이 없는 초과 된 경우 설정 된 hello 색입니다.  추가 하거나 hello를 클릭 하 여 임계값을 제거할 수 있습니다  **+**  또는 **x** 단추입니다.

다음 표에서 hello tresholds에 대 한 hello 설정을 설명 합니다.

| 설정 | 설명 |
|:--- |:--- |
| 임계값 사용 |해당 상태 상대 toospecified 임계값을 나타내는 각 값의 색 아이콘 toohello 왼쪽 toodisplay를 선택 합니다. |
| 이름 |Tooidentify hello 임계값 값을 이름을 지정 합니다. |
| 임계값 |Hello 임계값에 대 한 값입니다.  각 목록 항목에 대 한 상태 색 hello hello 가장 높은 임계값의 hello 항목의 값을 초과 toohello 색이 설정 됩니다.  hello 색 임계값 값이 없는 초과 된 경우 기본 임계값이 하나 있습니다. |
| 색 |Hello 임계값에 대 한 색입니다. |

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) 시각화 부분에서 toosupport hello 쿼리 합니다.
