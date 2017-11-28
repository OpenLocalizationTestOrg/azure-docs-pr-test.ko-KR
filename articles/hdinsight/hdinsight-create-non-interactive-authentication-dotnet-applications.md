---
title: "aaaCreate 비 대화형 인증.NET HDInsight applciations-Azure | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 비 대화형 인증 HDInsight.NET 응용 프로그램입니다."
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
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="27c43-103">비대화형 인증 .NET HDInsight 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="27c43-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="27c43-104">응용 프로그램 자체의 id (비 대화형) 또는 hello id (대화형) hello 응용 프로그램의 hello 로그인 사용자의 Azure HDInsight.NET 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="27c43-105">Hello 대화형 응용 프로그램의 샘플을 보려면 [tooAzure HDInsight 연결](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight)합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="27c43-106">이 문서에서는 어떻게 toocreate 비 대화형 인증.NET 응용 프로그램 tooconnect tooAzure HDInsight를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="27c43-107">비 대화형.NET 응용 프로그램에서 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="27c43-108">Azure 구독 테넌트 ID(즉, 디렉터리 ID)</span><span class="sxs-lookup"><span data-stu-id="27c43-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="27c43-109">[테넌트 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27c43-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="27c43-110">hello Azure Active Directory 응용 프로그램 클라이언트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="27c43-111">[Azure Active Directory 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)와 [응용 프로그램 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27c43-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="27c43-112">hello Azure Active Directory 응용 프로그램 비밀 키입니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="27c43-113">[응용 프로그램 인증 키 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27c43-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27c43-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="27c43-114">Prerequisites</span></span>
* <span data-ttu-id="27c43-115">HDInsight 클러스터.</span><span class="sxs-lookup"><span data-stu-id="27c43-115">HDInsight cluster.</span></span> <span data-ttu-id="27c43-116">[시작 자습서](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27c43-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="27c43-117">Azure AD 응용 프로그램 toorole 할당</span><span class="sxs-lookup"><span data-stu-id="27c43-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="27c43-118">응용 프로그램 tooa hello를 할당 해야 [역할](../active-directory/role-based-access-built-in-roles.md) toogrant 것 작업 수행을 위한 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="27c43-119">Hello 범위 hello 구독, 리소스 그룹 또는 리소스의 hello 수준에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="27c43-120">hello 권한은 상속 된 toolower 수준의 범위 (예: 리소스 그룹에 대 한 응용 프로그램 toohello 읽기 역할 의미 hello 리소스 그룹을 읽을 수를 추가 및 포함 된 모든 리소스).</span><span class="sxs-lookup"><span data-stu-id="27c43-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="27c43-121">이 자습서에서는 hello 리소스 그룹 수준에서 hello 범위를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="27c43-122">자세한 내용은 참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="27c43-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="27c43-123">**tooadd hello 소유자 역할 toohello Azure AD 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="27c43-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="27c43-124">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27c43-125">클릭 **리소스 그룹** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="27c43-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="27c43-126">이 자습서의 뒷부분에 나오는 하이브 쿼리를 실행할 hello HDInsight 클러스터를 포함 하는 hello 리소스 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="27c43-127">너무 많은 리소스 그룹이 없으면 hello 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="27c43-128">클릭 **액세스 제어 (IAM)** hello 리소스 그룹 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="27c43-129">클릭 **추가** hello에서 **사용자** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="27c43-130">Hello 명령 tooadd hello에 따라 **소유자** hello 마지막 절차에서 만든 역할 toohello Azure AD 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="27c43-131">성공적으로 완료 hello 소유자 역할을 가진 사용자 블레이드 hello에에서 나열 된 hello 응용 프로그램은 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="27c43-132">HDInsight 클라이언트 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="27c43-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="27c43-133">C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-133">Create a C# console application.</span></span>
2. <span data-ttu-id="27c43-134">Hello 다음 Nuget 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="27c43-135">아래의 코드 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c43-135">Use hello following code sample:</span></span>

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
                private static string secretKey = "<Enter hello Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="27c43-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27c43-136">Next steps</span></span>
* [<span data-ttu-id="27c43-137">포털을 사용하여 Azure Active Directory 응용 프로그램 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="27c43-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="27c43-138">Azure Resource Manager를 사용하여 서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="27c43-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="27c43-139">Azure 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="27c43-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
