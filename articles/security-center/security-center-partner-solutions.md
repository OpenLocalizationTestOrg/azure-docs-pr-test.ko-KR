---
title: "Azure 보안 센터에서 aaaManaging 파트너 솔루션 | Microsoft Docs"
description: "이 문서 Azure 보안 센터에서 Azure 구독과 통합 하 여 파트너 솔루션의 한 눈에 보기 hello 상태는 모니터를 통해 하는 방법 안내 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Azure 보안 센터를 사용하여 파트너 솔루션 모니터링
이 문서 toomonitor Azure 보안 센터에서 파트너 솔루션의 상태를 hello 하는 방법을 안내 합니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다. 이 문서는 단계별 가이드가 아닙니다.
>
>

## <a name="monitoring-partner-solutions"></a>파트너 솔루션 모니터링
hello **파트너 솔루션** hello 타일 **보안 센터** 블레이드 통해 통합 Azure 구독 된 파트너 솔루션의 한 눈에 보기 hello 상태 상태를 모니터링 합니다.

![파트너 솔루션 타일][1]

hello **파트너 솔루션** 타일 통합 구독 된 파트너 솔루션의 hello 수를 표시 합니다. 통합 된 솔루션이 없는 경우 hello 숫자를 0 hello 타일에 표시 됩니다.

파트너 솔루션의 tooview hello 상태:

1. 선택 hello **파트너 솔루션** 바둑판식으로 배열입니다. hello **파트너 솔루션** 파트너 솔루션의 목록을 표시 하는 블레이드에서 열립니다 tooSecurity 센터를 연결 합니다.

   ![파트너 솔루션][3]

   파트너 솔루션의 hello 상태 될 수 있습니다.

   * 보호됨(녹색) - 상태 문제가 없습니다.
   * 비정상(빨강) - 즉각적인 주의가 필요한 상태 문제가 있습니다.
   * 중지 된 보고 (주황색)-hello 솔루션의 상태를 보고 중지 되었습니다.
   * 알 수 없는 보호 상태 (주황색)-hello 솔루션의 hello 상태 알려져 있지 않은 새 리소스 toohello 기존 솔루션 추가 하지 못했습니다 tooa 과정 있으므로이 시간입니다.
   * 보고 되지 않습니다 (회색)-hello 솔루션 아무 것도 보고 하지 않았음을 아직 최근에 연결 여전히 배포 하는 경우 솔루션의 상태 보고 될 수 있습니다.

2. 파트너 솔루션을 선택합니다. 이 예제에서는 select hello를 통해 **Qualys** 솔루션입니다.  Hello 업체 솔루션 및 hello 솔루션의 hello 상태 관련 리소스를 보여 주는 블레이드를 엽니다. 선택 **솔루션 콘솔** 이 솔루션에 tooopen hello 파트너 관리 환경을 제공 합니다.

   ![파트너 솔루션 세부 정보][4]
3. Toohello 돌아가서 **Qualys** 블레이드에 대 한 선택 **링크 VM**합니다. hello **링크 응용 프로그램** 블레이드를 엽니다. 여기서 리소스 toohello 업체 솔루션을 연결할 수 있습니다.

   ![링크 리소스 toopartner 솔루션][5]

## <a name="next-steps"></a>다음 단계
이 문서에 도입 된 toohello 던 **파트너 솔루션** 보안 센터에 바둑판식으로 배열입니다. 보안 센터에 대해 자세히 toolearn hello 다음 문서 참조:

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
