---
title: "Spark-Azure에서에서 Python 라이브러리를 사용 하 여 웹 사이트 로그 aaaAnalyze | Microsoft Docs"
description: "이 전자 필기장 tooanalyze Azure HDInsight의 Spark와 함께 사용자 지정 라이브러리를 사용 하 여 데이터를 기록 하는 방법을 보여 줍니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>HDInsight에서 Spark 클러스터와 함께 사용자 지정 Python 라이브러리를 사용하여 웹 사이트 로그 분석

이 전자 필기장 tooanalyze HDInsight의 Spark와 함께 사용자 지정 라이브러리를 사용 하 여 데이터를 기록 하는 방법을 보여 줍니다. 사용 하 여 hello 사용자 지정 라이브러리는 호출 하는 Python 라이브러리 **iislogparser.py**합니다.

> [!TIP]
> 이 자습서는 HDInsight에서 만드는 Spark(Linux) 클러스터에서 Jupyter 노트북으로 사용할 수도 있습니다. hello 노트북 경험 자체 hello 노트북에서 Python 코드 조각을 hello를 실행할 수 있습니다. 노트북, 내에서 tooperform hello 자습서 Spark 클러스터를 만듭니다을 시작 하며, Jupyter 노트북 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), 다음 hello 노트북을 실행 하 고 **사용자 지정 library.ipynb를 사용 하 여 Spark와 함께 로그를 분석** hello 아래  **PySpark** 폴더입니다.
>
>

**필수 조건:**

Hello 다음이 필요 합니다.

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="save-raw-data-as-an-rdd"></a>RDD로 원시 데이터 저장
이 섹션을 사용 하 여 hello [Jupyter](https://jupyter.org) 원시 샘플 데이터를 처리 하 고 하이브 테이블로 저장 하는 HDInsight toorun 작업에는 Apache Spark 클러스터와 연결 된 노트북 합니다. hello 예제 데이터는.csv 파일 (hvac.csv) 사용할 수 있는 기본적으로 모든 클러스터에서.

하이브 테이블로 데이터를 저장 hello 다음 섹션에서 Power BI 및 Tableau와 같은 BI 도구를 사용 하 여 toohello 하이브 테이블을 연결할 것입니다.

1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.   
2. Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

   > [!NOTE]
   > 또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. 새 Notebook을 만듭니다. **새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.

    ![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "새 Jupyter 노트북 만들기")
4. 새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다. Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.

    ![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")
5. Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다. hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다 드립니다 hello 첫 번째 코드 셀을 실행 하는 경우. 이 시나리오에 대 한 필요한 hello 형식은 가져와서 시작할 수 있습니다. 다음 코드 조각에서 빈 셀을 hello를 붙여 넣고 다음 키를 누릅니다 **SHIFT + ENTER**합니다.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. RDD hello 클러스터에서 이미 사용할 수 있는 hello 샘플 로그 데이터를 사용 하 여 만듭니다. Hello 데이터에서 hello 클러스터와 연결 된 hello 기본 저장소 계정에 액세스할 수 있습니다 **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**합니다.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. 이전 단계에서 완료 hello 샘플 로그 집합 tooverify를 검색 합니다.

        logs.take(5)

    출력 유사한 toohello 다음을 나타나야 합니다.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>사용자 지정 Python 라이브러리를 사용하여 로그 데이터 분석
1. 위의 hello 출력 hello 처음 몇 줄 hello 헤더 정보를 포함 하 고 나머지 각 줄에 해당 헤더에 설명 된 hello 스키마와 일치 합니다. 이러한 로그를 구문 분석하는 것은 복잡할 수 있습니다. 따라서 이러한 로그를 훨씬 쉽게 구문 분석하는 사용자 지정 Python 라이브러리(**iislogparser.py**)를 사용합니다. 기본적으로 이 라이브러리는 HDInsight의 Spark 클러스터( **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**)에 포함됩니다.

    그러나이 라이브러리에에서 없는 hello `PYTHONPATH` 같은 import 문을 사용 하 여 사용할 수 있도록 `import iislogparser`합니다. toouse이이 라이브러리 tooall hello 작업자 노드를 배포 해야 했습니다. 다음 코드 조각 hello를 실행 합니다.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`함수를 제공 `parse_log_line` 반환 하는 `None` 로그 줄은 머리글 행과 hello의 인스턴스를 반환 하는 경우 `LogLine` 로그 줄 발생 하는 경우 클래스입니다. 사용 하 여 hello `LogLine` 클래스 tooextract hello RDD에서에서 로그 줄을만 hello:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. 몇 가지 단계에서 완료 hello 행 압축 푼된 정도가 tooverify 검색 합니다.

       logLines.take(2)

   hello 출력은 비슷한 toohello 다음 됩니다.

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. hello `LogLine` 클래스에 대 한 몇 가지 유용한 메서드 같은 `is_error()`, 로그 항목에서 오류 코드에 있는지 여부를 반환 하는 합니다. Hello 추출 로그 줄에서 오류의이 toocompute hello 수를 사용 하 여 하 한 다음 모든 hello 오류 tooa 다른 파일을 로그 합니다.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Hello 다음과 같은 출력을 표시 되어야 합니다.

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. 사용할 수도 있습니다 **Matplotlib** tooconstruct hello 데이터를 시각화 합니다. 예를 들어 tooisolate hello 원인을 오랜 시간 동안 실행 되는 요청을 사용 하도록 하려는 경우 toofind hello 파일 평균 hello 시간 tooserve 대부분을 사용 하는 경우가 있습니다.
   아래 hello 조각 hello 상위 25 리소스 검색 하는 대부분의 시간 tooserve 요청 합니다.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Hello 다음과 같은 출력을 표시 되어야 합니다.

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. 그림의 hello 형태로이 정보를 제공할 수 있습니다. 첫 번째 단계 toocreate 플롯을 알려 주세요 먼저 만드는 것이 임시 테이블 **AverageTime**합니다. 특정 시간에 모든 비정상적인 대기 시간 급증 되었으면 테이블 그룹 hello hello 시간 toosee로 기록 합니다.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. 다음에서 실행할 수 있습니다 다음 SQL 쿼리 tooget hello 모든 hello 레코드 hello **AverageTime** 테이블입니다.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   hello `%%sql` 매직 뒤 `-o averagetime` hello 쿼리의 hello 출력 (일반적으로 hello의 헤드 노드에 hello 클러스터) hello Jupyter 서버에서 로컬로 유지 되도록 보장 합니다. hello 출력으로 유지 되는 [팬더](http://pandas.pydata.org/) 데이터 프레임 hello로 이름을 지정 **averagetime**합니다.

   Hello 다음과 같은 출력을 표시 되어야 합니다.

   ![SQL 쿼리 출력](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL 쿼리 출력")

   Hello에 대 한 자세한 내용은 `%%sql` 매직, 참조 [hello로 지원 되는 매개 변수 %%sql 매직](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.
7. 이제 Matplotlib를 사용할 수 있습니다, 라이브러리의 데이터를 toocreate 플롯을 tooconstruct 시각화를 사용 합니다. 로컬로 hello에서 hello 플롯을 만들어야 하기 때문에 유지 **averagetime** 데이터 프레임을 hello 코드 조각 hello로 시작 해야 `%%local` 매직 합니다. 이렇게 하면 hello 코드 hello Jupyter 서버에서 로컬로 실행 됩니다.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Hello 다음과 같은 출력을 표시 되어야 합니다.

   ![Matplotlib 출력](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib 출력")
8. Hello 응용 프로그램 실행을 완료 한 후 종료 hello 노트북 toorelease hello 리소스 해야 합니다. toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다. 이 종료 및 닫기 hello 전자 필기장 합니다.

## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
