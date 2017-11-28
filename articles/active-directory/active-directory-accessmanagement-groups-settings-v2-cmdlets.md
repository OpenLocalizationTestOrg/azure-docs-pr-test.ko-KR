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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="ae398-104">그룹 관리를 위한 Azure Active Directory 버전 2 cmdlet</span><span class="sxs-lookup"><span data-stu-id="ae398-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae398-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae398-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="ae398-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="ae398-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="ae398-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae398-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="ae398-108">이 문서에는 방법의 예가 포함 되어 있습니다. toouse PowerShell toomanage Azure Active Directory (Azure AD)의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="ae398-109">또한 알 수 hello Azure AD PowerShell 모듈과 함께 tooget을 설정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="ae398-110">먼저 수행 해야 [hello Azure AD PowerShell 모듈을 다운로드](https://www.powershellgallery.com/packages/AzureAD/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="ae398-111">Hello Azure AD PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="ae398-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="ae398-112">tooinstall hello Azure AD PowerShell 모듈, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="ae398-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="ae398-113">모듈 hello tooverify 설치 된 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="ae398-114">이제 hello cmdlet을 사용 하 여 hello 모듈에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="ae398-115">에 대 한 전체 설명은 hello Azure AD 모듈의 hello cmdlet에 대 한 toohello 온라인 참조 설명서를 참조 하십시오 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="ae398-116">Toohello directory 연결</span><span class="sxs-lookup"><span data-stu-id="ae398-116">Connecting toohello directory</span></span>
<span data-ttu-id="ae398-117">Azure AD PowerShell cmdlet을 사용 하 여 그룹 관리를 시작 하려면 먼저 원하는 toomanage PowerShell 세션 toohello 디렉터리를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="ae398-118">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="ae398-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="ae398-119">hello cmdlet 묻는 hello 자격 증명에 대 한 원하는 toouse tooaccess 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="ae398-120">이 예제에서 사용 하 여 karen@drumkit.onmicrosoft.com tooaccess hello 데모 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="ae398-121">hello cmdlet 반환 확인 tooshow hello 세션을 성공적으로 연결 된 tooyour 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="ae398-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="ae398-122">이제 디렉터리에 hello azure Ad cmdlet toomanage 그룹을 사용 하 여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="ae398-123">그룹 검색</span><span class="sxs-lookup"><span data-stu-id="ae398-123">Retrieving groups</span></span>
<span data-ttu-id="ae398-124">에서는 디렉터리에서 기존 그룹 tooretrieve hello Get AzureADGroups cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae398-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="ae398-125">매개 변수 없이 hello cmdlet 사용 하 여 hello 디렉터리에 모든 tooretrieve 그룹:</span><span class="sxs-lookup"><span data-stu-id="ae398-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="ae398-126">hello cmdlet hello 연결 된 디렉터리의 모든 그룹을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="ae398-127">Hello-objectID 매개 변수 tooretrieve를 사용할 수 있습니다 hello 그룹의 objectID를 지정 하는 특정 그룹:</span><span class="sxs-lookup"><span data-stu-id="ae398-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="ae398-128">hello cmdlet은 해당 objectID hello hello 매개 변수 값을 입력 한 일치 하는 hello 그룹을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="ae398-129">사용 하 여 특정 그룹에 대 한 검색할 수 있습니다 hello-filter 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="ae398-130">이 매개 변수는 ODATA 필터 절을 사용 하 고 hello 다음 예제와 같이 hello 필터와 일치 하는 모든 그룹을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="ae398-131">azure Ad PowerShell cmdlet hello hello 표준 OData 쿼리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="ae398-132">자세한 내용은 참조 **$filter** 에 [hello OData 끝점을 사용 하 여 OData 시스템 쿼리 옵션](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="ae398-133">그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ae398-133">Creating groups</span></span>
<span data-ttu-id="ae398-134">toocreate hello 새로 AzureADGroup cmdlet 사용 하 여 디렉터리에 새 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="ae398-135">이 cmdlet을 "Marketing"이라는 새 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="ae398-136">그룹 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae398-136">Updating groups</span></span>
<span data-ttu-id="ae398-137">기존 그룹을 tooupdate hello 집합 AzureADGroup cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="ae398-138">이 예제에서는 예에서는 hello hello 그룹 "Intune 관리자 가"의 DisplayName 속성 변경</span><span class="sxs-lookup"><span data-stu-id="ae398-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="ae398-139">첫째, hello Get AzureADGroup cmdlet 및 hello / / DisplayName 특성을 사용 하 여 필터를 사용 하 여 hello 그룹을 찾는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="ae398-140">다음으로,이 예에서는 변경 hello Description 속성 toohello 새 값 "Intune 장치 관리자가":</span><span class="sxs-lookup"><span data-stu-id="ae398-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="ae398-141">이제 hello 그룹을 다시 찾으려면 보면 hello Description 속성 업데이트 tooreflect hello 새 값:</span><span class="sxs-lookup"><span data-stu-id="ae398-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="ae398-142">그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="ae398-142">Deleting groups</span></span>
<span data-ttu-id="ae398-143">디렉터리에서 toodelete 그룹은 다음과 같이 hello 제거 AzureADGroup cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="ae398-144">그룹 구성원 관리</span><span class="sxs-lookup"><span data-stu-id="ae398-144">Managing members of groups</span></span>
<span data-ttu-id="ae398-145">새 멤버 tooa 그룹 tooadd 필요한 경우 추가 AzureADGroupMember hello cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="ae398-146">이 명령은 hello 이전 예제에서 사용 멤버 toohello Intune 관리자가 그룹을 추가:</span><span class="sxs-lookup"><span data-stu-id="ae398-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="ae398-147">hello-ObjectId 매개 변수는 hello ObjectID hello 그룹 toowhich의 멤버인 tooadd 고 hello-RefObjectId는 hello ObjectID tooadd 멤버 toohello 그룹으로 원하는 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="ae398-148">다음이 예제와 같이 hello AzureADGroupMember Get cmdlet을 사용 하는 hello tooget 그룹의 기존 구성원:</span><span class="sxs-lookup"><span data-stu-id="ae398-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="ae398-149">tooremove hello 멤버 이전에 추가 되었습니다 toohello 그룹을 사용 하 여 hello 제거 AzureADGroupMember cmdlet은 다음과 같이.</span><span class="sxs-lookup"><span data-stu-id="ae398-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="ae398-150">tooverify hello 그룹 멤버 자격 사용자의 hello 선택 AzureADGroupIdsUserIsMemberOf cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="ae398-151">해당 매개 변수의 hello toocheck hello 그룹 구성원 자격을에 대 한 hello 사용자의 ObjectId로이 cmdlet에서는 어떤 toocheck hello 멤버 자격에 대 한 그룹의 목록과 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="ae398-152">hello 그룹 목록이 "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck" 형식의 복합 변수 hello 형태로 하므로 먼저 만들어야 변수 해당 형식으로 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="ae398-153">다음으로,이 복잡 한 변수의 "GroupIds" hello 특성에 groupIds toocheck hello에 대 한 값이 제공:</span><span class="sxs-lookup"><span data-stu-id="ae398-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="ae398-154">이제 hello 그룹 $g에 대해 ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea 있는 사용자의 toocheck hello 그룹 멤버 자격을 원하는 경우 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="ae398-155">반환 된 hello 값은이 사용자가 멤버인 그룹의 목록.</span><span class="sxs-lookup"><span data-stu-id="ae398-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="ae398-156">이 메서드 toocheck 주어진 목록은 선택-AzureADGroupIdsContactIsMemberOf 선택 AzureADGroupIdsGroupIsMemberOf를 사용 하 여 그룹, 연락처, 그룹 또는 서비스 사용자 구성원 자격을 적용할 수 있습니다 또는 AzureADGroupIdsServicePrincipalIsMemberOf 선택</span><span class="sxs-lookup"><span data-stu-id="ae398-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="ae398-157">그룹 소유자 관리</span><span class="sxs-lookup"><span data-stu-id="ae398-157">Managing owners of groups</span></span>
<span data-ttu-id="ae398-158">tooadd 소유자 tooa 그룹을 사용 하 여 hello 추가 AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ae398-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="ae398-159">hello-ObjectId 매개 변수는 hello ObjectID hello 그룹 toowhich의 소유자, tooadd 고 hello-RefObjectId는 hello ObjectID hello 사용자 hello 그룹의 소유자로 tooadd 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="ae398-160">해당 그룹의 tooretrieve hello 소유자 hello AzureADGroupOwner Get cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="ae398-161">hello cmdlet에는 hello 지정 된 그룹에 대 한 소유자의 hello 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="ae398-162">그룹에서 소유자 tooremove 원한다 면 hello 제거 AzureADGroupOwner cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="ae398-163">예약된 별칭</span><span class="sxs-lookup"><span data-stu-id="ae398-163">Reserved aliases</span></span> 
<span data-ttu-id="ae398-164">그룹을 만들 때 특정 끝점 허용 hello 최종 사용자 toospecify mailNickname 또는 별칭 toobe hello 그룹의 전자 메일 주소 hello의 일환으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="ae398-165">만 Azure AD 전역 관리자가 높은 권한이 있는 전자 메일 별칭을 따라 hello로 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="ae398-166">abuse</span><span class="sxs-lookup"><span data-stu-id="ae398-166">abuse</span></span> 
* <span data-ttu-id="ae398-167">관리자</span><span class="sxs-lookup"><span data-stu-id="ae398-167">admin</span></span> 
* <span data-ttu-id="ae398-168">관리자 역할</span><span class="sxs-lookup"><span data-stu-id="ae398-168">administrator</span></span> 
* <span data-ttu-id="ae398-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="ae398-169">hostmaster</span></span> 
* <span data-ttu-id="ae398-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="ae398-170">majordomo</span></span> 
* <span data-ttu-id="ae398-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="ae398-171">postmaster</span></span> 
* <span data-ttu-id="ae398-172">root</span><span class="sxs-lookup"><span data-stu-id="ae398-172">root</span></span> 
* <span data-ttu-id="ae398-173">secure</span><span class="sxs-lookup"><span data-stu-id="ae398-173">secure</span></span> 
* <span data-ttu-id="ae398-174">security</span><span class="sxs-lookup"><span data-stu-id="ae398-174">security</span></span> 
* <span data-ttu-id="ae398-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="ae398-175">ssl-admin</span></span> 
* <span data-ttu-id="ae398-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="ae398-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ae398-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae398-177">Next steps</span></span>
<span data-ttu-id="ae398-178">[Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0)에서 더 많은 Azure Active Directory PowerShell 설명서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae398-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="ae398-179">Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리</span><span class="sxs-lookup"><span data-stu-id="ae398-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="ae398-180">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="ae398-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
