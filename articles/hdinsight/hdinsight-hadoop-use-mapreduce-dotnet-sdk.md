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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>HDInsight .NET SDK를 사용하여 MapReduce 작업 실행
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Toosubmit MapReduce 작업 HDInsight.NET SDK를 사용 하는 방법에 대해 알아봅니다. HDInsight 클러스터에는 여러 MapReduce 샘플이 담긴 jar 파일이 포함되어 있습니다. hello jar 파일은 */example/jars/hadoop-mapreduce-examples.jar*합니다.  Hello 샘플 중 하나는 *wordcount*합니다. C# 콘솔 응용 프로그램 toosubmit wordcount 작업을 개발 합니다.  hello 작업 읽고 hello */example/data/gutenberg/davinci.txt* 파일과 출력 hello 결과 너무*/example/data/davinciwordcount*합니다.  Toorerun hello 응용 프로그램을 사용 하도록 하려는 경우 hello 출력 폴더 정리 해야 합니다.

> [!NOTE]
> 이 문서의 hello 단계는 Windows 클라이언트에서 수행 되어야 합니다. Linux, OS X 또는 Unix 클라이언트 toowork 하이브를 사용 하 여에 대 한 내용은 hello hello 문서 위쪽에 표시 된 hello 탭 선택기를 사용 합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **HDInsight에 Hadoop 클러스터**. [HDInsight에서 Linux 기반 Hadoop 사용 시작](./hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.
* **Visual Studio 2013/2015/2017**

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>HDInsight .NET SDK를 사용하여 MapReduce 작업 제출
hello HDInsight.NET SDK.NET에서 HDInsight 클러스터와 함께 보다 쉽게 toowork 하므로.NET 클라이언트 라이브러리를 제공 합니다. 

**tooSubmit 작업**

1. Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.
2. Hello Nuget 패키지 관리자 콘솔에서에서 다음 명령을 hello를 실행 합니다.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. 코드 다음 hello를 사용 합니다.
   
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
4. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.

toorun hello 작업 다시 변경 해야 hello 샘플에서 hello 작업 출력 폴더 이름는 "/ 예제/데이터/davinciwordcount"입니다.

Hello 작업이 성공적으로 완료 되 면 hello 응용 프로그램 "파트-r-00000" hello 출력 파일의 hello 콘텐츠를 인쇄 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 여러 가지 방법으로 toocreate HDInsight 클러스터에 배웠습니다. 더 toolearn hello 다음 문서를 참조:

* Hive 작업 제출에 대해서는 [HDInsight .NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.
* HDInsight 클러스터 만들기는 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.
* HDInsight 클러스터 관리는 [HDInsight에서 Hadoop 클러스터 관리](hdinsight-administer-use-portal-linux.md)를 참조하세요.
* HDInsight.NET SDK hello 학습, 참조 [HDInsight.NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx)합니다.
* 에 대 한 비 대화형 tooAzure 인증, 참조 [비 대화형 인증 HDInsight.NET 응용 프로그램을 만들](hdinsight-create-non-interactive-authentication-dotnet-applications.md)합니다.

