---
title: "aaaAzure 작업 보안 모범 사례 | Microsoft Docs"
description: "이 문서에서는 Azure 운영 보안을 위한 모범 사례 모음을 제공합니다."
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
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Azure 운영 보안 모범 사례
Azure Operational 보안 toohello 서비스, 컨트롤 및 기능 사용 가능한 toousers 데이터, 응용 프로그램 및 Microsoft Azure에서 기타 자산을 보호 하기 위한 참조 합니다. Azure Operational 보안 고유 tooMicrosoft, Microsoft SDL Security Development Lifecycle (), Microsoft 보안 대응 센터 hello hello를 포함 하는 다양 한 기능을 통해 얻은 hello 정보를 통합 하는 프레임 워크에 만들어집니다. 프로그램 및 hello 사이버 안보 위협 상황의 심층 인식 합니다.

이 문서에서는 Azure 데이터베이스 보안 모범 사례 모음에 대해 설명합니다. 이들 모범 사례는 경험상 Azure 데이터베이스 보안 및 고객의 hello 경험을와 같은 직접 합니다.

각 모범 사례에 대해 다음과 같이 설명합니다.
-   어떤 hello 것이 좋습니다.
-   이유는 tooenable 최선의 방법을
-   Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴
- Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.

이 문서가 작성 된 hello 시 존재 하므로이 Azure 작업 보안 모범 사례 문서 합의 의견 및 Azure 플랫폼 기능 및 기능 집합에 기반 합니다. 의견 및 기술 시간이 지남에 따라 변경 하 고이 문서 됩니다. 이러한 변경 내용을 정기적으로 tooreflect에서 업데이트 합니다.

이 문서에서 다루는 Azure 운영 보안 모범 사례는 다음과 같습니다.

-   클라우드 인프라 모니터링, 관리 및 보호
-   ID 관리 및 SSO(Single Sign-On) 구현
-   요청 추적, 사용 추세 분석 및 문제 진단
-   중앙 집중식모니터링 솔루션을 사용한 서비스 모니터링 
-   방지 하 고 검색 toothreats 응답
-   종단 간 시나리오 기반 네트워크 모니터링
-   검증된 DevOps 도구를 사용한 배포 보안

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>클라우드 인프라 모니터링, 관리 및 보호
IT 운영 팀은 데이터 센터 인프라, 응용 프로그램 및 이러한 시스템의 hello 안정성과 보안을 비롯 한 데이터를 관리 하는 일을 담당 합니다. 그러나 복잡 한 IT 환경을 종종 증가 간에 보안 통찰력을 얻는 여러 보안 및 관리 시스템에서 조직 toocobble 함께 데이터가 필요 합니다.

[Microsoft OMS(Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)는 온-프레미스 및 클라우드 인프라를 관리하고 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.

[OMS 보안 및 감사 솔루션](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) 보안 문제의 hello 영향을 최소화 하는 데 사용할 수 있는 모든 리소스를 모니터링 하는 IT tooactively 수 있습니다. OMS 보안 및 감사에는 리소스 모니터링에 사용할 수 있는 보안 도메인이 있습니다.

OMS에 대 한 자세한 내용은 hello 문서를 읽어 보세요. [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)합니다.

방지 하 고 검색 toothreats, 응답 toohelp [Operations Management Suite (OMS) 보안 및 감사 솔루션](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) 수집 하 고 포함 하는 리소스에 대 한 데이터를 처리 합니다.

-   보안 이벤트 로그
-   Windows (ETW) 이벤트에 대한 이벤트 추적
-   AppLocker 감사 이벤트
-   Windows 방화벽 로그
-   고급 위협 분석 이벤트
-   기준 평가 결과
-   맬웨어 방지 평가 결과
-   업데이트/패치 평가 결과
-   Hello 에이전트에서 명시적으로 활성화 되는 Syslog 스트림


## <a name="manage-identity-and-implement-single-sign-on"></a>ID 관리 및 SSO(Single Sign-On) 구현
[Azure AD(Azure Active Directory)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다.

또한 [Azure AD](https://azure.microsoft.com/services/active-directory/)는 [다단계 인증](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), 장치 등록, 셀프 서비스 암호 관리, 셀프 서비스 그룹 관리, 권한 있는 계정 관리, 역할 기반 액세스 제어, 응용 프로그램 사용 모니터링, 광범위한 감사 및 보안 모니터링 및 경고를 포함하여 완벽한 [ID 관리 기능](https://docs.microsoft.com/azure/security/security-identity-management-overview) 제품군을 갖추고 있습니다.

기능을 수행 하는 hello 수 보안 클라우드 기반 응용 프로그램, IT 프로세스를 간소화 하, 비용 절감 도움말과 도움말 기업 규정 준수 목표를 충족 하는지 확인:

-   Hello 클라우드에 대 한 id 및 액세스 관리
-   사용자 액세스 tooany 클라우드 응용 프로그램을 단순화 합니다.
-   중요한 데이터 및 응용 프로그램 보호
-   직원을 위한 셀프 서비스 지원
-   Azure Active Directory와 통합

### <a name="identity-and-access-management-for-hello-cloud"></a>Hello 클라우드에 대 한 id 및 액세스 관리
Azure Active Directory (Azure AD)는 포괄적인 [id 및 액세스 관리 클라우드 솔루션](https://www.microsoft.com/cloud-platform/identity-management), 강력한 집합 기능 toomanage 사용자 및 그룹을 제공 하는 합니다. 보안 액세스 tooon 온-프레미스 및 클라우드 응용 프로그램, saas () 응용 프로그램으로 Office 365 및 많은 타사 소프트웨어와 같은 Microsoft 웹 서비스를 포함 하 여 수 있습니다.
Azure ad에서 id 보호 tooenable 참조 하는 방법을 더 toolearn [사용 하면 Azure Active Directory Id 보호](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable)합니다.

### <a name="simplify-user-access-tooany-cloud-app"></a>사용자 액세스 tooany 클라우드 응용 프로그램을 단순화 합니다.
[Single sign-on 사용](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) Windows, Mac, Android 및 iOS 장치에서 클라우드 응용 프로그램의 사용자 액세스 toothousands toosimplify 합니다. 사용자는 자신의 회사 자격 증명을 사용하여 개인 설정된 웹 기반 액세스 패널 또는 모바일 앱에서 응용 프로그램을 실행할 수 있습니다. SaaS 응용 프로그램 이외의 응용 프로그램 프록시 모듈 toogo hello Azure AD 사용 하 고 온-프레미스 웹 응용 프로그램 tooprovide 매우 안전한 원격 액세스 및 single sign-on을 게시 합니다.

### <a name="protect-sensitive-data-and-applications"></a>중요한 데이터 및 응용 프로그램 보호
사용 하도록 설정 [Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) 무단 tooprevent tooon 온-프레미스 액세스 및 추가 수준의 인증을 제공 하 여 클라우드 응용 프로그램입니다. 일치하지 않는 액세스 패턴을 식별하는 보안 모니터링, 경고 및 기계 학습 기반 보고서로 비즈니스를 보호하고 발생 가능한 위협을 완화합니다.

### <a name="enable-self-service-for-your-employees"></a>직원을 위한 셀프 서비스 지원
암호 다시 설정 및 그룹 만들기 및 관리와 같은 중요 한 작업 tooyour 직원을 위임 합니다. Azure AD를 통해 [셀프 서비스 암호 변경](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password) 및 재설정 및 셀프 서비스 그룹 관리를 활성화합니다.

### <a name="integrate-with-azure-active-directory"></a>Azure Active Directory와 통합
확장 [Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) 다른 온-프레미스 디렉터리 tooAzure AD tooenable single sign on에 대 한 모든 클라우드 기반 응용 프로그램 및입니다. 사용자 특성에는 모든 종류의 온-프레미스 디렉터리에서 클라우드 디렉터리를 자동으로 동기화 된 tooyour 수 있습니다.

Azure Active Directory의 통합에 대 한 자세한 toolearn 어떻게 tooenable, 문서를 참조 하세요 hello 및 [Azure Active Directory와 온-프레미스 디렉터리 통합](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)합니다.

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>요청 추적, 사용 추세 분석 및 문제 진단
[ 분석](https://docs.microsoft.com/azure/storage/storage-analytics)은 로깅을 수행하며 저장소 계정에 대한 메트릭 데이터를 제공합니다. 이 데이터 tootrace 요청을 사용 하 고, 사용 추세를 분석 하 고, 저장소 계정 문제를 진단할 수 있습니다.

저장소 분석 메트릭은 새 저장소 계정에서 기본적으로 활성화됩니다. 로깅을 사용 하도록 설정 하 고 메트릭 및 hello; Azure 포털에서에서 로깅 구성 자세한 내용은 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account)합니다. Hello REST API를 통해 프로그래밍 방식으로 Storage Analytics 하거나 hello 클라이언트 라이브러리를 사용할 수도 있습니다. 각 서비스에 대해 개별적으로 hello Set Service Properties 작업 tooenable Storage Analytics를 사용 합니다.

저장소 분석 및 기타 도구 tooidentify를 사용 하 여 상세 가이드에 대 한 진단, 및 Azure 저장소 관련 문제를 해결 하 고, 참조 [모니터, 진단 및 해결 Microsoft Azure 저장소](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting)합니다.

Azure Active Directory의 통합에 대 한 자세한 toolearn tooenable를 읽는 방법 및 hello 문서 [분석 설정 및 구성 저장소](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN)합니다.

## <a name="monitoring-services"></a>서비스 모니터링
클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다. 모니터링 없이 계속 응용 프로그램 데이터 tooensure 정상 상태에서 실행 되 고 제공 합니다. 또한 있습니다 toostave 잠재적 문제를 해제 하거나 문제를 해결 하십시오. 지난 수 있습니다. 또한 응용 프로그램에 대 한 모니터링 데이터 toogain 깊은 통찰력을 사용할 수 있습니다. 이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다.

### <a name="monitor-azure-resources"></a>Azure 리소스 모니터링
[Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) 는 Azure 리소스를 모니터링 하기 위한 단일 소스를 제공 하는 hello 플랫폼 서비스입니다. Azure 모니터를 사용 시각화, 쿼리, 경로, 보관 하 고 수 hello 메트릭 및 Azure의에서 리소스에서 오는 로그 작업을 수행 합니다. Hello 모니터 포털 블레이드를 사용 하 여이 데이터를 사용 하 여 작업할 수 [모니터 PowerShell Cmdlet](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [플랫폼 간 CLI](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), 또는 [Azure 모니터 REST Api](https://msdn.microsoft.com/library/dn931943.aspx)합니다.

### <a name="enable-autoscale-with-azure-monitor"></a>Azure Monitor에서 자동 크기 조정 사용
사용 하도록 설정 [Azure 모니터 자동 크기 조정](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) toovirtual 컴퓨터 크기 집합 (VMSS), 클라우드 서비스, 앱 서비스 계획 및 앱 서비스 환경에 적용 됩니다.

### <a name="manage-roles-permissions-and-security"></a>역할 권한 및 보안 관리
많은 팀 필요 toostrictly [액세스 toomonitoring 규제](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) 데이터 및 설정 합니다. 예를 들어 관리 되는 서비스 공급자를 사용할 경우 toogrant tooonly 자신의 능력 toocreate 제한 하면서 모니터링 데이터 액세스 권한을 (기술 지원 엔지니어, devops 엔지니어) 모니터링에 작업 하는 팀 멤버가 있는 경우 수정, 또는 리소스를 삭제 합니다.

Tooquickly 기본 제공 모니터링 RBAC 역할 tooa 사용자가 Azure에서 적용 또는 고유한 사용자 지정 역할 모니터링 제한 된 권한이 필요로 하는 사용자에 대 한 빌드 방법을 표시 합니다. Azure 모니터와 관련 된 리소스에 대 한 보안 고려 사항에 설명 합니다 하며 포함 방법 toohello 데이터 액세스를 제한할 수 있습니다.

## <a name="prevent-detect-and-respond-toothreats"></a>방지 하 고 검색 toothreats 응답
보안 센터 위협 요소 탐지 자동으로 Azure 리소스, hello 네트워크 및 연결 된 파트너 솔루션의 보안 정보를 수집 하 여 작동 합니다. 종종 tooidentify 위협 여러 소스의 정보를 상호 연결 하는이 정보를 분석 하 고 합니다. 보안 경고 사항 tooremediate 위협 hello 하는 방법에 대 한 권장 사항과 함께 보안 센터에 우선 순위입니다.

-   Azure 구독의 [보안 정책을 구성](https://docs.microsoft.com/azure/security-center/security-center-policies)합니다.
-   사용 하 여 hello [보안 센터의 권장 사항을](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp Azure 리소스를 보호 합니다.
-   현재 [보안 경고](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)를 검토하고 관리합니다.

[Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro) 사용 방지를 감지 하 고 및 toothreats 파악할을 사용 하 여 응답을 제어할 수 hello Azure 리소스의 보안 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

보안 센터 사용 하기 쉬운이 고 효과적인 위협 tooAzure 제공 된 예방, 감지, 및 대처 기능을 제공 합니다. 주요 기능:

-   클라우드 보안 상태 파악
-   클라우드 보안 제어
-   통합 클라우드 보안 솔루션을 쉽게 배포
-   위협 감지 및 신속한 대응

### <a name="understand-cloud-security-state"></a>클라우드 보안 상태 파악
Azure 보안 센터를 사용 하 여 tooget 모든 Azure 리소스의 보안 상태 hello의 중앙 보기. 한 눈에 hello 적절 한 보안 제어에 올바르게 구성 고 주의가 필요한 모든 리소스를 신속 하 게 식별 되었는지 확인

### <a name="take-control-of-cloud-security"></a>클라우드 보안 제어
정의 [보안 정책](https://docs.microsoft.com/azure/security-center/security-center-policies) tooyour 회사에 따라 Azure 구독의 클라우드 보안 요구 사항, 맞는 toohello 유형의 응용 프로그램 또는 hello 데이터의 민감도 각 구독에 있습니다. 필요한 컨트롤을 구현 하는의 hello 프로세스를 통해 정책 기반 권장 사항을 tooguide 리소스 소유자를 사용 하 여-클라우드 보안을 hello 예측을 수행 합니다.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>통합 클라우드 보안 솔루션을 쉽게 배포
업계 최고 방화벽 및 맬웨어 방지 프로그램 등 Microsoft 및 관련 파트너의 [보안 솔루션을 활성화합니다](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).  사용 하 여 프로 비전 toodeploy 보안 솔루션을 간소화-네트워킹도 변경 내용이 구성 됩니다. 파트너 솔루션의 보안 이벤트는 분석 및 경고를 위해 자동으로 수집됩니다.

### <a name="detect-threats-and-respond-fast"></a>위협 감지 및 신속한 대응
분석 지향적이며 통합적인 접근 방식으로 현재와 미래의 클라우드 위협을 앞서 대비하세요. Security Center는 Microsoft의 글로벌 [위협 정보](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) 및 전문 지식을 Azure 배포의 클라우드 보안 관련 이벤트에 대한 통찰력과 결합하여 조기에 실제적인 위협을 감지하도록 지원하므로 가양성을 줄일 수 있습니다. 클라우드 보안 경고는 관련된 이벤트 및 영향을 받는 리소스를 포함 하 여 hello 공격 캠페인에 대 한 정보를 제공 하 고 tooremediate 발급 하 고 신속 하 게 복구 하는 방법을 제안 합니다.

## <a name="end-to-end-scenario-based-network-monitoring"></a>종단 간 시나리오 기반 네트워크 모니터링
고객은 VNet, ExpressRoute, Application Gateway, 부하 분산 장치 등과 같은 다양한 개별 네트워크 리소스를 오케스트레이션하고 구성하여 Azure에서 종단 간 네트워크를 구축합니다. 모니터링 하는 것은 각 hello 네트워크 리소스에 사용할 수 있습니다.

[네트워크 감시자](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) toomonitor 수 있는 지역 서비스 이며에서 및 Azure에서 네트워크 시나리오 수준에서 상태를 진단 합니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>패킷 캡처를 사용하여 원격 네트워크 모니터링 자동화
모니터링 하 고 tooyour Vm (가상 컴퓨터) 네트워크 감시자를 사용 하 여 로그인 하지 않고 네트워킹 문제를 진단 합니다. 트리거 [패킷 캡처](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) 으로 경고를 설정 하 고 hello 패킷 수준에서 액세스 tooreal 타임 성능 정보를 얻는 합니다. 문제를 발견하면 자세히 조사하여 더 정확히 진단할 수 있습니다.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>흐름 로그를 사용하여 네트워크 트래픽 이해
[네트워크 보안 그룹 흐름 로그](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)를 사용하여 네트워크 트래픽 패턴을 더 자세히 이해합니다. 흐름 로그에서 제공하는 정보를 사용하여 준수, 감사 및 네트워크 보안 프로필 모니터링에 필요한 데이터를 수집할 수 있습니다.

### <a name="diagnose-vpn-connectivity-issues"></a>VPN 연결 문제 진단
네트워크 감시자 제공 기능을 너무 hello[가장 일반적인 프로그램 VPN 게이트웨이 및 연결 문제를 진단](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity)합니다. Hello 로그 만든된 toohelp 추가 조사를 자세한 tooidentify hello 문제 뿐만 아니라 toouse 수 있도록 합니다.

방법에 대 한 자세한 toolearn tooconfigure 네트워크 감시자 어떻게 tooenable, 문서를 참조 하세요 hello 및 [네트워크 감시자 구성](https://docs.microsoft.com/azure/network-watcher/network-watcher-create)합니다.

## <a name="secure-deployment-using-proven-devops-tools"></a>검증된 DevOps 도구를 사용한 배포 보안
Hello 목록의 Azure DevOps 사례 생산성과 효율성을 기업 및 팀을 사용 하면이 Microsoft Cloud 공간에서의 일부입니다.

-   **인프라 (IaC) 코드로:** 코드로 인프라는 기술 집합 이며 방법으로, IT 전문가 들 hello 일 tooday 빌드 및 모듈식 인프라의 관리와 관련 된 hello 부담을 제거 합니다. IT 전문가 toobuild 있으며 소프트웨어 개발자가 구축 하 고 응용 프로그램 코드를 유지 관리 하는 방법과 같은 방식으로 최신 서버 환경을 유지 관리 합니다. Azure에 있는 [Azure 리소스 관리자]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) 있습니다 tooprovision 선언적 템플릿을 사용 하 여 응용 프로그램입니다. 단일 템플릿에서 여러 서비스를 해당 종속성과 함께 배포할 수 있습니다. Hello를 사용 하 여 동일한 템플릿 toorepeatedly hello 응용 프로그램 수명 주기의 다른 단계 동안 응용 프로그램을 배포 합니다.
-   **연속 통합 및 배포:** 너무 Visual Studio Online 팀 프로젝트를 구성할 수 있습니다[자동으로 빌드 및 배포](https://www.visualstudio.com/docs/build/overview) tooAzure 웹 앱 또는 클라우드 서비스입니다. VSO 빌드 tooAzure 모든 코드 체크 인 후에 작업을 수행한 후 hello 이진 파일을 자동으로 배포 합니다. hello 여기에서 설명 하는 패키지 빌드 프로세스는 Visual Studio에서 해당 toohello 패키지 명령을 이며 hello 게시 단계가 Visual Studio에서 해당 toohello 게시 명령을 합니다.
-   **릴리스 관리:** Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) 여러 단계로 이루어진 배포를 자동화 하 고 hello 관리 릴리스 프로세스 가장 좋은 방법입니다. 신속 하 게, 쉽고 자주 파이프라인 toorelease를 관리 되는 연속 배포를 만듭니다. Release Management를 통해 릴리스 프로세스 자동화 수준을 높이고 사전 정의된 승인 워크플로를 갖출 수 있습니다. 온-프레미스 및 toohello 배포 클라우드, 확장 및 필요에 따라 사용자 지정 합니다.
-   **앱 성능 모니터링:** 문제를 감지하고, 문제를 해결하고, 지속적으로 응용 프로그램을 개선합니다. 라이브 응용 프로그램의 모든 문제를 신속하게 진단합니다. 사용자가 어떤 작업을 하는지 확인합니다. 구성 되 고 쉬운 JS 코드 및 webconfig 항목을 추가 하 고 hello에 대 한 세부 정보를 모두 사용 하는 hello 포털에서 초 내 결과 확인 합니다. [App insights](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) 문제 및 수정에 대 한 빠른 감지에 대 한 높일 수 있습니다.
-   **부하 테스트 및 자동 크기 조정:** 앱 tooimprove 배포 품질 toomake 앱 항상는 사용할 수 없거나 최신 toocater toohello 비즈니스 요구에 성능 문제를 확인할 수 있습니다. 앱이 다음 번 출시나 마케팅 캠페인을 위한 트래픽을 처리할 수 있게 합니다. Visual Studio Online를 통해 거의 순식간에 클라우드 기반 [부하 테스트](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing)를 실행하기 시작합니다.

## <a name="next-steps"></a>다음 단계
- [Azure 운영 보안](https://docs.microsoft.com/azure/security/azure-operational-security)에 대한 자세한 정보
- 더 많은 tooLearn [Operations Management Suite | 보안 및 규정 준수](https://www.microsoft.com/cloud-platform/security-and-compliance)합니다.
- [Operations Management Suite 보안 및 감사 솔루션 시작](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)
