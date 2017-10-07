---
title: "로깅 및 감사 aaaAzure | Microsoft Docs"
description: "응용 프로그램에 대 한 깊은 통찰력 제공 toogain 로깅 데이터를 사용 하는 방법에 대해 알아봅니다."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Azure 로깅 및 감사
## <a name="introduction"></a>소개
### <a name="overview"></a>개요
tooassist 현재 및 향후 Azure 고객 이해 하 고 사용 하 여 다양 한 보안 관련 기능에서 사용할 수 있는 hello 및 hello Azure 플랫폼을 둘러싼 Microsoft는 개발 하는 일련의 백서, 보안 개요, 모범 사례 및 검사 목록입니다. hello 항목 폭과 깊이 기준으로 다양 하 고 정기적으로 업데이트 됩니다. 이 문서는 hello 추상 섹션 다음에 요약 된 것 처럼 해당 시리즈의 일부는입니다.
### <a name="azure-platform"></a>Azure 플랫폼
Azure는 유연한 개방형 클라우드 서비스 플랫폼으로 hello 광범위 한 프로그래밍 언어, 프레임 워크, 도구, 데이터베이스 및 장치 운영 체제를 선택할 수입니다.

예를 들어 다음을 수행할 수 있습니다.
-   Docker 통합으로 Linux 컨테이너를 실행합니다.

-   JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드합니다.

-   iOS, Android 및 Windows 장치용 백 엔드를 빌드합니다.

Azure 공용 클라우드 서비스는 hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다.

사용 하는 조직의 능력 tooprotect 응용 프로그램 및 사용 하 여 데이터 서비스 및 hello 컨트롤 hello를 작성 하거나 IT 자산 클라우드 공급자를 마이그레이션할 때 클라우드 기반 자산의 toomanage hello 보안을 제공 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고 비즈니스는 고유한 보안 요구를 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 다양 한 구성 가능한 보안 옵션 및 hello 기능 toocontrol와 보안 toomeet hello 하면 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다. 이 문서는 이러한 요구 사항을 충족하는 데 도움이 됩니다.

### <a name="abstract"></a>요약
보안 관련 이벤트의 감사와 로깅 및 관련 경고는 효과적인 데이터 보호 전략의 중요한 구성 요소입니다. 보안 로그 및 보고서의 의심 스러운 활동 및 내부 공격 뿐만 아니라 hello 네트워크의 외부 침투 시도한 또는 성공 여부를 나타낼 수 있는 패턴을 검색 하는 도움말 전자는 기록을 제공 합니다. 감사 toomonitor 사용자 작업, 문서 규정 준수를 사용 하 여, 법정 분석 등을 수행할 수 있습니다. 경고는 보안 이벤트가 발생할 때 즉각적인 알림을 제공합니다.

Microsoft Azure 서비스 및 제품 구성 가능한 보안 감사 제공 하 고 위반을 방지 로깅 옵션 toohelp에서 보안 정책 및 메커니즘의 차이 식별 하 고 해당 간격이 toohelp를 처리 합니다. 일부 Microsoft 서비스 제공 (및 경우에 따라 모든)의 다음 옵션 hello: 중앙 집중식으로 모니터링, 로깅 및 분석 시스템 tooprovide 연속 가시성; 시기 적절 한 경고입니다. 및 보고서 toohelp hello 많은 양의 장치 및 서비스에 의해 생성 된 정보를 관리 합니다.

Microsoft Azure 로그 데이터 분석을 위해 인시던트 및 이벤트 관리 SIEM () 시스템 내보낸된 tooSecurity 수 있으며 다른 공급 업체 감사 솔루션과 통합 되어 있습니다.

이 백서에서는 Azure에서 호스팅되는 서비스의 보안 로그 생성, 수집 및 분석을 소개하며, Azure 배포에 대한 보안을 깊이 이해할 수 있습니다. 이 백서의 hello 범위 제한 tooapplications 되며 작성 되 고 Azure에서 배포 된 서비스입니다.

> [!Note]
> 여기에 포함된 특정 권장 사항으로 인해 데이터, 네트워크 또는 계산 리소스 사용량이 증가하고, 라이선스 또는 구독 비용이 증가할 수 있습니다.

## <a name="types-of-logs-in-azure"></a>Azure의 로그 유형
클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다. 로그는 정상 상태에서 실행 되 고 응용 프로그램 없이 계속 데이터 tooensure 제공 합니다. 또한 있습니다 toostave 잠재적 문제를 해제 하거나 문제를 해결 하십시오. 지난 수 있습니다. 또한 응용 프로그램에 대 한 깊은 통찰력 제공 toogain 로깅 데이터를 사용할 수 있습니다. 이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다.

Azure에서는 모든 Azure 서비스에 대해 광범위한 로깅을 생성합니다. 이러한 로그는 다음과 같은 유형으로 분류됩니다.
-   **컨트롤/관리 로그** Azure 리소스 관리자 만들기, 업데이트 및 삭제 작업 hello에 대 한 가시성을 제공 합니다. [Azure 활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)가 이러한 로그 유형의 예입니다.

-   **데이터 로그를 평면** hello Azure 리소스 사용의 일부로 발생 하는 hello 이벤트에 대 한 가시성을 제공 합니다. 이 유형의 로그의 예로 Windows 이벤트 시스템, 보안, hello 및 응용 프로그램 로그에 가상 컴퓨터와 hello [진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) Azure 모니터를 통해 구성


-   **처리된 이벤트** - 사용자를 위해 처리된 분석 이벤트/경고에 대한 정보를 제공합니다. [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)에서 구독을 처리 및 분석하고 간결한 보안 경고를 제공하는 [Azure Security Center 경고](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)가 이러한 로그 유형의 예입니다.

hello 다음 표에서 목록 가장 중요 한 유형의 로그를 Azure에서 사용할 수 있습니다.

| 로그 범주 | 로그 형식 | 사용 | 통합 |
| ------------ | -------- | ------ | ----------- |
|[활동 로그](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Azure Resource Manager 리소스에 대한 제어 평면 이벤트| 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 합니다.|   Rest API 및 [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Azure 진단 로그](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|구독에서 Azure 리소스 관리자 리소스의 hello 작업에 대 한 데이터를 자주| 리소스 자체에서 수행한 작업에 대한 정보를 제공합니다.| Azure Monitor, [스트림](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[AAD 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|로그 및 보고서|사용자 로그인 활동 및 사용자와 그룹 관리에 대한 시스템 활동 정보|[그래프 API](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[가상 컴퓨터 및 Cloud Services](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Windows 이벤트 로그 및 Linux Syslog|  시스템 데이터 및 로깅 데이터 hello 가상 컴퓨터를 캡처하고 사용자가 선택한 저장소 계정에 해당 데이터를 전송 합니다.| Azure 모니터에서 [MAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics)(Microsoft Azure 진단 저장소)와 Linux를 사용하는 Windows|
|[저장소 분석](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|저장소 로깅을 수행하고, 저장소 계정에 대한 메트릭 데이터를 제공합니다.|추적 요청에 대한 정보를 제공하고, 사용 추세를 분석하며, 저장소 계정으로 문제를 진단합니다.|  REST API 또는 hello [클라이언트 라이브러리](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[NSG(네트워크 보안 그룹) 흐름 로그](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|JSON 형식이며, 규칙에 따라 아웃바운드 및 인바운드 흐름을 보여 줍니다.|네트워크 보안 그룹을 통한 수신 및 송신 IP 트래픽에 대한 정보를 보여 줍니다.|[Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application insight](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|로그, 예외 및 사용자 지정 진단|  여러 플랫폼의 웹 개발자를 위한 APM(Application Performance Management) 서비스| REST API, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|데이터 처리/보안 경고| Azure Security Center 경고, OMS 경고| 보안 정보 및 경고입니다.|   REST API, JSON|

### <a name="activity-log"></a>활동 로그
hello [Azure 활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 합니다. hello 활동 로그는 이전에 알려졌습니다 "감사 로그" 또는 "작업 로그"로 보고 하는 이후 [제어 평면 이벤트](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) 구독에 대 한 합니다. Hello 활동 로그를 사용 하 여 hello 확인할 수 있습니다 "부분, who, 시기 및" 모든 쓰기 작업 (PUT, POST, DELETE) hello 구독의 리소스에에서 대해 수행에 대 한 합니다. Hello 작업 및 기타 관련 속성의 hello 상태를 이해할 수 있습니다. hello 활동 로그 읽기 (GET) 작업을 포함 하지 않습니다.

여기 PUT, POST, DELETE tooall hello 쓰기 작업 hello 리소스에 포함 된 활동 로그를 참조 합니다. Hello 활동 로그 toofind 문제를 해결할 때 오류 또는 toomonitor을 사용할 수는 예를 들어 조직에서 사용자가 리소스를 수정 하는 방법입니다.

![활동 로그](./media/azure-log-audit/azure-log-audit-fig1.png)


Hello Azure 포털을 사용 하 여 활동 로그에서 이벤트를 검색할 수 있습니다 [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), PowerShell cmdlet 및 [Azure 모니터 REST API](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough)합니다. 활동 로그에는 19일간의 데이터 보존 기간이 있습니다.

통합 시나리오
-   [활동 로그 이벤트를 트리거 해제하는 전자 메일 또는 웹후크 경고를 만듭니다.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [이벤트 허브 tooan 스트림](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) 수집 제 3 자 서비스 또는 PowerBI 같은 사용자 지정 분석 솔루션에 대 한 합니다.

-   PowerBI hello를 사용 하 여 분석할 [PowerBI 콘텐츠 팩.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [보관 또는 수동 검사 하기 위해 tooa 저장소 계정을 저장 합니다.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Hello 보존 기간 (일) 로그 프로필을 사용 하 여 지정할 수 있습니다.

-   쿼리하고 hello Azure 포털에서에서 볼 합니다.

-   PowerShell Cmdlet, CLI 또는 REST API를 통해 쿼리합니다.

-   너무 hello 로그 프로필을 사용 하 여 활동 로그 내보내기[로그 분석](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)합니다.

저장소 계정을 사용할 수 있습니다 또는 [이벤트 허브 네임 스페이스](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) 에 없는 하나의 내보내는 로그 hello으로 동일한 구독 hello 합니다. hello 사용자 hello 설정을 구성가 적절 한 hello 있어야 [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) tooboth 구독에 액세스
### <a name="azure-diagnostic-logs"></a>Azure 진단 로그
Azure 진단 로그는 해당 리소스의 hello 작업에 대 한 데이터를 다양 하 고 자주 제공 하는 리소스에서 내보내집니다. 이러한 로그의 hello 콘텐츠 리소스 유형에 따라 달라 집니다 (예를 들어 [Windows 이벤트 시스템 로그](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)Vm에 대 한 진단 로그의 범주는 및 [blob, 테이블 및 큐 로그](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) 종류의 진단 로그 저장소 계정의 경우)와 다른 지 hello 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 하는 작업 로그입니다.

![Azure 진단 로그](./media/azure-log-audit/azure-log-audit-fig2.png)

Azure 진단 로그는 PowerShell, CLI(명령줄 인터페이스) 및 REST API를 사용하여 Azure Portal과 같은 여러 가지 구성 옵션을 제공합니다.

**통합 시나리오**
-   Tooa 저장해 [저장소 계정](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) 감사 또는 수동 검사 합니다. Hello 보존 기간 (일) hello 진단 설정을 사용 하 여 지정할 수 있습니다.

-   [TooEvent 허브 파일을 스트리밍할](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) 수집 제 3 자 서비스 또는 같은 사용자 지정 분석 솔루션에 대 한 [PowerBI 합니다.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   [OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)를 사용하여 분석합니다.

**지원되는 서비스, 진단 로그용 스키마 및 지원되는 리소스 종류별 로그 범주**


| 부여 | 스키마 및 문서 | 리소스 종류 | Category |
| ------- | ------------- | ------------- | -------- |
|부하 분산 장치| [Azure 부하 분산 장치에 대한 로그 분석(미리보기)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|네트워크 보안 그룹|[NSG(네트워크 보안 그룹)에 대한 로그 분석](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|응용 프로그램 게이트웨이|[응용 프로그램 게이트웨이에 대한 진단 로깅](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|키 자격 증명 모음|[Azure 키 자격 증명 모음 로깅](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Azure 검색|[검색 트래픽 분석 설정 및 사용](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|데이터 레이크 저장소|[Azure Data Lake Store에 대한 진단 로그에 액세스](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|감사|
|데이터 레이크 분석|[Azure Data Lake Analytics에 대한 진단 로그에 액세스](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|감사|
|||Microsoft.DataLakeAnalytics/accounts|요청|
|||Microsoft.DataLakeStore/accounts|요청|
|Logic Apps|[Logic Apps B2B 사용자 지정 추적 스키마](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure 배치|[Azure 배치 진단 로깅](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Azure 자동화|[Azure Automation에 대한 Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Event Hubs|[Azure Event Hubs 진단 로그](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|스트림 분석|[작업 진단 로그](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|실행|
|||Microsoft.StreamAnalytics/streamingjobs|작성|
|서비스 버스|[Azure Service Bus 진단 로그](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Azure Active Directory 보고
Azure AD(Azure Active Directory)에는 디렉터리에 대한 보안, 활동 및 감사 보고서가 포함되어 있습니다. hello [Azure Active Directory 감사 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) 고객이 privileged tooidentify 발생 한 작업을 Azure Active Directory에 편리 합니다. 특권이 필요한 작업 (예를 들어 역할 만들기 또는 암호 재설정) 상승 변경 내용을 포함 toodirectory 구성 변경 (예: 변경 내용 toodomain 페더레이션 설정) 또는 정책 구성 (예: 암호 정책)을 변경 합니다.

hello 보고서 hello 변경 및 hello 날짜 및 시간 (UTC)에 영향을 받는 hello 대상 리소스 hello 동작을 수행한 hello 행위자 hello 이벤트 이름에 대 한 hello 감사 레코드를 제공 합니다. 고객은 hello 통해 자신의 Azure Active Directory에 대 한 감사 이벤트의 수 tooretrieve hello 목록을 [Azure 포털](https://portal.azure.com/)에 설명 된 대로 [감사 로그를 보려면](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)합니다. 포함 된 hello 보고서 목록은 다음과 같습니다.

| 보안 보고서 | 작업 보고서 | 감사 보고서 |
| :--------------- | :--------------- | :------------ |
|알 수 없는 원본에서 로그인| 응용 프로그램 사용: 요약| 디렉터리 감사 보고서|
|여러 번의 실패 후 로그인|  응용 프로그램 사용: 세부||
|여러 지역에서의 로그인|    응용 프로그램 대시보드||
|의심스러운 작업이 있는 IP 주소에서 로그인|   계정 프로비전 오류||
|비정상적인 로그인 작업|    개별 사용자 장치||
|감염 가능성이 있는 장치에서 로그인|   개별 사용자 활동||
|비정상적인 로그인 활동을 포함하는 사용자| 그룹 활동 보고서||
||암호 재설정 등록 활동 보고서||
||암호 재설정 활동|||

이러한 보고서의 hello 데이터 SIEM 시스템, 감사, 비즈니스 인텔리전스 도구 등의 유용한 tooyour 응용 프로그램을 수 있습니다. hello Azure AD reporting Api는 REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다. 이러한 [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started)는 다양한 프로그래밍 언어와 도구에서 호출할 수 있습니다.

Hello Azure AD 감사 보고서의에서 이벤트는 180 일 동안 유지 됩니다.

> [!Note]
> 보고서 보존에 대한 자세한 내용은 [Azure Active Directory 보고서 보존 정책](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)을 참조하세요.

더 긴 보존 기간에 대 한 감사 이벤트를 저장 관심이 있는 고객, hello API 보고 될 수 있습니다 사용할 tooregularly 끌어오기 [감사 이벤트](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) 별도 데이터 저장소로 합니다.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Azure 진단을 사용하는 가상 컴퓨터 로그
[Azure 진단](https://docs.microsoft.com/azure/azure-diagnostics) hello 배포 된 응용 프로그램에서 진단 데이터 수집을 사용 하면 Azure 내에서 hello 기능입니다. 서로 다른 여러 원본의 hello 진단 확장을 사용할 수 있습니다. [Azure 클라우드 서비스 웹 및 작업자 역할](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)이 현재 지원되고 있습니다.

![Azure 진단을 사용하는 가상 컴퓨터 로그](./media/azure-log-audit/azure-log-audit-fig3.png)

Microsoft Windows를 실행하는 [Azure Virtual Machines](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) 및 [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)입니다.

다음을 사용하여 가상 컴퓨터에서 Azure 진단을 사용하도록 설정할 수 있습니다.

-   Visual Studio를 사용 하 여 참조 [tootrace Visual Studio를 사용 하 여 Azure 가상 컴퓨터](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Azure Virtual Machine에서 원격으로 Azure 진단 설정](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Azure 가상 컴퓨터에서 PowerShell tooset 한 진단 사용](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Azure Resource Manager 템플릿을 사용하여 모니터링 및 진단 기능으로 Windows 가상 컴퓨터 만들기](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>저장소 분석
[ 분석](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)은 로깅을 수행하며 저장소 계정에 대한 메트릭 데이터를 제공합니다. 이 데이터 tootrace 요청을 사용 하 고, 사용 추세를 분석 하 고, 저장소 계정 문제를 진단할 수 있습니다. 저장소 분석 로깅을 ´ ü ± hello [Blob, 큐 및 테이블 서비스입니다.](https://docs.microsoft.com/azure/storage/storage-introduction) Storage Analytics는 성공 및 실패 한 요청 tooa 저장소 서비스에 대 한 세부 정보를 기록 합니다.

이 정보는 개별 요청을 사용 하는 toomonitor 및 저장소 서비스와 toodiagnose 문제 수 있습니다. 요청은 최상의 노력을 기준으로 기록됩니다. Hello 서비스 끝점에 대 한 요청의 경우에 로그 항목이 생성 됩니다. 예를 들어 저장소 계정은 Blob 끝점에는 작업은 있지만 하지의 테이블 또는 큐 끝점에만 로그와 관련 된 경우 Blob 서비스 toohello가 만들어집니다.

toouse Storage Analytics를 사용 하도록 설정 해야 개별적으로 각 서비스에 대해 원하는 toomonitor 합니다. Hello에서 설정할 수 [Azure 포털](https://portal.azure.com/); 자세한 내용은 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링 합니다.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) Hello REST API를 통해 프로그래밍 방식으로 Storage Analytics 하거나 hello 클라이언트 라이브러리를 사용할 수도 있습니다. 각 서비스에 대해 개별적으로 hello Set Service Properties 작업 tooenable Storage Analytics를 사용 합니다.

hello 집계 된 데이터 및 저장 된 잘 알려진 blob (로깅용)에 잘 알려진 테이블 (통계용), hello Blob 서비스 및 테이블 서비스 Api 사용 하 여 액세스할 수 있는 합니다.

Storage Analytics에서는 저장소 계정의 총 한도와 hello와 독립적인 저장 된 데이터 양을 hello 20 TB 제한 됩니다. 모든 로그는 $logs라는 컨테이너의 [블록 Blob](https://docs.microsoft.com/azure/storage/storage-analytics)에 저장되며, 저장소 계정에 대해 저장소 분석을 사용하도록 설정하면 자동으로 만들어집니다.

> [!Note]
> 청구 및 데이터 보존 정책에 대한 자세한 내용은 [저장소 분석 및 청구](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)를 참조하세요.
>
> [!Note]
> 저장소 계정 제한에 대한 자세한 내용은 [Azure Storage 확장성 및 성능 목표](https://docs.microsoft.com/azure/storage/storage-scalability-targets)를 참조하세요.

다음 인증 및 익명 요청 유형의으로 hello 기록 됩니다.



| 인증됨  | 익명|
| :------------- | :-------------|
| 성공한 요청 | 성공한 요청 |
|실패한 요청(시간 제한, 제한, 네트워크, 권한 부여 및 기타 오류) | SAS(공유 액세스 서명)를 사용하는 요청(실패한 요청 및 성공한 요청 포함) |
| SAS(공유 액세스 서명)를 사용하는 요청(실패한 요청 및 성공한 요청 포함) |클라이언트와 서버 모두에 대한 시간 제한 오류 |
|   요청 tooanalytics 데이터 |    오류 코드가 304(수정되지 않음)인 실패한 GET 요청 |
| 로그 만들기/삭제 등 저장소 분석 자체에서 수행한 요청은 기록되지 않습니다. Hello 기록 데이터의 전체 목록은 hello에 설명 되어 [저장소 분석에서 기록한 작업 및 상태 메시지](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) 및 [저장소 분석 로그 형식](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) 항목입니다. | 기타 모든 실패한 익명 요청은 기록되지 않습니다. Hello 기록 데이터의 전체 목록은 hello에 설명 되어 [저장소 분석에서 기록한 작업 및 상태 메시지](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) 및 [저장소 분석 로그 형식](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format)합니다. |

### <a name="azure-networking-logs"></a>Azure 네트워킹 로그
Azure의 네트워킹 로깅 및 모니터링은 포괄적이며 다음 두 가지 범주를 포함합니다.

-   [네트워크 감시자](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -네트워크 감시자의 hello 기능과 함께 시나리오 기반 네트워크 모니터링이 제공 됩니다. 이 서비스에는 패킷 캡처, 다음 홉, IP 흐름 확인, 보안 그룹 보기, NSG 흐름 로그가 포함되어 있습니다. 수준 모니터링 시나리오는 전체적인 tooend 뷰 대비 tooindividual 네트워크 리소스 모니터링의 네트워크 리소스를 제공합니다.

-   [리소스 모니터링](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) - 리소스 수준 모니터링은 진단 로그, 메트릭, 문제 해결 및 리소스 상태의 네 가지 기능으로 구성됩니다. 이러한 모든 기능은 hello 네트워크 리소스 수준에서 빌드됩니다.

![Azure 네트워킹 로그](./media/azure-log-audit/azure-log-audit-fig4.png)

네트워크 감시자는 toomonitor 있습니다 수 있도록 하는 지역 서비스 및 네트워크 시나리오의 수준에서 및 Azure에서 상태를 진단 합니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.

**NSG 흐름 로깅** -네트워크 보안 그룹에 대 한 흐름 로그 허용 되거나 hello hello 그룹 보안 규칙에 의해 거부 된 toocapture 로그 관련된 tootraffic를 사용 합니다. 이러한 흐름 로그 JSON 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.

### <a name="network-security-group-flow-logging"></a>네트워크 보안 그룹 흐름 로깅

[네트워크 보안 그룹 흐름 로그](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다. 이러한 흐름 로그 JSON 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.

표시 되지 흐름 대상 네트워크 보안 그룹 로그, 동안 hello 동일 hello로 다른 로그입니다. 흐름 로그는 저장소 계정에만 저장됩니다.

동일한 hello 다른 로그에 표시 된 대로 보존 정책을 tooflow 로그를 적용 합니다. 로그에는 1 한 일에서 설정할 수 있는 보존 정책을 포함 합니다. 보존 정책이 설정 되어 있지 않으면 hello 로그 영원히 유지 됩니다.

**진단 로그**

정기적이 고 비 정기적인 이벤트는 네트워크 리소스에 의해 생성 및 tooan 이벤트 허브 또는 로그 분석을 전송 하는 저장소 계정에 기록 됩니다. 이러한 로그는 리소스의 hello 상태에 대 한 정보를 제공합니다. Power BI 및 Log Analytics와 같은 도구에서 볼 수 있습니다. tooview 진단 로그를 방문 하는 방법을 toolearn [로그 분석 합니다.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![진단 로그](./media/azure-log-audit/azure-log-audit-fig5.png)

진단 로그는 [부하 분산 장치](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), 경로 및 [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)에서 사용할 수 있습니다.

Network Watcher는 진단 로그 보기를 제공합니다. 이 보기에는 진단 로깅을 지원하는 모든 네트워킹 리소스가 포함됩니다. 이 보기에서 네트워킹 리소스를 빠르고 편리하게 사용하거나 사용하지 않도록 설정할 수 있습니다.


네트워크 감시자에는 추가 toopreceding 로깅 기능에 기능을 수행 하는 hello 현재에 있습니다.
- [토폴로지](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -다양 한 상호 연결 및 연결 된 리소스 그룹에에서 네트워크 리소스 간에 네트워크 개요 표시 된 hello를 제공 합니다.

- [변수 패킷 캡처](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) - 가상 컴퓨터의 내부 및 외부 패킷 데이터를 캡처합니다. Blob 저장소에 또는 로컬 디스크에.cap 형식 hello versatility.hello 패킷 데이터를 저장할 수 있습니다 시간 및 크기가 제한 제공 고급 필터링 옵션 및 수 tooset 예 세밀 하 게 제어 합니다.

-   [IP 흐름 확인](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) - 흐름 정보의 5개 튜플 패킷 매개 변수(대상 IP, 원본 IP, 대상 포트, 원본 포트 및 프로토콜)에 따라 패킷이 허용되거나 거부되는지 여부를 확인합니다. Hello 패킷 보안 그룹에 의해 거부 되 면 hello 규칙과 hello 패킷 거부 그룹 반환 됩니다.

-   [다음 홉](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -hello toodiagnose 잘못 구성 된 모든 사용자 정의 경로 사용 하면 Azure 네트워크 패브릭에서 라우팅되는 패킷의 hello 다음 홉을 결정 합니다.

-   [보안 그룹 보기](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -VM에 적용 되는 hello 효과적이 고 적용 된 보안 규칙을 가져옵니다.

-   [가상 네트워크 게이트웨이 및 연결 문제 해결](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -hello 기능 tootroubleshoot 제공 가상 네트워크 게이트웨이 및 연결 합니다.

-   [구독 제한 네트워크](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -제한에 대해 tooview 네트워크 리소스 사용을 활성화 합니다.

### <a name="application-insight"></a>Application Insight

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview)는 여러 플랫폼의 웹 개발자를 위한 확장성 있는 APM(Application Performance Management) 서비스입니다. Toomonitor를 사용 하 여 라이브 웹 응용 프로그램입니다. 성능 이상을 자동으로 검색합니다. Toounderstand 응용 프로그램과 함께 실제로 사용자가 수행 하 고 문제를 진단 하는 강력한 분석 도구 toohelp을 포함 됩니다.

 기능은 toohelp 성능과 유용성 지속적으로 향상 됩니다.

 앱에 대 한 작동.NET, Node.js 및 J2EE 포함 하는 플랫폼은 다양 한 온-프레미스 호스팅 또는 hello 클라우드에 있습니다. DevOps 프로세스와 통합 하 고 연결 포인트 toovarious 개발 도구가 합니다.

![Application Insight](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights는 hello 개발 팀에서 앱이 수행 되는 방법 및 사용 되는 방식을 이해 toohelp 목표로 합니다. 다음 사항을 모니터링합니다.

-   **요청 속도, 응답 시간 및 실패율** - 하루 중 어느 시간에 어떤 페이지를 가장 많이 방문하는지, 사용자가 어디에 있는지 확인합니다. 어떤 페이지가 가장 성능이 우수한지 확인합니다. 요청이 더 있는데 응답 시간과 실패율이 높아지면 아마도 리소스 문제가 있는 것입니다.

-   **종속성 비율, 응답 시간 및 실패율** - 외부 서비스 때문에 속도가 느려지는지 확인합니다.

-   **예외** -hello 집계 통계를 분석 하거나 특정 인스턴스를 선택 하 고 hello 스택 추적 및 관련된 요청으로 드릴 합니다. 서버 및 브라우저 예외가 전부 보고됩니다.

-   **페이지 보기 및 로드 성능** - 사용자의 브라우저에서 보고합니다.

-   웹 페이지의 **AJAX 호출** - 속도, 응답 시간 및 실패율.

-   **사용자 및 세션 수**.

-   Windows 또는 Linux 서버 컴퓨터의 **성능 카운터** - CPU, 메모리, 네트워크 사용량 등.

-   Docker 또는 Azure의 **호스트 진단**.

-   앱의 **진단 추적 로그** - 추적 이벤트를 요청과 상호 연결하는 데 사용됩니다.

-   **사용자 지정 이벤트 및 메트릭을** 는 사용자가 직접 작성 hello 클라이언트 또는 서버 코드에서 tootrack 비즈니스 이벤트 항목 판매 또는 획득 게임 등입니다.

**통합 시나리오 및 설명 목록:**

| 통합 시나리오 | 설명 |
| --------------------- | :---------- |
|[응용 프로그램 맵](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|주요 메트릭 및 경고와 함께 응용 프로그램의 hello 구성 요소입니다.||
|[인스턴스 데이터에 대한 진단 검색](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| 요청, 예외, 종속성 호출, 로그 추적 및 페이지 보기와 같은 이벤트를 검색하고 필터링할 수 있습니다.||
|[집계된 데이터에 대한 메트릭 탐색기](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|요청, 오류 및 예외의 비율과 응답 시간, 페이지 로드 시간과 같은 집계된 데이터를 탐색, 필터링 및 분할할 수 있습니다.||
|[대시보드](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|여러 리소스의 데이터를 매시업한 후 다른 사용자와 공유할 수 있습니다. 다중 구성 요소 응용 프로그램 및 hello 팀 대화방에 연속 표시에 유용 합니다.||
|[라이브 메트릭 스트림](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|새 빌드를 배포 하면 이러한 거의 실시간 성능 지표 toomake 있는지 예상 대로 작동 하는 것을 시청 합니다.||
|[분석](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|이 강력한 쿼리 언어를 사용하여 앱의 성능 및 사용 현황에 대한 까다로운 질문에 답변할 수 있습니다.||
|[자동 및 수동 경고](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|자동 경고 hello 일반 패턴 외부 대상이 있는 경우 원격 분석 및 트리거 tooyour 응용 프로그램의 일반 패턴을 활용 합니다. 특정 수준의 사용자 지정 또는 표준 메트릭에 대해 경고를 설정할 수도 있습니다.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Hello 코드의 성능 데이터를 참조 하십시오. 스택 추적에서 toocode를 이동 합니다.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|사용 현황 메트릭을 다른 비즈니스 인텔리전스와 통합합니다.||
|[REST API](https://dev.applicationinsights.io/)|메트릭 및 원시 데이터를 통해 코드 toorun 쿼리를 작성 합니다.||
|[연속 내보내기](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|대량 도착할 때 원시 데이터 toostorage 내보냅니다.||

### <a name="azure-security-center-alerts"></a>Azure Security Center 경고
[Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro) 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 방화벽 및 endpoint protection 솔루션과 toodetect 실제 위협 같은 연결 된 파트너 솔루션에서 로그 데이터를 통합 및 줄이기 거짓 긍정입니다. Hello와 함께 보안 센터에서 우선 순위가 지정 된 보안 경고의 목록이 표시 됩니다 hello 문제 및 방법에 대 한 권장 사항 tooquickly 필요한 정보를 조사 tooremediate 공격입니다.

보안 센터 위협 요소 탐지 자동으로 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 수집 하 여 작동 합니다. 이 정보를 종종 tooidentify 위협 여러 소스의 정보 상관 관계를 분석 합니다. 보안 경고 사항 tooremediate 위협 hello 하는 방법에 대 한 권장 사항과 함께 보안 센터에 우선 순위입니다.

![Azure 보안 센터](./media/azure-log-audit/azure-log-audit-fig7.png)

보안 센터는 서명 기반 방식을 뛰어 넘는 고급 보안 분석을 사용합니다. 큰 데이터의 문제를 해결 하면 및 [기계 학습](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) 기술은 것이 불가능 한 tooidentify 수동 방법을 사용 하 고 hello를 예측 하는 위협을 감지 – hello 전체 클라우드 패브릭에서 적용 된 tooevaluate 이벤트 공격 발전 합니다. 이러한 보안 분석은 다음과 같습니다.

-   **위협 인텔리전스 통합:** 찾습니다 알려진된 믿지 못할 자, Microsoft 제품 및 서비스에서 글로벌 위협 인텔리전스를 적용 하 여 Microsoft Digital Crimes 단위 (DCU), hello에 대 한 hello Microsoft 보안 대응 센터 (MSRC), 및 외부 피드를 나타냅니다.

-   **동작 분석:** 알려진된 패턴 toodiscover 악의적인 동작을 적용 합니다.

-   **이상 탐지:** toobuild 기록 기준선을 프로 파일링 통계 사용 합니다. 편차가 tooa 잠재적인 공격 벡터를 준수 하는 설정 된 기준에 게 알립니다.


많은 보안 작업 및 사고 대응 팀은 시작 지점에 대 한 심사 및 보안 경고를 조사 하는 hello를 보안 정보 및 이벤트 관리 (SIEM) 솔루션으로 사용 합니다. Azure 로그 통합을 사용하여 고객은 Azure 진단 및 Azure 감사 로그에 수집된 Azure Security Center 경고와 가상 컴퓨터 보안 이벤트를 거의 실시간으로 로그 분석 또는 SIEM 솔루션과 동기화할 수 있습니다.


## <a name="log-analytics"></a>Log Analytics

Log Analytics는 클라우드 및 온-프레미스 환경의 리소스로 생성된 데이터를 수집 및 분석할 수 있게 하는 [OMS(Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 서비스입니다. 통합된 검색을 사용 하 여 실시간 정보 제공 하 고 사용자 지정 대시보드 tooreadily 모든 작업 및 물리적 위치에 관계 없이 서버에서 수백만 개의 레코드를 분석 합니다.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Hello 센터의 로그 분석은 Azure 클라우드 hello에서 호스팅되는 hello OMS 리포지토리에입니다. 데이터 원본 구성 및 솔루션 tooyour 구독을 추가 하 여 연결 된 원본에서 hello 저장소로 데이터를 수집 합니다. 데이터 원본 및 솔루션 각 만들어집니다 다른 레코드 유형을 고유 속성 집합이 있지만 쿼리 toohello 리포지토리에 함께 분석 될 수 있습니다. 이렇게 하면 서로 다른 소스에 의해 수집 된 여러 종류의 데이터와 같은 도구와 방법을 toowork toouse hello 있습니다.

연결 된 소스 hello 컴퓨터 및 로그 분석에 의해 수집 된 데이터를 생성 하는 다른 리소스는 있습니다. 여기에는 직접 연결되어 있는 [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) 및 [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) 컴퓨터에 설치된 에이전트 또는 [연결된 System Center Operations Manager 관리 그룹](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents)의 에이전트가 포함될 수 있습니다. 또한 Log Analytics는 [Azure 저장소](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)에서 데이터를 수집할 수도 있습니다.

[데이터 원본](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) hello 여러 종류가 각 연결 된 소스에서 수집 된 데이터입니다. 이 이벤트를 포함 하 고 [성능 데이터](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) 에서 [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) 및 Linux 에이전트와 같은 추가 toosources에 [IIS 로그](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), 및 [사용자 지정 텍스트 로그입니다.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) 각 데이터 원본 toocollect, 원하는 및 hello 구성은 자동으로 배달 된 tooeach 연결된 원본 구성

[Azure 서비스에 대한 로그 및 메트릭을 수집](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)하는 방법에는 다음 네 가지가 있습니다.
1.  Azure 진단 직접 tooLog 분석 (다음 표는 hello에서 진단 사용)

2.  Azure 진단 tooAzure 저장소 tooLog 분석 (다음 표는 hello에 Storage)

3.  Azure 서비스 (다음 표는 hello의 커넥터)에 대 한 커넥터

4.  로그 분석 (다음 표는 hello에 나열 되지 않은 서비스에 대 한 공백) toocollect 및 게시 데이터 스크립트

| 부여 | 리소스 종류 | 로그 | 메트릭 | 해결 방법 |
| :------ | :------------ | :--- | :------ | :------- |
|응용 프로그램 게이트웨이|  Microsoft.Network/<br>applicationGateways|  진단|진단|    [Azure Application](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics) [Gateway Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application insights||     커넥터|  커넥터|  [Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [커넥터(미리 보기)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|자동화 계정|   Microsoft.Automation/<br>AutomationAccounts|    진단||       [자세한 정보](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|배치 계정|    Microsoft.Batch/<br>batchAccounts|  진단|    진단||
|클래식 Cloud Services||       저장소||       [자세한 정보](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Cognitive Services|    Microsoft.CognitiveServices/<br>계정|       진단|||
|Data Lake Analytics|   Microsoft.DataLakeAnalytics/<br>계정|   진단|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>계정|   진단|||
|이벤트 허브 네임스페이스|   Microsoft.EventHub/<br>namespaces|  진단|    진단||
|IoT Hub|  Microsoft.Devices/<br>IotHubs||     진단||
|키 자격 증명 모음| Microsoft.KeyVault/<br>vaults|  진단  || [KeyVault 분석](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|부하 분산 장치|    Microsoft.Network/<br>loadBalancers|    진단|||
|Logic Apps|    Microsoft.Logic/<br>workflows|  진단|    진단||
||Microsoft.Logic/<br>integrationAccounts||||
|네트워크 보안 그룹|   Microsoft.Network/<br>networksecuritygroups|진단||   [Azure 네트워크 보안 그룹 분석](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|복구 자격 증명|   Microsoft.RecoveryServices/<br>vaults|||[Azure Recovery Services 분석(미리 보기)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Search 서비스|   Microsoft.Search/<br>searchServices|    진단|    진단||
|서비스 버스 네임스페이스| Microsoft.ServiceBus/<br>namespaces|    진단|진단|    [Service Bus 분석(미리 보기)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       저장소||    [Service Fabric 분석(미리 보기)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL(v12)| Microsoft.Sql/<br>servers/<br>데이터베이스||       진단||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|저장소|||         스크립트| [Azure Storage 분석(미리 보기)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|가상 컴퓨터|  Microsoft.Compute/<br>virtualMachines|  내선 번호|  내선 번호||
||||진단||
|가상 컴퓨터 크기 집합|   Microsoft.Compute/<br>virtualMachines    ||진단||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|웹 서버 팜|Microsoft.Web/<br>serverfarms||   진단
|웹 사이트| Microsoft.Web/<br>sites ||      진단|    [자세한 정보](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slots|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>온-프레미스 SIEM 시스템과 로그 통합
[Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) toointegrate 원시 로그 tooyour 온-프레미스에서 Azure 리소스를 사용 하면 **보안 정보 및 이벤트 관리 SIEM () 시스템**합니다.

![로그 통합](./media/azure-log-audit/azure-log-audit-fig9.png)

Azure 로그 통합은 Windows(WAD) 가상 컴퓨터, Azure 활동 로그, Azure Security Center 경고 및 Azure 리소스 공급자 로그에서 Azure 진단을 수집합니다. 이러한 통합은 통합 된 대시보드 또는 hello 클라우드에 모든 자산을 온-프레미스에 대 한 있도록 집계, 상관 관계를 설정, 분석 및 보안 이벤트에 대 한 경고 수 있습니다.



Azure 로그 통합은 현재 Azure 활동 로그, Azure 구독의 Windows 가상 컴퓨터에서 제공된 Windows 이벤트 로그, Azure Security Center 경고, Azure 진단 로그 및 Azure Active Directory 감사 로그를 통합하도록 지원합니다.

| 로그 형식 | JSON(Splunk, ArcSight, Qradar)을 지원하는 Log Analytics |
| :------- | :-------------------------------------------------------- |
|AAD 감사 로그|    yes|
|활동 로그| 예|
|ASC 경고 |예|
|진단 로그(리소스 로그)|  예|
|VM 로그|   예(JSON을 통하지 않고 전달된 이벤트를 통해)|


hello 다음 표에서 설명 hello 로그 범주 및 SIEM 통합 세부 정보입니다.

[Azure 로그 통합 시작](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) - 이 자습서에서는 Azure 로그 통합을 설치하고, Azure WAD 저장소, Azure 활동 로그, Azure Security Center 경고 및 Azure Active Directory 감사 로그를 통합하는 방법을 단계별로 안내합니다.

통합 시나리오

-   [구성 단계를 파트너](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) –이 블로그 게시물을 보면 tooconfigure Azure Splunk, HP ArcSight 및 IBM QRadar 파트너 솔루션과 통합 toowork를 로그 하는 방법은 합니다.

-   [Azure 로그 통합 FAQ(질문과 대답)](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) - 이 FAQ는 Azure 로그 통합에 대한 질문에 답변합니다.

-   [보안 센터를 통합 합니다. Azure와 경고 로그 통합](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) -이 문서에서는 어떻게 toosync 보안 센터 경고, 로그 분석으로 Azure 진단 및 Azure 감사 로그에서 수집 하는 가상 컴퓨터 보안 이벤트와 함께 또는 SIEM 솔루션입니다.

## <a name="next-steps"></a>다음 단계

- [감사 및 로깅](https://www.microsoft.com/trustcenter/security/auditingandlogging)

표시 여부를 유지 관리 하 고 tootimely 보안 경고를 신속 하 게 대응 하 여 데이터 보호

- [Azure 내 보안 로깅 및 감사 로그 수집](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Azure 인스턴스를 수집 하는 있는지 tooenforce toomake 필요한 어떤 설정은 hello 올바른 보안 및 감사 로그입니다.

- [사이트 모음에 대한 감사 설정 구성](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

사이트 컬렉션 관리자 권한으로 특정 사용자가 수행한 작업의 hello 기록을 검색할 수 하나 있으며 특정 날짜 범위 동안 수행 된 작업의 hello 기록을 검색할 수도 있습니다. 

- [Hello hello Office 365 보안 및 준수 센터에서 감사 로그 검색](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Office 365 조직에 Office 365 보안 및 준수 센터 toosearch hello 통합된 감사 로그 tooview 사용자 hello 및 관리자 활동을 사용할 수 하나.


