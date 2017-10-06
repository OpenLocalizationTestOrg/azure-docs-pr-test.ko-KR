---
title: "Azure 이벤트 허브 캡처의 aaaOverview | Microsoft Docs"
description: "Event Hubs 캡처로 원격 분석 데이터 캡처"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Azure Event Hubs 캡처

Azure 이벤트 허브 캡처를 사용 하면 이벤트 허브 tooan의 데이터를 스트리밍 tooautomatically 배달 hello [Azure Blob 저장소](https://azure.microsoft.com/services/storage/blobs/) 또는 [Azure 데이터 레이크 저장소](https://azure.microsoft.com/services/data-lake-store/) hello 사용 하 여 선택한의 계정이 추가 유연성 간격을 시간 또는 크기를 지정 합니다. 캡처를 설정 하는 것은 빠른을 하며, 이벤트 허브와 함께 자동으로 확장 없습니다 관리 비용 toorun [처리량 단위](event-hubs-features.md#capacity)합니다. 이벤트 허브 캡처 hello 스트리밍 데이터를 Azure에는 가장 쉬운 방법은 tooload 이며 toofocus 대신 데이터 캡처에 데이터 처리에 있습니다.

이벤트 허브 캡처 tooprocess 실시간 있으며 파이프라인에서 일괄 처리 기반 hello 동일한 스트림을 합니다. 즉, 시간이 지나면서 요구에 따라 확장되는 솔루션을 빌드할 수 있습니다. 나중에 실시간 처리할 방향으로 염두에 두고 현재 일괄 처리 기반 시스템을 작성 하 든 tooadd 효율적인 콜드 경로 tooan 기존 실시간 솔루션을 원하는 스트리밍 데이터를 보다 쉽게 처리할 수 있으며 이벤트 허브 캡처합니다.

## <a name="how-event-hubs-capture-works"></a>Event Hubs 캡처의 작동 방식

이벤트 허브 원격 분석 수신, 비슷한 tooa 분산된 로그에 대 한 보존 시간 내구성이 있는 버퍼입니다. 이벤트 허브에 키 tooscaling hello는 hello [분할 된 소비자 모델](event-hubs-features.md#partitions)합니다. 각 파티션은 데이터의 독립적인 세그먼트이며 독립적으로 사용됩니다. 이 데이터는 해제 에이징 시간이 지남에 따라 hello 구성 가능한 보존 기간 기반으로 합니다. 결과적으로 지정된 이벤트 허브는 "꽉 참" 상태가 되지 않습니다.

이벤트 허브 캡처 자신의 Azure Blob 저장소 계정 및 컨테이너 또는 Azure 데이터 레이크 저장소 계정에 사용 되는 toostore hello 캡처된 데이터는 toospecify 있습니다 수 있습니다. 이러한 계정은 hello에 수 있는 이벤트 허브로 또는 toohello 유연성 hello 이벤트 허브 캡처 기능을 추가 하는 다른 지역에 동일한 영역입니다.

캡처된 데이터는 [Apache Avro][Apache Avro] 형식으로 작성되는데, 이는 인라인 스키마가 있는 풍부한 데이터 구조를 제공하는 간단하고 빠른 이진 형식입니다. 이 형식은 hello Hadoop 에코 시스템, 스트림 분석 및 Azure Data Factory에 널리 사용 됩니다. Avro 작업에 대한 자세한 내용은 이 문서의 뒷부분을 참조하세요.

### <a name="capture-windowing"></a>캡처 기간 이동

이벤트 허브 캡처 tooset을 창 toocontrol 캡처를 수 있습니다. 이 창은 최소 크기와 타임 구성 정책 사용 하 여"첫 번째 wins," 캡처 작업을 첫 번째 트리거 발생 원인을 hello는 의미입니다. 15 분 있으면 100MB 창 캡처하고 hello 기간 전에 hello 크기 창 트리거 1 m B / 초 송신 합니다. 각 파티션은 독립적으로 캡처합니다 있으며 어떤 hello에 캡처 간격 동안 발생 했습니다 hello 시간에 대 한 명명 된 캡처, hello 시 완성된 블록 blob에 기록 합니다. hello 저장소 명명 규칙은 다음과 같습니다.

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>크기 조정 toothroughput 단위

Event Hubs 트래픽은 [처리량 단위](event-hubs-features.md#capacity)로 제어됩니다. 단일 처리량 단위는 초당 1MB 또는 초당 1000개의 이벤트 수신을 허용하고 송신량은 그 두 배입니다. Standard Event Hubs는 1-20개의 처리량 단위로 구성할 수 있으며 할당량 증가 [지원 요청][support request]을 통해 더 구입할 수 있습니다. 구입한 처리량 단위 범위를 벗어나는 사용량은 제한됩니다. 처리량 단위 송신 할당량을 무시 하 고 프로그램 송신 Stream Analytics 또는 Spark와 같은 다른 처리 판독기에 대 한 저장 hello 내부 이벤트 허브 저장소에서 직접 데이터를 복사 이벤트 허브 캡처 합니다.

Event Hubs 캡처가 구성되면 첫 번째 이벤트를 전송하는 즉시 자동으로 실행되어 계속 실행됩니다. toomake 쉽게 프로그램 다운스트림 처리 tooknow hello 프로세스 작동 하는 이벤트 허브에 대 한 빈 파일 기록 데이터가 없는 경우. 이 프로세스는 일괄 처리 프로세서에 제공할 수 있는 예측 가능한 주기와 표식을 제공합니다.

## <a name="setting-up-event-hubs-capture"></a>Event Hubs 캡처 설정

Hello 이벤트 허브를 만들 때 hello를 사용 하 여 캡처를 구성할 수 있습니다 [Azure 포털](https://portal.azure.com), 또는 Azure 리소스 관리자 템플릿을 사용 합니다. 자세한 내용은 다음 문서는 hello 참조:

- [이벤트 허브 hello Azure 포털을 사용 하 여 캡처를 사용 하도록 설정](event-hubs-capture-enable-through-portal.md)
- [Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브가 있는 Event Hubs 네임스페이스를 만들고 캡처를 사용하도록 설정](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>캡처된 hello 파일을 탐색 및 Avro 사용

이벤트 허브 캡처 hello 구성 된 기간에 지정 된 대로 Avro 형식으로 파일을 만듭니다. [Azure Storage 탐색기][Azure Storage Explorer]와 같은 도구에서 이러한 파일을 볼 수 있습니다. 다운로드할 수 hello 파일을 로컬 toowork에 있습니다.

Avro 스키마를 따르는 hello 있어야 하는 이벤트 허브 캡처에 의해 생성 된 hello 파일:

![][3]

Hello를 사용 하 여 쉽게 tooexplore Avro 파일은 [Avro 도구] [ Avro Tools] Apache에서 jar. 이 jar 파일에 다운로드 한 후 hello 다음 명령을 실행 하 여 특정 Avro 파일의 hello 스키마를 확인할 수 있습니다.

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

이 명령은 다음을 반환합니다.

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

Avro 도구 tooconvert hello 파일 tooJSON 형식을 사용 하 고 다른 처리를 수행할 수도 있습니다.

tooperform 더 높은 수준의 처리 다운로드 및 Avro 사용자가 선택한 플랫폼에 대 한 설치 합니다. 이 문서 작성 hello 시 구현을 사용할 수 있는 C, c + +, C\#, Java, NodeJS, Perl, PHP, Python 및 Ruby 합니다.

Apache Avro에는 [Java][Java] 및 [Python][Python]에 대한 전체 시작 가이드가 있습니다. Hello 읽어 [이벤트 허브 캡처 시작](event-hubs-capture-python.md) 문서.

## <a name="how-event-hubs-capture-is-charged"></a>Event Hubs 캡처의 요금 부과 방식

이벤트 허브 캡처 유료일 toothroughput 단위 마찬가지로: 시간당 요금으로 합니다. hello 충전은 정비례 toohello hello 네임 스페이스에 대해 구입한 처리량 단위 수입니다. 처리량 단위를 증가 및 감소 이벤트 허브 캡처 미터 늘린 tooprovide 성능 일치 하는 감소 합니다. hello 미터 동시에 발생합니다. 가격 정보는 [Event Hubs 가격 책정](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요. 

## <a name="next-steps"></a>다음 단계

이벤트 허브 수집은 hello 가장 쉬운 방법은 tooget 데이터를 Azure로 됩니다. Azure Data Lake, Azure Data Factory 및 Azure HDInsight를 통해 규모에 관계없이 선택한 도구 및 플랫폼을 사용하여 선택한 일괄 처리 및 기타 분석을 수행할 수 있습니다.

Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 전송 및 수신 시작](event-hubs-dotnet-framework-getstarted-send.md)
* [Event Hubs를 사용하는 응용 프로그램 예제][sample application that uses Event Hubs] 전체
* [Event Hubs 개요][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
