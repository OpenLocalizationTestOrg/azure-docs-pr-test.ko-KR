---
title: "Azure HDInsight에 Curl와 Hadoop 하이브 aaaUse | Microsoft Docs"
description: "Tooremotely 전송 Pig tooHDInsight Curl을 사용 하 여 작업 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>REST를 사용하여 HDInsight에서 Hadoop으로 Hive 쿼리 실행

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Azure HDInsight 클러스터에서 하이브 toouse hello WebHCat REST API toorun Hadoop으로 쿼리 하는 방법에 대해 알아봅니다.

[Curl](http://curl.haxx.se/) 수의 상호 작용 HDInsight 원시 HTTP 요청을 사용 하 여 사용 되는 toodemonstrate 됩니다. hello [jq](http://stedolan.github.io/jq/) 유틸리티는 REST 요청에서 반환 된 사용 되는 tooprocess hello JSON 데이터입니다.

> [!NOTE]
> Linux 기반 Hadoop 서버를 사용 하 여 사용 하 던 해도 새 tooHDInsight는 경우 참조 hello [필요한 Linux 기반 HDInsight의 Hadoop에 대 한 tooknow](hdinsight-hadoop-linux-information.md) 문서.

## <a id="curl"></a>Hive 쿼리 실행

> [!NOTE]
> CURL 또는 기타 REST 통신와 함께 사용할 경우 WebHCat hello 사용자 이름 및 관리자에 게 HDInsight 클러스터에 대 한 암호를 제공 하 여 hello 요청을 인증 해야 합니다.
>
> 이 섹션의 hello 명령에 대 한 대체 **USERNAME** 을 바꾸고 hello 사용자 tooauthenticate toohello 클러스터 **암호** hello hello 사용자 계정의 암호를 사용 합니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.
>
> hello REST API는을 통해 보안 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다. toohelp 고 자격 증명이 안전 하 게 확인 보안 HTTP (HTTPS)을 사용 하 여 전송 된 toohello 서버 항상 요청을 확인 합니다.

1. 명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    텍스트 다음 응답 비슷한 toohello를 나타납니다.

        {"status":"ok","version":"v1"}

    이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.

   * **-u** -hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청 합니다.
   * **-G** - 이 요청이 GET 작업임을 나타냅니다.

     hello URL의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다. hello 경로 **/status**, hello 서버에 대 한 해당 hello 요청은 tooreturn WebHCat (Templeton이 라고도 함)의 상태를 나타냅니다. Hello 다음 명령을 사용 하 여 하이브 hello 버전을 요청할 수도 있습니다.

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     이 요청에는 텍스트 다음 응답 비슷한 toohello를 반환 합니다.

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}

2. Toocreate 라는 테이블을 다음 사용 하 여 hello **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    이 요청과 함께 사용 되는 매개 변수 뒤 hello:

   * **-d** -이후 `-G` 을 사용 하지 않으면 hello 요청 toohello POST 메서드를 기본값입니다. `-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.

     * **user.name** -hello 명령을 실행 하는 hello 사용자입니다.
     * **실행** -HiveQL 문은 tooexecute hello 합니다.
     * **statusdir** -이 작업에 대 한 상태 hello hello 디렉터리에 기록 됩니다.

     이러한 문은 hello 다음 작업을 수행 합니다.
   * **DROP TABLE** -hello 테이블이 이미 있으면 삭제 됩니다.
   * **CREATE EXTERNAL TABLE** - Hive에서 새 ‘외부’ 테이블을 만듭니다. 외부 테이블 하이브에 hello 테이블 정의 저장 됩니다. hello 데이터는 hello 원래 위치에 남아 있습니다.

     > [!NOTE]
     > 외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다. 예를 들어 자동화된 데이터 업로드 프로세스 또는 다른 MapReduce 작업이 있습니다.
     >
     > 외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.

   * **행 형식** hello 데이터의 서식을 지정 하는 방법-합니다. 각 로그에 hello 필드는 공백으로 구분 됩니다.
   * **AS 텍스트 파일 저장 위치** -hello 데이터가 저장 되는 경우 (hello 예제/데이터 디렉터리) 텍스트로 저장 됩니다.
   * **선택** -모든 행의 개수를 선택 합니다. 여기서 열 **t4** hello 값이 포함 된 **[오류]**합니다. 이 값이 포함된 행이 3개이므로 이 문은 **3** 값을 반환합니다.

     > [!NOTE]
     > Hello HiveQL 문은 사이 공백이 hello로 대체 됩니다 `+` Curl 함께 사용 하는 경우 문자입니다. Hello 구분 기호 같이 공백을 포함 하는 따옴표로 묶인된 값으로 대체 되어야 하지 `+`합니다.

   * **'%25.log'와 같은 INPUT__FILE__NAME** -이 문의 제한 hello 검색 tooonly 사용으로 끝나는 파일. 로그입니다.

     > [!NOTE]
     > hello `%25` hello URL로 인코딩된 형식의 %, 하는 hello 실제 상태 이므로 `like '%.log'`합니다. hello %의 toobe URL로 인코딩된, Url의 특수 문자로 처리 됩니다.

     이 명령은 hello 작업의 사용된 toocheck hello 상태가 될 수 있는 작업 ID를 반환 해야 합니다.

       {"id":"job_1415651640909_0026"}

3. 다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    대체 **JOBID** hello 이전 단계에서 반환 된 hello 값을 사용 합니다. 예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, 다음 **JOBID** 것 `job_1415651640909_0026`합니다.

    Hello 작업이 완료 되 면 hello 상태는 **SUCCEEDED**합니다.

   > [!NOTE]
   > 이 Curl 요청 hello 작업에 대 한 정보로 개체 JSON (JavaScript Notation) 문서를 반환합니다. Jq 사용 되는 tooretrieve 상태 값을 hello만 합니다.

4. Hello 작업의 hello 상태가 너무 변경 되 면**SUCCEEDED**, Azure Blob 저장소에서 hello 작업의 hello 결과 검색할 수 있습니다. hello `statusdir` hello 출력 파일의;이 경우 hello 위치를 포함 하는 hello 쿼리와 함께 전달 된 매개 변수 **/예제/curl**합니다. 이 주소 hello에 hello 출력 저장 **예제/curl** hello에 대 한 디렉터리는 기본 저장소를 클러스터 합니다.

    나열 하 고 hello를 사용 하 여 이러한 파일을 다운로드할 수 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)합니다. Hello Azure CLI를 사용 하 여 Azure 저장소에 대 한 자세한 내용은 참조 hello [Azure 저장소와 Azure CLI 2.0 사용](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) 문서.

5. 다음 문은 toocreate 라는 새 'internal' 테이블이 사용 하 여 hello **살펴볼**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    이러한 문은 hello 다음 작업을 수행 합니다.

   * **CREATE TABLE IF NOT EXISTS** - 테이블이 아직 없는 경우 테이블을 만듭니다. 이 문은 hello 하이브 데이터 웨어하우스에 저장 된 Hive에서 완전히 관리 되 고 있는 한 내부 테이블을 만듭니다.

     > [!NOTE]
     > 외부 테이블의 경우와 달리 hello 기본 데이터도 삭제 내부 테이블을 삭제 합니다.

   * **AS ORC 저장** -hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장 합니다. ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.
   * **덮어쓰기 삽입... 선택** -hello에서 행을 선택 **log4jLogs** 이 있는 테이블 **[오류]**, 삽입 hello에 데이터를 hello 다음 **살펴볼** 테이블입니다.
   * **선택** -새 hello에서 모든 행을 선택 **살펴볼** 테이블입니다.

6. Hello 작업의 toocheck hello 상태를 반환 하는 hello 작업 ID를 사용 합니다. 처리가 성공 하면 일단 hello hello 결과 toodownload 및 보기 앞에서 설명한 대로 Azure CLI를 사용 합니다. hello 출력 모두 포함 하는 세 줄을 포함 해야 **[오류]**합니다.

## <a id="nextsteps"></a>다음 단계

HDInsight Hive에 대한 일반적인 내용입니다.

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)

Tez 하이브가 있는 사용 하는 경우 hello 다음 디버깅 정보에 대 한 문서를 참조 하세요.

* [Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여](hdinsight-debug-ambari-tez-view.md)

이 문서에 사용 된 REST API hello에 대 한 자세한 내용은 참조 hello [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) 문서.

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


