---
title: "Azure Security Center에서 Endpoint Protection 설치 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **Endpoint Protection 설치**를 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Azure 보안 센터에서 Endpoint Protection 설치
Azure Security Center에서는 Endpoint Protection이 아직 사용하도록 설정되지 않은 경우 Azure VM(가상 컴퓨터)에 Endpoint Protection을 설치할 것을 권장합니다. 이 권장 사항은 Windows VM에만 적용됩니다.

> [!NOTE]
> 이 배포 예에서는 Microsoft 맬웨어 방지 프로그램을 사용합니다. Security Center와 통합된 파트너 목록은 [Azure Security Center에서 파트너 통합](security-center-partner-integration.md#partners-that-integrate-with-security-center)을 참조하세요.  
>
>

## <a name="implement-the-recommendation"></a>권장 사항 구현

> [!NOTE]
> 이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.  이 문서는 단계별 가이드가 아닙니다.
>
>

1. **권장 사항** 블레이드에서 **Endpoint Protection 설치**를 선택합니다.
   ![Endpoint Protection 설치 선택][1]
2. Endpoint Protection이 없는 VM의 목록을 표시하는 **Endpoint Protection 설치** 블레이드가 열립니다. 목록에서 Endpoint Protection 프로그램을 설치하려는 VM을 선택하고 **VM에 설치**를 클릭합니다.
   ![Endpoint Protection을 설치할 VM 선택][2]
3. 사용할 Endpoint Protection 솔루션을 선택할 수 있는 **Endpoint Protection 선택** 블레이드가 열립니다. 이 예제에서는 **Microsoft 맬웨어 방지 프로그램**을 선택합니다.
   ![Endpoint Protection 선택][3]
4. Endpoint Protection 솔루션에 대한 추가 정보가 표시됩니다. **만들기**를 선택합니다.
   ![맬웨어 방지 솔루션 만들기][4]
5. **확장 추가** 블레이드에서 필요한 구성 설정을 입력하고 **확인**을 선택합니다. 구성 설정에 대한 자세한 내용은 [기본 및 사용자 지정 맬웨어 방지 구성](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)을 참조하세요.

선택한 VM에서 [Microsoft 맬웨어 방지 프로그램](../security/azure-security-antimalware.md)이 활성화됩니다.

## <a name="see-also"></a>참고 항목
이 문서에서는 보안 센터 권장 사항 "Endpoint Protection 설치"를 구현하는 방법을 보여 주었습니다. Azure에서 Microsoft 맬웨어 방지 프로그램을 사용하도록 설정하는 방법에 대해 알아보려면 다음 문서를 참조하세요.

* [Cloud Services 및 Virtual Machines용 Microsoft 맬웨어 방지 프로그램](../security/azure-security-antimalware.md) -- Microsoft 맬웨어 방지 프로그램을 배포하는 방법을 알아봅니다.

Security Center에 대해 알아보려면 다음을 참조하세요.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- 보안 정책을 구성하는 방법을 알아봅니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.
* [Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
