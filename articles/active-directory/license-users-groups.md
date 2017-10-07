---
title: "Azure Active Directory에서 aaaLicense 사용자 | Microsoft Docs"
description: "자세한 방법을 toolicense 자신 및 Azure Active Directory에서 사용자가 있습니다."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>빠른 시작: Azure Active Directory에서 사용자의 라이선스
라이선스 기반 Azure AD 서비스는 Azure 테넌트에서 Azure AD(Active Directory) 구독을 활성화하면 작동됩니다. Hello 구독이 활성 상태 이면 서비스 기능이 Azure AD 관리자가 관리 되 고 사용이 허가 된 사용자가 사용 합니다. Enterprise Mobility + 보안, Azure AD Premium 또는 Azure AD Basic에서는 테 넌 트을 구입할 때 선불 라이선스로 hello 구독에서 유효 기간을 포함 하 여 업데이트 됩니다. 구독 정보를 사용할 수 없거나 할당 된 라이선스의 hello 번호를 포함 하는 hello Azure 통해 사용할 수에서 포털 **Azure Active Directory** 열어 hello 여 **라이선스** 바둑판식으로 배열 합니다. hello **라이선스** 블레이드 최상의 위치 toomanage 라이선스 할당 hello도 됩니다.

경우에 구독을 가져오는 모든 필요한 기능을 유료 tooconfigure 유료 Azure AD 유료 기능에 대 한 사용자 라이선스를 할당 해야 합니다. 액세스 권한이 있어야 하거나 Azure AD 유료 기능을 통해 관리되는 모든 사용자에게 라이선스가 할당되어야 합니다. 라이선스 할당은 Azure AD Premium, Basic 또는 Enterprise Mobility + Security 등의 구매한 서비스와 사용자 간의 매핑입니다.

사용할 수 있습니다 [그룹 기반의 라이선스 할당](active-directory-licensing-whatis-azure-portal.md) hello 다음과 같은 규칙을 tooset:
* 디렉터리의 모든 사용자가 자동으로 라이선스를 얻습니다.
* Hello 적절 한 직책을 가진 모든 사람에 게 라이선스
* Hello 조직에서 hello 의사 결정 tooother 관리자를 위임할 수 있습니다 (사용 하 여 [셀프 서비스 그룹](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> 라이선스 할당 toogroups, 대 한 자세한 내용은 포함 하 여 고급 시나리오 및 Office 365 라이선스 시나리오 참조 [toousers Azure Active Directory 그룹 멤버 자격을 통해 라이선스를 할당](active-directory-licensing-group-assignment-azure-portal.md)합니다.

## <a name="assign-licenses-toousers-and-groups"></a>라이선스 toousers 및 그룹 지정
활성 구독을 사용 하 여 먼저 라이선스 tooyourself 할당를 구독에 포함 된 예상 hello 기능을 모두 볼 수 있는 프로그램 브라우저 tooensure 새로 고침 합니다. hello 다음 단계 toopaid Azure AD 기능에 액세스 해야 하는 tooassign 라이선스 toohello 사용자입니다. 쉽게 tooassign 라이선스 tooindividuals가 아닌 사용자의 라이선스 toogroups tooassign입니다. 라이선스 tooa 그룹에 할당 하면 모든 그룹 구성원에는 라이선스가 할당 됩니다. 사용자가 더하거나 hello 그룹에서 제거 하는 경우 적절 한 라이선스 hello 자동으로 할당 하거나 제거 합니다. 

> [!NOTE]
> 일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다. 관리자에 게 hello를 지정 해야 tooa 사용자 라이선스를 할당할 수 있습니다, 전에 **사용 위치** hello 사용자에 대 한 속성. 이 속성을 설정할 수 있습니다 **사용자** &gt; **프로필** &gt; **설정을** hello Azure 포털의에서. 그룹 라이선스 할당을 사용할 경우 사용 위치가 지정 되지 않은 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다.

tooassign 라이선스 아래에서 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품**하나 이상의 제품을 선택한 다음 선택 **할당** hello 명령 모음에서 합니다.

![라이선스 tooassign 선택](media/license-users-groups/select-license-to-assign.png)

Hello를 사용할 수 있습니다 **사용자 및 그룹** 블레이드 toochoose hello 제품의 여러 사용자 또는 그룹 또는 toodisable 서비스 계획 합니다. 사용자 및 그룹 이름에 대 한 상위 toosearch에 hello 검색 상자를 사용 합니다.

![라이선스 할당을 위한 사용자 또는 그룹 선택](media/license-users-groups/select-user-for-license-assignment.png)

라이선스 tooa 그룹에 할당 하면 모든 사용자가 상속 hello 그룹의 hello 크기에 따라 hello 라이선스 되기까지 다소 시간이 걸릴 수 있습니다. Hello에 hello 처리 상태를 확인할 수 **그룹** hello 아래 블레이드 **라이선스** 바둑판식으로 배열입니다.

![라이선스 할당 상태](media/license-users-groups/license-assignment-status.png)

Azure AD 라이선스 할당 중에 할당 오류가 발생할 수 있지만 Azure AD 및 Enterprise Mobility + Security 제품을 관리할 경우에는 상대적으로 드물게 오류가 발생합니다. 잠재적 할당 오류는 다음으로 제한됩니다.
- 할당 충돌: 사용자 hello 현재 라이선스와 호환 되지 않는 라이선스를 이전에 할당 되었습니다. 이 경우 hello 새 라이선스를 할당 합니다. 현재 hello를 제거 해야 합니다.
- 사용 가능한 라이선스를 초과 했습니다: 사용자의 할당 상태가 반영 toomissing 라이선스 기한 오류 tooassign hello 할당 된 그룹에 사용자 수가 hello 사용 가능한 라이선스를 초과 합니다.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B 공동 작업 라이선스

B2B 공동 작업 tooinvite 게스트 사용자에 게 Azure AD 테 넌 트 tooprovide 액세스 tooAzure AD 서비스에 및 있습니다 사용할 수 있도록 모든 Azure 리소스 있습니다.  

무료 B2B 사용자 초대 및 Azure AD에서 응용 프로그램 tooan를 할당 합니다. 게스트 당 too10 앱을 사용자와 3 기본 보고서는 B2B 공동 작업 사용자에 게 무료로 합니다. 게스트 사용자 hello 파트너의 Azure AD 테 넌 트에 할당 된 적절 한 라이선스가 있으면은 합니다 라이선스를 취득 내용에 합니다.

필요 하지는 않지만 tooprovide 액세스 toopaid Azure AD 기능을 사용 하도록 하려는 경우 이러한 B2B 게스트 사용자에 게 사용 허가 받아야 적절 한 Azure AD 라이선스를 사용 합니다. 라이선스를 지불 하는 Azure AD와 테 넌 트 초대 B2B 공동 작업 사용자 권한 초대 tooan 추가 5 게스트 사용자에 게 할당할 수 toohello 테 넌 트입니다. 시나리오와 정보는 [B2B 공동 작업 라이선스 지침](active-directory-b2b-licensing.md)을 참조하세요.

## <a name="view-assigned-licenses"></a>할당된 라이선스 보기

할당된 라이선스 및 사용 가능한 라이선스에 대한 요약 보기는 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래 표시됩니다.

![라이선스 요약 보기](media/license-users-groups/view-license-summary.png)

특정 제품을 선택할 때 사용 가능한 할당된 사용자 및 그룹의 자세한 목록입니다. hello **사용이 허가 된 사용자가** 목록 현재 사용 하는 라이선스 및 여부 hello 라이선스가 할당 된 직접 toohello 사용자 또는 그룹에서 상속 하는 모든 사용자를 표시 합니다.

![라이선스 세부 정보 보기](media/license-users-groups/view-license-detail.png)

마찬가지로, hello **사용이 허가 된 그룹** 목록 toowhich 라이선스 할당 된 모든 그룹이 표시 됩니다. 사용자 또는 그룹 tooopen hello 선택 **라이선스** 모든 라이선스를 보여 주는 블레이드 toothat 개체를 할당 합니다.

## <a name="remove-a-license"></a>라이선스 제거

에 게 라이선스를 tooremove toohello 사용자 또는 그룹을 이동한 hello **라이선스** 바둑판식으로 배열입니다. Hello 라이선스를 선택 하 고 클릭 **제거**합니다.

![라이선스 제거](media/license-users-groups/remove-license.png)

라이선스 그룹에서 hello 사용자가 상속 직접 제거할 수 없습니다. 대신, hello 라이선스 상속 되는지은 hello 그룹에서 hello 사용자를 제거 합니다.


## <a name="next-steps"></a>다음 단계
이 퀵 스타트의 tooassign toousers 및 Azure AD 디렉터리에서 그룹을 허가 하는 방법을 배웠습니다. 

Hello Azure 포털에서에서 Azure AD에서 링크 tooconfigure 구독 라이선스 할당을 수행 하는 hello를 사용할 수 있습니다.

> [!div class="nextstepaction"]
> [Azure AD 라이선스 할당](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 