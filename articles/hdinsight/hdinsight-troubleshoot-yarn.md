---
title: "Azure HDInsight를 사용 하 여 YARN aaaTroubleshoot | Microsoft Docs"
description: "Apache Hadoop YARN 및 Azure HDInsight 작업에 대 한 toocommon 질문을 답변을 가져옵니다."
keywords: "Azure HDInsight, YARN, FAQ, 문제 해결 가이드, 일반적인 질문"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Azure HDInsight를 사용한 YARN 문제 해결

Apache Ambari에 Apache Hadoop YARN 페이로드를 작업할 때 hello 상위 문제와 그 해결 방법에 알아봅니다.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>클러스터에서 새 YARN 큐를 만드는 방법


### <a name="resolution-steps"></a>해결 단계: 

사용 하 여 hello 다음의에서 단계를 Ambari toocreate 새 YARN 큐를 다음 hello 용량 할당 모든 hello 큐 간에 균형을 조정 합니다. 

이 예제에서는 두 개의 기존 큐 (**기본** 및 **thriftsvr**) 둘 다에서 50% 용량 too25% 용량에 새 큐 (spark) 50% 용량 hello 제공 변경 됩니다.
| 큐 | 용량 | 최대 용량 |
| --- | --- | --- | --- |
| 기본값 | 25% | 50% |
| thrftsvr | 25% | 50% |
| spark | 50% | 50% |

1. 선택 hello **Ambari 뷰** 아이콘을 선택한 후 hello grid 패턴입니다. 다음으로, **YARN 큐 관리자**를 선택합니다.

    ![Hello Ambari 뷰 아이콘을 선택 합니다.](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. 선택 hello **기본** 큐입니다.

    ![Hello 기본 큐를 선택 합니다.](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Hello에 대 한 **기본** 큐, hello 변경 **용량** too25 50% %에서입니다. Hello에 대 한 **thriftsvr** 큐, hello 변경 **용량** too25%입니다.

    ![Hello 용량 too25 %hello 기본 및 thriftsvr 큐에 대 한 변경](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. 새 큐 toocreate 선택 **추가 큐**합니다.

    ![큐 추가 선택](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. 이름 hello 새 큐입니다.

    ![이름 hello 큐 Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Hello 둡니다 **용량** 값 50% 및 선택 hello **작업** 단추입니다.

    ![Hello 동작 단추를 선택 합니다.](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. **큐 저장 및 새로 고침**을 선택합니다.

    ![큐 저장 및 새로 고침 선택](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

이러한 변경 내용은 즉시 hello YARN 스케줄러 UI에 표시 됩니다.

### <a name="additional-reading"></a>추가 참조 자료

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>클러스터에서 YARN 로그를 다운로드하는 방법


### <a name="resolution-steps"></a>해결 단계: 

1. SSH (보안 셸) 클라이언트를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다. 자세한 내용은 [더 보기](#additional-reading-2)를 참조하세요.

2. 현재 실행 중인 hello YARN 응용 프로그램의 응용 프로그램 Id를 hello 모든 toolist hello 다음 명령을 실행 합니다.

    ```apache
    yarn top
    ```
    hello Id에에서 나열 됩니다 hello **APPLICATIONID** 열입니다. Hello에서 로그를 다운로드할 수 **APPLICATIONID** 열입니다.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. 모든 응용 프로그램 마스터에 대 한 toodownload YARN 컨테이너 로그 hello 다음 명령을 사용 합니다.
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    amlogs.txt라는 로그 파일이 만들어집니다. 

4. master에 대 한 유일한 hello 최신 응용 프로그램, toodownload YARN 컨테이너 로그 hello 다음 명령을 사용 합니다.

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    latestamlogs.txt라는 로그 파일이 만들어집니다. 

4. 첫 번째 두 응용 프로그램 마스터 hello에 대 한 toodownload YARN 컨테이너 로그 hello 다음 명령을 사용 합니다.

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    first2amlogs.txt라는 로그 파일이 만들어집니다. 

5. toodownload 모든 YARN 컨테이너 로그를 사용 하 여 다음 명령을 hello:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    logs.txt라는 로그 파일이 만들어집니다. 

6. toodownload hello YARN 컨테이너 로그에서 특정 컨테이너로, 다음 명령을 사용 하 여 hello:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    containerlogs.txt라는 로그 파일이 만들어집니다.

### <a name="additional-reading-2"></a>추가 참조 자료

- [SSH를 사용 하 여 tooHDInsight (Hadoop) 연결](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN 개념 및 응용 프로그램](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







