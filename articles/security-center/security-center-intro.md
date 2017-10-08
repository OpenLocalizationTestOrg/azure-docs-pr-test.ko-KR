---
title: "aaaIntroduction tooAzure 보안 센터 | Microsoft Docs"
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
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>소개 tooAzure 보안 센터
Azure 보안 센터, 주요 기능 및 작동 방법에 대해 알아봅니다.

> [!NOTE]
> 보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다. 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>
>

## <a name="what-is-azure-security-center"></a>Azure 보안 센터란?
 보안 센터를 사용 하면 방지 하 고 검색에 대 한 향상 된 가시성 및 Azure 리소스의 보안을 hello에 대 한 제어를 사용 하 여 toothreats 응답할 수 있습니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

## <a name="key-capabilities"></a>주요 기능
 보안 센터 사용 하기 쉬운이 고 효과적인 위협 tooAzure 제공 된 예방, 감지, 및 대처 기능을 제공 합니다. 주요 기능:

| 단계 | 기능 |
| --- | --- |
| 예방 |모니터 hello Azure 리소스의 보안 상태 |
| 예방 | Hello 유형의 응용 프로그램을 사용 하 고 데이터의 민감도 hello 회사의 보안 요구 사항에 기반 하 여 Azure 구독에 대 한 정책을 정의 합니다. |
| 예방 | 사용 하 여 정책 기반 보안 권장 사항 tooguide 서비스 소유자 구현의 hello 프로세스를 통해 필요한 컨트롤 |
| 예방 | Microsoft 및 파트너의 보안 서비스 및 어플라이언스를 빠르게 배포 |
| 감지 |자동으로 수집 하 여 Azure 리소스, hello 네트워크 및 맬웨어 방지 프로그램 및 방화벽와 같은 파트너 솔루션에서 보안 데이터를 분석 하 고 |
| 감지 | 전역 사용 하 여 위협 인텔리전스에서 Microsoft 제품 및 서비스를 Microsoft Digital Crimes 단위 (DCU), hello hello Microsoft 보안 대응 센터 (MSRC), 및 외부 피드 |
| 감지 | 기계 학습 및 행동 분석을 비롯한 고급 분석 적용 |
| 대응 |우선 순위가 지정된 보안 문제/경고 제공 |
| 대응 | Hello 소스 hello 공격 및 영향을 받는 리소스에 대 한 정보를 제공합니다. |
| 대응 | Toostop 현재 공격 hello 및 향후 공격을 방지 하는 방법을 제안합니다 |

## <a name="introductory-walkthrough"></a>기능 소개 연습

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다. 이 문서는 단계별 가이드가 아닙니다.
>
>

 보안 센터 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다. [Toohello 포털에 로그인](https://portal.azure.com)합니다. Hello 주 포털 메뉴에서 toohello 스크롤합니다 **보안 센터** 옵션 또는 선택 hello **보안 센터** toohello 포털 대시보드에서 고정 했던 바둑판식으로 배열 합니다.

![Azure 포털의 보안 타일][1]

보안 센터에서 보안 정책을 설정하고 보안 구성을 모니터링하며 보안 경고를 볼 수 있습니다.

### <a name="security-policies"></a>보안 정책
Tooyour 회사의 보안 요구 사항에 따라 Azure 구독에 대 한 정책을 정의할 수 있습니다. 조정할 수 있습니다 이러한 toohello 유형의 사용 하는 응용 프로그램 또는 toohello 민감도 hello 데이터의 각 구독에 있습니다. 예를 들어 개발 또는 테스트에 사용되는 리소스의 요구사항은 프로덕션 응용 프로그램에 사용되는 보안 요구 사항과 다릅니다. 마찬가지로 PII 같은 규제된 데이터를 가진 응용 프로그램에 대해서는 더 높은 수준의 보안이 필요할 수 있습니다.

> [!NOTE]
> 보안 정책 toomodify hello 또는 보안 관리자가 구독 소유자 또는 참가자 여야 합니다. 역할 및 보안 센터에서 허용 되는 작업에 대해 자세히 toolearn 참조 [Azure 보안 센터에서 사용 권한을](security-center-permissions.md)합니다.
>
>

Hello에 **보안 센터** 블레이드, 선택 hello **정책** 구독 / 리소스 그룹의 목록에 대 한 바둑판식으로 배열입니다.   

![보안 센터 블레이드][2]

Hello에 **보안 정책** 블레이드에서 구독 tooview hello 정책 세부 정보를 선택 합니다.

**데이터 수집**은 보안 정책에 대한 데이터 수집을 사용합니다. 사용하도록 설정하면 다음 작업이 수행됩니다.

* 보안 모니터링 및 권장 사항을 위해 지원되는 가상 컴퓨터(VM)를 매일 검색합니다.
* 분석 및 위협 감지를 위해 보안 이벤트를 수집합니다.

> [!NOTE]
> 데이터 수집 hello 구독 수준에서 구성 됩니다.
>
>

선택 **방지 정책** tooopen hello **방지 정책** 블레이드입니다. **에 대 한 권장 사항 표시** toosee hello 구독 내 hello 리소스의 hello 보안 요구 사항에 따라 원하는 toomonitor 및 hello 권장 사항을 원하는 hello 보안 컨트롤을 선택할 수 있습니다.

### <a name="security-recommendations"></a>보안 권장 사항
 보안 센터에 Azure 리소스 tooidentify 잠재적인 보안 취약점의 hello 보안 상태를 분석합니다. 권장 사항 목록 hello 필요한 컨트롤을 구성 과정을 안내 합니다. 예를 들면 다음과 같습니다.

* 맬웨어 방지 프로 비전 toohelp 식별 하 고 악성 소프트웨어를 제거 합니다.
* 네트워크 보안 그룹 및 규칙 toocontrol 트래픽 tooVMs 구성
* 웹 응용 프로그램 방화벽 toohelp 웹 응용 프로그램을 대상으로 하는 공격을 방어할의 프로 비전
* 누락된 시스템 업데이트 배포
* 초기 권장 hello와 일치 하지 않는 운영 체제 구성을 주소 지정

Hello 클릭 **권장 사항을** 권장 사항 목록에 대 한 바둑판식으로 배열입니다. 각 권장 사항 tooview 추가 정보 또는 tootake 작업 tooresolve hello 문제를 클릭 합니다.

![Azure 보안 센터의 보안 권장 사항][5]

### <a name="security-state-of-azure-resources"></a>Azure 리소스의 보안 상태
hello **방지** hello 대시보드의 리소스 종류, Vm, 웹 응용 프로그램 및 기타 리소스를 포함 하 여 hello 환경의 전반적인 보안 상태를 hello 보여 줍니다.   

리소스 종류 선택 **방지** tooview 목록이 표시 되는 모든 잠재적인 보안 취약점을 비롯 한 자세한 내용은 합니다. (**계산** hello 예제 아래에서 선택 합니다.)

![리소스 상태 타일][6]

### <a name="security-alerts"></a>보안 경고
 보안 센터 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 맬웨어 방지 프로그램 및 방화벽와 같은 파트너 솔루션에서 로그 데이터를 통합 합니다. 위협이 감지되었을 때 보안 경고가 생성됩니다. 감지되는 사항의 예:

* 알려진 악성 IP 주소와 통신하는 손상된 VM
* Windows 오류 보고를 사용하여 감지된 고급 맬웨어 프로그램
* VM에 대한 무작위 공격
* 통합 맬웨어 방지 프로그램 및 방화벽에서의 보안 경고

클릭 하 여 hello **보안 경고** 타일에는 우선 순위가 지정 된 경고 목록이 표시 됩니다.

![보안 경고][7]

경고를 선택 하면 hello 공격 및 방법에 대 한 제안 사항에 대 한 자세한 정보 표시 tooremediate 것입니다.

![보안 경고 세부 정보][8]

### <a name="partner-solutions"></a>파트너 솔루션
hello **파트너 솔루션** 파트너 솔루션의 한 눈에 보기 hello 보안 상태에 모니터링 하는 타일 사용 하면 Azure 구독와 통합 합니다. 보안 센터 들어오는 hello 솔루션에서 경고를 표시 합니다.

선택 hello **파트너 솔루션** 바둑판식으로 배열입니다. 블레이드가 열리고 연결된 모든 파트너 솔루션의 목록을 표시합니다.

![파트너 솔루션][9]

## <a name="get-started"></a>시작
보안 센터와 시작 tooget, 구독 tooMicrosoft Azure 필요 합니다. 보안 센터는 Azure 구독을 사용하여 사용하도록 설정됩니다. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.

 보안 센터 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다. Hello 참조 [포털 설명서](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn 더 합니다.

[Azure 보안 센터를 시작 하기](security-center-get-started.md) 보안 센터의 hello 보안 모니터링 및 정책 관리 구성 요소를 통해 신속 하 게 안내 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에 도입 된 tooSecurity 센터의 주요 기능 및 tooget 시작 하는 방법이 있었습니다. toolearn hello 다음 리소스를 더, 참조:

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
- [Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

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
