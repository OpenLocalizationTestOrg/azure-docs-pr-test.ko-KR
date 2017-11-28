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
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="05bab-103">Azure Event Hubs 캡처</span><span class="sxs-lookup"><span data-stu-id="05bab-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="05bab-104">Azure 이벤트 허브 캡처를 사용 하면 이벤트 허브 tooan의 데이터를 스트리밍 tooautomatically 배달 hello [Azure Blob 저장소](https://azure.microsoft.com/services/storage/blobs/) 또는 [Azure 데이터 레이크 저장소](https://azure.microsoft.com/services/data-lake-store/) hello 사용 하 여 선택한의 계정이 추가 유연성 간격을 시간 또는 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="05bab-105">캡처를 설정 하는 것은 빠른을 하며, 이벤트 허브와 함께 자동으로 확장 없습니다 관리 비용 toorun [처리량 단위](event-hubs-features.md#capacity)합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="05bab-106">이벤트 허브 캡처 hello 스트리밍 데이터를 Azure에는 가장 쉬운 방법은 tooload 이며 toofocus 대신 데이터 캡처에 데이터 처리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="05bab-107">이벤트 허브 캡처 tooprocess 실시간 있으며 파이프라인에서 일괄 처리 기반 hello 동일한 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="05bab-108">즉, 시간이 지나면서 요구에 따라 확장되는 솔루션을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="05bab-109">나중에 실시간 처리할 방향으로 염두에 두고 현재 일괄 처리 기반 시스템을 작성 하 든 tooadd 효율적인 콜드 경로 tooan 기존 실시간 솔루션을 원하는 스트리밍 데이터를 보다 쉽게 처리할 수 있으며 이벤트 허브 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="05bab-110">Event Hubs 캡처의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="05bab-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="05bab-111">이벤트 허브 원격 분석 수신, 비슷한 tooa 분산된 로그에 대 한 보존 시간 내구성이 있는 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="05bab-112">이벤트 허브에 키 tooscaling hello는 hello [분할 된 소비자 모델](event-hubs-features.md#partitions)합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="05bab-113">각 파티션은 데이터의 독립적인 세그먼트이며 독립적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="05bab-114">이 데이터는 해제 에이징 시간이 지남에 따라 hello 구성 가능한 보존 기간 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="05bab-115">결과적으로 지정된 이벤트 허브는 "꽉 참" 상태가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="05bab-116">이벤트 허브 캡처 자신의 Azure Blob 저장소 계정 및 컨테이너 또는 Azure 데이터 레이크 저장소 계정에 사용 되는 toostore hello 캡처된 데이터는 toospecify 있습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="05bab-117">이러한 계정은 hello에 수 있는 이벤트 허브로 또는 toohello 유연성 hello 이벤트 허브 캡처 기능을 추가 하는 다른 지역에 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="05bab-118">캡처된 데이터는 [Apache Avro][Apache Avro] 형식으로 작성되는데, 이는 인라인 스키마가 있는 풍부한 데이터 구조를 제공하는 간단하고 빠른 이진 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="05bab-119">이 형식은 hello Hadoop 에코 시스템, 스트림 분석 및 Azure Data Factory에 널리 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="05bab-120">Avro 작업에 대한 자세한 내용은 이 문서의 뒷부분을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05bab-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="05bab-121">캡처 기간 이동</span><span class="sxs-lookup"><span data-stu-id="05bab-121">Capture windowing</span></span>

<span data-ttu-id="05bab-122">이벤트 허브 캡처 tooset을 창 toocontrol 캡처를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="05bab-123">이 창은 최소 크기와 타임 구성 정책 사용 하 여"첫 번째 wins," 캡처 작업을 첫 번째 트리거 발생 원인을 hello는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="05bab-124">15 분 있으면 100MB 창 캡처하고 hello 기간 전에 hello 크기 창 트리거 1 m B / 초 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="05bab-125">각 파티션은 독립적으로 캡처합니다 있으며 어떤 hello에 캡처 간격 동안 발생 했습니다 hello 시간에 대 한 명명 된 캡처, hello 시 완성된 블록 blob에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="05bab-126">hello 저장소 명명 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="05bab-127">크기 조정 toothroughput 단위</span><span class="sxs-lookup"><span data-stu-id="05bab-127">Scaling toothroughput units</span></span>

<span data-ttu-id="05bab-128">Event Hubs 트래픽은 [처리량 단위](event-hubs-features.md#capacity)로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="05bab-129">단일 처리량 단위는 초당 1MB 또는 초당 1000개의 이벤트 수신을 허용하고 송신량은 그 두 배입니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="05bab-130">Standard Event Hubs는 1-20개의 처리량 단위로 구성할 수 있으며 할당량 증가 [지원 요청][support request]을 통해 더 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="05bab-131">구입한 처리량 단위 범위를 벗어나는 사용량은 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="05bab-132">처리량 단위 송신 할당량을 무시 하 고 프로그램 송신 Stream Analytics 또는 Spark와 같은 다른 처리 판독기에 대 한 저장 hello 내부 이벤트 허브 저장소에서 직접 데이터를 복사 이벤트 허브 캡처 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="05bab-133">Event Hubs 캡처가 구성되면 첫 번째 이벤트를 전송하는 즉시 자동으로 실행되어 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="05bab-134">toomake 쉽게 프로그램 다운스트림 처리 tooknow hello 프로세스 작동 하는 이벤트 허브에 대 한 빈 파일 기록 데이터가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="05bab-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="05bab-135">이 프로세스는 일괄 처리 프로세서에 제공할 수 있는 예측 가능한 주기와 표식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="05bab-136">Event Hubs 캡처 설정</span><span class="sxs-lookup"><span data-stu-id="05bab-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="05bab-137">Hello 이벤트 허브를 만들 때 hello를 사용 하 여 캡처를 구성할 수 있습니다 [Azure 포털](https://portal.azure.com), 또는 Azure 리소스 관리자 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="05bab-138">자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="05bab-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="05bab-139">이벤트 허브 hello Azure 포털을 사용 하 여 캡처를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05bab-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="05bab-140">Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브가 있는 Event Hubs 네임스페이스를 만들고 캡처를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05bab-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="05bab-141">캡처된 hello 파일을 탐색 및 Avro 사용</span><span class="sxs-lookup"><span data-stu-id="05bab-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="05bab-142">이벤트 허브 캡처 hello 구성 된 기간에 지정 된 대로 Avro 형식으로 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="05bab-143">[Azure Storage 탐색기][Azure Storage Explorer]와 같은 도구에서 이러한 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="05bab-144">다운로드할 수 hello 파일을 로컬 toowork에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="05bab-145">Avro 스키마를 따르는 hello 있어야 하는 이벤트 허브 캡처에 의해 생성 된 hello 파일:</span><span class="sxs-lookup"><span data-stu-id="05bab-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="05bab-146">Hello를 사용 하 여 쉽게 tooexplore Avro 파일은 [Avro 도구] [ Avro Tools] Apache에서 jar.</span><span class="sxs-lookup"><span data-stu-id="05bab-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="05bab-147">이 jar 파일에 다운로드 한 후 hello 다음 명령을 실행 하 여 특정 Avro 파일의 hello 스키마를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="05bab-148">이 명령은 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-148">This command returns</span></span>

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

<span data-ttu-id="05bab-149">Avro 도구 tooconvert hello 파일 tooJSON 형식을 사용 하 고 다른 처리를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="05bab-150">tooperform 더 높은 수준의 처리 다운로드 및 Avro 사용자가 선택한 플랫폼에 대 한 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="05bab-151">이 문서 작성 hello 시 구현을 사용할 수 있는 C, c + +, C\#, Java, NodeJS, Perl, PHP, Python 및 Ruby 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="05bab-152">Apache Avro에는 [Java][Java] 및 [Python][Python]에 대한 전체 시작 가이드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="05bab-153">Hello 읽어 [이벤트 허브 캡처 시작](event-hubs-capture-python.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="05bab-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="05bab-154">Event Hubs 캡처의 요금 부과 방식</span><span class="sxs-lookup"><span data-stu-id="05bab-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="05bab-155">이벤트 허브 캡처 유료일 toothroughput 단위 마찬가지로: 시간당 요금으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="05bab-156">hello 충전은 정비례 toohello hello 네임 스페이스에 대해 구입한 처리량 단위 수입니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="05bab-157">처리량 단위를 증가 및 감소 이벤트 허브 캡처 미터 늘린 tooprovide 성능 일치 하는 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="05bab-158">hello 미터 동시에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-158">hello meters occur in tandem.</span></span> <span data-ttu-id="05bab-159">가격 정보는 [Event Hubs 가격 책정](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05bab-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="05bab-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05bab-160">Next steps</span></span>

<span data-ttu-id="05bab-161">이벤트 허브 수집은 hello 가장 쉬운 방법은 tooget 데이터를 Azure로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="05bab-162">Azure Data Lake, Azure Data Factory 및 Azure HDInsight를 통해 규모에 관계없이 선택한 도구 및 플랫폼을 사용하여 선택한 일괄 처리 및 기타 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="05bab-163">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bab-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="05bab-164">이벤트 전송 및 수신 시작</span><span class="sxs-lookup"><span data-stu-id="05bab-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="05bab-165">[Event Hubs를 사용하는 응용 프로그램 예제][sample application that uses Event Hubs] 전체</span><span class="sxs-lookup"><span data-stu-id="05bab-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="05bab-166">[Event Hubs 개요][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="05bab-166">[Event Hubs overview][Event Hubs overview]</span></span>

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
