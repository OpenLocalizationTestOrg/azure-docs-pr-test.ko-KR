---
title: "RADIUS를 사용하는 RDG 및 Azure MFA 서버 | Microsoft Docs"
description: "RADIUS를 사용하여 RD(Remote Desktop) 게이트웨이 및 Azure Multi-Factor Authentication을 배포하는 데 도움이 되는 Azure Multi-Factor Authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 3b4181701c5df03a3df7e0446b313eac201ad99e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a><span data-ttu-id="e60b0-103">RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버</span><span class="sxs-lookup"><span data-stu-id="e60b0-103">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>
<span data-ttu-id="e60b0-104">종종 RD(Remote Desktop) 게이트웨이는 로컬 NPS(Network Policy Services)를 사용하여 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-104">Often, Remote Desktop (RD) Gateway uses the local Network Policy Services (NPS) to authenticate users.</span></span> <span data-ttu-id="e60b0-105">이 문서에서는 원격 데스크톱 게이트웨이(로컬 NPS를 통해)에서 Multi-Factor Authentication 서버까지 RADIUS 요청을 라우팅하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-105">This article describes how to route RADIUS requests out from the Remote Desktop Gateway (through the local NPS) to the Multi-Factor Authentication Server.</span></span> <span data-ttu-id="e60b0-106">Azure MFA와 RD 게이트웨이를 함께 사용하면 사용자가 강력한 인증을 수행하면서 어디서든 자신의 작업 환경에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-106">The combination of Azure MFA and RD Gateway means that your users can access their work environments from anywhere while performing strong authentication.</span></span> 

<span data-ttu-id="e60b0-107">터미널 서비스에 대한 Windows 인증이 Server 2012 R2에 대해 지원되지 않으므로 MFA 서버와 통합하려면 RD 게이트웨이 및 RADIUS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-107">Since Windows Authentication for terminal services is not supported for Server 2012 R2, use RD Gateway and RADIUS to integrate with MFA Server.</span></span> 

<span data-ttu-id="e60b0-108">별도의 서버에 Multi-Factor Authentication 서버를 설치합니다. 이 서버는 원격 데스크톱 게이트웨이 서버의 NPS로 RADIUS 요청을 다시 프록시합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-108">Install the Azure Multi-Factor Authentication Server on a separate server, which proxies the RADIUS request back to the NPS on the Remote Desktop Gateway Server.</span></span> <span data-ttu-id="e60b0-109">NPS에서 사용자 이름과 암호의 유효성을 검사한 후 Multi-Factor Authentication 서버로 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-109">After NPS validates the username and password, it returns a response to the Multi-Factor Authentication Server.</span></span> <span data-ttu-id="e60b0-110">그런 다음 MFA 서버에서 두 번째 인증 단계를 수행하고 결과를 게이트웨이로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-110">Then, the MFA Server performs the second factor of authentication and returns a result to the gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e60b0-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e60b0-111">Prerequisites</span></span>

- <span data-ttu-id="e60b0-112">도메인에 가입된 Azure MFA 서버.</span><span class="sxs-lookup"><span data-stu-id="e60b0-112">A domain-joined Azure MFA Server.</span></span> <span data-ttu-id="e60b0-113">설치되어 있지 않은 경우 [Azure Multi-factor Authentication 서버 시작](multi-factor-authentication-get-started-server.md)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-113">If you don't have one installed already, follow the steps in [Getting started with the Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server.md).</span></span>
- <span data-ttu-id="e60b0-114">네트워크 정책 서비스를 인증하는 원격 데스크톱 게이트웨이.</span><span class="sxs-lookup"><span data-stu-id="e60b0-114">A Remote Desktop Gateway that authenticates with Network Policy Services.</span></span>

## <a name="configure-the-remote-desktop-gateway"></a><span data-ttu-id="e60b0-115">원격 데스크톱 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="e60b0-115">Configure the Remote Desktop Gateway</span></span>
<span data-ttu-id="e60b0-116">Azure Multi-Factor Authentication 서버에 RADIUS 인증을 보내도록 RD 게이트웨이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-116">Configure the RD Gateway to send RADIUS authentication to an Azure Multi-Factor Authentication Server.</span></span> 

1. <span data-ttu-id="e60b0-117">RD 게이트웨이 관리자에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-117">In RD Gateway Manager, right-click the server name and select **Properties**.</span></span>
2. <span data-ttu-id="e60b0-118">**RD CAP 저장소** 탭으로 이동하고 **NPS를 실행하는 중앙 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-118">Go to the **RD CAP Store** tab and select **Central server running NPS**.</span></span> 
3. <span data-ttu-id="e60b0-119">각 서버의 이름 또는 IP 주소를 입력하여 하나 이상의 Azure Multi-Factor Authentication 서버를 RADIUS 서버로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-119">Add one or more Azure Multi-Factor Authentication Servers as RADIUS servers by entering the name or IP address of each server.</span></span> 
4. <span data-ttu-id="e60b0-120">각 서버에 대한 공유 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-120">Create a shared secret for each server.</span></span>

## <a name="configure-nps"></a><span data-ttu-id="e60b0-121">NPS 구성</span><span class="sxs-lookup"><span data-stu-id="e60b0-121">Configure NPS</span></span>
<span data-ttu-id="e60b0-122">RD 게이트웨이는 NPS를 사용하여 Azure Multi-Factor Authentication에 RADIUS 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-122">The RD Gateway uses NPS to send the RADIUS request to Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="e60b0-123">NPS를 구성하려면 먼저 RD 게이트웨이가 2단계 확인이 완료되기 전에 시간 초과되는 것을 방지하도록 시간 제한 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-123">To configure NPS, first you change the timeout settings to prevent the RD Gateway from timing out before the two-step verification has completed.</span></span> <span data-ttu-id="e60b0-124">그런 다음 MFA 서버에서 RADIUS 인증을 받도록 NPS를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-124">Then, you update NPS to receive RADIUS authentications from your MFA Server.</span></span> <span data-ttu-id="e60b0-125">NPS를 구성하려면 다음 절차를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e60b0-125">Use the following procedure to configure NPS:</span></span>

### <a name="modify-the-timeout-policy"></a><span data-ttu-id="e60b0-126">시간 제한 정책 수정</span><span class="sxs-lookup"><span data-stu-id="e60b0-126">Modify the timeout policy</span></span>

1. <span data-ttu-id="e60b0-127">NPS의 왼쪽 열에서 **RADIUS 클라이언트 및 서버** 메뉴를 열고 **원격 RADIUS 서버 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-127">In NPS, open the **RADIUS Clients and Server** menu in the left column and select **Remote RADIUS Server Groups**.</span></span> 
2. <span data-ttu-id="e60b0-128">**TS 게이트웨이 서버 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-128">Select the **TS GATEWAY SERVER GROUP**.</span></span> 
3. <span data-ttu-id="e60b0-129">**부하 분산** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-129">Go to the **Load Balancing** tab.</span></span> 
4. <span data-ttu-id="e60b0-130">**응답 없이 다음 시간(초)이 경과되면 요청이 손실된 것으로 간주** 및 **서버가 사용 불가능 상태로 표시된 경우 요청 사이의 시간(초)**을 모두 30-60초 사이로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-130">Change both the **Number of seconds without response before request is considered dropped** and the **Number of seconds between requests when server is identified as unavailable** to between 30 and 60 seconds.</span></span> <span data-ttu-id="e60b0-131">(인증하는 동안 여전히 서버가 시간 초과되는 경우 여기로 돌아와서 초 수를 늘립니다.)</span><span class="sxs-lookup"><span data-stu-id="e60b0-131">(If you find that the server still times out during authentication, you can come back here and increase the number of seconds.)</span></span>
5. <span data-ttu-id="e60b0-132">**인증/계정** 탭으로 이동하고 지정된 RADIUS 포트가 Multi-Factor Authentication 서버에서 수신 대기하는 포트와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-132">Go to the **Authentication/Account** tab and check that the RADIUS ports specified match the ports that the Multi-Factor Authentication Server is listening on.</span></span>

### <a name="prepare-nps-to-receive-authentications-from-the-mfa-server"></a><span data-ttu-id="e60b0-133">MFA 서버에서 인증을 받도록 NPS 준비</span><span class="sxs-lookup"><span data-stu-id="e60b0-133">Prepare NPS to receive authentications from the MFA Server</span></span>

1. <span data-ttu-id="e60b0-134">왼쪽 열의 RADIUS 클라이언트 및 서버 아래에서 **RADIUS 클라이언트**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-134">Right-click **RADIUS Clients** under RADIUS Clients and Servers in the left column and select **New**.</span></span>
2. <span data-ttu-id="e60b0-135">Azure Multi-Factor Authentication 서버를 RADIUS 클라이언트로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-135">Add the Azure Multi-Factor Authentication Server as a RADIUS client.</span></span> <span data-ttu-id="e60b0-136">친숙한 이름을 선택하고 공유 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-136">Choose a Friendly name and specify a shared secret.</span></span>
3. <span data-ttu-id="e60b0-137">왼쪽 열에서 **정책** 메뉴를 열고 **연결 요청 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-137">Open the **Policies** menu in the left column and select **Connection Request Policies**.</span></span> <span data-ttu-id="e60b0-138">RD 게이트웨이를 구성할 때 만든 TS 게이트웨이 권한 부여 정책이라는 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-138">You should see a policy called TS GATEWAY AUTHORIZATION POLICY that was created when RD Gateway was configured.</span></span> <span data-ttu-id="e60b0-139">이 정책은 Multi-Factor Authentication 서버에 RADIUS 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-139">This policy forwards RADIUS requests to the Multi-Factor Authentication Server.</span></span>
4. <span data-ttu-id="e60b0-140">**TS 게이트웨이 권한 부여 정책**을 마우스 오른쪽 단추로 클릭하고 **복제 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-140">Right-click **TS GATEWAY AUTHORIZATION POLICY** and select **Duplicate Policy**.</span></span> 
5. <span data-ttu-id="e60b0-141">새 정책을 열고 **조건** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-141">Open the new policy and go to the **Conditions** tab.</span></span>
6. <span data-ttu-id="e60b0-142">Azure Multi-Factor Authentication 서버 RADIUS 클라이언트에 대한 2단계에서 친숙한 이름과 클라이언트 이름이 일치하는 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-142">Add a condition that matches the Client Friendly Name with the Friendly name set in step 2 for the Azure Multi-Factor Authentication Server RADIUS client.</span></span> 
7. <span data-ttu-id="e60b0-143">**설정** 탭으로 이동하고 **인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-143">Go to the **Settings** tab and select **Authentication**.</span></span>
8. <span data-ttu-id="e60b0-144">인증 공급자를 **이 서버에서 요청 인증**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-144">Change the Authentication Provider to **Authenticate requests on this server**.</span></span> <span data-ttu-id="e60b0-145">이 정책은 NPS가 Azure MFA 서버에서 RADIUS 요청을 수신할 때 루프 조건이 될 수 있는 Azure Multi-Factor Authentication 서버에 RADIUS 요청을 전송하는 대신 로컬로 인증이 발생하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-145">This policy ensures that when NPS receives a RADIUS request from the Azure MFA Server, the authentication occurs locally instead of sending a RADIUS request back to the Azure Multi-Factor Authentication Server, which would result in a loop condition.</span></span> 
9. <span data-ttu-id="e60b0-146">루프 조건을 방지하려면 새 정책이 **연결 요청 정책** 창의 원래 정책 위에 정렬되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-146">To prevent a loop condition, make sure that the new policy is ordered ABOVE the original policy in the **Connection Request Policies** pane.</span></span>

## <a name="configure-azure-multi-factor-authentication"></a><span data-ttu-id="e60b0-147">Azure Multi-Factor Authentication 구성</span><span class="sxs-lookup"><span data-stu-id="e60b0-147">Configure Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="e60b0-148">Azure Multi-Factor Authentication 서버는 RD 게이트웨이 및 NPS 사이의 RADIUS 프록시로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-148">The Azure Multi-Factor Authentication Server is configured as a RADIUS proxy between RD Gateway and NPS.</span></span>  <span data-ttu-id="e60b0-149">RD 게이트웨이 서버와 별개의 도메인에 가입된 서버에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-149">It should be installed on a domain-joined server that is separate from the RD Gateway server.</span></span> <span data-ttu-id="e60b0-150">다음 절차에 따라 Azure Multi-Factor Authentication 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-150">Use the following procedure to configure the Azure Multi-Factor Authentication Server.</span></span>

1. <span data-ttu-id="e60b0-151">Azure Multi-Factor Authentication 서버를 열고 RADIUS 인증 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-151">Open the Azure Multi-Factor Authentication Server and select the RADIUS Authentication icon.</span></span> 
2. <span data-ttu-id="e60b0-152">**RADIUS 인증 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-152">Check the **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="e60b0-153">클라이언트 탭에서 포트가 NPS에 구성된 포트와 일치하는지 확인한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-153">On the Clients tab, ensure the ports match what is configured in NPS then select **Add**.</span></span>
4. <span data-ttu-id="e60b0-154">RD 게이트웨이 서버 IP 주소, 응용 프로그램 이름(선택 사항) 및 공유 암호를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-154">Add the RD Gateway server IP address, application name (optional), and a shared secret.</span></span> <span data-ttu-id="e60b0-155">공유 암호는 Azure Multi-Factor Authentication 서버 및 RD 게이트웨이 모두에서 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-155">The shared secret needs to be the same on both the Azure Multi-Factor Authentication Server and RD Gateway.</span></span>
3. <span data-ttu-id="e60b0-156">**대상** 탭으로 이동하고 **RADIUS 서버** 라디오 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-156">Go to the **Target** tab and select the **RADIUS server(s)** radio button.</span></span>
4. <span data-ttu-id="e60b0-157">**추가**를 선택하고 NPS 서버의 IP 주소, 공유 암호 및 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-157">Select **Add** and enter the IP address, shared secret, and ports of the NPS server.</span></span> <span data-ttu-id="e60b0-158">중앙 NPS를 사용하지 않는 한 RADIUS 클라이언트와 RADIUS 대상은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-158">Unless using a central NPS, the RADIUS client and RADIUS target are the same.</span></span> <span data-ttu-id="e60b0-159">공유 암호는 NPS 서버에서 RADIUS 클라이언트 섹션의 설정 하나와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e60b0-159">The shared secret must match the one setup in the RADIUS client section of the NPS server.</span></span>

![RADIUS 인증](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a><span data-ttu-id="e60b0-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e60b0-161">Next steps</span></span>

- <span data-ttu-id="e60b0-162">Azure MFA 및 [IIS 웹앱](multi-factor-authentication-get-started-server-iis.md) 통합</span><span class="sxs-lookup"><span data-stu-id="e60b0-162">Integrate Azure MFA and [IIS web apps](multi-factor-authentication-get-started-server-iis.md)</span></span>

- <span data-ttu-id="e60b0-163">[Azure Multi-Factor Authentication FAQ](multi-factor-authentication-faq.md)에서 답변 얻기</span><span class="sxs-lookup"><span data-stu-id="e60b0-163">Get answers in the [Azure Multi-Factor Authentication FAQ](multi-factor-authentication-faq.md)</span></span>
