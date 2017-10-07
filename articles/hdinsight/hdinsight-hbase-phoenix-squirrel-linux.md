---
title: "aaaUse Apache 피닉스 & HBase-Azure HDInsight를 스 쿼 럴 | Microsoft Docs"
description: "자세한 방법을 toouse, HDInsight의 Apache 피닉스 방법과 tooinstall 스 쿼 럴 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>HDInsight에서 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용
자세한 방법을 toouse [Apache 피닉스](http://phoenix.apache.org/) , HDInsight의 방법과 toouse SQLLine 합니다. Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요. Hello 피닉스 문법에 대 한 참조 [피닉스 문법](http://phoenix.apache.org/language/index.html)합니다.

> [!NOTE]
> HDInsight의 버전 정보 피닉스 hello에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md)합니다.
>
>

## <a name="use-sqlline"></a>SQLLine 사용
[SQLLine](http://sqlline.sourceforge.net/) 명령줄 유틸리티 tooexecute SQL 됩니다.

### <a name="prerequisites"></a>필수 조건
SQLLine를 사용 하려면 먼저 hello 다음이 있어야 합니다.

* **HDInsight의 HBase 클러스터**. HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.
* **Hello 원격 데스크톱 프로토콜을 통해 toohello HBase 클러스터를 연결**합니다. 자세한 내용은 [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello][hdinsight-manage-portal]합니다.

Tooan HBase 클러스터를 연결 하면 hello 사육의 tooconnect tooone가 필요 합니다. 각 HDInsight 클러스터에는 3개의 Zookeeper가 있습니다.

**toofind hello 사육 호스트 이름**

1. Ambari 너무 이동 하 여 열고**https://<ClusterName>. azurehdinsight.net**합니다.
2. Hello HTTP (클러스터) toologin 사용자 이름 및 암호를 입력 합니다.
3. 클릭 **사육** hello 왼쪽된 메뉴에서 합니다. 나열된 **ZooKeeper 서버** 중 하나를 클릭합니다.
4. Hello 중 하나를 클릭 **사육 서버** 나열 합니다. Hello 요약 창에서 찾을 hello **Hostname**합니다. 비슷합니다 너무*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*합니다.

**toouse SQLLine**

1. SSH를 사용 하 여 toohello 클러스터를 연결 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. SSH에서 다음 명령을 toorun SQLLine hello를 실행 합니다.

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. 명령을 toocreate 다음 hello HBase 테이블을 실행 하 고 일부 데이터를 삽입 합니다.

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.

## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 어떻게 toouse HDInsight의 Apache 피닉스 합니다.  toolearn 더 참조 하십시오.

* [HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.
* [Azure 가상 네트워크에서 HBase 클러스터를 프로 비전][hdinsight-hbase-provision-vnet]: 가상 네트워크 통합 HBase 클러스터 동일한 가상 네트워크로 응용 프로그램 이므로 배포 된 toohello 수 있는 응용 프로그램이 통신할 수 HBase에 직접 해당 합니다.
* [HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 자세한 방법 두 Azure 데이터 센터에서 tooconfigure HBase 복제 합니다.
* [HDInsight에서 HBase와 Twitter 감성 분석][hbase-twitter-sentiment]: 자세한 방법을 toodo 실시간 [감성 분석](http://en.wikipedia.org/wiki/Sentiment_analysis) HDInsight의 Hadoop 클러스터의 HBase를 사용 하 여 빅 데이터의 합니다.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
