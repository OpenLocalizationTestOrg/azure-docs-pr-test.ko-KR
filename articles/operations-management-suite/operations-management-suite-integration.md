---
title: "aaaIntegrating와 OMS Operations Management Suite () | Microsoft Docs"
description: "또한 toousing hello OMS의 표준 기능, 하이브리드 관리 환경을, tooprovide 사용자 지정 관리 시나리오 고유 tooyour 환경 또는 사용자 지정 tooprovide 다른 관리 응용 프로그램 및 서비스 tooprovide를 통합할 수 있습니다. 고객에 대 한 관리 경험 합니다.  이 문서에서는 OMS와 함께 통합 하기 위한 다른 옵션에 대해 간략하게 설명 하 고 자세한 기술 정보를 제공 하는 tooarticles 연결 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>OMS(Operations Management Suite)와 통합
Operations Management Suite란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.  또한 toousing hello OMS의 표준 기능, 하이브리드 관리 환경을, tooprovide 사용자 지정 관리 시나리오 고유 tooyour 환경 또는 사용자 지정 tooprovide 다른 관리 응용 프로그램 및 서비스 tooprovide를 통합할 수 있습니다. 고객에 대 한 관리 경험 합니다.  이 문서에서는 OMS와 함께 통합 하기 위한 다른 옵션에 대해 간략하게 서비스를 제공 하며 자세한 기술 정보를 제공 하는 tooarticles 링크를 제공 합니다. 

## <a name="log-analytics"></a>Log Analytics
Log Analytics에서 수집한 관리 데이터는 Azure에 호스팅되는 리포지토리에 저장됩니다.  Hello 저장소에 저장 된 모든 데이터는 아주 많은 양의 데이터에서 신속한 분석을 제공 하는 로그 검색에서 사용할 수 있는입니다.  통합 요구 사항, 분석에 사용할 수 있도록 새 데이터 나 tooextract 데이터 hello 리포지토리 tooprovide 새 시각화에에서 toopopulate hello 저장소 또는 다른 관리 도구로 toointegrate 수 있습니다.

Hello 저장소에서 데이터의 각 부분을 레코드로 저장 됩니다.  Hello 리포지토리를 채울 때 솔루션을 사용 하는 hello 레코드 종류 및 해당 속성에 대 한 설명을 사용 하 여 사용자를 제공 해야 합니다.  데이터를 검색할 때 사용 하는 hello 데이터에 대 한이 정보가 필요 합니다.

![Hello OMS 리포지토리에 채우기](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>로그 분석 저장소 hello 채우기
Hello OMS 리포지토리에 채우는 데 사용 하는 방법은 여러 가지가 있습니다.  hello를 사용 하면에 따라 달라 집니다 hello 원본 데이터 위치한, hello 형식의 hello 데이터와 같은 요소 클라이언트 toosupport 필요 합니다.  데이터는 hello 저장소에 저장 되 면 차이가 없습니다. 수집 된 방법입니다.

hello 다음 섹션에서는 옵션에 설명 hello 다른 hello OMS 리포지토리에 채우는 데 사용 합니다.

#### <a name="connected-sources-and-data-sources"></a>연결된 원본 및 데이터 원본
연결 된 원본은 hello OMS 리포지토리에 대 한 데이터를 검색할 수 있는 hello 위치입니다.  데이터 원본 및 솔루션에 연결 된 원본에서 실행 하 고 hello 수집 되는 특정 데이터를 정의 합니다.  응용 프로그램에서 이러한 데이터 원본의 데이터 tooone를 쓰려면 다음 수 수집 hello 데이터 소스를 구성 하 여 합니다.  예를 들어 응용 프로그램 Syslog 이벤트를 만드는 경우 다음은에서 수집할 수 hello Syslog 데이터 원본에 의해 Linux 에이전트입니다.

* [Log Analytics의 데이터 원본](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>솔루션
OMS의 hello 기능을 확장 하는 솔루션입니다.  솔루션 hello 연결된 원본에서 데이터를 수집할 수 있습니다 또는 hello 리포지토리에 이미 수집 된 레코드에 대해 분석을 수행 될 수 있습니다.  Microsoft에서 제공 하는 각 솔루션에는 각기 수집한 hello 데이터에 hello 세부 정보를 제공 하는 개별 문서를 있습니다.

* [Log Analytics의 솔루션](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>HTTP 데이터 수집기 API
로그 분석 HTTP 데이터 수집기 API hello는 tooadd JSON 데이터 toohello 로그 분석 저장소 수 있는 REST API입니다.  다른 데이터 원본 또는 솔루션 hello 중 하나를 통해 데이터를 제공 되지 않는 응용 프로그램이 있는 경우이 API를 활용할 수 있습니다.  Hello API를 호출할 수 있으며 모든 데이터 원본이 나 솔루션의 hello 수집 일정에 의존 하지 않는 클라이언트에서 사용 되는 toopopulate hello 리포지토리 수 있습니다.

* [Log Analytics HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Hello 로그 분석 저장소에서 데이터를 검색 합니다.
Hello OMS 리포지토리에서 데이터를 검색 하기 위한 여러 메서드가 있습니다.  Hello OMS 콘솔을 사용 하 여 사용자가 tooretrieve 데이터 하 고 다른 종류의 시각화 및 분석을 제공할 수 있습니다.  다른 관리 솔루션 같은 외부 프로세스에서 hello 데이터를 검색할 수도 있습니다.

#### <a name="log-searches"></a>로그 검색
Hello OMS 리포지토리에 저장 된 모든 데이터를 로그 검색을 통해 사용할 수 있습니다.  사용자는 hello OMS 콘솔에서 자신의 임시 분석을 수행 하거나 특정 로그 검색에 대 한 시각화와 대시보드를 만듭니다.  솔루션은 미리 정의 된 검색 결과에 따라 시각화를 사용한 사용자 지정 보기를 포함할 수 있습니다.  외부 응용 프로그램 또는 관리 도구에서 hello OMS 리포지토리에 hello 로그 검색 API tooaccess 데이터를 사용할 수 있습니다.  

* [Log Analytics의 로그 검색](../log-analytics/log-analytics-log-searches.md)
* [Log Analytics 로그 검색 REST API](../log-analytics/log-analytics-log-search-api.md)
* [Log Analytics cmdlet](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>사용자 지정 보기
뷰 디자이너 hello toocreate 사용자 지정 보기를 hello OMS 콘솔에서 시각화 및 분석 솔루션의 hello 데이터는 사용자가 제공 하는 있습니다.  각 보기 hello 콘솔 및 정의 하는 로그 검색을 기반으로 하는 시각화 부분 개수에 관계 없이의 hello 기본 페이지에 표시 되는 타일을 포함 합니다.

* [Log Analytics 뷰 디자이너](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
로그 분석 자동으로 내보낼 수 데이터 hello OMS 저장소에서 Power BI로 하므로 해당 시각화 및 분석 도구를 활용할 수 있습니다.  Toodate를 hello 데이터를 유지 하므로이 내보내기는 일정에 따라 수행 합니다. 

* [로그 분석 데이터 tooPower BI 내보내기](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automation
OMS를 자동화할 수 프로세스 tooreact toocollected 데이터 또는 tooperform 기타 관리 기능.  응용 프로그램에서 데이터를 수집 하 고 hello OMS 리포지토리에 삽입할 수 있습니다 또는 hello 감지가 응답 toodata hello 리포지토리에서 찾을 수의 알려진된 문제를 자동화할 수 있습니다. 

![Automation](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbook
Azure 자동화의 Runbook hello Azure 클라우드에서에서 PowerShell 스크립트 및 워크플로 실행 합니다.  Azure에서 toomanage 리소스나 hello 클라우드에서 액세스할 수 있는 다른 모든 리소스에 사용할 수 있습니다.  Hybrid Runbook Worker를 사용하는 로컬 데이터 센터에서 Runbook을 실행할 수도 있습니다.  다양 한 PowerShell과 같은 메서드를 사용 하 여 외부 프로세스 또는 hello Azure 포털에서에서 runbook을 시작 하거나 자동화 API hello 수 있습니다.

* [Azure 자동화에서 Runbook 시작](../automation/automation-starting-a-runbook.md)
* [Azure Automation cmdlet](https://msdn.microsoft.com/library/dn690262.aspx)
* [Automation REST API](https://msdn.microsoft.com/library/mt662285.aspx)
* [Automation .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>경고
경고 규칙 tooa 일정에 따라 로그 검색을 자동으로 실행 합니다.  일치 하는 hello 결과가 특정 조건 hello 결과 경고 Azure 자동화에서 runbook을 시작 하거나 외부 프로세스를 시작할 수 있는 webhook 호출 수 있습니다.  이러한 응답 모두 hello 로그 검색에서 반환 된 hello 데이터를 포함 하 여 hello 경고의 세부 정보를 포함할 수 있습니다.

* [Log Analytics의 경고](../log-analytics/log-analytics-alerts.md)
* [Log Analytics 경고 API](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Backup 및 Site Recovery
Azure 백업 및 사이트 복구에는 엔터프라이즈 데이터를 보호 하 고 서버 및 응용 프로그램의 hello 가용성을 보장 하는 것에 대 한 서비스를 제공 합니다.  이러한 서비스 tooperform 등의 방법으로 응용 프로그램에 대 한 백업 서비스를 제공 하거나 가상 컴퓨터의 장애 조치를 개시 활용할 수 있습니다.

* [Azure Backup cmdlet](https://msdn.microsoft.com/library/mt619253.aspx)
* [Azure Site Recovery REST API](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Azure Site Recovery Cmdlet](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>사용자 지정 솔루션
작업 영역에서 또는 고객의 작업 영역에서 사용자 지정 솔루션 toorun에 통합 논리를 캡슐화 할 수 있습니다.  솔루션에에서 포함할 수 hello 통합 방법 중 하나 추가 tooother 리소스 tooprovide에이 문서는 완전 한 관리 시나리오.  hello 솔루션 제거 되 면 hello OMS 작업 영역 및 Azure 구독에서 제거 됩니다 만들 hello 리소스를 모두 되도록 hello 솔루션의 hello 리소스 패키지 됩니다.

예를 들어 솔루션 자동화 runbook toogather 및 프로세스 데이터를 포함 하 고 hello 로그 분석 저장소 hello HTTP 데이터 수집기 API를 사용 하 여 채울 수 없습니다.  사용자 지정 보기를 표시 하 고 hello 수집 된 데이터를 분석 하는 포함 될 수 있습니다.  

* 사용자 지정 솔루션(출시 예정) 만들기    

## <a name="next-steps"></a>다음 단계
* 참조 hello [OMS SDK](operations-management-suite-sdk.md) 기술에 대 한 내용은 OMS 서비스를 자동화 합니다.  

