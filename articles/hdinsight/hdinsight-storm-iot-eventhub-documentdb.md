---
title: "HDInsight의 Apache Storm를 사용 하 여 aaaProcess 차량 센서 데이터 | Microsoft Docs"
description: "자세한 내용은 방법 HDInsight의 Apache Storm를 사용 하 여 이벤트 허브에서 tooprocess 자동차 센서 데이터입니다. Azure Cosmos DB에서 모델 데이터를 추가 하 고 출력 toostorage를 저장 합니다."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>HDInsight의 Apache Storm을 사용하여 Azure 이벤트 허브에서 차량 센서 데이터를 처리하는 방법에 대해 알아봅니다.

자세한 내용은 방법 HDInsight의 Apache Storm를 사용 하 여 Azure 이벤트 허브에서 tooprocess 자동차 센서 데이터입니다. 이 예제에서는 Azure 이벤트 허브에서 센서 데이터를 읽고, Azure Cosmos DB에 저장 된 데이터를 참조 하 여 hello 데이터를 강화 합니다. hello 데이터는 Hadoop 파일 시스템 (HDFS) hello를 사용 하 여 Azure 저장소에 저장 됩니다.

![HDInsight 및 hello 인터넷 IoT (사물) 아키텍처 다이어그램](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>개요

센서 toovehicles 추가 기록 데이터 추세를 기반으로 toopredict 장비 문제가 있습니다. Toomake 개선 사용량 패턴 분석에 따라 toofuture 버전을 수도 있습니다. 수 tooquickly를 여야 하며 효율적으로 hello 데이터 로드 모든 차량에서 Hadoop MapReduce 처리가 발생할 수 있습니다. 또한 중요 한 경로 (엔진 온도, brakes, 등)에 대 한 toodo 분석 실시간으로 지정할 수 있습니다.

Azure 이벤트 허브는 센서에 의해 생성 된 데이터의 toohandle hello 대규모 볼륨을 만들어집니다. Apache Storm HDFS에 저장 되기 전에 사용 되는 tooload 및 hello 데이터 처리를 수 있습니다.

## <a name="solution"></a>해결 방법

엔진 온도, 주변 온도 및 차량 속도에 대한 원격 분석 데이터는 센서에서 기록합니다. 데이터는 tooEvent 허브 hello 자동차의 자동차를 움직일 식별 번호 (VIN) 및 타임 스탬프와 함께 전송 됩니다. 여기에서 HDInsight 클러스터에는 Apache Storm에서 실행 되는 스톰 토폴로지 hello 데이터를 읽고, 처리 한 HDFS에 저장 합니다.

처리 하는 동안 hello VIN Cosmos DB에서 사용 되는 tooretrieve 모델 정보입니다. 이 데이터는 저장 되기 전에 toohello 데이터 스트림을 추가 됩니다.

Storm 토폴로지 hello에 사용 된 hello 구성 요소입니다.

* **EventHubSpout** - Azure 이벤트 허브에서 데이터를 읽습니다.
* **TypeConversionBolt** -변환 hello 같은 센서 데이터가 포함 된 튜플로 이벤트 허브에서 JSON 문자열 hello:
    * 엔진 온도
    * 주변 온도
    * 속도
    * VIN
    * Timestamp
* **DataReferencBolt** -hello VIN를 사용 하 여 Cosmos DB에서 hello 차량 모델을 조회 합니다.
* **WasbStoreBolt** -저장소 hello 데이터 tooHDFS (Azure 저장소)

hello 다음 이미지는이 솔루션의 다이어그램:

![Storm 토폴로지](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>구현

완전 한 자동화 된 방법으로이 시나리오를 사용할 수 없으면 hello의 일부로 [예제-스톰-HDInsight](https://github.com/hdinsight/hdinsight-storm-examples) GitHub의 리포지토리 합니다. toouse hello에 hello 단계 수행이이 예제에서는 [IoTExample 추가 정보입니다. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md)합니다.

## <a name="next-steps"></a>다음 단계

Storm 토폴로지에 대한 자세한 내용은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.

