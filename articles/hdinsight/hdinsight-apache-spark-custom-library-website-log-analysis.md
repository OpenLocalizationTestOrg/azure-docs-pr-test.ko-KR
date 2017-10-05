---
title: "Spark에서 Python 라이브러리를 사용하여 웹 사이트 로그 분석 - Azure | Microsoft Docs"
description: "이 Notebook에서는 Azure HDInsight의 Spark와 함께 사용자 지정 라이브러리를 사용하여 로그 데이터를 분석하는 방법을 보여 줍니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2a028beb1e9eae89d32238e61b6f67c4c059a94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="83c72-103">HDInsight에서 Spark 클러스터와 함께 사용자 지정 Python 라이브러리를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="83c72-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="83c72-104">이 노트북에서는 HDInsight의 Spark와 함께 사용자 지정 라이브러리를 사용하여 로그 데이터를 분석하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="83c72-105">사용하는 사용자 지정 라이브러리는 **iislogparser.py**라는 Python 라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="83c72-106">이 자습서는 HDInsight에서 만드는 Spark(Linux) 클러스터에서 Jupyter 노트북으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="83c72-107">Notebook 환경을 통해 Notebook 자체에서 Python 코드 조각을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="83c72-108">Notebook 내에서 자습서를 수행하려면 Spark 클러스터를 만들고 Jupyter Notebook(`https://CLUSTERNAME.azurehdinsight.net/jupyter`)을 시작한 다음 **PySpark** 폴더 아래의 **사용자 지정 library.ipynb를 사용하여 Spark에서 로그 분석** Notebook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="83c72-109">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="83c72-109">**Prerequisites:**</span></span>

<span data-ttu-id="83c72-110">다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-110">You must have the following:</span></span>

* <span data-ttu-id="83c72-111">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="83c72-111">An Azure subscription.</span></span> <span data-ttu-id="83c72-112">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c72-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="83c72-113">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="83c72-114">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c72-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="83c72-115">RDD로 원시 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="83c72-115">Save raw data as an RDD</span></span>
<span data-ttu-id="83c72-116">이 섹션에서는 HDInsight에서 Apache Spark 클러스터와 연결된 [Jupyter](https://jupyter.org) 노트북을 사용하여 원시 샘플 데이터를 처리하고 하이브 테이블로 저장하는 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="83c72-117">샘플 데이터는 기본적으로 모든 클러스터에서 사용 가능한 .csv 파일(hvac.csv)입니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="83c72-118">데이터를 하이브 테이블로 저장한 후에는 다음 섹션에서 Power BI 및 Tableau와 같은 BI 도구를 사용하여 하이브 테이블에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="83c72-119">[Azure Portal](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터의 타일을 클릭합니다(시작 보드에 고정한 경우).</span><span class="sxs-lookup"><span data-stu-id="83c72-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="83c72-120">**모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="83c72-121">Spark 클러스터 블레이드에서 **클러스터 대시보드**를 클릭하고 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="83c72-122">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="83c72-123">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter Notebook에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="83c72-124">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="83c72-125">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-125">Create a new notebook.</span></span> <span data-ttu-id="83c72-126">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="83c72-127">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="83c72-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="83c72-128">새 노트북이 만들어지고 Untitled.pynb 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="83c72-129">맨 위에서 노트북 이름을 클릭하고 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="83c72-130">![노트북 이름 제공](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "노트북 이름 제공")</span><span class="sxs-lookup"><span data-stu-id="83c72-130">![Provide a name for the notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="83c72-131">PySpark 커널을 사용하여 노트북을 만들었기 때문에 컨텍스트를 명시적으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="83c72-132">첫 번째 코드 셀을 실행하면 Spark 및 Hive 컨텍스트가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="83c72-133">이 시나리오에 필요한 형식을 가져와 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="83c72-134">빈 셀에 다음 코드 조각을 붙여넣은 다음 **SHIFT + ENTER**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="83c72-135">클러스터에서 이미 사용할 수 있는 샘플 로그 데이터를 사용하는 RDD를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="83c72-136">**\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**에서 클러스터와 연결된 기본 저장소 계정의 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="83c72-137">샘플 로그 설정을 검색하여 이전 단계가 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="83c72-138">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="83c72-139">사용자 지정 Python 라이브러리를 사용하여 로그 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="83c72-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="83c72-140">위의 출력에서 처음 몇 줄은 헤더 정보를 포함하고 나머지 줄은 해당 헤더에 설명된 스키마와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="83c72-141">이러한 로그를 구문 분석하는 것은 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="83c72-142">따라서 이러한 로그를 훨씬 쉽게 구문 분석하는 사용자 지정 Python 라이브러리(**iislogparser.py**)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="83c72-143">기본적으로 이 라이브러리는 HDInsight의 Spark 클러스터( **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="83c72-144">그러나 이 라이브러리는 `PYTHONPATH`에 있지 않으므로 `import iislogparser`와(과) 같은 import 문을 사용하여 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="83c72-145">이 라이브러리를 사용하려면 모든 작업자 노드에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="83c72-146">다음 조각을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-146">Run the following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="83c72-147">`iislogparser`은(는) 로그 줄이 머리글 행인 경우 함수 `None`을(를) 반환하고 로그 줄을 발견하는 경우 `LogLine` 클래스의 인스턴스를 반환하는 함수 `parse_log_line`을(를) 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="83c72-148">`LogLine` 클래스를 사용하여 RDD에서 로그 줄만을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="83c72-149">몇 가지 추출된 로그 줄을 검색하여 단계가 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="83c72-150">다음과 유사하게 출력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="83c72-151">그러면 `LogLine` 클래스에는 로그 항목에 오류 코드가 있는지 여부를 반환하는 `is_error()`와(과) 같은 몇 가지 유용한 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="83c72-152">이를 사용하여 추출된 로그 줄의 오류의 수를 계산한 다음 다른 파일에 모든 오류를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="83c72-153">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="83c72-154">**Matplotlib** 를 사용하여 데이터의 시각화를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="83c72-155">예를 들어 오랜 시간 동안 실행되는 요청의 원인을 격리하려는 경우 평균적으로 제공하는 데 가장 많은 시간이 걸리는 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="83c72-156">다음 코드 조각은 요청을 처리하는 데 가장 많은 시간이 걸리는 상위 25개의 리소스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="83c72-157">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-157">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="83c72-158">그림의 형식에 이 정보를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="83c72-159">플롯을 만드는 첫 번째 단계로, 먼저 임시 테이블 **AverageTime**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="83c72-160">이 테이블은 특정 시간에 특수한 대기 시간 급증 현상이 없는지 확인하도록 시간으로 로그를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="83c72-161">다음 SQL 쿼리를 실행하여 **AverageTime** 테이블의 모든 레코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="83c72-162">`-o averagetime` 앞의 `%%sql` 매직은 쿼리 출력이 Jupyter 서버(일반적으로 클러스터의 헤드 노드)에서 로컬로 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="83c72-163">출력은 [averagetime](http://pandas.pydata.org/) 이라는 이름이 지정된 **Pandas**데이터 프레임으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="83c72-164">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-164">You should see an output like the following:</span></span>

   <span data-ttu-id="83c72-165">![SQL 쿼리 출력](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL 쿼리 출력")</span><span class="sxs-lookup"><span data-stu-id="83c72-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="83c72-166">`%%sql` 매직에 대한 자세한 내용은 [%%sql 매직에서 지원되는 매개 변수](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c72-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="83c72-167">이제 데이터 시각화를 구성하는 데 사용되는 라이브러리인 Matplotlib를 사용하여 플롯을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="83c72-168">로컬로 유지되는 **averagetime** 데이터 프레임에서 플롯을 만들어야 하므로 코드 조각은 `%%local` magic으로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="83c72-169">그러면 코드가 Jupyter 서버에서 로컬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="83c72-170">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-170">You should see an output like the following:</span></span>

   <span data-ttu-id="83c72-171">![Matplotlib 출력](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib 출력")</span><span class="sxs-lookup"><span data-stu-id="83c72-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="83c72-172">응용 프로그램 실행을 완료한 후 리소스를 해제하도록 Notebook을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="83c72-173">이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="83c72-174">그러면 Notebook이 종료되고 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="83c72-174">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="83c72-175"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="83c72-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="83c72-176">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="83c72-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="83c72-177">시나리오</span><span class="sxs-lookup"><span data-stu-id="83c72-177">Scenarios</span></span>
* [<span data-ttu-id="83c72-178">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="83c72-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="83c72-179">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="83c72-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="83c72-180">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="83c72-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="83c72-181">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="83c72-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="83c72-182">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="83c72-182">Create and run applications</span></span>
* [<span data-ttu-id="83c72-183">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="83c72-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="83c72-184">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="83c72-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="83c72-185">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="83c72-185">Tools and extensions</span></span>
* [<span data-ttu-id="83c72-186">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="83c72-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="83c72-187">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="83c72-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="83c72-188">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="83c72-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="83c72-189">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="83c72-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="83c72-190">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="83c72-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="83c72-191">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="83c72-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="83c72-192">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="83c72-192">Manage resources</span></span>
* [<span data-ttu-id="83c72-193">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="83c72-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="83c72-194">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="83c72-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
