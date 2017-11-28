---
title: "aaaRunbook 설정 | Microsoft Docs"
description: "Azure 자동화에서 runbook에 대 한 구성 설정을 hello 설명 및 방법을 모두 사용 하 여 Azure 관리 포털 및 Windows PowerShell을 hello toochange 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="e4b9f-103">Runbook 설정</span><span class="sxs-lookup"><span data-stu-id="e4b9f-103">Runbook settings</span></span>
<span data-ttu-id="e4b9f-104">Azure 자동화에서 각 runbook에는 로깅 동작 toobe 식별 및 toochange는 데 도움이 되는 여러 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="e4b9f-105">이러한 각 설정은 아래에 설명 되어 방법에 대 한 절차가 함께 toomodify 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="e4b9f-106">설정</span><span class="sxs-lookup"><span data-stu-id="e4b9f-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="e4b9f-107">이름 및 설명</span><span class="sxs-lookup"><span data-stu-id="e4b9f-107">Name and description</span></span>
<span data-ttu-id="e4b9f-108">만든 후에 runbook의 이름을 hello를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="e4b9f-109">hello 설명은 선택 사항이 며 too512 문자가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="e4b9f-110">태그들</span><span class="sxs-lookup"><span data-stu-id="e4b9f-110">Tags</span></span>
<span data-ttu-id="e4b9f-111">태그를 사용 하면 tooassign 고유한 단어 및 구 toohelp runbook을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="e4b9f-112">예를 들어 runbook toohello 제출할 때 [PowerShell 갤러리](https://www.powershellgallery.com/), 지정한 특정 태그 tooidentify 범주는 hello runbook에 나열 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="e4b9f-113">쉼표로 구분하여 Runbook에 대한 여러 태그를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="e4b9f-114">로깅</span><span class="sxs-lookup"><span data-stu-id="e4b9f-114">Logging</span></span>
<span data-ttu-id="e4b9f-115">기본적으로 자세한 정보 표시 및 진행률 레코드는 toojob 기록을 기록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="e4b9f-116">이러한 레코드는 특정 runbook toolog에 대 한 hello 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="e4b9f-117">이러한 레코드에 대한 자세한 내용은 [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="e4b9f-118">Runbook 설정 변경</span><span class="sxs-lookup"><span data-stu-id="e4b9f-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="e4b9f-119">Hello Azure 포털을 사용 하 여 runbook 설정 변경</span><span class="sxs-lookup"><span data-stu-id="e4b9f-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="e4b9f-120">Hello에서 hello Azure 포털에서에서 runbook에 대 한 설정을 변경할 수 있습니다 **설정을** 블레이드 hello runbook에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="e4b9f-121">Hello Azure 포털에서에서 선택 **자동화** 다음 자동화 계정 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="e4b9f-122">선택 hello **Runbook** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="e4b9f-123">Runbook의 hello 이름을 클릭 하 고 hello runbook에 대 한 리디렉션된 toohello 설정 블레이드에서 있으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="e4b9f-124">여기에서 지정 하거나 태그를 수정, runbook 설명은 hello, 로깅 및 추적 설정, 구성 하 고 수 문제를 해결 하는 지원 도구 toohelp 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="e4b9f-125">Windows PowerShell을 사용하여 Runbook 설정 변경</span><span class="sxs-lookup"><span data-stu-id="e4b9f-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="e4b9f-126">Hello를 사용할 수 있습니다 [집합 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) runbook에 대 한 cmdlet toochange hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="e4b9f-127">여러 태그 toospecify 하려는 경우 쉼표로 구분 된 값 toohello 태그 매개 변수와 함께 배열 또는 단일 문자열을 제공 하거나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="e4b9f-128">Hello로 hello 현재 태그를 가져올 수 있습니다 [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="e4b9f-129">다음 명령 예제는 hello tooset runbook에 대 한 속성을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="e4b9f-130">이 샘플 태그를 삽입 하 고 자세한 레코드가 기록 되도록 지정 toohello 기존 3 개의 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b9f-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="e4b9f-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4b9f-131">Next steps</span></span>
* <span data-ttu-id="e4b9f-132">runbook에서 toocreate 및 검색 하 고 출력 및 오류 메시지를 확인 하려면 어떻게 toolearn [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e4b9f-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="e4b9f-133">runbook이 이미이 개발한 hello community 또는 다른 원본 또는 toocreate 고유한 runbook tooadd 확인 하려면 어떻게 해야 toounderstand [만들거나 Runbook 가져오기](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="e4b9f-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

