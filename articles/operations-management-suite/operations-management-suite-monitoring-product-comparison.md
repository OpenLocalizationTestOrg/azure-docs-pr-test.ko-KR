---
title: "제품 비교 모니터링 aaaMicrosoft | Microsoft Docs"
description: "Microsoft Operations Management Suite(OMS)란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.  이 문서는 OMS에 포함 하는 hello 다른 서비스를 식별 하 고 링크를 제공 tootheir 콘텐츠를 자세히 설명 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Microsoft 모니터링 제품 비교
이 문서에서는 System Center Operations Manager (SCOM)과 비교한 로그 분석 Operations Management Suite (OMS)에서 해당 아키텍처, 이러한 리소스를 모니터링 하는 방법 및 hello 데이터의 분석을 수행 하는 방법을 hello 논리를 기준으로 이러한 수집 합니다.  이것은 toogive 있습니다 차이 및 상대적 장점에 대 한 기본적인 이해 합니다.  

## <a name="basic-architecture"></a>기본 아키텍처
### <a name="system-center-operations-manager"></a>System Center Operations Manager
모든 SCOM 구성 요소는 데이터 센터에 설치하며  [에이전트](http://technet.microsoft.com/library/hh551142.aspx)는 SCOM에서 관리하는 Windows 및 Linux 컴퓨터에 설치합니다.  연결 하는 에이전트 너무[관리 서버](https://technet.microsoft.com/library/hh301922.aspx) hello SCOM 데이터베이스 및 데이터 웨어하우스 통신할입니다.  에이전트는 도메인 인증 tooconnect toomanagement 서버에 의존합니다.  인증서 인증을 수행 하거나 tooa 연결 수는 트러스트 된 도메인 외부에서 이러한 [게이트웨이 서버](https://technet.microsoft.com/library/hh212823.aspx)합니다.

SCOM에는 두 개의 SQL 데이터베이스, 운영 데이터에 대 한 및 다른 데이터 웨어하우스 toosupport 보고 및 데이터 분석 필요합니다.  A [보고 서버](https://technet.microsoft.com/library/hh298611.aspx) hello 데이터 웨어하우스에서 데이터에 대해 tooreport SQL Reporting Services를 실행 합니다. 

SCOM은 [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708), [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html) 등의 제품에 관리 팩을 사용하여 클라우드 리소스를 모니터링할 수 있습니다.  이러한 관리 팩을 사용 하 여 하나 또는 많은 로컬 에이전트를 검색 하기 위한 프록시로 클라우드 리소스 및 해당 성능 및 가용성 toomeasure 워크플로 실행 합니다.  프록시 에이전트 너무도 사용 됩니다[네트워크 장치 모니터링](https://technet.microsoft.com/library/hh212935.aspx) 및 기타 외부 리소스입니다.

hello 운영 콘솔은 tooone hello 관리 서버의 연결 및 관리자 tooview hello를 사용 하면 수집 된 데이터를 분석 및 hello SCOM 환경을 구성 하는 Windows 응용 프로그램입니다.  웹 기반 콘솔은 모든 IIS 서버에 호스팅할 수 있으며 브라우저를 통해 데이터 분석을 제공합니다.

![SCOM 아키텍처](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
배포 하 고 최소한의 비용 및 관리 업무도 관리할 수 있도록 Azure 클라우드 hello에 있는 대부분 OMS 구성 요소입니다.  로그 분석에 의해 수집 된 모든 데이터는 hello OMS 리포지토리에 저장 됩니다.

Log Analytics는 다음 세 가지 원본 중 하나에서 데이터를 수집할 수 있습니다.

* 실제 및 가상 컴퓨터를 Windows를 실행 하는 hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) Linux와 hello 또는 [Linux 용 Operations Management Suite 에이전트](https://technet.microsoft.com/library/mt622052.aspx)합니다.  이러한 컴퓨터는 Azure 또는 다른 클라우드에서 온-프레미스 또는 가상 컴퓨터일 수 있습니다.
* Azure의 작업자 역할, 웹 역할 또는 가상 컴퓨터에서 [Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 데이터를 수집하는 Azure 저장소 계정.
* [연결 tooa SCOM 관리 그룹](https://technet.microsoft.com/library/mt484104.aspx)합니다.  이 구성에서는 hello 에이전트는 다음 배달 위치 toohello OMS 데이터 저장소 hello 데이터 toohello SCOM 데이터베이스에 배달 하는 SCOM 관리 서버와 통신 합니다.
  관리자는 수집 된 데이터를 분석 하 고 Azure에서 호스팅되는 모든 브라우저에서 액세스할 수 있으며 hello OMS 포털을 통한 로그 분석을 구성 합니다.  모바일 앱 tooaccess이 있는이 데이터 hello 표준 플랫폼에서 사용할 수 있습니다.

![Log Analytics 아키텍처](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>SCOM 및 Log Analytics 통합
SCOM에 대 한 로그 분석 데이터 원본으로 사용 될 때 환경을 모니터링 하는 하이브리드 환경에서 두 제품의 hello 기능을 활용할 수 있습니다.  SCOM에서 toocontinuing toorun 관리 팩 뿐만 아니라, OMS에서 관리 하는 hello  ¼ ײ toobe 통해 기존의 SCOM 에이전트를 구성할 수 있습니다.  
연결 된 SCOM 관리 그룹에서 데이터 tooLog 분석 네 가지 방법 중 하나를 사용 하 여 배달 됩니다.

* 이벤트 및 성능 데이터 hello 에이전트에 의해 수집 되 고 tooSCOM 배달 됩니다.  다음에 SCOM 관리 서버 hello 데이터 tooLog 분석을 제공합니다.
* IIS 로그와 같은 일부 이벤트 및 보안 이벤트 toobe 배달 직접 tooLog 분석 hello 에이전트에서 계속 합니다.
* 일부 솔루션에 추가 소프트웨어 toohello 에이전트 배달 되거나 소프트웨어 설치 toocollect 추가 데이터도 록 요구할 됩니다.  이 데이터를 일반적으로 보내야 직접 tooLog 분석 합니다.
* 일부 솔루션 hello 에이전트에서 사용 하지 않고도 SCOM 관리 서버에서 직접 데이터를 수집 합니다.  예를 들어 hello [경고 관리 솔루션](https://technet.microsoft.com/library/mt484092.aspx) 생성 된 후 SCOM에서 경고를 수집 합니다.

## <a name="monitoring-logic"></a>모니터링 논리
로그 분석 및 SCOM 에이전트에서 수집 하는 유사한 데이터 작업을 설치 했지만 hello 수집 된 데이터를 분석 하는 방법을 정의 하 고 데이터 수집에 대 한 논리를 구현 하는 방법 및 근본적으로 다릅니다.

### <a name="operations-manager"></a>Operations Manager
구현 되는 SCOM에 대 한 모니터링 논리가 [관리 팩](https://technet.microsoft.com/library/hh457558.aspx) tooanalyze 데이터 수집 및 해당 구성 요소의 hello 상태를 측정 하는 구성 요소 toomonitor 검색에 대 한 논리를 포함 하는 합니다.  데이터 모니터링은 간단히 이벤트 또는 성능 카운터를 수집하는 작업일 수도 있고 스트립트에 구현된 복잡한 논리를 사용할 수도 있습니다.  전체 모니터링을 포함 하는 관리 팩의 다양 한에 대해 사용할 수 있는 [Microsoft 및 타사 응용 프로그램](http://go.microsoft.com/fwlink/?LinkId=82105) 더하기 toohardware 및 네트워크 장치에 있습니다.  사용자 지정 응용 프로그램에 대해 [고유한 관리 팩을 작성](http://aka.ms/mpauthor) 할 수 있습니다.

관리 팩 각 성능 카운터 샘플링, 서비스의 hello 상태를 확인 하거나 스크립트를 실행 등의 몇 가지 고유한 모니터링 기능을 수행 하는 여러 워크플로 포함 합니다.  각 워크플로에 독립적으로 실행 하 고 자체의 결과 데이터베이스와 같은 씁니다 tooand 경고를 생성 합니다 여부를 정의 합니다. 

워크플로 hello 빈도 실행 하는 오류를 고려해 야 하는 hello 임계값 등의 세부 정보 및 생성 하는 hello 경고의 hello 심각도 재정의할 수 있습니다.  또한 고유 워크플로를 추가하여 추가 기능을 제공할 수 있습니다.

![재정의](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

관리 팩 hello Operations Manager 데이터베이스에 설치 되 고 tooagents 관리 서버에 의해 자동으로 배포 됩니다.  각 에이전트는 자동으로 관리 팩을 다운로드 하 고 워크플로 관련 toohello가 설치 되어 응용 프로그램을 로드 합니다.  Hello 에이전트에 의해 수집 된 데이터는 삽입을 위한 백 toohello 관리 서버 hello SCOM 데이터베이스 및 데이터 웨어하우스에 배달 됩니다.  운영 콘솔 hello tooview 있으며 사용자 지정 보기, 대시보드 및 hello 관리 팩에 포함 된 보고서를 통해이 데이터를 분석 합니다.

hello 다이어그램을 다음 관리 팩의 hello 분포를 보여 줍니다.

![관리 팩 흐름](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>이벤트 및 성능 수집
Log Analytics는 Windows 이벤트 로그, IIS 로그, Syslog와 같은 원본을 사용하여 에이전트 시스템에서 이벤트 및 성능 카운터를 수집합니다.  에 대 한 데이터는 hello 로그 분석 포털을 통해 수집 되 고 다음 로그 쿼리 tooanalyze hello 수집 된 데이터를 만들 기준 정의할 수 있습니다.  OMS 작업 영역을 만들 때 표준 기준 집합을 정의하며 특정 애플리케이션에 대한 추가 데이터를 정의할 수 있습니다. 

![Log Analytics에서 이벤트 로그 정의](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

SCOM의 많은 일반적으로 데이터에 대 한 특정 조건을 정의 하는 자세한 워크플로에 대 한 응답으로 수행 해야 하는 hello 작업, 로그 분석에는 데이터 수집에 대 한 보다 일반적인 조건입니다.  로그 쿼리 및 솔루션에 분석 및 hello 클라우드에 특정 데이터를 수집한 후 수행에 대 한 대상된 조건을 더 제공 합니다.

#### <a name="solutions"></a>솔루션
솔루션은 데이터 수집 및 분석에 대해 추가 논리를 제공합니다.  솔루션 tooadd tooyour OMS 구독 hello 솔루션 갤러리에서에서 선택할 수 있습니다.

![솔루션 갤러리](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

솔루션은 주로 이벤트 및 hello OMS 리포지토리에 수집할 성능 카운터의 분석을 제공 하는 hello 클라우드에서 실행 합니다.  로그 쿼리 함께 또는 추가 사용자 인터페이스를 OMS 대시보드에 hello hello 솔루션에서 제공 하 여 분석할 수 있는 추가 데이터 toobe 수집를 정의할 수도 있습니다. 

예를 들어 hello [변경 내용 추적 솔루션](https://technet.microsoft.com/library/mt484099.aspx) 감지 구성 에이전트 시스템에서 변경 되 고 요약 하는 여러 그래픽 보기가 포함 된 분석할 수 있는 저장소 변경을 감지 했습니다. 이벤트 toohello OMS를 씁니다.  드릴 다운할 수 있습니다 hello 요약 보기에서 쿼리 로그에는 디스플레이 hello hello 솔루션에 의해 수집 된 데이터를 자세히 설명 합니다.

솔루션을 선택할 수 있습니다 tooyour 구독을 추가, 현재 없는 hello 기능 toocreate 솔루션 합니다.  Hello 이벤트 및 성능 카운터 toocollect를 선택 하 고 사용자 지정 로그 쿼리를 기반으로 하는 사용자 지정 뷰를 만들 수 있습니다.

로그 분석에 대 한 논리를 모니터링 하는 hello hello 다음 다이어그램에에서 요약 되어 있습니다.

![Log Analytics 솔루션 흐름](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>상태 모니터링
### <a name="operations-manager"></a>Operations Manager
SCOM 수 응용 프로그램의 hello 다른 구성 요소를 모델링 하 고 각각에 대 한 실시간 상태를 제공 합니다.  이렇게 하면 오류 및 시간에 따른 성능을 있습니다 toonot 보기 에서만 검색 되었지만 toovalidate 언제 든 지 응용 프로그램 또는 시스템의 실제 상태와 각 구성 요소를 hello 수도 있습니다.  Hello 응용 프로그램에서 사용할 수 있는 기간을 인식 하기 때문에 SCOM의 상태 엔진 hello에 서비스 수준 계약 (SLA) 분석 하 고 시간이 지남에 따라 응용 프로그램의 hello 가용성에 대해 보고 하는 지원 합니다.

예를 들어, 아래의 hello 보기 hello SCOM에서 모니터링 하는 SQL 데이터베이스 엔진의 실시간 상태를 보여 줍니다.  hello 보기의 절반 hello 아래쪽에 각각의 hello 데이터베이스 엔진의 하나에 대 한 hello 데이터베이스의 hello 상태 표시 됩니다.

![상태 뷰](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

hello hello 데이터베이스 엔진의 하나에 대 한 상태 탐색기 아래와 같습니다 hello 모니터를 사용 하는 toodetermine와의 전반적인 상태.  이러한 모니터는 hello SQL 관리 팩에에서 정의 되 고 SCOM에서 검색 된 모든 SQL 데이터베이스 엔진에 대해 실행 합니다.

![상태 탐색기](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

여러 시스템에서 구성 요소에는 분산된 응용 프로그램의 결합 된 toomeasure hello 상태 될 수 있습니다.  이 기능은 분산된 여러 구성 요소가 포함된 업무용 응용 프로그램에 특히 유용합니다.  Hello 각 구성 요소의 상태를 측정 하는 모델 해당 롤업 hello 응용 프로그램에 대 한 가용성을 만들 수 있습니다.

Active Directory는 모델 tooanalyze 분산된 된 구성 요소를 제공 하는 하나의 관리 팩의 예시입니다.  hello 샘플 다이어그램의 표시 hello 상태에서는 전체 환경 및 포리스트, 도메인 및 도메인 컨트롤러 간의 hello 관계 hello 합니다.  이러한 각 구성이 요소 하위 구성 요소를 포함 하 고 여러 위의 비슷한 toohello SQL 예제를 모니터링 합니다.

![SCOM 다이어그램 뷰](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS는 일반적인 엔진 toomodel 응용 프로그램이 하지 않거나 실시간 상태를 측정 합니다.  개별 솔루션 hello 평가 수 특정 서비스의 전반적인 상태 수집 된 데이터를 기반으로 하며 hello 에이전트 tooperform 실시간 분석을 사용자 지정 논리를 설치할 수 있습니다.  솔루션 toohello OMS 리포지토리에 대 한 액세스를 사용 하는 hello 클라우드에 실행 되므로 일반적으로 관리 팩에서 수행 하는 보다 자세히 분석을 자주 제공할 수 있습니다. 

예를 들어 hello [AD 평가 및 SQL 평가 솔루션](https://technet.microsoft.com/library/mt484102.aspx) 수집 된 데이터를 분석 하 고 hello 환경의 다양 한 측면에 대 한 등급을 제공 합니다.  Tooimprove hello 가용성과 성능을 hello 환경을 만들 수 있는 향상 된 기능에 대 한 권장 사항을 포함 합니다.

![AD 평가 솔루션](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>데이터 분석
SCOM와 로그 분석에는 각각 다양 한 기능 tooanalyze 수집 된 데이터를 제공합니다.  SCOM 다양 한 형식 및 테이블 형식으로 데이터 웨어하우스 hello의에서 데이터를 제공 하는 것에 대 한 보고서의에서 최근 데이터 분석을 위해 hello 운영 콘솔의에서 보기와 대시보드를에 있습니다.  로그 분석 hello OMS 리포지토리에 데이터를 분석 하기 위한 완전 한 로그 쿼리 언어 및 인터페이스를 제공 합니다.  SCOM은 로그 분석에 데이터 원본으로 사용 된 경우 hello 리포지토리 hello 로그 분석 도구는 두 시스템에서 사용 되는 tooanalyze 데이터 될 수 있도록 SCOM에 의해 수집 된 데이터가 포함 됩니다.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>뷰
Hello 운영 콘솔에서에서 뷰를 사용 하면 tooview 다른 데이터 형식에서에서 수집 된 SCOM에서 서로 다른 형식으로 이벤트, 경고 및 상태 데이터 및 성능 데이터에 대 한 선 그래프에 대 한 일반적으로 테이블 형식입니다.  뷰가 최소 분석 또는 hello 데이터의 통합을 수행 하지만 toofilter tooparticular 조건에 따라 허용 해 않습니다. 

![뷰](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

일반적으로 관리 팩 hello 응용 프로그램 또는 시스템 모니터링을 지 원하는 여러 뷰를 제공 합니다.  경고 검색 된 문제에 대 한 보기 및 카운터에 대 한 성능 보기, hello 관리 팩에서 검색 하는 hello 다른 개체에 대 한 상태 보기가 포함 될 수 있습니다이 됩니다.

뷰는 hello 미해결 경고 및 모니터링 되는 시스템 및 개체의 hello 성능 상태를 포함 하 여 hello 환경의 현재 상태를 분석 하는 데 특히 적합 합니다.  근본 원인 toodetailed 이벤트 또는 성능 데이터 순서 toodiagnose에서 특정 경고를 지 원하는 다운 드릴 수 있습니다. 마찬가지로, 볼 수 있습니다 hello 성능 및 응용 프로그램 tooassess의 다른 구성 요소 상태의 현재 상태.

#### <a name="dashboards"></a>대시보드
Hello 작업 주로 운영 콘솔에서에서 대시보드 보기 하지만 더 사용자 지정이 가능 하 고 다양 한 시각화 기능을 포함할 수 동일한 데이터를 hello 합니다.  사용자 목적에 맞게 쉽게 사용자 지정 가능한 표준 대시보드 집합을 사용할 수 있습니다.  또한 PowerShell 위젯을 사용하면 PowerShell 쿼리에서 반환한 데이터를 표시할 수 있습니다.

![대시보드](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

개발자는 해당 관리 팩에 포함 하는 hello 기능 tooadd 사용자 지정 구성 요소 toodashboards 있습니다.  특별 한 tooa hello 아래에 표시 된 SQL 관리 팩에서에서 hello 대시보드 등 특정 응용 프로그램 수 있습니다.  이 대시보드는 사용자 지정 버전의 템플릿으로도 사용할 수 있습니다.

![SQL 대시보드](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>보고서
SCOM의 보고서는 테이블 형식으로 hello 데이터 웨어하우스에서 데이터를 분석합니다.  이러한 보고서는 PDF, CSV, Word 등의 다양한 파일 형식으로 인쇄하여 자동 배달 예약을 할 수 있습니다.  보고서에서 장기적 추세 분석에 특히 적합 하므로 hello 데이터 웨어하우스의 데이터를에서 사용 합니다.

관리 팩은 일반적으로 특정 응용 프로그램에 대한 사용자 지정 보고서를 제공합니다.  또한 일반 보고서 라이브러리 중에서 선택하여 사용자 응용 프로그램에 맞게 사용자 지정하거나 임시 분석을 수행할 수 있습니다.

다음은 Active Directory 관리 팩 hello에 의해 수집 된 데이터를 표시 하는 샘플 성능 보고서입니다.

![보고서](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
로그 분석에는 [쿼리 언어](https://technet.microsoft.com/library/mt484120.aspx) 사용자 지정 보기 또는 보고서 hello 필요 toocreate 없이 여러 응용 프로그램의 데이터 간에 tooperform 분석을 사용할 수 있는 합니다.  OMS는 hello 클라우드로 구현 하기 때문에 쿼리 및 데이터 분석의 제목 tooany 하드웨어 제한 없는 성능과 수백만 개의 레코드를 포함 하 여 쿼리를 빠르게 분석할 수 있습니다. 

쿼리 로그 분석에는 또한 다른 기능의 기반이 hello 합니다.  쿼리를 저장할 지정, 그 결과 tooExcel 내보내기 또는 자동으로 정기적으로 실행 하 고 그 결과 특정 조건과 일치 하는 경우 경고를 생성 합니다.  

![로그 쿼리 흐름](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

다음은 Log Analytics 쿼리의 예입니다.  이 예제에서는 "시작" hello 이름에 모든 이벤트는 반환 되 고, 이벤트로 그룹화 id.  hello 사용자 인터페이스 tooperform hello 분석을 동적으로 생성 하는 로그 분석 및 hello 사용자는 단순히 hello 쿼리를 제공 합니다.  Hello 목록의 모든 항목을 선택 하는 반환 hello 이벤트 데이터를 자세히 설명 합니다.

![로그 쿼리](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

또한 tooproviding 임시 분석 로그 분석에 대 한 쿼리에 저장할 수 있는 나중에 사용 및 추가 된 tooyour [OMS 대시보드](http://technet.microsoft.com/library/mt484090.aspx) hello 다음 예제와 같이 합니다.

![OMS 대시보드](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>다음 단계
* [SCOM(System Center Operations Manager)](https://technet.microsoft.com/library/hh205987.aspx)을 배포합니다.
* [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics)에 등록합니다.  

