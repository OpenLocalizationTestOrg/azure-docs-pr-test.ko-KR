---
title: "Azure AD Privileged Identity Management에 aaaRoles | Microsoft Docs"
description: "Azure Privileged Identity Management 확장이 hello로 권한 있는 id 어떤 역할이 사용에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Azure Active Directory PIM의 다른 관리자 역할
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

사용자 할당 하 여 조직에서 toodifferent 관리 역할 Azure AD에서 합니다. 서비스 설정 변경, hello는 사용자가 수 tooperform Azure AD를 Office 365 및 기타 Microsoft 온라인 서비스와 연결 된 응용 프로그램 또는 역할은 사용자 추가 및 제거 등의 어떤 작업을 제어 합니다.  

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.

전역 관리자 사용자를 업데이트할 수 **영구적으로** tooroles 같은 PowerShell cmdlet을 사용 하 여 Azure AD에서 할당 된 `Add-MsolRoleMember` 및 `Remove-MsolRoleMember`, 또는에 설명 된 대로 hello 클래식 포털을 통해 [ Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)합니다.

Azure AD Privileged Identity Management(PIM)는 Azure AD에서 사용자에 대한 권한 있는 액세스의 정책을 관리합니다. PIM Azure AD에서 사용자가 tooone 또는 다른 역할을 할당 하 고 다른 사용자를 할당할 수 있습니다를 영구적으로 hello 역할 또는 hello 역할에 대 한 적격 toobe 합니다. 때 사용자 영구히 tooa 역할 할당 하거나 적합 한 역할 할당을 활성화 하는 다음 hello 사용 권한이 tootheir 역할을 할당 된 Azure Active Directory, Office 365 및 다른 응용 프로그램을 관리할 수 있습니다.

적격 역할 할당에 대 한 영구적인와 toosomeone hello 액세스에 차이가 없습니다. hello 유일한 차이 어떤 사람들 않아도 액세스 하는 모든 hello 시간입니다. Hello 역할에 대 한 적격 내용이 하며을 켤 수 있으며 오프 때마다 해야 합니다.

## <a name="roles-managed-in-pim"></a>PIM에서 관리되는 역할
Privileged Identity Management를 통해 포함 하 여 사용자가 toocommon 관리자 역할을 할당할 수 있습니다.

* **전역 관리자** (회사 관리자)에 대 한 액세스 tooall 관리 기능이 있습니다. 조직에는 전역 관리자가 두 개 이상 있을 수 있습니다. Office 365 toopurchase를 자동으로 등록 hello 사람이 전역 관리자가
* **권한 있는 역할 관리자** 는 Azure AD PIM을 관리하고 다른 사용자에 대한 역할 할당을 업데이트합니다.  
* **대금 청구 관리자** : 구입하고, 구독을 관리하고, 지원 티켓을 관리하고, 서비스 상태를 모니터링 합니다.
* **암호 관리자** : 암호를 재설정하고, 서비스 요청을 관리하고, 서비스 상태를 모니터링합니다. 암호 관리자는 사용자에 대 한 제한 된 tooresetting 암호.
* **서비스 관리자** : 서비스 요청을 관리하고 서비스 상태를 모니터링합니다.
  
  > [!NOTE]
  > Office 365를 사용 하는 경우 다음 hello 서비스 관리자 역할 tooa 사용자를 할당 하기 전에 먼저 hello 사용자 관리 권한을 할당 Exchange Online과 같은 tooa 서비스입니다.
  > 
  > 
* **사용자 관리 관리자** 는 암호를 다시 설정하고, 서비스 상태를 모니터링하고, 사용자 계정과 사용자 그룹 및 서비스 요청을 관리합니다. 사용자 관리 admin 님 안녕하세요 삭제할 전역 관리자, 다른 관리자 역할을 만들 하거나 청구, 전역 및 서비스 관리자가 관리자에 대 한 암호를 다시 설정할 수 없습니다.
* **Exchange 관리자** hello Exchange 관리 센터 (EAC)를 통해 온라인에 대 한 관리 액세스 tooExchange 있으며 Exchange Online에서 거의 모든 작업을 수행할 수 있습니다.
* **SharePoint 관리자** hello SharePoint Online 관리 센터를 통해 온라인에 대 한 관리 액세스 tooSharePoint 개이고 SharePoint Online에서 거의 모든 작업을 수행할 수 있습니다.
* **비즈니스 관리자에 대 한 Skype** 비즈니스 관리 센터에 대 한 Skype hello를 통해 비즈니스에 대 한 관리 액세스 tooSkype가와 온라인 비즈니스에 대 한 Skype에 거의 모든 작업을 수행할 수 있습니다.

[Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md) 및 [Office 365에서 관리자 역할 할당](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)에 대한 자세한 내용을 보려면 이 문서를 읽으세요.

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


수 PIM [이러한 역할 tooa 사용자 할당](active-directory-privileged-identity-management-how-to-add-role-to-user.md) hello 사용자 수 있도록 [필요할 때 hello 역할 활성화](active-directory-privileged-identity-management-how-to-activate-role.md)합니다.

Toogive PIM hello 사용자 toohave는에서 더 자세히 설명 해야 하는 hello 역할 자체를 PIM의 다른 사용자 액세스 toomanage를 원하는 경우 [toogive tooPIM를 액세스 하는 방법을](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)합니다.

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>PIM에서 관리되지 않는 역할
위에서 언급한 것을 제외하고 Exchange Online 또는 SharePoint Online 내에 있는 역할은 Azure AD에 표시되지 않으므로 PIM에서 볼 수 없습니다. 이러한 Office 365 서비스에서 세분화된 역할 할당 변경에 대한 자세한 내용은 [Office 365의 사용 권한](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d)을 참조하세요.

Azure 구독 및 리소스 그룹도 Azure AD에 표시되지 않습니다. toomanage Azure 구독을 참조 하세요. [어떻게 tooadd 또는 변경 Azure 관리자 역할](../billing/billing-add-change-azure-subscription-administrator.md) 및 Azure RBAC 참조에 대 한 자세한 내용은 [신속히 알아봅니다 액세스 제어](role-based-access-control-configure.md)합니다.

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>사용자 역할 및 로그인
일부 Microsoft 서비스 및 응용 프로그램에 대 한 사용자 tooa 역할을 할당 하지 않을 수 있습니다 충분 한 tooenable 해당 사용자 toobe 관리자 수 있습니다.

Azure 클래식 포털 액세스 toohello 필요 hello hello 사용자, 없는 경우에 필요 toomanage hello Azure 구독, 사용자는 Azure 구독에 공동 관리자 또는 서비스 관리자 여야 합니다.  예를 들어 hello 클래식 포털을 사용자의 Azure AD에 대 한 구성 설정을 toomanage Azure ad에서 전역 관리자와 Azure 구독에 대해 구독 공동 관리자 여야 합니다.  tooadd 사용자 tooAzure 구독을 확인 하려면 어떻게 해야 toolearn [어떻게 tooadd 또는 변경 Azure 관리자 역할](../billing/billing-add-change-azure-subscription-administrator.md)합니다.

온라인 서비스 해야 하는 액세스 tooMicrosoft hello 사용자도 할당 될 라이선스 관리 작업을 수행 하거나 hello 서비스 포털을 열 수 있습니다.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Azure AD에서 라이선스 tooa 사용자 지정
1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com) 전역 관리자 계정 또는 공동 관리자 계정.
2. 선택 **모든 항목** hello 주 메뉴에서 합니다.
3. Hello 디렉터리와 toowork와 연결 되어 있다는 라이선스 것을 선택 합니다.
4. **라이선스**를 선택합니다. 사용 가능한 라이선스의 hello 목록이 표시 됩니다.
5. Toodistribute hello 라이선스를 포함 하는 hello 라이선스 계획을 선택 합니다.
6. **사용자 할당**을 선택합니다.
7. 라이선스 tooassign 선택 hello 사용자를 합니다.
8. Hello 클릭 **할당** 단추입니다.  hello 사용자 tooAzure 지금 로그인 할 수 있습니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

