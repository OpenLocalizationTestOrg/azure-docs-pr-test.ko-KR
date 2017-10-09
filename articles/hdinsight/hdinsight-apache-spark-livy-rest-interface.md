---
title: "Azure HDInsight의 aaaUse 리비 Spark toosubmit 작업 tooSpark 클러스터 | Microsoft Docs"
description: "어떻게 toouse Apache Spark REST API toosubmit Spark 작업 원격으로 tooan Azure HDInsight 클러스터에 알아봅니다."
keywords: apache spark rest api, livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Apache Spark REST API toosubmit 원격 작업 tooan HDInsight Spark 클러스터를 사용 하 여

Toouse 리비, hello Apache Spark REST API 사용 되는 toosubmit 원격 인 tooan Azure HDInsight Spark 클러스터를 작업 하는 방법에 대해 알아봅니다. 자세한 설명서는 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)를 참조하세요.

리비 toorun 대화형 Spark 셸 사용 하거나 Spark에서 실행 하는 일괄 처리 작업 toobe 제출할 수 있습니다. 이 문서 리비 toosubmit 일괄 처리 작업을 사용 하는 방법에 대 한 설명입니다. 이 문서에서 hello 조각을 cURL toomake REST API 호출 toohello 리비 Spark 끝점을 사용합니다.

**필수 조건:**

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.

* [cURL](http://curl.haxx.se/). 이 문서에서는 cURL toodemonstrate HDInsight Spark 클러스터에 대해 toomake REST API 호출 하는 방법입니다.

## <a name="submit-a-livy-spark-batch-job"></a>Livy Spark 배치 작업 제출
일괄 작업을 제출 하기 전에 hello 응용 프로그램 jar hello 클러스터와 연결 된 hello 클러스터 저장소에 업로드 해야 합니다. 사용할 수 있습니다 [ **AzCopy**](../storage/common/storage-use-azcopy.md), 명령줄 유틸리티, toodo 하도록 합니다. 다른 다양 한 클라이언트를 tooupload 데이터를 사용할 수 있습니다. [HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**예제**:

* Hello jar 파일이 hello 클러스터 저장소 (WASB)에 있으면
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Toopass hello jar 파일 이름 및 입력된 파일의 일부로 classname hello (이 예제에서는 input.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Hello 클러스터에서 실행 되는 Spark 리비 일괄 처리에 대 한 정보 가져오기
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**예제**:

* Tooretrieve hello 클러스터에서 실행 중인 모든 hello 리비 Spark 배치 하려면:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Tooretrieve 주어진된 batchId와 특정 일괄 처리 하려는 경우
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Livy Spark 배치 작업 삭제
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**예제**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark 및 고가용성
리비는 hello 클러스터에서 실행 되는 Spark 작업에 대 한 고가용성을 제공 합니다. 다음은 몇 가지 예입니다.

* 원격으로 작업을 제출 하 고 나면 hello 리비 서비스 작동이 중지 된 경우 tooa Spark 클러스터를 hello 작업 toorun hello 백그라운드에서 계속 실행 됩니다. 백업 리비 이면 hello 작업 및 다시 보고서의 hello 상태를 복원 합니다.
* HDInsight에 대 한 Jupyter 노트북 hello 백 엔드에서 리비에 의해 제공 됩니다. 노트북 Spark 작업을 실행 하는 경우 hello 리비 서비스 다시 시작을 가져옵니다 hello 노트북은 toorun hello 코드 셀을 계속 합니다. 

## <a name="show-me-an-example"></a>예제 보기
이 섹션에서는 예제 toouse 리비 Spark toosubmit 일괄 작업 확인, hello 작업의 hello 진행률을 모니터링 하 고 삭제 합니다. hello 응용 프로그램을 사용 하 여이 예제는 hello hello 문서에서 개발한 하나 [HDInsight Spark 클러스터에서 독립 실행형 Scala 응용 프로그램 및 toorun 만들기](hdinsight-apache-spark-create-standalone-application.md)합니다. hello 단계 여기 있다고 가정 합니다.

* Hello 클러스터와 연결 된 hello 응용 프로그램 jar toohello 저장소 계정을 이미 복사 했습니다.
* CuRL 다음이 단계 시도 하 고 있는 hello 컴퓨터에 설치 해야 합니다.

Hello 다음 단계를 수행 합니다.

1. 주세요 먼저 확인 리비 Spark hello 클러스터에서 실행 됩니다. 실행 중인 배치 목록을 가져와서 확인할 수 있습니다. 사용 하 여 리비 hello에 대 한 처음으로 작업을 실행 하는 경우 hello 출력 0을 반환 해야 합니다.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    다음 코드 조각 출력 유사한 toohello을 받습니다.
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello 출력의 마지막 줄에서는 hello 이라고 표시 방법을 **총: 0**, 실행 중인 일괄 처리가 제안입니다.

2. 이제 배치 작업을 제출하도록 합니다. 다음 코드 조각 hello 매개 변수로 입력된 파일 (input.txt) toopass hello jar 이름 및 hello 클래스 이름을 사용 합니다. Windows 컴퓨터에서 다음이 단계를 실행 하는 경우 hello 권장 접근법은 입력된 파일 사용 합니다.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    hello 파일의 매개 변수를 hello **input.txt** ´ ï ´ ù.
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    다음 코드 조각 출력 유사한 toohello를 나타나야 합니다.
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello hello 출력의 마지막 행 이라고 표시 방법을 **상태: 시작**합니다. 또한 **id:0**을 말합니다. 여기에서 **0** hello 일괄 처리 ID입니다.

3. 이제 hello 일괄 처리 id입니다. 사용 하 여이 특정 일괄 처리의 hello 상태를 검색할 수 있습니다.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    다음 코드 조각 출력 유사한 toohello를 나타나야 합니다.
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    hello 출력에서는 이제 **상태: 성공**, 해당 hello 작업 제안는 성공적으로 완료 되었습니다.

4. 원하는 경우 이제 hello 일괄 처리를 삭제할 수 있습니다.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    다음 코드 조각 출력 유사한 toohello를 나타나야 합니다.
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    hello hello 출력의 마지막 줄에서는 해당 hello 일괄 처리 삭제 되었습니다. Hello 작업을 해제도 실행 되는 동안 작업을 삭제 합니다. 그렇지 않은 경우 또는 성공적으로 완료 된 작업을 삭제 하는 경우 작업 정보 hello 완전히 삭제 됩니다.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>HDInsight 3.5 클러스터에서 Livy Spark 사용

기본적으로 3.5 HDInsight 클러스터는 로컬 파일 경로 tooaccess 샘플 데이터 파일이 나 jar 사용을 해제합니다. 사용자는 좋습니다 toouse hello `wasb://` 경로 대신 tooaccess jar 예제 데이터 파일 또는 hello 클러스터에서 합니다. Toouse 로컬 경로 사용 하지 않으려면 hello Ambari 구성을 적절 하 게 업데이트 해야 합니다. toodo 하므로:

1. Hello 클러스터에 대 한 toohello Ambari 포털을 이동 합니다. hello Ambari 웹 UI는 https://에서 HDInsight 클러스터에서 사용할 수 있는**CLUSTERNAME**. 여기서 CLUSTERNAME는 클러스터의 이름을 hello azurehdidnsight.net 합니다.

2. 왼쪽 탐색 hello에서 클릭 **리비**, 클릭 하 고 **Configs**합니다.

3. 아래 **리비 기본** hello 속성 이름을 추가 `livy.file.local-dir-whitelist` 너무 그 값을 설정 하 고**"/"** tooallow 대 한 모든 권한을 toofile 시스템입니다. 특정 디렉터리에만 tooa tooallow 액세스 하려는 경우 hello 경로 toothat 디렉터리 hello 값으로 제공 합니다.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Azure Virtual Network 내에서 클러스터에 대한 Livy 작업 제출

Tooan Azure 가상 네트워크 내에서 HDInsight Spark 클러스터를 연결 하면 tooLivy hello 클러스터에 직접 연결할 수 있습니다. 이러한 경우 URL 리비 끝점은 hello `http://<IP address of hello headnode>:8998/batches`합니다. 여기에서 **8998** 리비 hello 클러스터 헤드 노드에에서 실행 되는 hello 포트입니다. 비공용 포트의 서비스 액세스에 대한 자세한 내용은 [HDInsight의 Hadoop 서비스에서 사용하는 포트](hdinsight-hadoop-port-settings-for-services.md)를 참조하세요.

## <a name="troubleshooting"></a>문제 해결

다음은 원격 작업 제출 tooSpark 클러스터에 대 한 리비를 사용 하는 동안에 실행 될 수 있는 몇 가지 문제입니다.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>외부 jar hello 추가 저장소를 사용 하 여 수 없습니다.

**문제:** 리비 Spark 작업을 참조 하는 외부 jar hello 클러스터와 연결 된 hello 추가 저장소 계정에서 hello 작업이 실패 합니다.

**해결 방법:** 해당 hello jar 원하는 toouse hello HDInsight 클러스터와 연결 된 hello 기본 저장소에서 사용할 수 있는지 확인 합니다.





## <a name="next-step"></a>다음 단계

* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

