---
title: "C#: Azure SQL Database 시작 | Microsoft Docs"
description: "SQL 및 C# 앱 개발을 위해 SQL 데이터베이스를 시도하고 .NET용 SQL 데이터베이스 라이브러리를 사용하여 C#으로 Azure SQL 데이터베이스를 만듭니다."
keywords: "sql 시도, sql c#"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: c8a2703da1ee3687f8d134e768dd8d31dc4f316b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-c-to-create-a-sql-database-with-the-sql-database-library-for-net"></a><span data-ttu-id="60cfe-104">C#을 사용하여 .NET용 SQL Database 라이브러리로 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="60cfe-104">Use C# to create a SQL database with the SQL Database Library for .NET</span></span>

<span data-ttu-id="60cfe-105">C#을 사용하여 [.NET용 Microsoft Azure SQL 관리 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)로 Azure SQL Database를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-105">Learn how to use C# to create an Azure SQL database with the [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="60cfe-106">이 문서에서는 SQL 및 C#으로 단일 데이터베이스를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-106">This article describes how to create a single database with SQL and C#.</span></span> <span data-ttu-id="60cfe-107">탄력적 풀을 만들려면 [탄력적 풀 만들기](sql-database-elastic-pool-manage-csharp.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60cfe-107">To create elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="60cfe-108">.NET용 Azure SQL Database 관리 라이브러리는 [Resource Manager 기반 SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)를 래핑하는 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-108">The Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps the [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="60cfe-109">SQL Database의 여러 새로운 기능은 [Azure Resource Manager 배포 모델](../azure-resource-manager/resource-group-overview.md)을 사용할 때 지원되므로 최신 **.NET용 SQL Database 관리 라이브러리([문서](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-109">Many new features of SQL Database are only supported when you are using the [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use the latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="60cfe-110">이전 [클래식 배포 모델 기반 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql)가 이전 버전과만 호환되므로 최신 Resource Manager 기반 라이브러리를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-110">The older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use the newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="60cfe-111">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-111">To complete the steps in this article, you need the following:</span></span>

* <span data-ttu-id="60cfe-112">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="60cfe-112">An Azure subscription.</span></span> <span data-ttu-id="60cfe-113">Azure 구독이 필요할 경우 이 페이지 위쪽에서 **무료 계정** 을 클릭하고 되돌아와 이 문서를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-113">If you need an Azure subscription simply click **FREE ACCOUNT** at the top of this page, and then come back to finish this article.</span></span>
* <span data-ttu-id="60cfe-114">있습니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-114">Visual Studio.</span></span> <span data-ttu-id="60cfe-115">Visual Studio의 무료 버전은 [Visual Studio 다운로드](https://www.visualstudio.com/downloads/download-visual-studio-vs) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60cfe-115">For a free copy of Visual Studio, see the [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="60cfe-116">이 문서에서는 비어 있는 새 SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="60cfe-117">다음 샘플에서 *CreateOrUpdateDatabase(...)* 메서드를 수정하여 데이터베이스를 복사하고 데이터베이스의 크기를 조정하며 풀에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-117">Modify the *CreateOrUpdateDatabase(...)* method in the following sample to copy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-the-required-libraries"></a><span data-ttu-id="60cfe-118">콘솔 앱 만들기 및 필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="60cfe-118">Create a console app and install the required libraries</span></span>
1. <span data-ttu-id="60cfe-119">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="60cfe-120">**파일** > **새로 만들기** > **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="60cfe-121">C# **콘솔 응용 프로그램** 을 만들고 이름을 *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="60cfe-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="60cfe-122">C#으로 SQL Database를 만들려면 [패키지 관리자 콘솔](http://docs.nuget.org/Consume/Package-Manager-Console)을 사용하여 필요한 관리 라이브러리를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-122">To create a SQL database with C#, load the required management libraries (using the [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="60cfe-123">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="60cfe-124">`Install-Package Microsoft.Azure.Management.Sql -Pre`을 입력하여 최신 [Microsoft Azure SQL 관리 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` to install the latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="60cfe-125">`Install-Package Microsoft.Azure.Management.ResourceManager -Pre` 을 입력하여 [Microsoft Azure Resource Manager 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` to install the [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="60cfe-126">`Install-Package Microsoft.Azure.Common.Authentication -Pre` 을 입력하여 [Microsoft Azure 공용 인증 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` to install the [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="60cfe-127">이 문서의 예제는 각 API요청의 동기 양식을 사용하며 REST가 완료되어 기본 서비스를 호출할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-127">The examples in this article use a synchronous form of each API request and block until completion of the REST call on the underlying service.</span></span> <span data-ttu-id="60cfe-128">비동기 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="60cfe-129">SQL Database 서버, 방화벽 규칙 및 SQL Database 만들기 - C# 예제</span><span class="sxs-lookup"><span data-stu-id="60cfe-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="60cfe-130">다음 샘플은 리소스 그룹, 서버, 방화벽 규칙 및 SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-130">The following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="60cfe-131">`_subscriptionId, _tenantId, _applicationId, and _applicationSecret` 변수를 가져오려면 [리소스에 액세스하는 서비스 주체 만들기](#create-a-service-principal-to-access-resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60cfe-131">See, [Create a service principal to access resources](#create-a-service-principal-to-access-resources) to get the `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="60cfe-132">**Program.cs** 콘텐츠를 다음으로 바꾸고 `{variables}`를 앱 값(`{}`을 포함하지 않음)으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-132">Replace the contents of **Program.cs** with the following, and update the `{variables}` with your app values (do not include the `{}`).</span></span>

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for the Azure resources your app needs to work with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key to continue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve the server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-to-access-resources"></a><span data-ttu-id="60cfe-133">리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="60cfe-133">Create a service principal to access resources</span></span>
<span data-ttu-id="60cfe-134">다음 PowerShell 스크립트는 AD(Active Directory) 응용 프로그램 및 C# 앱을 인증해야 하는 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-134">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="60cfe-135">스크립트는 이전 C# 샘플에 필요한 값을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-135">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="60cfe-136">자세한 내용은 [Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60cfe-136">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="60cfe-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60cfe-137">Next steps</span></span>
<span data-ttu-id="60cfe-138">이제 C#으로 SQL 데이터베이스를 시도하고 데이터베이스를 설정했으므로 다음 문서에 대한 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-138">Now that you've tried SQL Database and set up a database with C#, you're ready for the following articles:</span></span>

* [<span data-ttu-id="60cfe-139">SQL Server Management Studio를 사용하여 SQL 데이터베이스에 연결하고 샘플 T-SQL 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60cfe-139">Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="60cfe-140">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="60cfe-140">Additional Resources</span></span>
* [<span data-ttu-id="60cfe-141">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="60cfe-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="60cfe-142">데이터베이스 클래스</span><span class="sxs-lookup"><span data-stu-id="60cfe-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
