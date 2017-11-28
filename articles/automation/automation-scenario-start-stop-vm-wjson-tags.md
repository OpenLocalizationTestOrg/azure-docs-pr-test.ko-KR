---
title: "JSON 형식 태그 tooschedule Azure VM 상태 aaaUse | Microsoft Docs"
description: "이 문서에서는 VM 시작 및 종료의 tooautomate hello 예약 태그 toouse JSON 문자열 하는 방법을 보여줍니다."
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
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="2b6b6-103">Azure 자동화 시나리오: JSON 형식를 사용 하 여 Azure VM 시작 및 종료에 대 한 일정 toocreate 태그 지정</span><span class="sxs-lookup"><span data-stu-id="2b6b6-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="2b6b6-104">고객 tooschedule hello 시작은 경우가 종종 및 toohelp 가상 컴퓨터의 종료 구독 비용을 줄이거나 비즈니스 및 기술 요구 사항을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="2b6b6-105">hello 다음과 같은 시나리오 사용 하면 tooset를 자동된 시작 및 종료 Vm의 리소스 그룹 수준 또는 Azure에서 가상 컴퓨터 수준에서 일정 라고 하는 태그를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="2b6b6-106">시작 시간과 종료 시간 일요일 tooSaturday에서이 일정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="2b6b6-107">일부의 기본 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="2b6b6-108">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-108">These include:</span></span>

* <span data-ttu-id="2b6b6-109">[가상 컴퓨터 크기 집합](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooscale / 축소를 사용할 수 있는 자동 크기 조정 설정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="2b6b6-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) 서비스 기능이 hello 기본 제공 된 시작 및 종료 작업 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="2b6b6-111">그러나 이러한 옵션 특정 시나리오를만 지원 하며 적용된 tooinfrastructure-as a service (IaaS) Vm 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="2b6b6-112">적용 된 tooa 리소스 그룹 hello 태그 일정을 사용 하는 경우 해당 리소스 그룹 내의 가상 컴퓨터 적용 된 tooall 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="2b6b6-113">일정에 따라 직접 적용 된 tooa VM 이면 hello 마지막 일정 우선 순서에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="2b6b6-114">일정 적용 된 tooa 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="2b6b6-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="2b6b6-115">적용 된 tooa 리소스 그룹 및 hello 리소스 그룹에 가상 컴퓨터를 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="2b6b6-116">적용 되는 일정 tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="2b6b6-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="2b6b6-117">이 시나리오에서 기본적으로 지정 된 형식으로 JSON 문자열을 사용 하 고 hello 값으로 추가 Schedule 이라는 태그에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="2b6b6-118">다음 runbook는 모든 리소스 그룹 및 가상 컴퓨터를 나열 하 고 앞에서 나열 된 hello 시나리오에 따라 각 VM에 대 한 hello 일정을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="2b6b6-119">다음 hello 첨부 된 일정이 있는 Vm 반복 하 고 평가 어떤 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="2b6b6-120">예를 들어 Vm 중지 하거나 종료 하거나 무시 toobe 필요한 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="2b6b6-121">이러한 runbook hello를 사용 하 여 인증 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="2b6b6-122">Hello 시나리오에 대 한 hello runbook 다운로드</span><span class="sxs-lookup"><span data-stu-id="2b6b6-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="2b6b6-123">이 시나리오 hello에서 다운로드할 수 있는 4 개의 PowerShell 워크플로 runbook 이루어져 [TechNet 갤러리](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) 또는 hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) 이 프로젝트에 대 한 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="2b6b6-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="2b6b6-124">Runbook</span></span> | <span data-ttu-id="2b6b6-125">설명</span><span class="sxs-lookup"><span data-stu-id="2b6b6-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b6b6-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="2b6b6-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="2b6b6-127">각 가상 컴퓨터 일정을 확인 하 고 종료 또는 hello 일정에 따라 시작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="2b6b6-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="2b6b6-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="2b6b6-129">Hello는 일정 태그 tooa VM 또는 리소스 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="2b6b6-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="2b6b6-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="2b6b6-131">새 항목으로 대체 하 여 hello 기존 일정 태그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="2b6b6-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="2b6b6-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="2b6b6-133">VM 또는 리소스 그룹에서 hello 일정 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="2b6b6-134">이 시나리오 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="2b6b6-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="2b6b6-135">설치 하 고 hello runbook 게시</span><span class="sxs-lookup"><span data-stu-id="2b6b6-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="2b6b6-136">Hello runbook에 다운로드 한 후에 가져올 수의 hello 절차를 사용 하 여 [만들기 또는 Azure 자동화에서 runbook을 가져와](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="2b6b6-137">각 Runbook을 자동화 계정으로 가져온 후에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="2b6b6-138">일정 toohello ResourceSchedule 테스트 runbook을 추가</span><span class="sxs-lookup"><span data-stu-id="2b6b6-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="2b6b6-139">이러한 단계 tooenable hello hello 테스트 ResourceSchedule runbook에 대 한 일정에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="2b6b6-140">가상 컴퓨터를 시작 해야 함, 종료, 확인 하는 hello runbook 또는 왼쪽 그대로입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="2b6b6-141">Hello Azure 포털에서에서 자동화 계정을 열고 hello 클릭 **Runbook** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="2b6b6-142">Hello에 **테스트 ResourceSchedule** 블레이드에서 hello 클릭 **일정** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="2b6b6-143">Hello에 **일정** 블레이드에서 클릭 **일정을 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="2b6b6-144">Hello에 **일정** 블레이드를 **일정 tooyour runbook을 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="2b6b6-145">그런 다음 **새 일정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="2b6b6-146">Hello에 **새 일정** 블레이드에서 hello 이름에이 일정을 유형의 예를 들어: *HourlyExecution*합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="2b6b6-147">Hello 일정에 대 한 **시작**, hello 시작 시간 tooan 시간 증분을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="2b6b6-148">**되풀이**를 선택한 다음 **되풀이 간격**에서 **1시간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="2b6b6-149">되어 있는지 확인 **세트 만료** 너무 설정**아니요**, 클릭 하 고 **만들기** toosave 새 일정.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="2b6b6-150">Hello에 **일정 Runbook** 옵션 블레이드에서 **매개 변수 및 실행된 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="2b6b6-151">테스트 ResourceSchedule hello에 **매개 변수** 블레이드에서 hello에 구독 hello 이름을 입력 **SubscriptionName** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="2b6b6-152">이 hello runbook에 대 한 필요한 hello 유일한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="2b6b6-153">작업을 완료하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="2b6b6-154">완료 되 면 hello runbook 일정 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![구성된 Test-ResourceSchedule Runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="2b6b6-156">형식 hello JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="2b6b6-156">Format hello JSON string</span></span>
<span data-ttu-id="2b6b6-157">기본적으로이 솔루션은 JSON으로 지정된 된 형식으로 문자열을 태그에 대 한 hello 값으로 추가 일정을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="2b6b6-158">다음 runbook는 모든 리소스 그룹 및 가상 컴퓨터를 나열 하 고 각 가상 컴퓨터에 대 한 hello 일정을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="2b6b6-159">hello runbook hello 가상 컴퓨터를 연결 하는 일정을 반복 하 고 어떤 조치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="2b6b6-160">hello 다음은 hello 솔루션 포맷할 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-160">hello following is an example of how hello solutions should be formatted:</span></span>

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

<span data-ttu-id="2b6b6-161">이 구조에 대한 자세한 정보 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="2b6b6-162">hello이 JSON 구조 형식이 최적화 toowork Azure에서 단일 태그 값의 hello 256 자 제한 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="2b6b6-163">*TzId* hello 가상 컴퓨터의 표준 시간대를 hello 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="2b6b6-164">PowerShell 세션-의 hello TimeZoneInfo.NET 클래스를 사용 하 여이 ID를 가져올 수 있습니다**[System.TimeZoneInfo]:: GetSystemTimeZones()**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![PowerShell의 GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="2b6b6-166">평일 0 toosix의 숫자 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="2b6b6-167">hello 값 0은 일요일을 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="2b6b6-168">hello 시작 시간으로 표시 됩니다 hello **S** 특성과 해당 값은 24 시간 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="2b6b6-169">hello 끝 또는 종료 시간 표현 됩니다 hello로 **E** 특성과 해당 값은 24 시간 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="2b6b6-170">경우 hello **S** 및 **E** 각 특성에는 영 (0)의 값은, 평가 hello 시 hello 가상 컴퓨터를 현재 상태에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="2b6b6-171">Hello 주의 특정 요일에 대 한 tooskip 평가 하려는 경우 hello 주의 해당 요일에 대 한 섹션을 추가 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="2b6b6-172">Hello에 다음 예제에서는 월요일만 평가 되 고 hello hello 요일을 다른 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="2b6b6-173">리소스 그룹 또는 VM 태그 지정</span><span class="sxs-lookup"><span data-stu-id="2b6b6-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="2b6b6-174">Vm 아래로 tooshut, 해야 tootag hello Vm 또는는 날짜별 hello 리소스 그룹 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="2b6b6-175">Schedule 태그가 없는 가상 컴퓨터는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="2b6b6-176">따라서 시작되거나 종료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="2b6b6-177">이 솔루션에 두 가지 방법으로 tootag 리소스 그룹 또는 Vm 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="2b6b6-178">Hello 포털에서 직접 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="2b6b6-179">또는 hello ResourceSchedule 추가, 업데이트-ResourceSchedule 및 제거 ResourceSchedule runbook을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="2b6b6-180">Hello 포털을 통해 태그</span><span class="sxs-lookup"><span data-stu-id="2b6b6-180">Tag through hello portal</span></span>
<span data-ttu-id="2b6b6-181">이러한 단계 tootag 가상 컴퓨터 또는 hello 포털에서 리소스 그룹을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="2b6b6-182">Hello JSON 문자열을 결합 하 고 공백이 되지 해당 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="2b6b6-183">JSON 문자열은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="2b6b6-184">선택 hello **태그** VM 또는 리소스에 대 한 아이콘 그룹 tooapply이이 일정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![VM 태그 옵션](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="2b6b6-186">태그는 다음 키/값 쌍으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="2b6b6-187">형식 **일정** hello에 **키** 필드를 선택한 다음 hello에 hello JSON 문자열을 붙여 **값** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="2b6b6-188">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-188">Click **Save**.</span></span> <span data-ttu-id="2b6b6-189">이제 새 태그를 리소스에 대 한 태그의 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![VM Schedule 태그](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="2b6b6-191">PowerShell에서 태그 지정</span><span class="sxs-lookup"><span data-stu-id="2b6b6-191">Tag from PowerShell</span></span>
<span data-ttu-id="2b6b6-192">가져온된 모든 runbook tooexecute PowerShell에서 직접 runbook hello 하는 방법을 설명 하는 hello 스크립트의 hello 시작 부분에 도움말 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="2b6b6-193">PowerShell에서 hello ScheduleResource 추가 및 업데이트 ScheduleResource runbook을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="2b6b6-194">Hello 포털 외부에서 VM 또는 리소스 그룹에 toocreate 또는 업데이트 hello 일정 태그 수 있는 필수 매개 변수를 전달 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="2b6b6-195">먼저 너무 toocreate, 추가 및 PowerShell 통해 태그를 삭제,[Azure에 대 한 PowerShell 환경을 설정](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="2b6b6-196">Hello 설치를 완료 한 후 단계를 수행 하는 hello를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="2b6b6-197">PowerShell을 사용하여 Schedule 태그 만들기</span><span class="sxs-lookup"><span data-stu-id="2b6b6-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="2b6b6-198">PowerShell 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-198">Open a PowerShell session.</span></span> <span data-ttu-id="2b6b6-199">다음 예제에서는 tooauthenticate 실행 계정 및 구독 toospecify hello를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="2b6b6-200">일정 해시 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-200">Define a schedule hash table.</span></span> <span data-ttu-id="2b6b6-201">다음은 생성 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="2b6b6-202">Hello runbook에 필요한 hello 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="2b6b6-203">다음 예제는 hello, VM 대상:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="2b6b6-204">리소스 그룹을 태그 지정 하는 경우 제거 hello *VMName* hello $params 해시에서 매개 변수는 다음과 같이 테이블:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="2b6b6-205">매개 변수 toocreate hello 일정 태그 뒤 hello로 추가 ResourceSchedule hello runbook을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="2b6b6-206">리소스 그룹 또는 가상 컴퓨터 태그 tooupdate 실행 hello **업데이트 ResourceSchedule** runbook 매개 변수 뒤 hello로:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="2b6b6-207">PowerShell을 사용하여 Schedule 태그 삭제</span><span class="sxs-lookup"><span data-stu-id="2b6b6-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="2b6b6-208">PowerShell 세션을 열고 하 고 다음 실행 계정 및 tooselect tooauthenticate hello를 실행 한 구독을 지정:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="2b6b6-209">Hello runbook에 필요한 hello 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="2b6b6-210">다음 예제는 hello, VM 대상:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="2b6b6-211">리소스 그룹에서 태그를 제거 하는 경우 제거 hello *VMName* hello $params 해시에서 매개 변수는 다음과 같이 테이블:</span><span class="sxs-lookup"><span data-stu-id="2b6b6-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="2b6b6-212">Hello 제거 ResourceSchedule runbook tooremove hello 일정 태그를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="2b6b6-213">tooupdate 리소스 그룹 또는 가상 컴퓨터 태그를 매개 변수 뒤 hello로 hello 제거 ResourceSchedule runbook을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="2b6b6-214">사전를 모니터링 되는 가상 컴퓨터 tooverify 종료 이러한 runbook (및 hello 가상 컴퓨터 상태)을 권장 하 고 적절 하 게 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="2b6b6-215">hello 테스트 ResourceSchedule runbook의 tooview hello 세부 정보 선택 hello Azure 포털에서 hello 작업 **작업** hello runbook의 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="2b6b6-216">hello 작업 요약 표시 hello 입력된 매개 변수 및 hello 출력 스트림, 또한 hello 작업에 대 한 toogeneral 정보 및 예외 발생 한 경우.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="2b6b6-217">hello **작업 요약** hello 출력, 경고 및 오류 스트림에서 메시지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="2b6b6-218">선택 hello **출력** tooview 타일 hello runbook 실행의 결과 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Test-ResourceSchedule 출력](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="2b6b6-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b6b6-220">Next steps</span></span>
* <span data-ttu-id="2b6b6-221">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="2b6b6-222">runbook 형식이 장점 및 제한 사항에 대해 자세히 toolearn 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="2b6b6-223">PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="2b6b6-224">runbook 로깅이 및 출력에 대해 자세히 toolearn 참조 [Runbook 출력 및 메시지 Azure 자동화에서](automation-runbook-output-and-messages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="2b6b6-225">Azure 실행 계정 및 tooauthenticate runbook을 사용 하 여 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 toolearn [Azure 실행 계정 사용 하 여 runbook을 인증](automation-sec-configure-azure-runas-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6b6-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
