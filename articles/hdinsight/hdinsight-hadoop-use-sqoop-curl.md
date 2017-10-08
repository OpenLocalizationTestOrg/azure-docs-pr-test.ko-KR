---
title: "Azure HDInsight에 Curl와 Hadoop Sqoop aaaUse | Microsoft Docs"
description: "Tooremotely Sqoop 작업 tooHDInsight Curl을 사용 하 여 전송 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Curl을 사용하여 HDInsight에서 Hadoop으로 Sqoop 작업 실행
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

HDInsight에서 Hadoop에 대 한 toouse Curl toorun Sqoop 작업 클러스터링 하는 방법을 알아봅니다.

Curl 수의 상호 작용 HDInsight 원시 HTTP 요청 toorun, 모니터 및 hello 결과 Sqoop 작업의 검색을 사용 하 여 사용 되는 toodemonstrate입니다. WebHCat REST API (이전의 Templeton) HDInsight 클러스터에 제공한 hello를 사용 하 여 작동 합니다.

> [!NOTE]
> Linux 기반 Hadoop 서버를 사용 하 여 사용 하 던 해도 새 tooHDInsight는 경우 참조 [Linux에서 HDInsight를 사용 하는 방법은](hdinsight-hadoop-linux-information.md)합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.

* HDInsight 클러스터에서 Hadoop(Linux 또는 Windows 기반)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Curl을 사용하여 Sqoop 작업 제출
> [!NOTE]
> Curl 또는 기타 REST 통신와 함께 사용할 경우 WebHCat hello 사용자 이름 및 관리자에 게 HDInsight 클러스터에 대 한 암호를 제공 하 여 hello 요청을 인증 해야 합니다. 또한 hello 클러스터 이름을 사용 하 여 hello 식별자 URI (Uniform Resource)의 일부 toosend hello 요청 toohello 서버를 사용 해야 합니다.
> 
> 이 섹션의 hello 명령에 대 한 대체 **USERNAME** 을 바꾸고 hello 사용자 tooauthenticate toohello 클러스터 **암호** hello hello 사용자 계정의 암호를 사용 합니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.
> 
> hello REST API는을 통해 보안 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다. 항상 보안 HTTP (HTTPS) toohelp 보내지도록 자격 증명은 안전 하 게 toohello 서버를 사용 하 여 요청을 확인 해야 합니다.
> 
> 

1. 명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    응답 비슷한 toohello 다음을 받게 됩니다.
   
        {"status":"ok","version":"v1"}
   
    이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.
   
   * **-u** -hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청 합니다.
   * **-G** - GET 요청임을 나타냅니다.
     
     hello URL의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다. hello 경로 **/status**, hello 서버에 대 한 해당 hello 요청은 tooreturn WebHCat (Templeton이 라고도 함)의 상태를 나타냅니다. 
2. Toosubmit sqoop 작업을 수행 하는 hello를 사용 합니다.

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.

    * **-d** -이후 `-G` 을 사용 하지 않으면 hello 요청 toohello POST 메서드를 기본값입니다. `-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.

        * **user.name** -hello 명령을 실행 하는 hello 사용자입니다.

        * **명령** -Sqoop 명령 tooexecute hello 합니다.

        * **statusdir** -이 작업에 대 한 상태 hello hello 디렉터리에 기록 됩니다.

    이 명령은 hello 작업의 사용된 toocheck hello 상태가 될 수 있는 작업 ID를 반환 해야 합니다.

        {"id":"job_1415651640909_0026"}

1. 다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태입니다. 대체 **JOBID** hello 이전 단계에서 반환 된 hello 값을 사용 합니다. 예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, 다음 **JOBID** 것 `job_1415651640909_0026`합니다.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Hello 상태가 됩니다 hello 작업을 마친 경우 **SUCCEEDED**합니다.
   
   > [!NOTE]
   > 이 Curl 요청 hello 작업;에 대 한 정보로 개체 JSON (JavaScript Notation) 문서를 반환합니다. jq 사용 되는 tooretrieve 상태 값을 hello만 합니다.
   > 
   > 
2. Hello 작업의 hello 상태가 너무 변경 되 면**SUCCEEDED**, Azure Blob 저장소에서 hello 작업의 hello 결과 검색할 수 있습니다. hello `statusdir` hello 출력 파일의;이 경우 hello 위치를 포함 하는 hello 쿼리와 함께 전달 된 매개 변수 **wasb: / / / 예제/curl**합니다. 이 주소 hello에 hello 작업의 출력 hello 저장 **예제/curl** 디렉터리 HDInsight 클러스터에서 사용 하는 hello 기본 저장소 컨테이너에 있습니다.
   
    나열 하 고 hello를 사용 하 여 이러한 파일을 다운로드할 수 [Azure CLI](../cli-install-nodejs.md)합니다. 예를 들어 toolist 파일에 **예제/curl**, hello 다음 명령을 사용 하 여:
   
        azure storage blob list <container-name> example/curl
   
    파일을 toodownload hello 다음을 사용 합니다.
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Hello hello를 사용 하 여 hello blob이 포함 된 저장소 계정 이름 지정 `-a` 및 `-k` 매개 변수 또는 집합 hello **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_액세스\_키** 환경 변수입니다. 자세한 내용은 <a href="hdinsight-upload-data.md" target="_blank"를 참조하세요.
   > 
   > 

## <a name="limitations"></a>제한 사항
* 대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.
* 일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 삽입을 수행 합니다.

## <a name="summary"></a>요약
이 문서에서 볼 수 있듯이, HDInsight 클러스터에 원시 HTTP 요청 toorun, 모니터 및 보기 hello 결과 Sqoop 작업을 사용할 수 있습니다.

이 문서에서 사용 하는 hello REST 인터페이스에 대 한 자세한 내용은 참조 hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API 가이드</a>합니다.

## <a name="next-steps"></a>다음 단계
HDInsight Hive에 대한 일반적인 내용입니다.

* [HDInsight에서 Hadoop과 Sqoop 사용](hdinsight-use-sqoop.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)

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


