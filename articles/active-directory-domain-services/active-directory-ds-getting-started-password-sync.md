---
title: "Azure Active Directory Domain Services: 암호 동기화 활성화 | Microsoft Docs"
description: "Azure Active Directory Domain Services 시작"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>암호 동기화 tooAzure Active Directory 도메인 서비스를 사용 하도록 설정
이전 작업에서 Azure AD(Azure Active Directory) 테넌트에 대해 Azure Active Directory Domain Services를 사용하도록 설정했습니다. hello 다음 작업은 관리자 NTLM (NT LAN) 및 Kerberos 인증 tooAzure에 필요한 자격 증명 해시의 tooenable 동기화 AD 도메인 서비스. 자격 증명 동기화를 설정한 후 사용자가 회사 자격 증명으로 관리 되는 도메인 toohello 로그인 수 있습니다.

Azure AD Connect를 사용 하 여 온-프레미스 디렉터리에서 동기화 되는 클라우드 전용 사용자 계정 및 사용자 계정에 대 한 관련 된 hello 단계 서로 다릅니다.  Azure AD 테 넌 트의 조합은 하는 경우 사용자와 사용자가 온-프레미스에서 클라우드, AD tooperform 두 단계가 필요 합니다.

<br>

> [!div class="op_single_selector"]
> * **클라우드 전용 사용자 계정을**: [클라우드 전용 사용자 tooyour 관리 되는 도메인 계정에 대해 암호 동기화](active-directory-ds-getting-started-password-sync.md)
> * **온-프레미스 사용자 계정과**: [온-프레미스에서 동기화 된 사용자 계정에 대 한 암호 동기화 할 AD tooyour 도메인 관리](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>태스크 5: 암호 동기화 tooyour 클라우드 전용 사용자 계정에 대 한 관리 되는 도메인을 사용 하도록 설정
관리 되는 도메인에 hello tooauthenticate 사용자, Azure Active Directory 도메인 서비스에는 NTLM 및 Kerberos 인증을 위해 적합 한 형식으로 해시 자격 증명 필요 합니다. Azure AD를 생성 하지 않거나 형태로 표시 hello 테 넌 트에 대 한 Azure Active Directory 도메인 서비스를 설정할 때까지 NTLM 또는 Kerberos 인증을 하는 데 필요한 자격 증명 해시를 저장 합니다. 확실한 보안상의 이유로 Azure AD는 암호 자격 증명을 일반 텍스트 형식으로 저장하지 않습니다. 따라서 Azure AD 사용자의 기존 자격 증명에 따라 이러한 NTLM 또는 Kerberos 자격 증명 해시를 생성 하는 방식으로 tooautomatically가 없습니다.

> [!NOTE]
> 조직에 클라우드 전용 사용자 계정이 있는 경우 toouse Azure Active Directory 도메인 서비스를 해야 하는 사용자가 암호를 변경 해야 합니다. 클라우드 전용 사용자 계정에는 hello Azure 포털 또는 Azure AD PowerShell cmdlet 중 하나를 사용 하 여 Azure AD 디렉터리에서 만든 계정이입니다. 이러한 사용자 계정은 온-프레미스 디렉터리에서 동기화되지 않습니다.
>
>

이 암호 변경 프로세스는 hello 자격 증명은 Azure AD에서 생성 하는 Kerberos 및 NTLM 인증 toobe에 대 한 Azure Active Directory 도메인 서비스에 필요한 해시 하면 됩니다. Hello에서 모든 사용자 toouse Azure Active Directory 도메인 서비스를 해야 하는 테 넌 트 또는 toochange 지시에 대 한 hello 암호 만료 되거나 수는 암호입니다.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>클라우드 전용 사용자 계정에 대해 NTLM 및 Kerberos 자격 증명 해시 생성 사용
Hello 지침 tooprovide 사용자가 암호를 변경할 수는 다음과 같습니다.

1. Toohello 이동 [Azure AD 액세스 패널](http://myapps.microsoft.com) त ा.

    ![Hello Azure AD 액세스 패널을 시작 합니다.](./media/active-directory-domain-services-getting-started/access-panel.png)

2. Hello 오른쪽 위의 모서리에서 이름을 클릭 하 고 선택 **프로필** hello 메뉴에서 합니다.

    ![프로필 선택](./media/active-directory-domain-services-getting-started/select-profile.png)

3. Hello에 **프로필** 페이지에서 클릭 **암호 변경**합니다.

    !["암호 변경" 클릭](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > 경우 hello **암호 변경** hello 액세스 패널 창에 옵션이 표시 되지 않습니다, 조직에서 구성한 확인 [Azure AD의 암호 관리](../active-directory/active-directory-passwords-getting-started.md)합니다.
   >
   >
4. Hello에 **암호 변경** 페이지, 기존 (현재) 암호를 입력 하 고, 새 암호를 입력 하 고 확인 합니다.

    ![Azure AD 도메인 서비스에 대한 가상 네트워크를 만듭니다.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. **제출**을 클릭합니다.

암호를 변경한 후 몇 분이 hello 새 암호는 Azure Active Directory 도메인 서비스에서 사용할 수 있습니다. 몇 분 후 (일반적으로 약 20 분) hello 새로 변경 된 암호를 사용 하 여 관리 되는 도메인 조인된 toohello 있는 toocomputers 로그인 할 수 있습니다.

## <a name="related-content"></a>관련 콘텐츠
* [어떻게 tooupdate 암호](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Azure AD에서 암호 관리 시작](../active-directory/active-directory-passwords-getting-started.md)
* [암호 동기화 사용 tooAzure Active Directory 도메인 서비스에 대 한 동기화 된 Azure AD 테 넌 트](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Azure Active Directory Domain Services 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
* [Windows 가상 컴퓨터 tooan Azure Active Directory 도메인 서비스에서 관리 하는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)
* [Red Hat Enterprise Linux 가상 컴퓨터 tooan Azure Active Directory 도메인 서비스에서 관리 하는 도메인에 가입](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
