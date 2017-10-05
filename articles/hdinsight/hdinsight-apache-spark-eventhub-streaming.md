---
title: "Azure HDInsight에서 이벤트 허브와 함께 Apache Spark 스트리밍 사용 | Microsoft Docs"
description: "Azure 이벤트 허브에 데이터 스트림을 보내는 방법에 대한 Apache Spark 스트리밍 샘플을 빌드한 다음 scala 응용 프로그램을 사용하여 HDInsight Spark 클러스터에서 해당 이벤트를 수신합니다."
keywords: "apache spark 스트리밍, spark 스트리밍, spark 샘플, apache spark 스트리밍 예제, 이벤트 허브 azure 샘플, spark 샘플"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="18588-104">Apache Spark 스트리밍: HDInsight에서 Spark 클러스터로 Azure Event Hubs의 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="18588-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="18588-105">이 문서에서는 다음 단계를 포함하는 Apache Spark 샘플 스트리밍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="18588-106">독립 실행형 응용 프로그램을 사용하여 Azure 이벤트 허브로 메시지를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="18588-107">두 가지 방법으로 Azure HDInsight의 Spark 클러스터에서 실행 중인 응용 프로그램을 사용하여 실시간으로 Event Hub에서 메시지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="18588-108">스트리밍 분석 파이프라인을 빌드하여 데이터를 다른 저장소 시스템에 유지하거나 즉석에서 데이터의 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18588-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18588-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="18588-109">Prerequisites</span></span>

* <span data-ttu-id="18588-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="18588-110">An Azure subscription.</span></span> <span data-ttu-id="18588-111">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="18588-112">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="18588-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="18588-114">Spark 스트리밍 개념</span><span class="sxs-lookup"><span data-stu-id="18588-114">Spark Streaming concepts</span></span>

<span data-ttu-id="18588-115">Spark 스트리밍에 대한 자세한 내용은 [Apache Spark 스트리밍 개요](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="18588-116">HDInsight는 Azure에서 Spark 클러스터에 동일한 스트리밍 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="18588-117">이 솔루션의 기능은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="18588-117">What does this solution do?</span></span>

<span data-ttu-id="18588-118">이 문서에서 Spark 스트리밍 예제를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="18588-119">이벤트 스트림을 받을 Azure 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="18588-120">이벤트를 생성하고 Azure 이벤트 허브를 푸시하는 로컬 독립 실행형 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="18588-121">이 작업을 수행하는 샘플 응용 프로그램은 [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)에 게시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="18588-122">Azure Event Hub에서 스트리밍 이벤트를 읽는 Spark 클러스터에서 원격으로 스트리밍 응용 프로그램을 실행하고 다양한 데이터 처리/분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="18588-123">Azure 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="18588-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="18588-124">[Azure Portal](https://ms.portal.azure.com)에 로그온하고 화면 왼쪽 위에 있는 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="18588-125">**사물 인터넷**을 클릭한 다음 **Event Hubs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="18588-126">![Spark 스트리밍 예제에 대한 이벤트 허브 만들기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Spark 스트리밍 예제에 대한 이벤트 허브 만들기")</span><span class="sxs-lookup"><span data-stu-id="18588-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="18588-127">**네임스페이스 만들기** 블레이드에서 네임스페이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="18588-128">가격 책정 계층(기본 또는 표준)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="18588-129">또한 리소스를 만들 Azure 구독, 리소스 그룹 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="18588-130">**만들기** 를 클릭하여 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="18588-131">![Spark 스트리밍 예제에 대한 이벤트 허브 이름 제공](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Spark 스트리밍 예제에 대한 이벤트 허브 이름 제공")</span><span class="sxs-lookup"><span data-stu-id="18588-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="18588-132">대기 시간 및 비용을 줄이려면 HDInsight의 Apache Spark 클러스터와 동일한 **위치** 를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="18588-133">Event Hubs 네임스페이스 목록에서 새로 만든 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="18588-134">네임스페이스 블레이드에서 **이벤트 허브**를 클릭하고 **+ 이벤트 허브**를 클릭하여 새 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="18588-135">![Spark 스트리밍 예제에 대한 이벤트 허브 만들기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Spark 스트리밍 예제에 대한 이벤트 허브 만들기")</span><span class="sxs-lookup"><span data-stu-id="18588-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="18588-136">이벤트 허브에 사용할 이름을 입력하고, 파티션 수를 10으로, 메시지 보존을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="18588-137">이 솔루션에서 메시지를 보관하지 않으므로 나머지는 기본 설정으로 둔 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="18588-138">![Spark 스트리밍 예제에 대한 이벤트 허브 세부 정보 제공](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Spark 스트리밍 예제에 대한 이벤트 허브 세부 정보 제공")</span><span class="sxs-lookup"><span data-stu-id="18588-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="18588-139">새로 만든 이벤트 허브가 이벤트 허브 블레이드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="18588-140">![Spark 스트리밍 예제에 대한 이벤트 허브 보기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Spark 스트리밍 예제에 대한 이벤트 허브 보기")</span><span class="sxs-lookup"><span data-stu-id="18588-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="18588-141">네임스페이스 블레이드(특정 Event Hub 블레이드가 아님)로 돌아와서 **공유 액세스 정책**을 클릭한 다음 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="18588-142">![Spark 스트리밍 예제에 대한 이벤트 허브 정책 설정](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Spark 스트리밍 예제에 대한 이벤트 허브 정책 설정")</span><span class="sxs-lookup"><span data-stu-id="18588-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="18588-143">복사 단추를 클릭하여 **RootManageSharedAccessKey** 기본 키 및 연결 문자열을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="18588-144">이러한 항목은 자습서에서 나중에 사용할 수 있도록 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="18588-145">![Spark 스트리밍 예제에 대한 이벤트 허브 정책 키 보기](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "Spark 스트리밍 예제에 대한 이벤트 허브 정책 키 보기")</span><span class="sxs-lookup"><span data-stu-id="18588-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="18588-146">샘플 Scala 응용 프로그램을 사용하여 Azure 이벤트 허브에 메시지 전송</span><span class="sxs-lookup"><span data-stu-id="18588-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="18588-147">이 섹션에서는 이벤트 스트림을 만들고 이전에 만든 Azure 이벤트 허브에 전송하는 독립 실행형 로컬 Scala 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="18588-148">이 응용 프로그램은 [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer)의 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="18588-149">여기의 단계는 이 GitHub 리포지토리를 이미 분기했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="18588-150">이 응용 프로그램을 실행하는 컴퓨터에 다음 항목이 설치되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="18588-151">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="18588-151">Oracle Java Development kit.</span></span> <span data-ttu-id="18588-152">[여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="18588-153">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="18588-153">Apache Maven.</span></span> <span data-ttu-id="18588-154">[여기](https://maven.apache.org/download.cgi)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="18588-155">Maven 설치 지침은 [여기](https://maven.apache.org/install.html)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="18588-156">명령 프롬프트를 열고 샘플 Scala 응용 프로그램의 GitHub 리포지토리를 복제한 위치로 이동하고 다음 명령을 실행하여 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="18588-157">응용 프로그램의 출력 jar인 **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**은 **/target** 디렉터리 아래에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="18588-158">이 문서의 뒷부분에 나오는 이 jar 파일을 사용하여 전체 솔루션을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="18588-159">이벤트 허브에서 Spark 클러스터로 메시지를 수신하는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="18588-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="18588-160">두 가지 방법으로 Spark 스트리밍 및 Azure Event Hubs, 수신기 기반 연결 및 Direct-DStream 기반 연결에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="18588-161">Direct-DStream 기반은 2017년 1월에 도입된 2.0.3 릴리스에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="18588-162">이 기능은 성능이 우수하고 리소스 효율적이기 때문에 원래 수신기 기반 연결을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="18588-163">자세한 내용은 [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs)에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="18588-164">Direct DStream은 Spark 2.0+만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="18588-165">spark-eventhubs 커넥터에 종속된 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="18588-166">GitHub의 Spark-EventHubs 준비 버전도 발표할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="18588-167">Spark-EventHubs 준비 버전을 사용하려면 첫 번째 단계로 pom.xml에 다음 항목을 추가하여 GitHub를 소스 리포지토리로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="18588-168">그런 다음 프로젝트에 다음 종속성을 추가하여 이전에 릴리스된 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="18588-169">Maven 종속성</span><span class="sxs-lookup"><span data-stu-id="18588-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="18588-170">SBT 종속성</span><span class="sxs-lookup"><span data-stu-id="18588-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="18588-171">Direct DStream 연결</span><span class="sxs-lookup"><span data-stu-id="18588-171">Direct DStream Connection</span></span>

<span data-ttu-id="18588-172">[http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar)에서 Direct DStream을 사용하는 예제를 포함하는 미리 작성된 jar 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="18588-173">jar 파일은 [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream)에서 소스 코드를 사용할 수 있는 세 가지 예제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="18588-174">[WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala)를 예로 듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="18588-175">위의 예에서 `eventhubParameters`는 단일 EventHubs 인스턴스에 지정된 매개 변수로서 `createDirectStreams` API에 전달되어야 합니다. 여기에서 Event Hubs 네임스페이스에 매핑된 Direct DStream 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="18588-176">Direct DStream 개체에 대해 Spark 스트리밍 API Framework에서 제공하는 모든 DStream API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="18588-177">이 예제에서는 최근 3번의 마이크로 배치 간격 내에서 각 단어의 빈도를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="18588-178">수신기 기반 연결</span><span class="sxs-lookup"><span data-stu-id="18588-178">Receiver-based Connection</span></span>

<span data-ttu-id="18588-179">이벤트를 받고 이를 다른 대상으로 라우팅하는 Scala로 작성된 Spark 스트리밍 예제 응용 프로그램은 [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="18588-180">다음 단계를 수행하여 이벤트 허브 구성에 대한 응용 프로그램을 업데이트하고 출력 jar을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="18588-181">IntelliJ IDEA를 시작하고 시작 화면에서 **버전 제어에서 확인**을 선택한 다음 **Git**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="18588-182">![Apache Spark 스트리밍 예제 - Git에서 원본 가져오기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark 스트리밍 예제 - Git에서 원본 가져오기")</span><span class="sxs-lookup"><span data-stu-id="18588-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="18588-183">**리포지토리 복제** 대화 상자에서 복제할 Git 리포지토리의 URL을 제공하고 복제할 디렉터리를 지정한 다음 **복제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="18588-184">![Apache Spark 스트리밍 예제 - Git에서 복제](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark 스트리밍 예제 - Git에서 복제")</span><span class="sxs-lookup"><span data-stu-id="18588-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="18588-185">프로젝트가 완전히 복제될 때까지 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="18588-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="18588-186">**Alt + 1** 키를 눌러 **프로젝트 보기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18588-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="18588-187">다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="18588-188">![Apache Spark 스트리밍 예제 - 프로젝트 보기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark 스트리밍 예제 - 프로젝트 보기")</span><span class="sxs-lookup"><span data-stu-id="18588-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="18588-189">Java8로 컴파일된 응용 프로그램 코드가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="18588-190">이를 확인하려면 **파일**, **프로젝트 구조**를 차례로 클릭한 다음 **프로젝트** 탭에서 프로젝트 언어 수준이 **8 람다, 형식 주석 등**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="18588-191">![Apache Spark 스트리밍 예제 - 컴파일러 설정](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark 스트리밍 예제 - 컴파일러 설정")</span><span class="sxs-lookup"><span data-stu-id="18588-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="18588-192">**pom.xml** 을 열고 Spark 버전이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="18588-193">`<properties>` 노드 아래에서 다음 코드 조각을 찾고 Spark 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="18588-194">응용 프로그램에는 **JDBC 드라이버 jar**이라고도 하는 종속성 jar이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="18588-195">이벤트 허브에서 받은 메시지를 Azure SQL 데이터베이스에 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="18588-196">이 jar(v4.1 이상)을 [여기](https://msdn.microsoft.com/sqlserver/aa937724.aspx)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="18588-197">프로젝트 라이브러리에 이러한 jar에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="18588-198">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="18588-199">응용 프로그램이 열려 있는 IntelliJ IDEA 창에서 **파일**, **프로젝트 구조**, **라이브러리**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="18588-200">추가 아이콘(![추가 아이콘](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png))을 클릭하고 **Java**를 클릭한 다음 JDBC 드라이버 jar를 다운로드한 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="18588-201">지시에 따라 프로젝트 라이브러리에 jar 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="18588-202">![누락된 종속성 추가](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "누락된 종속성 jar 추가")</span><span class="sxs-lookup"><span data-stu-id="18588-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="18588-203">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-203">Click **Apply**.</span></span>

7. <span data-ttu-id="18588-204">출력 jar 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-204">Create the output jar file.</span></span> <span data-ttu-id="18588-205">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="18588-206">**프로젝트 구조** 대화 상자에서 **아티팩트**를 클릭한 다음 +(더하기) 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="18588-207">팝업 대화 상자에서 **JAR**, **종속성이 있는 모듈에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="18588-208">![Apache Spark 스트리밍 예제 - JAR 만들기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark 스트리밍 예제 - JAR 만들기")</span><span class="sxs-lookup"><span data-stu-id="18588-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="18588-209">**모듈에서 JAR 만들기** 대화 상자에서 **주 클래스**에 대한 ![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)(줄임표)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="18588-210">**주 클래스 선택** 대화 상자에서 사용 가능한 클래스를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="18588-211">![Apache Spark 스트리밍 예제 - jar에 대한 클래스 선택](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark 스트리밍 예제 - jar에 대한 클래스 선택")</span><span class="sxs-lookup"><span data-stu-id="18588-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="18588-212">**모듈에서 JAR 만들** 대화 상자에서 **대상 JAR에 추출** 옵션이 선택되었는지 확인한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="18588-213">이렇게 하면 모든 종속성이 있는 단일 JAR이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="18588-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="18588-214">![Apache Spark 스트리밍 예제 - 모듈에서 jar 만들기](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark 스트리밍 예제 - 모듈에서 jar 만들기")</span><span class="sxs-lookup"><span data-stu-id="18588-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="18588-215">**출력 레이아웃** 탭에는 Maven 프로젝트의 일부분으로 포함된 jar이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="18588-216">직접 종속성이 없는 Scala 응용 프로그램을 선택하고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="18588-217">여기에서 만든 응용 프로그램의 경우 마지막을 제외한 모두를 제거할 수 있습니다(**spark-streaming-data-persistence-examples 컴파일 출력**).</span><span class="sxs-lookup"><span data-stu-id="18588-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="18588-218">삭제할 jar을 선택한 다음 ![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)(**삭제**) 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="18588-219">![Apache Spark 스트리밍 예제 - 추출된 jar 삭제](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark 스트리밍 예제 - 추출된 jar 삭제")</span><span class="sxs-lookup"><span data-stu-id="18588-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="18588-220">프로젝트를 작성하거나 업데이트할 때마다 jar이 생성되는지 확인하는 **Build on make** 확인란이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="18588-221">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="18588-222">이전에 프로젝트 라이브러리에 추가한 SQL JDBC jar가 **출력 레이아웃** 탭의 **사용 가능한 요소** 상자의 오른쪽 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="18588-223">**출력 레이아웃** 탭에 이를 추가해야 합니다. jar 파일을 마우스 오른쪽 단추로 클릭한 다음 **출력 루트로 추출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="18588-224">![Apache Spark 스트리밍 예제 - 종속성 jar 추출](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark 스트리밍 예제 - 종속성 jar 추출")</span><span class="sxs-lookup"><span data-stu-id="18588-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="18588-225">**출력 레이아웃** 탭은 이제 다음과 같아집니다.</span><span class="sxs-lookup"><span data-stu-id="18588-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="18588-226">![Apache Spark 스트리밍 예제 - 최종 출력 탭](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark 스트리밍 예제 - 최종 출력 탭")</span><span class="sxs-lookup"><span data-stu-id="18588-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="18588-227">**프로젝트 구조** 대화 상자에서 **적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="18588-228">메뉴 모음에서 **빌드**를 클릭한 다음 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="18588-229">**빌드 아티팩트** 를 클릭하여 jar을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="18588-230">**\classes\artifacts** 아래에 출력 jar이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="18588-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="18588-231">![Apache Spark 스트리밍 예제 - 출력 JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark 스트리밍 예제 - 출력 JAR")</span><span class="sxs-lookup"><span data-stu-id="18588-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="18588-232">Livy를 사용하여 Spark 클러스터에서 원격으로 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="18588-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="18588-233">이 문서에서는 Livy를 사용하여 Spark 클러스터에서 Apache Spark 스트리밍 응용 프로그램을 원격으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="18588-234">HDInsight Spark 클러스터와 함께 Livy를 사용하는 방법에 대한 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터에 원격으로 작업 제출](hdinsight-apache-spark-livy-rest-interface.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="18588-235">Spark 스트리밍 응용 프로그램 실행을 시작하기 전에 몇 가지 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="18588-236">로컬 독립 실행형 응용 프로그램을 시작하여 이벤트를 생성하고 이벤트 허브로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="18588-237">이렇게 하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="18588-238">스트리밍 jar(**spark-streaming-data-persistence-examples.jar**)을 클러스터와 연결된 Azure Blob Storage에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="18588-239">이렇게 하면 jar이 Livy에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="18588-240">[**AzCopy**](../storage/common/storage-use-azcopy.md) 명령줄 유틸리티를 사용하면 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="18588-241">데이터를 업로드하는 데 사용할 수 있는 다른 클라이언트도 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="18588-242">[HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="18588-243">이러한 응용 프로그램을 실행 중인 컴퓨터에 CURL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="18588-244">Livy 끝점을 호출하는 CURL을 사용하여 작업을 원격으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="18588-245">텍스트로 Azure Storage Blob에 이벤트를 수신하는 Spark 스트리밍 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="18588-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="18588-246">명령 프롬프트를 열고 CURL을 설치한 디렉터리로 이동하고 다음 명령을 실행합니다(사용자 이름/암호 및 클러스터 이름 바꾸기).</span><span class="sxs-lookup"><span data-stu-id="18588-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="18588-247">파일 **inputBlob.txt**에서 매개 변수는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="18588-248">입력 파일에서 매개 변수가 무엇인지 이해하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="18588-249">**파일**은 클러스터와 연결된 Azure 저장소 계정의 응용 프로그램 jar 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="18588-250">**className**은 jar의 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="18588-251">**args**는 클래스에 필요한 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="18588-252">**numExecutors**는 스트리밍 응용 프로그램을 실행하기 위해 Spark에서 사용되는 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="18588-253">이는 항상 이벤트 허브 파티션 수의 두 배 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="18588-254">**executorMemory**, **executorCores**, **driverMemory**는 스트리밍 응용 프로그램에 필요한 리소스를 할당하는 데 사용되는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="18588-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="18588-255">매개 변수로 사용되는 출력 폴더(EventCheckpoint, EventCount/EventCount10)를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="18588-256">스트리밍 응용 프로그램은 이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="18588-257">명령을 실행하면 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="18588-258">출력의 마지막 줄에서 배치 ID를 기록해 둡니다(이 예에서 '1').</span><span class="sxs-lookup"><span data-stu-id="18588-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="18588-259">응용 프로그램이 성공적으로 실행되는지 확인하려면 클러스터와 연결된 Azure 저장소 계정을 확인하고 거기서 만든 **/EventCount/EventCount10** 폴더가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="18588-260">이 폴더는 매개 변수 **batch-interval-in-seconds**에 지정된 시간 간격 내에 처리되는 이벤트 수를 캡처하는 Blob을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="18588-261">Spark 스트리밍 응용 프로그램은 종료할 때까지 실행을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="18588-262">이렇게 하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="18588-263">JSON으로 Azure 저장소 Blob에 이벤트를 수신하는 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="18588-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="18588-264">명령 프롬프트를 열고 CURL을 설치한 디렉터리로 이동하고 다음 명령을 실행합니다(사용자 이름/암호 및 클러스터 이름 바꾸기).</span><span class="sxs-lookup"><span data-stu-id="18588-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="18588-265">파일 **inputJSON.txt** 에서 매개 변수는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="18588-266">매개 변수는 이전 단계에서 텍스트 출력에 지정한 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="18588-267">마찬가지로 매개 변수로 사용되는 출력 폴더(EventCheckpoint, EventCount/EventCount10)를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="18588-268">스트리밍 응용 프로그램은 이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="18588-269">명령을 실행한 후 클러스터와 연결된 Azure 저장소 계정을 확인하고 거기서 만든 **/EventStore10** 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="18588-270">**part-** 접두사가 있는 파일을 열고 JSON 형식으로 처리된 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="18588-271">Hive 테이블에 이벤트를 수신하는 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="18588-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="18588-272">Hive 테이블에 이벤트를 스트리밍하는 Spark 스트리밍 응용 프로그램을 실행하려면 몇 가지 추가 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="18588-273">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-273">These are:</span></span>

* <span data-ttu-id="18588-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="18588-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="18588-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="18588-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="18588-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="18588-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="18588-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="18588-277">hive-site.xml</span></span>

<span data-ttu-id="18588-278">**.jar** 파일은 `/usr/hdp/current/spark-client/lib`의 HDInsight Spark 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="18588-279">**hive-site.xml**은 `/usr/hdp/current/spark-client/conf`에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="18588-280">[WinScp](http://winscp.net/eng/download.php) 를 사용하여 해당 파일을 클러스터에서 로컬 컴퓨터에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="18588-281">그런 다음 도구를 사용하여 클러스터와 연결된 저장소 계정에 이러한 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="18588-282">저장소 계정에 파일을 업로드하는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="18588-283">Azure 저장소 계정에 파일을 복사한 후 명령 프롬프트를 열고 CURL을 설치한 디렉터리로 이동하고 다음 명령을 실행합니다(사용자 이름/암호 및 클러스터 이름 바꾸기).</span><span class="sxs-lookup"><span data-stu-id="18588-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="18588-284">파일 **inputHive.txt** 에서 매개 변수는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="18588-285">매개 변수는 이전 단계에서 텍스트 출력에 지정한 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="18588-286">마찬가지로 매개 변수로 사용되는 출력 폴더(EventCheckpoint, EventCount/EventCount10) 또는 출력 Hive 테이블(EventHiveTable10)을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="18588-287">스트리밍 응용 프로그램은 이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-287">The streaming application creates them for you.</span></span> <span data-ttu-id="18588-288">**jars** 및 **files** 옵션은 저장소 계정에 복사한 .jar 파일 및 hive-site.xml에 대한 경로를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="18588-289">hive 테이블이 성공적으로 만들어졌는지 확인하려면 클러스터로 SSH하고 Hive 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="18588-290">자세한 내용은 [SSH를 사용하는 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-ssh.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="18588-291">SSH를 사용하여 연결된 후 다음 명령을 실행하여 Hive 테이블, **EventHiveTable10**이 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="18588-292">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="18588-293">또한 SELECT 쿼리를 실행하여 테이블의 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="18588-294">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-294">You should see an output like the following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="18588-295">Azure SQL 데이터베이스 테이블에 이벤트를 수신하는 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="18588-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="18588-296">이 단계를 실행하기 전에 Azure SQL 데이터베이스를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="18588-297">자세한 내용은 [몇 분 만에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="18588-298">이 섹션을 완료하려면 매개 변수로 데이터베이스 이름, 데이터베이스 서버 이름 및 데이터베이스 관리자 자격 증명에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="18588-299">그러나 데이터베이스 테이블을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-299">You do not need to create the database table though.</span></span> <span data-ttu-id="18588-300">Spark 스트리밍 응용 프로그램은 이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18588-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="18588-301">명령 프롬프트를 열고 CURL을 설치한 디렉터리로 이동하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="18588-302">파일 **inputSQL.txt** 에서 매개 변수는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="18588-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="18588-303">응용 프로그램이 성공적으로 실행되는지 확인하려면 SQL Server Management Studio를 사용하여 Azure SQL 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="18588-304">작업을 수행하는 방법에 대한 자세한 내용은 [SQL Server Management Studio를 사용하여 SQL 데이터베이스에 연결](../sql-database/sql-database-connect-query-ssms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18588-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="18588-305">데이터베이스에 연결한 후 스트리밍 응용 프로그램에서 만든 **EventContent** 테이블로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="18588-306">빠른 쿼리를 실행하여 테이블에서 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18588-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="18588-307">다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="18588-308">다음과 비슷한 결과가 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18588-308">You should see output similar to the following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="18588-309"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="18588-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="18588-310">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="18588-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="18588-311">수신기 기반 연결 및 Direct DStream 설계</span><span class="sxs-lookup"><span data-stu-id="18588-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="18588-312">시나리오</span><span class="sxs-lookup"><span data-stu-id="18588-312">Scenarios</span></span>
* [<span data-ttu-id="18588-313">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="18588-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="18588-314">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="18588-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="18588-315">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="18588-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="18588-316">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="18588-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="18588-317">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="18588-317">Create and run applications</span></span>
* [<span data-ttu-id="18588-318">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="18588-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="18588-319">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="18588-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="18588-320">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="18588-320">Tools and extensions</span></span>
* [<span data-ttu-id="18588-321">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="18588-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="18588-322">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="18588-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="18588-323">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="18588-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="18588-324">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="18588-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="18588-325">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="18588-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="18588-326">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="18588-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="18588-327">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="18588-327">Manage resources</span></span>
* [<span data-ttu-id="18588-328">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="18588-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="18588-329">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="18588-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
