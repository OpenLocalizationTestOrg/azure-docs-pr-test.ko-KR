---
title: "aaaOperations Management Suite (OMS) 개요 | Microsoft Docs"
description: "OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.  이 문서에서는 OMS의 hello 값 hello 다른 서비스와 OMS에 포함 된 제품을 식별 하 고 링크를 제공 tootheir 콘텐츠를 자세히 설명 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>OMS(Operations Management Suite)란?
이 문서에서는 소개 tooOperations hello 비즈니스 가치를 제공, 포함, hello 서비스 및 관리 솔루션 및 다른 서비스를 패키지 하는 hello 제공의 간략 한 개요를 포함 하 여 Management Suite (OMS) 및 솔루션입니다.  링크는 포함 toohello 배포 하 고 각 서비스 및 솔루션 사용에 대 한 설명서를 자세히 설명 합니다.

## <a name="from-on-premises-toohello-cloud"></a>온-프레미스 toohello 클라우드에서
Microsoft는 오랫동안 기업 환경을 관리하기 위한 제품을 제공해 왔습니다.  여러 제품 2007에서 관리 제품의 hello System Center 제품군으로 통합 되었습니다.  이 Configuration Manager 같은 소프트웨어 배포 및 인벤토리를 사전에 모니터링 시스템 및 응용 프로그램을 Orchestrator runbook tooautomate 수동 프로세스를 포함 하는 제공 하는 Operations Manager 기능을 제공 하는 포함 및 Data Protection Manager 백업 및 중요 한 데이터의 복구 합니다.

Toohello 클라우드 이동 더욱 많은 컴퓨팅 리소스와 System Center 제품에는 Operations Manager 및 azure에서 리소스 관리 Orchestrator 같은 더 많은 클라우드 기능 왔습니다.  이러한 제품은 여전히 근본적으로 온-프레미스 솔루션으로 설계되었지만, 온-프레미스 관리 환경을 배포하고 유지 관리하는 데 상당한 투자가 필요합니다.  toocompletely hello 클라우드를 활용 하 고 향후 지원 응용 프로그램의 경우 새로운 접근 방식을 toomanagement 필요 했습니다.

## <a name="introducing-operations-management-suite"></a>Operations Management Suite 소개
Operations Management Suite (OMS)은 hello 처음부터 hello 클라우드에서으로 설계 된 관리 서비스의 컬렉션입니다.  OMS 구성 요소는 온-프레미스 리소스를 배포하고 관리하는 대신 Azure에서 전적으로 호스팅됩니다.  구성 작업이 최소화되어 문자 그대로 몇 분 안에 실행할 수 있습니다.  

- **배포에 드는 비용 및 복잡성 최소화.**  Azure에 저장 되므로 모든 hello 구성 요소 및 OMS에 대 한 데이터를 관리할 수 있습니다 및 짧은 시간 동안 hello 복잡성 및에 대 한 투자 없이 실행 온-프레미스 구성 요소입니다.
- **확장 toocloud 수준입니다.**  필요 하지 않은 계산 리소스에 대 한 요금을 지불 하는 방법에 대 한 tooworry 없거나 hello 이후의 저장소 공간이 부족 하는 방법에 대 한 클라우드 사용 하면 toopay 동안만 무엇 실제로 사용 하 고 필요한 tooany 부하를 쉽게 확장 됩니다.  시작 하는 몇 가지 리소스 tooget를 관리 하 여 시작을 다음 tooyour 환경 전체를 확장할 수 있습니다.
- **Hello 최신 기능을 사용 합니다.**  OMS 서비스의 기능은 지속적으로 추가되고 업데이트됩니다.  지속적으로 액세스를 포함 하지 않는 요구 사항 toodeploy toohello 최신 기능 해야합니다.
- **통합 서비스.**  중요 한 가치 자체적으로 제공 하는 각 hello OMS 서비스 수 연동 toosolve 복잡 한 관리 시나리오입니다.  예를 들어 Azure 자동화에서 runbook이 Azure Site Recovery와 장애 조치 프로세스를 드라이브 수도 있으며 다음 로그 정보 tooLog 분석 toogenerate 경고.
- **글로벌 지식.**  OMS의 관리 솔루션 액세스 toohello 최신 정보를 지속적으로 있어야 합니다.  예를 들어 보안 및 감사 솔루션 hello hello 전 세계 검색 하는 hello 최신 위협 요소를 사용 하 여 위협 분석을 수행할 수 있습니다.
- **어디서나 액세스.**  브라우저만 있다면 어디서나 관리 환경에 액세스할 수 있습니다.  스마트폰에서 액세스할 tooyour 모니터링 데이터에 대 한 hello OMS 앱을 설치 합니다.

### <a name="is-it-just-for-hello-cloud"></a>Hello 클라우드에 대 한 것 입니까?
OMS 서비스에서 실행 해 서 온-프레미스 환경 효과적으로 관리할 수 없다고 hello 클라우드가 아닙니다.  모든 Windows 에이전트를 저장 하거나 해당 데이터 센터의 Linux 컴퓨터는 클라우드 또는 온-프레미스 서비스에서 수집 된 다른 모든 데이터와 함께 분석 될 수 있습니다는 분석 데이터 tooLog 보냅니다.  온-프레미스 리소스에 대 한 백업 및 고가용성에 대 한 Azure 백업 및 Azure 사이트 복구 tooleverage hello 클라우드를 사용 합니다.  
Runbook hello 클라우드에서 온-프레미스 리소스를 액세스할 일반적으로 수 없지만 하나 이상의 컴퓨터에 에이전트를 설치할 수 있습니다 너무를 호스팅할 데이터 센터에서 runbook입니다.  Runbook을 시작 하면 지정 하면 추가할지 toorun hello 클라우드 또는 로컬 작업자에서 됩니다.

## <a name="hybrid-management-with-system-center"></a>System Center를 사용하여 하이브리드 관리
System Center의 기존 설치를 사용 하도록 설정한 경우에 두 온-프레미스에 대 한 OMS 서비스 tooprovide 하이브리드 솔루션으로 이러한 구성 요소를 통합할 수 있으며 클라우드 각 제품의 hello 상대 전문성을 활용 하는 환경 수 있습니다.  기존 Operations Manager 관리 그룹 tooLog 분석 tooanalyze 관리 에이전트 hello 클라우드에 연결 합니다.  데이터 toohello 클라우드 Data Protection Manager toobackup와 기존 백업 프로세스를 사용 합니다.  


## <a name="oms-services"></a>OMS 서비스
OMS의 핵심 기능 hello Azure에서 실행 되는 서비스 집합에서 제공 됩니다.  각 서비스는 특정 관리 기능을 제공 하 고 서비스 tooachieve 다른 관리 시나리오를 결합할 수 있습니다.

|| 부여 | 설명 |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | 모니터링 하 고 다양 한 리소스 등 물리적 및 가상 컴퓨터의 hello 가용성과 성능을 분석 합니다. |
| ![Azure Automation](media/operations-management-suite-overview/icon-automation.png) | Automation | 수동 프로세스를 자동화하고 실제 컴퓨터와 가상 컴퓨터에 대한 구성을 적용합니다. |
| ![Azure Backup](media/operations-management-suite-overview/icon-backup.png) | Backup | 중요한 데이터를 백업하고 복원합니다. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | 사이트 복구 | 중요한 응용 프로그램에 고가용성을 제공합니다. |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)는 관리형 리소스의 데이터를 중앙 리포지토리로 수집하여 OMS에 대한 모니터링 서비스를 제공합니다.  이 데이터는 이벤트, 성능 데이터 또는 hello API 통해 제공 되는 사용자 지정 데이터에 포함 될 수 있습니다. 수집 되 면 hello 데이터는 경고, 분석 및 내보내기에 사용할 수 있습니다.  이 방법을 사용 하면 있습니다 tooconsolidate 데이터 다양 한 소스에서에서 기존 온-프레미스 환경과 Azure 서비스에서 데이터를 결합할 수 있도록 합니다.  모든 작업을 사용할 수 있는 tooall 종류의 데이터를 해당 데이터에 대해 수행한 hello 동작의 결과로 명확 하 게 hello 데이터의 hello 컬렉션을 구분 합니다.  

![Log Analytics 개요](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>데이터 수집
로그 분석 tooanalyze에 대 한 hello 저장소로 데이터를 가져올 수 있는 방법의 여러 가지가 있습니다.

- **Windows 또는 Linux 컴퓨터와 가상 컴퓨터.**  에 hello Microsoft Monitoring Agent를 설치한 [Windows](../log-analytics/log-analytics-windows-agents.md) 및 [Linux](../log-analytics/log-analytics-linux-agents.md) 컴퓨터 또는 가상 컴퓨터의 toocollect 데이터입니다.  hello 에이전트에서는 이벤트 및 성능 데이터 toocollect 정의 하는 로그 분석 구성에서 자동으로 다운로드 됩니다.  Hello Azure 포털을 사용 하 여 Azure에서 실행 중인 가상 컴퓨터에서 손쉽게 hello 에이전트를 설치할 수 있습니다.  기존 Operations Manager 환경에 있으면 hello 관리 그룹 tooLog 분석을 연결 하 고 자동으로 기존의 모든 에이전트에서 데이터 수집을 시작할 수 있습니다.
- **Azure 서비스.**  로그 분석에서 원격 분석 수집 [Azure 진단 및 Azure 모니터링](../log-analytics/log-analytics-azure-storage.md) hello 저장소로 Azure 리소스를 모니터링할 수 있도록 합니다.
- **데이터 수집기 API.**  Log Analytics에는 [모든 클라이언트의 데이터를 채우는 REST API](../log-analytics/log-analytics-data-collector-api.md)가 있습니다.  이 타사 응용 프로그램에서 toocollect 데이터를 허용 하거나 사용자 지정 관리 시나리오를 구현 합니다.  일반적인 방법은 toouse toocollect 데이터 Azure 자동화에서에서 runbook은 및 다음 데이터 수집기 API toowrite hello를 사용 하 여 그 toohello 저장소입니다.

#### <a name="reporting-and-analyzing-data"></a>데이터 보고 및 분석
로그 분석 hello 저장소에 저장 하는 강력한 쿼리 언어 tooextract 데이터를 포함 합니다.  모든 소스의 데이터가 레코드로 저장되기 때문에 사용자가 여러 소스의 데이터를 단일 쿼리로 분석할 수 있습니다.
  
또한 tooad 임시 분석, 로그 분석은 여러 방법으로 tooreport 제공 하 고 쿼리에서 데이터를에서 분석 합니다.

- **보기 및 대시보드.**  [뷰](../log-analytics/log-analytics-view-designer.md) 및 [대시보드](../log-analytics/log-analytics-dashboards.md) hello hello 포털에서 쿼리 결과 시각화 합니다.  관리 솔루션 hello 솔루션에서 hello 데이터를 분석 하는 뷰를 일반적으로 포함 됩니다.  Tooanalyze 데이터 사용자 지정 보기를 만들 수 있고 사용자 지정 사용자 포털에서 쉽게 사용할 수 있도록 수도 있습니다.
- **내보내기.**  외부 로그 분석에서 분석할 수 있도록 쿼리 hello 옵션 tooexport hello 결과 해야 합니다.  일반 내보내기를 너무 예약할 수도 있습니다[Power BI](../log-analytics/log-analytics-powerbi.md) 상당한 시각화 및 분석 기능을 제공 하는 합니다.
- **로그 검색 API.**  Log Analytics에는 [모든 클라이언트의 데이터를 수집하는 REST API](../log-analytics/log-analytics-log-search-api.md)가 있습니다.  이 hello 저장소에 수집 된 데이터 한 tooprogrammatically 작업을 허용 하거나 다른 모니터링 도구에서 액세스 합니다.

#### <a name="alerting"></a>경고
Log Analytics는 문제가 발견되면 사용자에게 [미리 경고](../log-analytics/log-analytics-alerts.md)하거나 수정 작업을 수행할 수 있습니다.  Log Analytics의 다른 분석과 마찬가지로 로그 검색을 통해 수행됩니다.  이 검색 정기적인 일정으로 실행 하 고 hello 결과 특정 조건과 일치 하는 경우 경고가 생성 됩니다.

![Log Analytics 경고](media/operations-management-suite-overview/overview-alerts.png)

또한 toocreating hello 로그 분석 저장소에는 경고 레코드 경고 수 사용 hello 동작을 수행 합니다.

- **전자 메일.**  전자 메일 보내기 tooproactively의 검색 된 문제를 알려 줍니다.
- **Runbook.**  Log Analytics의 경고는 Azure Automation에서 runbook을 시작할 수 있습니다.  이 일반적으로 tooattempt toocorrect hello 검색 문제를 수행 합니다.  hello runbook 시작 될 수 있습니다 hello에서 클라우드를 hello Azure 또는 다른 클라우드 또는 것에서 문제의 대/소문자는 물리적 컴퓨터 또는 가상 컴퓨터에는 문제에 대 한 로컬 에이전트에서 시작할 수 있었습니다.
- **웹후크.**  경고는 webhook 시작한 hello hello 로그 검색 결과에서 데이터 전달 수 있습니다.  이렇게 하면 대체 경고 시스템 등 외부 서비스와의 통합 하거나 tootake 외부 웹 사이트에 대 한 수정 동작을 시도할 수 있습니다.

### <a name="azure-automation"></a>Azure Automation
[Azure 자동화](http://azure.microsoft.com/documentation/services/automation) 프로세스 자동화 및 구성 관리 tooOMS를 제공 합니다.  수동 프로세스를 자동화 하 고 물리적 및 가상 컴퓨터에 대 한 구성을 tooenforce는 데 도움이 됩니다.  

#### <a name="process-automation"></a>프로세스 Automation
Azure Automation은 PowerShell 스크립트 또는 PowerShell 워크플로 기반의 [runbook](../automation/automation-runbook-types.md)을 사용하여 수동 프로세스를 자동화합니다.  자격 증명 및 인증에 대 한 runbook에 대 한 필요할 수 있는 암호화 toostore 정보 수 있는 연결을 및 여러 runbook 간에 공유할 수 있는 변수와 같은 runbook을 지 원하는 자산도 포함 됩니다.
Runbook은 프로세스 자동화 hello에 대 한 hello 제품군의 다른 서비스를 제공합니다.  각 hello 이후 다른 서비스에 액세스할 수 powershell 또는 REST API를 통해 만들 수 있습니다 runbook tooperform 같은 기능 로그 분석에 관리 데이터를 수집 하거나 Azure Backup을 사용 하 여 백업을 시작 합니다.

##### <a name="accessing-resources"></a>리소스 액세스
runbook은 PowerShell을 기반으로 하기 때문에 PowerShell cmdlet을 통해 액세스할 수 있는 모든 리소스를 관리할 수 있습니다.  때 있습니다 [모듈을 로드](../automation/automation-integration-modules.md) 해당 계정에 사용할 수 있는 tooall runbook 자동화 고려 됩니다. 
 
Runbook hello 클라우드에서 실행 될 때 hello 클라우드에서 액세스할 수 있는 모든 리소스를 액세스할 수 있습니다.  Azure 구독, AWS(Amazon Web Services) 같은 다른 클라우드 또는 REST API를 통해 액세스할 수 있는 서비스의 리소스를 예로 들 수 있습니다.  Runbook hello 클라우드의 모든 자격 증명으로 실행 하지 않는 있지만 자격 증명, 연결 및 액세스 하는 인증서 tooauthenticate tooresources 등의 자동화 자산을 활용할 수 있습니다.

대개 데이터 센터의 리소스는 hello 클라우드에서 실행 되는 runbook에서 액세스할 수 없습니다.  하나 이상 설치할 수 [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) 데이터 센터를 통해 toolocal 리소스에 액세스 해야 하는 toorun runbook입니다.  Runbook을 시작할 때 hello 클라우드 또는 특정 작업자에서 실행 해야 하는지도 지정할 수 있습니다.

![Azure Automation runbook](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Runbook 시작
Runbook이 다양한 관리 시나리오에 포함되도록 [다양한 방법을 통해 Runbook을 시작](../automation/automation-starting-a-runbook.md)할 수 있습니다.  

- **Azure Portal.**  다른 Azure 서비스와 마찬가지로 Azure 자동화 hello Azure 포털에서에서 관리할 수 있습니다.  또한 toostarting runbook 있습니다 수 가져오거나 직접 작성 합니다.
- **예약.**  정기적으로 runbook toostart를 예약할 수 있습니다.  이렇게 하면 tooautomatically 반복 일반 관리 프로세스 또는 데이터 수집 tooLog 분석 있습니다.
- **PowerShell 및 API.**  Runbook 및 해당 PowerShell cmdlet에서 매개 변수 정보는 데 필요한 단계를 시작 하거나 Azure 자동화 REST API hello 수 있습니다.  
- **웹후크.**  허용 하는 모든 runbook에 대 한는 webhook을 만들 수 있습니다 toobe 외부 응용 프로그램 또는 웹 사이트에서 시작 합니다.
- **Log Analytics 경고.**  로그 분석에서 경고 hello 경고에서 식별 한 runbook tooattempt toocorrect hello 문제를 자동으로 시작할 수 있습니다.

#### <a name="configuration-management"></a>구성 관리
[PowerShell 필요한 상태 구성 (DSC)](../automation/automation-dsc-overview.md) toodeploy 있으며 hello 구성 물리적 및 가상 컴퓨터를 적용 하는 Windows PowerShell의 관리 플랫폼입니다.  Azure 자동화는 DSC 구성을 관리 하 고 에이전트 tooretrieve 필요한 구성에 액세스할 수 있도록 hello 클라우드에서 끌어오기 서버를 제공 합니다.

![Azure Automation DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure Backup 및 Azure Site Recovery
Azure 백업 및 Azure 사이트 복구 toobusiness 연속성 및 재해 복구를 영향을 줍니다.  구성 파일은 각각는 tooensure 중단이 발생 했을 때 반환 toonormal 작업 시스템을 다시 온라인 상태로 복구 하는 경우 응용 프로그램 계속 사용할 수 있는 기능이 있습니다.  두 서비스 모두 toohello 복구 지점 목표 (Rpo) 및 복구 시간 목표 (Rto) 조직에 대해 정의 된 영향을 줍니다. Hello 시간을 허용 가능한 정보량을 제한 하는 hello RTO 및 RPO에는 데이터 사용할 수 없는 중단이 발생 하는 동안 hello 허용 가능 한도 정의 하는 동안 가동 중단 된 서비스 또는 응용 프로그램 사용할 수 없습니다.

#### <a name="azure-backup"></a>Azure Backup
[Azure Backup](http://azure.microsoft.com/documentation/services/backup)은 OMS에 데이터 백업 및 복원 서비스를 제공합니다.  자본 투자 없이 최소한의 운영 비용으로 응용 프로그램 데이터를 보호하고 수년 간 보관합니다.  SQL Server 및 SharePoint와 같은 추가 tooapplication 작업의 실제 및 가상 Windows 서버에서 데이터를 백업할 수 있습니다.  또한 사용할 수 있습니다 System Center Data Protection Manager (DPM) 보호 된 tooreplicate 데이터 tooAzure에서 중복성 및 장기 저장에 대 한 합니다.

Azure Backup의 보호 데이터는 특정 지리적 지역에 있는 백업 저장소에 저장됩니다. hello 데이터가 복제 내 동일한 지역 hello 하 고, 자격 증명 모음에 hello 유형에 따라 추가 복구를 위한 복제 tooanother 영역을 될 수도 있습니다.

Azure Backup에는 세 가지 기본 시나리오가 있습니다.

- **Azure Backup 에이전트가 있는 Windows 컴퓨터.** 모든 Windows 서버 또는 클라이언트에서 파일 및 폴더를 백업 직접 tooyour Azure 백업 자격 증명 모음입니다.<br><br>![Azure Backup 에이전트가 있는 Windows 컴퓨터](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center DPM(Data Protection Manager) 또는 Microsoft Azure Backup Server.** 및 SQL 및 SharePoint toolocal 저장소와 같은 추가 tooapplication 작업에서 DPM 또는 Microsoft Azure 백업 서버 toobackup 파일 및 폴더를 활용 하면 tooyour Azure 백업 자격 증명 모음을 복제 됩니다. Hyper-V 또는 VMware에서 Windows 및 Linux 가상 컴퓨터를 지원합니다.<br><br>![System Center DPM(Data Protection Manager) 또는 Microsoft Azure Backup Server.](media/operations-management-suite-overview/overview-backup-02.png)
- **Azure 가상 컴퓨터 확장.** 백업 Windows 또는 Linux 가상 컴퓨터에서 Azure tooyour Azure 백업 자격 증명 모음입니다.<br><br>![Azure 가상 컴퓨터 확장](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) 온-프레미스 가상의 복제 및 물리적 컴퓨터 tooAzure 또는 tooa 보조 사이트를 오케스트레이션 하 여 비즈니스 연속성을 제공 합니다. 기본 사이트를 사용할 수 없는 경우 장애 조치 toohello 보조 위치는 사용자가 계속 작업할 수 있고 시스템 tooworking 순서를 반환 하는 경우 실패 합니다. 

Azure Site Recovery는 서버 및 응용 프로그램에 고가용성을 제공합니다.  복제, 장애 조치 및 온-프레미스 Hyper-v 가상 컴퓨터, VMware 가상 컴퓨터 및 물리적 Windows/Linux 서버 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략에 기여 합니다. 컴퓨터 tooa 보조 데이터 센터 하거나 tooAzure를 복제 하 여 데이터 센터를 확장할 수 있습니다. Site Recovery는 또한 워크로드에 대해 간단한 장애 조치(Failover) 및 복구를 제공합니다. SQL Server AlwaysOn과 같은 재해 복구 메커니즘과 통합되며 여러 컴퓨터에서 계층화되는 워크로드의 간단한 장애 조치(Faiover)에 대한 복구 계획을 제공합니다.

Azure Site Recovery에는 세 가지 기본 복제 시나리오가 있습니다.

- **Hyper-V 가상 컴퓨터 복제.**  VMM 클라우드에서 Hyper-v 가상 컴퓨터를 관리 하는 경우 보조 데이터 센터 또는 tooAzure 저장소 tooa 복제할 수 있습니다. 복제 tooAzure 보안 인터넷 연결입니다. 복제 tooa 보조 데이터 센터 hello LAN 끝났습니다.  Hyper-v 가상 컴퓨터에 VMM에서 관리 되지 않을 경우 tooAzure 저장에만 복제할 수 있습니다. 복제 tooAzure 보안 인터넷 연결입니다.<br><br>![Hyper-V 가상 컴퓨터 복제](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **VMware 가상 컴퓨터 복제.**  VMware 가상 컴퓨터 tooa 실행 보조 데이터 센터 VMware 또는 tooAzure 저장소를 복제할 수 있습니다. 사이트 간 VPN 이나 Azure express 경로 또는 보안 인터넷 연결을 통해 복제 tooAzure 발생할 수 있습니다. 복제 tooa 보조 데이터 센터 hello InMage Scout 데이터 채널을 통해 발생 합니다.<br><br>![VMware 가상 컴퓨터 복제](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **실제 Windows 또는 Linux 서버 복제.**  물리적 서버 tooa 보조 데이터 센터 또는 tooAzure 저장소를 복제할 수 있습니다. 사이트 간 VPN 이나 Azure express 경로 또는 보안 인터넷 연결을 통해 복제 tooAzure 발생할 수 있습니다. 복제 tooa 보조 데이터 센터 hello InMage Scout 데이터 채널을 통해 발생 합니다. Azure 사이트 복구에 몇 가지 통계를 표시 하는 OMS 솔루션이 있지만 임의 작업을 위해 hello Azure 포털을 사용 해야 합니다.<br><br>![물리적 Windows 또는 Linux 서버 복제](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Site Recovery는 특정 지역의 Azure 지역에 위치한 저장소에 메타데이터를 저장합니다. Hello Site Recovery 서비스에서 저장 되는 복제 된 데이터가 있습니다.

## <a name="management-solutions"></a>관리 솔루션
[관리 솔루션](operations-management-suite-solutions.md)은 하나 이상의 OMS 서비스를 활용하여 특정 관리 시나리오를 구현하는 미리 패키지된 논리 집합입니다.  다른 솔루션은 oms에서 투자의 tooyour tooincrease hello 가치를 Azure 구독을 쉽게 추가할 수는 파트너 및 Microsoft에서 사용할 수 있습니다.  파트너 응용 프로그램 및 서비스 사용자 고유의 솔루션 toosupport를 만들 수 있으며를 제공 하 고 hello Azure 마켓플레이스 또는 퀵 스타트 템플릿을 통해 toousers 키를 누릅니다.

여러 서비스 tooprovide 추가 기능을 사용 하는 솔루션의 좋은 예로 hello [업데이트 관리 솔루션](oms-solution-update-management.md)합니다.  이 솔루션에 각 에이전트 필수 업데이트에 대 한 있는 Windows 및 Linux toocollect 정보에 대 한 hello 로그 분석 에이전트를 사용합니다.  이 데이터 toohello 로그 분석 저장소에 포함 된 대시보드를 분석할 수를 기록 합니다.  배포를 만들 때 Azure 자동화의 runbook은 필요한 사용 되는 tooinstall 업데이트.  Hello 포털에서이 전체 프로세스를 관리 하 고 hello 기본 세부 정보에 대 한 tooworry 필요 하지 않습니다.

![해결 방법](media/operations-management-suite-overview/overview-solution.png)

대부분의 솔루션 hello 함수를 다음 중 하나 이상을 수행할 수 있습니다.

- 추가 정보를 수집합니다.  Log Analytics는 클라이언트와 서비스에서 이벤트 및 성능 데이터를 포함한 다양한 데이터를 수집합니다.  관리 솔루션은 종종 Azure Automation runbook을 사용하여 다른 데이터 소스에서 제공되지 않는 추가 정보를 수집할 수 있습니다.
- 수집된 정보를 추가로 분석합니다.  관리 솔루션에는 데이터 분석 및 시각화를 제공하는 대시보드와 보기가 포함되어 있습니다.  데이터를 자세히 toodrill hello를 사용 하면 이러한 링크 백 toopredefined 로그 검색 합니다.  이미 수집 된 hello 리포지토리로 예를 들어 위협이 나타내는 패턴에 대 한 보안 이벤트를 검색 하는 데이터에 분석을 수행할 수도 있습니다.
- 기능 추가.  Microsoft에서 제공 하는 일부 솔루션 hello 핵심 서비스 tooprovide 추가 기능의 hello 기능에 따라 작성 될 수 있습니다.  예를 들어 서비스 맵 자체 콘솔 toodiscover 제공 하 고 서버와 프로세스 종속성 실시간으로 매핑합니다.
솔루션은 정기적으로 추가 하 고 있는 tooOMS Microsoft와 파트너 toocontinuously 있도록 투자의 hello 값을 늘리십시오.  있습니다 수 찾아보기 hello 솔루션 카탈로그를 통해 Microsoft 솔루션 hello OMS 포털에서 또는 찾아보기 및 설치 hello Azure 마켓플레이스를 통해 Microsoft와 파트너 솔루션 hello Azure 포털의.  

![솔루션 갤러리](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>다음 단계
* [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)에 대해 알아보기
* [Azure Automation](../automation/automation-intro.md)에 대해 알아보기
* [Azure Backup](http://azure.microsoft.com/documentation/services/backup)에 대해 알아보기
* [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)에 대해 알아보기
* Hello 검색 [사용할 수 있는 솔루션이](../log-analytics/log-analytics-add-solutions.md) hello 다른 OMS 기능에서입니다. 

