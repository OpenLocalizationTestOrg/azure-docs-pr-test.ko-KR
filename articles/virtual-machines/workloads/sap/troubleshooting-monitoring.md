---
title: "Azure(큰 인스턴스)의 SAP HANA 문제 해결 및 모니터링 | Microsoft Docs"
description: "Azure(큰 인스턴스)에서 SAP HANA 문제 해결 및 모니터링"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="039e1-103">Azure(큰 인스턴스)에서 SAP HANA 문제를 해결하고 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="039e1-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="039e1-104">Azure(큰 인스턴스)의 SAP HANA 모니터링</span><span class="sxs-lookup"><span data-stu-id="039e1-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="039e1-105">Azure(큰 인스턴스)의 SAP HANA는 다른 IaaS 배포와 다르지 않습니다. OS 및 응용 프로그램의 기능 및 다음과 같은 리소스 사용 방법을 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="039e1-106">CPU</span><span class="sxs-lookup"><span data-stu-id="039e1-106">CPU</span></span>
- <span data-ttu-id="039e1-107">메모리</span><span class="sxs-lookup"><span data-stu-id="039e1-107">Memory</span></span>
- <span data-ttu-id="039e1-108">네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="039e1-108">Network bandwidth</span></span>
- <span data-ttu-id="039e1-109">디스크 공간</span><span class="sxs-lookup"><span data-stu-id="039e1-109">Disk space</span></span>

<span data-ttu-id="039e1-110">Azure Virtual Machines에서 위에 명시된 리소스 클래스가 충분한지 또는 고갈되는지 여부를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="039e1-111">다른 클래스 각각에 대한 자세한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="039e1-112">**CPU 리소스 소비량:** 메모리에 저장되는 데이터를 사용할 수 있는 CPU 리소스가 충분하도록 하기 위해 SAP에서 HANA에 대한 특정 워크로드에 정의한 비율이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="039e1-113">그럼에도 HANA가 누락된 인덱스 또는 유사한 문제점으로 인해 쿼리를 실행하는 데 많은 CPU를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="039e1-114">즉, HANA 큰 인스턴스 단위의 CPU 리소스 사용량뿐만 아니라 특정 HANA 서비스에서 사용하는 CPU 리소스를 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="039e1-115">**메모리 사용량:** 단위의 HANA 외부뿐만 아니라 HANA 내부에서도 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="039e1-116">HANA 내에서 데이터가 SAP의 필수 크기 조정 지침 내로 유지되기 위해 HANA 할당 메모리를 사용하는 방법을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="039e1-117">또한 큰 인스턴스 수준에서 메모리 사용량을 모니터링하여 추가 설치된 HANA 이외의 소프트웨어가 너무 많은 메모리를 소비하게 되어 메모리를 두고 HANA와 경쟁하지 않도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="039e1-118">**네트워크 대역폭:** Azure VNet 게이트웨이는 Azure VNet으로 이동하는 데이터의 대역폭으로 제한됩니다. 따라서 VNet 내의 모든 Azure VM에서 수신한 데이터를 모니터링하여 선택한 Azure 게이트웨이 SKU의 제한에 얼마나 근접했는지 파악하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="039e1-119">HANA 큰 인스턴스 단위에서 들어오고 나가는 네트워크 트래픽도 모니터링하고 시간이 지남에 따라 처리되는 볼륨도 추적하는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="039e1-120">**디스크 공간:** 디스크 공간 사용량은 일반적으로 시간이 지남에 따라 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="039e1-121">여러 가지 원인이 있지만 대부분 데이터 볼륨 증가, 트랜잭션 로그 백업 실행, 추적 파일 저장 및 저장소 스냅숏 수행으로 인해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="039e1-122">따라서 디스크 공간 사용량을 모니터링하고 HANA 큰 인스턴스 단위와 연결된 디스크 공간을 관리하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="039e1-123">HANA 쪽에서 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="039e1-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="039e1-124">Azure(큰 인스턴스)의 SAP HANA와 관련된 문제를 효과적으로 분석하기 위해 문제의 근본 원인을 찾는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="039e1-125">SAP는 도움이 될 많은 양의 문서를 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="039e1-126">SAP HANA 성능과 관련된 적용 가능한 FAQ는 다음 SAP 참고 사항에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- [<span data-ttu-id="039e1-127">SAP 참고 사항 #2222200 – FAQ: SAP HANA 네트워크</span><span class="sxs-lookup"><span data-stu-id="039e1-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="039e1-128">SAP 참고 사항 #2100040 – FAQ: SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="039e1-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="039e1-129">SAP 참고 사항 #199997 – FAQ: SAP HANA 메모리</span><span class="sxs-lookup"><span data-stu-id="039e1-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="039e1-130">SAP 참고 사항 #200000 – FAQ: SAP HANA 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="039e1-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="039e1-131">SAP 참고 사항 #199930 – FAQ: SAP HANA I/O 분석</span><span class="sxs-lookup"><span data-stu-id="039e1-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="039e1-132">SAP 참고 사항 #2177064 – FAQ: SAP HANA 서비스 다시 시작 및 충돌</span><span class="sxs-lookup"><span data-stu-id="039e1-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="039e1-133">**SAP HANA 경고**</span><span class="sxs-lookup"><span data-stu-id="039e1-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="039e1-134">첫 번째 단계로 현재 SAP HANA 경고 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="039e1-135">SAP HANA Studio에서 **관리 콘솔: 경고: 표시: 모든 경고**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="039e1-136">이 탭에서는 최소 및 최대 임계값 설정 범위에 속하지 않는 특정 값(사용 가능한 실제 메모리, CPU 사용률 등)에 대한 모든 SAP HANA 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="039e1-137">기본적으로 검사는 15분마다 자동으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![SAP HANA Studio에서 [관리 콘솔: 경고: 표시: 모든 경고]로 이동합니다.](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="039e1-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="039e1-139">**CPU**</span></span>

<span data-ttu-id="039e1-140">부적절한 임계값 설정으로 인해 트리거되는 경고의 경우 해결책은 기본값 또는 보다 적절한 크기의 임계값으로 다시 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![기본값 또는 보다 적절한 크기의 임계값으로 다시 설정](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="039e1-142">다음과 같은 경고는 CPU 리소스 문제를 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="039e1-143">호스트 CPU 사용량(경고 5)</span><span class="sxs-lookup"><span data-stu-id="039e1-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="039e1-144">가장 최근 저장 지점 작업(경고 28)</span><span class="sxs-lookup"><span data-stu-id="039e1-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="039e1-145">저장 지점 기간(경고 54)</span><span class="sxs-lookup"><span data-stu-id="039e1-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="039e1-146">다음 중 하나에서 SAP HANA 데이터베이스에 대한 높은 CPU 사용량을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="039e1-147">경고 5(호스트 CPU 사용량)는 현재 또는 과거 CPU 사용량에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="039e1-148">개요 화면에 표시된 CPU 사용량</span><span class="sxs-lookup"><span data-stu-id="039e1-148">The displayed CPU usage on the overview screen</span></span>

![개요 화면에 표시된 CPU 사용량](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="039e1-150">로드 그래프는 높은 CPU 사용량 또는 과거의 높은 사용량을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![로드 그래프는 높은 CPU 사용량 또는 과거의 높은 사용량을 표시할 수 있습니다.](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="039e1-152">CPU 사용률로 인해 트리거되는 경고는 특정 트랜잭션 실행, 데이터 로드, 장기 실행 SQL 문 및 잘못된 쿼리 성능(예: HANA 큐브의 BW)을 비롯한 다른 여러 가지 원인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="039e1-153">자세한 문제 해결 단계는 [SAP HANA 문제 해결: CPU 관련 원인 및 솔루션](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="039e1-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="039e1-154">**운영 체제**</span><span class="sxs-lookup"><span data-stu-id="039e1-154">**Operating System**</span></span>

<span data-ttu-id="039e1-155">Linux의 SAP HANA에 대한 가장 중요한 검사 중 하나는 Transparent Huge Pages를 사용하지 않도록 설정하는 것입니다. [SAP 참고 사항 #2131662 - SAP HANA 서버의 THP(Transparent Huge Pages)](https://launchpad.support.sap.com/#/notes/2131662)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="039e1-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="039e1-156">다음 Linux 명령을 통해 Transparent Huge Pages를 사용할 수 있는지 확인할 수 있습니다. **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span><span class="sxs-lookup"><span data-stu-id="039e1-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="039e1-157">_always_가 아래와 같이 대괄호로 묶이면 Transparent Huge Pages를 사용할 수 있다는 의미입니다. [always] madvise never _never_가 아래와 같이 대괄호로 묶이면 Transparent Huge Pages를 사용할 수 없다는 의미입니다. always madvise [never]</span><span class="sxs-lookup"><span data-stu-id="039e1-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="039e1-158">다음 Linux 명령은 아무것도 반환하지 않습니다. **rpm -qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="039e1-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="039e1-159">_ulimit_가 표시되는 경우 즉시 설치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="039e1-160">**메모리**</span><span class="sxs-lookup"><span data-stu-id="039e1-160">**Memory**</span></span>

<span data-ttu-id="039e1-161">SAP HANA 데이터베이스에 의해 할당된 메모리 양이 예상보다 높다는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="039e1-162">다음 경고는 높은 메모리 사용량에 문제가 있는 경우 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="039e1-163">호스트 실제 메모리 사용량(경고 1)</span><span class="sxs-lookup"><span data-stu-id="039e1-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="039e1-164">이름 서버의 메모리 사용량(경고 12)</span><span class="sxs-lookup"><span data-stu-id="039e1-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="039e1-165">열 저장소 테이블의 총 메모리 사용량(경고 40)</span><span class="sxs-lookup"><span data-stu-id="039e1-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="039e1-166">서비스의 메모리 사용량(경고 43)</span><span class="sxs-lookup"><span data-stu-id="039e1-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="039e1-167">열 저장소 테이블 중 기본 저장소의 메모리 사용량(경고 45)</span><span class="sxs-lookup"><span data-stu-id="039e1-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="039e1-168">런타임 덤프 파일(경고 46)</span><span class="sxs-lookup"><span data-stu-id="039e1-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="039e1-169">자세한 문제 해결 단계는 [SAP HANA 문제 해결: 메모리 문제](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="039e1-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="039e1-170">**네트워크**</span><span class="sxs-lookup"><span data-stu-id="039e1-170">**Network**</span></span>

<span data-ttu-id="039e1-171">[SAP 참고 사항 #2081065 - SAP HANA 네트워크 문제 해결](https://launchpad.support.sap.com/#/notes/2081065)을 참조하고 이 SAP 참고 사항에 있는 네트워크 문제 해결 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="039e1-172">서버와 클라이언트 간의 왕복 시간을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="039e1-173">A.</span><span class="sxs-lookup"><span data-stu-id="039e1-173">A.</span></span> <span data-ttu-id="039e1-174">SQL 스크립트 [_HANA\_네트워크\_클라이언트_](https://launchpad.support.sap.com/#/notes/1969700)_를 실행합니다._</span><span class="sxs-lookup"><span data-stu-id="039e1-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="039e1-175">노드 간 통신을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-175">Analyze internode communication.</span></span>
  <span data-ttu-id="039e1-176">A.</span><span class="sxs-lookup"><span data-stu-id="039e1-176">A.</span></span> <span data-ttu-id="039e1-177">SQL 스크립트 [_HANA\_네트워크\_서비스_](https://launchpad.support.sap.com/#/notes/1969700)_를 실행합니다._</span><span class="sxs-lookup"><span data-stu-id="039e1-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="039e1-178">Linux 명령 **ifconfig**를 실행합니다(패킷 손실이 발생하는 경우 출력에서 표시).</span><span class="sxs-lookup"><span data-stu-id="039e1-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="039e1-179">Linux 명령 **tcpdump**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="039e1-180">또한 오픈 소스 [IPERF](https://iperf.fr/) 도구(또는 유사한 기능)를 사용하여 실제 응용 프로그램 네트워크 성능을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="039e1-181">자세한 문제 해결 단계는 [SAP HANA 문제 해결: 네트워킹 성능 및 연결 문제](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="039e1-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="039e1-182">**저장소**</span><span class="sxs-lookup"><span data-stu-id="039e1-182">**Storage**</span></span>

<span data-ttu-id="039e1-183">I/O 성능 문제가 있는 경우 최종 사용자의 관점에서 응용 프로그램(또는 전체 시스템)이 느리게 실행되고 응답성이 우수하지 않으며 반응이 없는 것처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="039e1-184">SAP HANA Studio의 **볼륨** 탭에서 연결된 볼륨 및 각 서비스에서 사용하는 볼륨을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![SAP HANA Studio의 [볼륨] 탭에서 연결된 볼륨 및 각 서비스에서 사용하는 볼륨을 확인할 수 있습니다.](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="039e1-186">화면 아래쪽의 [연결된 볼륨]에서 파일 및 I/O 통계와 같은 볼륨의 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![화면 아래쪽의 [연결된 볼륨]에서 파일 및 I/O 통계와 같은 볼륨의 세부 정보를 볼 수 있습니다.](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="039e1-188">자세한 문제 해결 단계는 [SAP HANA 문제 해결: I/O 관련 근본 원인 및 솔루션](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) 및 [SAP HANA 문제 해결: 디스크 관련 근본 원인 및 솔루션](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="039e1-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="039e1-189">**진단 도구**</span><span class="sxs-lookup"><span data-stu-id="039e1-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="039e1-190">HANA\_Configuration\_Minichecks를 통해 SAP HANA 상태 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="039e1-191">이 도구는 SAP HANA Studio에서 이미 경고로 발생했어야 하는 잠재적으로 중요한 기술 문제를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="039e1-192">[SAP 참고 사항 #1969700 - SAP HANA에 대한 SQL 문 컬렉션](https://launchpad.support.sap.com/#/notes/1969700)을 참조하고 참고 사항에 연결된 SQL Statements.zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="039e1-193">로컬 하드 드라이브에서 이.zip 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="039e1-194">SAP HANA Studio의 **시스템 정보** 탭에서 **이름** 열을 마우스 오른쪽 단추로 클릭하고 **가져오기 SQL 문**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![SAP HANA Studio의 [시스템 정보] 탭에서 [이름] 열을 마우스 오른쪽 단추로 클릭하고 [가져오기 SQL 문]을 선택합니다.](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="039e1-196">로컬에 저장된 SQL Statements.zip 파일을 선택하고 해당 SQL 문을 포함한 폴더를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="039e1-197">이 시점에서 이러한 SQL 문으로 다른 여러 진단 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="039e1-198">예를 들어 SAP HANA 시스템 복제 대역폭 요구 사항을 테스트하려면 **복제: 대역폭** 아래에서 **대역폭** 문을 마우스 오른쪽 단추로 클릭하고 SQL 콘솔에서 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="039e1-199">입력 매개 변수(수정 섹션)을 변경한 다음 실행할 수 있도록 전체 SQL 문이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![입력 매개 변수(수정 섹션)을 변경한 다음 실행할 수 있도록 전체 SQL 문이 열립니다.](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="039e1-201">또 다른 예는 **복제: 개요** 아래에서 문을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="039e1-202">상황에 맞는 메뉴에서 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-202">Select **Execute** from the context menu:</span></span>

![또 다른 예는 [복제: 개요] 아래에서 문을 마우스 오른쪽 단추로 클릭합니다.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="039e1-205">그러면 문제 해결에 도움이 되는 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-205">This results in information that helps with troubleshooting:</span></span>

![그러면 문제 해결에 도움이 되는 정보가 표시됩니다.](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="039e1-207">HANA\_Configuration\_Minichecks에 대해 동일한 작업을 수행하고 _C_(위험) 열에서 _X_ 표시를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="039e1-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="039e1-208">샘플 출력:</span><span class="sxs-lookup"><span data-stu-id="039e1-208">Sample outputs:</span></span>

<span data-ttu-id="039e1-209">일반 SAP HANA 검사는 **HANA\_Configuration\_MiniChecks\_Rev102.01+1**.</span><span class="sxs-lookup"><span data-stu-id="039e1-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![일반 SAP HANA 검사는 [HANA\_Configuration\_MiniChecks\_Rev102.01+1].](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="039e1-211">현재 실행 중인 SAP HANA 서비스의 개요는 **HANA\_Services\_Overview**.</span><span class="sxs-lookup"><span data-stu-id="039e1-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![현재 실행 중인 SAP HANA 서비스의 개요는 [HANA\_Services\_Overview].](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="039e1-213">SAP HANA 서비스 정보(CPU, 메모리 등)는 **HANA\_Services\_Statistics**.</span><span class="sxs-lookup"><span data-stu-id="039e1-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="039e1-214">SAP HANA 서비스 정보는 [HANA\_Services\_Statistics].</span><span class="sxs-lookup"><span data-stu-id="039e1-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="039e1-215">SAP HANA 인스턴스에 대한 일반적인 정보는 **HANA\_Configuration\_Overview\_Rev110+**.</span><span class="sxs-lookup"><span data-stu-id="039e1-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![SAP HANA 인스턴스에 대한 일반적인 정보는 [HANA\_Configuration\_Overview\_Rev110+].](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="039e1-217">SAP HANA 매개 변수를 확인하려면 **HANA\_Configuration\_Parameters\_Rev70+**.</span><span class="sxs-lookup"><span data-stu-id="039e1-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![SAP HANA 매개 변수를 확인하려면 [HANA\_Configuration\_Parameters\_Rev70+].](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

