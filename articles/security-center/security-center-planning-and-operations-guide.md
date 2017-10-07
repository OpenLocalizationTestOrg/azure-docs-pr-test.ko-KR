---
title: "aaaSecurity 센터 계획 및 운영 가이드 | Microsoft Docs"
description: "이 문서를 사용 하면 tooplan 일상적인 작업에 대 한 고려 사항 및 Azure 보안 센터를 채택 하기 전에."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Azure 보안 센터 계획 및 작업 가이드
이 가이드는 정보 기술 (IT) 전문가, IT 설계자, 정보 보안 분석가 및 해당 조직이 toouse Azure 보안 센터를 계획 하는 클라우드 관리자에 대 한 합니다.

>[!NOTE] 
>보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다. 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>

## <a name="planning-guide"></a>계획 가이드
이 가이드의 단계와 사용자의 보안 센터 사용 하면 조직의 보안 요구 사항 및 클라우드 관리 모델에 따라 toooptimize 참고할 수 있는 작업 집합을 소개 합니다. tootake 완전히 활용 보안 센터를 중요 한 toounderstand 어떻게 서로 다른 개인 또는 팀에 조직 hello 서비스 toomeet 보안 개발 및 작동, 모니터링, 관리, 사용 및 사고 대응 요구 합니다. hello 주요 영역 tooconsider toouse 보안 센터를 계획할 때에

* 보안 역할 및 액세스 제어
* 보안 정책 및 권장 사항
* 데이터 수집 및 저장
* 지속적인 보안 모니터링
* 사고 대응

Hello 다음 섹션에 설명 합니다 방법을 tooplan 각 영역에 대 한 요구 사항에 따라 이러한 권장 사항을 적용 하 고 있습니다.

> [!NOTE]
> 읽기 [질문과 대답 (FAQ) Azure 보안 센터](security-center-faq.md) hello 디자인 및 계획 단계 동안 유용할 수 수도 있는 일반적인 질문의 목록에 대 한 합니다.
> 

## <a name="security-roles-and-access-controls"></a>보안 역할 및 액세스 제어
Hello 크기 및 사용자의 조직 구조에 따라 여러 개인과 팀 보안 센터 tooperform 다른 보안 관련 작업을 사용할 수 있습니다. 다음 다이어그램 hello 가상의 사용자 및 해당 역할 및 보안 책임의 예를 사용할 수 있습니다.

![역할](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

보안 센터 이러한 개인 toomeet 이러한 다양 한 책임을 수 있습니다. 예:

**Jeff(클라우드 워크로드 소유자)**

* 클라우드 워크로드와 관련 리소스를 관리
* 회사 보안 정책에 따라 보호를 구현하고 유지 관리하는 업무를 담당

**Ellen(CISO/CIO)**

* Hello 회사에 대 한 보안의 모든 측면에 대 한 책임
* Toounderstand hello 회사의 보안 상태는 클라우드 워크 로드 간에
* 요구 사항 toobe 주요 공격 및 위험에 대 한 안내

**David(IT 보안)**

* 집합 회사 tooensure hello에 대 한 적절 한 보호 사용 되는 보안 정책
* 정책 준수 여부를 모니터링
* 경영진 또는 감사를 위한 보고서를 작성

**Judy(보안 운영)**

* 모니터링 하 고 응답 toosecurity 경고 24/7
* 작업 소유자 tooCloud 또는 IT 보안 분석가 에스컬레이션합니다.

**Sam(보안 분석가)**

* 공격 여부 조사
* 클라우드 작업 소유자 tooapply 재구성 작업 

보안 센터를 사용 하 여 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md)를 제공 하는 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md) toousers, 그룹 및 Azure 서비스에에서 할당할 수 있습니다. 정보 표시 사용자가 보안 센터를 열면 tooresources 액세스할 수 있는 관련 합니다. 즉, hello 사용자가 소유자, 참가자 또는 판독기 toohello 구독 또는 리소스 그룹의 리소스에 속하는 hello 역할을 할당 합니다. 또한 toothese 역할에는 두 개의 특정 보안 센터 역할이 있습니다.

- **보안 판독기**: toothis 역할에 속하는 사용자 수 tooview 권한 tooSecurity 센터 권장 사항, 경고, 정책 및 상태를 포함 하는 수는 있지만 수 toomake 변경 하지 않습니다.
- **보안 관리자**: 동일 하지만 보안 판독기 수 hello 보안 정책 업데이트도 해제 권장 사항 및 경고 합니다.

위에서 설명한 hello 보안 센터 역할 저장소, 웹 및 모바일, 사물 인터넷 등 Azure의 액세스 tooother 서비스 영역을 갖지 않습니다.  

> [!NOTE]
> 사용자는 최소한 구독, 리소스 그룹 소유자 또는 참가자 toobe 수 toosee Azure 보안 센터 toobe 필요합니다. 
> 
> 

Hello 가상 사용자를 사용 하 여 다음 RBAC가 필요 합니다. hello hello 이전 다이어그램에 설명이 나와 있습니다.

**Jeff(클라우드 워크로드 소유자)**

* 리소스 그룹 소유자/협업자

**David(IT 보안)**

* 구독 소유자/협력자 또는 보안 관리자

**Judy(보안 운영)**

* 구독 판독기 또는 보안 사용자 tooview 경고
* 구독 소유자/협력자 또는 보안 관리자 필요한 toodismiss 경고

**Sam(보안 분석가)**

* 구독 사용자 tooview 경고
* 구독 소유자/공동 작업자 필요한 toodismiss 경고
* Toohello 작업 영역 액세스 해야 할 수 있습니다.

다른 중요 한 정보 tooconsider:

* 구독 소유자/참가자 및 보안 관리자만 보안 정책을 편집할 수 있음
* 구독 및 리소스 그룹 소유자 및 참가자만 리소스에 대한 보안 권장 사항을 적용할 수 있음

RBAC를 사용 하 여 보안 센터에 대 한 액세스 제어를 계획할 때는 보안 센터를 사용 하는 조직에 게 있는지 toounderstand 수 있습니다. 또한 수행할 작업 유형을 확인한 다음 RBAC을 적합하게 구성합니다.

> [!NOTE]
> Hello를 할당 하는 것이 좋습니다 사이의 역할 작업 사용자 toocomplete에 필요 합니다. 예를 들어 사용자에 게 리소스의 hello 보안 상태에 대 한 정보 tooview 하지만 권장 구성 적용 정책 편집 등의 작업 수행 하지만 hello 읽기 역할을 할당 되어야 합니다.
> 
> 

## <a name="security-policies-and-recommendations"></a>보안 정책 및 권장 사항
지정 된 hello 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 하는 보안 정책을 구독 합니다. 보안 센터 tooyour 회사의 보안 요구 사항 및 응용 프로그램의 hello 유형 또는 hello 데이터의 민감도 따라 정책을 정의 합니다.

Hello 다음 다이어그램에에서 표시 된 대로 hello 구독 내에서 tooall 리소스 그룹을 전파 하는 hello 구독 수준에 자동으로 설정 된 정책:

![보안 정책](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> 어떤 정책이 변경 된 tooreview 필요한 경우 사용할 수 있습니다 [Azure 감사 로그](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/)합니다. 정책 변경은 항상 Azure 감사 로그에 기록됩니다.
> 
> 

### <a name="security-recommendations"></a>보안 권장 사항
보안 정책을 구성 하기 전에 각 hello 검토 [보안 권장 사항](security-center-recommendations.md), 이러한 정책은 다양 한 구독 및 리소스 그룹에 적절 한 되는지 여부를 확인 합니다. 것도 중요 한 toounderstand 조치를 취해야 tooaddress [보안 권장 사항](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) 조직에서 누가 새 권장 사항 및 라인 hello 필요한 단계에 대 한 모니터링을 담당 됩니다.

Security Center는 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 것을 권장합니다. 이 정보는 Microsoft toocontact 하 여 사용 Microsoft 보안 대응 센터 (MSRC) hello 발견 불법 또는 무단 당사자가 고객 데이터에 액세스 하 고 있습니다. 읽기 [Azure 보안 센터에서 보안 연락처 세부 정보를 제공](security-center-provide-security-contact-details.md) 방법에 대 한 자세한 내용은 tooenable이이 권장 합니다.

## <a name="data-collection-and-storage"></a>데이터 수집 및 저장
Azure 보안 센터 hello Microsoft Monitoring Agent를 사용 하 여 –이 hello Operations Management Suite 및 로그 분석 서비스 – 가상 컴퓨터에서 보안 데이터 toocollect hello 동일한 에이전트를 사용 합니다. 이 에이전트에서 수집된 데이터는 Log Analytics 작업 영역에 저장됩니다.

### <a name="agent"></a>에이전트

Hello 보안 정책에서 데이터 수집을 활성화 한 후 Microsoft Monitoring Agent hello (에 대 한 [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) 또는 [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents))에 지원 되는 모든 Azure Vm 및 만들어진 새로 설치 합니다.  현재 hello hello VM에 이미 설치 된 Microsoft Monitoring Agent hello Azure 보안 센터를 활용 하는 경우 에이전트를 설치 합니다. hello 에이전트 프로세스 디자인 된 toobe 침투성 이며 VM 성능에 최소한의 영향을 줄 합니다.

Microsoft 모니터링 에이전트에 대 한 Windows hello 사용 하 여 TCP 포트 443 필요합니다. Hello 참조 [문제 해결 문서](security-center-troubleshooting-guide.md) 추가 세부 정보에 대 한 합니다.

특정 시점에 toodisable 데이터 수집을 원하는 경우 있습니다 수 해제 hello 보안 정책에서. 그러나 다른 Azure management에서 hello Microsoft Monitoring Agent를 사용할 수 있으며 서비스를 모니터링, hello 에이전트 제거 되지 것입니다 자동으로 하기 때문에 해제 하면 보안 센터에서 데이터를 수집 합니다. 필요한 경우 hello 에이전트를 수동으로 제거할 수 있습니다.

> [!NOTE]
> toofind hello 읽기를 지원 되는 Vm의 목록 [질문과 대답 (FAQ) Azure 보안 센터](security-center-faq.md)합니다.
> 

### <a name="workspace"></a>작업 영역

(Azure 보안 센터) 대신 하 여 Microsoft Monitoring Agent는 기존 로그 분석 중에 저장 되는 hello에서 수집 된 데이터 또는 연결 된 Azure 구독 새 중 계정 hello hello VM의 지역을 고려 합니다. 

Hello Azure 포털, Azure 보안 센터에서 만든을 포함 하 여, 로그 분석 작업 영역 목록이 toosee를 찾아볼 수 있습니다. 새 작업 영역에 관련된 리소스 그룹이 만들어질 수 있습니다. 둘 다 다음과 같은 명명 규칙을 따릅니다. 

* 작업 영역: *DefaultWorkspace-[subscription-ID]-[geo]*
* 리소스 그룹: *DefaultResouceGroup-[geo]*

Azure Security Center에서 만든 작업 영역의 경우 데이터는 30일 동안 보존됩니다. 작업 영역을 종료 하는 데 보존은 가격 책정 계층 hello 작업 영역을 기반으로 합니다.

> [!NOTE]
> Microsoft는 강력한 약정 tooprotect hello 개인 정보 및이 데이터의 보안을 확인 합니다. Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다. 데이터 처리 및 개인 정보 보호에 대한 자세한 내용은 [Azure Security Center 데이터 보안](security-center-data-security.md)을 참조하세요.
> 

## <a name="ongoing-security-monitoring"></a>지속적인 보안 모니터링
초기 구성 및 보안 센터 권장 사항 적용 한 후 다음 단계 hello 보안 센터 운영 프로세스 고려 하는 합니다.

보안 센터 hello 클릭할 수 있는 Azure 포털에서에서 tooaccess **찾아보기** 유형과 **보안 센터** hello에 **필터** 필드입니다. hello 뷰는 hello 사용자 가져옵니다 기반으로 하는 toothese 적용 된 필터, 아래 hello 예제 주소를 지정 하는 많은 문제 toobe 된 환경을 보여 줍니다.

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> 보안 센터 일반 운영 절차를 방해 하지 않도록, 수 동적으로 배포를 모니터링 하 고 사용 하도록 설정한 hello 보안 정책에 따라 권장 사항을 제공 합니다.

먼저 현재 Azure 환경에 대 한 보안 센터 toouse에서 선택, 하는 경우 hello에서 변환을 수행할 수 있는 모든 권장 사항을 검토 하 고 있는지 확인 **권장 사항을** 타일 또는 리소스 당 (**계산** **네트워킹**, **데이터 및 저장소**, **응용 프로그램**).

모든 권장 사항을 해결 되 면 hello **방지** 섹션 주소가 지정 된 모든 리소스에 대 한 녹색 이어야 합니다. 지속적인 모니터링이 시점에서 ý ´ ï 이후 hello 리소스 보안 상태 및 권장 사항 타일의 변화에 따라 작업만 사용 됩니다.

hello **검색** 섹션은 더 사후, 이들은 중 하나가 진행 중인은 now, 또는 지난 hello에서 발생 했으며 보안 센터 컨트롤과 제 3 자 시스템에서 검색 된 하는 문제에 대 한 경고입니다. hello 보안 경고 타일 hello 각 날짜 및 해당 배포 hello 다른 심각도 범주 (낮음, 보통, 높음) 사이 발견 된 위협 검색 경고 수를 나타내는 막대 그래프에 표시 됩니다. 보안 경고에 대 한 자세한 내용은 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다.

> [!NOTE]
> Microsoft Power BI toovisualize 보안 센터 데이터 활용할 수 있습니다. [Power BI로 Azure Security Center 데이터에서 정보 얻기](security-center-powerbi.md)를 읽어보세요.
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>새 또는 변경된 리소스 모니터링
대부분의 Azure 환경은 동적이며, 새 리소스가 일정 기준, 구성 또는 변경에 따라 확장 및 분리됩니다. 보안 센터를 사용 하면 이러한 새 리소스의 hello 보안 상태에 대 한 가시성을 해야 합니다.

새 리소스 (Vm, SQL Db) tooyour Azure 환경에 추가 하면 보안 센터 자동으로 이러한 리소스를 검색 하 고 toomonitor의 보안을 시작 합니다. 또한 PaaS 웹 역할 및 작업자 역할이 포함됩니다. Hello 데이터 수집을 활성화 한 경우 [보안 정책](security-center-policies.md)추가 모니터링 기능을 설정할 자동으로 가상 컴퓨터에 대 한 합니다.

![주요 영역](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. 가상 컴퓨터의 경우 **방지** 섹션에서 **계산**을 클릭합니다. Hello에 관련 데이터 또는 관련된 권장 사항을 사용 하도록 설정 된 모든 문제 표시지 것입니다 **개요** 탭 및 **권장 사항을 모니터링** 섹션.
2. 보기 hello **권장 사항을** toosee 부분, 보안 위험 hello 새 리소스에 대해 확인 된 경우.
3. 새 Vm tooyour 환경에 추가 되 면 hello 운영 체제만 처음 설치는 매우 일반적입니다. hello 리소스 소유자 이러한 Vm에서 사용할 수 있는 다른 앱 일부 시간 toodeploy 할 수 있습니다.  이상적으로이 작업의 최종 목적은 hello를 알고 있어야 합니다. Toobe 응용 프로그램 서버에 배포할? 내용에이에 따라 새 작업은 진행 중인 toobe, 적절 한 hello를 사용 하도록 설정할 수 **보안 정책**,이 워크플로의 세 번째 단계인 hello 합니다.
4. 새 리소스 tooyour Azure 환경에 추가 되 면 있기 hello에 새 경고 나타나는지 **보안 경고** 바둑판식으로 배열입니다. 항상이 타일에 새로운 경고가 없는지 확인 하 고 tooSecurity 센터 권장 사항에 따라 작업을 수행 합니다.

또한 tooregularly 모니터 hello 상태 보안 위험에 생성 된 기존 리소스 tooidentify 구성 변경을 권장 기준과 보안 경고에서 변경 해야 합니다. Hello 보안 센터 대시보드를 시작 합니다. 여기에서 일관적 세 가지 주요 영역 tooreview를 해야합니다.

![작업](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. hello **방지** 섹션 패널 빠른 액세스 tooyour 주요 리소스를 제공 합니다. 이 옵션 toomonitor 계산, 네트워킹, 저장소 및 데이터와 응용 프로그램을 사용 합니다.
2. hello **권장 사항을** 패널에서는 tooreview 보안 센터 권장 사항입니다. 지속적인 모니터링 하는 동안이 정상 hello 초기 보안 센터 설정에서 모든 권장 사항을 해결 하는 이후 매일 권장 사항을 권한이 없다는 것을 알 수 있습니다. 이러한 이유로 있습니다 수 새 정보에이 섹션 매일 없으며 tooaccess 있어야 합니다 필요에 따라 것입니다.
3. hello **검색** 섹션 매우 자주 또는 아주 드물게 기준 변경 될 수 있습니다. 항상 보안 경고를 검토하고 보안 센터 권장 사항에 따라 조치를 취합니다.

## <a name="incident-response"></a>사고 대응
보안 센터 감지 하 고 사용자에 게 경고 toothreats 발생할 때. 조직에서는 새 보안 경고에 대 한 모니터링 및 필요한 tooinvestigate 추가로으로 작업을 수행 하거나 hello 공격을 해결 해야 합니다. Security Center 위협 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참고하세요.

이 문서에서 되어 있지 않으면 hello 의도 tooassist 사고 대응 계획을 직접 만드는 동안 하겠습니다 hello 클라우드 수명 주기에서 Microsoft Azure 보안 응답 toouse hello 기반으로 사고 대응 단계에 대 한 합니다. hello 단계 hello 다음 다이어그램에에서 나와 있습니다.

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> National Institute of Standards hello 및 기술 NIST ()를 사용할 수 있습니다 [컴퓨터 보안 인시던트를 처리 가이드](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) 참조 tooassist으로 직접 작성할 수 있습니다.
> 

보안 센터 알림을 hello 단계를 수행 하는 동안 사용할 수 있습니다.

* **감지**: 하나 이상의 리소스에서 의심스러운 작업을 식별합니다. 
* **평가**: hello 초기 평가 tooobtain hello 의심 스러운 활동에 대 한 자세한 정보를 수행 합니다.
* **진단**: hello 재구성 단계 tooconduct hello 기술 프로시저 tooaddress hello 문제를 사용 합니다.

각 보안 경고 사용할 수 있는 정보를 제공 toobetter hello 공격의 hello 특성을 이해 하 고 가능한 완화 기능을 제안 합니다. 일부 경고는 또한 링크 tooeither 정보 Azure 내에서 더 많은 정보 또는 tooother 원본을 제공합니다. 추가 연구 및 toobegin 완화를 제공 하는 hello 정보를 사용할 수 있습니다 및 작업 영역에 저장 되어 있는 보안 관련 데이터를 검색할 수도 있습니다.

hello 다음 예제는 수행 하는 의심 스러운 RDP 활동.

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

볼 수 있듯이이 블레이드는 hello 공격이 발생 hello 시간과 관련 된 세부 정보를 표시, 원본 호스트 이름은 hello, 대상 VM hello 및 또한 권장 단계를 제공 합니다. 일부 경우 hello에 hello 공격에 대 한 소스 정보는 비어 있을 수 있습니다. 이러한 동작 유형에 대한 자세한 내용은 [Azure Security Center 경고에 누락된 원본 정보](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) 를 참고하세요.

Hello에 [tooLeverage 인시던트 응답에 대 한 Azure 보안 센터 & Microsoft Operations Management Suite을 hello 어떻게](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) 비디오 볼 수 있습니다 수 있는 각 보안 센터를 사용할 수 있는 방법을 toounderstand 일부 데모 이러한 단계 중 하나입니다.

> [!NOTE]
> 읽기 [인시던트 응답에 대 한 Azure 보안 센터 Leveraging](security-center-incident-response.md) toouse 보안 센터 기능 tooassist 처리 하는 방법은 사고 대응 하는 동안 대 한 자세한 내용은 합니다. 
> 
> 

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 tooplan 보안 센터 채택 합니다. 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답](security-center-managing-and-responding-alerts.md)
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

