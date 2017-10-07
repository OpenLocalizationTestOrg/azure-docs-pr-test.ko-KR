---
title: "Azure HDInsight의 Spark에 Jupyter 노트북에 대 한 aaaKernels 클러스터 | Microsoft Docs"
description: "Azure HDInsight의 Spark 클러스터와 함께 사용할 수 있는 Jupyter 노트북에 대 한 hello PySpark, PySpark3, 및 Spark 커널에 알아봅니다."
keywords: "spark의 jupyter 노트북, jupyter spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Azure HDInsight에서 Spark 클러스터의 Jupyter 노트북에 대한 커널 

HDInsight Spark 클러스터 응용 프로그램을 테스트 하기 위한 Spark에 hello Jupyter 노트북으로 사용할 수 있는 커널을 제공 합니다. 커널은 코드를 실행하고 해석하는 프로그램입니다. hello 세 커널 됩니다.

- **PySpark** - Python2에서 작성한 응용 프로그램용
- **PySpark3** - Python3에서 작성한 응용 프로그램용
- **Spark** - Scala에서 작성한 응용 프로그램용

이 문서에서는 설명 어떻게 toouse 이러한 커널 및 어설션을 사용 하 여 hello 이점입니다.

## <a name="prerequisites"></a>필수 조건

* HDInsight의 Apache Spark 클러스터. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Spark HDInsight에서 Jupyter 노트북 만들기

1. Hello에서 [Azure 포털](https://portal.azure.com/), 클러스터를 엽니다.  참조 [목록 및 표시 클러스터](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) hello 지침에 대 한 합니다. hello 클러스터에서 새 포털 블레이드가 열립니다.

2. Hello에서 **빠른 링크** 섹션에서 클릭 **클러스터 대시보드** tooopen hello **클러스터 대시보드** 블레이드입니다.  표시 되지 않으면 **빠른 링크**, 클릭 **개요** hello 블레이드에서 hello 왼쪽된 메뉴에서 합니다.

    ![Spark의 Jupyter 노트북](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Spark의 Jupyter 노트북") 

3. **Jupyter Notebook**을 클릭합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.
   
   > [!NOTE]
   > 또한 hello Jupyter 노트북 열어 hello 브라우저의 URL을 따라 하 여 Spark 클러스터에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. 클릭 **새로**, 다음 중 하나를 클릭 하 고 **Pyspark**, **PySpark3**, 또는 **Spark** toocreate 노트북 합니다. Scala 응용 프로그램에 대 한 hello Spark 커널, Python2 응용 프로그램에 대 한 PySpark 커널 및 PySpark3 커널 Python3에 사용 합니다.
   
    ![Spark의 Jupyter 노트북에 대한 커널](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Spark의 Jupyter 노트북에 대한 커널") 

4. 선택한 hello 커널 노트북이 열립니다.

## <a name="benefits-of-using-hello-kernels"></a>Hello 커널에서 사용의 이점

다음은 새 커널 hello를 사용 하 여 HDInsight Spark 클러스터에서 Jupyter 노트북으로의 몇 가지 이점입니다.

- **컨텍스트를 미리 설정합니다**. 와 **PySpark**, **PySpark3**, 또는 hello **Spark** 커널, 않아도 tooset hello Spark 또는 Hive 컨텍스트 명시적으로 응용 프로그램 사용을 시작 하기 전에. 이러한 컨텍스트는 기본적으로 사용할 수 있습니다. 이러한 컨텍스트는 다음과 같습니다.
   
   * **sc** - Spark 컨텍스트용
   * **sqlContext** - Hive 컨텍스트용

    따라서 tooset hello 컨텍스트에 따라 hello 같은 toorun 문이 필요가 없습니다.

        sc = SparkContext('yarn-client')    sqlContext = HiveContext(sc)

    대신, 직접 사용할 수 있습니다 hello 사전 응용 프로그램에서 컨텍스트를 설정 합니다.

- **매직 셀**입니다. hello PySpark 커널 제공 일부 미리 정의 된 "마법"으로 호출할 수 있는 특수 명령을 `%%` (예를 들어 `%%MAGIC` <args>). 여러 줄의 콘텐츠를 허용 하는 코드 셀에 첫 번째 단어 hello를 hello 매직 명령 합니다. hello 매직 단어 hello 셀에 첫 번째 단어 hello 이어야 합니다. Hello 매직, 짝수 메모 하기 전에 아무 것도 추가 하면 오류가 발생 합니다.     매직에 대한 자세한 내용은 [여기](http://ipython.readthedocs.org/en/stable/interactive/magics.html)를 참조하세요.
   
    hello 다음 표에 hello 다른 마법 hello 커널을 통해 사용할 수 있습니다.

   | 매직 | 예 | 설명 |
   | --- | --- | --- |
   | help |`%%help` |예제 및 설명과 함께 모든 hello 사용 가능한 마법 목차를 생성합니다. |
   | info |`%%info` |현재 리비 끝점 hello에 대 한 출력 세션 정보 |
   | 구성 |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |세션을 만들기 위한 hello 매개 변수를 구성 합니다. force 플래그가 hello (-f)는 필수 세션을 이미 만든 경우를 통해 해당 hello 세션을 삭제 하 고 다시 만들어집니다. 유효한 매개 변수 목록은 [Livy의 POST /sessions Request Body](https://github.com/cloudera/livy#request-body) 를 참조하세요. 매개 변수를 JSON 문자열로 전달 해야 하며 hello 예에서는 열에 표시 된 것 처럼 hello 매직 후 hello 다음 줄에서 이어야 합니다. |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |SqlContext hello에 대 한 하이브 쿼리를 실행합니다. 경우 hello `-o` 매개 변수를 전달, hello 쿼리의 hello 결과 hello에서 유지 되 % %로 로컬 Python 컨텍스트는 [팬더](http://pandas.pydata.org/) 데이터 프레임입니다. |
   | local |`%%local`<br>`a=1` |다음 줄의 모든 hello 코드가 로컬로 실행 됩니다. 코드를 사용 하는 hello 커널에 관계 없이 올바른 Python2 코드 여야 합니다. 따라서 선택한 경우에 **PySpark3** 또는 **Spark** hello를 사용 하는 경우 hello 노트북을 만드는 동안 커널 `%%local` 셀에 매직, 해당 셀만 유효한 Python2 코드가 있어야... |
   | 로그 |`%%logs` |출력은 hello 현재 리비 세션에 대 한 로그를 hello 합니다. |
   | delete |`%%delete -f -s <session number>` |Hello 현재 리비 끝점의 특정 세션을 삭제합니다. 참고 hello 커널 자체에 대 한 시작 된 hello 세션을 삭제할 수 없습니다. |
   | cleanup |`%%cleanup -f` |Hello 현재 리비 끝점의 경우이 전자 필기장의이 세션을 포함 하 여 모든 hello 세션을 삭제 합니다. hello force 플래그-f는 필수입니다. |

   > [!NOTE]
   > 또한 toohello 마법 추가 hello PySpark 커널에서 hello를 사용할 수도 있습니다 [기본 제공 IPython 마법](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics)를 포함 하 여 `%%sh`합니다. Hello를 사용할 수 있습니다 `%%sh` 매직 toorun 스크립트와의 hello 클러스터 헤드 노드에 코드 블록입니다.
   >
   >
2. **자동 시각화**. hello **Pyspark** 커널 hello 출력의 Hive 및 SQL 쿼리를 자동으로 시각화 합니다. 테이블, 원형, 선, 영역, 막대를 포함하여 다양한 시각화 형식 중에서 선택할 수 있습니다.

## <a name="parameters-supported-with-hello-sql-magic"></a>Hello로 지원 되는 매개 변수 %%sql 매직
hello `%%sql` 매직 toocontrol hello 종류의 쿼리를 실행할 때 나타나는 출력을 사용할 수 있는 다른 매개 변수를 지원 합니다. 다음 표에서 hello hello 출력을 나열 합니다.

| 매개 변수 | 예 | 설명 |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |이 매개 변수 toopersist hello hello 쿼리의 결과 사용 하 여 hello에 % % 로컬 Python 컨텍스트로는 [팬더](http://pandas.pydata.org/) 데이터 프레임입니다. hello hello 데이터 프레임 변수 이름이 hello 변수 이름을 지정 합니다. |
| -q |`-q` |Hello 셀에 대 한이 tooturn 시각화 off를 사용 합니다. Tooauto 하지 않으려면-셀의 hello 콘텐츠를 시각화 하 고 원하는 toocapture을 데이터 프레임으로 사용 하 여 `-q -o <VARIABLE>`합니다. Hello 결과 캡처하지 않고 tooturn 시각화 해제 하려는 경우 (같은 SQL 쿼리 실행에 대 한 예를 들어는 `CREATE TABLE` 문)를 사용 하 여 `-q` 지정 하지 않고는 `-o` 인수입니다. |
| -m |`-m <METHOD>` |여기서 **METHOD**는 **take** 또는 **sample**(기본값: **take**)입니다. Hello 메서드가 **걸릴**, hello 커널 MAXROWS (이 표의 뒷부분에서 설명)로 지정 된 hello 결과 데이터 집합의 hello 위에서 요소를 선택 합니다. Hello 메서드가 **샘플**, hello 커널 너무에 따라 hello 데이터 집합의 요소를 무작위로 샘플링`-r` 매개 변수를이 테이블에 다음에 설명 합니다. |
| -r |`-r <FRACTION>` |여기서 **FRACTION**은 0.0과 1.0 사이의 부동 소수점 숫자입니다. Hello SQL 쿼리를 위한 샘플 메서드가 hello 이면 `sample`, hello 커널 hello 요소 자동으로 설정 하는 hello 결과의 지정 된 비율 hello를 무작위로 샘플링 합니다. 예를 들어 hello 인수를 갖는 SQL 쿼리를 실행 하는 경우 `-m sample -r 0.01`, hello 결과 행의 1% 임의로 샘플링 됩니다. |
| -n |`-n <MAXROWS>` |**MAXROWS** 는 정수 값입니다. hello 커널 hello 출력 행 수를 너무 제한**MAXROWS**합니다. 경우 **MAXROWS** 은 음수와 같은 **-1**, hello hello 결과 집합의 행 수가 제한 되지 않습니다. |

**예제:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

위의 hello 문은 다음 hello지 않습니다.

* **hivesampletable**에서 모든 레코드를 선택합니다.
* -q를 사용하기 때문에 자동 시각화를 해제합니다.
* 사용 하므로 `-m sample -r 0.1 -n 500` hello hivesampletable의 hello 행 중 10%를 무작위로 샘플링 및 제한을 hello hello 결과 집합 too500 행의 크기입니다.
* 마지막으로 사용 하기 때문에 `-o query2` 라는 데이터 프레임이에 한 hello 출력을 저장할지 **query2**합니다.

## <a name="considerations-while-using-hello-new-kernels"></a>새 커널 hello를 사용 하는 동안 고려 사항

를 사용 하면 어떤 커널 hello 클러스터 리소스를 소비 hello 전자 필기장 실행을 종료 합니다.  이러한 커널 hello 컨텍스트는 미리 설정 때문에 단순히 hello 전자 필기장 종료 hello 컨텍스트를 중단 하지 않습니다 하 고 따라서 hello 클러스터 리소스 계속 toobe 사용 합니다. 일반적으로는 toouse hello **닫고 중단** hello 노트북에서 옵션 **파일** hello 컨텍스트 해당 프로세스를 중지 하는 hello 노트북을 사용 하 여 작업이 완료 되 고 다음 종료 되거나 hello 전자 필기장 메뉴.     

## <a name="show-me-some-examples"></a>몇 가지 예제 보기

Jupyter 노트북을 열 때 hello 루트 수준에서 사용할 수 있는 두 개의 폴더를 참조 합니다.

* hello **PySpark** 폴더에 샘플 전자 필기장을 사용 하 여 hello 새 **Python** 커널 합니다.
* hello **Scala** 폴더에 샘플 전자 필기장을 사용 하 여 hello 새 **Spark** 커널 합니다.

Hello를 열 수 **00-[읽기 나 처음] Spark 매직 커널 기능** hello에서 노트북 **PySpark** 또는 **Spark** 사용할 수 있는 다른 마법 hello에 대 한 폴더 toolearn 합니다. 사용할 수 있습니다 어떻게 hello 두 폴더 toolearn에서 사용할 수 있는 다른 샘플 전자 필기장 hello tooachieve 다양 한 시나리오를 Jupyter 노트북을 사용 하 여 HDInsight Spark 클러스터로 합니다.

## <a name="where-are-hello-notebooks-stored"></a>Hello 전자 필기장의 저장 위치

Jupyter 노트북 hello hello 클러스터와 연결 된 toohello 저장소 계정을 저장 **/HdiNotebooks** 폴더입니다.  노트북, 텍스트 파일 및 Jupyter 내에서 만드는 폴더는 hello 저장소 계정에서 액세스할 수입니다.  예를 들어, Jupyter toocreate 폴더를 사용 하는 경우 **myfolder** 와 노트북 **myfolder/mynotebook.ipynb**에서 해당 노트북에 액세스할 수 있습니다 `/HdiNotebooks/myfolder/mynotebook.ipynb` hello 저장소 계정 내에서.  hello 역방향는 true 이면 즉, tooyour 저장소 계정에서 직접 노트북을 업로드 하는 경우 `/HdiNotebooks/mynotebook1.ipynb`, hello 노트북도 Jupyter에서 표시 됩니다.  Hello 클러스터를 삭제 한 후에 전자 필기장 hello 저장소 계정에 남아 있습니다.

hello 방식으로 전자 필기장 toohello 저장소 계정에 저장 되는 HDFS 호환 됩니다. 따라서 경우 hello 다음 코드 조각에에서 나와 있는 것 처럼 관리 명령을 파일 SSH hello 클러스터를 사용할 수 있습니다.

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


Hello 전자 필기장 hello 헤드 노드에도 저장 됩니다 hello 클러스터에 대 한 hello 저장소 계정에 액세스 하는 문제가 있는 경우 `/var/lib/jupyter`합니다.

## <a name="supported-browser"></a>지원되는 브라우저

Spark HDInsight 클러스터의 Jupyter 노트북은 Google Chrome에서만 지원됩니다.

## <a name="feedback"></a>사용자 의견
새 커널 hello 진화 단계에 있으며 시간이 지남에 따라 완성 됩니다. 이는 API가 이러한 커널의 성숙에 따라 변경될 수 있음을 의미할 수 있습니다. 이러한 새로운 커널을 사용하는 동안 가진 의견을 보내주시면 감사하겠습니다. 이러한 커널의 최종 릴리스 hello 모양 지정에서 유용 합니다. Hello에서 주석을/피드백을 그대로 둘 수 **주석** 이 문서의 hello 아래쪽 섹션.

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
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
