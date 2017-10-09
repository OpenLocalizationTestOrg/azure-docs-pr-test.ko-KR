---
title: "MapReduce aaaUse 및 Azure HDInsight에서 Hadoop으로 Curl | Microsoft Docs"
description: "어떻게 tooremotely MapReduce 작업으로 실행 Hadoop HDInsight에 Curl을 사용 하 여에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>REST를 사용하여 HDInsight에서 Hadoop으로 MapReduce 작업 실행

HDInsight 클러스터에서 Hadoop에서 toouse hello WebHCat REST API toorun MapReduce 작업 하는 방법에 대해 알아봅니다. Curl 수의 상호 작용 HDInsight 원시 HTTP 요청 toorun MapReduce 작업을 사용 하 여 사용 되는 toodemonstrate입니다.

> [!NOTE]
> Linux 기반 Hadoop 서버를 사용 하 여 이미 익숙한 새 tooHDInsight는 표시 되지만 참조 hello [필요한 HDInsight의 Linux 기반 Hadoop에 대 한 tooknow](hdinsight-hadoop-linux-information.md) 문서.


## <a id="prereq"></a>필수 조건

* HDInsight 클러스터의 Hadoop
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Curl을 사용하여 MapReduce 작업 실행

> [!NOTE]
> WebHCat와 Curl 또는 기타 REST 통신을 사용할 경우 hello HDInsight 클러스터 관리자 사용자 이름 및 암호를 제공 하 여 hello 요청을 인증 해야 합니다. URI 사용 하는 toosend hello 요청 toohello 서버 hello의 일환으로 hello 클러스터 이름을 사용 해야 합니다.
>
> 이 섹션의 hello 명령에 대 한 대체 **USERNAME** hello 사용자 tooauthenticate toohello 클러스터와 및 **암호** hello hello 사용자 계정의 암호를 사용 합니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.
>
> hello REST API가 사용 하 여 보안 [기본 액세스 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다. 항상 HTTPS tooensure 사용자 자격 증명을 안전 하 게 보냄을 toohello 서버를 사용 하 여 요청을 확인 해야 합니다.


1. 명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    다음 JSON 응답 비슷한 toohello을 받게 됩니다.

        {"status":"ok","version":"v1"}

    이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.

   * **-u**: hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청을 나타냅니다
   * **-G**: 이 작업이 GET 요청임을 나타냅니다.

     hello URI의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다.

2. MapReduce 작업 toosubmit hello 다음 명령을 사용 합니다.

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    hello (/ mapreduce/jar) URI의 hello 끝이이 요청 jar 파일의 클래스에서 MapReduce 작업을 시작 됨 WebHCat을 알려 줍니다. 이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.

   * **-d**: `-G` 은 사용 되지 않으므로 hello 요청 toohello POST 메서드를 기본값입니다. `-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.
    * **user.name**: hello 명령을 실행 하는 hello 사용자
    * **jar**: hello 위치 toobe 클래스를 포함 하는 hello jar 파일의 실행
    * **클래스**: hello hello MapReduce 논리를 포함 하는 클래스
    * **arg**: hello 인수 toobe toohello MapReduce 작업을 전달 합니다. 이 경우 hello 입력 hello 출력에 사용 되는 텍스트 파일과 hello 디렉터리

     이 명령은 hello 작업의 사용된 toocheck hello 상태가 될 수 있는 작업 ID를 반환 해야 합니다.

       {"id":"job_1415651640909_0026"}

3. 다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Hello 대체 **JOBID** hello 이전 단계에서 반환 된 hello 값을 사용 합니다. 예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, JOBID 것 hello 다음 `job_1415651640909_0026`합니다.

    Hello 작업이 완료 되 면 hello 상태는 반환 `SUCCEEDED`합니다.

   > [!NOTE]
   > 이 Curl 요청 hello 작업에 대 한 정보가 포함 된 JSON 문서를 반환합니다. Jq 사용 되는 tooretrieve 상태 값을 hello만 합니다.

4. Hello 작업의 상태 hello 너무 변경 될 때`SUCCEEDED`, Azure Blob 저장소에서 hello 작업의 hello 결과 검색할 수 있습니다. hello `statusdir` hello 쿼리와 함께 전달 되는 매개 변수는 hello 출력 파일의 hello 위치를 포함 합니다. 이 예제에서는 hello 위치가 `/example/curl`합니다. 이 주소는 hello 작업의 출력 hello hello 클러스터 기본 저장소 위치에 저장 `/example/curl`합니다.

나열 하 고 hello를 사용 하 여 이러한 파일을 다운로드할 수 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다. Hello Azure CLI에서에서 blob 사용한 작업에 대 한 자세한 내용은 참조 hello [hello를 사용 하 여 Azure 저장소와 Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs) 문서.

## <a id="nextsteps"></a>다음 단계

HDInsight의 MapReduce 작업에 대한 일반적인 정보:

* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)

이 문서에서 사용 되는 REST 인터페이스를 hello에 대 한 자세한 내용은 참조 hello [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)합니다.
