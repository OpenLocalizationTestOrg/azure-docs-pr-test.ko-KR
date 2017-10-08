---
title: "Azure HDInsight의 Apache Spark에 대 한 aaaManage 리소스 클러스터 | Microsoft Docs"
description: "Toouse 성능 향상을 위해 Azure HDInsight의 Spark 클러스터에 대 한 리소스를 관리 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Azure HDInsight에서 Apache Spark 클러스터용 리소스 관리 

이 문서에서 Ambari UI, YARN UI 및 hello Spark 기록 서버와 같은 tooaccess hello 인터페이스 Spark 클러스터와 연결 된 하는 방법을 배웁니다. 어떻게 tootune hello 최적의 성능을 위해 클러스터 구성에 대 한 배우게 메시지가 표시 됩니다.

**필수 조건:**

Hello 다음이 필요 합니다.

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Hello Ambari 웹 UI를 시작 어떻게 합니까?
1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.
2. Hello Spark 클러스터 블레이드에서 클릭 **대시보드**합니다. 메시지가 표시 되 면 hello Spark 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

    ![Ambari 시작](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Resource Manager 시작")
3. 이 아래와 같이 hello Ambari 웹 UI를 시작 해야 합니다.

    ![Ambari 웹 UI](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari 웹 UI")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Spark 기록 서버 hello을 시작 하는 어떻게 합니까?
1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.
2. Hello에서 블레이드에서 아래에서 클러스터 **빠른 링크**, 클릭 **클러스터 대시보드**합니다. Hello에 **클러스터 대시보드** 블레이드에서 클릭 **Spark 기록 서버**합니다.

    ![Spark 기록 서버](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark 기록 서버")

    메시지가 표시 되 면 hello Spark 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Hello Yarn UI를 시작 어떻게 합니까?
Hello Spark 클러스터에서 현재 실행 중인 hello YARN UI toomonitor 응용 프로그램을 사용할 수 있습니다.

1. Hello 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **YARN**합니다.

    ![YARN UI 시작](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > 또는 hello Ambari UI에서에서 hello YARN UI를 시작할 수 있습니다. hello 클러스터 블레이드에서 toolaunch hello Ambari UI 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다. Ambari UI hello에서 클릭 **YARN**, 클릭 **빠른 링크**, hello 활성 리소스 관리자를 클릭 하 고 클릭 **ResourceManager UI**합니다.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Hello 최적 클러스터 구성 toorun Spark 응용 프로그램 이란?
응용 프로그램 요구 사항에 따라 Spark 구성에 대해 사용할 수 있는 세 hello 키 매개 변수는 `spark.executor.instances`, `spark.executor.cores`, 및 `spark.executor.memory`합니다. 실행자는 Spark 응용 프로그램을 위해 시작된 프로세스입니다. Hello 작업자 노드에서 실행 되며 hello 작업 hello 응용 프로그램에 대 한 책임 toocarry 됩니다. 단일 실행 및 각 클러스터에 대 한 hello 실행자 크기 hello 기본 수는 hello 수 작업자 노드 및 hello 작업자 노드 크기에 따라 계산 됩니다. 에 저장 됩니다 `spark-defaults.conf` hello 클러스터 헤드 노드에 있습니다.

hello 구성 매개 변수 3 개 (hello 클러스터에서 실행 하는 모든 응용 프로그램)에 대 한 hello 클러스터 수준에서 구성할 수 있습니다 또는 에서도 각 개별 응용 프로그램에 지정할 수 있습니다.

### <a name="change-hello-parameters-using-ambari-ui"></a>Ambari UI를 사용 하 여 hello 매개 변수 변경
1. Hello Ambari UI에서에서 클릭 **Spark**, 클릭 **Configs**, 펼친 다음 **사용자 지정 spark 기본값**합니다.

    ![Ambari를 사용하여 매개 변수 설정](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. hello 기본값은 좋은 toohave 4 Spark 응용 프로그램 hello 클러스터에서 동시에 실행 됩니다. 변경할 수 있습니다 이러한 값 hello 사용자 인터페이스에서 아래와 같이 합니다.

    ![Ambari를 사용하여 매개 변수 설정](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. 클릭 **저장** toosave hello 구성 변경 합니다. Hello 페이지의 hello 위쪽 나타납니다 toorestart hello 모든 영향을 받는 서비스입니다. **다시 시작**을 클릭합니다.

    ![서비스 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Jupyter 노트북에서 실행 중인 응용 프로그램에 대 한 hello 매개 변수 변경
Hello Jupyter 노트북에서 실행 중인 응용 프로그램에서는 hello를 사용할 수 있습니다 `%%configure` 매직 toomake hello 구성을 변경 합니다. 이상적으로 코드 첫 번째 셀을 실행 하기 전에 hello 응용 프로그램의 hello 시작 부분에서 이러한 변경 해야 합니다. 이렇게 하면 해당 hello 구성이 적용 된 toohello 리비 세션을 만들 때 가져옵니다. Hello를 사용 해야 hello 응용 프로그램의 이후 단계에서 toochange hello 구성 하려는 경우 `-f` 매개 변수입니다. 그러나 hello에 진행 되는 모든 하므로 실행 하 여 응용 프로그램 손실 됩니다.

아래 hello 조각 toochange Jupyter 실행 중인 응용 프로그램에 대 한 구성을 hello 하는 방법을 보여 줍니다.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

구성 매개 변수를 JSON 문자열로 전달 해야 하며 hello 예에서는 열에 표시 된 것 처럼 hello 매직 후 hello 다음 줄에서 이어야 합니다.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>사용 하 여 전송할 응용 프로그램에 대 한 매개 변수를 변경 hello spark 제출
Toochange 구성 매개 변수를 사용 하 여 전송 된 일괄 처리 응용 프로그램에 대 한 hello 하는 방법의 예는 다음 명령을 `spark-submit`합니다.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>CURL을 사용 하 여 전송할 응용 프로그램에 대 한 hello 매개 변수 변경
다음 명령을 toochange cURL을 사용 하 여 사용 하 여 전송 된 일괄 처리 응용 프로그램에 대 한 구성 매개 변수를 hello 하는 방법의 예시입니다.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Spark Thrift 서버에서 이러한 매개 변수를 변경하려면 어떻게 해야 하나요?
Spark Thrift 서버 제공 JDBC/ODBC 액세스 tooa Spark 클러스터 하며 사용 되는 tooservice Spark SQL 쿼리 합니다. Power BI, Tableau 등과 같은 도구는 Spark Thrift 서버 tooexecute Spark SQL 쿼리로 프로토콜 toocommunicate ODBC를 사용 하 여 Spark 응용 프로그램으로. Spark 클러스터를 만들 때 두 인스턴스의 각 헤드 노드에서 하나 hello Spark Thrift 서버가 시작 됩니다. 각 Spark Thrift 서버 hello YARN UI에서에서 Spark 응용 프로그램으로 표시 됩니다.

Spark Thrift 서버는 동적 실행자 할당 멤버를 사용 하며 따라서 hello `spark.executor.instances` 사용 되지 않습니다. Spark Thrift 서버 대신 사용 하 여 `spark.dynamicAllocation.minExecutors` 및 `spark.dynamicAllocation.maxExecutors` toospecify hello 실행 기 수입니다. 구성 매개 변수를 hello `spark.executor.cores` 및 `spark.executor.memory` 은 toomodify hello 실행자 크기를 사용 합니다. 아래와 같이 이러한 매개 변수를 변경할 수 있습니다.

* Hello 확장 **spark-thrift-sparkconf 고급** 범주 tooupdate hello 매개 변수 `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, 및 `spark.executor.memory`합니다.

    ![Spark Thrift 서버 구성](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Hello 확장 **사용자 지정 spark thrift sparkconf** 범주 tooupdate hello 매개 변수 `spark.executor.cores`합니다.

    ![Spark Thrift 서버 구성](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Spark Thrift 서버 hello의 hello 드라이버 메모리를 변경 하려면 어떻게 해야 합니까?
Spark Thrift 서버 드라이버 메모리는 제공 된 hello hello 헤드 노드의 총 RAM 크기는 14 GB 보다 큰 구성된 too25 %hello 헤드 노드 RAM 크기입니다. 아래와 같이 hello Ambari UI toochange hello 드라이버 메모리 내 구성에 사용할 수 있습니다.

* Hello Ambari UI에서에서 클릭 **Spark**, 클릭 **Configs**, 확장 **spark env 고급**, 다음에 대 한 hello 값을 제공 하 고 **spark_thrift_cmd_opts**.

    ![Spark Thrift 서버 RAM 구성](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>Spark 클러스터와 함께 BI를 사용하지 않습니다. Hello 리소스를 다시 사용지 않습니다는 방법
Spark 동적 할당을 사용 하므로 hello만 thrift 서버에서 사용 하는 리소스가 두 응용 프로그램 마스터 hello에 대 한 hello 리소스입니다. tooreclaim hello 클러스터에서 실행 중인 Thrift 서버 서비스를 hello 이러한 리소스를 중지 해야 합니다.

1. Hello 왼쪽된 창에서 hello Ambari UI에서에서 클릭 **Spark**합니다.
2. Hello 다음 페이지에서 클릭 **Spark Thrift 서버**합니다.

    ![Thrift 서버 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Spark Thrift 서버가 실행 중인 어떤 hello hello 두 headnodes를 표시 되어야 합니다. Hello headnodes 중 하나를 클릭 합니다.

    ![Thrift 서버 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. 다음 페이지 hello 해당 헤드 노드에에서 실행 중인 모든 hello 서비스를 나열 합니다. Hello 목록에서 hello 드롭 다운 단추 다음 tooSpark Thrift 서버를 클릭 한 다음 클릭 **중지**합니다.

    ![Thrift 서버 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. 다른 헤드 노드에 hello에서 이러한 단계를 반복 합니다.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>내 Jupyter Notebook이 예상대로 실행되지 않습니다. Hello 서비스를 다시 시작할 수는 방법
위와 같이 hello Ambari 웹 UI를 시작 합니다. Hello 왼쪽된 탐색 창에서 클릭 **Jupyter**, 클릭 **서비스 작업**, 클릭 하 고 **모든 다시 시작**합니다. 모든 hello headnodes에 hello Jupyter service가 시작 됩니다.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>리소스가 부족한지 어떻게 알 수 있나요?
위와 같이 hello Yarn UI를 시작 합니다. Hello 화면 위로 클러스터 메트릭 표에 값을 확인 **사용 메모리** 및 **총 메모리** 열입니다. Hello 2 값이 매우 유사 하지 될 충분 한 리소스 toostart hello 다음 응용 프로그램입니다. hello에 마찬가지 toohello **VCores 사용** 및 **VCores 총** 열입니다. 또한 hello 주 보기에 없는 경우 응용 프로그램에 그대로 유지 **"승인 됨"** 상태 및으로 전환 되지 **실행** 나 **실패** 상태 이면이 수도 있는 것일 수 에 충분 한 리소스 toostart를 얻을 수 없습니다.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>실행 중인을 kill 어떻게 리소스를 응용 프로그램 toofree?
1. Hello 왼쪽된 패널에서 hello Yarn UI 클릭 **실행**합니다. 실행 중인 응용 프로그램의 hello 목록에서 응용 프로그램 toobe hello 종료 하 고 hello에서 클릭 결정 **ID**합니다.

    ![App1 종료](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "App1 종료")

2. 클릭 **응용 프로그램을 중지** hello 오른쪽 위 모퉁이 클릭 한 다음 **확인**합니다.

    ![App2 종료](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "App2 종료")

## <a name="see-also"></a>참고 항목
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>데이터 분석가

* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석](hdinsight-spark-analyze-application-insight-logs.md)
* [분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Spark 개발자

* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
