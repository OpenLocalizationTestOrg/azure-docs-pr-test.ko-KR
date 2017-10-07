---
title: ".NET 및 Azure HDInsight를 사용 하 여 aaaRun Sqoop 작업 | Microsoft Docs"
description: "Toouse HDInsight.NET SDK toorun Sqoop 가져오고 Hadoop 클러스터와 Azure SQL 데이터베이스 내보내기에 대해 알아봅니다."
keywords: "sqoop 작업"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="f93fd-104">HDInsight에서 Hadoop용 .NET SDK를 사용하여 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f93fd-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="f93fd-105">HDInsight 클러스터와 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스 간에 내보내기 한 HDInsight tooimport toouse HDInsight.NET SDK toorun Sqoop 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="f93fd-106">이 문서의 hello 단계 중 하나는 Windows 기반 또는 Linux 기반 HDInsight 클러스터; 함께 사용할 수 있습니다. 그러나 다음이 단계는만 Windows 클라이언트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="f93fd-107">다른 방법을이 문서 toochoose hello 위에 hello 탭 선택기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="f93fd-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f93fd-108">Prerequisites</span></span>
<span data-ttu-id="f93fd-109">이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="f93fd-110">**HDInsight에 Hadoop 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="f93fd-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="f93fd-111">[클러스터 및 SQL 데이터베이스 만들기](hdinsight-use-sqoop.md#create-cluster-and-sql-database)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f93fd-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="f93fd-112">.NET SDK를 사용하여 HDInsight 클러스터에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="f93fd-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="f93fd-113">hello HDInsight.NET SDK.NET에서 HDInsight 클러스터와 함께 보다 쉽게 toowork 하므로.NET 클라이언트 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="f93fd-114">이 섹션에서는 C# 콘솔 응용 프로그램 tooexport hello hivesampletable toohello SQL 데이터베이스 테이블이이 자습서의 앞부분에서 만든 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="f93fd-115">Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="f93fd-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="f93fd-116">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="f93fd-117">Visual Studio 패키지 관리자 콘솔 hello hello 다음 Nuget 명령을 tooimport hello 패키지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="f93fd-118">Hello 코드 hello Program.cs 파일에 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="f93fd-119">키를 눌러 **F5** toorun hello 프로그램.</span><span class="sxs-lookup"><span data-stu-id="f93fd-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="f93fd-120">제한 사항</span><span class="sxs-lookup"><span data-stu-id="f93fd-120">Limitations</span></span>
* <span data-ttu-id="f93fd-121">대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="f93fd-122">일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 개의 삽입이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f93fd-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f93fd-123">Next steps</span></span>
<span data-ttu-id="f93fd-124">파악 했으므로 이제 어떻게 toouse Sqoop 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="f93fd-125">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f93fd-125">toolearn more, see:</span></span>

* <span data-ttu-id="f93fd-126">[HDInsight와 함께 Oozie 사용](hdinsight-use-oozie.md): Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="f93fd-127">[HDInsight를 사용 하 여 비행 연착 데이터를 분석](hdinsight-analyze-flight-delay-data.md): tooanalyze 비행 하이브 사용 하 여 데이터를 지연 하 고 다음 Sqoop tooexport 데이터 tooan Azure SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="f93fd-128">[데이터 tooHDInsight 업로드](hdinsight-upload-data.md): 데이터 tooHDInsight/Azure Blob 저장소에 업로드 하기 위한 다른 방법을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93fd-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

