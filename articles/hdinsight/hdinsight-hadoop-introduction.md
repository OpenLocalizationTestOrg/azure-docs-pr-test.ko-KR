---
title: "aaaWhat은 HDInsight, hello Hadoop 기술 스택 및 클러스터? - Azure | Microsoft Docs"
description: "소개 tooHDInsight 및 hello Hadoop 기술 스택 및 구성 요소, 빅 데이터 분석을 위해 Spark, Kafka, Hive, HBase를 포함 합니다."
keywords: "azure hadoop, hadoop azure, hadoop 소개, hadoop 소개, hadoop 기술 스택, 소개 toohadoop, 소개 toohadoop, hadoop 클러스터 이란는 hadoop 클러스터 이란 hadoop 용도 대 한"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>소개 tooAzure HDInsight, hello Hadoop 기술 스택 및 Hadoop 클러스터
 이 문서는 소개 tooAzure HDInsight의 Hadoop 기술 스택 hello 클라우드 배포를 제공합니다. 또한 Hadoop 클러스터에 대한 정의와 사용 시기에 대해서도 설명합니다. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>HDInsight 및 hello Hadoop 기술 스택에서 무엇 인가요? 
Azure HDInsight는 hello에서 hello Hadoop 구성 요소는 클라우드 배포 [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/)합니다. [Apache Hadoop](http://hadoop.apache.org/) hello 원래 분산된 처리 및 컴퓨터의 클러스터에서 큰 데이터 집합의 분석을 위한 공개 소스 프레임 워크 되었습니다. 


hello Hadoop 기술 스택에서 관련된 소프트웨어 및 Apache Hive, HBase, Spark, Kafka, 및 다른 많은 요인을 포함 하 여 유틸리티를 포함 합니다. toosee 사용할 수 있는 Hadoop 기술 스택 구성 요소, HDInsight의 참조 [구성 요소 및 HDInsight를 사용할 수 있는 버전][component-versioning]합니다. HDInsight에서 Hadoop에 대 한 자세한 tooread 참조 hello [HDInsight에 대 한 Azure 기능 페이지](https://azure.microsoft.com/services/hdinsight/)합니다.

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Hadoop 클러스터의 정의 및 사용 시기
*Hadoop*은 다음을 포함한 클러스터 형식이기도 합니다.

* 작업 예약 및 리소스 관리를 위한 YARN
* 병렬 처리를 위한 MapReduce
* hello Hadoop 분산 파일 시스템 (HDFS)
  
Hadoop 클러스터는 저장된 데이터의 일괄 처리에 가장 자주 사용됩니다. 다른 종류의 HDInsight의 클러스터에는 추가 기능이 있습니다. Spark는 더 빠른 메모리 내 처리 기능이기 때문에 널리 사용되고 있습니다. 자세한 내용은 [HDInsight의 클러스터 유형](#overview)을 참조하세요.

## <a name="what-is-big-data"></a>빅 데이터란?
빅 데이터는 다음과 같은 대용량의 디지털 정보를 설명합니다.

* 산업 장비의 센서 데이터
* 웹 사이트에서 수집한 고객 활동
* Twitter 뉴스 피드

다양한 형식인 많은 양의 빅 데이터가 더 빠르게 수집되고 있습니다. 실시간으로 (hello 원본에서 스트리밍 의미) 또는 기록 (의미 저장) 수 있습니다. 

## <a name="overview"></a>HDInsight의 클러스터 유형
HDInsight에는 구성 요소, 유틸리티 및 언어 추가와 같은 특정 클러스터 형식 및 클러스터 사용자 지정 기능이 포함됩니다.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Spark, Kafka, Interactive Hive, HBase, 사용자 지정 및 기타 클러스터 유형
HDInsight은 클러스터 유형만 hello를 제공 합니다.

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: 사용 하 여 [HDFS](#hdfs), [YARN](#yarn) 리소스 관리 및 간단한 [MapReduce](#mapreduce) 모델 tooprocess 프로그래밍 및 동시에 일괄 처리 데이터를 분석 합니다.
* **[Apache Spark](http://spark.apache.org/)**: 빅 데이터 분석 응용 프로그램의 메모리 내 처리 tooboost hello 성능이 지원 되는 병렬 처리 프레임 워크 데이터 스트리밍, SQL에 대 한 작동 멤버 및 기계 학습 합니다. [HDInsight의 Apache Spark란?](hdinsight-apache-spark-overview.md)을 참조하세요.
* **[Apache HBase](http://hbase.apache.org/)**: 구조화되지 않은/반구조화된 대량 데이터(잠재적으로 수십억 개의 행과 수십억 개의 열로 구성됨)에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 NoSQL 데이터베이스입니다. [HDInsight의 HBase란?](hdinsight-hbase-overview.md)을 참조하세요.
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: 병렬 분산된 R 프로세스를 호스팅하고 관리하기 위한 서버입니다. 데이터 과학자, 통계학자, 및 R 프로그래머 요청 시 액세스 tooscalable, HDInsight의 분석의 분산된 메서드를 제공합니다. [HDInsight의 서버 개요](hdinsight-hadoop-r-server-overview.md)를 참조하세요.
* **[Apache Storm](https://storm.incubator.apache.org/)**: 대규모 데이터 스트림을 빠르게 처리하기 위한 분산형 실시간 계산 시스템으로입니다. HDInsight에서 관리 클러스터로 제공됩니다. [Storm 및 Hadoop을 사용하여 실시간 센서 데이터 분석](hdinsight-storm-sensor-data-analysis.md)을 참조하세요.
* **[Apache Interactive Hive 미리 보기 (AKA: Live Long 및 Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: 대화형이며 더 빠른 하이브 쿼리에 대한 메모리 내 캐싱입니다. [HDInsight에서 대화형 Hive 사용](hdinsight-hadoop-use-interactive-hive.md)을 참조하세요.
* **[Apache Kafka](https://kafka.apache.org/)**: 스트리밍 데이터 파이프라인 및 응용 프로그램을 빌드하는 데 사용되는 오픈 소스 플랫폼입니다. 또한 Kafka toopublish 있으며 toodata 스트림을 구독 하는 메시지 큐 기능을 제공 합니다. 참조 [소개 tooApache HDInsight의 Kafka](hdinsight-apache-kafka-introduction.md)합니다.

메서드를 다음 hello를 사용 하 여 클러스터를 구성할 수 있습니다.
* **[도메인에 가입 된 클러스터 미리 보기](hdinsight-domain-joined-introduction.md)**: 클러스터 액세스를 제어 하 고 데이터에 대 한 거 버 넌 스를 제공할 수 있도록 tooan Active Directory 도메인에 가입 합니다.
* **[스크립트 동작을 사용하는 사용자 지정 클러스터](hdinsight-hadoop-customize-cluster-linux.md)**: 프로비전되는 동안에 실행되고 추가 구성 요소를 설치하는 스크립트가 있는 클러스터입니다.

### <a name="example-cluster-customization-scripts"></a>예제 클러스터 사용자 지정 스크립트
스크립트 동작 하는 linux 클러스터 프로 비전 하는 동안를 실행 하 고 hello 클러스터에서 사용 되는 tooinstall 추가 구성 요소를 일 수 있는 Bash 스크립트. 

hello 다음 예제에서는 제공 되는 스크립트 hello HDInsight 팀에서:

* **[색상](hdinsight-hadoop-hue-linux.md)**: 웹 응용 프로그램 사용 toointeract 클러스터의 집합입니다. Linux 클러스터에만 해당합니다.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: 작업 또는 사람 간의 toomodel 관계를 처리 하는 그래프입니다.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: 데이터에 대해 전체 텍스트를 검색할 수 있는 엔터프라이즈급 검색 플랫폼입니다.

사용자 고유의 스크립트 작업 개발에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.

## <a name="components-and-utilities-on-hdinsight-clusters"></a>HDInsight 클러스터의 구성 요소 및 유틸리티
hello 다음 구성 요소와 유틸리티에 포함 된 HDInsight 클러스터:

* **[Ambari](#ambari)**: 클러스터 프로비전, 관리, 모니터링 및 유틸리티.
* **[Avro](#avro)**  (Avro 용 Microsoft.NET 라이브러리): hello Microsoft.NET 환경에 대 한 데이터를 직렬화 합니다. 
* **[Hive 및 HCatalog](#hive)**: SQL과 같은 쿼리, 테이블 및 저장소 관리 계층입니다.
* **[Mahout](#mahout)**: 응용 프로그램을 학습하는 확장 가능한 컴퓨터의 경우.
* **[MapReduce](#mapreduce)**- Hadoop 분산 처리 및 리소스 관리를 위한 레거시 프레임워크. [YARN](#yarn)을 참조하세요.
* **[Oozie](#oozie)**- 워크플로 관리.
* **[Phoenix](#phoenix)**: HBase를 통한 관계형 데이터베이스 계층.
* **[Pig](#pig)**- MapReduce 변환을 위한 간단한 스크립팅.
* **[Sqoop](#sqoop)**-데이터 가져오기 및 내보내기.
* **[Tez](#tez)**: 규모로 데이터를 많이 사용 프로세스 toorun를 효율적으로 허용 합니다.
* **[YARN](#yarn)**: hello Hadoop 핵심 라이브러리의 일부인 리소스 관리.
* **[ZooKeeper](#zookeeper)**- 분산 시스템의 프로세스 조정.

> [!NOTE]
> Hello 특정 구성 요소에 대 한 정보 및 버전 정보에 대 한 참조 [Hadoop 구성 요소 및 HDInsight의 버전][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari는 Apache Hadoop 클러스터를 프로비전, 관리 및 모니터링합니다. 직관적인 도구 컬렉션으로 연산자와 강력한 클러스터 hello 작업 단순화 Hadoop의 hello 복잡성을 숨기는 Api 집합이 포함 됩니다. Linux에서 HDInsight 클러스터 Ambari web UI hello와 hello Ambari REST API를 모두 제공 합니다. HDInsight 클러스터의 Ambari 뷰는 플러그 인 UI 기능을 허용합니다.
[Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md) 및 <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Apache Ambari API 참조</a>를 참조하세요.

### <a name="avro"></a>Avro (Microsoft .NET Library for Avro)
hello Avro 용 Microsoft.NET 라이브러리는 hello Microsoft.NET 환경에 대 한 serialization에 대 한 hello Apache Avro compact 이진 데이터 교환 형식을 구현합니다. 한 언어로 직렬화된 데이터를 다른 언어로 읽을 수 있도록 언어 중립적 스키마를 정의합니다. Hello에서 hello 형식에 대 한 자세한 정보를 찾을 수 있습니다 < 대상 _ "빈" href = "http://avro.apache.org/docs/current/spec.html" = > Apache Avro 사양</a>합니다. Avro 파일 지원 hello hello 형식의 distributed MapReduce 프로그래밍 모델: 파일은 "분할 가능한" 의미 모든 지점에서 파일을 검색 하 고 특정 블록에서 읽기를 시작할 수 있습니다. 참조 하는 방법, toofind [Avro에 대 한 hello Microsoft.NET 라이브러리를 사용 하 여 데이터를 Serialize](hdinsight-dotnet-avro-serialization.md)합니다. Linux 기반 클러스터 지원 toocome 합니다.

### <a name="hdfs"></a>HDFS
Hadoop 분산 파일 시스템 (HDFS)는 YARN 및 MapReduce는 Hadoop 기술의 hello 코어 하는 파일 시스템입니다. HDInsight의 Hadoop 클러스터에 대 한 hello 표준 파일 시스템의 것입니다. [HDFS 호환 저장소에서 데이터 쿼리](hdinsight-hadoop-use-blob-storage.md)를 참조하세요.

### <a name="hive"></a>Hive & HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> 는 데이터 웨어하우스 tooquery 수 있는 Hadoop에서 구축 된 소프트웨어 및 HiveQL를 호출 하는 SQL 유사 언어를 사용 하 여 분산된 된 저장소에서 대규모 데이터 집합을 관리 합니다. Pig와 마찬가지로 Hive는 MapReduce에 기반하여 추상화되어 있으며 쿼리를 일련의 MapReduce 작업으로 변환합니다. 하이브는 Pig 보다 자세히 tooa 관계형 데이터베이스 관리 시스템 이며 더 구조화 된 데이터와 함께 사용 됩니다. 구조화 되지 않은 데이터에 대 한 Pig hello 것이 좋습니다. [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)을 참조하세요.

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a>는 사용자에게 데이터의 관계형 뷰를 표시하는 Hadoop의 테이블 및 저장소 관리 계층입니다. HCatalog에서, Hive SerDe(serializer-deserializer)에서 사용 가능한 모든 형식으로 파일을 읽고 쓸 수 있습니다.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a>는 Hadoop에서 실행되는 기계 학습 알고리즘의 라이브러리입니다. 통계의 원칙을 사용 하 여, 시스템 학습 응용 프로그램에서 데이터 및 결과 toodetermine 앞으로 동작을 지 나 toouse 시스템 toolearn를 설명 합니다. [Hadoop에서 Mahout를 사용하여 영화 추천 생성](hdinsight-mahout.md)을 참조하세요.

### <a name="mapreduce"></a>MapReduce
MapReduce 동시에 응용 프로그램 toobatch 프로세스 큰 데이터 집합을 작성 하기 위해 Hadoop에 대 한 hello 레거시 소프트웨어 프레임 워크 사용 되며 큰 데이터 집합을 분할 하 고 hello 데이터 처리에 대 한 키-값 쌍으로 구성 하는 MapReduce 작업 합니다. MapReduce 작업은 [YARN](#yarn)에서 실행됩니다. 참조 <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> hello Hadoop Wiki에서에서.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a>는 Hadoop 작업을 관리하는 워크플로 코디네이션 시스템입니다. Hadoop 스택 hello와 통합 하 고 MapReduce, Pig, Hive, 및 Sqoop에 대 한 Hadoop 작업을 지원 합니다. Java 프로그램 또는 셸 스크립트와 같은 사용된 tooschedule 작업 특정 tooa 시스템 수도 있습니다. [Hadoop과 함께 Oozie 사용](hdinsight-use-oozie-linux-mac.md)을 참조하세요.

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a>는 HBase를 기반으로 둔 관계형 데이터베이스 계층입니다. 피닉스는 tooquery 있으며 SQL 테이블을 직접 관리 하는 JDBC 드라이버를 포함 합니다. Phoenix는 MapReduce를 사용하지 않고 쿼리 및 다른 문을 네이티브 NoSQL API로 변환하므로 NoSQL 저장소 위에서 더 빠른 응용 프로그램을 사용할 수 있습니다. [HBase 클러스터와 함께 Apache Phoenix 및 SQuirreL 사용](hdinsight-hbase-phoenix-squirrel.md)을 참조하세요.

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> 수 있는 복잡 한 MapReduce 변환을 tooperform 큰 데이터 집합에서 Pig 라틴 라는 간단한 스크립팅 언어를 사용 하 여 높은 수준의 플랫폼입니다. Hadoop에서 실행할 수 있도록 pig hello 라틴 Pig 스크립트를 변환 합니다. 사용자 정의 함수 (Udf) tooextend Pig 라틴 문자를 만들 수 있습니다. [Hadoop과 함께 Pig 사용](hdinsight-use-pig.md)을 참조하세요.

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a>은 Hadoop과 관계형 데이터베이스(예: SQL) 또는 다른 구조적 데이터 저장소 간에 대량 데이터를 최대한 효율적으로 전송하는 도구입니다. [Hadoop과 함께 Sqoop 사용](hdinsight-use-sqoop.md)을 참조하세요.

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a>는 복잡하고 방향이 있는 일반 데이터 처리 그래프를 실행하는 Hadoop YARN에서 빌드된 응용 프로그램 프레임워크입니다. 이 보다 유연 하 고 강력한 후속 toohello MapReduce 하이브를 규모에 보다 효율적으로 toorun 같은 데이터를 많이 사용 프로세스를 허용 하 합니다. [Hive와 HiveQL에서"향상된 성능을 위해 Apache Tez 사용"](hdinsight-use-hive.md#usetez)을 참조하세요.

### <a name="yarn"></a>YARN
Apache YARN hello 차세대 MapReduce (MapReduce 2.0 또는 MRv2) 이며 MapReduce 일괄 실시간 처리와 확장성을 높이기 처리 초과 하는 데이터 처리 시나리오를 지원 합니다. YARN은 리소스 관리 및 분산된 응용 프로그램 프레임워크를 제공합니다. MapReduce 작업은 YARN에서 실행됩니다. <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce(YARN)</a>(영문)를 참조하세요.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a>는 데이터 레지스터(znode)의 공유 계층 구조 네임스페이스를 사용하여 대규모 분산 시스템의 프로세스를 조정합니다. Znodes 포함 적은 양의 메타 정보 필요한 toocoordinate 프로세스: 상태, 위치, 구성 및 등입니다. [HBase 클러스터 및 Apache Phoenix가 있는 ZooKeeper](hdinsight-hbase-phoenix-squirrel-linux.md)의 예제를 참조하세요. 

## <a name="programming-languages-on-hdinsight"></a>HDInsight의 프로그래밍 언어
HDInsight 클러스터, 즉 Spark, HBase, Kafka, Hadoop 및 기타 클러스터는 다양한 프로그래밍 언어를 지원하지만, 일부는 기본적으로 설치되지 않습니다. 라이브러리, 모듈 또는 기본적으로 설치 되어 있지는 패키지에 대 한 [스크립트 동작 tooinstall hello 구성 요소를 사용 하 여](hdinsight-hadoop-script-actions-linux.md)합니다. 

### <a name="default-programming-language-support"></a>기본 프로그래밍 언어 지원
기본적으로 HDInsight 클러스터는 다음을 지원합니다.

* 자바
* Python

추가 언어는 [스크립트 동작](hdinsight-hadoop-script-actions-linux.md)을 사용하여 설치할 수 있습니다.

### <a name="java-virtual-machine-jvm-languages"></a>Java 가상 컴퓨터(JVM) 언어
Java 이외의 여러 언어 JVM ();는 Java 가상 컴퓨터에서 실행할 수 있습니다. 그러나 이러한 언어 중 일부를 실행 중인 hello 클러스터에 설치 하는 추가 구성 요소가 필요할 수 있습니다.

이러한 JVM 기반 언어는 HDInsight 클러스터에서 지원됩니다.

* Clojure
* Jython(Java용 Python)
* 스칼라

### <a name="hadoop-specific-languages"></a>Hadoop 관련 언어
HDInsight 클러스터에 있는 특정 toohello Hadoop 기술 스택에서 언어를 다음 hello를 지원 합니다.

* Pig 작업에 대한 Pig Latin
* Hive 작업에 대한 HiveQL 및 SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard 및 HDInsight Premium
HDInsight는 빅 데이터 클라우드 제품을 표준 및 프리미엄이라는 두 범주로 제공합니다. HDInsight 표준은 제공 하는 엔터프라이즈 규모 클러스터 조직에서는 사용할 수 있는 toorun의 빅 데이터 작업량입니다. HDInsight 프리미엄은 표준 기능을 기반으로 하며, HDInsight 클러스터에 대한 고급 분석 및 보안 기능을 제공합니다. 자세한 내용은 [Azure HDInsight 프리미엄](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft 비즈니스 인텔리전스 및 HDInsight
익숙한 비즈니스 인텔리전스 (BI) 도구 검색, 분석 및 보고 어느 hello 파워 쿼리 추가 기능을 사용 하 여 HDInsight와 통합 되는 데이터 또는 Microsoft ODBC Driver 하이브 hello:

* [파워 쿼리를 사용 하 여 Excel tooHadoop 연결](hdinsight-connect-excel-power-query.md): tooconnect Excel toohello Azure 저장소 계정을 저장 하는 Excel 용 Microsoft Power Query를 사용 하 여 HDInsight 클러스터에서 데이터를 hello 하는 방법을 알아봅니다. Windows 워크스테이션이 필요합니다. 
* [Microsoft ODBC Driver 하이브 hello를 사용 하 여 Excel tooHadoop 연결](hdinsight-connect-excel-hive-odbc-driver.md): tooimport 데이터를 포함 하는 HDInsight Hive Microsoft ODBC Driver hello 하는 방법에 대해 알아봅니다. Windows 워크스테이션이 필요합니다. 
* [Microsoft 클라우드 플랫폼](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Office 365 용 Power BI에 대 한 자세한 내용은 hello SQL Server 평가판을 다운로드 하 여 SharePoint Server 2013 및 SQL Server BI 설정 합니다.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>다음 단계

* [HDInsight에서 Hadoop 시작](hdinsight-hadoop-linux-tutorial-get-started.md): HDInsight Hadoop 클러스터를 프로비전하고 샘플 Hive 쿼리를 실행하는 방법에 대한 빠른 시작 자습서입니다.
* [HDInsight에서 Spark 시작](hdinsight-apache-spark-jupyter-spark-sql.md): Spark 클러스터를 만들고 대화형 Spark SQL 쿼리를 실행하는 방법에 대한 빠른 시작 자습서입니다.
* [HDInsight에서 R Server 사용](hdinsight-hadoop-r-server-get-started.md): HDInsight Premium에서 R Server를 사용하기 시작합니다.
* [HDInsight 클러스터를 프로 비전](hdinsight-hadoop-provision-linux-clusters.md): Azure 포털, Azure CLI 또는 Azure PowerShell HDInsight Hadoop 클러스터를 통해 tooprovision hello 하는 방법에 대해 알아봅니다.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/