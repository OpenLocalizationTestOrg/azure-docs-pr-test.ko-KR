---
title: "분석 플랫폼: Apache Storm 비교 tooStream 분석 | Microsoft Docs"
description: "Apache Storm 비교 tooStream 분석을 사용 하 여 클라우드 분석 플랫폼을 선택 하는 지침을 알아봅니다. 기능 및 차이점을 이해하세요."
keywords: "분석 플랫폼, 클라우드 분석 플랫폼, storm 비교"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="f63ff-105">스트리밍 분석 플랫폼 선택: Apache Storm 및 Azure Stream Analytics 비교</span><span class="sxs-lookup"><span data-stu-id="f63ff-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="f63ff-106">Azure는 스트리밍 데이터 분석을 위해 [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) 및 [Azure HDInsight의 Apache Storm](https://azure.microsoft.com/services/hdinsight/apache-storm/)과 같은 여러 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="f63ff-107">분석 플랫폼은 모두 PaaS 솔루션의 hello 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="f63ff-108">하지만 hello 플랫폼도 구성 하 고 이러한 컴퓨터를 관리 하는 방법을 에서처럼의 기능에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="f63ff-109">이 문서에서는 Apache Storm와 클라우드 분석 플랫폼으로 서 Azure 스트림 분석 중에서 선택할 기능 toohelp-나란히 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="f63ff-110">일반 기능</span><span class="sxs-lookup"><span data-stu-id="f63ff-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="f63ff-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="f63ff-113">
                    <strong>HDInsight의 Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-114">
                    <strong>오픈 소스 여부</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-115">아니요.</span><span class="sxs-lookup"><span data-stu-id="f63ff-115">No.</span></span> <span data-ttu-id="f63ff-116">Azure Stream Analytics은 Microsoft 등록 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-117">예.</span><span class="sxs-lookup"><span data-stu-id="f63ff-117">Yes.</span></span> <span data-ttu-id="f63ff-118">Apache Storm은 Apache 라이선스가 허가된 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-119">
                    <strong>Microsoft 지원 여부</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-120">예</span><span class="sxs-lookup"><span data-stu-id="f63ff-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-121">예</span><span class="sxs-lookup"><span data-stu-id="f63ff-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-122">
                    <strong>하드웨어 요구 사항</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-123">없음.</span><span class="sxs-lookup"><span data-stu-id="f63ff-123">None.</span></span> <span data-ttu-id="f63ff-124">Azure Stream Analytics은  인스턴스 Azure 서비스 입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-125">없음.</span><span class="sxs-lookup"><span data-stu-id="f63ff-125">None.</span></span> <span data-ttu-id="f63ff-126">Apache Storm은 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-127">
                    <strong>최상위 단위</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-128">사용자가 스트리밍 작업을 배포 및 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-129">사용자는 다중 Storm 작업과 다른 워크로드(배치 포함)를 호스트할 수 있는 전체 클러스터를 배포하고 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-130">
                    <strong>가격 책정</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-131">처리 된 데이터의 볼륨에 의해 가격이 책정 hello 스트리밍 단위 수가 필요한 시간당 작업 hello 있지만 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="f63ff-132">자세한 내용은 <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics 가격</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f63ff-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-133">hello 단위 구입 클러스터 기반 이며 hello 클러스터가 실행 중인지, 배포 하는 작업의 독립적인 hello 시간에 따라 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="f63ff-134">자세한 내용은 <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight 가격</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f63ff-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="f63ff-135">작성</span><span class="sxs-lookup"><span data-stu-id="f63ff-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="f63ff-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="f63ff-138">
                    <strong>HDInsight의 Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-139">
                    <strong>기능: SQL DSL 여부</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-140">예.</span><span class="sxs-lookup"><span data-stu-id="f63ff-140">Yes.</span></span> <span data-ttu-id="f63ff-141">Stream Analytics는 변환을 만들기 위해 SQL 유사 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-142">아니요.</span><span class="sxs-lookup"><span data-stu-id="f63ff-142">No.</span></span> <span data-ttu-id="f63ff-143">사용자는 Java 또는 C#으로 코드를 작성하거나 Trident API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-144">
                    <strong>기능: 임시 연산자 여부</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-145">기간 이동 집계 및 temporal 조인이 기본적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-146">임시 연산자는 hello 사용자에 의해 구현 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-147">
                    <strong>개발 환경</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-148">사용자 만들 수, 디버깅 및 라이브 스트림을에서 파생 된 샘플 데이터를 사용 하 여 hello Azure 포털을 통해 작업을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-149">.NET을 사용하는 사용자는 Visual Studio를 통해 개발, 디버그 및 모니터할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="f63ff-150">Java 또는 기타 언어를 사용 하 여 사용자가 선택한 IDE hello를 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-151">
                    <strong>디버깅 지원</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-152">기본 작업 상태 및 작업 로그는 사용할 수 있는 toohelp 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="f63ff-153">스트림 분석 현재 수는 없습니다 사용자 지정 콘텐츠 또는 콘텐츠 hello 로그 (즉, 자세한 정보 표시 모드)에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-154">자세한 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-154">Detailed logs are available.</span></span> <span data-ttu-id="f63ff-155">사용자가 로그 toohello 클러스터를 로그인 하 고 hello 로그에 직접 액세스 하거나 Visual Studio에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-156">
                    <strong>사용자 지정 코드를 사용하여 확장 가능 여부</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-157">JavaScript UDF에서 부분적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="f63ff-158">자세한 내용은 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF 통합</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f63ff-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-159">예.</span><span class="sxs-lookup"><span data-stu-id="f63ff-159">Yes.</span></span> <span data-ttu-id="f63ff-160">사용자는 C#, Java 또는 Storm에서 지원되는 다른 언어로 사용자 지정 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="f63ff-161">데이터 원본(입력) 및 출력</span><span class="sxs-lookup"><span data-stu-id="f63ff-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="f63ff-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="f63ff-164">
                    <strong>HDInsight의 Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-165">
                 <strong>입력 데이터 원본</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="f63ff-166">Azure Event Hubs 및 Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f63ff-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-167">커넥터는 Azure Event Hubs, Azure Service Bus, Kafka 등에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="f63ff-168">사용자는 사용자 지정 코드를 사용하여 추가 커넥터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-169">
                    <strong>입력 데이터 형식</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="f63ff-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-171">사용자가 사용자 지정 코드를 사용하여 모든 형식을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-172">
                    <strong>출력</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-173">스트리밍 작업은 여러 출력을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="f63ff-174">지원되는 출력은 Azure Event Hubs, Azure Blob Storage, Azure Table Storage, Azure SQL DB 및 Power BI입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-175">Storm에서는 토폴로지의 많은 출력을 지원하여 각 출력에는 다운스트림 처리에 대한 사용자 지정 논리가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="f63ff-176">Storm은 Power BI, Azure Event Hubs, Azure Blob Storage, Azure Cosmos DB, SQL 및 HBase에 대한 커넥터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="f63ff-177">사용자는 사용자 지정 코드를 사용하여 추가 커넥터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-178">
                    <strong>데이터 인코딩 형식</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-179">데이터는 UTF-8을 사용하여 형식이 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-180">사용자가 사용자 지정 코드를 사용하여 모든 데이터 인코딩 형식을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="f63ff-181">관리 및 운영</span><span class="sxs-lookup"><span data-stu-id="f63ff-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="f63ff-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="f63ff-184">
                    <strong>HDInsight의 Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-185">
                    <strong>작업 배포 모델</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-186">Azure Portal, PowerShell 및 REST API.</span><span class="sxs-lookup"><span data-stu-id="f63ff-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-187">Azure Portal, PowerShell, Visual Studio 및 REST API.</span><span class="sxs-lookup"><span data-stu-id="f63ff-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-188">
                    <strong>모니터링(통계, 카운터 등)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-189">모니터링은 Azure Portal 및 REST API를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="f63ff-190">사용자는 Azure 경고를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-191">모니터링 스톰 UI hello 및 REST Api를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-192">
                    <strong>확장성</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-193">확장성은 hello 스트리밍 단위 수가 (SUs) 각 작업에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="f63ff-194">최대 50 명의 단위와 m B/초를 too1를 처리 하는 각 스트리밍 단위 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="f63ff-195">자세한 내용은 참조 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">배율 tooincrease 처리량</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-196">확장성은 hello hello HDInsight Storm 클러스터의에서 노드 수가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="f63ff-197">hello 상위 노드의 hello 수 제한은 15 hello 사용자의 Azure 할당량에 의해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-198">
                    <strong>데이터 처리 제한</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-199">사용자가 데이터 처리 늘리거나 증가 또는 감소 hello 개수 스트리밍 단위를 1 g B/초의 상한값을 적용 하 여 비용을 최적화 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-200">사용자가 클러스터 크기를 확장 또는 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-201">
                    <strong>중지/다시 시작</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-202">중지한 후 중지된 마지막 위치에서 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-203">중지한 후 워터마크에 따라 중지된 마지막 위치에서 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-204">
                    <strong>서비스 및 프레임워크 업데이트</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-205">가동 중지 시간 없이 자동 패치</span><span class="sxs-lookup"><span data-stu-id="f63ff-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-206">가동 중지 시간 없이 자동 패치</span><span class="sxs-lookup"><span data-stu-id="f63ff-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-207">
                    <strong>보장된 SLA와 고가용 서비스를 통한 비즈니스 연속성</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="f63ff-208">SLA 가동 시간 99.9%</span><span class="sxs-lookup"><span data-stu-id="f63ff-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="f63ff-209">오류에서 자동 복구</span><span class="sxs-lookup"><span data-stu-id="f63ff-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="f63ff-210">temporal 상태 저장 연산자의 기본 제공 복구</span><span class="sxs-lookup"><span data-stu-id="f63ff-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-211">Hello Storm 클러스터의 99.9% 가동률의 SLA를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="f63ff-212">Apache Storm는 내결함성이 있는 스트리밍 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="f63ff-213">그러나는 스트리밍 작업이 실행 되는 중단 없이 hello 사용자의 책임 tooensure 되기 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="f63ff-214">고급 기능</span><span class="sxs-lookup"><span data-stu-id="f63ff-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="f63ff-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="f63ff-217">
                    <strong>HDInsight의 Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-218">
                    <strong>지연 도착 및 순서가 벗어난 이벤트 처리</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-219">기본 제공 구성 가능 정책으로 이벤트 순서 조정, 이벤트 드롭 또는 이벤트 시간 조정이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-220">사용자가 논리 toohandle이이 시나리오를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-221">
                    <strong>참조 데이터</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-222">참조 데이터를 최대 100MB의 메모리 내 캐시가 있는 Azure Blob Storage에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="f63ff-223">참조 데이터는 hello 서비스에서 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-224">데이터 크기에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-224">No limits on data size.</span></span> <span data-ttu-id="f63ff-225">커넥터를 HBase, Azure Cosmos DB, SQL Server 및 Azure에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="f63ff-226">사용자는 사용자 지정 코드를 사용하여 추가 커넥터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="f63ff-227">참조 데이터는 사용자 지정 코드를 사용하여 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="f63ff-228">
                    <strong>Machine Learning과 통합</strong>
                </span><span class="sxs-lookup"><span data-stu-id="f63ff-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="f63ff-229">게시된 Azure Machine Learning 모델을 작업 생성 중에 함수로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="f63ff-230">자세한 내용은 <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Machine Learning 함수에 대한 크기 조정</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f63ff-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="f63ff-231">Storm Bolt를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f63ff-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
