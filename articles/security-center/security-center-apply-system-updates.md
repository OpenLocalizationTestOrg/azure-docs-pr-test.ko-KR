---
title: "Azure 보안 센터의 시스템 업데이트 aaaApply | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 적용 시스템 업데이트 * * 및 * * 후 시스템 업데이트 * *를 다시 부팅 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Azure 보안 센터의 시스템 업데이트 적용
Azure Security Center는 누락된 운영 체제 업데이트에 대해 매일 Windows 및 Linux 가상 컴퓨터(VM)를 모니터링합니다. 보안 센터는 Windows VM에서 구성된 서비스에 따라 Windows 업데이트 또는 WSUS(Windows Server Update Services)에서 사용 가능한 보안 및 중요 업데이트의 목록을 검색합니다.  또한 보안 센터 Linux 시스템에서 hello 최신 업데이트를 확인합니다. VM이 시스템 업데이트를 누락하는 경우 보안 센터는 시스템 업데이트 적용을 권장합니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  단계별 가이드는 아닙니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **시스템 업데이트를 적용**합니다.

   ![시스템 업데이트 적용][1]
2. hello **시스템 업데이트를 적용** 블레이드 열리고 Vm 누락 된 시스템 업데이트의 목록을 표시 합니다. VM을 선택합니다.

   ![VM 선택][2]
3. 해당 VM에 대한 누락된 업데이트의 목록을 표시하는 블레이드가 열립니다. 시스템 업데이트를 선택합니다. 이 예제에서는 KB3156016을 선택해 보겠습니다.

   ![누락된 보안 업데이트][3]

4. Hello에 hello 단계를 따라 **보안 업데이트** 블레이드 tooapply hello 누락 업데이트 합니다.

   ![보안 업데이트][4]

## <a name="reboot-after-system-updates"></a>시스템 업데이트 후 다시 부팅
1. Toohello 반환 **권장 사항을** 블레이드입니다. 시스템 업데이트를 적용한 후 **시스템 업데이트 후 다시 부팅**이라는 새 항목이 생성되었습니다. 이 항목에는 tooreboot hello VM toocomplete hello 프로세스의 시스템 업데이트를 적용 해야 하는 알 수 있습니다.

   ![시스템 업데이트 후 다시 부팅][5]
2. **시스템 업데이트 후 다시 부팅**을 선택합니다. 이렇게 하면 열립니다 **다시 시작이 보류 중인 toocomplete 시스템 업데이트** toorestart toocomplete hello 해야 하는 Vm의 목록 표시 블레이드 시스템 업데이트 프로세스를 적용 합니다.

   ![다시 시작 보류 중][6]

Azure toocomplete hello 프로세스에서 VM hello를 다시 시작 합니다.

## <a name="see-also"></a>참고 항목
보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
