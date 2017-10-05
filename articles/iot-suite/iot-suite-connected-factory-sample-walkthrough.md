---
title: "연결된 공장 Azure IoT Suite 솔루션 연습 | Microsoft Docs"
description: "공장 및 해당 아키텍처에 연결된 Azure IoT 미리 구성된 솔루션에 대한 설명입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 517e908a744734139ed0aeee314a4f3b9eda86cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="367c9-103">연결된 공장 미리 구성된 솔루션 연습</span><span class="sxs-lookup"><span data-stu-id="367c9-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="367c9-104">IoT Suite 연결된 공장 [미리 구성된 솔루션][lnk-preconfigured-solutions]은 종단 간 산업 솔루션의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-104">The IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="367c9-105">시뮬레이션된 공장 생산 라인에서 OPC UA 서버를 실행하는 시뮬레이션된 산업 장치 및 실제 OPC UA 서버 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="367c9-106">OPC UA에 대한 자세한 내용은 [연결된 팩터리 FAQ](iot-suite-faq-cf.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="367c9-106">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="367c9-107">이러한 장치 및 생산 라인의 운영 KPI 및 OEE를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="367c9-108">OPC UA 서버 시스템과 상호 작용하는 데 클라우드 기반 응용 프로그램을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span></span>
* <span data-ttu-id="367c9-109">고유한 OPC UA 서버 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-109">Enables you to connect your own OPC UA server devices.</span></span>
* <span data-ttu-id="367c9-110">OPC UA 서버 데이터를 검색하고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-110">Enables you to browse and modify the OPC UA server data.</span></span>
* <span data-ttu-id="367c9-111">Azure TSI(Time Series Insights) 서비스와 통합하여 OPC UA 서버에서 데이터의 사용자 지정된 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span></span>

<span data-ttu-id="367c9-112">솔루션을 고유한 구현을 위한 출발점으로 사용하고 사용자의 특정 비즈니스 요구 사항을 충족하도록 [사용자 지정][lnk-customize]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="367c9-113">이 문서는 작동 방식을 이해할 수 있도록 연결된 공장 솔루션의 핵심 요소 중 일부를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-113">This article walks you through some of the key elements of the connected factory solution to enable you to understand how it works.</span></span> <span data-ttu-id="367c9-114">이 정보는 다음 항목을 도울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="367c9-115">솔루션의 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-115">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="367c9-116">솔루션을 사용자 지정하여 고유한 특정 요구 사항을 충족하는 방법을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-116">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="367c9-117">Azure 서비스를 사용하는 고유한 IoT 솔루션을 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="367c9-118">OPC UA에 대한 자세한 내용은 [연결된 팩터리 FAQ](iot-suite-faq-cf.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="367c9-118">For more information, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="367c9-119">논리 아키텍처</span><span class="sxs-lookup"><span data-stu-id="367c9-119">Logical architecture</span></span>

<span data-ttu-id="367c9-120">다음 다이어그램에서는 미리 구성된 솔루션의 논리적 구성 요소를 간략히 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-120">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![연결된 공장 논리 아키텍처][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="367c9-122">통신 패턴</span><span class="sxs-lookup"><span data-stu-id="367c9-122">Communication patterns</span></span>

<span data-ttu-id="367c9-123">이 솔루션은 [OPC UA Pub/Sub 사양](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/)을 사용하여 OPC UA 원격 분석 데이터를 IoT Hub에 JSON 형식으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-123">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span></span> <span data-ttu-id="367c9-124">이 솔루션은 이 목표를 달성하기 위해 [OPC 게시자](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-124">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="367c9-125">또한 이 솔루션은 온-프레미스 OPC UA 서버와의 연결을 설정할 수 있는 OPC UA 클라이언트가 웹 응용 프로그램과 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-125">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="367c9-126">이 클라이언트는 [역방향 프록시](https://wikipedia.org/wiki/Reverse_proxy)를 사용하며 IoT Hub의 도움을 받아 온-프레미스 방화벽에서 포트를 열지 않고도 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-126">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span></span> <span data-ttu-id="367c9-127">이 통신 패턴을 [서비스 지원 통신](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="367c9-128">이 솔루션은 이 목표를 달성하기 위해 [OPC 프록시](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-128">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="367c9-129">시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="367c9-129">Simulation</span></span>

<span data-ttu-id="367c9-130">시뮬레이션된 스테이션과 시뮬레이션된 MES(제조 실행 시스템)는 공장 생산 라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-130">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="367c9-131">시뮬레이션된 장치 및 OPC 게시자 모듈은 OPC Foundation에서 게시한 [OPC UA .NET 표준][lnk-OPC-UA-NET-Standard]을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-131">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span></span>

<span data-ttu-id="367c9-132">OPC 프록시 및 OPC 게시자는 [Azure IoT Edge][lnk-Azure-IoT-Gateway]를 기반으로 하는 모듈로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-132">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="367c9-133">각 시뮬레이션된 생산 라인에는 지정된 게이트웨이가 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="367c9-134">모든 시뮬레이션 구성 요소는 Azure Linux VM에서 호스팅되는 Docker 컨테이너에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="367c9-135">시뮬레이션은 기본적으로 8개의 시뮬레이션된 생산 라인을 실행하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-135">The simulation is configured to run eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="367c9-136">시뮬레이션된 생산 라인</span><span class="sxs-lookup"><span data-stu-id="367c9-136">Simulated production line</span></span>

<span data-ttu-id="367c9-137">생산 라인 제조 파트.</span><span class="sxs-lookup"><span data-stu-id="367c9-137">A production line manufactures parts.</span></span> <span data-ttu-id="367c9-138">어셈블리 스테이션, 테스트 스테이션 및 패키징 스테이션과 같은 다른 스테이션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="367c9-139">시뮬레이션은 OPC UA 노드를 통해 노출되는 데이터를 실행 및 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-139">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span></span> <span data-ttu-id="367c9-140">모든 시뮬레이션된 생산 라인 스테이션은 OPC UA를 통해 MES에 의해 오케스트레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-140">All simulated production line stations are orchestrated by the MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="367c9-141">시뮬레이션된 제조 실행 시스템</span><span class="sxs-lookup"><span data-stu-id="367c9-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="367c9-142">MES는 스테이션 상태 변경 내용을 검색하는 OPC UA를 통해 생산 라인의 각 스테이션을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-142">The MES monitors each station in the production line through OPC UA to detect station status changes.</span></span> <span data-ttu-id="367c9-143">스테이션을 제어하는 OPC UA 메서드를 호출하고 완료될 때까지 한 스테이션에서 다음으로 제품을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-143">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="367c9-144">게이트웨이 OPC 게시자 모듈</span><span class="sxs-lookup"><span data-stu-id="367c9-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="367c9-145">OPC 게시자 모듈은 스테이션 OPC UA 서버에 연결하고 게시될 OPC 노드를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-145">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span></span> <span data-ttu-id="367c9-146">모듈은 노드 데이터를 JSON 형식으로 변환 및 암호화하고 OPC UA Pub/Sub 메시지로 IoT Hub에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-146">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="367c9-147">OPC 게시자 모듈에는 아웃바운드 https 포트(443)만 필요하며 기존 엔터프라이즈 인프라로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-147">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="367c9-148">게이트웨이 OPC 프록시 모듈</span><span class="sxs-lookup"><span data-stu-id="367c9-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="367c9-149">게이트웨이 OPC UA 프록시 모듈은 이진 OPC UA 명령 및 제어 메시지를 터널링하고 아웃바운드 https 포트(443)만을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-149">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="367c9-150">웹 프록시를 포함하여 기존 엔터프라이즈 인프라로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="367c9-151">IoT Hub 장치 메서드를 사용하여 응용 프로그램 계층에서 패킷으로 나누어진 TCP/IP 데이터를 전송하므로 끝점 신뢰, 데이터 암호화 및 SSL/TLS를 사용하여 무결성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-151">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="367c9-152">프록시 자체를 통해 릴레이된 OPC UA 이진 프로토콜은 UA 인증 및 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-152">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="367c9-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="367c9-153">Azure Time Series Insights</span></span>

<span data-ttu-id="367c9-154">게이트웨이 OPC 게시자 모듈은 OPC UA 서버 노드를 구독하여 데이터 값에서 변경을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-154">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span></span> <span data-ttu-id="367c9-155">노드 중 하나에서 데이터 변경이 감지되면 이 모듈은 Azure IoT Hub로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-155">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span></span>

<span data-ttu-id="367c9-156">IoT Hub는 Azure TSI에 이벤트 원본을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-156">IoT Hub provides an event source to Azure TSI.</span></span> <span data-ttu-id="367c9-157">TSI는 메시지에 연결된 타임스탬프에 따라 30일 동안 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-157">TSI stores data for 30 days based on timestamps attached to the messages.</span></span> <span data-ttu-id="367c9-158">이 데이터에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-158">This data includes:</span></span>

* <span data-ttu-id="367c9-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="367c9-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="367c9-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="367c9-160">OPC UA NodeId</span></span>
* <span data-ttu-id="367c9-161">노드 값</span><span class="sxs-lookup"><span data-stu-id="367c9-161">Value of the node</span></span>
* <span data-ttu-id="367c9-162">원본 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="367c9-162">Source timestamp</span></span>
* <span data-ttu-id="367c9-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="367c9-163">OPC UA DisplayName</span></span>

<span data-ttu-id="367c9-164">현재 TSI는 데이터를 유지하려는 기간에 대한 고객의 사용자 지정을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-164">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span></span>

<span data-ttu-id="367c9-165">TSI는 SearchSpan(Time.From, Time.To)을 사용하여 노드 데이터에 대해 쿼리하고 OPC UA ApplicationUri 또는 OPC UA NodeId 또는 OPC UA DisplayName으로 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="367c9-166">OEE 및 KPI 계기 및 시간열 차트에 대한 데이터를 검색하기 위해 데이터는 이벤트, Sum, Avg, Min 및 Max의 수로 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-166">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="367c9-167">시계열은 다른 프로세스를 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-167">The time series are built using a different process.</span></span> <span data-ttu-id="367c9-168">OEE 및 KPI는 스테이션 기본 데이터에서 계산되며 응용 프로그램에서 토폴로지(생산 라인, 공장, 엔터프라이즈)에 대해 버블링됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-168">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span></span>

<span data-ttu-id="367c9-169">또한 OEE 및 KPI 토폴로지에 대한 시계열은 표시된 timespan이 준비될 때마다 앱에서 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-169">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="367c9-170">예를 들어 일 보기는 1시간마다 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-170">For example, the day view is updated every full hour.</span></span>

<span data-ttu-id="367c9-171">노드 데이터의 시계열 보기는 timespan에 대한 집계를 사용하여 TSI에서 직접 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-171">The time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="367c9-172">IoT 허브</span><span class="sxs-lookup"><span data-stu-id="367c9-172">IoT Hub</span></span>
<span data-ttu-id="367c9-173">[IoT Hub][lnk-IoT Hub]는 OPC 게시자 모듈에서 클라우드로 전송된 데이터를 수신하고 Azure TSI 서비스에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-173">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span></span> 

<span data-ttu-id="367c9-174">또한 솔루션에서 IoT Hub는:</span><span class="sxs-lookup"><span data-stu-id="367c9-174">The IoT Hub in the solution also:</span></span>
- <span data-ttu-id="367c9-175">모든 OPC 게시자 모듈 및 모든 OPC 프록시 모듈에 대한 ID를 저장하는 ID 레지스트리를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-175">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="367c9-176">OPC 프록시 모듈의 양방향 통신에 대한 전송 채널로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-176">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="367c9-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="367c9-177">Azure Storage</span></span>
<span data-ttu-id="367c9-178">솔루션은 VM에 대 한 디스크 저장소로 Azure Blob 저장소를 사용하여 배포 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-178">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="367c9-179">웹앱</span><span class="sxs-lookup"><span data-stu-id="367c9-179">Web app</span></span>
<span data-ttu-id="367c9-180">미리 구성된 솔루션의 일부로 배포된 웹앱은 통합된 OPC UA 클라이언트, 경고 처리 및 원격 분석 시각화로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-180">The web app deployed as part of the preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="367c9-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="367c9-181">Next steps</span></span>

<span data-ttu-id="367c9-182">다음 문서를 참조하여 IoT Suite 시작 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="367c9-182">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="367c9-183">[azureiotsuite.com 사이트에 대한 사용 권한][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="367c9-183">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="367c9-184">연결된 팩터리의 미리 구성된 솔루션을 위해 Windows 또는 Linux에 게이트웨이 배포</span><span class="sxs-lookup"><span data-stu-id="367c9-184">Deploy a gateway on Windows or Linux for the connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
