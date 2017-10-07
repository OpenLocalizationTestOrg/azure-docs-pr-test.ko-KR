---
title: "aaaApache Kafka 크기-Azure HDInsight 늘이기 | Microsoft Docs"
description: "Tooconfigure tooincrease 확장성 Azure HDInsight의 Apache Kafka 클러스터에 대 한 디스크를 관리 하는 방법에 대해 알아봅니다."
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>HDInsight에서 Apache Kafka에 대한 확장성 및 저장소 구성

HDInsight의 Apache Kafka에 사용 되는 관리 되는 디스크의 tooconfigure hello 번호에 알아봅니다.

HDInsight의 Kafka hello HDInsight 클러스터에 hello hello 가상 컴퓨터의 로컬 디스크를 사용합니다. Kafka 많음, I/O 이므로 [Azure 관리 되는 디스크](../virtual-machines/windows/managed-disks-overview.md) tooprovide 사용 되는 높은 처리량 이며 노드당 더 많은 저장소를 제공 합니다. 기존 가상 하드 드라이브 (VHD) Kafka에 사용 된 경우 각 노드의 제한 too1 TB입니다. 관리 되는 디스크와 여러 개의 디스크 tooachieve를 사용할 수 있습니다 hello 클러스터의 각 노드에 대해 16TB입니다.

hello 다음 다이어그램에서는 관리 되는 디스크 하기 전에 HDInsight의 Kafka와 Kafka 간의 비교 HDInsight의 관리 되는 디스크와:

![vm당 하나의 vhd를 사용하는 HDInsight의 Kafka와 vm당 여러 관리 디스크가 있는 Kafka를 보여주는 다이어그램](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>관리 디스크 구성: Azure Portal

1. Hello에 hello 단계를 따라 [HDInsight 클러스터를 만들 수](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello 일반적인 단계 toocreate hello 포털을 사용 하는 클러스터입니다. Hello 포털 만들기 프로세스를 완료 하지 마세요.

2. Hello에서 __클러스터 크기__ 블레이드에서 사용 하 여 hello __작업자 노드당 디스크__ 디스크 tooconfigure hello 수 필드입니다.

    > [!NOTE]
    > hello 종류의 관리 되는 디스크 일 수 __표준__ (HDD) 또는 __프리미엄__ (SSD). 프리미엄 디스크는 DS 및 GS 시리즈 VM에 사용됩니다. 다른 모든 VM 유형은 표준을 사용합니다.

    ![강조 표시 하는 작업자 노드당 hello 디스크와 hello 클러스터 크기 블레이드의 이미지](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>관리 디스크 구성: Resource Manager 템플릿

hello 작업자 노드 Kafka 클러스터에서 사용 하 여 hello hello 서식 파일의 섹션 다음에 사용 되는 디스크 toocontrol hello 수:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Tooconfigure에서 디스크를 관리 하는 방법을 보여 주는 전체 템플릿을 찾을 수 있습니다 [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json)합니다.

## <a name="next-steps"></a>다음 단계

HDInsight의 Kafka와 작업에 자세한 내용은 다음 문서는 hello 참조:

* [HDInsight의 MirrorMaker toocreate Kafka의 복제본을 사용 하 여](hdinsight-apache-kafka-mirroring.md)
* [HDInsight의 Kafka에서 Apache Storm 사용](hdinsight-apache-storm-with-kafka.md)
* [HDInsight의 Kafka에서 Apache Spark 사용](hdinsight-apache-spark-with-kafka.md)
* [Azure 가상 네트워크를 통해 tooKafka 연결](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Kafka와 관리 디스크에 대한 HDInsight 블로그](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)