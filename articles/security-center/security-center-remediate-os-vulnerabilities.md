---
title: "Azure 보안 센터에서 운영 체제 aaaRemediate 취약성 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 수정 OS 취약점 * *입니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Azure 보안 센터에서 OS 취약성 해결
Azure 보안 센터를 분석 하 여 매일 가상 컴퓨터 (VM) 운영 체제 (OS) 만들 수 있는 구성이 hello VM에 대 한 으로부터 더 취약 tooattack 하 고 권장 구성이 tooaddress 이러한 취약점을 변경 합니다. 보안 센터는 VM의 OS 구성 권장 구성 규칙 hello 일치 하지 않는 경우 보안 문제를 해결 하는 것이 좋습니다.

> [!NOTE]
> 모니터링 되 고 hello 특정 구성에 대 한 자세한 내용은 참조 hello [권장 되는 구성 규칙 목록이](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)합니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  이 문서는 단계별 가이드가 아닙니다.
>
>

1. Hello에 **권장 사항을** 블레이드를 **재구성 OS 취약점**합니다.
   ![OS 취약성 해결][1]

    hello **재구성 OS 취약점** 블레이드 열리고 권장 구성 규칙 hello와 일치 하지 않는 운영 체제 구성으로 Vm을 나열 합니다.  각 VM에 대 한 hello 블레이드를 식별합니다.

   * **못했습니다 규칙** -실패 한 hello 수 hello VM의 OS 구성 하는 규칙입니다.
   * **마지막 검사 시간** --hello 날짜 및 시간을 보안 센터 마지막으로 검색 한 hello VM의 OS 구성 합니다.
   * **상태** -hello hello 취약점의 현재 상태:

     * 열기: hello 취약점에 처리 되지 아직
     * 진행: hello 취약점은 현재 적용 되 고, 사용자가 아무 작업도 필요
     * 확인할: hello 취약점이 이미 해결 (hello 문제가 해결 되 면 hello 항목은 회색으로 표시)
   * **심각도** -모든 취약성이 설정 low tooa 심각도 즉 취약점을 해결 해야 하지만 즉각적인 주의가 필요 하지 않습니다.

2. VM을 선택합니다. 해당 블레이드 VM 열리고 실패 한 hello 규칙이 표시 됩니다.
   ![실패한 구성 규칙][2]

3. 규칙을 선택합니다. 이 예제에서는 **암호는 복잡성 조건을 만족해야 함**을 선택합니다. 블레이드 설명 하는 hello 실패 규칙 및 hello에 미치는 영향을 엽니다. Hello 세부 정보를 검토 하 고 운영 체제 구성이 적용 되는 방법을 고려 합니다.
  ![Hello에 대 한 실패 규칙][3]

  보안 센터 구성 규칙에 대 한 일반적인 구성 열거형 CCE () tooassign 고유 식별자를 사용합니다. 다음 정보는 hello이이 블레이드에 제공 됩니다.

  - 이름 -- 규칙의 이름
  - 심각도 -- CCE 심각도 값, 즉 요주의, 중요 또는 경고
  - CCE CCIED-hello 규칙에 대 한 고유 식별자
  - 설명 -- 규칙에 대한 설명
  - 취약성 -- 규칙이 적용되지 않은 경우 취약성 또는 위험에 대한 설명
  - 영향 -- 규칙이 적용될 때 비즈니스 영향
  - 예상 값-값이 보안 센터 hello 규칙에 대해 VM OS 구성을 분석할 때 필요 합니다.
  - Hello 규칙에 대해 VM OS 구성의 분석 하는 동안 보안 센터에서 사용 되는 규칙 작업-규칙 작업
  - Hello 규칙에 대해 VM OS 구성의 분석 한 후 반환 된 값을 실제 값-
  - 평가 결과 –- 분석 결과: 통과, 실패

## <a name="see-also"></a>참고 항목
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "재구성 OS 취약점입니다." Hello 규칙 집합을 구성을 검토할 수 있습니다 [여기](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)합니다. 보안 센터 CCE (Common Configuration Enumeration) tooassign 고유 식별자를 사용 하 여 구성 규칙에 대 한 합니다. Hello 방문 [CCE](https://nvd.nist.gov/cce/index.cfm) 자세한 정보에 대 한 사이트입니다.

보안 센터에 대해 자세히 toolearn hello 다음 리소스를 참조 하십시오.

* [Azure Security Center에서 지원되는 플랫폼](security-center-os-coverage.md) - 지원되는 Windows 및 Linux VM의 목록을 제공합니다.
* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure Security Center에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
