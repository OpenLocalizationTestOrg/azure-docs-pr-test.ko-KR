---
title: "응용 프로그램 인증-Azure SQL 데이터베이스에 대 한 aaaGet 값 | Microsoft Docs"
description: "코드에서 SQL Database에 액세스하기 위한 서비스 사용자를 만듭니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a><span data-ttu-id="c7862-103">코드에서 응용 프로그램 tooaccess SQL 데이터베이스를 인증 하기 위해 필요한 hello 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7862-103">Get hello required values for authenticating an application tooaccess SQL Database from code</span></span>
<span data-ttu-id="c7862-104">toocreate 및 Azure 리소스 생성 된 hello 구독에서 hello Azure AAD (Active Directory) 도메인에 앱을 등록 해야 코드에서 SQL 데이터베이스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7862-104">toocreate and manage SQL Database from code you must register your app in hello Azure Active Directory (AAD) domain  in hello subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a><span data-ttu-id="c7862-105">응용 프로그램에서 서비스 보안 주체 tooaccess 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="c7862-105">Create a service principal tooaccess resources from an application</span></span>
<span data-ttu-id="c7862-106">최신 toohave hello 필요한 [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) 설치 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7862-106">You need toohave hello latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="c7862-107">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7862-107">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="c7862-108">hello 다음 PowerShell 스크립트를 만듭니다 hello Active Directory (AD) 응용 프로그램 및 서비스 hello 필요한 tooauthenticate C# 앱 주입니다.</span><span class="sxs-lookup"><span data-stu-id="c7862-108">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="c7862-109">hello 스크립트에서는 필요한 앞에 C# hello에 대 한 예제 값을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7862-109">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="c7862-110">자세한 내용은 참조 [Azure PowerShell을 사용 하 여 서비스 사용자 toocreate tooaccess 리소스](../azure-resource-manager/resource-group-authenticate-service-principal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7862-110">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

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




## <a name="see-also"></a><span data-ttu-id="c7862-111">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c7862-111">See also</span></span>
* [<span data-ttu-id="c7862-112">C#으로 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="c7862-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="c7862-113">데이터베이스를 사용 하 여 Azure Active Directory 인증 여 tooSQL 연결</span><span class="sxs-lookup"><span data-stu-id="c7862-113">Connecting tooSQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

