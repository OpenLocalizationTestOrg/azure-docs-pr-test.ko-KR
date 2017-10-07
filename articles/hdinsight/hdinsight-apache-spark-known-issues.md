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
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>HDInsight의 Apache Spark 클러스터에 대한 알려진 문제

이 문서는의 알려진 문제 hello HDInsight Spark 공개 미리 보기에 대 한 모든 hello 추적 합니다.  

## <a name="livy-leaks-interactive-session"></a>Livy 누수 대화형 세션
리비 시작 될 때 (Ambari 또는 tooheadnode 0 가상 컴퓨터를 다시 부팅 때문) 여전히 활성 대화형 세션으로 대화형 작업 세션 누출 됩니다. 이 때문에 새로운 작업 있습니다 hello 수락 됨 상태에서에서 멈출 하 고 시작할 수 없습니다.

**해결 방법:**

다음 프로시저 tooworkaround hello 문제 hello를 사용 합니다.

1. 헤드 노드로 ssh합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. 다음 명령은 toofind hello 응용 프로그램 실행된 hello hello 대화형 작업의 Id 리비를 통해 시작 합니다. 
   
        yarn application –list
   
    hello 기본 작업 이름은 됩니다 리비 hello 작업 hello에 대 한 지정 된 이름이 없으면 명시적 리비 대화형 세션으로 시작 된 경우 Jupyter 노트북에 의해 시작 리비 세션 hello 작업 이름은 remotesparkmagics_ *로 시작 됩니다. 
3. 다음 명령은 tookill hello 이러한 작업을 실행 합니다. 
   
        yarn application –kill <Application ID>

새 작업 실행이 시작됩니다. 

## <a name="spark-history-server-not-started"></a>Spark 기록 서버가 시작되지 않음
클러스터가 만들어진 후 Spark 기록 서버가 자동으로 시작되지 않습니다.  

**해결 방법:** 

Ambari에서 hello 기록 서버를 수동으로 시작 합니다.

## <a name="permission-issue-in-spark-log-directory"></a>Spark 로그 디렉터리에 대한 사용 권한 문제
Hdiuser가 spark-submit 인 작업을 제출 하는 경우 오류 java.io.FileNotFoundException 있습니다: /var/log/spark/sparkdriver_hdiuser.log (사용 권한이 거부 되었습니다) 및 hello 드라이버 로그 기록 되지 않습니다. 

**해결 방법:**

1. Hdiuser toohello Hadoop 그룹을 추가 합니다. 
2. 클러스터를 만든 후에 /var/log/spark에 777 권한을 제공합니다. 
3. Ambari toobe 디렉터리 777 사용 권한과 함께 사용 하는 hello spark 로그 위치를 업데이트 합니다.  
4. sudo로 spark-제출을 실행합니다.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Spark-Phoenix 커넥터가 지원되지 않음

현재 hello 피닉스 Spark 커넥터 HDInsight Spark 클러스터와 지원 되지 않습니다.

**해결 방법:**

Hello HBase Spark 커넥터를 대신 사용 해야 합니다. 에 대 한 참조 [어떻게 toouse HBase Spark 커넥터](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/)합니다.

## <a name="issues-related-toojupyter-notebooks"></a>TooJupyter 전자 필기장 관련 된 문제
다음은 몇 가지 알려진된 문제 관련된 tooJupyter 전자 필기장입니다.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>파일 이름에 ASCII가 아닌 문자가 있는 Notebook
Spark HDInsight 클러스터에서 사용할 수 있는 Jupyter Notebook은 파일 이름에 ASCII가 아닌 문자를 포함할 수 없습니다. 자동으로 실패 합니다 tooupload hello ASCII가 아닌 파일 이름 Jupyter UI를 통해 파일을 시도 하는 경우 (즉, Jupyter hello 파일을 업로드 하면 수 없을 하지만 하거나 표시 되는 오류를 발생 하지 않습니다 것). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>더 큰 Notebook을 로드하는 중 오류
더 큰 Notebook을 로드할 때 **`Error loading notebook`** 오류가 표시될 수 있습니다.  

**해결 방법:**

이 오류가 발생했다고 해서 데이터가 손상되거나 손실된 것은 아닙니다.  전자 필기장은 여전히 디스크에서 `/var/lib/jupyter`, hello 클러스터 tooaccess에 SSH를 사용 하면 해당 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

SSH를 사용 하 여 toohello 클러스터를 연결 하 고 나면 hello 전자 필기장의 중요 한 데이터 백업 tooprevent hello 손실로 전자 필기장 (SCP 또는 WinSCP 사용) 하 여 클러스터 tooyour 로컬 컴퓨터에서 복사할 수 있습니다. 그런 다음 SSH 터널 포트 8001 tooaccess Jupyter에서 프로그램 헤드 노드에 hello 게이트웨이 통과 하지 않고 있습니다.  여기에서 있습니다 수 전자 필기장의 hello 출력 지우고 다시 저장 toominimize hello 노트북의 크기입니다.

tooprevent이이 오류 이후 몇 가지 모범 사례를 수행 해야 하는 hello에 발생에서 합니다.

* 중요 한 tookeep hello 노트북 크기가 작은 경우 다시 전송 되기 tooJupyter hello 노트북에서 유지 되는 Spark 작업에서 출력 합니다.  Jupyter에 대 한 모범 사례를 실행 하는 일반 tooavoid 중인 `.collect()` on 큰 RDD 또는 데이터 프레임; RDD의 내용을 toopeek 하려는 경우를 고려해 야 실행 `.take()` 또는 `.sample()` 출력이 너무 커서 함을 알 수 있도록 합니다.
* 또한, 노트북을 저장할 때 선택을 취소 모든 출력을 셀 tooreduce hello 크기입니다.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>노트북 초기 시작이 예상보다 오래 걸리는 경우
Jupyter Notebook에서 Spark 매직을 사용한 첫 번째 코드 문의 경우 1분 이상이 걸릴 수 있습니다.  

**설명:**

이 첫 번째 코드 셀 hello를 실행할 때 발생 합니다. Hello 백그라운드에서이 세션 구성 및 Spark, SQL를 시작 하 고 하이브 컨텍스트가 설정 됩니다. 이러한 컨텍스트를 설정한 후 hello 첫 번째 문을 실행 하 고 hello 인상을 hello 문을 걸린 시간이 오래 toocomplete를 제공 합니다.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Hello 세션을 만드는 Jupyter 노트북 시간 제한
Spark 클러스터 리소스가 부족할 때 Spark hello 및 hello Jupyter 노트북에 Pyspark 커널 toocreate hello 세션 중 시간이 초과 됩니다. 

**해결 방법:** 

1. 다음과 같은 방법으로 Spark 클러스터의 리소스를 확보합니다.
   
   * 다른 스파크 전자 필기장 toohello 이동 닫기 및 중단 메뉴 하거나 hello 노트북 탐색기에서 시스템 종료를 클릭 하 여를 중지 하는 중입니다.
   * YARN에서 다른 Spark 응용 프로그램을 중지합니다.
2. Hello 노트북을 toostart 하려던 다시 시작 합니다. 충분 한 리소스는 세션을 지금 toocreate 있습니다 사용할 수 해야 합니다.

## <a name="see-also"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

