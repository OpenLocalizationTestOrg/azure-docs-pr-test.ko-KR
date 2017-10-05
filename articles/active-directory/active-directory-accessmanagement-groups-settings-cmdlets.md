---
title: "Azure Active Directory cmdlet을 사용하여 그룹 설정 구성 | Microsoft Docs"
description: "Azure Active Directory cmdlet을 사용하여 그룹 설정을 관리하는 방법"
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="cb3d6-103">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="cb3d6-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb3d6-104">이 콘텐츠는 Office 365 그룹에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="cb3d6-105">사용자가 보안 그룹을 만들 수 있도록 하는 방법에 대한 자세한 내용은 [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)에 설명된 대로 `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True`를 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="cb3d6-106">Office 365 그룹 설정은 설정 개체와 SettingsTemplate 개체를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="cb3d6-107">처음에는 디렉터리가 기본 설정으로 구성되어 있으므로 디렉터리에 설정 개체가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="cb3d6-108">기본 설정을 변경하려면 설정 템플릿을 사용하여 새 설정 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="cb3d6-109">설정 템플릿은 Microsoft가 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="cb3d6-110">여러 종류의 설정 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-110">There are several different settings templates.</span></span> <span data-ttu-id="cb3d6-111">디렉터리에 대한 Office 365 그룹 설정을 구성하려면 "Group.Unified" 템플릿을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="cb3d6-112">단일 그룹의 Office 365 그룹 설정을 구성하려면 "Group.Unified.Guest" 템플릿을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="cb3d6-113">이 템플릿은 Office 365 그룹에 대한 게스트 액세스 관리에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="cb3d6-114">cmdlet은 Azure Active Directory PowerShell V2 모듈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="cb3d6-115">컴퓨터에 모듈을 다운로드하여 설치하는 방법에 대한 지침은 [Azure Active Directory PowerShell 버전 2](https://docs.microsoft.com/powershell/azuread/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="cb3d6-116">모듈의 버전 2 릴리스를 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureAD/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="cb3d6-117">특정 설정 값 검색</span><span class="sxs-lookup"><span data-stu-id="cb3d6-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="cb3d6-118">검색할 설정의 이름을 알고 있는 경우 아래 cmdlet을 사용하여 현재 설정 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="cb3d6-119">이 예제에서는 "UsageGuidelinesUrl"이라는 설정의 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="cb3d6-120">향후 이 문서에서 디렉터리 설정 및 해당 이름에 대해 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="cb3d6-121">디렉터리 수준에서 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="cb3d6-121">Create settings at the directory level</span></span>
<span data-ttu-id="cb3d6-122">다음 단계는 디렉터리 수준에서 설정을 만드는 것입니다. 이 설정은 디렉터리에 있는 모든 Office 365 그룹(통합 그룹)에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="cb3d6-123">DirectorySettings cmdlet에서 사용하려는 SettingsTemplate의 ID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="cb3d6-124">이 ID를 모르면 cmdlet이 모든 설정 템플릿 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="cb3d6-125">이 cmdlet을 호출하면 사용할 수 있는 모든 템플릿이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="cb3d6-126">사용 지침 URL을 추가하려면 사용 지침 URL 값을 정의하는 SettingsTemplate 개체를 가져와야 합니다. 즉, Group.Unified 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="cb3d6-127">다음에는 위 템플릿에 기초하여 새 설정 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="cb3d6-128">그런 다음 사용 지침 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="cb3d6-129">마지막으로 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="cb3d6-130">성공적으로 완료되면 cmdlet이 새 설정 개체의 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="cb3d6-131">다음은 Group.Unified 설정 템플릿에서 정의된 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="cb3d6-132">**설정**</span><span class="sxs-lookup"><span data-stu-id="cb3d6-132">**Setting**</span></span> | <span data-ttu-id="cb3d6-133">**설명**</span><span class="sxs-lookup"><span data-stu-id="cb3d6-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="cb3d6-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="cb3d6-134">EnableGroupCreation</span></span><li><span data-ttu-id="cb3d6-135">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb3d6-135">Type: Boolean</span></span><li><span data-ttu-id="cb3d6-136">기본값: True</span><span class="sxs-lookup"><span data-stu-id="cb3d6-136">Default: True</span></span> |<span data-ttu-id="cb3d6-137">디렉터리에서 통합 그룹 만들기가 허용되는지 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="cb3d6-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="cb3d6-139">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-139">Type: String</span></span><li><span data-ttu-id="cb3d6-140">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-140">Default: “”</span></span> |<span data-ttu-id="cb3d6-141">EnableGroupCreation == false일 때도 구성원이 통합 그룹을 만들도록 허용된 보안 그룹의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="cb3d6-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="cb3d6-143">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-143">Type: String</span></span><li><span data-ttu-id="cb3d6-144">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-144">Default: “”</span></span> |<span data-ttu-id="cb3d6-145">그룹 사용 지침 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="cb3d6-146">ClassificationDescriptions</span></span><li><span data-ttu-id="cb3d6-147">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-147">Type: String</span></span><li><span data-ttu-id="cb3d6-148">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-148">Default: “”</span></span> | <span data-ttu-id="cb3d6-149">쉼표로 구분된 분류 설명 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="cb3d6-150">DefaultClassification</span></span><li><span data-ttu-id="cb3d6-151">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-151">Type: String</span></span><li><span data-ttu-id="cb3d6-152">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-152">Default: “”</span></span> | <span data-ttu-id="cb3d6-153">설정이 지정되지 않은 경우에 그룹의 기본 분류로 사용되는 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="cb3d6-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="cb3d6-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="cb3d6-155">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-155">Type: String</span></span><li><span data-ttu-id="cb3d6-156">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-156">Default: “”</span></span> |<span data-ttu-id="cb3d6-157">아직 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="cb3d6-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="cb3d6-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="cb3d6-159">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb3d6-159">Type: Boolean</span></span><li><span data-ttu-id="cb3d6-160">기본값: False</span><span class="sxs-lookup"><span data-stu-id="cb3d6-160">Default: False</span></span> | <span data-ttu-id="cb3d6-161">게스트 사용자가 그룹의 소유자일 수 있는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="cb3d6-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="cb3d6-163">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb3d6-163">Type: Boolean</span></span><li><span data-ttu-id="cb3d6-164">기본값: True</span><span class="sxs-lookup"><span data-stu-id="cb3d6-164">Default: True</span></span> | <span data-ttu-id="cb3d6-165">게스트 사용자가 통합 그룹의 콘텐츠에 액세스할 수 있는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="cb3d6-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="cb3d6-167">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-167">Type: String</span></span><li><span data-ttu-id="cb3d6-168">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-168">Default: “”</span></span> | <span data-ttu-id="cb3d6-169">게스트 사용 지침의 링크 url입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="cb3d6-170">AllowToAddGuests</span></span><li><span data-ttu-id="cb3d6-171">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb3d6-171">Type: Boolean</span></span><li><span data-ttu-id="cb3d6-172">기본값: True</span><span class="sxs-lookup"><span data-stu-id="cb3d6-172">Default: True</span></span> | <span data-ttu-id="cb3d6-173">이 디렉터리에 게스트를 추가하는 것이 허용되는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="cb3d6-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="cb3d6-174">ClassificationList</span></span><li><span data-ttu-id="cb3d6-175">형식: String</span><span class="sxs-lookup"><span data-stu-id="cb3d6-175">Type: String</span></span><li><span data-ttu-id="cb3d6-176">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="cb3d6-176">Default: “”</span></span> |<span data-ttu-id="cb3d6-177">통합 그룹에 적용할 수 있는 유효한 분류 값을 쉼표로 구분한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="cb3d6-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="cb3d6-178">EnableGroupCreation</span></span><li><span data-ttu-id="cb3d6-179">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="cb3d6-179">Type: Boolean</span></span><li><span data-ttu-id="cb3d6-180">기본값: True</span><span class="sxs-lookup"><span data-stu-id="cb3d6-180">Default: True</span></span> | <span data-ttu-id="cb3d6-181">관리자가 아닌 사용자가 새 통합 그룹을 만들 수 있는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="cb3d6-182">디렉터리 수준에서 설정 읽기</span><span class="sxs-lookup"><span data-stu-id="cb3d6-182">Read settings at the directory level</span></span>
<span data-ttu-id="cb3d6-183">다음 단계는 디렉터리 수준에서 설정을 읽는 것입니다. 이 설정은 디렉터리에 있는 모든 Office 그룹에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="cb3d6-184">모든 기존 디렉터리 설정 읽기:</span><span class="sxs-lookup"><span data-stu-id="cb3d6-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="cb3d6-185">이 cmdlet은 모든 디렉터리 설정 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="cb3d6-186">특정 그룹의 모든 설정 읽기:</span><span class="sxs-lookup"><span data-stu-id="cb3d6-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="cb3d6-187">설정 Id GUID를 사용하여 특정 디렉터리 설정 개체의 모든 디렉터리 설정 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="cb3d6-188">이 cmdlet은 이 특정 그룹에 대한 이 설정 개체의 이름과 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="cb3d6-189">특정 그룹의 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="cb3d6-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="cb3d6-190">"Groups.Unified.Guest"라는 설정 템플릿 검색</span><span class="sxs-lookup"><span data-stu-id="cb3d6-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="cb3d6-191">Groups.Unified.Guest 템플릿에 대한 템플릿 개체를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="cb3d6-192">템플릿으로 새로운 설정 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="cb3d6-193">필요한 값의 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="cb3d6-194">디렉터리에 필요한 그룹의 새로운 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="cb3d6-195">디렉터리 수준에서 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="cb3d6-195">Update settings at the directory level</span></span>

<span data-ttu-id="cb3d6-196">다음 단계는 디렉터리 수준에서 설정을 업데이트합니다. 이 설정은 디렉터리에 있는 모든 통합 그룹에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="cb3d6-197">다음 예에서는 이미 디렉터리에 설정 개체가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="cb3d6-198">기존 설정 개체를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="cb3d6-199">값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="cb3d6-200">설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="cb3d6-201">디렉터리 수준에서 설정 제거</span><span class="sxs-lookup"><span data-stu-id="cb3d6-201">Remove settings at the directory level</span></span>
<span data-ttu-id="cb3d6-202">다음 단계는 디렉터리 수준에서 설정을 제거하는 것입니다. 이 설정은 디렉터리에 있는 모든 Office 그룹에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="cb3d6-203">Cmdlet 구문 참조</span><span class="sxs-lookup"><span data-stu-id="cb3d6-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="cb3d6-204">[Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0)에서 더 많은 Azure Active Directory PowerShell 설명서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3d6-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="cb3d6-205">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="cb3d6-205">Additional reading</span></span>

* [<span data-ttu-id="cb3d6-206">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="cb3d6-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="cb3d6-207">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="cb3d6-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
