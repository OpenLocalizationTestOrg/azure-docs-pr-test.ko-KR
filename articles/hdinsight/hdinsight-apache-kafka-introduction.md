---
title: "aaaAn 소개 tooApache HDInsight-Azure의 Kafka | Microsoft Docs"
description: "HDInsight의 Apache Kafka에 대 한 자세한 내용은: 정의 용도, 및 toofind 예제 시점과 시작 정보입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>HDInsight의 Apache Kafka 소개(미리 보기)

[Apache Kafka](https://kafka.apache.org) 는 오픈 소스 분산된 스트리밍 플랫폼 실시간 사용된 toobuild 일 수 있는 스트리밍 데이터 파이프라인 및 응용 프로그램입니다. Kafka 제공 메시지 브로커 기능 비슷한 tooa 메시지 큐를 게시 하 고 toonamed 데이터 스트림을 구독할 수 있는 합니다. HDInsight의 Kafka hello Microsoft Azure 클라우드에서 관리 되는 확장성이 높은 고 항상 사용 가능한 서비스를 제공합니다.

## <a name="why-use-kafka-on-hdinsight"></a>HDInsight에서 Kafka를 사용하는 이유

Kafka hello를 같은 기능을 제공 합니다.

* 게시-구독 메시징 패턴: Kafka 레코드 tooa Kafka 항목을 게시 하기 위한 공급자 API를 제공 합니다. 소비자 API hello tooa 항목을 구독 하는 경우에 사용 됩니다.

* 스트림 처리: Kafka는 종종 실시간 스트리밍 처리를 위해 Apache Storm 또는 Apache Spark와 함께 사용됩니다. Kafka 0.10.0.0 (HDInsight 버전 3.5) 태풍이 나 Spark를 요구 하지 않고 솔루션을 스트리밍 toobuild 수 있는 스트리밍 API를 도입 했습니다.

* 가로 배율: Kafka hello HDInsight 클러스터의 hello 노드 간에 스트림을 분할 합니다. 소비자 프로세스 개별 파티션을 tooprovide 부하 분산 레코드를 사용할 때와 연결할 수 있습니다.

* 순서 대로 배달: 각 파티션 내에서 레코드 hello 스트림에 수신 된 hello 순서로 저장 됩니다. 파티션마다 소비자 프로세스를 하나씩 연결하여 레코드가 순서대로 처리되도록 보장할 수 있습니다.

* 내결함성: 파티션은 노드 tooprovide 내결함성을 간에 복제할 수 있습니다.

* Azure 관리 되는 디스크와의 통합: 관리 되는 디스크 hello HDInsight 클러스터의 hello 가상 컴퓨터에서 사용 하는 hello 디스크에 대 한 더 높은 처리량 및 크기를 제공 합니다.

    Kafka HDInsight에 대 한 관리 되는 디스크는 기본적으로 사용 하 고 HDInsight 만드는 동안 노드당 사용 되는 디스크의 hello 수를 구성할 수 있습니다. 관리 디스크에 대한 자세한 내용은 [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.

    HDInsight에서 Kafka로 관리 디스크 구성에 대한 자세한 내용은 [HDInsight에서 Kafka의 확장성 높이기](hdinsight-apache-kafka-scalability.md)를 참조하세요.

## <a name="use-cases"></a>사용 사례

* **메시징**: hello를 지원 하므로 게시-구독 패턴을 메시지, Kafka는 대개 메시지 브로커도 사용 됩니다.

* **활동 추적**: 이후 Kafka 레코드의 순서로 로깅을 제공, 사용 되는 tootrack 수 있으며 작업을 다시 생성 합니다. 예를 들어 웹 사이트 또는 응용 프로그램에서의 사용자 작업이 여기에 해당합니다.

* **집계**: 스트림 처리를 사용 하 여 다양 한 스트림 toocombine에서 정보를 집계 있고 hello 정보 운영 데이터를 중앙 집중화 하 고 있습니다.

* **변환**: 스트림 처리를 사용하여 여러 입력 토픽의 데이터를 하나 이상의 출력 토픽으로 결합하고 보강할 수 있습니다.

## <a name="next-steps"></a>다음 단계

사용 하 여 hello 다음 toolearn를 어떻게 링크 toouse HDInsight의 Apache Kafka:

* [HDInsight에서 Apache Kafka 시작](hdinsight-apache-kafka-get-started.md)

* [HDInsight의 MirrorMaker toocreate Kafka의 복제본을 사용 하 여](hdinsight-apache-kafka-mirroring.md)

* [HDInsight의 Kafka에서 Apache Storm 사용](hdinsight-apache-storm-with-kafka.md)

* [HDInsight의 Kafka에서 Apache Spark 사용](hdinsight-apache-spark-with-kafka.md)

* [Azure 가상 네트워크를 통해 tooKafka 연결](hdinsight-apache-kafka-connect-vpn-gateway.md)
