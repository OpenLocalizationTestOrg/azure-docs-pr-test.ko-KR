---
title: "HBase에서 Apache Phoenix & SQuirreL 사용 - Azure HDInsight | Microsoft Docs"
description: "HDInsight에서 Apache Phoenix를 사용하는 방법 및 워크스테이션에서 SQuirreL을 설치 및 구성하여 HDInsight에서 HBase 클러스터에 연결하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>HDInsight에서 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용
HDInsight에서 [Apache Phoenix](http://phoenix.apache.org/) 를 사용하는 방법 및 SQLLine을 사용하는 방법을 알아봅니다. Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요. Phoenix 문법은 [피닉스 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.

> [!NOTE]
> HDInsight의 Phoenix 버전 정보는 [HDInsight에서 제공하는 Hadoop 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)을 참조하세요.
>
>

## <a name="use-sqlline"></a>SQLLine 사용
[SQLLine](http://sqlline.sourceforge.net/)은 SQL을 실행하는 명령줄 유틸리티입니다.

### <a name="prerequisites"></a>필수 조건
SQLLine을 시작하려면 다음이 있어야 합니다.

* **HDInsight의 HBase 클러스터**. HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.
* **원격 데스크톱 프로토콜을 통해 HBase 클러스터에 연결**. 지침의 경우 [Azure Portal을 사용하여 HDInsight에서 Hadoop 클러스터 관리][hdinsight-manage-portal]를 참조하세요.

HBase 클러스터에 연결할 때 Zookeeper 중 하나에 연결해야 합니다. 각 HDInsight 클러스터에는 3개의 Zookeeper가 있습니다.

**Zookeeper 호스트 이름을 확인하려면**

1. **https://<ClusterName>.azurehdinsight.net**으로 이동하여 Ambari를 엽니다.
2. HTTP(클러스터) 사용자 이름 및 암호를 입력하여 로그인합니다.
3. 왼쪽 메뉴에서 **Zookeeper** 를 클릭합니다. 나열된 **ZooKeeper 서버** 중 하나를 클릭합니다.
4. 나열된 **ZooKeeper 서버** 중 하나를 클릭합니다. 요약 창에서 **호스트 이름**을 찾습니다. *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*과 비슷합니다.

**SQLLine을 사용하려면**

1. SSH를 사용하여 클러스터에 연결합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. SSH에서 다음 명령을 실행하여 SQLLine을 실행합니다.

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. 다음 명령을 실행하여 HBase 테이블을 만들고 일부 데이터를 삽입합니다.

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.

## <a name="next-steps"></a>다음 단계
이 문서에서는 HDInsight에서 Apache Phoenix를 사용하는 방법에 대해 알아보았습니다.  자세한 내용은 다음을 참조하세요.

* [HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.
* [Azure Virtual Network에서 HBase 클러스터 프로비전][hdinsight-hbase-provision-vnet]: Virtual Network 통합을 사용하면 응용 프로그램이 HBase와 직접 통신할 수 있도록 응용 프로그램과 동일한 Virtual Network에 HBase 클러스터를 배포할 수 있습니다.
* [HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 두 Azure 데이터 센터에서 HBase 복제를 구성하는 방법에 대해 알아봅니다.
* [HDInsight에서 HBase를 사용하여 Twitter 감정][hbase-twitter-sentiment]: HDInsight의 Hadoop 클러스터에서 HBase를 사용하여 빅 데이터에 대한 실시간 [감정 분석](http://en.wikipedia.org/wiki/Sentiment_analysis)을 수행하는 방법에 대해 알아봅니다.

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
