---
title: "Azure SQL Database를 사용하여 다중 테넌트 SaaS 응용 프로그램 구현 | Microsoft Docs"
description: "Azure SQL Database를 사용하여 다중 테넌트 SaaS 응용 프로그램을 구현합니다."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="8ec0b-103">Azure SQL Database를 사용하여 다중 테넌트 SaaS 응용 프로그램 구현</span><span class="sxs-lookup"><span data-stu-id="8ec0b-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="8ec0b-104">다중 테넌트 응용 프로그램은 클라우드 환경에서 호스팅되는 응용 프로그램이며, 서로의 데이터를 공유하거나 보지 않는 수백 또는 수천 명의 테넌트에게 동일한 서비스 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="8ec0b-105">예를 들어 클라우드 호스팅 환경에서 테넌트에 서비스를 제공하는 SaaS 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="8ec0b-106">이 모델은 각 테넌트에 대한 데이터를 격리하고 비용에 맞춰 리소스 배포를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="8ec0b-107">이 자습서에서는 Azure SQL Database를 사용하여 다중 테넌트 SaaS 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="8ec0b-108">이 자습서에서 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8ec0b-109">테넌트당 데이터베이스 패턴을 사용하여 다중 테넌트 SaaS 응용 프로그램을 지원하는 데이터베이스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="8ec0b-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="8ec0b-110">테넌트 카탈로그 만들기</span><span class="sxs-lookup"><span data-stu-id="8ec0b-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="8ec0b-111">테넌트 데이터베이스 프로비전 및 테넌트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="8ec0b-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="8ec0b-112">샘플 Java 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="8ec0b-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="8ec0b-113">간단한 Java 콘솔 응용 프로그램을 통한 테넌트 데이터베이스 액세스</span><span class="sxs-lookup"><span data-stu-id="8ec0b-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="8ec0b-114">테넌트 삭제</span><span class="sxs-lookup"><span data-stu-id="8ec0b-114">Delete a tenant</span></span>

<span data-ttu-id="8ec0b-115">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ec0b-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8ec0b-116">Prerequisites</span></span>

<span data-ttu-id="8ec0b-117">이 자습서를 완료하려면 다음이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="8ec0b-118">최신 버전의 PowerShell 및 [최신 Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8ec0b-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="8ec0b-119">최신 버전의 [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)</span><span class="sxs-lookup"><span data-stu-id="8ec0b-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="8ec0b-120">SQL Server Management Studio를 설치하면 다양한 데이터베이스 개발 작업을 자동화하는 데 사용할 수 있는 명령줄 유틸리티인 SQLPackage의 최신 버전도 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="8ec0b-121">컴퓨터에 설치된 [JRE(Java Runtime Environment) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 및 [최신 JDK(JAVA Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="8ec0b-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="8ec0b-122">[Apache Maven](https://maven.apache.org/download.cgi)</span><span class="sxs-lookup"><span data-stu-id="8ec0b-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="8ec0b-123">Maven은 종속성을 관리하고 샘플 Java 프로젝트를 빌드, 테스트 및 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="8ec0b-124">데이터 환경 설정</span><span class="sxs-lookup"><span data-stu-id="8ec0b-124">Set up data environment</span></span>

<span data-ttu-id="8ec0b-125">테넌트당 데이터베이스를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="8ec0b-126">테넌트당 데이터베이스 모델은 DevOps 비용이 거의 들지 않으면서 테넌트 간에 가장 높은 수준의 격리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="8ec0b-127">또한 클라우드 리소스 비용을 최적화하려면 데이터베이스 그룹에 대한 가격 대비 성능을 최적화할 수 있는 탄력적 풀에 테넌트 데이터베이스를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="8ec0b-128">다른 데이터베이스 프로비전 모델에 대해 알아보려면 [여기를 참조하세요](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="8ec0b-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="8ec0b-129">다음 단계에 따라 모든 테넌트 데이터베이스를 호스팅할 SQL 서버와 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="8ec0b-130">자습서의 나머지 부분에서 사용할 값을 저장하는 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="8ec0b-131">IP 주소를 포함하도록 IP 주소 변수를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="8ec0b-132">Azure에 로그인하고 SQL 서버와 탄력적 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="8ec0b-133">테넌트 카탈로그 만들기</span><span class="sxs-lookup"><span data-stu-id="8ec0b-133">Create tenant catalog</span></span> 

<span data-ttu-id="8ec0b-134">다중 테넌트 SaaS 응용 프로그램에서 테넌트 정보가 저장되어 있는 위치를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="8ec0b-135">이 정보는 일반적으로 카탈로그 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="8ec0b-136">카탈로그 데이터베이스는 테넌트와 해당 테넌트의 데이터가 저장된 데이터베이스 간의 매핑을 유지하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="8ec0b-137">기본 패턴은 다중 테넌트 또는 단일 테넌트 데이터베이스가 사용되는지 여부에 관계 없이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="8ec0b-138">다음 단계에 따라 샘플 SaaS 응용 프로그램에 대한 카탈로그 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="8ec0b-139">'tenant1'에 대한 데이터베이스 프로비전 및 테넌트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="8ec0b-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="8ec0b-140">Powershell을 사용하여 새로운 'tenant1' 테넌트에 대한 데이터베이스를 프로비전하고 이 테넌트를 카탈로그에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="8ec0b-141">'tenant2'에 대한 데이터베이스 프로비전 및 테넌트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="8ec0b-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="8ec0b-142">Powershell을 사용하여 새로운 'tenant2' 테넌트에 대한 데이터베이스를 프로비전하고 이 테넌트를 카탈로그에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="8ec0b-143">샘플 Java 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="8ec0b-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="8ec0b-144">maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-144">Create a maven project.</span></span> <span data-ttu-id="8ec0b-145">명령 프롬프트 창에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="8ec0b-146">이러한 종속성, 언어 수준 및 jar의 매니페스트 파일을 지원하는 빌드 옵션을 pom.xml 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. <span data-ttu-id="8ec0b-147">App.java 파일에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-147">Add the following into the App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in the system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="8ec0b-148">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-148">Save the file.</span></span>

5. <span data-ttu-id="8ec0b-149">명령 콘솔로 이동하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="8ec0b-150">완료되면 다음을 실행하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="8ec0b-151">성공적으로 실행되면 출력은 다음과 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="8ec0b-152">첫 번째 테넌트 삭제</span><span class="sxs-lookup"><span data-stu-id="8ec0b-152">Delete first tenant</span></span> 
<span data-ttu-id="8ec0b-153">PowerShell을 사용하여 첫 번째 테넌트에 대한 테넌트 데이터베이스 및 카탈로그 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="8ec0b-154">Java 응용 프로그램을 사용하여 'tenant1'에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="8ec0b-155">테넌트가 존재하지 않는다는 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ec0b-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ec0b-156">Next steps</span></span> 

<span data-ttu-id="8ec0b-157">이 자습서에서는 다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8ec0b-158">테넌트당 데이터베이스 패턴을 사용하여 다중 테넌트 SaaS 응용 프로그램을 지원하는 데이터베이스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="8ec0b-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="8ec0b-159">테넌트 카탈로그 만들기</span><span class="sxs-lookup"><span data-stu-id="8ec0b-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="8ec0b-160">테넌트 데이터베이스 프로비전 및 테넌트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="8ec0b-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="8ec0b-161">샘플 Java 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="8ec0b-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="8ec0b-162">간단한 Java 콘솔 응용 프로그램을 통한 테넌트 데이터베이스 액세스</span><span class="sxs-lookup"><span data-stu-id="8ec0b-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="8ec0b-163">테넌트 삭제</span><span class="sxs-lookup"><span data-stu-id="8ec0b-163">Delete a tenant</span></span>

* <span data-ttu-id="8ec0b-164">일반적인 작업에 대한 PowerShell 샘플은 [SQL Database PowerShell 샘플](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="8ec0b-165">다중 테넌트 SaaS 응용 프로그램에 대한 디자인 패턴은 [디자인 패턴](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="8ec0b-166">일반적인 Azure 작업에 대한 Java 샘플은 [Java 개발자 센터](https://azure.microsoft.com/develop/java/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ec0b-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



