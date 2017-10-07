---
title: "Azure Active Directory에서 삭제 된 Office 365 aaaRestore 그룹 | Microsoft Docs"
description: "Toorestore 삭제 된 그룹, 보기 복원 가능한 그룹 및 permamnently Azure Active Directory에서 그룹 삭제 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Azure Active Directory에서 삭제된 Office 365 그룹 복원

Hello Azure Active Directory (Azure AD)에 있는 Office 365 그룹을 삭제 하면 삭제 hello 그룹은 유지 하지만 표시 되지 않아야 30 일 동안 hello 삭제 날짜에서. 이 소프트웨어는 필요에 따라 hello 그룹 및 해당 콘텐츠를 복원할 수 있습니다. 이 기능은 제한 된 Azure AD의 그룹을 단독으로 tooOffice 365 합니다. 보안 그룹 및 배포 그룹에는 사용할 수 없습니다.

> [!NOTE] 
> 사용 하지 않는 `Remove-MsolGroup` hello 그룹을 영구적으로 제거 하기 때문에 있습니다. 항상 사용 하 여 `Remove-AzureADMSGroup` toodelete는 O365 그룹입니다. 

hello 권한이 필요 toorestore 그룹 hello 다음 중 하나일 수 있습니다.

역할  | 권한 
--------- | ---------
회사 관리자, 파트너 계층2 지원 및 InTune 서비스 관리자 | 모든 삭제된 Office 365 그룹을 복원할 수 있음 
사용자 계정 관리자 및 파트너 계층1 지원 | 할당 된 해당 toohello 회사 관리자 역할을 제외한 모든 삭제 된 Office 365 그룹을 복원할 수 있습니다. 
사용자 | 소유했던 모든 삭제된 Office 365 그룹을 복원할 수 있음 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>보기 hello toorestore 사용할 수 있는 Office 365 그룹 삭제
에 관심이 스토리 하지 아직 영구적으로 삭제 또는 cmdlet을 다음 hello hello 하나 사용 하는 tooview 삭제 hello 그룹 tooverify를 수 있습니다. 이러한 cmdlet hello의 일부인 [Azure AD PowerShell 모듈이](https://www.powershellgallery.com/packages/AzureAD/)합니다. 이 모듈에 대 한 자세한 내용은 hello에 있습니다 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0) 문서.

1.  모든 cmdlet toodisplay 다음 실행된 hello toorestore 계속 사용할 수 있는 테 넌 트에 Office 365 그룹을 삭제 합니다.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  또는 알고 있는 경우 특정 그룹의 hello objectID (1 단계에서 hello cmdlet에서 가져올 수 있습니다), 삭제 된 특정 그룹 hello cmdlet tooverify 다음 실행된 hello 하지 아직 영구적으로 삭제 되었습니다.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>어떻게 toorestore 삭제 된 Office 365 그룹
그 hello 그룹은 여전히 사용할 수 있는 toorestore를 확인 한 후 복원 hello hello 다음 단계 중 하나가 지정 된 그룹을 삭제 합니다. Hello에 포함 된 문서, SP 사이트 또는 다른 영구 개체는 그룹 및 해당 내용을 too24 시간 toofully 복원을 걸릴 수 있습니다.

1.  실행 hello 다음 cmdlet toorestore hello 그룹 및 해당 내용을 합니다.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

또는 hello 다음 cmdlet 실행할 수 toopermanently 삭제 hello 그룹을 제거 합니다.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>작동되었는지 어떻게 알 수 있습니까?
hello를 실행 하는 Office 365 그룹을 성공적으로 복원 했습니다 tooverify `Get-AzureADGroup –ObjectId <objectId>` hello 그룹에 대 한 cmdlet toodisplay 정보입니다. Hello 복원 후 요청 완료 됩니다.
- hello 그룹 교환에 hello 왼쪽된 탐색 모음에 나타납니다.
- hello 계획 hello 그룹에 대 한 계획에 나타납니다.
- 모든 Sharepoint 사이트와 모든 해당 콘텐츠를 사용할 수 있습니다.
- hello 그룹 hello Exchange 끝점 및 Office 365 그룹을 지 원하는 다른 Office 365 작업 중 하나에서 액세스할 수 있습니다.


## <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory 그룹에 대한 추가 정보를 제공합니다.

* [기존 그룹 보기](active-directory-groups-view-azure-portal.md)
* [그룹의 설정 관리](active-directory-groups-settings-azure-portal.md)
* [그룹의 멤버 관리](active-directory-groups-members-azure-portal.md)
* [그룹의 멤버 자격 관리](active-directory-groups-membership-azure-portal.md)
* [그룹의 사용자에 대한 동적 규칙 관리](active-directory-groups-dynamic-membership-azure-portal.md)
