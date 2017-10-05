---
title: "HDInsight .NET SDK를 사용한 MapReduce 작업 제출 - Azure | Microsoft Docs"
description: "HDInsight .NET SDK를 사용하여 Azure HDInsight Hadoop에 MapReduce 작업을 제출하는 방법에 대해 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="ef0f0-103">HDInsight .NET SDK를 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="ef0f0-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="ef0f0-104">HDInsight .NET SDK를 사용하여 MapReduce 작업을 제출하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="ef0f0-105">HDInsight 클러스터에는 여러 MapReduce 샘플이 담긴 jar 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="ef0f0-106">이 jar 파일은 */example/jars/hadoop-mapreduce-examples.jar*입니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="ef0f0-107">샘플 중 하나는 *wordcount*입니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="ef0f0-108">C# 콘솔 응용 프로그램을 개발하여 단어 세기 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="ef0f0-109">이 작업은 */example/data/gutenberg/davinci.txt* 파일을 읽고 결과를 */example/data/davinciwordcount*에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="ef0f0-110">응용 프로그램을 다시 실행하려면 출력 폴더를 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="ef0f0-111">이 문서의 단계는 Windows 클라이언트에서 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="ef0f0-112">Hive와 함께 작동하도록 Linux, OS X 또는 Unix 클라이언트를 사용하는 방법에 대한 정보를 보려면 문서 맨 위에 표시된 탭 선택기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ef0f0-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef0f0-113">Prerequisites</span></span>
<span data-ttu-id="ef0f0-114">이 문서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="ef0f0-115">**HDInsight에 Hadoop 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="ef0f0-116">[HDInsight에서 Linux 기반 Hadoop 사용 시작](./hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="ef0f0-117">**Visual Studio 2013/2015/2017**</span><span class="sxs-lookup"><span data-stu-id="ef0f0-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="ef0f0-118">HDInsight .NET SDK를 사용하여 MapReduce 작업 제출</span><span class="sxs-lookup"><span data-stu-id="ef0f0-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="ef0f0-119">HDInsight .NET SDK는 .NET에서 HDInsight 클러스터로 더 쉽게 작업하도록 지원하는 .NET 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="ef0f0-120">**작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="ef0f0-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="ef0f0-121">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="ef0f0-122">NuGet 패키지 관리자 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="ef0f0-123">다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-123">Use the following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="ef0f0-124">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="ef0f0-125">작업을 다시 실행하려면 작업 출력 폴더 이름을 변경해야 합니다. 이 샘플에서는 "/example/data/davinciwordcount"입니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="ef0f0-126">작업이 성공적으로 완료되면 응용 프로그램은 출력 파일의 내용 "part-r-00000"을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef0f0-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef0f0-127">Next steps</span></span>
<span data-ttu-id="ef0f0-128">이 문서에서는 HDInsight 클러스터를 만드는 여러 가지 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="ef0f0-129">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="ef0f0-130">Hive 작업 제출에 대해서는 [HDInsight .NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="ef0f0-131">HDInsight 클러스터 만들기는 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="ef0f0-132">HDInsight 클러스터 관리는 [HDInsight에서 Hadoop 클러스터 관리](hdinsight-administer-use-portal-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="ef0f0-133">HDInsight .NET SDK에 대한 내용은 [HDInsight .NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="ef0f0-134">Azure에 대한 비대화형 인증은 [비대화형 인증 .NET HDInsight 응용 프로그램 만들기](hdinsight-create-non-interactive-authentication-dotnet-applications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0f0-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

