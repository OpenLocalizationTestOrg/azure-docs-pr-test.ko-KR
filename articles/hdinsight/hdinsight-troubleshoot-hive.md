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
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Azure HDInsight를 사용한 Hive 문제 해결

Apache Hive 페이로드 Apache Ambari에서 작업할 때는 hello 상위 질문과 그 해결 방법에 알아봅니다.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Hive metastore를 내보내고 다른 클러스터로 가져오는 방법


### <a name="resolution-steps"></a>해결 단계:

1. SSH (보안 셸) 클라이언트를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다. 자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.

2. Hello tooexport hello metastore 원하는 hello HDInsight 클러스터에서 다음 명령을 실행 합니다.

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  이 명령은 allatables.sql이라는 파일을 생성합니다.

3. Hello 파일 alltables.sql toohello 새 HDInsight 클러스터에 복사한 다음 hello 다음 명령을 실행 합니다.

  ```apache
  hive -f alltables.sql
  ```

hello 해결 단계에 hello 코드 hello 새 클러스터에서 경로 데이터 hello 이전 클러스터에서 hello 데이터 경로와 동일한 hello를 가정 합니다. Hello 데이터 경로가 다른 경우 생성 된 hello alltables.sql 파일 tooreflect를 변경 내용을 수동으로 편집할 수 있습니다.

### <a name="additional-reading"></a>추가 참조 자료

- [SSH를 사용 하 여 tooan HDInsight 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>클러스터에서 Hive 로그를 찾는 방법

### <a name="resolution-steps"></a>해결 단계:

1. SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다. 자세한 내용은 **더 보기**를 참조하세요.

2. tooview 하이브 클라이언트 로그 hello 다음 명령을 사용 합니다.

  ```apache
  /tmp/<username>/hive.log 
  ```

3. tooview 하이브 metastore 로그, 다음 명령을 사용 하 여 hello:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver 로그 hello 다음 명령을 사용 합니다.

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>추가 참조 자료

- [SSH를 사용 하 여 tooan HDInsight 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Hello 클러스터에서 특정 구성으로 하이브 셸을 시작 하는 어떻게 합니까

### <a name="resolution-steps"></a>해결 단계:

1. Hello 하이브 shell을 시작 하면 구성 키-값 쌍을 지정 합니다. 자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist 하이브 shell 사용 하 여 hello 뒤의 모든 유효한 구성 명령 수 있습니다.

  ```apache
  hive> set;
  ```

  예를 들어 hello hello 콘솔에서 사용 하도록 설정 하는 디버그 로깅과 함께 toostart 하이브 명령 셸에 다음을 사용 합니다.

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>추가 참조 자료

- [Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)(Hive 구성 속성)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>클러스터 중요 경로에서 Tez DAG 데이터를 분석하는 방법


### <a name="resolution-steps"></a>해결 단계:
 
1. 클러스터에 중요 한 그래프에는 Apache Tez tooanalyze 방향성 비순환 그래프 (DAG), SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다. 자세한 내용은 [더 보기](#additional-reading-end)를 참조하세요.

2. 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist Tez DAG tooanalyze를 사용 하는 일 수 있는 다른 분석기 hello 다음 명령을 사용 합니다.

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Hello 첫 번째 인수로 예제 프로그램을 제공 해야 합니다.

  올바른 프로그램의 이름은 다음과 같습니다.
    - **ContainerReuseAnalyzer**: DAG에 컨테이너 다시 사용 세부 정보를 출력합니다.
    - **CriticalPath**: DAG의 hello 요주의 경로 찾기
    - **LocalityAnalyzer**: DAG에 위치 정보를 인쇄합니다.
    - **ShuffleTimeAnalyzer**: DAG에 hello 순서 섞기 시간 정보를 분석 합니다.
    - **SkewAnalyzer**: DAG에 hello 시간차 세부 정보를 분석 합니다.
    - **SlowNodeAnalyzer**: DAG에 노드 정보를 출력합니다.
    - **SlowTaskIdentifier**: DAG에 느린 작업 정보를 출력합니다.
    - **SlowestVertexAnalyzer**: DAG에 가장 느린 꼭지점 정보를 출력합니다.
    - **SlowNodeAnalyzer**: DAG에 분산 정보를 출력합니다.
    - **TaskConcurrencyAnalyzer**: DAG에서 hello 작업 동시성 세부 정보를 인쇄 합니다.
    - **VertexLevelCriticalPathAnalyzer**: 찾기 hello DAG에 꼭 짓 점 수준에서 중요 한 경로


### <a name="additional-reading"></a>추가 참조 자료

- [SSH를 사용 하 여 tooan HDInsight 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>클러스터에서 Tez DAG 데이터를 다운로드하는 방법


#### <a name="resolution-steps"></a>해결 단계:

두 가지가 toocollect hello Tez DAG 데이터:

- 명령줄 hello:
 
    SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다. Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Hello Ambari Tez 보기를 사용 합니다.
   
  1. TooAmbari 이동 합니다. 
  2. Hello hello 오른쪽 위 모퉁이에 타일 아이콘) (아래에 있는 이동 tooTez 보기. 
  3. Hello tooview 원하는 DAG를 선택 합니다.
  4. **데이터 다운로드**를 선택합니다.

### <a name="additional-reading-end"></a>추가 참조 자료

[SSH를 사용 하 여 tooan HDInsight 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)






