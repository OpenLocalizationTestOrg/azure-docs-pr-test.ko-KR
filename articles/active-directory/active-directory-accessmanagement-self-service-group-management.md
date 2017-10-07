---
title: "셀프 서비스 응용 프로그램 액세스 관리에 대 한 Azure Active directory aaaSetting | Microsoft Docs"
description: "셀프 서비스 그룹 관리 사용자 toocreate 있으며 특정 보안 그룹 또는 Azure Active Directory와 제안 사용자 hello 가능성 toorequest 보안 그룹 또는 Office 365 그룹 멤버 자격에서 Office 365 그룹 관리"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>셀프 서비스 그룹 관리를 위한 Azure Active Directory 설정
셀프 서비스 그룹 관리 사용자 toocreate 있으며 특정 보안 그룹 또는 Azure Active Directory (Azure AD)에 Office 365 그룹을 관리 합니다. 사용자 보안 그룹 또는 Office 365 그룹 멤버 자격을 요청할 수도 및 다음 hello hello 그룹의 소유자를 승인 하거나 거부할 수 멤버 자격입니다. 이러한 방식으로 일상적인 그룹 멤버 자격 제어 해당 구성원 자격에 대 한 hello 비즈니스 컨텍스트를 이해 하는 위임 된 toopeople 될 수 있습니다. 셀프 서비스 그룹 관리 기능은 보안 그룹 및 Office 365 그룹에 대해서만 사용할 수 있지만 메일 사용 가능 보안 그룹 및 메일 그룹에는 사용할 수 없습니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.

셀프 서비스 그룹 관리는 현재 위임된 그룹 관리 및 셀프 서비스 그룹 관리 등 두 개의 중요한 시나리오로 구성되어 있습니다.

* **위임 된 그룹 관리** 예로 hello 회사에서 사용 하는 액세스 tooa SaaS 응용 프로그램을 관리 하는 관리자입니다. 이러한 액세스 권한을 관리 져 서 번거롭게이 관리자 hello 비즈니스 소유자 toocreate 새 그룹을 요청 합니다. 관리자에 게 hello 응용 프로그램 toohello 새 그룹에 대 한 액세스를 할당 한 toohello 그룹이 이미 toohello 응용 프로그램에 액세스 하는 모든 사용자를 추가 합니다. hello 경영 주는 다음 추가할 수 더 많은 사용자가 있으며 해당 사용자가 자동으로 프로 비전 된 toohello 응용 프로그램. hello 경영 주는 사용자에 대 한 hello 관리자 toomanage 액세스용 toowait이 필요 하지 않습니다. 관리자에 게 부여 하는 경우 해당 사용자가 자신의 사용자에 대 한 액세스를 관리할 수도 한 다음 다른 비즈니스 그룹에 동일한 사용 권한 tooa 관리자 hello 합니다. Hello 경영 주는 아니고 hello 관리자 보거나 관리할 수 있는 다른 사용자의 사용자입니다. 관리자에 게 액세스 toohello 응용 프로그램 및 필요한 경우 블록 액세스 권한을 가진 모든 사용자가을 볼 수 있습니다.
* **셀프 서비스 그룹 관리** - 이 시나리오의 예제에서는 독립적으로 설정한 SharePoint Online 사이트를 보유한 두 사용자를 가정합니다. 다른 사용자의 액세스 tootheir 사이트 팀이 각 toogive를 원합니다. tooaccomplish이를 해당 그룹 tooprovide 액세스 tootheir 사이트 선택 각각의 SharePoint Online에서 하 고 Azure AD에서 그룹을 만들 수 있습니다. 액세스 하려는 사용자 hello 액세스 패널에서에서 해당 요청이 및 승인 후 이러한 액세스 tooboth SharePoint Online 사이트를 자동으로 가져옵니다. 나중에, 그 중 하나가 hello 사이트에 액세스 하는 모든 사용자 액세스 tooa 특정 SaaS 응용 프로그램을 가져올 수도 해야 결정 합니다. hello SaaS 응용 프로그램의 관리자에 게 hello 응용 프로그램 toohello SharePoint Online 사이트에 대 한 액세스 권한을 추가할 수 있습니다. 이제부터 승인을 받아야 하는 모든 요청 액세스 toohello 두 SharePoint Online 사이트 및 toothis SaaS 응용 프로그램을 제공 합니다.

## <a name="making-a-group-available-for-end-user-self-service"></a>최종 사용자 셀프 서비스에서 그룹을 사용할 수 있도록 지정
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), Azure AD 디렉터리를 엽니다.
2. Hello에 **구성** 탭, 설정 **위임 된 그룹 관리** tooEnabled 합니다.
3. 설정 **사용자 보안 그룹을 만들 수** 또는 **사용자가 Office 그룹을 만들 수** tooEnabled 합니다.

때 **사용자 보안 그룹을 만들 수** 가 활성화 디렉터리의 모든 사용자 toocreate 새 보안 그룹에 허용 되지 않으며 toothese 그룹을 구성원을 추가 합니다. 다른 모든 사용자에 대 한 hello 액세스 패널에에서 이러한 새 그룹 표시도 됩니다. Hello hello 그룹 정책 설정에서 허용 하는 경우 다른 사용자가 요청 toojoin 이러한 그룹 만들 수 있습니다. **사용자가 보안 그룹을 만들 수 있음** 을 사용하지 않도록 설정한 경우 사용자 그룹을 만들 수 없고 기존 그룹의 소유자를 변경할 수 없습니다. 그러나 수 여전히 관리 해당 그룹의 구성원 hello 하 해당 그룹의 다른 사용자가 toojoin 요청을 승인 합니다.

사용할 수도 있습니다 **보안 그룹에 대 한 셀프 서비스를 사용할 수 있는 사용자** tooachieve 사용자를 위한 셀프 서비스 그룹 관리를 통해 좀 더 세분화 된 액세스 제어 합니다. 때 **사용자 그룹을 만들 수** 가 활성화 디렉터리의 모든 사용자 toocreate 새 그룹에 허용 되지 않으며 toothese 그룹을 구성원을 추가 합니다. 또한 설정 하 여 **보안 그룹에 대 한 셀프 서비스를 사용할 수 있는 사용자** 제한 된 tooSome, 그룹 관리 tooonly 제한 된 사용자 그룹입니다. 이 스위치는 tooSome 설정 되 면 수 있으려면 먼저 새 그룹을 만들고 구성원 toothem 추가 사용자 toohello 그룹 SSGMSecurityGroupsUsers를 추가 해야 합니다. 설정 하 여 **보안 그룹에 대 한 셀프 서비스를 사용할 수 있는 사용자** tooAll, directory toocreate 새 그룹의 모든 사용자가 사용 합니다.

Hello를 사용할 수도 있습니다 **보안 그룹에 대 한 셀프 서비스를 사용할 수 있는 그룹** toospecify 멤버가 셀프 서비스를 사용할 수는 그룹에 대 한 사용자 지정 이름을 상자입니다.

## <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [그룹 설정을 구성하는 Azure Active Directory cmdlets](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory란?](active-directory-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
