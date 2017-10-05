---
title: "Azure Active Directory에서 그룹 관리를 위한 PowerShell 예제 | Microsoft Docs"
description: "이 페이지에는 Azure Active Directory에서 그룹을 관리하는 데 도움이 되는 PowerShell 예제가 나와 있습니다."
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
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="6f3a0-104">그룹 관리를 위한 Azure Active Directory 버전 2 cmdlet</span><span class="sxs-lookup"><span data-stu-id="6f3a0-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f3a0-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6f3a0-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="6f3a0-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="6f3a0-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="6f3a0-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f3a0-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="6f3a0-108">이 문서에서는 Azure AD(Azure Active Directory)에서 PowerShell을 사용하여 그룹을 관리하는 방법의 예제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="6f3a0-109">또한 Azure AD PowerShell 모듈을 사용하여 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="6f3a0-110">먼저 [Azure AD PowerShell 모듈을 다운로드](https://www.powershellgallery.com/packages/AzureAD/)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="6f3a0-111">Azure AD PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="6f3a0-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="6f3a0-112">Azure AD PowerShell 모듈을 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="6f3a0-113">모듈이 설치되어 있는지 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="6f3a0-114">이제 모듈에서 cmdlet 사용을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="6f3a0-115">Azure AD 모듈의 cmdlet에 대한 자세한 내용은 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0)에 대한 온라인 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="6f3a0-116">디렉터리에 연결</span><span class="sxs-lookup"><span data-stu-id="6f3a0-116">Connecting to the directory</span></span>
<span data-ttu-id="6f3a0-117">Azure AD PowerShell cmdlet을 사용하여 그룹 관리를 시작하기 전에 PowerShell 세션을 관리하려는 디렉터리에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="6f3a0-118">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="6f3a0-119">이 cmdlet은 디렉터리에 액세스하는 데 사용할 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="6f3a0-120">이 예제에서는 karen@drumkit.onmicrosoft.com 을 사용하여 데모 디렉터리에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="6f3a0-121">이 cmdlet은 세션이 디렉터리에 정상적으로 연결되었음을 표시하기 위한 확인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="6f3a0-122">이제 Azure AD cmdlet을 사용하여 디렉터리에서 그룹 관리를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="6f3a0-123">그룹 검색</span><span class="sxs-lookup"><span data-stu-id="6f3a0-123">Retrieving groups</span></span>
<span data-ttu-id="6f3a0-124">디렉터리에서 기존 그룹을 검색하려면 Get-AzureADGroups cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="6f3a0-125">디렉터리의 모든 그룹을 검색하려면 매개 변수 없이 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="6f3a0-126">이 cmdlet은 연결된 디렉터리의 모든 그룹을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="6f3a0-127">-objectID 매개 변수를 사용하여 그룹의 objectID를 지정하는 특정 그룹을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="6f3a0-128">이제 이 cmdlet은 해당 objectID가 사용자가 입력한 매개 변수의 값과 일치하는 그룹을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

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

<span data-ttu-id="6f3a0-129">-filter 매개 변수를 사용하여 특정 그룹을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="6f3a0-130">이 매개 변수는 다음 예제와 같이 ODATA 필터 절을 사용하고 필터와 일치하는 모든 그룹을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

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
> <span data-ttu-id="6f3a0-131">AzureAD PowerShell cmdlet에서는 OData 쿼리 표준을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="6f3a0-132">자세한 내용은 [OData 끝점을 사용하는 OData 시스템 쿼리 옵션](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter)의 **$filter**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="6f3a0-133">그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6f3a0-133">Creating groups</span></span>
<span data-ttu-id="6f3a0-134">디렉터리에 새 그룹을 만들려면 New-AzureADGroup cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="6f3a0-135">이 cmdlet을 "Marketing"이라는 새 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="6f3a0-136">그룹 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f3a0-136">Updating groups</span></span>
<span data-ttu-id="6f3a0-137">기존 그룹을 업데이트하려면 Set-AzureADGroup cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="6f3a0-138">이 예제에서는 그룹 “Intune Administrators”의 DisplayName 속성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="6f3a0-139">먼저 Get-AzureADGroup cmdlet을 사용하여 그룹을 찾고 DisplayName 특성을 사용하여 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

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

<span data-ttu-id="6f3a0-140">다음으로 Description 속성을 새 값인 “Intune 장치 관리자”로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="6f3a0-141">이제 해당 그룹을 다시 찾으면 새 값을 반영하도록 Description 속성이 업데이트된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="6f3a0-142">그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="6f3a0-142">Deleting groups</span></span>
<span data-ttu-id="6f3a0-143">디렉터리에서 그룹을 삭제하려면 다음과 같이 Remove-AzureADGroup cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="6f3a0-144">그룹 구성원 관리</span><span class="sxs-lookup"><span data-stu-id="6f3a0-144">Managing members of groups</span></span>
<span data-ttu-id="6f3a0-145">그룹에 새 구성원을 추가해야 하는 경우 Add-AzureADGroupMember cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="6f3a0-146">이 명령을 수행하면 이전 예제에서 사용한 Intune 관리자 그룹에 구성원이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="6f3a0-147">-ObjectId 매개 변수는 구성원을 추가하려는 그룹의 ObjectID이며, -RefObjectId는 그룹에 구성원으로 추가하려는 사용자의 ObjectID입니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="6f3a0-148">그룹의 기존 구성원을 가져오려면 다음 예제와 같이 Get-AzureADGroupMember cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="6f3a0-149">이전에 추가한 그룹에 구성원을 제거하려면 다음과 같이 Remove-AzureADGroupMember cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="6f3a0-150">사용자의 그룹 구성원 자격을 확인하려면 Select-AzureADGroupIdsUserIsMemberOf cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="6f3a0-151">이 cmdlet은 구성원 자격을 확인할 사용자의 ObjectId와 구성원 자격을 확인하려는 그룹의 목록을 해당 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="6f3a0-152">그룹 목록은 "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck" 형식의 복잡한 변수 형태로 제공되므로 먼저 해당 형식의 변수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="6f3a0-153">다음으로 다음 복합 변수의 "GroupIds" 특성에 확인할 groupId 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="6f3a0-154">이제 $g의 그룹에 대해 ObjectID가 72cd4bbd-2594-40a2-935c-016f3cfeeeea인 사용자의 그룹 구성원 자격을 확인하려는 경우 다음을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="6f3a0-155">반환되는 값은 이 사용자가 구성원인 그룹의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="6f3a0-156">또한 Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf 또는 Select-AzureADGroupIdsServicePrincipalIsMemberOf를 사용하여 지정된 그룹 목록에 대해 연락처, 그룹 또는 서비스 주체 구성원 자격을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="6f3a0-157">그룹 소유자 관리</span><span class="sxs-lookup"><span data-stu-id="6f3a0-157">Managing owners of groups</span></span>
<span data-ttu-id="6f3a0-158">그룹에 소유자를 추가하려면 Add-AzureADGroupOwner cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="6f3a0-159">-ObjectId 매개 변수는 소유자를 추가하려는 그룹의 ObjectID이며, -RefObjectId는 그룹에 소유자로 추가하려는 사용자의 ObjectID입니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="6f3a0-160">그룹의 소유자를 검색하려면 Get-AzureADGroupOwner cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="6f3a0-161">이 cmdlet을 실행하면 지정된 그룹에 대한 소유자 목록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="6f3a0-162">그룹에서 소유자를 제거하려면 Remove-AzureADGroupOwner cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="6f3a0-163">예약된 별칭</span><span class="sxs-lookup"><span data-stu-id="6f3a0-163">Reserved aliases</span></span> 
<span data-ttu-id="6f3a0-164">그룹을 만들 때 특정 끝점은 최종 사용자가 mailNickname 또는 별칭이 그룹의 전자 메일 주소의 일부로 사용되도록 지정할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="6f3a0-165">다음과 같은 높은 권한이 있는 전자 메일 별칭이 있는 그룹은 Azure AD 전역 관리자만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="6f3a0-166">abuse</span><span class="sxs-lookup"><span data-stu-id="6f3a0-166">abuse</span></span> 
* <span data-ttu-id="6f3a0-167">관리자</span><span class="sxs-lookup"><span data-stu-id="6f3a0-167">admin</span></span> 
* <span data-ttu-id="6f3a0-168">관리자 역할</span><span class="sxs-lookup"><span data-stu-id="6f3a0-168">administrator</span></span> 
* <span data-ttu-id="6f3a0-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="6f3a0-169">hostmaster</span></span> 
* <span data-ttu-id="6f3a0-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="6f3a0-170">majordomo</span></span> 
* <span data-ttu-id="6f3a0-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="6f3a0-171">postmaster</span></span> 
* <span data-ttu-id="6f3a0-172">root</span><span class="sxs-lookup"><span data-stu-id="6f3a0-172">root</span></span> 
* <span data-ttu-id="6f3a0-173">secure</span><span class="sxs-lookup"><span data-stu-id="6f3a0-173">secure</span></span> 
* <span data-ttu-id="6f3a0-174">security</span><span class="sxs-lookup"><span data-stu-id="6f3a0-174">security</span></span> 
* <span data-ttu-id="6f3a0-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="6f3a0-175">ssl-admin</span></span> 
* <span data-ttu-id="6f3a0-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="6f3a0-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6f3a0-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f3a0-177">Next steps</span></span>
<span data-ttu-id="6f3a0-178">[Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0)에서 더 많은 Azure Active Directory PowerShell 설명서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f3a0-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="6f3a0-179">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="6f3a0-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="6f3a0-180">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="6f3a0-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
