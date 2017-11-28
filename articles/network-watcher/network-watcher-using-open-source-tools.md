---
title: "Azure 네트워크 감시자 오픈 소스 도구와 aaaVisualize 네트워크 트래픽 패턴 | Microsoft Docs"
description: "이 페이지에서는 toouse 네트워크 감시자 패킷 캡처 Capanalysis toovisualize 트래픽 패턴 tooand 내 vm에서을 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="1f26c-103">오픈 소스 도구를 사용 하 여 Vm에서 네트워크 트래픽 패턴 tooand 시각화</span><span class="sxs-lookup"><span data-stu-id="1f26c-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="1f26c-104">패킷 캡처 tooperform 네트워크 법정 데이터와 심층 패킷 검사 수 있는 네트워크 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="1f26c-105">Tooanalyze 패킷 캡처 toogain insights를 사용 하 여 네트워크에 대 한 소스 도구는 많은 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="1f26c-106">이러한 도구 중 하나는 오픈 소스 패킷 캡처 시각화 도구인 CapAnalysis입니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="1f26c-107">패킷 캡처 데이터를 시각화는 tooquickly 패턴 및 네트워크 내에서 잘못 된 부분에 대 한 통찰력을 파생 하는 귀중 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="1f26c-108">또한 시각화는 이러한 정보를 손쉽게 공유할 수 있는 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="1f26c-109">Azure의 네트워크 감시자를 네트워크에 기능 toocapture tooperform 패킷을 허용 하 여이 중요 한 데이터를 캡처합니다 hello 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="1f26c-110">이 문서에서는 패킷에서 toovisualize 및 게인 insights 캡처합니다 CapAnalysis 네트워크 감시자를 사용 하 여 하는 방법을 보여 주는 연습을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="1f26c-111">시나리오</span><span class="sxs-lookup"><span data-stu-id="1f26c-111">Scenario</span></span>

<span data-ttu-id="1f26c-112">배포 하는 간단한 웹 응용 프로그램이 Azure 원하는 toouse 오픈 소스 도구 toovisualize에서 VM에 해당 네트워크 트래픽을 tooquickly 가능한 오류를 확인 및 흐름 패턴을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="1f26c-113">Network Watcher를 사용하면 네트워크 환경의 패킷 캡처를 획득하여 저장소 계정에 바로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="1f26c-114">그런 다음 CapAnalysis hello 패킷 캡처 직접 hello 저장소 blob에서 수집 하 고 해당 콘텐츠를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![시나리오][1]

## <a name="steps"></a><span data-ttu-id="1f26c-116">단계</span><span class="sxs-lookup"><span data-stu-id="1f26c-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="1f26c-117">CapAnalysis 설치</span><span class="sxs-lookup"><span data-stu-id="1f26c-117">Install CapAnalysis</span></span>

<span data-ttu-id="1f26c-118">tooinstall CapAnalysis 가상 컴퓨터에서 toohello 공식 지침을 참조할 수 있습니다 여기 https://www.capanalysis.net/ca/how-to-install-capanalysis 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="1f26c-119">순서 CapAnalysis를 원격으로 액세스, 새 인바운드 보안 규칙을 추가 하 여 VM에 tooopen 포트 9877 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="1f26c-120">네트워크 보안 그룹의 규칙을 만드는 방법에 대 한 자세한 참조 너무[기존 NSG에서 규칙을 만들](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="1f26c-121">수 tooaccess CapAnalysis 있어야 hello 규칙 성공적으로 추가 되 면에서`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="1f26c-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="1f26c-122">Azure 네트워크 감시자 toostart 패킷을 캡처 세션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1f26c-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="1f26c-123">네트워크 감시자는 가상 컴퓨터를 내부 및 외부로 toocapture 패킷을 tootrack 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="1f26c-124">Toohello 지침을 참조할 수 있습니다 [관리 패킷 캡처 네트워크 감시자를](network-watcher-packet-capture-manage-portal.md) toostart 패킷 캡처 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="1f26c-125">이 패킷 캡처 CapAnalysis에서 액세스 하는 저장소 blob toobe에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="1f26c-126">패킷 캡처 tooCapAnalysis 업로드</span><span class="sxs-lookup"><span data-stu-id="1f26c-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="1f26c-127">Hello 패킷 캡처를 저장 되어 있는 네트워크 감시자 hello "가져오기에서 URL" 탭을 사용 하 고 링크 toohello 저장소 blob를 제공 하 여 수행 되는 패킷 캡처를 직접 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="1f26c-128">링크 tooCapAnalysis를 제공 하는 SAS 토큰 toohello 저장소 blob URL tooappend 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="1f26c-129">toodo hello 저장소 계정에서 액세스 서명 tooShared 탐색이, 사용 권한을 허용 하는 hello를 지정 하 고 hello SAS 생성 단추 toocreate 토큰 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="1f26c-130">그런 다음이 SAS 토큰 toohello 패킷 캡처 저장소 blob URL을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="1f26c-131">hello 결과 URL은 다음과 같은: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="1f26c-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="1f26c-132">패킷 캡처 분석</span><span class="sxs-lookup"><span data-stu-id="1f26c-132">Analyzing packet captures</span></span>

<span data-ttu-id="1f26c-133">CapAnalysis 다양 한 옵션 toovisualize 패킷 캡처를 다른 관점에서 각 제공 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="1f26c-134">이러한 시각적 요약 정보를 통해 네트워크 트래픽 추세를 이해하고 신속하게 비정상적인 활동을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="1f26c-135">이러한 기능 중 몇 가지 hello 목록 다음에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="1f26c-136">흐름 테이블</span><span class="sxs-lookup"><span data-stu-id="1f26c-136">Flow Tables</span></span>

    <span data-ttu-id="1f26c-137">이 테이블을 제공 hello 패킷 데이터의 흐름 목록이 hello, hello 흐름와 연결 된 타임 스탬프 hello hello hello 흐름 뿐만 아니라 원본 및 대상 IP와 관련 된 다양 한 프로토콜.</span><span class="sxs-lookup"><span data-stu-id="1f26c-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![capanalysis 흐름 페이지][5]

1. <span data-ttu-id="1f26c-139">프로토콜 개요</span><span class="sxs-lookup"><span data-stu-id="1f26c-139">Protocol Overview</span></span>

    <span data-ttu-id="1f26c-140">이 창을 사용 하면 다양 한 프로토콜 및 지리적 tooquickly hello를 통해 네트워크 트래픽 분산 hello를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![capanalysis 프로토콜 개요][6]

1. <span data-ttu-id="1f26c-142">통계</span><span class="sxs-lookup"><span data-stu-id="1f26c-142">Statistics</span></span>

    <span data-ttu-id="1f26c-143">이 창에는 경우 tooview 네트워크 트래픽 통계 바이트를 소스 및 대상 Ip, hello 소스 및 대상 Ip, 각각에 대해 흐름에서 받은 프로토콜에 사용 되는 다양 한 흐름의 흐름 hello 기간 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![capanalysis 통계][7]

1. <span data-ttu-id="1f26c-145">지역 지도</span><span class="sxs-lookup"><span data-stu-id="1f26c-145">Geomap</span></span>

    <span data-ttu-id="1f26c-146">이 창을 사용 하면 네트워크 트래픽의 지도 보기 각 국가의 트래픽의 toohello 볼륨 크기 조정 하는 색으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="1f26c-147">해당 국가에서 Ip에서 보내고 받는 데이터의 hello 비율 등의 강조 표시 된 국가 tooview 추가 흐름 통계를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![지역 지도][8]

1. <span data-ttu-id="1f26c-149">필터</span><span class="sxs-lookup"><span data-stu-id="1f26c-149">Filters</span></span>

    <span data-ttu-id="1f26c-150">CapAnalysis는 특정 패킷을 신속하게 분석할 수 있는 필터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="1f26c-151">예를 들어 프로토콜 toogain 특정 insights 트래픽의 해당 하위 집합에 의해 toofilter hello 데이터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="1f26c-153">방문 [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn 모든 CapAnalysis 기능에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1f26c-154">결론</span><span class="sxs-lookup"><span data-stu-id="1f26c-154">Conclusion</span></span>

<span data-ttu-id="1f26c-155">네트워크 감시자 패킷 캡처 기능에는 네트워크 트래픽을 더 잘 이해 및 toocapture hello 필요한 tooperform 네트워크 법정 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="1f26c-156">이 시나리오에서는 Network Watcher의 패킷 캡처를 오픈 소스 시각화 도구와 간단하게 통합하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="1f26c-157">CapAnalysis toovisualize 패킷 캡처와 같은 오픈 소스 도구 사용 하면 심층 패킷 검사를 수행할 수 있으며 네트워크 트래픽을 내에서 추세를 빠르게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f26c-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f26c-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f26c-158">Next steps</span></span>

<span data-ttu-id="1f26c-159">NSG 흐름 로그에 대해 자세히 toolearn 방문 [NSG 흐름 기록](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1f26c-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="1f26c-160">Toovisualize NSG 흐름 기록 하는 방법을 Power BI를 방문 하 여 자세한 [NSG 시각화할 Power BI를 사용 하 여 로그 전달](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="1f26c-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
