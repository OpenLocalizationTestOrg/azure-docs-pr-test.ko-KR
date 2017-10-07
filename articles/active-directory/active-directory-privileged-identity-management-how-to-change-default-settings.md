---
title: "aaaHow toomanage 역할 활성화 설정을 | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management 확장 hello로 toochange 권한 있는 id에 대 한 기본 설정을 hello 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>방법을 Azure AD Privileged Identity Management에 toomanage 역할 활성화 설정
권한 있는 역할 관리자는 사용자에 게 적합 역할 할당을 활성화 하는 hello 환경을 변경 하는 등, 조직에서 Azure AD Privileged Identity Management (PIM)를 사용자 지정할 수 있습니다.

## <a name="manage-hello-role-activation-settings"></a>त ा ळ hello 역할 활성화
1. Toohello 이동 [Azure 포털](https://portal.azure.com) 및 선택 hello **Azure AD Privileged Identity Management** hello 대시보드에서 응용 프로그램입니다.
2. **권한 있는 역할 관리** > **설정** > **권한 있는 역할**을 선택합니다.
3. Hello 역할 설정을 선택 toomanage 원하는 합니다.

각 역할에 대 한 hello 설정 페이지에서 다양 한 설정 구성할 수 있습니다. 이러한 설정은 영구 관리자가 아닌, 적격 관리자인 사용자에게만 영향을 미칩니다.

**정품 인증**: 역할의 만료 되기 전에 들이 활성 상태로 유지 되는 시간 단위로 hello 시간입니다. 이는 1 ~ 72시간 사이가 될 수 있습니다.

**알림**: hello 시스템 역할을 활성화 한 것을 확인 하는 전자 메일 tooadmins 전송 여부를 선택할 수 있습니다. 이 정보는 무단 또는 불법 활성화를 탐지하는 데 유용할 수 있습니다.

**인시던트/요청 된 티켓**: toorequire 적격 admins tooinclude 티켓 번호의 역할을 활성화 여부를 선택할 수 있습니다. 이 기능은 역할 액세스 감사를 수행할 때 유용할 수 있습니다.

**Multi-factor Authentication**: 선택할 수 있습니다 여부 toorequire 사용자 tooverify 자신의 id의 역할을 활성화 하기 전에 MFA 사용 합니다. 들이 tooverify 역할을 활성화 될 때마다 하지 세션 마다 한 번이만이 있습니다. MFA를 사용 하도록 설정 하면 염두에 두 가지 팁 tookeep을 가지 있습니다.

* 전자 메일 주소에 대 한 Microsoft 계정을 가진 사용자 (일반적으로 @outlook.com, 항상 그렇지는 않지만) Azure MFA에 대해 등록할 수 없습니다. Microsoft 계정 가진 tooassign 역할 toousers 하려면 영구 관리자 있도록 하거나 해당 역할에 대 한 MFA를 사용 하지 않도록 설정 합니다.
* Azure AD 및 Office365에 대해 높은 권한이 있는 역할에 대한 MFA를 사용하지 않도록 설정할 수 없습니다. 이런 안전 기능을 둔 것은 이러한 역할을 신중하게 보호해야 하기 때문입니다.  
  
  * 응용 프로그램 관리자
  * 응용 프로그램 프록시 서버 관리자
  * 대금 청구 관리자  
  * 규정 준수 관리자  
  * CRM 서비스 관리자
  * 고객 LockBox 액세스 승인자
  * 디렉터리 기록기  
  * Exchange 관리자  
  * 전역 관리자
  * Intune 서비스 관리자
  * 사서함 관리자  
  * 파트너 계층1 지원  
  * 파트너 계층2 지원  
  * 권한 있는 역할 관리자   
  * 보안 관리자  
  * SharePoint 관리자  
  * 비즈니스용 Skype 관리자  
  * 사용자 계정 관리자  

PIM으로 MFA를 사용 하는 방법에 대 한 자세한 내용은 참조 [어떻게 MFA tooRequire](active-directory-privileged-identity-management-how-to-require-mfa.md)합니다.

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

