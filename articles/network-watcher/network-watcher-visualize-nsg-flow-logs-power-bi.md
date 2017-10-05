---
title: "Power BI를 사용하여 Azure 네트워크 보안 그룹 흐름 로그 시각화 | Microsoft Docs"
description: "이 페이지에서는 Power BI를 사용하여 NSG 흐름 로그를 시각화하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d8c61ca2a3bd5affe02e8f9500655db6699a245f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="65413-103">Power BI를 사용하여 네트워크 보안 그룹 흐름 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="65413-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="65413-104">네트워크 보안 그룹 흐름 로그를 통해 네트워크 보안 그룹의 송/수신 IP 트래픽에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="65413-105">이러한 흐름 로그는 트래픽이 허용되거나 거부된 경우 각 규칙을 기준으로 아웃바운드 및 인바운드 흐름, 흐름이 적용되는 NIC, 흐름에 대한 5개의 튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65413-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="65413-106">로그 파일을 수동으로 검색하는 방법으로는 흐름 로깅에 대한 정보를 얻기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="65413-107">이 문서에서는 가장 최근의 흐름 로그를 시각화하고 네트워크 트래픽에 대해 알아보는 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="65413-108">시나리오</span><span class="sxs-lookup"><span data-stu-id="65413-108">Scenario</span></span>

<span data-ttu-id="65413-109">다음 시나리오에서는 NSG 흐름 로깅 데이터에 대한 싱크로 구성한 저장소 계정에 Power BI 데스크톱을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="65413-110">저장소 계정에 연결되면 Power BI가 로그를 다운로드하고 구분 분석하여 네트워크 보안 그룹에서 기록한 트래픽의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="65413-111">템플릿에 제공된 시각화 기능을 사용하여 다음 항목을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="65413-112">상위 토커</span><span class="sxs-lookup"><span data-stu-id="65413-112">Top Talkers</span></span>
* <span data-ttu-id="65413-113">방향 및 규칙 결정에 따른 시계열 흐름 데이터</span><span class="sxs-lookup"><span data-stu-id="65413-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="65413-114">네트워크 인터페이스 MAC 주소에 따른 흐름</span><span class="sxs-lookup"><span data-stu-id="65413-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="65413-115">NSG 및 규칙에 따른 흐름</span><span class="sxs-lookup"><span data-stu-id="65413-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="65413-116">대상 포트에 따른 흐름</span><span class="sxs-lookup"><span data-stu-id="65413-116">Flows by Destination Port</span></span>

<span data-ttu-id="65413-117">제공된 템플릿은 편집 가능하므로 사용자는 템플릿을 수정하여 새 데이터와 시각 효과를 추가하거나 본인의 요구 사항에 맞게 쿼리를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="65413-118">설정</span><span class="sxs-lookup"><span data-stu-id="65413-118">Setup</span></span>

<span data-ttu-id="65413-119">시작하기 전에 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="65413-120">네트워크 보안 흐름 로그를 사용하도록 설정하는 방법에 대한 지침은 [네트워크 보안 그룹에 대한 흐름 로깅 소개](network-watcher-nsg-flow-logging-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65413-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="65413-121">또한 컴퓨터에 Power BI Desktop 클라이언트가 설치되어 있고, 저장소 계정에 있는 로그 데이터를 다운로드 및 로드하는 데 충분한 여유 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Visio 다이어그램][1]

### <a name="steps"></a><span data-ttu-id="65413-123">단계</span><span class="sxs-lookup"><span data-stu-id="65413-123">Steps</span></span>

1. <span data-ttu-id="65413-124">Power BI Desktop 응용 프로그램 [Network Watcher PowerBI 흐름 로그 템플릿](https://aka.ms/networkwatcherpowerbiflowlogstemplate)에서 다음 Power BI 템플릿을 다운로드하여 열기</span><span class="sxs-lookup"><span data-stu-id="65413-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="65413-125">필요한 쿼리 매개 변수 입력</span><span class="sxs-lookup"><span data-stu-id="65413-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="65413-126">**StorageAccountName** - 로드하여 시각화하려는 NSG 흐름 로그가 포함된 저장소 계정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="65413-127">**NumberOfLogFiles** – Power BI에서 다운로드하여 시각화하려는 로그 파일의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="65413-128">예를 들어 50을 지정하면 가장 최근의 로그 파일 50개가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="65413-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="65413-129">여기서는 NSG 2개가 활성화되어 이 계정에 NSG 흐름을 보내도록 구성되어 있으므로 지난 25시간의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![power BI 메인][2]

1. <span data-ttu-id="65413-131">저장소 계정의 액세스 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="65413-132">Azure Portal에서 저장소 계정으로 이동한 후 설정 메뉴에서 **액세스 키**를 선택하면 유효한 액세스 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="65413-133">그런 다음 **연결**을 클릭하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-133">Click **Connect** then apply changes.</span></span>

    ![액세스 키][3]

    ![액세스 키 2][4]

4.  <span data-ttu-id="65413-136">로그가 다운로드되고 구문 분석되며 사용자는 미리 작성된 시각 효과를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="65413-137">시각 효과의 이해</span><span class="sxs-lookup"><span data-stu-id="65413-137">Understanding the visuals</span></span>

<span data-ttu-id="65413-138">템플릿에는 NSG 흐름 로그 데이터를 이해하는 데 도움이 되는 일련의 시각 효과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="65413-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="65413-139">다음 이미지는 대시보드에 데이터가 채워지면 어떤 모습인지 살펴볼 수 있는 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="65413-140">아래에서는 각 시각 효과를 좀 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="65413-142">상위 토커 시각 효과는 지정된 시간 동안 가장 많은 연결을 시작한 IP를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="65413-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="65413-143">상자 크기는 연결 수에 비례합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="65413-145">다음 시계열 그래프는 시간에 따른 흐름의 수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="65413-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="65413-146">위쪽 그래프는 흐름 방향에 따라, 아래쪽 그래프는 내려진 결정(허용 또는 거부)에 따라 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="65413-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="65413-147">이 시각 효과를 사용하면 시간에 따른 트래픽 추세를 검사하고, 트래픽 또는 트래픽 세그먼트의 비정상적인 급증 현상 또는 급감 현상을 찾아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="65413-149">다음 그래프는 네트워크 인터페이스별 흐름을 보여주며, 위쪽은 흐름 방향, 아래쪽은 내려진 결정에 따르 세그먼트가 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="65413-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="65413-150">이 정보를 사용하면 다른 VM에 비해 가장 많이 통신한 VM을 파악하고 특정 VM에 대한 트래픽이 허용되는지 또는 거부되는지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="65413-152">다음 도넛 휠 차트는 대상 포트에 따른 흐름의 분류를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="65413-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="65413-153">이 정보를 사용하면 지정된 시간 동안 가장 많이 사용된 대상 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![donut][9]

<span data-ttu-id="65413-155">다음 가로 막대형 차트는 NSG 및 규칙에 따른 흐름을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="65413-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="65413-156">이 정보를 사용하면 가장 많은 트래픽을 담당하는 NSG를 살펴보고, NSG의 트래픽을 규칙에 따라 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="65413-158">다음 정보 차트는 로그에 있는 NSG에 대한 정보, 시간에 따른 캡처된 흐름 수, 가장 빠른 로그가 캡처된 날짜를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="65413-159">이 정보는 어떤 NSG가 기록되었는지 그리고 흐름의 날짜 범위가 어떻게 되는지 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="65413-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="65413-162">이 템플릿에는 가장 관심이 있는 데이터만 볼 수 있도록 다음 슬라이서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="65413-163">사용자는 리소스 그룹, NSG 및 규칙을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="65413-164">또한 5튜플 정보, 의사 결정 및 로그가 작성된 시간을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="65413-166">결론</span><span class="sxs-lookup"><span data-stu-id="65413-166">Conclusion</span></span>

<span data-ttu-id="65413-167">이 시나리오에서는 Network Watcher 및 Power BI에서 제공하는 네트워크 보안 그룹 흐름 로그를 사용하여 트래픽을 시각화하고 이해할 수 있다는 것을 보여드렸습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="65413-168">제공된 템플릿을 사용하여 Power BI는 저장소에서 직접 로그를 다운로드하여 로컬로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="65413-169">템플릿을 로드하는 데 걸리는 시간은 요청된 파일 수와 다운로드 파일의 전체 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="65413-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="65413-170">본인의 요구 사항에 맞게 얼마든지 이 템플릿을 사용자 지정해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65413-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="65413-171">Power BI를 네트워크 보안 그룹 흐름 로그와 함께 사용할 수 있는 매우 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="65413-172">참고 사항</span><span class="sxs-lookup"><span data-stu-id="65413-172">Notes</span></span>

* <span data-ttu-id="65413-173">로그는 기본적으로 `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="65413-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="65413-174">다른 디렉터리에 다른 데이터가 있으면 데이터를 가져와서 처리하는 쿼리를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65413-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="65413-175">로그 크기가 1GB를 초과하는 경우에는 제공된 템플릿을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="65413-176">로그 용량이 큰 경우 Data Lake 또는 SQL Server 같은 다른 데이터 저장소를 사용하는 솔루션을 알아보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65413-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65413-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65413-177">Next Steps</span></span>

<span data-ttu-id="65413-178">[오픈 소스 도구를 사용하여 VM과 주고 받는 네트워크 트래픽 패턴 시각화](network-watcher-using-open-source-tools.md)를 방문하여 탄력적 스택으로 NSG 흐름 로그를 시각화하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="65413-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
