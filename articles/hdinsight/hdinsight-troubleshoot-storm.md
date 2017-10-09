---
title: "Azure HDInsight를 사용 하 여 스톰 aaaTroubleshoot | Microsoft Docs"
description: "Apache Storm Azure HDInsight 사용에 대 한 toocommon 질문을 답변을 가져옵니다."
keywords: "Azure HDInsight, Storm, FAQ, 문제 해결 가이드, 일반적인 문제"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="6b1e6-104">Azure HDInsight를 사용한 Storm 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6b1e6-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="6b1e6-105">Hello 주요 문제 및 해결 방법은 Apache Ambari에 Apache Storm 페이로드를 사용 하기 위한 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="6b1e6-106">Hello 스톰 UI 클러스터에 액세스 하려면 어떻게 해야 합니까</span><span class="sxs-lookup"><span data-stu-id="6b1e6-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="6b1e6-107">브라우저에서 hello 스톰 UI에 액세스 하기 위한 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="6b1e6-108">Ambari UI</span><span class="sxs-lookup"><span data-stu-id="6b1e6-108">Ambari UI</span></span>
1. <span data-ttu-id="6b1e6-109">Toohello Ambari 대시보드를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="6b1e6-110">Hello 서비스 목록에서 선택 **스톰**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="6b1e6-111">Hello에 **빠른 링크** 메뉴 선택 **스톰 UI**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="6b1e6-112">직접 링크</span><span class="sxs-lookup"><span data-stu-id="6b1e6-112">Direct link</span></span>
<span data-ttu-id="6b1e6-113">Hello 스톰 UI hello url에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="6b1e6-114">https://\<클러스터 DNS 이름\>/stormui</span><span class="sxs-lookup"><span data-stu-id="6b1e6-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="6b1e6-115">예제:</span><span class="sxs-lookup"><span data-stu-id="6b1e6-115">Example:</span></span>

 <span data-ttu-id="6b1e6-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="6b1e6-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="6b1e6-117">한 토폴로지 tooanother에서 스톰 이벤트 허브 배출구 검사점 정보를 전달 하려면 어떻게 합니까</span><span class="sxs-lookup"><span data-stu-id="6b1e6-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="6b1e6-118">HDInsight Storm 이벤트 허브 배출구.jar 파일 hello를 사용 하 여 Azure 이벤트 허브에서 읽어야 하는 토폴로지를 개발 하는 경우 새 클러스터에서 이름과 같은 이름을 hello 있는 토폴로지를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="6b1e6-119">그러나 hello 이전 클러스터에서 커밋된 tooApache 사육 있던 hello 검사점 데이터를 보유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="6b1e6-120">검사점 데이터 저장 위치</span><span class="sxs-lookup"><span data-stu-id="6b1e6-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="6b1e6-121">오프셋에 대 한 검사점 데이터는 두 개의 루트 경로에 hello 이벤트 허브 배출구 사육에 의해 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="6b1e6-122">비트랜잭션 Spout 검사점 데이터는 /eventhubspout에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="6b1e6-123">트랜잭션 Spout 검사점 데이터는 /transactional에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="6b1e6-124">어떻게 toorestore</span><span class="sxs-lookup"><span data-stu-id="6b1e6-124">How toorestore</span></span>
<span data-ttu-id="6b1e6-125">tooget hello 스크립트 및 tooexport 테이블 사육에서 데이터를 사용 하 고 다음 hello 백 tooZooKeeper 새 이름으로 데이터를 가져올 라이브러리 참조 [HDInsight 스톰 예제](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="6b1e6-126">lib 폴더 안에 hello hello 내보내기/가져오기 작업에 대 한 hello 구현을 포함 하는.jar 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="6b1e6-127">hello bash 폴더 tooexport 데이터로 hello 이전 클러스터에서 사육 서버 hello 하는 방법을 보여 주는 예제 스크립트 개이고 백 toohello 사육 서버 hello 새 클러스터에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="6b1e6-128">Hello 실행 [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello 사육 노드 tooexport에서 스크립트를 다음 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="6b1e6-129">Hello 스크립트 toohello 올바른 Hortonworks Data Platform (HDP) 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="6b1e6-130">(이러한 스크립트를 HDInsight에서 제네릭으로 만들기 위해 작업 중입니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="6b1e6-131">일반 스크립트 모든 노드에서 클러스터에서 실행할 수 hello hello 사용자가 수정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="6b1e6-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="6b1e6-132">hello 내보내기 명령을 hello 메타 데이터 tooan Apache Hadoop 분산 파일 시스템 (HDFS) 경로 (Azure Blob 저장소 또는 Azure 데이터 레이크 저장소 저장소) 설정 하는 위치에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="6b1e6-133">예</span><span class="sxs-lookup"><span data-stu-id="6b1e6-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="6b1e6-134">오프셋 메타데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="6b1e6-134">Export offset metadata</span></span>
1. <span data-ttu-id="6b1e6-135">어떤 hello 검사점에서 오프셋 필요한 내보낸 toobe hello 클러스터에서 SSH toogo toohello 사육 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="6b1e6-136">실행된 hello 다음 명령은 (hello HDP 버전 문자열을 업데이트 하는 경우) 한 후 tooexport 사육 오프셋 데이터 toohello /stormmetadta/zkdata HDFS 경로:</span><span class="sxs-lookup"><span data-stu-id="6b1e6-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="6b1e6-137">오프셋 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b1e6-137">Import offset metadata</span></span>
1. <span data-ttu-id="6b1e6-138">어떤 hello 검사점에서 오프셋 필요한 내보낸 toobe hello 클러스터에서 SSH toogo toohello 사육 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="6b1e6-139">실행 hello 다음 (hello HDP 버전 문자열을 업데이트 하는 경우) 한 후 명령을 tooimport 사육 hello HDFS 경로/stormmetadata/zkdata toohello 사육 서버 hello 대상 클러스터에서의 데이터 오프셋:</span><span class="sxs-lookup"><span data-stu-id="6b1e6-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="6b1e6-140">타임 스탬프에서 해당 hello 사용자가 선택 하거나 토폴로지 hello 처음부터 데이터 처리를 시작할 수 있도록 오프셋된 메타 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="6b1e6-141">어떤 hello 검사점에서 오프셋 필요한 내보낸 toobe hello 클러스터에서 SSH toogo toohello 사육 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="6b1e6-142">실행 hello 다음 명령을 (hello HDP 버전 문자열을 업데이트 하는 경우) 한 후 모든 toodelete 사육 hello 현재 클러스터의 데이터 오프셋:</span><span class="sxs-lookup"><span data-stu-id="6b1e6-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="6b1e6-143">클러스터에서 Storm 이진 파일을 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="6b1e6-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="6b1e6-144">현재 HDP 스택 hello에 대 한 스톰 이진 /usr/hdp/current/storm-client에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="6b1e6-145">hello 위치는 헤드 노드 및 작업자 노드에 대 한 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="6b1e6-146">/usr/hdp에 특정 HDP 버전에 대한 이진 파일이 여러 개 있을 수 있습니다(예: /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="6b1e6-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="6b1e6-147">hello /usr/hdp/current/storm-client 폴더는 hello 클러스터에서 실행 되는 symlinked toohello 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="6b1e6-148">자세한 내용은 참조 [SSH를 사용 하 여 연결 tooan HDInsight 클러스터](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) 및 [스톰](http://storm.apache.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="6b1e6-149">Storm 클러스터의 hello 배포 토폴로지를 확인 하려면 어떻게 해야 합니까</span><span class="sxs-lookup"><span data-stu-id="6b1e6-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="6b1e6-150">먼저 HDInsight Storm과 함께 설치된 모든 구성 요소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="6b1e6-151">Storm 클러스터는 다음 4가지 노드 범주로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="6b1e6-152">게이트웨이 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-152">Gateway nodes</span></span>
* <span data-ttu-id="6b1e6-153">헤드 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-153">Head nodes</span></span>
* <span data-ttu-id="6b1e6-154">ZooKeeper 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="6b1e6-155">작업자 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="6b1e6-156">게이트웨이 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-156">Gateway nodes</span></span>
<span data-ttu-id="6b1e6-157">게이트웨이 노드는 게이트웨이 및 역방향 프록시 서비스 공용 액세스 tooan active Ambari 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="6b1e6-158">이 노드는 Ambari 리더 투표도 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="6b1e6-159">헤드 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-159">Head nodes</span></span>
<span data-ttu-id="6b1e6-160">Storm 헤드 노드 서비스를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="6b1e6-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="6b1e6-161">Nimbus</span></span>
* <span data-ttu-id="6b1e6-162">Ambari 서버</span><span class="sxs-lookup"><span data-stu-id="6b1e6-162">Ambari server</span></span>
* <span data-ttu-id="6b1e6-163">Ambari 메트릭 서버</span><span class="sxs-lookup"><span data-stu-id="6b1e6-163">Ambari Metrics server</span></span>
* <span data-ttu-id="6b1e6-164">Ambari 메트릭 수집기</span><span class="sxs-lookup"><span data-stu-id="6b1e6-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="6b1e6-165">ZooKeeper 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-165">ZooKeeper nodes</span></span>
<span data-ttu-id="6b1e6-166">HDInsight는 3 노드 ZooKeeper 쿼럼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="6b1e6-167">hello 쿼럼 크기가 고정 되며 다시 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="6b1e6-168">Hello 클러스터의 storm 서비스 구성된 tooautomatically 사용 하 여 hello 사육 쿼럼 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="6b1e6-169">작업자 노드</span><span class="sxs-lookup"><span data-stu-id="6b1e6-169">Worker nodes</span></span>
<span data-ttu-id="6b1e6-170">Storm 작업자 노드 hello 다음 서비스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="6b1e6-171">감독자</span><span class="sxs-lookup"><span data-stu-id="6b1e6-171">Supervisor</span></span>
* <span data-ttu-id="6b1e6-172">토폴로지를 실행하기 위한 작업자 JVM(Java Virtual Machines)</span><span class="sxs-lookup"><span data-stu-id="6b1e6-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="6b1e6-173">Ambari 에이전트</span><span class="sxs-lookup"><span data-stu-id="6b1e6-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="6b1e6-174">개발용 Storm 이벤트 허브 spout 이진을 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="6b1e6-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="6b1e6-175">스톰 이벤트 허브 배출구.jar 파일 토폴로지에을 사용 하는 방법에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="6b1e6-176">Java 기반 토폴로지</span><span class="sxs-lookup"><span data-stu-id="6b1e6-176">Java-based topology</span></span>
[<span data-ttu-id="6b1e6-177">HDInsight의 Storm으로 Azure Event Hubs에서 이벤트 처리(Java)</span><span class="sxs-lookup"><span data-stu-id="6b1e6-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="6b1e6-178">C# 기반 토폴로지(HDInsight 3.4 이상 Linux Storm 클러스터의 Mono)</span><span class="sxs-lookup"><span data-stu-id="6b1e6-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="6b1e6-179">HDInsight의 Storm(C#)에서 Azure Event Hubs의 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="6b1e6-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="6b1e6-180">HDInsight 3.5 이상의 Linux Storm 클러스터에 대한 최신 Storm 이벤트 허브 Spout 이진 파일</span><span class="sxs-lookup"><span data-stu-id="6b1e6-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="6b1e6-181">toolearn toouse hello 최신 스톰 이벤트 허브 배출구 HDInsight 3.5 +를 사용 하는 Linux Storm 클러스터 참조 hello mvn repo [추가 정보 파일](https://github.com/hdinsight/mvn-repo/blob/master/README.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="6b1e6-182">소스 코드 예제</span><span class="sxs-lookup"><span data-stu-id="6b1e6-182">Source code examples</span></span>
<span data-ttu-id="6b1e6-183">참조 [예제](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) 방법의 tooread (Java로 작성 된) 하는 Apache Storm 토폴로지를 사용 하 여 Azure HDInsight 클러스터에서 Azure 이벤트 허브에서 작성 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="6b1e6-184">클러스터에서 Storm Log4J 구성 파일을 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="6b1e6-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="6b1e6-185">tooidentify Log4J Apache Storm 서비스에 대 한 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="6b1e6-186">헤드 노드에서</span><span class="sxs-lookup"><span data-stu-id="6b1e6-186">On head nodes</span></span>
<span data-ttu-id="6b1e6-187">hello Nimbus Log4J 구성을 /usr/hdp/에서 읽을\<HDP 버전\>/storm/log4j2/cluster.xml 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="6b1e6-188">작업자 노드에서</span><span class="sxs-lookup"><span data-stu-id="6b1e6-188">On worker nodes</span></span>
<span data-ttu-id="6b1e6-189">hello 감독자 Log4J 구성을 /usr/hdp/에서 읽을\<HDP 버전\>/storm/log4j2/cluster.xml 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="6b1e6-190">hello 작업자 Log4J 구성 파일에서 /usr/hdp/읽은\<HDP 버전\>/storm/log4j2/worker.xml 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b1e6-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="6b1e6-191">예제: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="6b1e6-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

