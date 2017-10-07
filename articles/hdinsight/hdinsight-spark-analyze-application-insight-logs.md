---
title: "Azure HDInsight Spark-를 사용 하 여 aaaAnalyze Application Insight 기록 | Microsoft Docs"
description: "Application Insight tooexport tooblob 저장소를 기록 하는 방법을 알아보고 HDInsight의 spark hello 로그를 분석 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>HDInsight에서 Spark를 사용하여 Application Insights 원격 분석 로그 분석

자세한 내용은 HDInsight tooanalyze Application Insight 원격 분석 데이터에 toouse 멤버 하는 방법입니다.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) 는 웹 응용 프로그램을 모니터링하는 분석 서비스입니다. Application Insights에 의해 생성 된 원격 분석 데이터에는 내보낸된 tooAzure 저장 될 수 있습니다. HDInsight 사용된 tooanalyze 수 hello 데이터를 Azure 저장소에 해당 합니다.

## <a name="prerequisites"></a>필수 조건

* 응용 프로그램을 toouse Application Insights를 구성 합니다.

* Linux 기반 HDInsight 클러스터를 만드는 데 익숙해야 합니다. 자세한 내용은 [HDInsight에서 Spark 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

  > [!IMPORTANT]
  > 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* 웹 브라우저.

hello 다음 리소스에 사용 된 개발 하 고이 문서를 테스트 합니다.

* 응용 프로그램 Insights 원격 분석 데이터를 사용 하 여 생성 하는 [Node.js 웹 응용 프로그램 구성 toouse Application Insights](../application-insights/app-insights-nodejs.md)합니다.

* HDInsight 클러스터 버전 3.5에서 Linux 기반 Spark에 사용 되는 tooanalyze hello 데이터 했습니다.

## <a name="architecture-and-planning"></a>아키텍처 및 계획

다이어그램을 다음 hello이 예제의 hello 서비스 아키텍처를 보여 줍니다.

![HDInsight의 Spark에 의해 처리 되는 다음에 Application Insights tooblob 저장소에서 데이터를 보여 주는 다이어그램](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Azure 저장소

Application Insights 구성된 toocontinuously 내보내기 원격 분석 정보 tooblobs 수 있습니다. HDInsight은 hello blob에 저장 된 데이터 읽을 수 있습니다. 그러나 따라야 할 몇 가지 요구 사항이 있습니다.

* **위치**: hello 저장소 계정 및 HDInsight 서로 다른 위치에 있으면 대기 시간이 길어질 수 있습니다. 또한 전송 요금 적용된 toodata 지역 간 이동은 비용을 증가 합니다.

    > [!WARNING]
    > HDInsight와 다른 위치에서는 저장소 계정을 사용할 수 없습니다.

* **Blob 유형**: HDInsight는 블록 Blob만을 지원합니다. Application Insights toousing 블록 blob을 HDInsight 함께 기본적으로 작동 해야 하므로 기본값입니다.

추가 저장소 tooan 기존 HDInsight 클러스터를 추가 하는 방법에 대 한 정보를 참조 hello [추가 저장소 계정을 추가](hdinsight-hadoop-add-storage.md) 문서.

### <a name="data-schema"></a>데이터 스키마

Application Insights는 [데이터 모델을 내보낼](../application-insights/app-insights-export-data-model.md) hello 원격 분석 데이터 형식에 대 한 정보 tooblobs로 내보냅니다. 이 문서의 단계 hello hello 데이터로 Spark SQL toowork를 사용합니다. Spark SQL Application Insights에 의해 기록 된 hello JSON 데이터 구조에 대 한 스키마를 자동으로 생성할 수 있습니다.

## <a name="export-telemetry-data"></a>원격 분석 데이터 내보내기

Hello 단계에 따라 [연속 내보내기 구성](../application-insights/app-insights-export-telemetry.md) tooconfigure Application Insights tooexport 원격 분석 정보 tooan Azure 저장소 blob입니다.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>HDInsight tooaccess hello 데이터 구성

HDInsight 클러스터를 만드는 경우 클러스터를 만드는 동안 hello 저장소 계정을 추가 합니다.

Azure 저장소 계정 tooan 기존 클러스터 tooadd hello hello 정보를 사용 하 여 hello에 [다른 저장소 계정을 추가할](hdinsight-hadoop-add-storage.md) 문서.

## <a name="analyze-hello-data-pyspark"></a>Hello 데이터 분석: PySpark

1. Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터에서 Spark를 선택 합니다. Hello에서 **빠른 링크** 섹션에서 **클러스터 대시보드**를 선택한 후 **Jupyter 노트북** hello 클러스터 Dashboard__ 블레이드에서 합니다.

    ![hello 클러스터 대시보드](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. Hello 오른쪽 위 모서리로 hello Jupyter 페이지에서 선택 **새로**, 차례로 **PySpark**합니다. Python 기반 Jupyter Notebook을 포함하는 새 브라우저 탭이 열립니다.

3. Hello 첫 번째 필드에서 (호출을 **셀**) hello 페이지 hello 텍스트 다음 입력:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    이 코드는 hello 입력된 데이터에 대 한 Spark toorecursively 액세스 hello 디렉터리 구조를 구성합니다. Application Insights 원격 분석은 기록된 tooa 디렉터리 구조와 유사한 toohello `/{telemetry type}/YYYY-MM-DD/{##}/`합니다.

4. 사용 하 여 **SHIFT + ENTER** toorun hello 코드입니다. Hello hello 셀의 왼쪽에 '\*' hello 코드가이 셀에 실행 되 고 있음을 hello 대괄호 tooindicate 사이 나타납니다. 이 완료 되 면 hello '\*' tooa 번호 및 텍스트 다음 유사한 toohello hello 셀 아래에 표시 되어 출력을 변경 합니다.

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. 새로운 셀 hello 아래 만들어집니다. 첫 번째 항목이 있습니다. Hello 텍스트 hello 새로운 셀에서 다음을 입력 합니다. 대체 `CONTAINER` 및 `STORAGEACCOUNT` hello Azure 저장소 계정 이름 및 Application Insights 데이터를 포함 하는 blob 컨테이너 이름을 사용 합니다.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    사용 하 여 **SHIFT + ENTER** tooexecute이이 셀입니다. 텍스트 다음 결과 유사한 toohello를 표시 됩니다.

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    반환 된 hello wasb 경로 hello 위치 hello Application Insights 원격 분석 데이터입니다. 변경 hello `hdfs dfs -ls` 으로 hello 셀 toouse hello wasb 경로 반환 하 고 사용 하 여 **SHIFT + ENTER** toorun hello 셀 다시 합니다. 이 시간 hello 결과는 원격 분석 데이터를 포함 하는 hello 디렉터리 표시 되어야 합니다.

   > [!NOTE]
   > 이 섹션의 단계를 hello 나머지 hello hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` 디렉터리가 사용 되었습니다. 사용자의 디렉터리 구조는 다를 수 있습니다.

6. Hello 다음 셀에 입력 코드 다음 hello: 대체 `WASB_PATH` hello 이전 단계의 hello 경로 사용 합니다.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    이 코드는 hello 연속 내보내기 프로세스에서 내보내는 hello JSON 파일에서 데이터 프레임이 만듭니다. 사용 하 여 **SHIFT + ENTER** toorun이이 셀입니다.
7. Hello 다음 셀에 입력 하 고 hello tooview hello Spark에서 만든 스키마를 hello JSON 파일에 대 한 다음 실행:

   ```python
   jsonData.printSchema()
   ```

    각 유형의 원격 분석에 대 한 hello 스키마는 다릅니다. hello 다음 예제는 웹 요청에 대해 생성 되는 hello 스키마 (hello에 저장 된 데이터 `Requests` 하위 디렉터리):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. 임시 테이블과 tooregister hello 데이터 프레임을 따라 hello를 사용 하 여 하 고 hello 데이터에 대 한 쿼리를 실행 합니다.

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    이 쿼리 context.location.city null이 hello 상위 20 개의 레코드에 대 한 hello 도시 정보를 반환 합니다.

   > [!NOTE]
   > hello 컨텍스트 구조는 Application Insights에 의해 기록 된 모든 원격 분석에 존재 합니다. 로그에 hello 도시 요소를 채울 수 있습니다. Hello 스키마 tooidentify 프로그램 로그에 대 한 데이터를 포함할 수 있는 쿼리할 수 있는 다른 요소를 사용 합니다.

    이 쿼리 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Hello 데이터 분석: Scala

1. Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터에서 Spark를 선택 합니다. Hello에서 **빠른 링크** 섹션에서 **클러스터 대시보드**를 선택한 후 **Jupyter 노트북** hello 클러스터 Dashboard__ 블레이드에서 합니다.

    ![hello 클러스터 대시보드](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. Hello 오른쪽 위 모서리로 hello Jupyter 페이지에서 선택 **새로**, 차례로 **Scala**합니다. Scala 기반 Jupyter Notebook을 포함하는 새 브라우저 탭이 나타납니다.
3. Hello 첫 번째 필드에서 (호출을 **셀**) hello 페이지 hello 텍스트 다음 입력:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    이 코드는 hello 입력된 데이터에 대 한 Spark toorecursively 액세스 hello 디렉터리 구조를 구성합니다. Application Insights 원격 분석은 유사한 tooa 디렉터리 구조를 너무 기록`/{telemetry type}/YYYY-MM-DD/{##}/`합니다.

4. 사용 하 여 **SHIFT + ENTER** toorun hello 코드입니다. Hello hello 셀의 왼쪽에 '\*' hello 코드가이 셀에 실행 되 고 있음을 hello 대괄호 tooindicate 사이 나타납니다. 이 완료 되 면 hello '\*' tooa 번호 및 텍스트 다음 유사한 toohello hello 셀 아래에 표시 되어 출력을 변경 합니다.

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. 새로운 셀 hello 아래 만들어집니다. 첫 번째 항목이 있습니다. Hello 텍스트 hello 새로운 셀에서 다음을 입력 합니다. 대체 `CONTAINER` 및 `STORAGEACCOUNT` hello Azure 저장소 계정 이름 및 Application Insights 포함 된 blob 컨테이너 이름으로 기록 합니다.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    사용 하 여 **SHIFT + ENTER** tooexecute이이 셀입니다. 텍스트 다음 결과 유사한 toohello를 표시 됩니다.

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    반환 된 hello wasb 경로 hello 위치 hello Application Insights 원격 분석 데이터입니다. 변경 hello `hdfs dfs -ls` 으로 hello 셀 toouse hello wasb 경로 반환 하 고 사용 하 여 **SHIFT + ENTER** toorun hello 셀 다시 합니다. 이 시간 hello 결과는 원격 분석 데이터를 포함 하는 hello 디렉터리 표시 되어야 합니다.

   > [!NOTE]
   > 이 섹션의 단계를 hello 나머지 hello hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` 디렉터리가 사용 되었습니다. 원격 분석 데이터가 웹앱에 대한 것이 아니면 이 디렉터리는 없을 수도 있습니다.

6. Hello 다음 셀에 입력 코드 다음 hello: 대체 `WASB\_PATH` hello 이전 단계의 hello 경로 사용 합니다.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    이 코드는 hello 연속 내보내기 프로세스에서 내보내는 hello JSON 파일에서 데이터 프레임이 만듭니다. 사용 하 여 **SHIFT + ENTER** toorun이이 셀입니다.

7. Hello 다음 셀에 입력 하 고 hello tooview hello Spark에서 만든 스키마를 hello JSON 파일에 대 한 다음 실행:

   ```scala
   jsonData.printSchema
   ```

    각 유형의 원격 분석에 대 한 hello 스키마는 다릅니다. hello 다음 예제는 웹 요청에 대해 생성 되는 hello 스키마 (hello에 저장 된 데이터 `Requests` 하위 디렉터리):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. 임시 테이블과 tooregister hello 데이터 프레임을 따라 hello를 사용 하 여 하 고 hello 데이터에 대 한 쿼리를 실행 합니다.

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    이 쿼리 context.location.city null이 hello 상위 20 개의 레코드에 대 한 hello 도시 정보를 반환 합니다.

   > [!NOTE]
   > hello 컨텍스트 구조는 Application Insights에 의해 기록 된 모든 원격 분석에 존재 합니다. 로그에 hello 도시 요소를 채울 수 있습니다. Hello 스키마 tooidentify 프로그램 로그에 대 한 데이터를 포함할 수 있는 쿼리할 수 있는 다른 요소를 사용 합니다.
   >
   >

    이 쿼리 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>다음 단계

Spark toowork를 사용 하 여 데이터와 Azure에서 서비스의 자세한 예 hello 다음 문서를 참조:

* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

만들고 Spark 실행 중인 응용 프로그램에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)
