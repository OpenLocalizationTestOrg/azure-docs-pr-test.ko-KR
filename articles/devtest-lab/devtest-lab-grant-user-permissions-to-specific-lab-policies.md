---
title: "aaaGrant 사용자 권한 toospecific 랩 정책 | Microsoft Docs"
description: "DevTest Labs toogrant 사용자 권한을 toospecific 랩 정책의 각 사용자의 요구에 따라 하는 방법에 대해 알아봅니다"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="b18fd-103">Toospecific 랩 정책 사용자 권한 부여</span><span class="sxs-lookup"><span data-stu-id="b18fd-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="b18fd-104">개요</span><span class="sxs-lookup"><span data-stu-id="b18fd-104">Overview</span></span>
<span data-ttu-id="b18fd-105">이 문서에서는 설명 방법을 toouse PowerShell toogrant 사용자 권한 tooa 특정 랩 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="b18fd-106">이런 방식으로 각 사용자의 요구 사항에 따라 권한을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="b18fd-107">예를 들어 toogrant는 특정 사용자 hello 기능 toochange hello VM 정책 설정을 할 수 있습니다 하지만 하지 hello 정책 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="b18fd-108">리소스인 정책</span><span class="sxs-lookup"><span data-stu-id="b18fd-108">Policies as resources</span></span>
<span data-ttu-id="b18fd-109">Hello에 설명 된 대로 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md) RBAC 문서에서는 Azure에 대 한 리소스의 세분화 된 액세스 관리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="b18fd-110">RBAC를 사용 하 여 DevOps 팀 내에서 업무를 구분할 수 있으며 필요 하다는 tooperform 업무만 hello 양을 toousers 액세스 권한을 부여 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="b18fd-111">DevTest Labs 정책을 hello RBAC 동작을 사용 하는 리소스 형식을 **Microsoft.DevTestLab/labs/policySets/policies/**합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="b18fd-112">각 lab 정책 hello 정책 리소스 종류의에서 리소스 이며 범위 tooan RBAC 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="b18fd-113">예를 들어 순서 toogrant 사용자 읽기/쓰기 권한 toohello **VM 크기** 정책을 만들면 됩니다 hello를 사용 하는 사용자 지정 역할 **Microsoft.DevTestLab/labs/policySets/policies/** * 작업, 및 할당 hello 적절 한 사용자 toothis 사용자 지정 역할의 hello 범위에 **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="b18fd-114">사용자 지정 역할 RBAC에 대 한 자세한 정보는 toolearn hello 참조 [역할 사용자 지정 액세스 제어](../active-directory/role-based-access-control-custom-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="b18fd-115">PowerShell을 사용하여 랩 사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="b18fd-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="b18fd-116">시작 순서 tooget, 해야 tooread hello 다음 방법을 설명 하는 문서 어떻게 tooinstall hello Azure PowerShell cmdlet을 구성 하 고: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre)합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="b18fd-117">Hello Azure PowerShell cmdlet 설정한 후 작업을 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="b18fd-118">리소스 공급자에 대 한 모든 hello 작업/작업 나열</span><span class="sxs-lookup"><span data-stu-id="b18fd-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="b18fd-119">특정 역할의 작업 나열</span><span class="sxs-lookup"><span data-stu-id="b18fd-119">List actions in a particular role:</span></span>
* <span data-ttu-id="b18fd-120">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="b18fd-120">Create a custom role</span></span>

<span data-ttu-id="b18fd-121">방법의 예를 설명 하는 PowerShell 스크립트 뒤 hello tooperform 이러한 작업:</span><span class="sxs-lookup"><span data-stu-id="b18fd-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="b18fd-122">사용자 지정 역할을 사용 하 여 특정 정책에 대 한 사용 권한을 tooa 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="b18fd-123">사용자 지정 역할을 정의 하 고 나면을 할당할 수 있습니다 toousers 합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="b18fd-124">순서 tooassign 사용자 지정 역할 tooa 사용자에서에서 먼저 받아야 hello **ObjectId** 해당 사용자를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="b18fd-125">hello를 사용 하는 toodo **Get AzureRmADUser** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b18fd-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="b18fd-126">다음 예제는 hello에서 hello **ObjectId** 의 hello *SomeUser* 사용자가 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="b18fd-127">Hello 있으면 **ObjectId** hello 사용자 및 사용자 지정 역할 이름에 대 한 hello로 해당 역할 toohello 사용자를 할당할 수 있습니다 **새로 AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b18fd-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="b18fd-128">Hello 이전 예에서 hello **AllowedVmSizesInLab** 정책이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="b18fd-129">Hello 다음 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="b18fd-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="b18fd-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="b18fd-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="b18fd-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="b18fd-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="b18fd-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="b18fd-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="b18fd-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="b18fd-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b18fd-134">Next steps</span></span>
<span data-ttu-id="b18fd-135">한 번 권한이 부여 된 사용자 권한을 toospecific 랩 정책 다음 몇 가지 단계 tooconsider 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="b18fd-136">[보안 액세스 tooa 랩](devtest-lab-add-devtest-user.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="b18fd-137">[랩 정책 설정](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b18fd-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="b18fd-138">[랩 템플릿 만들기](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="b18fd-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="b18fd-139">[VM에 대한 사용자 지정 아티팩트  만들기](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="b18fd-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="b18fd-140">[Tooa 랩 아티팩트를 사용 하 여 VM을 추가](devtest-lab-add-vm-with-artifacts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b18fd-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

