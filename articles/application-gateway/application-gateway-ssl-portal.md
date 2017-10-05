---
title: "SSL 오프로드 구성 - Azure Application Gateway - Azure Portal | Microsoft Docs"
description: "이 페이지에서는 포털을 사용하여 SSL 오프로드와 함께 응용 프로그램 게이트웨이를 만드는 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="533fe-103">포털을 사용하여 SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="533fe-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="533fe-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="533fe-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="533fe-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="533fe-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="533fe-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="533fe-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="533fe-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="533fe-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="533fe-108">Azure Application Gateway 구성을 사용하여 웹 팜에서 발생하는 비용이 많이 드는 SSL(Secure Sockets Layer) 암호 해독 작업을 방지하기 위한 게이트웨이에서 SSL 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="533fe-109">SSL 오프로드는 또한 프런트 엔드 서버 설치 및 웹 응용 프로그램의 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="533fe-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="533fe-110">Scenario</span></span>

<span data-ttu-id="533fe-111">다음 시나리오에서는 기존 응용 프로그램 게이트웨이에서 SSL 오프로드를 구성하는 과정을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="533fe-112">이 시나리오에서는 [Application Gateway 만들기](application-gateway-create-gateway-portal.md)단계를 이미 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="533fe-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="533fe-113">Before you begin</span></span>

<span data-ttu-id="533fe-114">응용 프로그램 게이트웨이에서 SSL 오프로드를 구성하려면 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="533fe-115">이 인증서는 응용 프로그램 게이트웨이에 로드되며 SSL을 통해 전송된 트래픽을 암호화 및 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="533fe-116">인증서는 개인 정보 교환(.pfx) 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="533fe-117">이 파일 형식을 사용하면 응용 프로그램 게이트웨이에서 트래픽의 암호화 및 암호 해독을 수행하는 데 필요한 개인 키를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="533fe-118">HTTPS 수신기 추가</span><span class="sxs-lookup"><span data-stu-id="533fe-118">Add an HTTPS listener</span></span>

<span data-ttu-id="533fe-119">HTTPS 수신기는 구성에 따라 트래픽을 확인하며, 백 엔드 풀로 트래픽을 라우팅하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="533fe-120">1단계</span><span class="sxs-lookup"><span data-stu-id="533fe-120">Step 1</span></span>

<span data-ttu-id="533fe-121">Azure Portal로 이동하여 기존 응용 프로그램 게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="533fe-122">2단계</span><span class="sxs-lookup"><span data-stu-id="533fe-122">Step 2</span></span>

<span data-ttu-id="533fe-123">수신기를 클릭한 다음 추가 단추를 클릭하여 수신기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-123">Click Listeners and click the Add button to add a listener.</span></span>

![응용 프로그램 게이트웨이 개요 블레이드][1]

### <a name="step-3"></a><span data-ttu-id="533fe-125">3단계</span><span class="sxs-lookup"><span data-stu-id="533fe-125">Step 3</span></span>

<span data-ttu-id="533fe-126">수신기에 대한 필수 정보를 입력하고 .pfx 인증서를 업로드합니다. 완료되면 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="533fe-127">**이름** - 이 값은 수신기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="533fe-128">**프런트 엔드 IP 구성** - 이 값은 수신기에 사용되는 프런트 엔드 IP 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="533fe-129">**프런트 엔드 포트(이름/포트)** - 응용 프로그램 게이트웨이의 프런트 엔드에서 사용되는 포트 및 실제로 사용되는 포트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="533fe-130">**프로토콜** - 프런트 엔드에 https가 사용되는지 또는 http가 사용되는지를 결정하는 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="533fe-131">**인증서(이름/암호)** - SSL 오프로드를 사용하는 경우 이 설정에는 .pfx 인증서가 필요하며, 이름 및 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![수신기 추가 블레이드][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="533fe-133">규칙을 만들고 수신기에 연결</span><span class="sxs-lookup"><span data-stu-id="533fe-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="533fe-134">이제 수신기가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-134">The listener has now been created.</span></span> <span data-ttu-id="533fe-135">수신기에서 트래픽을 처리할 규칙을 만들 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="533fe-136">규칙은 쿠키 기반 세션 선호도가 사용되는지 여부를 비롯하여 여러 구성 설정, 프로토콜, 포트 및 상태 프로브에 따라 백 엔드 풀에 트래픽이 라우팅되는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="533fe-137">1단계</span><span class="sxs-lookup"><span data-stu-id="533fe-137">Step 1</span></span>

<span data-ttu-id="533fe-138">응용 프로그램 게이트웨이의 **규칙**을 클릭한 다음 추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![앱 게이트웨이 규칙 블레이드][3]

### <a name="step-2"></a><span data-ttu-id="533fe-140">2단계</span><span class="sxs-lookup"><span data-stu-id="533fe-140">Step 2</span></span>

<span data-ttu-id="533fe-141">**기본 규칙 추가** 블레이드에서 규칙의 이름을 입력하고 이전 단계에서 만든 수신기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="533fe-142">적절한 백 엔드 풀 및 http 설정을 선택하고 **확인**</span><span class="sxs-lookup"><span data-stu-id="533fe-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![https 설정 창][4]

<span data-ttu-id="533fe-144">이제 설정이 응용 프로그램 게이트웨이에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="533fe-145">이러한 설정의 저장 프로세스에는 약간의 시간이 걸릴 수 있으며, 그런 다음 포털 또는 PowerShell을 통해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="533fe-146">저장이 완료되면 응용 프로그램 게이트웨이에서 트래픽의 암호화 및 암호 해독을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="533fe-147">응용 프로그램 게이트웨이와 백 엔드 웹 서버 간의 모든 트래픽은 http를 통해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="533fe-148">Https를 통해 시작된 경우에는 클라이언트와의 모든 통신이 암호화된 상태로 클라이언트에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="533fe-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="533fe-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="533fe-149">Next steps</span></span>

<span data-ttu-id="533fe-150">Azure Application Gateway를 사용하여 사용자 지정 상태 프로브를 구성하는 방법을 알아보려면 [사용자 지정 상태 프로브 만들기](application-gateway-create-gateway-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="533fe-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
