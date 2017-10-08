---
title: "데이터 레이크 (Hadoop) tools for Visual Studio-Azure HDInsight aaaHive | Microsoft Docs"
description: "어떻게 toouse hello 데이터 레이크 용 도구 Visual Studio toorun Apache Hive Azure HDInsight의 Apache Hadoop으로 쿼리를 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Visual Studio에 대 한 hello 데이터 레이크 도구를 사용 하는 하이브 쿼리 실행

Apache Hive는 Visual Studio tooquery 용 toouse hello 데이터 레이크 도구 하는 방법에 대해 알아봅니다. 데이터 레이크 도구 hello 허용 tooeasily 만들고, 제출 하 고 Azure HDInsight의 Hive 쿼리 tooHadoop를 모니터링 합니다.

## <a id="prereq"></a>필수 조건

* Azure HDInsight(HDInsight의 Hadoop) 클러스터

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* Visual Studio (hello 버전을 다음 중 하나):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate 업데이트 4

    * Visual Studio 2015(모든 버전)

    * Visual Studio 2017(모든 버전)

* Visual Studio용 HDInsight 도구 또는 Visual Studio용 Azure Data Lake 도구 참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) 설치 및 구성 hello 도구에 대 한 내용은 합니다.

## <a id="run"></a>Hello Visual Studio를 사용 하 여 하이브 쿼리를 실행 합니다.

1. **Visual Studio**를 열고 **새로 만들기** > **프로젝트** > **Azure Data Lake** > **HIVE** > **Hive 응용 프로그램**을 차례로 선택합니다. 이 프로젝트에 대한 이름을 입력합니다.

2. 열기 hello **Script.hql** 이 프로젝트 및 다음 HiveQL 조건 hello에 붙여넣기를 사용 하 여 만든 파일:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    이러한 문은 hello 다음 작업을 수행 합니다.

   * `DROP TABLE`: Hello 테이블이 존재 하는 경우이 문은으로 삭제 됩니다.

   * `CREATE EXTERNAL TABLE`: Hive에서 새 '외부' 테이블을 만듭니다. 외부 테이블 (데이터는 hello 원래 위치에 그대로 남아 hello) 하이브에 hello 테이블 정의만 저장 됩니다.

     > [!NOTE]
     > 외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다. MapReduce 작업 또는 Azure 서비스를 예로 들 수 있습니다.
     >
     > 외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.

   * `ROW FORMAT`: 하이브 hello 데이터 형식 지정 방법을 알려 줍니다. 이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.

   * `STORED AS TEXTFILE LOCATION`: 지시 하이브 여기서 hello 데이터가 저장 됩니다 (hello 예제/데이터 디렉터리) 텍스트로 저장 됩니다.

   * `SELECT`: 모든 행의 개수를 선택 합니다. 여기서 열 `t4` hello 값이 포함 된 `[ERROR]`합니다. 이 문에서는 이 값을 포함하는 행이 3개 있으므로 `3` 값이 반환되어야 합니다.

   * `INPUT__FILE__NAME LIKE '%.log'` - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다. 이 절 hello 데이터가 포함 된 hello 검색 toohello sample.log 파일을 제한 합니다.

3. Hello 도구 모음에서 선택 hello **HDInsight 클러스터** 이 쿼리에 대 한 toouse 되도록 합니다. 선택 **전송** 하이브 작업으로 toorun hello 문.

   ![제출 표시줄](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. hello **작업 요약 하이브** 표시 되 고 작업을 실행 하는 hello에 대 한 정보를 표시 합니다. 사용 하 여 hello **새로 고침** hello까지 toorefresh hello 작업 정보를 연결 **작업 상태** 쪽 변경**Completed**합니다.

   ![완료된 작업을 표시하는 작업 요약](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. 사용 하 여 hello **작업 출력** 이 작업의 tooview hello 출력을 연결 합니다. 표시 `[ERROR] 3`, 값은이 쿼리에서 반환 하는 hello 값입니다.

6. 또한 프로젝트를 만들지 않고도 Hive 쿼리를 실행할 수 있습니다. **서버 탐색기**에서 **Azure** > **HDInsight**를 확장하고, HDInsight 서버를 마우스 오른쪽 단추로 클릭한 다음 **Hive 쿼리 작성**을 선택합니다.

7. Hello에 **temp.hql** 나타나는 문서 hello 다음 HiveQL 조건 추가:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    이러한 문은 hello 다음 작업을 수행 합니다.

   * `CREATE TABLE IF NOT EXISTS`: 테이블이 아직 없는 경우 테이블을 만듭니다. 때문에 hello `EXTERNAL` 키워드가 사용 되지 않습니다,이 문은 내부 테이블을 만듭니다. 내부 테이블 hello 하이브 데이터 웨어하우스에 저장 되 고 하이브에 의해 관리 됩니다.

     > [!NOTE]
     > 와 달리 `EXTERNAL` hello 내부 데이터를 삭제 하는 테이블의 경우 내부 테이블도 삭제 합니다.

   * `STORED AS ORC`: 저장소 hello 최적화 된 행의 열 (ORC) 형식 데이터입니다. ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.

   * `INSERT OVERWRITE ... SELECT`: Hello에서 행을 선택 합니다. `log4jLogs` 이 있는 테이블 `[ERROR]`, 삽입 hello에 데이터를 hello 다음 `errorLogs` 테이블입니다.

8. Hello 도구 모음에서 선택 **전송** toorun hello 작업 합니다. 사용 하 여 hello **작업 상태** toodetermine 해당 hello 작업이 성공적으로 완료 했습니다.

9. 작업을 만들었습니다. hello 테이블을 사용 하 여 hello tooverify **서버 탐색기** 확장 **Azure** > **HDInsight** > HDInsight 클러스터에 > **하이브 데이터베이스** > **기본**합니다. hello **살펴볼** 테이블과 hello **log4jLogs** 테이블 나열 됩니다.

## <a id="nextsteps"></a>다음 단계

볼 수 있듯이 Visual Studio 용 HDInsight 도구 hello HDInsight의 Hive 쿼리를 쉽게 toowork를 제공 합니다.

HDInsight의 Hive에 대한 일반적인 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)

* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)

Hello에 대 한 자세한 내용은 Visual Studio 용 HDInsight 도구:

* [Visual Studio용 HDInsight 도구 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
