---
title: "aaaDashboard, 모니터, 배율, 구성, 및에서 BizTalk 서비스 하이브리드 연결 | Microsoft Docs"
description: "Hello 컨트롤에 대해 알아보고 hello 클래식 포털 탭에서 BizTalk 서비스에 대 한 성능을 모니터링할: 대시보드, 모니터, 크기 조정, 구성 및 하이브리드 연결 합니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="fe029-104">Hello 대시보드, 모니터, 크기 조정, 구성 및 하이브리드 연결 탭 검토</span><span class="sxs-lookup"><span data-stu-id="fe029-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="fe029-105">BizTalk 서비스를 만들고 응용 프로그램을 배포 후 hello BizTalk 서비스 설정 중 일부를 변경할 수 있으며 hello 응용 프로그램 성능을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="fe029-106">Hello Azure 클래식 포털을 열 때 자동으로 hello에 배치 됩니다 **모든 항목이** 탭 tooview hello에서 BizTalk 서비스를 선택 하는 BizTalk 서비스를 **모든 항목** 탭 이나 선택 hello **BIZTALK 서비스** ; 탭 한 다음 BizTalk 서비스 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="fe029-107">다음 탭 hello로 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="fe029-108">이 항목에서는 이러한 탭에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="fe029-109">빠른 시작(</span><span class="sxs-lookup"><span data-stu-id="fe029-109">Quickstart (</span></span>![빠른 시작][Quickstart]<span data-ttu-id="fe029-111">)</span><span class="sxs-lookup"><span data-stu-id="fe029-111">)</span></span>
<span data-ttu-id="fe029-112">Hello BizTalk 서비스 버전에 따라 나열 된 모든 옵션을 사용 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="fe029-113"><strong>Hello 도구 가져오기</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="fe029-114">Hello BizTalk 서비스 SDK tooinstall hello Visual Studio 프로젝트 템플릿 온-프레미스 개발 컴퓨터에 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="fe029-115">이러한 서식 파일 만들기 hello <strong>BizTalk 서비스</strong> (브리지) 및 hello <strong>BizTalk 서비스 아티팩트</strong> 배포 tooyour BizTalk 서비스 (변환) Visual Studio 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="fe029-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Azure BizTalk Services SDK 어떻게 hello 사용 하 여 시작 합니까 </a> 및 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Azure BizTalk Services SDK 설치 hello</a> 목록 hello 단계 tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="fe029-117"><strong>파트너 규약 만들기</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="fe029-118">열립니다는 파트너를 추가 하 고 X12, AS2, 만들 Azure에서 호스팅되는 Azure BizTalk 서비스 포털 hello 및 EDIFACT EDI 규약입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="fe029-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services 포털에서 EDI 메시징에 대 한 구성 요소 구성</a> 목록 hello 단계 tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="fe029-120"><strong>BizTalk Services에 대한 자세한 정보</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="fe029-121">Toohello 이동 <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">학습 센터</a> toolearn Azure BizTalk 서비스에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="fe029-122">Hello 맨 아래에 hello 작업 표시줄에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="fe029-123">응용 프로그램 배포 <strong>관리</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="fe029-124">Hello Azure BizTalk 서비스 포털도를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="fe029-125">BizTalk 서비스 포털 hello는 파트너를 추가 하 고 X12, AS2, 만드는 포함 하 여 hello 입구 tooEDI 구성 및 EDIFACT 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="fe029-126">와 동일 hello은이 <strong>파트너 규약을 만들</strong> hello에 <strong>빠른 시작</strong> 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="fe029-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services 포털에서 EDI 메시징에 대 한 구성 요소 구성</a> hello BizTalk 서비스 포털에 더 많은 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="fe029-128"><strong>연결 정보</strong> 의 액세스 제어 Namespace hello</span><span class="sxs-lookup"><span data-stu-id="fe029-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="fe029-129">연결 정보를 선택 하면 다음 액세스 제어 Namespace, 기본 발급자 hello 하 고 기본 키 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="fe029-130">이러한 값은 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="fe029-131">Hello 액세스 제어 포털을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="fe029-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">액세스 제어 Namespace를 만들</a> hello 액세스 제어 포털에 더 많은 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="fe029-133"><strong>키를 동기화</strong> hello 저장소 계정에</span><span class="sxs-lookup"><span data-stu-id="fe029-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="fe029-134">저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="fe029-135">이러한 암호화 키 저장소 계정 액세스 tooyour를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="fe029-136">BizTalk 서비스는 hello 기본 키를 자동으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="fe029-137"><strong>키를 동기화</strong> hello BizTalk 서비스를 중단시 키 지 않고 사용자가 tooswitch hello 기본 키 및 보조 키 hello 사이 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="fe029-138">예를 들어 hello BizTalk 서비스 toouse hello 저장소 계정에 대 한 새 기본 키를 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="fe029-139">toodo이:</span><span class="sxs-lookup"><span data-stu-id="fe029-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="fe029-140">BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="fe029-141">Hello 보조 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-141">Select hello Secondary Key.</span></span> <span data-ttu-id="fe029-142">이렇게 하면 BizTalk 서비스 hello hello 보조 키를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="fe029-143">Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 기본 키를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="fe029-144">BizTalk 서비스는 hello 보조 키를 사용 하 여 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fe029-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="fe029-145">BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="fe029-146">이제 hello 기본 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="fe029-147">이 hello 새로운 재생성 하는 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="fe029-148">Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 보조 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="fe029-149">이 프로세스를 "키 롤오버"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-149">This process is called "rollover keys".</span></span> <span data-ttu-id="fe029-150">hello 목적은 hello BizTalk 서비스를 중단시 키 지 않고 tooenable 사용자 tooswitch hello 기본 키 및 보조 키 hello 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="fe029-151">응용 프로그램 <strong>삭제</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="fe029-152">선택 하면 BizTalk 서비스를 삭제 하 고 모든 배포 항목 tooit 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="fe029-153">대시보드</span><span class="sxs-lookup"><span data-stu-id="fe029-153">Dashboard</span></span>
<span data-ttu-id="fe029-154">Hello BizTalk 서비스 버전에 따라 나열 된 모든 옵션을 사용 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="fe029-155">BizTalk 서비스 이름을 선택 하면 hello 대시보드 탭이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="fe029-156">대시보드에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="fe029-157">사용 개요: hello 사용 되는 하이브리드 연결 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="fe029-158">또한 gb에서 hello 데이터 사용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="fe029-159">메트릭 그래프: 성능 메트릭의 고정 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="fe029-160">이러한 메트릭은 hello BizTalk 서비스의 hello 상태에 대 한 실시간 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="fe029-161">Hello를 선택할 수도 있습니다 **상대** 또는 **절대** 시간 범위 값과 hello **간격** hello 그래프에 표시 되는 hello 메트릭.</span><span class="sxs-lookup"><span data-stu-id="fe029-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="fe029-162">이러한 성능 메트릭에 대 한 이동 너무[사용 가능한 메트릭](#Metrics) 이 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="fe029-163">간략 상태: BizTalk 서비스 속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="fe029-164"><strong>추적 데이터베이스 자격 증명 업데이트</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="fe029-165">변경 내용을 hello 사용자 이름 및 암호 toolog hello 추적 데이터베이스에 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-166"><strong>SSL 인증서 업데이트</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="fe029-167">Hello BizTalk 서비스 toouse 서로 다른 SSL 인증서를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="fe029-168">자체 서명 된 SSL 인증서를 자동으로 생성 됩니다 있습니다 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">hello BizTalk 서비스 만들기</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-169"><strong>인증서 다운로드</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="fe029-170">BizTalk 서비스 tooa 로컬 컴퓨터에서 사용 하는 hello SSL 인증서를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-171"><strong>상태</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="fe029-172">Hello BizTalk 서비스의 현재 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="fe029-173"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: 서비스 상태 차트</a>를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="fe029-174"><strong>서비스 URL</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="fe029-175">BizTalk 서비스에 대 한 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="fe029-176">Hello로 동일 hello은이 <strong>도메인 URL</strong> BizTalk 서비스를 만들 때 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-177"><strong>공용 VIP(가상 IP) 주소</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="fe029-178">hello IP 주소가 tooyour BizTalk 서비스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="fe029-179">모든 입력된 끝점에 사용 되 고 아웃 바운드 트래픽에 대 한 hello 원본 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="fe029-180">이 IP 주소 생성 될 때 BizTalk 서비스 tooyour를 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="fe029-181">Hello BizTalk 서비스를 삭제 하면 BizTalk 서비스 tooanother hello IP 주소에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-182"><strong>ACS 네임스페이스</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="fe029-183">BizTalk 서비스 hello로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-184"><strong>에디션</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="fe029-185">Hello Edition hello BizTalk 서비스를 만들 때 입력 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-186"><strong>위치</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="fe029-187">표시 hello BizTalk 서비스를 호스팅하는 지역.</span><span class="sxs-lookup"><span data-stu-id="fe029-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-188"><strong>생성일</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="fe029-189">Hello 날짜 및 시간 hello는 표시 합니다. BizTalk 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-190"><strong>추적 데이터베이스</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="fe029-191">BizTalk 서비스에 사용 되는 테이블을 추적 하는 hello를 저장 하는 hello Azure SQL 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="fe029-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">요구 사항 Explained</a> hello 추적 데이터베이스에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-193"><strong>모니터링/보관 저장소</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="fe029-194">BizTalk 서비스의 출력을 모니터링 하는 hello를 저장 하는 hello Azure 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="fe029-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">요구 사항 Explained</a> hello 저장소 계정에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-196"><strong>구독 이름</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="fe029-197">BizTalk 서비스를 호스트 하는 hello 구독을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="fe029-198">hello 구독 액세스 toohello Azure 클래식 포털을 통해 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-199"><strong>구독 ID</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="fe029-200">구독을 만들 때 구독 ID가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="fe029-201">REST Api를 사용 하는 경우 구독 id. tooenter hello 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="fe029-202">[BizTalk 서비스:를 사용 하 여 Azure 클래식 포털을 프로 비전](http://go.microsoft.com/fwlink/p/?LinkID=302280) 목록 hello 단계 toocreate BizTalk 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="fe029-203">연결 정보를 동기화 키를 관리 하 고 hello 작업 표시줄에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="fe029-204">응용 프로그램 배포 <strong>관리</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="fe029-205">Hello Azure BizTalk 서비스 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="fe029-206">BizTalk 서비스 포털 hello는 파트너를 추가 하 고 X12, AS2, 만드는 포함 하 여 hello 입구 tooEDI 구성 및 EDIFACT 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="fe029-207">와 동일 hello은이 <strong>파트너 규약을 만들</strong> hello에 <strong>빠른 시작</strong> 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="fe029-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services 포털에서 EDI 메시징에 대 한 구성 요소 구성</a> hello BizTalk 서비스 포털에 더 많은 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-209"><strong>연결 정보</strong> 의 액세스 제어 Namespace hello</span><span class="sxs-lookup"><span data-stu-id="fe029-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="fe029-210">표시 hello 액세스 제어 Namespace, 기본 발급자 및 기본 키 값이 있습니다. 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="fe029-211">Hello 액세스 제어 포털을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="fe029-212">이 액세스 제어 포털 hello Active Directory 옵션을 사용 하 여 hello 왼쪽된 탐색 창에서 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="fe029-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Your ACS Namespace 관리</a> hello 액세스 제어 포털에 더 많은 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-214"><strong>키를 동기화</strong> hello 저장소 계정에</span><span class="sxs-lookup"><span data-stu-id="fe029-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="fe029-215">저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="fe029-216">이러한 암호화 키 저장소 계정 액세스 tooyour를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="fe029-217">BizTalk 서비스는 hello 기본 키를 자동으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="fe029-218"><strong>키를 동기화</strong> hello BizTalk 서비스를 중단시 키 지 않고 사용자가 tooswitch hello 기본 키 및 보조 키 hello 사이 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="fe029-219">예를 들어 hello BizTalk 서비스 toouse hello 저장소 계정에 대 한 새 기본 키를 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="fe029-220">toodo이:</span><span class="sxs-lookup"><span data-stu-id="fe029-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="fe029-221">BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="fe029-222">Hello 보조 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-222">Select hello Secondary Key.</span></span> <span data-ttu-id="fe029-223">이렇게 하면 BizTalk 서비스 hello hello 보조 키를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="fe029-224">Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 기본 키를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="fe029-225">BizTalk 서비스는 hello 보조 키를 사용 하 여 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fe029-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="fe029-226">BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="fe029-227">이제 hello 기본 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="fe029-228">이 hello 새로운 재생성 하는 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="fe029-229">Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 보조 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="fe029-230">이 프로세스를 "키 롤오버"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-230">This process is called "rollover keys".</span></span> <span data-ttu-id="fe029-231">hello 목적은 hello BizTalk 서비스를 중단시 키 지 않고 tooenable 사용자 tooswitch hello 기본 키 및 보조 키 hello 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="fe029-232">응용 프로그램 <strong>삭제</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="fe029-233">BizTalk 서비스와 모든 배포 항목 tooit 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="fe029-234">모니터</span><span class="sxs-lookup"><span data-stu-id="fe029-234">Monitor</span></span>
<span data-ttu-id="fe029-235">Toohello 적용 되지 않습니다 무료 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="fe029-236">BizTalk 서비스 이름을 선택 하면 hello 모니터 탭 ´ ï ´ 하 고 hello 다음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="fe029-237">메트릭 그래프: 표시 hello 선택한 성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="fe029-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="fe029-238">이러한 메트릭은 hello BizTalk 서비스의 hello 상태에 대 한 실시간 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="fe029-239">표시할 성능 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="fe029-240">최대 6개의 성능 메트릭을 동시에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="fe029-241">Hello를 선택할 수도 있습니다 **상대** 또는 **절대** 시간 범위 값과 hello **간격** 표시 되는 hello 메트릭.</span><span class="sxs-lookup"><span data-stu-id="fe029-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="fe029-242">hello 그래프에 메트릭 tooremove 또는 표시:</span><span class="sxs-lookup"><span data-stu-id="fe029-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="fe029-243">선택 hello **모니터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="fe029-244">선택 **메트릭 추가** hello 작업 표시줄에서:</span><span class="sxs-lookup"><span data-stu-id="fe029-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="fe029-245">![메트릭 추가 선택][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="fe029-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="fe029-246">원하는 toodisplay hello 성능 메트릭을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="fe029-247">Hello 확인 표시 tooreturn toohello 선택 **모니터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="fe029-248">Hello 그래프에 hello 원 다음 toohello 메트릭 toodisplay 해당 메트릭이 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="fe029-249">예를 들어 hello **CPU 사용량** 메트릭을 회색; 출력 hello 그래프에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="fe029-250">![CPU 사용량 메트릭이 회색으로 표시됨][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="fe029-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="fe029-251">Select hello 원 tooenable hello 회색 **CPU 사용량** 메트릭 toodisplay hello 그래프에서 해당 출력:</span><span class="sxs-lookup"><span data-stu-id="fe029-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="fe029-252">![CPU 사용량 메트릭 사용][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="fe029-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="fe029-253">tooremove hello 디스플레이 그래프 및 hello 목록에서 메트릭을 선택 **메트릭을 삭제** hello 작업 표시줄에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="fe029-254">tooadd hello 백 toohello 메트릭 목록에서 **메트릭 추가** hello 작업 표시줄에서 hello 메트릭을 그리고 선택 hello 확인 표시 tooreturn toohello 확인 **모니터** 탭 합니다. Select hello 원 tooenable hello 메트릭을 회색으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="fe029-255"><a name="Metrics"></a>사용 가능한 메트릭</span><span class="sxs-lookup"><span data-stu-id="fe029-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="fe029-256">hello 다음 성능 카운터/메트릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="fe029-257"><strong>왕복 대기 시간</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="fe029-258">데 걸린 시간 (밀리초) (ms) tooprocess 모든 브리지에서 BizTalk 서비스 hello hello 메시지를 완전히 처리 될 때까지 hello 시간 hello 메시지에서 메시지를 수신 하는 hello 평균 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="fe029-259">성공적으로 처리된 메시지만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="fe029-260">이벤트를 수행 하는 hello 발생 하는 경우 타임 스탬프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="fe029-261">메시지가 전달 hello 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="fe029-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="fe029-262">메시지는 라우트된 toohello 대상</span><span class="sxs-lookup"><span data-stu-id="fe029-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="fe029-263">대상 응답을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="fe029-263">Destination response is received</span></span></li>
<li><span data-ttu-id="fe029-264">대상 승인 보낸 응답 toohello 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="fe029-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="fe029-265">이 메트릭은 계산을 수행 하는 hello의 hello 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="fe029-266">[대상 승인 보낸 응답 toohello 게이트웨이]-[메시지가 hello 게이트웨이 전달 하는 데 사용]</span><span class="sxs-lookup"><span data-stu-id="fe029-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-267"><strong>원본에서 실패</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="fe029-268">Hello에 실패 한 메시지의 총 수를 표시 하 여 hello hello 원본 끝점에서 메시지를 끌어오는 경우 BizTalk 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-269"><strong>CPU 사용량</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="fe029-270">모든 역할 인스턴스의 hello 평균 % 프로세서 시간을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-271"><strong>처리 대기 시간</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="fe029-272">Hello hello 시간을 제외한 모든 브리지에서 hello BizTalk 서비스에서 메시지 대상에 소요 된 시간 (밀리초) (ms) tooprocess에서 수행 되는 평균 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="fe029-273">성공적으로 처리된 메시지만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="fe029-274">각 이벤트 뒤 hello 발생 하는 경우 타임 스탬프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="fe029-275">메시지가 전달 hello 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="fe029-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="fe029-276">메시지는 라우트된 toohello 대상</span><span class="sxs-lookup"><span data-stu-id="fe029-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="fe029-277">대상 응답을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="fe029-277">Destination response is received</span></span></li>
<li><span data-ttu-id="fe029-278">대상 승인 보낸 응답 toohello 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="fe029-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="fe029-279">이 메트릭은 계산을 수행 하는 hello의 hello 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="fe029-280">[대상 승인 보낸 응답 toohello 게이트웨이]-[메시지가 전달 게이트웨이 hello]-[대상 응답을 받을] + [메시지 라우팅된 toohello 대상]</span><span class="sxs-lookup"><span data-stu-id="fe029-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-281"><strong>처리 중 실패</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="fe029-282">Hello 총 시간 간격 내에서 모든 hello 브리지에서 hello BizTalk 서비스에서 처리 하는 동안 실패 한 메시지 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-283"><strong>전송된 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="fe029-284">시간 간격 내에서 모든 브리지 hello BizTalk 서비스에서 보낸 메시지의 표시 hello의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="fe029-285">이 메트릭은 파이프라인에서 보낸 메시지 hello 경로 대상에 도달 하는 경우에 증가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="fe029-286">이 메트릭이 메시지가 성공적으로 처리되었음을 나타내지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="fe029-287">요청-회신 시나리오에서 hello 메트릭은 hello 경로 대상에서 수신 승인을 백 toohello 파이프라인을 보낼 때 증가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-288"><strong>수신된 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="fe029-289">시간 간격 내에서 모든 브리지 hello BizTalk 서비스에서 받은 메시지의 표시 hello의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="fe029-290">이 메트릭은 hello 파이프라인에서 새 메시지를 받으면 증가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-291"><strong>진행 중 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="fe029-292">표시 hello 메시지에서 현재 처리 중인 BizTalk 서비스 hello 시간 간격 내에서 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fe029-293"><strong>처리된 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="fe029-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="fe029-294">표시 hello 시간 간격 내에서 모든 브리지 hello BizTalk 서비스에서 성공적으로 처리 하는 메시지의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="fe029-295">이 메트릭은 hello 파이프라인과 toohello 성공적으로 라우팅된 대상으로 메시지를 성공적으로 수신 되 면 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="fe029-296">확장</span><span class="sxs-lookup"><span data-stu-id="fe029-296">Scale</span></span>
<span data-ttu-id="fe029-297">Hello 크기 조정 탭에서 추가 하거나 BizTalk 서비스에 사용 되는 단위 수가 hello 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="fe029-298">기본적으로 한 개의 단위가 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="fe029-299">추가 단위가 tooscale를 추가할 수 있습니다 BizTalk 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="fe029-300">Hello 눈금을 늘리면 처리량이 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="fe029-301">hello 리소스의도 늘어나면 처리 능력 및 배포 된 브리지, 계약, LOB 연결을 포함 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="fe029-302">예를 들어 hello 범위 1 단위 too2 단위에서 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="fe029-303">이 경우 이중 hello 수가 브리지, double hello 계약, double hello LOB 연결 및 이중 hello 처리 능력을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="fe029-304">일부 BizTalk 버전에서는 크기 조정 옵션을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="fe029-305">이 경우 1 단위가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="fe029-306">toodetermine 버전을 확장할 수 있습니다, 단위의 수 참조 너무[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="fe029-307">Hello 단위 수를 늘리면 가격 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="fe029-308">Hello 단위를 늘릴 경우을 선택 하면 **저장** 청구 영향을 받는지 여부를 알려 주는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="fe029-309">Toocontinue을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-309">You then choose toocontinue.</span></span> <span data-ttu-id="fe029-310">Hello 단위 수를 늘리면 활성 tooUpdating에서 hello BizTalk 서비스 상태를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="fe029-311">Hello 업데이트 상태, BizTalk 서비스 toorun를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="fe029-312">[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md) 에 “단위"가 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="fe029-313">구성</span><span class="sxs-lookup"><span data-stu-id="fe029-313">Configure</span></span>
<span data-ttu-id="fe029-314">TooHybrid 연결 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="fe029-315">백업 상태 tooNone hello 또는 자동 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="fe029-316">TooNone, 설정 된 경우 백업이 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="fe029-317">TooAutomatic, 설정 된 경우 hello 백업 위치, hello 백업과 기간 tookeep hello 백업 파일의 hello 빈도 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="fe029-318">[BizTalk 서비스: 백업 및 복원](biztalk-backup-restore.md) hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="fe029-319"><a name="HybridConnections"></a>하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="fe029-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="fe029-320">하이브리드 연결은 Azure 앱 서비스, SQL Server, MySQL, HTTP 웹 Api 가장 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하 여 tooan 온-프레미스 리소스에서에서 모바일 앱 또는 웹 앱과 같은 Azure 응용 프로그램을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="fe029-321">하이브리드 연결은 BizTalk 서비스의 hello Azure 클래식 포털에서에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="fe029-322">Azure 앱 서비스에 하이브리드 연결이 toocreate 참조 [액세스 온-프레미스 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="fe029-323">toocreate Azure BizTalk 서비스에서 하이브리드 연결을 관리, 참조 또는 [하이브리드 연결](integration-hybrid-connection-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="fe029-324">다음</span><span class="sxs-lookup"><span data-stu-id="fe029-324">Next</span></span>
<span data-ttu-id="fe029-325">Hello 다른 탭에 익숙하다면 했으므로 hello Azure BizTalk 서비스 기능에 대 한 더 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe029-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="fe029-326">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="fe029-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="fe029-327">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="fe029-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="fe029-328">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="fe029-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="fe029-329">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fe029-329">See Also</span></span>
* [<span data-ttu-id="fe029-330">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="fe029-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="fe029-331">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="fe029-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="fe029-332">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="fe029-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="fe029-333">BizTalk 서비스: BizTalk 서비스 상태 차트</span><span class="sxs-lookup"><span data-stu-id="fe029-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="fe029-334">Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까</span><span class="sxs-lookup"><span data-stu-id="fe029-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

