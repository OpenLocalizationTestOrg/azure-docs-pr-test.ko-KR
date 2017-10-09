---
title: "aaaRun Pig Apache Hadoop-Azure HDInsight.NET SDK와 함께 작업이 | Microsoft Docs"
description: "Toouse.NET SDK에 대 한 HDInsight의 Hadoop Pig 작업 tooHadoop를 toosubmit hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="88aae-103">HDInsight에서 Hadoop에 대 한 hello.NET SDK를 사용 하 여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="88aae-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="88aae-104">Toouse hello.NET SDK에 대 한 Hadoop toosubmit Apache Pig tooHadoop Azure HDInsight에서 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="88aae-105">hello HDInsight.NET SDK.NET에서 HDInsight 클러스터와 함께 보다 쉽게 toowork를 사용 하면.NET 클라이언트 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="88aae-106">Pig 일련의 데이터 변환 모델링 toocreate MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="88aae-107">이 문서에서는 toouse 기본 C# 응용 프로그램 toosubmit 마감할 tooan HDInsight 클러스터를 작업 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88aae-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="88aae-108">Prerequisites</span></span>

<span data-ttu-id="88aae-109">이 문서의 toocomplete hello 단계 hello 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="88aae-110">Azure HDInsight(HDInsight의 Hadoop) 클러스터(Windows 또는 Linux 기반)</span><span class="sxs-lookup"><span data-stu-id="88aae-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="88aae-111">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="88aae-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88aae-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="88aae-113">Visual Studio 2012, 2013, 2015 또는 2017.</span><span class="sxs-lookup"><span data-stu-id="88aae-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="88aae-114">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="88aae-114">Create hello application</span></span>

<span data-ttu-id="88aae-115">hello HDInsight.NET SDK.NET에서 HDInsight 클러스터와 함께 보다 쉽게 toowork 하므로.NET 클라이언트 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="88aae-116">Hello에서 **파일** 선택 Visual Studio에서 메뉴 **새로** 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="88aae-117">Hello 새 프로젝트에 대 한 값 형식 또는 다음 선택 hello:</span><span class="sxs-lookup"><span data-stu-id="88aae-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="88aae-118">속성</span><span class="sxs-lookup"><span data-stu-id="88aae-118">Property</span></span> | <span data-ttu-id="88aae-119">값</span><span class="sxs-lookup"><span data-stu-id="88aae-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="88aae-120">Category</span><span class="sxs-lookup"><span data-stu-id="88aae-120">Category</span></span> | <span data-ttu-id="88aae-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="88aae-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="88aae-122">Template</span><span class="sxs-lookup"><span data-stu-id="88aae-122">Template</span></span> | <span data-ttu-id="88aae-123">콘솔 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="88aae-123">Console Application</span></span> |
   | <span data-ttu-id="88aae-124">이름</span><span class="sxs-lookup"><span data-stu-id="88aae-124">Name</span></span> | <span data-ttu-id="88aae-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="88aae-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="88aae-126">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="88aae-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="88aae-127">Hello에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 또는 **Nuget 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="88aae-128">tooinstall hello.NET SDK 패키지 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="88aae-129">솔루션 탐색기에서 두 번 클릭 **Program.cs** tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="88aae-130">Hello 다음과 같이 hello 기존 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-130">Replace hello existing code with hello following.</span></span>

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
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
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

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="88aae-131">toostart hello 응용 프로그램 키를 눌러 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="88aae-132">tooexit hello 응용 프로그램 키를 눌러 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="88aae-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="88aae-133">요약</span><span class="sxs-lookup"><span data-stu-id="88aae-133">Summary</span></span>

<span data-ttu-id="88aae-134">볼 수 있듯이 hello Hadoop에 대 한.NET SDK 있습니다 Pig 작업 tooan HDInsight 클러스터를 제출 하 고 hello 작업 상태를 모니터링 하는 toocreate.NET 응용 프로그램을.</span><span class="sxs-lookup"><span data-stu-id="88aae-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88aae-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88aae-135">Next steps</span></span>

<span data-ttu-id="88aae-136">HDInsight의 Pig에 대한 자세한 내용은 [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88aae-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="88aae-137">HDInsight의 Hadoop 사용에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="88aae-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="88aae-138">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="88aae-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="88aae-139">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="88aae-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
