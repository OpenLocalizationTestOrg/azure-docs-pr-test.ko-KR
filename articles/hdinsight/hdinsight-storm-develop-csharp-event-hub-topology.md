---
title: "Storm-Azure HDInsight으로 이벤트 허브에서 aaaProcess 이벤트 | Microsoft Docs"
description: "C# 스톰 토폴로지를 사용 하 여 Azure 이벤트 허브에서 tooprocess 데이터 만드는 방법 Visual Studio에서 hello를 사용 하 여 HDInsight tools for Visual Studio에 알아봅니다."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>HDInsight의 Storm(C#)으로 Azure Event Hubs에서 이벤트 처리

자세한 방법을 toowork HDInsight의 Apache Storm에서 Azure 이벤트 허브입니다. 이 문서에서는 Evbent 허브에서 C# 스톰 토폴로지 tooread 및 쓰기 데이터 사용

> [!NOTE]
> 이 프로젝트의 Java 버전은 [HDInsight의 Storm(Java)으로 Azure Event Hubs에서 이벤트 처리](hdinsight-storm-develop-java-event-hub-topology.md)를 참조하세요.

## <a name="scpnet"></a>SCP.NET

이 문서의 단계 hello SCP.NET, NuGet 패키지를 사용 하면 쉽게 toocreate C# 토폴로지 및 스톰와 함께 사용할 구성 요소에 HDInsight를 사용 합니다.

> [!IMPORTANT]
> Hello이 문서의 단계 동안 Visual Studio와 함께 Windows 개발 환경에 의존, hello 컴파일된 프로젝트 Linux를 사용 하는 HDInsight 클러스터에 제출 된 tooa 스톰 될 수 있습니다. 2016년 10월 28일 이후에 만든 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.

HDInsight 3.4 및 큰 사용 모노 toorun C# 토폴로지입니다. 이 문서에 사용 된 hello 예제 HDInsight 3.6 작동 합니다. HDInsight에 대 한.NET 솔루션을 만드는 방법에 하려는 경우 확인 hello [모노 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 잠재적인 호환성 문제에 대 한 문서입니다.

### <a name="cluster-versioning"></a>클러스터 버전 관리

hello Microsoft.SCP.Net.SDK NuGet 패키지를 프로젝트에 사용할 HDInsight에 설치 된 Storm의 주 버전 hello 일치 해야 합니다. HDInsight 버전 3.5 및 3.6은 Storm 1.x를 사용하므로 이 클러스터와 함께 SCP.NET 버전 1.0.x.x를 사용해야 합니다.

> [!IMPORTANT]
> 이 문서에 hello 예제 HDInsight 3.5 또는 3.6 클러스터에 필요합니다.
>
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

C# 토폴로지도 .NET 4.5를 대상으로 해야 합니다.

## <a name="how-toowork-with-event-hubs"></a>어떻게 toowork 이벤트 허브

Microsoft 스톰 토폴로지에서 이벤트 허브 사용된 toocommunicate 일 수 있는 Java 구성 요소 집합을 제공 합니다. HDInsight 3.6 호환 버전에서 이러한 구성 요소를 포함 하는 hello Java 보관 파일 (JAR) 파일을 찾을 수 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)합니다.

> [!IMPORTANT]
> Hello 구성 요소는 Java로 작성 된 경우 C# 토폴로지에서 쉽게 사용할 수 있습니다.

이 예제에 다음과 같은 구성 요소가 hello 사용 됩니다.

* __EventHubSpout__: Event Hubs에서 데이터를 읽습니다.
* __EventHubBolt__: tooEvent 데이터 허브를 씁니다.
* __EventHubSpoutConfig__: tooconfigure EventHubSpout를 사용 합니다.
* __EventHubBoltConfig__: tooconfigure EventHubBolt를 사용 합니다.

### <a name="example-spout-usage"></a>예제 Spout 사용

SCP.NET은 EventHubSpout tooyour 토폴로지를 추가 하기 위한 메서드를 제공 합니다. 이러한 메서드는 Java 구성 요소를 추가 하기 위한 hello 제네릭 메서드를 사용 하 여 보다 쉽게 tooadd는 배출구 만듭니다. hello 다음 예제에서는 방법을 사용 하 여 배출구 toocreate hello __SetEventHubSpout__ 및 **EventHubSpoutConfig** SCP.NET에서 제공 하는 메서드:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

이전 예제 hello 라는 새 배출구 구성 요소를 만들고 __EventHubSpout__, 이벤트 허브 사용 toocommunicate을 구성 합니다. hello 구성 요소에 대 한 병렬 처리 힌트 hello hello 이벤트 허브에 toohello 파티션 수가 설정 됩니다. 이 설정을 통해 스톰 toocreate 각 파티션에 대 한 hello 구성 요소의 인스턴스.

### <a name="example-bolt-usage"></a>예제 Bolt 사용

사용 하 여 hello **JavaComponmentConstructor** 메서드 toocreate hello 볼트의 인스턴스입니다. hello 다음 예제에서는 어떻게 toocreate hello의 새 인스턴스를 구성 하 고 **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> 이 예에서는 사용 하는 대신 문자열로 전달 Clojure 식 **JavaComponentConstructor** toocreate는 **EventHubBoltConfig**hello 배출구 예제 때와 마찬가지로, 합니다. 어떤 방법이든 작동합니다. 최상의 tooyou 판단는 hello 방법을 사용 합니다.

## <a name="download-hello-completed-project"></a>완료 하는 hello 프로젝트 다운로드

이 자습서에서 만든 hello 프로젝트의 전체 버전을 다운로드할 수 있습니다 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)합니다. 그러나 보내야 tooprovide 구성 설정을이 자습서에서는 hello 단계에 따라 합니다.

### <a name="prerequisites"></a>필수 조건

* [HDInsight 클러스터 버전 3.5 또는 3.6의 Apache Storm](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > 이 문서에 사용 되는 hello 예제 스톰 HDInsight 버전 3.5 또는 3.6에 필요 합니다. 기한 toobreaking 클래스 이름 변경, HDInsight의 이전 버전으로 작동 하지 않습니다. 이전 클러스터에서 작동하는 이 예제의 버전은 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases)를 참조하세요.

* [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

* hello [Azure.NET SDK](http://azure.microsoft.com/downloads/)합니다.

* hello [Visual Studio 용 HDInsight 도구](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.

* 개발 환경에서 Java JDK 1.8 이상. JDK 다운로드는 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 사용할 수 있습니다.

  * hello **JAVA_HOME** Java 포함 되어 있는 환경 변수 해야 지점 toohello 디렉터리입니다.
  * hello **%JAVA_HOME%/bin** 디렉터리 hello 경로에 있어야 합니다.

## <a name="download-hello-event-hubs-components"></a>Hello 이벤트 허브 구성 요소 다운로드

다운로드 hello 이벤트 허브 spout 및 구성 요소에서 볼트 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)합니다.

라는 디렉터리를 만들고 `eventhubspout`, hello 디렉터리로 hello 파일을 저장 합니다.

## <a name="configure-event-hubs"></a>Event Hubs 구성

이벤트 허브는이 예제에 대 한 hello 데이터 원본. Hello 정보를 사용 하 여의 hello "이벤트 허브 만들기" 섹션에 [이벤트 허브 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)합니다.

1. Hello 이벤트 허브를 만든 후 보기 hello **EventHub** hello Azure 포털에서 선택에 블레이드 **공유 액세스 정책을**합니다. 선택 **+ 추가** tooadd hello 다음 정책:

   | 이름 | 권한 |
   | --- | --- |
   | 기록기 |보내기 |
   | 판독기 |수신 대기 |

    ![공유 액세스 정책 창의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. 선택 hello **판독기** 및 **기록기** 정책입니다. 복사 하 고 이러한 값은 나중에 사용 되는 두 정책 모두에 대 한 hello 기본 키 값을 저장 합니다.

## <a name="configure-hello-eventhubwriter"></a>Hello EventHubWriter 구성

1. Visual Studio 용 hello 최신 버전의 hello HDInsight 도구를 아직 설치 하지 있을 경우 참조 [Visual Studio 용 HDInsight 도구를 사용 하 여 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.

2. Hello 솔루션에서 다운로드 [eventhub-스톰-하이브리드](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)합니다.

3. Hello에 **EventHubWriter** 프로젝트, 열기 hello **App.config** 파일입니다. Hello 키 다음에 대 한 hello 값에서 이전 toofill를 구성 하는 hello 이벤트 허브에서 hello 정보를 사용 하 여:

   | 키 | 값 |
   | --- | --- |
   | EventHubPolicyName |기록기 (hello 정책에 다른 이름을 사용 하는 경우 *보낼* 권한, 대신 사용 합니다.) |
   | EventHubPolicyKey |hello 기록기 정책에 대 한 hello 키입니다. |
   | EventHubNamespace |이벤트 허브를 포함 하는 hello 네임 스페이스 |
   | EventHubName |이벤트 허브 이름 |
   | EventHubPartitionCount |이벤트 허브에 대 한 파티션 hello 수입니다. |

4. 저장 후 닫기 hello **App.config** 파일입니다.

## <a name="configure-hello-eventhubreader"></a>Hello EventHubReader 구성

1. 열기 hello **EventHubReader** 프로젝트.

2. 열기 hello **App.config** hello에 대 한 파일 **EventHubReader**합니다. Hello 키 다음에 대 한 hello 값에서 이전 toofill를 구성 하는 hello 이벤트 허브에서 hello 정보를 사용 하 여:

   | 키 | 값 |
   | --- | --- |
   | EventHubPolicyName |판독기 (hello 정책에 다른 이름을 사용 하는 경우 *수신* 권한, 대신 사용 합니다.) |
   | EventHubPolicyKey |hello 판독기 정책에 대 한 hello 키입니다. |
   | EventHubNamespace |이벤트 허브를 포함 하는 hello 네임 스페이스 |
   | EventHubName |이벤트 허브 이름 |
   | EventHubPartitionCount |이벤트 허브에 대 한 파티션 hello 수입니다. |

3. 저장 후 닫기 hello **App.config** 파일입니다.

## <a name="deploy-hello-topologies"></a>Hello 토폴로지를 배포 합니다.

1. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **EventHubReader** 프로젝트를 마우스 선택 **HDInsight의 tooStorm 제출**합니다.

    ![스크린샷의 솔루션 탐색기에서 강조 표시 하는 HDInsight의 전송 tooStorm와](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. Hello에 **제출 토폴로지** 대화 상자를 선택 하면 **Storm 클러스터**합니다. 확장 **추가 구성을**선택, **Java 파일 경로**선택, **...** , 및 이전에 다운로드 한 hello JAR 파일이 포함 된 select hello 디렉터리입니다. 마지막으로 **제출**을 클릭합니다.

    ![토폴로지 제출 대화 상자의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Hello 토폴로지가 제출 될 때 hello **스톰 토폴로지 뷰어** 나타납니다. hello 토폴로지를 선택 하는 hello에 대 한 정보 tooview **EventHubReader** hello 왼쪽된 창에는 토폴로지입니다.

    ![Storm Topologies Viewer의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **EventHubWriter** 프로젝트를 마우스 선택 **HDInsight의 tooStorm 제출**합니다.

5. Hello에 **제출 토폴로지** 대화 상자를 선택 하면 **Storm 클러스터**합니다. 확장 **추가 구성을**선택, **Java 파일 경로**선택, **...** , hello JAR 파일이 포함 된 select hello 디렉터리 이전에 다운로드 한 및 합니다. 마지막으로 **제출**을 클릭합니다.

6. Hello 토폴로지가 제출 될 때 hello에 hello 토폴로지 목록 새로 고침 **스톰 토폴로지 뷰어** tooverify 두 토폴로지 모두 hello 클러스터에서 실행 되는 합니다.

7. **스톰 토폴로지 뷰어**선택, hello **EventHubReader** 토폴로지입니다.

8. hello 모양에 대 한 요약 tooopen hello 구성 요소를 두 번 클릭 hello **LogBolt** hello 다이어그램에서 구성 요소입니다.

9. Hello에 **Executor** hello에서 hello 링크 중 하나를 선택 하십시오 섹션 **포트** 열입니다. Hello 구성 요소에 의해 기록 된 정보를 표시 합니다. hello 기록 정보는 텍스트 다음 유사한 toohello 됩니다.

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Hello 토폴로지를 중지 합니다.

toostop hello 토폴로지 hello에서 각각의 토폴로지를 선택 **스톰 토폴로지 뷰어**, 클릭 **Kill**합니다.

![종료 단추가 강조 표시된 Storm Topologies Viewer의 스크린샷](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>클러스터 삭제

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>다음 단계

이 문서에서는 어떻게 toouse hello Java 이벤트 허브 spout 및 C# 토폴로지 toowork Azure 이벤트 허브의 데이터로에서 볼트 배웠습니다. C# 토폴로지를 만들기에 대 한 더 toolearn hello 다음을 참조 합니다.

* [Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [SCP 프로그래밍 가이드](hdinsight-storm-scp-programming-guide.md)
* [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)
