---
title: "Azure Active Directory cmdlet을 사용 하 여 aaaConfigure 그룹 설정을 | Microsoft Docs"
description: "Azure Active Directory cmdlet을 사용 하 여 그룹에 대 한 hello 설정을 어떻게 관리"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>그룹 설정을 구성하는 Azure Active Directory cmdlets

> [!IMPORTANT]
> 이 콘텐츠는 365 그룹에 tooOffice만 적용 됩니다. 방법에 대 한 자세한 내용은 tooallow 사용자 toocreate 보안 그룹을 설정할 `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` 에 설명 된 대로 [Set-msolcompanysettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)합니다. 

Office 365 그룹 설정은 설정 개체와 SettingsTemplate 개체를 사용하여 구성됩니다. 처음에 보이지 않으면 설정 개체에 모든 디렉터리의 디렉터리 hello 기본 설정으로 구성 되어 있으므로 합니다. toochange hello 기본 설정을 설정 템플릿을 사용 하 여 새 설정 개체를 만들어야 합니다. 설정 템플릿은 Microsoft가 정의합니다. 여러 종류의 설정 템플릿이 있습니다. "Group.Unified" hello 템플릿이 사용할 tooconfigure Office 365 그룹에 대 한 설정 디렉터리에 있습니다. 단일 그룹에 tooconfigure Office 365 그룹 설정 "Group.Unified.Guest" 라는 hello 서식 파일을 사용 합니다. 이 서식 파일은 사용 되는 toomanage 게스트 액세스 tooan Office 365 그룹입니다. 

hello cmdlet은 hello Azure Active Directory PowerShell V2 모듈의 일부입니다. 어떻게 toodownload 및 컴퓨터에 설치 hello 모듈 참조 hello 문서 [Azure Active Directory PowerShell 버전 2](https://docs.microsoft.com/powershell/azuread/)합니다. hello 모듈의 hello 버전 2 릴리스를 설치할 수 [hello PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureAD/)합니다.

## <a name="retrieve-a-specific-settings-value"></a>특정 설정 값 검색
hello 이름을 알고 있는 이벤트를 설정 하는 hello 시킬 tooretrieve hello 아래 cmdlet tooretrieve hello 현재 설정 값을 사용할 수 있습니다. 이 예제에서는 "UsageGuidelinesUrl." 라는 설정에 대 한 hello 값을 검색 하는 것 향후 이 문서에서 디렉터리 설정 및 해당 이름에 대해 자세히 살펴볼 수 있습니다.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Hello 디렉터리 수준에서 설정 만들기
다음이 단계 설정 만들기 디렉터리 수준에서 tooall hello 디렉터리에 Office 365 그룹 (통합 그룹)를 적용 합니다.

1. Hello DirectorySettings cmdlet, hello toouse 원하는 SettingsTemplate의 hello ID를 지정 해야 합니다. 이 ID를 모르는 경우이 cmdlet에는 모든 설정 템플릿의 hello 목록을 반환 합니다.
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  이 cmdlet을 호출하면 사용할 수 있는 모든 템플릿이 반환됩니다.
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. 사용 지침 URL tooadd 먼저 hello 사용 지침 URL 값; 정의 하는 tooget hello SettingsTemplate 개체 즉, hello Group.Unified 템플릿:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. 다음에는 위 템플릿에 기초하여 새 설정 개체를 만듭니다.
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. 그런 다음 hello 사용 지침 값을 업데이트 합니다.
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. 마지막으로 hello 설정을 적용 합니다.
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

성공적으로 완료 되 면 hello cmdlet hello 새 설정 개체의 hello ID를 반환합니다.
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
다음은 Group.Unified SettingsTemplate hello에 정의 된 hello 설정을입니다.

| **설정** | **설명** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>형식: Boolean<li>기본값: True |hello 디렉터리에 통합 그룹 만들기가 허용 되는지 여부를 나타내는 hello 플래그입니다. |
|  <ul><li>GroupCreationAllowedGroupId<li>형식: String<li>기본값: “” |경우에 멤버는 toocreate 통합 그룹을 허용 하는 데는 hello에 대 한 hello 보안 그룹의 GUID EnableGroupCreation = = false. |
|  <ul><li>UsageGuidelinesUrl<li>형식: String<li>기본값: “” |링크 toohello 그룹 사용 지침 |
|  <ul><li>ClassificationDescriptions<li>형식: String<li>기본값: “” | 쉼표로 구분된 분류 설명 목록입니다. |
|  <ul><li>DefaultClassification<li>형식: String<li>기본값: “” | toobe에 지정 된 경우 그룹에 대 한 기본 분류 hello로 사용 되는 hello 분류 합니다.|
|  <ul><li>PrefixSuffixNamingRequirement<li>형식: String<li>기본값: “” |아직 구현되지 않았습니다.
|  <ul><li>AllowGuestsToBeGroupOwner<li>형식: Boolean<li>기본값: False | 게스트 사용자가 그룹의 소유자일 수 있는지 여부를 나타내는 부울 값입니다. |
|  <ul><li>AllowGuestsToAccessGroups<li>형식: Boolean<li>기본값: True | 게스트 사용자 액세스 tooUnified 그룹 콘텐츠를 가질 수 있는지 여부를 나타내는 부울입니다. |
|  <ul><li>GuestUsageGuidelinesUrl<li>형식: String<li>기본값: “” | 링크 toohello 게스트 사용 지침의 hello url입니다. |
|  <ul><li>AllowToAddGuests<li>형식: Boolean<li>기본값: True | 허용 된 tooadd 게스트 toothis 디렉터리 인지 여부를 나타내는 부울 값입니다.|
|  <ul><li>ClassificationList<li>형식: String<li>기본값: “” |적용 된 tooUnified 그룹 일 수 있는 유효한 분류 값을 쉼표로 구분 된 목록입니다. |
|  <ul><li>EnableGroupCreation<li>형식: Boolean<li>기본값: True | 관리자가 아닌 사용자가 새 통합 그룹을 만들 수 있는지 여부를 나타내는 부울 값입니다. |


## <a name="read-settings-at-hello-directory-level"></a>Hello 디렉터리 수준에서 설정 읽기
다음이 단계 읽기 tooall Office 그룹 hello 디렉터리에 적용 되는 디렉터리 수준에서 설정 합니다.

1. 모든 기존 디렉터리 설정 읽기:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  이 cmdlet은 모든 디렉터리 설정 목록을 반환합니다.
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. 특정 그룹의 모든 설정 읽기:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. 설정 Id GUID를 사용하여 특정 디렉터리 설정 개체의 모든 디렉터리 설정 값을 읽습니다.
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  이 cmdlet이 특정 그룹에 대 한이 설정 개체에 hello 이름 및 값을 반환합니다.
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a>특정 그룹의 설정 업데이트

1. "Groups.Unified.Guest" 라는 hello 설정 서식 파일을 검색
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. Hello Groups.Unified.Guest 템플릿에 대 한 hello 템플릿 개체를 검색 합니다.
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Hello 템플릿에서 새 설정 개체를 만듭니다.
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Hello 설정 toohello 필요한 값을 설정 합니다.
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Hello 디렉터리에 hello hello 필수 그룹에 대 한 새 설정 만들기:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Hello 디렉터리 수준에서 설정 업데이트

다음이 단계에는 tooall 통합 그룹 hello 디렉터리에 적용 되는 디렉터리 수준에서 설정을 업데이트 합니다. 다음 예에서는 이미 디렉터리에 설정 개체가 있는 것으로 가정합니다.

1. Hello 기존 설정 개체를 찾습니다.
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Hello 값을 업데이트 합니다.
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Hello 설정을 업데이트 합니다.
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Hello 디렉터리 수준에서 설정 제거
이 단계는 tooall Office 그룹 hello 디렉터리에 적용 되는 디렉터리 수준에서 설정을 제거 합니다.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Cmdlet 구문 참조
[Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0)에서 더 많은 Azure Active Directory PowerShell 설명서를 찾을 수 있습니다.

## <a name="additional-reading"></a>추가 참조 자료

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
