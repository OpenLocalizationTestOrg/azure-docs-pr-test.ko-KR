---
title: "Azure Active Directory에서 만료를 그룹화 하는 Office 365 aaaPreview | Microsoft Docs"
description: "Azure Active Directory (미리 보기)에서 tooset Office 365에 대 한 만료를 그룹화 하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Office 365 그룹 만료 구성(미리 보기)

이제 선택 하는 모든 Office 365 그룹에 대 한 만료를 설정 하 여 Office 365 그룹의 hello 수명 주기를 관리할 수 있습니다. 해당 그룹의 소유자는이 만료 설정 되 고 나면 hello 그룹 해야 할 경우 toorenew 해당 그룹을 요청 합니다. 갱신되지 않은 Office 365 그룹은 삭제됩니다. Hello 그룹 소유자 또는 관리자에 게 30 일 이내 삭제 된 모든 Office 365 그룹을 복원할 수 있습니다.  


> [!NOTE]
> Office 365 그룹에 대해서만 만료를 설정할 수 있습니다.
>
> O365 그룹에 대한 만료 설정에는 할당된 Azure AD Premium 라이선스가 필요합니다.
>   - hello 테 넌 트에 대 한 hello 만료 설정을 구성 하는 hello 관리자
>   - 이 설정에 대해 선택한 hello 그룹의 모든 멤버

## <a name="set-office-365-groups-expiration"></a>Office 365 그룹 만료 설정

1. 열기 hello [Azure AD 관리 센터](https://aad.portal.azure.com) Azure AD 테 넌 트의 전역 관리자 인 계정을 사용 합니다.

2. Azure AD를 열고 **사용자 및 그룹**을 선택합니다.

3. 선택 **그룹 설정** 선택한 후 **만료** tooopen hello 만료 설정 합니다.
  
  ![만료 블레이드](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. Hello에 **만료** 블레이드에서 수행할 수 있습니다.

  * Hello 그룹 수명 (일)에 설정 합니다. 중 하나를 선택할 수 있습니다 (31 일 이상 이어야 함)는 사용자 지정 값 또는 hello 미리 설정 합니다. 
  * Hello 갱신 및 만료 알림 해야를 보낼 수 있는 그룹에 소유자가 없는 경우 전자 메일 주소를 지정 합니다. 
  * 만료되는 Office 365 그룹을 선택합니다. 에 대 한 만료를 사용할 수 **모든** hello Office 365 그룹 중에서 선택 Office 365 그룹을 선택 하거나 **None** 모든 그룹에 대 한 만료를 사용 하지 않도록 설정 하려면.
  * 완료되면 **저장**을 선택하여 설정을 저장합니다.

어떻게 toodownload 및 설치는 PowerShell 통해 Office 365 그룹에 대 한 Microsoft PowerShell 모듈 tooconfigure 만료 hello에 대 한 지침을 참조 하십시오. [Azure Active Directory V2 PowerShell 모듈-공개 미리 보기 릴리스 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137)합니다.

이 이와 같은 전자 메일 알림은 toohello Office 365 그룹 소유자 30 일, 15 일 hello 그룹의 1 일 이전 tooexpiration 전송 됩니다.

![만료 전자 메일 알림](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

hello 그룹 소유자 선택 수 **갱신 그룹** toorenew Office 365 그룹 hello 또는 선택할 수 **toogroup 이동** toosee hello 멤버 및 기타 세부 정보에 대 한 hello 그룹입니다.

그룹에 만료 되 면 hello 그룹이 하루 hello 만료 날짜 이후 삭제 됩니다. 와 같은 전자 메일 알림은 hello 만료 및는 Office 365 그룹의 후속 삭제에 대해 알려주는 toohello Office 365 그룹 소유자 전송 됩니다.

![그룹 삭제 전자 메일 알림](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

hello 그룹을 선택 하 여 복원할 수 있습니다 **복원 그룹** 또는 [Azure Active Directory에서 그룹 삭제 된 Office 365 복원]에 설명 된 대로 PowerShell cmdlet을 사용 하 여 (https://docs.microsoft.com/azure/active-directory/ active-directory-groups-restore-azure-portal).
    
Hello 그룹을 복원 하려는 문서, SharePoint 사이트 또는 다른 영구 개체 있으면 too24 시간 toofully 복원 hello 그룹 및 해당 내용을 걸릴 수도 있습니다.

> [!NOTE]
> * Hello 만료 설정을 배포 하는 경우 hello 만료 기간 보다 오래 된 일부 그룹이 있을 수 있습니다. 이러한 그룹은 즉시 삭제 되지 않는 too30 일 만료 기간을 설정 합니다. 하루 이내 hello 첫 번째 갱신 알림 전자 메일이 전송 됩니다. 예를 들어 그룹 A에는 400 일 전에 만들어진 및 hello 만료 간격 설정 too180 일 수 있습니다. 만료 설정을 적용 하면 그룹 A에 있는 30 일 삭제 하기 전에 hello 소유자를 갱신 하지 않으면 합니다.
> * 동적 그룹 삭제 되 고 복원, 경우에 따라 다시 채워진된 toohello 규칙와 새 그룹으로 표시 됩니다. 이 프로세스는 too24 시간이 걸릴 수 있습니다.

## <a name="next-steps"></a>다음 단계
이러한 문서는 Azure AD 그룹에 대한 추가 정보를 제공합니다.

* [기존 그룹 보기](active-directory-groups-view-azure-portal.md)
* [그룹의 설정 관리](active-directory-groups-settings-azure-portal.md)
* [그룹의 멤버 관리](active-directory-groups-members-azure-portal.md)
* [그룹의 멤버 자격 관리](active-directory-groups-membership-azure-portal.md)
* [그룹의 사용자에 대한 동적 규칙 관리](active-directory-groups-dynamic-membership-azure-portal.md)
