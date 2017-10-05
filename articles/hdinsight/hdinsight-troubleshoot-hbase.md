---
title: "Azure HDInsight를 사용한 HBase 문제 해결 | Microsoft Docs"
description: "HBase 및 Azure HDInsight 작업에 대한 일반적인 질문에 답합니다."
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 15412c3853a2b8436c5e96034c9a92a2a1094662
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="6a61f-103">Azure HDInsight를 사용한 HBase 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6a61f-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="6a61f-104">Apache Ambari에서 Apache HBase 페이로드를 사용할 때의 주요 문제 및 해결 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-104">Learn about the top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="6a61f-105">할당되지 않은 여러 지역이 포함된 hbck 명령 보고서를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="6a61f-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="6a61f-106">`hbase hbck` 명령을 실행할 때 볼 수 있는 일반적인 오류 메시지는 “할당되지 않은 여러 영역이 있거나 영역 체인에 빈 영역이 있습니다.”입니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-106">A common error message that you might see when you run the `hbase hbck` command is "multiple regions being unassigned or holes in the chain of regions."</span></span>

<span data-ttu-id="6a61f-107">HBase Master UI에서 모든 영역 서버 중 부하가 분산되지 않은 영역 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-107">In the HBase Master UI, you can see the number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="6a61f-108">그런 후 `hbase hbck` 명령을 실행하여 영역 체인의 빈 영역을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-108">Then, you can run `hbase hbck` command to see holes in the region chain.</span></span>

<span data-ttu-id="6a61f-109">빈 영역은 오프라인 영역으로 인해 야기된 것일 수 있으므로 먼저 할당을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-109">Holes might be caused by the offline regions, so fix the assignments first.</span></span> 

<span data-ttu-id="6a61f-110">할당되지 않은 영역을 정상 상태로 전환하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-110">To bring the unassigned regions back to a normal state, complete the following steps:</span></span>

1. <span data-ttu-id="6a61f-111">SSH를 사용하여 HDInsight HBase 클러스터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-111">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="6a61f-112">ZooKeeper 셸에 연결하려면 `hbase zkcli` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-112">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="6a61f-113">`rmr /hbase/regions-in-transition` 명령 또는 `rmr /hbase-unsecure/regions-in-transition` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-113">Run the `rmr /hbase/regions-in-transition` command or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="6a61f-114">`hbase zkcli` 셸을 종료하려면 `exit` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-114">To exit from the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="6a61f-115">Apache Ambari UI를 열고 활성 HBase Master 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-115">Open the Apache Ambari UI, and then restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="6a61f-116">`hbase hbck` 명령을 다시 실행합니다(옵션 제외).</span><span class="sxs-lookup"><span data-stu-id="6a61f-116">Run the `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="6a61f-117">이 명령의 출력을 확인하고 모든 영역이 할당되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-117">Check the output of this command to ensure that all regions are being assigned.</span></span>


## <span data-ttu-id="6a61f-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>영역 할당에 대해 hbck 명령을 사용하여 시간 제한 문제를 해결하는 방법</span><span class="sxs-lookup"><span data-stu-id="6a61f-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="6a61f-119">문제</span><span class="sxs-lookup"><span data-stu-id="6a61f-119">Issue</span></span>

<span data-ttu-id="6a61f-120">`hbck` 명령을 사용할 때 시간 초과 문제가 발생하는 잠재적 원인은 오랜 시간 동안 여러 영역이 "전환" 상태에 있다는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-120">A potential cause for timeout issues when you use the `hbck` command might be that several regions are in the "in transition" state for a long time.</span></span> <span data-ttu-id="6a61f-121">HBase Master UI에서 이러한 영역이 오프라인으로 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-121">You can see those regions as offline in the HBase Master UI.</span></span> <span data-ttu-id="6a61f-122">전환하려는 영역 수가 많기 때문에 HBase Master에서 시간이 초과되어 해당 영역을 온라인 상태로 전환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-122">Because a high number of regions are attempting to transition, HBase Master might timeout and be unable to bring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6a61f-123">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-123">Resolution steps</span></span>

1. <span data-ttu-id="6a61f-124">SSH를 사용하여 HDInsight HBase 클러스터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-124">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="6a61f-125">ZooKeeper 셸에 연결하려면 `hbase zkcli` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-125">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="6a61f-126">`rmr /hbase/regions-in-transition` 또는 `rmr /hbase-unsecure/regions-in-transition` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-126">Run the `rmr /hbase/regions-in-transition` or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="6a61f-127">`hbase zkcli` 셸을 종료하려면 `exit` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-127">To exit the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="6a61f-128">Ambari UI에서 활성 HBase Master 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-128">In the Ambari UI, restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="6a61f-129">`hbase hbck -fixAssignments` 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-129">Run the `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="6a61f-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>클러스터에서 HDFS 안전 모드 사용 안 함을 적용하는 방법</span><span class="sxs-lookup"><span data-stu-id="6a61f-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="6a61f-131">문제</span><span class="sxs-lookup"><span data-stu-id="6a61f-131">Issue</span></span>

<span data-ttu-id="6a61f-132">로컬 HDFS(Hadoop 분산 파일 시스템)가 HDInsight 클러스터에서 안전 모드 상태로 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-132">The local Hadoop Distributed File System (HDFS) is stuck in safe mode on the HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="6a61f-133">자세한 설명</span><span class="sxs-lookup"><span data-stu-id="6a61f-133">Detailed description</span></span>

<span data-ttu-id="6a61f-134">다음 HDFS 명령을 실행할 때 실패하여 이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-134">This error might be caused by a failure when you run the following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="6a61f-135">이 명령을 실행하려고 할 때 표시될 수 있는 오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-135">The error you might see when you try to run the command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="6a61f-136">가능한 원인:</span><span class="sxs-lookup"><span data-stu-id="6a61f-136">Probable cause</span></span>

<span data-ttu-id="6a61f-137">HDInsight 클러스터 규모가 매우 적은 수의 노드로 축소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-137">The HDInsight cluster has been scaled down to a very few nodes.</span></span> <span data-ttu-id="6a61f-138">노드 수가 HDFS 복제 계수보다 낮거나 이 계수에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-138">The number of nodes is below or close to the HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6a61f-139">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-139">Resolution steps</span></span> 

1. <span data-ttu-id="6a61f-140">다음 명령을 실행하여 HDInsight 클러스터에서 HDFS 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-140">Get the status of the HDFS on the HDInsight cluster by running the following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="6a61f-141">또한 다음 명령을 실행하여 HDInsight 클러스터에서 HDFS의 무결성을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-141">You also can check the integrity of the HDFS on the HDInsight cluster by using the following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting to namenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   The filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="6a61f-142">복제된 블록에서 누락되었거나 손상된 부분이 없거나 해당 블록을 무시할 수 있다고 판단되면 다음 명령을 실행하여 이름 노드를 안전 모드에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run the following command to take the name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="6a61f-143">Apache Phoenix를 사용한 JDBC 또는 SQLLine 연결 문제를 해결하는 방법</span><span class="sxs-lookup"><span data-stu-id="6a61f-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6a61f-144">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-144">Resolution steps</span></span>

<span data-ttu-id="6a61f-145">Phoenix와 연결하려면 활성 ZooKeeper 노드의 IP 주소를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-145">To connect with Phoenix, you must provide the IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="6a61f-146">sqlline.py에서 연결하려는 ZooKeeper 서비스가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-146">Ensure that the ZooKeeper service to which sqlline.py is trying to connect is up and running.</span></span>
1. <span data-ttu-id="6a61f-147">SSH를 사용하여 HDInsight 클러스터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-147">Sign in to the HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="6a61f-148">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-148">Enter the following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="6a61f-149">Ambari UI에서 활성 ZooKeeper 노드의 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-149">You can get the IP address of the active ZooKeeper node from the Ambari UI.</span></span> <span data-ttu-id="6a61f-150">**HBase** > **빠른 링크** > **ZK\*(활성)** > **ZooKeeper 정보**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-150">Go to **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="6a61f-151">sqlline.py가 Phoenix에 연결되어 있고 시간이 초과되지 않으면 다음 명령을 실행하여 Phoenix의 가용성과 상태에 대한 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-151">If the sqlline.py connects to Phoenix and does not timeout, run the following command to validate the availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="6a61f-152">이 명령이 작동하는 경우 문제가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-152">If this command works, there is no issue.</span></span> <span data-ttu-id="6a61f-153">사용자가 제공한 IP 주소가 잘못되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-153">The IP address provided by the user might be incorrect.</span></span> <span data-ttu-id="6a61f-154">그러나 이 명령이 오랫동안 일시 중지되었다가 다음 오류를 표시하는 경우 5단계를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-154">However, if the command pauses for an extended time and then displays the following error, continue to step 5.</span></span>

   ```apache
           Error while connecting to sqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting to jdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="6a61f-155">헤드 노드(hn0)에서 다음 명령을 실행하여 Phoenix SYSTEM.CATALOG 테이블의 상태를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-155">Run the following commands from the head node (hn0) to diagnose the condition of the Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="6a61f-156">명령에서 다음과 비슷한 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-156">The command should return an error similar to the following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="6a61f-157">Ambari UI에서 다음 단계를 완료하여 모든 ZooKeeper 노드에서 HMaster 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-157">In the Ambari UI, complete the following steps to restart the HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="6a61f-158">HBase의 **요약** 섹션에서 **HBase** > **Active HBase Master**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-158">In the **Summary** section of HBase, go to **HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="6a61f-159">**구성 요소** 섹션에서 HBase Master 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-159">In the **Components** section, restart the HBase Master service.</span></span>
    3. <span data-ttu-id="6a61f-160">나머지 모든 **Standby HBase Master** 서비스에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="6a61f-161">HBase Master 서비스가 안정화되고 복구 프로세스를 완료하는 데 최대 5분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-161">It can take up to five minutes for the HBase Master service to stabilize and finish the recovery process.</span></span> <span data-ttu-id="6a61f-162">몇 분 후에 sqlline.py 명령을 반복하여 SYSTEM.CATALOG 테이블이 작동되고 쿼리될 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-162">After a few minutes, repeat the sqlline.py commands to confirm that the SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="6a61f-163">SYSTEM.CATALOG 테이블이 정상으로 전환되면 Phoenix에 대한 연결 문제가 자동으로 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-163">When the SYSTEM.CATALOG table is back to normal, the connectivity issue to Phoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-to-fail-to-start"></a><span data-ttu-id="6a61f-164">마스터 서버를 시작하지 못하게 하는 원인</span><span class="sxs-lookup"><span data-stu-id="6a61f-164">What causes a master server to fail to start</span></span>

### <a name="error"></a><span data-ttu-id="6a61f-165">오류</span><span class="sxs-lookup"><span data-stu-id="6a61f-165">Error</span></span> 

<span data-ttu-id="6a61f-166">원자성 이름 바꾸기 실패가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="6a61f-167">자세한 설명</span><span class="sxs-lookup"><span data-stu-id="6a61f-167">Detailed description</span></span>

<span data-ttu-id="6a61f-168">시작 프로세스 동안 HMaster는 많은 초기화 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-168">During the startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="6a61f-169">여기에는 스크래치(.tmp) 폴더에서 데이터 폴더로 데이터를 이동하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-169">These include moving data from the scratch (.tmp) folder to the data folder.</span></span> <span data-ttu-id="6a61f-170">또한 HMaster는 WAL(미리 쓰기 로그) 폴더를 찾아 응답하지 않는 영역 서버가 있는지 등을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-170">HMaster also looks at the write-ahead logs (WALs) folder to see if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="6a61f-171">시작 동안 HMaster는 이러한 폴더에 대해 기본 `list` 명령을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="6a61f-172">언제든지 이러한 폴더에 예기치 않은 파일이 있을 경우 예외가 발생하고 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="6a61f-173">가능한 원인:</span><span class="sxs-lookup"><span data-stu-id="6a61f-173">Probable cause</span></span>

<span data-ttu-id="6a61f-174">영역 서버 로그에서 파일 생성 타임라인을 확인한 다음, 파일이 만들어진 시간에 프로세스 충돌이 있었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-174">In the region server logs, try to identify the timeline of the file creation, and then see if there was a process crash around the time the file was created.</span></span> <span data-ttu-id="6a61f-175">(HBase 지원 서비스에 문의하여 이 작업에 대한 도움을 요청하세요.) 이렇게 하면 이 버그에 연결하지 않도록 방지하고 정상적인 프로세스 종료를 보장하는 보다 강력한 메커니즘을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-175">(Contact HBase support to assist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="6a61f-176">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-176">Resolution steps</span></span>

<span data-ttu-id="6a61f-177">호출 스택을 확인하고 문제를 일으킬 수 있는 폴더(예: WAL 폴더 또는 .tmp 폴더)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-177">Check the call stack and try to determine which folder might be causing the problem (for instance, it might be the WALs folder or the .tmp folder).</span></span> <span data-ttu-id="6a61f-178">그런 다음 클라우드 탐색기 또는 HDFS 명령을 사용하여 문제가 있는 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-178">Then, in Cloud Explorer or by using HDFS commands, try to locate the problem file.</span></span> <span data-ttu-id="6a61f-179">일반적으로 \*-renamePending.json 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="6a61f-180">(\*-renamePending.json 파일은 WASB 드라이버에서 원자성 이름 바꾸기 작업을 구현하는 데 사용되는 저널 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-180">(The \*-renamePending.json file is a journal file that's used to implement the atomic rename operation in the WASB driver.</span></span> <span data-ttu-id="6a61f-181">이 구현의 버그 때문에 이러한 파일은 프로세스 충돌 등이 발생한 후에도 남아 있을 수 있습니다.) 클라우드 탐색기 또는 HDFS 명령을 사용하여 이 파일을 강제로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-181">Due to bugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="6a61f-182">경우에 따라 *$$$.$$$* 같은 임시 파일이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="6a61f-183">이 파일을 보기 위해 HDFS `ls` 명령을 사용해야 합니다. 클라우드 탐색기에서는 이 파일을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-183">You have to use HDFS `ls` command to see this file; you cannot see the file in Cloud Explorer.</span></span> <span data-ttu-id="6a61f-184">이 파일을 삭제하려면 HDFS 명령 `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-184">To delete this file, use the HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="6a61f-185">이러한 명령을 실행한 후 HMaster는 즉시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="6a61f-186">오류</span><span class="sxs-lookup"><span data-stu-id="6a61f-186">Error</span></span>

<span data-ttu-id="6a61f-187">xxx 영역에 대한 서버 주소가 *hbase: meta*에 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="6a61f-188">자세한 설명</span><span class="sxs-lookup"><span data-stu-id="6a61f-188">Detailed description</span></span>

<span data-ttu-id="6a61f-189">Linux 클러스터에 *hbase:meta* 테이블이 온라인 상태가 아님을 나타내는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-189">You might see a message on your Linux cluster that indicates that the *hbase: meta* table is not online.</span></span> <span data-ttu-id="6a61f-190">`hbck`를 실행하면 "모든 영역에서 replicaId 0 hbase: meta 테이블을 찾을 없습니다."라고 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="6a61f-191">HBase를 다시 시작한 후에 HMaster를 초기화하지 못하여 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-191">The problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="6a61f-192">HMaster 로그에서 "hbase: backup \<영역 이름\>에 대한 서버 주소가 나열되지 않습니다."라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-192">In the HMaster logs, you might see the message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="6a61f-193">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-193">Resolution steps</span></span>

1. <span data-ttu-id="6a61f-194">HBase 셸에서 다음 명령을 입력합니다(해당되는 경우 실제 값 변경).</span><span class="sxs-lookup"><span data-stu-id="6a61f-194">In the HBase shell, enter the following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="6a61f-195">*hbase: namespace* 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-195">Delete the *hbase: namespace* entry.</span></span> <span data-ttu-id="6a61f-196">이 항목은 *hbase:namespace* 테이블이 검색될 때 보고되는 것과 같은 오류일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-196">This entry might be the same error that's being reported when the *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="6a61f-197">HMaster를 실행 상태로 만들려면 Ambari UI에서 활성 HBase 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-197">To bring up HBase in a running state, in the Ambari UI, restart the Active HMaster service.</span></span>  

4. <span data-ttu-id="6a61f-198">HBase 셸에서 모든 오프라인 테이블을 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-198">In the HBase shell, to bring up all offline tables, run the following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="6a61f-199">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="6a61f-199">Additional reading</span></span>

[<span data-ttu-id="6a61f-200">HBase 테이블을 처리할 수 없음</span><span class="sxs-lookup"><span data-stu-id="6a61f-200">Unable to process the HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="6a61f-201">오류</span><span class="sxs-lookup"><span data-stu-id="6a61f-201">Error</span></span>

<span data-ttu-id="6a61f-202">"java.io.IOException: 네임스페이스 테이블이 할당될 때까지 기다리는 시간(300000ms)을 초과했습니다."와 같은 심각한 예외로 인해 HMaster에서 시간을 초과했습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-202">HMaster times out with a fatal exception similar to "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="6a61f-203">자세한 설명</span><span class="sxs-lookup"><span data-stu-id="6a61f-203">Detailed description</span></span>

<span data-ttu-id="6a61f-204">HMaster 서비스를 다시 시작할 때 플러시되지 않은 많은 테이블 및 영역이 있는 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="6a61f-205">다시 시작이 실패할 수 있으며 위의 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-205">Restart might fail, and you'll see the preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="6a61f-206">가능한 원인:</span><span class="sxs-lookup"><span data-stu-id="6a61f-206">Probable cause</span></span>

<span data-ttu-id="6a61f-207">HMaster 서비스의 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-207">This is a known issue with the HMaster service.</span></span> <span data-ttu-id="6a61f-208">일반 클러스터 시작 작업이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="6a61f-209">네임스페이스 테이블이 아직 할당되지 않았으므로 HMaster가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-209">HMaster shuts down because the namespace table isn’t yet assigned.</span></span> <span data-ttu-id="6a61f-210">이 오류는 플러시되지 않은 대량의 데이터가 있고 5분의 제한 시간으로는 부족한 시나리오에서만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="6a61f-211">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-211">Resolution steps</span></span>

1. <span data-ttu-id="6a61f-212">Ambari UI에서 **HBase** > **Configs**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-212">In the Ambari UI, go to **HBase** > **Configs**.</span></span> <span data-ttu-id="6a61f-213">사용자 지정 hbase-site.xml 파일에서 다음 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-213">In the custom hbase-site.xml file, add the following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="6a61f-214">필요한 서비스(HMaster 및 가능한 경우 다른 HBase 서비스)를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-214">Restart the required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="6a61f-215">지역 서버에서 다시 시작 실패가 발생하는 원인</span><span class="sxs-lookup"><span data-stu-id="6a61f-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="6a61f-216">문제</span><span class="sxs-lookup"><span data-stu-id="6a61f-216">Issue</span></span>

<span data-ttu-id="6a61f-217">영역 서버의 다시 시작 실패는 다음의 모범 사례를 통해 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="6a61f-218">HBase 영역 서버를 다시 시작하려는 경우 과도한 워크로드 활동을 일시 중지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-218">We recommend that you pause heavy workload activity when you are planning to restart HBase region servers.</span></span> <span data-ttu-id="6a61f-219">종료가 진행 중일 때 응용 프로그램이 영역 서버와 계속 연결되면 영역 서버 재시작 작업이 몇 분 정도 더 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-219">If an application continues to connect with region servers when shutdown is in progress, the region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="6a61f-220">또한 먼저 모든 테이블을 플러시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-220">Also, it's a good idea to first flush all the tables.</span></span> <span data-ttu-id="6a61f-221">테이블을 플러시하는 방법에 대한 참조는 [HDInsight HBase: 테이블에 플러시하여 HBase 클러스터 다시 시작 시간을 개선하는 방법](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a61f-221">For a reference on how to flush tables, see [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="6a61f-222">Ambari UI에서 HBase 영역 서버에 대한 다시 시작 작업을 시작하면 영역 서버가 다운되지만 바로 다시 시작되지 않는 것을 보게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-222">If you initiate the restart operation on HBase region servers from the Ambari UI, you immediately see that the region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="6a61f-223">백그라운드에서 진행되는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-223">Here's what's happening behind the scenes:</span></span> 

1. <span data-ttu-id="6a61f-224">Ambari 에이전트가 영역 서버에 중지 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-224">The Ambari agent sends a stop request to the region server.</span></span>
2. <span data-ttu-id="6a61f-225">Ambari 에이전트에서 영역 서버가 정상적으로 종료될 때까지 30초 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-225">The Ambari agent waits for 30 seconds for the region server to shut down gracefully.</span></span> 
3. <span data-ttu-id="6a61f-226">응용 프로그램이 영역 서버에 계속 연결될 경우 서버는 즉시 종료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-226">If your application continues to connect with the region server, the server won't shut down immediately.</span></span> <span data-ttu-id="6a61f-227">종료되기 전에 30초 제한 시간에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-227">The 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="6a61f-228">30초 후 Ambari 에이전트는 영역 서버에 강제 종료(`kill -9`) 명령을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-228">After 30 seconds, the Ambari agent sends a force-kill (`kill -9`) command to the region server.</span></span> <span data-ttu-id="6a61f-229">이 사항은 ambari-agent 로그(해당 작업자 노드의 /var/log/ 디렉터리)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-229">You can see this in the ambari-agent log (in the /var/log/ directory of the respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="6a61f-230">이러한 갑작스러운 종료로 인해 영역 서버 프로세스가 중지되더라도 프로세스와 연결된 포트가 해제되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-230">Because of the abrupt shutdown, the port associated with the process might not be released, even though the region server process is stopped.</span></span> <span data-ttu-id="6a61f-231">이러한 상황으로 인해 다음 로그와 같이 영역 서버가 시작되는 동안 AddressBindException이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-231">This situation can lead to an AddressBindException when the region server is starting, as shown in the following logs.</span></span> <span data-ttu-id="6a61f-232">영역 서버가 시작되지 못할 경우 작업자 노드의 /var/log/hbase 디렉터리에 있는 region-server.log에서 이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-232">You can verify this in the region-server.log in the /var/log/hbase directory on the worker nodes where the region server fails to start.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding to /10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="6a61f-233">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="6a61f-233">Resolution steps</span></span>

1. <span data-ttu-id="6a61f-234">HBase 영역 서버의 부하를 줄인 후에 다시 시작을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6a61f-234">Try to reduce the load on the HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="6a61f-235">또는 다음 명령을 사용하여 작업자 노드의 영역 서버를 수동으로 다시 시작합니다(1단계가 도움이 되지 않을 경우).</span><span class="sxs-lookup"><span data-stu-id="6a61f-235">Alternatively (if step 1 doesn't help), try to manually restart region servers on the worker nodes by using the following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

