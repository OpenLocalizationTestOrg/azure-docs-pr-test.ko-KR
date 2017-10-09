---
title: "Linux 기반 HDInsight-Azure의 Solr aaaUse 스크립트 동작 tooinstall | Microsoft Docs"
description: "Linux 기반 HDInsight Hadoop에서 Solr tooinstall 스크립트 동작을 사용 하는 클러스터 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>HDInsight Hadoop 클러스터에서 Solr 설치 및 사용

자세한 내용은 방법 스크립트를 사용 하 여 Azure HDInsight의 Solr tooinstall 합니다. Solr은 강력한 검색 플랫폼으로서 Hadoop에서 관리하는 데이터에 대한 엔터프라이즈 수준의 검색 기능을 제공합니다.

> [!IMPORTANT]
    > 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

> [!IMPORTANT]
> 이 문서에 사용 된 hello 샘플 스크립트는 특정 구성으로 Solr 4.9를 설치 합니다. 다양 한 컬렉션, 분할 된 데이터베이스, 스키마, 복제본 등 tooconfigure hello Solr 클러스터 하려는 경우 hello 스크립트 및 Solr 이진 파일을 수정 해야 합니다.

## <a name="whatis"></a>Solr이란

[Apache Solr](http://lucene.apache.org/solr/features.html)은 데이터에 대한 강력한 전체 텍스트 검색을 가능하게 해주는 엔터프라이즈 검색 플랫폼입니다. Hadoop에 저장 하 고 방대한 양의 데이터를 관리 있습니다, Apache Solr hello 검색 기능이 제공 tooquickly hello 데이터를 검색 합니다.

> [!WARNING]
> Hello HDInsight 클러스터와 함께 제공 되는 구성 요소는 Microsoft에서 완전히 지원 됩니다.
>
> Solr 같은 사용자 지정 구성 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다. Microsoft 지원에 수 tooresolve 문제를 사용자 지정 구성 요소를 사용할 수 없습니다. 지원용 tooengage hello 오픈 소스 커뮤니티를 할 수 있습니다. 예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).

## <a name="what-hello-script-does"></a>어떤 hello이 스크립트는

이 스크립트에서는 hello 변경 toohello HDInsight 클러스터를 수행 합니다.

* `/usr/hdp/current/solr`에 Solr 4.9 설치
* 사용자를 만드는 **solrusr**, 하는 사용 되는 toorun hello Solr 서비스
* 집합 **solruser** hello 소유자`/usr/hdp/current/solr`
* Solr을 자동으로 시작하는 [Upstart](http://upstart.ubuntu.com/) 구성을 추가합니다.

## <a name="install"></a>스크립트 동작을 사용하여 Solr 설치

HDInsight 클러스터에서 샘플 스크립트 tooinstall Solr hello 수정할 수 있는 위치에서 제공 됩니다.

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

Solr 설치 되어 있는 클러스터 toocreate hello에서 단계를 사용 하 여 hello [만들 HDInsight 클러스터](hdinsight-hadoop-create-linux-clusters-portal.md) 문서. Hello 만드는 프로세스 동안 다음 단계 tooinstall Solr hello를 사용 합니다.

1. Hello에서 __클러스터 요약__ 블레이드, select__Advanced settings__, 다음 __스크립트 작업을__합니다. 다음 정보 toopopulate hello 양식 hello를 사용 합니다.

   * **이름**: hello 스크립트 동작에 대 한 이름을 입력 합니다.
   * **SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**: 이 옵션 선택
   * **WORKER**: 이 옵션을 선택합니다.
   * **사육**:이 옵션 tooinstall hello 사육 노드 확인
   * **PARAMETERS**: 이 필드는 공백으로 둡니다.

2. Hello hello 맨 아래에 **스크립트 작업을** 블레이드에서 사용 하 여 hello **선택** 단추 toosave hello 구성 합니다. 마지막으로 hello를 사용 하 여 **다음** 단추 tooreturn toohello __클러스터 요약__

3. Hello에서 __클러스터 요약__ 페이지에서 __만들기__ toocreate hello 클러스터입니다.

## <a name="usesolr"></a>HDInsight에서 Solr을 사용하는 방법

> [!IMPORTANT]
> 이 섹션의 단계 hello 기본 Solr 기능을 보여 줍니다. Solr 사용에 대 한 자세한 내용은 참조 hello [Apache Solr 사이트](http://lucene.apache.org/solr/)합니다.

### <a name="index-data"></a>데이터 인덱싱

다음 단계 tooadd 예제 데이터 tooSolr hello를 사용 하 고 쿼리할 수 있습니다:

1. SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

     > [!IMPORTANT]
     > 이 문서의 뒷부분에 나오는 단계 SSL 터널 tooconnect toohello Solr 웹 UI를 사용합니다. 이 단계는 toouse, SSL을 설정 해야 터널 및 다음 브라우저 toouse 구성 것입니다.
     >
     > 자세한 내용은 참조 hello [사용 하 여 SSH 터널링 HDInsight와](hdinsight-linux-ambari-ssh-tunnel.md) 문서.

2. 같은 명령 toohave Solr 인덱스 샘플 데이터가 hello를 사용 합니다.

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    hello 다음 출력은 반환 toohello 콘솔:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    hello `post.jar` hello를 추가 하는 유틸리티 **solr.xml** 및 **monitor.xml** 문서 toohello 인덱스입니다.
  
3. Hello 다음 명령 tooquery hello Solr REST API를 사용 합니다.

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    이 명령은 검색 **collection1** 일치 하는 모든 문서에 대해  **\*:\***  (로 인코딩된 \*%3A\* hello 쿼리 문자열에). 다음 JSON 문서 hello은 hello 응답의 예:

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>Hello Solr 대시보드를 사용 하 여

hello Solr 대시보드는 웹 Solr와 웹 브라우저를 통해 toowork 수 있는 UI입니다. hello Solr 대시보드 HDInsight 클러스터에서 hello 인터넷에 직접 노출 되지 않습니다. 에서는 SSH 터널 tooaccess 것입니다. SSH 터널이 사용에 대 한 자세한 내용은 참조 hello [사용 하 여 SSH 터널링 HDInsight와](hdinsight-linux-ambari-ssh-tunnel.md) 문서.

SSH 터널이 설정 하 고 나면 다음 단계 toouse hello Solr 대시보드 hello를 사용 합니다.

1. 기본 헤드 노드에 hello에 대 한 hello 호스트 이름을 확인 합니다.

   1. SSH tooconnect toohello 클러스터 헤드 노드를 사용 합니다. 예: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       SSH를 사용 하 여에 대 한 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

   2. 다음 명령을 tooget hello 정규화 된 호스트 이름 hello를 사용 합니다.

        ```bash
        hostname -f
        ```

        이 명령은 호스트 이름 뒤에 나오는 값 비슷한 toohello를 반환 합니다.

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        나중에 사용 중 이므로 반환 하는 hello 값을 저장 합니다.

2. 브라우저에서 연결 너무**http://HOSTNAME:8983/solr / #/**여기서 **HOSTNAME** hello 이전 단계에서 결정 하는 hello 이름입니다.

    hello 요청 클러스터에 hello SSH 터널 toohello Solr 웹 UI 통해 라우팅됩니다. hello 페이지가 다음 이미지와 비슷한 toohello 나타납니다.

    ![Solr 대시보드의 이미지](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. Hello 왼쪽된 창에서 hello를 사용 하 여 **코어 선택기** 드롭 다운 tooselect **collection1**합니다. 여러 항목이 **collection1** 아래에 나타나야 합니다.

4. Hello 항목 아래에서 **collection1**선택, **쿼리**합니다. 다음 값 toopopulate hello 검색 페이지 hello를 사용 합니다.

   * Hello에 **q** 텍스트 상자에 입력  **\*:**\*합니다. 이 쿼리 Solr에 인덱싱된 모든 hello 문서를 반환 합니다. Toosearch hello 문서 내에서 특정 문자열을 하려는 경우에 여기에 해당 문자열을 입력할 수 있습니다.
   * Hello에 **wt** 텍스트 상자, 선택 hello 출력 형식입니다. 기본값은 **json**입니다.

     마지막으로 hello 선택 **쿼리 실행** hello 검색 pate hello 맨 아래에 단추입니다.

     ![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     hello 출력 hello 두 문서 toohello를 추가한 이전 인덱스를 반환 합니다. hello 출력은 유사한 toohello 다음 JSON 문서입니다.

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Solr 시작 및 중지

다음 명령 toomanually 중지 및 시작 Solr hello를 사용 합니다.

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>인덱싱된 데이터 백업

다음 단계 tooback Solr 데이터 toohello 기본 저장소 클러스터에 대 한 hello를 사용 합니다.

1. SSH를 사용 하 여 toohello 클러스터에 연결 하 고 hello 헤드 노드에 대 한 명령 tooget hello 호스트 이름 뒤에 나오는 hello를 사용 합니다.

    ```bash
    hostname -f
    ```

2. 다음 명령 toocreate hello 인덱싱된 데이터의 스냅숏을 hello를 사용 합니다. 대체 **HOSTNAME** hello 이전 명령에서 반환 된 hello 이름의:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    hello 응답은 다음과 같은 XML 비슷한 toohello입니다.

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. 디렉터리를 너무 변경`/usr/hdp/current/solr/example/solr`합니다. 여기에 각 컬렉션에 대한 하위 디텍터리가 있습니다. 각 컬렉션 디렉터리를 포함 한 `data` hello 컬렉션에 대 한 hello 스냅숏이 포함 된 디렉터리입니다.

4. 다음 명령을 사용 하 여 hello hello 스냅숏 폴더의 압축된 된 보관 파일 toocreate:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Hello 대체 `snapshot.20150806185338855` 컬렉션 hello 스냅숏의 hello 이름을 사용 하 여 값입니다.

    이 명령은 명명 된 보관 파일이 만들어지며 **snapshot.20150806185338855.tgz**, hello의 hello 내용을 포함 하 **snapshot.20150806185338855** 디렉터리입니다.

5. 그런 다음 다음 명령을 hello를 사용 하 여 hello 보관 toohello 클러스터의 주 저장소를 저장할 수 있습니다.

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Solr 백업 및 복원 작업에 대한 자세한 내용은 [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups)를 참조하세요.

## <a name="next-steps"></a>다음 단계

* [HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md). 클러스터 사용자 지정 tooinstall Giraph에 HDInsight Hadoop 클러스터를 사용 합니다. Giraph는 tooperform 그래프 Hadoop을 사용 하 여 처리를 허용 하 고 Azure HDInsight 함께 사용할 수 있습니다.

* [HDInsight 클러스터에서 Hue를 설치](hdinsight-hadoop-hue-linux.md)합니다. HDInsight Hadoop 클러스터에서 클러스터 사용자 지정 tooinstall 색상을 사용 합니다. 색상은 Hadoop 클러스터 toointeract를 사용 하는 웹 응용 프로그램 집합입니다.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
