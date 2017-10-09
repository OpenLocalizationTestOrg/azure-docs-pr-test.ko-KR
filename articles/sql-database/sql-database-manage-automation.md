---
title: "Azure 자동화를 사용 하 여 Azure SQL 데이터베이스 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 규모에 사용 되는 toomanage Azure SQL 데이터베이스를 수 있는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="16f16-103">Azure 자동화를 사용하여 Azure SQL 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="16f16-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="16f16-104">이 가이드에서는 toohello Azure 자동화 서비스 및 Azure SQL 데이터베이스의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="16f16-105">Azure 자동화 정의</span><span class="sxs-lookup"><span data-stu-id="16f16-105">What is Azure Automation?</span></span>
<span data-ttu-id="16f16-106">[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="16f16-107">Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 되는 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="16f16-108">Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="16f16-109">Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="16f16-110">작동 오버 헤드를 줄이고 확보 IT / DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="16f16-111">Azure 자동화를 통해 Azure SQL 데이터베이스 관리 향상</span><span class="sxs-lookup"><span data-stu-id="16f16-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="16f16-112">Hello를 사용 하 여 Azure 자동화에서 azure SQL 데이터베이스를 관리할 수 있습니다 [Azure SQL 데이터베이스 PowerShell cmdlet](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) hello에서 사용 가능한 [Azure PowerShell 도구](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="16f16-113">Azure 자동화에는 사용할 수 있는 Azure SQL 데이터베이스 PowerShell cmdlet이 hello 상자 밖의 hello 서비스 내에서 SQL DB 관리 작업을 모두 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="16f16-114">또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="16f16-115">Azure 자동화에는 SQL 서버와 hello 기능 toocommunicate를 직접 PowerShell을 사용 하 여 SQL 명령을 실행 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="16f16-116">hello [Azure 자동화 runbook 갤러리](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 에 다양 한 제품 팀과 커뮤니티 runbook tooget Azure SQL 데이터베이스, 다른 Azure 서비스 및 제 3 자 시스템 관리를 자동화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="16f16-117">Runbook 갤러리에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="16f16-118">SQL Server 데이터베이스에 대해 SQL 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="16f16-119">일정에 따라 Azure SQL 데이터베이스를 세로로(위쪽 또는 아래쪽) 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="16f16-120">해당 데이터베이스의 최대 크기에 도달한 경우 SQL 테이블을 줄이세요.</span><span class="sxs-lookup"><span data-stu-id="16f16-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="16f16-121">Azure SQL 데이터베이스가 심하게 조각화 된 경우 테이블에 색인을 달아주세요.</span><span class="sxs-lookup"><span data-stu-id="16f16-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="16f16-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16f16-122">Next steps</span></span>
<span data-ttu-id="16f16-123">Azure 자동화 및 Azure SQL 데이터베이스를 사용 하는 toomanage 수 있는 방법의 hello 기본 사항 학습 한를 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f16-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="16f16-124">Azure 자동화 개요</span><span class="sxs-lookup"><span data-stu-id="16f16-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="16f16-125">내 첫 번째 runbook</span><span class="sxs-lookup"><span data-stu-id="16f16-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="16f16-126">Azure 자동화 학습 맵</span><span class="sxs-lookup"><span data-stu-id="16f16-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="16f16-127">Azure 자동화: hello 클라우드에서에서 SQL 에이전트</span><span class="sxs-lookup"><span data-stu-id="16f16-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

