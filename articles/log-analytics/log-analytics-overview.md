---
title: "aaaWhat은 Operations Management Suite (OMS)에서 로그 분석을 인가요? | Microsoft Docs"
description: "Log Analytics는 클라우드 및 온-프레미스 환경에서 리소스에 의해 생성된 운영 데이터를 수집 및 분석하도록 도와주는 OMS(Operations Management Suite)의 서비스입니다.  이 문서에서는 로그 분석 및 링크 toodetailed 콘텐츠 hello 서로 다른 구성 요소에 간략하게 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Log Analytics란?
로그 분석은 서비스에 [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) 프로그램 클라우드 및 온-프레미스 환경 toomaintain의 가용성과 성능을 모니터링 하는 합니다.  여러 소스에서 리소스를 클라우드 및 온-프레미스 환경에서와 다른 모니터링 도구 tooprovide 분석에 의해 생성 된 데이터를 수집 합니다.  링크 toomore 더 알아볼 수 있도록 콘텐츠를 자세히 설명 및이 문서는 로그 분석의 개요를 제공 작동 방식을 hello 값에 대 한 간략 한 설명은 제공 합니다.

## <a name="is-log-analytics-for-you"></a>Log Analytics를 사용하시겠습니까?
현재 사용자의 Azure 환경에 모니터링을 설정하지 않은 경우 Azure 리소스에 대한 모니터링 데이터를 수집하고 분석하는 [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md)를 시작해야 합니다.  로그 분석 수 [Azure 모니터에서 데이터를 수집](log-analytics-azure-storage.md) toocorrelate 다른 데이터와 분석 추가 기능을 제공 합니다.

하려는 경우 toomonitor 온-프레미스 환경 또는 Azure 모니터 또는 System Center Operations Manager와 같은 서비스를 사용 하 여 기존 모니터링 있는, 로그 분석 중요 한 가치를 추가할 수 있습니다.  에이전트 및 이러한 다른 도구에서 단일 리포지토리로 직접 데이터를 수집할 수 있습니다.  로그 검색, 뷰 및 솔루션과 같은 Log Analytics의 분석 도구는 전체 사용자 환경의 중앙 집중식 분석을 제공하는 모든 수집된 데이터에 대해 작동합니다.


## <a name="using-log-analytics"></a>Log Analytics 사용
로그 분석 hello OMS 포털 또는 hello 모든 브라우저에서 실행 하 고 액세스 tooconfiguration 설정으로 하 고 여러 도구 tooanalyze 제공 하 고 수집 된 데이터에 있는 Azure 포털을 통해 액세스할 수 있습니다.  Hello 포털에서 활용할 수 있습니다 [검색 로그](log-analytics-log-searches.md) tooanalyze 수집 된 데이터를 쿼리를 생성 하는 경우 [대시보드](log-analytics-dashboards.md) 가장 중요 한 검색의 그래픽 보기가 포함 된 사용자 지정할 수 있습니다 및 [솔루션](log-analytics-add-solutions.md) 추가 기능 및 분석 도구를 제공 합니다.

hello에 대 한 요약 정보를 표시 하는 표시 hello 대시보드 hello OMS 포털에서 아래 hello 이미지는 [솔루션](#add-functionality-with-management-solutions) hello 작업 영역에 설치 되어 있습니다.  해당 솔루션에 대 한 hello 데이터에 더 이상 모든 타일 toodrill를 클릭할 수 있습니다.

![OMS 포털](media/log-analytics-overview/portal.png)

로그 분석 쿼리 언어 tooquickly 검색을 포함 하며 hello 리포지토리에 데이터를 통합 합니다.  만들고 저장할 수 [로그 검색](log-analytics-log-searches.md) toodirectly hello 포털에서 데이터를 분석 하거나 로그 검색이 자동으로 실행 toocreate 경고 hello hello 쿼리 결과 중요 한 상태를 표시 하는 경우.

![로그 검색](media/log-analytics-overview/log-search.png)

tooget 전반적인 환경의 hello 상태 그래픽 빠른 보기, 저장 된 로그 검색 tooyour에 대 한 시각화를 추가할 수 있습니다 [대시보드](log-analytics-dashboards.md)합니다.   

![대시보드](media/log-analytics-overview/dashboard.png)

로그 분석 외 주문 tooanalyze 데이터를 내보낼 수 있습니다 hello 데이터 hello OMS 리포지토리에서 도구와 같은 [Power BI](log-analytics-powerbi.md) 또는 Excel입니다.  Hello 활용할 수 있습니다 [로그 검색 API](log-analytics-log-search-api.md) toobuild 로그 분석 데이터 또는 다른 시스템과 toointegrate 활용 하는 사용자 지정 솔루션입니다.

## <a name="add-functionality-with-management-solutions"></a>관리 솔루션에서 기능 추가
[관리 솔루션](log-analytics-add-solutions.md) 추가 데이터 및 분석 도구 tooLog 분석을 제공 하는 기능 tooOMS를 추가 합니다.  새 레코드 종류 toobe 수집 된 로그 검색 함께 또는 추가 사용자 인터페이스 hello 대시보드에 hello 솔루션에서 제공 하 여 분석할 수 있는 정의할 수도 있습니다.  아래 예제에서는 이미지 hello hello를 보여 줍니다. [변경 내용 추적 솔루션](log-analytics-change-tracking.md)

![변경 내용 추적 솔루션](media/log-analytics-overview/change-tracking.png)

다양한 기능에 솔루션을 사용할 수 있으며 추가 솔루션을 지속적으로 추가합니다.  사용 가능한 솔루션을 쉽게 찾아볼 수 있습니다 및 [tooyour OMS 작업 영역에 추가](log-analytics-add-solutions.md) hello 솔루션 갤러리 또는 Azure Marketplace에서 제공 합니다.  보통 구성이 필요할 수 있는 다른 프로그램과 달리, 대부분 자동으로 배포되며 즉시 작업을 시작합니다.

![솔루션 갤러리](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Log Analytics 구성 요소
Hello 센터의 로그 분석은 Azure 클라우드 hello에서 호스팅되는 hello OMS 리포지토리에입니다.  데이터 원본 구성 및 솔루션 tooyour 구독을 추가 하 여 연결 된 원본에서 hello 저장소로 데이터를 수집 합니다.  데이터 원본 및 솔루션 각 만들어집니다 다른 레코드 유형을 고유 속성 집합이 있지만 쿼리 toohello 리포지토리에 함께 분석 될 수 있습니다.  이렇게 하면 서로 다른 소스에 의해 수집 된 여러 종류의 데이터와 같은 도구와 방법을 toowork toouse hello 있습니다.

![OMS 리포지토리](media/log-analytics-overview/overview.png)

연결 된 소스 hello 컴퓨터 및 로그 분석에 의해 수집 된 데이터를 생성 하는 다른 리소스는 있습니다.  여기에는 직접 연결된 [Windows](log-analytics-windows-agents.md) 및 [Linux](log-analytics-linux-agents.md) 컴퓨터에 설치된 에이전트 또는 [연결된 System Center Operations Manager 관리 그룹](log-analytics-om-agents.md)의 에이전트가 포함될 수 있습니다.  Azure 리소스의 경우 Log Analytics는 [Azure Monitor 및 Azure 진단](log-analytics-azure-storage.md)에서 데이터를 수집합니다.

[데이터 원본](log-analytics-data-sources.md) hello 여러 종류가 각 연결 된 소스에서 수집 된 데이터입니다.  여기에 [이벤트](log-analytics-data-sources-windows-events.md) 및 [성능 데이터](log-analytics-data-sources-performance-counters.md) 에서 [Windows](log-analytics-data-sources-windows-events.md) 및 Linux 에이전트와 같은 추가 toosources [IIS 로그](log-analytics-data-sources-iis-logs.md), 및 [사용자 지정 텍스트 로그](log-analytics-data-sources-custom-logs.md)합니다.  각 데이터 원본 toocollect, 원하는 및 hello 구성은 자동으로 배달 된 tooeach 연결된 원본 구성

사용자 지정 요구 사항이 있는 경우 hello를 사용할 수 있습니다 [HTTP 데이터 수집기 API](log-analytics-data-collector-api.md) toowrite 데이터 toohello 저장소 REST API 클라이언트에서.

## <a name="log-analytics-architecture"></a>Log Analytics 아키텍처
로그 분석의 hello 배포 요구 사항을 최소화 되므로 hello Azure 클라우드에서에서 호스팅되는 hello 중앙 구성 요소입니다.  이 hello 리포지토리를 toocorrelate를 허용 하 고 수집 된 데이터를 분석 하는 추가 toohello 서비스에 포함 됩니다.  hello 포털 클라이언트 소프트웨어에 대 한 요구 사항은 이므로 모든 브라우저에서 액세스할 수 있습니다.

[Windows](log-analytics-windows-agents.md) 및 [Linux](log-analytics-linux-agents.md) 컴퓨터에 에이전트를 설치해야 하지만 이미 [연결된 SCOM 관리 그룹](log-analytics-om-agents.md)의 멤버인 컴퓨터에 필요한 추가 에이전트는 없습니다.  SCOM 에이전트는 해당 데이터 tooLog 분석을 전달 하는 관리 서버와 toocommunicate를 계속 됩니다.  그러나 일부 솔루션 로그 분석을 사용 하 여 직접 에이전트 toocommunicate가 필요 합니다.  각 솔루션에 대 한 hello 설명서에는 해당 통신 요구 사항을 지정 합니다.

[Log Analytics에 등록](log-analytics-get-started.md)하면 OMS 작업 영역이 만들어집니다.  Hello 작업 영역 자체 데이터 저장소, 데이터 원본 및 솔루션에 고유한 로그 분석 환경으로 생각할 수 있습니다. 프로덕션와 같은 여러 환경을 구독 toosupport에 여러 작업 영역을 만들어 하 고 테스트할 수 있습니다.

![Log Analytics 아키텍처](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>다음 단계
* [사용 가능한 로그 분석 계정을 등록](log-analytics-get-started.md) tootest 사용자 환경에 있습니다.
* 다른 보기 hello [데이터 소스](log-analytics-data-sources.md) hello OMS 리포지토리에 사용할 수 있는 toocollect 데이터입니다.
* [Hello 솔루션 갤러리에서에서 사용할 수 있는 솔루션 hello 찾아보기](log-analytics-add-solutions.md) tooadd 기능 tooLog 분석 합니다.

