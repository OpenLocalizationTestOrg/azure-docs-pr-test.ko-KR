---
title: ".NET 및 HDInsight를 사용하여 Sqoop 작업 실행 - Azure | Microsoft Docs"
description: "HDInsight .NET SDK를 사용하여 Hadoop 클러스터와 Azure SQL 데이터베이스 사이에서 Sqoop 가져오기 및 내보내기를 실행하는 방법을 알아봅니다."
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="dae57-104">HDInsight에서 Hadoop용 .NET SDK를 사용하여 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="dae57-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="dae57-105">HDInsight에서 HDInsight .NET SDK를 사용하여 HDInsight 클러스터와 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스 사이에서 가져오기 및 내보내는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="dae57-106">이 문서의 단계는 Windows 기반 또는 Linux 기반 HDInsight 클러스터와 사용할 수 있지만 이 단계에서만 Windows 클라이언트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="dae57-107">이 문서의 맨 위에 있는 탭 선택기를 사용하여 다른 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="dae57-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dae57-108">Prerequisites</span></span>
<span data-ttu-id="dae57-109">이 자습서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="dae57-110">**HDInsight에 Hadoop 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="dae57-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="dae57-111">[클러스터 및 SQL 데이터베이스 만들기](hdinsight-use-sqoop.md#create-cluster-and-sql-database)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dae57-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="dae57-112">.NET SDK를 사용하여 HDInsight 클러스터에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="dae57-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="dae57-113">HDInsight .NET SDK는 .NET에서 HDInsight 클러스터로 더 쉽게 작업하도록 지원하는 .NET 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="dae57-114">이 섹션에서는 C# 콘솔 응용 프로그램을 만들어 이 자습서의 앞 부분에서 만든 SQL Database 테이블에 hivesampletable을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="dae57-115">Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="dae57-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="dae57-116">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="dae57-117">Visual Studio 패키지 관리자 콘솔에서 다음 Nuget 명령을 실행하여 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="dae57-118">Program.cs 파일에서 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="dae57-119">**F5** 키를 눌러 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="dae57-120">제한 사항</span><span class="sxs-lookup"><span data-stu-id="dae57-120">Limitations</span></span>
* <span data-ttu-id="dae57-121">대량 내보내기 - Linux 기반 HDInsight와 함께 Microsoft SQL Server 또는 Azure SQL 데이터베이스에 데이터를 내보내는 데 사용된 Sqoop 커넥터도 현재 대량 삽입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="dae57-122">배치 - Linux 기반 HDInsight에서 삽입을 수행할 때 `-batch` 스위치를 사용하는 경우 Sqoop는 삽입 작업을 일괄 처리하는 대신 여러 번의 삽입 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dae57-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dae57-123">Next steps</span></span>
<span data-ttu-id="dae57-124">이제 Sqoop을 사용하는 방법에 대해 알아봤습니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="dae57-125">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dae57-125">To learn more, see:</span></span>

* <span data-ttu-id="dae57-126">[HDInsight와 함께 Oozie 사용](hdinsight-use-oozie.md): Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="dae57-127">[HDInsight를 사용하여 비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md): Hive를 사용하여 비행 지연 데이터를 분석한 후 Sqoop을 사용하여 데이터를 Azure SQL 데이터베이스로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="dae57-128">[HDInsight에 데이터 업로드](hdinsight-upload-data.md): HDInsight/Azure Blob 저장소에 데이터를 업로드하는 다른 방법을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dae57-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

