---
title: "Azure SQL 데이터 웨어하우스에 aaaManage 데이터베이스 | Microsoft Docs"
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
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="8134b-104">Azure SQL 데이터 웨어하우스의 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="8134b-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8134b-105">SQL 데이터 웨어하우스는 데이터베이스 관리의 여러 측면을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="8134b-106">예를 들어 tooscale 성능 tooadjust 하기만 하 고 계산 리소스의 오른쪽 수준 hello에 대 한 비용을 지불 하 고 후자의 경우 나중에 SQL 데이터 웨어하우스 확장 및 업그레이드 뒷면의 모든 hello 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="8134b-107">경우에 합니다 toomonitor 프로그램 작업 부하 tooidentify 성능이 필요한으로 장기 실행 쿼리 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="8134b-108">또한 권한이 필요 합니다 tooperform 몇 가지 보안 작업 toomanage 사용자와 로그인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="8134b-109">이 개요에서는 SQL 데이터 웨어하우스 관리에 대한 이러한 측면에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="8134b-110">관리 도구</span><span class="sxs-lookup"><span data-stu-id="8134b-110">Management tools</span></span>
* <span data-ttu-id="8134b-111">계산 조정</span><span class="sxs-lookup"><span data-stu-id="8134b-111">Scale Compute</span></span>
* <span data-ttu-id="8134b-112">일지 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="8134b-112">Pause and Resume</span></span>
* <span data-ttu-id="8134b-113">성능 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8134b-113">Performance Best Practices</span></span>
* <span data-ttu-id="8134b-114">쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="8134b-114">Query Monitoring</span></span>
* <span data-ttu-id="8134b-115">보안</span><span class="sxs-lookup"><span data-stu-id="8134b-115">Security</span></span>
* <span data-ttu-id="8134b-116">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="8134b-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="8134b-117">관리 도구</span><span class="sxs-lookup"><span data-stu-id="8134b-117">Management tools</span></span>
<span data-ttu-id="8134b-118">SQL 데이터 웨어하우스의 다양 한 도구 toomanage 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="8134b-119">기본 설정 도구에서 개발 데이터베이스를 관리 하는 대로 tooperform 각 유형의 태스크에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8134b-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="8134b-120">Azure portal</span></span>
<span data-ttu-id="8134b-121">hello [Azure 포털] [ Azure portal] 은 웹 기반 포털 수, 업데이트 및 데이터베이스를 삭제 만들고 있는 데이터베이스 리소스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="8134b-122">이 도구는 좋은 경우 적은 수의 데이터 웨어하우스 데이터베이스를 관리 하는 azure를 시작 방금 또는 필요한 tooquickly 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="8134b-123">Azure 포털 hello로 시작 하는 tooget 참조 [SQL 데이터 웨어하우스 (Azure 포털)을 만들][Create a SQL Data Warehouse (Azure portal)]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="8134b-124">Visual Studio에서 SQL Server 데이터 도구</span><span class="sxs-lookup"><span data-stu-id="8134b-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="8134b-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) Visual Studio에서 사용 하면 tooconnect를 관리 하 고 데이터베이스를 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="8134b-126">Visual Studio 또는 다른 IDE(통합 개발 환경)에 익숙한 응용 프로그램 개발자라면 Visual Studio에서 SSDT를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8134b-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="8134b-127">SSDT hello toovisualize 사용할 수 있는 SQL Server 개체 탐색기에 포함 되어, 연결 하 고 SQL 데이터 웨어하우스 데이터베이스에 대 한 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="8134b-128">tooquickly tooSQL 데이터 웨어하우스 연결, hello 클릭 **Visual Studio에서 열기** hello Azure 클래식 포털에서에서 hello 데이터베이스 세부 정보를 볼 때 hello 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="8134b-129">Visual Studio에서 SSDT 시작 tooget 참조 [Visual Studio와 함께 Azure SQL 데이터 웨어하우스 쿼리][Query Azure SQL Data Warehouse with Visual Studio]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="8134b-130">명령줄 도구</span><span class="sxs-lookup"><span data-stu-id="8134b-130">Command-line tools</span></span>
<span data-ttu-id="8134b-131">명령줄은 워크로드 자동화에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="8134b-132">PowerShell 및 sqlcmd는 두 가지 유용한 방법은 tooautomate 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="8134b-133">이러한 도구를 관리 하기 위한 많은 수의 논리 서버는 프로덕션 환경에서 리소스 변경 필요한 hello 작업 이름이 스크립팅되고 후 자동으로 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="8134b-134">동적 관리 뷰</span><span class="sxs-lookup"><span data-stu-id="8134b-134">Dynamic management views</span></span>
<span data-ttu-id="8134b-135">Dmv는 hello 측면도 SQL 데이터 웨어하우스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="8134b-136">Hello 포털에서 표시 하는 거의 모든 정보는 Dmv를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="8134b-137">SQL 데이터 웨어하우스 Dmv 목록이 toosee 참조 [SQL 데이터 웨어하우스 시스템 뷰][SQL Data Warehouse system views]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="8134b-138">시작 tooget 참조 [연결 및 sqlcmd 사용 하 여 쿼리][Connect and query with sqlcmd], 및 [(PowerShell) 데이터베이스를 만들][Create a database (PowerShell)]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="8134b-139">계산 조정</span><span class="sxs-lookup"><span data-stu-id="8134b-139">Scale compute</span></span>
<span data-ttu-id="8134b-140">SQL 데이터 웨어하우스에서 CPU의 계산 리소스, 메모리, I/O 대역폭을 늘리거나 줄여 성능을 빠르게 확장 또는 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="8134b-141">tooscale 성능이 조정 hello 단위의 수 데이터 웨어하우스 (Dwu) SQL 데이터 웨어하우스 tooyour 데이터베이스를 할당 하기만 하면 toodo 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="8134b-142">SQL 데이터 웨어하우스를 변경 하는 hello 신속 하 게 만들고 모든 변경 내용 toohardware를 원본으로 사용 하는 hello 또는 소프트웨어를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="8134b-143">Dwu, 확장에 대 한 더 toolearn 참조 [성능을 확장]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="8134b-144">일지 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="8134b-144">Pause and resume</span></span>
<span data-ttu-id="8134b-145">toosave 비용을 일시 중지할 수 있습니다 및 다시 시작 요청 시 리소스를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="8134b-146">예를 들어 사용 하지 않을 hello 데이터베이스 hello 밤 및 주말에, 하는 경우 해당 시간 동안 일시 중지 하 고 hello 일 동안 다시 시작 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="8134b-147">Hello 데이터베이스 일시 중지 된 동안 Dwu를 청구 되지는지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="8134b-148">자세한 내용은 [계산 일시 중지][Pause compute] 및 [계산 다시 시작][Resume compute]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8134b-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="8134b-149">성능 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8134b-149">Performance Best Practices</span></span>
<span data-ttu-id="8134b-150">새로운 기술을 시작 hello 팁과 요령 hello 시작에서 가장 오른쪽 작동 하는 검색을 절약할 수 있는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="8134b-151">Microsoft의 다양한 항목에 모범 사례가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="8134b-152">여러 워크 로드를 개발할 때 가장 중요 한 고려 hello 요약 toosee 참조 [SQL 데이터 웨어하우스 모범 사례][SQL Data Warehouse Best Practices]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="8134b-153">쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="8134b-153">Query Monitoring</span></span>
<span data-ttu-id="8134b-154">쿼리가 너무 오래 실행 중인 경우에 따라 하지만 아닌 어느 것을 hello 오류의 원인이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="8134b-155">SQL 데이터 웨어하우스 쿼리 너무 오래 걸리면 아웃 동적 관리 뷰 (Dmv) toofigure를 사용할 수 있는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="8134b-156">toofind 장기 실행 쿼리 참조 [Dmv를 사용 하 여 작업을 모니터링][Monitor your workload using DMVs]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="8134b-157">보안</span><span class="sxs-lookup"><span data-stu-id="8134b-157">Security</span></span>
<span data-ttu-id="8134b-158">보안 시스템 toomaintain hello 경고 이며 모든 종류의 무단된 액세스 로부터 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="8134b-159">보안 시스템 toomake 방화벽 규칙이 충족 되는지 권한이 부여 되므로 IP 주소에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="8134b-160">사용자 자격 증명을 올바르게 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="8134b-161">사용자가 toohello 데이터베이스를 연결한 다음 hello 사용자만 있어야 권한을 tooperform 작업 수는 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="8134b-162">toosecure 데이터 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="8134b-163">감사 및 추적 하는 의심 스러운 활동 하는 경우에 이벤트를 재 추적할 수 있도록 중요 한 toohave 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="8134b-164">보안, toohello 찾아보려면 관리 하는 방법에 대 한 toolearn [보안 개요][Security overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="8134b-165">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="8134b-165">Backup and restore</span></span>
<span data-ttu-id="8134b-166">데이터의 신뢰할 수 있는 백업을 만드는 것은 프로덕션 데이터베이스의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="8134b-167">SQL 데이터 웨어하우스는 정기적으로 활성 데이터베이스를 자동으로 백업하여 데이터를 안전하게 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="8134b-168">이러한 백업을 사용 하면 데이터를 손상 하거나 데이터 나 데이터베이스를 실수로 삭제 한 시나리오에서 toorecover 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="8134b-169">Hello 데이터 백업 일정을 보존 정책에 대 한 toorestore 데이터베이스를 확인 하는 방법 및 [스냅숏에서 복원][Restore from snapshot]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="8134b-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8134b-170">Next steps</span></span>
<span data-ttu-id="8134b-171">최적의 데이터베이스 디자인 원칙을 사용 하면 더욱 쉽게 toomanage SQL 데이터 웨어하우스 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="8134b-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="8134b-172">toolearn 더 toohello 찾아보려면 [개발 개요][Development overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="8134b-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

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
[성능을 확장]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
