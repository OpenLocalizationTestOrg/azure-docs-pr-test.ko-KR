---
title: "Azure 보안 센터에서 웹 응용 프로그램 방화벽 aaaAdd | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 추가 웹 응용 프로그램 방화벽 * * 및 * * 응용 프로그램 보호 * * 마무리 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Azure 보안 센터에서 웹 응용 프로그램 방화벽 추가
Azure 보안 센터를 추가 하는 웹 응용 프로그램 방화벽 (WAF)는 Microsoft 파트너 toosecure에서 웹 응용 프로그램을 권장할 수 있습니다. 이 문서 과정을 안내 하는 방법의 예 tooapply이이 권장 합니다.

공개 인바운드 웹 포트(80,443)으로 연결된 네트워크 보안 그룹에 있는 모든 공용 연결 IP(인스턴스 수준 IP 또는 부하 분산된 IP)에 대해 WAF 권장 사항이 표시됩니다.

보안 센터 앱 서비스 환경 및 가상 컴퓨터에서 웹 응용 프로그램을 대상으로 하는 공격 방어 WAF toohelp 구축 하는 것이 좋습니다. ASE(App Service 환경)는 Azure App Service의 [프리미엄](https://azure.microsoft.com/pricing/details/app-service/) 서비스 계획 옵션으로, Azure App Service 앱의 안전한 실행을 위해 완전히 격리된 전용 환경을 제공합니다. toolearn ASE에 대 한 자세한 참조 hello [앱 서비스 환경 설명서](../app-service/app-service-app-service-environments-readme.md)합니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  이 문서는 단계별 가이드가 아닙니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **웹 응용 프로그램 방화벽을 사용 하 여 웹 응용 프로그램을 보안**합니다.
   ![웹 응용 프로그램 보안][1]
2. Hello에 **웹 응용 프로그램 방화벽을 사용 하 여 웹 응용 프로그램을 보호** 블레이드를 웹 응용 프로그램을 선택 합니다. hello **추가 웹 응용 프로그램 방화벽** 블레이드를 엽니다.
   ![웹 응용 프로그램 방화벽 추가][2]
3. 선택할 수 있습니다 toouse 기존 웹 응용 프로그램 방화벽 사용 가능한 경우 또는 새를 만들 수 있습니다. 이 예제에서는 기존 WAF가 없으므로 WAF를 만들어 보겠습니다.
4. WAF toocreate hello 통합된 파트너 목록에서 솔루션을 선택 합니다. 이 예제에서는 **Barracuda Web Application Firewall**을 선택합니다.
5. hello **Barracuda 웹 응용 프로그램 방화벽** 블레이드에서 열립니다 hello 업체 솔루션에 대 한 정보를 제공 합니다. 선택 **만들기** hello 정보 블레이드에서 합니다.

   ![방화벽 정보 블레이드][3]

6. hello **새 웹 응용 프로그램 방화벽** 수행할 수 있는 블레이드 열리고 **VM 구성** 제공 하 여 단계 **WAF 정보**합니다. **VM 구성**을 선택합니다.
7. Hello에 **VM 구성** 정보를 실행 하는 hello 가상 컴퓨터를 필요한 toospin hello WAF 입력 블레이드를 만듭니다.
   ![VM configuration][4]
8. Toohello 반환 **새 웹 응용 프로그램 방화벽** 블레이드에 대 한 선택 **WAF 정보**합니다. Hello에 **WAF 정보** 블레이드에서 hello WAF 자체를 구성 합니다. 7 단계는 hello WAF에서 실행 되 고 8 단계 사용 하면 자체 WAF tooprovision hello tooconfigure hello 가상 컴퓨터가 있습니다.

## <a name="finalize-application-protection"></a>응용 프로그램 보호 완료
1. Toohello 반환 **권장 사항을** 블레이드입니다. 새 항목을 호출 하는 hello WAF를 만든 후 생성 된 **응용 프로그램 보호 완료**합니다. 이 항목에는 toocomplete hello 과정 실제로 hello 응용 프로그램을 보호할 수 있도록 hello Azure 가상 네트워크 내에서 WAF hello를 연결 해야 하는 알 수 있습니다.

   ![응용 프로그램 보호 완료][5]

2. **응용 프로그램 보호 완료**를 선택합니다. 새 블레이드가 열립니다. Toohave 해 해당 트래픽을 하는 웹 응용 프로그램 있다는 것을 볼 수 있습니다.
3. Hello 웹 응용 프로그램을 선택 합니다. 블레이드는 hello 웹 응용 프로그램 방화벽 설치를 완료 하는 중에 단계 수 있게 해 주는 열립니다. Hello 단계를 완료 한 다음 선택 **트래픽을 제한**합니다. 다음 보안 센터 배선 접속 드립니다 hello지 않습니다.

   ![트래픽 제한][6]

> [!NOTE]
> 이러한 응용 프로그램 tooyour 기존 WAF 배포를 추가 하 여 보안 센터에서 여러 웹 응용 프로그램을 보호할 수 있습니다.
>
>

이제 해당 WAF에서 hello 로그 완전히 통합 됩니다. 보안 센터 자동으로 수집 하 고 중요 한 보안 경고 tooyou를 표면 수 있도록 hello 로그 분석을 시작할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "웹 응용 프로그램을 추가 합니다." 웹 응용 프로그램 방화벽 구성에 대 한 더 toolearn hello 다음을 참조 합니다.

* [앱 서비스 환경에 대한 웹 응용 프로그램 방화벽(WAF) 구성](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
