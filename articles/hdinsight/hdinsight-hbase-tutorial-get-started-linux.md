---
title: "Azure HDInsight에서 HBase 첫 번째 예 aaaGet 시작 | Microsoft Docs"
description: "HDInsight에서 hadoop을 사용 하 여 Apache HBase 예제 toostart이를 수행 합니다. HBase 셸 hello에서 테이블을 만들고 해당 데이터를 쿼리할 하이브를 사용 하 여 합니다."
keywords: "hbasecommand, hbase 예제"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>HDInsight에서 Apache HBase 예제 시작

Toocreate HDInsight에서 HBase 클러스터의 HBase 테이블을 만들 및 하이브를 사용 하 여 테이블 내용을 쿼리 방법을 알아봅니다. 일반 HBase 정보는 [HDInsight HBase 개요][hdinsight-hbase-overview]를 참조하세요.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>필수 조건
HBase 예제 시도 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* [SSH(Secure Shell)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>HBase 클러스터 만들기
hello 다음 절차에서는 Azure 리소스 관리자 템플릿 toocreate 버전 3.4 Linux 기반 HBase 클러스터와 hello 종속 된 기본 Azure 저장소 계정 다른 클러스터 만들기 방법을 hello 프로시저에 사용 되는 toounderstand hello 매개 변수 참조 [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](hdinsight-hadoop-provision-linux-clusters.md)합니다.

1. Hello 이미지 tooopen hello 템플릿을 hello Azure 포털에서에서 다음을 클릭 합니다. hello 서식 파일은 공용 blob 컨테이너에 있습니다. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Hello에서 **사용자 지정 배포** 블레이드에서 hello 다음 값을 입력 합니다.
   
   * **구독**: 사용 되는 toocreate hello 클러스터를 Azure 구독을 선택 합니다.
   * **리소스 그룹**: Azure 리소스 관리 그룹을 만들거나 기존 그룹을 사용합니다.
   * **위치**: hello 리소스 그룹의 hello 위치를 지정 합니다. 
   * **ClusterName**: hello HBase 클러스터에 대 한 이름을 입력 합니다.
   * **로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 **admin**합니다.
   * **SSH 사용자 이름 및 암호**: hello 기본 사용자 이름은 **sshuser**합니다.  이름은 변경할 수 있습니다.
     
     다른 매개 변수는 선택 사항입니다.  
     
     각 클러스터에는 Azure Storage 계정 종속성이 있습니다. 클러스터를 삭제 한 후 hello 데이터 hello 저장소 계정에 유지 됩니다. hello 클러스터 기본 저장소 계정 이름은 "store"가 추가 된 hello 클러스터 이름이입니다. Hello 템플릿 변수 섹션에서 하드 코드 된 경우
3. 선택 **toohello 약관 위에서 설명한 동의**, 클릭 하 고 **구매**합니다. 클러스터 toocreate 약 20 분이 필요합니다.

> [!NOTE]
> Hello를 사용 하 여 다른 HBase 클러스터를 만들 수 HBase 클러스터를 삭제 한 후 동일한 기본 blob 컨테이너입니다. 새 클러스터 hello hello 원본 클러스터에서 만든 hello HBase 테이블을 선택 합니다. tooavoid 불일치 hello 클러스터를 삭제 하기 전에 hello HBase 테이블을 사용 하지 않도록 설정 하는 두는 것이 좋습니다.
> 
> 

## <a name="create-tables-and-insert-data"></a>테이블 만들기 및 데이터 삽입
SSH tooconnect tooHBase 클러스터를 사용 하 고 HBase 셸 toocreate HBase 테이블을 사용 하 여, 데이터 및 쿼리 데이터를 삽입 수 있습니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

대부분의 사용자에 대 한 데이터 hello 표 형식으로 나타납니다.

![HDInsight HBase 테이블 형식 데이터][img-hbase-sample-data-tabular]

HBase (포함 하는 BigTable의 구현)에서 다음과 같은 동일한 데이터가 hello:

![HDInsight HBase BigTable 데이터][img-hbase-sample-data-bigtable]


**HBase 셸 toouse hello**

1. SSH에서 hello 다음 HBase 명령을 실행 합니다.
   
    ```bash
    hbase shell
    ```

2. 두 열 패밀리가 있는 HBase를 만듭니다.

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. 일부 데이터 삽입:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase 셸][img-hbase-shell]
4. 단일 행 가져오기
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    행을 하나만 있기 때문에 hello 스캔 명령을 사용 하 여 hello 같은 결과 표시 되어야 합니다.
   
    Hello HBase 테이블 스키마에 대 한 자세한 내용은 참조 [소개 tooHBase 스키마 디자인][hbase-schema]합니다. HBase 명령에 대한 자세한 내용은 [Apache HBase 참조 가이드][hbase-quick-start]를 참조하세요.
5. 종료 hello 셸
   
    ```hbaseshell
    exit
    ```

**toobulk hello 연락처 HBase 테이블로 데이터 로드**

HBase는 테이블로 데이터를 로드하는 여러 방법을 포함합니다.  자세한 내용은 [대량 로드](http://hbase.apache.org/book.html#arch.bulk.load)를 참조하세요.

샘플 데이터 파일은 공용 Blob 컨테이너인 *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*에 있습니다.  hello 데이터 파일의 hello 콘텐츠가입니다.

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

필요에 따라 텍스트 파일을 만들고 hello 파일 tooyour 고유한 저장소 계정에 업로드 수 있습니다. Hello 지침은 [HDInsight에서 Hadoop 작업에 대 한 데이터 업로드][hdinsight-upload-data]합니다.

> [!NOTE]
> 이 절차는 hello 마지막 절차에서 만든 hello 연락처 HBase 테이블을 사용 합니다.
> 

1. SSH, 다음 명령은 tootransform hello 데이터 tooStoreFiles를 파일 및 Dimporttsv.bulk.output로 지정 된 상대 경로에 저장 하는 hello를 실행 합니다.  HBase 셸에 있는 경우 종료 명령 tooexit hello를 사용 합니다.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Hello 명령 tooupload hello 데이터 /example/data/storeDataFileOutput toohello HBase 테이블에서 다음을 실행 합니다.
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. Hello HBase 셸을 열고 hello 스캔 명령 toolist hello 테이블 콘텐츠를 사용할 수 있습니다.

## <a name="use-hive-tooquery-hbase"></a>하이브 tooquery HBase를 사용 하 여

Hive를 사용하여 HBase 테이블의 데이터를 쿼리할 수 있습니다. 이 섹션에서는 테이블을 만들면 하이브는 toohello HBase 테이블을 매핑하고 HBase 테이블의 tooquery hello 데이터를 사용 합니다.

1. 열기 **PuTTY**, toohello 클러스터에 연결 하 고 있습니다.  Hello 이전 절차의 hello 지침을 참조 하십시오.
2. Hello SSH 세션에서 다음 명령을 toostart Beeline hello를 사용 합니다.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Beeline에 대한 자세한 내용은 [Beeline을 사용하여 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-beeline.md)을 참조하세요.
       
3. HiveQL 스크립트 toocreate 다음 hello toohello HBase 테이블로 매핑된 하이브 테이블을 실행 합니다. 이 문을 실행 하기 전에 HBase 셸을 hello를 사용 하 여이 자습서의 앞부분에 언급 된 hello 예제 테이블을 만들었는지 확인 합니다.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Hello hello HBase 테이블에 HiveQL 스크립트 tooquery hello 데이터가 다음을 실행 합니다.

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Curl을 사용하여 HBase REST API 사용

hello REST API는을 통해 보안 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다. 항상 보안 HTTP (HTTPS) toohelp 보내지도록 자격 증명은 안전 하 게 toohello 서버를 사용 하 여 요청을 확인 해야 합니다.

2. 다음 명령은 toolist hello 기존 HBase 표 hello를 사용 합니다.

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. 명령 toocreate 2 열 제품군으로 새 HBase 테이블을 다음 hello를 사용 합니다.

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    hello 스키마 hello JSon 형식으로 제공 됩니다.
4. 다음 명령은 tooinsert hello 일부 데이터를 사용 합니다.

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    Base64 해야 hello-d 스위치에 지정 된 hello 값 인코딩합니다. Hello 예제:
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [false-행 키](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert 사용 하면 여러 (일괄 처리 된) 값입니다.
5. 다음 명령 tooget 행 hello를 사용 합니다.
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

HBase Rest에 대한 자세한 내용은 [Apache HBase 참조 가이드](https://hbase.apache.org/book.html#_rest)를 참조하세요.

> [!NOTE]
> Thrift는 HDInsight의 HBase에서 지원되지 않습니다.
>
> Curl 또는 기타 REST 통신와 함께 사용할 경우 WebHCat hello 사용자 이름 및 관리자에 게 HDInsight 클러스터에 대 한 암호를 제공 하 여 hello 요청을 인증 해야 합니다. Hello 식별자 URI (Uniform Resource)의 일부 toosend hello 요청 toohello 서버 사용에 hello 클러스터 이름을 사용 해야 합니다.
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    응답에 따라 응답 비슷한 toohello을 받게 됩니다.
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>클러스터 상태 확인
HDInsight에서 HBase는 클러스터 모니터링에 대한 웹 UI와 함께 제공됩니다. Hello 웹 UI를 사용 하 여 통계 또는 지역에 대 한 정보를 요청할 수 있습니다.

**tooaccess hello HBase 마스터 UI**

1. Hello에 로그인 https://에서 Ambari 웹 UI hello&lt;Clustername >. azurehdinsight.net 합니다.
2. 클릭 **HBase** hello 왼쪽된 메뉴에서 합니다.
3. 클릭 **빠른 링크** hello 페이지에서 지점 toohello 활성 사육 노드 링크의 맨 위에 hello 되 고 클릭 **HBase 마스터 UI**합니다.  hello UI를 다른 브라우저 탭에서 열:

  ![HDInsight HBase HMaster UI](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  hello를 HBase 마스터 UI는 다음 섹션 hello를 포함 되어 있습니다.

  - 지역 서버
  - 백업 마스터
  - 테이블
  - 태스크
  - 소프트웨어 특성

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.
tooavoid 불일치 hello 클러스터를 삭제 하기 전에 hello HBase 테이블을 사용 하지 않도록 설정 하는 두는 것이 좋습니다.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계
이 문서에서는 toocreate HBase 클러스터 및 toocreate 테이블 및 뷰 hello에서 이러한 테이블의 데이터가 어떻게 HBase 셸을 hello 방법을 배웠습니다. 또한 toouse 하이브 HBase 테이블을 데이터 HBase 테이블 및 toouse HBase C# REST Api toocreate hello 하는 방법에 대해 쿼리 및 hello 테이블에서 데이터를 검색할 방법을 배웠습니다.

toolearn 더 참조 하십시오.

* [HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
