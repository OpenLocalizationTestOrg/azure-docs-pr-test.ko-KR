---
title: "Azure HDInsight의 Hadoop 서비스에서 사용 하는 aaaPorts | Microsoft Docs"
description: "HDInsight에서 실행 중인 Hadoop 서비스에 사용된 포트 목록입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>HDInsight의 Hadoop 서비스에서 사용하는 포트

이 문서는 Linux 기반 HDInsight 클러스터에서 실행 되는 Hadoop 서비스에서 사용 하는 hello 포트의 목록을 제공 합니다. 또한 SSH를 사용 하 여 tooconnect toohello 클러스터를 사용 하는 포트에 대 한 정보를 제공 합니다.

## <a name="public-ports-vs-non-public-ports"></a>공용 포트 및 비-공용 포트

Linux 기반 HDInsight 클러스터만 포트 세 개 공개적으로 노출에 hello 인터넷; 22, 23, 및 443입니다. 이러한 포트는 SSH 및 hello 보안 HTTPS 프로토콜을 통해 노출 되는 서비스를 사용 하 여 사용 되는 toosecurely 액세스 hello 클러스터입니다.

HDInsight는 여러 Azure 가상 컴퓨터에서 (hello 클러스터 내에서 hello 노드)를 구현 하는 내부적으로 Azure 가상 네트워크에서 실행 합니다. hello 가상 네트워크 내에서 액세스할 수 있습니다 hello를 통해 노출 되지 포트 인터넷 합니다. 예를 들어 tooone SSH를 사용 하 여 hello 헤드 노드를 연결 하는 경우 hello 헤드 노드에서 다음 직접 액세스할 수 있습니다 hello 클러스터 노드에서 실행 되는 서비스입니다.

> [!IMPORTANT]
> HDInsight의 구성 옵션으로 Azure Virtual Network를 지정하지 않을 경우 하나는 자동으로 생성됩니다. 그러나 다른 컴퓨터 (예: 다른 Azure 가상 컴퓨터 또는 클라이언트 개발 컴퓨터) toothis 가상 네트워크를 조인할 수 없습니다.


toojoin 추가 컴퓨터 toohello 가상 네트워크를 먼저 hello 가상 네트워크를 만든 하며 다음 HDInsight 클러스터를 만들 때 지정 합니다. 자세한 내용은 [Azure 가상 네트워크를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>공용 포트

HDInsight 클러스터의 노드는 Azure 가상 네트워크에 있고에서 직접 액세스할 수 없는 모든 hello hello 인터넷 합니다. 공용 게이트웨이 인터넷 액세스 toohello 다음 모든 HDInsight 클러스터 형식 간에 공통적으로 적용 되는 포트를 제공 합니다.

| 부여 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |클라이언트 toosshd hello 기본 헤드 노드에 연결합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요. |
| sshd |22 |SSH |클라이언트 toosshd hello 가장자리 노드에 연결합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요. |
| sshd |23 |SSH |클라이언트 toosshd hello 보조 헤드 노드에 연결합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요. |
| Ambari |443 |HTTPS |Ambari 웹 UI. 참조 [Ambari 웹 UI hello 관리할 HDInsight를 사용 하 여](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |Ambari REST API. 참조 [Ambari REST API를 hello 관리할 HDInsight를 사용 하 여](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |HCatalog REST API. [Curl에서 Hive 사용](hdinsight-hadoop-use-pig-curl.md), [Curl에서 Pig 사용](hdinsight-hadoop-use-pig-curl.md), [Curl에서 MapReduce 사용](hdinsight-hadoop-use-mapreduce-curl.md)을 참조하세요. |
| HiveServer2 |443 |ODBC |TooHive ODBC를 사용 하 여 연결 합니다. 참조 [hello Microsoft ODBC 드라이버와 함께 Excel 연결 tooHDInsight](hdinsight-connect-excel-hive-odbc-driver.md)합니다. |
| HiveServer2 |443 |JDBC |TooHive JDBC를 사용 하 여 연결 합니다. 참조 [tooHive hello 하이브 JDBC 드라이버를 사용 하 여 HDInsight의 연결](hdinsight-connect-hive-jdbc-driver.md) |

hello 다음은 특정 클러스터 유형에 사용할 수 있는입니다.

| 부여 | 포트 | 프로토콜 | 클러스터 유형 | 설명 |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |HBase REST API. [HBase를 사용하여 시작](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |Spark REST API. [Livy를 사용하여 원격으로 Spark 작업 제출](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Storm 웹 UI. [HDInsight에서 Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>인증

인터넷 인증 되어야 하는 hello에 공개적으로 노출 되는 모든 서비스:

| 포트 | 자격 증명 |
| --- | --- |
| 22 또는 23 |hello SSH 사용자 자격 증명 클러스터 생성 중에 지정 |
| 443 |hello 로그인 이름 (기본값: 관리자) 및 클러스터를 만드는 동안 설정 된 암호 |

## <a name="non-public-ports"></a>비-공용 포트

> [!NOTE]
> 일부 서비스는 특정 클러스터 형식에서만 사용할 수 있습니다. 예를 들어 HBase는 HBase 클러스터 형식에서만 사용할 수 있습니다.

> [!IMPORTANT]
> 일부 서비스는 한 번에 하나의 헤드 노드에서만 실행됩니다. 기본 헤드 노드에 hello에 tooconnect toohello 서비스 시도 404 오류를 수신 하는 경우 보조 헤드 노드에 hello를 사용 하 여 다시 시도 하십시오.

### <a name="ambari"></a>Ambari

| 부여 | 노드 | 포트 | URL 경로 | 프로토콜 | 
| --- | --- | --- | --- | --- |
| Ambari 웹 UI | 헤드 노드 | 8080 | / | http |
| Ambari REST API | 헤드 노드 | 8080 | /api/v1 | HTTP |

예제:

* Ambari REST API: `curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>HDFS 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| NameNode 웹 UI |헤드 노드 |30070 |HTTPS |웹 UI tooview 상태 |
| NameNode 메타데이터 서비스 |헤드 노드 |8020 |IPC |파일 시스템 메타데이터 |
| DataNode |모든 작업자 노드 |30075 |HTTPS |웹 UI tooview 상태, 로그, 등입니다. |
| DataNode |모든 작업자 노드 |30010 |&nbsp; |데이터 전송 |
| DataNode |모든 작업자 노드 |30020 |IPC |메타데이터 작업 |
| 보조 NameNode |헤드 노드 |50090 |HTTP |NameNode 메타데이터에 대한 검사점 |

### <a name="yarn-ports"></a>YARN 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| Resource Manager 웹 UI |헤드 노드 |8088 |HTTP |Resource Manager용 웹 UI |
| Resource Manager 웹 UI |헤드 노드 |8090 |HTTPS |Resource Manager용 웹 UI |
| Resource Manager 관리 인터페이스 |헤드 노드 |8141 |IPC |응용 프로그램 제출용(Hive, Hive server, Pig 등) |
| Resource Manager 스케줄러 |헤드 노드 |8030 |HTTP |관리 인터페이스 |
| Resource Manager 응용 프로그램 인터페이스 |헤드 노드 |8050 |HTTP |Hello 응용 프로그램 관리자 인터페이스의 주소 |
| NodeManager |모든 작업자 노드 |30050 |&nbsp; |hello 컨테이너 관리자의 hello 주소 |
| NodeManager 웹 UI |모든 작업자 노드 |30060 |HTTP |Resource Manager 인터페이스 |
| 타임라인 주소 |헤드 노드 |10200 |RPC |시간 표시 막대 서비스 RPC 서비스 번호입니다. |
| 타임라인 웹 UI |헤드 노드 |8181 |HTTP |hello 타임 라인 서비스 웹 UI |

### <a name="hive-ports"></a>Hive 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| HiveServer2 |헤드 노드 |10001 |Thrift |TooHive Thrift/JDBC ()를 연결 하기 위한 서비스 |
| Hive Metastore |헤드 노드 |9083 |Thrift |연결 tooHive 메타 데이터 (Thrift/JDBC)에 대 한 서비스 |

### <a name="webhcat-ports"></a>WebHCat 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| WebHCat 서버 |헤드 노드 |30111 |HTTP |HCatalog 및 기타 Hadoop 서비스 맨 위의 웹 API |

### <a name="mapreduce-ports"></a>MapReduce 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| JobHistory |헤드 노드 |19888 |HTTP |MapReduce JobHistory 웹 UI |
| JobHistory |헤드 노드 |10020 |&nbsp; |MapReduce JobHistory 서버 |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |전송을 중간 지도 toorequesting 이경소켓을 출력합니다. |

### <a name="oozie"></a>Oozie

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| Oozie 서버 |헤드 노드 |11000 |HTTP |Oozie 서비스에 대한 URL |
| Oozie 서버 |헤드 노드 |11001 |HTTP |Oozie 관리자에 대한 포트 |

### <a name="ambari-metrics"></a>Ambari 메트릭

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| 타임라인(응용 프로그램 기록) |헤드 노드 |6188 |HTTP |hello 타임 라인 서비스 웹 UI |
| 타임라인(응용 프로그램 기록) |헤드 노드 |30200 |RPC |hello 타임 라인 서비스 웹 UI |

### <a name="hbase-ports"></a>HBase 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| HMaster |헤드 노드 |16000 |&nbsp; |&nbsp; |
| HMaster 정보 웹 UI |헤드 노드 |16010 |HTTP |hello HBase 마스터 웹 UI에 대 한 hello 포트 |
| Region 서버 |모든 작업자 노드 |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |클라이언트 tooconnect tooZooKeeper 사용 하 여 hello 포트 |

### <a name="kafka-ports"></a>Kafka 포트

| 부여 | 노드 | 포트 | 프로토콜 | 설명 |
| --- | --- | --- | --- | --- |
| Broker |작업자 노드 |9092 |[Kafka 유선 프로토콜](http://kafka.apache.org/protocol.html) |클라이언트 통신에 사용됨 |
| &nbsp; |Zookeeper 노드 |2181 |&nbsp; |클라이언트 tooconnect tooZookeeper 사용 하 여 hello 포트 |

### <a name="spark-ports"></a>Spark 포트

| 부여 | 노드 | 포트 | 프로토콜 | URL 경로 | 설명 |
| --- | --- | --- | --- | --- | --- |
| Spark Thrift 서버 |헤드 노드 |10002 |Thrift | &nbsp; | TooSpark SQL Thrift/JDBC ()를 연결 하기 위한 서비스 |
| Livy 서버 | 헤드 노드 | 8998 | HTTP | /batches | 문, 작업 및 응용 프로그램을 실행하기 위한 서비스 |

예제:

* Livy: `curl "http://10.0.0.11:8998/batches"`. 이 예제에서는 `10.0.0.11` hello 리비 서비스를 호스팅하는 hello 헤드 노드에의 hello IP 주소입니다.
