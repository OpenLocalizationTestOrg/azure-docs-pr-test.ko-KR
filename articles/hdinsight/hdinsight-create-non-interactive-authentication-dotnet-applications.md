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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>비대화형 인증 .NET HDInsight 응용 프로그램 만들기
응용 프로그램 자체의 id (비 대화형) 또는 hello id (대화형) hello 응용 프로그램의 hello 로그인 사용자의 Azure HDInsight.NET 응용 프로그램을 실행할 수 있습니다. Hello 대화형 응용 프로그램의 샘플을 보려면 [tooAzure HDInsight 연결](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight)합니다. 이 문서에서는 어떻게 toocreate 비 대화형 인증.NET 응용 프로그램 tooconnect tooAzure HDInsight를 관리 합니다.

비 대화형.NET 응용 프로그램에서 다음 항목이 필요합니다.

* Azure 구독 테넌트 ID(즉, 디렉터리 ID) [테넌트 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)를 참조하세요.
* hello Azure Active Directory 응용 프로그램 클라이언트 id입니다. [Azure Active Directory 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)와 [응용 프로그램 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.
* hello Azure Active Directory 응용 프로그램 비밀 키입니다. [응용 프로그램 인증 키 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
* HDInsight 클러스터. [시작 자습서](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)를 참조하세요.



## <a name="assign-azure-ad-application-toorole"></a>Azure AD 응용 프로그램 toorole 할당
응용 프로그램 tooa hello를 할당 해야 [역할](../active-directory/role-based-access-built-in-roles.md) toogrant 것 작업 수행을 위한 사용 권한입니다. Hello 범위 hello 구독, 리소스 그룹 또는 리소스의 hello 수준에서 설정할 수 있습니다. hello 권한은 상속 된 toolower 수준의 범위 (예: 리소스 그룹에 대 한 응용 프로그램 toohello 읽기 역할 의미 hello 리소스 그룹을 읽을 수를 추가 및 포함 된 모든 리소스). 이 자습서에서는 hello 리소스 그룹 수준에서 hello 범위를 설정 합니다. 자세한 내용은 참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)

**tooadd hello 소유자 역할 toohello Azure AD 응용 프로그램**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **리소스 그룹** hello 왼쪽된 창에서.
3. 이 자습서의 뒷부분에 나오는 하이브 쿼리를 실행할 hello HDInsight 클러스터를 포함 하는 hello 리소스 그룹을 클릭 합니다. 너무 많은 리소스 그룹이 없으면 hello 필터를 사용할 수 있습니다.
4. 클릭 **액세스 제어 (IAM)** hello 리소스 그룹 메뉴에서 합니다.
5. 클릭 **추가** hello에서 **사용자** 블레이드입니다.
6. Hello 명령 tooadd hello에 따라 **소유자** hello 마지막 절차에서 만든 역할 toohello Azure AD 응용 프로그램입니다. 성공적으로 완료 hello 소유자 역할을 가진 사용자 블레이드 hello에에서 나열 된 hello 응용 프로그램은 표시 됩니다.

## <a name="develop-hdinsight-client-application"></a>HDInsight 클라이언트 응용 프로그램 개발

1. C# 콘솔 응용 프로그램을 만듭니다.
2. Hello 다음 Nuget 패키지를 추가 합니다.

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. 아래의 코드 예제는 hello를 사용 합니다.

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

## <a name="next-steps"></a>다음 단계
* [포털을 사용하여 Azure Active Directory 응용 프로그램 및 서비스 주체 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Azure Resource Manager를 사용하여 서비스 주체 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)
