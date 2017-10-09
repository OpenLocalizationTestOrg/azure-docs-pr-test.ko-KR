---
title: "Azure HDInsight Spark 클러스터에서 대화형 쿼리 aaaRun | Microsoft Docs"
description: "HDInsight의 Apache Spark toocreate 클러스터 되는 방법에 HDInsight Spark 빠른 시작 합니다."
keywords: "spark 빠른 시작, 대화형 spark, 대화형 쿼리, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에서 대화형 쿼리 실행

이 문서는 Jupyter 노트북 toorun 대화형 Spark SQL에 대 한 쿼리 Spark 클러스터를 사용합니다. Jupyter 노트북은 hello 대화형 콘솔 기반 환경 toohello 웹을 확장 하는 브라우저 기반 응용 프로그램. 자세한 내용은 참조 [hello Jupyter 노트북](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html)합니다.

Hello를 사용 하면이 자습서에서는 **PySpark** 커널 hello Jupyter 노트북 toorun 대화형 Spark SQL 쿼리 합니다. HDInsight 클러스터의 Jupyter 노트북은 **PySpark3** 및 **Spark**의 두 가지 다른 커널도 지원합니다. Hello 커널 및 hello 사용할 경우의 이점에 대 한 자세한 내용은 **PySpark**, 참조 [HDInsight의 Apache Spark와 함께 사용 하 여 Jupyter 노트북 커널 클러스터](hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.

## <a name="prerequisites"></a>필수 조건

* **Azure HDInsight Spark 클러스터**. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Jupyter 노트북 toorun 대화형 쿼리 만들기

toorun 쿼리는 hello 클러스터와 연결 된 hello 저장소에서 사용할 수 있는 기본적으로는 예제 데이터를 사용 합니다. 그러나 먼저 데이터를 Spark에 데이터 프레임으로 로드해야 합니다. Hello 데이터 프레임을 사용 하는 후에 hello Jupyter 노트북을 사용 하 여 쿼리를 실행할 수 있습니다. 이 섹션에서는 다음을 수행하는 방법을 살펴봅니다.

* 예제 데이터 집합을 Spark 데이터 프레임으로 등록
* Hello 데이터 프레임에서 쿼리를 실행 합니다.

1. 열기 hello [Azure 포털](https://portal.azure.com/)합니다. Toopin hello 클러스터 toohello 대시보드를 선택한 경우 hello 대시보드 toolaunch hello 클러스터 블레이드에서 hello 클러스터 타일을 클릭 합니다.

    Hello 왼쪽된 창에서 hello 클러스터 toohello 대시보드에 고정 하지 않은 경우 클릭 **HDInsight 클러스터**, hello 클러스터를 만든 다음 클릭 합니다.

3. **빠른 링크**에서 **클러스터 대시보드**를 클릭한 다음 **Jupyter Notebook**을 클릭합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

   ![Jupyter 노트북 toorun 대화형 Spark SQL 쿼리 열기](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "열기 Jupyter 노트북 toorun 대화형 Spark SQL 쿼리")

   > [!NOTE]
   > 브라우저에서 URL을 다음 열어 hello 통해 클러스터에 대 한 hello Jupyter 노트북에 액세스할 수도 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Notebook을 만듭니다. **새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.

   ![Jupyter 노트북 toorun 대화형 Spark SQL 쿼리를 만들](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter 노트북 toorun 대화형 Spark SQL 쿼리를 만들려면")

   새 전자 필기장 만들어지고 Untitled(Untitled.pynb) hello 이름으로 열립니다.

4. Hello 위쪽에, hello 노트북 이름을 클릭 하 고 원하는 이름을 입력 합니다.

    ![Hello Jupter 노트북 toorun 대화형 Spark에서 쿼리 이름을 제공](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "hello Jupter 노트북 toorun 대화형 Spark에서 쿼리 이름을 제공 합니다.")

5. 붙여넣기 hello 다음 빈 셀을 코드로 바꾸고 다음 키를 누릅니다 **SHIFT + ENTER** toorun hello 코드입니다. hello 코드에는이 시나리오에 필요한 하는 hello 형식을 가져옵니다.

        from pyspark.sql.types import *

    Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다. hello 첫 번째 코드 셀을 실행할 때 사용자에 대 한 hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다.

    ![대화형 Spark SQL 쿼리 상태](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "대화형 Spark SQL 쿼리 상태")

    Jupyter에서 대화형 쿼리를 실행할 때 웹 브라우저 창 제목 표시는 **(Busy)** hello 노트북 제목 함께 상태입니다. 이 찬 원 모양 다음 toohello 표시 **PySpark** hello 오른쪽 위 모퉁이의 텍스트입니다. Hello 작업이 완료 되 면 tooa 흰색 원을 변경 합니다.

6. Spark 클러스터로 hello 데이터를 로드 하기 전에 응의 스냅숏으로 표시 합니다. hello이 자습서에 사용 되는 샘플 데이터를 사용할 수 HDInsight Spark 클러스터에서 모든 CSV 파일로 **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**합니다. hello 데이터 hello 온도 변화가 건물을 캡처합니다. 다음 hello hello 데이터의 처음 몇 행은입니다.

    ![대화형 Spark SQL 쿼리용 데이터의 스냅숏](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "대화형 Spark SQL 쿼리용 데이터의 스냅숏")

6. 임시 테이블 및 데이터 프레임이 만듭니다 (**hvac**) hello 코드 다음을 실행 하 여 합니다. 이 자습서에서는 만들지 않습니다 모든 hello 열 hello 임시 테이블의 CSV 데이터의 원시 hello에 비해 toohello 열으로. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Hello 테이블을 만든 후 hello 데이터에 대해 대화형 쿼리 실행 코드 다음 hello를 사용 합니다.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   PySpark 커널을 사용 하는 실행할 수 있습니다 이제 직접 대화형 SQL 쿼리 hello 임시 테이블에 **hvac** hello를 사용 하 여 만든 `%%sql` 매직 합니다. Hello에 대 한 자세한 내용은 `%%sql` 매직, 및 기타 마법 hello PySpark 커널 사용할 수 있는 참조 [Jupyter 노트북 HDInsight Spark 클러스터에서 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.

   다음 표 형식으로 출력 하는 hello 기본적으로 표시 됩니다.

     ![대화형 Spark 쿼리 결과의 테이블 출력](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "대화형 Spark 쿼리 결과의 테이블 출력")

    다른 시각화 요소에서 hello 결과 확인할 수 있습니다. 예를 들어 영역에 대 한 그래프 hello hello 다음과 같은 동일한 출력이 표시 됩니다.

    ![대화형 Spark 쿼리 결과의 영역 그래프](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "대화형 Spark 쿼리 결과의 영역 그래프")

9. Hello 응용 프로그램 실행을 완료 한 후 hello 노트북 toorelease hello 클러스터 리소스를 종료 합니다. toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다.

## <a name="next-step"></a>다음 단계

이 방법에 대해 배웠습니다 문서 Jupyter 노트북을 사용 하 여 spark에서 toorun 대화형 쿼리 합니다. Power BI와 Tableau와 같은 BI 분석 도구에 toohello 다음 문서 toosee hello 데이터 Spark에 등록 되어 끌어올 수 있습니다 어떻게를 진행 합니다. 

> [!div class="nextstepaction"]
>[Azure HDInsight와 함께 데이터 시각화 도구를 사용하는 Spark BI](hdinsight-apache-spark-use-bi-tools.md)




