---
title: "Azure Network Watcher 및 오픈 소스 도구를 사용하여 네트워크 트래픽 패턴 시각화 | Microsoft Docs"
description: "이 페이지에서는 Capanalysis와 함께 Network Watcher 패킷 캡처를 사용하여 VM과 주고 받는 트래픽을 시각화하는 방법을 설명합니다."
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
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="5768c-103">오픈 소스 도구를 사용하여 VM과 주고 받는 네트워크 트래픽 패턴 시각화</span><span class="sxs-lookup"><span data-stu-id="5768c-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="5768c-104">패킷 캡처에는 네트워크 과학 수사 및 상세한 패킷 검사를 수행할 수 있는 네트워크 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="5768c-105">패킷 캡처를 분석하여 네트워크에 대한 정보를 파악할 수 있는 여러 오픈 소스 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="5768c-106">이러한 도구 중 하나는 오픈 소스 패킷 캡처 시각화 도구인 CapAnalysis입니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="5768c-107">패킷 캡처 데이터 시각화는 네트워크의 패턴 및 오류에 대한 정보를 신속하게 얻을 수 있는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="5768c-108">또한 시각화는 이러한 정보를 손쉽게 공유할 수 있는 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="5768c-109">Azure의 Network Watcher는 네트워크에서 패킷 캡처를 수행하여 이 중요한 데이터를 캡처하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="5768c-110">이 문서에서는 CapAnalysis를 Network Watcher와 함께 사용하여 패킷 캡처를 시각화하고 정보를 얻는 방법을 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="5768c-111">시나리오</span><span class="sxs-lookup"><span data-stu-id="5768c-111">Scenario</span></span>

<span data-ttu-id="5768c-112">Azure VM에 간단한 웹 응용 프로그램을 배포했으며 오픈 소스 도구를 통해 네트워크 트래픽을 시각화하여 흐름 패턴과 오류를 신속하게 식별하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="5768c-113">Network Watcher를 사용하면 네트워크 환경의 패킷 캡처를 획득하여 저장소 계정에 바로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="5768c-114">그러면 CapAnalysis가 저장소 BLOB에서 직접 패킷 캡처를 수집하고 해당 콘텐츠를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![시나리오][1]

## <a name="steps"></a><span data-ttu-id="5768c-116">단계</span><span class="sxs-lookup"><span data-stu-id="5768c-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="5768c-117">CapAnalysis 설치</span><span class="sxs-lookup"><span data-stu-id="5768c-117">Install CapAnalysis</span></span>

<span data-ttu-id="5768c-118">가상 컴퓨터에 CapAnalysis를 설치하는 방법은 https://www.capanalysis.net/ca/how-to-install-capanalysis에서 공식 절차를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5768c-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="5768c-119">CapAnalysis에 원격으로 액세스하려면 새 인바운드 보안 규칙을 추가하여 VM에서 9877 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="5768c-120">네트워크 보안 그룹에서 규칙을 만드는 방법에 대한 자세한 내용은 [기존 NSG에서 규칙 만들기](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5768c-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="5768c-121">규칙이 추가되면 `http://<PublicIP>:9877`에서 CapAnalysis에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="5768c-122">Azure Network Watcher를 사용하여 패킷 캡처 세션 시작</span><span class="sxs-lookup"><span data-stu-id="5768c-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="5768c-123">Network Watcher를 사용하면 가상 컴퓨터가 주고 받는 트래픽을 추적하는 패킷을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="5768c-124">패킷 캡처 세션을 시작하는 방법은 [Network Watcher를 사용하여 패킷 캡처 관리](network-watcher-packet-capture-manage-portal.md)의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5768c-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="5768c-125">이 패킷 캡처는 CapAnalysis가 액세스할 수 있도록 저장소 BLOB에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="5768c-126">CapAnalysis에 패킷 캡처 업로드</span><span class="sxs-lookup"><span data-stu-id="5768c-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="5768c-127">"URL에서 가져오기" 탭을 사용하여 패킷 캡처가 저장된 저장소 BLOB의 링크를 제공하는 방법을 통해 Network Watcher가 만든 패킷 캡처를 직접 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="5768c-128">CapAnalysis에 대한 링크를 제공할 때 저장소 BLOB URL에 SAS 토큰을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="5768c-129">이렇게 하려면 저장소 계정에서 공유 액세스 서명으로 이동하여 허용되는 권한을 지정하고 SAS 생성 단추를 눌러 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="5768c-130">그런 다음 이 SAS 토큰을 패킷 캡처 저장소 BLOB URL에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="5768c-131">그 결과로 표시되는 URL은 http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere와 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="5768c-132">패킷 캡처 분석</span><span class="sxs-lookup"><span data-stu-id="5768c-132">Analyzing packet captures</span></span>

<span data-ttu-id="5768c-133">CapAnalysis는 패킷 캡처를 시각화하는 다양한 옵션을 제공하며, 각 옵션은 서로 다른 관점에서 패킷 캡처를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="5768c-134">이러한 시각적 요약 정보를 통해 네트워크 트래픽 추세를 이해하고 신속하게 비정상적인 활동을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="5768c-135">이러한 기능 중 일부는 다음 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="5768c-136">흐름 테이블</span><span class="sxs-lookup"><span data-stu-id="5768c-136">Flow Tables</span></span>

    <span data-ttu-id="5768c-137">이 테이블은 패킷 데이터의 흐름 목록, 흐름과 연결된 타임 스탬프 및 흐름과 연결된 다양한 프로토콜 그리고 원본 및 대상 IP를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![capanalysis 흐름 페이지][5]

1. <span data-ttu-id="5768c-139">프로토콜 개요</span><span class="sxs-lookup"><span data-stu-id="5768c-139">Protocol Overview</span></span>

    <span data-ttu-id="5768c-140">이 창에서는 다양한 프로토콜 및 지리적 위치의 네트워크 트래픽 분산을 신속하게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![capanalysis 프로토콜 개요][6]

1. <span data-ttu-id="5768c-142">통계</span><span class="sxs-lookup"><span data-stu-id="5768c-142">Statistics</span></span>

    <span data-ttu-id="5768c-143">이 창에서는 원본 및 대상 IP와 주고 받은 바이트, 각 원본 및 대상 IP의 흐름, 다양한 흐름에 사용된 프로토콜, 흐름의 기간 등 네트워크 트래픽 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![capanalysis 통계][7]

1. <span data-ttu-id="5768c-145">지역 지도</span><span class="sxs-lookup"><span data-stu-id="5768c-145">Geomap</span></span>

    <span data-ttu-id="5768c-146">이 창에서는 각 국가의 트래픽 볼륨 크기에 따라 색깔이 표시된 네트워크 트래픽의 지도 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="5768c-147">강조 표시된 국가를 선택하면 해당 국가의 IP에서 주고 받은 데이터 비율 같은 추가 흐름 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![지역 지도][8]

1. <span data-ttu-id="5768c-149">필터</span><span class="sxs-lookup"><span data-stu-id="5768c-149">Filters</span></span>

    <span data-ttu-id="5768c-150">CapAnalysis는 특정 패킷을 신속하게 분석할 수 있는 필터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="5768c-151">예를 들어 프로토콜을 기준으로 데이터를 필터링하여 해당 트래픽 하위 집합에 대한 구체적인 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="5768c-153">CapAnalysis의 모든 기능에 대한 자세한 내용은 [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5768c-154">결론</span><span class="sxs-lookup"><span data-stu-id="5768c-154">Conclusion</span></span>

<span data-ttu-id="5768c-155">Network Watcher의 패킷 캡처 기능을 사용하면 네트워크 과학 수사를 수행하고 네트워크 트래픽을 보다 정확하게 이해하는 데 필요한 데이터를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="5768c-156">이 시나리오에서는 Network Watcher의 패킷 캡처를 오픈 소스 시각화 도구와 간단하게 통합하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="5768c-157">CapAnalysis 같은 오픈 소스 도구를 사용하여 패킷 캡처를 시각화하면 패킷을 자세히 검사하여 네트워크 트래픽의 추세를 신속하게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5768c-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5768c-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5768c-158">Next steps</span></span>

<span data-ttu-id="5768c-159">[NSG 흐름 기록](network-watcher-nsg-flow-logging-overview.md)을 방문하여 NSG 흐름 로그에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5768c-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="5768c-160">[Power BI에서 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)를 방문하여 Power BI로 NSG 흐름 로그를 시각화하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="5768c-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
