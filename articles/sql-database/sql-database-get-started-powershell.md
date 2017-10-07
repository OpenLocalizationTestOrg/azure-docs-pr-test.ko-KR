---
title: "Azure PowerShell: SQL Database 만들기 | Microsoft Docs"
description: "Toocreate SQL 데이터베이스 논리 서버, 서버 수준 방화벽 규칙의 데이터베이스 및 Azure 포털을 hello 방법에 대해 알아봅니다."
keywords: "SQL 데이터베이스 자습서, SQL 데이터베이스 만들기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="be12d-104">PowerShell을 사용하여 단일 Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="be12d-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="be12d-105">PowerShell 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="be12d-106">이 가이드 toodeploy PowerShell을 사용 하 여 정보에 Azure SQL 데이터베이스는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 에 [Azure SQL 데이터베이스 논리 서버](sql-database-features.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="be12d-107">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="be12d-108">이 자습서는 hello Azure PowerShell 모듈 버전 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="be12d-109">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="be12d-110">Tooinstall 또는 업그레이드를 보려면 참고 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="be12d-111">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="be12d-111">Log in tooAzure</span></span>

<span data-ttu-id="be12d-112">Hello를 사용 하 여 Azure 구독 tooyour 로그인 [추가 AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="be12d-113">변수 만들기</span><span class="sxs-lookup"><span data-stu-id="be12d-113">Create variables</span></span>

<span data-ttu-id="be12d-114">이 빠른 시작의 hello 스크립트에서 사용할 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="be12d-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="be12d-115">Create a resource group</span></span>

<span data-ttu-id="be12d-116">만들기는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello를 사용 하 여 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="be12d-117">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="be12d-118">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westeurope` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="be12d-119">논리 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="be12d-119">Create a logical server</span></span>

<span data-ttu-id="be12d-120">만들기는 [Azure SQL 데이터베이스 논리 서버](sql-database-features.md) hello를 사용 하 여 [새로 AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="be12d-121">논리 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="be12d-122">hello 다음 예제에서는 만듭니다 임의로 지정 된 서버 리소스 그룹에 라는 관리자 로그인과 `ServerAdmin` 이 고 암호가 `ChangeYourAdminPassword1`합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="be12d-123">이러한 미리 정의된 값은 필요에 따라 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="be12d-124">서버 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="be12d-124">Configure a server firewall rule</span></span>

<span data-ttu-id="be12d-125">만들기는 [Azure SQL 데이터베이스 서버 수준 방화벽 규칙](sql-database-firewall-configure.md) hello를 사용 하 여 [새로 AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="be12d-126">서버 수준 방화벽 규칙에는 SQL Server Management Studio 또는 hello SQLCMD 유틸리티 tooconnect tooa SQL 데이터베이스 같은 hello SQL 데이터베이스 서비스 방화벽을 통해 외부 응용을 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="be12d-127">다음 예제는 hello,에서는 hello 방화벽은 다른 Azure 리소스에 대 한 열만.</span><span class="sxs-lookup"><span data-stu-id="be12d-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="be12d-128">tooenable 외부 연결을 변경 hello IP 주소 tooan 사용자 환경에 대 한 적절 한 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="be12d-129">tooopen 모든 IP 주소를 IP 주소와 255.255.255.255 끝 주소 hello로 시작 하는 hello로 0.0.0.0를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="be12d-130">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="be12d-131">회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="be12d-132">이 경우 됩니다 수 tooconnect tooyour Azure SQL 데이터베이스 서버 않으면 IT 부서는 포트 1433을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="be12d-133">샘플 데이터로 hello 서버에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="be12d-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="be12d-134">사용 하 여 데이터베이스를 만들기는 [S0 성능 수준이](sql-database-service-tiers.md) hello를 사용 하 여 hello 서버에서 [새로 AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="be12d-135">hello 다음 예에서는 라는 데이터베이스를 만드는 `mySampleDatabase` 로드 AdventureWorksLT 샘플 데이터를이 데이터베이스에 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="be12d-136">이러한 미리 정의 된 대체 값 (hello 값이 빠른 시작에서에이 컬렉션 빌드에서 다른 빠른 시작)이 원하는 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="be12d-137">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="be12d-137">Clean up resources</span></span>

<span data-ttu-id="be12d-138">이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="be12d-139">후속 빠른 시작으로 toowork toocontinue 하려는 경우이 빠른에서 만든 hello 리소스를 정리 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="be12d-140">Toocontinue 않으려는 경우 모든 리소스를 만들 단계 toodelete hello Azure 포털에서에서이 빠른 시작에서 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="be12d-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be12d-141">Next steps</span></span>

<span data-ttu-id="be12d-142">이제 데이터베이스가 생겼으니 자주 사용하는 도구를 사용하여 데이터베이스에 연결하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be12d-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="be12d-143">아래에서 도구를 선택하여 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="be12d-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="be12d-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="be12d-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="be12d-145">Contact.java</span><span class="sxs-lookup"><span data-stu-id="be12d-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="be12d-146">.NET</span><span class="sxs-lookup"><span data-stu-id="be12d-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="be12d-147">PHP</span><span class="sxs-lookup"><span data-stu-id="be12d-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="be12d-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="be12d-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="be12d-149">Java</span><span class="sxs-lookup"><span data-stu-id="be12d-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="be12d-150">Python</span><span class="sxs-lookup"><span data-stu-id="be12d-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="be12d-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="be12d-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

