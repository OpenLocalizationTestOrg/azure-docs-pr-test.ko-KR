---
title: "스크립트 작업 - Azure HDInsight의 Jupyter를 사용해 Python 패키지 설치 | Microsoft Docs"
description: "스크립트 작업을 사용하여 HDInsight Spark 클러스터와 함께 제공되는 Jupyter 노트북에서 외부 python 패키지를 사용하도록 구성하는 방법에 대한 단계별 지침입니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="0a7d0-103">HDInsight의 Apache Spark 클러스터에서 스크립트 작업을 사용하여 Jupyter Notebook용 외부 python 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="0a7d0-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a7d0-104">셀 매직 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="0a7d0-105">스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="0a7d0-106">클러스터에 기본적으로 포함되지 않는 외부의 커뮤니티 제공 **python** 패키지를 사용하도록 HDInsight(Linux)의 Apache Spark 클러스터를 구성하는 스크립트 작업 사용 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="0a7d0-107">`%%configure` 매직을 사용하여 외부 패키지를 사용하도록 Jupyter Notebook을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="0a7d0-108">지침에 대해서는 [HDInsight의 Apache Spark 클러스터에서 Jupyter Notebook과 함께 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="0a7d0-109">사용할 수 있는 패키지의 전체 목록은 [패키지 인덱스](https://pypi.python.org/pypi)를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="0a7d0-110">다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="0a7d0-111">예를 들어 [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) 또는 [conda-forge](https://conda-forge.github.io/feedstocks.html)를 통해 제공되는 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="0a7d0-112">이 문서에서는 클러스터에서 스크립트 작업을 사용하여 [TensorFlow](https://www.tensorflow.org/) 패키지를 설치하고 Jupyter 노트북을 통해 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a7d0-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0a7d0-113">Prerequisites</span></span>
<span data-ttu-id="0a7d0-114">다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-114">You must have the following:</span></span>

* <span data-ttu-id="0a7d0-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-115">An Azure subscription.</span></span> <span data-ttu-id="0a7d0-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0a7d0-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0a7d0-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0a7d0-119">Hdinsight Linux에 Spark 클러스터가 아직 없는 경우 클러스터를 만드는 동안 스크립트 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="0a7d0-120">[사용자 지정 스크립트 작업을 사용하는 방법](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="0a7d0-121">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="0a7d0-122">[Azure 포털](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터에 대한 타일을 클릭합니다(시작 보드에 고정한 경우).</span><span class="sxs-lookup"><span data-stu-id="0a7d0-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="0a7d0-123">**모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="0a7d0-124">Spark 클러스터 블레이드에서 **사용량** 아래 **스크립트 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="0a7d0-125">헤드 노드 및 작업자 노드에 TensorFlow를 설치하는 사용자 지정 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="0a7d0-126">Bash 스크립트는 https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh에서 참조할 수 있습니다. [사용자 지정 스크립트 작업을 사용하는 방법](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0a7d0-127">클러스터에 두 개의 python 설치 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="0a7d0-128">Spark는 `/usr/bin/anaconda/bin`에 있는 Anaconda python 설치 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="0a7d0-129">`/usr/bin/anaconda/bin/pip` 및 `/usr/bin/anaconda/bin/conda`를 통해 사용자 지정 작업에서 해당 설치 프로그램을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="0a7d0-130">PySpark Jupyter 노트북을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="0a7d0-131">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="0a7d0-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="0a7d0-132">새 노트북이 만들어지고 Untitled.pynb 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="0a7d0-133">맨 위에서 노트북 이름을 클릭하고 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="0a7d0-134">![노트북 이름 제공](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "노트북 이름 제공")</span><span class="sxs-lookup"><span data-stu-id="0a7d0-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="0a7d0-135">이제 `import tensorflow` 및 hello world 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="0a7d0-136">복사할 코드:</span><span class="sxs-lookup"><span data-stu-id="0a7d0-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="0a7d0-137">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7d0-137">The result will look like this:</span></span>
    
    <span data-ttu-id="0a7d0-138">![TensorFlow 코드 실행](./media/hdinsight-apache-spark-python-package-installation/execution.png "TensorFlow 코드 실행")</span><span class="sxs-lookup"><span data-stu-id="0a7d0-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="0a7d0-139"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="0a7d0-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0a7d0-140">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="0a7d0-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0a7d0-141">시나리오</span><span class="sxs-lookup"><span data-stu-id="0a7d0-141">Scenarios</span></span>
* [<span data-ttu-id="0a7d0-142">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="0a7d0-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0a7d0-143">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0a7d0-144">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0a7d0-145">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="0a7d0-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0a7d0-146">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="0a7d0-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0a7d0-147">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="0a7d0-147">Create and run applications</span></span>
* [<span data-ttu-id="0a7d0-148">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0a7d0-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0a7d0-149">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0a7d0-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0a7d0-150">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="0a7d0-150">Tools and extensions</span></span>
* [<span data-ttu-id="0a7d0-151">HDInsight의 Apache Spark 클러스터에서 Jupyter 노트북과 함께 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0a7d0-152">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="0a7d0-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0a7d0-153">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="0a7d0-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0a7d0-154">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="0a7d0-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0a7d0-155">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="0a7d0-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0a7d0-156">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="0a7d0-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0a7d0-157">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="0a7d0-157">Manage resources</span></span>
* [<span data-ttu-id="0a7d0-158">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="0a7d0-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0a7d0-159">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="0a7d0-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
