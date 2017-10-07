---
title: "aaaIntroduction tooAzure 보안 | Microsoft Docs"
description: "Azure 보안, 해당 서비스 및 작동 방법에 대해 알아봅니다."
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
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>소개 tooAzure 보안
## <a name="overview"></a>개요
회원님의 보안은 hello 클라우드에서 작업 하나 고 Azure 보안에 대 한 정확 하 고 시기 적절 한 정보를 찾을 얼마나 중요 한지 됩니다. Hello 최상의 이유 toouse Azure 응용 프로그램 및 서비스에 대 한 중 하나 tootake 활용 하는 다양 한 보안 도구 및 기능입니다. 이러한 도구와 기능 hello 보안 Azure 플랫폼에서 가능한 toocreate 보안 솔루션을 확인할 수 있습니다. Microsoft Azure는 고객 데이터의 기밀성, 무결성 및 가용성을 제공하는 한편 투명한 책임도 가능하게 합니다.

hello 컬렉션 모두 hello 고객 및 Microsoft 작업의 관점에서이 백서 "소개 tooAzure 보안" Microsoft Azure 내에서 구현 하는 보안 제어를 더 잘 이해 toohelp tooprovide 기록 되는 Microsoft Azure와 함께 사용할 수 있는 hello 보안 포괄적인 보기.

### <a name="azure-platform"></a>Azure 플랫폼
Azure는 다양한 운영 체제, 프로그래밍 언어, 프레임워크, 도구, 데이터베이스 및 장치를 지원하는 공용 클라우드 서비스 플랫폼입니다. Docker 통합으로 Linux 컨테이너를 실행할 수 있습니다. JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드할 수 있습니다. iOS, Android 및 Windows 장치용 백 엔드를 빌드할 수 있습니다.

Azure 공용 클라우드 서비스는 hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다. 를, 작성 하거나 IT 자산을 마이그레이션할 때 해당 조직의 능력 tooprotect 응용 프로그램 및 데이터 hello 서비스 및 hello 컨트롤을 사용 하는 공용 클라우드 서비스 공급자 제공 toomanage hello 보안의 클라우드 기반 자산에 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 tooapplications 시설에서에서 azure의 인프라를 디자인 하 고는 기업의 보안 요구 사항을 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다.

또한 Azure는 다양 한 구성 가능한 보안 옵션 및 hello 기능 toocontrol와 보안 toomeet hello 조직의 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다. 이 문서는 Azure 보안 기능이 이러한 요구 사항을 충족하는 방법을 이해하는 데 도움이 됩니다.

> [!Note]
> 이 문서의 주된 초점은 hello toocustomize를 사용할 수 있으며 응용 프로그램 및 서비스에 대 한 보안을 강화 고객 관련 컨트롤 켜져 있습니다.
>
> 자체를 Azure 플랫폼에 대 한 자세한 내용은 Microsoft hello를 보호 하는 방법을 hello에 제공 된 정보를 참조 하지만 일부 개요 정보를 제공지 않습니다 [Microsoft 보안 센터](https://www.microsoft.com/TrustCenter/default.aspx)합니다.

### <a name="abstract"></a>요약
처음에 공용 클라우드 마이그레이션 비용 절감 효과 및 민첩성 tooinnovate에 의해 발생 했습니다. 보안은 한동안 공용 클라우드 마이그레이션에 대한 중요한 관심사로 간주되었으며, 심지어는 쇼 스토퍼로도 간주되었습니다. 그러나 공용 클라우드 보안 문제 tooone 클라우드 마이그레이션에 대 한 hello 드라이버의 주요에서 전환 되었습니다. hello 적어두고가 hello 큰 공용 클라우드 서비스 공급자 tooprotect 응용 프로그램의 뛰어난 기능 및 클라우드 기반 자산 hello 데이터 됩니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고 비즈니스는 고유한 보안 요구를 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 다양 한 구성 가능한 보안 옵션 및 hello 기능 toocontrol와 해당 it 부서 제어 정책 및 준수 tooexternal 보안 toomeet hello 배포 toomeet의 고유한 요구를 사용자 지정할 수 있도록 규정 합니다.

이 문서는 hello Microsoft Azure 클라우드 플랫폼 내에서 Microsoft의 접근 방식을 toosecurity를 설명합니다.
* Microsoft Azure 인프라 toosecure hello, 고객 데이터 및 응용 프로그램에서 구현 된 보안 기능입니다.
* Azure 서비스 및 보안 기능 사용 가능한 tooyou toomanage hello hello 서비스 및 Azure 구독 내에서 데이터의 보안 합니다.

## <a name="summary-azure-security-capabilities"></a>Azure 보안 기능 요약
hello 테이블 다음에는 Microsoft Azure 인프라 toosecure hello, 고객 데이터 및 보안 응용 프로그램에서 구현 되는 hello 보안 기능에 대 한 간략 한 설명을 제공 합니다.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>보안 기능을 구현 tooSecure hello Azure Platform:
hello 나열 된 다음 기능은 기능 Azure 플랫폼에서 안전한 방식으로 관리 되는 hello tooprovide hello 보증을 검토할 수 있습니다. Microsoft에서 보안 플랫폼, 개인 정보 보호 및 제어, 규정 준수 및 투명성의 네 가지 영역에서 고객의 신뢰 문제를 해결하는 방법에 대해 추가로 드릴다운할 수 있는 링크를 제공하고 있습니다.


| [보안 플랫폼](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [개인 정보 보호 및 제어](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[규정 준수](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [투명성](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [보안 개발 주기](https://www.microsoft.com/en-us/sdl/)(영문), 내부 감사 | [모든 hello 시간 데이터를 관리 합니다.](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [보안 센터](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Microsoft Azure 서비스에서 고객 데이터를 보호하는 방법](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)(영문) |
| [필수 보안 교육, 백그라운드 검사](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc)(영문) |  [데이터 위치에서 제어](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [일반 컨트롤 허브](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub)(영문) |[Microsoft Azure 서비스에서 데이터 위치를 관리하는 방법](http://azuredatacentermap.azurewebsites.net/)(영문)|
| [침투 테스트](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [침입 검색, DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [감사 및 로깅](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [조건부 데이터 액세스 제공](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [hello 클라우드 서비스 Due 성실 검사 목록](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[데이터에 누가 그리고 어떤 조건으로 액세스할 수 있는가](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [세계 첨단의 데이터 센터](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), 물리적 보안, [네트워크 보안](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [응답 toolaw 적용](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [서비스별, 지역별 및 산업별 규정 준수](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Microsoft Azure 서비스에서 고객 데이터를 보호하는 방법](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)(영문)|
|  [보안 사고 대응](http://aka.ms/SecurityResponsepaper)(영문), [공동 책임](http://aka.ms/sharedresponsibility)(영문) |[엄격한 개인 정보 보호 표준](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Azure 서비스, 투명성 허브에 대한 인증 검토](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)(영문)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Azure tooSecure 데이터에서 제공 되는 보안 기능 및 응용 프로그램
Hello 클라우드 서비스 모델에 따라서는 hello 응용 프로그램 또는 서비스의 hello 보안 관리 책임이 있는 사람에 대 한 변수 책임이 있습니다. Hello Azure 플랫폼 tooassist 및 기본 제공 기능을 통해 이러한 책임을 충족 하면 파트너는 Azure 구독에 배포할 수 있는 솔루션에서에서 사용할 수 있는 기능이 있습니다.

기본 제공 기능 hello 6 개의 기능 영역에서 구성 됩니다: 작업, 응용 프로그램, 저장소, 네트워킹, 계산 및 Id입니다. Hello 기능과 hello 6 (6) 영역에서 Azure 플랫폼에서에서 사용할 수 있는 기능에 대 한 세부 정보가 요약 정보를 통해 제공 됩니다.

## <a name="operations"></a>작업
이 섹션에서는 보안 작업의 주요 기능에 대한 추가 정보와 이러한 기능에 대한 요약 정보를 제공합니다.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Operations Management Suite 보안 및 감사 대시보드
hello [OMS 보안 및 감사 솔루션](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) 제공 한 포괄적인 뷰를 조직의 IT 보안 상태에 [기본 제공 검색 쿼리](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) 주의가 필요한 주요 문제에 대 한 합니다. hello [보안 및 감사](https://technet.microsoft.com/library/mt484091.aspx) 대시보드는 모든 항목에 대 한 홈 화면 hello 관련 OMS에서 toosecurity 합니다. Hello 컴퓨터의 보안 상태에 대 한 개략적인 정보를 제공합니다. 지난 24 시간, 7 일 hello에서 모든 이벤트 또는 다른 사용자 지정 시간 프레임 hello 기능 tooview도 있습니다.

또한 구성할 수 있습니다 OMS 보안 및 규정 준수 너무[특정 작업을 자동으로 수행](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) 특정 이벤트 감지 되 면 합니다.

### <a name="azure-resource-manager"></a>Azure 리소스 관리자
[Azure 리소스 관리자 ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) toowork hello 리소스 그룹으로 솔루션에 있습니다. 배포 지정, 업데이트 또는 단일, 통합 작업에서 솔루션에 대 한 모든 hello 리소스를 삭제 합니다. 배포용 [Azure Resource Manager 템플릿](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/)을 사용하고, 해당 템플릿은 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다. 리소스 관리자는 감사 보안을 제공 하 고 리소스 배포 된 후 관리 기능 toohelp 태그를 지정 합니다.

Azure 리소스 관리자 템플릿 기반 배포 보안을 개선 하 hello 표준 보안 설정을 제어 하 고 수 때문에 Azure에 배포 된 솔루션의 표준화 된 템플릿 기반 배포에 통합할 수 있습니다. 이렇게 하면 보안 구성 오류가 발생할 수 있는 수동 배포 하는 동안 hello 발생할 가능성이 줄어듭니다.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/)는 웹 개발자를 위한 확장 가능한 APM(응용 프로그램 성능 관리) 서비스입니다. Application Insights를 사용하면 라이브 웹 응용 프로그램을 모니터링하고 성능 이상을 자동으로 검색할 수 있습니다. Toounderstand 여 응용 프로그램과 함께 실제로 사용자가 수행 하 고 문제를 진단 하는 강력한 분석 도구 toohelp을 포함 됩니다. 응용 프로그램 테스트 및 게시 하거나 배포 된 후 실행 중인 모든 hello 시간을 모니터링 합니다.

예를 들어 있는 시간을 대부분의 사용자가 가져올 응답 hello 앱이 되는 서비스는 올바른 외부에서 제공 하는 방법 등에 종속에 application Insights를 보여 주는 테이블과 차트를 만듭니다.

충돌, 오류 또는 성능 문제가 있는 경우에 세부 toodiagnose hello 원인에서 hello 원격 분석 데이터를 통해 검색할 수 있습니다. 및 hello 서비스 보낸 전자 메일 앱의 hello 가용성과 성능을에 변경 된 경우. 따라서 application Insight hello 기밀성, 무결성 및 가용성 보안 두꺼운 수직선의 hello 가용성과 함께 사용 하면 때문에 중요 한 보안 도구를 됩니다.

### <a name="azure-monitor"></a>Azure Monitor
[Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) hello Azure 인프라에서에서 시각화, 쿼리, 라우팅, 경고, 자동 크기 조정 및 자동화 데이터 모두에 대해 제공 ([활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) 및 각 개별 Azure 리소스 ([ 진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). Azure 모니터 tooalert를 사용할 수는 Azure 로그에 생성 하는 보안 관련 이벤트에 있습니다.

### <a name="log-analytics"></a>Log Analytics
[로그 분석](https://azure.microsoft.com/documentation/services/log-analytics/) 의 일부가 [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) – IT 관리 솔루션 온-프레미스와 타사 클라우드 기반 인프라 (예: AWS)에 대 한 또한 tooAzure 리소스 제공. Azure 모니터에서 데이터를 라우팅할 수 직접 tooLog 분석 한 곳에 전체 환경에 대 한 메트릭 및 로그를 볼 수 있습니다.

Hello 도구를 사용 하면 많은 양의 유연한 쿼리 접근 방식으로 보안 관련 항목을 통해 있습니다 tooquickly 검색 법정에 유용한 도구 및 기타 보안 분석 로그 분석 될 수 있습니다. 또한 온-프레미스 [방화벽 및 프록시 로그를 Azure로 내보내고 Log Analytics를 사용하여 분석할 수 있습니다.](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure Advisor
[Azure 관리자](https://docs.microsoft.com/azure/advisor/) toooptimize를 도움이 되는 개인 설정 된 클라우드 컨설턴트 Azure 배포 됩니다. 리소스 구성 및 사용 원격 분석을 분석 합니다. 그런 다음 해결책을 제시 toohelp 향상 hello [성능](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [보안](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), 및 [고가용성](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) 너무 기회를 찾는 동안 리소스[줄일 전체 Azure 지출](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations)합니다. Azure Advisor는 보안 권장 사항을 제공하므로 Azure에 배포하는 솔루션의 전반적인 보안 상태를 크게 향상시킬 수 있습니다. 이러한 권장 사항은 [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)에서 수행한 보안 분석에서 가져온 것입니다.

### <a name="azure-security-center"></a>Azure 보안 센터
[Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro) 사용 방지를 감지 하 고 및 toothreats 파악할을 사용 하 여 응답을 제어할 수 hello Azure 리소스의 보안 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

또한 Azure Security Center는 즉시 수행할 수 있는 경고와 권장 사항을 보여 주는 단일 대시보드를 제공하여 보안 운영을 지원합니다. 종종 hello Azure 보안 센터 콘솔 내에서 한 번의 클릭으로 문제를 해결할 수 있습니다.
## <a name="applications"></a>응용 프로그램
hello 섹션에서는 이러한 기능에 대 한 보안 및 요약 정보를 응용 프로그램의 주요 기능에 대 한 추가 정보를 제공 합니다.

### <a name="web-application-vulnerability-scanning"></a>웹 응용 프로그램 취약성 스캔
가장 쉬운 방법으로 tooget hello 중 하나에서 취약점에 대 한 테스트를 시작 하면 [앱 서비스 앱](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) 는 toouse hello [와 Tinfoil Security 통합](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform 한 번의 클릭 취약점의 검색 응용 프로그램입니다. 이해 하기 쉬운 보고서에 hello 테스트 결과 검토 하 고 알아볼 수 있습니다 어떻게 toofix 단계별 지침이 포함 된 각 취약점입니다.

### <a name="penetration-testing"></a>침투 테스트
사용자 고유의 침투 테스트 또는 toouse 다른 스캐너 제품군 또는 공급자를 hello 따라야 tooperform 선호 하는 경우 [승인 프로세스를 테스트 하는 Azure 침투](https://security-forms.azure.com/penetration-testing/terms) 가져오고, 사전 승인 tooperform 원하는 hello 침투 테스트 합니다.

### <a name="web-application-firewall"></a>웹 응용 프로그램 방화벽
웹 응용 프로그램 방화벽 (WAF) hello [Azure 응용 프로그램 게이트웨이](https://azure.microsoft.com/services/application-gateway/) SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 세션 하이재킹에서 웹 응용 프로그램을 보호 합니다. Hello로 식별 된 위협 요소 로부터 미리 구성 된 보호 제공 [열기 웹 응용 프로그램 보안 프로젝트 (OWASP) hello로 상위 10 개의 일반적인 보안 문제](https://msdn.microsoft.com/library/)합니다.

### <a name="authentication-and-authorization-in-azure-app-service"></a>Azure 앱 서비스의 인증 및 권한 부여
[앱 서비스 인증 / 권한 부여](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) 는 hello 앱 백 엔드에 toochange 코드가 없는 있도록 사용자의 응용 프로그램 toosign 프로그램에 대 한는 방법을 제공 하는 기능입니다. 제공을 쉽게 tooprotect 응용 프로그램 및 작업 사용자별 데이터를 사용 합니다.

### <a name="layered-security-architecture"></a>계층화된 보안 아키텍처
[App Service 환경](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro)이 [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)에 배포된 격리된 런타임 환경을 제공하므로 개발자는 각 응용 프로그램 계층에 서로 다른 수준의 네트워크 액세스를 제공하는 계층화된 보안 아키텍처를 만들 수 있습니다. 일반적인 desire toohide API 백 엔드가 일반 인터넷 액세스 로부터 이며 Api toobe 업스트림 웹 응용 프로그램에 의해 호출을 허용 합니다. [네트워크 보안 그룹 (Nsg)](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) 앱 서비스 환경 toorestrict 공용 액세스 tooAPI 응용 프로그램이 포함 된 Azure 가상 네트워크 서브넷에서 사용할 수 있습니다.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>웹 서버 진단 및 응용 프로그램 진단
앱 서비스 웹 앱 hello 웹 서버와 hello 웹 응용 프로그램에서 로깅 정보에 대 한 진단 기능을 제공 합니다. 이는 논리적으로 [웹 서버 진단](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) 및 [응용 프로그램 진단](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx)으로 구분됩니다. 웹 서버에서 사이트와 응용 프로그램을 진단하고 문제를 해결하는 두 가지의 큰 발전이 이루어졌습니다.

hello 첫 번째 새로운 기능에는 응용 프로그램 풀, 작업자 프로세스, 사이트, 응용 프로그램 도메인 및 요청 실행 하는 방법에 대 한 실시간 상태 정보입니다. 두 번째 새 장점 hello hello 전체 요청-응답 프로세스 전체에서 요청을 추적 하는 자세한 추적 이벤트 hello 됩니다.

이러한 추적 이벤트 tooenable hello 컬렉션, IIS 7 경과 된 시간 또는 오류 응답 코드를 기반으로 하는 특정 요청에 대 한 XML 형식으로 구성 된 tooautomatically 캡처 전체 추적 로그 될 수 있습니다.

#### <a name="web-server-diagnostics"></a>웹 서버 진단
다음 종류의 로그 hello를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

-   자세한 오류 로깅 - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)에 대한 자세한 오류 정보입니다. 이 hello 서버 hello 오류 코드를 반환 하는 이유를 확인 하는 데 유용한 정보를 포함할 수 있습니다.

-   실패 한 요청 추적-실패 한 요청을 추적 hello IIS 구성 요소 사용 tooprocess hello 요청 및 각 구성 요소에서 수행 되는 hello 시간을 포함 하 여 대 한 상세 정보가 있습니다. 반환 된 HTTP 오류 toobe를 특정 원인을 격리 tooincrease 사이트 성능을 하려고 하는 경우에 유용할 수 있습니다.

-   웹 서버 로깅-hello W3C 확장된 로그 파일 형식을 사용 하 여 HTTP 트랜잭션에 대 한 정보입니다. 특정 IP 주소에서 처리 하는 요청의 hello 번호와 같은 전반적인 사이트 메트릭 또는 요청 수를 결정할 때 유용 합니다.

#### <a name="application-diagnostics"></a>응용 프로그램 진단
[응용 프로그램 진단](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) toocapture 정보는 웹 응용 프로그램에서 만든 있습니다. ASP.NET 응용 프로그램에서는 hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) 클래스 toolog 정보 toohello 응용 프로그램 진단 로그입니다. Application Diagnostics, 두 가지 유형의 주요 이벤트, tooapplication 성능 관련 있으며 tooapplication 실패 및 오류와 관련 된 것입니다. hello 실패 및 오류 나눌 수 있으며 연결, 보안 및 실패 문제로 합니다. 실패 문제는 일반적으로 관련된 tooa hello 응용 프로그램 코드 문제입니다.

응용 프로그램 진단에서 다음과 같은 방법으로 그룹화된 이벤트를 볼 수 있습니다.

-   모두(모든 이벤트 표시)
-   응용 프로그램 오류(예외 이벤트 표시)
-   성능(성능 이벤트 표시)

## <a name="storage"></a>저장소
hello 섹션에서는 이러한 기능에 대 한 보안 및 요약 정보를 Azure 저장소의 주요 기능에 대 한 추가 정보를 제공 합니다.

### <a name="role-based-access-control-rbac"></a>역할 기반 액세스 제어(RBAC)
RBAC(역할 기반 액세스 제어)를 사용하여 저장소 계정의 보안을 유지할 수 있습니다. Hello에 따라 액세스를 제한 [tooknow 필요](https://en.wikipedia.org/wiki/Need_to_know) 및 [최소 권한](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 보안 주체는 데이터 액세스를 위한 보안 정책 tooenforce는 조직을 위한 것입니다. 적절 한 RBAC 역할 toogroups hello 및 특정 범위의 응용 프로그램을 할당 하 여 이러한 액세스 권한이 부여 됩니다. 사용할 수 있습니다 [기본 제공 RBAC 역할](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), 저장소 계정 참가자와 같은 tooassign 권한 toousers 합니다. 액세스 hello를 사용 하 여 저장소 계정에 대 한 저장소 키 toohello [Azure 리소스 관리자](https://docs.microsoft.com/azure/storage/storage-security-guide) 모델 역할 기반 액세스 제어 (RBAC)를 통해 제어할 수 있습니다.

### <a name="shared-access-signature"></a>공유 액세스 서명
A [공유 액세스 서명 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) 저장소 계정의 tooresources 위임 된 액세스를 제공 합니다. hello SAS 클라이언트 제한 된 사용 권한을 tooobjects 저장소 계정에 지정된 된 기간 동안 및 지정한 사용 권한 집합으로 부여할 수 있는 것을 의미 합니다. 계정 액세스 키 tooshare 필요 없이 이러한 제한 된 사용 권한을 부여할 수 있습니다.

### <a name="encryption-in-transit"></a>전송 중 암호화
전송 중 암호화는 네트워크를 통해 전송되는 경우 데이터 보호의 메커니즘입니다. Azure Storage를 사용하면 다음을 사용하여 데이터를 보호할 수 있습니다.
-   [전송 수준 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit)(예: Azure 저장소 안팎으로 데이터를 전송하는 경우 HTTPS)

-   [실시간 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares)(예: [Azure 파일 공유](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files)에 대한 [SMB 3.0 암호화](https://docs.microsoft.com/azure/storage/storage-security-guide))

-   클라이언트 쪽 암호화, tooencrypt hello 데이터 저장소로 전송 될 때까지 및 toodecrypt hello 데이터 저장소에서 전송 된 후 중에서 선택 합니다.

### <a name="encryption-at-rest"></a>휴지 상태의 암호화
많은 조직에서 미사용 데이터 암호화는 데이터 개인 정보 보호, 규정 준수 및 데이터 주권을 위한 필수 단계입니다. "미사용" 데이터 암호화를 제공하는 세 가지 Azure 저장소 보안 기능이 있습니다.

-   [저장소 서비스 암호화](https://docs.microsoft.com/azure/storage/storage-service-encryption) toorequest hello 저장소 서비스 tooAzure 저장소를 작성할 때 자동으로 데이터를 암호화를 사용 하면 됩니다.

-   [클라이언트 쪽 암호화](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) 미사용 데이터 암호화의 hello 기능을 사용 합니다.

-   [Azure 디스크 암호화](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) tooencrypt hello OS 디스크 및 데이터 디스크는 IaaS 가상 컴퓨터에서 사용 하는 사용자에 게 있습니다.

### <a name="storage-analytics"></a>저장소 분석
[ 분석](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)은 로깅을 수행하며 저장소 계정에 대한 메트릭 데이터를 제공합니다. 이 데이터 tootrace 요청을 사용 하 고, 사용 추세를 분석 하 고, 저장소 계정 문제를 진단할 수 있습니다. Storage Analytics는 성공 및 실패 한 요청 tooa 저장소 서비스에 대 한 세부 정보를 기록 합니다. 이 정보는 개별 요청을 사용 하는 toomonitor 및 저장소 서비스와 toodiagnose 문제 수 있습니다. 요청은 최상의 노력을 기준으로 기록됩니다. hello 다음 유형의 인증 된 요청이 기록 됩니다.
-   성공한 요청

-   실패한 요청(제한 시간, 제한, 네트워크, 권한 부여 및 기타 오류)

-   실패한 요청 및 성공한 요청을 포함하는 SAS(공유 액세스 서명)를 사용하는 요청

-   요청 tooanalytics 데이터입니다.

### <a name="enabling-browser-based-clients-using-cors"></a>CORS를 통해 브라우저 기반 클라이언트를 사용하도록 설정
[크로스-원본 자원 공유 (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) 도메인 toogive 서로 수 있는 메커니즘은 다른 사용자의 리소스에 액세스 하는 것에 대 한 권한이 있습니다. hello 사용자 에이전트는 특정 도메인에서 로드 된 hello JavaScript 코드에 다른 도메인에 있는 tooaccess 리소스 허용 되는 추가 헤더 tooensure를 보냅니다. 추가 헤더를 허용 하거나 거부 hello 원래 도메인 액세스 tooits 리소스 hello 후자 도메인 회신 합니다.

Azure 저장소 서비스 지금은 지원 CORS는 않도록 hello 서비스에 대 한 hello CORS 규칙을 설정한 후 hello 서비스에 대해 다른 도메인에서 수행 된 제대로 인증 된 요청 평가 toodetermine 있는 toohello 규칙에 따라 허용 지정 합니다.
## <a name="networking"></a>네트워킹
hello 섹션에서는 이러한 기능에 대 한 보안 및 요약 정보를 Azure 네트워크의 주요 기능에 대 한 추가 정보를 제공 합니다.

### <a name="network-layer-controls"></a>네트워크 계층 제어
네트워크 액세스 제어는 특정 장치 또는 서브넷에서 연결 tooand 제한 hello act 및 나타냅니다 hello 네트워크 보안의 핵심입니다. 네트워크 액세스 제어의 hello 목표에는 가상 컴퓨터 및 서비스는 액세스할 수 있는 tooonly 사용자 및 장치 toowhich 원하는 액세스할 수 있는지 toomake입니다.

#### <a name="network-security-groups"></a>네트워크 보안 그룹
A [보안 그룹 NSG (네트워크)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) 필터링 방화벽 및 그 기본 상태 저장 패킷 수 toocontrol 액세스할 수에 따라 한 [5-튜플](https://www.techopedia.com/definition/28190/5-tuple)합니다. NSG는 응용 프로그램 계층 검사 또는 인증된 액세스 제어를 제공하지 않습니다. 사용할 수 toocontrol 트래픽이 Azure 가상 네트워크 내의 서브넷과 Azure 가상 네트워크와 hello 인터넷 간의 트래픽 간에 이동 합니다.

#### <a name="route-control-and-forced-tunneling"></a>경로 제어 및 터널링 적용
Azure 가상 네트워크에 hello 기능 toocontrol 라우팅 동작 중요 한 네트워크 보안 및 액세스 제어 기능입니다. 예를 들어 Azure 가상 네트워크에서 모든 트래픽 tooand 해당 가상 보안 어플라이언스 거치 있는지 toomake 원하는 toobe 수 toocontrol를 해야 라우팅 동작을 사용자 지정 합니다. 이렇게 하려면 Azure에서 사용자 정의 경로를 구성하면 됩니다.

[사용자 정의 경로](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) toocustomize 사용 하면 개별 가상 컴퓨터 또는 서브넷 tooinsure 안팎으로 이동 하는 트래픽에 대 한 인바운드 및 아웃 바운드 경로 hello 가장 안전한 경로 가능한 합니다. [강제 터널링](https://www.petri.com/azure-forced-tunneling) tooensure 없는 서비스를 사용할 수 있는 메커니즘에 사용할 수 tooinitiate 연결 toodevices hello 인터넷 합니다.

다를 수 tooaccept 들어오는 연결 되 고 한 다음 응답 toothem 합니다. 프런트 엔드 웹 서버에서 인터넷 호스트 toorespond toorequests 필요 하며 인바운드 toothese 웹 서버와 웹 서버 hello 응답할 수 있는 인터넷 원본에서 얻었는지 트래픽이 허용 됩니다.

강제 터널링은 온-프레미스 보안 프록시 및 방화벽을 통해 자주 사용 되는 tooforce 아웃 바운드 트래픽을 toohello 인터넷 toogo입니다.

#### <a name="virtual-network-security-appliances"></a>가상 네트워크 보안 어플라이언스
네트워크 보안 그룹, 사용자 정의 경로 및 강제 터널링 제공 hello의 hello 네트워크와 전송 계층에서 보안 수준의 [OSI 모델](https://en.wikipedia.org/wiki/OSI_model), 싶을 때 tooenable 보안의 상위 수준에 있을 수 있습니다 hello 스택입니다. Azure 파트너 네트워크 보안 어플라이언스 솔루션을 사용하여 이러한 향상된 네트워크 보안 기능에 액세스할 수 있습니다. Hello를 방문 하 여 hello 최신 Azure 파트너 네트워크 보안 솔루션을 찾을 수 있습니다 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) "보안" 및 "네트워크 보안 합니다."를 검색 하 고

### <a name="azure-virtual-network"></a>Azure Virtual Network

Azure 가상 네트워크 (VNet)는 hello 클라우드에서 사용자의 네트워크의 표현입니다. Azure 네트워크 패브릭 전용 tooyour 구독 hello의 논리적 격리는 Hello IP 주소 블록, DNS 설정, 보안 정책 및이 네트워크 내에서 경로 테이블을 완벽 하 게 제어할 수 있습니다. Azure Virtual Networks에서 VNet을 서브넷으로 분할하고 Azure IaaS VM(가상 컴퓨터) 및/또는 [Cloud services(PaaS 역할 인스턴스)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)를 배치할 수 있습니다.

Hello 중 하나를 사용 하 여 hello 가상 네트워크 tooyour 온-프레미스 네트워크를 연결할 수는 또한 [연결 옵션](https://docs.microsoft.com/azure/vpn-gateway/) Azure에서 사용할 수 있습니다. 기본적으로 Azure에서 제공 하는 엔터프라이즈 규모의 hello 혜택을 사용 하 여 IP 주소 블록에 완벽 한 제어 하 여 네트워크 tooAzure 확장할 수 있습니다.

Azure 네트워킹은 다양한 보안 원격 액세스 시나리오를 지원합니다. 그 중 일부는 다음과 같습니다.

-   [개별 워크스테이션 tooan Azure 가상 네트워크를 연결 합니다.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [온-프레미스 네트워크 tooan Azure 가상 네트워크 vpn 연결](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [전용된 WAN 링크를 사용 하 여 온-프레미스 네트워크 tooan Azure 가상 네트워크 연결](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [다른 Azure 가상 네트워크 tooeach 연결](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>VPN 게이트웨이
Azure 가상 네트워크와 온-프레미스 사이트 간의 네트워크 트래픽을 toosend 만들어야 VPN 게이트웨이 Azure 가상 네트워크에 대 한 합니다. [VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways)는 공용 연결을 통해 암호화된 트래픽을 보내는 가상 네트워크 게이트웨이의 유형입니다. 또한 Azure 네트워크 패브릭 hello 통해 Azure 가상 네트워크 간의 VPN 게이트웨이 toosend 트래픽을 사용할 수 있습니다.

### <a name="express-route"></a>Express 경로
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) 연결 공급자를 통해 지원 되는 전용된 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장할 수 있는 전용된 WAN 링크입니다.

![Express 경로](./media/azure-security/azure-security-fig1.png)

ExpressRoute를 사용 Microsoft Azure, Office 365, CRM Online과 같은 연결 tooMicrosoft 클라우드 서비스를 설정할 수 있습니다. 공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다.

ExpressRoute 연결은 공용 인터넷 hello 및 따라서 간주 될 수 있습니다 VPN 기반 솔루션 보다 더 안전 지나치지 않습니다. 이렇게 하면 express 경로 연결 toooffer 안정성, 빨라진 속도, 낮은 대기 시간, 및 일반 연결 보다 보안성이 높으며 더 많은 hello 인터넷을 통해.


### <a name="application-gateway"></a>응용 프로그램 게이트웨이
Microsoft [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)는 [ADC(Application Delivery Controller)](https://en.wikipedia.org/wiki/Application_delivery_controller)를 서비스로 제공하여 응용 프로그램에 다양한 계층 7 부하 분산 기능을 제공합니다.

![응용 프로그램 게이트웨이](./media/azure-security/azure-security-fig2.png)

있습니다 toooptimize 웹 팜 생산성을 CPU 집약적인 SSL 종료 toohello 응용 프로그램 게이트웨이 ("SSL 오프 로드" 또는 "SSL 브리징" 라고도 함)를 오프 로드 합니다. 들어오는 트래픽을, 쿠키 기반 세션 선호도, URL 경로 기반 라우팅 및 hello 기능 toohost 라운드 로빈 배포를 포함 하는 다른 계층 7 라우팅 기능 단일 응용 프로그램 게이트웨이 뒤에 있는 여러 웹 사이트도 제공 합니다. Azure Application Gateway는 계층 7 부하 분산 장치입니다.

장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다.

응용 프로그램은 HTTP 부하 분산, 쿠키 기반 세션 선호도, [SSL(Secure Sockets Layer)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타를 포함하여 많은 ADC 기능을 제공합니다.

### <a name="web-application-firewall"></a>웹 응용 프로그램 방화벽
웹 응용 프로그램 방화벽의 기능은 [Azure 응용 프로그램 게이트웨이](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) tooweb 응용 프로그램 표준 응용 프로그램 배달 제어 ADC () 함수에 대 한 응용 프로그램 게이트웨이 사용 하는 보호를 제공 하는 합니다. 웹 응용 프로그램 방화벽 대부분의 hello OWASP 상위 10 개의 일반적인 웹 취약점 으로부터 보호 하 여이 작업을 수행 합니다.

![웹 응용 프로그램 방화벽](./media/azure-security/azure-security-fig1.png)

-   SQL 삽입 공격 보호

-   명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호

-   HTTP 프로토콜 위반 보호

-   누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호

-   보트, 크롤러 및 스캐너 방지

-   일반적인 응용 프로그램 구성 오류(즉 Apache, IIS 등) 검색


웹 공격에 대 한 중앙 집중식된 웹 응용 프로그램 방화벽 tooprotect 보안 관리 보다 간단 하 게 만들고 침입 hello 위협 으로부터 더 나은 보증 toohello 응용 프로그램을 제공 합니다. WAF 솔루션와 각각의 개별 웹 응용 프로그램 보안을 중앙 위치에서 알려진된 취약점의 패치를 적용 하 여 tooa 보안 위협이 더 빠르게 반응 수 있습니다. 기존 응용 프로그램 게이트웨이 수와 웹 응용 프로그램 방화벽 tooan 응용 프로그램 게이트웨이 쉽게 변환 합니다.
### <a name="traffic-manager"></a>트래픽 관리자
Microsoft [Azure 트래픽 관리자](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) 여러 데이터 센터의 서비스 끝점에 대 한 사용자 트래픽의 toocontrol hello 배포 있습니다. Traffic Manager에서 지원하는 서비스 끝점에는 Azure VM, Web Apps 및 클라우드 서비스가 포함됩니다. 또한 외부, Azure가 아닌 끝점으로 Traffic Manager를 사용할 수 있습니다. 트래픽 관리자 사용 하 여 DNS 도메인 이름 () toodirect 클라이언트 요청에 따라 toohello 가장 적합 한 끝점 hello는 [트래픽 라우팅 방법](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) 및 hello 끝점의 hello 상태입니다.

트래픽 관리자는 트래픽 라우팅 방법 toosuit 다른 응용 프로그램 요구 끝점 상태 다양 한 제공 [모니터링](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring), 및 자동 장애 조치 합니다. 트래픽 관리자는 전체 Azure 지역의 hello 못하고 탄력적 toofailure입니다.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Azure 부하 분산 장치](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) 높은 가용성 및 네트워크 성능을 tooyour 응용 프로그램을 제공 합니다. 이 장치는 부하 분산 장치 집합에 정의된 서비스의 정상 인스턴스 간에 들어오는 트래픽을 분산하는 계층 4(TCP, UDP) 부하 분산 장치입니다. Azure Load Balancer를 다음과 같이 구성할 수 있습니다.

-   부하 분산 들어오는 인터넷 트래픽을 toovirtual 컴퓨터. 이 구성을 [인터넷 연결 부하 분산](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)이라고 합니다.

-   가상 네트워크의 가상 컴퓨터 간, 클라우드 서비스의 가상 컴퓨터 간 또는 크로스-프레미스 가상 네트워크의 온-프레미스 컴퓨터와 가상 컴퓨터 간에 트래픽을 부하 분산합니다. 이 구성을 [내부 부하 분산](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview)이라고 합. 

- 외부 트래픽 전달 tooa 특정 가상 컴퓨터

### <a name="internal-dns"></a>내부 DNS
Hello 목록 hello 네트워크 구성 파일 또는 hello 관리 포털에서에서 VNet에서 사용 되는 DNS 서버를 관리할 수 있습니다. 고객은 각 VNet에 대 한 too12 DNS 서버를 추가할 수 있습니다. DNS 서버를 지정할 경우에 중요 한 tooverify 고객의 환경에 대 한 hello 올바른 순서로 고객의 DNS 서버를 나열할 수 있습니다. DNS 서버 목록은 라운드 로빈 방식으로 작동하지 않으며, 지정 된 hello 순서에 사용 됩니다. Hello 목록에 첫 번째 DNS 서버 hello에 도달할 수 toobe 이면 hello 클라이언트 hello DNS 서버 여부 제대로 작동 하는지 여부에 관계 없이 해당 DNS 서버를 사용 합니다. toochange hello 고객의 가상 네트워크에 대 한 DNS 서버 순서 hello DNS 서버 hello 목록에서 제거 하 고 해당 고객 hello 순서로 다시 추가 하려고 합니다. DNS는 hello "CIA" 보안 두꺼운 수직선의 hello 가용성 측면을 지원합니다.

### <a name="azure-dns"></a>Azure DNS
hello [Domain Name System](https://technet.microsoft.com/library/bb629410.aspx), 또는 DNS는 변환 합니다 (또는 해결) 웹 사이트 또는 서비스 이름을 지정 tooits IP 주소입니다. [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview)는 Microsoft Azure 인프라를 사용하여 이름 확인을 제공하는 DNS 도메인에 대한 호스팅 서비스입니다. Azure에서 도메인을 호스트 하 여 DNS를 관리할 수 있습니다 레코드를 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, Api, 도구 및 대금 청구 hello 합니다. DNS는 hello "CIA" 보안 두꺼운 수직선의 hello 가용성 측면을 지원합니다.
### <a name="log-analytics-nsgs"></a>Log Analytics NSG
Nsg에 대 한 진단 로그 범주를 수행 하는 hello를 설정할 수 있습니다.
-   이벤트: 항목을 NSG에 대 한 규칙은 적용 된 tooVMs 및 MAC 주소에 따라 인스턴스 역할을 포함 합니다. 이러한 규칙에 대 한 hello 상태 60 초 마다 수집 됩니다.

-   규칙 카운터: 각 NSG 규칙은 적용 된 toodeny 횟수에 대 한 항목을 포함 하거나 트래픽을 허용 합니다.

### <a name="azure-security-center"></a>Azure 보안 센터
보안 센터를 사용 하면 방지 하 고 검색 toothreats, 응답 하 고 증가 하면에 대 한 가시성을 보고 제어할, hello Azure 리소스의 보안을 제공 합니다. Azure 구독을 통해 통합된 보안 모니터링 및 정책 관리를 제공하고, 달리 발견되지 않을 수도 있는 위협을 검색하는 데 도움이 되며, 보안 솔루션의 광범위한 에코시스템에서 작동합니다. 네트워크 권장 사항은 방화벽, 네트워크 보안 그룹, 인바운드 트래픽 규칙 구성 등에 초점을 맞추고 있습니다.

사용 가능한 네트워크 권장 사항은 다음과 같습니다.

-   [다음 생성 방화벽을 추가할](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) 추가할 것을 권장 다음 세대 방화벽 (NGFW)에서 Microsoft 파트너 tooincrease 보안 보호

-   [만 NGFW 트래픽을 라우팅하](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) 구성 하는 것을 권장 하는 인바운드 트래픽을 tooyour 프로그램 NGFW 통해 VM을 강제 하는 보안 그룹 (NSG) 규칙 네트워크입니다.

-   [서브넷 또는 가상 컴퓨터에서 네트워크 보안 그룹 사용](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups) - 서브넷 또는 VM에서 NSG를 사용하는 것이 좋습니다.

-   [인터넷 연결 끝점을 통한 액세스 제한](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints) - NSG에 대한 인바운드 트래픽 규칙을 구성하는 것이 좋습니다.


## <a name="compute"></a>계산

hello 섹션에서는 이러한 기능에 대 한이 영역 및 요약 정보에 대 한 주요 기능에 대 한 추가 정보를 제공 합니다.

### <a name="antimalware--antivirus"></a>맬웨어 방지 및 바이러스 백신
Azure IaaS와 같은 Microsoft "," Symantec "," Trend Micro "," McAfee "및" Kaspersky tooprotect 보안 공급 업체의 맬웨어 방지 소프트웨어 악의적인 파일, 애드웨어, 및 기타 위협을에서 가상 컴퓨터를 사용할 수 있습니다. Azure Cloud Services 및 Virtual Machines를 위한 [Microsoft 맬웨어 방지 프로그램](https://docs.microsoft.com/azure/security/azure-security-antimalware)은 바이러스, 스파이웨어 및 기타 악성 소프트웨어를 식별하고 제거하는 데 도움이 되는 보호 기능입니다. Microsoft 맬웨어 방지 자체 악성 또는 동의 없이 설치 된 소프트웨어 시도 tooinstall 알 수 없거나 Azure 시스템에서 실행 하는 경우 구성 가능한 알림을 제공 합니다. 또한 Microsoft 맬웨어 방지 프로그램은 Azure Security Center를 통해 배포할 수도 있습니다.

### <a name="hardware-security-module"></a>하드웨어 보안 모듈
암호화 및 인증 hello 키 자체는 보호 하지 않으면 보안을 향상 되지 않습니다. 에 저장 하 여 중요 한 암호 및 키의 hello 관리 및 보안을 간소화할 수 [Azure 키 자격 증명 모음](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)합니다. 주요 자격 증명 모음 hello 옵션 toostore 하드웨어 보안 모듈 (Hsm) 인증 된 tooFIPS 140-2 수준 2 표준에 키를 제공합니다. 백업 또는 [투명한 데이터 암호화](https://msdn.microsoft.com/library/bb934049.aspx)를 위한 SQL Server 암호화 키는 응용 프로그램의 키 또는 암호와 함께 주요 자격 증명 모음에 저장됩니다. 사용 권한 및 toothese 보호 된 항목 액세스를 통해 관리 되 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)합니다.

### <a name="virtual-machine-backup"></a>가상 컴퓨터 백업
[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)은 자본 투자 없이 최소의 운영 비용으로 응용 프로그램 데이터를 보호하는 솔루션입니다. 응용 프로그램 오류 데이터를 손상 될 수 있습니다 및 오류의 toosecurity 문제를 일으킬 수 있는 응용 프로그램에 버그가 발생할 수 있습니다. Azure Backup은 Windows 및 Linux를 실행하는 가상 컴퓨터의 보호에 도움이 됩니다.

### <a name="azure-site-recovery"></a>Azure Site Recovery
조직의 중요 한 부분이 [비즈니스 연속성/장애 복구 (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) 전략은 tookeep 회사 작업 부하 및 응용 프로그램을 실행 계획 및 계획 되지 않은 중단 발생 하는 방식을 파악 합니다. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)를 사용하면 기본 위치가 중단되는 경우 보조 위치에서 사용할 수 있도록 워크로드 및 앱의 복제, 장애 조치 및 복구를 오케스트레이션할 수 있습니다.

### <a name="sql-vm-tde"></a>SQL VM TDE
[TDE(투명한 데이터 암호화)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) 및 CLE(열 수준 암호화)는 SQL Server 암호화 기능입니다. 이 형식의 암호화는 고객 toomanage와 저장소 암호화 키 암호화에 사용할 hello 필요 합니다.

hello Azure 키 자격 증명 모음 (AKV) 서비스 안전 하 고 항상 사용 가능한 위치에 이러한 키의 디자인 된 tooimprove hello 보안 및 관리 됩니다. hello SQL Server 커넥터를 사용 하면 SQL Server toouse Azure 키 자격 증명 모음에서 이러한 키입니다.

온-프레미스 컴퓨터와 SQL Server를 실행 하는 경우 온-프레미스 SQL Server 컴퓨터에서 tooaccess Azure 키 자격 증명 모음을 수행할 수 있는 사항이 있습니다. 하지만 Azure Vm에서 SQL Server에 대 한 hello Azure 키 자격 증명 모음 통합 기능을 사용 하 여 시간을 절약할 수 있습니다. 몇 가지 Azure PowerShell cmdlet tooenable와이 기능을 자동화할 수 있습니다 hello 구성에 대 한 SQL VM tooaccess 필요한 주요 자격 증명 모음입니다.

### <a name="vm-disk-encryption"></a>VM 디스크 암호화
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)은 Windows 및 Linux IaaS 가상 컴퓨터 디스크를 암호화할 수 있게 하는 새로운 기능입니다. Windows hello 업계 표준 BitLocker 기능 및 운영 체제 hello에 대 한 Linux tooprovide 볼륨 암호화의 hello DM 암호화 기능 및 hello 데이터 디스크를 적용합니다. hello 솔루션은 Azure 키 자격 증명 모음 toohelp 제어 하 고 주요 자격 증명 모음 구독에서 hello 디스크 암호화 키 및 암호를 관리할와 통합 됩니다. hello 솔루션 하면 hello 가상 컴퓨터 디스크에 있는 모든 데이터가 Azure 저장소에 저장 된 상태의 암호화 됩니다.

### <a name="virtual-networking"></a>가상 네트워킹
가상 컴퓨터는 네트워크 연결이 필요합니다. toosupport 해당 요구 사항을 Azure 필요 연결 된 가상 컴퓨터 toobe tooan Azure 가상 네트워크입니다. Azure 가상 네트워크는 hello Azure 실제 네트워크 패브릭 기반으로 하는 논리적 구문입니다. 논리적 [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 각각은 다른 모든 Azure Virtual Network와 격리됩니다. 이 격리는 배포에서 네트워크 트래픽을 tooother 액세스할 수 있는 Microsoft Azure 고객과 아닌지 확인 합니다.

### <a name="patch-updates"></a>패치 업데이트
패치 업데이트 잠재적인 문제 확인 및 수정에 대 한 hello 기초를 제공 하 고 기업에 배포 해야 하는 소프트웨어 업데이트의 hello 수를 줄여 및 기능 toomonitor 늘려 모두 hello 소프트웨어 업데이트 관리 프로세스를 단순화 규정 준수 합니다.

### <a name="security-policy-management-and-reporting"></a>보안 정책 관리 및 보고
[Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro) 방지 하 고 검색 응답 toothreats를 활용 하 고에 대 한 가시성 및에 대 한 제어, Azure 리소스의 hello 보안 향상을 제공 합니다. Azure 구독을 통해 통합된 보안 모니터링 및 정책 관리를 제공하고, 달리 발견되지 않을 수도 있는 위협을 검색하는 데 도움이 되며, 보안 솔루션의 광범위한 에코시스템에서 작동합니다.

### <a name="azure-security-center"></a>Azure 보안 센터
보안 센터를 사용 하면 방지 하 고 검색에 대 한 향상 된 가시성 및 Azure 리소스의 보안을 hello에 대 한 제어를 사용 하 여 toothreats 응답할 수 있습니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

## <a name="identify-and-access-management"></a>ID 및 액세스 관리

시스템, 응용 프로그램 및 데이터 보안은 ID 기반 액세스 제어로 시작합니다. Microsoft 비즈니스 제품 및 서비스에 구축 된 hello id 및 액세스 관리 기능 도움말 때마다 하 고 아무 곳에 나 사용할 수 있는 toolegitimate 사용자 수 있도록 하는 동안 무단된 액세스 로부터 사용자의 조직 및 개인 정보 보호 할 수 있습니다.

### <a name="secure-identity"></a>보안 ID
Microsoft 제품 및 서비스 toomanage id 및 액세스를 통해 여러 보안 방법 및 기술을 사용합니다.
-   [Multi-factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/) hello 클라우드 및 온-프레미스 액세스를 위한 사용자 toouse 메서드가 여러 개 필요 합니다. 간단한 로그인 프로세스를 통해 사용자를 수용하면서 편리한 확인 옵션을 통해 강력한 인증을 제공합니다.

-   [Microsoft Authenticator](https://aka.ms/authenticator) - Microsoft Azure Active Directory 및 Microsoft 계정 모두에서 작동하는 친숙한 Multi-Factor Authentication 환경을 제공하고, 착용식 장치 및 지문 기반 승인을 지원합니다.

-   [암호 정책 적용](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) 증가 길이 및 복잡도 요구 사항, 정기적으로 회전을 강제 적용 하는 방식으로 기존의 암호의 보안을 hello 및 실패 한 인증 후 계정 잠금 시도 합니다.

-   [토큰 기반 인증](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) - AD FS(Active Directory Federation Service) 또는 타사 보안 토큰 시스템을 통해 인증할 수 있게 합니다.

-   [역할 기반 액세스 제어 (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) toogrant 액세스 hello 사용자에 따라 역할을 할당 하면, 사용자가 쉽게 toogive 사용자만 hello 제한 된 액세스 있어서 tooperform 자신의 작업 임무 합니다. 조직의 비즈니스 모델 및 위험 허용 범위에 따라 RBAC를 사용자 지정할 수 있습니다.

-   [Id 관리 (하이브리드 id)를 통합](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) 내부와 클라우드 데이터 센터를 플랫폼 간에 인증 및 권한 부여에 대 한 단일 사용자 id를 tooall 리소스를 만드는 toomaintain 사용자의 액세스 제어를 사용 합니다.

### <a name="secure-apps-and-data"></a>보안 앱 및 데이터
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 포괄적인 id 및 액세스 관리 클라우드 솔루션을 hello 클라우드 및 사이트에서 응용 프로그램에 대 한 보안 액세스 toodata 주며 사용자 및 그룹의 hello 관리를 단순화 합니다. 핵심 디렉터리 서비스, 고급 id 관리, 보안 및 응용 프로그램 액세스 관리를 결합 하며, 해당 앱에 개발자가 toobuild id 정책 기반 관리를 위한 쉽게. tooenhance Azure Active Directory를 Azure Active Directory Basic, 프리미엄 P1 및 P2 Premium edition hello 사용 하 여 유료 기능을 추가할 수 있습니다.

| 평가판/일반 기능     | Basic 기능    |Premium P1 기능 |Premium P2 기능 | Azure Active Directory 조인 – Windows 10 전용 관련 기능|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [디렉터리 개체](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [사용자/그룹 관리 (추가/업데이트/삭제) 사용자 기반 / 프로 비전, 장치 등록](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [Single Sign-on (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [셀프 서비스 클라우드 사용자를 위한 암호 변경을](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [연결 (온-프레미스 디렉터리 tooAzure Active Directory를 확장 하는 동기화 엔진)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [보안 / 사용 보고서](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [그룹 기반 액세스 관리/프로비전](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [클라우드 사용자를 위한 셀프 서비스 암호 재설정](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [회사 브랜딩(로그온 페이지/액세스 패널 사용자 지정)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [응용 프로그램 프록시](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [SLA 99.9%](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [셀프 서비스 그룹 및 응용 프로그램 관리/셀프 서비스 응용 프로그램 추가/동적 그룹](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [셀프 서비스 암호 재설정/변경/온-프레미스 쓰기 저장을 통한 잠금 해제](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [Multi-Factor Authentication(클라우드 및 온-프레미스(MFA 서버))](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [MIM CAL + MIM 서버](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [클라우드 앱 검색](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [그룹 계정에 대한 자동 암호 롤오버](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [ID 보호](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Azure AD 관리자가 Bitlocker 복구에 대 한 Microsoft Passport 장치 tooAzure AD, 데스크톱 SSO 가입](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM 자동 등록, 셀프 서비스 Bitlocker 복구, Azure 통해 로컬 관리자 추가 tooWindows 10 장치 AD 연결](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) hello 조직의 직원이 사용 하는 tooidentify 클라우드 응용 프로그램 수 있는 Azure Active Directory의 프리미엄 기능입니다.

- [Azure Active Directory Id 보호](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) Azure Active Directory 변칙 검색 기능 tooprovide 위험 이벤트와 영향을 줄 수 있는 잠재적 보안 문제에 대 한 통합된 뷰를 사용 하는 보안 서비스는 사용자 조직 id입니다.

- [Azure Active Directory 도메인 서비스](https://azure.microsoft.com/services/active-directory-ds/) hello toodeploy 도메인 컨트롤러 필요 없이 toojoin Azure Vm tooa 도메인을 사용 합니다. 사용자는 회사 Active Directory 자격 증명을 사용 하 여 toothese Vm에에서 로그인 및 리소스에 원활 하 게 액세스할 수 있습니다.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) 은 toohundreds 수백만 id의 크기를 조정 하 고 모바일에서 통합할 수 있는 소비자 용 응용 프로그램에는 항상 사용 가능한 글로벌 id 관리 서비스 및 웹 플랫폼입니다. 고객에 게 로그인 할 수 tooall 기존 소셜 미디어 계정을 사용 하는 사용자 지정 가능한 환경을 통해 앱 또는 새 독립 실행형 자격 증명을 만들 수 있습니다.

- [Azure Active Directory B2B 공동 작업](https://aka.ms/aad-b2b-collaboration) 보안 파트너 통합 솔루션을 사용 하 여 회사 간 관계를 지원 하더라도 파트너 tooaccess 회사 응용 프로그램과 데이터 선택적으로 해당 자체 관리 되는 사용 하 여은 id입니다.

- [Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) 중앙 집중식된 관리를 위해 tooextend 클라우드 기능 tooWindows 10 장치를 사용 하면 됩니다. 클라우드에 대 한 사용자가 tooconnect toohello 회사 또는 조직 Azure Active Directory를 통해 가능 하 게 하 고 액세스 tooapps 및 리소스를 간소화 합니다.

- [Azure Active Directory 응용 프로그램 프록시](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) - 온-프레미스에 호스팅되는 웹 응용 프로그램에 대해 SSO(Single Sign-On) 및 보안된 원격 액세스를 제공합니다.

## <a name="next-steps"></a>다음 단계
- [Microsoft Azure 보안 시작](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Azure 서비스 및 toohelp를 사용할 수 있는 기능 서비스 및 Azure 내에서 데이터 보안

- [Azure Security Center](https://azure.microsoft.com/services/security-center/)

방지 하 고 검색 toothreats 가시성을 높이기 및 Azure 리소스의 보안을 hello에 대 한 제어를 사용 하 여 응답

- [Azure Security Center에서 보안 상태 모니터링](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

hello Azure 보안 센터 toomonitor 준수 정책 사용 하 여 모니터링 되는 기능입니다.
