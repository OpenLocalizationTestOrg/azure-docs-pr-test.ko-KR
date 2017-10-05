---
title: "Azure Site Recovery에서 복구 계획에 Azure Automation Runbook 추가 | Microsoft Docs"
description: "Azure Site Recovery가 Azure Automation을 사용하여 복구 계획을 확장하는 데 어떻게 도움이 되는지 알아봅니다. Azure로 복구하는 동안 복잡한 작업을 완료하는 방법을 알아봅니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="c4ded-104">복구 계획에 Azure Automation Runbook 추가</span><span class="sxs-lookup"><span data-stu-id="c4ded-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="c4ded-105">이 문서에서는 Azure Site Recovery를 Azure Automation에 통합하여 복구 계획을 확장하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="c4ded-106">복구 계획으로 Site Recovery로 보호되는 VM의 복구를 오케스트레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="c4ded-107">복구 계획은 보조 클라우드로 복제 및 Azure로의 복제 모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="c4ded-108">복구 계획을 통해 복구를 **일관적으로 정확**하고, **반복 가능**하며, **자동화**되도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="c4ded-109">VM을 Azure로 장애 조치(failover)하는 경우 Azure Automation과 통합하면 복구 계획이 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="c4ded-110">이를 통해 강력한 자동화 작업을 제공하는 Runbook을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="c4ded-111">Azure Automation을 처음 접하는 경우 [등록](https://azure.microsoft.com/services/automation/)하여 [샘플 스크립트를 다운로드](https://azure.microsoft.com/documentation/scripts/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="c4ded-112">[복구 계획](https://azure.microsoft.com/blog/?p=166264)을 사용하여 Azure에 복구를 오케스트레이션하는 방법에 대한 자세한 내용은 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ded-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="c4ded-113">이 문서에서는 Azure Automation Runbook을 복구 계획에 어떻게 통합할 수 있는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="c4ded-114">이전에는 수동 개입이 필요했던 기본 작업을 자동화하는 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="c4ded-115">또한 다단계 복구를 단일 클릭 복구 작업으로 변환하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="c4ded-116">복구 계획 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c4ded-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="c4ded-117">**Site Recovery** 복구 계획 리소스 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="c4ded-118">이 예제의 경우 복구 계획에 두 개의 VM이 복구용으로 추가되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="c4ded-119">Runbook 추가를 시작하려면 **사용자 지정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![[사용자 지정] 단추 클릭](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="c4ded-121">**그룹 1: 시작**을 마우스 오른쪽 단추로 클릭한 후 **사후 작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![그룹 1: 시작을 마우스 오른쪽 단추로 클릭하고 사후 작업 추가](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="c4ded-123">**스크립트 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="c4ded-124">**업데이트 작업** 블레이드에서 스크립트 이름을 **Hello World**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![업데이트 작업 블레이드](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="c4ded-126">Automation 계정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="c4ded-127">Automation 계정은 모든 Azure 지역에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="c4ded-128">Automation 계정은 Azure Site Recovery 자격 증명 모음과 동일한 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="c4ded-129">Automation 계정에서 Runbook을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="c4ded-130">이 Runbook은 첫 번째 그룹을 복구한 후에 복구 계획을 실행하는 동안 실행할 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="c4ded-131">스크립트를 저장하려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-131">To save the script, click **OK**.</span></span> <span data-ttu-id="c4ded-132">스크립트가 **그룹 1: 사후 단계**에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-132">The script is added to **Group 1: Post-steps**.</span></span>

    ![사후 작업 그룹 1: 시작](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="c4ded-134">스크립트를 추가하기 위한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c4ded-134">Considerations for adding a script</span></span>

* <span data-ttu-id="c4ded-135">**단계 삭제** 또는 **스크립트 업데이트**에 대한 옵션에서 스크립트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="c4ded-136">스크립트는 온-프레미스 컴퓨터에서 Azure로 장애 조치하는 동안 Azure에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="c4ded-137">또한 Azure에서 온-프레미스 컴퓨터로 장애 복구(failback)하는 동안 종료하기 전에 주 사이트 스크립트로 Azure에서 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="c4ded-138">스크립트가 실행되면 복구 계획 컨텍스트가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="c4ded-139">다음 예제는 컨텍스트 변수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-139">The following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="c4ded-140">다음 표에는 컨텍스트의 각 변수에 대한 이름과 설명이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="c4ded-141">**변수 이름**</span><span class="sxs-lookup"><span data-stu-id="c4ded-141">**Variable name**</span></span> | <span data-ttu-id="c4ded-142">**설명**</span><span class="sxs-lookup"><span data-stu-id="c4ded-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="c4ded-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="c4ded-143">RecoveryPlanName</span></span> |<span data-ttu-id="c4ded-144">실행되는 계획의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-144">The name of the plan being run.</span></span> <span data-ttu-id="c4ded-145">이 변수를 사용하면 복구 계획 이름에 따라 서로 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="c4ded-146">또한 스크립트 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="c4ded-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="c4ded-147">FailoverType</span></span> |<span data-ttu-id="c4ded-148">장애 조치(failover)가 테스트, 계획됨 또는 계획되지 않음인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="c4ded-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="c4ded-149">FailoverDirection</span></span> |<span data-ttu-id="c4ded-150">복구가 주 사이트 쪽으로 이루어지는지 보조 사이트 쪽으로 이루어지는지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="c4ded-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="c4ded-151">GroupID</span></span> |<span data-ttu-id="c4ded-152">계획이 실행 중일 때 복구 계획에서 그룹 번호를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="c4ded-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="c4ded-153">VmMap</span></span> |<span data-ttu-id="c4ded-154">그룹의 모든 VM 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="c4ded-155">VMMap key</span><span class="sxs-lookup"><span data-stu-id="c4ded-155">VMMap key</span></span> |<span data-ttu-id="c4ded-156">각 VM에 대한 고유 키(GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="c4ded-157">해당되는 경우 VM의 Azure VMM(Virtual Machine Manager) ID와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="c4ded-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="c4ded-158">SubscriptionId</span></span> |<span data-ttu-id="c4ded-159">VM이 만들어진 Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="c4ded-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="c4ded-160">RoleName</span></span> |<span data-ttu-id="c4ded-161">복구 중인 Azure VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="c4ded-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="c4ded-162">CloudServiceName</span></span> |<span data-ttu-id="c4ded-163">VM이 만들어진 Azure 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="c4ded-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c4ded-164">ResourceGroupName</span></span>|<span data-ttu-id="c4ded-165">VM이 만들어진 Azure 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="c4ded-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="c4ded-166">RecoveryPointId</span></span>|<span data-ttu-id="c4ded-167">VM이 복구될 때의 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="c4ded-168">Automation 계정에 다음 모듈이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="c4ded-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="c4ded-169">AzureRM.profile</span></span>
    * <span data-ttu-id="c4ded-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="c4ded-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="c4ded-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="c4ded-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="c4ded-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="c4ded-172">AzureRM.Network</span></span>
    * <span data-ttu-id="c4ded-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="c4ded-173">AzureRM.Compute</span></span>

<span data-ttu-id="c4ded-174">모든 모듈은 호환되는 버전이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="c4ded-175">모든 모듈이 호환되는지 확인하는 간단한 방법은 모든 모듈에 대한 최신 버전을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="c4ded-176">루프에서 VMMap의 모든 VM 액세스</span><span class="sxs-lookup"><span data-stu-id="c4ded-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="c4ded-177">다음 코드를 사용하여 Microsoft VMMap의 모든 VM을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="c4ded-178">스크립트가 부팅 그룹에 대한 사전 작업인 경우 리소스 그룹 이름과 역할 이름 값이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="c4ded-179">해당 그룹의 VM이 성공적으로 장애 조치되는 경우에만 값이 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="c4ded-180">이 스크립트는 부팅 그룹의 사후 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="c4ded-181">여러 복구 계획에 동일한 Automation Runbook 사용</span><span class="sxs-lookup"><span data-stu-id="c4ded-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="c4ded-182">단일 스크립트는 외부 변수를 사용하여 여러 복구 계획에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="c4ded-183">[Azure Automation 변수](../automation/automation-variables.md)를 사용하여 복구 계획 실행을 위해 전달할 수 있는 매개 변수를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="c4ded-184">복구 계획 이름을 변수에 대한 접두사로 추가하여 각 복구 계획에 대한 개별 변수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="c4ded-185">그런 다음 매개 변수로 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="c4ded-186">스크립트를 변경하지 않고 매개 변수를 변경할 수 있으며 스크립트가 작동하는 방식도 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="c4ded-187">Runbook 스크립트에서 단순 문자열 변수 사용</span><span class="sxs-lookup"><span data-stu-id="c4ded-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="c4ded-188">이 예제에서 스크립트는 NSG(네트워크 보안 그룹)의 입력을 받아서 복구 계획의 VM에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="c4ded-189">스크립트에서 실행 중인 복구 계획을 검색할 수 있도록 복구 계획 컨텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="c4ded-190">기존 NSG를 적용하려면 NSG 이름과 NSG 리소스 그룹 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="c4ded-191">복구 계획 스크립트에 대한 입력으로 이러한 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="c4ded-192">이렇게 하려면 Automation 계정 자산에서 두 개의 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="c4ded-193">변수 이름에 대한 접두사로 매개 변수를 생성 중인 복구 계획의 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="c4ded-194">NSG 이름을 저장할 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="c4ded-195">복구 계획의 이름을 사용하여 변수 이름에 접두사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![NSG 이름 변수 만들기](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="c4ded-197">NSG의 리소스 그룹 이름을 저장할 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="c4ded-198">복구 계획의 이름을 사용하여 변수 이름에 접두사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![NSG 리소스 그룹 이름 만들기](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="c4ded-200">스크립트에서 다음 참조 코드를 사용하여 변수 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="c4ded-201">Runbook에서 변수를 사용하여 장애 조치된 VM의 네트워크 인터페이스에 NSG를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="c4ded-202">각 복구 계획마다 개별 변수를 만들어 스크립트를 다시 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="c4ded-203">복구 계획 이름을 사용하여 접두사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="c4ded-204">이 시나리오에 대한 종단 간 전체 스크립트는 [Site Recovery 복구 계획의 테스트 장애 조치 중에 VM에 공용 IP 및 NSG 추가](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ded-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="c4ded-205">복합 변수를 사용하여 자세한 정보 저장</span><span class="sxs-lookup"><span data-stu-id="c4ded-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="c4ded-206">단일 스크립트에서 특정 VM의 공용 IP를 설정하는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="c4ded-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="c4ded-207">다른 시나리오에서는 서로 다른 VM(모든 VM 아님)에는 다른 NSG를 적용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="c4ded-208">모든 복구 계획에 다시 사용할 수 있는 스크립트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="c4ded-209">각 복구 계획에는 다양한 수의 VM이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="c4ded-210">예를 들어 SharePoint 복구에는 두 개의 프런트 엔드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="c4ded-211">기본 LOB(기간 업무) 응용 프로그램에는 하나의 프런트 엔드만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="c4ded-212">각 복구 계획에 별도의 변수를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="c4ded-213">다음 예제에서는 Azure Automation 계정 자산에서 새 기술을 사용하고 [복합 변수](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="c4ded-214">여러 값을 지정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="c4ded-215">다음 단계를 완료하려면 Azure PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="c4ded-216">PowerShell에서 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="c4ded-217">매개 변수를 저장하려면 복구 계획의 이름을 사용하여 복합 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="c4ded-218">이 복합 변수에서 **VMDetails**는 보호된 VM의 VM ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="c4ded-219">Azure Portal에서 VM ID를 가져오려면 VM 속성을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="c4ded-220">다음 스크린샷은 두 VM의 세부 정보를 저장하는 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![VM ID를 GUID로 사용](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="c4ded-222">Runbook에서 이 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-222">Use this variable in your runbook.</span></span> <span data-ttu-id="c4ded-223">표시된 VM GUID가 복구 계획 컨텍스트에 있으면 VM에서 NSG를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="c4ded-224">Runbook에서 복구 계획 컨텍스트 VM을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="c4ded-225">**$VMDetailsObj**에서 VM의 존재 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="c4ded-226">존재하는 경우 변수 속성에 액세스하여 NSG를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="c4ded-227">다른 복구 계획에 대해 동일한 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="c4ded-228">다른 변수에서 복구 계획에 해당하는 값을 저장하여 서로 다른 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="c4ded-229">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c4ded-229">Sample scripts</span></span>

<span data-ttu-id="c4ded-230">Automation 계정에 샘플 스크립트를 배포하려면 **Azure에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="c4ded-231">[![Azure에 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="c4ded-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="c4ded-232">다른 예제를 보려면 다음 비디오를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ded-232">For another example, see the following video.</span></span> <span data-ttu-id="c4ded-233">Azure로 2계층 WordPress 응용 프로그램을 복구하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4ded-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="c4ded-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c4ded-234">Additional resources</span></span>
* [<span data-ttu-id="c4ded-235">Azure Automation 서비스 실행 계정</span><span class="sxs-lookup"><span data-stu-id="c4ded-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="c4ded-236">Azure Automation 개요</span><span class="sxs-lookup"><span data-stu-id="c4ded-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation 개요")
* [<span data-ttu-id="c4ded-237">Azure Automation 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c4ded-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation 샘플 스크립트")
