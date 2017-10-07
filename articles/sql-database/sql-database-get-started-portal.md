---
title: "Azure Portal: SQL Database 만들기 | Microsoft Docs"
description: "Toocreate SQL 데이터베이스 논리 서버, 서버 수준 방화벽 규칙의 데이터베이스 및 Azure 포털을 hello 방법에 대해 알아봅니다. Tooquery hello Azure 포털을 사용 하 여 Azure SQL 데이터베이스 또한 알아봅니다."
keywords: "SQL 데이터베이스 자습서, SQL 데이터베이스 만들기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a><span data-ttu-id="86b47-105">Hello Azure 포털에서에서 Azure SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="86b47-105">Create an Azure SQL database in hello Azure portal</span></span>

<span data-ttu-id="86b47-106">이 빠른 시작 자습서는 Azure에서 SQL toocreate 데이터베이스 방법 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-106">This quick start tutorial walks through how toocreate a SQL database in Azure.</span></span> <span data-ttu-id="86b47-107">Azure SQL 데이터베이스는는 "데이터베이스-as a Service" 수 있게 해 주는 hello 클라우드에서 toorun와 소수 자릿수 항상 사용 가능한 SQL Server 데이터베이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you toorun and scale highly available SQL Server databases in hello cloud.</span></span> <span data-ttu-id="86b47-108">이 빠른 시작에서는 tooget hello Azure 포털을 사용 하 여 SQL 데이터베이스를 만들고 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-108">This quick start shows you how tooget started by creating a SQL database using hello Azure portal.</span></span>

<span data-ttu-id="86b47-109">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="86b47-110">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="86b47-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="86b47-111">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="86b47-112">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="86b47-112">Create a SQL database</span></span>

<span data-ttu-id="86b47-113">Azure SQL Database는 일련의 정의된 [계산 및 저장소 리소스](sql-database-service-tiers.md)를 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="86b47-114">hello 데이터베이스 내에서 만들어집니다는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 및는 [Azure SQL 데이터베이스 논리 서버](sql-database-features.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-114">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="86b47-115">이러한 단계 toocreate hello Adventure Works LT 예제 데이터를 포함 하는 SQL 데이터베이스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-115">Follow these steps toocreate a SQL database containing hello Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="86b47-116">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-116">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="86b47-117">선택 **데이터베이스** hello에서 **새로** 선택한 페이지 **SQL 데이터베이스** hello에서 **데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="86b47-117">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span>

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="86b47-119">Hello 이미지 앞에 표시 된 대로 hello SQL 데이터베이스에 대 한 양식을 사용 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-119">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="86b47-120">설정</span><span class="sxs-lookup"><span data-stu-id="86b47-120">Setting</span></span>       | <span data-ttu-id="86b47-121">제안 값</span><span class="sxs-lookup"><span data-stu-id="86b47-121">Suggested value</span></span> | <span data-ttu-id="86b47-122">설명</span><span class="sxs-lookup"><span data-stu-id="86b47-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="86b47-123">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="86b47-123">**Database name**</span></span> | <span data-ttu-id="86b47-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="86b47-124">mySampleDatabase</span></span> | <span data-ttu-id="86b47-125">유효한 데이터베이스 이름은 [데이터베이스 식별자](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="86b47-126">**구독**</span><span class="sxs-lookup"><span data-stu-id="86b47-126">**Subscription**</span></span> | <span data-ttu-id="86b47-127">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="86b47-127">Your subscription</span></span>  | <span data-ttu-id="86b47-128">구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="86b47-129">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="86b47-129">**Resource group**</span></span>  | <span data-ttu-id="86b47-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86b47-130">myResourceGroup</span></span> | <span data-ttu-id="86b47-131">유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="86b47-132">**원본 소스**</span><span class="sxs-lookup"><span data-stu-id="86b47-132">**Source source**</span></span> | <span data-ttu-id="86b47-133">샘플(AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="86b47-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="86b47-134">새 데이터베이스를 hello AdventureWorksLT 스키마와 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="86b47-134">Loads hello AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="86b47-135">이 빠른 시작의 hello 나머지 부분에 사용 되므로이 양식에 hello 예제 데이터베이스를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-135">You must select hello sample database on this form because it is used in hello remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="86b47-136">아래 **서버**, 클릭 **필요한 설정 구성** hello 다음 이미지에 표시 된 것과 같이 hello로 SQL server (논리 서버) 형식 hello 사용자에 게 다음 정보를 및:</span><span class="sxs-lookup"><span data-stu-id="86b47-136">Under **Server**, click **Configure required settings** and fill out hello SQL server (logical server) form with hello following information, as shown on hello following image:</span></span>   

   | <span data-ttu-id="86b47-137">설정</span><span class="sxs-lookup"><span data-stu-id="86b47-137">Setting</span></span>       | <span data-ttu-id="86b47-138">제안 값</span><span class="sxs-lookup"><span data-stu-id="86b47-138">Suggested value</span></span> | <span data-ttu-id="86b47-139">설명</span><span class="sxs-lookup"><span data-stu-id="86b47-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="86b47-140">**서버 이름**</span><span class="sxs-lookup"><span data-stu-id="86b47-140">**Server name**</span></span> | <span data-ttu-id="86b47-141">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="86b47-141">Any globally unique name</span></span> | <span data-ttu-id="86b47-142">유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="86b47-143">**서버 관리자 로그인**</span><span class="sxs-lookup"><span data-stu-id="86b47-143">**Server admin login**</span></span> | <span data-ttu-id="86b47-144">모든 유효한 이름</span><span class="sxs-lookup"><span data-stu-id="86b47-144">Any valid name</span></span> | <span data-ttu-id="86b47-145">유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="86b47-146">**암호**</span><span class="sxs-lookup"><span data-stu-id="86b47-146">**Password**</span></span> | <span data-ttu-id="86b47-147">유효한 암호</span><span class="sxs-lookup"><span data-stu-id="86b47-147">Any valid password</span></span> | <span data-ttu-id="86b47-148">암호가 8 자 이상 있어야 하며 hello 다음 범주 중 세 범주의 문자를 포함 해야 합니다: 대문자, 소문자, 숫자 및 및 영숫자가 아닌 문자.</span><span class="sxs-lookup"><span data-stu-id="86b47-148">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="86b47-149">**구독**</span><span class="sxs-lookup"><span data-stu-id="86b47-149">**Subscription**</span></span> | <span data-ttu-id="86b47-150">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="86b47-150">Your subscription</span></span> | <span data-ttu-id="86b47-151">구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="86b47-152">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="86b47-152">**Resource group**</span></span> | <span data-ttu-id="86b47-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86b47-153">myResourceGroup</span></span> | <span data-ttu-id="86b47-154">유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="86b47-155">**위치**:</span><span class="sxs-lookup"><span data-stu-id="86b47-155">**Location**</span></span> | <span data-ttu-id="86b47-156">모든 유효한 위치</span><span class="sxs-lookup"><span data-stu-id="86b47-156">Any valid location</span></span> | <span data-ttu-id="86b47-157">지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="86b47-158">여기서 지정 하는 hello 서버 관리자 로그인 및 암호는 toohello 서버에서 필요한 toolog와이 빠른 시작의 뒷부분에 나오는 해당 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="86b47-158">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="86b47-159">나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-159">Remember or record this information for later use.</span></span> 
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="86b47-161">Hello 폼을 완료 했으면 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-161">When you have completed hello form, click **Select**.</span></span>

6. <span data-ttu-id="86b47-162">클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="86b47-163">슬라이더 tooselect hello를 사용 하 여 **20 Dtu** 및 **250** g B의 저장소가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-163">Use hello slider tooselect **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="86b47-164">DTU에 대한 자세한 내용은 [DTU란?](sql-database-what-is-a-dtu.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="86b47-166">Dtu 선택한 hello 지나면 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-166">After selected hello amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="86b47-167">이제 SQL 데이터베이스 폼 hello를 완료 했으면 클릭 **만들기** tooprovision hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-167">Now that you have completed hello SQL Database form, click **Create** tooprovision hello database.</span></span> <span data-ttu-id="86b47-168">프로비전하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="86b47-169">Hello 도구 모음에서 **알림** toomonitor hello 배포 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-169">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![알림](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="86b47-171">서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="86b47-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="86b47-172">hello SQL 데이터베이스 서비스는 hello 서버 수준 방화벽 규칙은 특정 IP 주소에 대 한 tooopen hello 방화벽을 만들지 않은 toohello 서버나 hello 서버에 있는 모든 데이터베이스를 연결 하지 못하도록 외부 응용 프로그램 및 도구를 방지 하에 방화벽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-172">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="86b47-173">이러한 단계 toocreate에 따라 한 [SQL 데이터베이스 서버 수준 방화벽 규칙](sql-database-firewall-configure.md) 클라이언트의 IP 주소에 대 한 사용자만 IP 주소에 대 한 hello SQL 데이터베이스 방화벽을 통해 외부 연결을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-173">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="86b47-174">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="86b47-175">회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-175">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="86b47-176">이 경우에 IT 부서는 포트 1433을 엽니다 하지 않는 한 tooyour Azure SQL 데이터베이스 서버를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-176">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="86b47-177">Hello 배포가 완료 된 후 클릭 **SQL 데이터베이스** hello 왼쪽 메뉴에서 **mySampleDatabase** hello에 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="86b47-177">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="86b47-178">hello 완벽 하 게 hello 보여 주는 데이터베이스 열리면 프로그램에 대 한 개요 페이지에 정규화 된 서버 이름 (예: **mynewserver20170313.database.windows.net**) 하 고 더 이상의 구성에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-178">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="86b47-179">나중에 사용하기 위해 이 정규화된 서버 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="86b47-180">이 정규화 된 서버 이름 tooconnect tooyour 서버와 데이터베이스의 후속 빠른 시작 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-180">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="86b47-182">클릭 **서버 방화벽 설정** hello 이전 그림에 나와 있는 것 처럼 hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-182">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="86b47-183">hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-183">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![서버 방화벽 규칙](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="86b47-185">클릭 **클라이언트 IP 추가** hello 도구 모음 tooadd에 현재 IP 주소 tooa 새 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-185">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="86b47-186">방화벽 규칙은 단일 IP 주소 또는 IP 주소의 범위에 1433 포트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="86b47-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-187">Click **Save**.</span></span> <span data-ttu-id="86b47-188">서버 수준 방화벽 규칙 hello 논리 서버에 포트 1433을 열지 현재 IP 주소에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-188">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![set server firewall rule](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="86b47-190">클릭 **확인** hello 다음 닫고 **방화벽 설정** 페이지.</span><span class="sxs-lookup"><span data-stu-id="86b47-190">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="86b47-191">Toohello SQL 데이터베이스 서버와 SQL Server Management Studio 또는 이전에 만든 hello 서버 관리자 계정을 사용 하 여이 IP 주소에서 선택한 다른 도구를 사용 하 여 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-191">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86b47-192">기본적으로 액세스 hello SQL 데이터베이스 방화벽을 통해 모든 Azure 서비스에 대해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-192">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="86b47-193">클릭 **OFF** 모든 Azure 서비스에 대 한이 페이지 toodisable에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-193">Click **OFF** on this page toodisable for all Azure services.</span></span>
>

## <a name="query-hello-sql-database"></a><span data-ttu-id="86b47-194">Hello SQL 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="86b47-194">Query hello SQL database</span></span>

<span data-ttu-id="86b47-195">Azure에서 예제 데이터베이스를 만든 hello Azure 포털 tooconfirm toohello 데이터베이스 데이터 및 쿼리 hello를 연결할 수 있는지 내 hello 기본 제공 쿼리 도구를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-195">Now that you have created a sample database in Azure, let’s use hello built-in query tool within hello Azure portal tooconfirm that you can connect toohello database and query hello data.</span></span> 

1. <span data-ttu-id="86b47-196">데이터베이스에 대 한 hello SQL 데이터베이스 페이지에서 클릭 **도구** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-196">On hello SQL Database page for your database, click **Tools** on hello toolbar.</span></span> <span data-ttu-id="86b47-197">hello **도구** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-197">hello **Tools** page opens.</span></span>

   ![도구 메뉴](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="86b47-199">클릭 **쿼리 편집기 (미리 보기)**, hello 클릭 **용어를 미리 볼** 확인란을 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-199">Click **Query editor (preview)**, click hello **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="86b47-200">hello 쿼리 편집기 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-200">hello Query editor page opens.</span></span>

3. <span data-ttu-id="86b47-201">클릭 **로그인** 대화 상자가 나타나면 다음을 선택 하 고 **SQL server 인증** hello 서버 관리자 로그인과 이전에 만든 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide hello server admin login and password that you created earlier.</span></span>

   ![로그인](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="86b47-203">클릭 **확인** toolog에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-203">Click **OK** toolog in.</span></span>

5. <span data-ttu-id="86b47-204">인증 된 후 hello 다음 hello 쿼리 편집기 창에서 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-204">After you are authenticated, type hello following query in hello query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="86b47-205">클릭 **실행** hello에 hello 쿼리 결과 검토 한 다음 **결과** 창.</span><span class="sxs-lookup"><span data-stu-id="86b47-205">Click **Run** and then review hello query results in hello **Results** pane.</span></span>

   ![쿼리 편집기 결과](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="86b47-207">닫기 hello **쿼리 편집기** 페이지와 hello **도구** 페이지.</span><span class="sxs-lookup"><span data-stu-id="86b47-207">Close hello **Query editor** page and hello **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="86b47-208">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="86b47-208">Clean up resources</span></span>

<span data-ttu-id="86b47-209">빠른 시작/자습서에 대 한이 리소스인 경우 필요 하지 않습니다 (참조 [다음 단계](#next-steps)), hello 다음을 수행 하 여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing hello following:</span></span>


1. <span data-ttu-id="86b47-210">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 클릭 하 고 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-210">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="86b47-211">리소스 그룹 페이지에서 클릭 **삭제**, 형식 **myResourceGroup** hello 텍스트 상자와 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-211">On your resource group page, click **Delete**, type **myResourceGroup** in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86b47-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86b47-212">Next steps</span></span>

<span data-ttu-id="86b47-213">이제 데이터베이스가 생겼으니 자주 사용하는 도구를 사용하여 데이터베이스에 연결하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86b47-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="86b47-214">아래에서 도구를 선택하여 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="86b47-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="86b47-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="86b47-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="86b47-216">Contact.java</span><span class="sxs-lookup"><span data-stu-id="86b47-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="86b47-217">.NET</span><span class="sxs-lookup"><span data-stu-id="86b47-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="86b47-218">PHP</span><span class="sxs-lookup"><span data-stu-id="86b47-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="86b47-219">Node.JS</span><span class="sxs-lookup"><span data-stu-id="86b47-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="86b47-220">Java</span><span class="sxs-lookup"><span data-stu-id="86b47-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="86b47-221">Python</span><span class="sxs-lookup"><span data-stu-id="86b47-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="86b47-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="86b47-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
