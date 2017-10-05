---
title: "스케줄러 PowerShell Cmdlet 참조"
description: "스케줄러 PowerShell Cmdlet 참조"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 141919ab4506b3de4c4a69670dcf54c60ee6409c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="55e68-103">스케줄러 PowerShell Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="55e68-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="55e68-104">다음 표에서는 Azure 스케줄러의 주요 cmdlet을 설명하고 참조 페이지에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-104">The following table describes and links to the reference page of each of the major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="55e68-105">Azure PowerShell을 설치하고 Azure 구독에 연결하려면 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e68-105">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="55e68-106">[Azure Resource Manager cmdlet](/powershell/azure/overview)에 대한 자세한 내용은 [Azure Resource Manager로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e68-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="55e68-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="55e68-107">Cmdlet</span></span> | <span data-ttu-id="55e68-108">Cmdlet 설명</span><span class="sxs-lookup"><span data-stu-id="55e68-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="55e68-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="55e68-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="55e68-110">작업 컬렉션을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="55e68-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="55e68-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="55e68-112">작업 컬렉션을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="55e68-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="55e68-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="55e68-114">Scheduler 작업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="55e68-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="55e68-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="55e68-116">작업 컬렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-116">Gets job collections.</span></span> |
| [<span data-ttu-id="55e68-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="55e68-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="55e68-118">작업 내역을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-118">Gets job history.</span></span> |
| [<span data-ttu-id="55e68-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="55e68-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="55e68-120">HTTP 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="55e68-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="55e68-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="55e68-122">작업 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="55e68-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="55e68-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="55e68-124">Service Bus 큐 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="55e68-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="55e68-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="55e68-126">Service Bus 토픽 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="55e68-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="55e68-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="55e68-128">Storage 큐 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="55e68-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="55e68-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="55e68-130">Scheduler 작업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="55e68-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="55e68-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="55e68-132">작업 컬렉션을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="55e68-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="55e68-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="55e68-134">Scheduler HTTP 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="55e68-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="55e68-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="55e68-136">작업 컬렉션을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="55e68-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="55e68-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="55e68-138">Service Bus 큐 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="55e68-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="55e68-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="55e68-140">Service Bus 토픽 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="55e68-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="55e68-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="55e68-142">Storage 큐 작업을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="55e68-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="55e68-143">자세한 내용을 보려면, 다음 중 원하는 cmdlet을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="55e68-143">For more detailed information, you can run any of the following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="55e68-144">참고 항목</span><span class="sxs-lookup"><span data-stu-id="55e68-144">See Also</span></span>
 [<span data-ttu-id="55e68-145">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="55e68-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="55e68-146">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="55e68-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="55e68-147">Azure 포털에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="55e68-147">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="55e68-148">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="55e68-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="55e68-149">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="55e68-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="55e68-150">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="55e68-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="55e68-151">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="55e68-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="55e68-152">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="55e68-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

