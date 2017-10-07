---
title: "Azure Active Directory의 그룹을 관리 하기 위한 aaaPowerShell 예 | Microsoft Docs"
description: "이 페이지에서는 PowerShell 예제 toohelp Azure Active Directory에서 그룹 관리"
keywords: "Azure AD, Azure Active Directory, PowerShell, 그룹, 그룹 관리"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>그룹 관리를 위한 Azure Active Directory 버전 2 cmdlet
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Azure 클래식 포털](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

이 문서에는 방법의 예가 포함 되어 있습니다. toouse PowerShell toomanage Azure Active Directory (Azure AD)의 그룹입니다.  또한 알 수 hello Azure AD PowerShell 모듈과 함께 tooget을 설정 하는 방법입니다. 먼저 수행 해야 [hello Azure AD PowerShell 모듈을 다운로드](https://www.powershellgallery.com/packages/AzureAD/)합니다.

## <a name="installing-hello-azure-ad-powershell-module"></a>Hello Azure AD PowerShell 모듈 설치
tooinstall hello Azure AD PowerShell 모듈, 다음 명령을 사용 하 여 hello:

    PS C:\Windows\system32> install-module azuread

모듈 hello tooverify 설치 된 다음 명령을 hello를 사용 합니다.

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

이제 hello cmdlet을 사용 하 여 hello 모듈에서 시작할 수 있습니다. 에 대 한 전체 설명은 hello Azure AD 모듈의 hello cmdlet에 대 한 toohello 온라인 참조 설명서를 참조 하십시오 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0)합니다.

## <a name="connecting-toohello-directory"></a>Toohello directory 연결
Azure AD PowerShell cmdlet을 사용 하 여 그룹 관리를 시작 하려면 먼저 원하는 toomanage PowerShell 세션 toohello 디렉터리를 연결 해야 합니다. 다음 명령을 사용 하 여 hello:

    PS C:\Windows\system32> Connect-AzureAD

hello cmdlet 묻는 hello 자격 증명에 대 한 원하는 toouse tooaccess 디렉터리입니다. 이 예제에서 사용 하 여 karen@drumkit.onmicrosoft.com tooaccess hello 데모 디렉터리입니다. hello cmdlet 반환 확인 tooshow hello 세션을 성공적으로 연결 된 tooyour 디렉터리:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

이제 디렉터리에 hello azure Ad cmdlet toomanage 그룹을 사용 하 여 시작할 수 있습니다.

## <a name="retrieving-groups"></a>그룹 검색
에서는 디렉터리에서 기존 그룹 tooretrieve hello Get AzureADGroups cmdlet. 매개 변수 없이 hello cmdlet 사용 하 여 hello 디렉터리에 모든 tooretrieve 그룹:

    PS C:\Windows\system32> get-azureadgroup

hello cmdlet hello 연결 된 디렉터리의 모든 그룹을 반환합니다.

Hello-objectID 매개 변수 tooretrieve를 사용할 수 있습니다 hello 그룹의 objectID를 지정 하는 특정 그룹:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

hello cmdlet은 해당 objectID hello hello 매개 변수 값을 입력 한 일치 하는 hello 그룹을 반환 합니다.

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

사용 하 여 특정 그룹에 대 한 검색할 수 있습니다 hello-filter 매개 변수입니다. 이 매개 변수는 ODATA 필터 절을 사용 하 고 hello 다음 예제와 같이 hello 필터와 일치 하는 모든 그룹을 반환 합니다.

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> azure Ad PowerShell cmdlet hello hello 표준 OData 쿼리를 구현 합니다. 자세한 내용은 참조 **$filter** 에 [hello OData 끝점을 사용 하 여 OData 시스템 쿼리 옵션](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter)합니다.

## <a name="creating-groups"></a>그룹 만들기
toocreate hello 새로 AzureADGroup cmdlet 사용 하 여 디렉터리에 새 그룹입니다. 이 cmdlet을 "Marketing"이라는 새 보안 그룹을 만듭니다.

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>그룹 업데이트
기존 그룹을 tooupdate hello 집합 AzureADGroup cmdlet을 사용 합니다. 이 예제에서는 예에서는 hello hello 그룹 "Intune 관리자 가"의 DisplayName 속성 변경 첫째, hello Get AzureADGroup cmdlet 및 hello / / DisplayName 특성을 사용 하 여 필터를 사용 하 여 hello 그룹을 찾는 했습니다.

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

다음으로,이 예에서는 변경 hello Description 속성 toohello 새 값 "Intune 장치 관리자가":

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

이제 hello 그룹을 다시 찾으려면 보면 hello Description 속성 업데이트 tooreflect hello 새 값:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a>그룹 삭제
디렉터리에서 toodelete 그룹은 다음과 같이 hello 제거 AzureADGroup cmdlet을 사용 합니다.

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>그룹 구성원 관리
새 멤버 tooa 그룹 tooadd 필요한 경우 추가 AzureADGroupMember hello cmdlet을 사용 합니다. 이 명령은 hello 이전 예제에서 사용 멤버 toohello Intune 관리자가 그룹을 추가:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

hello-ObjectId 매개 변수는 hello ObjectID hello 그룹 toowhich의 멤버인 tooadd 고 hello-RefObjectId는 hello ObjectID tooadd 멤버 toohello 그룹으로 원하는 hello 사용자입니다.

다음이 예제와 같이 hello AzureADGroupMember Get cmdlet을 사용 하는 hello tooget 그룹의 기존 구성원:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

tooremove hello 멤버 이전에 추가 되었습니다 toohello 그룹을 사용 하 여 hello 제거 AzureADGroupMember cmdlet은 다음과 같이.

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify hello 그룹 멤버 자격 사용자의 hello 선택 AzureADGroupIdsUserIsMemberOf cmdlet을 사용 합니다. 해당 매개 변수의 hello toocheck hello 그룹 구성원 자격을에 대 한 hello 사용자의 ObjectId로이 cmdlet에서는 어떤 toocheck hello 멤버 자격에 대 한 그룹의 목록과 합니다. hello 그룹 목록이 "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck" 형식의 복합 변수 hello 형태로 하므로 먼저 만들어야 변수 해당 형식으로 제공 해야 합니다.

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

다음으로,이 복잡 한 변수의 "GroupIds" hello 특성에 groupIds toocheck hello에 대 한 값이 제공:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

이제 hello 그룹 $g에 대해 ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea 있는 사용자의 toocheck hello 그룹 멤버 자격을 원하는 경우 사용 해야 합니다.

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


반환 된 hello 값은이 사용자가 멤버인 그룹의 목록. 이 메서드 toocheck 주어진 목록은 선택-AzureADGroupIdsContactIsMemberOf 선택 AzureADGroupIdsGroupIsMemberOf를 사용 하 여 그룹, 연락처, 그룹 또는 서비스 사용자 구성원 자격을 적용할 수 있습니다 또는 AzureADGroupIdsServicePrincipalIsMemberOf 선택

## <a name="managing-owners-of-groups"></a>그룹 소유자 관리
tooadd 소유자 tooa 그룹을 사용 하 여 hello 추가 AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

hello-ObjectId 매개 변수는 hello ObjectID hello 그룹 toowhich의 소유자, tooadd 고 hello-RefObjectId는 hello ObjectID hello 사용자 hello 그룹의 소유자로 tooadd 원하는 합니다.

해당 그룹의 tooretrieve hello 소유자 hello AzureADGroupOwner Get cmdlet을 사용 합니다.

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

hello cmdlet에는 hello 지정 된 그룹에 대 한 소유자의 hello 목록을 반환합니다.

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

그룹에서 소유자 tooremove 원한다 면 hello 제거 AzureADGroupOwner cmdlet을 사용 합니다.

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>예약된 별칭 
그룹을 만들 때 특정 끝점 허용 hello 최종 사용자 toospecify mailNickname 또는 별칭 toobe hello 그룹의 전자 메일 주소 hello의 일환으로 사용 합니다. 만 Azure AD 전역 관리자가 높은 권한이 있는 전자 메일 별칭을 따라 hello로 그룹을 만들 수 있습니다. 
  
* abuse 
* 관리자 
* 관리자 역할 
* hostmaster 
* majordomo 
* postmaster 
* root 
* secure 
* security 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>다음 단계
[Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0)에서 더 많은 Azure Active Directory PowerShell 설명서를 찾을 수 있습니다.

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
