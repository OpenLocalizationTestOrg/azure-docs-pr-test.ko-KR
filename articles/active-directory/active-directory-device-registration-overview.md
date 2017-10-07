---
title: "aaaAzure Active Directory 장치 등록 개요 | Microsoft Docs"
description: "Azure Active Directory device registration은 장치 기반 조건부 액세스 시나리오에 대 한 hello foundation 합니다. 장치를 등록할 때 Azure Active Directory 장치 등록 규정 hello hello 사용자가 로그인 할 때 사용 되는 tooauthenticate hello를 장치가 되는 id 사용 하 여 장치입니다."
services: active-directory
keywords: "장치 등록, 장치 등록 사용, 장치 등록 및 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록 시작
Azure Active Directory device registration은 장치 기반 조건부 액세스 시나리오에 대 한 hello foundation 합니다. 장치가 등록 되 면 Azure Active Directory 장치 등록 hello 사용자가 로그인 할 때 사용 되는 tooauthenticate hello를 장치가 되는 id 사용 하 여 hello 장치를 제공 합니다. 인증 된 hello 장치와 hello 장치의 hello 특성 수 hello 클라우드 및 온-프레미스에서 호스트 되는 응용 프로그램에 대 한 조건부 액세스 정책을 사용 하는 tooenforce 합니다.

Microsoft Intune 같은 모바일 장치 management(MDM) 솔루션을 함께 사용 하면 Azure Active Directory의 장치 특성이 hello hello 장치에 대 한 추가 정보로 업데이트 됩니다. 이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다. Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 [Intune에서 관리에 대해 장치 등록](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)을 참조하세요.

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록으로 사용할 수 있는 시나리오
Azure Active Directory 장치 등록에서는 iOS, Android 및 Windows 장치를 지원합니다. Azure AD device registration을 활용 하는 hello 개별 시나리오는 보다 구체적인 요구 사항 및 플랫폼 지원이 있을 수 있습니다. 이러한 시나리오는 다음과 같습니다.

* **조건부 액세스 tooapplications 온-프레미스 호스팅**: 응용 프로그램을 Windows Server 2012 r 2를 사용 하 여 toouse AD FS 구성에 대 한 액세스 정책을 사용 하 여 등록 된 장치를 사용할 수 있습니다. 온-프레미스에 대해 조건부 액세스를 설정하는 방법에 대한 자세한 내용은 [Azure Active Directory 장치 등록을 사용하여 온-프레미스 조건부 액세스 설정](active-directory-device-registration-on-premises-setup.md)을 참조하세요.
* **Microsoft Intune을 사용한 Office 365 응용 프로그램에 대 한 조건부 액세스** : hello에서 동일한 시간 규격 장치에서 정보 근로자를 허용 하는 동안 IT 관리자는 다음 조건부 액세스 장치 정책을 toosecure 회사 리소스를 프로 비전 할 수 tooaccess hello 서비스입니다. 자세한 내용은 [Office 365 서비스에 대한 조건부 액세스 장치 정책](active-directory-conditional-access-device-policies.md)을 참조하세요.

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록 설정
모바일 장치는 알려진 DNS 레코드를 검색 하 여 hello service를 검색할 수 있도록 hello Azure 포털에서에서 tooenable Azure AD 장치 등록을 해야 합니다. Windows 10, Windows 8.1, Windows 7, Android 및 iOS 장치를 검색 하 고 hello 서비스를 사용할 수 있도록 회사 DNS를 구성 해야 합니다.
볼 있고 hello 관리자 포털을 사용 하 여 Azure Active Directory에 등록 된 장치를 설정/해제 합니다.

> [!NOTE]
> 자동 장치 등록을 tooset 참조 하는 방법에 대 한 최신 지침에 대 한 [toosetup 자동 등록 Windows 도메인의 Azure Active Directory를 사용 하 여 장치를 조인 하는 방법을](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Azure Active Directory 장치 등록 서비스 사용
1. 관리자 권한으로 Microsoft Azure 포털 toohello에 로그인 합니다.
2. Hello 왼쪽된 창에서 선택 **Active Directory**합니다.
3. Hello에 **디렉터리** 탭에서 디렉터리를 선택 합니다.
4. 선택 hello **구성** 탭 합니다.
5. 이라는 toohello 섹션 스크롤하여 **장치**합니다.
6. **사용자가 장치에 작업 공간을 연결할 수 있습니다.**에 대해 **모두**를 선택합니다.
7. Hello 최대 수를 선택 하려는 tooauthorize 사용자 당 장치의 합니다.

> [!NOTE]
> Office 365에 대한 모바일 장치 관리 및 Microsoft Intune에 등록하려면 작업 공간 연결이 필요합니다. 이러한 서비스 중 하나를 구성 했으면 모두 선택 되 고 hello NONE 버튼을 사용할 수 없습니다.
> 
> 

기본적으로 hello 서비스에 대 한 2 단계 인증이 사용 되지 않습니다. 그러나 장치를 등록하는 경우 2단계 인증을 사용하는 것이 좋습니다.

* 이 서비스에 대 한 2 단계 인증을 요구 하기 전에 해야 합니다 Azure Active Directory에서 다단계 인증 공급자를 구성 하 고 Multi-factor Authentication에 대 한 사용자 계정을 구성 하십시오 참조 [Multi-factor 추가 Active Directory 인증 tooAzure](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Windows Server 2012 R2에서 AD FS를 사용하는 경우 AD FS에서 2단계 인증 모듈을 구성해야 합니다. [Active Directory Federation Services로 Multi-Factor Authentication 사용](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)을 참조하세요.

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Azure Active Directory 장치 등록 검색 구성
Windows 7 및 Windows 8.1 장치는 잘 알려진 장치 등록 서버 이름으로 hello 사용자 계정 이름을 결합 하 여 hello 장치 등록 서비스를 검색 합니다.

Azure Active Directory device registration service와 연결 된 toohello A 레코드를 가리키는 DNS CNAME 레코드를 만들어야 합니다. hello CNAME 레코드는 hello 알려진 접두사인 enterpriseregistration 뒤에 사용자의 조직에서 hello 사용자 계정에서 사용 하는 hello UPN 접미사를 사용 해야 합니다. 조직에서 여러 UPN 접미사를 사용하는 경우 DNS에 여러 CNAME 레코드를 만들어야 합니다.

예를 들어, 두 UPN 접미사를 사용 하 여 조직에서 @contoso.com 및 @region.contoso.com, hello DNS 레코드를 만듭니다.

| 항목 | 형식 | 주소 |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Azure Active Directory에서 장치 개체 보기 및 관리
1. Hello Azure 관리자 포털에서 볼, 차단, 있고 장치를 차단 해제 합니다. 차단 된 장치는 등록 된 장치 에서만 tooallow 구성된 된 액세스 tooapplications가 더 이상.
2. 관리자 권한으로 toohello Microsoft Azure 포털에 로그인 합니다.
3. Hello 왼쪽된 창에서 선택 **Active Directory**합니다.
4. 디렉터리를 선택합니다.
5. 선택 hello **사용자** 탭 합니다. 다음 사용자 tooview 자신의 장치를 선택
6. 선택 hello **장치** 탭 합니다.
7. 선택 **등록 된 장치가** hello에서 드롭다운 메뉴.
8. 여기, 같이 볼 수 있습니다. 차단 또는 hello 사용자가 등록 된 장치를 차단 해제 합니다.

## <a name="additional-topics"></a>추가 항목
Azure AD 장치 등록을 사용하여 Windows 7 및 Windows 8.1 도메인 가입 장치를 등록할 수 있습니다. 다음 항목 hello Windows 7 및 Windows 8.1 장치에 hello 필수 구성 요소 및 hello 단계 필요한 tooconfigure 장치 등록에 대 한 자세한 정보를 제공 합니다.

* [도메인 가입 Windows 장치의 Azure Active Directory 자동 장치 등록](active-directory-conditional-access-automatic-device-registration.md)
* [Windows 10 도메인에 가입된 장치의 Azure Active Directory 자동 장치 등록](active-directory-azureadjoin-devices-group-policy.md)

