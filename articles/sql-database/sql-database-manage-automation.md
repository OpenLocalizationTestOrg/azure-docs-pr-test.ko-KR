---
title: "Azure Automation을 사용하여 Azure SQL Databases 관리 | Microsoft Docs"
description: "Azure 자동화 서비스를 사용하여 대규모 Azure SQL 데이터베이스를 관리하는 방법을 알아봅니다."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: 7f45b8b654691063823c13bee61e9bb874a6a13a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="f1569-103">Azure 자동화를 사용하여 Azure SQL 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="f1569-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="f1569-104">이 가이드에서는 Azure 자동화 서비스 및 이 서비스를 사용하여 Azure SQL 데이터베이스 관리를 간소화하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="f1569-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="f1569-105">What is Azure Automation?</span></span>
<span data-ttu-id="f1569-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="f1569-107">Azure 자동화를 통해 장기 실행 작업, 수동 작업, 오류가 발생하기 쉬운 작업 및 빈번하게 반복되는 작업을 자동화하여 조직의 안정성, 효율성 및 가치 창출 시간을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="f1569-108">Azure 자동화는 조직이 성장함에 따라 요구를 충족하기 위해 크기가 조정되는 안정성과 가용성 높은 워크플로 실행 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="f1569-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="f1569-110">Azure 자동화에 의해 자동으로 실행되도록 클라우드 관리 작업을 이동하여 작업 오버헤드를 줄이고 IT/DevOps 직원들이 비즈니스 가치를 추가하는 작업에 집중할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="f1569-111">Azure 자동화를 통해 Azure SQL 데이터베이스 관리 향상</span><span class="sxs-lookup"><span data-stu-id="f1569-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="f1569-112">Azure SQL Database는 [Azure PowerShell 도구](/powershell/azure/overview)에서 사용할 수 있는 [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/)를 이용하여 Azure Automation에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-112">Azure SQL Database can be managed in Azure Automation by using the [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in the [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="f1569-113">Azure 자동화에서는 이러한 Azure SQL 데이터베이스 PowerShell cmdlet을 기본적으로 사용할 수 있으므로 서비스 내에서 SQL DB 관리 작업을 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of the box, so that you can perform all of your SQL DB management tasks within the service.</span></span> <span data-ttu-id="f1569-114">Azure 자동화에서 이러한 cmdlet을 다른 Azure 서비스용 cmdlet과 연결하여 Azure 서비스와 타사 시스템 간의 복잡한 작업을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="f1569-115">또한 Azure 자동화에서 PowerShell을 통해 SQL 명령을 실행하여 SQL 서버와 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-115">Azure Automation also has the ability to communicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="f1569-116">[Azure 자동화 runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 는 다양한 Azure 저장소, 다른 Azure 서비스 및 타사 시스템의 관리 자동화를 시작하도록 제품 군 및 커뮤니티 runbook을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-116">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="f1569-117">Runbook 갤러리에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="f1569-118">SQL Server 데이터베이스에 대해 SQL 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="f1569-119">일정에 따라 Azure SQL 데이터베이스를 세로로(위쪽 또는 아래쪽) 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1569-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="f1569-120">해당 데이터베이스의 최대 크기에 도달한 경우 SQL 테이블을 줄이세요.</span><span class="sxs-lookup"><span data-stu-id="f1569-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="f1569-121">Azure SQL 데이터베이스가 심하게 조각화 된 경우 테이블에 색인을 달아주세요.</span><span class="sxs-lookup"><span data-stu-id="f1569-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="f1569-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1569-122">Next steps</span></span>
<span data-ttu-id="f1569-123">Azure 자동화의 기본 사항과 Azure 자동화를 사용하여 SQL 데이터베이스를 관리하는 방법을 알아보았으므로 이제 다음 링크에 따라 Azure 자동화에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f1569-123">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure SQL databases, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="f1569-124">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="f1569-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="f1569-125">내 첫 번째 runbook</span><span class="sxs-lookup"><span data-stu-id="f1569-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="f1569-126">Azure 자동화 학습 맵</span><span class="sxs-lookup"><span data-stu-id="f1569-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="f1569-127">Azure 자동화: 클라우드의 SQL 에이전트</span><span class="sxs-lookup"><span data-stu-id="f1569-127">Azure Automation: Your SQL Agent in the Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

