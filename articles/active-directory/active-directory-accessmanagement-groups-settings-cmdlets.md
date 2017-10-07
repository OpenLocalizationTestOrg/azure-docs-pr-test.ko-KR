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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="5eefe-103">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="5eefe-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5eefe-104">이 콘텐츠는 365 그룹에 tooOffice만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="5eefe-105">방법에 대 한 자세한 내용은 tooallow 사용자 toocreate 보안 그룹을 설정할 `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` 에 설명 된 대로 [Set-msolcompanysettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="5eefe-106">Office 365 그룹 설정은 설정 개체와 SettingsTemplate 개체를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="5eefe-107">처음에 보이지 않으면 설정 개체에 모든 디렉터리의 디렉터리 hello 기본 설정으로 구성 되어 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="5eefe-108">toochange hello 기본 설정을 설정 템플릿을 사용 하 여 새 설정 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="5eefe-109">설정 템플릿은 Microsoft가 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="5eefe-110">여러 종류의 설정 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-110">There are several different settings templates.</span></span> <span data-ttu-id="5eefe-111">"Group.Unified" hello 템플릿이 사용할 tooconfigure Office 365 그룹에 대 한 설정 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="5eefe-112">단일 그룹에 tooconfigure Office 365 그룹 설정 "Group.Unified.Guest" 라는 hello 서식 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="5eefe-113">이 서식 파일은 사용 되는 toomanage 게스트 액세스 tooan Office 365 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="5eefe-114">hello cmdlet은 hello Azure Active Directory PowerShell V2 모듈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="5eefe-115">어떻게 toodownload 및 컴퓨터에 설치 hello 모듈 참조 hello 문서 [Azure Active Directory PowerShell 버전 2](https://docs.microsoft.com/powershell/azuread/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="5eefe-116">hello 모듈의 hello 버전 2 릴리스를 설치할 수 [hello PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureAD/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="5eefe-117">특정 설정 값 검색</span><span class="sxs-lookup"><span data-stu-id="5eefe-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="5eefe-118">hello 이름을 알고 있는 이벤트를 설정 하는 hello 시킬 tooretrieve hello 아래 cmdlet tooretrieve hello 현재 설정 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="5eefe-119">이 예제에서는 "UsageGuidelinesUrl." 라는 설정에 대 한 hello 값을 검색 하는 것</span><span class="sxs-lookup"><span data-stu-id="5eefe-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="5eefe-120">향후 이 문서에서 디렉터리 설정 및 해당 이름에 대해 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="5eefe-121">Hello 디렉터리 수준에서 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="5eefe-121">Create settings at hello directory level</span></span>
<span data-ttu-id="5eefe-122">다음이 단계 설정 만들기 디렉터리 수준에서 tooall hello 디렉터리에 Office 365 그룹 (통합 그룹)를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="5eefe-123">Hello DirectorySettings cmdlet, hello toouse 원하는 SettingsTemplate의 hello ID를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="5eefe-124">이 ID를 모르는 경우이 cmdlet에는 모든 설정 템플릿의 hello 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="5eefe-125">이 cmdlet을 호출하면 사용할 수 있는 모든 템플릿이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-125">This cmdlet call returns all templates that are available:</span></span>
  
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
2. <span data-ttu-id="5eefe-126">사용 지침 URL tooadd 먼저 hello 사용 지침 URL 값; 정의 하는 tooget hello SettingsTemplate 개체 즉, hello Group.Unified 템플릿:</span><span class="sxs-lookup"><span data-stu-id="5eefe-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="5eefe-127">다음에는 위 템플릿에 기초하여 새 설정 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="5eefe-128">그런 다음 hello 사용 지침 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="5eefe-129">마지막으로 hello 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="5eefe-130">성공적으로 완료 되 면 hello cmdlet hello 새 설정 개체의 hello ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="5eefe-131">다음은 Group.Unified SettingsTemplate hello에 정의 된 hello 설정을입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="5eefe-132">**설정**</span><span class="sxs-lookup"><span data-stu-id="5eefe-132">**Setting**</span></span> | <span data-ttu-id="5eefe-133">**설명**</span><span class="sxs-lookup"><span data-stu-id="5eefe-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="5eefe-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="5eefe-134">EnableGroupCreation</span></span><li><span data-ttu-id="5eefe-135">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="5eefe-135">Type: Boolean</span></span><li><span data-ttu-id="5eefe-136">기본값: True</span><span class="sxs-lookup"><span data-stu-id="5eefe-136">Default: True</span></span> |<span data-ttu-id="5eefe-137">hello 디렉터리에 통합 그룹 만들기가 허용 되는지 여부를 나타내는 hello 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="5eefe-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="5eefe-139">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-139">Type: String</span></span><li><span data-ttu-id="5eefe-140">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-140">Default: “”</span></span> |<span data-ttu-id="5eefe-141">경우에 멤버는 toocreate 통합 그룹을 허용 하는 데는 hello에 대 한 hello 보안 그룹의 GUID EnableGroupCreation = = false.</span><span class="sxs-lookup"><span data-stu-id="5eefe-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="5eefe-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="5eefe-143">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-143">Type: String</span></span><li><span data-ttu-id="5eefe-144">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-144">Default: “”</span></span> |<span data-ttu-id="5eefe-145">링크 toohello 그룹 사용 지침</span><span class="sxs-lookup"><span data-stu-id="5eefe-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="5eefe-146">ClassificationDescriptions</span></span><li><span data-ttu-id="5eefe-147">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-147">Type: String</span></span><li><span data-ttu-id="5eefe-148">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-148">Default: “”</span></span> | <span data-ttu-id="5eefe-149">쉼표로 구분된 분류 설명 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="5eefe-150">DefaultClassification</span></span><li><span data-ttu-id="5eefe-151">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-151">Type: String</span></span><li><span data-ttu-id="5eefe-152">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-152">Default: “”</span></span> | <span data-ttu-id="5eefe-153">toobe에 지정 된 경우 그룹에 대 한 기본 분류 hello로 사용 되는 hello 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="5eefe-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="5eefe-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="5eefe-155">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-155">Type: String</span></span><li><span data-ttu-id="5eefe-156">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-156">Default: “”</span></span> |<span data-ttu-id="5eefe-157">아직 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="5eefe-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="5eefe-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="5eefe-159">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="5eefe-159">Type: Boolean</span></span><li><span data-ttu-id="5eefe-160">기본값: False</span><span class="sxs-lookup"><span data-stu-id="5eefe-160">Default: False</span></span> | <span data-ttu-id="5eefe-161">게스트 사용자가 그룹의 소유자일 수 있는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="5eefe-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="5eefe-163">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="5eefe-163">Type: Boolean</span></span><li><span data-ttu-id="5eefe-164">기본값: True</span><span class="sxs-lookup"><span data-stu-id="5eefe-164">Default: True</span></span> | <span data-ttu-id="5eefe-165">게스트 사용자 액세스 tooUnified 그룹 콘텐츠를 가질 수 있는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="5eefe-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="5eefe-167">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-167">Type: String</span></span><li><span data-ttu-id="5eefe-168">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-168">Default: “”</span></span> | <span data-ttu-id="5eefe-169">링크 toohello 게스트 사용 지침의 hello url입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="5eefe-170">AllowToAddGuests</span></span><li><span data-ttu-id="5eefe-171">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="5eefe-171">Type: Boolean</span></span><li><span data-ttu-id="5eefe-172">기본값: True</span><span class="sxs-lookup"><span data-stu-id="5eefe-172">Default: True</span></span> | <span data-ttu-id="5eefe-173">허용 된 tooadd 게스트 toothis 디렉터리 인지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="5eefe-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="5eefe-174">ClassificationList</span></span><li><span data-ttu-id="5eefe-175">형식: String</span><span class="sxs-lookup"><span data-stu-id="5eefe-175">Type: String</span></span><li><span data-ttu-id="5eefe-176">기본값: “”</span><span class="sxs-lookup"><span data-stu-id="5eefe-176">Default: “”</span></span> |<span data-ttu-id="5eefe-177">적용 된 tooUnified 그룹 일 수 있는 유효한 분류 값을 쉼표로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="5eefe-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="5eefe-178">EnableGroupCreation</span></span><li><span data-ttu-id="5eefe-179">형식: Boolean</span><span class="sxs-lookup"><span data-stu-id="5eefe-179">Type: Boolean</span></span><li><span data-ttu-id="5eefe-180">기본값: True</span><span class="sxs-lookup"><span data-stu-id="5eefe-180">Default: True</span></span> | <span data-ttu-id="5eefe-181">관리자가 아닌 사용자가 새 통합 그룹을 만들 수 있는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="5eefe-182">Hello 디렉터리 수준에서 설정 읽기</span><span class="sxs-lookup"><span data-stu-id="5eefe-182">Read settings at hello directory level</span></span>
<span data-ttu-id="5eefe-183">다음이 단계 읽기 tooall Office 그룹 hello 디렉터리에 적용 되는 디렉터리 수준에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="5eefe-184">모든 기존 디렉터리 설정 읽기:</span><span class="sxs-lookup"><span data-stu-id="5eefe-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="5eefe-185">이 cmdlet은 모든 디렉터리 설정 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="5eefe-186">특정 그룹의 모든 설정 읽기:</span><span class="sxs-lookup"><span data-stu-id="5eefe-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="5eefe-187">설정 Id GUID를 사용하여 특정 디렉터리 설정 개체의 모든 디렉터리 설정 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="5eefe-188">이 cmdlet이 특정 그룹에 대 한이 설정 개체에 hello 이름 및 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="5eefe-189">특정 그룹의 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="5eefe-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="5eefe-190">"Groups.Unified.Guest" 라는 hello 설정 서식 파일을 검색</span><span class="sxs-lookup"><span data-stu-id="5eefe-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="5eefe-191">Hello Groups.Unified.Guest 템플릿에 대 한 hello 템플릿 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="5eefe-192">Hello 템플릿에서 새 설정 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="5eefe-193">Hello 설정 toohello 필요한 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="5eefe-194">Hello 디렉터리에 hello hello 필수 그룹에 대 한 새 설정 만들기:</span><span class="sxs-lookup"><span data-stu-id="5eefe-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="5eefe-195">Hello 디렉터리 수준에서 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="5eefe-195">Update settings at hello directory level</span></span>

<span data-ttu-id="5eefe-196">다음이 단계에는 tooall 통합 그룹 hello 디렉터리에 적용 되는 디렉터리 수준에서 설정을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="5eefe-197">다음 예에서는 이미 디렉터리에 설정 개체가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="5eefe-198">Hello 기존 설정 개체를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="5eefe-199">Hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="5eefe-200">Hello 설정을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="5eefe-201">Hello 디렉터리 수준에서 설정 제거</span><span class="sxs-lookup"><span data-stu-id="5eefe-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="5eefe-202">이 단계는 tooall Office 그룹 hello 디렉터리에 적용 되는 디렉터리 수준에서 설정을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="5eefe-203">Cmdlet 구문 참조</span><span class="sxs-lookup"><span data-stu-id="5eefe-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="5eefe-204">[Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0)에서 더 많은 Azure Active Directory PowerShell 설명서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eefe-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="5eefe-205">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="5eefe-205">Additional reading</span></span>

* [<span data-ttu-id="5eefe-206">Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리</span><span class="sxs-lookup"><span data-stu-id="5eefe-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="5eefe-207">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="5eefe-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
