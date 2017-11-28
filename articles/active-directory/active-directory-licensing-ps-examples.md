---
title: "Azure AD에서 라이선스 그룹 기반 aaaPowerShell 예 | Microsoft Docs"
description: "Azure Active Directory 그룹 기반 라이선스에 대한 PowerShell 시나리오"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.openlocfilehash: 31eeab0a34c35e80849a4cd11f5447a30b7c04be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-examples-for-group-based-licensing-in-azure-ad"></a><span data-ttu-id="2db08-104">Azure AD의 그룹 기반 라이선스에 대한 PowerShell 예제</span><span class="sxs-lookup"><span data-stu-id="2db08-104">PowerShell examples for group-based licensing in Azure AD</span></span>

<span data-ttu-id="2db08-105">그룹 기반 라이선스에 대 한 전체 기능은 hello를 통해 사용할 수 [Azure 포털](https://portal.azure.com), 현재 PowerShell 지원이 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-105">Full functionality for group-based licensing is available through hello [Azure portal](https://portal.azure.com), and currently PowerShell support is limited.</span></span> <span data-ttu-id="2db08-106">그러나 몇 가지 유용한 작업 기존 hello를 사용 하 여 수행할 수 있는 [MSOnline PowerShell cmdlet](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory)합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-106">However, there are some useful tasks that can be performed using hello existing [MSOnline PowerShell cmdlets](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory).</span></span> <span data-ttu-id="2db08-107">이 문서는 가능한 작업에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-107">This document provides examples of what is possible.</span></span>

> [!NOTE]
> <span data-ttu-id="2db08-108">Cmdlet을 실행을 시작 하기 전에 hello를 실행 하 여 먼저 tooyour 테 넌 트를 연결 했는지 확인 `Connect-MsolService` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2db08-108">Before you begin running cmdlets, make sure you connect tooyour tenant first, by running hello `Connect-MsolService` cmdlet.</span></span>

## <a name="view-product-licenses-assigned-tooa-group"></a><span data-ttu-id="2db08-109">제품 라이선스 tooa 할당 된 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="2db08-109">View product licenses assigned tooa group</span></span>
<span data-ttu-id="2db08-110">[Get-msolgroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) cmdlet 사용된 tooretrieve hello 그룹 개체 수 있고 hello 확인 *라이선스* 속성: 현재 toohello 그룹을 할당 하는 모든 제품 라이선스를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-110">The [Get-MsolGroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) cmdlet can be used tooretrieve hello group object and check hello *Licenses* property: it lists all product licenses currently assigned toohello group.</span></span>
```
(Get-MsolGroup -ObjectId 99c4216a-56de-42c4-a4ac-e411cd8c7c41).Licenses
| Select SkuPartNumber
```
<span data-ttu-id="2db08-111">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-111">Output:</span></span>
```
SkuPartNumber
-------------
ENTERPRISEPREMIUM
EMSPREMIUM
```

> [!NOTE]
> <span data-ttu-id="2db08-112">hello 데이터는 제한 된 tooproduct (SKU) 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-112">hello data is limited tooproduct (SKU) information.</span></span> <span data-ttu-id="2db08-113">가능한 toolist hello 서비스 계획 hello 라이선스에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-113">It is not possible toolist hello service plans disabled in hello license.</span></span>

## <a name="get-all-groups-with-licenses"></a><span data-ttu-id="2db08-114">라이선스가 있는 모든 그룹 가져오기</span><span class="sxs-lookup"><span data-stu-id="2db08-114">Get all groups with licenses</span></span>

<span data-ttu-id="2db08-115">Hello 다음 명령을 실행 하 여 할당 된 라이선스가 있는 모든 그룹을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-115">You can find all groups with any license assigned by running hello following command:</span></span>
```
Get-MsolGroup | Where {$_.Licenses}
```
<span data-ttu-id="2db08-116">어떤 제품이 할당되어 있는지에 대해 자세한 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-116">More details can be displayed about what products are assigned:</span></span>
```
Get-MsolGroup | Where {$_.Licenses} | Select `
    ObjectId, `
    DisplayName, `
    @{Name="Licenses";Expression={$_.Licenses | Select -ExpandProperty SkuPartNumber}}
```

<span data-ttu-id="2db08-117">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-117">Output:</span></span>
```
ObjectId                             DisplayName              Licenses
--------                             -----------              --------
7023a314-6148-4d7b-b33f-6c775572879a EMS E5 – Licensed users  EMSPREMIUM
cf41f428-3b45-490b-b69f-a349c8a4c38e PowerBi - Licensed users POWER\_BI\_STANDARD
962f7189-59d9-4a29-983f-556ae56f19a5 O365 E3 - Licensed users ENTERPRISEPACK
c2652d63-9161-439b-b74e-fcd8228a7074 EMSandOffice             {ENTERPRISEPREMIUM,EMSPREMIUM}
```

## <a name="get-statistics-for-groups-with-licenses"></a><span data-ttu-id="2db08-118">라이선스가 있는 그룹에 대한 통계 가져오기</span><span class="sxs-lookup"><span data-stu-id="2db08-118">Get statistics for groups with licenses</span></span>
<span data-ttu-id="2db08-119">라이선스가 있는 그룹에 대해 기본적인 통계를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-119">You can report basic statistics for groups with licenses.</span></span> <span data-ttu-id="2db08-120">아래의 hello 예에서 hello 총 사용자 수, hello hello 그룹 및 사용자에 라이선스를 할당할 수 없습니다 hello 그룹별로 hello 수에서 이미 할당 된 라이선스는 사용자 개수 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-120">In hello example below we list hello total user count, hello count of users with licenses already assigned by hello group, and hello count of users for whom licenses could not be assigned by hello group.</span></span>

```
#get all groups with licenses
Get-MsolGroup -All | Where {$_.Licenses}  | Foreach {
    $groupId = $_.ObjectId;
    $groupName = $_.DisplayName;
    $groupLicenses = $_.Licenses | Select -ExpandProperty SkuPartNumber
    $totalCount = 0;
    $licenseAssignedCount = 0;
    $licenseErrorCount = 0;

    Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in hello group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $totalCount++

        #check if any licenses are assigned via this group
        if($user.Licenses | ? {$_.GroupsAssigningLicense -ieq $groupId })
        {
            $licenseAssignedCount++
        }
        #check if user has any licenses that failed toobe assigned from this group
        if ($user.IndirectLicenseErrors | ? {$_.ReferencedObjectId -ieq $groupId })
        {
            $licenseErrorCount++
        }     
    }

    #aggregate results for this group
    New-Object Object |
                    Add-Member -NotePropertyName GroupName -NotePropertyValue $groupName -PassThru |
                    Add-Member -NotePropertyName GroupId -NotePropertyValue $groupId -PassThru |
                    Add-Member -NotePropertyName GroupLicenses -NotePropertyValue $groupLicenses -PassThru |
                    Add-Member -NotePropertyName TotalUserCount -NotePropertyValue $totalCount -PassThru |
                    Add-Member -NotePropertyName LicensedUserCount -NotePropertyValue $licenseAssignedCount -PassThru |
                    Add-Member -NotePropertyName LicenseErrorCount -NotePropertyValue $licenseErrorCount -PassThru

    } | Format-Table
```


<span data-ttu-id="2db08-121">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-121">Output:</span></span>
```
GroupName         GroupId                              GroupLicenses       TotalUserCount LicensedUserCount LicenseErrorCount
---------         -------                              -------------       -------------- ----------------- -----------------
Dynamics Licen... 9160c903-9f91-4597-8f79-22b6c47eafbf AAD_PREMIUM_P2                   0                 0                 0
O365 E5 - base... 055dcca3-fb75-4398-a1b8-f8c6f4c24e65 ENTERPRISEPREMIUM                2                 2                 0
O365 E5 - extr... 6b14a1fe-c3a9-4786-9ee4-3a2bb54dcb8e ENTERPRISEPREMIUM                3                 3                 0
EMS E5 - all s... 7023a314-6148-4d7b-b33f-6c775572879a EMSPREMIUM                       2                 2                 0
PowerBi - Lice... cf41f428-3b45-490b-b69f-a349c8a4c38e POWER_BI_STANDARD                2                 2                 0
O365 E3 - all ... 962f7189-59d9-4a29-983f-556ae56f19a5 ENTERPRISEPACK                   2                 2                 0
O365 E5 - EXO     102fb8f4-bbe7-462b-83ff-2145e7cdd6ed ENTERPRISEPREMIUM                1                 1                 0
Access tooOffi... 11151866-5419-4d93-9141-0603bbf78b42 STANDARDPACK                     4                 3                 1
```

## <a name="get-all-groups-with-license-errors"></a><span data-ttu-id="2db08-122">라이선스 오류가 있는 모든 그룹 가져오기</span><span class="sxs-lookup"><span data-stu-id="2db08-122">Get all groups with license errors</span></span>
<span data-ttu-id="2db08-123">toofind 사용자 포함 된 그룹 일부 대상에 대 한 라이선스를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-123">toofind groups that contain some users for whom licenses could not be assigned:</span></span>
```
Get-MsolGroup -HasLicenseErrorsOnly $true
```
<span data-ttu-id="2db08-124">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-124">Output:</span></span>
```
ObjectId                             DisplayName             GroupType Description
--------                             -----------             --------- -----------
11151866-5419-4d93-9141-0603bbf78b42 Access tooOffice 365 E1 Security  Users who should have E1 licenses
```
## <a name="get-all-users-with-license-errors-in-a-group"></a><span data-ttu-id="2db08-125">그룹에서 라이선스 오류가 있는 모든 사용자 가져오기</span><span class="sxs-lookup"><span data-stu-id="2db08-125">Get all users with license errors in a group</span></span>

<span data-ttu-id="2db08-126">라이선스 관련 오류가 포함된 그룹이 있는 경우 오류의 영향을 받는 모든 사용자를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-126">Given a group that contains some license related errors, you can now list all users affected by those errors.</span></span> <span data-ttu-id="2db08-127">다른 그룹의 오류도 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-127">A jser can have errors from other groups, too.</span></span> <span data-ttu-id="2db08-128">그러나 제한 되어 확인 하 여 결과 tooerrors 관련 toohello 그룹에이 예에서는 **ReferencedObjectId** 각 속성 **IndirectLicenseError** hello 사용자에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-128">However, in this example we limit results only tooerrors relevant toohello group in question by checking the **ReferencedObjectId** property of each **IndirectLicenseError** entry on hello user.</span></span>

```
#a sample group with errors
$groupId = '11151866-5419-4d93-9141-0603bbf78b42'

#get all user members of hello group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full information about user objects
    Get-MsolUser -ObjectId {$_.ObjectId} |
    #filter out users without license errors and users with licenense errors from other groups
    Where {$_.IndirectLicenseErrors -and $_.IndirectLicenseErrors.ReferencedObjectId -eq $groupId} |
    #display id, name and error detail. Note: we are filtering out license errors from other groups
    Select ObjectId, `
           DisplayName, `
           @{Name="LicenseError";Expression={$_.IndirectLicenseErrors | Where {$_.ReferencedObjectId -eq $groupId} | Select -ExpandProperty Error}}
```

<span data-ttu-id="2db08-129">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-129">Output:</span></span>
```
ObjectId                             DisplayName      License Error
--------                             -----------      ------------
6d325baf-22b7-46fa-a2fc-a2500613ca15 Catherine Gibson MutuallyExclusiveViolation
```
## <a name="get-all-users-with-license-errors-in-hello-entire-tenant"></a><span data-ttu-id="2db08-130">라이선스 오류로 hello 전체 테 넌 트의 모든 사용자를 가져오기</span><span class="sxs-lookup"><span data-stu-id="2db08-130">Get all users with license errors in hello entire tenant</span></span>

<span data-ttu-id="2db08-131">toolist 하나 또는 더 많은 그룹, 스크립트를 다음 hello에서 라이선스 오류 있는 모든 사용자가을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-131">toolist all users who have license errors from one or more groups, hello following script can be used.</span></span> <span data-ttu-id="2db08-132">이 스크립트에 행이 하나씩 표시 합니다. 사용자 당 수 있는 사용권 오류 당 tooclearly 식별 hello 각 오류의 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-132">This script will list one row per user, per license error which allows you tooclearly identify hello source of each error.</span></span>

> [!NOTE]
> <span data-ttu-id="2db08-133">이 스크립트는 테 넌 트의 큰 최적이 아닐 수 한 hello 테 넌 트의 모든 사용자가 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-133">This script will enumerate all users in hello tenant, which might not be optimal for large tenants.</span></span>

```
Get-MsolUser -All | Where {$_.IndirectLicenseErrors } | % {   
    $user = $_;
    $user.IndirectLicenseErrors | % {
            New-Object Object |
                Add-Member -NotePropertyName UserName -NotePropertyValue $user.DisplayName -PassThru |
                Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                Add-Member -NotePropertyName GroupId -NotePropertyValue $_.ReferencedObjectId -PassThru |
                Add-Member -NotePropertyName LicenseError -NotePropertyValue $_.Error -PassThru
        }
    }  
```

<span data-ttu-id="2db08-134">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-134">Output:</span></span>

```
UserName         UserId                               GroupId                              LicenseError
--------         ------                               -------                              ------------
Anna Bergman     0d0fd16d-872d-4e87-b0fb-83c610db12bc 7946137d-b00d-4336-975e-b1b81b0666d0 MutuallyExclusiveViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 f2503e79-0edc-4253-8bed-3e158366466b CountViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 11151866-5419-4d93-9141-0603bbf78b42 MutuallyExclusiveViolation
Drew Fogarty     f2af28fc-db0b-4909-873d-ddd2ab1fd58c 1ebd5028-6092-41d0-9668-129a3c471332 MutuallyExclusiveViolation
```

<span data-ttu-id="2db08-135">다음은 라이선스 오류가 포함 된 그룹을 통해만 검색 하는 hello 스크립트의 다른 버전이입니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-135">Here is another version of hello script that searches only through groups that contain license errors.</span></span> <span data-ttu-id="2db08-136">더 시나리오에 맞게 최적화 toohave 필요한 위치에 문제가 있는 몇 가지 그룹 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-136">It may be more optimized for scenarios where you expect toohave few groups with problems.</span></span>

```
Get-MsolUser -All | Where {$_.IndirectLicenseErrors } | % {   
    $user = $_;
    $user.IndirectLicenseErrors | % {
            New-Object Object |
                Add-Member -NotePropertyName UserName -NotePropertyValue $user.DisplayName -PassThru |
                Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                Add-Member -NotePropertyName GroupId -NotePropertyValue $_.ReferencedObjectId -PassThru |
                Add-Member -NotePropertyName LicenseError -NotePropertyValue $_.Error -PassThru
        }
    }
```

## <a name="check-if-user-license-is-assigned-directly-or-inherited-from-a-group"></a><span data-ttu-id="2db08-137">사용자 라이선스가 직접 할당되었는지 또는 그룹에서 상속되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="2db08-137">Check if user license is assigned directly or inherited from a group</span></span>

<span data-ttu-id="2db08-138">사용자 개체에 대 한 직접 할당 된 경우 또는 특정 제품 라이선스 그룹에서 지정 되 면 가능한 toocheck 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-138">For a user object it is possible toocheck if a particular product license is assigned from a group or if it is assigned directly.</span></span>

<span data-ttu-id="2db08-139">아래 두 hello 샘플 함수 일 수 있습니다 tooanalyze hello 유형의 할당 된 개별 사용자에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-139">hello two sample functions below can be used tooanalyze hello type of assignment on an individual user:</span></span>
```
#Returns TRUE if hello user has hello license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for hello specific license SKU in all licenses assigned toohello user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
            #This could be a group object or a user object (contrary toowhat hello name suggests)
            #If hello collection is empty, this means hello license is assigned directly - this is hello case for users who have never been licensed via groups in hello past
            if ($license.GroupsAssigningLicense.Count -eq 0)
            {
                return $true
            }

            #If hello collection contains hello ID of hello user object, this means hello license is assigned directly
            #Note: hello license may also be assigned through one or more groups in addition toobeing assigned directly
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                if ($assignmentSource -ieq $user.ObjectId)
                {
                    return $true
                }
            }
            return $false
        }
    }
    return $false
}
#Returns TRUE if hello user is inheriting hello license from a group
function UserHasLicenseAssignedFromGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for hello specific license SKU in all licenses assigned toohello user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
            #This could be a group object or a user object (contrary toowhat hello name suggests)
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                #If hello collection contains at least one ID not matching hello user ID this means that hello license is inherited from a group.
                #Note: hello license may also be assigned directly in addition toobeing inherited
                if ($assignmentSource -ine $user.ObjectId)
                {
                    return $true
                }
            }
            return $false
        }
    }
    return $false
}
```

<span data-ttu-id="2db08-140">이 스크립트는 hello 테 넌 트에서 hello SKU ID를 사용 하 여 입력으로 각 사용자에 대 한 이러한 함수의 실행-이 예제에서이 연습에 대 한 hello 라이선스 *Enterprise Mobility + 보안*, 우리의 테 넌 트에 나타나는 id *contoso:EMS*:</span><span class="sxs-lookup"><span data-stu-id="2db08-140">This script executes those functions on each user in hello tenant, using hello SKU ID as input - in this example we are interested in hello license for *Enterprise Mobility + Security*, which in our tenant is represented with ID *contoso:EMS*:</span></span>
```
#hello license SKU we are interested in. use Msol-GetAccountSku toosee a list of all identifiers in your tenant
$skuId = "contoso:EMS"

#find all users that have hello SKU license assigned
Get-MsolUser -All | where {$_.isLicensed -eq $true -and $_.Licenses.AccountSKUID -eq $skuId} | select `
    ObjectId, `
    @{Name="SkuId";Expression={$skuId}}, `
    @{Name="AssignedDirectly";Expression={(UserHasLicenseAssignedDirectly $_ $skuId)}}, `
    @{Name="AssignedFromGroup";Expression={(UserHasLicenseAssignedFromGroup $_ $skuId)}}
```

<span data-ttu-id="2db08-141">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-141">Output:</span></span>
```
ObjectId                             SkuId       AssignedDirectly AssignedFromGroup
--------                             -----       ---------------- -----------------
157870f6-e050-4b3c-ad5e-0f0a377c8f4d contoso:EMS             True             False
1f3174e2-ee9d-49e9-b917-e8d84650f895 contoso:EMS            False              True
240622ac-b9b8-4d50-94e2-dad19a3bf4b5 contoso:EMS             True              True
```

## <a name="remove-direct-licenses-for-users-with-group-licenses"></a><span data-ttu-id="2db08-142">그룹 라이선스가 있는 사용자에 대한 직접 라이선스 제거</span><span class="sxs-lookup"><span data-stu-id="2db08-142">Remove direct licenses for users with group licenses</span></span>
<span data-ttu-id="2db08-143">이 스크립트의 hello 목적은 tooremove 불필요 한 직접 라이선스를 이미 동일한 라이선스 hello; 그룹에서 상속 된 사용자 예를 들어의 일환으로는 [toogroup 기반 라이선스 전환](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-143">hello purpose of this script is tooremove unnecessary direct licenses from users who already inherit hello same license from a group; for example, as part of a [transitioning toogroup-based licensing](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal).</span></span>
> [!NOTE]
> <span data-ttu-id="2db08-144">Toofirst 해당 hello 유효성을 검사 반드시 제거 직접 라이선스 toobe hello 라이선스를 상속 하는 보다 더 많은 서비스 기능을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2db08-144">It is important toofirst validate that hello direct licenses toobe removed do not enable more service functionality than hello inherited licenses.</span></span> <span data-ttu-id="2db08-145">그렇지 않으면 hello 직접 라이선스를 제거 하지 못할 수 있습니다 액세스 tooservices 및 사용자에 대 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-145">Otherwise, removing hello direct license may disable access tooservices and data for users.</span></span> <span data-ttu-id="2db08-146">현재 직접 상속 된 라이선스 vs를 통해 사용 되는 서비스는 PowerShell 통해 가능한 toocheck는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-146">Currently it is not possible toocheck via PowerShell which services are enabled via inherited licenses vs direct.</span></span> <span data-ttu-id="2db08-147">Hello 스크립트에서 म 지정 hello 최소 수준의 회원님의 서비스 그룹에서 상속 되는 있는 대해 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-147">In hello script we will specify hello minimum level of services we know are being inherited from groups and we will check against that.</span></span>

```
#BEGIN: Helper functions used by hello script

#Returns TRUE if hello user has hello license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
        #This could be a group object or a user object (contrary toowhat hello name suggests)
        #If hello collection is empty, this means hello license is assigned directly - this is hello case for users who have never been licensed via groups in hello past
        if ($license.GroupsAssigningLicense.Count -eq 0)
        {
            return $true
        }

        #If hello collection contains hello ID of hello user object, this means hello license is assigned directly
        #Note: hello license may also be assigned through one or more groups in addition toobeing assigned directly
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            if ($assignmentSource -ieq $user.ObjectId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}
#Returns TRUE if hello user is inheriting hello license from a specific group
function UserHasLicenseAssignedFromThisGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning hello license
        #This could be a group object or a user object (contrary toowhat hello name suggests)
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            #If hello collection contains at least one ID not matching hello user ID this means that hello license is inherited from a group.
            #Note: hello license may also be assigned directly in addition toobeing inherited
            if ($assignmentSource -ieq $groupId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}

#Returns hello license object corresponding toohello skuId. Returns NULL if not found
function GetUserLicense
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)
    #we look for hello specific license SKU in all licenses assigned toohello user
    foreach($license in $user.Licenses)
    {
        if ($license.AccountSkuId -ieq $skuId)
        {
            return $license
        }
    }
    return $null
}

#produces a list of disabled service plan names for a set of plans we want tooleave enabled
function GetDisabledPlansForSKU
{
    Param([string]$skuId, [string[]]$enabledPlans)

    $allPlans = Get-MsolAccountSku | where {$_.AccountSkuId -ieq $skuId} | Select -ExpandProperty ServiceStatus | Where {$_.ProvisioningStatus -ieq "PendingActivation"} | Select -ExpandProperty ServicePlan | Select -ExpandProperty ServiceName
    $disabledPlans = $allPlans | Where {$enabledPlans -inotcontains $_}

    return $disabledPlans
}

function GetUnexpectedEnabledPlansForUser
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [string[]]$expectedDisabledPlans)

    $license = GetUserLicense $user $skuId

    $extraPlans = @();

    if($license -ne $null)
    {
        $userDisabledPlans = $license.ServiceStatus | where {$_.ProvisioningStatus -ieq "Disabled"} | Select -ExpandProperty ServicePlan | Select -ExpandProperty ServiceName

        $extraPlans = $expectedDisabledPlans | where {$userDisabledPlans -notcontains $_}
    }
    return $extraPlans
}
#END: helper functions

#BEGIN: executing hello script
#hello group toobe processed
$groupId = "48ca647b-7e4d-41e5-aa66-40cab1e19101"

#license toobe removed - Office 365 E3
$skuId = "contoso:ENTERPRISEPACK"

#minimum set of service plans we know are inherited from groups - we want toomake sure that there aren't any users who have more services enabled
#which could mean that they may lose access after we remove direct licenses
$servicePlansFromGroups = ("EXCHANGE_S_ENTERPRISE", "SHAREPOINTENTERPRISE", "OFFICESUBSCRIPTION")

$expectedDisabledPlans = GetDisabledPlansForSKU $skuId $servicePlansFromGroups

#process all members in hello group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in hello group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $operationResult = "";

        #check if Direct license exists on hello user
        if (UserHasLicenseAssignedDirectly $user $skuId)
        {
            #check if hello license is assigned from this group, as expected
            if (UserHasLicenseAssignedFromThisGroup $user $skuId $groupId)
            {
                #check if there are any extra plans we didn't expect - we are being extra careful not tooremove unexpected services
                $extraPlans = GetUnexpectedEnabledPlansForUser $user $skuId $expectedDisabledPlans
                if ($extraPlans.Count -gt 0)
                {
                    $operationResult = "User has extra plans that may be lost - license removal was skipped. Extra plans: $extraPlans"
                }
                else
                {
                    #remove hello direct license from user
                    Set-MsolUserLicense -ObjectId $user.ObjectId -RemoveLicenses $skuId
                    $operationResult = "Removed direct license from user."   
                }

            }
            else
            {
                $operationResult = "User does not inherit this license from this group. License removal was skipped."
            }
        }
        else
        {
            $operationResult = "User has no direct license tooremove. Skipping."
        }

        #format output
        New-Object Object |
                    Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                    Add-Member -NotePropertyName OperationResult -NotePropertyValue $operationResult -PassThru
    } | Format-Table
#END: executing hello script
```

<span data-ttu-id="2db08-148">출력:</span><span class="sxs-lookup"><span data-stu-id="2db08-148">Output:</span></span>
```
UserId                               OperationResult                                                                                
------                               ---------------                                                                                
7c7f860f-700a-462a-826c-f50633931362 Removed direct license from user.                                                              
0ddacdd5-0364-477d-9e4b-07eb6cdbc8ea User has extra plans that may be lost - license removal was skipped. Extra plans: SHAREPOINTWAC
aadbe4da-c4b5-4d84-800a-9400f31d7371 User has no direct license tooremove. Skipping.                                                
```

## <a name="next-steps"></a><span data-ttu-id="2db08-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2db08-149">Next steps</span></span>

<span data-ttu-id="2db08-150">그룹을 통해 라이선스 관리에 대 한 설정 hello 기능에 대 한 자세한 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2db08-150">toolearn more about hello feature set for license management through groups, see hello following:</span></span>

* [<span data-ttu-id="2db08-151">Azure Active Directory의 그룹 기반 라이선스란?</span><span class="sxs-lookup"><span data-stu-id="2db08-151">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="2db08-152">Azure Active Directory에서 tooa 그룹 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="2db08-152">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="2db08-153">Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="2db08-153">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="2db08-154">Toomigrate 개별 toogroup 기반 라이선스 Azure Active Directory에서 사용자가 사용이 허가 된 방법</span><span class="sxs-lookup"><span data-stu-id="2db08-154">How toomigrate individual licensed users toogroup-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="2db08-155">Azure Active Directory 그룹 기반 라이선스 추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="2db08-155">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
