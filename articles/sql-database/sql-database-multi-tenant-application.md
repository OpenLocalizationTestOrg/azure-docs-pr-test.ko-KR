---
title: "aaaImplement 다중 테 넌 트 SaaS 응용 프로그램을 Azure SQL 데이터베이스 | Microsoft Docs"
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
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="15c72-103">Azure SQL Database를 사용하여 다중 테넌트 SaaS 응용 프로그램 구현</span><span class="sxs-lookup"><span data-stu-id="15c72-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="15c72-104">다중 테 넌 트 응용 프로그램은 클라우드 환경에서 호스팅되는 응용 프로그램 및 서비스 toohundreds 또는 수천 개의 공유 하지 않거나 다른 사용자의 데이터를 볼 수 있는 테 넌 트가 집합이 동일한 hello를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="15c72-105">예로 서비스 tootenants 클라우드 호스팅 환경에서 제공 하는 SaaS 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="15c72-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="15c72-106">이 모델 각 테 넌 트에 대 한 hello 데이터를 격리 하 고 비용에 대 한 리소스의 hello 배포를 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="15c72-107">이 자습서에서는 설명 방법을 toocreate Azure SQL 데이터베이스를 사용 하 여 다중 테 넌 트 SaaS 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="15c72-108">이 자습서에서 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="15c72-109">데이터베이스 환경 toosupport hello 테 넌 당 데이터베이스 패턴을 사용 하 여 다중 테 넌 트 SaaS 응용 프로그램, 설정</span><span class="sxs-lookup"><span data-stu-id="15c72-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="15c72-110">테넌트 카탈로그 만들기</span><span class="sxs-lookup"><span data-stu-id="15c72-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="15c72-111">테 넌 트 데이터베이스 프로 비전 하 고 hello 테 넌 트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="15c72-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="15c72-112">샘플 Java 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="15c72-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="15c72-113">간단한 Java 콘솔 응용 프로그램을 통한 테넌트 데이터베이스 액세스</span><span class="sxs-lookup"><span data-stu-id="15c72-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="15c72-114">테넌트 삭제</span><span class="sxs-lookup"><span data-stu-id="15c72-114">Delete a tenant</span></span>

<span data-ttu-id="15c72-115">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15c72-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="15c72-116">Prerequisites</span></span>

<span data-ttu-id="15c72-117">toocomplete이 자습서, 확인을 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="15c72-118">설치 된 hello 최신 버전의 PowerShell 및 hello [최신 Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="15c72-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="15c72-119">최신 버전의 설치 된 hello [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="15c72-120">SQL Server Management Studio를 설치 hello SQLPackage 사용 하는 데이터베이스 개발 태스크의 범위 tooautomate 일 수 있는 명령줄 유틸리티의 최신 버전도 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="15c72-121">설치 된 hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 및 hello [최신 키트 JDK (JAVA Development)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="15c72-122">[Apache Maven](https://maven.apache.org/download.cgi)</span><span class="sxs-lookup"><span data-stu-id="15c72-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="15c72-123">Maven 사용될지 toohelp 종속성 관리, 빌드, 테스트 및 hello 샘플 Java 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="15c72-124">데이터 환경 설정</span><span class="sxs-lookup"><span data-stu-id="15c72-124">Set up data environment</span></span>

<span data-ttu-id="15c72-125">테넌트당 데이터베이스를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="15c72-126">hello 테 넌 당 데이터베이스 모델 hello 가장 높은 수준의 DevOps 비용이 들지 않는 테 넌 트 간에 격리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="15c72-127">클라우드 리소스의 toooptimize hello 비용, 됩니다도 프로 비전 됩니까 hello 테 넌 트 데이터베이스를 탄력적 풀 데이터베이스 그룹에 대 한 toooptimize hello 가격 성능 수 있는로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="15c72-128">모델을 프로 비전 하는 다른 데이터베이스에 대 한 toolearn [여기에서 볼](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models)합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="15c72-129">SQL server 및 모든 테 넌 트 데이터베이스를 호스팅하는 탄력적인 풀에 이러한 단계 toocreate를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="15c72-130">Hello 자습서의 나머지 부분 hello에에서 toostore 값 사용 되는 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="15c72-131">있는지 toomodify hello IP 주소 변수 tooinclude IP 주소 확인</span><span class="sxs-lookup"><span data-stu-id="15c72-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="15c72-132">로그인 tooAzure 및 SQL server 및 탄력적인 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="15c72-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="15c72-133">테넌트 카탈로그 만들기</span><span class="sxs-lookup"><span data-stu-id="15c72-133">Create tenant catalog</span></span> 

<span data-ttu-id="15c72-134">다중 테 넌 트 SaaS 응용 프로그램에서는 테 넌 트에 대 한 정보가 저장 된 중요 한 tooknow는.</span><span class="sxs-lookup"><span data-stu-id="15c72-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="15c72-135">이 정보는 일반적으로 카탈로그 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="15c72-136">hello 카탈로그 데이터베이스에 사용 되는 테 넌 트 및 해당 테 넌 트의 데이터가 저장 되는 데이터베이스 간의 매핑을 toohold입니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="15c72-137">단일 테 넌 트 데이터베이스를 사용 또는 여부는 다중 테 넌 트 hello 기본 패턴 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="15c72-138">이러한 단계 toocreate hello 샘플 SaaS 응용 프로그램에 대 한 카탈로그 데이터베이스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="15c72-139">'tenant1'에 대한 데이터베이스 프로비전 및 테넌트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="15c72-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="15c72-140">새 테 넌 트 'tenant1'에 대 한 Powershell tooprovision 데이터베이스를 사용 하 하며이 테 넌이 트 hello 카탈로그에서 등록 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register 'tenant1' in hello tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="15c72-141">'tenant2'에 대한 데이터베이스 프로비전 및 테넌트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="15c72-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="15c72-142">새 테 넌 트 'tenant2'에 대 한 Powershell tooprovision 데이터베이스를 사용 하 하며이 테 넌이 트 hello 카탈로그에서 등록 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register tenant 'tenant2' in hello tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="15c72-143">샘플 Java 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="15c72-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="15c72-144">maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-144">Create a maven project.</span></span> <span data-ttu-id="15c72-145">명령 프롬프트 창의 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="15c72-146">이 종속성, 언어 수준 및 추가 빌드 옵션 toosupport jar toohello pom.xml 파일에 매니페스트 파일:</span><span class="sxs-lookup"><span data-stu-id="15c72-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="15c72-147">Hello 다음 hello App.java 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-147">Add hello following into hello App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
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
   
   // List all tenants that currently exist in hello system
   
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
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
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

4. <span data-ttu-id="15c72-148">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-148">Save hello file.</span></span>

5. <span data-ttu-id="15c72-149">Toocommand 콘솔 이동 및 실행</span><span class="sxs-lookup"><span data-stu-id="15c72-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="15c72-150">완료 되 면 hello 다음 toorun hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="15c72-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="15c72-151">hello 출력 성공적으로 실행 되는 경우 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="15c72-152">첫 번째 테넌트 삭제</span><span class="sxs-lookup"><span data-stu-id="15c72-152">Delete first tenant</span></span> 
<span data-ttu-id="15c72-153">Hello 첫 번째 테 넌 트에 대 한 PowerShell는 toodelete hello 테 넌 트 데이터베이스 및 카탈로그 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="15c72-154">연결을 시도 너무 Java 응용 프로그램 hello 'tenant1'를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="15c72-155">오류 메시지가 해당 hello 테 넌 트 존재 하지 않는 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15c72-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15c72-156">Next steps</span></span> 

<span data-ttu-id="15c72-157">이 자습서에서는 다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="15c72-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="15c72-158">데이터베이스 환경 toosupport hello 테 넌 당 데이터베이스 패턴을 사용 하 여 다중 테 넌 트 SaaS 응용 프로그램, 설정</span><span class="sxs-lookup"><span data-stu-id="15c72-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="15c72-159">테넌트 카탈로그 만들기</span><span class="sxs-lookup"><span data-stu-id="15c72-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="15c72-160">테 넌 트 데이터베이스 프로 비전 하 고 hello 테 넌 트 카탈로그에 등록</span><span class="sxs-lookup"><span data-stu-id="15c72-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="15c72-161">샘플 Java 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="15c72-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="15c72-162">간단한 Java 콘솔 응용 프로그램을 통한 테넌트 데이터베이스 액세스</span><span class="sxs-lookup"><span data-stu-id="15c72-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="15c72-163">테넌트 삭제</span><span class="sxs-lookup"><span data-stu-id="15c72-163">Delete a tenant</span></span>

* <span data-ttu-id="15c72-164">일반적인 작업에 대한 PowerShell 샘플은 [SQL Database PowerShell 샘플](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15c72-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="15c72-165">다중 테넌트 SaaS 응용 프로그램에 대한 디자인 패턴은 [디자인 패턴](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15c72-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="15c72-166">일반적인 Azure 작업에 대한 Java 샘플은 [Java 개발자 센터](https://azure.microsoft.com/develop/java/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15c72-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



