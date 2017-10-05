---
title: "하이브리드 연결 만들기 및 관리 | Microsoft Docs"
description: "하이브리드 연결을 만들고, 연결을 관리하며, 하이브리드 연결 관리자를 설치하는 방법에 대해 알아봅니다. MABS, WABS"
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
ms.openlocfilehash: fceb6b0671e0f77c1f8f92bbb49c986fda3660ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-hybrid-connections"></a><span data-ttu-id="60e1e-104">하이브리드 연결 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="60e1e-104">Create and Manage Hybrid Connections</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60e1e-105">BizTalk 하이브리드 연결은 사용 중지되고 App Service 하이브리드 연결로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="60e1e-106">기존 BizTalk 하이브리드 연결 관리 방법을 비롯한 자세한 내용은 [Azure App Service 하이브리드 연결](../app-service/app-service-hybrid-connections.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e1e-106">For more information, including how to manage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>


## <a name="overview-of-the-steps"></a><span data-ttu-id="60e1e-107">단계의 개요</span><span class="sxs-lookup"><span data-stu-id="60e1e-107">Overview of the Steps</span></span>
1. <span data-ttu-id="60e1e-108">개인 네트워크에 있는 온-프레미스 리소스의 **host name** 또는 **FQDN** of the on-premises resource in your private netw또는k.</span><span class="sxs-lookup"><span data-stu-id="60e1e-108">Create a Hybrid Connection by entering the **host name** or **FQDN** of the on-premises resource in your private network.</span></span>
2. <span data-ttu-id="60e1e-109">하이브리드 연결에 Azure 웹앱 또는 Azure 모바일 앱을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-109">Link your Azure web apps or Azure mobile apps to the Hybrid Connection.</span></span>
3. <span data-ttu-id="60e1e-110">온-프레미스 리소스에 하이브리드 연결 관리자를 설치하고 특정 하이브리드 연결에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-110">Install the Hybrid Connection Manager on your on-premises resource and connect to the specific Hybrid Connection.</span></span> <span data-ttu-id="60e1e-111">Azure 포털은 한 번 클릭으로 설치하고 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-111">The Azure portal provides a single-click experience to install and connect.</span></span>
4. <span data-ttu-id="60e1e-112">하이브리드 연결을 관리하고 연결 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-112">Manage Hybrid Connections and their connection keys.</span></span>

<span data-ttu-id="60e1e-113">이 항목에서는 이러한 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-113">This topic lists these steps.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="60e1e-114">하이브리드 연결 끝점을 IP 주소로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-114">It is possible to set a Hybrid Connection endpoint to an IP address.</span></span> <span data-ttu-id="60e1e-115">IP 주소를 사용하는 경우 클라이언트에 따라 온-프레미스 리소스에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-115">If you use an IP address, you may or may not reach the on-premises resource, depending on your client.</span></span> <span data-ttu-id="60e1e-116">하이브리드 연결은 DNS 조회를 수행하는 클라이언트에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-116">The Hybrid Connection depends on the client doing a DNS lookup.</span></span> <span data-ttu-id="60e1e-117">대부분의 경우에는 **클라이언트** 는 응용 프로그램 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-117">In most cases, the **client** is your application code.</span></span> <span data-ttu-id="60e1e-118">클라이언트가 DNS 조회를 수행하지 않는 경우(도메인 이름(x.x.x.x)인 것처럼 보이면 IP 주소를 확인하지 않음), 하이브리드 연결을 통해 트래픽을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-118">If the client does not perform a DNS lookup, (it does not try to resolve the IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through the Hybrid Connection.</span></span>
> 
> <span data-ttu-id="60e1e-119">예를 들어, **10.4.5.6** (의사 코드)을 온-프레미스 호스트로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-119">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span></span>
> 
> <span data-ttu-id="60e1e-120">**다음 시나리오는 다음과 같은 경우 적용됩니다**.</span><span class="sxs-lookup"><span data-stu-id="60e1e-120">**The following scenario works:**</span></span>  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves to 127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> <span data-ttu-id="60e1e-121">**다음 시나리오는 다음과 같은 경우 적용되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="60e1e-121">**The following scenario doesn't work:**</span></span>  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route to host`
> 
> 

## <span data-ttu-id="60e1e-122"><a name="CreateHybridConnection"></a>하이브리드 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="60e1e-122"><a name="CreateHybridConnection"></a>Create a Hybrid Connection</span></span>
<span data-ttu-id="60e1e-123">하이브리드 연결은 웹앱 **또는** BizTalk 서비스를 사용하여 Azure 포털에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-123">A Hybrid Connection can be created in the Azure portal using Web Apps **or** using BizTalk Services.</span></span> 

<span data-ttu-id="60e1e-124">**웹앱을 사용하여 하이브리드 연결을 만들려면**[Azure 웹앱을 온-프레미스 리소스에 연결](../app-service-web/web-sites-hybrid-connection-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e1e-124">**To create Hybrid Connections using Web Apps**, see [Connect Azure Web Apps to an On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span> <span data-ttu-id="60e1e-125">기본 방법인 웹앱에서 하이브리드 연결 관리자(HCM)를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-125">You can also install the Hybrid Connection Manager (HCM) from your web app, which is the preferred method.</span></span> 

<span data-ttu-id="60e1e-126">**BizTalk 서비스에서 하이브리드 연결을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="60e1e-126">**To create Hybrid Connections in BizTalk Services**:</span></span>

1. <span data-ttu-id="60e1e-127">[Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-127">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="60e1e-128">왼쪽 탐색 창에서 **BizTalk 서비스** 를 선택하고 BizTalk 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-128">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
   
    <span data-ttu-id="60e1e-129">기존 BizTalk 서비스가 없는 경우 [BizTalk 서비스를 만들 수](biztalk-provision-services.md)있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-129">If you don't have an existing BizTalk Service, you can [Create a BizTalk Service](biztalk-provision-services.md).</span></span>
3. <span data-ttu-id="60e1e-130">**하이브리드 연결** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-130">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="60e1e-131">![하이브리드 연결 탭][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="60e1e-131">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="60e1e-132">**하이브리드 연결 만들기**를 선택하거나 작업 표시줄의 **추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-132">Select **Create a Hybrid Connection** or select the **ADD** button in the task bar.</span></span> <span data-ttu-id="60e1e-133">다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-133">Enter the following:</span></span>
   
   | <span data-ttu-id="60e1e-134">속성</span><span class="sxs-lookup"><span data-stu-id="60e1e-134">Property</span></span> | <span data-ttu-id="60e1e-135">설명</span><span class="sxs-lookup"><span data-stu-id="60e1e-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="60e1e-136">이름</span><span class="sxs-lookup"><span data-stu-id="60e1e-136">Name</span></span> |<span data-ttu-id="60e1e-137">하이브리드 연결 이름은 고유해야 하며 BizTalk 서비스와 같은 이름일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-137">The Hybrid Connection name must be unique and cannot be the same name as the BizTalk Service.</span></span> <span data-ttu-id="60e1e-138">어떤 이름을 입력해도 괜찮지만 용도에 맞는 구체적인 이름을 입력하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-138">You can enter any name but be specific with its purpose.</span></span> <span data-ttu-id="60e1e-139">이러한 예로 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-139">Examples include:</span></span><br/><br/><span data-ttu-id="60e1e-140">Payroll*SQLServer*</span><span class="sxs-lookup"><span data-stu-id="60e1e-140">Payroll*SQLServer*</span></span><br/><span data-ttu-id="60e1e-141">SupplyList*SharepointServer*</span><span class="sxs-lookup"><span data-stu-id="60e1e-141">SupplyList*SharepointServer*</span></span><br/><span data-ttu-id="60e1e-142">Customers*OracleServer*</span><span class="sxs-lookup"><span data-stu-id="60e1e-142">Customers*OracleServer*</span></span> |
   | <span data-ttu-id="60e1e-143">호스트 이름</span><span class="sxs-lookup"><span data-stu-id="60e1e-143">Host Name</span></span> |<span data-ttu-id="60e1e-144">온-프레미스 리소스의 정규화된 호스트 이름, 호스트 이름만 또는 IPv4 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-144">Enter the fully qualified host name, only the host name, or the IPv4 address of the on-premises resource.</span></span> <span data-ttu-id="60e1e-145">이러한 예로 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-145">Examples include:</span></span><br/><br/><span data-ttu-id="60e1e-146">mySQLServer</span><span class="sxs-lookup"><span data-stu-id="60e1e-146">mySQLServer</span></span><br/><span data-ttu-id="60e1e-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="60e1e-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span></span><br/><span data-ttu-id="60e1e-148">*myHTTPSharePointServer*</span><span class="sxs-lookup"><span data-stu-id="60e1e-148">*myHTTPSharePointServer*</span></span><br/><span data-ttu-id="60e1e-149">*myHTTPSharePointServer*.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="60e1e-149">*myHTTPSharePointServer*.*yourCompany*.com</span></span><br/><span data-ttu-id="60e1e-150">10.100.10.10</span><span class="sxs-lookup"><span data-stu-id="60e1e-150">10.100.10.10</span></span><br/><br/><span data-ttu-id="60e1e-151">IPv4 주소를 사용하는 경우, 클라이언트 또는 응용 프로그램 코드에서 IP 주소를 확인하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-151">If you use the IPv4 address, note that your client or application code may not resolve the IP address.</span></span> <span data-ttu-id="60e1e-152">이 항목의 맨 위에 있는 중요한 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e1e-152">See the Important note at the top of this topic.</span></span> |
   | <span data-ttu-id="60e1e-153">포트</span><span class="sxs-lookup"><span data-stu-id="60e1e-153">Port</span></span> |<span data-ttu-id="60e1e-154">온-프레미스 리소스의 포트 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-154">Enter the port number of the on-premises resource.</span></span> <span data-ttu-id="60e1e-155">예를들어, 웹앱을 사용하는 경우 포트 80 또는 443을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-155">For example, if you're using Web Apps, enter port 80 or port 443.</span></span> <span data-ttu-id="60e1e-156">SQL Server를 사용하는 경우 포트 1433을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-156">If you're using SQL Server, enter port 1433.</span></span> |
5. <span data-ttu-id="60e1e-157">설정을 완료하려면 확인 표시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-157">Select the check mark to complete the setup.</span></span> 

#### <a name="additional"></a><span data-ttu-id="60e1e-158">추가 항목</span><span class="sxs-lookup"><span data-stu-id="60e1e-158">Additional</span></span>
* <span data-ttu-id="60e1e-159">하이브리드 연결을 여러 개 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-159">Multiple Hybrid Connections can be created.</span></span> <span data-ttu-id="60e1e-160">허용되는 연결 수는 [BizTalk 서비스: Editions 차트](biztalk-editions-feature-chart.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e1e-160">See the [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for the number of connections allowed.</span></span> 
* <span data-ttu-id="60e1e-161">각 하이브리드 연결은 송신하는 응용 프로그램 키와 수신하는 온-프레미스 키, 연결 문자열 쌍으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-161">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span></span> <span data-ttu-id="60e1e-162">각 쌍에는 기본 및 보조 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-162">Each pair has a Primary and a Secondary key.</span></span> 

## <span data-ttu-id="60e1e-163"><a name="LinkWebSite"></a>Azure App Service Web App 또는 Mobile App 연결</span><span class="sxs-lookup"><span data-stu-id="60e1e-163"><a name="LinkWebSite"></a>Link your Azure App Service Web App or Mobile App</span></span>
<span data-ttu-id="60e1e-164">Azure App Service에서 Web App 또는 Mobile App을 기존 하이브리드 연결에 연결하려면 하이브리드 연결 블레이드에서 **기존 하이브리드 연결 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-164">To link a Web App or Mobile App in Azure App Service to an existing Hybrid Connection, select **use an existing Hybrid Connection** in the Hybrid Connections blade.</span></span> <span data-ttu-id="60e1e-165">[Azure App Service에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스](../app-service-web/web-sites-hybrid-connection-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e1e-165">See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <span data-ttu-id="60e1e-166"><a name="InstallHCM"></a>온-프레미스에 하이브리드 연결 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="60e1e-166"><a name="InstallHCM"></a>Install the Hybrid Connection Manager on-premises</span></span>
<span data-ttu-id="60e1e-167">하이브리드 연결이 만들어진 후에는 온-프레미스 리소스에 하이브리드 연결 관리자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-167">After a Hybrid Connection is created, install the Hybrid Connection Manager on the on-premises resource.</span></span> <span data-ttu-id="60e1e-168">이 관리자는 Azure 웹앱이나 BizTalk 서비스에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-168">It can be downloaded from your Azure web apps or from your BizTalk Service.</span></span> <span data-ttu-id="60e1e-169">BizTalk 서비스 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-169">BizTalk Services steps:</span></span> 

1. <span data-ttu-id="60e1e-170">[Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-170">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="60e1e-171">왼쪽 탐색 창에서 **BizTalk 서비스** 를 선택하고 BizTalk 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-171">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="60e1e-172">**하이브리드 연결** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-172">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="60e1e-173">![하이브리드 연결 탭][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="60e1e-173">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="60e1e-174">작업 표시줄에서 **온-프레미스 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-174">In the task bar, select **On-Premises Setup**:</span></span>  
   <span data-ttu-id="60e1e-175">![온-프레미스 설치][HCOnPremSetup]</span><span class="sxs-lookup"><span data-stu-id="60e1e-175">![On-Premises Setup][HCOnPremSetup]</span></span>
5. <span data-ttu-id="60e1e-176">**설치 및 구성** 을 선택하여 온-프레미스 시스템에서 하이브리드 연결 관리자를 실행하거나 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-176">Select **Install and Configure** to run or download the Hybrid Connection Manager on the on-premises system.</span></span> 
6. <span data-ttu-id="60e1e-177">설치를 시작하려면 확인 표시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-177">Select the check mark to start the installation.</span></span> 

<!--
You can also download the Hybrid Connection Manager MSI file and copy the file to your on-premises resource. Specific steps:

1. Copy the on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for the specific steps.
2. Download the Hybrid Connection Manager MSI file. 
3. On the on-premises resource, install the Hybrid Connection Manager from the MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a><span data-ttu-id="60e1e-178">추가 항목</span><span class="sxs-lookup"><span data-stu-id="60e1e-178">Additional</span></span>
* <span data-ttu-id="60e1e-179">하이브리드 연결 관리자는 다음 운영 체제에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-179">Hybrid Connection Manager can be installed on the following operating systems:</span></span>
  
  * <span data-ttu-id="60e1e-180">Windows Server 2008 R2(.NET Framework 4.5+ 및 Windows Management Framework 4.0+ 필수)</span><span class="sxs-lookup"><span data-stu-id="60e1e-180">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="60e1e-181">Windows Server 2012 (Windows Management Framework 4.0+ 필수)</span><span class="sxs-lookup"><span data-stu-id="60e1e-181">Windows Server 2012 (Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="60e1e-182">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="60e1e-182">Windows Server 2012 R2</span></span>
* <span data-ttu-id="60e1e-183">하이브리드 연결 관리자를 설치한 후에 다음이 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-183">After you install the Hybrid Connection Manager, the following occurs:</span></span> 
  
  * <span data-ttu-id="60e1e-184">Azure에 호스트된 하이브리드 연결은 기본 응용 프로그램 연결 문자열을 사용하도록 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-184">The Hybrid Connection hosted on Azure is automatically configured to use the Primary Application Connection String.</span></span> 
  * <span data-ttu-id="60e1e-185">온-프레미스 리소스는 기본 온-프레미스 연결 문자열을 사용하도록 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-185">The On-Premises resource is automatically configured to use the Primary On-Premises Connection String.</span></span>
* <span data-ttu-id="60e1e-186">하이브리드 연결 관리자는 권한 부여를 위해 유효한 온-프레미스 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-186">The Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span></span> <span data-ttu-id="60e1e-187">Azure 웹앱 또는 모바일 앱은 권한 부여를 위해 유효한 응용 프로그램 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-187">The Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span></span>
* <span data-ttu-id="60e1e-188">다른 서버에 하이브리드 연결 관리자의 다른 인스턴스를 설치하여 하이브리드 연결을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-188">You can scale Hybrid Connections by installing another instance of the Hybrid Connection Manager on another server.</span></span> <span data-ttu-id="60e1e-189">첫 번째 온-프레미스 수신기와 동일한 주소를 사용하도록 온-프레미스 수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-189">Configure the on-premises listener to use the same address as the first on-premises listener.</span></span> <span data-ttu-id="60e1e-190">이 상황에서 트래픽이 활성 온-프레미스 수신기 사이에서 임의로 분산됩니다(라운드 로빈).</span><span class="sxs-lookup"><span data-stu-id="60e1e-190">In this situation, the traffic is randomly distributed (round robin) between the active on-premises listeners.</span></span> 

## <span data-ttu-id="60e1e-191"><a name="ManageHybridConnection"></a>하이브리드 연결 관리</span><span class="sxs-lookup"><span data-stu-id="60e1e-191"><a name="ManageHybridConnection"></a>Manage Hybrid Connections</span></span>
<span data-ttu-id="60e1e-192">하이브리드 연결을 관리하기 위해 다음을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-192">To manage your Hybrid Connections, you can:</span></span>

* <span data-ttu-id="60e1e-193">Azure 포털을 사용하고 BizTalk 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-193">Use the Azure portal and go to your BizTalk Service.</span></span> 
* <span data-ttu-id="60e1e-194">[REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-194">Use [REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

#### <a name="copyregenerate-the-hybrid-connection-strings"></a><span data-ttu-id="60e1e-195">하이브리드 연결 문자열 복사/다시 생성</span><span class="sxs-lookup"><span data-stu-id="60e1e-195">Copy/regenerate the Hybrid Connection Strings</span></span>
1. <span data-ttu-id="60e1e-196">[Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-196">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="60e1e-197">왼쪽 탐색 창에서 **BizTalk 서비스** 를 선택하고 BizTalk 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-197">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="60e1e-198">**하이브리드 연결** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-198">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="60e1e-199">![하이브리드 연결 탭][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="60e1e-199">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="60e1e-200">하이브리드 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-200">Select the Hybrid Connection.</span></span> <span data-ttu-id="60e1e-201">작업 표시줄에서 **연결 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-201">In the task bar, select **Manage Connection**:</span></span>  
   <span data-ttu-id="60e1e-202">![옵션 관리][HCManageConnection]</span><span class="sxs-lookup"><span data-stu-id="60e1e-202">![Manage Options][HCManageConnection]</span></span>
   
    <span data-ttu-id="60e1e-203">**연결 관리** 에는 응용 프로그램 및 온-프레미스 연결 문자열이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-203">**Manage Connection** lists the Application and On-Premises connection strings.</span></span> <span data-ttu-id="60e1e-204">연결 문자열을 복사하거나 연결 문자열에 사용된 액세스 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-204">You can copy the Connection Strings or regenerate the Access Key used in the connection string.</span></span> 
   
    <span data-ttu-id="60e1e-205">**다시 생성을 선택하면**연결 문자열에 사용된 공유 선택키가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-205">**If you select Regenerate**, the Shared Access Key used within the Connection String is changed.</span></span> <span data-ttu-id="60e1e-206">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-206">Do the following:</span></span>
   
   * <span data-ttu-id="60e1e-207">Azure 클래식 포털의 Azure 응용 프로그램에서 **키 동기화** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-207">In the Azure classic portal, select **Sync Keys** in the Azure application.</span></span>
   * <span data-ttu-id="60e1e-208">**온-프레미스 설치**를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-208">Re-run the **On-Premises Setup**.</span></span> <span data-ttu-id="60e1e-209">온-프레미스 설치를 다시 실행하면 온-프레미스 리소스가 업데이트된 기본 연결 문자열을 사용하도록 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-209">When you re-run the On-Premises Setup, the on-premises resource is automatically configured to use the updated Primary connection string.</span></span>

#### <a name="use-group-policy-to-control-the-on-premises-resources-used-by-a-hybrid-connection"></a><span data-ttu-id="60e1e-210">그룹 정책을 사용하여 하이브리드 연결에 사용되는 온-프레미스 리소스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-210">Use Group Policy to control the on-premises resources used by a Hybrid Connection</span></span>
1. <span data-ttu-id="60e1e-211">[하이브리드 연결 관리자 관리 템플릿](http://www.microsoft.com/download/details.aspx?id=42963)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-211">Download the [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span></span>
2. <span data-ttu-id="60e1e-212">파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-212">Extract the files.</span></span>
3. <span data-ttu-id="60e1e-213">그룹 정책을 수정하는 컴퓨터에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-213">On the computer that modifies group policy, do the following:</span></span>  
   
   * <span data-ttu-id="60e1e-214">.ADMX 파일을 *%WINROOT%\PolicyDefinitions* 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-214">Copy the .ADMX files to the *%WINROOT%\PolicyDefinitions* folder.</span></span>
   * <span data-ttu-id="60e1e-215">.ADML 파일을 *%WINROOT%\PolicyDefinitions\en-us* 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-215">Copy the .ADML files to the *%WINROOT%\PolicyDefinitions\en-us* folder.</span></span>

<span data-ttu-id="60e1e-216">복사되면 그룹 정책 편집기를 사용하여 정책을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e1e-216">Once copied, you can use Group Policy Editor to change the policy.</span></span>

## <a name="next"></a><span data-ttu-id="60e1e-217">다음</span><span class="sxs-lookup"><span data-stu-id="60e1e-217">Next</span></span>
[<span data-ttu-id="60e1e-218">Azure 웹앱을 온-프레미스 리소스에 연결</span><span class="sxs-lookup"><span data-stu-id="60e1e-218">Connect Azure Web Apps to an On-Premises Resource</span></span>](../app-service-web/web-sites-hybrid-connection-get-started.md)  
<span data-ttu-id="60e1e-219">[Azure Web Apps에서 온-프레미스 SQL Server에 연결](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="60e1e-219">[Connect to on-premises SQL Server from Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span></span>  
[<span data-ttu-id="60e1e-220">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="60e1e-220">Hybrid Connections Overview</span></span>](integration-hybrid-connection-overview.md)

## <a name="see-also"></a><span data-ttu-id="60e1e-221">참고 항목</span><span class="sxs-lookup"><span data-stu-id="60e1e-221">See Also</span></span>
[<span data-ttu-id="60e1e-222">Microsoft Azure의 BizTalk Services를 관리하기 위한 REST API</span><span class="sxs-lookup"><span data-stu-id="60e1e-222">REST API for Managing BizTalk Services on Microsoft Azure</span></span>](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[<span data-ttu-id="60e1e-223">BizTalk 서비스: Editions 차트</span><span class="sxs-lookup"><span data-stu-id="60e1e-223">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
[<span data-ttu-id="60e1e-224">Azure 클래식 포털을 사용하여 BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="60e1e-224">Create a BizTalk Service using Azure classic portal</span></span>](biztalk-provision-services.md)  
[<span data-ttu-id="60e1e-225">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="60e1e-225">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
