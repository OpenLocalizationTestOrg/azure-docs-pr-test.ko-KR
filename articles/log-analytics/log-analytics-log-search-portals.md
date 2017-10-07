---
title: "만들고 Azure 로그 분석에서 로그 쿼리를 편집 하기 위한 aaaPortals | Microsoft Docs"
description: "이 문서에서는 hello 포털 toocreate Azure 로그 분석에서에서 사용 하 고 로그 검색을 편집할 수 있는지를 설명 합니다."
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
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Azure Log Analytics에서 로그 쿼리를 만들고 편집하기 위한 포털 | Microsoft Docs

> [!NOTE]
> 이 문서에서는 hello 새로운 쿼리 언어를 사용 하 여 Azure 로그 분석에서 포털을 설명 합니다.  Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.  
>
> 작업 영역에는 업그레이드 된 toohello 새로운 쿼리 언어 되지 않았는지를 하는 경우를 참조 해야 너무[로그 분석 로그 검색을 사용 하 여 데이터를 찾을](log-analytics-log-searches.md) hello hello 로그 검색 포털의 최신 버전에 대 한 내용은 합니다.

Hello 작업 영역에서 다양 한 로그 분석 tooretrieve 데이터 부분에서에서 로그 검색을 사용합니다.  실제로 만들고 쿼리를 편집 하기 위한 또한 tooworking와 대화형 데이터를 반환 하지만, 아래에 설명한 두 옵션을 사용할 수 있습니다.  

## <a name="log-search-portal"></a>로그 검색 포털
hello 로그 검색 포털은 Azure 포털 hello 또는 hello OMS 포털에서 액세스할 수 있습니다.  한 줄에 만들 수 있는 기본 쿼리를 만들기에 적합합니다.  hello 로그 검색 포털 외부 포털을 시작 하지 않고도 사용할 수 있으며 경고 규칙을 만들고 컴퓨터 그룹을 만들고, hello hello 쿼리 결과 내보내는 포함 하 여 로그 검색으로 다양 한 기능 tooperform 사용할 수 있습니다.  

hello 로그 검색 포털 hello 쿼리 언어의 완전 한 지식이 필요 없이 hello 쿼리를 편집 하기 위해 여러 기능을 제공 합니다.  이러한 기능에 대 한 요약을 가져올 수 있습니다 [hello 로그 검색 포털을 사용 하는 Azure 로그 분석에서 Create 로그 검색](log-analytics-log-search-log-search-portal.md)합니다.


![로그 검색 포털](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>고급 분석 포털
hello 고급 분석 포털은 hello 로그 검색 포털에서 사용할 수 없는 고급 기능을 제공 하는 전용된 포털입니다.  기능으로는 hello 기능 tooedit 여러 줄에 대 한 쿼리, 선택적으로 코드, 상황에 맞는 Intellisense 및 스마트 분석을 실행 합니다.  hello Advanced Analytics 포털은 복잡 한 쿼리는 다음 로그 검색으로 저장 하거나 복사 하 여 다른 로그 분석 요소에 붙여 넣은 디자인 하는 데 가장 적합 합니다.  하면 hello 로그 검색 포털의 링크에서 hello Advanced Analytics 포털을 시작합니다.

![고급 분석 포털](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


고급 기능으로 인해 일반적으로 사용 hello 고급 분석 포털 기본 도구를 만들고 쿼리를 편집 합니다.  확인 한 후 예상 대로 작동 하는 hello 쿼리 다음 복사 하 고 로그 검색 포털 hello 또는 뷰 디자이너와 같은 다른 곳에서 붙여 합니다.  Hello Advanced Analytics 포털 여러 줄이 포함 된 쿼리를 통해 지원 하므로이 포털에서 쿼리를 복사 하는 경우 tootake hello 다음 사항을 고려 필요 합니다.

- 에 복사 하 고 다른 위치에 붙여 hello 쿼리에서 주석은 제거 해야 합니다.  줄 앞에 슬래시(//) 두 개를 삽입하면 주석을 달 수 있습니다.  여러 줄 쿼리를 한 줄로 붙여넣는 경우 줄 바꿈이 제거됩니다.  코멘트가 포함 hello 첫 번째 주석 뒤의 모든 문자가 hello 주석 처리를 고려 합니다.


## <a name="next-steps"></a>다음 단계

- Hello를 사용 하는 자습서를 살펴보면서 [로그 검색 포털](log-analytics-log-search-log-search-portal.md) 또는 hello [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587) toocreate 쿼리 합니다.
- 체크 아웃 한 [쿼리 작성의 자습서](https://go.microsoft.com/fwlink/?linkid=856078) hello 새로운 쿼리 언어를 사용 하 여 합니다.
