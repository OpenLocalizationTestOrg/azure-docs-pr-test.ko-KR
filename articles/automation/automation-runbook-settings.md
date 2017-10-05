---
title: "Runbook 설정 | Microsoft Docs"
description: "Azure 자동화의 Runbook에 대한 구성 설정 및 Azure 관리 포털과 Windows PowerShell을 사용하여 이를 변경하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="55719-103">Runbook 설정</span><span class="sxs-lookup"><span data-stu-id="55719-103">Runbook settings</span></span>
<span data-ttu-id="55719-104">Azure 자동화의 각 Runbook에는 해당 로깅 동작을 쉽게 식별하고 변경하는 데 유용한 여러 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="55719-105">이러한 각 설정은 아래에서 해당 설정을 수정하는 방법에 대한 절차 다음에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="55719-106">설정</span><span class="sxs-lookup"><span data-stu-id="55719-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="55719-107">이름 및 설명</span><span class="sxs-lookup"><span data-stu-id="55719-107">Name and description</span></span>
<span data-ttu-id="55719-108">Runbook을 만든 후에는 이름을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="55719-109">이 설명은 선택 사항이며, 최대 512자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="55719-110">태그</span><span class="sxs-lookup"><span data-stu-id="55719-110">Tags</span></span>
<span data-ttu-id="55719-111">태그를 사용하면 Runbook을 쉽게 식별할 수 있는 고유한 단어 및 구를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="55719-112">예를 들어 [PowerShell 갤러리](https://www.powershellgallery.com/)에 Runbook을 제출할 때 Runbook이 나열되어야 하는 범주를 식별하는 특정 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55719-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="55719-113">쉼표로 구분하여 Runbook에 대한 여러 태그를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="55719-114">로깅</span><span class="sxs-lookup"><span data-stu-id="55719-114">Logging</span></span>
<span data-ttu-id="55719-115">기본적으로 자세한 정보 표시 및 진행률 레코드 작업 기록에 기록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="55719-116">이러한 레코드를 기록하려면 특정 Runbook에 대한 설정을 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55719-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="55719-117">이러한 레코드에 대한 자세한 내용은 [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55719-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="55719-118">Runbook 설정 변경</span><span class="sxs-lookup"><span data-stu-id="55719-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="55719-119">Azure Portal을 사용하여 Runbook 설정 변경</span><span class="sxs-lookup"><span data-stu-id="55719-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="55719-120">Azure Portal의 Runbook에 대한 **설정** 블레이드에서 해당 Runbook의 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="55719-121">Azure 포털에서 **자동화**를 선택한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55719-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="55719-122">**Runbook** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55719-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="55719-123">Runbook의 이름을 클릭하면 해당 runbook에 대한 설정 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55719-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="55719-124">여기에서 태그 또는 runbook 설명을 지정하거나 수정하고, 로깅 및 추적 설정을 구성하고, 문제 해결을 도와주는 지원 도구에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="55719-125">Windows PowerShell을 사용하여 Runbook 설정 변경</span><span class="sxs-lookup"><span data-stu-id="55719-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="55719-126">[Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet을 사용하여 Runbook의 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="55719-127">여러 태그를 지정하려면 Tags 매개 변수에 배열 또는 쉼표로 구분된 값이 있는 단일 문자열을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55719-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="55719-128">[Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx)을 사용하여 현재 태그를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55719-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="55719-129">다음 명령 예제에서는 Rnbook에 대한 속성을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55719-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="55719-130">이 예제에서는 기존 태그에 세 개의 태그를 추가하고 자세한 정보 표시 레코드가 기록되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55719-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="55719-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55719-131">Next steps</span></span>
* <span data-ttu-id="55719-132">Runbook에서 출력 및 오류 메시지를 만들고 검색하는 방법은 [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55719-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="55719-133">커뮤니티 또는 다른 출처에서 이미 개발된 runbook을 추가하거나 사용자 고유의 runbook을 만드는 방법은 [Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55719-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

