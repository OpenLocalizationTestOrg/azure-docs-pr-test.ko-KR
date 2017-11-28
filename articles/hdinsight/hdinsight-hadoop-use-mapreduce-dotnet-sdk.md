---
title: "HDInsight.NET SDK-Azure를 사용 하 여 aaaSubmit MapReduce 작업 | Microsoft Docs"
description: "MapReduce toosubmit tooAzure HDInsight Hadoop HDInsight.NET SDK를 사용 하 여 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="2dfe1-103">HDInsight .NET SDK를 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="2dfe1-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="2dfe1-104">Toosubmit MapReduce 작업 HDInsight.NET SDK를 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="2dfe1-105">HDInsight 클러스터에는 여러 MapReduce 샘플이 담긴 jar 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="2dfe1-106">hello jar 파일은 */example/jars/hadoop-mapreduce-examples.jar*합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="2dfe1-107">Hello 샘플 중 하나는 *wordcount*합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="2dfe1-108">C# 콘솔 응용 프로그램 toosubmit wordcount 작업을 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="2dfe1-109">hello 작업 읽고 hello */example/data/gutenberg/davinci.txt* 파일과 출력 hello 결과 너무*/example/data/davinciwordcount*합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="2dfe1-110">Toorerun hello 응용 프로그램을 사용 하도록 하려는 경우 hello 출력 폴더 정리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="2dfe1-111">이 문서의 hello 단계는 Windows 클라이언트에서 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="2dfe1-112">Linux, OS X 또는 Unix 클라이언트 toowork 하이브를 사용 하 여에 대 한 내용은 hello hello 문서 위쪽에 표시 된 hello 탭 선택기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2dfe1-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2dfe1-113">Prerequisites</span></span>
<span data-ttu-id="2dfe1-114">이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="2dfe1-115">**HDInsight에 Hadoop 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="2dfe1-116">[HDInsight에서 Linux 기반 Hadoop 사용 시작](./hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="2dfe1-117">**Visual Studio 2013/2015/2017**</span><span class="sxs-lookup"><span data-stu-id="2dfe1-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="2dfe1-118">HDInsight .NET SDK를 사용하여 MapReduce 작업 제출</span><span class="sxs-lookup"><span data-stu-id="2dfe1-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="2dfe1-119">hello HDInsight.NET SDK.NET에서 HDInsight 클러스터와 함께 보다 쉽게 toowork 하므로.NET 클라이언트 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="2dfe1-120">**tooSubmit 작업**</span><span class="sxs-lookup"><span data-stu-id="2dfe1-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="2dfe1-121">Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="2dfe1-122">Hello Nuget 패키지 관리자 콘솔에서에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="2dfe1-123">코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-123">Use hello following code:</span></span>
   
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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
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
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
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
4. <span data-ttu-id="2dfe1-124">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="2dfe1-125">toorun hello 작업 다시 변경 해야 hello 샘플에서 hello 작업 출력 폴더 이름는 "/ 예제/데이터/davinciwordcount"입니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="2dfe1-126">Hello 작업이 성공적으로 완료 되 면 hello 응용 프로그램 "파트-r-00000" hello 출력 파일의 hello 콘텐츠를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dfe1-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2dfe1-127">Next steps</span></span>
<span data-ttu-id="2dfe1-128">이 문서에서는 여러 가지 방법으로 toocreate HDInsight 클러스터에 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="2dfe1-129">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="2dfe1-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="2dfe1-130">Hive 작업 제출에 대해서는 [HDInsight .NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="2dfe1-131">HDInsight 클러스터 만들기는 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="2dfe1-132">HDInsight 클러스터 관리는 [HDInsight에서 Hadoop 클러스터 관리](hdinsight-administer-use-portal-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="2dfe1-133">HDInsight.NET SDK hello 학습, 참조 [HDInsight.NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="2dfe1-134">에 대 한 비 대화형 tooAzure 인증, 참조 [비 대화형 인증 HDInsight.NET 응용 프로그램을 만들](hdinsight-create-non-interactive-authentication-dotnet-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dfe1-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

