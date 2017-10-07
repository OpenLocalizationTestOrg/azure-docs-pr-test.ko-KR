---
title: "Azure 보안 센터와 게이트웨이 통합 aaaApplication | Microsoft Docs"
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
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="b7181-103">Application Gateway와 Azure Security Center 간의 통합 개요</span><span class="sxs-lookup"><span data-stu-id="b7181-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="b7181-104">Application Gateway와 Security Center에서 웹 응용 프로그램 리소스를 보호하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="b7181-105">응용 프로그램 게이트웨이 웹 응용 프로그램 방화벽 (WAF)와 통합 되어 [보안 센터](../security-center/security-center-intro.md) tooprovide 원활한 뷰 tooprevent 검색 하 고 사용자 환경에서 toothreats toounprotected 웹 응용 프로그램에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="b7181-106">개요</span><span class="sxs-lookup"><span data-stu-id="b7181-106">Overview</span></span>

<span data-ttu-id="b7181-107">Application Gateway WAF는 악용 및 취약성으로부터 웹 응용 프로그램을 보호하는 Security Center의 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="b7181-108">사용 하도록 설정 하는 웹 리소스 WAF로 보호 되지 않는 심각도 높은 권장 사항으로 hello 보안 센터에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="b7181-109">웹 응용 프로그램 방화벽에 대 한 권장 hello에 표시 됩니다 **개요** 페이지의 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![Security Center와의 통합][1]

<span data-ttu-id="b7181-111">웹 응용 프로그램 방화벽에 관한 권장 사항을 클릭 하면 hello 권장 구성의 hello 세부 정보를 표시 하는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="b7181-112">웹 응용 프로그램 방화벽 tooan 기존 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="b7181-113">너무 이동**더 서비스** > **보안 + Id** > **보안 센터** hello에 **보안 센터 정보-개요**  블레이드에서 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="b7181-114">Hello에 **보안 센터-응용 프로그램** 블레이드에서 hello 테이블의 보안 센터 구독에서 발견 되는 응용 프로그램 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![웹 응용 프로그램][3]

<span data-ttu-id="b7181-116">중요 한 문제에는 웹 응용 프로그램을 클릭 하 여 hello 얻게 **응용 프로그램 보안 상태가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="b7181-117">Hello 이미지 아래에서 웹 응용 프로그램 방화벽으로 보호 되지 않는 웹 응용 프로그램을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![보호되지 않는 웹 리소스][2]

<span data-ttu-id="b7181-119">클릭 **추가 웹 응용 프로그램 방화벽** 아래 **권장 사항을** tooopen hello **추가 웹 응용 프로그램 방화벽** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="b7181-120">클릭 하 여 기존 응용 프로그램 게이트웨이 하지 않거나 새 toocreate를 원하는 경우 **새로 만들기** hello에 **만드는 새 웹 응용 프로그램 방화벽** 블레이드에서 하 고 클릭 **Microsoft- 응용 프로그램 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="b7181-121">이 hello 단계 toocreate 응용 프로그램 게이트웨이 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="b7181-122">이 시점에서 웹 응용 프로그램을 보호되는 리소스로 추가하면 Security Center에서 이 리소스가 웹 응용 프로그램 방화벽으로 보호되고 있는지를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="b7181-123">이 경우 백 엔드 풀 멤버로는 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="b7181-124">기존 응용 프로그램 게이트웨이가 있는 경우 **기존 솔루션 사용** 아래에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![웹 응용 프로그램 방화벽 추가 블레이드][4]

<span data-ttu-id="b7181-126">보안 센터를 통해 웹 응용 프로그램 tooan 응용 프로그램 게이트웨이 백 엔드 풀 멤버로 hello 리소스를 추가 하지 않습니다 추가, 해야 이렇게 hello 응용 프로그램 게이트웨이 리소스에 직접 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="b7181-127">추가 리소스 tooan 기존 웹 응용 프로그램 방화벽</span><span class="sxs-lookup"><span data-stu-id="b7181-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="b7181-128">너무 이동**더 서비스** > **보안 + Id** > **보안 센터** hello에 **보안 센터 정보-개요**  블레이드에서 클릭 **파트너 솔루션**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="b7181-129">기존 보안 센터 인식 응용 프로그램 게이트웨이 hello에 표시할 **파트너 솔루션** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![파트너 솔루션][7]

<span data-ttu-id="b7181-131">클릭 **링크 앱** tooopen hello **링크 응용 프로그램** 블레이드에서 여기 제공 됩니다 hello 옵션 tooselect 기존 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="b7181-132">응용 프로그램 tooprotect hello를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="b7181-133">이 응용 프로그램 게이트웨이 hello의 hello 웹 응용 프로그램 toohello 백 엔드 풀을 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="b7181-134">보안 센터를 추적할 수 hello 리소스를 보호 된 리소스로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="b7181-135">백 엔드 풀 멤버로 tooadd hello 리소스를 응용 프로그램 게이트웨이 hello에이 작업을 수행할 수 있어야, hello 현재 블레이드에서 클릭할 수 있는 **솔루션 콘솔** toobe hello 웹을 추가할 수 있는 응용 프로그램 게이트웨이 리소스 toohello 수행 응용 프로그램 toohello 백 엔드 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![파트너 솔루션 응용 프로그램][6]

## <a name="finalize-configuration"></a><span data-ttu-id="b7181-137">구성 완료</span><span class="sxs-lookup"><span data-stu-id="b7181-137">Finalize configuration</span></span>

<span data-ttu-id="b7181-138">보안 센터 트랙 응용 프로그램 보호 된 리소스로 tooan 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="b7181-139">이 리소스의 hello 상태를 모니터링 하 고 된 응용 프로그램 게이트웨이 하 여 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="b7181-140">hello 다음 단계는 tooadd hello 개인 IP, 공용 IP 또는 NIC의 hello 응용 프로그램 게이트웨이 가상 컴퓨터 toohello 백 엔드 풀의입니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="b7181-141">이 작업은 수행의 추가 권장 구성 될 때까지 **응용 프로그램 보호 완료** hello 리소스 추가 될 때까지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![웹 응용 프로그램 방화벽 추가 블레이드][5]

## <a name="security-alerts"></a><span data-ttu-id="b7181-143">보안 경고</span><span class="sxs-lookup"><span data-stu-id="b7181-143">Security Alerts</span></span>

<span data-ttu-id="b7181-144">보안 센터 내에서 이동 너무**검색** > **보안 경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="b7181-145">여기서 응용 프로그램 게이트웨이에 대한 WAF 경고를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="b7181-146">경고는 WAF 규칙으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-146">Alerts are broken down by WAF rule.</span></span>

![보안 경고][8]

<span data-ttu-id="b7181-148">규칙을 클릭하면 해당 WAF 규칙에 대한 경고 목록이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="b7181-149">각 경고 hello 찾기에 추가 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="b7181-150">hello 정보 링크 toohello 응용 프로그램 게이트웨이 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7181-150">hello details provide a link toohello application gateway.</span></span>
 
![경고 세부 정보][9]

## <a name="next-steps"></a><span data-ttu-id="b7181-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7181-152">Next steps</span></span>

<span data-ttu-id="b7181-153">tooenable 웹 응용 프로그램 방화벽에서 기존 응용 프로그램 게이트웨이 방문 하는 방법을 toolearn [만들기 또는 업데이트 된 웹 응용 프로그램 방화벽 Azure 응용 프로그램 게이트웨이](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="b7181-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png