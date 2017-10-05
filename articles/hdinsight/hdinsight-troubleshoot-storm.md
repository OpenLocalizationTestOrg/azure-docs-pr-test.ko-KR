---
title: "Azure HDInsight를 사용한 Storm 문제 해결 | Microsoft Docs"
description: "Azure HDInsight에서 Apache Storm을 사용할 때 제기되는 일반적인 질문에 답합니다."
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
ms.openlocfilehash: 70a3d762431d90acdd6ed2a432a569f34d0ce447
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="79522-104">Azure HDInsight를 사용한 Storm 문제 해결</span><span class="sxs-lookup"><span data-stu-id="79522-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="79522-105">Apache Ambari에서 Apache Storm 페이로드를 사용할 때의 주요 문제 및 해결 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="79522-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a><span data-ttu-id="79522-106">클러스터에서 Storm UI에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-106">How do I access the Storm UI on a cluster</span></span>
<span data-ttu-id="79522-107">브라우저에서 Storm UI에 액세스할 때는 다음 두 가지 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-107">You have two options for accessing the Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="79522-108">Ambari UI</span><span class="sxs-lookup"><span data-stu-id="79522-108">Ambari UI</span></span>
1. <span data-ttu-id="79522-109">Ambari 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-109">Go to the Ambari dashboard.</span></span>
2. <span data-ttu-id="79522-110">서비스 목록에서 **Storm**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-110">In the list of services, select **Storm**.</span></span>
3. <span data-ttu-id="79522-111">**빠른 연결** 메뉴에서 **Storm UI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-111">In the **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="79522-112">직접 링크</span><span class="sxs-lookup"><span data-stu-id="79522-112">Direct link</span></span>
<span data-ttu-id="79522-113">다음 URL에서 Storm UI에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-113">You can access the Storm UI at the following URL:</span></span>

<span data-ttu-id="79522-114">https://\<클러스터 DNS 이름\>/stormui</span><span class="sxs-lookup"><span data-stu-id="79522-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="79522-115">예제:</span><span class="sxs-lookup"><span data-stu-id="79522-115">Example:</span></span>

 <span data-ttu-id="79522-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="79522-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a><span data-ttu-id="79522-117">한 토폴로지에서 다른 토폴로지로 Storm EventHub Spout 검사점 정보를 전송하는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-117">How do I transfer Storm event hub spout checkpoint information from one topology to another</span></span>

<span data-ttu-id="79522-118">HDInsight Storm 이벤트 허브 spout .jar 파일을 사용하여 Azure Event Hubs에서 읽은 토폴로지를 개발하는 경우 새 클러스터와 동일한 이름을 갖는 토폴로지를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-118">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span></span> <span data-ttu-id="79522-119">그러나 Apache ZooKeeper에 커밋된 검사점 데이터를 이전 클러스터에서 보유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-119">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="79522-120">검사점 데이터 저장 위치</span><span class="sxs-lookup"><span data-stu-id="79522-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="79522-121">오프셋에 대한 검사점 데이터는 Zookeeper의 이벤트 허브 Spout를 통해 다음 두 루트 경로에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="79522-121">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="79522-122">비트랜잭션 Spout 검사점 데이터는 /eventhubspout에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="79522-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="79522-123">트랜잭션 Spout 검사점 데이터는 /transactional에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="79522-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-to-restore"></a><span data-ttu-id="79522-124">복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-124">How to restore</span></span>
<span data-ttu-id="79522-125">ZooKeeper에서 데이터를 내보낸 다음 새 이름을 사용해서 다시 ZooKeeper로 가져오는 데 사용하는 스크립트 및 라이브러리를 가져오려면 [HDInsight Storm 예제](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79522-125">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="79522-126">lib 폴더에는 가져오기/내보내기 작업에 대한 구현이 포함된 .jar 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-126">The lib folder has .jar files that contain the implementation for the export/import operation.</span></span> <span data-ttu-id="79522-127">bash 폴더에는 이전 클러스터의 ZooKeeper 서버에서 데이터를 내보낸 후 새 클러스터의 ZooKeeper 서버로 다시 가져오는 방법을 보여 주는 예제 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-127">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span></span>

<span data-ttu-id="79522-128">데이터를 내보낸 후 가져오려면 ZooKeeper 노드에서 [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-128">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span></span> <span data-ttu-id="79522-129">올바른 HDP(Hortonworks Data Platform) 버전으로 스크립트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-129">Update the script to the correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="79522-130">(이러한 스크립트를 HDInsight에서 제네릭으로 만들기 위해 작업 중입니다.</span><span class="sxs-lookup"><span data-stu-id="79522-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="79522-131">제네릭 스크립트는 사용자가 수정하지 않고 클러스터의 모든 노드에서 실행할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="79522-131">Generic scripts can run from any node on the cluster without modifications by the user.)</span></span>

<span data-ttu-id="79522-132">내보내기 명령은 설정한 Azure Blob Storage 또는 Azure Data Lake Store 저장소의 Apache HDFS(Hadoop 분산 파일 시스템) 경로에 메타데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="79522-132">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="79522-133">예</span><span class="sxs-lookup"><span data-stu-id="79522-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="79522-134">오프셋 메타데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="79522-134">Export offset metadata</span></span>
1. <span data-ttu-id="79522-135">SSH를 사용하여 검사점 오프셋을 내보내야 하는 클러스터의 ZooKeeper 클러스터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-135">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="79522-136">HDP 버전 문자열을 업데이트한 후 다음 명령을 실행하여 Zookeeper 오프셋 데이터를 /stormmetadta/zkdata HDFS 경로로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="79522-136">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="79522-137">오프셋 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="79522-137">Import offset metadata</span></span>
1. <span data-ttu-id="79522-138">SSH를 사용하여 검사점 오프셋을 내보내야 하는 클러스터의 ZooKeeper 클러스터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-138">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="79522-139">HDP 버전 문자열을 업데이트한 후 다음 명령을 실행하여 ZooKeeper 오프셋 데이터를 /stormmetadta/zkdata HDFS 경로에서 대상 클러스터의 ZooKeeper 서버로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="79522-139">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a><span data-ttu-id="79522-140">토폴로지에서 맨 처음부터 또는 사용자가 선택하는 타임스탬프부터 데이터 처리를 시작할 수 있도록 오프셋 메타데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="79522-140">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span></span>
1. <span data-ttu-id="79522-141">SSH를 사용하여 검사점 오프셋을 내보내야 하는 클러스터의 ZooKeeper 클러스터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-141">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="79522-142">HDP 버전 문자열을 업데이트한 후 다음 명령을 실행하여 현재 클러스터의 모든 ZooKeeper 오프셋 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-142">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="79522-143">클러스터에서 Storm 이진 파일을 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="79522-144">현재 HDP 스택에 대한 Storm 이진 파일은 /usr/hdp/current/storm-client에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-144">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="79522-145">위치는 헤드 노드 및 작업자 노드 둘 다에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-145">The location is the same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="79522-146">/usr/hdp에 특정 HDP 버전에 대한 이진 파일이 여러 개 있을 수 있습니다(예: /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="79522-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="79522-147">/usr/hdp/current/storm-client 폴더는 클러스터에서 실행되는 최신 버전과 기호화된 링크로 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-147">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span></span>

<span data-ttu-id="79522-148">자세한 내용은 [SSH를 사용하여 HDInsight 클러스터에 연결](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) 및 [Storm](http://storm.apache.org/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79522-148">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="79522-149">Storm 클러스터의 배포 토폴로지를 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-149">How do I determine the deployment topology of a Storm cluster</span></span>
<span data-ttu-id="79522-150">먼저 HDInsight Storm과 함께 설치된 모든 구성 요소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="79522-151">Storm 클러스터는 다음 4가지 노드 범주로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="79522-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="79522-152">게이트웨이 노드</span><span class="sxs-lookup"><span data-stu-id="79522-152">Gateway nodes</span></span>
* <span data-ttu-id="79522-153">헤드 노드</span><span class="sxs-lookup"><span data-stu-id="79522-153">Head nodes</span></span>
* <span data-ttu-id="79522-154">ZooKeeper 노드</span><span class="sxs-lookup"><span data-stu-id="79522-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="79522-155">작업자 노드</span><span class="sxs-lookup"><span data-stu-id="79522-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="79522-156">게이트웨이 노드</span><span class="sxs-lookup"><span data-stu-id="79522-156">Gateway nodes</span></span>
<span data-ttu-id="79522-157">게이트웨이 노드는 활성 Ambari 관리 서비스에 공용으로 액세스할 수 있는 게이트웨이 및 역방향 프록시 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="79522-157">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span></span> <span data-ttu-id="79522-158">이 노드는 Ambari 리더 투표도 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="79522-159">헤드 노드</span><span class="sxs-lookup"><span data-stu-id="79522-159">Head nodes</span></span>
<span data-ttu-id="79522-160">Storm 헤드 노드에서 실행하는 서비스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-160">Storm head nodes run the following services:</span></span>
* <span data-ttu-id="79522-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="79522-161">Nimbus</span></span>
* <span data-ttu-id="79522-162">Ambari 서버</span><span class="sxs-lookup"><span data-stu-id="79522-162">Ambari server</span></span>
* <span data-ttu-id="79522-163">Ambari 메트릭 서버</span><span class="sxs-lookup"><span data-stu-id="79522-163">Ambari Metrics server</span></span>
* <span data-ttu-id="79522-164">Ambari 메트릭 수집기</span><span class="sxs-lookup"><span data-stu-id="79522-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="79522-165">ZooKeeper 노드</span><span class="sxs-lookup"><span data-stu-id="79522-165">ZooKeeper nodes</span></span>
<span data-ttu-id="79522-166">HDInsight는 3 노드 ZooKeeper 쿼럼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="79522-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="79522-167">쿼럼 크기는 고정되어 있으며 다시 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-167">The quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="79522-168">클러스터의 Storm 서비스는 ZooKeeper 쿼럼을 자동으로 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="79522-168">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="79522-169">작업자 노드</span><span class="sxs-lookup"><span data-stu-id="79522-169">Worker nodes</span></span>
<span data-ttu-id="79522-170">Storm 작업자 노드에서 실행하는 서비스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-170">Storm worker nodes run the following services:</span></span>
* <span data-ttu-id="79522-171">감독자</span><span class="sxs-lookup"><span data-stu-id="79522-171">Supervisor</span></span>
* <span data-ttu-id="79522-172">토폴로지를 실행하기 위한 작업자 JVM(Java Virtual Machines)</span><span class="sxs-lookup"><span data-stu-id="79522-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="79522-173">Ambari 에이전트</span><span class="sxs-lookup"><span data-stu-id="79522-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="79522-174">개발용 Storm 이벤트 허브 spout 이진을 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="79522-175">토폴로지에 Storm 이벤트 허브 spout .jar 파일을 사용하는 방법에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79522-175">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="79522-176">Java 기반 토폴로지</span><span class="sxs-lookup"><span data-stu-id="79522-176">Java-based topology</span></span>
[<span data-ttu-id="79522-177">HDInsight의 Storm으로 Azure Event Hubs에서 이벤트 처리(Java)</span><span class="sxs-lookup"><span data-stu-id="79522-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="79522-178">C# 기반 토폴로지(HDInsight 3.4 이상 Linux Storm 클러스터의 Mono)</span><span class="sxs-lookup"><span data-stu-id="79522-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="79522-179">HDInsight의 Storm(C#)에서 Azure Event Hubs의 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="79522-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="79522-180">HDInsight 3.5 이상의 Linux Storm 클러스터에 대한 최신 Storm 이벤트 허브 Spout 이진 파일</span><span class="sxs-lookup"><span data-stu-id="79522-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="79522-181">HDInsight 3.5 이상의 Linux Storm 클러스터에서 작동하는 최신 Storm 이벤트 허브 spout을 사용하는 방법을 알아보려면 mvn-repo [추가 정보 파일](https://github.com/hdinsight/mvn-repo/blob/master/README.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79522-181">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="79522-182">소스 코드 예제</span><span class="sxs-lookup"><span data-stu-id="79522-182">Source code examples</span></span>
<span data-ttu-id="79522-183">Azure HDInsight 클러스터에서 Java로 작성된 Apache Storm 토폴로지를 사용하여 Azure 이벤트 허브에서 읽고 쓰기 방법에 대해서는 [예제](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79522-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="79522-184">클러스터에서 Storm Log4J 구성 파일을 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="79522-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="79522-185">Storm 서비스에 대한 Apache Log4J 구성 파일을 식별하려면</span><span class="sxs-lookup"><span data-stu-id="79522-185">To identify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="79522-186">헤드 노드에서</span><span class="sxs-lookup"><span data-stu-id="79522-186">On head nodes</span></span>
<span data-ttu-id="79522-187">Nimbus Log4J 구성은 /usr/hdp/\<HDP 버전\>/storm/log4j2/cluster.xml에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-187">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="79522-188">작업자 노드에서</span><span class="sxs-lookup"><span data-stu-id="79522-188">On worker nodes</span></span>
<span data-ttu-id="79522-189">감독자 Log4J 구성은 /usr/hdp/\<HDP 버전\>/storm/log4j2/cluster.xml에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-189">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="79522-190">작업자 Log4J 구성은 /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79522-190">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="79522-191">예제: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="79522-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

