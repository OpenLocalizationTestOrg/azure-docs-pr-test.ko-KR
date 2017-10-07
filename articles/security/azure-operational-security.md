---
title: "작업 보안 aaaAzure | Microsoft Docs"
description: "Microsoft OMS(Operations Management Suite), 해당 서비스 및 작동 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Azure 운영 보안
## <a name="introduction"></a>소개

### <a name="overview"></a>개요
회원님의 보안은 hello 클라우드에서 작업 하나 고 Azure 보안에 대 한 정확 하 고 시기 적절 한 정보를 찾을 얼마나 중요 한지 됩니다. Hello 최상의 이유 toouse Azure 응용 프로그램 및 서비스에 대 한 중 하나 tootake 활용 hello 다양 한 보안 도구 및 사용할 수 있는 기능입니다. 이러한 도구와 기능 hello 보안 Azure 플랫폼에서 가능한 toocreate 보안 솔루션을 확인할 수 있습니다. Microsoft Azure는 고객 데이터의 기밀성, 무결성 및 가용성을 제공해야 하는 한편 투명한 책임도 가능하게 해야 합니다.

toohelp 고객 hello 배열에서 두 hello 고객의 Microsoft Azure 내에서 구현 하는 보안 제어를 더 잘 이해 하 고 Microsoft operational 큐브 뷰를이 백서, "Azure Operational 보안"를 제공 하는 기록 됩니다.는 Windows Azure와 함께 사용할 수 있는 작업 보안 hello 포괄적인 보기.

### <a name="azure-platform"></a>Azure 플랫폼
Azure는 다양한 운영 체제, 프로그래밍 언어, 프레임워크, 도구, 데이터베이스 및 장치를 지원하는 공용 클라우드 서비스 플랫폼입니다. Docker 통합으로 Linux 컨테이너를 실행할 수 있습니다. JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드할 수 있습니다. iOS, Android 및 Windows 장치용 백 엔드를 빌드할 수 있습니다. Azure 클라우드 서비스는 hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다.

를, 작성 하거나 IT 자산을 마이그레이션할 때 해당 조직의 능력 tooprotect 응용 프로그램 및 데이터 hello 서비스 및 hello 컨트롤을 사용 하는 공용 클라우드 서비스 공급자 제공 toomanage hello 보안의 클라우드 기반 자산에 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고는 기업의 보안 요구 사항을 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 다양 한 구성 가능한 보안 옵션 및 hello 기능 toocontrol와 보안 toomeet hello 조직의 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다. 이 문서는 Azure 보안 기능이 이러한 요구 사항을 충족하는 방법을 이해하는 데 도움이 됩니다.

### <a name="abstract"></a>요약
Azure Operational 보안 toohello 서비스, 컨트롤 및 기능 사용 가능한 toousers 데이터, 응용 프로그램 및 Microsoft Azure에서 기타 자산을 보호 하기 위한 참조 합니다. Azure Operational 보안 고유 tooMicrosoft, Microsoft SDL Security Development Lifecycle (), Microsoft 보안 대응 센터 hello hello를 포함 하는 다양 한 기능을 통해 얻은 hello 정보를 통합 하는 프레임 워크에 만들어집니다. 프로그램 및 hello 사이버 안보 위협 상황의 심층 인식 합니다.

이 백서에서는 hello Microsoft Azure 클라우드 플랫폼 및 적용 됩니다. 다음 서비스 내에서 Microsoft의 접근 방식을 tooAzure 작업 보안을 설명 합니다.
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure 저장소 분석](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft 작업 관리 도구 모음

Microsoft Operations Management Suite (OMS)는 hello hello 하이브리드 클라우드 용 IT 관리 솔루션입니다. 단독으로 사용 하거나 기존 System Center 배포 OMS를 사용 하면 tooextend hello 최대 유연성과 인프라의 클라우드 기반 관리에 대 한 제어 합니다.

![Microsoft 작업 관리 도구 모음](./media/azure-operational-security/azure-operational-security-fig1.png)

OMS를 사용하면 경쟁력 있는 솔루션보다 저렴한 비용으로 온-프레미스, Azure, AWS, Windows Server, Linux, VMware 및 OpenStack을 포함한 모든 클라우드의 모든 인스턴스를 관리할 수 있습니다. OMS를 새로운 접근 방식을 toomanaging에서는 클라우드 우선 world hello에 대 한 기본 제공 hello 가장 빠르고 가장 비용 효과적인 방법 toomeet 새로운 비즈니스 과제 하 고 응용 프로그램 및 클라우드 환경을 새 워크 로드를 수용 하는 기업입니다.

### <a name="oms-services"></a>OMS 서비스

OMS의 핵심 기능 hello Azure에서 실행 되는 서비스 집합에서 제공 됩니다. 각 서비스는 특정 관리 기능을 제공 하 고 서비스 tooachieve 다른 관리 시나리오를 결합할 수 있습니다.

| 부여  | 설명|
| :------------- | :-------------|
| Log Analytics | 모니터링 하 고 다양 한 리소스 등 물리적 및 가상 컴퓨터의 hello 가용성과 성능을 분석 합니다. |
|Automation | 수동 프로세스를 자동화하고 실제 컴퓨터와 가상 컴퓨터에 대한 구성을 적용합니다. |
| 백업 | 중요한 데이터를 백업하고 복원합니다. |
| 사이트 복구 | 중요한 응용 프로그램에 고가용성을 제공합니다. |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)는 관리형 리소스의 데이터를 중앙 리포지토리로 수집하여 OMS에 대한 모니터링 서비스를 제공합니다. 이 데이터는 이벤트, 성능 데이터 또는 hello API 통해 제공 되는 사용자 지정 데이터에 포함 될 수 있습니다. 수집 되 면 hello 데이터는 경고, 분석 및 내보내기에 사용할 수 있습니다.


이 방법을 사용 하면 다양 한 소스에서 tooconsolidate 데이터를 결합할 수 있으므로 데이터는 기존 Azure 서비스를 온-프레미스 환경. 모든 작업을 사용할 수 있는 tooall 종류의 데이터를 해당 데이터에 대해 수행한 hello 동작의 결과로 명확 하 게 hello 데이터의 hello 컬렉션을 구분 합니다.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

hello 로그 분석 서비스 메서드를 다음 hello를 사용 하 여 클라우드 기반 데이터를 안전 하 게 관리 합니다.
-   데이터 분리
-   데이터 보존
-   물리적 보안
-   인시던트 관리
-   규정 준수
-   보안 표준 인증

### <a name="azure-backup"></a>Azure Backup

[Azure 백업](http://azure.microsoft.com/documentation/services/backup) 백업 및 복원 서비스 및 hello OMS 제품군 제품 및 서비스의 일부인 데이터를 제공 합니다.
자본 투자 없이 최소한의 운영 비용으로 응용 프로그램 데이터를 보호하고 수년 간 보관합니다. 해당 데이터를 백업할 수 물리적 및 가상 Windows 서버에서 뿐만 아니라 SQL Server 및 SharePoint와 같은 tooapplication 작업 합니다. 사용할 수도 있습니다 [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate 중복성 및 장기 저장에 대 한 데이터 tooAzure 보호 합니다.


Azure Backup의 보호 데이터는 특정 지리적 지역에 있는 백업 저장소에 저장됩니다. hello 데이터가 복제 내 동일한 지역 hello 하 고, 자격 증명 모음에 hello 유형에 따라 추가 복구를 위한 복제 tooanother 영역을 될 수도 있습니다.

### <a name="management-solutions"></a>관리 솔루션
[Microsoft OMS(Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)는 온-프레미스 및 클라우드 인프라를 관리하고 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.


[관리 솔루션](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions)은 하나 이상의 OMS 서비스를 사용하여 특정 관리 시나리오를 구현하는 미리 패키지된 논리 집합입니다. 다른 솔루션은 oms에서 투자의 tooyour tooincrease hello 가치를 Azure 구독을 쉽게 추가할 수는 파트너 및 Microsoft에서 사용할 수 있습니다. 파트너 응용 프로그램 및 서비스 사용자 고유의 솔루션 toosupport를 만들 수 있으며 hello Azure 마켓플레이스 또는 빠른 시작 템플릿을 통해 toousers를 제공 하 고 키를 누릅니다.


![관리 솔루션](./media/azure-operational-security/azure-operational-security-fig4.png)

여러 서비스 tooprovide 추가 기능을 사용 하는 솔루션의 좋은 예로 hello [업데이트 관리 솔루션](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management)합니다. 이 솔루션에서는 hello [로그 분석](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) 각 에이전트에 필요한 업데이트에 대 한 있는 Windows 및 Linux toocollect 정보에 대 한 에이전트입니다. 이 데이터 toohello 로그 분석 저장소에 포함 된 대시보드를 분석할 수를 기록 합니다.

Runbook에는 배포를 만들 때 [Azure 자동화](https://docs.microsoft.com/azure/automation/automation-intro) 업데이트가 사용 되는 tooinstall 필요 합니다. Hello 포털에서이 전체 프로세스를 관리 하 고 hello 기본 세부 정보에 대 한 tooworry 필요 하지 않습니다.

## <a name="azure-security-center"></a>Azure 보안 센터

Azure Security Center는 Azure 리소스를 보호하는 데 도움이 됩니다. Azure 구독에서 통합된 보안 모니터링 및 정책 관리를 제공합니다. Hello 서비스 내에서 수 있다면 toodefine 정책을 뿐만 아니라 Azure 구독에 대 한도 대 한 [리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)이므로 보다 세부적인 할 수 있습니다.

### <a name="security-policies-and-recommendations"></a>보안 정책 및 권장 사항

보안 정책 hello 지정된 구독 또는 리소스 그룹 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 합니다.

보안 센터 tooyour 회사의 보안 요구 사항 및 응용 프로그램의 hello 유형 또는 hello 데이터의 민감도 따라 정책을 정의 합니다.

![보안 정책 및 권장 사항](./media/azure-operational-security/azure-operational-security-fig5.png)


Hello 오른쪽에 hello 다이어그램에 나타난 대로 hello 구독 내에서 tooall 리소스 그룹을 전파 하는 hello 구독 수준에 자동으로 설정 된 정책:


### <a name="data-collection"></a>데이터 수집

보안 센터에서에서 데이터를 수집한 가상 컴퓨터 (Vm) tooassess 자신의 보안 상태, 보안 권장 사항을 제공 하 고 있습니다 toothreats 경고 합니다. Security Center에 처음 액세스하는 경우 구독의 모든 VM에서 데이터 수집이 활성화됩니다. 데이터 수집 좋지만 hello 정책 보안 센터에서에서 데이터 수집을 해제 하 여 취소할 수 있습니다.

### <a name="data-sources"></a>데이터 원본

- 소스 tooprovide 가시성 보안 상태에 따라 hello에서 데이터를 분석 하는 azure 보안 센터, 취약성을 식별 하 고 완화, 권장 있으며 활성 위협이 검색:

-   Azure 서비스: 해당 서비스의 리소스 공급자와 통신 하 여 배포한 hello Azure 서비스 구성에 대 한 정보를 사용 합니다.

- 네트워크 트래픽: 원본/대상 IP/포트, 패킷 크기 및 네트워크 프로토콜과 같은 Microsoft의 인프라에서 샘플링된 네트워크 트래픽 메타데이터를 사용합니다.

-   파트너 솔루션: 방화벽 및 맬웨어 방지 솔루션과 같은 통합된 파트너 솔루션의 보안 경고를 사용합니다.

-   가상 컴퓨터: Windows 이벤트 및 감사 로그, IIS 로그, syslog 메시지 및 가상 컴퓨터의 크래시 덤프 파일과 같은 보안 이벤트에 대한 구성 정보 및 정보를 사용합니다.

### <a name="data-protection"></a>데이터 보호

toohelp 고객 방지 감지 하 고 toothreats 응답, Azure 보안 센터를 수집 하 고 구성 정보, 메타 데이터, 이벤트 로그, 크래시 덤프 파일 등의 보안 관련 데이터를 처리 합니다. Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다.

-   **데이터 분리**: 데이터 hello 서비스 전체에서 각 구성 요소에 논리적으로 별도로 유지 됩니다. 모든 데이터에는 조직별로 태그가 지정됩니다. 이 태그 hello 데이터 수명 주기 동안 유지 되며 hello 서비스의 각 계층에서 적용 됩니다.

-   **데이터 액세스**: tooprovide 보안 권장 사항 및 잠재적 보안 위협을 조사할 Microsoft 담당자 수집 된 정보에 액세스 하거나 VM 디스크를 만드는 이벤트, 처리 크래시 덤프 파일을 비롯 한 Azure 서비스를 사용 하 여 분석할 수 있습니다 스냅숏 및 아티팩트 고객 데이터 또는 가상 컴퓨터의 개인 데이터가 의도 하지 않게 포함 될 수 있습니다. Toohello 준수 우리 [Microsoft 온라인 서비스 약관 및 개인정보취급방침](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), Microsoft는이 상태를 고객 데이터를 사용 하 여 또는 광고 또는 유사한 상업적 목적에서 정보를 파생 합니다.

-   **데이터 사용**: 패턴을 사용 하 여 Microsoft 및 위협 인텔리전스 표시를 여러 테 넌 트에서 tooenhance 취급 예방 및 감지 기능;에 설명 된 hello 개인 정보 행에 따라 이렇게 우리의 [개인 정보 문](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx)합니다.

### <a name="data-location"></a>데이터 위치

Azure 보안 센터는 크래시 덤프 파일의 임시 복사본을 수집하고 이용 시도 및 손상 성공의 증거를 찾기 위해 분석합니다. Azure 보안 센터 내에서이 분석을 수행 합니다. 작업 영역에서 hello으로 같은 지역 hello 및 분석이 완료 되 면 삭제 hello 임시 복사본입니다. 컴퓨터 아티팩트 중앙에 저장 된 VM hello으로 같은 지역 hello 합니다.

-   **저장소 계정**: 가상 컴퓨터가 실행되는 각 지역에 대해 지정됩니다. 있습니다 toostore 데이터는 hello에서 데이터를 수집 하는 hello 가상 컴퓨터와 같은 지역의 hello 따라서 수 있습니다.

-   **Azure 보안 센터 저장소**: 파트너 경고, 권장 사항 및 보안 상태를 포함 하 여 보안 경고에 대 한 정보에 중앙 집중식으로, 현재 hello 미국에 저장 됩니다. 이 정보는 관련된 구성 정보를 포함할 수 있습니다 및 보안 이벤트 수집 된 가상 컴퓨터에서 필요한 tooprovide 있습니다 hello 보안 경고, 권장 또는 보안 상태 상태와 함께 합니다.


## <a name="azure-monitor"></a>Azure Monitor

hello [OMS 보안](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) 및 보안 문제의 hello 영향을 최소화 하는 데 사용할 수 있는 모든 리소스를 모니터링 하는 IT tooactively 감사 솔루션 수 있습니다. OMS 보안 및 감사에는 리소스 모니터링에 사용할 수 있는 보안 도메인이 있습니다. toooptions 빠른 액세스를 제공 하는 hello 보안 도메인, 보안 hello 모니터링에 대 한 다음 도메인에에서 대해서는 설명 자세한 세부 정보:

-   맬웨어 평가
-   업데이트 평가
-   ID 및 액세스

Azure 모니터 특정 유형의 리소스에 대 한 포인터 tooinformation를 제공합니다. 시각화, 쿼리, 라우팅, 경고, 자동 크기 조정 및 자동화 hello Azure 인프라 (활동 로그)에서 데이터 및 각 개별 Azure 리소스 (진단 로그의 경우)에 제공합니다.

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다. 모니터링 없이 계속 응용 프로그램 데이터 tooensure 정상 상태에서 실행 되 고 제공 합니다. 또한 있습니다 toostave 잠재적 문제를 해제 하거나 문제를 해결 하십시오. 지난 수 있습니다.

또한 응용 프로그램에 대 한 모니터링 데이터 toogain 깊은 통찰력을 사용할 수 있습니다. 이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다.

### <a name="azure-activity-log"></a>Azure 동작 로그


해당 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 하는 로그입니다. hello 활동 로그는 구독에 대 한 제어 평면 이벤트를 보고 하므로 이전에 "감사 로그" 또는 "작업 로그"로 알려졌습니다.

![Azure 동작 로그](./media/azure-operational-security/azure-operational-security-fig7.png)

Hello 활동 로그를 사용 하 여 hello를 확인할 수 ' 부분, who, 시기 및 ' hello 구독의 리소스에에서 대해 수행 하는 작업 (PUT, POST, DELETE) 쓰기에 대 한 합니다. Hello 작업 및 기타 관련 속성의 hello 상태를 이해할 수 있습니다. 읽기 (GET) 작업 또는 작업 hello 클래식 모델을 사용 하는 리소스에 대 한 활동 로그 hello 포함 되지 않습니다.

### <a name="azure-diagnostic-logs"></a>Azure 진단 로그

이러한 로그 리소스에 의해 발생 하 고 해당 리소스의 hello 작업에 대 한 풍부한 자주 데이터를 제공 합니다. 이러한 로그의 hello 콘텐츠 리소스 유형에 따라 달라 집니다.

예를 들어, Windows 이벤트 시스템 로그는 VM 및 Blob에 대한 진단 로그의 범주이고 테이블 및 큐 로그는 저장소 계정에 대한 진단 로그의 범주입니다.

진단 로그 hello에서 다 [(이전의 작업 로그 또는 감사 로그) 활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)합니다. hello 활동 로그 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 합니다. 진단 로그는 리소스 자체에서 수행하는 작업에 대한 정보를 제공합니다.

### <a name="metrics"></a>메트릭

Azure 모니터 hello 성능 및 Azure에서 작업의 상태에 대 한 tooconsume 원격 분석 toogain 가시성이 있습니다. Azure 원격 분석 데이터의 가장 중요 한 형식은 hello에는 대부분의 Azure 리소스에서 내보내는 hello 메트릭 (성능 카운터)입니다. Azure 모니터 여러 가지 방법으로 tooconfigure 제공 하 고 이러한 사용할 [메트릭](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) 모니터링 및 문제 해결 합니다. 메트릭 원격 분석의 중요 한 소스로 및 toodo hello 다음 작업을 사용 하면:

-   **Hello 성능을 추적** 포털 차트에서 해당 메트릭이 그래프에 표시 및 해당 차트 tooa 대시보드에 고정 하 여 리소스 (예: VM, 웹 사이트 또는 논리 앱).

-   **문제의 알림** 된 메트릭이 특정 임계값을 초과할 때 영향을 미치는 리소스의 성능을 hello 하 합니다.

-   메트릭이 특정 임계값을 초과할 때 리소스 자동 크기 조정 또는 runbook 실행과 같은 **자동화된 작업을 구성합니다**.

-   리소스의 성능 또는 사용 추세에 대한 **고급 분석**이나 보고를 수행합니다.

-   **보관** hello 규정 준수 또는 감사 목적에 대 한 리소스의 성능이 나 상태 기록 합니다.

### <a name="azure-diagnostics"></a>Azure 진단

이 배포 된 응용 프로그램에서 진단 데이터의 hello 수집할 수 있도록 하는 Azure 내에서 hello 기능입니다. 서로 다른 다양 한 원본의 hello 진단 확장을 사용할 수 있습니다. [Azure 클라우드 서비스 웹 및 작업자 역할](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), Microsoft Windows를 실행하는 [Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/overview) 및 [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics)이 현재 지원되고 있습니다. 다른 Azure 서비스에는 별도의 자체 진단이 있습니다.

## <a name="azure-network-watcher"></a>Azure Network Watcher

네트워크 보안 감사는 네트워크 취약성을 검색하고 IT 보안 및 규제 관리 모델을 준수하는 것이 중요합니다. 보안 그룹 보기를 구성 하는 hello 네트워크 보안 그룹 및 보안 규칙을 검색할 수 있으며 효과적인 보안 규칙 hello 수 있습니다. 적용 되는 규칙 hello 목록을 사용 하 여 hello 포트 열려 있으며 네트워크 취약성 평가 확인할 수 있습니다.

[네트워크 감시자](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) toomonitor 수 있는 지역 서비스 이며에서 및에서 Azure 네트워크 수준에서 상태를 진단 합니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다. 이 서비스에는 패킷 캡처, 다음 홉, IP 흐름 확인, 보안 그룹 보기, NSG 흐름 로그가 포함되어 있습니다. 수준 모니터링 시나리오는 전체적인 tooend 뷰 대비 tooindividual 네트워크 리소스 모니터링의 네트워크 리소스를 제공합니다.

![Azure Network Watcher](./media/azure-operational-security/azure-operational-security-fig8.png)

네트워크 감시자는 현재 hello 기능 뒤에 있습니다.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">감사 로그</a>**-네트워크의 hello 구성의 일부분으로 수행 되는 작업 기록 됩니다. 이러한 로그는 hello Azure 포털에서에서 볼 수 있습니다 또는 Power BI와 같은 Microsoft 도구 또는 타사 도구를 사용 하 여 검색 합니다. 감사 로그는 hello 포털, PowerShell, CLI 및 Rest API를 통해 사용할 수 있습니다. 감사 로그에 대한 자세한 내용은 "Resource Manager로 작업 감사"를 참조하세요. 감사 로그는 모든 네트워크 리소스에서 수행된 작업에 사용할 수 있습니다.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">IP 흐름 확인</a>** - 흐름 정보의 5개 튜플 패킷 매개 변수(대상 IP, 원본 IP, 대상 포트, 원본 포트 및 프로토콜)에 따라 패킷이 허용되거나 거부되는지 여부를 확인합니다. Hello 패킷 네트워크 보안 그룹에 의해 거부 되 면 hello 규칙과 hello 패킷 거부 네트워크 보안 그룹 반환 됩니다.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">다음 홉</a>**  -hello toodiagnose 잘못 구성 된 모든 사용자 정의 경로 사용 하면 Azure 네트워크 패브릭에서 라우팅되는 패킷의 hello 다음 홉을 결정 합니다.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">보안 그룹 보기</a>**  -VM에 적용 되는 hello 효과적이 고 적용 된 보안 규칙을 가져옵니다.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">NSG 흐름 로깅</a>**  -네트워크 보안 그룹에 대 한 흐름 로그 허용 되거나 hello hello 그룹 보안 규칙에 의해 거부 된 toocapture 로그 관련된 tootraffic를 사용 합니다. hello 흐름은 5-튜플 정보 – 원본 IP, 대상 IP, 원본 포트, 대상 포트 및 프로토콜에 의해 정의 됩니다.

## <a name="azure-storage-analytics"></a>Azure Storage 분석

[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) 요청 tooa 저장소 서비스에 대 한 집계 된 트랜잭션 통계 및 용량 데이터가 포함 된 메트릭을 저장할 수 있습니다. 두 hello API 작업 수준 및 hello 저장소 서비스 수준에서 트랜잭션을 보고 하 고 용량은 hello 저장소 서비스 수준에서 보고 됩니다. 메트릭 데이터는 사용 되는 tooanalyze 저장소 서비스 사용 될, hello 저장소 서비스 및 서비스를 사용 하는 응용 프로그램의 tooimprove hello 성능에 대해 수행 된 요청 문제를 진단할 수 있습니다.

[ 분석](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)은 로깅을 수행하며 저장소 계정에 대한 메트릭 데이터를 제공합니다. 이 데이터 tootrace 요청을 사용 하 고, 사용 추세를 분석 하 고, 저장소 계정 문제를 진단할 수 있습니다. 저장소 분석 로깅을 ´ ü ± hello [Blob, 큐 및 테이블 서비스](https://docs.microsoft.com/azure/storage/storage-introduction)합니다. Storage Analytics는 성공 및 실패 한 요청 tooa 저장소 서비스에 대 한 세부 정보를 기록 합니다.

이 정보는 개별 요청을 사용 하는 toomonitor 및 저장소 서비스와 toodiagnose 문제 수 있습니다. 요청은 최상의 노력을 기준으로 기록됩니다. Hello 서비스 끝점에 대 한 요청의 경우에 로그 항목이 생성 됩니다. 예제에서는 저장소 계정에 활동의 테이블 또는 큐 끝점 있지만 해당 Blob 끝점에만 로그에 관련 된 Blob 서비스 toohello가 만들어집니다.

toouse Storage Analytics를 사용 하도록 설정 해야 개별적으로 각 서비스에 대해 원하는 toomonitor 합니다. Hello에서 설정할 수 [Azure 포털](https://portal.azure.com/); 자세한 내용은 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account)합니다. Hello REST API를 통해 프로그래밍 방식으로 Storage Analytics 하거나 hello 클라이언트 라이브러리를 사용할 수도 있습니다. 각 서비스에 대해 개별적으로 hello Set Service Properties 작업 tooenable Storage Analytics를 사용 합니다.

hello 집계 된 데이터 및 저장 된 잘 알려진 blob (로깅용)에 잘 알려진 테이블 (통계용), hello Blob 서비스 및 테이블 서비스 Api 사용 하 여 액세스할 수 있는 합니다.

Storage Analytics에서는 저장소 계정의 총 한도와 hello와 독립적인 저장 된 데이터 양을 hello 20 TB 제한 됩니다. 모든 로그는 $logs라는 컨테이너의 [블록 Blob](https://docs.microsoft.com/azure/storage/storage-analytics)에 저장되며, 저장소 계정에 대해 저장소 분석을 사용하도록 설정하면 자동으로 만들어집니다.

Storage Analytics에서 수행 하는 작업을 수행 하는 hello는 청구 가능 합니다.

-   로깅에 대 한 요청 toocreate blob
-   메트릭에 대 한 요청 toocreate 테이블 엔터티입니다.

> [!Note]
> 청구 및 데이터 보존 정책에 대한 자세한 내용은 [저장소 분석 및 청구](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)를 참조하세요.
> 최적의 성능을 위해서는 toolimit hello 수의 고도로 과소 디스크 연결 toohello 가상 컴퓨터 tooavoid 가능한 제한 하는 것이 좋습니다. 하는 경우 모든 디스크는 사용 하지 않도록 항상 hello에서 같은 시간 hello 저장소 계정에서 가장 큰 숫자 디스크를 지원할 수 있습니다.

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
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD에는 다단계 인증, 장치 등록, 셀프 서비스 암호 관리, 셀프 서비스 그룹 관리, 권한 있는 계정 관리, 역할 기반 액세스 제어, 응용 프로그램 사용 모니터링, 광범위한 감사, 보안 모니터링 및 경고를 포함한 완벽한 ID 관리 기능이 포함되어 있습니다.

-   Azure AD 다단계 인증 및 조건부 액세스를 사용하여 응용 프로그램 보안을 개선합니다.

-   응용 프로그램 사용을 모니터링하고 보안 보고 및 모니터링을 통해 비즈니스를 고급 위협으로부터 보호합니다.

Azure AD(Azure Active Directory)에는 디렉터리에 대한 보안, 활동 및 감사 보고서가 포함되어 있습니다. [Azure Active Directory 감사 보고서 hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) 고객이 privileged tooidentify 발생 한 작업을 Azure Active Directory에 편리 합니다. 특권이 필요한 작업 (예를 들어 역할 만들기 또는 암호 재설정) 상승 변경 내용을 포함 toodirectory 구성 변경 (예: 변경 내용 toodomain 페더레이션 설정) 또는 정책 구성 (예: 암호 정책)을 변경 합니다.

hello 보고서 hello 변경 및 hello 날짜 및 시간 (UTC)에 영향을 받는 hello 대상 리소스 hello 동작을 수행한 hello 행위자 hello 이벤트 이름에 대 한 hello 감사 레코드를 제공 합니다. 고객은 hello 통해 자신의 Azure Active Directory에 대 한 감사 이벤트의 수 tooretrieve hello 목록을 [Azure 포털](https://portal.azure.com/)에 설명 된 대로 [감사 로그를 보려면](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)합니다. 포함 된 hello 보고서 목록은 다음과 같습니다.

| 보안 보고서  | 작업 보고서| 감사 보고서 |
| :------------- | :-------------| :-------------|
|알 수 없는 원본에서 로그인 | 응용 프로그램 사용: 요약 | 디렉터리 감사 보고서 |
|여러 번의 실패 후 로그인 | 응용 프로그램 사용: 세부 |   |
|여러 지역에서의 로그인 | 응용 프로그램 대시보드 |  |
|의심스러운 작업이 있는 IP 주소에서 로그인 |계정 프로비전 오류 |  |
|비정상적인 로그인 작업 |개별 사용자 장치 |  |
|감염 가능성이 있는 장치에서 로그인 |개별 사용자 활동 |   |
|비정상적인 로그인 활동을 포함하는 사용자 |그룹 활동 보고서 |   |
| |암호 재설정 등록 활동 보고서 |   |
| |암호 재설정 활동 |   | |



이러한 보고서의 hello 데이터 SIEM 시스템, 감사, 비즈니스 인텔리전스 도구 등의 유용한 tooyour 응용 프로그램을 수 있습니다. hello Azure AD 보고 [Api](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다. 이러한 API는 다양한 프로그래밍 언어와 도구에서 호출할 수 있습니다.

Hello Azure AD 감사 보고서의에서 이벤트는 180 일 동안 유지 됩니다.

> [!Note]
> 보고서에 보존하는 방법에 대한 자세한 내용은 [Azure Active Directory 보고서 보존 정책](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)을 참조하세요.

저장 관심이 있는 고객에 대 한 자신의 [감사 이벤트](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) 더 긴 보존 기간에 대 한 hello Reporting API 수를 별도 데이터 저장소로 사용 되는 tooregularly 끌어오기 감사 이벤트입니다.

## <a name="summary"></a>요약

사용자의 개인 정보를 보호 하 고, 소프트웨어 및 서비스 수를 제공 하는 동시에 데이터를 보호 하려면이 문서 요약 hello 조직의 IT 인프라를 관리 합니다. Microsoft는 해당 데이터 tooothers을 맡길 될 때 해당 신뢰 엄격한 보안이 필요 함을 인식 합니다. Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다. 데이터 보안 및 보호는 Microsoft의 최우선 과제입니다.

이 문서에서 설명하는 내용은 다음과 같습니다.

-   데이터는 수집, 처리 및 보안 방법 hello Operations Management Suite (OMS)에서.

-   여러 데이터 원본에서 이벤트를 빠르게 분석합니다. 보안 위험을 파악 하 고 hello 범위 및 위협 및 공격 toomitigate hello 손상 보안 위반의 영향을 이해 합니다.

-   아웃바운드 악성 IP 트래픽과 악성 위협 유형을 시각화하여 공격 패턴을 식별합니다. 플랫폼에 관계 없이 전체 사용자 환경의 hello 보안 상태를 이해 합니다.

-   보안 또는 감사에 필요한 모든 hello 로그 및 이벤트 데이터를 캡처하십시오. 슬래시 hello 시간과 리소스가 필요 toosupply 완전 하 고 내보낼 수 있는 검색 가능한, 로그 및 이벤트 데이터 집합으로 보안 감사 합니다.

<ul>
<li>보안 관련 이벤트, 감사 및 위반 분석 tookeep 깊게 시각 자산을 수집 합니다.</li>
<ul>
<li>보안 상태</li>
<li>주목할 만한 문제</li>
<li>위협 요약</li>
</ul>
</ul>

## <a name="next-steps"></a>다음 단계

- [설계 및 운영 보안](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft 서비스를 디자인 하 고 소프트웨어 고려 toohelp의 보안이 포함 된 클라우드 인프라 탄력적이 고 공격 으로부터 방어가 인지 확인 합니다.

- [Operations Management Suite | 보안 및 규정 준수](https://www.microsoft.com/cloud-platform/security-and-compliance)

Microsoft 보안 데이터 및 분석 tooperform 지능적이 고 효과적인를 사용 하 여 위협 검색 합니다.

- [Azure 보안 센터 계획 및 작업](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) toooptimize 조직의 보안 요구 사항 및 클라우드 관리 모델을 기반으로 보안 센터의 사용을 따를 수 있는 단계 및 작업의 집합입니다.

