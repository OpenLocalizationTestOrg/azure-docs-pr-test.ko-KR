---
title: "Azure HDInsight를 사용 하 여 하이브 aaaTroubleshoot | Microsoft Docs"
description: "Apache Hive 및 Azure HDInsight 작업에 대 한 toocommon 질문을 답변을 가져옵니다."
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
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="f56ae-104">Azure HDInsight를 사용한 Hive 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f56ae-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="f56ae-105">Apache Hive 페이로드 Apache Ambari에서 작업할 때는 hello 상위 질문과 그 해결 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="f56ae-106">Hive metastore를 내보내고 다른 클러스터로 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="f56ae-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f56ae-107">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f56ae-107">Resolution steps</span></span>

1. <span data-ttu-id="f56ae-108">SSH (보안 셸) 클라이언트를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="f56ae-109">자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f56ae-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="f56ae-110">Hello tooexport hello metastore 원하는 hello HDInsight 클러스터에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="f56ae-111">이 명령은 allatables.sql이라는 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="f56ae-112">Hello 파일 alltables.sql toohello 새 HDInsight 클러스터에 복사한 다음 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="f56ae-113">hello 해결 단계에 hello 코드 hello 새 클러스터에서 경로 데이터 hello 이전 클러스터에서 hello 데이터 경로와 동일한 hello를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="f56ae-114">Hello 데이터 경로가 다른 경우 생성 된 hello alltables.sql 파일 tooreflect를 변경 내용을 수동으로 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="f56ae-115">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f56ae-115">Additional reading</span></span>

- [<span data-ttu-id="f56ae-116">SSH를 사용 하 여 tooan HDInsight 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f56ae-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="f56ae-117">클러스터에서 Hive 로그를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="f56ae-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f56ae-118">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f56ae-118">Resolution steps</span></span>

1. <span data-ttu-id="f56ae-119">SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f56ae-120">자세한 내용은 **더 보기**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f56ae-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="f56ae-121">tooview 하이브 클라이언트 로그 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="f56ae-122">tooview 하이브 metastore 로그, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="f56ae-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="f56ae-123">tooview Hiveserver 로그 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="f56ae-124">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f56ae-124">Additional reading</span></span>

- [<span data-ttu-id="f56ae-125">SSH를 사용 하 여 tooan HDInsight 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f56ae-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="f56ae-126">Hello 클러스터에서 특정 구성으로 하이브 셸을 시작 하는 어떻게 합니까</span><span class="sxs-lookup"><span data-stu-id="f56ae-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f56ae-127">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f56ae-127">Resolution steps</span></span>

1. <span data-ttu-id="f56ae-128">Hello 하이브 shell을 시작 하면 구성 키-값 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="f56ae-129">자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f56ae-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="f56ae-130">toolist 하이브 shell 사용 하 여 hello 뒤의 모든 유효한 구성 명령 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="f56ae-131">예를 들어 hello hello 콘솔에서 사용 하도록 설정 하는 디버그 로깅과 함께 toostart 하이브 명령 셸에 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="f56ae-132">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f56ae-132">Additional reading</span></span>

- <span data-ttu-id="f56ae-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)(Hive 구성 속성)</span><span class="sxs-lookup"><span data-stu-id="f56ae-133">[Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)</span></span>


## <span data-ttu-id="f56ae-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>클러스터 중요 경로에서 Tez DAG 데이터를 분석하는 방법</span><span class="sxs-lookup"><span data-stu-id="f56ae-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f56ae-135">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f56ae-135">Resolution steps</span></span>
 
1. <span data-ttu-id="f56ae-136">클러스터에 중요 한 그래프에는 Apache Tez tooanalyze 방향성 비순환 그래프 (DAG), SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f56ae-137">자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f56ae-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="f56ae-138">명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="f56ae-139">toolist Tez DAG tooanalyze를 사용 하는 일 수 있는 다른 분석기 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="f56ae-140">Hello 첫 번째 인수로 예제 프로그램을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="f56ae-141">올바른 프로그램의 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-141">Valid program names include:</span></span>
    - <span data-ttu-id="f56ae-142">**ContainerReuseAnalyzer**: DAG에 컨테이너 다시 사용 세부 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="f56ae-143">**CriticalPath**: DAG의 hello 요주의 경로 찾기</span><span class="sxs-lookup"><span data-stu-id="f56ae-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="f56ae-144">**LocalityAnalyzer**: DAG에 위치 정보를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="f56ae-145">**ShuffleTimeAnalyzer**: DAG에 hello 순서 섞기 시간 정보를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="f56ae-146">**SkewAnalyzer**: DAG에 hello 시간차 세부 정보를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="f56ae-147">**SlowNodeAnalyzer**: DAG에 노드 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="f56ae-148">**SlowTaskIdentifier**: DAG에 느린 작업 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="f56ae-149">**SlowestVertexAnalyzer**: DAG에 가장 느린 꼭지점 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="f56ae-150">**SlowNodeAnalyzer**: DAG에 분산 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="f56ae-151">**TaskConcurrencyAnalyzer**: DAG에서 hello 작업 동시성 세부 정보를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="f56ae-152">**VertexLevelCriticalPathAnalyzer**: 찾기 hello DAG에 꼭 짓 점 수준에서 중요 한 경로</span><span class="sxs-lookup"><span data-stu-id="f56ae-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="f56ae-153">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f56ae-153">Additional reading</span></span>

- [<span data-ttu-id="f56ae-154">SSH를 사용 하 여 tooan HDInsight 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f56ae-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="f56ae-155">클러스터에서 Tez DAG 데이터를 다운로드하는 방법</span><span class="sxs-lookup"><span data-stu-id="f56ae-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="f56ae-156">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="f56ae-156">Resolution steps</span></span>

<span data-ttu-id="f56ae-157">두 가지가 toocollect hello Tez DAG 데이터:</span><span class="sxs-lookup"><span data-stu-id="f56ae-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="f56ae-158">명령줄 hello:</span><span class="sxs-lookup"><span data-stu-id="f56ae-158">From hello command line:</span></span>
 
    <span data-ttu-id="f56ae-159">SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="f56ae-160">Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="f56ae-161">Hello Ambari Tez 보기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="f56ae-162">TooAmbari 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="f56ae-163">Hello hello 오른쪽 위 모퉁이에 타일 아이콘) (아래에 있는 이동 tooTez 보기.</span><span class="sxs-lookup"><span data-stu-id="f56ae-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="f56ae-164">Hello tooview 원하는 DAG를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="f56ae-165">**데이터 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f56ae-165">Select **Download data**.</span></span>

### <span data-ttu-id="f56ae-166"><a name="additional-reading-end"></a>추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f56ae-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="f56ae-167">SSH를 사용 하 여 tooan HDInsight 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f56ae-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






