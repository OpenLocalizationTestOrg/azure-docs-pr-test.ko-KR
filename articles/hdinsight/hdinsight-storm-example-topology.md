---
title: "HDInsight의 Apache Storm 토폴로지 aaaExample | Microsoft Docs"
description: "이벤트 허브와 함께 작동하며 기본 C# 및 Java 토폴로지를 포함하여 HDInsight에서 Apache Storm을 통해 생성 및 테스트된 Storm 토폴로지 예제 목록입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>HDInsight의 Apache Storm에 대한 Storm 토폴로지 및 구성 요소 예제

hello 다음은 예제에서 만들고 유지 관리 Microsoft HDInsight의 Apache Storm와 함께 사용할의 목록입니다. 이 예에서는 다양 한 이벤트 허브, Cosmos DB, Power BI, SQL 데이터베이스, Azure 저장소 및 HDInsight에서 HBase과 같은 Azure 서비스를 사용 하 여 기본 C#과 Java 토폴로지 tooworking 만들기에서 항목을 다룹니다. 몇 가지 예를 보여 줍니다 방법을 toowork SignalR Socket.IO 등의 비 Azure 또는 Microsoft 이외의 기술 사용 합니다.

| 설명 | 데모 | 언어/프레임워크 |
|:--- |:--- |:--- |
| [Apache Storm에서 쓰기를 tooAzure 데이터 레이크 저장소](hdinsight-storm-write-data-lake-store.md) |데이터 레이크 저장소 tooAzure 작성 |Java |
| [이벤트 허브 Spout 및 Bolt 원본](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |이벤트 허브 Spout hello 및 모양에 대 한 소스 |Java |
| [HDInsight에서 Apache Storm에 대한 Java 기반 토폴로지 개발][5797064f] |Maven |자바 |
| [Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발][16fce2d1] |Visual Studio용 HDInsight 도구 |C#, Java |
| [C# Storm 토폴로지에서 여러 데이터 스트림 만들기][ec5a4064] |여러 스트림 |C# |
| [HDInsight의 Storm(C#)에서 Azure Event Hubs의 이벤트 처리][844d1d81] |Event Hubs |C# 및 Java |
| [HDInsight의 Storm으로 Azure Event Hubs에서 이벤트 처리(Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Event Hubs |Java |
| [Power Bi toovisualize 데이터 스톰 토폴로지를 사용 하 여][94d15238] |Power BI |C# |
| [HDInsight에서 Apache Storm 및 HBase를 사용하여 센서 데이터 분석][ab894747] |Event Hubs, HBase, Socket.IO, 웹 대시보드 |C#, Java, JavaScript, HTML |
| [HDInsight의 Storm을 사용하여 Event Hub에서 차량 센서 데이터 처리][246ee964] |Event Hubs, Cosmos DB, Azure Storage Blob(WASB) |C#, Java |
| [추출, 변환 및 로드 (ETL)에서 Azure 이벤트 허브 tooHBase 스톰 HDInsight에서 사용 하 여][b4b68194] |Event Hubs, HBase |C# |
| [HDInsight의 Storm에서 Azure 서비스로 작업하는 데 사용되는 템플릿 C# Storm 토폴로지 프로젝트][ce0c02a2] |Event Hub, Cosmos DB SQL Database, HBase, SignalR |C#, Java |
| [HDInsight의 Storm을 사용하여 Azure Event Hub에서 읽기에 대한 확장성 벤치마크][d6c540e3] |메시지 처리량, Event Hubs, SQL Database |C#, Java |
| [HDInsight에서 Storm 및 HBase를 사용하여 이벤트의 상관 관계 지정](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [HDInsight에서 Storm으로 Python 사용](hdinsight-storm-develop-python-topology.md) |Flux 토폴로지를 포함하는 Python 구성 요소 |파이썬 |
| [HDInsight의 Storm에서 Kafka 사용](hdinsight-apache-storm-with-kafka.md) | Apache Storm 읽기 및 쓰기 tooApache Kafka | Java |

### <a name="next-steps"></a>다음 단계

* [HDInsight의 Apache Storm 시작][2b8c3488]
* [자세한 내용은 방법 toodeploy 및 HDInsight의 Storm 스톰 토폴로지 관리][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "HDInsight 클러스터 및 용도에 스톰 toocreate 스톰 대시보드 toodeploy 예제 토폴로지 hello 하는 방법에 대해 알아봅니다."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "자세한 방법을 toodeploy hello 스톰 웹 기반 대시보드 및 스톰 UI 또는 hello HDInsight 도구를 사용 하 여 Visual Studio에 대 한 토폴로지를 관리 합니다."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Toocreate C# 스톰 토폴로지를 사용 하 여 Visual Studio에 대 한 HDInsight 도구에 hello 하는 방법에 대해 알아봅니다."
[5797064f]: hdinsight-storm-develop-java-topology.md "자세한 방법을 Maven에서 기본 wordcount 토폴로지를 만들어서 사용 하 여 java에서 toocreate 스톰 토폴로지입니다."
[94d15238]: hdinsight-storm-power-bi-topology.md "보여 줍니다 toowrite 데이터 tooPower BI는 C# 토폴로지를에서 다음에서 만드는 방법을 차트 및 대시보드 hello 데이터입니다."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "C#으로 구현된 단어 개수를 수행하는 기본 Storm 토폴로지를 보여 줍니다. 또한 방법을 toocreate 여러 데이터는 C# 토폴로지 내에서 스트림을 설명 합니다."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "자세한 내용은 방법 HDInsight의 Storm와 Azure 이벤트 허브에서 데이터를 tooread 및 쓰기입니다."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Azure 이벤트 허브의 HDInsight tooprocess 센서 데이터에 대해 Apache Storm toouse D3.js를 사용 하 여 시각화 하 고 (옵션) tooHBase 저장 하는 방법을 알아봅니다."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "어떻게 toouse Azure 이벤트 허브에서 Storm 토폴로지 tooread 메시지 문서 Azure Cosmos DB에서 참조 하는 데이터에 대 한 읽고 저장할 데이터 tooAzure 저장소에 알아봅니다."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "여러 토폴로지 toodemonstrate 처리량 HDInsight의 Apache Storm를 사용 하 여 데이터베이스를 Azure 이벤트 허브에서 읽기 및 tooSQL 저장 하는 경우."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Tooread 데이터 Azure 이벤트 허브, 집계 및 변환에서에서 데이터를 hello 하 다음 HDInsight의 tooHBase을 저장 하는 방법에 대해 알아봅니다."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "이 프로젝트 spouts, 볼트 및 토폴로지 toointeract 이벤트 허브, Cosmos DB 및 SQL 데이터베이스와 같은 여러 Azure 서비스에 대 한 템플릿을 포함합니다."

