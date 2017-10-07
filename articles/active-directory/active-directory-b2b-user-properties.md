---
title: "Azure Active Directory B2B 공동 작업 사용자의 aaaProperties | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 사용자 속성은 구성 가능합니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Azure Active Directory B2B 공동 작업 사용자 속성

Azure AD(Azure Active Directory) B2B 공동 작업 사용자는 UserType이 Guest인 사용자입니다. 이 게스트 사용자는 파트너 조직에서 일반적으로 되며 제한 된 hello 기본적으로 디렉터리를 초대에 권한을 갖는 합니다.

조직의 요구를 초대 hello에 따라 Azure AD B2B 공동 작업 사용자 hello 계정 상태를 다음 중 하나에 하나일 수 있습니다.

- 상태 1: Azure AD의 인스턴스 외부에 이며 조직 초대 hello에서 게스트 사용자로 표시 합니다. 이 경우 hello B2B 사용자 초대 toohello 테 넌 트에 속하는 Azure AD 계정을 사용 하 여 로그인 합니다. Hello 파트너 조직에서 Azure AD를 사용 하지 않는 경우 Azure AD에서 게스트 사용자 hello 여전히 만들어집니다. hello 요건은 자신의 초대를 교환 하 고 Azure AD가 전자 메일 주소를 확인 합니다. 이것을 JIT(Just In Time) 테넌트 또는 “바이럴” 테넌트라고도 합니다.

- 상태 2: Microsoft 계정에 속한 이며 hello 호스트 조직에서 게스트 사용자로 표시 합니다. 이 경우 hello 게스트 사용자가 Microsoft 계정으로 로그인 합니다. hello 초대 사용자의 소셜 id (google.com 또는 유사한 곳), 상환 제공 하는 동안 Microsoft 계정으로 만들어집니다 Microsoft 계정 않습니다.

- 상태 3: hello 호스트 조직 온-프레미스 Active Directory에 속한 및 동기화 hello 호스트 조직의 azure AD. 이 버전에서는 PowerShell toomanually 변경 hello 이러한 사용자의 UserType hello 클라우드에서 사용 해야 합니다.

- 상태 4: Azure 호스트 조직에에서 속한 AD UserType와 = 게스트 및 hello 호스트 조직에서 관리 하는 자격 증명입니다.

  ![hello 초대자 이니셜을 표시합니다.](media/active-directory-b2b-user-properties/redemption-diagram.png)


이제 Azure AD에서 상태 1의 Azure AD B2B 공동 작업 사용자가 어떻게 보이는지 살펴보겠습니다.

### <a name="before-invitation-redemption"></a>초대 상환 전

![제안 상환 전](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>초대 상환 후

![제안 상환 후](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Hello Azure AD B2B 공동 작업 사용자의 키 속성
### <a name="usertype"></a>UserType
이 속성의 테 넌 트 사용자 toohello 호스트 hello hello 관계를 나타냅니다. 이 속성에는 다음 두 가지 값이 사용될 수 있습니다.
- 멤버:이 값의 hello 호스트 조직 직원 및 사용자 hello 조직의 급여에 나타냅니다. 예를 들어이 사용자는 toohave 액세스 toointernal 전용 사이트 필요합니다. 이 사용자는 외부 공동 작업자로 간주되지 않습니다.

- 게스트:이 값은 사용자가 내부 toohello 회사 외부 공동 작업자, 파트너, 고객 또는 유사한 사용자와 같은 것으로 간주 되지 않습니다 나타냅니다. 이러한 사용자가 될 예상된 tooreceive CEO의 내부 메모, 또는 예를 들어 회사 혜택을 받을입니다.

  > [!NOTE]
  > hello UserType 없고 관계 toohow hello 사용자가 로그인에, hello 사용자 및 등의 hello 디렉터리 역할에 있습니다. 이 속성 단순히 hello 사용자의 관계 toohello 호스트 조직 나타내고이 속성에 종속 된 tooenforce 정책을 hello 조직을 수 있습니다.

### <a name="source"></a>원본
이 속성은 hello 사용자가 로그인 하는 방법을 나타냅니다.

- 초대된 사용자: 이 사용자는 초대되었지만 초대를 아직 상환하지 않았습니다.

- 외부 Active Directory:이 사용자는 외부 조직에서 홈 고 다른 조직의 toohello에 속하는 Azure AD 계정을 사용 하 여 인증 합니다. 이 유형의 로그인 tooState 1 해당합니다.

- Microsoft 계정: 이 사용자는 Microsoft 계정에 속하며 Microsoft 계정을 사용하여 인증합니다. 이 유형의 로그인 tooState 2 해당합니다.

- Windows Server Active Directory:이 사용자가 로그인 toothis 조직 속한 온-프레미스 Active Directory에서. 이 유형의 로그인 tooState 3은 해당합니다.

- Azure Active Directory: toothis 조직에 속하는 Azure AD 계정을 사용 하 여이 사용자를 인증 합니다. 이 유형의 로그인 tooState 4 해당합니다.
  > [!NOTE]
  > Source와 UserType은 독립적인 속성입니다. Source의 값은 UserType에 대한 특정 값을 의미하지 않습니다.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Azure AD B2B 사용자를 게스트 대신 구성원으로 추가할 수 있습니까?
일반적으로 Azure AD B2B 사용자와 게스트 사용자는 동의어입니다. 따라서 Azure AD B2B 공동 작업 사용자는 기본적으로 UserType = Guest인 사용자로 추가됩니다. 그러나 경우에 따라 hello 파트너 조직의 대규모 조직 toowhich hello 호스트 조직의 구성원도 속합니다. 이 경우 hello 호스트 조직은 tootreat 게스트 대신 멤버로 hello 파트너 조직의 사용자가 할 수 있습니다. Azure AD B2B 초대 관리자 Api tooadd hello를 사용 하 여 또는 멤버로 hello 파트너 조직 toohello 호스트 조직에서 사용자를 초대 합니다.

## <a name="filter-for-guest-users-in-hello-directory"></a>Hello 디렉터리의 게스트 사용자에 대 한 필터

![게스트 사용자 필터링](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>UserType 변환
현재 있기 사용자 tooconvert UserType 멤버 tooGuest 그 반대로 줄에서 PowerShell을 사용 하 여 합니다. 그러나 hello UserType 속성 toorepresent hello 사용자의 관계 toohello 조직이 있어야 합니다. 따라서이 속성의 값 hello hello 사용자 toohello 조직의 hello 관계가 변경 하는 경우에 변경 해야 합니다. Hello 사용자의 hello 관계 변경 되 면 hello 사용자 계정 이름 (UPN) 변경 해야 하는지 여부와 같은 문제를 해결 해야? Hello 사용자 toohave 액세스 toohello 계속 동일한 리소스? 사서함을 할당해야 합니까?와 같은 다른 질문에 답변해야 합니다. 따라서 원자성 활동으로 PowerShell을 사용 하 여 hello UserType을 변경 하지 않는 것이 좋습니다. 뿐만 아니라 PowerShell을 사용하여 이 속성을 변경 불가능으로 만드는 경우 이 값에 의존하지 않는 것이 좋습니다.

## <a name="remove-guest-user-limitations"></a>게스트 사용자 제한 제거
사례 toogive 게스트 사용자가 더 높은 권한이 있을 수 있습니다. 게스트 사용자 tooany 역할을 추가 하 고도 hello 디렉터리 toogive에 hello 기본 게스트 사용자 제한을 구성원으로 권한을 동일 사용자 hello 제거할 수 있습니다.

Hello 회사 디렉터리에 게스트 사용자에 게 제공할 수 있도록 가능한 tooturn hello 기본 게스트 사용자 제한이 해제는 hello 구성원 사용자와 같은 권한을 사용 합니다.

![게스트 사용자 제한 제거](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [B2B 공동 작업 사용자 감사 및 보고](active-directory-b2b-auditing-and-reporting.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업을 위한 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
