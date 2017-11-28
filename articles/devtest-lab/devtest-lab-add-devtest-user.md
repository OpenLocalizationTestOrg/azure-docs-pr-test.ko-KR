---
title: "aaaAdd 소유자 및 사용자가 Azure DevTest Labs | Microsoft Docs"
description: "Hello Azure 포털 또는 PowerShell을 사용 하 여 Azure DevTest Labs에 소유자와 사용자 추가"
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
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="cc83f-103">Azure DevTest Labs에 소유자 및 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="cc83f-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="cc83f-104">Azure DevTest Labs의 액세스는 [Azure RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-what-is.md)를 통해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="cc83f-105">RBAC를 사용 하 여 있습니다 수 구분할 업무에 팀 내에서 *역할* 하면 부여 hello 양의 데이터만 액세스가 필요한 toousers tooperform 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="cc83f-106">이러한 세 가지 RBAC 역할은 *소유자*, *DevTest Labs 사용자* 및 *참가자*입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="cc83f-107">이 문서에 알아봅니다 hello 세 가지 주요 RBAC 역할의 각 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="cc83f-108">어떻게 tooadd 사용자 tooa 랩-를 통해 둘 다 hello 배웁니다 여기서에서 포털 및 PowerShell 스크립트 및에서 tooadd 사용자 구독 수준 hello 하는 방법을 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="cc83f-109">각 역할에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="cc83f-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="cc83f-110">사용자를 할당할 수 있는 세 가지 주요 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="cc83f-111">소유자</span><span class="sxs-lookup"><span data-stu-id="cc83f-111">Owner</span></span>
* <span data-ttu-id="cc83f-112">DevTest Lab 사용자</span><span class="sxs-lookup"><span data-stu-id="cc83f-112">DevTest Labs User</span></span>
* <span data-ttu-id="cc83f-113">참여자</span><span class="sxs-lookup"><span data-stu-id="cc83f-113">Contributor</span></span>

<span data-ttu-id="cc83f-114">hello 다음 테이블에서는 이러한 각 역할의 사용자가 수행할 수 있는 hello 작업 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="cc83f-115">**이 역할의 사용자가 수행할 수 있는 작업**</span><span class="sxs-lookup"><span data-stu-id="cc83f-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="cc83f-116">**DevTest Lab 사용자**</span><span class="sxs-lookup"><span data-stu-id="cc83f-116">**DevTest Labs User**</span></span> | <span data-ttu-id="cc83f-117">**소유자**</span><span class="sxs-lookup"><span data-stu-id="cc83f-117">**Owner**</span></span> | <span data-ttu-id="cc83f-118">**참여자**</span><span class="sxs-lookup"><span data-stu-id="cc83f-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cc83f-119">**랩 작업**</span><span class="sxs-lookup"><span data-stu-id="cc83f-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="cc83f-120">사용자가 tooa 랩 추가</span><span class="sxs-lookup"><span data-stu-id="cc83f-120">Add users tooa lab</span></span> |<span data-ttu-id="cc83f-121">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-121">No</span></span> |<span data-ttu-id="cc83f-122">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-122">Yes</span></span> |<span data-ttu-id="cc83f-123">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-123">No</span></span> |
| <span data-ttu-id="cc83f-124">비용 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="cc83f-124">Update cost settings</span></span> |<span data-ttu-id="cc83f-125">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-125">No</span></span> |<span data-ttu-id="cc83f-126">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-126">Yes</span></span> |<span data-ttu-id="cc83f-127">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-127">Yes</span></span> |
| <span data-ttu-id="cc83f-128">**VM 기본 작업**</span><span class="sxs-lookup"><span data-stu-id="cc83f-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="cc83f-129">사용자 지정 이미지 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="cc83f-129">Add and remove custom images</span></span> |<span data-ttu-id="cc83f-130">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-130">No</span></span> |<span data-ttu-id="cc83f-131">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-131">Yes</span></span> |<span data-ttu-id="cc83f-132">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-132">Yes</span></span> |
| <span data-ttu-id="cc83f-133">수식 추가, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="cc83f-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="cc83f-134">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-134">Yes</span></span> |<span data-ttu-id="cc83f-135">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-135">Yes</span></span> |<span data-ttu-id="cc83f-136">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-136">Yes</span></span> |
| <span data-ttu-id="cc83f-137">Azure Marketplace 이미지를 허용 목록에 추가</span><span class="sxs-lookup"><span data-stu-id="cc83f-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="cc83f-138">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-138">No</span></span> |<span data-ttu-id="cc83f-139">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-139">Yes</span></span> |<span data-ttu-id="cc83f-140">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-140">Yes</span></span> |
| <span data-ttu-id="cc83f-141">**VM 작업**</span><span class="sxs-lookup"><span data-stu-id="cc83f-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="cc83f-142">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cc83f-142">Create VMs</span></span> |<span data-ttu-id="cc83f-143">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-143">Yes</span></span> |<span data-ttu-id="cc83f-144">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-144">Yes</span></span> |<span data-ttu-id="cc83f-145">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-145">Yes</span></span> |
| <span data-ttu-id="cc83f-146">VM 시작, 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="cc83f-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="cc83f-147">Hello 사용자가 만든 Vm에만</span><span class="sxs-lookup"><span data-stu-id="cc83f-147">Only VMs created by hello user</span></span> |<span data-ttu-id="cc83f-148">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-148">Yes</span></span> |<span data-ttu-id="cc83f-149">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-149">Yes</span></span> |
| <span data-ttu-id="cc83f-150">VM 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="cc83f-150">Update VM policies</span></span> |<span data-ttu-id="cc83f-151">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-151">No</span></span> |<span data-ttu-id="cc83f-152">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-152">Yes</span></span> |<span data-ttu-id="cc83f-153">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-153">Yes</span></span> |
| <span data-ttu-id="cc83f-154">VM에 데이터 디스크 추가/VM에서 데이터 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="cc83f-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="cc83f-155">Hello 사용자가 만든 Vm에만</span><span class="sxs-lookup"><span data-stu-id="cc83f-155">Only VMs created by hello user</span></span> |<span data-ttu-id="cc83f-156">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-156">Yes</span></span> |<span data-ttu-id="cc83f-157">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-157">Yes</span></span> |
| <span data-ttu-id="cc83f-158">**아티팩트 작업**</span><span class="sxs-lookup"><span data-stu-id="cc83f-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="cc83f-159">아티팩트 리포지토리 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="cc83f-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="cc83f-160">아니요</span><span class="sxs-lookup"><span data-stu-id="cc83f-160">No</span></span> |<span data-ttu-id="cc83f-161">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-161">Yes</span></span> |<span data-ttu-id="cc83f-162">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-162">Yes</span></span> |
| <span data-ttu-id="cc83f-163">아티팩트 적용</span><span class="sxs-lookup"><span data-stu-id="cc83f-163">Apply artifacts</span></span> |<span data-ttu-id="cc83f-164">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-164">Yes</span></span> |<span data-ttu-id="cc83f-165">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-165">Yes</span></span> |<span data-ttu-id="cc83f-166">예</span><span class="sxs-lookup"><span data-stu-id="cc83f-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="cc83f-167">사용자는 VM을 만들 해당 사용자가 자동으로 할당 toohello **소유자** VM을 만든 hello의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="cc83f-168">Hello 랩 수준에서 소유자 또는 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="cc83f-169">Hello Azure 포털을 통해 hello 랩 수준에서 소유자 및 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="cc83f-170">여기에는 유효한 [MSA(Microsoft 계정)](devtest-lab-faq.md#what-is-a-microsoft-account)를 가진 외부 사용자도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="cc83f-171">단계를 수행 하는 hello Azure DevTest Labs에는 소유자 또는 사용자 tooa 랩을 추가 hello 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="cc83f-172">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="cc83f-173">선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="cc83f-174">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="cc83f-175">Hello 랩 블레이드에서 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="cc83f-176">Hello에 **구성** 블레이드를 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="cc83f-177">Hello에 **사용자** 블레이드를 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![사용자 추가](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="cc83f-179">Hello에 **역할 선택** 블레이드, 선택 hello 할당할된 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="cc83f-180">섹션 hello [각 역할에서 수행할 수 있는 작업](#actions-that-can-be-performed-in-each-role) 목록 hello hello 소유자, DevTest 사용자 및 참가자 역할의 사용자가 수행할 수 있는 다양 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="cc83f-181">Hello에 **사용자 추가** 블레이드에서 hello 전자 메일 주소 또는 지정한 hello 역할에 tooadd hello 사용자의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="cc83f-182">Hello 사용자를 찾을 수 없는 경우 오류 메시지가 hello 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="cc83f-183">Hello 사용자의 경우, 해당 사용자가 선택 되어 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="cc83f-184">**선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-184">Select **Select**.</span></span>
10. <span data-ttu-id="cc83f-185">선택 **확인** tooclose hello **액세스 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="cc83f-186">Toohello 돌아가서 **사용자** 블레이드에서 hello 사용자가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="cc83f-187">PowerShell을 사용 하는 외부 사용자 tooa 랩을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="cc83f-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="cc83f-188">또한 hello Azure 포털에서에서 tooadding 사용자, PowerShell 스크립트를 사용 하는 외부 사용자 tooyour 랩을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="cc83f-189">Hello에서 hello에서 hello 매개 변수 값을 수정 하면 다음 예제를 **값 toochange** 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="cc83f-190">Hello를 검색할 수 있습니다 `subscriptionId`, `labResourceGroup`, 및 `labName` hello Azure 포털에서에서 hello 랩 블레이드의 값으로에서.</span><span class="sxs-lookup"><span data-stu-id="cc83f-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="cc83f-191">hello 샘플 스크립트는 hello 사용자 게스트 toohello Active Directory로 추가 되 고 hello 대/소문자 그렇지 않은 경우 실패 합니다를 지정 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="cc83f-192">Active Directory tooa 랩 hello에 없는 사용자 tooadd hello 섹션에 설명 된 대로 hello Azure 포털 tooassign hello 사용자 tooa 역할을 사용 [hello 랩 수준에서 소유자 또는 사용자를 추가](#add-an-owner-or-user-at-the-lab-level)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="cc83f-193">Hello 구독 수준에서 소유자 또는 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="cc83f-194">Azure에서 부모 범위 toochild 범위에서 azure 권한 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="cc83f-195">따라서 랩을 포함하는 Azure 구독 소유자는 자동으로 해당 랩의 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="cc83f-196">Hello Vm 및 기타 리소스 hello lab의 사용자 및 hello Azure DevTest Labs 서비스에서 만든 또한 소유한.</span><span class="sxs-lookup"><span data-stu-id="cc83f-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="cc83f-197">Hello에 hello 랩 블레이드를 통해 tooa 랩 추가 소유자를 추가할 수 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="cc83f-198">그러나 hello 소유자의 관리 범위는 hello 구독 소유자의 범위 보다 더 세부적인 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="cc83f-199">예를 들어 hello 추가 소유자 hello DevTest Labs 서비스에 의해 hello 구독에서 만들어진 hello 리소스에 대 한 모든 권한을 toosome 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="cc83f-200">tooadd 소유자 tooan Azure 구독에는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="cc83f-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="cc83f-201">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="cc83f-202">선택 **더 서비스**를 선택한 후 **구독** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="cc83f-203">Hello 원하는 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="cc83f-204">**액세스** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-204">Select **Access** icon.</span></span> 
   
    ![사용자 액세스](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="cc83f-206">Hello에 **사용자** 블레이드를 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![사용자 추가](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="cc83f-208">Hello에 **역할 선택** 블레이드에서 선택 **소유자**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="cc83f-209">Hello에 **사용자 추가** 블레이드에서 hello 전자 메일 주소 또는 이름을 입력 hello 사용자의 소유자로 tooadd 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="cc83f-210">Hello 사용자를 찾을 수 없는 경우 hello 문제를 설명 하는 오류 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="cc83f-211">Hello 사용자의 경우, 해당 사용자 아래에 있는지 hello **사용자** 입력란.</span><span class="sxs-lookup"><span data-stu-id="cc83f-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="cc83f-212">Hello 있는 사용자 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-212">Select hello located user name.</span></span>
9. <span data-ttu-id="cc83f-213">**선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-213">Select **Select**.</span></span>
10. <span data-ttu-id="cc83f-214">선택 **확인** tooclose hello **액세스 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="cc83f-215">Toohello 돌아가서 **사용자** 블레이드에서 hello 사용자가 소유자로 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="cc83f-216">이 사용자는 이제이 구독에서 만든 모든 랩의 소유자가 되며 수 tooperform 소유자 작업 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83f-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

