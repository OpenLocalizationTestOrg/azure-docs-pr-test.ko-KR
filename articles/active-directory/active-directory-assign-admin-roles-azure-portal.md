---
title: "Azure Active Directory에서 관리자 역할 aaaAssigning | Microsoft Docs"
description: "관리자 역할 또는 사용자 편집, 관리 역할 tooothers 할당, 사용자 암호 다시 설정, 사용자 라이선스 관리 만들거나 도메인 관리. 관리자 역할이 할당 된 사용자에 게 hello 되므로 조직이 구독 하는 모든 클라우드 서비스 toowhich에서 동일한 사용 권한."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: it-pro;
ms.openlocfilehash: 41cddbf311767d9995c99ee386e6d276745dad18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Azure Active Directory에서 관리자 역할 할당
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-assign-admin-roles-azure-portal.md)
> * [Azure 클래식 포털](active-directory-assign-admin-roles.md)
>
>

Azure Active Directory (Azure AD)를 사용 하 여 지정할 수 있습니다 별도 관리자 tooserve 다양 한 기능입니다. 이러한 관리자는 액세스 toovarious 기능 hello Azure 포털 또는 Azure 클래식 포털에 있고, 해당 역할에 따라 컴퓨터 이름은 수 toocreate 또는 사용자를 편집, 관리 역할 tooothers 할당, 사용자 암호 다시 설정를 사용자 라이선스를 관리 하 고 무엇 보다도 도메인을 관리 합니다. 관리자 역할 할당은 사용자가 동일한 사용 권한을 할당 하는 여부에 관계 없이, 조직에서 구독 하는 hello 클라우드 서비스의 모든 hello Office 365 포털에서에서 역할 hello 또는 hello Azure 클래식 포털에서에서 또는 사용 하 여 hello hello를 갖습니다 합니다. Windows PowerShell 용 azure AD 모듈입니다.

관리자 역할을 수행 하는 hello 사용할 수 있습니다.

* **대금 청구 관리자**: 구입하고, 구독을 관리하고, 지원 티켓을 관리하고, 서비스 상태를 모니터링합니다.

* **호환성 관리자**:이 역할의 사용자는 hello Office 365 보안 및 규정 준수 센터 및 Exchange 관리 센터 내에서 관리 권한이 있어야 합니다. 자세한 내용은 “[Office 365 관리 역할 정보](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)”를 참조하세요.

* **CRM 서비스 관리자**:이 역할의 사용자가 Microsoft CRM Online 내에서 전역 권한을, hello 서비스가 있는 경우 hello 기능 toomanage 뿐만 아니라 티켓을 지원 하 고 서비스 상태를 모니터링 합니다. 자세한 내용은 [Office 365 관리 역할 정보](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)를 참조하세요.

* **장치 관리자**:이 역할의 사용자는 모든 Windows 10 장치에 조인 된 tooAzure Active Directory에 로컬 시스템 관리자로 지정할 수 있습니다. Azure Active Directory에 hello 기능 toomanage 장치 개체 없는 합니다.

* **디렉터리 읽기 권한자**: 이것은 레거시 중인 역할을 할당 toobe tooapplications hello를 지원 하지 않는 [동의 프레임 워크](active-directory-integrating-applications.md)합니다. Tooany 사용자가 할당 되지 않습니다.

* **디렉터리 동기화 계정**: 사용하지 마십시오. 이 역할 toohello Azure AD Connect 서비스는 자동으로 할당 하 고 의도 한 하거나 다른 용도로 지원지 않습니다.

* **디렉터리 기록기**: 이것은 레거시 중인 역할을 할당 toobe tooapplications hello를 지원 하지 않는 [동의 프레임 워크](active-directory-integrating-applications.md)합니다. Tooany 사용자가 할당 되지 않습니다.

* **Exchange 서비스 관리자**:이 역할의 사용자는 권한이 전역 내 Microsoft Exchange Online에서 hello 서비스가 있는 경우. 자세한 내용은 [Office 365 관리 역할 정보](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)를 참조하세요.

* **전역 관리자 / 회사 관리자**:이 역할의 사용자는 Azure Active Directory에 액세스 tooall 관리 기능이 있는 뿐만 아니라 해당 연결 tooAzure Exchange Online, SharePoint Online와 같은 Active Directory 서비스 및 비즈니스용 Skype Online 합니다. hello Azure Active Directory 테 넌 트에 가입한 hello 사람이 전역 관리자가 됩니다. 전역 관리자만 다른 관리자 역할을 할당할 수 있습니다. 회사에 여러 전역 관리자가 있을 수 있습니다. 전역 관리자는 모든 사용자 및 다른 모든 관리자에 대 한 hello 암호를 재설정할 수 있습니다.

  > [!NOTE]
  > Microsoft Graph API, Azure AD Graph API 및 Azure AD PowerShell에서 이 역할은 "회사 관리자"로 식별됩니다. "전역 관리자" hello 중인 [Azure 포털](https://portal.azure.com)합니다.
  >
  >

* **게스트 초대자**: hello "멤버 초대할 수 있는" 사용자 설정 tooNo 설정 된 경우이 역할의 사용자가 Azure Active Directory B2B 게스트 사용자 초대를 관리할 수 있습니다. B2B 공동 작업에 대 한 자세한 내용은 [hello Azure AD B2B 공동 작업 미리 보기에 대 한](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)합니다. 다른 권한은 포함되지 않습니다.

* **Intune 서비스 관리자**: hello 서비스가 있는 경우이 역할의 사용자가 Microsoft Intune Online 내에서 전역 권한을 합니다. 또한이 역할 hello 기능 toomanage 사용자 및 장치 순서 tooassociate 정책에 포함으로 그룹 만들기 및 관리 합니다.

* **사서함 관리자**: 이 역할은 RIM Blackberry 장치에 대한 Exchange Online 전자 메일 지원의 일부로만 사용됩니다. 조직이 RIM Blackberry 장치에서 Exchange Online 전자 메일을 사용하지 않는 경우 이 역할을 사용하지 마십시오.

* **파트너 계층 1 지원**: 사용하지 마십시오. 이 역할 되지 않으며 향후 hello에 Azure AD에서 제거 됩니다. 이 역할은 적은 수의 Microsoft 전매 파트너에서 사용하기 위한 것으로 일반적인 용도로는 적합하지 않습니다.

* **파트너 계층 2 지원**: 사용하지 마십시오. 이 역할 되지 않으며 향후 hello에 Azure AD에서 제거 됩니다. 이 역할은 적은 수의 Microsoft 전매 파트너에서 사용하기 위한 것으로 일반적인 용도로는 적합하지 않습니다.

* **암호 관리자/Helpdesk 관리자**: 이 역할의 사용자는 암호를 재설정하고, 서비스 요청을 관리하고, 서비스 상태를 모니터링할 수 있습니다. 암호 관리자는 사용자 및 다른 암호 관리자에 대해서만 암호를 다시 설정할 수 있습니다.

  > [!NOTE]
  > Microsoft Graph API, Azure AD Graph API 및 Azure AD PowerShell에서 이 역할은 "기술 지원팀 관리자"로 식별됩니다. "암호 관리자" hello 중인 [Azure 포털](https://portal.azure.com/)합니다.
  >
  >
  
* **Power BI 서비스 관리자**: hello 서비스가 있는 경우 hello 기능 toomanage 뿐만 아니라 티켓을 지원 하 고 서비스 상태를 모니터링,이 역할의 사용자는 Microsoft Power BI 내에서 전역 권한이 있어야 합니다. 자세한 내용은 [Office 365 관리 역할 정보](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US)를 참조하세요.

* **권한 있는 역할 관리자**: 이 역할의 사용자는 Azure Active Directory 및 Azure AD Privileged Identity Management 내에서 역할 할당을 관리할 수 있습니다. 또한 이 역할을 통해 Privileged Identity Management의 모든 측면을 관리할 수 있습니다.

* **보안 관리자**:이 역할의 사용자는 모든 hello 보안 읽기 역할 및 보안 관련 서비스에 대 한 hello 기능 toomanage 구성을 hello 읽기 전용 권한이 적용: Azure Active Directory Id 보호 권위 있는 Id 관리 및 Office 365 보안 및 준수 센터입니다. Office 365 사용 권한에 대 한 자세한 정보는 [hello Office 365 보안 및 규정 준수 센터에서 사용 권한을](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1)합니다.

* **보안 판독기**:이 역할의 사용자는 전역 읽기 전용 액세스는 모든 정보를 포함 하 여 Azure Active Directory, Id 보호, Privileged Identity Management으로 hello 기능 tooread Azure Active Directory에 로그인 보고서와 로그를 감사 합니다. hello 역할에는 Office 365 보안 및 준수 센터에서 읽기 전용 권한이 부여 됩니다. Office 365 사용 권한에 대 한 자세한 정보는 [hello Office 365 보안 및 규정 준수 센터에서 사용 권한을](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1)합니다.

* **서비스 지원 관리자**:이 역할의 사용자는 Azure 및 Office 365 서비스에 대 한 microsoft의 지원 요청에 열 수 있으며 뷰 hello hello Azure 포털의에서 대시보드 및 메시지 센터 서비스 및 Office 365 관리 포털. 자세한 내용은 [Office 365 관리 역할 정보](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)를 참조하세요.

* **SharePoint 서비스 관리자**: hello 서비스가 있는 경우 hello 기능 toomanage 뿐만 아니라 티켓을 지원 하 고 서비스 상태를 모니터링,이 역할의 사용자는 Microsoft SharePoint Online 내에서 전역 권한이 있어야 합니다. 자세한 내용은 [Office 365 관리 역할 정보](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)를 참조하세요.

* **비즈니스용 Skype / Lync 서비스 관리자**:이 역할의 사용자는 전역 내에서 사용 권한도 비즈니스용 Microsoft Skype hello 서비스 없으면으로 Azure Active Directory에 Skype 특정 사용자 특성을 관리 합니다. 또한이 역할 부여 hello 기능 toomanage 지원 티켓 및 모니터 상태를 서비스합니다. 자세한 내용은 [Office 365 관리 역할 정보](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)를 참조하세요.

  > [!NOTE]
  > Microsoft Graph API, Azure AD Graph API 및 Azure AD PowerShell에서 이 역할은 "Lync Service 관리자"로 식별됩니다. "Skype에 대 한 비즈니스 서비스 관리자" hello 중인 [Azure 포털](https://portal.azure.com/)합니다.
  >
  >

* **사용자 계정 관리자**: 이 역할의 사용자는 사용자 및 그룹의 모든 측면을 만들고 관리할 수 있습니다. 또한이 역할 hello 기능 toomanage 지원 티켓을 포함 하 고 모니터 상태를 서비스. 몇 가지 제한 사항이 적용됩니다. 예를 들어 이 역할은 전역 관리자 삭제를 허용하지 않는 반면 관리자가 아닌 사용자에 대한 암호 변경을 허용하며 전역 관리자 또는 다른 권한 있는 관리자에 대한 암호 변경을 허용하지 않습니다.

## <a name="administrator-permissions"></a>관리자 권한

### <a name="billing-administrator"></a>대금 청구 관리자

| 가능한 작업 | 불가능한 작업 |
| --- | --- |
|<p>회사 및 사용자 정보 보기</p><p>Office 지원 티켓 관리</p><p>Office 제품의 대금 청구 및 구매 작업 수행</p> |<p>사용자 암호 다시 설정</p><p>사용자 보기 만들기 및 관리</p><p>사용자 및 그룹 만들기/편집/삭제, 사용자 라이선스 관리</p><p>도메인 관리</p><p>회사 정보 관리</p><p>Tooothers 관리 역할 위임</p><p>디렉터리 동기화 사용</p><p>감사 로그 보기</p>|

### <a name="global-administrator"></a>전역 관리자
| 가능한 작업 | 불가능한 작업 |
| --- | --- |
| <p>회사 및 사용자 정보 보기</p><p>Office 지원 티켓 관리</p><p>Office 제품의 대금 청구 및 구매 작업 수행</p><p>사용자 암호 다시 설정</p>
<p>다른 관리자의 암호를 다시 설정</p> <p>사용자 보기 만들기 및 관리</p><p>사용자 및 그룹 만들기/편집/삭제, 사용자 라이선스 관리</p><p>도메인 관리</p><p>회사 정보 관리</p><p>Tooothers 관리 역할 위임</p><p>디렉터리 동기화 사용</p><p>다단계 인증 사용/사용 안 함</p><p>감사 로그 보기</p> |해당 없음 |

### <a name="password-administrator"></a>암호 관리자
| 가능한 작업 | 불가능한 작업 |
| --- | --- |
| <p>회사 및 사용자 정보 보기</p><p>Office 지원 티켓 관리</p><p>사용자 암호 다시 설정</p> <p>다른 관리자의 암호를 다시 설정</p>|<p>Office 제품의 대금 청구 및 구매 작업 수행</p><p>사용자 보기 만들기 및 관리</p><p>사용자 및 그룹 만들기/편집/삭제, 사용자 라이선스 관리</p><p>도메인 관리</p><p>회사 정보 관리</p><p>Tooothers 관리 역할 위임</p><p>디렉터리 동기화 사용</p><p>보고서 보기</p>|

### <a name="service-administrator"></a>서비스 관리자
| 가능한 작업 | 불가능한 작업 |
| --- | --- |
| <p>회사 및 사용자 정보 보기</p><p>Office 지원 티켓 관리</p> |<p>사용자 암호 다시 설정</p><p>Office 제품의 대금 청구 및 구매 작업 수행</p><p>사용자 보기 만들기 및 관리</p><p>사용자 및 그룹 만들기/편집/삭제, 사용자 라이선스 관리</p><p>도메인 관리</p><p>회사 정보 관리</p><p>Tooothers 관리 역할 위임</p><p>디렉터리 동기화 사용</p><p>감사 로그 보기</p> |

### <a name="user-administrator"></a>사용자 관리자
| 가능한 작업 | 불가능한 작업 |
| --- | --- |
| <p>회사 및 사용자 정보 보기</p><p>Office 지원 티켓 관리</p><p>제한 사항과 함께 사용자 암호 다시 설정.</p><p>다른 관리자의 암호를 다시 설정</p><p>다른 사용자의 암호를 다시 설정</p><p>사용자 보기 만들기 및 관리</p><p>제한 사항과 함께 사용자 및 그룹 만들기/편집/삭제, 사용자 라이선스 관리. 전역 관리자를 삭제하거나 다른 관리자를 만들 수 없습니다.</p> |<p>Office 제품의 대금 청구 및 구매 작업 수행</p><p>도메인 관리</p><p>회사 정보 관리</p><p>Tooothers 관리 역할 위임</p><p>디렉터리 동기화 사용</p><p>다단계 인증 사용/사용 안 함</p><p>감사 로그 보기</p> |

### <a name="security-reader"></a>보안 판독기
| 내용 | 가능한 작업 |
| --- | --- |
| ID 보호 센터 |모든 보안 보고서 및 보안 기능에 대한 설정 정보를 읽습니다.<ul><li>스팸 방지<li>암호화<li>데이터 손실 방지<li>맬웨어 방지<li>Advanced Threat Protection<li>피싱 방지<li>메일 흐름 규칙 |
| Privileged Identity Management |<p>Azure AD PIM에 표시 하는 읽기 전용 액세스 tooall 정보가: 정책 및 Azure AD 역할 할당에 대 한 보고서 보안을 검토 하 고 hello 미래 읽기 toopolicy 데이터 액세스 및 시나리오 외에도 Azure AD 역할 할당에 대 한 보고서입니다.<p>**없습니다** Azure AD PIM에 등록 하거나 모든 변경 내용을 tooit를 확인 합니다. PIM의 포털 또는 PowerShell을 통해 hello 사용자는 적합 한 경우 (예를 들어 전역 관리자 또는 역할 관리자 권한이 있는)에 추가 역할을 활성화할 수 있습니다이 역할에 속하는 사람. |
| <p>Office 365 서비스 상태 모니터링</p><p>Office 365 보안 및 규정 준수 센터</p> |<ul><li>경고 읽기 및 관리<li>보안 정책 읽기<li>위협 인텔리전스, 클라우드 앱 검색 및 검색 및 조사의 격리 읽기<li>모든 보고서 읽기 |

### <a name="security-administrator"></a>보안 관리자
| 내용 | 가능한 작업 |
| --- | --- |
| ID 보호 센터 |<ul><li>Hello 보안 읽기 역할의 모든 권한입니다.<li>또한 기능 tooperform 암호 재설정을 제외한 모든 IPC 작업 hello 합니다. |
| Privileged Identity Management |<ul><li>Hello 보안 읽기 역할의 모든 권한입니다.<li>**없습니다** . |
| <p>Office 365 서비스 상태 모니터링</p><p>Office 365 보안 및 규정 준수 센터 |<ul><li>Hello 보안 읽기 역할의 모든 권한입니다.<li>Hello Advanced Threat Protection 기능 (바이러스 및 맬웨어 보호, 악성 URL 구성, URL 추적 등)에서 모든 설정을 구성할 수 있습니다. |

## <a name="details-about-hello-global-administrator-role"></a>Hello 전역 관리자 역할에 대 한 세부 정보
전역 관리자에 게 액세스 tooall 관리 기능에 있습니다. 기본적으로 Azure 구독에 대 한 등록 hello 사람이 hello 디렉터리에 대 한 hello 전역 관리자 역할이 할당 됩니다. 전역 관리자만 다른 관리자 역할을 할당할 수 있습니다.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>전역 관리자로 동료 tooadd

1. Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 테 넌 트 디렉터리의 전역 관리자 인 계정을 사용 합니다.

   ![Azure AD 관리 센터 열기](./media/active-directory-assign-admin-roles-azure-portal/active-directory-admin-center.png)

2. **사용자 및 그룹 &gt; 모든 사용자**를 차례로 선택합니다.

3. 전역 관리자로 toodesignate을 해당 사용자에 대 한 hello 블레이드를 여세요 hello 사용자를 찾습니다.

4. Hello 사용자 블레이드 선택 **디렉터리 역할**합니다.
 
5. Hello 디렉터리 역할 블레이드에서 hello 선택 **전역 관리자** 역할을 하 고 저장 합니다.

## <a name="assign-or-remove-administrator-roles"></a>관리자 역할 할당 또는 제거
tooassign 관리 역할 tooa 사용자 Azure Active Directory에서 참조 하는 방법을 toolearn [Azure Active Directory 미리 보기에서 tooadministrator 역할에 사용자 지정](active-directory-users-assign-role-azure-portal.md)합니다.

## <a name="deprecated-roles"></a>사용되지 않는 역할

역할을 수행 하는 hello 사용할 수 없습니다. 이러한 되어 사용 되지 않으며 향후 hello에 Azure AD에서 제거 됩니다.

* 임시 라이선스 관리자
* 전자 메일 확인 사용자 생성자
* 장치 연결
* 장치 관리
* 장치 사용자
* 작업 공간 장치 연결

## <a name="next-steps"></a>다음 단계

* toochange 관리자는 Azure 구독에 대 한 참조 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooadd 또는 변경 Azure 관리자 역할](../billing-add-change-azure-subscription-administrator.md)
* Microsoft Azure에서 리소스 액세스 제어 하는 방법에 대 한 자세한 toolearn 참조 [Azure에서 리소스 액세스 이해](active-directory-understanding-resource-access.md)
* Azure Active Directory tooyour Azure 구독 연결 되는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 구독은 Azure Active Directory와 연결](active-directory-how-subscriptions-associated-directory.md)
* [사용자 관리](active-directory-create-users.md)
* [암호 관리](active-directory-manage-passwords.md)
* [그룹 관리](active-directory-manage-groups.md)
