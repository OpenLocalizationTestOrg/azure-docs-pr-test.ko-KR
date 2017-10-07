---
title: "심층 학습에 대 한 Azure HDInsight spark Cognitive Toolkit aaaMicrosoft | Microsoft Docs"
description: "알아봅니다 방법는 숙련 된 Microsoft Cognitive 도구 키트 심층 학습 모델에는 Azure HDInsight Spark 클러스터에 hello Spark Python API를 사용 하 여 적용 된 tooa dataset 될 수 있습니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="a4992-103">Azure HDInsight Spark 클러스터에서 Microsoft Cognitive 도구 키트 심층 학습 모델 사용</span><span class="sxs-lookup"><span data-stu-id="a4992-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="a4992-104">이 문서에서는 다음 단계 hello 수행 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="a4992-105">Azure HDInsight Spark 클러스터에서 사용자 지정 스크립트 tooinstall Microsoft Cognitive 도구 키트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="a4992-106">Jupyter 노트북 toohello Spark 클러스터 toosee을 어떻게 업로드는 숙련 된 Microsoft Cognitive 도구 키트 학습 hello를 사용 하 여 Azure Blob 저장소 계정에 모델 toofiles 심층 tooapply [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="a4992-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4992-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a4992-107">Prerequisites</span></span>

* <span data-ttu-id="a4992-108">**Azure 구독** -</span><span class="sxs-lookup"><span data-stu-id="a4992-108">**An Azure subscription**.</span></span> <span data-ttu-id="a4992-109">이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="a4992-110">[지금 무료 Azure 계정 만들기](https://azure.microsoft.com/free)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4992-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="a4992-111">**Azure HDInsight Spark 클러스터** -</span><span class="sxs-lookup"><span data-stu-id="a4992-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="a4992-112">이 문서에서는 Spark 2.0 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="a4992-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4992-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="a4992-114">이 솔루션을 전달하는 방법</span><span class="sxs-lookup"><span data-stu-id="a4992-114">How does this solution flow?</span></span>

<span data-ttu-id="a4992-115">이 솔루션은 이 문서와 이 자습서의 일부로 업로드하는 Jupyter 노트북으로 분할되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="a4992-116">이 문서의 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="a4992-117">Tooinstall Microsoft Cognitive Toolkit 및 Python 패키지 HDInsight Spark 클러스터에서 스크립트 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="a4992-118">Hello 솔루션 toohello HDInsight Spark 클러스터를 실행 하는 hello Jupyter 노트북을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="a4992-119">hello 다음 나머지 단계에에서 설명 되어 hello Jupyter 노트북 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="a4992-120">Spark RDD(Resilient Distributed Dataset)에 샘플 이미지 로드</span><span class="sxs-lookup"><span data-stu-id="a4992-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="a4992-121">모듈 로드 및 사전 설정 정의</span><span class="sxs-lookup"><span data-stu-id="a4992-121">Load modules and define presets</span></span>
   - <span data-ttu-id="a4992-122">Hello Spark 클러스터에서 로컬로 hello 데이터 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="a4992-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="a4992-123">RDD hello 데이터 집합 변환</span><span class="sxs-lookup"><span data-stu-id="a4992-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="a4992-124">그러면 Cognitive 도구 키트를 사용 하 여 hello 이미지 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="a4992-125">학습 hello Cognitive Toolkit 모델 toohello Spark 클러스터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="a4992-126">작업자 노드에서 사용 하는 함수 toobe 정의</span><span class="sxs-lookup"><span data-stu-id="a4992-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="a4992-127">작업자 노드 점수 hello 이미지</span><span class="sxs-lookup"><span data-stu-id="a4992-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="a4992-128">모델 정확도 평가</span><span class="sxs-lookup"><span data-stu-id="a4992-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="a4992-129">Microsoft Cognitive 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="a4992-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="a4992-130">스크립트 동작을 사용하여 Spark 클러스터에 Microsoft Cognitive 도구 키트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="a4992-131">기본적으로 사용할 수 없는 hello 클러스터에서 사용자 지정 스크립트 tooinstall 구성 요소를 사용 하는 스크립트 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="a4992-132">HDInsight.NET SDK를 사용 하 여 또는 Azure PowerShell을 사용 하 여 hello hello Azure 포털에서에서 사용자 지정 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="a4992-133">또한 hello 스크립트 tooinstall hello 도구 키트를 hello 클러스터가 실행 되 고 후 또는 클러스터 만들기의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="a4992-134">이 문서에서는 hello 클러스터를 만든 후 hello 포털 tooinstall hello 도구 키트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="a4992-135">다른 방법으로 toorun hello 사용자 지정 스크립트를 참조 하십시오. [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="a4992-136">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a4992-136">Using hello Azure Portal</span></span>

<span data-ttu-id="a4992-137">Toouse hello Azure 포털 toorun 작업을 스크립팅 하는 방법에 지침은 [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="a4992-138">다음 입력 tooinstall Microsoft Cognitive Toolkit hello를 제공 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="a4992-139">스크립트 작업 이름이 hello에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="a4992-140">**Bash 스크립트 URI**의 경우 `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="a4992-141">헤드 노드와 작업자 노드 hello에 대해서만 hello 스크립트를 실행 하 고 다른 확인란의 선택 모든 hello 선택을 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="a4992-142">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="a4992-143">Hello Jupyter 노트북 tooAzure HDInsight Spark 클러스터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="a4992-144">toouse hello Microsoft Cognitive Toolkit hello Azure HDInsight Spark 클러스터와 hello Jupyter 노트북을 로드 해야 **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="a4992-145">이 노트북은 GitHub의 [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="a4992-146">복제 hello GitHub 리포지토리 [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="a4992-147">지침 tooclone 참조 [리포지토리 복제](https://help.github.com/articles/cloning-a-repository/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="a4992-148">Hello Azure 포털에서에서 이미 클릭 클라우드를 프로 비전 하는 hello Spark 클러스터 블레이드를 여세요 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="a4992-149">Toohello URL을 이동 하 여 hello Jupyter 노트북을 시작할 수도 있습니다 `https://<clustername>.azurehdinsight.net/jupyter/`합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="a4992-150">대체 \<clustername > HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="a4992-151">Hello Jupyter 노트북에서 클릭 **업로드** 에 오른쪽 위 모퉁이 hello 이동한 후 toohello 위치 hello GitHub 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="a4992-152">![Jupyter 노트북 tooAzure HDInsight Spark 클러스터 업로드](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "업로드 Jupyter 노트북 tooAzure HDInsight Spark 클러스터")</span><span class="sxs-lookup"><span data-stu-id="a4992-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="a4992-153">**업로드**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="a4992-154">Hello 노트북을 업로드 한 후 hello 전자 필기장의 hello 이름을 클릭 한 다음 tooload 데이터 집합을 hello 하 고 hello 자습서를 수행 하는 방법에 자체 hello 전자 필기장의 hello 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="a4992-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a4992-155">See also</span></span>
* [<span data-ttu-id="a4992-156">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="a4992-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a4992-157">시나리오</span><span class="sxs-lookup"><span data-stu-id="a4992-157">Scenarios</span></span>
* [<span data-ttu-id="a4992-158">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="a4992-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a4992-159">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="a4992-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a4992-160">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="a4992-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a4992-161">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="a4992-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a4992-162">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="a4992-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="a4992-163">HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="a4992-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a4992-164">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="a4992-164">Create and run applications</span></span>
* [<span data-ttu-id="a4992-165">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a4992-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a4992-166">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a4992-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a4992-167">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="a4992-167">Tools and extensions</span></span>
* [<span data-ttu-id="a4992-168">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="a4992-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a4992-169">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="a4992-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a4992-170">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="a4992-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a4992-171">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="a4992-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a4992-172">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="a4992-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a4992-173">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a4992-174">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="a4992-174">Manage resources</span></span>
* [<span data-ttu-id="a4992-175">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4992-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a4992-176">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="a4992-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
