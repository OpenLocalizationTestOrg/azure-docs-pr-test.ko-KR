---
title: "aaaWhat은 Azure HDInsight에서 HBase 인가요? | Microsoft Docs"
description: "소개 tooApache HDInsight에서 HBase, NoSQL 데이터베이스 Hadoop에 구축 합니다. 사용 사례에 대해 알아보고 HBase tooother Hadoop 클러스터를 비교 합니다."
keywords: "BigTable, NoSQL, HBase란?, Apache HBase, HBase, HBase 개요"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>HDInsight의 HBase: Hadoop에 BigTable 같은 기능을 제공하는 NoSQL 데이터베이스
Apache HBase는 Hadoop을 기반으로 하고 Google BigTable 이후에 모델링된 오픈 소스 NoSQL 데이터베이스입니다. HBase는 열 패밀리로 구성된 스키마 없는 데이터베이스에서 구조화되지 않은/반구조화된 대량 데이터에 대해 임의 액세스 및 강력한 일관성을 제공합니다.

데이터는 테이블의 hello 행에 저장 하 고 데이터 행 내의 열 패밀리로 그룹화 됩니다. HBase는 hello 의미 열에 저장 된 데이터의 hello 형식에도 hello 둘 다에서 schemaless 데이터베이스 정의 사용 하기 전에 toobe 할입니다. hello 오픈 소스 코드 거의 선형적 toohandle 페타바이트 규모의 데이터 수천 대의 노드. 데이터 중복성, 처리, 일괄 처리 및 hello Hadoop 에코 시스템에서 배포 응용 프로그램에서 제공 되는 기타 기능에 의존할 수 있습니다.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Azure HDInsight에서 HBase를 구현하는 방법
HDInsight HBase hello Azure 환경에 통합 되는 관리 클러스터로 제공 됩니다. hello 클러스터에서 직접 구성된 toostore 데이터는 [Azure 저장소](./hdinsight-hadoop-use-blob-storage.md) 또는 [Azure 데이터 레이크 저장소](./hdinsight-hadoop-use-data-lake-store.md), 짧은 대기 시간 및 성능 및 비용 선택 옵션의 향상 된 유연성을 제공 합니다. 따라서 고객 toobuild 대화형 웹 사이트를 Hadoop 작업을 사용 하 여이 데이터를 큰 데이터 집합의 끝 점과 tooanalyze 수백만의 센서 및 원격 분석 데이터를 저장 하는 toobuild 서비스 작업할 수 있습니다. HBase 및 Hadoop 좋은지; Azure의 빅 데이터 프로젝트에 대 한 시작점 특히 큰 데이터 집합으로 toowork 실시간 응용 프로그램을 활성화할 수 있습니다.

HBase tooprovide 자동 분할 테이블의 읽기 및 쓰기 및 자동 장애 조치에 대해 강력한 일관성의 hello 스케일 아웃 아키텍처를 활용 하는 hello HDInsight 구현 합니다. 읽기를 위한 메모리 내 캐싱과 쓰기를 위한 높은 처리량 스트리밍을 통해 성능이 향상됩니다. HBase 클러스터는 가상 네트워크 내에 만들 수 있습니다. 자세한 내용은 [Azure Virtual Network에 HDInsight 클러스터 만들기][hbase-provision-vnet]를 참조하세요.

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>HDInsight HBase에서 데이터를 관리하는 방법
Hello를 사용 하 여 HBase에서 데이터를 관리할 수 있습니다 `create`, `get`, `put`, 및 `scan` hello HBase 셸에서에서 명령입니다. 데이터를 사용 하 여 toohello 데이터베이스 쓰여집니다 `put` 를 사용 하 여 읽고 `get`합니다. hello `scan` 명령 테이블의 여러 행에서 사용 되는 tooobtain 데이터입니다. 데이터는 hello hello HBase REST API를 기반으로 클라이언트 라이브러리를 제공 하는 HBase C# API를 사용 하 여 관리할 수 있습니다. 또한 Hive를 사용하여 HBase 데이터베이스를 쿼리할 수 있습니다. 프로그래밍 모델 소개 toothese는을 참조 하십시오. [HDInsight에서 Hadoop으로 HBase를 사용 하 여 시작][hbase-get-started]합니다. 공동 프로세서는 또한를 사용할 수 있도록 허용 하기 위해 데이터 처리 hello 노드에 해당 호스트 hello 데이터베이스입니다.

> [!NOTE]
> Thrift는 HDInsight의 HBase에서 지원되지 않습니다.
>

## <a name="scenarios-use-cases-for-hbase"></a>시나리오: HBase의 사용 사례
hello 정식 사용 사례를 포함 하는 BigTable (및 확장 하면 HBase) 만들어진 웹 검색 되었습니다. 검색 엔진을 포함 하는 용어 toohello 웹 페이지를 매핑하는 인덱스를 작성 합니다. 그러나 HBase가 적합한 다른 많은 사용 사례가 있으며, 몇 가지 사례가 이 섹션에 나와 있습니다.

* 키-값 저장소
  
    HBase를 키-값 저장소로 사용할 수 있으며 메시지 시스템 관리에 적합합니다. Facebook은 해당 메시징 시스템에 HBase를 사용하며 인터넷 통신 저장 및 관리에 유용합니다. WebTable에 대 한 toosearch HBase를 사용 하 고 웹 페이지에서 추출 된 테이블을 관리 합니다.
* 센서 데이터
  
    HBase는 다양한 소스에서 증분 방식으로 수집된 데이터를 캡처하는 데 유용합니다. 여기에는 소셜 분석, 시계열, 추세 및 카운터로 대화형 대시보드를 최신 상태로 유지, 감사 로그 시스템 관리가 포함됩니다. 예로 터미널 Bloomberg 거래 업체 및 hello 열린 시간 시계열 데이터베이스 (OpenTSDB) 저장 하 고 액세스 toometrics 제공 하는 서버 시스템의 hello 상태에 대 한 수집 합니다.
* 실시간 쿼리
  
    [Phoenix](http://phoenix.apache.org/) 는 Apache HBase용 SQL 쿼리 엔진입니다. JDBC 드라이버로 액세스되며 SQL을 사용하여 HBase 테이블을 쿼리하고 관리할 수 있도록 합니다.
* HBase를 플랫폼으로 사용
  
    HBase를 데이터 저장소로 사용하여 HBase 위에서 응용 프로그램을 실행할 수 있습니다. 예를 들어 Phoenix, OpenTSDB, Kiji, Titan 등이 있습니다. 응용 프로그램이 HBase와 통합될 수도 있습니다. 예를 들어 Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia, Drill 등이 있습니다.

## <a name="next-steps"></a>다음 단계
* [HDInsight의 Hadoop에서 HBase 사용 시작][hbase-get-started]
* [Azure Virtual Network에 HDInsight 클러스터 만들기][hbase-provision-vnet]
* [HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md)
* [HDInsight에서 HBase를 사용하여 Twitter 데이터 분석][hbase-twitter-sentiment]
* [(Hadoop) HDInsight HBase를 사용 하는 Maven toobuild Java 응용 프로그램을 사용 하 여][hbase-build-java-maven]

## <a name="see-also"></a>참고 항목
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable: 구조화된 데이터의 분산 저장소 시스템](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
