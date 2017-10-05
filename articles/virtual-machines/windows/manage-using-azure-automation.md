---
title: "Azure Automation을 사용하여 VM 관리 | Microsoft Docs"
description: "Azure 자동화 서비스를 사용하여 대규모 Azure 가상 컴퓨터를 관리하는 방법을 알아봅니다."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="9140f-103">Azure 자동화를 사용하여 Azure 가상 컴퓨터 관리</span><span class="sxs-lookup"><span data-stu-id="9140f-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="9140f-104">이 가이드에서는 Azure 자동화 서비스 및 이 서비스를 사용하여 Azure 가상 컴퓨터 관리를 간소화하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="9140f-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="9140f-105">What is Azure Automation?</span></span>
<span data-ttu-id="9140f-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="9140f-107">Azure 자동화를 통해 장기 실행 작업, 수동 작업, 오류가 발생하기 쉬운 작업 및 빈번하게 반복되는 작업을 자동화하여 조직의 안정성, 효율성 및 가치 창출 시간을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="9140f-108">Azure 자동화는 조직이 성장함에 따라 요구를 충족하기 위해 크기가 조정되는 안정성과 가용성 높은 워크플로 실행 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="9140f-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="9140f-110">Azure 자동화에서 자동으로 실행되도록 클라우드 관리 작업을 실행하여 작업 오버헤드를 줄이고 IT 및 DevOps 직원들이 비즈니스 가치를 추가하는 작업에 집중할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="9140f-111">Azure 자동화를 통해 Azure 가상 컴퓨터 관리 향상</span><span class="sxs-lookup"><span data-stu-id="9140f-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="9140f-112">[Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)을 사용하여 Azure 자동화에서 가상 컴퓨터를 관리 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="9140f-113">Azure 자동화에서는 이러한 PowerShell cmdlet을 포함하고 있으므로 서비스 내에서 모든 가 컴퓨터 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="9140f-114">Azure 자동화에서 이러한 cmdlet을 다른 Azure 서비스용 cmdlet과 연결하여 Azure 서비스와 타사 시스템 간의 복잡한 작업을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9140f-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9140f-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9140f-115">Next steps</span></span>
<span data-ttu-id="9140f-116">Azure 자동화의 기본 사항과 Azure 자동화를 사용하여 Azure 가상 컴퓨터를 관리하는 방법을 알아보았습니다. 추가 정보는</span><span class="sxs-lookup"><span data-stu-id="9140f-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="9140f-117">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="9140f-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="9140f-118">내 첫 번째 runbook</span><span class="sxs-lookup"><span data-stu-id="9140f-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="9140f-119">Azure 자동화 학습 맵</span><span class="sxs-lookup"><span data-stu-id="9140f-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

