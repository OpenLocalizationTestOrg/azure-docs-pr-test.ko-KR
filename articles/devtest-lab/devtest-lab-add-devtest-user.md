---
title: "Azure DevTest Labs에 소유자 및 사용자 추가 | Microsoft 문서"
description: "Azure Portal 또는 PowerShell을 사용하여 Azure DevTest Labs에 소유자 및 사용자 추가"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="814ea-103">Azure DevTest Labs에 소유자 및 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="814ea-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="814ea-104">Azure DevTest Labs의 액세스는 [Azure RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-what-is.md)를 통해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="814ea-105">RBAC를 사용하면 팀 내에서 업무를 수행하기 위해 사용자에게 필요한 만큼의 액세스 권한을 부여하는 *역할* 로 업무를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="814ea-106">이러한 세 가지 RBAC 역할은 *소유자*, *DevTest Labs 사용자* 및 *참가자*입니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="814ea-107">이 문서에서는 세 가지 주요 RBAC 역할에서 각각 수행할 수 있는 작업을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="814ea-108">여기서 포털 및 PowerShell 스크립트를 통해 랩에 사용자를 추가하는 방법과 구독 수준에서 사용자를 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="814ea-109">각 역할에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="814ea-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="814ea-110">사용자를 할당할 수 있는 세 가지 주요 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="814ea-111">소유자</span><span class="sxs-lookup"><span data-stu-id="814ea-111">Owner</span></span>
* <span data-ttu-id="814ea-112">DevTest Lab 사용자</span><span class="sxs-lookup"><span data-stu-id="814ea-112">DevTest Labs User</span></span>
* <span data-ttu-id="814ea-113">참여자</span><span class="sxs-lookup"><span data-stu-id="814ea-113">Contributor</span></span>

<span data-ttu-id="814ea-114">다음 표에는 이러한 각 역할의 사용자가 수행할 수 있는 작업에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="814ea-115">**이 역할의 사용자가 수행할 수 있는 작업**</span><span class="sxs-lookup"><span data-stu-id="814ea-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="814ea-116">**DevTest Lab 사용자**</span><span class="sxs-lookup"><span data-stu-id="814ea-116">**DevTest Labs User**</span></span> | <span data-ttu-id="814ea-117">**소유자**</span><span class="sxs-lookup"><span data-stu-id="814ea-117">**Owner**</span></span> | <span data-ttu-id="814ea-118">**참여자**</span><span class="sxs-lookup"><span data-stu-id="814ea-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="814ea-119">**랩 작업**</span><span class="sxs-lookup"><span data-stu-id="814ea-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="814ea-120">랩에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="814ea-120">Add users to a lab</span></span> |<span data-ttu-id="814ea-121">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-121">No</span></span> |<span data-ttu-id="814ea-122">예</span><span class="sxs-lookup"><span data-stu-id="814ea-122">Yes</span></span> |<span data-ttu-id="814ea-123">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-123">No</span></span> |
| <span data-ttu-id="814ea-124">비용 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="814ea-124">Update cost settings</span></span> |<span data-ttu-id="814ea-125">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-125">No</span></span> |<span data-ttu-id="814ea-126">예</span><span class="sxs-lookup"><span data-stu-id="814ea-126">Yes</span></span> |<span data-ttu-id="814ea-127">예</span><span class="sxs-lookup"><span data-stu-id="814ea-127">Yes</span></span> |
| <span data-ttu-id="814ea-128">**VM 기본 작업**</span><span class="sxs-lookup"><span data-stu-id="814ea-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="814ea-129">사용자 지정 이미지 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="814ea-129">Add and remove custom images</span></span> |<span data-ttu-id="814ea-130">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-130">No</span></span> |<span data-ttu-id="814ea-131">예</span><span class="sxs-lookup"><span data-stu-id="814ea-131">Yes</span></span> |<span data-ttu-id="814ea-132">예</span><span class="sxs-lookup"><span data-stu-id="814ea-132">Yes</span></span> |
| <span data-ttu-id="814ea-133">수식 추가, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="814ea-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="814ea-134">예</span><span class="sxs-lookup"><span data-stu-id="814ea-134">Yes</span></span> |<span data-ttu-id="814ea-135">예</span><span class="sxs-lookup"><span data-stu-id="814ea-135">Yes</span></span> |<span data-ttu-id="814ea-136">예</span><span class="sxs-lookup"><span data-stu-id="814ea-136">Yes</span></span> |
| <span data-ttu-id="814ea-137">Azure Marketplace 이미지를 허용 목록에 추가</span><span class="sxs-lookup"><span data-stu-id="814ea-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="814ea-138">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-138">No</span></span> |<span data-ttu-id="814ea-139">예</span><span class="sxs-lookup"><span data-stu-id="814ea-139">Yes</span></span> |<span data-ttu-id="814ea-140">예</span><span class="sxs-lookup"><span data-stu-id="814ea-140">Yes</span></span> |
| <span data-ttu-id="814ea-141">**VM 작업**</span><span class="sxs-lookup"><span data-stu-id="814ea-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="814ea-142">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="814ea-142">Create VMs</span></span> |<span data-ttu-id="814ea-143">예</span><span class="sxs-lookup"><span data-stu-id="814ea-143">Yes</span></span> |<span data-ttu-id="814ea-144">예</span><span class="sxs-lookup"><span data-stu-id="814ea-144">Yes</span></span> |<span data-ttu-id="814ea-145">예</span><span class="sxs-lookup"><span data-stu-id="814ea-145">Yes</span></span> |
| <span data-ttu-id="814ea-146">VM 시작, 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="814ea-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="814ea-147">사용자가 만든 VM만</span><span class="sxs-lookup"><span data-stu-id="814ea-147">Only VMs created by the user</span></span> |<span data-ttu-id="814ea-148">예</span><span class="sxs-lookup"><span data-stu-id="814ea-148">Yes</span></span> |<span data-ttu-id="814ea-149">예</span><span class="sxs-lookup"><span data-stu-id="814ea-149">Yes</span></span> |
| <span data-ttu-id="814ea-150">VM 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="814ea-150">Update VM policies</span></span> |<span data-ttu-id="814ea-151">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-151">No</span></span> |<span data-ttu-id="814ea-152">예</span><span class="sxs-lookup"><span data-stu-id="814ea-152">Yes</span></span> |<span data-ttu-id="814ea-153">예</span><span class="sxs-lookup"><span data-stu-id="814ea-153">Yes</span></span> |
| <span data-ttu-id="814ea-154">VM에 데이터 디스크 추가/VM에서 데이터 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="814ea-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="814ea-155">사용자가 만든 VM만</span><span class="sxs-lookup"><span data-stu-id="814ea-155">Only VMs created by the user</span></span> |<span data-ttu-id="814ea-156">예</span><span class="sxs-lookup"><span data-stu-id="814ea-156">Yes</span></span> |<span data-ttu-id="814ea-157">예</span><span class="sxs-lookup"><span data-stu-id="814ea-157">Yes</span></span> |
| <span data-ttu-id="814ea-158">**아티팩트 작업**</span><span class="sxs-lookup"><span data-stu-id="814ea-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="814ea-159">아티팩트 리포지토리 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="814ea-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="814ea-160">아니요</span><span class="sxs-lookup"><span data-stu-id="814ea-160">No</span></span> |<span data-ttu-id="814ea-161">예</span><span class="sxs-lookup"><span data-stu-id="814ea-161">Yes</span></span> |<span data-ttu-id="814ea-162">예</span><span class="sxs-lookup"><span data-stu-id="814ea-162">Yes</span></span> |
| <span data-ttu-id="814ea-163">아티팩트 적용</span><span class="sxs-lookup"><span data-stu-id="814ea-163">Apply artifacts</span></span> |<span data-ttu-id="814ea-164">예</span><span class="sxs-lookup"><span data-stu-id="814ea-164">Yes</span></span> |<span data-ttu-id="814ea-165">예</span><span class="sxs-lookup"><span data-stu-id="814ea-165">Yes</span></span> |<span data-ttu-id="814ea-166">예</span><span class="sxs-lookup"><span data-stu-id="814ea-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="814ea-167">사용자가 VM을 만들면 해당 사용자는 만든 VM의 **소유자** 역할에 자동으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="814ea-168">랩 수준에서 소유자 또는 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="814ea-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="814ea-169">Azure Portal을 통해 랩 수준에서 소유자 및 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="814ea-170">여기에는 유효한 [MSA(Microsoft 계정)](devtest-lab-faq.md#what-is-a-microsoft-account)를 가진 외부 사용자도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="814ea-171">다음 단계는 Azure DevTest Labs에서 랩에 소유자 또는 사용자를 추가하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="814ea-172">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="814ea-173">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="814ea-174">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="814ea-175">랩의 블레이드에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="814ea-176">**구성** 블레이드에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="814ea-177">**사용자** 블레이드에서 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![사용자 추가](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="814ea-179">**역할 선택** 블레이드에서 원하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="814ea-180">[각 역할에서 수행할 수 있는 작업](#actions-that-can-be-performed-in-each-role) 섹션에서 소유자, DevTest 사용자 및 참여자 역할의 사용자가 수행할 수 있는 다양한 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="814ea-181">**사용자 추가** 블레이드에서 지정한 역할에 추가할 사용자의 메일 주소 또는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="814ea-182">사용자를 찾을 수 없는 경우 문제를 설명하는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="814ea-183">사용자를 찾은 경우 해당 사용자가 나열되고 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="814ea-184">**선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-184">Select **Select**.</span></span>
10. <span data-ttu-id="814ea-185">**확인**을 선택하여 **액세스 추가** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="814ea-186">**사용자** 블레이드로 돌아가면 사용자가 추가되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="814ea-187">PowerShell을 사용하여 랩에 외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="814ea-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="814ea-188">Azure Portal에 사용자를 추가하는 것 외에도 PowerShell 스크립트를 사용하여 랩에 외부 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="814ea-189">다음 예제에서 **변경할 값** 설명대로 매개 변수 값을 간단히 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="814ea-190">Azure Portal의 랩 블레이드에서 `subscriptionId`, `labResourceGroup` 및 `labName` 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="814ea-191">샘플 스크립트는 지정된 사용자가 Active Directory에 게스트로 추가된 것으로 가정하고 사례가 없는 경우 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="814ea-192">Active Directory에 없는 사용자를 랩에 추가하려면 [랩 수준에서 소유자 또는 사용자 추가](#add-an-owner-or-user-at-the-lab-level)섹션에 설명된 대로 Azure Portal을 사용하여 사용자를 역할에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="814ea-193">구독 수준에서 소유자 또는 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="814ea-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="814ea-194">Azure 권한은 Azure의 부모 범위에서 자식 범위로 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="814ea-195">따라서 랩을 포함하는 Azure 구독 소유자는 자동으로 해당 랩의 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="814ea-196">랩의 사용자가 만든 다른 리소스와 VM 및 Azure DevTest Labs 서비스의 소유자이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="814ea-197">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)에서 랩의 블레이드를 통해 랩에 소유자를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="814ea-198">그러나 추가된 소유자의 관리 범위는 구독 소유자 범위보다 더 좁습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="814ea-199">예를 들어 추가된 소유자는 DevTest Labs 서비스에서 구독에 만든 일부 리소스에 대해서는 모든 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="814ea-200">Azure 구독에 소유자를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="814ea-201">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="814ea-202">**추가 서비스**를 선택한 다음 목록에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="814ea-203">원하는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="814ea-204">**액세스** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-204">Select **Access** icon.</span></span> 
   
    ![사용자 액세스](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="814ea-206">**사용자** 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-206">On the **Users** blade, select **Add**.</span></span>
   
    ![사용자 추가](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="814ea-208">**역할 선택** 블레이드에서 **소유자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="814ea-209">**사용자 추가** 블레이드에서 소유자로 추가할 사용자의 메일 주소 또는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="814ea-210">사용자를 찾을 수 없는 경우 문제를 설명하는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="814ea-211">사용자를 찾은 경우 해당 사용자가 **사용자** 텍스트 상자 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="814ea-212">찾은 사용자 이름을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-212">Select the located user name.</span></span>
9. <span data-ttu-id="814ea-213">**선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-213">Select **Select**.</span></span>
10. <span data-ttu-id="814ea-214">**확인**을 선택하여 **액세스 추가** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="814ea-215">**사용자** 블레이드로 돌아가면 사용자가 소유자로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="814ea-216">이제 이 사용자는 이 구독 아래에 만든 랩의 소유자이므로 소유자 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814ea-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

