---
title: "aaaUse Azure Active Directory에 액세스 tooresources toomanage 그룹화 | Microsoft Docs"
description: "Azure Active Directory toomanage 사용자의 toouse 그룹 액세스 방법을 tooon 온-프레미스 및 클라우드 응용 프로그램 및 리소스."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리
Azure Active Directory (Azure AD)는 방대한 집합이 기능 toomanage 액세스 tooon 온-프레미스 및 클라우드 응용 프로그램 및 Office 365 같은 Microsoft 온라인 서비스를 포함 하 여 리소스를 제공 하는 포괄적인 id 및 액세스 관리 솔루션 및 무수 한 타사 SaaS 응용 프로그램입니다. 이 문서에서는 개요를 제공 하지만 Azure AD를 사용 하 여 toostart 지금 바로 그룹화 하려는 경우, hello 지침에 따라 [Azure AD에서 보안 그룹 관리](active-directory-accessmanagement-manage-groups.md)합니다. 자세한 내용은 Azure Active directory에 toosee 하려는 경우 PowerShell toomanage를 사용 하는 방법을 그룹화 [그룹 관리에 대 한 Azure Active Directory cmdlet](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)합니다.

> [!NOTE]
> Azure Active Directory toouse Azure 계정이 필요 합니다. 계정이 없으면 [무료 Azure 계정을 등록](https://azure.microsoft.com/pricing/free-trial/)할 수 있습니다.
>
>

Azure AD within hello 기능 toomanage 액세스 tooresources은 hello 주요 기능 중 하나입니다. 이러한 리소스는 hello 디렉터리나 SaaS 응용 프로그램, Azure 서비스 및 SharePoint 사이트 또는 온-프레미스와 같은 외부 toohello 디렉터리에 있는 리소스에 대 한 역할을 통해 권한 toomanage 개체 hello 경우 처럼 hello 디렉터리의 일부가 될 수 있습니다. 리소스입니다. 네 가지 방법으로 사용자 액세스 권한 tooa 리소스를 할당할 수 있습니다.

1. 직접 할당

    사용자가 할당 될 수 있습니다 직접 tooa 리소스 해당 리소스의 hello 소유자입니다.
2. 그룹 멤버 자격

    그룹 수와 할당할 수 tooa 리소스 hello 리소스 소유자에 의해 이렇게 하면 해당 그룹 액세스 toohello 리소스의 hello 멤버 부여. Hello 그룹의 hello 소유자에 의해 hello 그룹의 구성원이 관리할 수 있습니다. 효과적으로 hello 리소스 소유자 대리자 hello hello 그룹 권한 tooassign 사용자 tootheir 리소스 toohello 소유자입니다.
3. 규칙 기반

    hello 리소스 소유자는 어떤 사용자가 액세스 tooa 리소스를 할당 해야 하는 규칙 tooexpress를 사용할 수 있습니다. hello 결과가 hello 규칙의 특정 사용자에 대 한 해당 규칙 및 해당 값에 사용 된 hello 특성에 종속 하 고 작업을 통해 hello 리소스 소유자 효과적으로 위임 hello 오른쪽 toomanage 액세스 tootheir 리소스 toohello 권위 hello에 대 한 hello 규칙에 사용 되는 특성입니다. hello 리소스 소유자는 여전히 자체 hello 규칙을 관리 하 고 tootheir 리소스 액세스를 제공 하는 특성 및 값을 결정 합니다.
4. 외부 기관

    외부 소스;에서 파생 된 hello 액세스 tooa 리소스 예를 들어, 온-프레미스 디렉터리와 같은 신뢰할 수 있는 소스는 또는 WorkDay와 같은 SaaS 응용 프로그램에서 동기화 되는 그룹입니다. hello 리소스 소유자 hello 그룹 tooprovide 액세스 toohello 리소스를 할당 하 고 hello 외부 소스 hello 그룹의 구성원 hello를 관리 합니다.

   ![액세스 관리 다이어그램의 개요](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>액세스 관리를 설명하는 비디오 보기
이에 대해 자세히 설명하는 짧은 비디오를 볼 수 있습니다.

**그룹에 대 한 azure AD: 소개 toodynamic 멤버 자격**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Azure Active Directory에서 액세스 관리는 어떻게 작동합니까?
Hello에 hello Azure AD 액세스 관리 솔루션의 중심은 hello 보안 그룹입니다. 보안 그룹 toomanage 액세스 tooresources를 사용 하 여 hello 의도 한 사용자 그룹에 대해 유연 하 고 이해 하기 쉬운 방식으로 tooprovide 액세스 tooa 리소스에 대 한 허용 하는 잘 알려진 패러다임입니다. hello 리소스 소유자 (또는 hello 디렉터리의 관리자에 게) 그룹 tooprovide 특정는 액세스 오른쪽 toohello 리소스 자신이 소유한 할당할 수 있습니다. hello 그룹의 구성원 hello hello 액세스가 제공 됩니다 및 hello 리소스 소유자의 부서 관리자 또는 기술 지원팀 관리자 같은 다른 한 그룹 toosomeone hello 오른쪽 toomanage hello 멤버 목록에 위임할 수 있습니다.

![Azure Active Directory 액세스 관리 다이어그램](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

그룹 소유자 hello 작업도 가능 해당 그룹 셀프 서비스 요청에 사용할 수 있습니다. 이 과정에서 최종 사용자 수를 검색 하 고 hello 그룹을 찾을 요청 toojoin hello 그룹을 통해 관리 되는 권한 tooaccess hello 리소스를 효율적으로 검색. 조인 요청을 자동으로 승인 또는 hello 소유자에 의해 hello 그룹의 승인이 필요 있도록 hello 그룹의 hello 소유자 hello 그룹을 설정할 수 있습니다. 사용자 요청 toojoin 그룹의 구성, toohello 그룹의 소유자를 hello hello 조인 요청이 전달 됩니다. Hello 요청을 승인 하는 hello 소유자 중 하나로 hello 요청 하는 사용자 알림이 전송 되 고 hello 사용자가 조인 된 toohello 그룹입니다. Hello 요청을 거부 하는 hello 소유자 중 하나로 hello 요청 하는 사용자가 알림이 되지만 toohello 그룹에 조인 되지 않습니다.

## <a name="getting-started-with-access-management"></a>액세스 관리 시작
준비 tooget 시작 합니까? 일부의 hello Azure AD 그룹으로 수행할 수 있는 기본적인 작업을 시도해 보십시오. 이러한 기능 tooprovide 특수화를 사용 하 여 toodifferent 그룹에 속한 조직의 리소스에 액세스 합니다. 다음은 기본 첫 단계 목록입니다.

* [그룹에 대 한 동적 멤버 자격 tooconfigure는 간단한 규칙 만들기](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [그룹 toomanage 액세스 tooSaaS 응용 프로그램을 사용 하 여](active-directory-accessmanagement-group-saasapps.md)
* [최종 사용자 셀프서비스에 사용할 수 있는 그룹 만들기](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect를 사용 하는 온-프레미스 그룹 tooAzure를 동기화 하는 중](active-directory-aadconnect.md)
* [그룹에 대한 소유자 관리](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>다음 단계
액세스 관리의 hello 기본 사항을 이해 했으면,이 몇 가지 추가 고급 기능을 Azure Active Directory에서 사용할 수 있는 액세스 tooyour 응용 프로그램 및 리소스를 관리 합니다.

* [고급 규칙 toocreate 특성을 사용 하 여](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Azure AD의 보안 그룹 관리](active-directory-accessmanagement-manage-groups.md)
* [Azure AD에서 전용 그룹 설정](active-directory-accessmanagement-dedicated-groups.md)
* [그룹에 대한 그래프 API 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [그룹 설정을 구성하는 Azure Active Directory cmdlets](active-directory-accessmanagement-groups-settings-cmdlets.md)
