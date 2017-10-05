---
title: "RADIUS 인증 및 Azure MFA 서버 | Microsoft Docs"
description: "RADIUS 인증 및 Azure Multi-Factor Authentication을 배포하는 데 도움이 되는 Azure Multi-Factor Authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: a4c52cc40b17902d92f7a94028ddb3c641911e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="58afc-103">Azure Multi-Factor Authentication 서버와 RADIUS 인증 통합</span><span class="sxs-lookup"><span data-stu-id="58afc-103">Integrate RADIUS authentication with Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="58afc-104">Azure MFA 서버의 RADIUS 인증 섹션을 사용하여 RADIUS 인증을 사용하도록 설정하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-104">Use the RADIUS Authentication section of Azure MFA Server to enable and configure RADIUS authentication.</span></span> <span data-ttu-id="58afc-105">RADIUS는 인증 요청을 수락하고 이 요청을 처리하는 표준 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-105">RADIUS is a standard protocol to accept authentication requests and to process those requests.</span></span> <span data-ttu-id="58afc-106">Azure Multi-Factor Authentication 서버는 RADIUS 서버 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-106">The Azure Multi-Factor Authentication Server acts as a RADIUS server.</span></span> <span data-ttu-id="58afc-107">RADIUS 클라이언트(VPN 어플라이언스)와 AD(Active Directory), LDAP 디렉터리 또는 다른 RADIUS 서버일 수 있는 인증 대상 사이에 삽입하여 Azure Multi-Factor Authentication을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-107">Insert it between your RADIUS client (VPN appliance) and your authentication target, which could be Active Directory (AD), an LDAP directory, or another RADIUS server to add Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="58afc-108">Azure MFA(Multi-Factor Authentication)가 동작하려면 클라이언트 서버와 인증 대상 모두와 통신할 수 있도록 Azure MFA 서버를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-108">For Azure Multi-Factor Authentication (MFA) to function, you must configure the Azure MFA Server so that it can communicate with both the client servers and the authentication target.</span></span> <span data-ttu-id="58afc-109">Azure MFA 서버는 RADIUS 클라이언트의 요청을 수락하고, 인증 대상에 대해 자격 증명의 유효성을 검사하고, Azure Multi-Factor Authentication을 추가하고 다시 RADIUS 클라이언트로 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-109">The Azure MFA Server accepts requests from a RADIUS client, validates credentials against the authentication target, adds Azure Multi-Factor Authentication, and sends a response back to the RADIUS client.</span></span> <span data-ttu-id="58afc-110">기본 인증 및 Azure Multi-Factor Authentication 모두가 성공한 경우에만 인증 요청이 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-110">The authentication request only succeeds if both the primary authentication and the Azure Multi-Factor Authentication succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="58afc-111">MFA 서버는 RADIUS 서버로 작동하는 경우 PAP(암호 인증 프로토콜)와 MSCHAPv2(Microsoft의 Challenge-Handshake 인증 프로토콜) RADIUS 프로토콜만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-111">The MFA Server only supports PAP (password authentication protocol) and MSCHAPv2 (Microsoft's Challenge-Handshake Authentication Protocol) RADIUS protocols when acting as a RADIUS server.</span></span>  <span data-ttu-id="58afc-112">EAP(확장할 수 있는 인증 프로토콜) 같은 기타 프로토콜은 MFA 서버가 프로토콜을 지원하는 또 다른 RADIUS 서버에 대한 RADIUS 프록시로 작동하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-112">Other protocols, like EAP (extensible authentication protocol), can be used when the MFA server acts as a RADIUS proxy to another RADIUS server that supports that protocol.</span></span>
>
> <span data-ttu-id="58afc-113">이 구성에서 MFA 서버가 대체 프로토콜을 사용하여 성공적인 RADIUS Challenge 응답을 시작할 수 없기 때문에 단방향 SMS 및 OATH 토큰이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-113">In this configuration, one-way SMS and OATH tokens don't work since the MFA Server can't initiate a successful RADIUS Challenge response using alternative protocols.</span></span>

![RADIUS 인증](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a><span data-ttu-id="58afc-115">RADIUS 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="58afc-115">Add a RADIUS client</span></span>
<span data-ttu-id="58afc-116">RADIUS 인증을 구성하려면 Windows 서버에 Azure Multi-Factor Authentication 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-116">To configure RADIUS authentication, install the Azure Multi-Factor Authentication Server on a Windows server.</span></span> <span data-ttu-id="58afc-117">Active Directory 환경에 있으면 서버가 네트워크 내의 도메인에 가입되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-117">If you have an Active Directory environment, the server should be joined to the domain inside the network.</span></span> <span data-ttu-id="58afc-118">다음 절차에 따라 Azure Multi-Factor Authentication 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-118">Use the following procedure to configure the Azure Multi-Factor Authentication Server:</span></span>

1. <span data-ttu-id="58afc-119">Azure Multi-Factor Authentication 서버에서 왼쪽 메뉴의 RADIUS 인증 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-119">In the Azure Multi-Factor Authentication Server, click the RADIUS Authentication icon in the left menu.</span></span>
2. <span data-ttu-id="58afc-120">**RADIUS 인증 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-120">Check the **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="58afc-121">클라이언트 탭에서 Azure MFA RADIUS 서비스가 비표준 포트에서 RADIUS 요청을 수신해야 하는 경우 인증 및 계정 포트를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-121">On the Clients tab, change the Authentication and Accounting ports if the Azure MFA RADIUS service needs to listen for RADIUS requests on non-standard ports.</span></span>
4. <span data-ttu-id="58afc-122">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-122">Click **Add**.</span></span>
5. <span data-ttu-id="58afc-123">Azure Multi-Factor Authentication 서버, 응용 프로그램 이름(옵션) 및 공유 암호를 인증하는 어플라이언스/서버의 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-123">Enter the IP address of the appliance/server that will authenticate to the Azure Multi-Factor Authentication Server, an application name (optional), and a shared secret.</span></span>

  <span data-ttu-id="58afc-124">응용 프로그램 이름이 Azure Multi-Factor Authentication 보고서에 나타나며 SMS 또는 모바일 앱 인증 메시지 내에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-124">The application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>

  <span data-ttu-id="58afc-125">공유 암호는 Azure Multi-Factor Authentication 서버 및 어플라이언스/서버 모두에서 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-125">The shared secret needs to be the same on both the Azure Multi-Factor Authentication Server and appliance/server.</span></span>

6. <span data-ttu-id="58afc-126">모든 사용자를 내부 서버로 가져왔거나 가져올 예정이고 Multi-Factor Authentication을 사용하려는 경우 **Require Azure Multi-Factor Authentication user match**(Azure Multi-Factor Authentication 사용자 일치 필요) 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-126">Check the **Require Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to multi-factor authentication.</span></span> <span data-ttu-id="58afc-127">많은 수의 사용자를 서버에 아직 가져오지 않았거나 2단계 확인에서 제외할 예정이면 이 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-127">If a significant number of users have not yet been imported into the Server and/or will be exempt from two-step verification, leave the box unchecked.</span></span>
7. <span data-ttu-id="58afc-128">대역외 전화 통화, SMS 또는 푸시 알림에 대한 대체(fallback)로 모바일 확인 앱에서 OATH 암호를 사용하려는 경우 **대체 OATH 토큰 사용** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-128">Check the **Enable fallback OATH token** box if you want to use OATH passcodes from mobile verification apps as a fallback to the out-of-band phone call, SMS, or push notification.</span></span>
8. <span data-ttu-id="58afc-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-129">Click **OK**.</span></span>

<span data-ttu-id="58afc-130">4-8단계를 반복하여 필요한 만큼 추가 RADIUS 클라이언트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-130">Repeat steps 4 through 8 to add as many additional RADIUS clients as you need.</span></span>

## <a name="configure-your-radius-client"></a><span data-ttu-id="58afc-131">RADIUS 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="58afc-131">Configure your RADIUS client</span></span>

1. <span data-ttu-id="58afc-132">**대상** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-132">Click the **Target** tab.</span></span>
2. <span data-ttu-id="58afc-133">Azure MFA 서버가 Active Directory 환경의 도메인 연결된 서버에 설치된 경우 Windows 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-133">If the Azure MFA Server is installed on a domain-joined server in an Active Directory environment, select Windows domain.</span></span>
3. <span data-ttu-id="58afc-134">LDAP 디렉터리에 대해 사용자를 인증해야 하는 경우 **LDAP 바인딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-134">If users should be authenticated against an LDAP directory, select **LDAP bind**.</span></span>

  <span data-ttu-id="58afc-135">LDAP 바인딩을 사용하려면 디렉터리 통합 아이콘을 클릭하고 서버가 디렉터리에 바인딩할 수 있도록 설정 탭에서 LDAP 구성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-135">To use LDAP bind, click the Directory Integration icon and edit the LDAP configuration on the Settings tab so that the Server can bind to your directory.</span></span> <span data-ttu-id="58afc-136">LDAP 구성을 위한 지침은 [LDAP 프록시 구성 가이드](multi-factor-authentication-get-started-server-ldap.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-136">Instructions for configuring LDAP can be found in the [LDAP Proxy configuration guide](multi-factor-authentication-get-started-server-ldap.md).</span></span>

4. <span data-ttu-id="58afc-137">다른 RADIUS 서버에 대해 사용자를 인증해야 하는 경우 RADIUS 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-137">If users should be authenticated against another RADIUS server, select RADIUS server(s).</span></span>
5. <span data-ttu-id="58afc-138">**추가**를 클릭하여 Azure MFA 서버가 RADIUS 요청을 프록시할 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-138">Click **Add** to configure the server to which the Azure MFA Server will proxy the RADIUS requests.</span></span>
6. <span data-ttu-id="58afc-139">RADIUS 서버 추가 대화 상자에서 RADIUS 서버의 IP 주소와 공유 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-139">In the Add RADIUS Server dialog box, enter the IP address of the RADIUS server and a shared secret.</span></span>

  <span data-ttu-id="58afc-140">공유 암호는 Azure Multi-Factor Authentication 서버 및 RADIUS 서버 모두에서 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-140">The shared secret needs to be the same on both the Azure Multi-Factor Authentication Server and RADIUS server.</span></span> <span data-ttu-id="58afc-141">RADIUS 서버에서 다른 포트를 사용하는 경우 인증 포트 및 계정 포트를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-141">Change the Authentication port and Accounting port if different ports are used by the RADIUS server.</span></span>

7. <span data-ttu-id="58afc-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-142">Click **OK**.</span></span>
8. <span data-ttu-id="58afc-143">Azure MFA 서버에서 전송되는 액세스 요청을 처리할 수 있도록 다른 RADIUS 서버에서 RADIUS 클라이언트로 Azure MFA 서버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-143">Add the Azure MFA Server as a RADIUS client in the other RADIUS server so that it can process access requests sent to it from the Azure MFA Server.</span></span> <span data-ttu-id="58afc-144">Azure Multi-Factor Authentication 서버에 구성된 동일한 공유 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-144">Use the same shared secret configured in the Azure Multi-Factor Authentication Server.</span></span>

<span data-ttu-id="58afc-145">해당 단계를 반복하여 더 많은 RADIUS 서버를 추가하고 **위로 이동** 및 **아래로 이동** 단추로 Azure MFA 서버에서 호출해야 하는 순서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-145">Repeat these steps to add more RADIUS servers and configure the order in which the Azure MFA Server should call them with the **Move Up** and **Move Down** buttons.</span></span>

<span data-ttu-id="58afc-146">Azure Multi-Factor Authentication 서버 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-146">This completes the Azure Multi-Factor Authentication Server configuration.</span></span> <span data-ttu-id="58afc-147">이제 서버는 구성된 클라이언트에서의 RADIUS 액세스 요청에 대해 구성된 포트에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-147">The Server is now listening on the configured ports for RADIUS access requests from the configured clients.</span></span>   

## <a name="radius-client-configuration"></a><span data-ttu-id="58afc-148">RADIUS 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="58afc-148">RADIUS Client configuration</span></span>
<span data-ttu-id="58afc-149">RADIUS 클라이언트를 구성하려면 지침을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="58afc-149">To configure the RADIUS client, use the guidelines:</span></span>

* <span data-ttu-id="58afc-150">RADIUS 서버 역할을 Azure Multi-Factor Authentication 서버의 IP 주소에 RADIUS를 통해 인증하도록 어플라이언스/서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-150">Configure your appliance/server to authenticate via RADIUS to the Azure Multi-Factor Authentication Server’s IP address, which will act as the RADIUS server.</span></span>
* <span data-ttu-id="58afc-151">이전에 구성된 동일한 공유 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-151">Use the same shared secret that was configured earlier.</span></span>
* <span data-ttu-id="58afc-152">사용자의 자격 증명의 유효성을 검사하고, 2단계 인증을 수행하고, 자신의 응답을 수신한 다음 RADIUS 액세스 요청에 응답할 시간이 있도록 30-60초 사이로 RADIUS 제한 시간을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58afc-152">Configure the RADIUS timeout to 30-60 seconds so that there is time to validate the user’s credentials, perform two-step verification, receive their response, and then respond to the RADIUS access request.</span></span>
