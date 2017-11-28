---
title: "Azure 자동화에서 runbook aaaTesting | Microsoft Docs"
description: "Azure 자동화에서 runbook을 게시 하기 전에 예상 대로 작동 tooensure를 테스트할 수 있습니다.  이 문서에서는 설명 방법을 tootest runbook 해당 출력을 봅니다."
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
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a><span data-ttu-id="ef011-104">Azure 자동화에서 Runbook 테스트</span><span class="sxs-lookup"><span data-stu-id="ef011-104">Testing a runbook in Azure Automation</span></span>
<span data-ttu-id="ef011-105">Runbook을 테스트할 때는 hello [초안 버전](automation-creating-importing-runbook.md#publishing-a-runbook) 실행 되며 수행 하는 모든 작업이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-105">When you test a runbook, hello [Draft version](automation-creating-importing-runbook.md#publishing-a-runbook) is executed and any actions that it performs are completed.</span></span> <span data-ttu-id="ef011-106">작업 기록은 만들어지기는 하지만 hello [출력](automation-runbook-output-and-messages.md#output-stream) 및 [경고 및 오류](automation-runbook-output-and-messages.md#message-streams) 스트림을 표시 하는 hello 테스트 출력 창.</span><span class="sxs-lookup"><span data-stu-id="ef011-106">No job history is created, but hello [Output](automation-runbook-output-and-messages.md#output-stream) and [Warning and Error](automation-runbook-output-and-messages.md#message-streams) streams are displayed in hello Test output Pane.</span></span> <span data-ttu-id="ef011-107">메시지 toohello [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) 경우에 hello hello 출력 창에에서 표시 됩니다 [$VerbosePreference 변수](automation-runbook-output-and-messages.md#preference-variables) tooContinue 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-107">Messages toohello [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) are displayed in hello Output Pane only if hello [$VerbosePreference variable](automation-runbook-output-and-messages.md#preference-variables) is set tooContinue.</span></span>

<span data-ttu-id="ef011-108">Hello 초안 버전을 실행 하는 경우에 hello runbook 여전히 hello 워크플로 정상적으로 실행 하 고 hello 환경에서 리소스에 대 한 모든 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-108">Even though hello draft version is being run, hello runbook still executes hello workflow normally and performs any actions against resources in hello environment.</span></span> <span data-ttu-id="ef011-109">이러한 이유로 프로덕션이 아닌 리소스에서만 Runbook을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-109">For this reason, you should only test runbooks at non-production resources.</span></span>

<span data-ttu-id="ef011-110">프로시저 tootest hello [runbook의 형식을](automation-runbook-types.md) hello 동일 하 고 테스트 hello 텍스트 편집기와 hello hello Azure 포털의에서 그래픽 편집기 사이 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-110">hello procedure tootest each [type of runbook](automation-runbook-types.md) is hello same, and there is no difference in testing between hello textual editor and hello graphical editor in hello Azure portal.</span></span>  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a><span data-ttu-id="ef011-111">tootest hello Azure 포털에서 runbook</span><span class="sxs-lookup"><span data-stu-id="ef011-111">tootest a runbook in hello Azure portal</span></span>
<span data-ttu-id="ef011-112">사용 하 여 작업 수 [runbook 형식](automation-runbook-types.md) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="ef011-112">You can work with any [runbook type](automation-runbook-types.md) in hello Azure portal.</span></span>

1. <span data-ttu-id="ef011-113">어느 hello에 hello runbook의 초안 버전 열기 hello [텍스트 편집기](automation-edit-textual-runbook.md) 또는 [그래픽 편집기](automation-graphical-authoring-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-113">Open hello Draft version of hello runbook in either hello [textual editor](automation-edit-textual-runbook.md) or [graphical editor](automation-graphical-authoring-intro.md).</span></span>
2. <span data-ttu-id="ef011-114">Hello 클릭 **테스트** 단추 tooopen hello 테스트 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-114">Click hello **Test** button tooopen hello Test blade.</span></span>
3. <span data-ttu-id="ef011-115">Hello runbook에 매개 변수가 hello 테스트에 사용 되는 값 toobe를 제공할 수 있는 hello 왼쪽된 창에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-115">If hello runbook has parameters, they will be listed in hello left pane where you can provide values toobe used for hello test.</span></span>
4. <span data-ttu-id="ef011-116">toorun hello 테스트 하려는 경우는 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), 다음 변경 **실행 설정** 너무**Hybrid Worker** 및 hello 대상 그룹의 이름을 선택 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-116">If you want toorun hello test on a [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), then change **Run Settings** too**Hybrid Worker** and select hello name of hello target group.</span></span>  <span data-ttu-id="ef011-117">그렇지 않으면 hello 기본값을 유지 **Azure** hello 클라우드에서 toorun hello 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-117">Otherwise, keep hello default **Azure** toorun hello test in hello cloud.</span></span>
5. <span data-ttu-id="ef011-118">Hello 클릭 **시작** 단추 toostart hello 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-118">Click hello **Start** button toostart hello test.</span></span>
6. <span data-ttu-id="ef011-119">Hello runbook이 [PowerShell 워크플로](automation-runbook-types.md#powershell-workflow-runbooks) 또는 [그래픽](automation-runbook-types.md#graphical-runbooks), 다음 hello 출력 창 아래의 hello 단추를 사용 하 여 테스트 되는 일시 중단 하거나 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-119">If hello runbook is [PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) or [Graphical](automation-runbook-types.md#graphical-runbooks), then you can stop or suspend it while it is being tested with hello buttons underneath hello Output Pane.</span></span> <span data-ttu-id="ef011-120">Hello runbook을 일시 중단 하는 경우 일시 중단 되기 전에 hello 현재 작업이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-120">When you suspend hello runbook, it completes hello current activity before being suspended.</span></span> <span data-ttu-id="ef011-121">Hello runbook이 일시 중단 되 면 중지 하거나 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-121">Once hello runbook is suspended, you can stop it or restart it.</span></span>
7. <span data-ttu-id="ef011-122">Hello hello 출력 창에는 runbook에서 hello 출력을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef011-122">Inspect hello output from hello runbook in hello output pane.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef011-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef011-123">Next Steps</span></span>
* <span data-ttu-id="ef011-124">toocreate 또는 가져오기 runbook 확인 하려면 어떻게 해야 toolearn [만들기 또는 Azure 자동화에서 runbook 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="ef011-124">toolearn how toocreate or import a runbook, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="ef011-125">그래픽 작성에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ef011-125">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="ef011-126">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="ef011-126">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="ef011-127">runboks tooreturn 상태 메시지 및 권장 되는 방법을 비롯 하 여 오류 구성에 대 한 더 toolearn 참조 [Runbook 출력 및 Azure 자동화에서 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="ef011-127">toolearn more about configuring runboks tooreturn status messages and errors, including recommended practices, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

