---
title: "Azure 자동화 DSC 개요 | Microsoft Docs"
description: "Azure 자동화 DSC(필요한 상태 구성)의 개요, 용어 및 알려진 문제"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell DSC, 필요한 상태 구성, PowerShell DSC Azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="ec8d5-104">Azure 자동화 DSC 개요</span><span class="sxs-lookup"><span data-stu-id="ec8d5-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="ec8d5-105">Azure Automation DSC는 Azure 서비스로, 모든 클라우드에서 PowerShell DSC(Desired State Configuration) [구성](https://msdn.microsoft.com/powershell/dsc/configurations)을 작성, 관리 및 컴파일하고 [DSC 리소스](https://msdn.microsoft.com/powershell/dsc/resources)를 가져오고 대상 노드에 구성을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="ec8d5-106">Azure Automation DSC를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="ec8d5-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="ec8d5-107">Azure Automation DSC는 Azure 외부에서 DSC를 사용하는 것보다 몇 가지 장점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="ec8d5-108">기본 제공 끌어오기 서버</span><span class="sxs-lookup"><span data-stu-id="ec8d5-108">Built-in pull server</span></span>

<span data-ttu-id="ec8d5-109">Azure Automation에서는 대상 노드가 구성을 자동으로 수신하고 원하는 상태를 따르며 규정 준수를 다시 보고하도록 [DSC 끌어오기 서버](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="ec8d5-110">Azure Automation에 있는 기본 제공 끌어오기 서버는 자체 끌어오기 서버를 설정하고 유지 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="ec8d5-111">Azure Automation은 클라우드 또는 온-프레미스에서 가상 또는 실제 Windows 또는 Linux 컴퓨터를 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="ec8d5-112">모든 DSC 아티팩트 관리</span><span class="sxs-lookup"><span data-stu-id="ec8d5-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="ec8d5-113">Azure Automation DSC는 Azure Automation에서 PowerShell 스크립팅을 위해 제공하는 것과 동일한 관리 계층을 [PowerShell 필요한 상태 구성](https://msdn.microsoft.com/powershell/dsc/overview)에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="ec8d5-114">Azure Portal 또는 PowerShell에서 DSC 구성, 리소스 및 대상 노드를 모두 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Azure Automation 블레이드의 스크린샷](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="ec8d5-116">Log Analytics로 보고 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="ec8d5-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="ec8d5-117">Azure Automation DSC로 관리되는 노드는 상세한 보고 상태 데이터를 기본 제공 끌어오기 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="ec8d5-118">이 데이터를 Microsoft OMS(Operations Management Suite) Log Analytics 작업 영역으로 보내도록 Azure Automation DSC를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="ec8d5-119">DSC 상태 데이터를 Log Analytics 작업 영역으로 보내는 방법을 알아보려면 [Azure Automation DSC 보고 데이터를 OMS Log Analytics로 전달](automation-dsc-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="ec8d5-120">소개 비디오</span><span class="sxs-lookup"><span data-stu-id="ec8d5-120">Introduction video</span></span>

<span data-ttu-id="ec8d5-121">읽기보다 비디오를 시청하기가 편하신가요?</span><span class="sxs-lookup"><span data-stu-id="ec8d5-121">Prefer watching to reading?</span></span> <span data-ttu-id="ec8d5-122">2015년 5월 Azure Automation DSC가 처음 발표될 당시의 비디오를 다음에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="ec8d5-123">이 비디오에 언급된 개념 및 수명은 정확하지만 이 비디오가 기록된 이후에 Azure Automation DSC는 많이 발전되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="ec8d5-124">일반적으로 사용할 수 있고 Azure 포털의 UI는 보다 강력해졌으며 더 많은 기능을 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="ec8d5-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec8d5-125">Next steps</span></span>

* <span data-ttu-id="ec8d5-126">Azure Automation DSC로 관리되는 노드를 온보딩하는 방법을 알아보려면 [Azure Automation DSC에 의한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="ec8d5-127">Azure Automation DSC 사용을 시작하려면 [Azure Automation DSC 시작하기](automation-dsc-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="ec8d5-128">DSC 구성을 대상 노드에 할당할 수 있도록 DSC 구성을 컴파일하는 방법에 대해 알아보려면 [Azure Automation DSC에서 구성을 컴파일](automation-dsc-compile.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="ec8d5-129">Azure Automation DSC에 대한 PowerShell cmdlet 참조는 [Azure Automation DSC cmdlet ](/powershell/module/azurerm.automation/#automation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="ec8d5-130">가격 책정 정보는 [Azure Automation DSC 가격 책정](https://azure.microsoft.com/pricing/details/automation/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec8d5-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="ec8d5-131">연속 배포 파이프라인에서 Azure 자동화 DSC를 사용 하는 예제를 보려면 [IaaS Vm 사용 하 여 Azure 자동화 DSC 및 Chocolatey 연속 배포](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="ec8d5-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>