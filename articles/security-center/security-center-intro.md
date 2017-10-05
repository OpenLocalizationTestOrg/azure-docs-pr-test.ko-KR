---
title: "Azure Security Center 소개 | Microsoft Docs"
description: "Azure 보안 센터, 주요 기능 및 작동 방법에 대해 알아봅니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a>Azure 보안 센터 소개
Azure 보안 센터, 주요 기능 및 작동 방법에 대해 알아봅니다.

> [!NOTE]
> 2017년 6월 초를 시작으로 Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집 및 저장합니다. 자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요. 이 문서의 정보는 Microsoft Monitoring Agent로 전환된 후의 Security Center 기능을 나타냅니다.
>
>

## <a name="what-is-azure-security-center"></a>Azure 보안 센터란?
 보안 센터는 Azure 리소스의 보안에 대한 향상된 가시성과 제어권을 통해 위협을 예방하고 감지하며 위협에 대응하는 데 도움이 됩니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

## <a name="key-capabilities"></a>주요 기능
 보안 센터는 Azure에 기본 제공되는 사용하기 쉽고 효과적인 위협 예방, 감지 및 대응 기능을 제공합니다. 주요 기능:

| 단계 | 기능 |
| --- | --- |
| 예방 |Azure 리소스의 보안 상태 모니터링 |
| 예방 | 회사의 보안 요구 사항, 사용할 응용 프로그램 형식 및 데이터의 민감도에 따라 Azure 구독에 대한 정책 정의 |
| 예방 | 정책 기반 보안 권장 사항을 사용하여 서비스 소유자에게 필요한 제어를 구현하는 과정 안내 |
| 예방 | Microsoft 및 파트너의 보안 서비스 및 어플라이언스를 빠르게 배포 |
| 감지 |Azure 리소스, 네트워크 및 맬웨어 방지 프로그램과 방화벽 같은 파트너 솔루션에서 자동으로 보안 데이터 수집 및 분석 |
| 감지 | Microsoft 제품과 서비스, Microsoft DCU(Digital Crimes Unit), MSRC(Microsoft 보안 대응 센터) 및 외부 피드에서 글로벌 위협 인텔리전스 사용 |
| 감지 | 기계 학습 및 행동 분석을 비롯한 고급 분석 적용 |
| 대응 |우선 순위가 지정된 보안 문제/경고 제공 |
| 대응 | 공격 출처 및 영향을 받는 리소스에 대한 정보 제공 |
| 대응 | 현재 공격을 중지하고 미래 공격을 예방하는 데 도움이 되는 방법 제안 |

## <a name="introductory-walkthrough"></a>기능 소개 연습

> [!NOTE]
> 이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다. 이 문서는 단계별 가이드가 아닙니다.
>
>

 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)에서 보안 센터에 액세스합니다. [포털](https://portal.azure.com)에 로그인합니다. 주 포털 메뉴에서 **Security Center** 옵션으로 스크롤하거나 이전에 포털 대시보드에 고정한 **Security Center** 타일을 선택합니다.

![Azure 포털의 보안 타일][1]

보안 센터에서 보안 정책을 설정하고 보안 구성을 모니터링하며 보안 경고를 볼 수 있습니다.

### <a name="security-policies"></a>보안 정책
회사의 보안 요구 사항에 따라 Azure 구독에 대한 정책을 정의할 수 있습니다. 또한 사용하는 응용 프로그램의 형식 또는 각 구독에서 데이터의 민감도에 대해 정책을 조정할 수 있습니다. 예를 들어 개발 또는 테스트에 사용되는 리소스의 요구사항은 프로덕션 응용 프로그램에 사용되는 보안 요구 사항과 다릅니다. 마찬가지로 PII 같은 규제된 데이터를 가진 응용 프로그램에 대해서는 더 높은 수준의 보안이 필요할 수 있습니다.

> [!NOTE]
> 보안 정책을 수정하려면 보안 관리자이거나 구독의 소유자 또는 참가자여야 합니다. Security Center의 역할 및 허용된 작업에 대해 알아보려면 [Azure Security Center의 권한](security-center-permissions.md)을 참조하세요.
>
>

**Security Center** 블레이드에서 구독 및 리소스 그룹 목록에 대한 **정책** 타일을 선택합니다.   

![보안 센터 블레이드][2]

**보안 정책** 블레이드에서 정책 세부 정보를 볼 구독을 선택합니다.

**데이터 수집**은 보안 정책에 대한 데이터 수집을 사용합니다. 사용하도록 설정하면 다음 작업이 수행됩니다.

* 보안 모니터링 및 권장 사항을 위해 지원되는 가상 컴퓨터(VM)를 매일 검색합니다.
* 분석 및 위협 감지를 위해 보안 이벤트를 수집합니다.

> [!NOTE]
> 데이터 수집은 구독 수준에서 구성됩니다.
>
>

**방지 정책**을 선택하여 **방지 정책** 블레이드를 엽니다. **권장 사항 표시**를 사용하면 구독 내에서 리소스의 보안 요구를 기반으로 모니터링하려는 보안 컨트롤과 보려는 권장 지침을 선택할 수 있습니다.

### <a name="security-recommendations"></a>보안 권장 사항
 보안 센터는 Azure 리소스의 보안 상태를 분석하여 잠재적인 보안 취약성을 식별합니다. 권장 사항 목록은 필요한 컨트롤 구성 과정을 안내합니다. 예를 들면 다음과 같습니다.

* 맬웨어 방지 프로그램을 프로비전하여 악성 소프트웨어 식별 및 제거 지원
* 네트워크 보안 그룹 및 VM에 대한 트래픽 제어 규칙 구성
* 웹 응용 프로그램 방화벽을 프로비전하여 웹 응용 프로그램의 대상이 되는 공격에 대한 방어 지원
* 누락된 시스템 업데이트 배포
* 권장 기준과 일치하지 않는 OS 구성 해결

권장 사항 목록에 대한 **권장 사항** 타일을 클릭합니다. 각 권장 사항을 클릭하여 추가 정보를 보거나 문제를 해결하기 위한 조치를 취합니다.

![Azure 보안 센터의 보안 권장 사항][5]

### <a name="security-state-of-azure-resources"></a>Azure 리소스의 보안 상태
대시보드의 **방지**섹션은 환경의 전체 보안 상태를 VM, 웹 응용 프로그램 및 다른 리소스를 비롯한 리소스 형식별로 표시합니다.   

**방지**에서 리소스 형식을 선택하여 식별된 잠재적 보안 취약성 목록을 비롯한 자세한 정보를 봅니다. (아래 예제에서**계산**을 선택합니다.)

![리소스 상태 타일][6]

### <a name="security-alerts"></a>보안 경고
 보안 센터는 Azure 리소스, 네트워크 및 맬웨어 방지 프로그램과 방화벽 같은 파트너 솔루션에서 자동으로 로그 데이터를 수집, 분석 및 통합합니다. 위협이 감지되었을 때 보안 경고가 생성됩니다. 감지되는 사항의 예:

* 알려진 악성 IP 주소와 통신하는 손상된 VM
* Windows 오류 보고를 사용하여 감지된 고급 맬웨어 프로그램
* VM에 대한 무작위 공격
* 통합 맬웨어 방지 프로그램 및 방화벽에서의 보안 경고

**보안 경고** 타일을 클릭하면 우선 순위가 지정된 경고의 목록이 표시됩니다.

![보안 경고][7]

경고를 선택하면 공격 및 공격을 해결하는 방법 제안에 대한 더 자세한 정보가 표시됩니다.

![보안 경고 세부 정보][8]

### <a name="partner-solutions"></a>파트너 솔루션
**파트너 솔루션** 타일을 통해 Azure 구독과 통합된 파트너 솔루션의 보안 상태를 한 눈에 모니터링할 수 있습니다. 보안 센터에는 솔루션에서 가져온 경고가 표시됩니다.

**파트너 솔루션** 타일을 선택합니다. 블레이드가 열리고 연결된 모든 파트너 솔루션의 목록을 표시합니다.

![파트너 솔루션][9]

## <a name="get-started"></a>시작
보안 센터를 시작하려면 Microsoft Azure에 대한 구독이 필요합니다. 보안 센터는 Azure 구독을 사용하여 사용하도록 설정됩니다. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.

 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)에서 보안 센터에 액세스합니다. 자세한 내용은 [포털 설명서](https://azure.microsoft.com/documentation/services/azure-portal/)를 참조하세요.

[Azure 보안 센터 시작](security-center-get-started.md)은 보안 센터의 보안 모니터링 및 정책 관리 구성 요소를 빠르게 안내합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 보안 센터, 주요 기능 및 시작하는 방법을 소개하였습니다. 자세한 내용은 다음 리소스를 참조하세요.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.
* [Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) — 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.
- [Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
