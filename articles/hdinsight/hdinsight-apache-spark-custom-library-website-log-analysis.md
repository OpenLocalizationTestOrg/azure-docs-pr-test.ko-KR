---
title: "Spark-Azure에서에서 Python 라이브러리를 사용 하 여 웹 사이트 로그 aaaAnalyze | Microsoft Docs"
description: "이 전자 필기장 tooanalyze Azure HDInsight의 Spark와 함께 사용자 지정 라이브러리를 사용 하 여 데이터를 기록 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="07370-103">HDInsight에서 Spark 클러스터와 함께 사용자 지정 Python 라이브러리를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="07370-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="07370-104">이 전자 필기장 tooanalyze HDInsight의 Spark와 함께 사용자 지정 라이브러리를 사용 하 여 데이터를 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07370-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="07370-105">사용 하 여 hello 사용자 지정 라이브러리는 호출 하는 Python 라이브러리 **iislogparser.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="07370-106">이 자습서는 HDInsight에서 만드는 Spark(Linux) 클러스터에서 Jupyter 노트북으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="07370-107">hello 노트북 경험 자체 hello 노트북에서 Python 코드 조각을 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="07370-108">노트북, 내에서 tooperform hello 자습서 Spark 클러스터를 만듭니다을 시작 하며, Jupyter 노트북 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), 다음 hello 노트북을 실행 하 고 **사용자 지정 library.ipynb를 사용 하 여 Spark와 함께 로그를 분석** hello 아래  **PySpark** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="07370-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="07370-109">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="07370-109">**Prerequisites:**</span></span>

<span data-ttu-id="07370-110">Hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-110">You must have hello following:</span></span>

* <span data-ttu-id="07370-111">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="07370-111">An Azure subscription.</span></span> <span data-ttu-id="07370-112">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07370-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="07370-113">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="07370-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="07370-114">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07370-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="07370-115">RDD로 원시 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="07370-115">Save raw data as an RDD</span></span>
<span data-ttu-id="07370-116">이 섹션을 사용 하 여 hello [Jupyter](https://jupyter.org) 원시 샘플 데이터를 처리 하 고 하이브 테이블로 저장 하는 HDInsight toorun 작업에는 Apache Spark 클러스터와 연결 된 노트북 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="07370-117">hello 예제 데이터는.csv 파일 (hvac.csv) 사용할 수 있는 기본적으로 모든 클러스터에서.</span><span class="sxs-lookup"><span data-stu-id="07370-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="07370-118">하이브 테이블로 데이터를 저장 hello 다음 섹션에서 Power BI 및 Tableau와 같은 BI 도구를 사용 하 여 toohello 하이브 테이블을 연결할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07370-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="07370-119">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="07370-120">아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="07370-121">Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="07370-122">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="07370-123">또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="07370-124">대체 **CLUSTERNAME** 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="07370-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="07370-125">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07370-125">Create a new notebook.</span></span> <span data-ttu-id="07370-126">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="07370-127">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="07370-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="07370-128">새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="07370-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="07370-129">Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="07370-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="07370-130">![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")</span><span class="sxs-lookup"><span data-stu-id="07370-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="07370-131">Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="07370-132">hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다 드립니다 hello 첫 번째 코드 셀을 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="07370-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="07370-133">이 시나리오에 대 한 필요한 hello 형식은 가져와서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="07370-134">다음 코드 조각에서 빈 셀을 hello를 붙여 넣고 다음 키를 누릅니다 **SHIFT + ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="07370-135">RDD hello 클러스터에서 이미 사용할 수 있는 hello 샘플 로그 데이터를 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07370-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="07370-136">Hello 데이터에서 hello 클러스터와 연결 된 hello 기본 저장소 계정에 액세스할 수 있습니다 **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="07370-137">이전 단계에서 완료 hello 샘플 로그 집합 tooverify를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="07370-138">출력 유사한 toohello 다음을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="07370-139">사용자 지정 Python 라이브러리를 사용하여 로그 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="07370-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="07370-140">위의 hello 출력 hello 처음 몇 줄 hello 헤더 정보를 포함 하 고 나머지 각 줄에 해당 헤더에 설명 된 hello 스키마와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="07370-141">이러한 로그를 구문 분석하는 것은 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="07370-142">따라서 이러한 로그를 훨씬 쉽게 구문 분석하는 사용자 지정 Python 라이브러리(**iislogparser.py**)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="07370-143">기본적으로 이 라이브러리는 HDInsight의 Spark 클러스터( **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="07370-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="07370-144">그러나이 라이브러리에에서 없는 hello `PYTHONPATH` 같은 import 문을 사용 하 여 사용할 수 있도록 `import iislogparser`합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="07370-145">toouse이이 라이브러리 tooall hello 작업자 노드를 배포 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="07370-146">다음 코드 조각 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="07370-147">`iislogparser`함수를 제공 `parse_log_line` 반환 하는 `None` 로그 줄은 머리글 행과 hello의 인스턴스를 반환 하는 경우 `LogLine` 로그 줄 발생 하는 경우 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="07370-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="07370-148">사용 하 여 hello `LogLine` 클래스 tooextract hello RDD에서에서 로그 줄을만 hello:</span><span class="sxs-lookup"><span data-stu-id="07370-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="07370-149">몇 가지 단계에서 완료 hello 행 압축 푼된 정도가 tooverify 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="07370-150">hello 출력은 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07370-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="07370-151">hello `LogLine` 클래스에 대 한 몇 가지 유용한 메서드 같은 `is_error()`, 로그 항목에서 오류 코드에 있는지 여부를 반환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="07370-152">Hello 추출 로그 줄에서 오류의이 toocompute hello 수를 사용 하 여 하 한 다음 모든 hello 오류 tooa 다른 파일을 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="07370-153">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="07370-154">사용할 수도 있습니다 **Matplotlib** tooconstruct hello 데이터를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="07370-155">예를 들어 tooisolate hello 원인을 오랜 시간 동안 실행 되는 요청을 사용 하도록 하려는 경우 toofind hello 파일 평균 hello 시간 tooserve 대부분을 사용 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="07370-156">아래 hello 조각 hello 상위 25 리소스 검색 하는 대부분의 시간 tooserve 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="07370-157">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-157">You should see an output like hello following:</span></span>

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
5. <span data-ttu-id="07370-158">그림의 hello 형태로이 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07370-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="07370-159">첫 번째 단계 toocreate 플롯을 알려 주세요 먼저 만드는 것이 임시 테이블 **AverageTime**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="07370-160">특정 시간에 모든 비정상적인 대기 시간 급증 되었으면 테이블 그룹 hello hello 시간 toosee로 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="07370-161">다음에서 실행할 수 있습니다 다음 SQL 쿼리 tooget hello 모든 hello 레코드 hello **AverageTime** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="07370-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="07370-162">hello `%%sql` 매직 뒤 `-o averagetime` hello 쿼리의 hello 출력 (일반적으로 hello의 헤드 노드에 hello 클러스터) hello Jupyter 서버에서 로컬로 유지 되도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="07370-163">hello 출력으로 유지 되는 [팬더](http://pandas.pydata.org/) 데이터 프레임 hello로 이름을 지정 **averagetime**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="07370-164">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="07370-165">![SQL 쿼리 출력](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL 쿼리 출력")</span><span class="sxs-lookup"><span data-stu-id="07370-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="07370-166">Hello에 대 한 자세한 내용은 `%%sql` 매직, 참조 [hello로 지원 되는 매개 변수 %%sql 매직](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="07370-167">이제 Matplotlib를 사용할 수 있습니다, 라이브러리의 데이터를 toocreate 플롯을 tooconstruct 시각화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="07370-168">로컬로 hello에서 hello 플롯을 만들어야 하기 때문에 유지 **averagetime** 데이터 프레임을 hello 코드 조각 hello로 시작 해야 `%%local` 매직 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="07370-169">이렇게 하면 hello 코드 hello Jupyter 서버에서 로컬로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07370-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="07370-170">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="07370-171">![Matplotlib 출력](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib 출력")</span><span class="sxs-lookup"><span data-stu-id="07370-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="07370-172">Hello 응용 프로그램 실행을 완료 한 후 종료 hello 노트북 toorelease hello 리소스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="07370-173">toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="07370-174">이 종료 및 닫기 hello 전자 필기장 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="07370-175"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="07370-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="07370-176">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="07370-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="07370-177">시나리오</span><span class="sxs-lookup"><span data-stu-id="07370-177">Scenarios</span></span>
* [<span data-ttu-id="07370-178">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="07370-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="07370-179">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="07370-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="07370-180">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="07370-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="07370-181">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="07370-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="07370-182">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="07370-182">Create and run applications</span></span>
* [<span data-ttu-id="07370-183">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="07370-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="07370-184">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="07370-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="07370-185">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="07370-185">Tools and extensions</span></span>
* [<span data-ttu-id="07370-186">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="07370-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="07370-187">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="07370-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="07370-188">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="07370-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="07370-189">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="07370-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="07370-190">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="07370-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="07370-191">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="07370-192">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="07370-192">Manage resources</span></span>
* [<span data-ttu-id="07370-193">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07370-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="07370-194">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="07370-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
