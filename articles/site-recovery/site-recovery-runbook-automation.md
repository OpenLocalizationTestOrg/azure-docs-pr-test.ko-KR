---
title: "Azure 사이트 복구의 aaaAdd Azure 자동화 runbook toorecovery 계획 | Microsoft Docs"
description: "Azure Site Recovery가 Azure Automation을 사용하여 복구 계획을 확장하는 데 어떻게 도움이 되는지 알아봅니다. 복구 tooAzure 중 toocomplete 복잡 한 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="2e56f-104">Azure 자동화 runbook toorecovery 계획 추가</span><span class="sxs-lookup"><span data-stu-id="2e56f-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="2e56f-105">이 문서에서는 Azure Site Recovery Azure 자동화 toohelp와 통합 하는 방법을 설명 복구 계획을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="2e56f-106">복구 계획으로 Site Recovery로 보호되는 VM의 복구를 오케스트레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="2e56f-107">복구 계획에는 복제 tooa 보조 클라우드 계정과 복제 tooAzure 모두 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="2e56f-108">복구 계획 hello 복구를 만들어 줍니다 **일관 되 게 정확한**, **반복 가능한**, 및 **자동화 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="2e56f-109">를 장애 조치 Vm tooAzure Azure 자동화와의 통합에서는 복구 계획을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="2e56f-110">강력한 자동화 작업을 제공 하는 tooexecute runbook을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="2e56f-111">새 tooAzure 자동화 인 경우 다음을 할 수 있습니다 [등록](https://azure.microsoft.com/services/automation/) 및 [샘플 스크립트를 다운로드할](https://azure.microsoft.com/documentation/scripts/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="2e56f-112">대 한 자세한 내용과 toolearn 방법을 사용 하 여 tooorchestrate 복구 tooAzure [복구 계획](https://azure.microsoft.com/blog/?p=166264), 참조 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="2e56f-113">이 문서에서는 Azure Automation Runbook을 복구 계획에 어떻게 통합할 수 있는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="2e56f-114">수동 작업이 필요 했던 예제 tooautomate 기본 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="2e56f-115">어떻게 tooconvert multi-step 복구 tooa 단일 클릭 복구 작업을 설명 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="2e56f-116">Hello 복구 계획 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2e56f-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="2e56f-117">Toohello 이동 **사이트 복구** 계획 리소스 블레이드를 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="2e56f-118">예를 들어 hello 복구 계획에 복구를 위해 두 개의 Vm 추가 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="2e56f-119">runbook을 추가 하는 toobegin 클릭 hello **사용자 지정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Hello 사용자 지정 단추를 클릭 합니다.](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="2e56f-121">**그룹 1: 시작**을 마우스 오른쪽 단추로 클릭한 후 **사후 작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![그룹 1: 시작을 마우스 오른쪽 단추로 클릭하고 사후 작업 추가](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="2e56f-123">**스크립트 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="2e56f-124">Hello에 **업데이트 동작** 블레이드, 이름 hello 스크립트 **Hello World**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![hello 업데이트 작업 블레이드](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="2e56f-126">Automation 계정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="2e56f-127">모든 Azure 지역에서 자동화 계정을 hello 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="2e56f-128">자동화 계정 hello hello에 있어야 합니다. hello Azure Site Recovery 자격 증명 모음과 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="2e56f-129">Automation 계정에서 Runbook을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="2e56f-130">이 runbook은 hello 첫 번째 그룹의 hello 복구 후 hello 복구 계획의 hello 실행 하는 동안 실행 하는 hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="2e56f-131">toosave hello 스크립트 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="2e56f-132">hello 스크립트가 추가 되 고 너무**그룹 1: 사후 단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![사후 작업 그룹 1: 시작](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="2e56f-134">스크립트를 추가하기 위한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2e56f-134">Considerations for adding a script</span></span>

* <span data-ttu-id="2e56f-135">옵션에 대 한 너무**단계를 삭제** 또는 **업데이트 hello 스크립트**, hello 스크립트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="2e56f-136">스크립트를 온-프레미스 컴퓨터 tooAzure에서 장애 조치 하는 동안 Azure에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="2e56f-137">또한 실행할 있습니다 Azure에서 종료 하기 전에 기본 사이트 스크립트로 Azure tooan 온-프레미스 컴퓨터에서 장애 복구 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="2e56f-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="2e56f-138">스크립트가 실행되면 복구 계획 컨텍스트가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="2e56f-139">다음 예제는 hello 컨텍스트 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-139">hello following example shows a context variable:</span></span>

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

    <span data-ttu-id="2e56f-140">다음 표에서 hello hello 컨텍스트에서 각 변수에의 hello 이름 및 설명을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="2e56f-141">**변수 이름**</span><span class="sxs-lookup"><span data-stu-id="2e56f-141">**Variable name**</span></span> | <span data-ttu-id="2e56f-142">**설명**</span><span class="sxs-lookup"><span data-stu-id="2e56f-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="2e56f-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="2e56f-143">RecoveryPlanName</span></span> |<span data-ttu-id="2e56f-144">실행 되 고 hello 계획의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-144">hello name of hello plan being run.</span></span> <span data-ttu-id="2e56f-145">이 변수를 사용 하 여 hello 복구 계획 이름에 따라 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="2e56f-146">또한 hello 스크립트 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="2e56f-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="2e56f-147">FailoverType</span></span> |<span data-ttu-id="2e56f-148">Hello 장애 조치 인지 테스트 지정, 계획 된, 또는 계획 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="2e56f-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="2e56f-149">FailoverDirection</span></span> |<span data-ttu-id="2e56f-150">복구 tooa 기본 또는 보조 사이트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="2e56f-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="2e56f-151">GroupID</span></span> |<span data-ttu-id="2e56f-152">Hello 계획 실행 중일 때 hello 복구 계획의 hello 그룹 번호를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="2e56f-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="2e56f-153">VmMap</span></span> |<span data-ttu-id="2e56f-154">Hello 그룹의 모든 Vm의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="2e56f-155">VMMap key</span><span class="sxs-lookup"><span data-stu-id="2e56f-155">VMMap key</span></span> |<span data-ttu-id="2e56f-156">각 VM에 대한 고유 키(GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="2e56f-157">해당 되는 VM을 hello 하는 hello Azure Virtual Machine Manager (VMM) ID의 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="2e56f-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="2e56f-158">SubscriptionId</span></span> |<span data-ttu-id="2e56f-159">hello Azure 구독 ID는 hello VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="2e56f-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="2e56f-160">RoleName</span></span> |<span data-ttu-id="2e56f-161">hello 복구 중인 Azure VM의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="2e56f-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="2e56f-162">CloudServiceName</span></span> |<span data-ttu-id="2e56f-163">VM이 생성 되었고 어떤 hello에서 hello Azure 클라우드 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="2e56f-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2e56f-164">ResourceGroupName</span></span>|<span data-ttu-id="2e56f-165">hello Azure 리소스 그룹 이름은는 hello VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="2e56f-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="2e56f-166">RecoveryPointId</span></span>|<span data-ttu-id="2e56f-167">VM hello를 복구에 대 한 hello 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="2e56f-168">해당 hello 자동화 계정에 모듈을 따라 hello 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="2e56f-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="2e56f-169">AzureRM.profile</span></span>
    * <span data-ttu-id="2e56f-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="2e56f-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="2e56f-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="2e56f-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="2e56f-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="2e56f-172">AzureRM.Network</span></span>
    * <span data-ttu-id="2e56f-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="2e56f-173">AzureRM.Compute</span></span>

<span data-ttu-id="2e56f-174">모든 모듈은 호환되는 버전이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="2e56f-175">모든 모듈은 호환 되는 쉽게 tooensure toouse hello 모든 hello 모듈의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="2e56f-176">Hello VMMap 루프에서의 모든 Vm에 액세스</span><span class="sxs-lookup"><span data-stu-id="2e56f-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="2e56f-177">Hello 코드 tooloop hello Microsoft VMMap의 모든 Vm에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="2e56f-178">hello 리소스 그룹 이름 및 역할 이름 값은 hello 스크립트는 이전 tooa 부팅 그룹 경우 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="2e56f-179">hello 값은 hello 해당 그룹의 VM을 성공적으로 장애 조치 하는 경우에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="2e56f-180">hello 스크립트는 hello 부팅 그룹의 작업 후입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="2e56f-181">사용 하 여 hello 동일한 여러 복구 계획에서 자동화 runbook</span><span class="sxs-lookup"><span data-stu-id="2e56f-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="2e56f-182">단일 스크립트는 외부 변수를 사용하여 여러 복구 계획에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="2e56f-183">사용할 수 있습니다 [Azure 자동화 변수](../automation/automation-variables.md) toostore 매개 변수는 복구에 전달할 수 있는 계획 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="2e56f-184">Hello 복구 계획 이름은 접두사 toohello 변수를 추가 하 여 각 복구 계획에 대 한 개별 변수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="2e56f-185">그런 다음 hello 변수를 매개 변수로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="2e56f-186">Hello 스크립트를 변경 하지 않고 매개 변수를 변경할 수는 있지만 변경 hello 스크립트의 작동 방식으로 hello 되는 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="2e56f-187">Runbook 스크립트에서 단순 문자열 변수 사용</span><span class="sxs-lookup"><span data-stu-id="2e56f-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="2e56f-188">이 예제에서는 스크립트 hello 입력의는 보안 그룹 NSG (네트워크)을 복구 계획의 toohello Vm 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="2e56f-189">Hello 스크립트 toodetect 어떤 복구 계획이 실행 되 고, 복구 계획 컨텍스트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="2e56f-190">기존 NSG tooapply hello NSG 이름 및 hello NSG 리소스 그룹 이름을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="2e56f-191">복구 계획 스크립트에 대한 입력으로 이러한 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="2e56f-192">toodo이 자동화 계정 자산 hello에 두 개의 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="2e56f-193">접두사 toohello 변수 이름으로 hello 매개 변수를 만들고 있는 hello 복구 계획의 hello 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="2e56f-194">변수 toostore hello NSG 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="2e56f-195">Hello 복구 계획의 hello 이름을 사용 하 여 접두사 toohello 변수 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![NSG 이름 변수 만들기](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="2e56f-197">리소스 그룹 이름은 변수 toostore hello NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="2e56f-198">Hello 복구 계획의 hello 이름을 사용 하 여 접두사 toohello 변수 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![NSG 리소스 그룹 이름 만들기](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="2e56f-200">Hello 스크립트에 다음 참조 코드 tooget hello 변수 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="2e56f-201">Hello runbook tooapply hello NSG toohello 네트워크 인터페이스의 hello에 hello 변수를 사용 하 여 실패 한 VM:</span><span class="sxs-lookup"><span data-stu-id="2e56f-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="2e56f-202">각 복구 계획에 대 한 hello 스크립트를 다시 사용할 수 있도록 독립 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="2e56f-203">복구 계획 이름은 hello를 사용 하 여 접두사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="2e56f-204">이 시나리오에 대 한 완전 한 종단 간 스크립트를 참조 하십시오. [사이트 복구는 복구 계획의 테스트 장애 조치 중 공용 IP와 NSG tooVMs 추가](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="2e56f-205">자세한 내용은 복합 변수 toostore를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2e56f-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="2e56f-206">특정 Vm에서 공용 IP에서 단일 스크립트 tooturn 원하는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="2e56f-207">다른 시나리오에서는 tooapply 할 수 있습니다 (모든 Vm)에 없는 다른 Vm에서 다른 Nsg 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="2e56f-208">모든 복구 계획에 다시 사용할 수 있는 스크립트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="2e56f-209">각 복구 계획에는 다양한 수의 VM이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="2e56f-210">예를 들어 SharePoint 복구에는 두 개의 프런트 엔드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="2e56f-211">기본 LOB(기간 업무) 응용 프로그램에는 하나의 프런트 엔드만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="2e56f-212">각 복구 계획에 별도의 변수를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="2e56f-213">다음 예제는 hello,에서는 새 기법을 사용 하 고 만들는 [복합 변수](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) hello Azure 자동화 계정 자산에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="2e56f-214">여러 값을 지정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="2e56f-215">다음 단계는 Azure PowerShell toocomplete hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="2e56f-216">PowerShell에서 tooyour Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="2e56f-217">toostore hello 매개 변수는 hello 복구 계획의 hello 이름을 사용 하 여 hello 복잡 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="2e56f-218">이 복잡 한 변수에 **VMDetails** 는 hello VM 보호 된 hello VM ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="2e56f-219">hello Azure 포털에서에서 VM ID tooget hello는 hello VM 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="2e56f-220">hello 다음 스크린 샷에서 두 개의 Vm hello 세부 정보를 저장 하는 변수</span><span class="sxs-lookup"><span data-stu-id="2e56f-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![GUID hello hello VM ID 사용](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="2e56f-222">Runbook에서 이 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-222">Use this variable in your runbook.</span></span> <span data-ttu-id="2e56f-223">Hello 지정 된 경우 VM GUID를 hello 복구 계획 컨텍스트에서 찾을 수, hello VM에 NSG hello를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="2e56f-224">runbook을 hello 복구 계획 컨텍스트의 hello Vm을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="2e56f-225">Hello VM의 존재 여부 확인 **$VMDetailsObj**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="2e56f-226">이 특성이 있으면 hello 변수 tooapply hello NSG의 hello 속성에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="2e56f-227">다른 복구 계획에 대 한 hello 동일한 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="2e56f-228">다른 변수에서 tooa 복구 계획에 해당 하는 hello 값을 저장 하 여 서로 다른 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="2e56f-229">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2e56f-229">Sample scripts</span></span>

<span data-ttu-id="2e56f-230">toodeploy 샘플 스크립트 tooyour 자동화 계정을 클릭 hello **tooAzure 배포** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2e56f-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="2e56f-231">[![TooAzure 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="2e56f-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="2e56f-232">또 다른 예로, hello 다음 비디오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2e56f-232">For another example, see hello following video.</span></span> <span data-ttu-id="2e56f-233">코드를 보여 줍니다 방법을 2 계층 WordPress 응용 프로그램 tooAzure toorecover:</span><span class="sxs-lookup"><span data-stu-id="2e56f-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="2e56f-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2e56f-234">Additional resources</span></span>
* [<span data-ttu-id="2e56f-235">Azure Automation 서비스 실행 계정</span><span class="sxs-lookup"><span data-stu-id="2e56f-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="2e56f-236">Azure Automation 개요</span><span class="sxs-lookup"><span data-stu-id="2e56f-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation 개요")
* [<span data-ttu-id="2e56f-237">Azure Automation 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2e56f-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation 샘플 스크립트")
