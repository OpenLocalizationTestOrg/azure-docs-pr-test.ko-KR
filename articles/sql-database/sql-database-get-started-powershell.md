---
title: "Azure PowerShell: SQL Database 만들기 | Microsoft Docs"
description: "Azure Portal에서 SQL Database 논리 서버, 서버 수준 방화벽 규칙 및 데이터베이스를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 44ed4a603977617c898315c4fc0b2d3dd3a8f16a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="3b425-104">PowerShell을 사용하여 단일 Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="3b425-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="3b425-105">명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 PowerShell이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="3b425-106">이 가이드에서는 PowerShell을 사용하여 [Azure SQL Database 논리 서버](sql-database-features.md)의 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)에서 Azure SQL Database를 배포하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="3b425-107">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="3b425-108">이 자습서에는 Azure PowerShell 모듈 버전 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-108">This tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="3b425-109">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="3b425-110">설치 또는 업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b425-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="3b425-111">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="3b425-111">Log in to Azure</span></span>

<span data-ttu-id="3b425-112">[Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) 명령을 사용하여 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-112">Log in to your Azure subscription using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="3b425-113">변수 만들기</span><span class="sxs-lookup"><span data-stu-id="3b425-113">Create variables</span></span>

<span data-ttu-id="3b425-114">이 빠른 시작의 스크립트에서 사용할 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-114">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3b425-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="3b425-115">Create a resource group</span></span>

<span data-ttu-id="3b425-116">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령을 사용하여 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="3b425-117">리소스 그룹은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="3b425-118">다음 예제는 `westeurope` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-118">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="3b425-119">논리 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="3b425-119">Create a logical server</span></span>

<span data-ttu-id="3b425-120">[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) 명령을 사용하여 [Azure SQL Database 논리 서버](sql-database-features.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-120">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="3b425-121">논리 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="3b425-122">다음 예제에서는 관리자 로그인 이름이 `ServerAdmin`이고 암호가 `ChangeYourAdminPassword1`인 리소스 그룹에 임의로 이름이 지정된 서버를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-122">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="3b425-123">이러한 미리 정의된 값은 필요에 따라 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="3b425-124">서버 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="3b425-124">Configure a server firewall rule</span></span>

<span data-ttu-id="3b425-125">[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) 명령을 사용하여 [Azure SQL Database 서버 수준 방화벽 규칙](sql-database-firewall-configure.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="3b425-126">서버 수준 방화벽 규칙을 통해 외부 응용 프로그램(예: SQL Server Management Studio 또는 SQLCMD 유틸리티)이 SQL Database 서비스 방화벽을 통해 SQL Database에 연결되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="3b425-127">다음 예제에서 방화벽은 다른 Azure 리소스에 대해서만 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-127">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="3b425-128">외부 연결을 사용하려면 IP 주소를 사용자 환경에 적절한 주소로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-128">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="3b425-129">모든 IP 주소를 열려면 시작 IP 주소로 0.0.0.0을, 끝나는 IP 주소로 255.255.255.255를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-129">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="3b425-130">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="3b425-131">회사 네트워크 내에서 연결을 시도하는 경우 포트 1433을 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-131">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3b425-132">이 경우 IT 부서에서 포트 1433을 열지 않으면 Azure SQL Database 서버에 연결할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="3b425-132">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="3b425-133">샘플 데이터를 사용하여 서버에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3b425-133">Create a database in the server with sample data</span></span>

<span data-ttu-id="3b425-134">[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) 명령을 사용하여 서버에 [S0 성능 수준](sql-database-service-tiers.md)인 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="3b425-135">다음 예제에서는 `mySampleDatabase`라는 데이터베이스를 만들고 AdventureWorksLT 샘플 데이터를 이 데이터베이스에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-135">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="3b425-136">이러한 미리 정의된 값을 원하는 대로 대체합니다(이 컬렉션 빌드의 다른 빠른 시작은 이 빠른 시작의 값에 기반함).</span><span class="sxs-lookup"><span data-stu-id="3b425-136">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="3b425-137">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="3b425-137">Clean up resources</span></span>

<span data-ttu-id="3b425-138">이 컬렉션의 다른 빠른 시작은 이 빠른 시작을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="3b425-139">다음 빠른 시작을 사용하여 계속하려는 경우 이 빠른 시작에서 만든 리소스를 정리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-139">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="3b425-140">계속하지 않으려는 경우 다음 단계에 따라 Azure Portal에서 이 빠른 시작에서 만든 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-140">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="3b425-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b425-141">Next steps</span></span>

<span data-ttu-id="3b425-142">이제 데이터베이스가 생겼으니 자주 사용하는 도구를 사용하여 데이터베이스에 연결하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b425-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="3b425-143">아래에서 도구를 선택하여 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3b425-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="3b425-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3b425-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="3b425-145">Contact.java</span><span class="sxs-lookup"><span data-stu-id="3b425-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="3b425-146">.NET</span><span class="sxs-lookup"><span data-stu-id="3b425-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="3b425-147">PHP</span><span class="sxs-lookup"><span data-stu-id="3b425-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="3b425-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="3b425-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="3b425-149">Java</span><span class="sxs-lookup"><span data-stu-id="3b425-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="3b425-150">Python</span><span class="sxs-lookup"><span data-stu-id="3b425-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="3b425-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="3b425-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

