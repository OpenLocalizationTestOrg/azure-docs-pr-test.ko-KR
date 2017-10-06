---
title: "HDInsight.NET SDK-Azure를 사용 하 여 aaaRun 하이브 쿼리 | Microsoft Docs"
description: "Hadoop toosubmit tooAzure HDInsight Hadoop HDInsight.NET SDK를 사용 하 여 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>HDInsight .NET SDK를 사용하여 Hive 쿼리 실행
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

HDInsight.NET SDK를 사용 하 여 하이브 toosubmit을 쿼리 하는 방법에 대해 알아봅니다. C# 프로그램 toosubmit 하이브 테이블을 나열 하는 것에 대 한 하이브 쿼리를 작성 하 고 hello 결과 표시 합니다.

> [!NOTE]
> 이 문서의 hello 단계는 Windows 클라이언트에서 수행 되어야 합니다. Linux, OS X 또는 Unix 클라이언트 toowork 하이브를 사용 하 여에 대 한 내용은 hello hello 문서 위쪽에 표시 된 hello 탭 선택기를 사용 합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **HDInsight에 Hadoop 클러스터**. [HDInsight에서 Linux 기반 Hadoop 사용 시작](./hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.
* **Visual Studio 2013/2015/2017**

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>HDInsight .NET SDK를 사용하여 Hive 쿼리 제출
hello HDInsight.NET SDK.NET에서 HDInsight 클러스터와 함께 보다 쉽게 toowork 하므로.NET 클라이언트 라이브러리를 제공 합니다. 

**tooSubmit 작업**

1. Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.
2. Hello Nuget 패키지 관리자 콘솔에서에서 다음 명령을 hello를 실행 합니다.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. 코드 다음 hello를 사용 합니다.

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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
4. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.

hello 응용 프로그램의 출력을 hello 유사 해야 합니다.:

![HDInsight Hadoop Hive 작업 출력](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>다음 단계
이 문서에서는 여러 가지 방법으로 toocreate HDInsight 클러스터에 배웠습니다. 더 toolearn hello 다음 문서를 참조:

* [Azure HDInsight 시작][hdinsight-get-started]
* [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision]
* [Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop 클러스터를 관리 합니다.](hdinsight-administer-use-management-portal.md)
* [HDInsight .NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Sqoop 사용](hdinsight-use-sqoop-mac-linux.md)
* [비대화형 인증 .NET HDInsight 응용 프로그램 만들기](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


