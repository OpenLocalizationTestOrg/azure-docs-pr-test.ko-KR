---
title: "aaaConfigure SSL 오프 로드를-Azure 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate hello 포털을 사용 하 여 응용 프로그램 게이트웨이 ssl 오프 로드"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="b7350-103">Hello 포털을 사용 하 여 SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="b7350-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7350-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="b7350-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="b7350-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7350-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="b7350-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7350-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="b7350-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b7350-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="b7350-108">Azure 응용 프로그램 게이트웨이 hello 게이트웨이 tooavoid 비용이 많이 드는 SSL 암호 해독 작업 toohappen hello 웹 팜에서에 구성 된 tooterminate hello (SECURE Sockets Layer) 세션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="b7350-109">SSL 오프 로드 hello 프런트 엔드 서버 설치 및 hello 웹 응용 프로그램 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="b7350-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="b7350-110">Scenario</span></span>

<span data-ttu-id="b7350-111">기존 응용 프로그램 게이트웨이에 SSL 오프 로드를 구성 하는 과정 hello 시나리오를 따르는 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="b7350-112">hello 시나리오에서는 가정 이미 수행 hello 단계 너무[응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7350-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b7350-113">Before you begin</span></span>

<span data-ttu-id="b7350-114">응용 프로그램 게이트웨이와 tooconfigure SSL 오프 로드는 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="b7350-115">이 인증서의 hello 응용 프로그램 게이트웨이에 로드 된 tooencrypt 사용 및 SSL을 통해 전송 하는 hello 트래픽 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="b7350-116">hello 인증서 toobe 개인 정보 교환 (pfx) 형태로 표시 되어야합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="b7350-117">이 파일 형식을 사용 하면 hello에 대 한 개인 키 toobe 내보낸 hello 응용 프로그램 게이트웨이 tooperform hello 암호화 및 암호 해독 트래픽의 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="b7350-118">HTTPS 수신기 추가</span><span class="sxs-lookup"><span data-stu-id="b7350-118">Add an HTTPS listener</span></span>

<span data-ttu-id="b7350-119">hello HTTPS 수신기는 해당 구성에 따라 트래픽에 대 한 검색 하 고 경로 hello 트래픽 toohello 백 엔드 풀을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="b7350-120">1단계</span><span class="sxs-lookup"><span data-stu-id="b7350-120">Step 1</span></span>

<span data-ttu-id="b7350-121">Azure 포털 toohello를 이동한 후 기존 응용 프로그램 게이트웨이 선택</span><span class="sxs-lookup"><span data-stu-id="b7350-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="b7350-122">2단계</span><span class="sxs-lookup"><span data-stu-id="b7350-122">Step 2</span></span>

<span data-ttu-id="b7350-123">수신기를 클릭 하 고 hello 추가 단추 tooadd 수신기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![응용 프로그램 게이트웨이 개요 블레이드][1]

### <a name="step-3"></a><span data-ttu-id="b7350-125">3단계</span><span class="sxs-lookup"><span data-stu-id="b7350-125">Step 3</span></span>

<span data-ttu-id="b7350-126">입력 hello 수신기에 대 한 필요한 정보를 hello 및 완료 되 면 업로드 hello.pfx 인증서 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="b7350-127">**이름** -이 값은 hello 수신기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="b7350-128">**프런트 엔드 IP 구성** -이 값은 hello hello 수신기에 사용 되는 프런트 엔드 IP 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="b7350-129">**프런트 엔드 포트 (이름/포트)** -hello 프런트 엔드 응용 프로그램 게이트웨이 hello 및 사용 하는 hello 실제 포트에 사용 되는 hello 포트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="b7350-130">**프로토콜** -hello 프런트 엔드 https 또는 http를 사용 하는 경우 스위치 toodetermine 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="b7350-131">**인증서(이름/암호)** - SSL 오프로드를 사용하는 경우 이 설정에는 .pfx 인증서가 필요하며, 이름 및 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![수신기 추가 블레이드][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="b7350-133">규칙을 만들고 toohello 수신기 연결</span><span class="sxs-lookup"><span data-stu-id="b7350-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="b7350-134">hello 수신기를 지금 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-134">hello listener has now been created.</span></span> <span data-ttu-id="b7350-135">시간 toocreate hello 수신기에서 규칙 toohandle hello 트래픽 이며</span><span class="sxs-lookup"><span data-stu-id="b7350-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="b7350-136">규칙에 여러 쿠키 기반 세션 선호도 사용 되는지 여부를 비롯 한 구성 설정, 프로토콜, 포트 및 상태 프로브를 바탕으로 라우트된 toohello 백 엔드 풀 트래픽은 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="b7350-137">1단계</span><span class="sxs-lookup"><span data-stu-id="b7350-137">Step 1</span></span>

<span data-ttu-id="b7350-138">Hello 클릭 **규칙** hello 응용 프로그램 게이트웨이의 다음 [추가]를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![앱 게이트웨이 규칙 블레이드][3]

### <a name="step-2"></a><span data-ttu-id="b7350-140">2단계</span><span class="sxs-lookup"><span data-stu-id="b7350-140">Step 2</span></span>

<span data-ttu-id="b7350-141">Hello에 **기본 규칙 추가** 블레이드에서 hello hello 규칙에 대 한 친숙 한 이름을 입력 하 고 hello 이전 단계에서 만든 hello 수신기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="b7350-142">Hello 적절 한 백 엔드 풀 및 설정 하는 http를 선택 하 고 클릭 **확인**</span><span class="sxs-lookup"><span data-stu-id="b7350-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![https 설정 창][4]

<span data-ttu-id="b7350-144">hello 설정은 toohello 응용 프로그램 게이트웨이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="b7350-145">이러한 설정에 대 한 프로세스 저장 hello hello 포털을 통해 또는 PowerShell을 통해 사용할 수 있는 tooview 되기 전에 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="b7350-146">한 번 저장 된 hello 응용 프로그램 게이트웨이 hello 암호화 및 암호 해독의 트래픽 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="b7350-147">응용 프로그램 게이트웨이 hello 및 hello 백 엔드 웹 서버 간의 모든 트래픽은 http를 통해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="b7350-148">Https를 통해 시작 하는 경우 모든 통신 백 toohello 클라이언트 암호화 toohello 클라이언트를 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7350-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7350-149">Next steps</span></span>

<span data-ttu-id="b7350-150">toolearn Azure 응용 프로그램 게이트웨이와 tooconfigure 사용자 지정 상태 프로브 참조 [사용자 지정 상태 프로브를 만들](application-gateway-create-gateway-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7350-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
