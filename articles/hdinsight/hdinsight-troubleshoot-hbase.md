---
title: "Azure HDInsight를 사용 하 여 HBase aaaTroubleshoot | Microsoft Docs"
description: "HBase 및 Azure HDInsight 작업에 대 한 toocommon 질문을 답변을 가져옵니다."
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
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Azure HDInsight를 사용한 HBase 문제 해결

Apache Ambari에 Apache HBase 페이로드를 작업할 때 hello 상위 문제와 그 해결 방법에 알아봅니다.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>할당되지 않은 여러 지역이 포함된 hbck 명령 보고서를 실행하는 방법

일반적인 오류 메시지는 hello를 실행 하는 경우 표시 될 수도 `hbase hbck` 명령입니다 "여러 지역 되 고 할당 되지 않은 또는 구멍 영역의 hello 체인에."

HBase 마스터 UI hello에서 모든 지역의 서버에 대해 불균형이 영역의 hello 번호를 볼 수 있습니다. 다음을 실행 하거나 `hbase hbck` toosee 구멍 hello 지역 체인에 명령 합니다.

구멍은 hello 오프 라인 영역, 따라서 수정 hello 할당 하 여 먼저 발생할 수 있습니다. 

toobring hello 할당 되지 않은 영역 백 tooa 정상 상태를 hello 다음 단계를 따르십시오.

1. SSH를 사용 하 여 HDInsight HBase 클러스터 toohello에 로그인 합니다.
2. hello 실행 되는 hello 사육 셸 사용 하 여 tooconnect `hbase zkcli` 명령입니다.
3. Hello 실행 `rmr /hbase/regions-in-transition` 명령 또는 hello `rmr /hbase-unsecure/regions-in-transition` 명령입니다.
4. hello에서 tooexit `hbase zkcli` 셸, hello를 사용 하 여 `exit` 명령입니다.
5. Hello Apache Ambari UI를 열고 hello 활성 HBase 마스터 서비스 다시 시작 합니다.
6. Hello 실행 `hbase hbck` 명령을 다시 (옵션 없이). 모든 지역 할당 되 고이 명령 tooensure의 hello 출력을 확인 합니다.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>영역 할당에 대해 hbck 명령을 사용하여 시간 제한 문제를 해결하는 방법

### <a name="issue"></a>문제

Hello를 사용 하는 경우 시간 초과 문제에 대 한 잠재적 원인 `hbck` 명령이 "전환" hello에는 여러 지역의 있을 수 있습니다 오랜 시간 동안 상태입니다. 해당 영역 hello HBase 마스터 UI에서에서 오프 라인으로 볼 수 있습니다. 많은 수의 지역 tootransition 시도 중인 HBase 마스터 시간 초과 수 고 없습니다 toobring 해당 영역을 다시 온라인 됩니다.

### <a name="resolution-steps"></a>해결 단계:

1. SSH를 사용 하 여 HDInsight HBase 클러스터 toohello에 로그인 합니다.
2. hello 실행 되는 hello 사육 셸 사용 하 여 tooconnect `hbase zkcli` 명령입니다.
3. Hello 실행 `rmr /hbase/regions-in-transition` 또는 hello `rmr /hbase-unsecure/regions-in-transition` 명령입니다.
4. tooexit hello `hbase zkcli` 셸, hello를 사용 하 여 `exit` 명령입니다.
5. Ambari UI hello hello 활성 HBase 마스터 서비스 다시 시작 했습니다.
6. Hello 실행 `hbase hbck -fixAssignments` 명령을 다시 합니다.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>클러스터에서 HDFS 안전 모드 사용 안 함을 적용하는 방법

### <a name="issue"></a>문제

hello 로컬 Hadoop 분산 파일 시스템 (HDFS) hello HDInsight 클러스터에서 안전 모드에서 중단 합니다.

### <a name="detailed-description"></a>자세한 설명

이 오류는 hello 다음 HDFS 명령을 실행 하는 경우는 오류로 인해 발생할 수 있습니다.

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

hello 오류 toorun hello 명령 려 할 때 표시 될 수는 다음과 같습니다.

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
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

### <a name="probable-cause"></a>가능한 원인:

hello HDInsight 클러스터 된 노드가 거의 tooa 축소 합니다. 노드 수가 hello 아래 되었거나 toohello HDFS 복제 요소를 닫습니다.

### <a name="resolution-steps"></a>해결 단계: 

1. Hello hello HDInsight에서 HDFS hello 다음 명령을 실행 하 여 클러스터의 hello 상태를 가져옵니다.

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
2. Hello hello HDInsight에서 HDFS hello 다음 명령을 사용 하 여 클러스터의 hello 무결성을 확인할 수도 있습니다.

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
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

   hello filesystem under path '/' is HEALTHY
   ```

3. 없는 없거나 손상 under-복제 된 블록 또는 해당 블록을 무시할 수 있는지를 확인 하는 경우 안전 모드에서 명령 tootake hello 이름 노드 다음에 오는 hello를 실행 합니다.

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Apache Phoenix를 사용한 JDBC 또는 SQLLine 연결 문제를 해결하는 방법

### <a name="resolution-steps"></a>해결 단계:

Phoenix와 tooconnect, 활성 사육 노드의 hello IP 주소를 제공 해야 합니다. 해당 hello 서비스 toowhich sqlline.py 시도 사육 확인 tooconnect 실행 되 고 있습니다.
1. SSH를 사용 하 여 HDInsight 클러스터 toohello에 로그인 합니다.
2. Hello 다음 명령을 입력 합니다.
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Hello Ambari UI에서에서 hello 활성 사육 노드의 hello IP 주소를 가져올 수 있습니다. 너무 이동**HBase** > **빠른 링크** > **ZK\* (활성)** > **사육정보**. 

3. Hello sqlline.py tooPhoenix 연결 시간 초과 되지 않는 경우 실행된 hello 다음 명령 toovalidate hello 가용성 및 피닉스의 상태 수 있습니다.

   ```apache
           !tables
           !quit
   ```      
4. 이 명령이 작동하는 경우 문제가 발생하지 않습니다. hello 사용자가 제공한 hello IP 주소가 올바르지 않을 수 있습니다. 그러나 hello 명령 오랜된 시간 동안 일시 중지 하 고 다음 hello 다음 오류가 표시를 하는 경우 계속 toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Hello 명령을 hello 피닉스 시스템의 hello 헤드 노드 (hn0) toodiagnose hello 조건에서 다음을 실행 합니다. 카탈로그 테이블:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   hello 명령이 오류 유사한 toohello 다음을 반환 해야 합니다. 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Ambari UI hello hello 단계 toorestart hello HMaster 서비스 사육 모든 노드에서 다음을 수행 합니다.

    1. Hello에 **요약** 섹션 HBase의 이동 너무**HBase** > **활성 HBase 마스터**합니다. 
    2. Hello에 **구성 요소** 섹션에서 hello HBase 마스터 서비스를 다시 시작 합니다.
    3. 나머지 모든 **Standby HBase Master** 서비스에 대해 이러한 단계를 반복합니다. 

Hello HBase 마스터 서비스 toostabilize toofive 분이 걸릴 하 고 hello 복구 프로세스를 완료할 수 있습니다. 몇 분 후 해당 hello 시스템 hello sqlline.py 명령을 tooconfirm 반복 합니다. 카탈로그 테이블, 이며 한다는 쿼리할 수 있습니다. 

시스템 hello 경우. 카탈로그 테이블은 백 toonormal, hello 연결 문제 tooPhoenix를 자동으로 해결 해야 합니다.


## <a name="what-causes-a-master-server-toofail-toostart"></a>마스터 서버 toofail toostart를 원인을

### <a name="error"></a>오류 

원자성 이름 바꾸기 실패가 발생했습니다.

### <a name="detailed-description"></a>자세한 설명

HMaster는 hello 시작 과정에서 많은 초기화 단계를 완료합니다. 여기에 hello 처음 (.tmp)에서 데이터를 이동할 폴더 toohello 데이터 폴더. HMaster도 살펴봅니다 hello 미리 쓰기 로그 (WALs) 폴더 toosee 모든 응답 하지 않는 지역 서버가 있는 경우 등입니다. 

시작 동안 HMaster는 이러한 폴더에 대해 기본 `list` 명령을 수행합니다. 언제든지 이러한 폴더에 예기치 않은 파일이 있을 경우 예외가 발생하고 시작되지 않습니다.  

### <a name="probable-cause"></a>가능한 원인:

Hello 지역 서버 로그에서 tooidentify hello 타임 라인 hello 파일 생성을 시도 하 고 hello 시간 hello 파일 주위 프로세스 충돌을 만든 경우를 확인 합니다. (HBase 지원 tooassist 문의이 작업을 수행 합니다.) 이렇게 하면 이 버그에 연결하지 않도록 방지하고 정상적인 프로세스 종료를 보장하는 보다 강력한 메커니즘을 제공할 수 있습니다.

### <a name="resolution-steps"></a>해결 단계:

Hello 호출 스택을 확인 하 고 시도 toodetermine 폴더 hello 문제를 초래할 수 있습니다 (예를 들어, 것 hello WALs 폴더 또는 hello.tmp 폴더). 그런 다음 클라우드 탐색기 또는 HDFS 명령을 사용 하 여 toolocate hello 문제가 있는 파일을 시도 합니다. 일반적으로 \*-renamePending.json 파일입니다. (hello \*-renamePending.json 파일이 hello WASB 드라이버에 tooimplement hello 원자성 이름 바꾸기 작업을 사용 하는 저널 파일은 합니다. 인해이 구현에서 toobugs, 이러한 파일 수 수 후 남은 프로세스 충돌 및 기타 등등.) 클라우드 탐색기 또는 HDFS 명령을 사용하여 이 파일을 강제로 삭제합니다. 

경우에 따라 *$$$.$$$* 같은 임시 파일이 있을 수도 있습니다. HDFS toouse 있는 `ls` toosee이이 파일을 명령; 클라우드 탐색기에서 hello 파일을 볼 수 없습니다. toodelete이 파일을 사용 하 여 hello HDFS 명령 `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`합니다.  

이러한 명령을 실행한 후 HMaster는 즉시 시작됩니다. 

### <a name="error"></a>오류

xxx 영역에 대한 서버 주소가 *hbase: meta*에 나열되지 않습니다.

### <a name="detailed-description"></a>자세한 설명

해당 hello 나타내는 Linux 클러스터에는 메시지가 표시 될 수 있습니다 *hbase: 메타* 테이블 온라인이 아닙니다. `hbck`를 실행하면 "모든 영역에서 replicaId 0 hbase: meta 테이블을 찾을 없습니다."라고 보고할 수 있습니다. hello 문제일 수 있습니다 HBase를 다시 시작한 후 HMaster 초기화 하지 못했습니다. Hello HMaster 로그 hello 메시지를 표시 될 수 있습니다: "hbase에 나열 된 주소가 없습니다. 서버: hbase 지역에 대 한 메타: 백업 \<지역 이름\>"입니다.  

### <a name="resolution-steps"></a>해결 단계:

1. HBase 셸 hello hello 명령 (해당 될 실제 값 변경) 다음을 입력 합니다.  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Hello 삭제 *hbase: 네임 스페이스* 항목입니다. 이 항목 수 있습니다 때 hello 보고 되는 동일한 오류 hello *hbase: 네임 스페이스* 테이블을 검색 합니다.

3. HBase hello Ambari UI에서에서 실행 중 상태에서를 toobring hello 활성 HMaster 서비스를 다시 시작 합니다.  

4. HBase 셸, 모든 오프 라인 상태 테이블을 toobring hello hello 다음 명령을 실행 합니다.

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>추가 참조 자료

[없습니다 tooprocess hello HBase 테이블](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>오류

심각한 예외와 유사한 too"java.io.IOException와 HMaster 시간 초과: 네임 스페이스 테이블 toobe 할당에 대 한 대기 시간이 초과 되어 300000ms."

### <a name="detailed-description"></a>자세한 설명

HMaster 서비스를 다시 시작할 때 플러시되지 않은 많은 테이블 및 영역이 있는 경우 이 문제가 발생할 수 있습니다. 다시 시작 실패 하 고 hello 앞에 오류 메시지가 표시 됩니다.  

### <a name="probable-cause"></a>가능한 원인:

Hello HMaster 서비스로 알려진된 문제입니다. 일반 클러스터 시작 작업이 오래 걸릴 수 있습니다. HMaster는 hello 네임 스페이스 테이블 아직 할당 되지 않은 때문에 종료 됩니다. 이 오류는 플러시되지 않은 대량의 데이터가 있고 5분의 제한 시간으로는 부족한 시나리오에서만 발생합니다.
  
### <a name="resolution-steps"></a>해결 단계:

1. Ambari UI hello에서 이동 너무**HBase** > **Configs**합니다. Hello 사용자 지정 hbase-site.xml 파일에서 설정에 따라 hello를 추가 합니다. 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. 필요한 hello 서비스 (HMaster, 및 기타 HBase 서비스)를 다시 시작 합니다.  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>지역 서버에서 다시 시작 실패가 발생하는 원인

### <a name="issue"></a>문제

영역 서버의 다시 시작 실패는 다음의 모범 사례를 통해 방지할 수 있습니다. 작업량이 많을 활동 toorestart HBase 영역 서버를 계획할 때 일시 중지 하는 것이 좋습니다. 응용 프로그램 계속 되 면 지역 서버와 tooconnect shutdown이 진행 중인 경우 hello 지역 서버 다시 시작 작업이 속도 느려집니다 몇 분 후입니다. 또한 테이블 hello 모든 플러시는 것이 좋습니다 toofirst를 됩니다. 방법에 대 한 참조에 대 한 tooflush 테이블 참조 [HDInsight HBase: tooimprove hello HBase 클러스터 테이블 플러시하여 시간을 다시 시작 방법](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/)합니다.

Hello Ambari UI에서에서 HBase 지역 서버의 hello 다시 시작 작업을 시작 하면 hello 지역 서버 다운 하지만 바로 다시 시작 하지 않으면 즉시 표시 됩니다. 

Hello 백그라운드 일어나는 다음과 같습니다. 

1. hello Ambari 에이전트가 중지 요청 toohello 영역 서버를 보냅니다.
2. hello Ambari 에이전트가 정상적으로 아래로 지역 서버 tooshut hello에 대 한 30 초 동안 대기 합니다. 
3. 를 응용 프로그램이 tooconnect hello 지역 서버와 계속 hello 서버 즉시 종료 되지 않습니다. hello 제한 시간은 30 초 전에 종료가 발생 만료 됩니다. 
4. 30 초 후 hello Ambari 에이전트를 강제 종료를 보냅니다 (`kill -9`) 명령 toohello 지역 서버. Hello /var/로그/디렉토리의 hello 각 작업자 노드 hello ambari 에이전트 로그에서이 확인할 수 있습니다.

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
Hello 상황이 뜻하지 않게 종료 되어 hello 프로세스와 관련 된 hello 포트 수 해제 되지, hello 지역 서버 프로세스를 중지 하는 경우에 합니다. 이 경우 발생할 수 있습니다 tooan AddressBindException hello 영역 서버를 시작할 때 hello 다음 로그에에서 표시 된 대로 합니다. Hello 지역 server.log hello /var/log/hbase 디렉터리에 hello 작업자 노드 hello 지역 서버 toostart 실패 한 지점에서이 확인할 수 있습니다. 

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
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
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

### <a name="resolution-steps"></a>해결 단계:

1. 다시 시작을 시작 하기 전에 hello HBase 영역 서버의 tooreduce hello 로드를 해 보십시오. 
2. 서버를 사용 하 여 hello 작업자 노드를 다음 hello 시도 toomanually 다시 시작 영역 (하는 경우 1 단계 데 도움이 되지 않습니다), 또는 명령:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

