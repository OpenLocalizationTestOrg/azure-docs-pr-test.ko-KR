---
title: "aaaSpark BI 데이터 시각화 도구를 사용 하 여 Azure HDInsight의 | Microsoft Docs"
description: "HDInsight 클러스터에서 Apache Spark BI를 사용하는 분석에 대해 데이터 시각화 도구 사용"
keywords: "apache spark bi,spark bi, spark 데이터 시각화, spark 비즈니스 인텔리전스"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Azure HDInsight와 함께 데이터 시각화 도구를 사용하는 Apache Spark BI

어떻게 toouse 데이터 시각화 도구 등 Power BI와 Tableau tooanalyze Apache Spark BI를 사용 하 여 HDInsight 클러스터에서 원시 샘플 데이터 집합에 알아봅니다.

> [!NOTE]
> 이 문서에 설명된 BI 도구와의 연결은 Azure HDInsight 3.6 Preview의 Spark 2.1에서 지원되지 않습니다. Spark 버전 1.6 및 2.0(각각 HDInsight 3.4, 3.5)만 지원됩니다.
>

이 자습서는 HDInsight Spark 클러스터에서 Jupyter 노트북으로 사용할 수도 있습니다. hello 노트북 경험 자체 hello 노트북에서 Python 코드 조각을 hello를 실행할 수 있습니다. 노트북, 내에서 tooperform hello 자습서 Spark 클러스터를 만듭니다을 시작 하며, Jupyter 노트북 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), 다음 hello 노트북을 실행 하 고 **HDInsight.ipynb의 Apache Spark와 함께 사용 하 여 BI 도구** hello 아래 **Python**  폴더입니다.

## <a name="prerequisites"></a>필수 조건

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.


## <a name="hivetable"></a>Spark 데이터 시각화를 위한 데이터 준비

이 섹션을 사용 하 여 hello [Jupyter](https://jupyter.org) 원시 샘플 데이터를 처리 하 고 표 형식으로 저장 하는 HDInsight Spark 클러스터 toorun 작업에서 노트북 합니다. hello 예제 데이터는.csv 파일 (hvac.csv) 사용할 수 있는 기본적으로 모든 클러스터에서. 데이터를 테이블로 저장 hello 다음 섹션에서는 BI 도구 tooconnect toohello 테이블을 사용 하 고 데이터 시각화를 수행 합니다.

> [!NOTE]
> Hello의 hello 지침을 완료 한 후이 문서의 단계를 수행 하는 경우 [HDInsight Spark 클러스터에서 대화형 쿼리를 실행](hdinsight-apache-spark-load-data-run-query.md), 아래의 8 tooStep를 건너뛸 수 있습니다.
>

1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.   

2. Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

   > [!NOTE]
   > 또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Notebook을 만듭니다. **새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.

    ![Apache Spark BI에 대한 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Apache Spark BI에 대한 Jupyter 노트북 만들기")

4. 새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다. Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.

    ![Apache Spark BI에 대 한 hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Apache Spark BI에 대 한 hello 전자 필기장에 대 한 이름을 제공")

5. Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다. hello 첫 번째 코드 셀을 실행할 때 사용자에 대 한 hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다. 이 시나리오에 필요한 hello 종류를 가져와서 시작할 수 있습니다. toodo 누릅니다 hello 셀에 등 hello 커서를 놓고 **SHIFT + ENTER**합니다.

        from pyspark.sql import *

6. 샘플 데이터를 임시 테이블에 로드합니다. Hello 예제 데이터 파일, HDInsight의 Spark 클러스터를 만들 때 **hvac.csv**, 복사한 toohello 연결 된 저장소 계정에는 **\HdiSamples\HdiSamples\SensorSampleData\hvac**합니다.

    빈 셀을 붙여넣고 hello 다음 코드 조각 및 키를 눌러 **SHIFT + ENTER**합니다. 이 코드 조각 이라고 하는 테이블에 hello 데이터 등록 **hvac**합니다.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. 해당 hello 테이블 올바르게 만들어졌는지 확인 합니다. Hello를 사용할 수 있습니다 `%%sql` toorun 하이브 쿼리를 직접 매직 합니다. Hello에 대 한 자세한 내용은 `%%sql` 매직, 및 기타 마법 hello PySpark 커널 사용할 수 있는 참조 [Jupyter 노트북 HDInsight Spark 클러스터에서 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.

        %%sql
        SHOW TABLES

    아래와 같은 출력이 표시됩니다.

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Hello에서 false가 테이블에만 hello **isTemporary** 열은 하이브 테이블 hello metastore에 저장 되 고 hello BI 도구에서 액세스할 수입니다. 이 자습서에서는 toohello 연결 **hvac** 테이블을 만들었습니다.

8. Hello 의도 한 데이터를 포함 하는 hello 테이블을 확인 합니다. Hello 전자 필기장의 빈 셀을 복사 hello 다음 코드 조각 및 키를 눌러 **SHIFT + ENTER**합니다.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Hello 노트북 toorelease hello 리소스를 종료 합니다. toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다.

## <a name="powerbi"></a>Spark 데이터 시각화에 대해 Power BI 사용

> [!NOTE]
> 이 섹션은 HDInsight 3.4의 Spark 1.6 및 HDInsight 3.5의 Spark 2.0에만 사용할 수 있습니다.
>
>

Power BI tooconnect toohello 데이터를 사용할 수 있으며 toocreate 보고서 시각화 hello 데이터 테이블을 저장 한 후 대시보드, 등입니다.

1. 액세스 tooPower BI 있는지 확인 합니다. [http://www.powerbi.com/](http://www.powerbi.com/)에서 Power BI의 미리 보기 구독을 무료로 받을 수 있습니다.

2. 역시 로그인[Power BI](http://www.powerbi.com/)합니다.

3. Hello hello 왼쪽된 창 아래쪽에서 클릭 **데이터 가져오기**합니다.

4. Hello에 **데이터 가져오기** 페이지의 **가져오기 또는 연결 tooData**에 대 한 **데이터베이스**, 클릭 **가져오기**합니다.

    ![Apache Spark BI용 Power BI로 데이터 가져오기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Apache Spark BI용 Power BI로 데이터 가져오기")

5. Hello 다음 화면에서 클릭 **Azure HDInsight의 Spark** 클릭 하 고 **연결**합니다. 메시지가 표시 되 면 hello 클러스터 URL을 입력 합니다. (`mysparkcluster.azurehdinsight.net`) 및 hello 자격 증명 tooconnect toohello 클러스터입니다.

    ![Spark BI tooApache 연결](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "tooApache Spark BI를 연결 합니다.")

    Hello 연결이 설정 된 후 Power BI는 HDInsight의 Spark 클러스터 hello에서에서 데이터 가져오기 시작 합니다.

6. Power BI가 hello 데이터를 가져오고 추가 **Spark** hello에 데이터 집합 **데이터 집합** 제목입니다. Hello 데이터 집합 tooopen 새 워크시트 toovisualize hello 데이터를 클릭 합니다. 보고서를 보고서로 hello 워크시트에 저장할 수도 있습니다. toosave hello에서 워크시트 **파일** 메뉴를 클릭 하 여 **저장**합니다.

    ![Power BI 대시보드의 Apache Spark BI 타일](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI 대시보드의 Apache Spark BI 타일")
7. 해당 hello 확인 **필드** 목록 hello 오른쪽에 나열 hello **hvac** 앞에서 만든 테이블입니다. 이전 노트북에 정의 된 hello 테이블의 hello 테이블 toosee hello 필드를 확장 합니다.

      ![Apache Spark BI 대시보드에 테이블 나열](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Apache Spark BI 대시보드에 테이블 나열")

8. 대상 온도 각 구성에 대 한 실제 온도 간의 시각화 tooshow hello 차이 빌드하십시오. toovisualize를 데이터 선택 **영역형 차트** (빨간색 상자에 표시). 끌어서 놓기 hello toodefine hello 축 **BuildingID** 아래 **축**, 및 **ActualTemp**/**TargetTemp** 아래 필드 **값**합니다.

    ![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")

9. 기본적으로 hello 시각화에 대 한 hello 합계를 표시 **ActualTemp** 및 **TargetTemp**합니다. 예를 둘 다 hello hello 드롭다운 목록에서에서 필드를 선택 **평균** tooget 실제 평균 및 대상 온도 두 건물에 대 한 합니다.

    ![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")

10. 데이터 시각화 hello 화면에 비슷한 toohello 하나 여야 합니다. 관련 데이터와 함께 hello 시각화 tooget 도구 설명 위로 커서를 이동 합니다.

    ![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")

11. 클릭 **저장** hello에서 최상위 메뉴와 보고서 이름을 제공 합니다. Hello visual를 고정할 수 있습니다. 시각화를 고정 하면 hello 최신 값을 한눈에 추적할 수 있도록 대시보드에 저장 됩니다.

   원하는 만큼 많은 시각화 요소를 추가할 수 있습니다 hello 동일한 데이터 집합 및 데이터의 스냅샷에 대 한 toohello 대시보드 고정 합니다. 또한 HDInsight의 Spark 클러스터에 연결 된 tooPower direct 사용 하 여 BI 연결 됩니다. 이렇게 하면는 Power BI는 항상 한 hello 클러스터에서 대부분의 최신 데이터 있으므로 hello 데이터 집합에 대 한 새로 고침 tooschedule 필요가 없습니다.

## <a name="tableau"></a>Spark 데이터 시각화에 대해 Tableau Desktop 사용

> [!NOTE]
> 이 섹션은 Azure HDInsight에서 만든 Spark 1.5.2 클러스터에만 적용할 수 있습니다.
>
>

1. 설치 [Tableau 데스크톱](http://www.tableau.com/products/desktop) 이 Apache Spark BI 자습서를 실행 중인 hello 컴퓨터에 있습니다.

2. 또한 Microsoft Spark ODBC 드라이버가 컴퓨터에 설치되어 있는지 확인합니다. Hello 드라이버를 설치할 수 있습니다 [여기](http://go.microsoft.com/fwlink/?LinkId=616229)합니다.

1. Tableau Desktop을 실행합니다. Hello, 서버 tooconnect 목록에서 hello 왼쪽된 창에서 클릭 **Spark SQL**합니다. Spark SQL hello 왼쪽된 창에서 기본적으로 나열 되지 않으면 경우 클릭 하 여 찾을 수 있습니다 **더 서버**합니다.
2. Hello 스크린샷에 표시 된 대로 hello Spark SQL 연결 대화 상자에서 hello 값을 제공 하 고 클릭 **확인**합니다.

    ![Apache Spark BI에 대 한 연결 tooa 클러스터](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Apache Spark BI에 대 한 연결 tooa 클러스터")

    인증 드롭 다운 목록을 hello **Microsoft Azure HDInsight 서비스** hello를 설치한 경우에 선택적으로 [Microsoft Spark ODBC 드라이버가](http://go.microsoft.com/fwlink/?LinkId=616229) hello 컴퓨터에 있습니다.
3. Hello에서 hello 다음 화면에서 **스키마** 드롭다운 목록에서 클릭 hello **찾을** 아이콘을 클릭 한 다음 **기본**합니다.

    ![Apache Spark BI용 스키마 찾기](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Apache Spark BI용 스키마 찾기")
4. Hello에 대 한 **테이블** 필드을 hello 클릭 **찾을** 아이콘 다시 모든 hello toolist 하이브 hello 클러스터에서 사용할 수 있는 테이블입니다. Hello 표시 되어야 **hvac** 이전 hello 노트북을 사용 하 여 만든 테이블입니다.

    ![Apache Spark BI용 테이블 찾기](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Apache Spark BI용 테이블 찾기")
5. 끌어서 hello 테이블 toohello 맨 위에 있는 상자 hello 오른쪽에 놓습니다. Tableau hello 데이터를 가져오며 hello 빨간색 상자로 강조 표시 된 대로 hello 스키마가 표시 됩니다.

    ![Apache Spark BI에 대 한 테이블 tooTableau 추가](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "테이블 tooTableau Apache Spark BI에 대 한 추가")
6. Hello 클릭 **Sheet1** hello 왼쪽 아래에는 탭 합니다. 각 날짜에 대 한 hello 평균 대상과 모든 건물 실제 온도 표시 하는 시각화를 확인 합니다. 끌기 **날짜** 및 **건물 ID** 너무**열** 및 **실제 Temp**/**대상 Temp**너무**행**합니다. 아래 **표시**선택, **영역** toouse Spark 데이터 시각화에 대 한 영역 맵.

     ![Spark 데이터 시각화를 위한 필드 추가](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Spark 데이터 시각화를 위한 필드 추가")
7. 기본적으로 hello 온도 필드가 표시 되어 집계로 합니다. 대신 tooshow hello 평균 온도 원하는 경우 후 그렇게 hello 드롭다운 목록에서 아래와 같이 합니다.

    ![Spark 데이터 시각화에 대한 온도 평균 구하기](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Spark 데이터 시각화에 대한 온도 평균 구하기")

8. 적용할 수도 있습니다 슈퍼-온도 매핑이 두 개 이상의 다른 tooget 대상과 실제 온도 사이의 차이 보다 나은 느낌 hello 합니다. Hello 핸들 셰이프가 강조 표시는 빨간색 원이 나타날 때까지 hello 낮은 영역 맵의 hello 마우스 toohello 모퉁이 이동 합니다. 끌어서 hello 빨간색 사각형으로 강조 표시 하는 hello 셰이프가 나타날 때 toohello hello 위쪽과 릴리스 hello 마우스 단추를 다른 map을 매핑합니다.

    ![Spark 데이터 시각화를 위한 맵 병합](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Spark 데이터 시각화를 위한 맵 병합")

     데이터 시각화 hello 스크린샷에 표시 된 대로 변경 해야 합니다.

    ![Spark 데이터 시각화에 대한 Tableau 출력](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 데이터 시각화에 대한 Tableau 출력")
9. 클릭 **저장** toosave hello 워크시트입니다. 대시보드를 만들고 하나 이상의 시트 tooit를 추가할 수 있습니다.

## <a name="next-steps"></a>다음 단계

지금까지 어떻게 toocreate 클러스터 Spark 데이터 프레임 tooquery 데이터를 만들고 다음 BI 도구에서 해당 데이터에 액세스 배웠습니다. 이제 toomanage 클러스터 리소스 hello 하 고 HDInsight Spark 클러스터에서 실행 중인 작업을 디버그 하는 방법에 대 한 지침을 살펴볼 수 있습니다.

* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

