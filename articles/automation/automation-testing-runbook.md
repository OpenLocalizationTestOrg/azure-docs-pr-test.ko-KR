---
title: "Azure 자동화에서 Runbook 테스트 | Microsoft Docs"
description: "Azure 자동화에서 Runbook을 게시하기 전에 테스트하여 예상대로 작동하는지 확인할 수 있습니다.  이 문서에서는 Runbook을 테스트하고 해당 출력을 보는 방법에 대해 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 5186eb8f1732d533cbceb397b4d8b5224ad773cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a><span data-ttu-id="39e62-104">Azure 자동화에서 Runbook 테스트</span><span class="sxs-lookup"><span data-stu-id="39e62-104">Testing a runbook in Azure Automation</span></span>
<span data-ttu-id="39e62-105">Runbook을 테스트할 때 [초안 버전](automation-creating-importing-runbook.md#publishing-a-runbook) 이 실행되며 해당 Runbook에서 수행하는 모든 작업이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-105">When you test a runbook, the [Draft version](automation-creating-importing-runbook.md#publishing-a-runbook) is executed and any actions that it performs are completed.</span></span> <span data-ttu-id="39e62-106">작업 기록은 만들어지지 않지만 [출력](automation-runbook-output-and-messages.md#output-stream)과 [경고 및 오류](automation-runbook-output-and-messages.md#message-streams) 스트림은 테스트 출력 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-106">No job history is created, but the [Output](automation-runbook-output-and-messages.md#output-stream) and [Warning and Error](automation-runbook-output-and-messages.md#message-streams) streams are displayed in the Test output Pane.</span></span> <span data-ttu-id="39e62-107">[자세한 정보 스트림](automation-runbook-output-and-messages.md#message-streams)에 대한 메시지는 [$VerbosePreference 변수](automation-runbook-output-and-messages.md#preference-variables)가 Continue로 설정되는 경우에만 출력 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-107">Messages to the [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) are displayed in the Output Pane only if the [$VerbosePreference variable](automation-runbook-output-and-messages.md#preference-variables) is set to Continue.</span></span>

<span data-ttu-id="39e62-108">초안 버전이 실행 중이어도 Runbook은 여전히 정상적으로 워크플로를 실행하고 해당 환경에서 리소스에 대해 모든 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-108">Even though the draft version is being run, the runbook still executes the workflow normally and performs any actions against resources in the environment.</span></span> <span data-ttu-id="39e62-109">이러한 이유로 프로덕션이 아닌 리소스에서만 Runbook을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-109">For this reason, you should only test runbooks at non-production resources.</span></span>

<span data-ttu-id="39e62-110">각 [Runbook 유형](automation-runbook-types.md) 을 테스트하는 절차는 동일하며 Azure 포털에서 테스트할 때 텍스트 편집기와 그래픽 편집기 간에 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-110">The procedure to test each [type of runbook](automation-runbook-types.md) is the same, and there is no difference in testing between the textual editor and the graphical editor in the Azure portal.</span></span>  

## <a name="to-test-a-runbook-in-the-azure-portal"></a><span data-ttu-id="39e62-111">Azure 포털에서 Runbook을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="39e62-111">To test a runbook in the Azure portal</span></span>
<span data-ttu-id="39e62-112">Azure 포털에서 모든 [Runbook 유형](automation-runbook-types.md) 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-112">You can work with any [runbook type](automation-runbook-types.md) in the Azure portal.</span></span>

1. <span data-ttu-id="39e62-113">[텍스트 편집기](automation-edit-textual-runbook.md) 또는 [그래픽 편집기](automation-graphical-authoring-intro.md)에서 Runbook의 초안 버전을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-113">Open the Draft version of the runbook in either the [textual editor](automation-edit-textual-runbook.md) or [graphical editor](automation-graphical-authoring-intro.md).</span></span>
2. <span data-ttu-id="39e62-114">**테스트** 단추를 클릭하여 테스트 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-114">Click the **Test** button to open the Test blade.</span></span>
3. <span data-ttu-id="39e62-115">Runbook에 매개 변수가 있는 경우 테스트에 사용되는 값을 제공할 수 있는 왼쪽 창에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-115">If the runbook has parameters, they will be listed in the left pane where you can provide values to be used for the test.</span></span>
4. <span data-ttu-id="39e62-116">[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)에서 테스트를 실행하려는 경우는 **실행 설정**을 **Hybrid Worker**로 변경하고 대상 그룹의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-116">If you want to run the test on a [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), then change **Run Settings** to **Hybrid Worker** and select the name of the target group.</span></span>  <span data-ttu-id="39e62-117">그렇지 않은 경우 기본 **Azure** 를 유지하여 클라우드에서 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-117">Otherwise, keep the default **Azure** to run the test in the cloud.</span></span>
5. <span data-ttu-id="39e62-118">**시작** 단추를 클릭하여 테스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-118">Click the **Start** button to start the test.</span></span>
6. <span data-ttu-id="39e62-119">Runbook이 [PowerShell 워크플로](automation-runbook-types.md#powershell-workflow-runbooks) 또는 [그래픽](automation-runbook-types.md#graphical-runbooks)인 경우 출력 창 아래의 단추를 사용하여 테스트되는 동안 중지하거나 일시 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-119">If the runbook is [PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) or [Graphical](automation-runbook-types.md#graphical-runbooks), then you can stop or suspend it while it is being tested with the buttons underneath the Output Pane.</span></span> <span data-ttu-id="39e62-120">Runbook을 일시 중단하는 경우 일시 중단하기 전에 현재 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-120">When you suspend the runbook, it completes the current activity before being suspended.</span></span> <span data-ttu-id="39e62-121">Runbook이 일시 중단되면 중지하거나 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-121">Once the runbook is suspended, you can stop it or restart it.</span></span>
7. <span data-ttu-id="39e62-122">출력 창에서 Runbook의 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="39e62-122">Inspect the output from the runbook in the output pane.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39e62-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39e62-123">Next Steps</span></span>
* <span data-ttu-id="39e62-124">Runbook을 만들거나 가져오는 방법을 알아보려면 [Azure 자동화에서 Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="39e62-124">To learn how to create or import a runbook, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="39e62-125">그래픽 작성에 대해 자세히 알아보려면 [Azure 자동화에서 그래픽 작성](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="39e62-125">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="39e62-126">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="39e62-126">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="39e62-127">권장 방법을 포함하여 상태 메시지 및 오류를 반환하도록 Runbook을 구성하는 방법에 대한 자세한 내용은 [Azure 자동화에서 Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="39e62-127">To learn more about configuring runboks to return status messages and errors, including recommended practices, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

