---
title: "JSON 형식 태그를 사용하여 Azure VM 상태 예약 | Microsoft Docs"
description: "이 문서에서는 태그에 JSON 문자열을 사용하여 VM 시작 및 종료 예약을 자동화하는 방법을 보여 줍니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="e082d-103">Azure 자동화 시나리오: JSON 형식 태그를 사용하여 Azure VM 시작 및 종료 일정 만들기</span><span class="sxs-lookup"><span data-stu-id="e082d-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="e082d-104">고객은 종종 가상 컴퓨터의 시작 및 종료를 예약하여 구독 비용을 절감하거나 비즈니스 및 기술 요구 사항을 지원하는 데 도움을 주려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="e082d-105">다음 시나리오에서는 Azure의 리소스 그룹 수준 또는 가상 컴퓨터 수준에서 일정이라는 태그를 사용하여 VM의 자동화된 시작 및 종료를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="e082d-106">이 일정은 시작 시간 및 종료 시간을 사용하여 일요일부터 토요일까지 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="e082d-107">일부의 기본 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="e082d-108">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-108">These include:</span></span>

* <span data-ttu-id="e082d-109">[가상 컴퓨터 크기 조정 설정](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) 입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="e082d-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) 서비스에는 시작 및 종료 작업을 예약하는 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="e082d-111">그러나 이러한 옵션은 특정 시나리오만 지원하고 IaaS(infrastructure-as-a-service) VM에 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="e082d-112">리소스 그룹에는 Schedule 태그를 적용하는 경우 해당 리소스 그룹 내의 모든 가상 컴퓨터에도 해당 태그가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="e082d-113">일정이 VM에 직접 적용될 경우 마지막 일정이 다음과 같은 순서로 먼저 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="e082d-114">리소스 그룹에 적용된 일정</span><span class="sxs-lookup"><span data-stu-id="e082d-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="e082d-115">리소스 그룹 및 리소스 그룹의 가상 컴퓨터에 적용된 일정</span><span class="sxs-lookup"><span data-stu-id="e082d-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="e082d-116">가상 컴퓨터에 적용된 일정</span><span class="sxs-lookup"><span data-stu-id="e082d-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="e082d-117">이 시나리오에서는 기본적으로 지정된 형식의 JSON 문자열을 가져온 후 Schedule이라는 태그의 값으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="e082d-118">그런 다음 Runbook은 모든 리소스 그룹 및 가상 컴퓨터를 나열하고 앞서 나열한 시나리오에 따라 각 VM에 대한 일정을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="e082d-119">다음으로 연결된 일정이 있는 VM을 반복하고 어떤 조치 취할지 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="e082d-120">예를 들어 중지, 종료 또는 무시해야 하는 VM을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="e082d-121">이러한 Runbook은 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="e082d-122">시나리오에 대한 Runbook 다운로드</span><span class="sxs-lookup"><span data-stu-id="e082d-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="e082d-123">이 시나리오는 이 프로젝트에 대한 [TechNet 갤러리](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) 또는 [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) 저장소에서 다운로드할 수 있는 4개의 PowerShell 워크플로 Runbook으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="e082d-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="e082d-124">Runbook</span></span> | <span data-ttu-id="e082d-125">설명</span><span class="sxs-lookup"><span data-stu-id="e082d-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e082d-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e082d-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="e082d-127">각 가상 컴퓨터의 일정을 확인하고 일정에 따라 종료 또는 시작을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="e082d-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e082d-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="e082d-129">Schedule 태그를 VM 또는 리소스 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="e082d-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e082d-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="e082d-131">기존 Schedule 태그를 새 태그로 바꾸어 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="e082d-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="e082d-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="e082d-133">VM 또는 리소스 그룹에서 Schedule 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="e082d-134">이 시나리오 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="e082d-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="e082d-135">Runbook 설치 및 게시</span><span class="sxs-lookup"><span data-stu-id="e082d-135">Install and publish the runbooks</span></span>
<span data-ttu-id="e082d-136">Runbook을 다운로드한 후에 [Azure 자동화에서 Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)의 절차를 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="e082d-137">각 Runbook을 자동화 계정으로 가져온 후에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="e082d-138">Test-ResourceSchedule Runbook에 일정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="e082d-139">다음 단계에 따라 Test-ResourceSchedule Runbook에 대한 일정을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="e082d-140">시작, 종료하거나 그대로 유지해야 하는 가상 컴퓨터를 확인하는 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="e082d-141">Azure 포털에서 자동화 계정을 열고 **Runbook** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="e082d-142">**Test-ResourceSchedule** 블레이드에서 **일정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="e082d-143">**일정** 블레이드에서 **일정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="e082d-144">**일정** 블레이드에서 **Runbook에 일정 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="e082d-145">그런 다음 **새 일정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="e082d-146">**새 일정** 블레이드에서 이 일정의 이름(예: *HourlyExecution*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="e082d-147">일정 **시작**은 시작 시간을 시간 증분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="e082d-148">**되풀이**를 선택한 다음 **되풀이 간격**에서 **1시간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="e082d-149">**만료 설정**이 **아니요**로 설정되어 있는지 확인한 후 **만들기**를 클릭하여 새 일정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="e082d-150">**일정 Runbook** 옵션 블레이드에서 **매개 변수 및 실행 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="e082d-151">Test-ResourceSchedule **매개 변수** 블레이드의 **SubscriptionName** 필드에 구독 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="e082d-152">Runbook에는 이 매개 변수만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="e082d-153">작업을 완료하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="e082d-154">완료되면 Runbook 일정은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-154">The runbook schedule should look like the following when it's completed:</span></span>

![구성된 Test-ResourceSchedule Runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="e082d-156">JSON 문자열의 형식 지정</span><span class="sxs-lookup"><span data-stu-id="e082d-156">Format the JSON string</span></span>
<span data-ttu-id="e082d-157">이 솔루션은 기본적으로 지정된 형식의 JSON 문자열을 가져온 후 Schedule이라는 태그의 값으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="e082d-158">그런 다음 Runbook은 모든 리소스 그룹 및 가상 컴퓨터를 나열하고 각 가상 컴퓨터에 대한 일정을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="e082d-159">Runbook은 일정이 연결된 가상 컴퓨터를 반복하고 어떤 조치를 취해야 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="e082d-160">다음은 솔루션의 서식을 지정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-160">The following is an example of how the solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="e082d-161">이 구조에 대한 자세한 정보 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="e082d-162">이 JSON 구조의 형식은 Azure의 단일 태그 값에 대한 256자 제한을 해결하도록 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="e082d-163">*TzId* 는 가상 컴퓨터의 표준 시간대를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="e082d-164">이 ID는 PowerShell 세션에서 TimeZoneInfo .NET 클래스를 사용하여 구할 수 있습니다.--**[System.TimeZoneInfo]::GetSystemTimeZones()**</span><span class="sxs-lookup"><span data-stu-id="e082d-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![PowerShell의 GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="e082d-166">요일은 0에서 6의 숫자 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="e082d-167">값 0은 일요일입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="e082d-168">시작 시간은 **S** 특성으로 표시되고 해당 값은 24시간 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="e082d-169">끝 또는 종료 시간은 **E** 특성으로 표시되고 해당 값은 24시간 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="e082d-170">**S** 및 **E** 특성 값이 각각 0인 경우 가상 컴퓨터는 평가 시의 현재 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="e082d-171">특정 요일에 대한 평가를 생략하려면 해당 요일의 섹션을 추가하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e082d-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="e082d-172">다음 예제에서는 월요일만 평가되고 다른 요일은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="e082d-173">리소스 그룹 또는 VM 태그 지정</span><span class="sxs-lookup"><span data-stu-id="e082d-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="e082d-174">VM을 종료하려면 VM 또는 리소스 그룹이 위치한 곳에서 해당 항목의 태그를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="e082d-175">Schedule 태그가 없는 가상 컴퓨터는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="e082d-176">따라서 시작되거나 종료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="e082d-177">이 솔루션을 포함한 리소스 그룹 또는 VM의 태그를 지정하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="e082d-178">포털에서 직접 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-178">You can do it directly from the portal.</span></span> <span data-ttu-id="e082d-179">또는 Add-ResourceSchedule, Update-ResourceSchedule 및 Remove-ResourceSchedule Runbook을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="e082d-180">포털을 통해 태그 지정</span><span class="sxs-lookup"><span data-stu-id="e082d-180">Tag through the portal</span></span>
<span data-ttu-id="e082d-181">다음은 포털에서 가상 컴퓨터 또는 리소스 그룹에 태그를 지정하는 작업 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="e082d-182">JSON 문자열을 평면화하고 공백이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="e082d-183">JSON 문자열은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="e082d-184">VM 또는 리소스 그룹에 대한 **태그** 아이콘을 선택하여 이 일정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![VM 태그 옵션](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="e082d-186">태그는 다음 키/값 쌍으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="e082d-187">**키** 필드에 **일정**을 입력한 다음 JSON 문자열을 **값** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="e082d-188">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-188">Click **Save**.</span></span> <span data-ttu-id="e082d-189">이제 리소스에 대한 태그 목록에 새 태그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![VM Schedule 태그](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="e082d-191">PowerShell에서 태그 지정</span><span class="sxs-lookup"><span data-stu-id="e082d-191">Tag from PowerShell</span></span>
<span data-ttu-id="e082d-192">가져온 모든 Runbook은 스크립트 맨 처음에 PowerShell에서 직접 Runbook을 실행하는 방법을 설명하는 도움말 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="e082d-193">PowerShell에서 Add-ScheduleResource 및 Update-ScheduleResource Runbook을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="e082d-194">포털 외부에서 VM 또는 리소스 그룹에 Schedule 태그를 만들거나 업데이트할 수 있도록 하는 필수 매개 변수를 전달하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="e082d-195">PowerShell을 통해 태그를 만들고 추가 및 삭제하려면 먼저 [Azure에 맞게 PowerShell 환경](/powershell/azure/overview)을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="e082d-196">설정을 완료한 후에 다음 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="e082d-197">PowerShell을 사용하여 Schedule 태그 만들기</span><span class="sxs-lookup"><span data-stu-id="e082d-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="e082d-198">PowerShell 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-198">Open a PowerShell session.</span></span> <span data-ttu-id="e082d-199">다음 예제를 사용하여 실행 계정으로 인증하고 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="e082d-200">일정 해시 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-200">Define a schedule hash table.</span></span> <span data-ttu-id="e082d-201">다음은 생성 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="e082d-202">Runbook에 필요한 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="e082d-203">다음 예제에서는 VM을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="e082d-204">리소스 그룹에 태그를 지정하려는 경우 다음과 같이 $params 해시 테이블에서 *VMName* 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="e082d-205">다음 매개 변수로 Add-ResourceSchedule Runbook을 실행하여 Schedule 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="e082d-206">리소스 그룹 또는 가상 컴퓨터 태그를 업데이트하려면 다음 매개 변수로 **Update-ResourceSchedule** Runbook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="e082d-207">PowerShell을 사용하여 Schedule 태그 삭제</span><span class="sxs-lookup"><span data-stu-id="e082d-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="e082d-208">PowerShell 세션을 열고 다음을 실행하여 실행 계정으로 인증하고 구독을 선택하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="e082d-209">Runbook에 필요한 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="e082d-210">다음 예제에서는 VM을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="e082d-211">리소스 그룹에서 태그를 제거하려는 경우 다음과 같이 $params 해시 테이블에서 *VMName* 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="e082d-212">Remove-ResourceSchedule Runbook을 실행하여 Schedule 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="e082d-213">리소스 그룹 또는 가상 컴퓨터 태그를 업데이트하려면 다음 매개 변수로 Remove-ResourceSchedule Runbook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="e082d-214">이러한 Runbook(및 가상 컴퓨터 상태)을 사전에 모니터링하여 가상 컴퓨터가 적절히 종료 및 시작되고 있는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="e082d-215">Azure 포털에서 Test-ResourceSchedule Runbook 작업의 세부 정보를 보려면 Runbook의 **작업** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="e082d-216">작업 요약은 작업 및 발생하는 모든 예외에 대한 일반 정보 외에도 입력 매개 변수 및 출력 스트림을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="e082d-217">**작업 요약** 은 출력, 경고 및 오류 스트림의 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="e082d-218">Runbook 실행의 자세한 결과를 보려면 **출력** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e082d-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Test-ResourceSchedule 출력](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="e082d-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e082d-220">Next steps</span></span>
* <span data-ttu-id="e082d-221">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e082d-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="e082d-222">Runbook 형식, 해당 장점 및 제한 사항에 대해 자세히 알아보려면 [Azure 자동화 Runbook 형식](automation-runbook-types.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e082d-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="e082d-223">PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e082d-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="e082d-224">Runbook 로깅 및 출력에 대한 자세한 내용은 [Azure 자동화에서 Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e082d-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="e082d-225">Azure 실행 계정 및 이 계정을 사용하여 Runbook을 인증하는 방법에 대한 자세한 내용은 [Azure 실행 계정으로 Runbook 인증](automation-sec-configure-azure-runas-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e082d-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
