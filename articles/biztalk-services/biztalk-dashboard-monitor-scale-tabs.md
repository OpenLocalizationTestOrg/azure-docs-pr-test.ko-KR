---
title: "BizTalk 서비스의 대시보드, 모니터, 크기 조정, 구성 및 하이브리드 연결 | Microsoft Docs"
description: "대시보드, 모니터, 크기 조정, 구성, 하이브리드 연결 등 BizTalk 서비스에 대한 클래식 포털 탭에서 성능을 제어하고 모니터링하는 방법을 알아봅니다. MABS, WABS"
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
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="f2237-104">대시보드, 모니터, 확장, 구성 및 하이브리드 연결 탭 검토</span><span class="sxs-lookup"><span data-stu-id="f2237-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="f2237-105">BizTalk 서비스를 만들고 응용 프로그램을 배포한 후 BizTalk 서비스 설정 중 일부를 변경하고 응용 프로그램 성능을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="f2237-106">Azure 클래식 포털을 열면 **모든 항목** 탭이 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="f2237-107">BizTalk Service를 보려면 **모든 항목** 탭에서 BizTalk Service를 선택하거나 **BIZTALK Services** 탭을 선택한 후 BizTalk Service 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="f2237-108">그러면 다음 탭이 포함된 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="f2237-109">이 항목에서는 이러한 탭에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="f2237-110">빠른 시작(</span><span class="sxs-lookup"><span data-stu-id="f2237-110">Quickstart (</span></span>![빠른 시작][Quickstart]<span data-ttu-id="f2237-112">)</span><span class="sxs-lookup"><span data-stu-id="f2237-112">)</span></span>
<span data-ttu-id="f2237-113">BizTalk 서비스 버전에 따라 나열된 일부 옵션을 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="f2237-114"><strong>도구 얻기</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="f2237-115">BizTalk 서비스 SDK를 다운로드하여 온-프레미스 개발 컴퓨터에 Visual Studio 프로젝트 템플릿을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="f2237-116">이러한 템플릿은 BizTalk Service에 배포되는 <strong>BizTalk Services</strong>(브리지) 및 <strong>BizTalk Service Artifacts</strong>(변형) Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="f2237-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Azure BizTalk Services SDK로 시작하는 방법</a> 및 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Azure BizTalk Services SDK 설치</a>에서 시작 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="f2237-118"><strong>파트너 규약 만들기</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="f2237-119">Azure에서 호스트되는 Azure BizTalk 서비스 포털을 엽니다. 이 포털에서 파트너를 추가하고 X12, AS2 및 EDIFACT EDI 계약을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="f2237-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services Portal에서 EDI 메시징 구성 요소 구성</a>에서 시작 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="f2237-121"><strong>BizTalk Services에 대한 자세한 정보</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="f2237-122">Azure BizTalk Services에 대해 자세히 알아보려면 <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">학습 센터</a>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="f2237-123">맨 아래에 있는 작업 표시줄에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="f2237-124">응용 프로그램 배포 <strong>관리</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="f2237-125">Azure BizTalk 서비스 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="f2237-126">BizTalk 서비스 포털에서 파트너를 추가하거나 X12, AS2 및 EDIFACT 계약을 만드는 등의 EDI 구성을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="f2237-127">이 메뉴는 <strong>빠른 시작</strong> 탭의 <strong>파트너 계약 만들기</strong>와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="f2237-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services Portal에서 EDI 메시징 구성 요소 구성</a>에서 BizTalk Services Portal에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f2237-129">[액세스 제어 네임스페이스]의 <strong>연결 정보</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="f2237-130">연결 정보를 선택하면 액세스 제어 네임스페이스, 기본 발급자 및 기본 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="f2237-131">이러한 값은 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="f2237-132">또한 액세스 제어 포털을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="f2237-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">액세스 제어 네임 스페이스 만들기</a>에서 Access Control Portal에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f2237-134">[저장소 계정]의 <strong>동기화 키</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="f2237-135">저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="f2237-136">이러한 암호화 키는 저장소 계정에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="f2237-137">BizTalk 서비스는 자동으로 기본 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="f2237-138">사용자는 <strong>동기화 키</strong>를 통해 BizTalk Service를 중단하지 않고 [기본 키]와 [보조 키] 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="f2237-139">예를 들어 BizTalk 서비스에서 저장소 계정의 새로운 기본 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="f2237-140">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="f2237-141">[BizTalk Service]를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f2237-142">보조 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-142">Select the Secondary Key.</span></span> <span data-ttu-id="f2237-143">이 작업을 수행하면 BizTalk 서비스에서 보조 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="f2237-144">Azure 클래식 포털에서 저장소 계정을 선택하고 기본 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="f2237-145">BizTalk 서비스에서 보조 키를 사용하고 있다는 점에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="f2237-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="f2237-146">[BizTalk Service]를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f2237-147">이제 기본 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-147">Now, select the Primary Key.</span></span> <span data-ttu-id="f2237-148">이 키는 앞서 다시 생성한 새로운 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="f2237-149">Azure 클래식 포털에서 저장소 계정을 선택하고 보조 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="f2237-150">이 프로세스를 "키 롤오버"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-150">This process is called "rollover keys".</span></span> <span data-ttu-id="f2237-151">이 프로세스의 목적은 사용자가 BizTalk 서비스를 중단하지 않고 기본 키와 보조 키 간에 전환할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f2237-152">응용 프로그램 <strong>삭제</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="f2237-153">삭제를 선택하면 BizTalk 서비스와 해당 서비스에 배포된 모든 항목이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="f2237-154">대시보드</span><span class="sxs-lookup"><span data-stu-id="f2237-154">Dashboard</span></span>
<span data-ttu-id="f2237-155">BizTalk 서비스 버전에 따라 나열된 일부 옵션을 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="f2237-156">BizTalk 서비스 이름을 선택하면 대시보드 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="f2237-157">대시보드에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="f2237-158">사용 개요: 사용한 하이브리드 연결 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="f2237-159">또한 데이터 사용량(GB)도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="f2237-160">메트릭 그래프: 성능 메트릭의 고정 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="f2237-161">이러한 메트릭은 BizTalk 서비스 상태와 관련된 실시간 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="f2237-162">또한 그래프에 표시되는 메트릭의 **상대** 또는 **절대** 값과 시간 범위 **간격**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="f2237-163">이러한 성능 메트릭에 대한 설명은 이 항목의 [사용 가능한 메트릭](#Metrics) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2237-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="f2237-164">간략 상태: BizTalk 서비스 속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="f2237-165"><strong>추적 데이터베이스 자격 증명 업데이트</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="f2237-166">추적 데이터베이스에 로그인하는 데 사용하는 사용자 이름 및 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-167"><strong>SSL 인증서 업데이트</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="f2237-168">다른 SSL 인증서를 사용하도록 BizTalk 서비스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="f2237-169"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">BizTalk Service를 만들</a> 때는 자체 서명된 SSL 인증서가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-170"><strong>인증서 다운로드</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="f2237-171">BizTalk 서비스에서 사용하는 SSL 인증서를 로컬 컴퓨터에 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-172"><strong>상태</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="f2237-173">BizTalk 서비스의 현재 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="f2237-174"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: 서비스 상태 차트</a>를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="f2237-175"><strong>서비스 URL</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="f2237-176">BizTalk 서비스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="f2237-177">이는 [BizTalk Service]를 만들 때 입력한 <strong>도메인 URL</strong>과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-178"><strong>공용 VIP(가상 IP) 주소</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="f2237-179">BizTalk 서비스에 할당된 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="f2237-180">이는 모든 입력 끝점에 사용되며 아웃바운드 트래픽의 원본 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="f2237-181">이 IP 주소는 만들어진 상태에서는 BizTalk 서비스에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="f2237-182">BizTalk 서비스를 삭제하면 IP 주소가 다른 BizTalk 서비스에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-183"><strong>ACS 네임스페이스</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="f2237-184">BizTalk 서비스로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-185"><strong>에디션</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="f2237-186">BizTalk 서비스를 만들 때 입력한 버전을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-187"><strong>위치</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="f2237-188">BizTalk 서비스를 호스트하는 지리적 지역을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-189"><strong>생성일</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="f2237-190">BizTalk 서비스를 만든 날짜 및 시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-191"><strong>추적 데이터베이스</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="f2237-192">BizTalk 서비스에 사용되는 추적 테이블을 저장하는 Azure SQL 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="f2237-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">요구 사항 설명</a>에서는 [추적 데이터베이스]에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-194"><strong>모니터링/보관 저장소</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="f2237-195">BizTalk 서비스에 대한 모니터링 출력을 저장하는 Azure 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="f2237-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">요구 사항 설명</a>에서는 저장소 계정에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-197"><strong>구독 이름</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="f2237-198">BizTalk 서비스를 호스트하는 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="f2237-199">구독은 Azure 클래식 포털에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-200"><strong>구독 ID</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="f2237-201">구독을 만들 때 구독 ID가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="f2237-202">REST API를 사용할 경우 구독 ID를 입력해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="f2237-203">[BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전](http://go.microsoft.com/fwlink/p/?LinkID=302280) 에 BizTalk 서비스를 만드는 단계가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="f2237-204">작업 표시줄의 관리, 연결 정보, 동기화 키 및 삭제:</span><span class="sxs-lookup"><span data-stu-id="f2237-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="f2237-205">응용 프로그램 배포 <strong>관리</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="f2237-206">Azure BizTalk 서비스 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="f2237-207">BizTalk 서비스 포털에서 파트너를 추가하거나 X12, AS2 및 EDIFACT 계약을 만드는 등의 EDI 구성을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="f2237-208">이 메뉴는 <strong>빠른 시작</strong> 탭의 <strong>파트너 계약 만들기</strong>와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="f2237-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services Portal에서 EDI 메시징 구성 요소 구성</a>에서 BizTalk Services Portal에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-210">[액세스 제어 네임스페이스]의 <strong>연결 정보</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="f2237-211">액세스 제어 네임스페이스, 기본 발급자 및 기본 키를 표시하며, 이러한 항목을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="f2237-212">또한 액세스 제어 포털을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="f2237-213">이 액세스 제어 포털은 왼쪽 탐색 창에서 Active Directory 옵션을 사용하는 경우와 동일한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="f2237-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">ACS 네임 스페이스 관리</a>에서 Access Control Portal에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-215">[저장소 계정]의 <strong>동기화 키</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="f2237-216">저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="f2237-217">이러한 암호화 키는 저장소 계정에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="f2237-218">BizTalk 서비스는 자동으로 기본 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="f2237-219">사용자는 <strong>동기화 키</strong>를 통해 BizTalk Service를 중단하지 않고 [기본 키]와 [보조 키] 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="f2237-220">예를 들어 BizTalk 서비스에서 저장소 계정의 새로운 기본 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="f2237-221">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="f2237-222">[BizTalk Service]를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f2237-223">보조 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-223">Select the Secondary Key.</span></span> <span data-ttu-id="f2237-224">이 작업을 수행하면 BizTalk 서비스에서 보조 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="f2237-225">Azure 클래식 포털에서 저장소 계정을 선택하고 기본 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="f2237-226">BizTalk 서비스에서 보조 키를 사용하고 있다는 점에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="f2237-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="f2237-227">[BizTalk Service]를 선택하고 <strong>동기화 키</strong>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="f2237-228">이제 기본 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-228">Now, select the Primary Key.</span></span> <span data-ttu-id="f2237-229">이 키는 앞서 다시 생성한 새로운 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="f2237-230">Azure 클래식 포털에서 저장소 계정을 선택하고 보조 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="f2237-231">이 프로세스를 "키 롤오버"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-231">This process is called "rollover keys".</span></span> <span data-ttu-id="f2237-232">이 프로세스의 목적은 사용자가 BizTalk 서비스를 중단하지 않고 기본 키와 보조 키 간에 전환할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f2237-233">응용 프로그램 <strong>삭제</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="f2237-234">BizTalk 서비스와 이 서비스에 배포된 모든 항목이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="f2237-235">모니터</span><span class="sxs-lookup"><span data-stu-id="f2237-235">Monitor</span></span>
<span data-ttu-id="f2237-236">Free Edition에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="f2237-237">BizTalk 서비스 이름을 선택하면 다음 항목이 표시된 모니터 탭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="f2237-238">메트릭 그래프: 선택한 성능 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="f2237-239">이러한 메트릭은 BizTalk 서비스 상태와 관련된 실시간 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="f2237-240">표시할 성능 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="f2237-241">최대 6개의 성능 메트릭을 동시에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="f2237-242">또한 표시되는 메트릭의 **상대** 또는 **절대** 값과 시간 범위 **간격**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="f2237-243">그래프에서 메트릭을 제거하거나 표시하려면</span><span class="sxs-lookup"><span data-stu-id="f2237-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="f2237-244">**모니터** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="f2237-245">작업 표시줄에서 다음과 같은 **메트릭 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="f2237-246">![메트릭 추가 선택][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="f2237-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="f2237-247">표시할 성능 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="f2237-248">확인 표시를 선택하여 **모니터** 탭으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="f2237-249">메트릭 옆에 있는 원을 선택하여 그래프에 메트릭 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="f2237-250">예를 들어 다음과 같이 **CPU 사용량** 메트릭이 회색으로 표시되며, 이 메트릭의 출력은 그래프에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="f2237-251">![CPU 사용량 메트릭이 회색으로 표시됨][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="f2237-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="f2237-252">**CPU 사용량** 메트릭의 출력을 그래프에 표시하려면 다음과 같이 회색으로 표시된 원을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="f2237-253">![CPU 사용량 메트릭 사용][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="f2237-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="f2237-254">디스플레이 그래프 및 목록에서 메트릭을 제거하려면 작업 표시줄에서 **메트릭 삭제** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="f2237-255">목록에 메트릭을 다시 추가하려면 작업 표시줄에서 **메트릭 추가**를 선택하고 메트릭을 선택한 후 확인 표시를 선택하여 **모니터** 탭으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="f2237-256">회색으로 표시된 원을 선택하면 해당 메트릭이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="f2237-257"><a name="Metrics"></a>사용 가능한 메트릭</span><span class="sxs-lookup"><span data-stu-id="f2237-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="f2237-258">다음 성능 카운터/메트릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="f2237-259"><strong>왕복 대기 시간</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="f2237-260">메시지를 받은 시간부터 BizTalk 서비스가 모든 브리지에 걸쳐 메시지를 완전히 처리할 때까지 메시지를 처리하는 데 걸린 평균 시간을 밀리초(ms) 단위로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="f2237-261">성공적으로 처리된 메시지만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="f2237-262">다음 이벤트가 발생할 경우 타임스탬프가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="f2237-263">메시지가 게이트웨이에 들어오는 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="f2237-264">메시지가 대상으로 라우팅되는 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="f2237-265">대상 응답을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-265">Destination response is received</span></span></li>
<li><span data-ttu-id="f2237-266">대상 확인 응답이 게이트웨이에 전송된 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="f2237-267">이 메트릭은 다음 계산의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="f2237-268">[대상 확인 응답이 게이트웨이에 전송된 시간] - [메시지가 게이트웨이에 들어온 시간]</span><span class="sxs-lookup"><span data-stu-id="f2237-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-269"><strong>원본에서 실패</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="f2237-270">원본 끝점에서 메시지를 끌어올 때 BizTalk 서비스에서 실패한 총 메시지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-271"><strong>CPU 사용량</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="f2237-272">모든 역할 인스턴스의 평균 프로세서 시간 백분율을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-273"><strong>처리 대기 시간</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="f2237-274">BizTalk 서비스가 모든 브리지에 걸쳐 메시지를 처리하는 데 걸린 평균 시간을 밀리초(ms)로 표시합니다. 단, 대상에서 소요된 시간은 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="f2237-275">성공적으로 처리된 메시지만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="f2237-276">다음 이벤트가 발생할 경우 타임스탬프가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="f2237-277">메시지가 게이트웨이에 들어오는 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="f2237-278">메시지가 대상으로 라우팅되는 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="f2237-279">대상 응답을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-279">Destination response is received</span></span></li>
<li><span data-ttu-id="f2237-280">대상 확인 응답이 게이트웨이에 전송된 경우</span><span class="sxs-lookup"><span data-stu-id="f2237-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="f2237-281">이 메트릭은 다음 계산의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="f2237-282">[대상 확인 응답이 게이트웨이에 전송된 시간] - [메시지가 게이트웨이에 들어온 시간] - [대상 응답을 받은 시간] + [메시지가 대상으로 라우팅된 시간]</span><span class="sxs-lookup"><span data-stu-id="f2237-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-283"><strong>처리 중 실패</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="f2237-284">BizTalk 서비스가 일정 시간 간격 내에 모든 브리지에 걸쳐 메시지를 처리하는 동안 실패한 총 메시지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-285"><strong>전송된 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="f2237-286">BizTalk 서비스가 일정 시간 간격 내에 모든 브리지에 걸쳐 전송한 총 메시지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="f2237-287">이 메트릭은 파이프라인에서 전송된 메시지가 경로 대상에 도달할 때 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="f2237-288">이 메트릭이 메시지가 성공적으로 처리되었음을 나타내지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="f2237-289">요청-회신 시나리오에서, 경로 대상이 수신 확인을 파이프라인에 다시 보낼 때 이 메트릭이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-290"><strong>수신된 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="f2237-291">BizTalk 서비스가 일정 시간 간격 내에 모든 브리지에 걸쳐 받은 총 메시지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="f2237-292">이 메트릭은 파이프라인에서 새 메시지를 수신할 때 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-293"><strong>진행 중 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="f2237-294">BizTalk 서비스가 일정 시간 간격 내에 처리 중인 총 메시지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f2237-295"><strong>처리된 메시지</strong></span><span class="sxs-lookup"><span data-stu-id="f2237-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="f2237-296">BizTalk 서비스가 일정 시간 간격 내에 모든 브리지에 걸쳐 성공적으로 처리한 총 메시지 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="f2237-297">이 메트릭은 파이프라인에서 메시지를 성공적으로 수신하여 대상으로 라우팅할 때 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="f2237-298">확장</span><span class="sxs-lookup"><span data-stu-id="f2237-298">Scale</span></span>
<span data-ttu-id="f2237-299">크기 조정 탭에서 BizTalk 서비스에 사용되는 단위 수를 추가하거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="f2237-300">기본적으로 한 개의 단위가 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="f2237-301">단위를 더 추가하여 BizTalk 서비스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="f2237-302">크기를 늘리면 처리량을 늘리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="f2237-303">배포된 브리지, 계약, LOB 연결, 처리 능력 등 리소스의 양도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="f2237-304">예를 들어 1단위에서 2단위로 크기를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="f2237-305">이 경우 브리지 수, 계약, LOB 연결, 처리 기능을 두 배로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="f2237-306">일부 BizTalk 버전에서는 크기 조정 옵션을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="f2237-307">이 경우 1 단위가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="f2237-308">사용 중인 버전에서 크기 조정할 수 있는 단위 수를 확인하려면 [BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2237-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="f2237-309">단위 수를 늘리면 가격이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="f2237-310">단위를 늘리고 **저장** 을 선택하면 청구 금액이 달라질 수 있다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="f2237-311">그런 다음 계속하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-311">You then choose to continue.</span></span> <span data-ttu-id="f2237-312">단위 수를 늘리면 BizTalk 서비스 상태가 활성에서 업데이트 중으로 변합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="f2237-313">업데이트 중 상태에서도 BizTalk 서비스는 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="f2237-314">[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md) 에 “단위"가 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="f2237-315">구성</span><span class="sxs-lookup"><span data-stu-id="f2237-315">Configure</span></span>
<span data-ttu-id="f2237-316">하이브리드 연결에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="f2237-317">백업 상태를 없음 또는 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="f2237-318">없음으로 설정하면 백업이 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="f2237-319">자동으로 설정한 경우에는 백업 위치, 백업 빈도 및 백업 파일을 유지할 기간을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="f2237-320">[BizTalk 서비스: 백업 및 복원](biztalk-backup-restore.md) 에 자세한 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="f2237-321"><a name="HybridConnections"></a>하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="f2237-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="f2237-322">[하이브리드 연결]은 Azure 응용 프로그램(예: Azure App Service의 Web Apps 또는 Mobile Apps)을 정적 TCP 포트를 사용하는 온-프레미스 리소스(예: SQL Server, MySQL, HTTP 웹 API 및 대부분의 사용자 지정 웹 서비스)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="f2237-323">[하이브리드 연결]은 Azure 클래식 포털의 BizTalk Services에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="f2237-324">Azure App Service에서 [하이브리드 연결]을 만들려면 [Azure App Service에서하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스](../app-service-web/web-sites-hybrid-connection-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2237-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="f2237-325">Azure BizTalk 서비스에서 하이브리드 연결을 만들거나 관리하려면 [하이브리드 연결](integration-hybrid-connection-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2237-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="f2237-326">다음</span><span class="sxs-lookup"><span data-stu-id="f2237-326">Next</span></span>
<span data-ttu-id="f2237-327">여러 탭을 살펴봤으므로 다음과 같은 Azure BizTalk 서비스 기능에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2237-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="f2237-328">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="f2237-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="f2237-329">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="f2237-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="f2237-330">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="f2237-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="f2237-331">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f2237-331">See Also</span></span>
* [<span data-ttu-id="f2237-332">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="f2237-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="f2237-333">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="f2237-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="f2237-334">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="f2237-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="f2237-335">BizTalk 서비스: BizTalk 서비스 상태 차트</span><span class="sxs-lookup"><span data-stu-id="f2237-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="f2237-336">Azure BizTalk 서비스 SDK로 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2237-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

