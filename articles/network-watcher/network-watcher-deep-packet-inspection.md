---
title: "Azure 네트워크 감시자도 aaaPacket 검사 | Microsoft Docs"
description: "이 문서에서 설명 하는 VM에서 toouse 네트워크 감시자 tooperform 심층 패킷 검사 수집 하는 방법"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="56731-103">Azure Network Watcher로 패킷 검사</span><span class="sxs-lookup"><span data-stu-id="56731-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="56731-104">네트워크 감시자의 hello 패킷 캡처 기능을 사용 하 여 시작 하 고 hello 포털, PowerShell, CLI 및 hello SDK 통해 프로그래밍 방식으로 Azure Vm 및 REST API에 캡처 세션을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="56731-105">패킷 캡처를 쉽게 사용 가능한 형식에 대 한 hello 정보를 제공 하 여 패킷 수준 데이터 해야 하는 tooaddress 시나리오 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="56731-106">무료로 사용할 수 있는 도구 tooinspect hello 데이터를 활용 하 tooand Vm에서 전달 되는 통신을 검사 하 고 네트워크 트래픽에 대 한 이해력 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="56731-107">패킷 캡처 데이터를 사용하는 예로는, 네트워크 또는 응용 프로그램 문제 조사, 네트워크 악용 및 침입 시도 감지 또는 규정 준수 유지 관리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="56731-108">이 문서에서는 어떻게 tooopen 패킷 캡처 파일에서 제공 네트워크 감시자는 인기 있는 오픈 소스 도구를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56731-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="56731-109">또한 toocalculate 연결 대기 시간, 비정상적인 트래픽을 식별 하 고 네트워킹 통계를 검사 하는 방법을 보여 주는 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56731-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="56731-110">Before you begin</span></span>

<span data-ttu-id="56731-111">이 문서에서는 이전에 실행했던 패킷 캡처에 대해 미리 구성된 몇 가지 시나리오를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="56731-112">이러한 시나리오는 패킷 캡처를 검토하여 액세스할 수 있는 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56731-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="56731-113">이 시나리오에서는 사용 [WireShark](https://www.wireshark.org/) tooinspect hello 패킷 캡처.</span><span class="sxs-lookup"><span data-stu-id="56731-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="56731-114">이 시나리오에서는 가상 컴퓨터에서 패킷 캡처를 이미 실행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="56731-115">toolearn toocreate 패킷 캡처를 방문 하는 방법을 [관리 패킷 캡처를 hello 포털](network-watcher-packet-capture-manage-portal.md) 방문 하 여 rest 또는 [패킷 관리 REST api 캡처](network-watcher-packet-capture-manage-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="56731-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="56731-116">Scenario</span></span>

<span data-ttu-id="56731-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-117">In this scenario, you:</span></span>

* <span data-ttu-id="56731-118">패킷 캡처 검토</span><span class="sxs-lookup"><span data-stu-id="56731-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="56731-119">네트워크 대기 시간 계산</span><span class="sxs-lookup"><span data-stu-id="56731-119">Calculate network latency</span></span>

<span data-ttu-id="56731-120">이 시나리오에서는 tooview 초기 왕복 시간 RTT ()는 두 개의 끝점 사이 발생 하는 프로토콜 TCP (Transmission Control) 대화의 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56731-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="56731-121">TCP 연결 되 면 hello hello 연결에서 전송 되는 처음 3 개의 패킷을 따라 흔히 패턴 tooas hello 3 방향 핸드셰이크 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="56731-122">이 핸드셰이크, hello 클라이언트에서 초기 요청 및 hello 서버 로부터 응답에 전송 되는 hello 처음 두 개의 패킷의 검사 하 여이 연결을 설정할 때 hello 대기 시간이 계산 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="56731-123">이 대기는 참조 된 tooas hello 왕복 시간 (RTT)입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="56731-124">Hello TCP 프로토콜 및 3 방향 핸드셰이크 hello에 대 한 자세한 내용은 다음 리소스 toohello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="56731-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="56731-125">https://support.microsoft.com/ko-kr/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="56731-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="56731-126">1단계</span><span class="sxs-lookup"><span data-stu-id="56731-126">Step 1</span></span>

<span data-ttu-id="56731-127">WireShark를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="56731-128">2단계</span><span class="sxs-lookup"><span data-stu-id="56731-128">Step 2</span></span>

<span data-ttu-id="56731-129">부하 hello **.cap** 패킷 캡처에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="56731-130">이 파일이 우리의 로컬로 hello 가상 컴퓨터에 저장 된 hello blob에 구성한 방법에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="56731-131">3단계</span><span class="sxs-lookup"><span data-stu-id="56731-131">Step 3</span></span>

<span data-ttu-id="56731-132">tooview hello TCP 대화에 초기 왕복 시간 (RTT)만 살펴볼 것 hello TCP 핸드셰이크에 관련 된 처음 두 개의 패킷을 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="56731-133">Hello 처음 두 개의 패킷을 hello 3 방향 핸드셰이크에서 요소인 hello [SYN]를 사용 합니다 [SYN, ACK] 패킷을 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="56731-134">Hello TCP 헤더에 설정 된 플래그에 대 한 이름으로 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="56731-135">이 시나리오에서는 hello 마지막 패킷으로 hello [ACK] 패킷 hello 핸드셰이크에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="56731-136">hello [SYN] 패킷이 hello 클라이언트에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56731-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="56731-137">수신 되 면 hello 서버 hello SYN hello 클라이언트로부터 받는의 인정으로 hello [ACK] 패킷을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="56731-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="56731-138">Hello 서버 응답 오버 헤드가 거의 필요 하다는 hello 팩트를 활용 하는 hello 시간 [SYN] 패킷이 hello [SYN, ACK] 패킷이 hello 클라이언트에서 수신 되었습니다 hello 시간을 빼서 RTT hello 클라이언트에서 보낸 hello를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="56731-139">WireShark를 사용하여 이 값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="56731-140">toomore hello TCP 3 방향 핸드셰이크에서 처음 두 hello 패킷에 쉽게 볼, WireShark에서 제공 하는 기능을 필터링 하는 hello를 이용 하 게 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="56731-141">WireShark에서 tooapply hello 필터는 hello 프로그램 캡처의 [SYN] 패킷의 "Transmission Control Protocol" 세그먼트를 확장 하 고 hello TCP 헤더에 설정 된 hello 플래그를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="56731-142">모든 SYN에 toofilter 찾고 이후 및 [SYN, ACK] 플래그에서 패킷을 시스템이 hello Syn 비트가 too1, 다음 필터 선택 됨->-> 적용을-> hello Syn 비트 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![그림 7][7]

### <a name="step-4"></a><span data-ttu-id="56731-144">4단계</span><span class="sxs-lookup"><span data-stu-id="56731-144">Step 4</span></span>

<span data-ttu-id="56731-145">Hello 창 tooonly 참조 패킷 수를 필터링 했으므로 hello [SYN] 비트가 설정, 쉽게 선택할 수 있습니다 tooview에 관심이 대화 hello 초기 RTT 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="56731-146">간단한 방법을 tooview hello WireShark의 RTT "SEQ/ACK" 분석을 표시 하는 hello 드롭다운을 클릭 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56731-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="56731-147">그런 다음 RTT 표시 hello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="56731-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="56731-148">이 경우 hello RTT 0.0022114 초 또는 2.211 ms 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![그림 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="56731-150">원치 않는 프로토콜</span><span class="sxs-lookup"><span data-stu-id="56731-150">Unwanted protocols</span></span>

<span data-ttu-id="56731-151">Azure에 배포한 가상 컴퓨터 인스턴스에 많은 응용 프로그램이 실행 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="56731-152">대부분의 이러한 응용 프로그램 사용자의 명시적인 허가 없이 아마도 hello 네트워크를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="56731-153">패킷 캡처 toostore 네트워크 통신을 사용 하 여, 응용 프로그램 hello 네트워크에서 통신 하 고 모든 문제에 대 한 확인 하는 방법을 조사할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="56731-154">이 예에서는 컴퓨터에서 실행 중인 응용 프로그램에서 무단 통신을 나타낼 수 있는 원치 않는 프로토콜에 대해 이전에 실행된 패킷 캡처를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="56731-155">1단계</span><span class="sxs-lookup"><span data-stu-id="56731-155">Step 1</span></span>

<span data-ttu-id="56731-156">이전 시나리오 클릭 hello에에서 동일한 캡처 hello를 사용 하 여 **통계** > **프로토콜 계층**</span><span class="sxs-lookup"><span data-stu-id="56731-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![프로토콜 계층 메뉴][2]

<span data-ttu-id="56731-158">hello 프로토콜 계층 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="56731-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="56731-159">이 보기에서 패킷 전송 되 고 hello 프로토콜을 사용 하 여 받은 hello 수 hello 캡처 세션 중 사용 했던 모든 hello 프로토콜의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56731-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="56731-160">이 보기는 가상 컴퓨터 또는 네트워크에서 원치 않는 네트워크 트래픽을 찾는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![프로토콜 계층 열림][3]

<span data-ttu-id="56731-162">화면 캡처를 수행 하는 hello에 보시 피어 toopeer 파일 공유에 사용 되는 hello 들어오는 BitTorrent 프로토콜을 사용 하 여 트래픽을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="56731-163">관리자 권한으로이 특정 가상 컴퓨터에서 toosee 들어오는 BitTorrent 트래픽을 예상 되지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="56731-164">이제이 트래픽을 인식할 수 있습니다 hello 피어 toopeer 소프트웨어를 제거할 수이 가상 컴퓨터 또는 블록 hello에 설치 된 네트워크 보안 그룹 또는 방화벽을 사용 하 여 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="56731-165">또한 hello 프로토콜 사용 하 여 가상 컴퓨터에서 정기적으로 검토할 수 있습니다는 일정에 따라 toorun 패킷 캡처를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="56731-166">Tooautomate 네트워크 방문을 azure에서 작업 하는 방법의 예제를 보려면 [azure 자동화를 사용 하 여 네트워크 리소스를 모니터링 합니다.](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="56731-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="56731-167">상위 대상 및 포트 찾기</span><span class="sxs-lookup"><span data-stu-id="56731-167">Finding top destinations and ports</span></span>

<span data-ttu-id="56731-168">끝점 hello hello 트래픽 종류를 이해 하 고 hello 포트를 통해 전달 되는 중요 한 응용 프로그램 및 네트워크의 리소스 문제를 해결 하거나 모니터링 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="56731-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="56731-169">위의 패킷 캡처 파일을 사용 하 여, 파악할 수 있습니다 신속 하 게 hello 상위 대상 우리의 VM와 통신 하 고 hello 사용 중인 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="56731-170">1단계</span><span class="sxs-lookup"><span data-stu-id="56731-170">Step 1</span></span>

<span data-ttu-id="56731-171">이전 시나리오 클릭 hello에에서 동일한 캡처 hello를 사용 하 여 **통계** > **IPv4 통계** > **포트 및 대상**</span><span class="sxs-lookup"><span data-stu-id="56731-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![패킷 캡처 창][4]

### <a name="step-2"></a><span data-ttu-id="56731-173">2단계</span><span class="sxs-lookup"><span data-stu-id="56731-173">Step 2</span></span>

<span data-ttu-id="56731-174">Hello 결과 통해 의견에 귀 줄 돋 보입니다, 그리고 111 포트에서 여러 연결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="56731-175">hello 가장 사용 되는 포트 3389는 원격 데스크톱 되었으며 hello 남은 RPC 동적 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="56731-176">이 트래픽은 아무 의미가 수, 하는 동안에 많은 연결에 사용 된 있으며 알 수 없는 toohello 관리자 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![그림 5][5]

### <a name="step-3"></a><span data-ttu-id="56731-178">3단계</span><span class="sxs-lookup"><span data-stu-id="56731-178">Step 3</span></span>

<span data-ttu-id="56731-179">내부 포트를 벗어난 결정 했으므로 우리의 캡처 hello 포트에 따라 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="56731-180">이 시나리오에서는 hello 필터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="56731-181">에서는 hello 필터 텍스트 상자에 위에서 hello 필터 텍스트를 입력 하 고 enter 키를 눌러 합니다.</span><span class="sxs-lookup"><span data-stu-id="56731-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![그림 6][6]

<span data-ttu-id="56731-183">모든 hello 트래픽이 hello에 로컬 가상 컴퓨터에서 온 것인지 확인할 수 있습니다 hello 결과에서 동일한 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="56731-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="56731-184">여전히이 트래픽이 발생 하는 이유와 이해 하지 못하면, hello 패킷에 toodetermine 이유 111 포트에서 이러한 호출 하는 것을 추가 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="56731-185">이 정보로 hello 적절 한 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56731-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56731-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56731-186">Next steps</span></span>

<span data-ttu-id="56731-187">자세한 정도 방문 하 여 네트워크 감시자의 다른 진단 기능을 hello [Azure 네트워크 모니터링 개요](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="56731-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













