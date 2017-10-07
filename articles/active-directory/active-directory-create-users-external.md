---
title: "다른 디렉터리 또는 Azure Active Directory에서 파트너 회사의 사용자가 aaaAdd | Microsoft Docs"
description: "에 대해 설명 방법을 tooadd 사용자가 외부 및 게스트 사용자를 포함 한 Azure Active Directory에서 사용자 정보를 변경 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가

이 문서에서는 설명 어떻게 tooadd 사용자가 Azure Active Directory에 있는 다른 디렉터리에서 또는 파트너 회사에서 사용자를 추가 합니다. 조직 내에서 새 사용자를 추가 하 고 Microsoft 계정을 가진 사용자를 추가 하는 방법에 대 한 정보를 참조 하십시오. [추가 Active Directory에 새 사용자 tooAzure](active-directory-create-users.md)합니다. 

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. Admin 님 안녕하세요 Azure AD에서에서 tooadd B2B 공동 작업 게스트 사용자의 가운데에 대 한 참조 [Azure AD B2B 공동 작업 이란?](active-directory-b2b-what-is-azure-ad-b2b.md)

기본적으로 추가 된 사용자가 관리자 권한이 필요는 없지만 언제 든 지 역할 toothem를 할당할 수 있습니다.

## <a name="add-a-user"></a>사용자 추가
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. **Active Directory**를 선택한 다음 디렉터리를 엽니다.
3. 선택 hello **사용자** 탭을 선택한 다음 hello 명령 모음에서 선택 **사용자 추가**합니다.
4. Hello에 **이 사용자에 대해 알리기** 페이지의 **유형의 사용자**을 하나 선택:

   * **다른 Azure AD 디렉터리의 사용자** – 다른 Azure AD 디렉터리에서 소싱 된 사용자 계정 tooyour 디렉터리에 추가 합니다. 또한 사용자는 해당 디렉터리의 멤버인 경우에만 또 다른 디렉터리의 사용자를 선택할 수 있습니다.
   * **파트너 회사의 사용자** -tooinvite 고 파트너 회사 사용자 tooyour 디렉터리 권한을 부여 (참조 [Azure Active Directory B2B 공동 작업](active-directory-b2b-what-is-azure-ad-b2b.md)). 너무 해야[전자 메일 주소를 지정 하는 CSV 파일 업로드](active-directory-b2b-references-csv-file-format.md)합니다.
5. Hello 사용자에 **프로필** 페이지에서 첫 번째 및 마지막 이름, 사용자에 게 친숙 한 이름 및 hello에서 사용자 역할을 제공 합니다. **역할** 목록입니다. 사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요. 지정 여부 너무**다단계 인증 사용** hello 사용자에 대 한 합니다.
6. Hello에 **임시 암호 가져오기** 페이지에서 **만들기**합니다.

> [!IMPORTANT]
> 조직에서 둘 이상의 도메인을 사용 하는 경우 사용자 계정을 추가할 때 문제를 다음 hello 알아야:
>
> * tooadd 사용자 계정과 도메인 간에 동일한 사용자 계정 이름 (UPN) hello **첫 번째** 추가, 예를 들어 geoffgrisso@contoso.onmicrosoft.com, **이어서** geoffgrisso@contoso.com합니다.
> * geoffgrisso@contoso.onmicrosoft.com을 추가하기 전에 geoffgrisso@contoso.com을 추가하지 **마세요**.
>

온-프레미스 Active Directory 서비스와 id 동기화 되는 사용자에 대 한 정보를 변경 하면 hello Azure 클래식 포털에서에서 hello 사용자 정보를 변경할 수 없습니다. toochange hello 사용자 정보를 온-프레미스 Active Directory 관리 도구를 사용 합니다.

## <a name="add-external-users"></a>외부 사용자 추가
추가할 수 있습니다도 사용자가 사용자가 속한 다른 Azure AD 디렉터리 toowhich 또는 파트너 회사에서 CSV 파일을 업로드 하 여 합니다. tooadd 외부 사용자에 대 한 **사용자 유형**, 지정 **다른 Microsoft Azure AD 디렉터리의 사용자** 또는 **파트너 회사의 사용자**합니다.

두 형식의 사용자는 모두 다른 디렉터리가 원본이며 **외부 사용자**로 추가됩니다. 외부 사용자는 모든 요구 사항 tooadd 새 계정 및 자격 증명 없이 디렉터리에 다른 사용자와 공동 작업할 수 있습니다. 외부 사용자가 로그인 할 때 추가 된 다른 디렉터리 toowhich 인증은 해당 홈 디렉터리도 인증 합니다.

## <a name="external-user-management-and-limitations"></a>외부 사용자 관리 및 제한 사항
다른 디렉터리 tooyour 디렉터리에서 사용자를 추가 하면 해당 사용자는 디렉터리의 외부 사용자입니다. hello 표시 이름 및 사용자 이름 홈 디렉터리에서 복사 하 고 hello 디렉터리에 외부 사용자에 대해 사용 됩니다. 이제부터 hello 외부 사용자 계정의 속성은 완전히 독립적입니다. 속성이 변경 되 면 toohello 사용자가 홈 디렉터리에서 해당 변경 내용이 전파 되지 toohello 외부 사용자 계정을 디렉터리에 있습니다.

hello 두 개의 계정 사이의 유일한 연결은 hello 해당 hello 사용자가 항상 홈 디렉터리에 대해 또는 Microsoft 계정으로 인증 됩니다. 바로 이러한 이유로 옵션 tooreset hello 암호를 표시 하지 않거나 외부 사용자에 대해 multi-factor authentication을 사용 하도록 설정 합니다. 현재 hello 홈 디렉터리 또는 Microsoft 계정의 hello 인증 정책을 하나 hello 사용자가 로그인 할 때 평가 되는 hello입니다.

> [!NOTE]
> 여전히 hello tooyour 디렉터리에 액세스를 차단 하는 hello 디렉터리에 외부 사용자를 해제할 수 있습니다.
>
>

에서 홈 디렉터리에서 사용자가 삭제 되거나 Microsoft 계정을 취소 하는 경우 hello 외부 사용자는 디렉터리에 여전히 존재 합니다. 그러나 디렉터리의 hello 사용자 홈 디렉터리 또는 Microsoft 계정으로 인증할 수 없는 리소스 액세스할 수 없습니다.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>현재 Azure AD 외부 사용자의 액세스를 지원하는 서비스
* **Azure 클래식 포털**:는 외부 사용자가 여러 디렉터리 toomanage 각 해당 디렉터리의 관리자가 있습니다.
* **SharePoint Online**: 외부 공유를 사용 하는 경우 외부 사용자 tooaccess 권한이 SharePoint Online 리소스에 있습니다.
* **Dynamics CRM**: hello 사용자에 PowerShell을 통해 사용이 허가 하는 경우에 외부 사용자 tooaccess Dynamics CRM의 리소스 수 있는 권한이 있습니다.
* **Dynamics AX**: hello 사용자에 PowerShell을 통해 사용이 허가 하는 경우에 외부 사용자 tooaccess Dynamics AX의 리소스 수 있는 권한이 있습니다. 제한 사항에 대 한 hello [외부 사용자가 Azure AD](#known-limitations-of-azure-ad-external-users) tooexternal 사용자가 Dynamics AX에도 적용 합니다.

## <a name="next-steps"></a>다음 단계
* [새 사용자 tooAzure Active Directory를 추가 합니다.](active-directory-create-users.md)
* [Azure AD 관리](active-directory-administer.md)
* [Azure AD에서 암호 관리](active-directory-manage-passwords.md)
* [Azure AD에서 그룹 관리](active-directory-manage-groups.md)
