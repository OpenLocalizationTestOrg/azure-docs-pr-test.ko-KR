---
title: "aaaCreate 및 하이브리드 연결 관리 | Microsoft Docs"
description: "하이브리드 연결을 toocreate hello 연결을 관리 하 고 hello 하이브리드 연결 관리자를 설치 하는 방법을 알아봅니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a><span data-ttu-id="aad22-104">하이브리드 연결 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="aad22-104">Create and Manage Hybrid Connections</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aad22-105">BizTalk 하이브리드 연결은 사용 중지되고 App Service 하이브리드 연결로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="aad22-106">를 비롯 한 자세한 내용은 toomanage 기존 BizTalk 하이브리드 연결을 확인 하려면 어떻게 해야 [Azure 앱 서비스 하이브리드 연결](../app-service/app-service-hybrid-connections.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-106">For more information, including how toomanage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>


## <a name="overview-of-hello-steps"></a><span data-ttu-id="aad22-107">Hello 단계의 개요</span><span class="sxs-lookup"><span data-stu-id="aad22-107">Overview of hello Steps</span></span>
1. <span data-ttu-id="aad22-108">Hello를 입력 하 여 하이브리드 연결을 만들 **호스트 이름** 또는 **FQDN** 개인 네트워크에 hello 온-프레미스 리소스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-108">Create a Hybrid Connection by entering hello **host name** or **FQDN** of hello on-premises resource in your private network.</span></span>
2. <span data-ttu-id="aad22-109">Azure 웹 앱 또는 Azure 모바일 앱 toohello 하이브리드 연결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-109">Link your Azure web apps or Azure mobile apps toohello Hybrid Connection.</span></span>
3. <span data-ttu-id="aad22-110">온-프레미스 리소스에 대해 hello 하이브리드 연결 관리자를 설치 하 고 연결 toohello 특정 하이브리드 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-110">Install hello Hybrid Connection Manager on your on-premises resource and connect toohello specific Hybrid Connection.</span></span> <span data-ttu-id="aad22-111">Azure 포털 hello 단일 클릭 환경을 tooinstall 제공 하 고 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-111">hello Azure portal provides a single-click experience tooinstall and connect.</span></span>
4. <span data-ttu-id="aad22-112">하이브리드 연결을 관리하고 연결 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-112">Manage Hybrid Connections and their connection keys.</span></span>

<span data-ttu-id="aad22-113">이 항목에서는 이러한 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-113">This topic lists these steps.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="aad22-114">가능한 tooset 하이브리드 연결 끝점 tooan IP 주소는</span><span class="sxs-lookup"><span data-stu-id="aad22-114">It is possible tooset a Hybrid Connection endpoint tooan IP address.</span></span> <span data-ttu-id="aad22-115">IP 주소를 사용 하는 경우 있거나 클라이언트에 따라 hello 온-프레미스 리소스에 도달 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-115">If you use an IP address, you may or may not reach hello on-premises resource, depending on your client.</span></span> <span data-ttu-id="aad22-116">하이브리드 연결 hello DNS 조회를 수행 하는 hello 클라이언트에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-116">hello Hybrid Connection depends on hello client doing a DNS lookup.</span></span> <span data-ttu-id="aad22-117">대부분의 경우에서 hello **클라이언트** 응용 프로그램 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-117">In most cases, hello **client** is your application code.</span></span> <span data-ttu-id="aad22-118">클라이언트에서 DNS 조회를 수행 하지 않습니다, (시도 하지 않습니다 tooresolve hello IP 주소는 도메인 이름 (x.x.x.x) 하는 경우), 경우 hello 다음 hello 하이브리드 연결을 통해 트래픽을 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-118">If hello client does not perform a DNS lookup, (it does not try tooresolve hello IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through hello Hybrid Connection.</span></span>
> 
> <span data-ttu-id="aad22-119">예를 들어, **10.4.5.6** (의사 코드)을 온-프레미스 호스트로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-119">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span></span>
> 
> <span data-ttu-id="aad22-120">**다음 시나리오 작동 hello:**</span><span class="sxs-lookup"><span data-stu-id="aad22-120">**hello following scenario works:**</span></span>  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> <span data-ttu-id="aad22-121">**시나리오를 따르는 hello 작동 하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="aad22-121">**hello following scenario doesn't work:**</span></span>  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <span data-ttu-id="aad22-122"><a name="CreateHybridConnection"></a>하이브리드 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="aad22-122"><a name="CreateHybridConnection"></a>Create a Hybrid Connection</span></span>
<span data-ttu-id="aad22-123">하이브리드 연결을 만들 수 있습니다 hello 웹 응용 프로그램을 사용 하 여 Azure 포털 **또는** BizTalk 서비스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-123">A Hybrid Connection can be created in hello Azure portal using Web Apps **or** using BizTalk Services.</span></span> 

<span data-ttu-id="aad22-124">**웹 앱을 사용 하 여 하이브리드 연결 toocreate**, 참조 [Azure 웹 앱 연결 tooan 온-프레미스 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-124">**toocreate Hybrid Connections using Web Apps**, see [Connect Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span> <span data-ttu-id="aad22-125">또한 기본 hello 메서드인 웹 앱에서 하이브리드 연결 관리자 (HCM) hello를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-125">You can also install hello Hybrid Connection Manager (HCM) from your web app, which is hello preferred method.</span></span> 

<span data-ttu-id="aad22-126">**BizTalk 서비스에 하이브리드 연결이 toocreate**:</span><span class="sxs-lookup"><span data-stu-id="aad22-126">**toocreate Hybrid Connections in BizTalk Services**:</span></span>

1. <span data-ttu-id="aad22-127">Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-127">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="aad22-128">Hello 왼쪽된 탐색 창에서 선택 **BizTalk 서비스** 한 다음 BizTalk 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-128">In hello left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
   
    <span data-ttu-id="aad22-129">기존 BizTalk 서비스가 없는 경우 [BizTalk 서비스를 만들 수](biztalk-provision-services.md)있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-129">If you don't have an existing BizTalk Service, you can [Create a BizTalk Service](biztalk-provision-services.md).</span></span>
3. <span data-ttu-id="aad22-130">선택 hello **하이브리드 연결** 탭:</span><span class="sxs-lookup"><span data-stu-id="aad22-130">Select hello **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="aad22-131">![하이브리드 연결 탭][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="aad22-131">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="aad22-132">선택 **하이브리드 연결을 만들** 또는 선택 hello **추가** hello 작업 표시줄에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-132">Select **Create a Hybrid Connection** or select hello **ADD** button in hello task bar.</span></span> <span data-ttu-id="aad22-133">Hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-133">Enter hello following:</span></span>
   
   | <span data-ttu-id="aad22-134">속성</span><span class="sxs-lookup"><span data-stu-id="aad22-134">Property</span></span> | <span data-ttu-id="aad22-135">설명</span><span class="sxs-lookup"><span data-stu-id="aad22-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="aad22-136">이름</span><span class="sxs-lookup"><span data-stu-id="aad22-136">Name</span></span> |<span data-ttu-id="aad22-137">hello 하이브리드 연결 이름은 고유 해야 하며 hello 수 없습니다 이름이 hello BizTalk 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-137">hello Hybrid Connection name must be unique and cannot be hello same name as hello BizTalk Service.</span></span> <span data-ttu-id="aad22-138">어떤 이름을 입력해도 괜찮지만 용도에 맞는 구체적인 이름을 입력하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-138">You can enter any name but be specific with its purpose.</span></span> <span data-ttu-id="aad22-139">이러한 예로 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-139">Examples include:</span></span><br/><br/><span data-ttu-id="aad22-140">Payroll*SQLServer*</span><span class="sxs-lookup"><span data-stu-id="aad22-140">Payroll*SQLServer*</span></span><br/><span data-ttu-id="aad22-141">SupplyList*SharepointServer*</span><span class="sxs-lookup"><span data-stu-id="aad22-141">SupplyList*SharepointServer*</span></span><br/><span data-ttu-id="aad22-142">Customers*OracleServer*</span><span class="sxs-lookup"><span data-stu-id="aad22-142">Customers*OracleServer*</span></span> |
   | <span data-ttu-id="aad22-143">호스트 이름</span><span class="sxs-lookup"><span data-stu-id="aad22-143">Host Name</span></span> |<span data-ttu-id="aad22-144">Hello 호스트 이름만 hello 정규화 된 호스트 이름을 입력 하거나 hello hello 온-프레미스 리소스의 IPv4 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-144">Enter hello fully qualified host name, only hello host name, or hello IPv4 address of hello on-premises resource.</span></span> <span data-ttu-id="aad22-145">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-145">Examples include:</span></span><br/><br/><span data-ttu-id="aad22-146">mySQLServer</span><span class="sxs-lookup"><span data-stu-id="aad22-146">mySQLServer</span></span><br/><span data-ttu-id="aad22-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="aad22-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span></span><br/><span data-ttu-id="aad22-148">*myHTTPSharePointServer*</span><span class="sxs-lookup"><span data-stu-id="aad22-148">*myHTTPSharePointServer*</span></span><br/><span data-ttu-id="aad22-149">*myHTTPSharePointServer*.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="aad22-149">*myHTTPSharePointServer*.*yourCompany*.com</span></span><br/><span data-ttu-id="aad22-150">10.100.10.10</span><span class="sxs-lookup"><span data-stu-id="aad22-150">10.100.10.10</span></span><br/><br/><span data-ttu-id="aad22-151">Hello IPv4 주소를 사용 하면 note 클라이언트 또는 응용 프로그램 코드 hello IP 주소를 확인 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-151">If you use hello IPv4 address, note that your client or application code may not resolve hello IP address.</span></span> <span data-ttu-id="aad22-152">Hello 중요 참조 hello 위쪽이 항목의 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-152">See hello Important note at hello top of this topic.</span></span> |
   | <span data-ttu-id="aad22-153">포트</span><span class="sxs-lookup"><span data-stu-id="aad22-153">Port</span></span> |<span data-ttu-id="aad22-154">Hello 온-프레미스 리소스의 hello 포트 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-154">Enter hello port number of hello on-premises resource.</span></span> <span data-ttu-id="aad22-155">예를들어, 웹앱을 사용하는 경우 포트 80 또는 443을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-155">For example, if you're using Web Apps, enter port 80 or port 443.</span></span> <span data-ttu-id="aad22-156">SQL Server를 사용하는 경우 포트 1433을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-156">If you're using SQL Server, enter port 1433.</span></span> |
5. <span data-ttu-id="aad22-157">Hello 확인 표시가 toocomplete hello 설치 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-157">Select hello check mark toocomplete hello setup.</span></span> 

#### <a name="additional"></a><span data-ttu-id="aad22-158">추가 항목</span><span class="sxs-lookup"><span data-stu-id="aad22-158">Additional</span></span>
* <span data-ttu-id="aad22-159">하이브리드 연결을 여러 개 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-159">Multiple Hybrid Connections can be created.</span></span> <span data-ttu-id="aad22-160">Hello 참조 [BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md) hello 수가 허용 되는 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-160">See hello [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for hello number of connections allowed.</span></span> 
* <span data-ttu-id="aad22-161">각 하이브리드 연결은 송신하는 응용 프로그램 키와 수신하는 온-프레미스 키, 연결 문자열 쌍으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-161">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span></span> <span data-ttu-id="aad22-162">각 쌍에는 기본 및 보조 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-162">Each pair has a Primary and a Secondary key.</span></span> 

## <span data-ttu-id="aad22-163"><a name="LinkWebSite"></a>Azure App Service Web App 또는 Mobile App 연결</span><span class="sxs-lookup"><span data-stu-id="aad22-163"><a name="LinkWebSite"></a>Link your Azure App Service Web App or Mobile App</span></span>
<span data-ttu-id="aad22-164">Azure 앱 서비스 tooan 기존 하이브리드 연결의에서 웹 응용 프로그램 또는 모바일 앱 toolink 선택 **기존 하이브리드 연결을 사용 하 여** hello 하이브리드 연결 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-164">toolink a Web App or Mobile App in Azure App Service tooan existing Hybrid Connection, select **use an existing Hybrid Connection** in hello Hybrid Connections blade.</span></span> <span data-ttu-id="aad22-165">[Azure App Service에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스](../app-service-web/web-sites-hybrid-connection-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aad22-165">See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <span data-ttu-id="aad22-166"><a name="InstallHCM"></a>Hello 하이브리드 연결 관리자 온-프레미스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-166"><a name="InstallHCM"></a>Install hello Hybrid Connection Manager on-premises</span></span>
<span data-ttu-id="aad22-167">하이브리드 연결을 만든 후 hello 온-프레미스 리소스에 hello 하이브리드 연결 관리자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-167">After a Hybrid Connection is created, install hello Hybrid Connection Manager on hello on-premises resource.</span></span> <span data-ttu-id="aad22-168">이 관리자는 Azure 웹앱이나 BizTalk 서비스에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-168">It can be downloaded from your Azure web apps or from your BizTalk Service.</span></span> <span data-ttu-id="aad22-169">BizTalk 서비스 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-169">BizTalk Services steps:</span></span> 

1. <span data-ttu-id="aad22-170">Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-170">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="aad22-171">Hello 왼쪽된 탐색 창에서 선택 **BizTalk 서비스** 한 다음 BizTalk 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-171">In hello left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="aad22-172">선택 hello **하이브리드 연결** 탭:</span><span class="sxs-lookup"><span data-stu-id="aad22-172">Select hello **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="aad22-173">![하이브리드 연결 탭][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="aad22-173">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="aad22-174">Hello 작업 표시줄에서 선택 **온-프레미스 설정과**:</span><span class="sxs-lookup"><span data-stu-id="aad22-174">In hello task bar, select **On-Premises Setup**:</span></span>  
   <span data-ttu-id="aad22-175">![온-프레미스 설치][HCOnPremSetup]</span><span class="sxs-lookup"><span data-stu-id="aad22-175">![On-Premises Setup][HCOnPremSetup]</span></span>
5. <span data-ttu-id="aad22-176">선택 **설치 및 구성** toorun 또는 다운로드 hello 하이브리드 연결 관리자 hello에 온-프레미스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-176">Select **Install and Configure** toorun or download hello Hybrid Connection Manager on hello on-premises system.</span></span> 
6. <span data-ttu-id="aad22-177">Hello 확인 표시가 toostart hello 설치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-177">Select hello check mark toostart hello installation.</span></span> 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a><span data-ttu-id="aad22-178">추가 항목</span><span class="sxs-lookup"><span data-stu-id="aad22-178">Additional</span></span>
* <span data-ttu-id="aad22-179">하이브리드 연결 관리자 hello 다음 운영 체제에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-179">Hybrid Connection Manager can be installed on hello following operating systems:</span></span>
  
  * <span data-ttu-id="aad22-180">Windows Server 2008 R2(.NET Framework 4.5+ 및 Windows Management Framework 4.0+ 필수)</span><span class="sxs-lookup"><span data-stu-id="aad22-180">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="aad22-181">Windows Server 2012 (Windows Management Framework 4.0+ 필수)</span><span class="sxs-lookup"><span data-stu-id="aad22-181">Windows Server 2012 (Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="aad22-182">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aad22-182">Windows Server 2012 R2</span></span>
* <span data-ttu-id="aad22-183">Hello 하이브리드 연결 관리자를 설치한 후에 hello 다음과 같은 결과가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-183">After you install hello Hybrid Connection Manager, hello following occurs:</span></span> 
  
  * <span data-ttu-id="aad22-184">Azure에서 호스팅되는 하이브리드 연결 hello는 자동으로 구성 된 toouse hello 기본 응용 프로그램 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-184">hello Hybrid Connection hosted on Azure is automatically configured toouse hello Primary Application Connection String.</span></span> 
  * <span data-ttu-id="aad22-185">hello 온-프레미스 리소스는 자동으로 구성 된 toouse hello 기본 온-프레미스 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-185">hello On-Premises resource is automatically configured toouse hello Primary On-Premises Connection String.</span></span>
* <span data-ttu-id="aad22-186">hello 하이브리드 연결 관리자는 권한 부여에 대 한 유효한 온-프레미스 연결 문자열을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-186">hello Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span></span> <span data-ttu-id="aad22-187">hello Azure 웹 앱 또는 모바일 앱 권한 부여에 대 한 올바른 응용 프로그램 연결 문자열을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-187">hello Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span></span>
* <span data-ttu-id="aad22-188">Hello 하이브리드 연결 관리자의 다른 인스턴스가 다른 서버에 설치 하 여 하이브리드 연결을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-188">You can scale Hybrid Connections by installing another instance of hello Hybrid Connection Manager on another server.</span></span> <span data-ttu-id="aad22-189">첫 번째 온-프레미스 수신기 hello로 hello 온-프레미스 수신기 toouse hello 동일한 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-189">Configure hello on-premises listener toouse hello same address as hello first on-premises listener.</span></span> <span data-ttu-id="aad22-190">이 경우 hello 트래픽을 임의로 분산된 (라운드 로빈) hello 활성 온-프레미스 수신기 간에 경우</span><span class="sxs-lookup"><span data-stu-id="aad22-190">In this situation, hello traffic is randomly distributed (round robin) between hello active on-premises listeners.</span></span> 

## <span data-ttu-id="aad22-191"><a name="ManageHybridConnection"></a>하이브리드 연결 관리</span><span class="sxs-lookup"><span data-stu-id="aad22-191"><a name="ManageHybridConnection"></a>Manage Hybrid Connections</span></span>
<span data-ttu-id="aad22-192">toomanage 하이브리드 연결을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-192">toomanage your Hybrid Connections, you can:</span></span>

* <span data-ttu-id="aad22-193">Hello Azure 포털을 사용 하 하며 tooyour BizTalk 서비스를 이동.</span><span class="sxs-lookup"><span data-stu-id="aad22-193">Use hello Azure portal and go tooyour BizTalk Service.</span></span> 
* <span data-ttu-id="aad22-194">[REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-194">Use [REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a><span data-ttu-id="aad22-195">Hello 하이브리드 연결 문자열을 복사/재생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-195">Copy/regenerate hello Hybrid Connection Strings</span></span>
1. <span data-ttu-id="aad22-196">Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-196">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="aad22-197">Hello 왼쪽된 탐색 창에서 선택 **BizTalk 서비스** 한 다음 BizTalk 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-197">In hello left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="aad22-198">선택 hello **하이브리드 연결** 탭:</span><span class="sxs-lookup"><span data-stu-id="aad22-198">Select hello **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="aad22-199">![하이브리드 연결 탭][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="aad22-199">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="aad22-200">Hello 하이브리드 연결을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-200">Select hello Hybrid Connection.</span></span> <span data-ttu-id="aad22-201">Hello 작업 표시줄에서 선택 **연결 관리**:</span><span class="sxs-lookup"><span data-stu-id="aad22-201">In hello task bar, select **Manage Connection**:</span></span>  
   <span data-ttu-id="aad22-202">![옵션 관리][HCManageConnection]</span><span class="sxs-lookup"><span data-stu-id="aad22-202">![Manage Options][HCManageConnection]</span></span>
   
    <span data-ttu-id="aad22-203">**연결을 관리** 목록 hello 응용 프로그램 및 온-프레미스 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-203">**Manage Connection** lists hello Application and On-Premises connection strings.</span></span> <span data-ttu-id="aad22-204">Hello 연결 문자열을 복사 하거나 hello hello 연결 문자열에 사용 되는 액세스 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-204">You can copy hello Connection Strings or regenerate hello Access Key used in hello connection string.</span></span> 
   
    <span data-ttu-id="aad22-205">**다시 생성을 선택 하는 경우**, hello 연결 문자열이 변경 된 hello 내에서 사용 되는 공유 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-205">**If you select Regenerate**, hello Shared Access Key used within hello Connection String is changed.</span></span> <span data-ttu-id="aad22-206">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-206">Do hello following:</span></span>
   
   * <span data-ttu-id="aad22-207">Hello Azure 클래식 포털에서에서 선택 **키 동기화** hello Azure 응용 프로그램에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-207">In hello Azure classic portal, select **Sync Keys** in hello Azure application.</span></span>
   * <span data-ttu-id="aad22-208">다시 실행 하는 hello **온-프레미스 설정과**합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-208">Re-run hello **On-Premises Setup**.</span></span> <span data-ttu-id="aad22-209">Hello를 다시 실행 하는 경우 온-프레미스 설정, 온-프레미스 리소스를 자동으로 hello toouse 업데이트 hello 기본 연결 문자열 구성.</span><span class="sxs-lookup"><span data-stu-id="aad22-209">When you re-run hello On-Premises Setup, hello on-premises resource is automatically configured toouse hello updated Primary connection string.</span></span>

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a><span data-ttu-id="aad22-210">사용 하 여 그룹 정책 toocontrol hello 온-프레미스 하이브리드 연결을 사용 하는 리소스</span><span class="sxs-lookup"><span data-stu-id="aad22-210">Use Group Policy toocontrol hello on-premises resources used by a Hybrid Connection</span></span>
1. <span data-ttu-id="aad22-211">Hello 다운로드 [하이브리드 연결 관리자 관리 템플릿](http://www.microsoft.com/download/details.aspx?id=42963)합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-211">Download hello [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span></span>
2. <span data-ttu-id="aad22-212">Hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-212">Extract hello files.</span></span>
3. <span data-ttu-id="aad22-213">그룹 정책을 수정 하는 hello 컴퓨터에서 수행 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-213">On hello computer that modifies group policy, do hello following:</span></span>  
   
   * <span data-ttu-id="aad22-214">Hello를 복사 합니다. ADMX 파일 toohello *%WINROOT%\PolicyDefinitions* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-214">Copy hello .ADMX files toohello *%WINROOT%\PolicyDefinitions* folder.</span></span>
   * <span data-ttu-id="aad22-215">Hello를 복사 합니다. ADML 파일 toohello *%WINROOT%\PolicyDefinitions\en-us* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-215">Copy hello .ADML files toohello *%WINROOT%\PolicyDefinitions\en-us* folder.</span></span>

<span data-ttu-id="aad22-216">그룹 정책 편집기 toochange hello 정책을 사용 하 여 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aad22-216">Once copied, you can use Group Policy Editor toochange hello policy.</span></span>

## <a name="next"></a><span data-ttu-id="aad22-217">다음</span><span class="sxs-lookup"><span data-stu-id="aad22-217">Next</span></span>
[<span data-ttu-id="aad22-218">Azure 웹 앱 tooan 연결 온-프레미스 리소스</span><span class="sxs-lookup"><span data-stu-id="aad22-218">Connect Azure Web Apps tooan On-Premises Resource</span></span>](../app-service-web/web-sites-hybrid-connection-get-started.md)  
<span data-ttu-id="aad22-219">[Azure 웹 앱에서 tooon 온-프레미스 SQL Server 연결](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="aad22-219">[Connect tooon-premises SQL Server from Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span></span>  
[<span data-ttu-id="aad22-220">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="aad22-220">Hybrid Connections Overview</span></span>](integration-hybrid-connection-overview.md)

## <a name="see-also"></a><span data-ttu-id="aad22-221">참고 항목</span><span class="sxs-lookup"><span data-stu-id="aad22-221">See Also</span></span>
[<span data-ttu-id="aad22-222">Microsoft Azure의 BizTalk Services를 관리하기 위한 REST API</span><span class="sxs-lookup"><span data-stu-id="aad22-222">REST API for Managing BizTalk Services on Microsoft Azure</span></span>](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[<span data-ttu-id="aad22-223">BizTalk 서비스: Editions 차트</span><span class="sxs-lookup"><span data-stu-id="aad22-223">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
[<span data-ttu-id="aad22-224">Azure 클래식 포털을 사용하여 BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="aad22-224">Create a BizTalk Service using Azure classic portal</span></span>](biztalk-provision-services.md)  
[<span data-ttu-id="aad22-225">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="aad22-225">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
