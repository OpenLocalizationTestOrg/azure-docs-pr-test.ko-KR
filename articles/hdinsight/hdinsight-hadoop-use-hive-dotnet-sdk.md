---
title: "HDInsight .NET SDK를 사용하여 Hive 쿼리 실행 - Azure | Microsoft Docs"
description: "HDInsight .NET SDK를 사용하여 Azure HDInsight Hadoop에 Hadoop 작업을 제출하는 방법에 대해 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 7b1a5f7ea3b2bda438727dc75a85557ea7930280
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="d028e-103">HDInsight .NET SDK를 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="d028e-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="d028e-104">HDInsight.NET SDK를 사용하여 Hive 쿼리를 제출하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="d028e-105">Hive 테이블을 나열하기 위한 Hive 쿼리를 제출한 후 결과를 표시하는 C# 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span></span>

> [!NOTE]
> <span data-ttu-id="d028e-106">이 문서의 단계는 Windows 클라이언트에서 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-106">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="d028e-107">Hive와 함께 작동하도록 Linux, OS X 또는 Unix 클라이언트를 사용하는 방법에 대한 정보를 보려면 문서 맨 위에 표시된 탭 선택기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d028e-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d028e-108">Prerequisites</span></span>
<span data-ttu-id="d028e-109">이 문서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-109">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="d028e-110">**HDInsight에 Hadoop 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="d028e-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="d028e-111">[HDInsight에서 Linux 기반 Hadoop 사용 시작](./hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d028e-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="d028e-112">**Visual Studio 2013/2015/2017**</span><span class="sxs-lookup"><span data-stu-id="d028e-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="d028e-113">HDInsight .NET SDK를 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="d028e-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="d028e-114">HDInsight .NET SDK는 .NET에서 HDInsight 클러스터로 더 쉽게 작업하도록 지원하는 .NET 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-114">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="d028e-115">**작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="d028e-115">**To Submit jobs**</span></span>

1. <span data-ttu-id="d028e-116">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d028e-117">NuGet 패키지 관리자 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-117">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="d028e-118">다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-118">Use the following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the Hive job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="d028e-119">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-119">Press **F5** to run the application.</span></span>

<span data-ttu-id="d028e-120">응용 프로그램의 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-120">The output of the application shall be similar to:</span></span>

![HDInsight Hadoop Hive 작업 출력](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="d028e-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d028e-122">Next steps</span></span>
<span data-ttu-id="d028e-123">이 문서에서는 HDInsight 클러스터를 만드는 여러 가지 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d028e-123">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="d028e-124">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d028e-124">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d028e-125">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d028e-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d028e-126">[HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="d028e-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="d028e-127">Azure Portal을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="d028e-127">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="d028e-128">HDInsight .NET SDK 참조</span><span class="sxs-lookup"><span data-stu-id="d028e-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="d028e-129">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="d028e-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d028e-130">HDInsight에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="d028e-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="d028e-131">비대화형 인증 .NET HDInsight 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d028e-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


