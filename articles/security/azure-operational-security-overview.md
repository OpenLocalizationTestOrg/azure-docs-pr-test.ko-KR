---
title: "aaaAzure 작업 보안 개요 | Microsoft Docs"
description: "이 문서에서는 hello Azure 작업 보안의 개요를 제공 합니다."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Azure 운영 보안 개요
Azure Operational 보안 toohello 서비스, 컨트롤 및 기능 사용 가능한 toousers 데이터, 응용 프로그램 및 Microsoft Azure에서 기타 자산을 보호 하기 위한 참조 합니다. [Azure Operational 보안](https://docs.microsoft.com/azure/security/azure-operational-security) 은 다양 한 Microsoft SDL Security Development Lifecycle (), Microsoft Security hello hello를 포함 하는 고유한 tooMicrosoft 되는 기능을 통해 얻은 hello 기술을 통합 하는 프레임 워크 응답 센터 프로그램 및 hello 사이버 보안 위협 상황의 심층 인식 합니다.

Azure Operational 보안 개요 중점적으로 영역을 다음 hello:

- Azure Operations Management Suite
-   Azure 보안 센터
-   Azure Monitor
-   Azure Network Watcher
-   Azure Storage 분석
-   Azure Active Directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
IT 운영 팀은 데이터 센터 인프라, 응용 프로그램 및 이러한 시스템의 hello 안정성과 보안을 비롯 한 데이터를 관리 하는 일을 담당 합니다. 그러나 복잡 한 IT 환경을 종종 증가 간에 보안 통찰력을 얻는 여러 보안 및 관리 시스템에서 조직 toocobble 함께 데이터가 필요 합니다.

[Microsoft OMS(Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)는 온-프레미스 및 클라우드 인프라를 관리하고 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.

OMS는 IT Automation, Security & Compliance, Log Analytics 및 Backup & Recovery와 같은 다양한 제품을 갖춘 클라우드 기반 IT 관리 솔루션입니다. 따라서 완벽 한 지원 toomanage 되며 IT 인프라 보호-온-프레미스와 클라우드 hello 합니다.

OMS의 핵심 기능 hello Azure에서 실행 되는 서비스 집합에서 제공 됩니다. 각 서비스는 특정 관리 기능을 제공 하 고 서비스 tooachieve 다른 관리 시나리오를 결합할 수 있습니다. 포함되는 서비스는 다음과 같습니다.

-   Log Analytics
-   자동화
-   Backup
-   사이트 복구

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)는 관리형 리소스의 데이터를 중앙 리포지토리로 수집하여 OMS에 대한 모니터링 서비스를 제공합니다. 이 데이터는 이벤트, 성능 데이터 또는 hello API 통해 제공 되는 사용자 지정 데이터에 포함 될 수 있습니다. 수집 되 면 hello 데이터는 경고, 분석 및 내보내기에 사용할 수 있습니다. 이 방법을 사용 하면 있습니다 tooconsolidate 데이터 다양 한 소스에서에서 기존 온-프레미스 환경과 Azure 서비스에서 데이터를 결합할 수 있도록 합니다. 모든 작업을 사용할 수 있는 tooall 종류의 데이터를 해당 데이터에 대해 수행한 hello 동작의 결과로 명확 하 게 hello 데이터의 hello 컬렉션을 구분 합니다.

### <a name="automation"></a>Automation
Microsoft [Azure 자동화](https://docs.microsoft.com/azure/automation/automation-intro) 사용자 tooautomate 클라우드 및 엔터프라이즈 환경에서 일반적으로 수행 되며 hello 수동, 장기 실행, 오류가 발생 하기 쉽고 자주 반복 되 작업 있는 방법을 제공 합니다. 시간을 절약할 수 및 일반 관리 작업의 hello 안정성이 증가 하 고도 예약으로 toobe 자동으로 정기적으로 수행 합니다. Runbook을 사용하는 프로세스를 자동화하거나 원하는 상태 구성을 사용하여 구성 관리를 자동화할 수 있습니다.

### <a name="backup"></a>백업
[Azure 백업](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) 는 hello Azure 기반 서비스 수 tooback를 사용 하 여 (또는 보호) 및 Microsoft 클라우드 hello에서 데이터를 복원 합니다. 기존의 온-프레미스 또는 오프사이트 백업 솔루션을 신뢰할 수 있고 안전하며 가격 경쟁력이 있는 클라우드 기반 솔루션으로 대체합니다. Azure 백업 제공 다운로드 하 고 hello 적절 한 컴퓨터에 배포 하는 여러 구성 요소 서버 또는 hello 클라우드입니다. 대상에 따라 달라 집니다 hello 구성 요소 또는 배포 하는 에이전트 tooprotect 합니다. 모든 Azure 백업 구성 요소 (온-프레미스 데이터를 보호 하는 여부에 관계 없이 또는 hello 클라우드)에 Azure에서 데이터 tooa 복구 서비스 자격 증명 모음을 사용 하는 tooback 될 수 있습니다. Hello 참조 [Azure 백업 구성 요소 테이블](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use)합니다.

### <a name="site-recovery"></a>Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) 온-프레미스 가상의 복제 및 물리적 컴퓨터 tooAzure 또는 tooa 보조 사이트를 오케스트레이션 하 여 비즈니스 연속성을 제공 합니다. 기본 사이트를 사용할 수 없는 경우 장애 조치 toohello 보조 위치는 사용자가 계속 작업할 수 있고 시스템 tooworking 순서를 반환 하는 경우 실패 합니다. 지능적이고 효과적인 위협 검색.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario)는 Microsoft의 포괄적인 IDaaS(Identity as a Service) 솔루션입니다.

-   클라우드 서비스로 IAM 사용
-   중앙 액세스 관리, SSO(Single Sign-On) 및 보고 제공
-   통합 된 액세스 관리에 대 한 지원 [응용 프로그램](https://azure.microsoft.com/marketplace/active-directory/) hello 응용 프로그램 갤러리에서 비롯 한 Salesforce, Google Apps, Box, Concur, 및 더 합니다.

또한 Azure AD는 [다단계 인증](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), [장치 등록]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [셀프 서비스 암호 관리](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [권한 있는 계정 관리](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [역할 기반 액세스 제어](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [응용 프로그램 사용 모니터링](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [광범위한 감사](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 및 [보안 모니터링 및 경고](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts)를 포함하여 완벽한 [ID 관리 기능](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports) 제품군을 갖추고 있습니다.

Azure Active Directory와 모든 응용 프로그램에 게시 하면 파트너 및 고객 (비즈니스 또는 소비자) hello 들이 동일한 id 및 액세스 관리 기능. 이 사용 하면 toosignificantly 운영 비용을 절감 합니다.

## <a name="azure-security-center"></a>Azure 보안 센터
[Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-get-started) 사용 방지를 감지 하 고 및 toothreats 파악할을 사용 하 여 응답을 제어할 수 hello Azure 리소스의 보안 합니다. 이는 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

[Security Center](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine)를 사용하면 가상 컴퓨터의 보안 설정에 대한 가시성을 제공하고 위협을 모니터링하여 Azure의 가상 컴퓨터 데이터를 보호할 수 있습니다. Security Center는 다음의 목적으로 가상 컴퓨터를 모니터링할 수 있습니다.

-   권장 구성 규칙 hello로 운영 체제 (OS) 보안 설정
-   시스템 보안 및 누락된 중요 업데이트
-   끝점 보호 권장 사항
-   디스크 암호화 유효성 검사
-   네트워크 기반 공격

Azure 보안 센터를 사용 하 여 [역할 기반 액세스 제어 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)를 제공 하는 [기본 제공 역할](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) toousers, 그룹 및 Azure 서비스에에서 할당할 수 있습니다.

보안 센터의 리소스 tooidentify 보안 문제 및 취약점 hello 구성을 평가합니다. 보안 센터에만 정보를 확인할 때 hello 구독 또는 리소스 그룹에 속한 리소스에 대 한 소유자, 참가자 또는 판독기의 hello 역할이 할당 된 경우 tooa 리소스와 관련 된 합니다.

>[!Note]
>참조 [Azure 보안 센터에서 사용 권한을](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn 역할 및 보안 센터에서 허용 되는 작업에 대 한 자세한 합니다.

보안 센터 hello Microsoft Monitoring Agent를 사용 하 여 –이 hello 동일한 에이전트 hello Operations Management Suite 및 로그 분석 서비스에서 사용 합니다. 이 에이전트에서 수집 된 데이터는 기존 로그 분석에 저장 됩니다 [작업 영역](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) 또는 연결 된 Azure 구독 새 중 hello VM의 계정 hello 지리적 위치를 고려 합니다.

## <a name="azure-monitor"></a>Azure Monitor
클라우드 앱의 성능 문제는 비즈니스에 영향을 미칠 수 있습니다. 상호 연결된 여러 구성 요소와 자주 제공되는 릴리스를 사용하면 언제든지 성능 저하가 발생할 수 있습니다. 앱을 개발하는 경우 사용자는 일반적으로 테스트에서 찾지 못한 문제를 발견합니다. 이러한 문제를 즉시 알아야 하 고 hello 문제 진단 및 해결에 대 한 도구를 설치 해야 합니다.

[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) - Azure에서 실행되는 서비스를 모니터링하는 기본 도구입니다. 서비스와 환경 주변 hello hello 처리량에 대 한 인프라 수준의 데이터 제공 합니다. Azure에서 모든 앱을 관리 하는 경우 여부를 리소스를 위아래로 tooscale, 다음 Azure 모니터 제공 사용 하 여 결정 toostart 합니다.

또한 응용 프로그램에 대 한 모니터링 데이터 toogain 깊은 통찰력을 사용할 수 있습니다. 이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다. 다음을 포함합니다.

-   Azure 동작 로그
-   Azure 진단 로그
-   메트릭
-   Azure 진단

### <a name="azure-activity-log"></a>Azure 동작 로그
해당 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 하는 로그입니다. hello [활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) 구독에 대 한 제어 평면 이벤트를 보고 하므로 이전에 "감사 로그" 또는 "작업 로그"으로 알려져 있습니다.

### <a name="azure-diagnostic-logs"></a>Azure 진단 로그
[Azure 진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) 리소스에 의해 발생 되며 및 해당 리소스의 hello 작업에 대 한 다양 하 고 자주 데이터를 제공 합니다. 이러한 로그의 hello 콘텐츠 리소스 유형에 따라 달라 집니다.

예를 들어, Windows 이벤트 시스템 로그는 VM 및 Blob에 대한 진단 로그의 범주이고 테이블 및 큐 로그는 저장소 계정에 대한 진단 로그의 범주입니다.

진단 로그 hello에서 다 [(이전의 작업 로그 또는 감사 로그) 활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)합니다. hello 활동 로그 구독의 리소스에에서 대해 수행 된 hello 작업에 대 한 정보를 제공 합니다. 진단 로그는 리소스 자체에서 수행하는 작업에 대한 정보를 제공합니다.

### <a name="metrics"></a>메트릭
Azure 모니터 hello 성능 및 Azure에서 작업의 상태에 대 한 tooconsume 원격 분석 toogain 가시성이 있습니다. Azure 원격 분석 데이터의 가장 중요 한 형식은 hello에는 대부분의 Azure 리소스에서 내보내는 hello 메트릭 (성능 카운터)입니다. Azure 모니터 여러 가지 방법으로 tooconfigure 제공 하 고 이러한 사용할 [메트릭](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) 모니터링 및 문제 해결 합니다.

### <a name="azure-diagnostics"></a>Azure 진단
이 배포 된 응용 프로그램에서 진단 데이터의 hello 수집할 수 있도록 하는 Azure 내에서 hello 기능입니다. 서로 다른 다양 한 원본의 hello 진단 확장을 사용할 수 있습니다. 현재 [Azure 클라우드 서비스 웹 및 작업자 역할](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), Microsoft Windows를 실행하는 [Azure Virtual Machines](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) 및 [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics)이 지원되고 있습니다.


## <a name="network-watcher"></a>Network Watcher
고객은 VNet, ExpressRoute, Application Gateway, 부하 분산 장치 등과 같은 다양한 개별 네트워크 리소스를 오케스트레이션하고 구성하여 Azure에서 종단 간 네트워크를 구축합니다. 모니터링 하는 것은 각 hello 네트워크 리소스에 사용할 수 있습니다.

복잡 한 구성 및 리소스를 만드는 시나리오 기반 네트워크 감시자를 통해 모니터링 해야 하는 복잡 한 시나리오 간의 상호 작용 hello 엔드 tooend 네트워크를 가질 수 있습니다.

[Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)는 Azure 네트워크의 모니터링 및 진단을 간소화합니다. 네트워크 감시자 사용 하면 tootake 원격 패킷 캡처에 Azure 가상 컴퓨터를 사용할 수 있는 진단 및 시각화 도구 흐름 로그를 사용 하 여 네트워크 트래픽에 대 한 이해력 및 VPN 게이트웨이 및 연결 진단 합니다.

네트워크 감시자는 현재 hello 기능 뒤에 있습니다.

- [토폴로지](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -다양 한 상호 연결 및 연결 된 리소스 그룹에에서 네트워크 리소스 간에 네트워크 개요 표시 된 hello를 제공 합니다.
-   [변수 패킷 캡처](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) - 가상 컴퓨터의 내부 및 외부 패킷 데이터를 캡처합니다. 고급 필터링 옵션 및 수 tooset 시간 예 세밀 하 게 컨트롤 크기 제한 다양 한 기능을 제공 합니다. blob 저장소에 또는 로컬 디스크에.cap 형식 hello hello 패킷 데이터를 저장할 수 있습니다.
-   [IP 흐름 확인](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) - 흐름 정보의 5개 튜플 패킷 매개 변수(대상 IP, 원본 IP, 대상 포트, 원본 포트 및 프로토콜)에 따라 패킷을 허용하거나 거부하는지 확인합니다. Hello 패킷 보안 그룹에 의해 거부 되 면 hello 규칙과 hello 패킷 거부 그룹 반환 됩니다.
-   [다음 홉](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -hello toodiagnose 잘못 구성 된 모든 사용자 정의 경로 사용 하면 Azure 네트워크 패브릭에서 라우팅되는 패킷의 hello 다음 홉을 결정 합니다.
-   [보안 그룹 보기](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -VM에 적용 되는 hello 효과적이 고 적용 된 보안 규칙을 가져옵니다.
-   [NSG 흐름 로깅](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -네트워크 보안 그룹에 대 한 흐름 로그 허용 되거나 hello hello 그룹 보안 규칙에 의해 거부 된 toocapture 로그 관련된 tootraffic를 사용 합니다. hello 흐름은 5-튜플 정보 – 원본 IP, 대상 IP, 원본 포트, 대상 포트 및 프로토콜에 의해 정의 됩니다.
-   [가상 네트워크 게이트웨이 및 연결 문제 해결](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -hello 기능 tootroubleshoot 제공 가상 네트워크 게이트웨이 및 연결 합니다.
-   [구독 제한 네트워크](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -제한에 대해 tooview 네트워크 리소스 사용을 활성화 합니다.
-   [진단 로그 구성](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) – 단일 창 tooenable 제공 하거나 리소스 그룹의 네트워크 리소스에 대 한 진단 로그를 사용 하지 않도록 설정 합니다.

네트워크 감시자 tooconfigure 참조 하는 방법을 더 toolearn [네트워크 감시자 구성](https://docs.microsoft.com/azure/network-watcher/network-watcher-create)합니다.

## <a name="developer-operations-devops"></a>DevOps(개발자 작업)
이전 tooDevOps 응용 프로그램 개발 팀 담당 하는 소프트웨어 프로그램에 대 한 비즈니스 요구 사항을 수집 하 고 코드를 작성 했습니다. 그런 다음 별도 QA 팀 요구 사항이 충족 되었다고 고 릴리스 hello toodeploy 작업에 대 한 코드에 hello 프로그램은 격리 된 개발 환경에서 테스트 합니다. hello 배포 팀은 추가 네트워킹 및 데이터베이스와 같은 사일로 그룹으로 조각화 됩니다. 각 소프트웨어 프로그램은 "throw 시간 hello 벽 통해" tooan 독립 팀 병목 상태를 추가 합니다.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) 팀 toodeliver를 사용 하면 빠르고 저렴 한 비용 보다 안전 하 고 더 높은 품질 솔루션입니다. 고객은 소프트웨어 및 서비스를 사용할 때 동적이고 안정적인 환경을 기대합니다.  팀 소프트웨어 업데이트에 신속 하 게 반복 해야 합니다 hello 업데이트의 hello 영향이 측정 되 고 새로운 개발 반복 tooaddress 문제를 사용 하 여 신속 하 게 응답할 하거나 더 많은 가치를 제공 합니다.  Microsoft Azure와 같은 클라우드 플랫폼은 기존 병목 현상을 제거하고 인프라를 범용 상품화(commoditize)하도록 지원했습니다. 소프트웨어 hello 하지만 주요 변수 및 계수 비즈니스 결과에 따라 모든 비즈니스에서 reigns 합니다. 없거나 조직, 개발자, IT 작업자 수 또는 hello DevOps 이동 하지 않아야 합니다.

성숙한 DevOps 전문가 일부의 사항을 수행 하는 hello 채택 합니다. 이러한 사례 [사람들](https://www.visualstudio.com/learn/what-is-devops-culture/) hello 비즈니스 시나리오에 따라 다르게 tooform 전략입니다.  도구를 자동화할 수 있습니다 다양 한 사례 hello:

-   [Agile 계획 및 프로젝트 관리](https://www.visualstudio.com/learn/what-is-agile/) 기술을 tooplan 사용 되는 격리 작업을 스 프린트도, 팀 수용 작업량, 관리 하 고 팀에서 신속 하 게 toochanging 비즈니스 요구를 조정 합니다.
-   [버전 제어에 Git가 포함 된 일반적으로](https://www.visualstudio.com/learn/what-is-git/)hello world tooshare 소스에 있는 팀을 사용 하도록 설정 하 고 소프트웨어 개발 도구 tooautomate hello 릴리스 파이프라인와 통합 합니다.
-   [연속 통합](https://www.visualstudio.com/learn/what-is-continuous-integration/) 드라이브 hello 진행 중인 병합 하 고 초기 toofinding 결함을 유발 하는 코드를 테스트 합니다.  다른 이점으로 병합 문제를 해결하는 데 걸리는 시간을 줄이고 개발 팀에게 신속한 피드백을 제공할 수 있습니다.
-   [지속적인 업데이트](https://www.visualstudio.com/learn/what-is-continuous-delivery/) tooproduction 및 테스트 환경 도움말 조직 신속 하 게 버그를 수정 하 고 비즈니스 tooever 변경 응답 소프트웨어 솔루션의 요구 사항입니다.
-   응용 프로그램 상태뿐만 아니라 고객 사용을 위한 프로덕션 환경을 포함하여 실행 중인 응용 프로그램의 [모니터링](https://www.visualstudio.com/learn/what-is-monitoring/)을 사용하면 조직에서 가설을 세우고 전략을 신속하게 유효성을 검사하거나 반증할 수 있습니다.  자세한 데이터가 캡처되어 다양한 로깅 형식으로 저장됩니다.
-   [인프라 (IaC) 코드로](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) 이 hello 자동화 및 만들기의 유효성을 검사 하 고 안전 하 고 안정적인 응용 프로그램 호스팅 플랫폼을 제공 toohelp 네트워크 및 가상 컴퓨터 종료를 사용 하면 좋습니다.
-   [Microservices](https://www.visualstudio.com/learn/what-are-microservices/) 아키텍처는 사용된 tooisolate 비즈니스 사례 작은 다시 사용할 수 있는 서비스를 사용 합니다.  이 아키텍처는 확장성과 효율성을 가능하게 합니다.

## <a name="next-steps"></a>다음 단계
OMS 보안 및 감사 솔루션에 대해 자세히 toolearn hello 다음 문서 참조:

- [Operations Management Suite | Security & Compliance](https://www.microsoft.com/cloud-platform/security-and-compliance)
- [Operations Management Suite 보안 및 감사 솔루션에서 경고를 모니터링 및 응답 tooSecurity](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts)합니다.
- [Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources)
