---
title: "보안 센터 계획 및 작업 가이드| Microsoft Docs"
description: "이 문서는 Azure 보안 센터 도입 전 계획과 일상 운영과 관련한 고려 사항을 지원합니다."
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
ms.openlocfilehash: c502e4363dbaa37455d1aad90d1e9fa855fd09b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Azure 보안 센터 계획 및 작업 가이드
이 가이드는 Azure Security Center의 사용을 계획 중인 정보 기술(IT) 전문가, IT 설계자, 정보 보안 분석가 및 클라우드 관리자를 대상으로 합니다.

>[!NOTE] 
>2017년 6월 초를 시작으로 Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집 및 저장합니다. 자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요. 이 문서의 정보는 Microsoft Monitoring Agent로 전환된 후의 Security Center 기능을 나타냅니다.
>

## <a name="planning-guide"></a>계획 가이드
이 가이드에서는 조직의 보안 요구 사항과 클라우드 관리 모델에 따라 보안 센터의 사용을 최적화하기 위해 따를 수 있는 일련의 단계 및 작업을 다룹니다. Security Center를 완벽하게 활용하려면 조직의 서로 다른 개인 또는 팀이 보안 개발 및 운영, 모니터링, 관리 및 사고 대응 요구에 맞게 서비스를 사용하는 방법에 대해 이해하는 것이 중요합니다. 보안 센터의 사용을 계획할 때 고려할 주요 영역은 다음과 같습니다.

* 보안 역할 및 액세스 제어
* 보안 정책 및 권장 사항
* 데이터 수집 및 저장
* 지속적인 보안 모니터링
* 사고 대응

다음 섹션에서는 요구 사항에 따라 이러한 각각의 영역을 계획하고 권장 사항을 적용하는 방법에 대해 학습합니다.

> [!NOTE]
> [Azure 보안 센터 FAQ(질문과 대답)](security-center-faq.md) 설계 및 계획 단계에서 유용할 수 있는 일반적인 질문의 목록을 읽어 보세요.
> 

## <a name="security-roles-and-access-controls"></a>보안 역할 및 액세스 제어
조직의 규모와 구조에 따라, 여러 개인과 팀이 보안 센터를 통해 서로 다른 보안 관련 업무를 수행할 수 있습니다. 다음 다이어그램에는 가상의 사용자와 그 역할 및 보안 책임의 예가 나와 있습니다.

![역할](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

이러한 개인들은 보안 센터를 통해 다양한 책임에 부합할 수 있습니다. 예:

**Jeff(클라우드 워크로드 소유자)**

* 클라우드 워크로드와 관련 리소스를 관리
* 회사 보안 정책에 따라 보호를 구현하고 유지 관리하는 업무를 담당

**Ellen(CISO/CIO)**

* 회사의 모든 보안 업무를 담당
* 클라우드 워크로드에 걸쳐 회사의 보안 태세를 파악하고자 함
* 주요 공격 및 위험에 대해 숙지해야 함

**David(IT 보안)**

* 적절한 보호 조치가 마련되도록 회사 보안 정책을 설정
* 정책 준수 여부를 모니터링
* 경영진 또는 감사를 위한 보고서를 작성

**Judy(보안 운영)**

* 보안 경고를 연중무휴(24/7) 모니터링하고 대응
* 클라우드 워크로드 소유자 또는 IT 보안 분석가에게 보안 문제 제기

**Sam(보안 분석가)**

* 공격 여부 조사
* 클라우드 워크로드 소유자와 함께 해결책 적용 

Security Center는 Azure에서 사용자, 그룹 및 서비스에 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 제공하는 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md)를 사용합니다. 사용자가 Security Center를 열면 액세스한 리소스와 관련된 정보만 표시됩니다. 이는 구독 또는 리소스가 속한 리소스 그룹에 대한 소유자, 참가자 또는 읽기 권한자의 역할이 사용자에게 할당된다는 것을 의미합니다. 이러한 역할 외에도 두 개의 특정한 Security Center 역할이 있습니다.

- **보안 읽기 권한자**: 이 역할에 속하는 사용자는 권장 사항, 경고, 정책 및 상태를 포함하여 Security Center에 대한 권한을 볼 수 있지만 변경할 수는 없습니다.
- **보안 관리자**: 보안 읽기 권한자와 동일하지만 보안 정책을 업데이트하고 권장 사항 및 경고를 해제할 수 있습니다.

위에서 설명한 Security Center 역할은 Storage, 웹 및 모바일, 사물 인터넷 등 Azure의 다른 서비스 영역에 액세스할 수 없습니다.  

> [!NOTE]
> 사용자는 적어도 Azure에서 Security Center를 볼 수 있는 구독, 리소스 그룹 소유자 또는 참가자여야 합니다. 
> 
> 

이전 다이어그램에 설명된 가상 사용자를 사용하는 경우 다음 RBAC가 필요합니다.

**Jeff(클라우드 워크로드 소유자)**

* 리소스 그룹 소유자/협업자

**David(IT 보안)**

* 구독 소유자/협력자 또는 보안 관리자

**Judy(보안 운영)**

* 경고를 보는 구독 읽기 권한자 또는 보안 읽기 권한자
* 경고를 해제하는 데 필요한 구독 소유자/협력자 또는 보안 관리자

**Sam(보안 분석가)**

* 경고를 보는 구독 읽기 권한자
* 경고를 해제하는 데 필요한 구독 소유자/협력자
* 작업 영역에 대한 액세스가 필요할 수 있음

고려가 필요한 몇 가지 다른 중요 정보:

* 구독 소유자/참가자 및 보안 관리자만 보안 정책을 편집할 수 있음
* 구독 및 리소스 그룹 소유자 및 참가자만 리소스에 대한 보안 권장 사항을 적용할 수 있음

Security Center의 RBAC을 사용하여 액세스 제어를 계획하는 경우, Security Center를 사용할 조직 내 대상을 알아야 합니다. 또한 수행할 작업 유형을 확인한 다음 RBAC을 적합하게 구성합니다.

> [!NOTE]
> 사용자가 자신의 작업을 완료하는 데 필요한 최소한의 역할을 할당하는 것이 좋습니다. 예를 들어, 리소스의 보안 상태에 대한 정보를 보기만 하고 권장 사항 적용이나 정책 편집 등의 조치는 취하지 않는 사용자라면 읽기 권한자 역할을 할당해야 합니다.
> 
> 

## <a name="security-policies-and-recommendations"></a>보안 정책 및 권장 사항
보안 정책은 지정된 구독 내에서 리소스에 대해 권장되는 제어 집합을 정의합니다. 보안 센터에서 회사의 보안 요구 사항 및 응용 프로그램 유형 또는 데이터 민감도에 따라 정책을 정의합니다.

구독 수준에서 실행된 정책은 다음 다이어그램에 표시된 것처럼 구독 내 모든 리소스 그룹에 자동으로 전파됩니다.

![보안 정책](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> 어떤 정책이 변경되었는지 검토가 필요한 경우 [Azure 감사 로그](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/)를 사용할 수 있습니다. 정책 변경은 항상 Azure 감사 로그에 기록됩니다.
> 
> 

### <a name="security-recommendations"></a>보안 권장 사항
보안 정책을 구성하기 전에 각각의 [보안 권장 사항](security-center-recommendations.md)을 검토하여 이들 정책이 다양한 구독 및 리소스 그룹에 적합한지 판단합니다. [보안 권장 사항](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations)을 확인하기 위해 취해야 하는 조치 및 조직에서 새 권장 사항을 모니터링하고 필요한 단계를 수행하는 담당자를 알아야 합니다.

Security Center는 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 것을 권장합니다. 이 정보는 MSRC(Microsoft 보안 대응 센터)에서 불법적인 또는 권한 없는 당사자가 고객 데이터에 액세스한 것을 발견하는 경우 사용자에게 연락하기 위해 Microsoft에서 사용됩니다. 이 권장 사항을 사용하는 방법에 대한 자세한 내용은 [Azure Security Center에 보안 연락처 세부 정보 제공](security-center-provide-security-contact-details.md) 을 참고하세요.

## <a name="data-collection-and-storage"></a>데이터 수집 및 저장
Azure Security Center는 가상 컴퓨터에서 보안 데이터를 수집하는 데 Microsoft Monitoring Agent를 사용하며 이는 Operations Management Suite 및 Log Analytics 서비스에서 사용하는 동일한 에이전트입니다. 이 에이전트에서 수집된 데이터는 Log Analytics 작업 영역에 저장됩니다.

### <a name="agent"></a>에이전트

데이터 수집이 보안 정책에서 활성화된 후에 Microsoft Monitoring Agent([Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) 또는 [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)용)는 지원되는 모든 Azure VM 및 새로 만들어진 VM에 설치됩니다.  VM이 Microsoft Monitoring Agent에 이미 설치된 경우 Azure Security Center는 현재 설치된 에이전트를 활용합니다. 에이전트의 프로세스는 사용자 작업에 영향을 미치지 않으며 VM의 성능에도 거의 영향을 미치지 않습니다.

Windows용 Microsoft Monitoring Agent는 TCP 포트 443을 사용해야 합니다. 추가 세부 정보는 [문제 해결 문서](security-center-troubleshooting-guide.md)를 참조하세요.

데이터 수집을 사용하지 않으려는 특정 지점의 경우 보안 정책에서 수집을 해제할 수 있습니다. 그러나 다른 Azure Management 및 모니터링 서비스에서 Microsoft Monitoring Agent를 사용할 수 있기 때문에 Security Center에서 데이터 수집을 끄는 경우에도 자동으로 에이전트를 제거하지 않습니다. 필요한 경우 에이전트를 수동으로 제거할 수 있습니다.

> [!NOTE]
> 지원되는 VM 목록을 찾아보려면 [Azure Security Center FAQ](security-center-faq.md)를 읽어보세요.
> 

### <a name="workspace"></a>작업 영역

(Azure Security Center 대신) Microsoft Monitoring Agent에서 수집된 데이터는 VM의 지역을 고려하여 Azure 구독 또는 새 작업 영역에 연결된 기존 Log Analytics 작업 영역 중 하나에 저장됩니다. 

Azure Portal에서 Azure Security Center에서 만든 항목을 포함하여 Log Analytics 작업 영역 목록을 찾아볼 수 있습니다. 새 작업 영역에 관련된 리소스 그룹이 만들어질 수 있습니다. 둘 다 다음과 같은 명명 규칙을 따릅니다. 

* 작업 영역: *DefaultWorkspace-[subscription-ID]-[geo]*
* 리소스 그룹: *DefaultResouceGroup-[geo]*

Azure Security Center에서 만든 작업 영역의 경우 데이터는 30일 동안 보존됩니다. 기존 작업 영역의 경우 작업 영역 가격 책정 계층에 따라 보존됩니다.

> [!NOTE]
> Microsoft는 이 데이터의 개인 정보 및 보안을 보호하기 위해 노력하고 있습니다. Microsoft는 코딩부터 서비스에 이르기까지 엄격한 규정 준수 및 보안 지침을 따릅니다. 데이터 처리 및 개인 정보 보호에 대한 자세한 내용은 [Azure Security Center 데이터 보안](security-center-data-security.md)을 참조하세요.
> 

## <a name="ongoing-security-monitoring"></a>지속적인 보안 모니터링
보안 센터 권장 사항의 최초 구성과 적용 후에는 보안 센터 운영 프로세스를 고려합니다.

Azure 포털에서 Security Center에 액세스하려면 **찾아보기**를 클릭하고 **필터** 필드에 **Security Center**를 입력합니다. 사용자가 사용하는 보기는 이렇게 적용된 필터에 따라 다릅니다. 아래 예제에서는 많은 문제를 해결해야 하는 환경을 보여줍니다.

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Security Center는 일반 작동 프로시저를 방해하지 않으면서 배포를 소극적으로 모니터링하고 사용자가 설정한 보안 정책에 따라 권장 사항을 제공합니다.

현재 Azure 환경에 Security Center를 사용하도록 처음으로 설정할 때는 모든 권장 사항을 검토해야 합니다. 이 작업은 **권장 사항** 타일에서 또는 리소스별(**계산**, **네트워킹**, **저장소 및 데이터**, **응용 프로그램**)로 수행할 수 있습니다.

모든 권장 사항을 해결한 후에는 해결된 모든 리소스에 대해 **방지** 섹션이 녹색이어야 합니다. 이 시점에서는 리소스 보안 상태와 권장 사항 타일에서의 변경 사항을 기준으로 조치를 취하면 되므로 지속적인 모니터링이 더 용이해집니다.

**감지** 섹션은 더 대응적인 부분으로, 지금 발생 중이거나 과거에 발생하여 Security Center 컨트롤과 타사 시스템에서 감지된 문제와 관련한 경고입니다. 보안 경고 타일은 매일 확인된 위협 감지의 수를 나타내는 막대 그래프와, 여러 심각도 카테고리(낮음, 중간, 높음) 간의 분포를 표시합니다. 보안 경고에 대한 자세한 내용은 [Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)을 읽어보세요.

> [!NOTE]
> Microsoft Power BI를 활용하여 Security Center 데이터를 시각화할 수도 있습니다. [Power BI로 Azure Security Center 데이터에서 정보 얻기](security-center-powerbi.md)를 읽어보세요.
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>새 또는 변경된 리소스 모니터링
대부분의 Azure 환경은 동적이며, 새 리소스가 일정 기준, 구성 또는 변경에 따라 확장 및 분리됩니다. Security Center는 이러한 새 리소스의 보안 상태에 대한 정보를 얻는 데 도움이 됩니다.

Azure 환경에 새 리소스(VM, SQL DB)를 추가하면 보안 센터가 자동으로 해당 리소스를 감지하고 보안을 모니터링하기 시작합니다. 또한 PaaS 웹 역할 및 작업자 역할이 포함됩니다. [보안 정책](security-center-policies.md)에서 데이터 수집을 사용하도록 설정한 경우 가상 컴퓨터에 대해 추가적인 모니터링 기능이 자동으로 적용됩니다.

![주요 영역](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. 가상 컴퓨터의 경우 **방지** 섹션에서 **계산**을 클릭합니다. 데이터를 사용하도록 설정하는 것과 관련한 문제나 관련 권장 사항은 **개요** 탭 및 **모니터링 권장 사항** 섹션에 표시됩니다.
2. 새 리소스에 대한 보안 위협이 있다면 무엇인지를 확인하기 위해 **권장 사항** 을 봅니다.
3. 새 VM이 환경에 추가되면 운영 체제만 최초로 설치되는 것이 매우 일반적입니다. 리소스 소유자는 이러한 VM에서 사용할 다른 앱을 배포하는 데 다소 시간이 걸릴 수 있습니다.  이상적으로는 이 워크로드의 최종 목적을 파악하고 있어야 합니다. 응용 프로그램 서버가 됩니까? 이 새 워크로드의 용도에 맞게 적절한 **보안 정책**을 사용하도록 설정할 수 있으며, 이 워크플로의 세 번째 단계에 해당합니다.
4. 새 리소스가 Azure 환경에 추가되면 **보안 경고** 타일에 새 경고가 표시될 수 있습니다. 항상 이 타일에 새 경고가 있는지 확인하고 보안 센터 권장 사항에 따라 조치를 취합니다.

또한 기존 리소스 상태를 정기적으로 모니터링하여 보안 위험을 초래하고 권장 기준에 미치지 못하는 구성 변경 내용과 보안 경고를 파악하고자 할 수 있습니다. 보안 센터 대시보드에서 시작합니다. 여기에서는 일관된 기준에 따라 3가지 주요 영역을 검토하게 됩니다.

![작업](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. **방지** 섹션 패널은 주요 리소스에 대한 신속한 액세스를 제공합니다. 이 옵션을 사용하여 계산, 네트워킹, 저장소와 데이터 및 응용 프로그램을 모니터링합니다.
2. **권장 사항** 패널에서 Security Center 권장 사항을 검토할 수 있습니다. 지속적인 모니터링이 이루어질 때는 매일 권장 사항이 있는 것이 아닙니다. 이것은 최초 Security Center 설정 시 모든 권장 사항을 해결했기 때문에 정상입니다. 따라서 매일 이 섹션에 새 정보가 있는 것은 아니며 필요에 따라 액세스하면 됩니다.
3. **감지** 섹션은 매우 자주 또는 매우 드물게 변경될 수 있습니다. 항상 보안 경고를 검토하고 보안 센터 권장 사항에 따라 조치를 취합니다.

## <a name="incident-response"></a>사고 대응
보안 센터는 위협이 발생하면 감지하여 사용자에게 경고합니다. 조직에서는 새 보안 경고를 모니터링하고 필요에 따라 조치를 통해 추가적인 조사를 수행하거나 공격에 대처해야 합니다. Security Center 위협 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참고하세요.

이 문서가 인시던트 대응 계획을 직접 작성하는 데 도움을 주려는 목적은 아니지만 인시던트 대응 단계에 대한 기반으로 클라우드 수명 주기에 Microsoft Azure 보안 응답을 사용합니다. 단계는 다음 다이어그램에 나와 있습니다.

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> 자체 계획을 마련할 때는 NIST(National Institute of Standards and Technology) [컴퓨터 보안 인시던트 처리 가이드](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) 를 사용할 수 있습니다.
> 

다음 단계에서 보안 센터 경고를 사용할 수 있습니다.

* **감지**: 하나 이상의 리소스에서 의심스러운 작업을 식별합니다. 
* **평가**: 초기 평가를 수행하여 의심스러운 작업에 대한 자세한 정보를 가져옵니다.
* **진단**: 수정 단계를 사용하여 문제를 해결하는 기술 절차를 수행합니다.

각 보안 경고는 공격의 근원을 더 잘 이해하는 데 도움이 될 수 있는 정보를 제공하며 가능한 해결 방법을 제안합니다. 일부 경고에서는 Azure 내부의 타 정보원이나 다른 추가 정보에 대한 링크를 제공할 수 있습니다. 완화를 시작하려면 다시 추가 검색에 제공되는 정보를 사용하고 작업 영역에 저장되어 있는 보안 관련 데이터를 검색할 수도 있습니다.

다음 예제에서는 미심쩍은 RDP 활동이 발생하고 있음을 보여줍니다.

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

여기에서 보듯이 이 블레이드는 공격 발생 시간, 소스 호스트 이름, 대상 VM과 관련한 자세한 내용을 표시하며 권장 절차를 안내합니다. 일부 상황에서는 공격의 소스 정보가 비어 있을 수 있습니다. 이러한 동작 유형에 대한 자세한 내용은 [Azure Security Center 경고에 누락된 원본 정보](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) 를 참고하세요.

[사고 대응에 대해 Azure Security Center 및 Microsoft Operations Management Suite를 활용하는 방법](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) 비디오를 통해 각 단계에서 Security Center를 사용할 수 있는 방식을 이해하는 데 도움이 되는 몇 가지 데모를 확인할 수 있습니다.

> [!NOTE]
> 인시던트 대응 프로세스 중에 도움이 될 보안 센터 기능을 사용하는 방법에 대한 자세한 내용은 [인시던트 대응에 Azure Security Center 활용](security-center-incident-response.md) 을 참고하세요. 
> 
> 

## <a name="see-also"></a>참고 항목
이 문서에서는 보안 센터를 도입하도록 계획하는 방법을 살펴보았습니다. 보안 센터에 대한 자세한 내용은 다음을 참조하세요.

* [Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) — Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure Security Center를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) — 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure Security Center FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

