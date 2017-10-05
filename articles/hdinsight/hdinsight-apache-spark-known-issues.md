---
title: "Azure HDInsight에서 Apache Spark 클러스터 관련 문제 해결 | Microsoft Docs"
description: "Azure HDInsight의 Apache Spark 클러스터 관련 문제 및 이를 해결하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="97f4c-103">HDInsight의 Apache Spark 클러스터에 대한 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="97f4c-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="97f4c-104">이 문서는 HDInsight Spark 공개 미리 보기에 대한 모든 알려진 문제를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="97f4c-105">Livy 누수 대화형 세션</span><span class="sxs-lookup"><span data-stu-id="97f4c-105">Livy leaks interactive session</span></span>
<span data-ttu-id="97f4c-106">Livy가 여전히 활성 상태인 대화형 세션으로 재시작하는 경우(Ambari에서 또는 헤드 노드 0 가상 컴퓨터 재부팅으로 인해) 대화형 작업 세션이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="97f4c-107">이로 인해 새 작업은 수락된 상태에 멈출 수 있으며 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="97f4c-108">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-108">**Mitigation:**</span></span>

<span data-ttu-id="97f4c-109">다음 절차에 따라 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="97f4c-110">헤드 노드로 ssh합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-110">Ssh into headnode.</span></span> <span data-ttu-id="97f4c-111">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97f4c-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="97f4c-112">다음 명령을 실행하여 Livy를 통해 시작한 대화형 작업의 응용 프로그램 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="97f4c-113">작업이 명시적 이름이 지정되지 않은 Livy 대화형 세션으로 시작된 경우 기본 작업 이름은 Livy가 되며 Jupyter 노트북으로 시작된 Livy 세션의 경우 작업 이름은 remotesparkmagics_*로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="97f4c-114">다음 명령을 실행하여 해당 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="97f4c-115">새 작업 실행이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="97f4c-116">Spark 기록 서버가 시작되지 않음</span><span class="sxs-lookup"><span data-stu-id="97f4c-116">Spark History Server not started</span></span>
<span data-ttu-id="97f4c-117">클러스터가 만들어진 후 Spark 기록 서버가 자동으로 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="97f4c-118">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-118">**Mitigation:**</span></span> 

<span data-ttu-id="97f4c-119">Ambari에서 기록 서버를 수동으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="97f4c-120">Spark 로그 디렉터리에 대한 사용 권한 문제</span><span class="sxs-lookup"><span data-stu-id="97f4c-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="97f4c-121">hdiuser가 spark-제출로 작업을 제출하는 경우 오류 java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log(사용 권한 거부됨)가 있고 드라이버 로그가 작성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="97f4c-122">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-122">**Mitigation:**</span></span>

1. <span data-ttu-id="97f4c-123">hdiuser를 Hadoop 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="97f4c-124">클러스터를 만든 후에 /var/log/spark에 777 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="97f4c-125">Ambari를 사용하여 777 권한으로 디렉터리가 되도록 spark 로그 위치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="97f4c-126">sudo로 spark-제출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="97f4c-127">Spark-Phoenix 커넥터가 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="97f4c-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="97f4c-128">현재 Spark-Phoenix 커넥터는 HDInsight Spark 클러스터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="97f4c-129">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-129">**Mitigation:**</span></span>

<span data-ttu-id="97f4c-130">대신 Spark-HBase 커넥터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="97f4c-131">자세한 내용은 [Spark-HBase 커넥터 사용 방법](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97f4c-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="97f4c-132">Jupyter Notebook 관련 문제</span><span class="sxs-lookup"><span data-stu-id="97f4c-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="97f4c-133">다음은 Jupyter Notebook과 관련된 몇 가지 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="97f4c-134">파일 이름에 ASCII가 아닌 문자가 있는 Notebook</span><span class="sxs-lookup"><span data-stu-id="97f4c-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="97f4c-135">Spark HDInsight 클러스터에서 사용할 수 있는 Jupyter Notebook은 파일 이름에 ASCII가 아닌 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="97f4c-136">ASCII가 아닌 파일 이름을 가진 파일을 Jupyter UI를 통해 업로드하려고 하면 자동으로 실패합니다. 즉, Jupyter에서 파일을 업로드할 수 없지만 시각적 오류도 throw되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="97f4c-137">더 큰 Notebook을 로드하는 중 오류</span><span class="sxs-lookup"><span data-stu-id="97f4c-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="97f4c-138">더 큰 Notebook을 로드할 때 **`Error loading notebook`** 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="97f4c-139">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-139">**Mitigation:**</span></span>

<span data-ttu-id="97f4c-140">이 오류가 발생했다고 해서 데이터가 손상되거나 손실된 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="97f4c-141">Notebook은 여전히 `/var/lib/jupyter`의 디스크에 있으며 클러스터에 대한 SSH를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="97f4c-142">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97f4c-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="97f4c-143">SSH를 사용하여 클러스터에 연결한 경우 Notebook을 사용자의 클러스터에서 로컬 컴퓨터에(SCP 또는 WinSCP를 사용하여) 백업으로 복사하여 Notebook의 중요 데이터 손실을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="97f4c-144">그런 다음 포트 8001의 헤드 노드에 대한 SSH 터널을 통해 게이트웨이를 거치지 않고 Jupyter에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="97f4c-145">여기에서 노트북의 출력을 지우고 다시 저장하여 노트북의 크기를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="97f4c-146">나중에 이 오류가 발생하지 않도록 하려면 몇 가지 모범 사례를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="97f4c-147">노트북 크기를 작게 유지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="97f4c-148">Jupyter에 다시 전송된 Spark 작업의 출력은 노트북에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="97f4c-149">RDD의 데이터 프레임에서 `.collect()`를 실행하지 못하도록 하는 것이 Jupyter의 모범 사례입니다. 그 대신 RDD의 콘텐츠를 살펴보려면 출력이 너무 커지지 않도록 `.take()` 또는 `.sample()`의 실행을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="97f4c-150">또한 노트북을 저장할 때 모든 출력을 지워서 크기를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="97f4c-151">노트북 초기 시작이 예상보다 오래 걸리는 경우</span><span class="sxs-lookup"><span data-stu-id="97f4c-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="97f4c-152">Jupyter Notebook에서 Spark 매직을 사용한 첫 번째 코드 문의 경우 1분 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="97f4c-153">**설명:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-153">**Explanation:**</span></span>

<span data-ttu-id="97f4c-154">이는 첫 번째 코드 셀이 실행될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="97f4c-155">백그라운드에서 세션 구성이 시작되고 Spark, SQL 및 Hive 컨텍스트가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="97f4c-156">이러한 컨텍스트가 설정된 후 첫 번째 문이 실행되므로 문이 완료되는 데 시간이 오래 걸린 것 같은 느낌이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="97f4c-157">세션 만들기에서 Jupyter 노트북 시간 제한</span><span class="sxs-lookup"><span data-stu-id="97f4c-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="97f4c-158">Spark 클러스터에 리소스가 부족할 때 Jupyter 노트북에서 Spark 및 Pyspark 커널은 세션을 만들려고 할 때 시간 초과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="97f4c-159">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="97f4c-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="97f4c-160">다음과 같은 방법으로 Spark 클러스터의 리소스를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="97f4c-161">Close and Halt 메뉴로 이동하거나 노트북 탐색기에서 종료를 클릭하여 다른 Spark 노트북을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="97f4c-162">YARN에서 다른 Spark 응용 프로그램을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="97f4c-163">시작하려는 노트북을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="97f4c-164">이제 세션을 만들기 위한 충분한 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f4c-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="97f4c-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="97f4c-165">See also</span></span>
* [<span data-ttu-id="97f4c-166">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="97f4c-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="97f4c-167">시나리오</span><span class="sxs-lookup"><span data-stu-id="97f4c-167">Scenarios</span></span>
* [<span data-ttu-id="97f4c-168">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="97f4c-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="97f4c-169">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="97f4c-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="97f4c-170">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="97f4c-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="97f4c-171">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="97f4c-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="97f4c-172">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="97f4c-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="97f4c-173">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="97f4c-173">Create and run applications</span></span>
* [<span data-ttu-id="97f4c-174">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="97f4c-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="97f4c-175">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="97f4c-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="97f4c-176">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="97f4c-176">Tools and extensions</span></span>
* [<span data-ttu-id="97f4c-177">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="97f4c-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="97f4c-178">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="97f4c-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="97f4c-179">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="97f4c-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="97f4c-180">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="97f4c-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="97f4c-181">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="97f4c-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="97f4c-182">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="97f4c-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="97f4c-183">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="97f4c-183">Manage resources</span></span>
* [<span data-ttu-id="97f4c-184">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="97f4c-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="97f4c-185">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="97f4c-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

