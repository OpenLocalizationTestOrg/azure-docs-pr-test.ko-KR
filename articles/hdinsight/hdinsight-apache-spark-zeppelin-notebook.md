---
title: "Azure HDInsight의 Apache Spark와 함께 aaaUse 선을 전자 필기장 클러스터 | Microsoft Docs"
description: "Azure HDInsight의 Apache Spark와 함께 toouse 선을 전자 필기장 클러스터 하는 방법에 대해 단계별로 설명 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Azure HDInsight에서 Apache Spark 클러스터와 함께 Zeppelin Notebook 사용

HDInsight Spark 클러스터 toorun Spark 작업을 사용할 수 있는 선을 전자 필기장 포함 됩니다. 이 문서에서는 toouse HDInsight 클러스터에서 선을 노트북 hello 하는 방법을 배웁니다.

> [!NOTE]
> Zeppelin Notebook은 HDInsight 3.5의 Spark 1.6.3 및 HDInsight 3.6의 Spark 2.1.0에만 사용할 수 있습니다.
>

**필수 조건:**

* Azure 구독. [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

## <a name="launch-a-zeppelin-notebook"></a>Zeppelin Notebook 시작
1. Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **선을 노트북**합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.
   
   > [!NOTE]
   > 또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello 선을 노트북에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. 새 Notebook을 만듭니다. Hello 헤더 창에서 클릭 **노트북**, 클릭 하 고 **만들 새 메모**합니다.
   
    ![새 Zeppelin Notebook 만들기](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "새 Zeppelin Notebook 만들기")
   
    Hello 전자 필기장에 대 한 이름을 입력 한 다음 클릭 **만들 참고**합니다.
3. 연결 된 상태를 표시 하는 hello 노트북 헤더 있는지 확인 합니다. 녹색 점 hello 오른쪽 위 모서리에 표시 됩니다.
   
    ![Zeppelin Notebook 상태](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin Notebook 상태")
4. 샘플 데이터를 임시 테이블에 로드합니다. Hello 예제 데이터 파일, HDInsight의 Spark 클러스터를 만들 때 **hvac.csv**, 복사한 toohello 연결 된 저장소 계정에는 **\HdiSamples\SensorSampleData\hvac**합니다.
   
    기본적으로 새 전자 필기장 hello에에서 만들어지는 빈 단락 hello에서 다음 코드 조각 hello를 붙여 넣습니다.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    키를 눌러 **SHIFT + ENTER** hello 키를 누르거나 **재생** hello 단락 toorun hello 조각에 대 한 단추입니다. hello 단락의 hello 오른쪽 모서리에서 hello 상태 보류 중, 실행 tooFINISHED 준비에서 진행 해야 합니다. hello 출력에 hello hello 맨 아래에 참석 같은 단락 합니다. hello 스크린 샷 hello 다음과 같이 표시 됩니다.
   
    ![원시 데이터에서 임시 테이블 만들기](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "원시 데이터에서 임시 테이블 만들기")
   
    또한 제목 tooeach 단락을 제공할 수 있습니다. Hello 오른쪽 모서리에서 클릭 hello **설정** 아이콘을 클릭 한 다음 **제목 표시**합니다.
5. Hello에 이제 Spark SQL 문을 실행할 수 있습니다 **hvac** 테이블입니다. Hello를 다음 새 단락에서 쿼리를 붙여 넣습니다. hello 쿼리 hello 차이 hello 대상과 특정된 날짜에 각 빌드에 대 한 실제 온도 및 hello 건물 ID를 검색 합니다. **Shift + Enter**를 누릅니다.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    hello **%sql** hello 시작 부분에는 문을 hello 노트북 toouse hello 리비 Scala 인터프리터를 알려 줍니다.
   
    hello 다음 스크린 샷에서 hello 출력이 나와 있습니다.
   
    ![Hello 노트북을 사용 하 여 Spark SQL 문을 실행](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "hello 노트북을 사용 하 여 Spark SQL 문 실행")
   
     Hello에 대 한 다른 표현 간의 hello 표시 옵션 (에 강조 표시 된 사각형) tooswitch 클릭 동일한 출력 합니다. 클릭 **설정을** toochoose 어떤 consitutes hello 키와 hello 출력에는 값입니다. 사용 하 여 위에 화면 캡처 hello **buildingID** hello 키와의 hello 평균 **temp_diff** hello 값으로.
6. 또한 hello 쿼리에서 변수를 사용 하 여 Spark SQL 문을 실행할 수 있습니다. 다음 조각과 hello 방법을 toodefine 변수에 **Temp**와 tooquery 원하는 hello 가능한 값을 사용 하 여 hello 쿼리 합니다. Hello 쿼리를 처음 실행 하면 드롭 다운 hello hello 변수에 대해 지정한 값이 자동으로 채워집니다.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    새 단락에 이 코드 조각을 붙여넣고 **Shift + Enter**를 누릅니다. hello 다음 스크린 샷에서 hello 출력이 나와 있습니다.
   
    ![Hello 노트북을 사용 하 여 Spark SQL 문을 실행](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "hello 노트북을 사용 하 여 Spark SQL 문 실행")
   
    후속 쿼리에 대 한 hello 드롭다운 목록에서 새 값을 선택 하 고 hello 쿼리를 다시 실행할 수 있습니다. 클릭 **설정을** toochoose 어떤 consitutes hello 키와 hello 출력에는 값입니다. 사용 하 여 위에 화면 캡처 hello **buildingID** hello 키로의 평균 hello **temp_diff** hello 값으로 및 **targettemp** hello 그룹으로 합니다.
7. Hello 리비 인터프리터 tooexit hello 응용 프로그램을 다시 시작 합니다. toodo 인터프리터 설정을 hello 오른쪽 위 모서리에서 사용자 이름에 기록 하는 hello를 클릭 하 여 열고 클릭 **인터프리터**합니다.
   
    ![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")
8. TooLivy 인터프리터 설정을 스크롤한 다음 클릭 **다시 시작**합니다.
   
    ![리비 intepreter hello를 다시 시작](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 선을 intepreter를 다시 시작")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>외부 패키지 hello 노트북으로 사용 하려면 어떻게 해야 합니까?
Hello 선을 노트북에 HDInsight (Linux) toouse 외부, 커뮤니티 제공 하지 않은 패키지를 포함된-의-즉시 hello 클러스터의 Apache Spark 클러스터에서 구성할 수 있습니다. Hello를 검색할 수 있습니다 [Maven 리포지토리](http://search.maven.org/) 사용할 수 있는 패키지의 전체 목록은 hello에 대 한 합니다. 다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다. 예를 들어 커뮤니티 제공 패키지의 전체 목록은 [Spark 패키지](http://spark-packages.org/)에서 사용할 수 있습니다.

이 문서에서 볼 수 있습니다 어떻게 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter 노트북을 사용 하 여 패키지 합니다.

1. 인터프리터 설정을 엽니다. Hello 오른쪽 위 모서리에서 사용자 이름에 기록 하는 hello를 클릭 한 다음 클릭 **인터프리터**합니다.
   
    ![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")
2. TooLivy 인터프리터 설정을 스크롤한 다음 클릭 **편집**합니다.
   
    ![인터프리터 설정 변경](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "인터프리터 설정 변경")
3. 새 키를 추가 호출 **livy.spark.jars.packages** hello 형식에서 값을 설정 하 고 `group:id:version`합니다. 따라서 toouse hello를 원하는 경우 [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 패키지 hello hello 키 값을 너무 설정 해야`com.databricks:spark-csv_2.10:1.4.0`합니다.
   
    ![인터프리터 설정 변경](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "인터프리터 설정 변경")
   
    클릭 **저장** 고 hello 리비 인터프리터를 다시 시작 합니다.
4. **팁**: 원하는 toounderstand hello hello 키 값에 tooarrive 여기의 위에 입력 되는 한 방법입니다.
   
    a. Maven 리포지토리 hello hello 패키지를 찾습니다. 이 자습서에서는 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)를 사용했습니다.
   
    b. 에 대 한 hello 값을 수집 hello 리포지토리에서 **GroupId**, **의 ArtifactId**, 및 **버전**합니다.
   
    ![Jupyter Notebook에서 외부 패키지 사용](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Jupyter Notebook에서 외부 패키지 사용")
   
    c. 콜론으로 구분 하는 hello 3 값 연결 (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>어디 hello를 저장 하는 선을 전자 필기장 입니까?
hello 선을 전자 필기장 toohello 클러스터 headnodes를 저장 됩니다. 따라서 hello 클러스터를 삭제 하면 hello 전자 필기장도 삭제 됩니다. 다른 클러스터에 나중에 사용할 전자 필기장 toopreserve 않으려면 hello 작업 실행을 완료 한 후 내보낼 해야 있습니다. 노트북, tooexport 클릭 hello **내보내기** hello 이미지 아래에 나와 있는 것 처럼 아이콘입니다.

![노트북 다운로드](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "다운로드 hello 노트북")

이렇게 하면 hello 노트북 JSON 파일로 다운로드 위치에 저장 합니다.

## <a name="livy-session-management"></a>Livy 세션 관리
선 노트북에서 첫 번째 코드 단락 hello를 실행할 때 새 리비 세션 HDInsight Spark 클러스터에 만들어집니다. 이 세션은 이후에 만드는 모든 Zeppelin Notebook에서 공유됩니다. 몇 가지 이유 hello에 대 한 경우 세션은 리비 종료 (클러스터 다시 부팅 등), hello 선 전자 필기장에서 수 toorun 작업 됩니다.

이러한 경우 hello 선 전자 필기장에서 실행 중인 작업을 시작 하기 전에 다음 단계를 수행 해야 합니다. 

1. Hello hello 선 전자 필기장에서 리비 인터프리터를 다시 시작 합니다. toodo 인터프리터 설정을 hello 오른쪽 위 모서리에서 사용자 이름에 기록 하는 hello를 클릭 하 여 열고 클릭 **인터프리터**합니다.
   
    ![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")
2. TooLivy 인터프리터 설정을 스크롤한 다음 클릭 **다시 시작**합니다.
   
    ![리비 intepreter hello를 다시 시작](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 선을 intepreter를 다시 시작")
3. 기존 Zeppelin Notebook에서 코드 셀을 실행합니다. Hello HDInsight 클러스터에 새 리비 세션을 만들어집니다.

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
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







