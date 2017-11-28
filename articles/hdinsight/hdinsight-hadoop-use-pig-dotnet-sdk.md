---
title: "Hadoop용 .NET SDK로 Apache Pig 작업 실행 - Azure HDInsight | Microsoft Docs"
description: "HDInsight에서 Hadoop로 Pig 작업을 제출하기 위해 Hadoop용 .NET SDK를 사용하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="19c1f-103">HDInsight에서 Hadoop용 .NET SDK를 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="19c1f-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="19c1f-104">Azure HDInsight에서 Hadoop로 Apache Pig 작업을 제출하기 위해 Hadoop용 .NET SDK를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="19c1f-105">HDInsight .NET SDK는 .NET에서 HDInsight 클러스터로 더 쉽게 작업하도록 지원하는 .NET 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="19c1f-106">Pig를 사용하면 일련의 데이터 변환을 모델링하여 MapReduce 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="19c1f-107">이 문서에서는 기본 C# 응용 프로그램을 사용하여 HDInsight 클러스터에 Pig 작업을 제출하는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19c1f-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="19c1f-108">Prerequisites</span></span>

<span data-ttu-id="19c1f-109">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="19c1f-110">Azure HDInsight(HDInsight의 Hadoop) 클러스터(Windows 또는 Linux 기반)</span><span class="sxs-lookup"><span data-stu-id="19c1f-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="19c1f-111">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19c1f-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19c1f-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="19c1f-113">Visual Studio 2012, 2013, 2015 또는 2017.</span><span class="sxs-lookup"><span data-stu-id="19c1f-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="19c1f-114">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="19c1f-114">Create the application</span></span>

<span data-ttu-id="19c1f-115">HDInsight .NET SDK는 .NET에서 HDInsight 클러스터로 더 쉽게 작업하도록 지원하는 .NET 클라이언트 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="19c1f-116">Visual Studio의 **파일** 메뉴에서 **새로 만들기**와 **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="19c1f-117">새 프로젝트에서 다음 값을 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="19c1f-118">속성</span><span class="sxs-lookup"><span data-stu-id="19c1f-118">Property</span></span> | <span data-ttu-id="19c1f-119">값</span><span class="sxs-lookup"><span data-stu-id="19c1f-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="19c1f-120">Category</span><span class="sxs-lookup"><span data-stu-id="19c1f-120">Category</span></span> | <span data-ttu-id="19c1f-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="19c1f-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="19c1f-122">Template</span><span class="sxs-lookup"><span data-stu-id="19c1f-122">Template</span></span> | <span data-ttu-id="19c1f-123">콘솔 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="19c1f-123">Console Application</span></span> |
   | <span data-ttu-id="19c1f-124">이름</span><span class="sxs-lookup"><span data-stu-id="19c1f-124">Name</span></span> | <span data-ttu-id="19c1f-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="19c1f-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="19c1f-126">**확인** 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="19c1f-127">**도구** 메뉴에서 **라이브러리 패키지 관리자** 또는 **Nuget 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="19c1f-128">.NET SDK 패키지를 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="19c1f-129">솔루션 탐색기에서 **Program.cs** 를 두 번 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="19c1f-130">기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-130">Replace the existing code with the following.</span></span>

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="19c1f-131">응용 프로그램을 시작하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="19c1f-132">응용 프로그램을 종료하려면 **ENTER** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="19c1f-133">요약</span><span class="sxs-lookup"><span data-stu-id="19c1f-133">Summary</span></span>

<span data-ttu-id="19c1f-134">이처럼 Hadoop용 .NET SDK를 사용하면 Pig 작업을 HDInsight 클러스터를 제출하고, 작업 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19c1f-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19c1f-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19c1f-135">Next steps</span></span>

<span data-ttu-id="19c1f-136">HDInsight의 Pig에 대한 자세한 내용은 [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19c1f-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="19c1f-137">HDInsight에서 Hadoop을 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19c1f-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="19c1f-138">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="19c1f-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="19c1f-139">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="19c1f-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
