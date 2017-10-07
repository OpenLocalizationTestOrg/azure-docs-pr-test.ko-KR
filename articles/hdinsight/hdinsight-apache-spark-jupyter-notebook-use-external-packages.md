---
title: "Azure HDInsight의 Spark에 Jupyter와 사용자 지정 Maven 패키지 aaaUse | Microsoft Docs"
description: "HDInsight Spark와 함께 사용할 수 있는 tooconfigure Jupyter 노트북 toouse 사용자 지정 Maven 패키지를 클러스터 하는 방법에 대해 단계별로 설명 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>HDInsight의 Apache Spark 클러스터에서 Jupyter Notebook과 함께 외부 패키지 사용
> [!div class="op_single_selector"]
> * [셀 매직 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [스크립트 작업 사용](hdinsight-apache-spark-python-package-installation.md)
>
>

자세한 방법을 tooconfigure HDInsight toouse 외부에 Apache Spark 클러스터에서 Jupyter 노트북 커뮤니티 제공 **maven** 하지 않은 패키지를 hello 클러스터에 기본적으로 포함 합니다. 

Hello를 검색할 수 있습니다 [Maven 리포지토리](http://search.maven.org/) 사용할 수 있는 패키지의 전체 목록은 hello에 대 한 합니다. 다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다. 예를 들어 커뮤니티 제공 패키지의 전체 목록은 [Spark 패키지](http://spark-packages.org/)에서 사용할 수 있습니다.

이 문서에서는 살펴보겠습니다 어떻게 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter 노트북을 사용 하 여 패키지 합니다.



## <a name="prerequisites"></a>필수 조건
Hello 다음이 필요 합니다.

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="use-external-packages-with-jupyter-notebooks"></a>Jupyter 노트북에서 외부 패키지 사용
1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.   
2. Hello Spark 클러스터 블레이드에서 클릭 **빠른 링크**, 한 다음 hello **클러스터 대시보드** 블레이드에서 클릭 **Jupyter 노트북**합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

    > [!NOTE]
    > 또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. 새 Notebook을 만듭니다. **새로 만들기**를 클릭한 후 **Spark**를 클릭합니다.
   
    ![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "새 Jupyter 노트북 만들기")

4. 새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다. Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.
   
    ![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")

5. Hello를 사용 하 여 `%%configure` 매직 tooconfigure hello 노트북 toouse 외부 패키지 합니다. 외부 패키지를 사용 하는 노트북에서 hello 호출 되었는지 확인 `%%configure` hello 첫 번째 코드 셀에서 매직 합니다. 이렇게 하면 해당 hello 커널 hello 세션이 시작 되기 전에 구성 된 toouse hello 패키지입니다.

    >[!IMPORTANT] 
    >Hello hello 첫 번째 셀에 tooconfigure hello 커널 기억나지 않는 경우 사용할 수 있습니다 `%%configure` hello로 `-f` 매개 변수를 있었으나에 hello 세션 다시 시작 되 고 모든 진행률 손실 됩니다.

    | HDInsight 버전 | 명령 |
    |-------------------|---------|
    |HDInsight 3.3 및 HDInsight 3.4용 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | HDInsight 3.5용 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. 위의 코드 조각 hello Maven 중앙 리포지토리에 hello 외부 패키지에 대 한 hello maven 좌표는 필요합니다. 이 코드 조각 `com.databricks:spark-csv_2.10:1.4.0` hello maven 좌표에 대 한 **spark csv** 패키지 합니다. 패키지에 대 한 hello 좌표를 구성 하는 방법을 다음과 같습니다.
   
    a. Maven 리포지토리 hello hello 패키지를 찾습니다. 이 자습서에서는 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)를 사용합니다.
   
    b. 에 대 한 hello 값을 수집 hello 리포지토리에서 **GroupId**, **의 ArtifactId**, 및 **버전**합니다. Hello 값을 수집 하 여 클러스터와 일치 하는지 확인 합니다. 이 경우 Scala 2.10 및 Spark 1.4.0 패키지를 사용 하는 것 이지만 클러스터의 hello 적절 한 Scala 또는 Spark 버전에 대 한 tooselect 서로 다른 버전을 할 수 있습니다. 확인할 수 있습니다 hello Scala 버전 클러스터에서 실행 하 여 `scala.util.Properties.versionString` hello Spark Jupyter 커널 또는 Spark 제출 합니다. 확인할 수 있습니다 hello Spark 버전 클러스터에서 실행 하 여 `sc.version` Jupyter 노트북에서 합니다.
   
    ![Jupyter Notebook에서 외부 패키지 사용](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Jupyter Notebook에서 외부 패키지 사용")
   
    c. 콜론으로 구분 하는 hello 3 값 연결 (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Hello를 사용 하 여 hello 코드 셀 실행 `%%configure` 매직 합니다. 이렇게 하면 hello 기본 리비 세션 toouse hello 패키지 사용자가 제공한 구성 됩니다. Hello 전자 필기장의 후속 셀 hello에에서 아래와 같이 hello 패키지를 지금 사용할 수 있습니다.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Hello 조각을 실행할 수 있습니다, tooview, 아래 그림과 같이 hello hello 데이터 프레임에서 데이터 단계에서 만든 hello 이전 합니다.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>참고 항목
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

* [HDInsight Linux의 Apache Spark 클러스터에서 Jupyter 노트북과 함께 외부 python 패키지 사용](hdinsight-apache-spark-python-package-installation.md)
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

