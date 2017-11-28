---
title: "Azure HDInsight의 Apache Spark와 함께 aaaTroubleshoot 문제 클러스터가 | Microsoft Docs"
description: "Azure HDInsight의 Spark 클러스터 관련된 tooApache 문제에 대 한 자세한 내용은 방법과 toowork 주위 하는 것입니다."
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
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="c0787-103">HDInsight의 Apache Spark 클러스터에 대한 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c0787-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="c0787-104">이 문서는의 알려진 문제 hello HDInsight Spark 공개 미리 보기에 대 한 모든 hello 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="c0787-105">Livy 누수 대화형 세션</span><span class="sxs-lookup"><span data-stu-id="c0787-105">Livy leaks interactive session</span></span>
<span data-ttu-id="c0787-106">리비 시작 될 때 (Ambari 또는 tooheadnode 0 가상 컴퓨터를 다시 부팅 때문) 여전히 활성 대화형 세션으로 대화형 작업 세션 누출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="c0787-107">이 때문에 새로운 작업 있습니다 hello 수락 됨 상태에서에서 멈출 하 고 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="c0787-108">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c0787-108">**Mitigation:**</span></span>

<span data-ttu-id="c0787-109">다음 프로시저 tooworkaround hello 문제 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="c0787-110">헤드 노드로 ssh합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-110">Ssh into headnode.</span></span> <span data-ttu-id="c0787-111">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0787-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c0787-112">다음 명령은 toofind hello 응용 프로그램 실행된 hello hello 대화형 작업의 Id 리비를 통해 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="c0787-113">hello 기본 작업 이름은 됩니다 리비 hello 작업 hello에 대 한 지정 된 이름이 없으면 명시적 리비 대화형 세션으로 시작 된 경우 Jupyter 노트북에 의해 시작 리비 세션 hello 작업 이름은 remotesparkmagics_ *로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="c0787-114">다음 명령은 tookill hello 이러한 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="c0787-115">새 작업 실행이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="c0787-116">Spark 기록 서버가 시작되지 않음</span><span class="sxs-lookup"><span data-stu-id="c0787-116">Spark History Server not started</span></span>
<span data-ttu-id="c0787-117">클러스터가 만들어진 후 Spark 기록 서버가 자동으로 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="c0787-118">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c0787-118">**Mitigation:**</span></span> 

<span data-ttu-id="c0787-119">Ambari에서 hello 기록 서버를 수동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="c0787-120">Spark 로그 디렉터리에 대한 사용 권한 문제</span><span class="sxs-lookup"><span data-stu-id="c0787-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="c0787-121">Hdiuser가 spark-submit 인 작업을 제출 하는 경우 오류 java.io.FileNotFoundException 있습니다: /var/log/spark/sparkdriver_hdiuser.log (사용 권한이 거부 되었습니다) 및 hello 드라이버 로그 기록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="c0787-122">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c0787-122">**Mitigation:**</span></span>

1. <span data-ttu-id="c0787-123">Hdiuser toohello Hadoop 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="c0787-124">클러스터를 만든 후에 /var/log/spark에 777 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="c0787-125">Ambari toobe 디렉터리 777 사용 권한과 함께 사용 하는 hello spark 로그 위치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="c0787-126">sudo로 spark-제출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="c0787-127">Spark-Phoenix 커넥터가 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="c0787-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="c0787-128">현재 hello 피닉스 Spark 커넥터 HDInsight Spark 클러스터와 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="c0787-129">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c0787-129">**Mitigation:**</span></span>

<span data-ttu-id="c0787-130">Hello HBase Spark 커넥터를 대신 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="c0787-131">에 대 한 참조 [어떻게 toouse HBase Spark 커넥터](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="c0787-132">TooJupyter 전자 필기장 관련 된 문제</span><span class="sxs-lookup"><span data-stu-id="c0787-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="c0787-133">다음은 몇 가지 알려진된 문제 관련된 tooJupyter 전자 필기장입니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="c0787-134">파일 이름에 ASCII가 아닌 문자가 있는 Notebook</span><span class="sxs-lookup"><span data-stu-id="c0787-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="c0787-135">Spark HDInsight 클러스터에서 사용할 수 있는 Jupyter Notebook은 파일 이름에 ASCII가 아닌 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="c0787-136">자동으로 실패 합니다 tooupload hello ASCII가 아닌 파일 이름 Jupyter UI를 통해 파일을 시도 하는 경우 (즉, Jupyter hello 파일을 업로드 하면 수 없을 하지만 하거나 표시 되는 오류를 발생 하지 않습니다 것).</span><span class="sxs-lookup"><span data-stu-id="c0787-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="c0787-137">더 큰 Notebook을 로드하는 중 오류</span><span class="sxs-lookup"><span data-stu-id="c0787-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="c0787-138">더 큰 Notebook을 로드할 때 **`Error loading notebook`** 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="c0787-139">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c0787-139">**Mitigation:**</span></span>

<span data-ttu-id="c0787-140">이 오류가 발생했다고 해서 데이터가 손상되거나 손실된 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="c0787-141">전자 필기장은 여전히 디스크에서 `/var/lib/jupyter`, hello 클러스터 tooaccess에 SSH를 사용 하면 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="c0787-142">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0787-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="c0787-143">SSH를 사용 하 여 toohello 클러스터를 연결 하 고 나면 hello 전자 필기장의 중요 한 데이터 백업 tooprevent hello 손실로 전자 필기장 (SCP 또는 WinSCP 사용) 하 여 클러스터 tooyour 로컬 컴퓨터에서 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="c0787-144">그런 다음 SSH 터널 포트 8001 tooaccess Jupyter에서 프로그램 헤드 노드에 hello 게이트웨이 통과 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="c0787-145">여기에서 있습니다 수 전자 필기장의 hello 출력 지우고 다시 저장 toominimize hello 노트북의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="c0787-146">tooprevent이이 오류 이후 몇 가지 모범 사례를 수행 해야 하는 hello에 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="c0787-147">중요 한 tookeep hello 노트북 크기가 작은 경우</span><span class="sxs-lookup"><span data-stu-id="c0787-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="c0787-148">다시 전송 되기 tooJupyter hello 노트북에서 유지 되는 Spark 작업에서 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="c0787-149">Jupyter에 대 한 모범 사례를 실행 하는 일반 tooavoid 중인 `.collect()` on 큰 RDD 또는 데이터 프레임; RDD의 내용을 toopeek 하려는 경우를 고려해 야 실행 `.take()` 또는 `.sample()` 출력이 너무 커서 함을 알 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="c0787-150">또한, 노트북을 저장할 때 선택을 취소 모든 출력을 셀 tooreduce hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="c0787-151">노트북 초기 시작이 예상보다 오래 걸리는 경우</span><span class="sxs-lookup"><span data-stu-id="c0787-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="c0787-152">Jupyter Notebook에서 Spark 매직을 사용한 첫 번째 코드 문의 경우 1분 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="c0787-153">**설명:**</span><span class="sxs-lookup"><span data-stu-id="c0787-153">**Explanation:**</span></span>

<span data-ttu-id="c0787-154">이 첫 번째 코드 셀 hello를 실행할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="c0787-155">Hello 백그라운드에서이 세션 구성 및 Spark, SQL를 시작 하 고 하이브 컨텍스트가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="c0787-156">이러한 컨텍스트를 설정한 후 hello 첫 번째 문을 실행 하 고 hello 인상을 hello 문을 걸린 시간이 오래 toocomplete를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="c0787-157">Hello 세션을 만드는 Jupyter 노트북 시간 제한</span><span class="sxs-lookup"><span data-stu-id="c0787-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="c0787-158">Spark 클러스터 리소스가 부족할 때 Spark hello 및 hello Jupyter 노트북에 Pyspark 커널 toocreate hello 세션 중 시간이 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="c0787-159">**해결 방법:**</span><span class="sxs-lookup"><span data-stu-id="c0787-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="c0787-160">다음과 같은 방법으로 Spark 클러스터의 리소스를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="c0787-161">다른 스파크 전자 필기장 toohello 이동 닫기 및 중단 메뉴 하거나 hello 노트북 탐색기에서 시스템 종료를 클릭 하 여를 중지 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="c0787-162">YARN에서 다른 Spark 응용 프로그램을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="c0787-163">Hello 노트북을 toostart 하려던 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="c0787-164">충분 한 리소스는 세션을 지금 toocreate 있습니다 사용할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0787-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c0787-165">See also</span></span>
* [<span data-ttu-id="c0787-166">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c0787-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c0787-167">시나리오</span><span class="sxs-lookup"><span data-stu-id="c0787-167">Scenarios</span></span>
* [<span data-ttu-id="c0787-168">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="c0787-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c0787-169">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="c0787-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c0787-170">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="c0787-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c0787-171">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="c0787-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c0787-172">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="c0787-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c0787-173">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="c0787-173">Create and run applications</span></span>
* [<span data-ttu-id="c0787-174">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c0787-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c0787-175">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c0787-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c0787-176">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="c0787-176">Tools and extensions</span></span>
* [<span data-ttu-id="c0787-177">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출</span><span class="sxs-lookup"><span data-stu-id="c0787-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c0787-178">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="c0787-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c0787-179">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="c0787-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c0787-180">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="c0787-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c0787-181">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="c0787-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c0787-182">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c0787-183">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="c0787-183">Manage resources</span></span>
* [<span data-ttu-id="c0787-184">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0787-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c0787-185">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="c0787-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

