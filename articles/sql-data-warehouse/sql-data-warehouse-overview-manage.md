---
title: "Azure SQL Data Warehouse의 데이터베이스 관리 | Microsoft Docs"
description: "SQL 데이터 웨어하우스 데이터베이스 관리 개요. 관리 도구, DWU 및 성능 확장, 쿼리 성능 문제 해결, 보안 정책 설정, 데이터 손상 또는 지역적 중단으로부터 데이터베이스 복원 등이 포함되어 있습니다."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: b14d0aad5a1f50c225391dbab27ec6240423a65a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="55e55-104">Azure SQL 데이터 웨어하우스의 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="55e55-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="55e55-105">SQL 데이터 웨어하우스는 데이터베이스 관리의 여러 측면을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="55e55-106">예를 들어 성능을 조정하려는 경우 적정 수준의 계산 리소스를 조정하고 해당 비용만 지불하기만 하면 SQL 데이터 웨어하우스에서 모든 확장 및 축소 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-106">For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.</span></span>

<span data-ttu-id="55e55-107">성능 요구 사항을 식별하고 오래 실행되는 쿼리의 문제를 해결하기 위해 워크로드를 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-107">You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="55e55-108">또한 사용자의 권한과 로그인을 관리하기 위해 몇 가지 보안 작업도 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-108">You will also need to perform a few security tasks to manage permissions for users and logins.</span></span>

<span data-ttu-id="55e55-109">이 개요에서는 SQL 데이터 웨어하우스 관리에 대한 이러한 측면에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="55e55-110">관리 도구</span><span class="sxs-lookup"><span data-stu-id="55e55-110">Management tools</span></span>
* <span data-ttu-id="55e55-111">계산 조정</span><span class="sxs-lookup"><span data-stu-id="55e55-111">Scale Compute</span></span>
* <span data-ttu-id="55e55-112">일지 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="55e55-112">Pause and Resume</span></span>
* <span data-ttu-id="55e55-113">성능 모범 사례</span><span class="sxs-lookup"><span data-stu-id="55e55-113">Performance Best Practices</span></span>
* <span data-ttu-id="55e55-114">쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="55e55-114">Query Monitoring</span></span>
* <span data-ttu-id="55e55-115">보안</span><span class="sxs-lookup"><span data-stu-id="55e55-115">Security</span></span>
* <span data-ttu-id="55e55-116">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="55e55-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="55e55-117">관리 도구</span><span class="sxs-lookup"><span data-stu-id="55e55-117">Management tools</span></span>
<span data-ttu-id="55e55-118">다양한 도구를 사용하여 SQL 데이터 웨어하우스의 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-118">You can use a variety of tools to manage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="55e55-119">데이터베이스를 관리하면서 수행해야 하는 각 작업 유형의 도구 기본 설정을 개발해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-119">As you manage databases, you will develop tool preferences for each type of task you need to perform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="55e55-120">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="55e55-120">Azure portal</span></span>
<span data-ttu-id="55e55-121">[Azure Portal][Azure portal]은 데이터베이스를 생성, 업데이트, 삭제하고 데이터베이스 리소스를 모니터링할 수 있는 웹 기반 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-121">The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="55e55-122">Azure를 방금 시작했거나 관리하는 데이터웨어하우스 데이터베이스 수가 적거나 신속하게 작업을 수행해야 하는 경우에 매우 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.</span></span>

<span data-ttu-id="55e55-123">Azure Portal을 시작하려면 [SQL Data Warehouse 만들기(Azure Portal)][Create a SQL Data Warehouse (Azure portal)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-123">To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="55e55-124">Visual Studio에서 SQL Server 데이터 도구</span><span class="sxs-lookup"><span data-stu-id="55e55-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="55e55-125">[SSDT(SSDT(SQL Server Data Tools))][SQL Server Data Tools]를 사용하여 데이터베이스를 연결, 관리, 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases.</span></span> <span data-ttu-id="55e55-126">Visual Studio 또는 다른 IDE(통합 개발 환경)에 익숙한 응용 프로그램 개발자라면 Visual Studio에서 SSDT를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="55e55-127">SSDT에는 SQL 데이터 웨어하우스 데이터베이스에 대해 스크립트를 시각화, 연결 및 실행할 수 있게 해주는 SQL 서버 탐색기가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-127">SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="55e55-128">SQL 데이터 웨어하우스에 빠르게 연결하려면 Azure 클래식 포털에서 데이터베이스 세부 정보를 볼 때 명령 모음에서 **Visual Studio에서 열기** 단추를 클릭하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-128">To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.</span></span>  

<span data-ttu-id="55e55-129">Visual Studio에서 SSDT를 시작하려면 [Visual Studio로 Azure SQL Data Warehouse 쿼리][Query Azure SQL Data Warehouse with Visual Studio]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-129">To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="55e55-130">명령줄 도구</span><span class="sxs-lookup"><span data-stu-id="55e55-130">Command-line tools</span></span>
<span data-ttu-id="55e55-131">명령줄은 워크로드 자동화에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="55e55-132">PowerShell 및 sqlcmd는 프로세스를 자동화하는 데 적합한 두 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-132">PowerShell and sqlcmd are two great ways to automate your processes.</span></span>  <span data-ttu-id="55e55-133">이들 도구는 필수 작업을 스크립트 및 자동화할 수 있는 프로덕션 환경에서 많은 수의 논리 서버를 관리하고 리소스 변경 사항을 배포할 때 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="55e55-134">동적 관리 뷰</span><span class="sxs-lookup"><span data-stu-id="55e55-134">Dynamic management views</span></span>
<span data-ttu-id="55e55-135">SQL 데이터 웨어하우스는 주로 DMV를 사용하여 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-135">DMVs are the bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="55e55-136">포털에 표시되는 거의 모든 정보가 DMV에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-136">Almost all information that surfaces in the portal relies on DMVs.</span></span> <span data-ttu-id="55e55-137">SQL Data Warehouse DMV 목록을 보려면 [SQL Data Warehouse 시스템 뷰][SQL Data Warehouse system views]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-137">To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="55e55-138">시작하려면 [sqlcmd를 사용하여 연결 및 쿼리][Connect and query with sqlcmd] 및 [데이터베이스 만들기(PowerShell)][Create a database (PowerShell)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-138">To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="55e55-139">계산 조정</span><span class="sxs-lookup"><span data-stu-id="55e55-139">Scale compute</span></span>
<span data-ttu-id="55e55-140">SQL 데이터 웨어하우스에서 CPU의 계산 리소스, 메모리, I/O 대역폭을 늘리거나 줄여 성능을 빠르게 확장 또는 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="55e55-141">성능을 조정할 경우 SQL 데이터 웨어하우스에서 데이터베이스에 할당하는 DWU(데이터 웨어하우스 단위) 수를 조정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-141">To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database.</span></span> <span data-ttu-id="55e55-142">SQL 데이터 웨어하우스가 빠르게 변경하고 하드웨어 또는 소프트웨어의 모든 기본 변경 사항을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-142">SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.</span></span>

<span data-ttu-id="55e55-143">DWU 확장에 대한 자세한 내용은 [성능 조정]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-143">To learn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="55e55-144">일지 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="55e55-144">Pause and resume</span></span>
<span data-ttu-id="55e55-145">비용을 절약하기 위해 필요에 따라 계산 리소스를 일지 중지 및 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-145">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="55e55-146">예를 들어, 밤 시간과 주말에 데이터베이스를 사용하지 않으려면 해당 시간에 일시 중지했다가 주간에 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-146">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="55e55-147">데이터베이스 일시 중지 중에는 DWU 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-147">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="55e55-148">자세한 내용은 [계산 일시 중지][Pause compute] 및 [계산 다시 시작][Resume compute]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="55e55-149">성능 모범 사례</span><span class="sxs-lookup"><span data-stu-id="55e55-149">Performance Best Practices</span></span>
<span data-ttu-id="55e55-150">새 기술을 시작할 경우 처음부터 가장 적절한 팁과 요령을 발견하면 많은 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-150">When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.</span></span>  <span data-ttu-id="55e55-151">Microsoft의 다양한 항목에 모범 사례가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="55e55-152">워크로드를 개발할 때 가장 중요한 고려 사항의 요약 문서를 보려면 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-152">To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="55e55-153">쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="55e55-153">Query Monitoring</span></span>
<span data-ttu-id="55e55-154">쿼리가 너무 오래 실행될 때 무엇이 문제인지 확실히 파악할 수 없는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-154">Sometimes a query is running too long, but you aren't sure of which one is the culprit.</span></span> <span data-ttu-id="55e55-155">SQL 데이터 웨어하우스에는 어느 쿼리가 너무 오래 실행되는지 확인하는 데 사용하는 동적 관리 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.</span></span>

<span data-ttu-id="55e55-156">오래 실행되는 쿼리를 찾으려면 [DMV를 사용하여 워크로드 모니터링][Monitor your workload using DMVs]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-156">To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="55e55-157">보안</span><span class="sxs-lookup"><span data-stu-id="55e55-157">Security</span></span>
<span data-ttu-id="55e55-158">안전한 시스템을 유지하려면 모든 종류의 무단 액세스로부터 보호하고 경계를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-158">To maintain a secure system, you must be on the alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="55e55-159">보안 시스템은 허가된 IP 주소만 연결할 수 있도록 하는 방화벽을 구현하고</span><span class="sxs-lookup"><span data-stu-id="55e55-159">A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="55e55-160">사용자 자격 증명을 올바르게 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="55e55-161">사용자가 데이터베이스에 연결한 후에는 최소한의 작업만 수행할 수 있는 권한만 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-161">After a user has connected to the database, the user should only have permissions to perform a minimal number of actions.</span></span> <span data-ttu-id="55e55-162">데이터 보호를 위해 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-162">To secure data, you can use encryption.</span></span> <span data-ttu-id="55e55-163">또한 의심스러운 활동이 있는지 여부를 추적할 수 있도록 감사와 추적 기능을 갖추는 것도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-163">It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="55e55-164">보안 관리에 대한 자세한 내용은 [보안 개요][Security overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-164">To learn about managing security, head over to the [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="55e55-165">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="55e55-165">Backup and restore</span></span>
<span data-ttu-id="55e55-166">데이터의 신뢰할 수 있는 백업을 만드는 것은 프로덕션 데이터베이스의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="55e55-167">SQL 데이터 웨어하우스는 정기적으로 활성 데이터베이스를 자동으로 백업하여 데이터를 안전하게 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="55e55-168">이러한 백업을 사용하여 데이터를 손상했거나 데이터 또는 데이터베이스를 실수로 삭제한 시나리오에서 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-168">These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="55e55-169">데이터 백업 일정, 보존 정책 및 데이터베이스를 복원하는 방법은 [스냅숏에서 복원][Restore from snapshot]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-169">For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="55e55-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55e55-170">Next steps</span></span>
<span data-ttu-id="55e55-171">좋은 데이터베이스 디자인 원칙을 사용할 경우 SQL 데이터 웨어하우스를 더 손쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e55-171">Using good database design principles will make it easier to manage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="55e55-172">자세한 내용은 [개발 개요][Development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e55-172">To learn more, head over to the [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
<span data-ttu-id="55e55-173">[성능 조정]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span><span class="sxs-lookup"><span data-stu-id="55e55-173">[Scale performance]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span></span>
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
