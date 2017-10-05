---
title: "Azure HDInsight를 사용한 Hive 문제 해결 | Microsoft Docs"
description: "Apache Hive 및 Azure HDInsight 작업에 대한 일반적인 질문에 답합니다."
keywords: "Azure HDInsight, Hive, FAQ, 문제 해결 가이드, 일반적인 질문"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: 53e9685458190efe6a586504721b8e7baadaed60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="f6c30-104">Azure HDInsight를 사용한 Hive 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f6c30-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="f6c30-105">Apache Ambari에서 Apache Hive 페이로드를 사용할 때의 주요 질문 사항 및 해결 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-105">Learn about the top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="f6c30-106">Hive metastore를 내보내고 다른 클러스터로 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="f6c30-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f6c30-107">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f6c30-107">Resolution steps</span></span>

1. <span data-ttu-id="f6c30-108">SSH(Secure Shell) 클라이언트를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-108">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="f6c30-109">자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6c30-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="f6c30-110">metastore를 내보내려는 HDInsight 클러스터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-110">Run the following command on the HDInsight cluster from which you want to export the metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="f6c30-111">이 명령은 allatables.sql이라는 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="f6c30-112">alltables.sql 파일을 새 HDInsight 클러스터에 복사하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-112">Copy the file alltables.sql to the new HDInsight cluster, and then run the following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="f6c30-113">해결 단계의 코드는 새 클러스터의 데이터 경로가 이전 클러스터의 데이터 경로와 동일하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-113">The code in the resolution steps assumes that data paths on the new cluster are the same as the data paths on the old cluster.</span></span> <span data-ttu-id="f6c30-114">데이터 경로가 다른 경우 변경 내용을 반영하도록 생성된 alltables.sql 파일을 수동으로 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-114">If the data paths are different, you can manually edit the generated alltables.sql file to reflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="f6c30-115">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f6c30-115">Additional reading</span></span>

- [<span data-ttu-id="f6c30-116">SSH를 사용하여 HDInsight 클러스터 연결</span><span class="sxs-lookup"><span data-stu-id="f6c30-116">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="f6c30-117">클러스터에서 Hive 로그를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="f6c30-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f6c30-118">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f6c30-118">Resolution steps</span></span>

1. <span data-ttu-id="f6c30-119">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-119">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f6c30-120">자세한 내용은 **더 보기**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6c30-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="f6c30-121">Hive 클라이언트 로그를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-121">To view Hive client logs, use the following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="f6c30-122">Hive metastore 로그를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-122">To view Hive metastore logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="f6c30-123">HiveServer 로그를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-123">To view Hiveserver logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="f6c30-124">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f6c30-124">Additional reading</span></span>

- [<span data-ttu-id="f6c30-125">SSH를 사용하여 HDInsight 클러스터 연결</span><span class="sxs-lookup"><span data-stu-id="f6c30-125">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="f6c30-126">클러스터에서 특정 구성으로 Hive 셸을 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="f6c30-126">How do I launch the Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f6c30-127">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f6c30-127">Resolution steps</span></span>

1. <span data-ttu-id="f6c30-128">Hive 셸을 시작할 때 구성 키-값 쌍을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-128">Specify a configuration key-value pair when you start the Hive shell.</span></span> <span data-ttu-id="f6c30-129">자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6c30-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="f6c30-130">Hive 셸에서 모든 유효 구성을 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-130">To list all effective configurations on Hive shell, use the following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="f6c30-131">예를 들어 다음 명령을 사용하여 콘솔에서 디버그 로깅이 사용하도록 설정된 상태로 Hive 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-131">For example, use the following command to start Hive shell with debug logging enabled on the console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="f6c30-132">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f6c30-132">Additional reading</span></span>

- <span data-ttu-id="f6c30-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)(Hive 구성 속성)</span><span class="sxs-lookup"><span data-stu-id="f6c30-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)</span></span>


## <span data-ttu-id="f6c30-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>클러스터 중요 경로에서 Tez DAG 데이터를 분석하는 방법</span><span class="sxs-lookup"><span data-stu-id="f6c30-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f6c30-135">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f6c30-135">Resolution steps</span></span>
 
1. <span data-ttu-id="f6c30-136">클러스터에 중요한 그래프에서 Apache Tez DAG(방향성 비순환 그래프)를 분석하려면 SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-136">To analyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f6c30-137">자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6c30-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="f6c30-138">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-138">At a command prompt, run the following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="f6c30-139">Tez DAG를 분석하는 데 사용할 수 있는 다른 분석기를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-139">To list other analyzers that can be used to analyze Tez DAG, use the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="f6c30-140">예제 프로그램을 첫 번째 인수로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-140">You must provide an example program as the first argument.</span></span>

  <span data-ttu-id="f6c30-141">올바른 프로그램의 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-141">Valid program names include:</span></span>
    - <span data-ttu-id="f6c30-142">**ContainerReuseAnalyzer**: DAG에 컨테이너 다시 사용 세부 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="f6c30-143">**CriticalPath**: DAG의 중요한 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-143">**CriticalPath**: Find the critical path of a DAG</span></span>
    - <span data-ttu-id="f6c30-144">**LocalityAnalyzer**: DAG에 위치 정보를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="f6c30-145">**ShuffleTimeAnalyzer**: DAG에서 순서 섞기 시간 정보를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-145">**ShuffleTimeAnalyzer**: Analyze the shuffle time details in a DAG</span></span>
    - <span data-ttu-id="f6c30-146">**SkewAnalyzer**: DAG에서 기울이기 정보를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-146">**SkewAnalyzer**: Analyze the skew details in a DAG</span></span>
    - <span data-ttu-id="f6c30-147">**SlowNodeAnalyzer**: DAG에 노드 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="f6c30-148">**SlowTaskIdentifier**: DAG에 느린 작업 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="f6c30-149">**SlowestVertexAnalyzer**: DAG에 가장 느린 꼭지점 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="f6c30-150">**SlowNodeAnalyzer**: DAG에 분산 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="f6c30-151">**TaskConcurrencyAnalyzer**: DAG에 작업 동시성 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-151">**TaskConcurrencyAnalyzer**: Print the task concurrency details in a DAG</span></span>
    - <span data-ttu-id="f6c30-152">**VertexLevelCriticalPathAnalyzer**: DAG에서 꼭짓점 수준의 중요 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-152">**VertexLevelCriticalPathAnalyzer**: Find the critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="f6c30-153">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f6c30-153">Additional reading</span></span>

- [<span data-ttu-id="f6c30-154">SSH를 사용하여 HDInsight 클러스터 연결</span><span class="sxs-lookup"><span data-stu-id="f6c30-154">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="f6c30-155">클러스터에서 Tez DAG 데이터를 다운로드하는 방법</span><span class="sxs-lookup"><span data-stu-id="f6c30-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="f6c30-156">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f6c30-156">Resolution steps</span></span>

<span data-ttu-id="f6c30-157">Tez DAG 데이터를 수집하는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-157">There are two ways to collect the Tez DAG data:</span></span>

- <span data-ttu-id="f6c30-158">명령줄에서:</span><span class="sxs-lookup"><span data-stu-id="f6c30-158">From the command line:</span></span>
 
    <span data-ttu-id="f6c30-159">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-159">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f6c30-160">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-160">At the command prompt, run the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="f6c30-161">Ambari Tez 보기 사용:</span><span class="sxs-lookup"><span data-stu-id="f6c30-161">Use the Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="f6c30-162">Ambari로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-162">Go to Ambari.</span></span> 
  2. <span data-ttu-id="f6c30-163">오른쪽 위 구석의 타일 아이콘 아래에 있는 Tez 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-163">Go to Tez view (under the tiles icon in the upper-right corner).</span></span> 
  3. <span data-ttu-id="f6c30-164">보려는 DAG를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-164">Select the DAG you want to view.</span></span>
  4. <span data-ttu-id="f6c30-165">**데이터 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c30-165">Select **Download data**.</span></span>

### <span data-ttu-id="f6c30-166"><a name="additional-reading-end"></a>추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f6c30-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="f6c30-167">SSH를 사용하여 HDInsight 클러스터 연결</span><span class="sxs-lookup"><span data-stu-id="f6c30-167">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






