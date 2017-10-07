---
title: "Azure Active Directory의 aaaManaging 그룹 | Microsoft Docs"
description: "어떻게 toocreate 그룹 toomanage Azure 관리 및 사용자가 Azure Active Directory를 사용 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Azure Active Directory에서 그룹 관리
> [!div class="op_single_selector"]
> * [쉬운 테이블](active-directory-groups-create-azure-portal.md)
> * [Azure 클래식 포털](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Azure Active Directory (Azure AD) 사용자 관리 hello 기능 중 하나는 사용자의 hello 기능 toocreate 그룹입니다. 할당 하는 등 라이선스 또는 권한을 tooa 사용자 수가 한 번에 한 그룹 tooperform 관리 작업을 사용 합니다. 또한 그룹 tooassign 액세스 권한을 사용할 수 있습니다.

* 예: hello 디렉터리의 개체는 리소스
* SaaS 응용 프로그램, Azure 서비스, SharePoint 사이트 또는 온-프레미스 리소스와 같은 리소스 외부 toohello 디렉터리

또한 리소스 소유자는 다른 사용자가 소유한 액세스 tooa 리소스 tooan Azure AD 그룹을 할당할 수도 있습니다. 이 할당 해당 그룹 액세스 toohello 리소스의 hello 구성원에 게 부여 합니다. 그런 다음 hello 그룹의 hello 소유자 hello 그룹의 멤버 자격을 관리합니다. 효과적으로 hello 리소스 소유자 대리자 toohello의 소유자 hello 그룹 hello 권한 tooassign 사용자 tootheir 리소스입니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. Hello Azure AD 관리 센터에서 toomanage 그룹 방법을 참조 [그룹을 만들고 Azure Active Directory에 멤버 추가](active-directory-groups-create-azure-portal.md)합니다.

## <a name="how-do-i-create-a-group"></a>그룹을 만드는 방법
Hello 서비스 toowhich 조직에서 구독을 따라 hello 다음 중 하나를 사용 하 여 그룹을 만들 수 있습니다.

* hello Azure 클래식 포털
* hello Office 365 계정 포털
* hello Windows Intune 계정 포털

설명 하 고 작업 hello Azure 클래식 포털에서에서 수행 합니다. Azure AD 디렉터리 toomanage 비 Azure 포털을 사용 하는 방법에 대 한 자세한 내용은 참조 [Azure AD 디렉터리 관리](active-directory-administer.md)합니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.
2. 선택 hello **그룹** 탭 합니다.
3. **그룹 추가**를 선택합니다.
4. Hello에 **그룹 추가** 창의 hello 이름을 지정 하 고 hello에 대 한 그룹 설명 합니다.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>보안 그룹에서 개별 사용자를 추가하거나 제거하는 방법
**개별 사용자 tooa 그룹 tooadd**

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.
2. 선택 hello **그룹** 탭 합니다.
3. Hello 그룹 toowhich를 tooadd 구성원이 엽니다. 열기 hello **멤버** hello 탭 그룹을 선택 하는 경우 표시 되지 것입니다.
4. **멤버 추가**를 선택합니다.
5. Hello에 **구성원 추가** 페이지, hello 사용자 또는이 그룹의 구성원으로 tooadd 원하는 그룹이 선택 hello 이름입니다. 이 이름은 toohello 추가 되는지 확인 **선택한** 창.

**tooremove 개별 사용자의 그룹**

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.
2. 선택 hello **그룹** 탭 합니다.
3. Tooremove 멤버 원하는 hello 그룹을 엽니다.
4. 선택 hello **멤버** 탭,이 그룹에서 tooremove 원하고 클릭 hello 멤버의 선택 hello 이름 **제거**합니다.
5. Hello 프롬프트 것인지 확인 하는 tooremove hello 그룹에서이 멤버입니다.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>그룹의 구성원이 hello를 동적으로 관리할 수는 방법
Azure AD에서 사용자 toobe 그룹의 멤버인 hello 간단한 규칙 toodetermine를를 매우 쉽게 설정할 수 있습니다. 간단한 규칙에서 단일 비교를 수행합니다. 예를 들어 그룹이 SaaS 응용 프로그램 tooa 할당 되 면 설정할 수 있습니다 "Sales Rep". 직함을 가진 규칙 tooadd 사용자를 이 규칙의 디렉터리에 해당 직책을 가진 toothis SaaS 응용 프로그램 tooall 사용자 액세스를 다음 권한을 부여 합니다.

사용자 변경의 특성을 hello 시스템 평가 되 면 hello 특성 변경 hello 사용자의 모든 그룹을 발생 시키는 경우 디렉터리 toosee의 모든 동적 그룹 규칙을 추가 하거나 제거 합니다. 그룹에 규칙을 충족 하는 사용자, 멤버 toothat 그룹으로 추가 됩니다. 멤버인 그룹의 hello 규칙을 더 이상 만족 하는 경우는 멤버와 해당 그룹에서 제거 됩니다.

> [!NOTE]
> 보안 그룹 또는 Office 365 그룹에서 동적 멤버 자격에 대한 규칙을 설정할 수 있습니다. 중첩 된 그룹 멤버 자격 그룹 기반 할당 tooapplications에 대 한 현재 지원 되지 않습니다.
>
> 그룹에 대 한 동적 멤버 자격을 할당 하는 Azure AD Premium 라이선스 toobe 필요
>
> * hello 규칙 그룹에서 관리 하는 hello 관리자
> * Hello 그룹의 모든 멤버
>
>

**그룹에 대 한 동적 멤버 자격 tooenable**

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.
2. 선택 hello **그룹** 탭 및 tooedit hello open 그룹입니다.
3. 선택 hello **구성** 탭을 클릭 한 다음 설정 **동적 멤버 자격 사용** 너무**예**합니다.
4. 그룹 toocontrol hello에 대 한 간단한 단일 규칙을 설정 합니다.이 그룹 기능에 대 한 동적 멤버 자격입니다. 있는지 hello 확인 **사용자 추가 위치** 옵션을 선택 하 고 (예를 들어, 부서, 직책 등), hello 목록에서 사용자 속성을 선택 합니다
5. 그런 다음, 조건(같지 않음, 같음, 다음으로 시작 안 함, 다음으로 시작, 포함 안 함, 포함, 일치하지 않음, 일치)을 선택합니다.
6. Hello 선택한 사용자 속성에 대 한 비교 값을 지정 합니다.

방법에 대 한 toolearn toocreate *고급* 규칙 (여러 비교를 포함할 수 있는 규칙) 동적 그룹 멤버 자격에 대 한 참조 [toocreate 특성을 사용 하 여 고급 규칙](active-directory-accessmanagement-groups-with-advanced-rules.md)합니다.

## <a name="additional-information"></a>추가 정보
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [그룹 설정을 구성하는 Azure Active Directory cmdlets](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory란?](active-directory-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
