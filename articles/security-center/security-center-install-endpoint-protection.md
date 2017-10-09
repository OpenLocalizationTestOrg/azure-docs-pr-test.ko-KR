---
title: "Azure 보안 센터에서 Endpoint Protection aaaInstall | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 설치 끝점 보호 * *입니다."
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
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Azure 보안 센터에서 Endpoint Protection 설치
Azure Security Center에서는 Endpoint Protection이 아직 사용하도록 설정되지 않은 경우 Azure VM(가상 컴퓨터)에 Endpoint Protection을 설치할 것을 권장합니다. 이 권장 tooWindows Vm만 적용 됩니다.

> [!NOTE]
> 이 배포 예에서는 Microsoft 맬웨어 방지 프로그램을 사용합니다. Security Center와 통합된 파트너 목록은 [Azure Security Center에서 파트너 통합](security-center-partner-integration.md#partners-that-integrate-with-security-center)을 참조하세요.  
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  이 문서는 단계별 가이드가 아닙니다.
>
>

1. Hello에 **권장 사항을** 블레이드를 **Endpoint Protection 설치**합니다.
   ![Endpoint Protection 설치 선택][1]
2. hello **Endpoint Protection 설치** 블레이드 열리고 끝점 보호 없이 Vm의 목록을 표시 합니다. Hello 목록 hello에 tooinstall 끝점 보호 사용을 선택 하 고를 클릭 하는 Vm 중에서 선택 **Vm에 설치**합니다.
   ![Vm tooinstall Endpoint Protection을 선택 합니다.][2]
3. hello **Endpoint Protection 선택** 블레이드에서 열립니다 tooallow 있습니다 tooselect hello 끝점 보호 솔루션 toouse 원하는 합니다. 이 예제에서는 **Microsoft 맬웨어 방지 프로그램**을 선택합니다.
   ![Endpoint Protection 선택][3]
4. Hello 끝점 보호 솔루션에 대 한 추가 정보가 표시 됩니다. **만들기**를 선택합니다.
   ![맬웨어 방지 솔루션 만들기][4]
5. Hello에서 필요한 hello 구성 설정을 입력 **확장 추가** 블레이드에서 다음을 선택 하 고 **확인**합니다. hello 구성 설정에 대해 자세히 toolearn 참조 [기본 및 사용자 지정 맬웨어 방지 구성](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)합니다.

[Microsoft 맬웨어 방지](../security/azure-security-antimalware.md) 이제 hello 사용 중인 Vm을 선택 합니다.

## <a name="see-also"></a>참고 항목
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "Endpoint Protection." Microsoft Azure에서 맬웨어 방지 프로그램 사용에 대 한 더 toolearn hello 다음 문서 참조:

* [클라우드 서비스 및 가상 컴퓨터에 대 한 Microsoft 맬웨어 방지](../security/azure-security-antimalware.md) -자세한 방법을 toodeploy Microsoft 맬웨어 방지 합니다.

보안 센터에 대해 자세히 toolearn hello 다음 문서를 참조 하십시오.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
