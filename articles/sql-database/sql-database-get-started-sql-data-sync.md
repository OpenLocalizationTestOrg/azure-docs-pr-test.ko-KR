---
title: "Azure SQL 데이터 동기화 (미리 보기) aaaGetting 시작 | Microsoft Docs"
description: "이 자습서는 Azure SQL 데이터 동기화(미리 보기)를 시작하도록 도와줍니다."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="81b8b-103">Azure SQL 데이터 동기화 시작(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="81b8b-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="81b8b-104">이 자습서에서는 하이브리드 동기화 그룹을 만들어 Azure SQL 데이터 동기화를 tooset Azure SQL 데이터베이스와 SQL Server 인스턴스를 포함 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="81b8b-105">hello 새 동기화 그룹 구성 완벽 하 게 되 고 설정한 hello 일정에 따라 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="81b8b-106">이 자습서에서는 사용자가 SQL Database 및 SQL Server를 사용해본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="81b8b-107">SQL 데이터 동기화의 개요는 [데이터 동기화](sql-database-sync-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b8b-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="81b8b-108">전체 PowerShell 보여 주는 예제 tooconfigure SQL 데이터 동기화 hello 다음 문서를 참조 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="81b8b-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="81b8b-109">여러 Azure SQL 데이터베이스 간에 toosync PowerShell을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="81b8b-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="81b8b-110">Azure SQL 데이터베이스와 SQL Server 온-프레미스 데이터베이스 간의 toosync PowerShell을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="81b8b-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="81b8b-111">hello 전체 기술 설명서 MSDN에 있는 이전 Azure SQL 데이터 동기화에 대 한 집합은 사용할 수는 있습니다. PDF 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="81b8b-112">[여기](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)에서 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="81b8b-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="81b8b-113">1단계 - 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="81b8b-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="81b8b-114">Hello 데이터 동기화를 찾아보려면</span><span class="sxs-lookup"><span data-stu-id="81b8b-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="81b8b-115">브라우저에서 toohello Azure 포털을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="81b8b-116">Hello 포털에서 SQL 데이터베이스를 대시보드 또는 hello SQL 데이터베이스 아이콘에서 hello 도구 모음에서 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Azure SQL Database 목록](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="81b8b-118">Hello에 **SQL 데이터베이스** 블레이드, 선택 hello 기존 SQL 데이터베이스는 원하는 toouse hello 허브 데이터베이스 데이터 동기화. hello SQL 데이터베이스 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="81b8b-119">Hello 선택한 데이터베이스에 대 한 SQL 데이터베이스 블레이드에서 hello 선택 **tooother 데이터베이스를 동기화**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="81b8b-120">hello 데이터 동기화 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-120">hello Data Sync blade opens.</span></span>

    ![Sync tooother 데이터베이스 옵션](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="81b8b-122">새 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="81b8b-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="81b8b-123">Hello 데이터 동기화 블레이드에서 선택 **새 동기화 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="81b8b-124">hello **새 동기화 그룹** 단계 1, 블레이드에서 열립니다 **동기화 그룹 만들기**, 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="81b8b-125">hello **데이터 동기화 그룹 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="81b8b-126">Hello에 **데이터 동기화 그룹 만들기** 블레이드에서 작업 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="81b8b-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="81b8b-127">Hello에 **동기화 그룹 이름은** 필드 hello 새 동기화 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="81b8b-128">Hello에 **동기화 메타 데이터 데이터베이스** 섹션에서 toocreate (권장) 새 데이터베이스 또는 toouse 기존의 데이터베이스 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="81b8b-129">동기화 메타 데이터 데이터베이스 hello으로 빈 새 데이터베이스 toouse를 만들어야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="81b8b-130">데이터 동기화는 이 데이터베이스에서 테이블을 만들고 자주 실행되는 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="81b8b-131">이 데이터베이스는 자동으로 모든 hello 선택한 지역에서 동기화 그룹에 대 한 동기화 메타 데이터 데이터베이스 hello로 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="81b8b-132">Hello 동기화 메타 데이터 데이터베이스, 해당 이름 또는 서비스 수준이 놓지 않고 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="81b8b-133">**새 데이터베이스**를 선택한 경우 **새 데이터베이스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="81b8b-134">hello **SQL 데이터베이스** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="81b8b-135">Hello에 **SQL 데이터베이스** 블레이드에서 이름을 지정 하 고 hello 새 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="81b8b-136">그런 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-136">Then select **OK**.</span></span>

        <span data-ttu-id="81b8b-137">선택한 경우 **기존 데이터베이스를 사용 하 여**선택, hello 목록에서 hello 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="81b8b-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="81b8b-138">Hello에 **자동 동기화** 섹션을 먼저 선택 **에** 또는 **오프**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="81b8b-139">선택한 경우 **에**, hello에 **동기화 빈도** 섹션 번호를 입력 하 고 초, 분, 시간 또는 일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![동기화 빈도 지정](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="81b8b-141">Hello에 **충돌 해결** 섹션에서 "허브 wins" 또는 "멤버 wins."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![충돌 해결 방법 지정](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="81b8b-143">선택 **확인** hello 새 동기화 그룹 toobe 만들고 배포 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="81b8b-144">2단계 - 동기화 구성원 추가</span><span class="sxs-lookup"><span data-stu-id="81b8b-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="81b8b-145">Hello 새 동기화 그룹을 만들고 배포 하 고, 2 단계 후 **동기화 멤버 추가**, hello에서 강조 표시 됩니다 **새 동기화 그룹** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="81b8b-146">Hello에 **허브 데이터베이스** 섹션에서 어떤 hello 허브 데이터베이스가 hello SQL 데이터베이스 서버에 대 한 hello 기존 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="81b8b-147">이 섹션에서 *새* 자격 증명을 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-147">Don't enter *new* credentials in this section.</span></span>

![허브 데이터베이스가 toosync 그룹 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="81b8b-149">Azure SQL Database 추가</span><span class="sxs-lookup"><span data-stu-id="81b8b-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="81b8b-150">Hello에 **멤버 데이터베이스** 섹션에서 필요에 따라 선택 하 여 Azure SQL 데이터베이스 toohello 동기화 그룹을 추가할 **Azure 데이터베이스를 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="81b8b-151">hello **Azure 데이터베이스를 구성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="81b8b-152">Hello에 **Azure 데이터베이스를 구성** 블레이드에서 작업 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="81b8b-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="81b8b-153">Hello에 **동기화 멤버 이름** 필드 hello 새 동기화 멤버에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="81b8b-154">이 이름은 hello 데이터베이스 자체의 hello 이름과 구별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="81b8b-155">Hello에 **구독** 필드를 선택 하는 hello 청구 용 Azure 구독에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="81b8b-156">Hello에 **Azure SQL Server** 기존 SQL 데이터베이스 서버 hello 필드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="81b8b-157">Hello에 **Azure SQL 데이터베이스** 기존 SQL 데이터베이스 hello 필드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="81b8b-158">Hello에 **동기화 방향이** 필드에서는 양방향 동기화, 허브 toohello 선택 또는 hello 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![새 SQL Database 동기화 구성원 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="81b8b-160">Hello에 **Username** 및 **암호** 필드는 hello 멤버 데이터베이스가 hello SQL 데이터베이스 서버에 대 한 hello 기존 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="81b8b-161">이 섹션에서 *새* 자격 증명을 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="81b8b-162">선택 **확인** hello 새 동기화 멤버 toobe 만들고 배포 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![새 SQL Database 동기화 구성원 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="81b8b-164">온-프레미스 SQL Server 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="81b8b-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="81b8b-165">Hello에 **멤버 데이터베이스** 섹션에서 필요에 따라 온-프레미스 SQL Server toohello 동기화 그룹을 선택 하 여 추가 **온-프레미스 데이터베이스를 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="81b8b-166">hello **구성 온-프레미스** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="81b8b-167">Hello에 **구성 온-프레미스** 블레이드에서 작업 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="81b8b-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="81b8b-168">선택 **선택 hello 동기화 에이전트 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="81b8b-169">hello **동기화 에이전트 선택** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Hello 동기화 에이전트 게이트웨이 선택](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="81b8b-171">Hello에 **선택 hello 동기화 에이전트 게이트웨이** 블레이드에서 선택 여부를 toouse 기존 에이전트 하거나 새 에이전트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="81b8b-172">선택한 경우 **기존 에이전트**, 선택 hello hello 목록에서 기존 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="81b8b-173">선택한 경우 **새 에이전트를 만들고**, 작업이 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="81b8b-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="81b8b-174">제공 하는 hello 링크 hello 클라이언트 동기화 에이전트 소프트웨어를 다운로드 하 고 hello SQL Server가 있는 hello 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="81b8b-175">Tooopen 아웃 바운드 TCP 포트 1433 hello 방화벽 toolet hello 클라이언트 에이전트의 hello 서버와 통신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="81b8b-176">Hello 에이전트에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="81b8b-177">**키 만들기 및 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="81b8b-178">Hello 에이전트 키 toohello 클립보드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![새 동기화 에이전트 만들기](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="81b8b-180">선택 **확인** tooclose hello **동기화 에이전트 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="81b8b-181">SQL Server 컴퓨터-hello에서 찾아 hello 클라이언트 동기화 에이전트 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![hello 데이터 동기화 클라이언트 에이전트 응용 프로그램](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="81b8b-183">Hello 동기화 에이전트 app **에이전트 키 전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="81b8b-184">hello **동기화 메타 데이터 데이터베이스 구성** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="81b8b-185">Hello에 **동기화 메타 데이터 데이터베이스 구성** 대화 상자, 붙여넣기에 hello 에이전트 키 hello Azure 포털에서에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="81b8b-186">또한 hello는 hello 메타 데이터 데이터베이스가 hello Azure SQL 데이터베이스 서버에 대 한 기존 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="81b8b-187">(새 메타 데이터 데이터베이스를 만든 경우이 데이터베이스는 hello hello 허브 데이터베이스와 같은 서버입니다.) 선택 **확인** hello 구성 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Hello 에이전트 키 및 서버 자격 증명을 입력 합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="81b8b-189">이 시점에서 방화벽 오류를 발생 하면 toocreate 방화벽 규칙이 있는 hello SQL Server 컴퓨터에서 Azure tooallow 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="81b8b-190">Hello 포털에서 수동으로 hello 규칙을 만들 수 있지만 toocreate 더 쉽게 찾을 수 있습니다이 SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="81b8b-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="81b8b-191">SSMS에서 Azure에서 tooconnect toohello 허브 데이터베이스를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="81b8b-192">데이터베이스 이름을 \<hub_database_name\>.database.windows.net으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="81b8b-193">Hello 대화 상자 tooconfigure hello Azure 방화벽 규칙의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="81b8b-194">Toohello 클라이언트 동기화 에이전트 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="81b8b-195">Hello 클라이언트 동기화 에이전트 응용 프로그램에서 클릭 **등록** tooregister hello 에이전트와 SQL Server 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="81b8b-196">hello **SQL Server 구성** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![SQL Server 데이터베이스를 추가하고 구성합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="81b8b-198">Hello에 **SQL Server 구성** 대화 상자에서 선택 하는지 여부를 SQL Server 인증 또는 Windows 인증을 사용 하 여 tooconnect 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="81b8b-199">SQL Server 인증을 선택한 경우 hello 기존 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="81b8b-200">원하는 toosync hello SQL Server 이름과 hello hello 데이터베이스 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="81b8b-201">선택 **연결 테스트** tootest 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="81b8b-202">그런 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-202">Then select **Save**.</span></span> <span data-ttu-id="81b8b-203">hello 등록된 데이터베이스 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-203">hello registered database appears in hello list.</span></span>

        ![SQL Server 데이터베이스를 지금 등록합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="81b8b-205">이제 hello 클라이언트 동기화 에이전트 앱을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="81b8b-206">Hello 포털 hello **구성 온-프레미스** 블레이드를 **선택 hello 데이터베이스입니다.**</span><span class="sxs-lookup"><span data-stu-id="81b8b-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="81b8b-207">hello **데이터베이스 선택** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="81b8b-208">Hello에 **데이터베이스 선택** 블레이드 hello **동기화 멤버 이름** 필드 hello 새 동기화 멤버에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="81b8b-209">이 이름은 hello 데이터베이스 자체의 hello 이름과 구별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="81b8b-210">Hello 데이터베이스 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-210">Select hello database from hello list.</span></span> <span data-ttu-id="81b8b-211">Hello에 **동기화 방향이** 필드에서는 양방향 동기화, 허브 toohello 선택 또는 hello 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![내부 데이터베이스에 대 한 hello를 선택 합니다.](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="81b8b-213">선택 **확인** tooclose hello **데이터베이스 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="81b8b-214">그런 다음 선택 **확인** tooclose hello **구성 온-프레미스** 블레이드에 대 한 대기 hello에 대 한 새 멤버 toobe을 만들고 배포한 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="81b8b-215">마지막으로, 클릭 **확인** tooclose hello **동기화 멤버 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![내부 데이터베이스에서 toosync 그룹 추가](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="81b8b-217">tooconnect tooSQL 데이터 동기화 및 hello 로컬 에이전트 사용자 이름이 toohello 역할 추가 `DataSync_Executor`합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="81b8b-218">데이터 동기화는 hello SQL Server 인스턴스에서이 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="81b8b-219">3단계 - 동기화 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="81b8b-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="81b8b-220">Hello 새 동기화 그룹 멤버가 생성 되어 배포 3 단계 후 **동기화 그룹 구성**, hello에서 강조 표시 됩니다 **새 동기화 그룹** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="81b8b-221">Hello에 **테이블** 블레이드에서 선택 데이터베이스 동기화의 hello 목록에서 멤버를 그룹화 한 다음 선택 **스키마 새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="81b8b-222">사용 가능한 테이블 hello 목록에서 원하는 toosync hello 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![테이블 선택 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="81b8b-224">Hello 테이블의 모든 열은 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="81b8b-225">않으려면 toosync 모든 hello 열, toosync 않도록 hello 열에 대 한 hello 확인란을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="81b8b-226">Tooleave hello 기본 키 열을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-226">Be sure tooleave hello primary key column selected.</span></span>

    ![필드 선택 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="81b8b-228">마지막으로 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81b8b-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81b8b-229">Next steps</span></span>
<span data-ttu-id="81b8b-230">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-230">Congratulations.</span></span> <span data-ttu-id="81b8b-231">SQL Database 인스턴스와 SQL Server 데이터베이스가 모두 포함된 동기화 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="81b8b-232">SQL Database 및 SQL 데이터 동기화에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b8b-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="81b8b-233">Hello 전체 SQL 데이터 동기화 기술 설명서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b8b-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="81b8b-234">Hello SQL 데이터 동기화 REST API 설명서 다운로드</span><span class="sxs-lookup"><span data-stu-id="81b8b-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="81b8b-235">SQL 데이터베이스 개요</span><span class="sxs-lookup"><span data-stu-id="81b8b-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="81b8b-236">데이터베이스 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="81b8b-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
