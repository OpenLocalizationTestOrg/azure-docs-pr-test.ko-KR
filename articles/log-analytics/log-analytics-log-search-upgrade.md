---
title: "aaaUpgrading Azure 로그 분석 toonew 로그 검색 | Microsoft Docs"
description: "거의 여기에 새로운 로그 분석 쿼리 언어 hello 및 hello 공개 미리 보기에 참여할 수 있습니다.  이 문서에서는 hello 새로운 언어의 hello 장점을 설명 및 방법을 tooconvert 작업 영역입니다."
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
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Azure 로그 분석 작업 영역 toonew 로그 검색 업그레이드

> [!NOTE]
> 업그레이드 toohello 새로운 로그 분석 쿼리 언어는 현재 선택적 제공 하면 시간을 너무[hello 새 언어에 성능을 향상 시키는](https://go.microsoft.com/fwlink/?linkid=856078)합니다.  

여기에 새로운 로그 분석 쿼리 언어 hello 고 tooupgrade의 작업 영역 tootake 있다는 이점이 해야 합니다.  이 문서에서는 hello 새로운 언어의 hello 장점을 설명 및 방법을 tooconvert 작업 영역입니다.  을 선택 하지 않으면 tooupgrade 이제 toooperate 것 처럼 항상 하지만 나중에 자동으로 변환 됩니다 작업 영역 계속 됩니다.  해당 날짜가 정해지면 뜻 깊은 시간과 알림을 받게 될 것입니다.

이 문서는 hello 새로운 언어와 hello 업그레이드 프로세스에 세부 정보를 제공합니다.

## <a name="why-hello-new-language"></a>새로운 언어 hello 이유?
점을 이해 하는 창에 있는 모든 전환 있고 म만 즐거움을 hello에 대 한 hello 쿼리 언어를 변경 되지 않습니다.  이 변경은 중요 한 가치 tooour 로그 분석 고객 제공할 예정 몇 가지 이유가 있습니다.

- **단순하면서도 강력합니다.** hello 새 언어는 보다 쉽게 toounderstand 및 자세한 구문으로 유사한 tooSQL 같은 hello 레거시 언어 보다 자연어입니다.
- **전체 파이핑 언어입니다.**  hello 새 언어는 hello 레거시 언어 보다 더욱 광범위 한 파이핑 기능이 있습니다.  거의 모든 출력 파이프 된 tooanother 명령 toocreate 된 하 던 것 보다 더 복잡 한 쿼리 될 수 있습니다.
- **검색-시간 필드 추출.**  hello 새로운 언어 hello 레거시 언어 보다 더 많은 고급 런타임 계산 필드를 지원합니다.  확장된 필드에 대 한 복잡 한 계산을 사용할 수 있으며 다음 hello 계산 필드를 사용 하 여 조인 및 집계를 포함 하 여 추가 명령은 있습니다.
- **고급 조인.**  hello 새 언어는 여러 필드에 대해 hello 기능 toojoin 테이블을 포함 하 여 hello 레거시 언어 보다 더 많은 고급 조인을 제공 하 고 내부 및 외부 조인을 사용 하 여 확장된 필드에 조인 합니다.
- **날짜/시간 함수.**  hello 새로운 언어 날짜/시간 함수 hello 레거시 언어 보다 고급 있습니다.
- **스마트 분석.**  hello 새 언어는 데이터 집합과 비교 여러 데이터 집합의 알고리즘 tooevaluate 패턴 고급 합니다.
- **고급 분석 포털.**  hello 고급 분석 포털 기능을 제공 분석 여러 줄을 포함 하 여 hello 로그 분석 포털에서 사용할 수 없는 쿼리, 추가 시각화 및 고급 진단 편집 합니다.
- **다른 응용 프로그램과의 일관성.**  안녕 새로운 언어와 hello 고급 분석 포털 이미 Application Insights에서 분석을 위해 사용 됩니다.  Log Analytics에 대한 구현은 Azure 서비스 전반에 걸쳐 일관성을 제공합니다.
- **Power BI와의 더 나은 통합.** Hello 새 언어에서는 쿼리는 내보낸된 tooPower BI Desktop 될 수 있으므로 다양 한 데이터 변환 기능을 활용할 수 있습니다.
- **그 외 더 많은 요소들이 있습니다.** Toohello 참조 [Azure 로그 분석 쿼리 언어](https://docs.loganalytics.io) 전체 세부 정보 및 hello 새 언어에 대 한 자습서에 대 한 사이트입니다.


## <a name="when-can-i-upgrade"></a>언제 업그레이드할 수 있습니까?
hello 업그레이드가 출시 될 예정 모든 Azure 지역에 걸쳐 하므로 다른 대체 이전 일부 지역에서는 사용할 수 있습니다.  작업 영역 tooupgrade 초대 작업 공간의 hello 위쪽 hello 자주색 배너가 표시 하는 경우 업그레이드 하는 사용 가능한 toobe 때 알 수 있습니다.

![업그레이드 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>업그레이드하면 어떻게 되나요?
작업 영역을 변환 하는 경우 모든 저장 된 검색, 경고 규칙 및 hello 뷰 디자이너를 사용 하 여 만든 뷰는 자동으로 변환 된 toohello 새 언어입니다.  솔루션에 포함 된 검색은 자동으로 변환 되지 않습니다 하지만 열 때 대신 hello 신속 하 게 변환 하는 합니다.  이것이 완전히 투명 하 게 tooyou입니다.

## <a name="can-i-go-back-after-i-upgrade"></a>업그레이드 후에 다시 돌아갈 수 있습니까?
업그레이드하면 작업 영역의 전체 백업이 수행되며, 모든 저장된 검색, 경고 규칙 및 뷰에 대한 스냅숏을 포함합니다.  이렇게 하면 toorestore 나중에 원하는 해야 하는 경우 이전 작업 영역입니다.

toorestore 레거시 작업 영역을 이동 너무**설정** 작업 영역에서 다음 **업그레이드 요약**합니다.  다음 옵션을 선택할 있습니다 hello 너무**레거시 작업 영역 복원**합니다.  

![레거시 복원](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Hello 업그레이드를 수행 하려면 어떻게 해야 합니까?
Hello 포털의 hello 위쪽 hello 자주색 배너를 표시 하는 경우 작업 영역을 업그레이드할 수 있습니다.  

1.  알리는 hello 자주색 배너를 클릭 하 여 hello 업그레이드 프로세스를 시작 **자세히 알아보고 업그레이드**합니다.<br>![업그레이드 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Hello 업그레이드 정보 페이지에 hello 업그레이드에 대 한 hello 추가 정보를 자세히 읽습니다.<br>![업그레이드 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  클릭 **지금 업그레이드** toostart hello 업그레이드 합니다.<br>![업그레이드 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Hello 오른쪽 위 모서리에 있는 알림 상자 hello 상태가 표시 됩니다.<br>![업그레이드 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  끝났습니다.  업그레이드 된 작업 영역을 살펴보고 toohello 로그 검색 페이지 toohave 검토 합니다.<br>![업그레이드 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Toohello 넘어가면 hello 업그레이드 toofail 되는 문제를 발생 하면 [토론 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) 질문을 게시 하 고 또는 [지원 요청](../azure-supportability/how-to-create-azure-support-request.md) hello Azure 포털에서에서 합니다.

## <a name="how-do-i-learn-hello-new-language"></a>Hello 새 언어를 어떻게 알 수 있나요?
만들고 이후 여러 서비스에서 사용 되는 [외부 사이트 toohost hello 설명서](https://docs.loganalytics.io/) hello 새 언어에 대 한 합니다.  자습서, 샘플 및 toospeed 수립 전체 참조 toohelp이 포함 됩니다. hello 새 언어에 대 한 자습서를 진행할 수 [쿼리 시작](https://go.microsoft.com/fwlink/?linkid=856078) hello 언어 참조에 액세스 하 고 [로그 분석 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856079)합니다.  

이미 친숙 한 인 경우 hello로 레거시 로그 분석 쿼리 언어 하지만 다음 hello 업그레이드의 일부로 tooyour 작업 영역에 추가 되는 hello 언어 변환기를 사용할 수 있습니다.

레거시 쿼리에서 방금 입력 한 다음 클릭 **변환** toosee hello 번역 된 버전입니다.  하나 또는 hello 검색 toorun hello 검색 단추를 클릭 하 고 변환 hello 쿼리 toouse 경고 규칙 같은 다른 위치에 붙여 넣을 수 있습니다.

![언어 변환기](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>다음 단계
- 체크 아웃 한 [hello 새로운 언어의 자습서](https://go.microsoft.com/fwlink/?linkid=856078)합니다.
- 안내는 [hello 로그 검색 포털을 사용 하 여의 자습서](log-analytics-log-search-log-search-portal.md) hello 새로운 쿼리 언어를 사용 합니다.
- 소개 toohello 새 가져오기 [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587)합니다.
