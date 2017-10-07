---
title: "Apache Kafka-Azure HDInsight와 aaaHigh 가용성 | Microsoft Docs"
description: "자세한 내용은 어떻게 Azure HDInsight의 Apache Kafka 있는 고가용성 tooensure 합니다. HDInsight를 포함 하는 Azure 지역 hello 내에서 여러 오류 도메인에 있는 있도록 toorebalance Kafka의 복제본을 분할 하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>HDInsight의 Apache Kafka(미리 보기)를 통한 데이터 고가용성

기본 하드웨어 Kafka 항목 tootake 사용에 대 한 파티션 복제본 tooconfigure 구성 랙 하는 방법에 대해 알아봅니다. 이 구성을 통해 hello 가용성 HDInsight의 Apache Kafka에 저장 된 데이터.

## <a name="fault-and-update-domains-with-kafka"></a>Kafka를 사용하는 장애 및 업데이트 도메인

장애 도메인은 Azure 데이터 센터에 있는 기본 하드웨어의 논리적 그룹입니다. 장애 도메인마다 공통 전원과 네트워크 스위치를 공유합니다. hello 가상 컴퓨터 및 hello 노드 HDInsight 클러스터 내에서 구현 하는 관리 되는 디스크는 이러한 오류 도메인에 걸쳐 분산 됩니다. 이 아키텍처는 hello 물리적 하드웨어 오류의 잠재적 영향을 제한합니다.

Azure 지역마다 특정 수의 장애 도메인이 있습니다. 도메인 및 hello 포함 하는 장애 도메인 수의 목록이 참조 hello [가용성 집합](../virtual-machines/linux/regions-and-availability.md#availability-sets) 설명서입니다.

> [!IMPORTANT]
> Kafka는 장애 도메인을 인식하지 않습니다. Hello에서 모든 파티션 복제본을 저장할 수 있습니다 Kafka에 항목을 만들 때 동일한 장애 도메인입니다. toosolve hello 제공이 문제를 [Kafka 파티션을 리 밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools)합니다.

## <a name="when-toorebalance-partition-replicas"></a>Toorebalance 복제본을 분할 하는 경우

tooensure Kafka 데이터의 가장 높은 가용성을 hello를 있습니다 해야 균형을 다시 조정할 hello 파티션 복제본 hello 다음 번에 항목:

* 새 토픽 또는 파티션을 만들 때

* 클러스터를 확장할 때

## <a name="replication-factor"></a>복제 계수

> [!IMPORTANT]
> 3개의 장애 도메인을 포함하는 Azure 지역을 사용하고 복제 계수로 3을 사용하는 것이 좋습니다.

두 개의 오류 도메인을 포함 하는 영역의 사용 해야 할 경우 사용 하 여 4 toospread hello 복제본의 복제 요소 균등 하 게 hello 두 개의 오류 도메인입니다.

항목 및 설정 hello 복제 요소를 만드는 예를 들어 참조 hello [HDInsight의 Kafka로 시작](hdinsight-apache-kafka-get-started.md) 문서.

## <a name="how-toorebalance-partition-replicas"></a>Toorebalance 복제본을 분할 하는 방법

사용 하 여 hello [Kafka 파티션을 리 밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance 항목을 선택 합니다. SSH 세션 toohello의 헤드 노드 Kafka 클러스터에서에서이 도구를 실행 해야 합니다.

SSH를 사용 하 여 tooHDInsight 연결 방법에 대 한 자세한 내용은 참조는 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

## <a name="next-steps"></a>다음 단계

* [HDInsight의 Kafka 확장성](hdinsight-apache-kafka-scalability.md)
* [HDInsight의 Kafka 미러링](hdinsight-apache-kafka-mirroring.md)