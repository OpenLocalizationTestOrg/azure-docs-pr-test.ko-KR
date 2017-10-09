---
title: "aaaAzure 고급 위협 요소 탐지 | Microsoft Docs"
description: "ID 보호 및 해당 기능에 대해 알아봅니다."
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
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Azure 고급 위협 검색
## <a name="introduction"></a>소개

### <a name="overview"></a>개요

Microsoft는 일련의 백서, 보안 개요, 모범 사례 및 검사 목록이 tooassist Azure 개발 하는 다양 한 보안 관련 기능에서 사용할 수 있는 및 주변 hello Azure 플랫폼에 대 한 고객 hello 합니다. hello 항목 폭과 깊이 기준으로 다양 하 고 정기적으로 업데이트 됩니다. 이 문서는 hello 추상 섹션 다음에 요약 된 것 처럼 해당 시리즈의 일부는입니다.

### <a name="azure-platform"></a>Azure 플랫폼

Azure는 hello 광범위 한 프로그래밍 언어, 프레임 워크, 도구, 데이터베이스 및 장치 운영 체제를 선택할 수 있는 공용 클라우드 서비스 플랫폼입니다.
Hello 다음 프로그래밍 언어를 지원 합니다.
-   Docker 통합으로 Linux 컨테이너를 실행합니다.
-   JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드합니다.
-   iOS, Android 및 Windows 장치용 백 엔드를 빌드합니다.

Azure 공용 클라우드 서비스는 hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다.

조직 tooa 공용 클라우드로 마이그레이션하는 경우 해당 조직의 책임 tooprotect 데이터 이며 보안 및 hello 시스템 주위 거 버 넌 스를 제공 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고 비즈니스는 고유한 보안 요구를 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. Azure에는 응용 프로그램 배포의 보안 toomeet hello 요구 사항을 사용자 지정 및 다양 한 옵션 tooconfigure 제공 합니다. 이 문서는 이러한 요구 사항을 충족하는 데 도움이 됩니다.

### <a name="abstract"></a>요약

Microsoft Azure는 Azure Active Directory, Azure OMS(Operations Management Suite) 및 Azure Security Center와 같은 서비스를 통해 고급 위협 검색 기능을 기본적으로 제공하고 있습니다. 이 컬렉션 보안 서비스와 기능을 Azure 배포 내에서 발생 하는 작업을 쉽고 빠른 방법 toounderstand에 제공 합니다.

이 백서에서는 안내 합니다 "Microsoft Azure 방법" hello 진단 위협 취약점으로 및 hello 위험을 분석 하 여 서버와 다른 Azure 리소스에 대해 대상으로 하는 hello 악의적인 작업 합니다. 이렇게 하면 식별 tooidentify hello 방법 및 사용 하 여 취약성 관리 hello Azure 플랫폼 및 고객 관련 보안 서비스와 기술에서 솔루션에 최적화 된 합니다.

이 백서 Azure 플랫폼 및 고객 관련 컨트롤의 hello 기술 이며 tooaddress Sla, 모델 및 DevOps 사례 고려 사항 가격을 시도 하지 않습니다.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory ID 보호

![Azure Active Directory ID 보호](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory Id 보호](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) hello의 기능이 [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) hello 위험 이벤트와 조직에 영향을 미치는 잠재적 보안 문제에 대 한 개요를 제공 하는 버전 id입니다. Microsoft 10 년 이상에 대 한 클라우드 기반 id 보안 되었습니다에 및 Azure AD Identity Protection을 사용한 Microsoft가 자사의 이러한 동일한 보호 시스템 사용할 수 있는 tooenterprise 고객 합니다. ID 보호는 [Azure AD의 비정상적인 활동 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)를 통해 제공되는 기존 Azure AD의 변칙 검색 기능을 사용하고, 실시간으로 비정상을 검색할 수 있는 새로운 위험 이벤트 유형을 도입하고 있습니다.

Id 보호 적응 기계 학습 알고리즘 및 추론 toodetect 비정상 보고서 및 id가 손상 된 나타낼 수 있는 위험 이벤트를 사용 합니다. 이 데이터를 사용 하 여 Id 보호 이러한 위험 이벤트 보고서 및 tooinvestigate 수 있도록 하는 경고를 생성 적절 한 조치 업데이트 관리 또는 완화 합니다.

하지만 Azure Active Directory ID 보호는 모니터링 및 보고 도구 이상입니다. 위험 이벤트에 따라, Identity Protection을 각 사용자에 대 한 사용자 위험 수준을 계산, tooconfigure 위험 기반 정책 tooautomatically 보호 hello 수 있게 해 주는 조직의 id입니다.

이러한 위험 기반 정책을 추가할 tooother [조건부 액세스 제어](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) Azure Active Directory에서 제공 하 고 [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), 자동으로 받거나 지연 될 수를 포함 하는 적응형 수정 작업을 제공 합니다. 암호 재설정 및 multi-factor authentication이 적용 됩니다.

### <a name="identity-protections-capabilities"></a>ID 보호 기능

Azure Active Directory ID 보호는 모니터링 및 보고 도구 이상입니다. tooprotect 조직의 id를 지정 된 위험 수준에 도달 했을 때 toodetected 문제를 자동으로 응답 하는 위험 기반 정책을 구성할 수 있습니다. 이러한 정책에서는 또한 tooother 조건부 Azure Active Directory 및 EMS에서 제공 하는 컨트롤에 액세스할 자동으로 차단 하거나 암호 재설정 및 다단계 인증 적용을 포함 한 적응 업데이트 관리 작업을 시작 합니다.

Azure Id 보호 하도록 도와주는 hello 방식 중 몇 가지 사용자 계정을 보호 하 고 id로는 합니다.

[위험 이벤트 및 위험한 계정 검색:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   기계 학습 및 추론 규칙을 사용하여 6가지 위험 이벤트 유형 검색
-   사용자 위험 수준 계산
-   사용자 지정 권장 사항을 tooimprove 제공 취약점을 강조 표시 하 여 전반적인 보안 상태

[위험 이벤트 조사:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   위험 이벤트에 대한 알림 보내기
-   관련된 컨텍스트 정보를 사용하여 위험 이벤트 조사
-   Tootrack 조사 기본 워크플로 제공합니다.
-   쉽게 액세스할 수 tooremediation 암호 다시 설정 하는 등의 작업

[위험 기준 조건부 액세스 정책:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   정책 toomitigate 위험한 로그인 하 여 로그인을 차단 하거나 다단계 인증 챌린지를 요구 합니다.
-   정책 tooblock 또는 보안 위험 사용자 계정
-   Multi-factor authentication에 대해 정책 toorequire 사용자 tooregister

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD PIM(Privileged Identity Management)

[Azure AD(Active Directory) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)를 사용하는 경우

![Azure AD Privileged Identity Management](./media/azure-threat-detection/azure-threat-detection-fig2.png)

조직 내 액세스를 관리, 제어 및 모니터링할 수 있습니다. Azure AD에서 액세스 tooresources 및 Microsoft Intune 또는 Office 365와 같은 다른 Microsoft 온라인 서비스에이 포함 됩니다.

Azure AD Privileged Identity Management를 통해 다음을 할 수 있습니다.

-   경고가 발생 하 고 Azure AD 관리자와 "just in time" 관리자 액세스 tooMicrosoft와 같은 Office 365 및 Intune 온라인 서비스 보고

-   관리자 액세스 기록 및 관리자 할당 변경에 대한 보고서 가져오기

-   액세스 tooa 권한 있는 역할에 대 한 경고를 받으려면

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft OMS(Operations Management Suite)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)는 온-프레미스 및 클라우드 인프라를 관리하고 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. OMS는 클라우드 기반 서비스로 구현되므로 인프라 서비스에 대한 최소한의 투자로 빠르게 실행할 수 있습니다. 새로운 보안 기능을 자동으로 제공하므로 지속적인 유지 관리 및 업그레이드 비용이 절감됩니다.

또한 tooproviding 중요 한 서비스 자체를 OMS에 통합할 수 있습니다 System Center 구성 요소와 같은 [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend hello에 보안 되어 기존 관리 투자를 클라우드입니다. System Center 및 OMS 수 협력 전체 하이브리드 관리 환경을 tooprovide 합니다.

### <a name="holistic-security-and-compliance-posture"></a>전체적인 보안 및 규정 준수 상태

hello [OMS 보안 및 감사 대시보드](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) 제공 한 포괄적인 뷰를 조직의 IT 보안 상태에는 주의가 필요한 주요 문제에 대 한 기본 제공 검색 쿼리. hello 보안 및 감사 대시보드는 모든 항목에 대 한 홈 화면 hello 관련 OMS에서 toosecurity입니다. 컴퓨터의 hello 보안 상태에 대 한 개략적인 정보를 제공합니다. 지난 24 시간, 7 일 hello에서 모든 이벤트 또는 다른 사용자 지정 시간 프레임 hello 기능 tooview도 있습니다.

신속 하 고 쉽게 이해 하는 OMS 대시보드 도움말 hello 포함 한 IT 작업의 hello 컨텍스트 내에서 모든 환경의 전반적인 보안 환경을: 소프트웨어 업데이트 평가, 맬웨어 방지 평가 및 구성 기준을 합니다. 보안 로그 데이터에 쉽게 액세스할 수는 또한 toostreamline hello 보안 및 규정 준수 프로세스를 감사 합니다.

hello OMS 보안 및 감사 대시보드는 4 개의 주요 범주로 구성 되어 있습니다.

![OMS 보안 및 감사 대시보드](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **보안 도메인:** 이 영역의 수 toofurther 됩니다 시간에 따른 보안 레코드를 탐색, 맬웨어 평가 액세스, 보안 이벤트를 평가, 네트워크 보안, id 및 액세스 정보, 컴퓨터를 업데이트, 빠르게 tooAzure 보안 센터 대시보드에 액세스 합니다.

-   **주목할 만한 문제:** 이 옵션을 통해 tooquickly 수 hello 수가 활성 문제를 식별 하 고 이러한 문제의 심각도 hello 합니다.

-   **검색 (미리 보기):** 리소스에 대해 수행 하는 대로 보안 경고를 시각화 하 여 tooidentify 공격 패턴 수 있도록 합니다.

-   **위협 인텔리전스:** hello 총 아웃 바운드 악성 IP 트래픽이, hello 악의적인 위협 유형 및 이러한 Ip에서 생성 되는 위치를 보여 주는 지도 서버 수를 시각화 하 여 tooidentify 공격 패턴 수 있도록 합니다.

-   **일반적인 보안 쿼리:** 이 옵션은 사용할 수 있는 toomonitor 환경 쿼리 있습니다 hello 가장 일반적인 보안의 목록을 제공 합니다. 이러한 쿼리 중 하나를 클릭 하는 경우 해당 쿼리에 대 한 hello 결과으로 hello 검색 블레이드를 문서가 열립니다.

### <a name="insight-and-analytics"></a>Insight and Analytics
Hello 가운데에서 [로그 분석](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) hello Azure 클라우드에 호스트 된 hello OMS 리포지토리에 됩니다.

![Insight and Analytics](./media/azure-threat-detection/azure-threat-detection-fig4.png)

데이터 원본 구성 및 솔루션 tooyour 구독을 추가 하 여 연결 된 원본에서 hello 저장소로 데이터를 수집 합니다.

![subscription](./media/azure-threat-detection/azure-threat-detection-fig5.png)

데이터 원본 및 솔루션 각 만들어집니다 다른 레코드 유형을 고유 속성 집합이 있지만 쿼리 toohello 리포지토리에 함께 분석 될 수 있습니다. 이렇게 하면 서로 다른 소스에 의해 수집 된 여러 종류의 데이터와 같은 도구와 방법을 toowork toouse hello 있습니다.


대부분의 로그 분석와의 상호 작용 모든 브라우저에서 실행 되 고 액세스 tooconfiguration 설정 하 고 여러 도구 tooanalyze 및 act에서 수집 된 데이터를 제공 하는 hello OMS 포털을 통해 수행 됩니다. Hello 포털에서 사용할 수 있습니다 [검색 로그](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) tooanalyze 수집 된 데이터를 쿼리를 생성 하는 경우 [대시보드](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), 가장 중요 한 검색 및 그래픽보기가포함된사용자지정할수있습니다[솔루션](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), 추가 기능 및 분석 도구를 제공 합니다.

![분석 도구](./media/azure-threat-detection/azure-threat-detection-fig6.png)

솔루션 추가 기능 tooLog 분석 합니다. 주로 hello 클라우드에서 실행 및 hello OMS 리포지토리에 수집 된 데이터의 분석 기능을 제공 합니다. 새 레코드 종류 toobe 수집 된 로그 검색 함께 또는 추가 사용자 인터페이스를 OMS 대시보드에 hello hello 솔루션에서 제공 하 여 분석할 수 있는 정의할 수도 있습니다.
hello 보안 및 감사는 이러한 종류의 솔루션의 예시입니다.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>자동화 및 제어: 보안 구성 표류에 대한 경고

Azure 자동화는 PowerShell을 기반으로 하 고 hello Azure 클라우드에에서 실행 하는 runbook으로 관리 프로세스를 자동화 합니다. Runbook의 서버 로컬 데이터 센터 toomanage 로컬 리소스에도 실행할 수 있습니다. Azure Automation은 PowerShell DSC(필요한 상태 구성)를 사용하여 구성 관리를 제공합니다.

![Azure Automation](./media/azure-threat-detection/azure-threat-detection-fig7.png)

만들거나 수 있습니다 및 Azure에서 호스트 되는 DSC 리소스를 관리 및 toocloud 및 온-프레미스 시스템 toodefine를 적용 하 고 자동으로 구성을 적용 보고서 가져오기 드리프트 시 toohelp 정책 내에서 보안 구성 남아 있는지 확인 합니다.

## <a name="azure-security-center"></a>Azure 보안 센터

Azure Security Center는 Azure 리소스를 보호하는 데 도움이 됩니다. Azure 구독에서 통합된 보안 모니터링 및 정책 관리를 제공합니다. Hello 서비스 내에서 수 있다면 toodefine 정책을 뿐만 아니라 Azure 구독에 대 한도 대 한 [리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)이므로 보다 세부적인 할 수 있습니다.

![Azure 보안 센터](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Microsoft 보안 연구원 위협에 대 한 lookout hello에 지속적으로 있습니다. 액세스 tooan 과다 집합 hello 클라우드 및 온-프레미스 Microsoft의 글로벌 상태에서 확보 하는 원격 분석을 포함 합니다. 이 광범위 하 고 다양 한 컬렉션 데이터 집합의 온라인 서비스와 해당 온-프레미스 소비자 및 엔터프라이즈 제품에서 Microsoft toodiscover 새 공격 패턴 및 추세를 사용합니다.

따라서 공격자가 새롭고 점차 정교해지는 악용을 방출함에 따라 Security Center에서 검색 알고리즘을 빠르게 업데이트할 수 있습니다. 이 방법을 사용하면 빠르게 변하는 위협 환경과 보조를 맞추며 대응할 수 있습니다.

![보안 센터](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

보안 센터 위협 요소 탐지 자동으로 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 수집 하 여 작동 합니다.  이 정보를 tooidentify 위협 여러 소스의 정보를 상관 관계를 분석 합니다.
보안 경고 사항 tooremediate 위협 hello 하는 방법에 대 한 권장 사항과 함께 보안 센터에 우선 순위입니다.

보안 센터는 서명 기반 방식을 뛰어 넘는 고급 보안 분석을 사용합니다. 빅 데이터의 문제를 해결 하면 및 [기계 학습](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) 기술은 것이 불가능 한 tooidentify 수동 방법을 사용 하 고 hello를 예측 하는 위협을 감지 – hello 전체 클라우드 패브릭에서 사용 되는 tooevaluate 이벤트 공격 발전 합니다. 이러한 보안 분석 hello 다음이 포함 됩니다.

### <a name="threat-intelligence"></a>위협 인텔리전스

Microsoft는 방대한 글로벌 위협 인텔리전스가 있습니다.
Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes 단위 (DCU), Microsoft 보안 대응 센터 (MSRC) 등의 여러 원본에서 원격 분석에서 이동합니다.

![위협 인텔리전스](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

또한 연구원은 주요 클라우드 서비스 공급자 간에 공유 되 고 제 3 자에서 toothreat intelligence 피드를 구독 하는 위협 인텔리전스 정보를 받습니다. Azure 보안 센터가 정보 tooalert צ ְ ײ 알려진된 믿지 못할 자에서 toothreats 있습니다. 일부 사례:

-   **기계 학습의 전원-hello을 활용 하 여** Azure 보안 센터에 액세스 tooa 방대한 분량의 데이터가 될 수 있는 클라우드 네트워크 활동에 대 한 Azure 배포를 대상으로 하는 toodetect 위협 요소를 사용 합니다. 예:

-   **Brute Force 검색-** 기계 학습 사용 되는 toocreate SSH, RDP, 및 SQL 포트에 대 한 무차별 암호 대입 공격 toodetect 수 있는 원격 액세스 시도 기록 패턴입니다.

-   **아웃 바운드 DDoS 및 봇 네트 감지** -클라우드 리소스를 대상으로 하는 공격 일반적인 목표 toouse hello 계산의 거듭제곱이 이러한 리소스 tooexecute 다른 공격입니다.

-   **새 동작 분석 서버 및 Vm-** 공격자가 검색 방지, 지 속성을 확인 하 고, 그리고 하는 동안 다양 한 기술 tooexecute 악성 코드가 해당 시스템에 서버 또는 가상 컴퓨터를 손상 되 면 사용 하도록 보안 제어입니다.

-   **Azure SQL 데이터베이스 위협 검색-** 한 문제가 될 수 있는 비정상 데이터베이스 작업을 식별 하는 Azure SQL 데이터베이스 위협 검색 tooaccess 또는 악용 데이터베이스를 시도 합니다.

### <a name="behavioral-analytics"></a>동작 분석

동작 분석은 분석 하 고 알려진된 패턴의 tooa 컬렉션 데이터를 비교 하는 기술입니다. 그러나 이러한 패턴은 단순한 서명이 아닙니다. 데이터 집합이 적용 된 toomassive는 복잡 한 기계 학습 알고리즘을 통해 결정 됩니다.

![동작 분석](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


또한 전문 분석가가 악의적인 행동을 신중하게 분석하여 결정합니다. Azure 보안 센터 분석 로그 가상 컴퓨터, 가상 네트워크 장치 로그, 패브릭 로그, 크래시 덤프 및 기타 소스에 따라 동작 분석 tooidentify 손상 리소스를 사용할 수 있습니다.

또한 광범위 한 캠페인의 증거를 지원 하기 위한 다른 신호 toocheck와의 상관 관계는 합니다. 이 상관 관계가 손상의 설정 된 표시기와 일치 하는 tooidentify 이벤트 수 있습니다.

일부 사례:
-   **의심 스러운 프로세스 실행:** 공격자가 몰래 몇 가지 기술을 tooexecute 악성 소프트웨어를 사용 합니다. 예를 들어 공격자 수 제공 맬웨어 hello 승인 된 시스템 파일 이름이 같은 하지만 이러한 파일을 대체 위치에에서 배치, 무해 파일 또는 true 마스크 hello 파일의 확장명와 같은 매우 이름을 사용 합니다. 보안 센터 모델 프로세스 동작 및 모니터 같은 실행 toodetect 이상 값 처리합니다.

-   **맬웨어 및 악용 시도 숨겨진:** 정교한 맬웨어 toodisk 작성 되지 하거나 디스크에 저장 하는 소프트웨어 구성 요소를 암호화 하 여 기존 맬웨어 방지 제품을 피할 수 있습니다. 그러나 이러한 맬웨어 수 감지할 수 메모리 분석을 사용 하 여 hello 맬웨어 메모리 toofunction에 추적을 두어야 합니다. 소프트웨어 충돌, 크래시 덤프는 hello 충돌 hello 시 메모리의 일부를 캡처합니다. Hello 크래시 덤프의 hello 메모리를 분석 하 여 Azure 보안 센터 수 검색 기술을 tooexploit 취약점 소프트웨어에서 사용 되는, 기밀 데이터를 액세스 및 부정적 hello 성능에 영향을 주지 않고 손상 된 컴퓨터 내에서 유지 컴퓨터입니다.

-   **내부 정찰 및 이동 하 여 측면:** 손상 된 네트워크 및 찾기/수집 중요 한 데이터에 toopersist, 종종 공격자가 손상 hello에서 가로로 toomove 컴퓨터 tooothers 내에서 동일한 네트워크 hello 합니다. 보안 센터 프로세스를 모니터링 하 고 로그인 활동 toodiscover tooexpand 원격 명령 실행, 네트워크 검색 및 계정 열거와 같은 hello 네트워크는 공격자의 발판을 마련 합니다.

-   **PowerShell 스크립트 악의적인:** PowerShell을 다양 한 용도로 대상 가상 컴퓨터에서 공격자가 tooexecute 악성 코드에서 사용할 수 있습니다. 보안 센터는 의심스러운 활동의 증거에 대해 PowerShell 작업을 검사합니다.

-   **공격을 나가는:** 공격자는 종종 이러한 리소스 toomount 추가 공격을 사용 하 여 hello 목표를 사용 하 여 클라우드 리소스 대상입니다. 손상 된 가상 컴퓨터, 예를 들어 수 다른 가상 컴퓨터에 대 한 사용된 toolaunch 무차별 암호 대입 공격 이거나 스팸 메일을 보낼 또는 열려 있는 포트 및 hello 인터넷에서 다른 장치를 검색 합니다. 컴퓨터를 적용 하 여 toonetwork 트래픽 학습, 보안 센터 감지할 수 아웃 바운드 네트워크 통신 hello norm를 초과 하는 경우. 스팸 때, 보안 센터 hello 메일을 가능성이 있는지를 Office 365 toodetermine에서 정보를 바탕으로 트래픽 비정상적인 전자 메일도 상관 불법 또는 올바른 전자 메일 캠페인의 hello 결과입니다.

### <a name="anomaly-detection"></a>이상 감지

또한 azure 보안 센터 비정상 탐지 tooidentify 위협 요소를 사용합니다. (있음 큰 데이터 집합에서 파생 된 알려진된 패턴에 따라 다름) 대비 toobehavioral 분석에서 변칙 검색 더 "개인화 된" 및 특정 tooyour 배포 하는 기준에 중점을 둡니다. 기계 학습 배포에 대해 적용 된 toodetermine 정상적인 작업을 하 고 규칙은 보안 이벤트를 나타낼 수 있는 생성 된 toodefine 이상 값 조건을 합니다. 예를 들면 다음과 같습니다.

-   **인바운드 RDP/SSH 무차별 암호 대입 공격**: 배포에는 매일 많은 로그인이 있는 바쁜 가상 컴퓨터와 로그인이 거의 없는 다른 가상 컴퓨터가 있을 수 있습니다. Azure 보안 센터 이러한 가상 컴퓨터에 대 한 초기 로그인 활동을 확인 하 고 hello 일반적인 로그인 동작 관련 컴퓨터 학습 toodefine를 사용 합니다. Hello 기준선에 대해 정의 된 모든 일치 하는 경우 로그인와 관련 된 특성을 다음 경고가 생성 될 수 있습니다. 다시, 기계 학습은 무엇이 중요한지를 결정합니다.

### <a name="continuous-threat-intelligence-monitoring"></a>연속 위협 인텔리전스 모니터링

Azure 보안 센터 보안 연구 및 데이터 과학 전반에 걸쳐 팀 hello world hello 위협 환경에서 변경 내용을 지속적으로 모니터링 하는 작동 합니다. 이 이니셔티브 다음 hello 포함 됩니다.

-   **위협 인텔리전스 모니터링**: 위협 인텔리전스에는 기존 또는 새로운 위협에 대한 메커니즘, 표시기, 영향 및 조치 가능한 조언이 포함됩니다. 이 정보는 hello 보안 커뮤니티에서 공유 및 Microsoft 내부 및 외부 소스에서 위협 인텔리전스 피드를 지속적으로 모니터링 합니다.

-   **신호 공유**: Microsoft의 클라우드 및 온-프레미스 서비스, 서버 및 클라이언트 끝점 장치의 광범위한 포트폴리오에 대한 보안 팀의 정보를 공유하고 분석합니다.

-   **Microsoft 보안 전문가**: 법정 분석 및 웹 공격 검색과 같은 전문 보안 분야에서 Microsoft 팀과 지속적인 관계를 유지하며 활동합니다.

-   **검색 튜닝:** 알고리즘 실제 고객 데이터 집합에 대해 실행 되 고 보안 연구원 고객 toovalidate hello 결과 함께 작동 합니다. 여러 참과 거짓 긍정은 사용 되는 toorefine 기계 학습 알고리즘입니다.

이러한 결합 된 활동에서 즉시 얻을 수 있는 새로운 기능과 향상 된 검색에 누적 – tootake 있습니다에 대 한 작업이 없습니다.

## <a name="advanced-threat-detection-features---other-azure-services"></a>고급 위협 검색 기능 - 다른 Azure 서비스

### <a name="virtual-machine-microsoft-antimalware"></a>Virtual Machine: Microsoft 맬웨어 방지 프로그램

[Microsoft 맬웨어 방지](https://docs.microsoft.com/azure/security/azure-security-antimalware) Azure 응용 프로그램 및 테 넌 트 환경에 대 한 단일 에이전트 솔루션에 대 한 사용자의 개입 없이 hello 백그라운드에서 toorun 설계 되었습니다. 보호 중 하나가 기본 보안 기본적으로 응용 프로그램 작업 부하의 hello 요구 사항에 따라 또는 고급 사용자 지정 구성, 모니터링 하는 맬웨어 방지 프로그램을 포함 하 여 배포할 수 있습니다. Azure 맬웨어 방지 프로그램은 Azure Virtual Machines의 보안 옵션이며, 모든 Azure PaaS 가상 컴퓨터에 자동으로 설치됩니다.

**Azure toodeploy 및 응용 프로그램에 대 한 Microsoft 맬웨어 방지 설정의 기능**

#### <a name="microsoft-antimalware-core-features"></a>Microsoft 맬웨어 방지 프로그램 핵심 기능

-   **실시간 보호-** toodetect 및 블록 맬웨어 실행 가상 컴퓨터 및 클라우드 서비스에서 작업을 모니터링 합니다.

-   **검색-예약 된** 적극적으로 실행 중인 프로그램을 포함 하 여 검색 대상된 toodetect 맬웨어를 주기적으로 수행 합니다.

-   **맬웨어 치료** - 검색된 맬웨어에 대해 악성 파일을 삭제 또는 격리하고 악성 레지스트리 항목을 정리하는 것과 같은 작업을 자동으로 수행합니다.

-   **서명 업데이트-** 자동으로 설치 hello 최신 보호 (바이러스 정의) 서명 tooensure 보호는 미리 결정된 된 주파수에서 최신 상태입니다.

-   **맬웨어 방지 엔진 업데이트-** 자동으로 업데이트 hello Microsoft 맬웨어 방지 엔진입니다.

-   **맬웨어 방지 플랫폼 업데이트 –** 자동으로 업데이트 hello Microsoft 맬웨어 방지 플랫폼입니다.

-   **활성 보호-** 발견 된 위협 요소 및 의심 스러운 리소스 tooMicrosoft Azure tooensure 신속한 응답 toohello 위협 환경에서 진화 하 고을 통해 실시간 동기 서명 배달을 사용 하도록 설정 하는 방법에 대 한 원격 분석 메타 데이터를 보고 합니다. Microsoft Active Protection 시스템 (MAPS) 번호입니다.

-   **보고-샘플** 제공 하 고 샘플 보고서 toohello Microsoft 맬웨어 방지 서비스 toohelp hello 서비스 및 활성화 문제 해결을 구체화 합니다.

-   **제외 –** 에서 보호 하 고 성능 및/또는 기타 이유로 검사 tooexclude를 드라이브 및 특정 파일, 프로세스, 응용 프로그램 및 서비스 관리자 tooconfigure을 선택할 수 있습니다.

-   **맬웨어 방지 이벤트 수집-** hello 맬웨어 방지 서비스 상태, 의심 스러운 활동 및 hello 운영 체제 이벤트 로그에서 수행 된 수정 작업을 기록 하 고 hello 고객의 Azure 저장소 계정에이 수집 합니다.

### <a name="azure-sql-database-threat-detection"></a>Azure SQL Database 위협 검색

[Azure SQL 데이터베이스 위협 검색](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) hello Azure SQL 데이터베이스 서비스에 기본 제공 되는 새 보안 인텔리전스 기능입니다. Hello 따르게 클록 toolearn, 프로필 및 비정상 데이터베이스 작업을 검색, 잠재적 위협 toohello 데이터베이스를 식별 하는 Azure SQL 데이터베이스 위협 검색 합니다.

보안 책임자 또는 지정된 다른 관리자는 의심스러운 데이터베이스 활동이 발생하는 즉시 알림을 받을 수 있습니다. 각 알림에 hello 의심 스러운 활동의 세부 정보를 제공 하 고 toofurther 조사 하 고 hello 위협을 완화 하는 방법을 제시 합니다.

현재 Azure SQL Database 위협 검색은 잠재적인 취약성과 SQL 삽입 공격 및 비정상적인 데이터베이스 액세스 패턴을 검색합니다.

위협 검색 전자 메일 알림을 받으면 사용자 레코드가 수 toonavigate 뷰와 hello 관련 감사 hello 딥 링크를 사용 하 여 감사 뷰어 및/또는 hello 관련 감사를 보여 주는 미리 구성 된 감사 Excel 서식 파일을 열고 hello 메일 hello 시간 toohello 다음에 따라 hello 의심 스러운 이벤트의 레코드:
-   Hello/와 데이터베이스 서버를 hello 비정상 데이터베이스 작업에 대 한 감사 저장소

-   Hello 이벤트 toowrite 감사 로그의 hello 시 사용 되는 관련 된 감사 저장소 테이블

-   Hello hello 이벤트 발생 하므로 시간을 다음의 레코드를 감사 합니다.

-   감사 레코드 (일부 탐지기 선택 사항) hello 이벤트의 hello 시 비슷한 이벤트 id

SQL 데이터베이스 위협 탐지기 hello 다음 검색 방법 중 하나를 사용 합니다.

-   **결정적 검색 –** 알려진된 공격을 일치 하는 hello SQL 클라이언트 쿼리에서 의심 스러운 패턴 (규칙 기반)을 검색 합니다. 그러나 높은 검색과 낮은 거짓 긍정이이 방법론에 "원자성 검색"의 hello 범주에 속하도록 때문에 검사를 제한 합니다.

-   **Behavioural 검색 –** 결함 비정상적인 동작 hello 데이터베이스를 찾을 수 없으며 hello 동안 지난 30 일 이내에 비정상적인 활동입니다.  SQL 클라이언트에 대 한 비정상적인 활동에 대 한 예제는 실패 한 로그인/쿼리, 데이터 압축을 풀, 비정상적인 정식 쿼리 및 생소 한 IP 주소가 사용 tooaccess hello 데이터베이스 스파이크 될 수 있습니다.

### <a name="application-gateway-web-application-firewall"></a>Application Gateway 웹 응용 프로그램 방화벽

[웹 응용 프로그램 방화벽](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) 의 기능은 [Azure 응용 프로그램 게이트웨이](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) 보호를 제공 하는 표준에 대 한 응용 프로그램 게이트웨이 사용 하는 tooweb 응용 [응용프로그램배달제어](https://kemptechnologies.com/in/application-delivery-controllers) 함수입니다. 웹 응용 프로그램 방화벽은 대부분의 hello에 대 한 하 여이 [OWASP 상위 10 개의 일반적인 웹 취약점](https://www.owasp.org/index.php/Top_10_2010-Main)

![Application Gateway 웹 응용 프로그램 방화벽](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   SQL 삽입 공격 보호

-   교차 사이트 스크립팅 공격 보호

-   명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호

-   HTTP 프로토콜 위반 보호

-   누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호

-   보트, 크롤러 및 스캐너 방지

-   일반적인 응용 프로그램 구성 오류(즉 Apache, IIS 등) 검색

응용 프로그램 게이트웨이 WAF 중 구성 hello를 혜택 tooyou 다음을 제공 합니다.

-   웹 응용 프로그램 웹 취약점 및 toobackend 코드를 수정 하지 않고 공격 으로부터 보호 합니다.

-   보호 여러 웹 응용 프로그램 게이트웨이 뒤 시간이 hello에서 응용 프로그램입니다. 모든 웹 공격 으로부터 보호 될 수 있는 단일 게이트웨이 뒤 too20 웹 사이트를 호스팅 응용 프로그램 게이트웨이 지원 합니다.

-   Application Gateway WAF 로그에서 생성하는 실시간 보고서를 사용하여 공격을 받는 웹 응용 프로그램을 모니터링할 수 있습니다.

-   특정 규정 준수 컨트롤 모든 인터넷 WAF 솔루션에 의해 보호 되는 끝점 toobe 연결 해야 합니다. WAF가 활성화된 Application Gateway를 사용하면 이러한 규정 준수 요구 사항을 충족할 수 있습니다.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>변칙 검색 – Azure Machine Learning으로 작성된 API

변칙 검색은 Azure Machine Learning으로 작성된 API이며, 시계열 데이터에서 다양한 유형의 비정상 패턴을 검색하는 데 유용합니다. 경고를 생성에 사용할 수 있는 hello 시계열에서 점수 tooeach 데이터 요소는 변칙을 할당 하는 hello API 대시보드를 통해 모니터링 하거나 발권 시스템을 사용 하 여 연결 합니다.

hello [변칙 검색 API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) hello 나오는 시계열 데이터에 따라 변칙 유형을 감지할 수 있습니다.

-   **스파이크 및 Dip:** 예를 들어 로그인 오류 tooa 서비스의 hello 번호 또는 전자 상거래 사이트에서의 체크 아웃 횟수를 모니터링 하는 경우 비정상적인 스파이크 또는 dip 수 보안 공격을 나타내거나 서비스 중단 합니다.

-   **긍정 추세 및 부정 추세:** 예를 들어 컴퓨팅에서 메모리 사용량을 모니터링할 때 사용 가능한 메모리 크기가 줄어들면 잠재적인 메모리 누수가 있음을 나타냅니다. 서비스 큐 길이를 모니터링할 때 지속적으로 증가하는 추세는 기본 소프트웨어 문제를 나타낼 수도 있습니다.

-   **변경 내용 및 값의 동적 범위에서 변경 내용을 수준:** 예를 들어 수준 변경 서비스의 대기 시간이 서비스 업그레이드 하거나 보다 낮은 수준 예외도 후 흥미로운 toomonitor 하지 않을 수 있습니다.

hello 기계 학습 기반 API 사용:

-   **유연 하 고 강력한 검색:** hello 비정상 검색 모델 tooconfigure 민감도 설정을 사용자가 허용 하 고, 없는 seasonal 계절별 데이터 집합 간에 변칙을 검색할 합니다. 보다 중요 한 따라 tootheir 필요한 또는 사용자는 덜 hello 비정상 검색 모델 toomake hello 검색 API를 조정할 수 있습니다. 이 구성이 hello 검색 데이터와 없는 seasonal 패턴에에서 더 많거나 적은 보이는 비정상입니다.

-   **확장 가능 하 고 시기 적절 한 검색:** hello 전통적인 방법 전문가 도메인 지식을 하면 현재 임계값을 사용한 모니터링은 비용이 많이 들고 확장성 않음 toomillions 동적으로 데이터 집합을 변경 합니다. 이 API의 hello 비정상 검색 모델 학습 되 고 모델은 이전 및 실시간 데이터에서 자동으로 튜닝 됩니다.

-   **사전 대응 및 실행 가능 검색:** 느린 추세 및 수준 변경 검색은 초기 변칙 검색에 적용할 수 있습니다. hello 초기 비정상적인 신호 검색 사용된 toodirect 인간이 tooinvestigate를 수 있으며 hello 문제 영역에 대해 작동 됩니다.  또한 이 변칙 검색 API 서비스를 기반으로 하여 근본 원인 분석 모델 및 경고 도구를 개발할 수도 있습니다.

hello 변칙 검색 API에는 다양 한 서비스 상태 및 KPI 모니터링, IoT, 성능 모니터링 및 네트워크 트래픽 모니터링와 같은 시나리오에 대 한 효과적이 고 효율적인 솔루션입니다. 이 API가 유용할 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.
- IT 부서에서는 도구 tootrack 이벤트, 오류 코드, 사용 현황 로그 및 성능 (CPU, 메모리 및 등)를 적시에 필요 합니다.

-   온라인 판매 사이트 tootrack 고객 활동, 페이지 보기, 클릭, 및 등 원하는 합니다.

-   유틸리티 회사 물, 가스, 전기, 및 기타 리소스의 tootrack 소비를 원합니다.

-   관리 서비스 기능/빌드 toomonitor 온도, 습기, 트래픽 및 등 원하는 합니다.

-   IoT/제조업체 toouse 센서 데이터를 시간 시계열 toomonitor 포함 하려는 워크플로, 품질 및 등입니다.

-   서비스 공급자, 전화 교환 국 필요 건 수가 toomonitor 서비스 요청 추세와 같은 대기 큐 길이 등입니다.

-   비즈니스 분석 그룹 (예: 판매량, 가격, 고객 표현의) toomonitor 비즈니스 Kpi 원하는 실시간으로 비정상적인 이동 합니다.

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) hello Microsoft 클라우드 보안 스택의 주요 구성 요소는 합니다. Tootake 완전히 활용 클라우드 응용 프로그램의 hello 프라미스를 이동 하지만 활동에 대 한 향상 된 가시성을 통해 제어를 유지 조직 데 도움이 되는 포괄적인 솔루션입니다. 또한 클라우드 응용 프로그램에서 중요 한 데이터의 hello 보호를 늘릴 수 있습니다.

그림자 IT를 확인할 위험 평가, 정책 적용, 활동을 조사 및 위협을 중지 데 도움이 되는 도구를 사용 하 여 조직의 중요 한 데이터의 제어를 유지 하면서 toohello 클라우드를 보다 안전 하 게 이동할 수 있습니다.

<table style="width:100%">
 <tr>
   <td>검색</td>
   <td>Cloud App Security로 섀도 IT를 발견합니다. 클라우드 환경에서 앱, 활동, 사용자, 데이터 및 파일을 검색하여 가시성을 확보합니다. 연결 된 타사 앱 검색 tooyour 클라우드입니다.</td>
 </tr>
 <tr>
   <td>조사</td>
   <td>위험한 앱, 특정 사용자 및 네트워크의 파일에 클라우드 법정 도구 toodeep 분석을 사용 하 여 클라우드 앱을 조사 합니다. 클라우드에서 수집 된 hello 데이터에서 패턴을 찾을 합니다. 보고서 toomonitor 클라우드를 생성 합니다.</td>

 </tr>
 <tr>
   <td>제어</td>
   <td>Tooachieve 최대한 네트워크 클라우드 트래픽의 제어 정책 및 경고를 설정 하 여 위험을 완화 합니다. Cloud App Security toomigrate 프로그램 사용자 toosafe, 권한 부여 클라우드 앱 대 안으로 사용 합니다.</td>

 </tr>
 <tr>
   <td>보호</td>
   <td>Cloud App Security toosanction를 사용 하 여 또는 응용 프로그램을 (를) 금지, 데이터 손실 방지, 제어 권한 및 공유, 적용 및 사용자 지정 보고서 및 경고를 생성 합니다.</td>

 </tr>
 <tr>
   <td>제어</td>
   <td>Tooachieve 최대한 네트워크 클라우드 트래픽의 제어 정책 및 경고를 설정 하 여 위험을 완화 합니다. Cloud App Security toomigrate 프로그램 사용자 toosafe, 권한 부여 클라우드 앱 대 안으로 사용 합니다.</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security는 다음과 같은 방법으로 클라우드와 가시성을 통합합니다.

-   Cloud Discovery toomap를 사용 하 여 클라우드 환경을 식별 하 고 조직에서 사용 하는 클라우드 앱 hello 합니다.


-   클라우드의 앱을 승인하거나 금지합니다.



-   연결하는 앱의 가시성과 관리를 위해 공급자 API를 활용하는 배포하기 쉬운 앱 커넥터를 사용합니다.

-   정책을 설정하고 지속적으로 자세히 튜닝하여 연속적으로 제어하도록 지원합니다.

이러한 원본의 데이터를 수집 Cloud App Security hello 데이터에 대해 복잡 한 분석을 실행 합니다. 즉시 tooanomalous 활동을 경고 하 고 클라우드 환경에 대 한 심층 가시성을 제공 합니다. Cloud App Security에 한 정책을 구성 하 고 tooprotect 사용할 수 있습니다 클라우드 환경에서 모든 항목입니다.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Azure Marketplace를 통한 타사 ATD 기능

### <a name="web-application-firewall"></a>웹 응용 프로그램 방화벽

웹 응용 프로그램 방화벽은 인바운드 웹 트래픽을 검사하고 SQL 삽입 공격, 사이트 간 스크립팅, 맬웨어 업로드, 응용 프로그램 DDoS 및 웹 응용 프로그램을 대상으로 하는 기타 공격을 차단합니다. Hello 백 엔드 웹 서버에서 응답 hello에 대 한 데이터 손실 방지 (DLP)도 검사합니다. hello 통합 된 액세스 제어 엔진 인증, 권한 부여 및 계정 AAA (), 조직 강력한 인증 및 사용자 정의 컨트롤 수 있도록 관리자 toocreate 세부적인 액세스 제어 정책 수 있습니다.

**주요 사항:**
-   SQL 삽입 공격, 사이트 간 스크립팅, 맬웨어 업로드, 응용 프로그램 DDoS 또는 응용 프로그램에 대한 기타 모든 공격을 검색하고 차단합니다.

-   인증 및 액세스 제어

-   아웃 바운드 트래픽을 toodetect 중요 한 데이터를 검색 하 고 숨길 수 또는 hello 정보 누출 되를 차단 합니다.

-   웹 응용 프로그램 콘텐츠, 캐싱, 압축 및 다른 트래픽 최적화와 같은 기능을 사용 하 여 hello 배달의 속도 높여 합니다.

다음은 Azure Market Place에서 사용할 수 있는 웹 응용 프로그램 방화벽의 예입니다.

[Barracuda 웹 응용 프로그램 방화벽, Brocade 가상 웹 응용 프로그램 방화벽 (Brocade vWAF), Imperva SecureSphere 및 hello ThreatSTOP IP 방화벽입니다.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>다음 단계

- [Azure Security Center 감지 기능](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Azure 보안 센터의 고급 검색 기능이 tooidentify 활성 위협이 Microsoft Azure 리소스를 대상으로 사용 하 고 hello insights 필요한 toorespond 신속 하 게 제공 합니다.

- [Azure SQL Database 위협 검색](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Azure SQL 데이터베이스 위협 검색에서는 잠재적인 위협 tootheir 데이터베이스에 대 한 해당 문제를 해결 합니다.
