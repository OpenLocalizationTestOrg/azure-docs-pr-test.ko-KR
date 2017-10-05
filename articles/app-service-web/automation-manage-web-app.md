---
title: "Azure Automation을 사용하여 Azure 웹앱 관리 | Microsoft Docs"
description: "Azure 자동화 서비스를 사용하여 Azure 웹앱을 관리하는 방법에 대해 알아봅니다."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="7b1db-103">Azure 자동화를 사용하여 Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="7b1db-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="7b1db-104">이 가이드에서는 Azure 자동화 서비스 및 이 서비스를 사용하여 Azure SQL 웹앱 관리를 간소화하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="7b1db-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="7b1db-105">What is Azure Automation?</span></span>
<span data-ttu-id="7b1db-106">[Azure 자동화](../automation/automation-intro.md) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="7b1db-107">Azure 자동화, 수동, 반복되는, 장기 실행 및 오류가 발생하기 쉬운 작업을 사용하면 조직의 안정성, 효율성 및 가치 창출 시간을 개선하도록 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="7b1db-108">Azure 자동화는 요구 사항에 맞게 크기가 조정되는 매우 안정적이며 가용성이 높은 워크플로 실행 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="7b1db-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="7b1db-110">Azure 자동화에서 자동으로 실행되도록 클라우드 관리 작업을 이동하여 작업 오버헤드를 줄이고 IT 및 DevOps 직원들이 비즈니스 가치를 추가하는 작업에 집중할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="7b1db-111">어떻게 Azure 자동화가 Azure 웹앱을 관리할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7b1db-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="7b1db-112">[Azure PowerShell 모듈](/powershell/azureps-cmdlets-docs)에서 사용할 수 있는 PowerShell cmdlet을 사용하여 Azure 자동화에서 웹앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="7b1db-113">[Azure 자동화에서는 이러한 웹앱 PowerShell cmdlet을 설치](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)할 수 있으므로 서비스 내에서 웹앱 관리 작업을 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="7b1db-114">Azure 자동화에서 이러한 cmdlet을 다른 Azure 서비스용 cmdlet과 연결하여 Azure 서비스와 타사 시스템 간의 복잡한 작업을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="7b1db-115">자동화를 사용하여 앱 서비스를 관리하는 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b1db-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="7b1db-116">웹앱을 관리하기 위한 스크립트</span><span class="sxs-lookup"><span data-stu-id="7b1db-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="7b1db-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b1db-117">Next steps</span></span>
<span data-ttu-id="7b1db-118">Azure 자동화의 기본 사항과 Azure 자동화를 사용하여 Azure 웹앱을 관리하는 방법을 알아보았으므로 이제 다음 링크에 따라 Azure 자동화에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7b1db-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="7b1db-119">Azure 자동화 [시작 자습서](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="7b1db-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

