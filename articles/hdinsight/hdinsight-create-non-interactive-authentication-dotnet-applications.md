---
title: "비대화형 인증 .NET HDInsight 응용 프로그램 만들기 - Azure | Microsoft Docs"
description: "비대화형 인증 .NET HDInsight 응용 프로그램을 만드는 방법을 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="c3079-103">비대화형 인증 .NET HDInsight 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c3079-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="c3079-104">응용 프로그램의 고유한 ID(비대화형) 또는 응용 프로그램에 로그인한 사용자의 ID(대화형)로 .NET Azure HDInsight 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="c3079-105">대화형 응용 프로그램의 샘플은 [Azure HDInsight에 연결](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3079-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="c3079-106">이 문서에서는 비대화형 인증 .NET 응용 프로그램을 만들어 Azure에 연결하고 HDInsight를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="c3079-107">비 대화형.NET 응용 프로그램에서 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="c3079-108">Azure 구독 테넌트 ID(즉, 디렉터리 ID)</span><span class="sxs-lookup"><span data-stu-id="c3079-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="c3079-109">[테넌트 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3079-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="c3079-110">Azure Active Directory 응용 프로그램 클라이언트 ID.</span><span class="sxs-lookup"><span data-stu-id="c3079-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="c3079-111">[Azure Active Directory 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)와 [응용 프로그램 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3079-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="c3079-112">Azure Active Directory 응용 프로그램 비밀 키.</span><span class="sxs-lookup"><span data-stu-id="c3079-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="c3079-113">[응용 프로그램 인증 키 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3079-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3079-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3079-114">Prerequisites</span></span>
* <span data-ttu-id="c3079-115">HDInsight 클러스터.</span><span class="sxs-lookup"><span data-stu-id="c3079-115">HDInsight cluster.</span></span> <span data-ttu-id="c3079-116">[시작 자습서](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3079-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="c3079-117">역할에 Azure AD 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="c3079-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="c3079-118">작업 수행 권한을 부여하려면 응용 프로그램을 [역할](../active-directory/role-based-access-built-in-roles.md)에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="c3079-119">구독, 리소스 그룹 또는 리소스 수준에서 범위를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="c3079-120">권한은 하위 수준의 범위로 상속됩니다. 예를 들어 응용 프로그램에 리소스 그룹에 대한 읽기 권한자 역할을 추가하면 응용 프로그램이 리소스 그룹과 그 안에 포함된 모든 리소스를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="c3079-121">이 자습서에서는 리소스 그룹 수준에서 범위를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="c3079-122">자세한 정보는 [역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스 관리](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3079-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="c3079-123">**Azure AD 응용 프로그램에 소유자 역할을 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="c3079-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="c3079-124">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c3079-125">왼쪽 창에서 **리소스 그룹** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="c3079-126">이 자습서의 뒷부분에서 Hive 쿼리를 실행할 HDInsight 클러스터가 포함된 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="c3079-127">너무 많은 리소스 그룹이 있는 경우 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="c3079-128">리소스 그룹 메뉴에서 **액세스 제어(IAM)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="c3079-129">**사용자** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="c3079-130">지침에 따라 마지막 절차에서 만든 Azure AD 응용 프로그램에 **소유자**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="c3079-131">성공적으로 완료하면 소유자 역할이 있는 사용자가 블레이드에 나열된 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="c3079-132">HDInsight 클라이언트 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="c3079-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="c3079-133">C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-133">Create a C# console application.</span></span>
2. <span data-ttu-id="c3079-134">다음 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="c3079-135">다음 코드 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3079-135">Use the following code sample:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter the Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a><span data-ttu-id="c3079-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3079-136">Next steps</span></span>
* [<span data-ttu-id="c3079-137">포털을 사용하여 Azure Active Directory 응용 프로그램 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="c3079-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="c3079-138">Azure Resource Manager를 사용하여 서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="c3079-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="c3079-139">Azure 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="c3079-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
