---
title: "특정 랩 정책에 사용자 권한 부여| Microsoft 문서"
description: "각 사용자의 요구에 따라 DevTest Lab에서 특정 랩 정책에 사용자 권한을 부여하는 방법 알아보기"
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
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="8042d-103">특정 랩 정책에 사용자 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8042d-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="8042d-104">개요</span><span class="sxs-lookup"><span data-stu-id="8042d-104">Overview</span></span>
<span data-ttu-id="8042d-105">이 문서에서는 PowerShell을 사용하여 특정 랩 정책에 사용자 권한을 부여하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="8042d-106">이런 방식으로 각 사용자의 요구 사항에 따라 권한을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="8042d-107">예를 들어 특정 사용자에게 VM 정책 설정을 변경할 수 있는 기능은 부여하지만 비용 정책에 대해서는 부여하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="8042d-108">리소스인 정책</span><span class="sxs-lookup"><span data-stu-id="8042d-108">Policies as resources</span></span>
<span data-ttu-id="8042d-109">[Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md) 문서에 설명된 대로 RBAC를 사용하면 Azure 리소스에 대해 세밀한 리소스 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="8042d-110">RBAC를 사용하여 DevOps 팀 내에서 업무를 분리하고 사용자에게 해당 작업을 수행하는 데 필요한 만큼의 권한만 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="8042d-111">DevTest Lab에서 정책은 RBAC 작업 **Microsoft.DevTestLab/labs/policySets/policies/**를 지원하는 리소스 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="8042d-112">각 랩 정책은 정책 리소스 종류에 속한 리소스이며 RBAC 역할에 범위로 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="8042d-113">예를 들어, 사용자가 읽기/쓰기 권한을 부여 하기 위해는 **VM 크기** 정책을 사용 하는 사용자 지정 역할 만듭니다는 **Microsoft.DevTestLab/labs/policySets/policies/*** 작업 후의 범위에이 사용자 지정 역할에 적절 한 사용자를 할당 **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**합니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="8042d-114">RBAC의 사용자 지정 역할에 대한 자세한 내용은 [사용자 지정 역할 액세스 제어](../active-directory/role-based-access-control-custom-roles.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8042d-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="8042d-115">PowerShell을 사용하여 랩 사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="8042d-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="8042d-116">작업을 시작하려면 Azure PowerShell cmdlet을 설치하고 구성하는 방법을 설명하는 [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre)문서의 내용을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="8042d-117">Azure PowerShell cmdlet을 설정한 후 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="8042d-118">리소스 공급자에 대한 모든 작업 나열</span><span class="sxs-lookup"><span data-stu-id="8042d-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="8042d-119">특정 역할의 작업 나열</span><span class="sxs-lookup"><span data-stu-id="8042d-119">List actions in a particular role:</span></span>
* <span data-ttu-id="8042d-120">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="8042d-120">Create a custom role</span></span>

<span data-ttu-id="8042d-121">다음 PowerShell 스크립트는 이러한 작업을 수행하는 방법의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
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

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="8042d-122">사용자 지정 역할을 사용하여 특정 정책에 대해 사용자에게 권한 할당</span><span class="sxs-lookup"><span data-stu-id="8042d-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="8042d-123">사용자 지정 역할을 정의하고 나면 사용자에게 이 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="8042d-124">사용자 지정 역할을 사용자에게 할당하려면 먼저 해당 사용자를 나타내는 **ObjectId** 를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="8042d-125">이 작업을 수행하려면 **Get-AzureRmADUser** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="8042d-126">다음 예제에서 **SomeUser** 사용자의 *ObjectId* 는 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3입니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="8042d-127">사용자에 대한 **ObjectId**와 사용자 지정 역할 이름이 있으면 **New-AzureRmRoleAssignment** cmdlet을 사용하여 사용자에게 해당 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="8042d-128">앞의 예제에서는 **AllowedVmSizesInLab** 정책이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="8042d-129">다음 정책 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="8042d-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="8042d-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="8042d-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="8042d-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="8042d-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="8042d-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="8042d-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="8042d-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="8042d-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8042d-134">Next steps</span></span>
<span data-ttu-id="8042d-135">특정 랩 정책에 사용자 권한을 부여한 경우 다음 몇 가지 단계를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8042d-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="8042d-136">[랩에 안전하게 액세스](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="8042d-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="8042d-137">[랩 정책 설정](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8042d-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="8042d-138">[랩 템플릿 만들기](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="8042d-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="8042d-139">[VM에 대한 사용자 지정 아티팩트  만들기](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="8042d-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="8042d-140">[아티팩트가 지정된 VM을 랩에 추가](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="8042d-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

