---
title: "Azure 자동화에서 runbook aaaStarting | Microsoft Docs"
description: "Azure 자동화에서 runbook을 사용 하는 toostart 수 있으며 모두 사용 하 여에 대 한 내용은 hello Azure 포털 및 Windows PowerShell을 제공 하는 hello 다른 메서드를 요약 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="1aa58-103">Azure Automation에서 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="1aa58-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="1aa58-104">다음 표에서 hello hello 메서드 toostart 가장 적합 한 tooyour 특정 시나리오는 Azure 자동화에서 runbook을 결정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="1aa58-105">이 문서에는 hello Azure 포털 및 Windows PowerShell로 runbook 시작에 대 한 내용은 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="1aa58-106">세부 정보 아래 hello 링크에서 액세스할 수 있는 기타 문서에 hello에 다른 메서드가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="1aa58-107">**방법**</span><span class="sxs-lookup"><span data-stu-id="1aa58-107">**METHOD**</span></span> | <span data-ttu-id="1aa58-108">**특성**</span><span class="sxs-lookup"><span data-stu-id="1aa58-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="1aa58-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1aa58-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="1aa58-110">대화형 사용자 인터페이스를 사용하는 간단한 방법</span><span class="sxs-lookup"><span data-stu-id="1aa58-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="1aa58-111">폼 tooprovide 간단한 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="1aa58-112">작업 상태를 쉽게 추적</span><span class="sxs-lookup"><span data-stu-id="1aa58-112">Easily track job state.</span></span><br> <li><span data-ttu-id="1aa58-113">Azure 로그온을 사용하여 액세스 인증</span><span class="sxs-lookup"><span data-stu-id="1aa58-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="1aa58-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1aa58-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="1aa58-115">Windows PowerShell cmdlet을 사용하여 명령줄에서 호출</span><span class="sxs-lookup"><span data-stu-id="1aa58-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="1aa58-116">여러 단계로 구성된 자동화된 솔루션에 포함할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1aa58-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="1aa58-117">인증서 또는 OAuth 사용자 계정/서비스 보안 주체를 사용하여 요청 인증</span><span class="sxs-lookup"><span data-stu-id="1aa58-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="1aa58-118">단순한 매개 변수 값 및 복잡한 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="1aa58-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="1aa58-119">작업 상태 추적</span><span class="sxs-lookup"><span data-stu-id="1aa58-119">Track job state.</span></span><br> <li><span data-ttu-id="1aa58-120">클라이언트는 toosupport PowerShell cmdlet을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="1aa58-121">Azure Automation API</span><span class="sxs-lookup"><span data-stu-id="1aa58-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="1aa58-122">가장 유연하지만 가장 복잡한 방법</span><span class="sxs-lookup"><span data-stu-id="1aa58-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="1aa58-123">HTTP 요청을 수행할 수 있는 모든 사용자 지정 코드에서 호출</span><span class="sxs-lookup"><span data-stu-id="1aa58-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="1aa58-124">인증서 또는 OAuth 사용자 계정/서비스 보안 주체를 사용하여 요청 인증</span><span class="sxs-lookup"><span data-stu-id="1aa58-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="1aa58-125">단순한 매개 변수 값 및 복잡한 매개 변수 값 제공</span><span class="sxs-lookup"><span data-stu-id="1aa58-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="1aa58-126">작업 상태 추적</span><span class="sxs-lookup"><span data-stu-id="1aa58-126">Track job state.</span></span> |
| [<span data-ttu-id="1aa58-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="1aa58-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="1aa58-128">단일 HTTP 요청에서 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="1aa58-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="1aa58-129">URL의 보안 토큰으로 인증</span><span class="sxs-lookup"><span data-stu-id="1aa58-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="1aa58-130">Webhook를 만들 때 지정된 매개 변수 값을 클라이언트에서 재정의할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1aa58-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="1aa58-131">Runbook은 hello HTTP 요청 세부 정보로 채워진 단일 매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="1aa58-132">Webhook URL 통해 없음 기능 tootrack 작업 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="1aa58-133">TooAzure 경고에 응답</span><span class="sxs-lookup"><span data-stu-id="1aa58-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="1aa58-134">응답 tooAzure 경고에서 runbook을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="1aa58-135">Runbook에 대 한 webhook을 구성 하 고 tooalert를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="1aa58-136">URL의 보안 토큰으로 인증</span><span class="sxs-lookup"><span data-stu-id="1aa58-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="1aa58-137">일정</span><span class="sxs-lookup"><span data-stu-id="1aa58-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="1aa58-138">매시간, 매일, 매주 또는 매월 일정에 따라 Runbook을 자동으로 시작</span><span class="sxs-lookup"><span data-stu-id="1aa58-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="1aa58-139">Azure Portal, PowerShell cmdlet 또는 Azure API를 통해 일정 조작</span><span class="sxs-lookup"><span data-stu-id="1aa58-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="1aa58-140">일정에 함께 사용 되는 매개 변수 값 toobe를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="1aa58-141">다른 Runbook에서</span><span class="sxs-lookup"><span data-stu-id="1aa58-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="1aa58-142">Runbook을 다른 Runbook의 활동으로 사용</span><span class="sxs-lookup"><span data-stu-id="1aa58-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="1aa58-143">여러 Runbook에서 사용하는 기능에 유용</span><span class="sxs-lookup"><span data-stu-id="1aa58-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="1aa58-144">매개 변수 값 toochild runbook을 제공 하 고 부모 runbook에서 출력을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="1aa58-145">hello 다음 이미지에서는 자세한 단계별 프로세스는 runbook의 hello 수명 주기에서</span><span class="sxs-lookup"><span data-stu-id="1aa58-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="1aa58-146">다른 방법으로 Azure 자동화에서 runbook 시작 Hybrid Runbook Worker tooexecute Azure 자동화 runbook 및 여러 구성 요소 간의 상호 작용에 필요한 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="1aa58-147">데이터 센터를에서 자동화 runbook을 실행 하는 방법에 대 한 toolearn 너무 참조[hybrid runbook worker](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="1aa58-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook 아키텍처](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="1aa58-149">Azure 포털 hello로 runbook 시작</span><span class="sxs-lookup"><span data-stu-id="1aa58-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="1aa58-150">Hello Azure 포털에서에서 선택 **자동화** 다음 자동화 계정 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="1aa58-151">Hello 허브 메뉴에서 선택 **Runbook**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="1aa58-152">Hello에 **Runbook** 블레이드에서 runbook을 선택 하 고 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="1aa58-153">Hello runbook에 매개 변수가 있으면 각 매개 변수에 대 한 텍스트 상자를 사용 하 여 증명된 tooprovide 값 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="1aa58-154">매개 변수에 대한 자세한 내용은 아래의 [Runbook 매개 변수](#Runbook-parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa58-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="1aa58-155">Hello에 **작업** 블레이드에서 hello runbook 작업의 hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="1aa58-156">Windows PowerShell을 사용하여 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="1aa58-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="1aa58-157">Hello를 사용할 수 있습니다 [시작 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart Windows PowerShell로 runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="1aa58-158">hello 다음 샘플 코드 시작 runbook 테스트 Runbook을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="1aa58-159">사용할 수 있는 tootrack 상태 hello runbook이 시작 된 후 개체를 작업 시작 AzureRmAutomationRunbook 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="1aa58-160">이 작업 개체를 사용할 수 있습니다 [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) hello 작업의 toodetermine hello 상태 및 [Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="1aa58-161">다음 샘플 코드는 hello Runbook을 완료 된 다음 해당 출력을 표시 될 때까지 기다린 호출 되는 runbook을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="1aa58-162">Hello runbook에 매개 변수가 필요한 경우와 같이 제공 해야 합니다는 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) hello 매개 변수 값은 hello 매개 변수 이름과 hello 값 hello 해시 테이블의 hello 키와 일치 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="1aa58-163">hello 다음 예제에서는 toostart 두 문자열 매개 변수를 사용 하 여 runbook의 이름을 지정 방법 FirstName 및 LastName, RepeatCount 라는 정수 및 Show 라는 부울 매개 변수</span><span class="sxs-lookup"><span data-stu-id="1aa58-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="1aa58-164">매개 변수에 대한 자세한 내용은 아래의 [Runbook 매개 변수](#Runbook-parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa58-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="1aa58-165">Runbook 매개 변수</span><span class="sxs-lookup"><span data-stu-id="1aa58-165">Runbook parameters</span></span>
<span data-ttu-id="1aa58-166">Hello Azure 포털 또는 Windows PowerShell에서 runbook을 시작할 때 hello 명령이 hello Azure 자동화 웹 서비스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="1aa58-167">이 서비스는 복잡한 데이터 형식을 가진 매개 변수를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="1aa58-168">Tooprovide 값 복잡 한 매개 변수를 사용 해야 경우 있습니다 인라인으로 호출 해야 다른 runbook에서에 설명 된 대로 [Azure 자동화에서 자식 runbook](automation-child-runbooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="1aa58-169">hello Azure 자동화 웹 서비스는 hello 다음 섹션에에서 설명 된 대로 특정 데이터 형식을 사용 하 여 매개 변수에 대 한 특별 한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="1aa58-170">명명된 값</span><span class="sxs-lookup"><span data-stu-id="1aa58-170">Named values</span></span>
<span data-ttu-id="1aa58-171">Hello 매개 변수가 [object] 데이터 형식인 경우 hello 다음 JSON 형식을 toosend 것 목록은 명명 된 값을 사용할 수 있습니다: *{Name1: 'Value1', Name2: 'Value2', Name3: 'Value3'}*합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="1aa58-172">이러한 값은 단순한 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-172">These values must be simple types.</span></span> <span data-ttu-id="1aa58-173">hello runbook으로 hello 매개 변수를 받게 됩니다는 [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) tooeach 명명 된 값을 해당 하는 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="1aa58-174">Hello를 사용자 라는 매개 변수를 허용 하는 테스트 runbook을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="1aa58-175">hello 다음 텍스트를 사용할 수 hello user 매개 변수에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="1aa58-176">이 인해 hello 출력을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="1aa58-177">배열</span><span class="sxs-lookup"><span data-stu-id="1aa58-177">Arrays</span></span>
<span data-ttu-id="1aa58-178">Hello 매개 변수가 [array]와 같은 배열이 면 또는 [string []]를 사용 하 여 hello JSON 형식 toosend 다음 그 값 목록이: *[Value1, Value2, Value3]*합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="1aa58-179">이러한 값은 단순한 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-179">These values must be simple types.</span></span>

<span data-ttu-id="1aa58-180">Hello 다음 테스트 runbook을 호출 하는 매개 변수를 허용 하는 것이 좋습니다 *사용자*합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="1aa58-181">hello 다음 텍스트를 사용할 수 hello user 매개 변수에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="1aa58-182">이 인해 hello 출력을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="1aa58-183">자격 증명</span><span class="sxs-lookup"><span data-stu-id="1aa58-183">Credentials</span></span>
<span data-ttu-id="1aa58-184">Hello 매개 변수 데이터 형식이 면 **PSCredential**, Azure 자동화의 hello 이름을 제공할 수 있습니다 [자격 증명 자산](automation-credentials.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="1aa58-185">hello runbook 지정 하는 hello 이름의 hello 자격 증명을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="1aa58-186">Hello를 라는 자격 증명 매개 변수를 허용 하는 테스트 runbook을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="1aa58-187">hello 다음 텍스트에 사용 될 수 있다고 가정할 때 이라는 자격 증명 자산이 hello user 매개 변수에 *내 자격 증명*합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="1aa58-188">Hello 자격 증명의 사용자 이름 hello 가정함 *jsmith*,이 인해 hello 다음 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="1aa58-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1aa58-189">Next steps</span></span>
* <span data-ttu-id="1aa58-190">현재 문서의 hello runbook 아키텍처는 Azure 및 온-프레미스 하이브리드 Runbook 작업자 hello로에서 리소스 관리는 runbook의 대략적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="1aa58-191">데이터 센터를에서 자동화 runbook을 실행 하는 방법에 대 한 toolearn 너무 참조[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="1aa58-192">특정 또는 일반 함수에 대 한 다른 runbook에서 사용 되는 모듈식 runbook toobe 만드는 hello에 대 한 자세한 toolearn 너무 참조[자식 Runbook](automation-child-runbooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa58-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

