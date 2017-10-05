---
title: "Azure Security Center와의 Application Gateway 통합 | Microsoft Docs"
description: "이 페이지에서는 Application Gateway가 Azure Security Center에 통합되는 방법에 대한 정보를 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="aaa2a-103">Application Gateway와 Azure Security Center 간의 통합 개요</span><span class="sxs-lookup"><span data-stu-id="aaa2a-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="aaa2a-104">Application Gateway와 Security Center에서 웹 응용 프로그램 리소스를 보호하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="aaa2a-105">Application Gateway WAF(웹 응용 프로그램 방화벽)는 [Security Center](../security-center/security-center-intro.md)와 통합되어 사용자 환경에서 보호되지 않는 웹 응용 프로그램에 대한 위협을 방지, 검색 및 대응할 수 있는 완벽한 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="aaa2a-106">개요</span><span class="sxs-lookup"><span data-stu-id="aaa2a-106">Overview</span></span>

<span data-ttu-id="aaa2a-107">Application Gateway WAF는 악용 및 취약성으로부터 웹 응용 프로그램을 보호하는 Security Center의 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="aaa2a-108">WAF에서 보호되지 않는 웹 지원 리소스는 Security Center에서 높은 심각도 수준의 권장 사항으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="aaa2a-109">웹 응용 프로그램 방화벽에 대한 권장 사항은 **개요** 페이지의 **응용 프로그램** 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![Security Center와의 통합][1]

<span data-ttu-id="aaa2a-111">웹 응용 프로그램 방화벽과 관련된 권장 사항을 클릭하면 권장 사항의 세부 정보를 보여 주는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="aaa2a-112">기존 리소스에 웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="aaa2a-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="aaa2a-113">**추가 서비스** > **보안 + ID** > **Security Center**로 차례로 이동하고, **Security Center - 개요** 블레이드에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="aaa2a-114">**Security Center - 응용 프로그램** 블레이드의 표에는 Security Center를 통해 구독에서 검색한 응용 프로그램 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![웹 응용 프로그램][3]

<span data-ttu-id="aaa2a-116">중요한 문제가 있는 웹 응용 프로그램을 클릭하면 **응용 프로그램 보안 상태** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="aaa2a-117">아래 이미지에서는 웹 응용 프로그램 방화벽에서 보호되지 않는 웹 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![보호되지 않는 웹 리소스][2]

<span data-ttu-id="aaa2a-119">**권장 사항** 아래에서 **웹 응용 프로그램 방화벽 추가**를 클릭하여 **웹 응용 프로그램 방화벽 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="aaa2a-120">기존 Application Gateway가 없거나 새 Application Gateway를 만들려면, **새 웹 응용 프로그램 방화벽 만들기** 블레이드에서 **새로 만들기**, **Microsoft - Application Gateway**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="aaa2a-121">이를 통해 응용 프로그램 게이트웨이를 단계적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="aaa2a-122">이 시점에서 웹 응용 프로그램을 보호되는 리소스로 추가하면 Security Center에서 이 리소스가 웹 응용 프로그램 방화벽으로 보호되고 있는지를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="aaa2a-123">이 경우 백 엔드 풀 멤버로는 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="aaa2a-124">기존 응용 프로그램 게이트웨이가 있는 경우 **기존 솔루션 사용** 아래에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![웹 응용 프로그램 방화벽 추가 블레이드][4]

<span data-ttu-id="aaa2a-126">Security Center를 통해 응용 프로그램 게이트웨이에 웹 응용 프로그램을 추가하더라도 해당 리소스가 백 엔드 풀 멤버로 추가되지 않습니다. 이렇게 하려면 응용 프로그램 게이트웨이 리소스에서 직접 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="aaa2a-127">기존 웹 응용 프로그램 방화벽에 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="aaa2a-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="aaa2a-128">**추가 서비스** > **보안 + ID** > **Security Center**로 차례로 이동하고, **Security Center - 개요** 블레이드에서 **파트너 솔루션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="aaa2a-129">기존 Security Center 인식 응용 프로그램 게이트웨이가 **파트너 솔루션** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![파트너 솔루션][7]

<span data-ttu-id="aaa2a-131">**앱 연결**을 클릭하여 **링크 응용 프로그램 연결** 블레이드를 엽니다. 여기서는 기존 응용 프로그램을 선택할 수 있는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="aaa2a-132">보호할 응용 프로그램을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="aaa2a-133">이 경우 웹 응용 프로그램은 응용 프로그램 게이트웨이의 백 엔드 풀에 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="aaa2a-134">이렇게 하면 Security Center에서 추적할 수 있도록 리소스를 보호된 리소스로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="aaa2a-135">리소스를 백 엔드 풀 멤버로 추가하려면 응용 프로그램 게이트웨이에서 수행해야 합니다. 즉 현재 블레이드에서 **솔루션 콘솔**을 클릭하여 웹 응용 프로그램을 백 엔드 풀에 추가할 수 있는 응용 프로그램 게이트웨이 리소스로 가져오면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![파트너 솔루션 응용 프로그램][6]

## <a name="finalize-configuration"></a><span data-ttu-id="aaa2a-137">구성 완료</span><span class="sxs-lookup"><span data-stu-id="aaa2a-137">Finalize configuration</span></span>

<span data-ttu-id="aaa2a-138">Security Center에서는 응용 프로그램 게이트웨이에 추가한 응용 프로그램을 보호된 리소스로 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="aaa2a-139">이 리소스의 상태를 모니터링하고, 해당 리소스가 응용 프로그램 게이트웨이에서 보호되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="aaa2a-140">다음 단계는 가상 컴퓨터의 개인 IP, 공용 IP 또는 NIC를 응용 프로그램 게이트웨이의 백 엔드 풀에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="aaa2a-141">**응용 프로그램 보호 마무리**에 대한 추가 권장 사항은 이 작업을 완료할 때까지 표시되며, 리소스를 추가하면 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![웹 응용 프로그램 방화벽 추가 블레이드][5]

## <a name="security-alerts"></a><span data-ttu-id="aaa2a-143">보안 경고</span><span class="sxs-lookup"><span data-stu-id="aaa2a-143">Security Alerts</span></span>

<span data-ttu-id="aaa2a-144">Security Center에서 **검색** > **보안 경고**로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="aaa2a-145">여기서 응용 프로그램 게이트웨이에 대한 WAF 경고를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="aaa2a-146">경고는 WAF 규칙으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-146">Alerts are broken down by WAF rule.</span></span>

![보안 경고][8]

<span data-ttu-id="aaa2a-148">규칙을 클릭하면 해당 WAF 규칙에 대한 경고 목록이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="aaa2a-149">경고마다 찾기에 대한 자세한 추가 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="aaa2a-150">세부 정보에서는 응용 프로그램 게이트웨이에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-150">The details provide a link to the application gateway.</span></span>
 
![경고 세부 정보][9]

## <a name="next-steps"></a><span data-ttu-id="aaa2a-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aaa2a-152">Next steps</span></span>

<span data-ttu-id="aaa2a-153">기존 응용 프로그램 게이트웨이에서 웹 응용 프로그램 방화벽을 사용하도록 설정하는 방법을 알아보려면 [웹 응용 프로그램 방화벽이 있는 Azure Application Gateway 만들기 또는 업데이트](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aaa2a-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png