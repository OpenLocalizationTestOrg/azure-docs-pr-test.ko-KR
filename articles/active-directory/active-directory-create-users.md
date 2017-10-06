---
title: "aaaAdd 새 사용자 tooAzure Active Directory | Microsoft Docs"
description: "에 대해 설명 방법을 tooadd 새 사용자 또는 Azure Active Directory에서 사용자 정보를 변경 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>새 사용자 또는 Microsoft 계정 tooAzure Active Directory와 사용자 추가
사용자가 toopopulate 디렉터리를 추가 합니다. 이 문서에서는 설명 방법을 tooadd 조직 내에서 새 사용자와 방법을 tooadd 사용자에 게 Microsoft 계정을 있습니다. Azure Active Directory의 다른 디렉터리의 사용자 추가 또는 파트너 회사의 사용자 추가에 대한 자세한 내용은 [Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가](active-directory-create-users-external.md)를 참조하세요. 기본적으로 추가 된 사용자가 관리자 권한이 필요는 없지만 언제 든 지 역할 toothem를 할당할 수 있습니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. Tooadd hello Azure AD 관리 센터에서 사용자 참조에 대 한 [추가 Active Directory에 새 사용자 tooAzure](active-directory-users-create-azure-portal.md)합니다.

## <a name="add-a-user"></a>사용자 추가
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **Active Directory**, 조직 디렉터리의 hello 이름을 선택 합니다.
3. 선택 hello **사용자** 탭을 선택한 다음 hello 명령 모음에서 선택 **사용자 추가**합니다.
4. Hello에 **이 사용자에 대해 알리기** 페이지의 **유형의 사용자**을 하나 선택:

   * **조직의 새 사용자** – 디렉터리에 새 사용자 계정을 추가합니다.
   * **기존 Microsoft 계정 사용자** – 기존 Microsoft 소비자 계정 tooyour 디렉터리 (예: Outlook 계정)를 추가 합니다.
5. **사용자 유형**에 따라 사용자 이름(새 사용자) 또는 전자 메일 주소(Microsoft 계정이 있는 사용자)를 입력합니다.
6. Hello 사용자에 **프로필** 페이지에서 첫 번째 및 마지막 이름, 사용자에 게 친숙 한 이름 및 hello에서 사용자 역할을 제공 합니다. **역할** 목록입니다. 사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요. 지정 여부 너무**다단계 인증 사용** hello 사용자에 대 한 합니다.
7. Hello에 **임시 암호 가져오기** 페이지에서 **만들기**합니다.

> [!IMPORTANT]
> 조직에서 둘 이상의 도메인을 사용 하는 경우 사용자 계정을 추가할 때 문제를 다음 hello 알아야:
>
> * tooadd 사용자 계정과 도메인 간에 동일한 사용자 계정 이름 (UPN) hello **첫 번째** 추가, 예를 들어 geoffgrisso@contoso.onmicrosoft.com, **이어서** geoffgrisso@contoso.com합니다.
> * geoffgrisso@contoso.onmicrosoft.com을 추가하기 전에 geoffgrisso@contoso.com을 추가하지 **마세요**. 이 순서는 중요, 하며 번거로운 tooundo 될 수 있습니다.
>
>

## <a name="change-user-information"></a>사용자 정보 변경
Hello 개체 ID 제외 하 고 모든 사용자 특성을 변경할 수 있습니다.

1. 디렉터리를 엽니다.
2. 선택 hello **사용자** 탭 및의 표시 이름을 선택한 후 hello hello toochange 하려는 사용자입니다.
3. 변경을 완료하고 **저장**을 클릭합니다.

변경 하는 hello 사용자는 온-프레미스 Active Directory 서비스와 동기화 되 면이 절차를 사용 하 여 hello 사용자 정보를 변경할 수 없습니다. toochange hello 사용자 하려면 온-프레미스 Active Directory 관리 도구를 사용 합니다.

## <a name="guest-user-management-and-limitations"></a>게스트 사용자 관리 및 제한 사항
게스트 계정은 초대한 tooyour 디렉터리 tooaccess SharePoint 문서, 응용 프로그램, 또는 다른 Azure 리소스로 이었던 다른 디렉터리의 사용자입니다. 디렉터리에 게스트 계정에는 기본 UserType 특성 설정 너무 "Guest." 일반 사용자 (특히, 디렉터리의 구성원) 특성이 hello UserType "멤버"입니다.

게스트는 hello 디렉터리에 제한 된 권한 집합이 있어야 합니다. 이러한 권한은 hello 디렉터리에 다른 사용자에 대 한 게스트 toodiscover 정보에 대 한 hello 기능을 제한합니다. 그러나 게스트 사용자에 게 hello 사용자 및 그룹에서 작업 하는 hello 리소스와 관련 된 상호 작용 여전히 있습니다. 게스트 사용자는 다음 작업을 수행할 수 있습니다.

* 다른 사용자와 그룹을 할당 하는 Azure 구독 toowhich와 관련 된 참조
* 소속 그룹 toowhich의 hello 멤버를 참조 하십시오.
* Hello 사용자의 hello 전체 전자 메일 주소를 알고 있으면 hello 디렉터리에 다른 사용자가을 조회합니다
* 제한 된 집합의 특성을-제한 toodisplay 이름, 전자 메일 주소, 사용자 계정 이름 (UPN) 및 미리 보기 사진 찾아볼 hello 사용자의를 참조 하십시오.
* Hello 디렉터리의 확인 된 도메인 목록 가져오기
* 권한을 부여 하는 동의 tooapplications hello 멤버 디렉터리에 있는 동일한 액세스

## <a name="set-guest-user-access-policies"></a>게스트 사용자 액세스 정책 설정
hello **구성** 디렉터리의 탭에는 게스트 사용자에 대 한 옵션 toocontrol 액세스 합니다. 이러한 옵션은 디렉터리 전역 관리자에 의해 Azure 클래식 포털에서만 변경될 수 있습니다. 현재는 PowerShell 또는 API 메서드가 없습니다.

tooopen hello **구성** hello에 탭 Azure 클래식 포털에서 선택 **Active Directory**, hello 디렉터리의 hello 이름을 선택 합니다.

![Azure Active Directory의 구성 탭][1]

다음 게스트 사용자에 대 한 hello 옵션 toocontrol 액세스를 편집할 수 있습니다.

![게스트 사용자에 대한 액세스 제어 옵션][2]

## <a name="whats-next"></a>다음 단계
* [Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가](active-directory-create-users-external.md)
* [Azure AD 관리](active-directory-administer.md)
* [Azure AD에서 암호 관리](active-directory-manage-passwords.md)
* [Azure AD에서 그룹 관리](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
