---
title: "Power BI를 사용 하 여 Azure 네트워크 보안 그룹 흐름 aaaVisualizing 기록 | Microsoft Docs"
description: "이 페이지는 Power BI를 사용 하 여 toovisualize NSG 흐름을 기록 하는 방법을 설명 합니다."
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
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="95ebd-103">Power BI를 사용하여 네트워크 보안 그룹 흐름 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="95ebd-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="95ebd-104">네트워크 보안 그룹 흐름 로그 IP 트래픽이 ingress 및 egress에 대 한 네트워크 보안 그룹에 tooview 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="95ebd-105">이러한 흐름 로그 아웃 바운드 나타나며 당 규칙 별로 인바운드 흐름 hello NIC hello 흐름 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜) 및 hello 트래픽을 허용 또는 거부 된 경우에 대 한 5-튜플 정보에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="95ebd-106">수동으로 hello 로그 파일을 검색 하 여 로깅 데이터 흐름에 대 한 어려운 toogain 정보 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="95ebd-107">이 문서에서는 가장 최근의 흐름 로그 및 네트워크의 트래픽에 대 한 자세한 내용은 솔루션 toovisualize를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="95ebd-108">시나리오</span><span class="sxs-lookup"><span data-stu-id="95ebd-108">Scenario</span></span>

<span data-ttu-id="95ebd-109">시나리오를 따르는 hello에서 NSG 흐름 로깅 데이터에 대 한 hello 싱크로 구성 했습니다 Power BI 데스크톱 toohello 저장소 계정을 연결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="95ebd-110">Tooour 저장소 계정, 연결 후 Power BI는 다운로드 하 고 hello 로그 tooprovide을 시각적으로 네트워크 보안 그룹에 의해 기록 된 hello 트래픽 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="95ebd-111">Hello 서식 파일을 검사할 수 있습니다에 제공 된 hello 시각적 개체를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="95ebd-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="95ebd-112">상위 토커</span><span class="sxs-lookup"><span data-stu-id="95ebd-112">Top Talkers</span></span>
* <span data-ttu-id="95ebd-113">방향 및 규칙 결정에 따른 시계열 흐름 데이터</span><span class="sxs-lookup"><span data-stu-id="95ebd-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="95ebd-114">네트워크 인터페이스 MAC 주소에 따른 흐름</span><span class="sxs-lookup"><span data-stu-id="95ebd-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="95ebd-115">NSG 및 규칙에 따른 흐름</span><span class="sxs-lookup"><span data-stu-id="95ebd-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="95ebd-116">대상 포트에 따른 흐름</span><span class="sxs-lookup"><span data-stu-id="95ebd-116">Flows by Destination Port</span></span>

<span data-ttu-id="95ebd-117">제공 된 hello 템플릿을 편집할 수 있으므로 tooadd 새 데이터를 시각적 개체를 수정 하거나 쿼리 toosuit 요구에 맞게 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="95ebd-118">설정</span><span class="sxs-lookup"><span data-stu-id="95ebd-118">Setup</span></span>

<span data-ttu-id="95ebd-119">시작하기 전에 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="95ebd-120">네트워크 보안을 사용 하도록 설정에 대 한 지침은 로그 흐름 toohello 다음 문서를 참조 하십시오: [네트워크 보안 그룹에 대 한 소개 tooflow 로깅을](network-watcher-nsg-flow-logging-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="95ebd-121">또한 hello Power BI Desktop 클라이언트와 충분 한 컴퓨터에 설치 되어 컴퓨터 toodownload 및 부하 hello 로그 데이터의 저장소 계정에서 사용 가능한 공간 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Visio 다이어그램][1]

### <a name="steps"></a><span data-ttu-id="95ebd-123">단계</span><span class="sxs-lookup"><span data-stu-id="95ebd-123">Steps</span></span>

1. <span data-ttu-id="95ebd-124">다운로드 및 hello Power BI Desktop 응용 프로그램에서에서 Power BI 템플릿을 다음 열기 hello [네트워크 감시자 PowerBI 흐름 기록 서식 파일](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="95ebd-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="95ebd-125">Hello 필요한 쿼리 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="95ebd-126">**StorageAccountName** – toohello 이름을 포함 하는 hello NSG 흐름 로그 hello 저장소 계정의 지정 tooload 선택한 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="95ebd-127">**NumberOfLogFiles** – hello toodownload 같은 및 Power BI의 시각화는 로그 파일 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="95ebd-128">예를 들어 50을 지정 하는 경우 hello 50 최신 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="95ebd-129">설정 하 고 toosend NSG 흐름 로그 toothis 계정을 구성 하는 ff 2 Nsg는 다음 hello 25 지난 시간의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![power BI 메인][2]

1. <span data-ttu-id="95ebd-131">Hello 저장소 계정에 대 한 액세스 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="95ebd-132">Hello Azure 선택 하 고 포털에서 저장소 계정을 tooyour를 탐색 하 여 유효한 액세스 키를 찾을 수 **선택 키** hello 설정 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="95ebd-133">그런 다음 **연결**을 클릭하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-133">Click **Connect** then apply changes.</span></span>

    ![액세스 키][3]

    ![액세스 키 2][4]

4.  <span data-ttu-id="95ebd-136">로그를 다운로드 되 고 구문 분석 하 고 이제 hello 미리 작성된 된 시각적 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="95ebd-137">Hello 시각적 표시 이해</span><span class="sxs-lookup"><span data-stu-id="95ebd-137">Understanding hello visuals</span></span>

<span data-ttu-id="95ebd-138">Hello 서식 파일은 제공 된 데 도움이 되는 시각적 개체 집합이 hello NSG 흐름 로그 데이터의 의미를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="95ebd-139">hello 다음 이미지가 표시 hello 대시보드 데이터로 채울 때 처럼 보이는의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="95ebd-140">아래에서는 각 시각 효과를 좀 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="95ebd-142">hello Top 송신기 시각적 표시 hello Ip를 시작 했습니다. 지정 된 기간 hello를 통해 대부분의 연결을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="95ebd-143">hello 상자 hello 크기 toohello 상대 연결 수가 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="95ebd-145">hello 다음 시간 시계열 그래프 표시 hello 기간 동안 흐름 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="95ebd-146">hello 위쪽 그래프 hello 흐름 방향으로 분리 된 및 hello 결정 (허용 또는 거부) 하 여 hello 낮은 조각화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="95ebd-147">이 시각 효과를 사용하면 시간에 따른 트래픽 추세를 검사하고, 트래픽 또는 트래픽 세그먼트의 비정상적인 급증 현상 또는 급감 현상을 찾아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="95ebd-149">hello 다음 그래프에 표시 hello 흐름 hello 위쪽 방향으로 분리 및 hello 낮은 내린 결정 기호로 분리 된 네트워크 인터페이스당.</span><span class="sxs-lookup"><span data-stu-id="95ebd-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="95ebd-150">이 정보를 전달 하 여 Vm 중 어떤 hello 대부분 상대 tooothers 및 트래픽 tooa 특정 VM 되는 경우에 대 한 정보를 얻을 수 있습니다 허용 또는 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="95ebd-152">hello 도넛 휠 차트 다음 분석 대상 포트 여 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="95ebd-153">이 정보를 지정 하는 hello 내에서 사용 되는 가장 일반적으로 사용 하는 hello 대상 포트를 볼 수 있습니다 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![donut][9]

<span data-ttu-id="95ebd-155">hello 다음 가로 막대형 차트에서는 hello NSG 및 규칙 흐름</span><span class="sxs-lookup"><span data-stu-id="95ebd-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="95ebd-156">이 정보를 볼 수 있습니다 hello Nsg hello에 대 한 책임 대부분 트래픽과 트래픽의 hello 분석 NSG에서 규칙에 의해.</span><span class="sxs-lookup"><span data-stu-id="95ebd-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="95ebd-158">hello hello Nsg에 대 한 정보 제공 용 이므로 차트 표시 정보를 다음 hello 로그에 있는, hello 흐름 hello 기간 및 hello 날짜 캡처된 hello 가장 빠른 로그를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="95ebd-159">이 정보를 사용 하면 어떤 Nsg는 기록 되 고 및 흐름의 날짜 범위를 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="95ebd-162">이 템플릿에 안녕하세요 슬라이서 tooallow 다음 tooview 유일한 hello 데이터에 가장 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="95ebd-163">사용자는 리소스 그룹, NSG 및 규칙을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="95ebd-164">5 튜플 정보, 의사 결정, 및 hello 로그 기록 된 hello 시간에 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="95ebd-166">결론</span><span class="sxs-lookup"><span data-stu-id="95ebd-166">Conclusion</span></span>

<span data-ttu-id="95ebd-167">했죠이 시나리오에서는 네트워크 감시자 및 Power BI에서 제공 하는 네트워크 보안 그룹 흐름 로그를 사용 하 여 우리 수 toovisualize를 hello 트래픽을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="95ebd-168">제공 된 hello 템플릿을 사용 하 여, Power BI hello 로그 저장소에서 직접 다운로드 합니다. 하 고 로컬로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="95ebd-169">다운로드 한 파일의 전체 크기 및 타임 라인 tooload hello 템플릿을 hello 요청한 파일 수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="95ebd-170">무료 toocustomize 요구에 따라이 서식 파일을 느낍니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="95ebd-171">Power BI를 네트워크 보안 그룹 흐름 로그와 함께 사용할 수 있는 매우 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="95ebd-172">참고 사항</span><span class="sxs-lookup"><span data-stu-id="95ebd-172">Notes</span></span>

* <span data-ttu-id="95ebd-173">로그는 기본적으로 `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="95ebd-174">다른 디렉터리에 다른 데이터가 있는 경우 쿼리 toopull를 hello 및 프로세스 hello 데이터를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="95ebd-175">1GB 이상의 로그와 함께 사용할 hello 제공 템플릿의 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="95ebd-176">로그 용량이 큰 경우 Data Lake 또는 SQL Server 같은 다른 데이터 저장소를 사용하는 솔루션을 알아보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="95ebd-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95ebd-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95ebd-177">Next Steps</span></span>

<span data-ttu-id="95ebd-178">Toovisualize NSG 흐름 기록 하는 방법을 Elastick 스택 hello로 방문 하 여 자세한 [오픈 소스 도구를 사용 하 여 Vm에서 네트워크 트래픽 패턴 tooand 시각화](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="95ebd-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

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
