---
title: "맵 솔루션 aaaService 데모 진도 맞추어 학습 자체 | Microsoft Docs"
description: "서비스 맵을에 OMS Operations Management Suite () Windows에서 응용 프로그램 구성 요소를 자동으로 검색 하는 솔루션 이며 Linux 시스템 및 지도 hello 서비스 간의 통신 합니다.  서비스 맵을 tooidentify를 사용 하 여 안내 하 고 웹 응용 프로그램에서 시뮬레이션 된 문제를 진단 하는 자체 진도 데모입니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a><span data-ttu-id="a076a-104">OMS(Operations Management Suite) 자가 진행식 데모 - 서비스 맵</span><span class="sxs-lookup"><span data-stu-id="a076a-104">Operations Management Suite (OMS) self paced demo - Service Map</span></span>
<span data-ttu-id="a076a-105">이 hello를 사용 하 여 안내 하는 자체 진도 데모 [서비스 맵 솔루션](operations-management-suite-service-map.md) tooidentify Operations Management Suite (OMS)에서 웹 응용 프로그램에서 시뮬레이션 된 문제를 진단 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-105">This is a self paced demo that walks through using hello [Service Map solution](operations-management-suite-service-map.md) in Operations Management Suite (OMS) tooidentify and diagnose a simulated problem in a web application.</span></span>  <span data-ttu-id="a076a-106">Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색 하는 서비스 지도 및 지도 hello 서비스 간의 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-106">Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span>  <span data-ttu-id="a076a-107">다른 OMS 서비스 tooassist에 의해 수집 된 데이터 통합 되어에서 성능을 분석 하 고 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-107">It also consolidates data collected by other OMS services tooassist you in analyzing performance and identifying issues.</span></span>  <span data-ttu-id="a076a-108">또한 사용 [로그 분석 검색 로그인](../log-analytics/log-analytics-log-searches.md) 순서 tooidentify hello 루트 문제가에 수집 된 데이터에 다운 toodrill 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-108">You'll also use [log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) toodrill down on collected data in order tooidentify hello root problem.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a076a-109">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a076a-109">Scenario description</span></span>
<span data-ttu-id="a076a-110">방금 hello ACME 고객 포털 응용 프로그램은 데 성능 문제가 알림을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-110">You've just received a notification that hello ACME Customer Portal application is having performance issues.</span></span>  <span data-ttu-id="a076a-111">hello 해야 하는 유일한 정보는 이러한 문제에 대 한 정보 4시 am PST 오늘 시작 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-111">hello only information that you have is that these issues started about 4:00 am PST today.</span></span>  <span data-ttu-id="a076a-112">Hello에 대 한 구성 요소를 모두 완전히 확실 하지 않은 hello 포털이 아닌 웹 서버 집합에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-112">You aren't entirely sure of all hello components that hello portal is dependent on other than a set of web servers.</span></span>  

## <a name="components-and-features-used"></a><span data-ttu-id="a076a-113">사용된 구성 요소 및 기능</span><span class="sxs-lookup"><span data-stu-id="a076a-113">Components and features used</span></span>
- [<span data-ttu-id="a076a-114">서비스 맵 솔루션</span><span class="sxs-lookup"><span data-stu-id="a076a-114">Service Map solution</span></span>](operations-management-suite-service-map.md)
- [<span data-ttu-id="a076a-115">Log Analytics 로그 검색</span><span class="sxs-lookup"><span data-stu-id="a076a-115">Log Analytics log searches</span></span>](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a><span data-ttu-id="a076a-116">방법 설명</span><span class="sxs-lookup"><span data-stu-id="a076a-116">Walk through</span></span>

### <a name="1-connect-toohello-oms-experience-center"></a><span data-ttu-id="a076a-117">1. Toohello OMS 환경 센터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-117">1. Connect toohello OMS Experience Center</span></span>
<span data-ttu-id="a076a-118">이 연습을 hello를 사용 하 여 [Operations Management Suite 경험 센터](https://experience.mms.microsoft.com/) 샘플 데이터로 완벽 한 OMS 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-118">This walk through uses hello [Operations Management Suite Experience Center](https://experience.mms.microsoft.com/) which provides a complete OMS environment with sample data.</span></span> <span data-ttu-id="a076a-119">이 링크를 수행 하 여 시작을 정보를 입력 한 다음 hello를 선택 **정보 및 분석** 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-119">Start by following this link, provide your information and then select hello **Insight and Analytics** scenario.</span></span>


### <a name="2-start-service-map"></a><span data-ttu-id="a076a-120">2. 서비스 맵 시작</span><span class="sxs-lookup"><span data-stu-id="a076a-120">2. Start Service Map</span></span>
<span data-ttu-id="a076a-121">Hello를 클릭 하 여 hello 서비스 맵을 솔루션 시작 **서비스 맵을** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-121">Start hello Service Map solution by clicking on hello **Service Map** tile.</span></span>

![서비스 맵 타일](media/operations-management-suite-walkthrough-servicemap/tile.png)

<span data-ttu-id="a076a-123">hello 서비스 맵 콘솔이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-123">hello Service Map console is displayed.</span></span>  <span data-ttu-id="a076a-124">Hello 왼쪽된 창에는 hello 서비스 맵 에이전트가 설치 되어 있는 환경에서 컴퓨터의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-124">In hello left pane is a list of computers in your environment with hello Service Map agent installed.</span></span>  <span data-ttu-id="a076a-125">이 목록에서 tooview hello 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-125">You'll select hello computer that you want tooview from this list.</span></span>

![컴퓨터 목록](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a><span data-ttu-id="a076a-127">3. 컴퓨터 보기</span><span class="sxs-lookup"><span data-stu-id="a076a-127">3. View computer</span></span>
<span data-ttu-id="a076a-128">적절 한 위치 toostart 언뜻 하므로 AcmeWFE001 및 AcmeWFE002, hello 웹 서버 라고는 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-128">We know that hello web servers are called AcmeWFE001 and AcmeWFE002, so this seems like a reasonable place toostart.</span></span>  <span data-ttu-id="a076a-129">**AcmeWFE001**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-129">Click on **AcmeWFE001**.</span></span>  <span data-ttu-id="a076a-130">Hello AcmeWFE001에 대 한 맵과 모든 종속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-130">This displays hello map for AcmeWFE001 and all of its dependencies.</span></span>  <span data-ttu-id="a076a-131">어느 프로세스가 및 hello 선택한 컴퓨터에서 실행 중인 나타나면 외부 서비스와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-131">You can see which processes are running on hello selected computer and which external services they communicate with.</span></span>

![웹 서버](media/operations-management-suite-walkthrough-servicemap/web-server.png)

<span data-ttu-id="a076a-133">웹의 hello 성능에 관심이 있기 hello에 응용 프로그램 이므로 클릭 **AcmeAppPool (IIS 응용 프로그램 풀)** 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-133">We're concerned about hello performance of our web application so click on hello **AcmeAppPool (IIS App Pool)** process.</span></span>  <span data-ttu-id="a076a-134">이 프로세스에 대 한 hello 세부 정보를 표시 하 고 해당 종속성을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-134">This displays hello details for this process and highlights its dependencies.</span></span>  

![앱 풀](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a><span data-ttu-id="a076a-136">4. 기간 변경</span><span class="sxs-lookup"><span data-stu-id="a076a-136">4. Change time window</span></span>

<span data-ttu-id="a076a-137">Hello 문제는 이제 오전 4 시에 시작 된 당시에 일어나 살펴보고이 많았습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-137">We heard that hello problem started at 4:00 AM so let's have a look at what was happening at that time.</span></span> <span data-ttu-id="a076a-138">클릭 **시간 범위** hello 시간 too4 변경: 00 AM PST (유지 hello 현재 날짜와 현지 표준 시간대에 대 한 조정) 기간은 20 분입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-138">Click on **Time Range** and change hello time too4:00 AM PST (keep hello current date and adjust for your local time zone) with a duration of 20 minutes.</span></span>

![시간 선택](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a><span data-ttu-id="a076a-140">5. 경고 보기</span><span class="sxs-lookup"><span data-stu-id="a076a-140">5. View alert</span></span>

<span data-ttu-id="a076a-141">이제 해당 hello를 보면 **acmetomcat** 우리의 잠재적인 문제 때문 종속성에 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-141">We now see that hello **acmetomcat** dependency has an alert displayed, so that's our potential problem.</span></span>  <span data-ttu-id="a076a-142">Hello에 경고 아이콘을 클릭 **acmetomcat** tooshow hello hello 경고 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-142">Click on hello alert icon in **acmetomcat** tooshow hello details for hello alert.</span></span>  <span data-ttu-id="a076a-143">여기서 중요한 CPU 사용률을 확인하고 자세한 내용을 보기 위해 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-143">We can see that we have critical CPU utilization and can expand it for more detail.</span></span>  <span data-ttu-id="a076a-144">이 때문에 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-144">This is probably what's causing our slow performance.</span></span> 

![경고](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a><span data-ttu-id="a076a-146">6. 성능 보기</span><span class="sxs-lookup"><span data-stu-id="a076a-146">6. View performance</span></span>

<span data-ttu-id="a076a-147">**acmetomcat**을 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-147">Let's have a closer look at **acmetomcat**.</span></span>  <span data-ttu-id="a076a-148">Hello에 클릭의 오른쪽 위 **acmetomcat** 선택 **서버 맵 로드** tooshow hello 세부 데이터와이 컴퓨터에 대 한 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-148">Click in hello top right of **acmetomcat** and select **Load Server Map** tooshow hello detail and dependencies for this machine.</span></span> <span data-ttu-id="a076a-149">찾을 수 있습니다 다음 좀 더 이러한 성능 카운터 tooverify에 우리의 하려고 한다고 의심 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-149">We can then look a bit more into those performance counters tooverify our suspicion.</span></span>  <span data-ttu-id="a076a-150">선택 hello **성능** 탭 toodisplay hello [로그 분석에서 성능 카운터를 수집](../log-analytics/log-analytics-data-sources-performance-counters.md) hello 시간 범위 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-150">Select hello **Performance** tab toodisplay hello [performance counters collected by Log Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) over hello time range.</span></span>  <span data-ttu-id="a076a-151">정기적인 급격히 증가 하는 hello 프로세서 및 메모리를 가져오기 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-151">We can see that we're getting periodic spikes in hello processor and memory.</span></span>

![성능](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a><span data-ttu-id="a076a-153">7. 변경 내용 추적 보기</span><span class="sxs-lookup"><span data-stu-id="a076a-153">7. View change tracking</span></span>
<span data-ttu-id="a076a-154">이 높은 사용률을 일으킨 원인을 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-154">Let's see if we can find out what might have caused this high utilization.</span></span>  <span data-ttu-id="a076a-155">Hello 클릭 **요약** 탭 합니다.  이 OMS hello 컴퓨터에서와 같은 수집 정보를 연결, 중요 한 알림 및 소프트웨어에 변경 하지 못했습니다. 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-155">Click on hello **Summary** tab.  This provides information that OMS has collected from hello computer such as failed connections, critical alerts, and software changes.</span></span>  <span data-ttu-id="a076a-156">흥미로운 새로운 정보 섹션 확장 되어 해야 하 고 포함 된 기타 섹션 tooinspect 정보를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-156">Sections with interesting recent information should already be expanded, and you can expand other sections tooinspect information that they contain.</span></span>


<span data-ttu-id="a076a-157">**변경 내용 추적**이 열려 있지 않은 경우 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-157">If **Change Tracking** isn't already open, then expand it.</span></span>  <span data-ttu-id="a076a-158">Hello에 의해 수집 된 정보를 표시 하는이 [변경 내용 추적 솔루션](../log-analytics/log-analytics-change-tracking.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-158">This shows information collected by hello [Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span></span>  <span data-ttu-id="a076a-159">이 기간 동안 소프트웨어가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-159">It looks like there was a software change made during this time window.</span></span>  <span data-ttu-id="a076a-160">클릭 **소프트웨어** tooget 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-160">Click on **Software** tooget details.</span></span>  <span data-ttu-id="a076a-161">백업 프로세스는 사용 되 고 hello 과도 한 리소스에 대 한 toobe hello 오류의 원인이이 나타나도록 toohello 컴퓨터 오전 4시 바로 뒤 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-161">A backup process was added toohello machine just after 4:00 AM, so this appears toobe hello culprit for hello excessive resources being consumed.</span></span>

![변경 내용 추적](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a><span data-ttu-id="a076a-163">8. 로그 검색에서 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="a076a-163">8. View details in Log Search</span></span>
<span data-ttu-id="a076a-164">Hello 확인 하 여이 추가로 확인 하기 hello 로그 분석 저장소에 수집 된 성능 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-164">We can further verify this by looking at hello detailed performance information collected in hello Log Analytics repository.</span></span>  <span data-ttu-id="a076a-165">Hello 클릭 **경고** 탭을 다시 hello 중 하나에서 **cpu 사용률이** 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-165">Click on hello **Alerts** tab again and then on one of hello **High CPU** alerts.</span></span>  <span data-ttu-id="a076a-166">**로그 검색에 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-166">Click on  **Show in Log Search**.</span></span>  <span data-ttu-id="a076a-167">이 창을 hello 로그 검색을 수행할 수 있는 [검색 로그](../log-analytics/log-analytics-log-searches.md) hello 저장소에 저장 된 모든 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-167">This opens hello Log Search window where you can perform [log searches](../log-analytics/log-analytics-log-searches.md) against any data stored in hello repository.</span></span>  <span data-ttu-id="a076a-168">서비스 맵을 우리는 queriy 이미 입력에 관심이 tooretrieve hello 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-168">Service Map already filled in a queriy for us tooretrieve hello alert we're interested in.</span></span>  

![로그 검색](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a><span data-ttu-id="a076a-170">9. 저장된 검색 열기</span><span class="sxs-lookup"><span data-stu-id="a076a-170">9. Open saved search</span></span>
<span data-ttu-id="a076a-171">이 경고를 생성 하는 성능 수집-hello에 일부 자세한 내용을 보려면 수 있으며 해당 백업 프로세스 hello 문제의 원인이 되 고 우리의 하려고 한다고 의심 확인할 म 경우 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-171">Let's see if we can get some more detail on hello performance collection that generated this alert and verify our suspicion that hello problems are being caused by that backup process.</span></span>  <span data-ttu-id="a076a-172">Hello 시간 범위에도 변경**6 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-172">Change hello time range too**6 hours**.</span></span>  <span data-ttu-id="a076a-173">클릭 **즐겨찾기** 및 저장 toohello 검색 아래로 스크롤하여 **서비스 맵을**합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-173">Then click on **Favorites** and scroll down toohello saved searches for **Service Map**.</span></span>  <span data-ttu-id="a076a-174">이 분석을 위해 특별히 만들어진 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-174">These are queries that we created specifically for this analysis.</span></span>  <span data-ttu-id="a076a-175">**acmetomcat의 CPU에 따른 상위 5개 프로세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-175">Click on **Top 5 Processes by CPU for acmetomcat**.</span></span>

![저장된 검색](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


<span data-ttu-id="a076a-177">이 쿼리 프로세서에서 사용 하는 상위 5 개 프로세스 hello의 목록을 반환 **acmetomcat**합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-177">This query returns a list of hello top 5 processes consuming processor on **acmetomcat**.</span></span>  <span data-ttu-id="a076a-178">Hello 쿼리 tooget 로그 검색에 사용 되는 소개 toohello 쿼리 언어를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-178">You can inspect hello query tooget an introduction toohello query language used for log searches.</span></span>  <span data-ttu-id="a076a-179">다른 컴퓨터에서 hello 프로세스에 관심이 있다면 해당 정보가 hello 쿼리 tooretrieve를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-179">If you were interested in hello processes on other computers, you could modify hello query tooretrieve that information.</span></span>

<span data-ttu-id="a076a-180">이 경우 hello 백업 프로세스 hello 응용 프로그램 서버의 CPU의 약 60%를 사용 하 고 일관 되 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-180">In this case, we can see that hello backup process is consistently consuming about 60% of hello app server’s CPU.</span></span>  <span data-ttu-id="a076a-181">새 프로세스가 성능 문제의 원인임이 분명합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-181">It's pretty obvious that this new process is responsible for our performance problem.</span></span>  <span data-ttu-id="a076a-182">이 솔루션은이 새로운 tooremove 수 분명히 hello 응용 프로그램에는 서버 소프트웨어를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-182">Our solution would obviously be tooremove this new backup software off hello application server.</span></span>  <span data-ttu-id="a076a-183">실제로 구성 DSC (필요한 상태)이이 프로세스는 이러한 중요 한 시스템에서 실행 되지 않습니다 보장 하는 Azure 자동화 toodefine 정책에 의해 관리 활용 하 여 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-183">We could actually leverage Desired State Configuration (DSC) managed by Azure Automation toodefine policies that ensure this process never runs on these critical systems.</span></span>


## <a name="summary-points"></a><span data-ttu-id="a076a-184">요약 지점</span><span class="sxs-lookup"><span data-stu-id="a076a-184">Summary points</span></span>
- <span data-ttu-id="a076a-185">[서비스 맵](operations-management-suite-service-map.md)은 해당 서버 및 종속성을 모두 알 수 없더라도 전체 응용 프로그램의 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-185">[Service Map](operations-management-suite-service-map.md) provides you with a view of your entire application even if you don't know all of its servers and dependencies.</span></span>
- <span data-ttu-id="a076a-186">서비스 맵 표면 데이터 다른 OMS 솔루션 toohelp를 통해 수집한를 식별 한 경우 문제는 기본 인프라 및 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-186">Service Map surfaces data collected by other OMS solutions toohelp you identify issues with your application and its underlying infrastructure.</span></span>
- <span data-ttu-id="a076a-187">[로그 검색](../log-analytics/log-analytics-log-searches.md) 를 사용 하면 toodrill 아래로 hello 로그 분석 저장소에 수집 된 특정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-187">[Log searches](../log-analytics/log-analytics-log-searches.md) allow you toodrill down into specific data collected in hello Log Analytics repository.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="a076a-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a076a-188">Next steps</span></span>
- <span data-ttu-id="a076a-189">[서비스 맵](operations-management-suite-service-map.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-189">Learn more about [Service Map](operations-management-suite-service-map.md).</span></span>
- <span data-ttu-id="a076a-190">서비스 맵을 [배포 및 구성](operations-management-suite-service-map-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-190">[Deploy and configure](operations-management-suite-service-map-configure.md) Service Map.</span></span>
- <span data-ttu-id="a076a-191">서비스 맵에 필요하고 에이전트에서 저장하는 작업 데이터를 저장하는 [Log Analytics](../log-analytics/log-analytics-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a076a-191">Learn about [Log Analytics](../log-analytics/log-analytics-overview.md) which is required for Service Map and stores operational data stored by agents.</span></span>