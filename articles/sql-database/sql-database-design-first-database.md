---
title: "첫 번째 Azure SQL Database 디자인 | Microsoft Docs"
description: "첫 번째 Azure SQL Database를 디자인하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 69cfffdae5ce2db53acc6d668dbe468c3ef22dc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="32932-103">첫 번째 Azure SQL Database 디자인</span><span class="sxs-lookup"><span data-stu-id="32932-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="32932-104">Azure SQL Database는 Microsoft Cloud("Azure")의 관계형 DBaaS(Database-As-A-Service)입니다.</span><span class="sxs-lookup"><span data-stu-id="32932-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="32932-105">이 자습서에서는 Azure Portal 및 SSMS[(SQL Server Management Studio)](https://msdn.microsoft.com/library/ms174173.aspx)를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="32932-105">In this tutorial, you learn how to use the Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="32932-106">Azure Portal에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="32932-107">Azure Portal에서 서버 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="32932-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="32932-108">SSMS로 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="32932-108">Connect to the database with SSMS</span></span>
> * <span data-ttu-id="32932-109">SSMS를 사용하여 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="32932-110">BCP를 사용하여 데이터 대량 로드</span><span class="sxs-lookup"><span data-stu-id="32932-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="32932-111">SSMS를 사용하여 해당 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="32932-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="32932-112">Azure Portal에서 데이터베이스를 이전 [특정 시점 복원](sql-database-recovery-using-backups.md#point-in-time-restore)으로 복원</span><span class="sxs-lookup"><span data-stu-id="32932-112">Restore the database to a previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in the Azure portal</span></span>

<span data-ttu-id="32932-113">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32932-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32932-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32932-114">Prerequisites</span></span>

<span data-ttu-id="32932-115">이 자습서를 완료하려면 다음을 설치했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-115">To complete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="32932-116">최신 버전의 SSMS([SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx))를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-116">The newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="32932-117">최신 버전의 [BCP 및 SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="32932-117">The newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="32932-118">Azure Portal에 로그인</span><span class="sxs-lookup"><span data-stu-id="32932-118">Log in to the Azure portal</span></span>

<span data-ttu-id="32932-119">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="32932-120">빈 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-120">Create a blank SQL database</span></span>

<span data-ttu-id="32932-121">Azure SQL Database는 일련의 정의된 [계산 및 저장소 리소스](sql-database-service-tiers.md)를 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="32932-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="32932-122">데이터베이스는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 및 [Azure SQL Database 논리 서버](sql-database-features.md)에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="32932-122">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="32932-123">빈 SQL Database를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-123">Follow these steps to create a blank SQL database.</span></span> 

1. <span data-ttu-id="32932-124">Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-124">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="32932-125">**새로 만들기** 페이지에서 **데이터베이스**를 선택하고 **데이터베이스** 페이지에서 **SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-125">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span> 

   ![빈 데이터베이스 만들기](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="32932-127">위의 이미지에 표시된 대로 다음과 같은 정보를 사용하여 SQL Database 형식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-127">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="32932-128">설정</span><span class="sxs-lookup"><span data-stu-id="32932-128">Setting</span></span>       | <span data-ttu-id="32932-129">제안 값</span><span class="sxs-lookup"><span data-stu-id="32932-129">Suggested value</span></span> | <span data-ttu-id="32932-130">설명</span><span class="sxs-lookup"><span data-stu-id="32932-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="32932-131">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="32932-131">**Database name**</span></span> | <span data-ttu-id="32932-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="32932-132">mySampleDatabase</span></span> | <span data-ttu-id="32932-133">유효한 데이터베이스 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="32932-134">**구독**</span><span class="sxs-lookup"><span data-stu-id="32932-134">**Subscription**</span></span> | <span data-ttu-id="32932-135">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="32932-135">Your subscription</span></span>  | <span data-ttu-id="32932-136">구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="32932-137">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="32932-137">**Resource group**</span></span> | <span data-ttu-id="32932-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32932-138">myResourceGroup</span></span> | <span data-ttu-id="32932-139">유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="32932-140">**원본 선택**</span><span class="sxs-lookup"><span data-stu-id="32932-140">**Select source**</span></span> | <span data-ttu-id="32932-141">빈 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="32932-141">Blank database</span></span> | <span data-ttu-id="32932-142">빈 데이터베이스를 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="32932-143">**서버**를 클릭하여 새 데이터베이스에 새 서버를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-143">Click **Server** to create and configure a new server for your new database.</span></span> <span data-ttu-id="32932-144">다음 정보로 **새 서버 양식**을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-144">Fill out the **New server form** with the following information:</span></span> 

   | <span data-ttu-id="32932-145">설정</span><span class="sxs-lookup"><span data-stu-id="32932-145">Setting</span></span>       | <span data-ttu-id="32932-146">제안 값</span><span class="sxs-lookup"><span data-stu-id="32932-146">Suggested value</span></span> | <span data-ttu-id="32932-147">설명</span><span class="sxs-lookup"><span data-stu-id="32932-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="32932-148">**서버 이름**</span><span class="sxs-lookup"><span data-stu-id="32932-148">**Server name**</span></span> | <span data-ttu-id="32932-149">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="32932-149">Any globally unique name</span></span> | <span data-ttu-id="32932-150">유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="32932-151">**서버 관리자 로그인**</span><span class="sxs-lookup"><span data-stu-id="32932-151">**Server admin login**</span></span> | <span data-ttu-id="32932-152">모든 유효한 이름</span><span class="sxs-lookup"><span data-stu-id="32932-152">Any valid name</span></span> | <span data-ttu-id="32932-153">유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="32932-154">**암호**</span><span class="sxs-lookup"><span data-stu-id="32932-154">**Password**</span></span> | <span data-ttu-id="32932-155">유효한 암호</span><span class="sxs-lookup"><span data-stu-id="32932-155">Any valid password</span></span> | <span data-ttu-id="32932-156">암호는 8자 이상이어야 하며 대문자, 소문자, 숫자 및 영숫자가 아닌 문자 범주 중 세 가지 범주의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-156">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="32932-157">**위치**</span><span class="sxs-lookup"><span data-stu-id="32932-157">**Location**</span></span> | <span data-ttu-id="32932-158">모든 유효한 위치</span><span class="sxs-lookup"><span data-stu-id="32932-158">Any valid location</span></span> | <span data-ttu-id="32932-159">지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![create database-server](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="32932-161">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-161">Click **Select**.</span></span>

6. <span data-ttu-id="32932-162">**가격 책정 계층**을 클릭하고 새 데이터베이스의 서비스 계층 및 성능 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="32932-163">이 자습서에서는 **20 DTU** 및 **250**GB의 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="32932-165">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="32932-166">빈 데이터베이스에 대한 **데이터 정렬**을 선택합니다(이 자습서의 경우 기본값 사용).</span><span class="sxs-lookup"><span data-stu-id="32932-166">Select a **collation** for the blank database (for this tutorial, use the default value).</span></span> <span data-ttu-id="32932-167">데이터 정렬에 대한 자세한 내용은 [데이터 정렬](https://docs.microsoft.com/sql/t-sql/statements/collations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="32932-168">**만들기**를 클릭하여 데이터베이스를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-168">Click **Create** to provision the database.</span></span> <span data-ttu-id="32932-169">프로비전을 완료하는 데 약 1분 30초가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="32932-169">Provisioning takes about a minute and a half to complete.</span></span> 

10. <span data-ttu-id="32932-170">도구 모음에서 **알림**을 클릭하여 배포 프로세스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-170">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![알림](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="32932-172">서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="32932-173">방화벽 규칙을 만들어서 특정 IP 주소에 대한 방화벽을 열지 않으면 SQL Database 서비스는 외부 응용 프로그램 및 도구가 서버 또는 서버의 데이터베이스에 연결되지 않도록 방지하는 서버 수준에 방화벽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32932-173">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="32932-174">다음 단계에 따라 클라이언트의 IP 주소에 대한 [SQL Database 서버 수준 방화벽 규칙](sql-database-firewall-configure.md)을 만들고 IP 주소에만 SQL Database 방화벽을 통해 외부 연결을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-174">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="32932-175">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="32932-176">회사 네트워크 내에서 연결을 시도하는 경우 포트 1433을 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-176">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="32932-177">이 경우 IT 부서에서 포트 1433을 열지 않으면 Azure SQL Database 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-177">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="32932-178">배포가 완료되면 왼쪽 메뉴에서 **SQL Database**를 클릭한 다음 **SQL Database** 페이지에서 **mySampleDatabase**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-178">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="32932-179">데이터베이스에 대한 개요 페이지가 열리고 이 페이지에 정규화된 서버 이름(예: **mynewserver20170313.database.windows.net**)이 표시되며 추가 구성을 위한 옵션도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="32932-179">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="32932-180">나중에 사용하기 위해 이 정규화된 서버 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="32932-181">이후 빠른 시작에서 서버 및 해당 데이터베이스에 연결하려면 이 정규화된 서버 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-181">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="32932-183">이전 이미지에 표시된 대로 도구 모음에서 **서버 방화벽 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-183">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="32932-184">SQL Database 서버에 대한 **방화벽 설정** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="32932-184">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![서버 방화벽 규칙](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="32932-186">도구 모음에서 **클라이언트 IP 추가**를 클릭하여 현재 IP 주소를 새 방화벽 규칙에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-186">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="32932-187">방화벽 규칙은 단일 IP 주소 또는 IP 주소의 범위에 1433 포트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="32932-188">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-188">Click **Save**.</span></span> <span data-ttu-id="32932-189">논리 서버의 1433 포트를 여는 현재 IP 주소에 서버 수준 방화벽 규칙이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="32932-189">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![set server firewall rule](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="32932-191">**확인**을 클릭한 후 **방화벽 설정** 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-191">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="32932-192">이제 SQL Server Management Studio 또는 이전에 만든 서버 관리자 계정을 사용하여 이 IP 주소에서 원하는 다른 도구를 사용하여 SQL Database 서버 및 해당 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-192">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32932-193">SQL Database 방화벽을 통한 액세스는 기본적으로 모든 Azure 서비스에 대해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32932-193">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="32932-194">이 페이지에서 **끄기**를 클릭하여 모든 Azure 서비스에 대해 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-194">Click **OFF** on this page to disable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="32932-195">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="32932-195">SQL server connection information</span></span>

<span data-ttu-id="32932-196">Azure Portal에 있는 Azure SQL Database 서버의 정규화된 서버 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="32932-196">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span></span> <span data-ttu-id="32932-197">정규화된 서버 이름을 사용하여 SQL Server Management Studio를 사용하는 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-197">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="32932-198">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-198">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="32932-199">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-199">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="32932-200">데이터베이스의 경우 Azure Portal의 **Essentials** 창에서 **서버 이름**을 찾고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-200">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span></span>

   ![연결 정보](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="32932-202">SSMS로 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="32932-202">Connect to the database with SSMS</span></span>

<span data-ttu-id="32932-203">[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용하여 Azure SQL Database 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span></span>

1. <span data-ttu-id="32932-204">SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32932-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="32932-205">**서버에 연결** 대화 상자에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-205">In the **Connect to Server** dialog box, enter the following information:</span></span>

   | <span data-ttu-id="32932-206">설정</span><span class="sxs-lookup"><span data-stu-id="32932-206">Setting</span></span>       | <span data-ttu-id="32932-207">제안 값</span><span class="sxs-lookup"><span data-stu-id="32932-207">Suggested value</span></span> | <span data-ttu-id="32932-208">설명</span><span class="sxs-lookup"><span data-stu-id="32932-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="32932-209">서버 유형</span><span class="sxs-lookup"><span data-stu-id="32932-209">Server type</span></span> | <span data-ttu-id="32932-210">데이터베이스 엔진</span><span class="sxs-lookup"><span data-stu-id="32932-210">Database engine</span></span> | <span data-ttu-id="32932-211">이 값은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="32932-211">This value is required</span></span> |
   | <span data-ttu-id="32932-212">서버 이름</span><span class="sxs-lookup"><span data-stu-id="32932-212">Server name</span></span> | <span data-ttu-id="32932-213">정규화된 서버 이름</span><span class="sxs-lookup"><span data-stu-id="32932-213">The fully qualified server name</span></span> | <span data-ttu-id="32932-214">이름은 **mynewserver20170313.database.windows.net**과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-214">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="32932-215">인증</span><span class="sxs-lookup"><span data-stu-id="32932-215">Authentication</span></span> | <span data-ttu-id="32932-216">공개</span><span class="sxs-lookup"><span data-stu-id="32932-216">SQL Server Authentication</span></span> | <span data-ttu-id="32932-217">SQL 인증은 이 자습서에서 구성한 유일한 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="32932-217">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="32932-218">로그인</span><span class="sxs-lookup"><span data-stu-id="32932-218">Login</span></span> | <span data-ttu-id="32932-219">서버 관리자 계정</span><span class="sxs-lookup"><span data-stu-id="32932-219">The server admin account</span></span> | <span data-ttu-id="32932-220">서버를 만들 때 지정한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="32932-220">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="32932-221">암호</span><span class="sxs-lookup"><span data-stu-id="32932-221">Password</span></span> | <span data-ttu-id="32932-222">서버 관리자 계정의 암호</span><span class="sxs-lookup"><span data-stu-id="32932-222">The password for your server admin account</span></span> | <span data-ttu-id="32932-223">서버를 만들 때 지정한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="32932-223">This is the password that you specified when you created the server.</span></span> |

   ![서버 연결](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="32932-225">**서버에 연결** 대화 상자에서 **옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-225">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="32932-226">**데이터베이스에 연결** 섹션에서 **mySampleDatabase**를 입력하여 이 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-226">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![서버에서 db에 연결](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="32932-228">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-228">Click **Connect**.</span></span> <span data-ttu-id="32932-229">SSMS에서 개체 탐색기 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="32932-229">The Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="32932-230">개체 탐색기에서 **데이터베이스**를 확장한 다음 **mySampleDatabase**를 확장하여 샘플 데이터베이스에 있는 개체를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="32932-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

   ![데이터베이스 개체](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-the-database"></a><span data-ttu-id="32932-232">데이터베이스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-232">Create tables in the database</span></span> 

<span data-ttu-id="32932-233">[Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)을 사용하여 대학의 학생 관리 시스템을 모델링하는 네 개의 테이블이 있는 데이터베이스 스키마 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="32932-234">사람</span><span class="sxs-lookup"><span data-stu-id="32932-234">Person</span></span>
- <span data-ttu-id="32932-235">과정</span><span class="sxs-lookup"><span data-stu-id="32932-235">Course</span></span>
- <span data-ttu-id="32932-236">학생</span><span class="sxs-lookup"><span data-stu-id="32932-236">Student</span></span>
- <span data-ttu-id="32932-237">대학의 학생 관리 시스템을 모델링하는 크레딧</span><span class="sxs-lookup"><span data-stu-id="32932-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="32932-238">다음 다이어그램에서는 이러한 테이블 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32932-238">The following diagram shows how these tables are related to each other.</span></span> <span data-ttu-id="32932-239">이러한 테이블 중 일부는 다른 테이블의 열을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="32932-240">예를 들어 Student 테이블은 **Person** 테이블의 **PersonId** 열을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-240">For example, the Student table references the **PersonId** column of the **Person** table.</span></span> <span data-ttu-id="32932-241">다이어그램에 대해 학습하여 이 자습서에서 테이블 간의 관계를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-241">Study the diagram to understand how the tables in this tutorial are related to one another.</span></span> <span data-ttu-id="32932-242">효과적인 데이터베이스 테이블을 만드는 방법에 대한 자세한 내용은 [효과적인 데이터베이스 테이블 만들기](https://msdn.microsoft.com/library/cc505842.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-242">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="32932-243">데이터 형식을 선택하는 방법은 [데이터 형식](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="32932-244">또한 [SQL Server Management Studio의 테이블 디자이너](https://msdn.microsoft.com/library/hh272695.aspx)를 사용하여 테이블을 만들고 디자인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-244">You can also use the [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) to create and design your tables.</span></span> 

![테이블 관계](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="32932-246">개체 탐색기에서 **mySampleDatabase**를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="32932-247">데이터베이스에 연결된 비어 있는 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="32932-247">A blank query window opens that is connected to your database.</span></span>

2. <span data-ttu-id="32932-248">쿼리 창에서 다음 쿼리를 실행하여 데이터베이스에 4개의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32932-248">In the query window, execute the following query to create four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![테이블 만들기](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="32932-250">사용자가 만든 테이블을 보려면 SQL Server Management Studio 개체 탐색기에서 '테이블' 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-250">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span></span>

   ![ssms 테이블 생성](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-the-tables"></a><span data-ttu-id="32932-252">테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="32932-252">Load data into the tables</span></span>

1. <span data-ttu-id="32932-253">다운로드 폴더에 **SampleTableData**라는 폴더를 만들어 데이터베이스의 샘플 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-253">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span></span> 

2. <span data-ttu-id="32932-254">다음 링크를 마우스 오른쪽 단추로 클릭하고 **SampleTableData** 폴더에 샘플 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-254">Right-click the following links and save them into the **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="32932-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="32932-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="32932-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="32932-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="32932-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="32932-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="32932-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="32932-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="32932-259">명령 프롬프트 창을 열고 SampleTableData 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-259">Open a command prompt window and navigate to the SampleTableData folder.</span></span>

4. <span data-ttu-id="32932-260">다음 명령을 실행하여 테이블에 샘플 데이터를 삽입합니다. **ServerName**, **DatabaseName**, **UserName** 및 **Password** 값은 사용자 환경에 대한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="32932-260">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="32932-261">이제 앞에서 만든 테이블에 샘플 데이터가 로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-261">You have now loaded sample data into the tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="32932-262">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="32932-262">Query data</span></span>

<span data-ttu-id="32932-263">다음 쿼리를 실행하여 데이터베이스 테이블에서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-263">Execute the following queries to retrieve information from the database tables.</span></span> <span data-ttu-id="32932-264">SQL 쿼리 작성에 대한 자세한 내용은 [SQL 쿼리 작성](https://technet.microsoft.com/library/bb264565.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32932-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span></span> <span data-ttu-id="32932-265">첫 번째 쿼리는 4개의 테이블을 모두 조인하여 'Dominick Pope' 선생님의 학생 중에 성적이 75%보다 높은 모든 학생을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-265">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="32932-266">두 번째 쿼리는 4개의 테이블을 모두 조인하여 'Noe Coleman'이 등록한 적 있는 모든 과정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-266">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="32932-267">SQL Server Management Studio 쿼리 창에서 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-267">In a SQL Server Management Studio query window, execute the following query:</span></span>

   ```sql 
   -- Find the students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. <span data-ttu-id="32932-268">SQL Server Management Studio 쿼리 창에서 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all the courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="32932-269">이전 시점으로 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="32932-269">Restore a database to a previous point in time</span></span>

<span data-ttu-id="32932-270">실수로 테이블을 삭제한 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="32932-271">이런 경우는 쉽게 복구할 수 없는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="32932-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="32932-272">Azure SQL Database를 사용하면 최근 35일 내 특정 시점으로 돌아가서 이 특정 시점을 새 데이터베이스에 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-272">Azure SQL Database allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new database.</span></span> <span data-ttu-id="32932-273">이 데이터베이스를 사용하여 삭제된 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-273">You can you this database to recover your deleted data.</span></span> <span data-ttu-id="32932-274">다음 단계를 수행하면 샘플 데이터베이스가 테이블이 추가되기 이전 시점으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="32932-274">The following steps restore the sample database to a point before the tables were added.</span></span>

1. <span data-ttu-id="32932-275">데이터베이스에 대한 SQL Database 페이지의 도구 모음에서 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-275">On the SQL Database page for your database, click **Restore** on the toolbar.</span></span> <span data-ttu-id="32932-276">**복원** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="32932-276">The **Restore** page opens.</span></span>

   ![복원](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="32932-278">필요한 정보로 **복원** 양식을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="32932-278">Fill out the **Restore** form with the required information:</span></span>
    * <span data-ttu-id="32932-279">데이터베이스 이름: 데이터베이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="32932-280">지정 시간: 복원 양식의 **지정 시간** 탭</span><span class="sxs-lookup"><span data-stu-id="32932-280">Point-in-time: Select the **Point-in-time** tab on the Restore form</span></span> 
    * <span data-ttu-id="32932-281">복원 지점: 데이터베이스를 변경하기 이전 시간 선택</span><span class="sxs-lookup"><span data-stu-id="32932-281">Restore point: Select a time that occurs before the database was changed</span></span>
    * <span data-ttu-id="32932-282">대상 서버: 데이터베이스를 복원할 때는 이 값을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="32932-283">탄력적 데이터베이스 풀: **없음** 선택</span><span class="sxs-lookup"><span data-stu-id="32932-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="32932-284">가격 책정 계층: **20DTU** 및 **250**GB의 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![복원 시점](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="32932-286">**확인**을 클릭하여 데이터베이스를 테이블이 추가되기 이전 [시점으로 복원](sql-database-recovery-using-backups.md#point-in-time-restore)합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-286">Click **OK** to restore the database to [restore to a point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before the tables were added.</span></span> <span data-ttu-id="32932-287">다른 시점으로 데이터베이스를 복원하면 지정한 시점을 기준으로 원본 데이터베이스와 동일한 서버에 중복 데이터베이스가 생성됩니다([서비스 계층](sql-database-service-tiers.md)에 대한 보존 기간 내에 있는 경우).</span><span class="sxs-lookup"><span data-stu-id="32932-287">Restoring a database to a different point in time creates a duplicate database in the same server as the original database as of the point in time you specify, as long as it is within the retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32932-288">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32932-288">Next Steps</span></span> 
<span data-ttu-id="32932-289">이 자습서에서는 데이터베이스 및 테이블 만들기, 데이터 로드 및 쿼리, 데이터베이스를 이전 시점으로 복원과 같은 기본적인 데이터베이스 작업에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="32932-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="32932-290">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="32932-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="32932-291">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-291">Create a database</span></span>
> * <span data-ttu-id="32932-292">방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="32932-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="32932-293">SQL Server Management Studio[(SSMS)](https://msdn.microsoft.com/library/ms174173.aspx)를 사용하여 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="32932-293">Connect to the database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="32932-294">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="32932-294">Create tables</span></span>
> * <span data-ttu-id="32932-295">데이터 대량 로드</span><span class="sxs-lookup"><span data-stu-id="32932-295">Bulk load data</span></span>
> * <span data-ttu-id="32932-296">해당 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="32932-296">Query that data</span></span>
> * <span data-ttu-id="32932-297">SQL Database [특정 시점 복원](sql-database-recovery-using-backups.md#point-in-time-restore) 기능을 사용하여 데이터베이스를 이전의 시점으로 복원</span><span class="sxs-lookup"><span data-stu-id="32932-297">Restore the database to a previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="32932-298">Visual Studio 및 C#을 사용하여 데이터베이스를 설계하는 방법에 대한 자세한 내용을 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="32932-298">Advance to the next tutorial to learn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="32932-299">Azure SQL Database 설계 및 C#과 ADO.NET에 연결T</span><span class="sxs-lookup"><span data-stu-id="32932-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
