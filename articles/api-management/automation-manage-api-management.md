---
title: "Azure 자동화를 사용하여 Azure API 관리를 관리"
description: "Azure 자동화 서비스를 사용하여 Azure API 관리를 관리하는 방법에 대해 알아봅니다."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="5cfb1-103">Azure 자동화를 사용하여 Azure API 관리를 관리</span><span class="sxs-lookup"><span data-stu-id="5cfb1-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="5cfb1-104">이 가이드에서는 Azure 자동화 서비스 및 이를 사용하여 Azure API 관리의 관리를 간소화하는 방법에 대해 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="5cfb1-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="5cfb1-105">What is Azure Automation?</span></span>
<span data-ttu-id="5cfb1-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="5cfb1-107">Azure 자동화, 수동, 반복되는, 장기 실행 및 오류가 발생하기 쉬운 작업을 사용하면 조직의 안정성, 효율성 및 가치 창출 시간을 개선하도록 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="5cfb1-108">Azure 자동화는 요구 사항에 맞게 크기가 조정되는 매우 안정적이며 가용성이 높은 워크플로 실행 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="5cfb1-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="5cfb1-110">Azure 자동화에서 자동으로 실행되도록 클라우드 관리 작업을 이동하여 작업 오버헤드를 줄이고 IT 및 DevOps 직원들이 비즈니스 가치를 추가하는 작업에 집중할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="5cfb1-111">Azure 자동화를 통해 Azure API 관리를 쉽게 관리하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="5cfb1-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="5cfb1-112">API 관리는 [Azure API 관리 API용 Windows PowerShell cmdlet](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/)을 사용하여 Azure 자동화에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="5cfb1-113">Azure 자동화 내에서 cmdlet을 사용하여 API 관리 작업을 수행하도록 PowerShell 워크플로 스크립트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="5cfb1-114">Azure 자동화에서 이러한 cmdlet을 다른 Azure 서비스용 cmdlet과 연결하여 Azure 서비스와 타사 시스템 간의 복잡한 작업을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="5cfb1-115">다음은 자동화를 통해 API 관리를 사용하는 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="5cfb1-116">Azure API 관리 – 백업 및 복원에 PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="5cfb1-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="5cfb1-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cfb1-117">Next Steps</span></span>
<span data-ttu-id="5cfb1-118">Azure 자동화의 기본 사항과 Azure 자동화를 사용하여 Azure API 관리를 관리하는 방법을 알아보았으므로, 이제 다음 링크에 따라 더 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="5cfb1-119">Azure 자동화 [시작 자습서](../automation/automation-first-runbook-graphical.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cfb1-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

