---
title: "aaaScript 작업-Python 설치 패키지를 Azure HDInsight의 Jupyter | Microsoft Docs"
description: "HDInsight Spark와 함께 사용할 수 있는 toouse 스크립트 동작 tooconfigure Jupyter 노트북 toouse 외부 python 패키지를 클러스터 하는 방법에 대해 단계별로 설명 합니다."
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="d400c-103">스크립트 동작 tooinstall 외부 Python 패키지를 사용 하 여 HDInsight의 Apache Spark 클러스터에서 Jupyter 노트북에 대 한</span><span class="sxs-lookup"><span data-stu-id="d400c-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d400c-104">셀 매직 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="d400c-105">스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="d400c-106">자세한 방법을 toouse 스크립트 동작 tooconfigure HDInsight (Linux) toouse 외부에는 Apache Spark 클러스터 커뮤니티 제공 **python** 하지 않은 패키지를 hello 클러스터에 기본적으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d400c-107">사용 하 여 Jupyter 노트북을 구성할 수도 있습니다 `%%configure` 매직 toouse 외부 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="d400c-108">지침에 대해서는 [HDInsight의 Apache Spark 클러스터에서 Jupyter Notebook과 함께 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d400c-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="d400c-109">Hello를 검색할 수 있습니다 [패키지 인덱스](https://pypi.python.org/pypi) 사용할 수 있는 패키지의 전체 목록은 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="d400c-110">다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="d400c-111">예를 들어 [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) 또는 [conda-forge](https://conda-forge.github.io/feedstocks.html)를 통해 제공되는 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="d400c-112">이 문서에서는 살펴보겠습니다 방법을 tooinstall hello [TensorFlow](https://www.tensorflow.org/) Actoin 스크립트를 사용 하 여 클러스터에 패키지 하 고 hello Jupyter 노트북을 통해 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d400c-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d400c-113">Prerequisites</span></span>
<span data-ttu-id="d400c-114">Hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-114">You must have hello following:</span></span>

* <span data-ttu-id="d400c-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d400c-115">An Azure subscription.</span></span> <span data-ttu-id="d400c-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d400c-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d400c-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="d400c-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d400c-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="d400c-119">Hdinsight Linux에 Spark 클러스터가 아직 없는 경우 클러스터를 만드는 동안 스크립트 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="d400c-120">Hello 설명서 방문 [toouse 사용자 지정 스크립트 작업을 어떻게](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="d400c-121">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="d400c-122">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="d400c-123">아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="d400c-124">Hello Spark 클러스터 블레이드에서 클릭 **스크립트 동작** 아래 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="d400c-125">Hello hello 헤드 노드 및 hello 작업자 노드에 TensorFlow를 설치 하는 사용자 지정 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="d400c-126">hello bash 스크립트에서 참조할 수 있습니다:에 대 한 방문을 hello 설명서 https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh [toouse 사용자 지정 스크립트 작업을 어떻게](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="d400c-127">Hello 클러스터 설치는 두 개의 python 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="d400c-128">Spark hello Anaconda python 설치에 있는 사용할지 `/usr/bin/anaconda/bin`합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="d400c-129">`/usr/bin/anaconda/bin/pip` 및 `/usr/bin/anaconda/bin/conda`를 통해 사용자 지정 작업에서 해당 설치 프로그램을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d400c-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="d400c-130">PySpark Jupyter 노트북을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="d400c-131">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="d400c-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="d400c-132">새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="d400c-133">Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="d400c-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="d400c-134">![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d400c-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="d400c-135">이제 `import tensorflow` 및 hello world 예제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="d400c-136">코드 toocopy:</span><span class="sxs-lookup"><span data-stu-id="d400c-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="d400c-137">hello 결과 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="d400c-138">![TensorFlow 코드 실행](./media/hdinsight-apache-spark-python-package-installation/execution.png "TensorFlow 코드 실행")</span><span class="sxs-lookup"><span data-stu-id="d400c-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="d400c-139"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="d400c-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d400c-140">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="d400c-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d400c-141">시나리오</span><span class="sxs-lookup"><span data-stu-id="d400c-141">Scenarios</span></span>
* [<span data-ttu-id="d400c-142">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="d400c-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d400c-143">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d400c-144">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="d400c-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d400c-145">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="d400c-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d400c-146">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="d400c-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d400c-147">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="d400c-147">Create and run applications</span></span>
* [<span data-ttu-id="d400c-148">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d400c-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d400c-149">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="d400c-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d400c-150">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="d400c-150">Tools and extensions</span></span>
* [<span data-ttu-id="d400c-151">HDInsight의 Apache Spark 클러스터에서 Jupyter 노트북과 함께 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="d400c-152">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="d400c-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d400c-153">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d400c-154">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="d400c-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d400c-155">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="d400c-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d400c-156">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="d400c-157">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="d400c-157">Manage resources</span></span>
* [<span data-ttu-id="d400c-158">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d400c-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d400c-159">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="d400c-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
