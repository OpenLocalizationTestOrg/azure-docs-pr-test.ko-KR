---
title: "C#: Azure SQL Database 시작 | Microsoft Docs"
description: "SQL 및 C# 앱 개발을 위한 SQL 데이터베이스로 시도 하 고 C# for.net hello SQL 데이터베이스 라이브러리를 사용 하 여 Azure SQL 데이터베이스를 만듭니다."
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
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>C# toocreate SQL 데이터베이스를 사용 하 여.NET에 대 한 SQL 데이터베이스 라이브러리 hello로

Hello로 toouse C# toocreate Azure SQL 데이터베이스 하는 방법에 대해 알아봅니다 [.NET 용 Microsoft Azure SQL 관리 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)합니다. 이 문서에서는 toocreate 단일 데이터베이스 방법 SQL 및 C#으로 설명 합니다. 탄력적 풀 toocreate, 참조 [탄력적 풀을 만들](sql-database-elastic-pool-manage-csharp.md)합니다.

.NET 용 Azure SQL 데이터베이스 관리 라이브러리 hello 제공는 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md)-hello를 래핑하는 API 기반 [SQL 데이터베이스 REST API 리소스 관리자 기반](https://docs.microsoft.com/rest/api/sql/)합니다.

> [!NOTE]
> SQL 데이터베이스의 여러 가지 새로운 기능이 hello를 사용 하는 경우에 지원 됩니다 [Azure 리소스 관리자 배포 모델](../azure-resource-manager/resource-group-overview.md)이므로 항상 사용 해야 hello 최신 **.NET 용 Azure SQL 데이터베이스 관리 라이브러리 ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**합니다. 이전 hello [클래식 배포 모델 기반 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) 하므로 hello 최신 리소스 관리자 기반 라이브러리를 사용 하는 것이 좋습니다 이전 버전과 호환성 으로만 지원 됩니다.
> 
> 

이 문서의 toocomplete hello 단계 hello 다음이 필요합니다.

* Azure 구독. Azure 구독을 단순히 필요 하면 클릭 **무료 계정을** 이 hello 위쪽에 페이지를 선택한 후에 다시 시도 toofinish이이 문서입니다.
* 있습니다. Visual Studio의 무료 복사본을 hello 참조 [Visual Studio 다운로드](https://www.visualstudio.com/downloads/download-visual-studio-vs) 페이지.

> [!NOTE]
> 이 문서에서는 비어 있는 새 SQL Database를 만듭니다. Hello 수정 *CreateOrUpdateDatabase(...)*  메서드 예제 toocopy 데이터베이스 다음 hello, 데이터베이스의 크기를 조정, 등 풀에 데이터베이스를 만듭니다.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>콘솔 응용 프로그램을 만들고 필요한 hello 라이브러리 설치
1. Visual Studio를 시작합니다.
2. **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.
3. C# **콘솔 응용 프로그램** 을 만들고 이름을 *SqlDbConsoleApp*

C#, 부하 hello와 SQL 데이터베이스 toocreate 필요한 관리 라이브러리 (hello를 사용 하 여 [패키지 관리자 콘솔](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. **도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 클릭합니다.
2. 형식 `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello 최신 [Microsoft Azure SQL 관리 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)합니다.
3. 형식 `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure 리소스 관리자 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)합니다.
4. 형식 `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure 공용 인증 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication)합니다. 

> [!NOTE]
> hello이 문서의 예제에서는 동기 양식을 사용 각 API 요청 및 블록의 기본 서비스가 hello에 hello REST 호출 완료 될 때까지 합니다. 비동기 메서드를 사용할 수 있습니다.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>SQL Database 서버, 방화벽 규칙 및 SQL Database 만들기 - C# 예제
다음 예제는 hello 리소스 그룹, 서버, 방화벽 규칙 및 SQL 데이터베이스를 만듭니다. 참조, [서비스 보안 주체 tooaccess 리소스 만들기](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` 변수입니다.

Hello 내용 바꾸기 **Program.cs** hello 다음 업데이트 hello와 `{variables}` 응용 프로그램 값을 가진 (hello를 넣지 마십시오 `{}`).

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

        // Create management clients for hello Azure resources your app needs toowork with.
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


            Console.WriteLine("Press any key toocontinue...");
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
            // Retrieve hello server that will host this database
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





## <a name="create-a-service-principal-tooaccess-resources"></a>서비스 보안 주체 tooaccess 리소스 만들기
hello 다음 PowerShell 스크립트를 만듭니다 hello Active Directory (AD) 응용 프로그램 및 서비스 hello 필요한 tooauthenticate C# 앱 주입니다. hello 스크립트에서는 필요한 앞에 C# hello에 대 한 예제 값을 출력 합니다. 자세한 내용은 참조 [Azure PowerShell을 사용 하 여 서비스 사용자 toocreate tooaccess 리소스](../azure-resource-manager/resource-group-authenticate-service-principal.md)합니다.

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>다음 단계
SQL 데이터베이스를 시도 하 고 C#을 사용 하 여 데이터베이스를 설정 했으므로, 다음 문서는 hello에 대 한 수행할 수 있습니다.

* [SQL Server Management Studio로 tooSQL 데이터베이스를 연결 하 고 샘플 T-SQL 쿼리를 수행 합니다.](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>추가 리소스
* [SQL 데이터베이스](https://azure.microsoft.com/documentation/services/sql-database/)
* [데이터베이스 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
