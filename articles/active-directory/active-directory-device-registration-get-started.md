---
title: "Windows Azure Active directory 도메인에 가입 된 장치 aaaHow tooconfigure 자동 등록 | Microsoft Docs"
description: "설정 하면 도메인에 가입 된 Windows 장치 tooregister 자동으로 Azure Active Directory와 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Azure Active Directory 장치 등록 시작

Azure Active Directory device registration은 장치 기반 조건부 액세스 시나리오에 대 한 hello foundation 합니다. 장치가 등록 되 면 Azure Active Directory 장치 등록 hello 사용자가 로그인 할 때 사용 되는 tooauthenticate hello를 장치가 되는 id 사용 하 여 hello 장치를 제공 합니다. 인증 된 hello 장치와 hello 장치의 hello 특성 수 hello 클라우드 및 온-프레미스에서 호스트 되는 응용 프로그램에 대 한 조건부 액세스 정책을 사용 하는 tooenforce 합니다.

Microsoft Intune 같은 모바일 장치 management(MDM) 솔루션을 함께 사용 하면 Azure Active Directory의 장치 특성이 hello hello 장치에 대 한 추가 정보로 업데이트 됩니다. 이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다. Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 Intune에서 관리에 대해 장치 등록을 참조하세요.
Azure Active Directory Device Registration으로 사용할 수 있는 시나리오. Azure Active Directory 장치 등록에서는 iOS, Android 및 Windows 장치를 지원합니다. Azure AD Device Registration을 활용 하는 hello 개별 시나리오는 보다 구체적인 요구 사항 및 플랫폼 지원이 있을 수 있습니다. 

이러한 시나리오는 다음과 같습니다.

- **Microsoft Intune을 사용한 Office 365 응용 프로그램에 대 한 조건부 액세스:** hello에서 동일한 시간 규격 장치에서 정보 근로자를 허용 하는 동안 IT 관리자는 다음 조건부 액세스 장치 정책을 toosecure 회사 리소스를 프로 비전 할 수 tooaccess hello 서비스입니다. 자세한 내용은 Office 365 서비스에 대한 조건부 액세스 장치 정책을 참조하세요.

- **조건부 액세스 tooapplications 온-프레미스 호스팅:** 응용 프로그램을 Windows Server 2012 r 2를 사용 하 여 toouse AD FS 구성에 대 한 액세스 정책을 사용 하 여 등록 된 장치를 사용할 수 있습니다. 온-프레미스에 대해 조건부 액세스를 설정하는 방법에 대한 자세한 내용은 [Azure Active Directory 장치 등록을 사용하여 온-프레미스 조건부 액세스 설정](active-directory-device-registration-on-premises-setup.md)을 참조하세요.

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory Device Registration 설정

toosetup 장치 등록을 여러 가지가 있습니다.

- 장치를 등록할 때 수 조인된 tooAzure AD 도메인입니다. 이 항목에 대 한 자세한에 대 한 사용자가 toojoin Azure AD 도메인에 필요한 Azure AD Join 및 hello 설정을 자세히 알아볼 수 있습니다.

- 사용자가 추가 작업 또는 학교 계정 tooWindows 개인 장치에서 모바일 장치 등록에 필요한 tooa 작업 리소스를 연결 하는 경우 장치를 등록할 수 있습니다. tooensure이 hello Azure 포털에서에서 Azure AD Device Registration을 사용 하도록 설정 해야 합니다. 

- 기존 도메인 조인 컴퓨터에 대해서는 자동 장치 등록을 사용하여 장치를 등록할 수 있습니다. tooensure이를 자동 장치 등록을 계속 하기 전에 설치 프로그램이 Azure AD Connect를 첫 번째 수행 해야 합니다.

최신 지침을 참조 하십시오. [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.  
검토 하 고 사용 하도록 설정 하거나 수도 hello 관리자 포털을 사용 하 여 Azure Active Directory에 등록 된 장치를 사용 하지 않도록 설정 합니다.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Hello Azure Active Directory 장치 등록 서비스를 사용 하도록 설정

**tooenable hello Azure Active Directory 장치 등록 서비스:**

1.  관리자 권한으로 Microsoft Azure 포털 toohello에 로그인 합니다.

2.  Hello 왼쪽된 창에서 선택 **Active Directory**합니다.

3.  Hello 디렉터리 탭에서 디렉터리를 선택 합니다.

4.  **Configure**를 클릭합니다.

5.  너무 스크롤하여**장치**합니다.

6.  “사용자가 장치를 Azure AD에 등록할 수 있습니다.”에 대해 모두를 선택합니다.

7.  Hello 최대 수를 선택 하려는 tooauthorize 사용자 당 장치의 합니다.

Office 365에 대 한 Microsoft Intune 또는 모바일 장치 관리 hello 등록 장치 등록이 필요합니다. 이러한 서비스 중 하나를 구성한 경우 **모두**가 선택되고 **없음** 단추는 사용할 수 없습니다. 이러한 올바르게 구성 되어 있고 hello 적절 한 라이선스를 확인 하십시오.

기본적으로 hello 서비스에 대 한 2 단계 인증이 사용 되지 않습니다. 그러나 장치를 등록하는 경우 2단계 인증을 사용하는 것이 좋습니다.

- 이 서비스에 대 한 2 단계 인증을 요구 하기 전에 해야 합니다 Azure Active Directory에서 다단계 인증 공급자를 구성 하 고 Multi-factor Authentication에 대 한 사용자 계정을 구성 하십시오 다단계 인증 추가 참조 Active Directory tooAzure

- Windows Server 2012 R2에서 AD FS를 사용하는 경우 AD FS에서 2단계 인증 모듈을 구성해야 합니다. Active Directory Federation Services로 Multi-Factor Authentication 사용을 참조하세요.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Azure Active Directory에서 장치 개체 보기 및 관리

Hello Azure 관리자 포털에서 볼, 차단, 있고 장치를 차단 해제 합니다. 차단 된 장치는 등록 된 장치 에서만 tooallow 구성된 된 액세스 tooapplications가 더 이상.

**tooview 및 Azure Active Directory의 장치 개체를 관리 합니다.**
 
1.  관리자 권한으로 Microsoft Azure 포털 toohello에 로그인 합니다.

2.  Hello 왼쪽된 창에서 선택 **Active Directory**합니다.

3.  디렉터리를 선택합니다.

4.  **사용자**를 선택합니다. 

5.  Toosee hello 장치 원하는 hello 사용자를 클릭 합니다.

6.  **장치**를 선택합니다.

7.  **등록된 장치**를 선택합니다.

이제, 검토, 차단, 또는 hello 사용자의 등록 된 장치를 차단 해제 합니다.
온-프레미스 도메인에 가입 하 고 자동으로 등록 된 Windows 10 장치 hello 사용자 탭 아래에 표시 되지 않습니다. 모든 엔터프라이즈 장치를 hello Get MsolDevice PowerShell 명령 toofind 키를 따르십시오. 


## <a name="next-steps"></a>다음 단계

toosetup 자동 장치 등록 참조 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.


