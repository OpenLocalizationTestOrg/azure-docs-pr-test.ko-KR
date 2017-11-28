---
title: "Azure SQL 데이터베이스 지리적으로 분산 솔루션 aaaImplement | Microsoft Docs"
description: "Tooconfigure 데이터베이스, Azure SQL 데이터베이스 및 장애 조치 tooa 복제에 대 한 응용 프로그램 및 테스트 장애 조치에 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="4a6c3-103">지리적으로 분산된 데이터베이스 구현</span><span class="sxs-lookup"><span data-stu-id="4a6c3-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="4a6c3-104">이 자습서에서는 Azure SQL 데이터베이스 및 응용 프로그램 장애 조치 tooa 원격 영역에 대 한 구성 하 고 장애 조치 계획을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="4a6c3-105">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4a6c3-106">데이터베이스 사용자를 만들고 권한 부여</span><span class="sxs-lookup"><span data-stu-id="4a6c3-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="4a6c3-107">데이터베이스 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="4a6c3-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="4a6c3-108">[지역에서 복제 장애 조치(failover) 그룹](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4a6c3-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="4a6c3-109">만들고 컴파일하는 Java 응용 프로그램 tooquery Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4a6c3-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="4a6c3-110">재해 복구 훈련 수행</span><span class="sxs-lookup"><span data-stu-id="4a6c3-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="4a6c3-111">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4a6c3-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4a6c3-112">Prerequisites</span></span>

<span data-ttu-id="4a6c3-113">toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="4a6c3-114">설치 된 hello 최신 [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="4a6c3-115">Azure SQL Database를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="4a6c3-116">이 자습서는 hello AdventureWorksLT 샘플 데이터베이스의 이름으로 사용 하 여 **mySampleDatabase** 이러한 빠른 시작 중 하나에서:</span><span class="sxs-lookup"><span data-stu-id="4a6c3-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="4a6c3-117">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="4a6c3-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="4a6c3-118">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="4a6c3-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="4a6c3-119">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a6c3-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="4a6c3-120">식별 메서드 tooexecute SQL 데이터베이스에 대해 스크립트를 사용할 수 있습니다 hello 쿼리 도구를 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="4a6c3-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="4a6c3-121">hello의 쿼리 편집기를 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4a6c3-122">Hello 쿼리 편집기를 사용 하 여 hello Azure 포털에에서 대 한 자세한 내용은 참조 하십시오. [연결 및 쿼리 편집기를 사용 하 여 쿼리](sql-database-get-started-portal.md#query-the-sql-database)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="4a6c3-123">최신 버전의 hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), 하는 SQL Server tooSQL Microsoft Windows에 대 한 데이터베이스에서에서 모든 SQL 인프라를 관리 하기 위한 통합된 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="4a6c3-124">최신 버전의 hello [Visual Studio Code](https://code.visualstudio.com/docs), Linux, macOS 등에 대 한 그래픽 코드 편집기는 및 확장을 포함 하 여 원하는 Windows hello [확장명이 mssql](https://aka.ms/mssql-marketplace) Microsoft SQL Server를 쿼리 하기 위한 Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="4a6c3-125">Azure SQL Database에서 이 도구를 사용하는 방법에 대한 자세한 내용은 [VS Code를 사용하여 연결 및 쿼리](sql-database-connect-query-vscode.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="4a6c3-126">데이터베이스 사용자를 만들고 권한 부여</span><span class="sxs-lookup"><span data-stu-id="4a6c3-126">Create database users and grant permissions</span></span>

<span data-ttu-id="4a6c3-127">Tooyour 데이터베이스를 연결 하 고 hello 쿼리 도구를 다음 중 하나를 사용 하 여 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="4a6c3-128">hello Azure 포털의에서 hello 쿼리 편집기</span><span class="sxs-lookup"><span data-stu-id="4a6c3-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="4a6c3-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="4a6c3-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="4a6c3-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4a6c3-130">Visual Studio Code</span></span>

<span data-ttu-id="4a6c3-131">이러한 사용자 계정은 tooyour 보조 서버를 자동으로 복제 한 동기화 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="4a6c3-132">toouse SQL Server Management Studio 또는 Visual Studio Code IP 주소를 구성 하지 않은 아직 방화벽에서 클라이언트에서 연결 하는 경우 tooconfigure 방화벽 규칙을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="4a6c3-133">자세한 단계에 대해서는 [서버 수준 방화벽 규칙 만들기](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="4a6c3-134">쿼리 창에서 데이터베이스의 쿼리 toocreate 두 개의 사용자 계정이 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="4a6c3-135">이 스크립트를 부여 **db_owner** 권한 toohello **app_admin** 계정 및 권한 부여 **선택** 및 **업데이트** toohello 사용 권한 **app_user** 계정.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="4a6c3-136">데이터베이스 수준 방화벽 만들기</span><span class="sxs-lookup"><span data-stu-id="4a6c3-136">Create database-level firewall</span></span>

<span data-ttu-id="4a6c3-137">SQL Database에 대한 [데이터베이스 수준 방화벽 규칙](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="4a6c3-138">이 데이터베이스 수준 방화벽 규칙이이 자습서에서 만드는 toohello 보조 서버를 자동으로 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="4a6c3-139">이 자습서의 경우) (의 편의 위해 hello hello 컴퓨터에이 자습서에서 hello 단계를 수행 하 고 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="4a6c3-140">toodetermine hello IP 주소를 현재 컴퓨터에 대 한 hello 서버 수준 방화벽 규칙에 사용 되는 참조 [서버 수준 방화벽 만들](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="4a6c3-141">쿼리 열기 창의 hello 이전 쿼리에서 다음 쿼리, 사용자 환경에 대 한 hello 적절 한 IP 주소와 hello IP 주소를 대체 하는 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="4a6c3-142">활성 지역 복제 자동 장애 조치(failover) 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="4a6c3-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="4a6c3-143">Azure PowerShell을 사용 하 여 만들는 [활성 지리적 복제 자동 장애 조치 그룹](sql-database-geo-replication-overview.md) 기존 Azure SQL server 및 새 hello 간의 Azure 지역에서 Azure SQL server를 비우고 샘플 데이터베이스 toohello 장애 조치 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a6c3-144">이러한 cmdlet에는 Azure PowerShell 4.0이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="4a6c3-145">Hello 값을 사용 하 여 기존 서버 및 샘플 데이터베이스에 대 한 PowerShell 스크립트에 대 한 변수를 채운 장애 조치 그룹 이름에 대 한 전역 고유 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="4a6c3-146">장애 조치 지역에 빈 백업 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="4a6c3-147">Hello 두 서버 간에 장애 조치 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="4a6c3-148">데이터베이스 toohello 장애 조치 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="4a6c3-149">Java 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="4a6c3-149">Install Java software</span></span>

<span data-ttu-id="4a6c3-150">이 섹션의 단계 hello Java를 사용 하 여 개발에 익숙한 하 고 새 tooworking Azure SQL 데이터베이스는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="4a6c3-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="4a6c3-151">**Mac OS**</span></span>
<span data-ttu-id="4a6c3-152">터미널 열고 Java 프로젝트를 만드는 방법에 설치할 tooa 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="4a6c3-153">설치 **끓여** 및 **Maven** hello 다음 명령을 입력 하 여:</span><span class="sxs-lookup"><span data-stu-id="4a6c3-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="4a6c3-154">설치 및 Java와 Maven 환경 구성에 자세한 지침에 대 한 hello 이동 [SQL Server를 사용 하 여 응용 프로그램을 구축](https://www.microsoft.com/sql-server/developer-get-started/)을 선택 **Java**선택, **MacOS**, 한 다음에 따라 hello는 1.2 및 1.3 단계에서 Java 및 Maven을 구성 하기 위한 지침을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4a6c3-155">**Linux(Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="4a6c3-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="4a6c3-156">터미널 열고 Java 프로젝트를 만드는 방법에 설치할 tooa 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="4a6c3-157">설치 **Maven** hello 다음 명령을 입력 하 여:</span><span class="sxs-lookup"><span data-stu-id="4a6c3-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="4a6c3-158">설치 및 Java와 Maven 환경 구성에 자세한 지침에 대 한 hello 이동 [SQL Server를 사용 하 여 응용 프로그램을 구축](https://www.microsoft.com/sql-server/developer-get-started/)을 선택 **Java**선택, **Ubuntu**, 한 다음에 따라 hello는 1.2, 1.3 및 1.4 단계에서 Java 및 Maven을 구성 하기 위한 지침을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="4a6c3-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="4a6c3-159">**Windows**</span></span>
<span data-ttu-id="4a6c3-160">설치 [Maven](https://maven.apache.org/download.cgi) hello 공식 설치 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="4a6c3-161">Maven toohelp 종속성 관리, 빌드, 테스트 및 Java 프로젝트 실행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="4a6c3-162">설치 및 Java와 Maven 환경 구성에 자세한 지침에 대 한 hello 이동 [SQL Server를 사용 하 여 응용 프로그램을 구축](https://www.microsoft.com/sql-server/developer-get-started/)선택, **Java**Windows를 선택한 다음 수행 hello 자세한 지침 Java 및 Maven 1.2 및 1.3 단계에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="4a6c3-163">SqlDbSample 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4a6c3-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="4a6c3-164">(예: Bash) hello 명령 콘솔에서 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="4a6c3-165">**Y**를 입력하고 **Enter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="4a6c3-166">디렉터리를 새로 만든 프로젝트로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="4a6c3-167">선호 하는 편집기를 사용 하 여 프로젝트 폴더에 있는 hello pom.xml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="4a6c3-168">원하는 텍스트 편집기를 열고 SQL Server 종속성 tooyour Maven 프로젝트에 대 한 hello Microsoft JDBC 드라이버를 추가 하 고 복사 및 붙여넣기 hello pom.xml 파일에 줄을 다음 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="4a6c3-169">Hello 파일에 미리 채워져 hello 기존 값을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="4a6c3-170">hello JDBC 종속성 hello 큰 "종속성" 섹션 () 내에서 붙여 넣을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="4a6c3-171">Hello 버전에 대해 Java toocompile hello 프로젝트의 hello "종속성" 섹션 뒤 hello pom.xml 파일로 "속성" 섹션을 따라 hello를 추가 하 여 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="4a6c3-172">Hello "빌드" 섹션 hello pom.xml 파일로 후 hello "속성" 섹션 toosupport 매니페스트 파일 jar에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="4a6c3-173">저장 하 고 hello pom.xml 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="4a6c3-174">Hello App.java 파일 (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java)를 열고 내용을 따라 hello hello 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="4a6c3-175">Hello 장애 조치 그룹 이름을 장애 조치 그룹에 대 한 hello 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="4a6c3-176">Hello 데이터베이스 이름, 사용자 또는 암호에 대 한 hello 값 변경 되 면 해당 값도 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="4a6c3-177">저장 하 고 hello App.java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="4a6c3-178">컴파일 및 hello SqlDbSample 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="4a6c3-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="4a6c3-179">Hello 명령 콘솔에서 toofollowing 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="4a6c3-180">완료 되 면 hello 명령 toorun hello 실행 응용 프로그램 (약 1 시간 동안 수동으로 중지 하지 않는 한) 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="4a6c3-181">재해 복구 훈련 수행</span><span class="sxs-lookup"><span data-stu-id="4a6c3-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="4a6c3-182">장애 조치(failover) 그룹의 수동 장애 조치(failover)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="4a6c3-183">장애 조치 중 hello 응용 프로그램 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-183">Observe hello application results during failover.</span></span> <span data-ttu-id="4a6c3-184">일부 삽입 hello DNS 캐시를 새로 고치는 동안 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="4a6c3-185">재해 복구 서버가 수행하는 역할을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="4a6c3-186">장애 복구(failback)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="4a6c3-187">장애 복구 하는 동안 hello 응용 프로그램 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-187">Observe hello application results during failback.</span></span> <span data-ttu-id="4a6c3-188">일부 삽입 hello DNS 캐시를 새로 고치는 동안 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="4a6c3-189">재해 복구 서버가 수행하는 역할을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="4a6c3-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a6c3-190">Next steps</span></span> 

<span data-ttu-id="4a6c3-191">자세한 내용은 [활성 지역 복제 및 장애 조치(failover) 그룹](sql-database-geo-replication-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a6c3-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
