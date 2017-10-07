---
title: "메모리 부족 오류 Azure HDInsight의 Hive aaaFix | Microsoft Docs"
description: "HDInsight에서 Hive 메모리 부족 오류를 수정합니다. hello 고객 시나리오는 많은 큰 테이블 간에 쿼리입니다."
keywords: "메모리 부족 오류, OOM, Hive 설정"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Azure HDInsight에서 Hive 메모리 부족 오류 수정

자세한 내용은 방법 toofix 메모리 부족 오류 하이브 하이브 메모리 설정을 구성 하 여 큰 테이블을 처리할 때.

## <a name="run-hive-query-against-large-tables"></a>큰 테이블에서 Hive 쿼리 실행

고객은 Hive 쿼리를 실행했습니다.

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

이 쿼리의 미묘한 차이는 다음과 같습니다.

* T 1은 별칭 tooa 큰 테이블, TABLE1 많은 문자열 열 형식입니다.
* 다른 테이블은 크지는 않지만 많은 열을 포함합니다.
* 모든 테이블은 서로 조인되며 TABLE1 및 기타 테이블의 여러 열과 조인되기도 합니다.

hello 하이브 쿼리는 toofinish를 26 분 24 노드 A3 HDInsight 클러스터에 걸렸습니다. 경고 메시지에 따라 고객 알지 못하게 hello을 hello:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

Hello Tez 실행 엔진을 사용 합니다. hello 동일한 쿼리를 15 분 동안 실행 하 고 다음 hello 다음 오류가 발생 했습니다.

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

hello 오류에는 더 큰 가상 컴퓨터 (예를 들어 D12)를 사용할 때 유지 됩니다.


## <a name="debug-hello-out-of-memory-error"></a>메모리 부족 오류 hello 디버그

지원 하 고 엔지니어링 팀을 함께 hello 메모리 부족 오류를 일으키는 hello 문제 중 하나는 되었다는 걸 발견 한 [알려진 Apache JIRA hello에 설명 된 문제](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

hello **hive.auto.convert.join.noconditionaltask** hello hive-site.xml 파일 너무 설정 되었으며**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

가능성이 맵 조인 원인은 hello hello Java 힙 공간이의 우리의 메모리 오류가 발생 합니다. Hello 블로그 게시물에 설명 된 대로 [HDInsight의 Hadoop Yarn 메모리 설정을](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx)실행 엔진은 사용 된 hello 사용 되는 힙 공간 Tez toohello Tez 컨테이너를 실제로 속해 있는 경우, 합니다. 다음 이미지 설명 하는 hello Tez 컨테이너 메모리 hello를 참조 하십시오.

![Tez 컨테이너 메모리 다이어그램: Hive 메모리 부족 오류](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

다음 두 가지 메모리 설정을 hello hello 힙에 대 한 hello 컨테이너 메모리 정의 hello 블로그 게시물에서 알 수 있듯이: **hive.tez.container.size** 및 **hive.tez.java.opts**합니다. 경험에 따르면에서 메모리 부족 예외 hello가 아닙니다 hello 컨테이너 크기가 너무 작습니다. Java 힙 크기 (hive.tez.java.opts) hello 너무 작습니다.을 의미 합니다. 메모리 부족 나타날 때마다 tooincrease 시도할 수 있음 **hive.tez.java.opts**합니다. 필요한 경우 tooincrease 해야할 **hive.tez.container.size**합니다. hello **java.opts** 설정은 되어야 약 80%의 **container.size**합니다.

> [!NOTE]
> hello 설정을 **hive.tez.java.opts** 보다 항상 작아야 **hive.tez.container.size**합니다.
> 
> 

D12 컴퓨터에 28GB 메모리에 있으므로 우리 toouse 10GB (10240 MB)의 컨테이너 크기를 결정 하 고 할당 80 %toojava.opts:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

Hello 새 설정을 사용 하 여 hello 쿼리 아래에서 10 분 후에 성공적으로 실행 했습니다.

## <a name="next-steps"></a>다음 단계

OOM 오류가 반드시 의미 hello 컨테이너 크기가 너무 작습니다. 대신, hello 힙 크기 증가 하 고 hello 컨테이너 메모리 크기의 80% 이상 있도록 hello 메모리 설정을 구성 해야 합니다. Hive 쿼리 최적화는 [HDInsight에서 Hadoop에 대한 Hive 쿼리 최적화](hdinsight-hadoop-optimize-hive-query.md)를 참조하세요.
