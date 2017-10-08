---
title: "인증 및 Azure MFA 서버 aaaRADIUS | Microsoft Docs"
description: "RADIUS 인증 및 Azure Multi-factor Authentication 서버를 배포 하는 데 도움이 되는 hello Azure multi-factor authentication 페이지입니다."
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
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="6eeec-103">Azure Multi-Factor Authentication 서버와 RADIUS 인증 통합</span><span class="sxs-lookup"><span data-stu-id="6eeec-103">Integrate RADIUS authentication with Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="6eeec-104">Azure MFA 서버 tooenable의 hello RADIUS 인증 섹션을 사용 하 고 RADIUS 인증을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-104">Use hello RADIUS Authentication section of Azure MFA Server tooenable and configure RADIUS authentication.</span></span> <span data-ttu-id="6eeec-105">RADIUS는 표준 프로토콜 tooaccept 인증 요청 및 tooprocess 이러한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-105">RADIUS is a standard protocol tooaccept authentication requests and tooprocess those requests.</span></span> <span data-ttu-id="6eeec-106">hello Azure Multi-factor Authentication 서버는 RADIUS 서버로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-106">hello Azure Multi-Factor Authentication Server acts as a RADIUS server.</span></span> <span data-ttu-id="6eeec-107">RADIUS 클라이언트 (VPN 어플라이언스)와 Active Directory (AD), LDAP 디렉터리, 또는 다른 RADIUS 서버 tooadd Azure Multi-factor Authentication 될 수 있는 인증 대상 사이 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-107">Insert it between your RADIUS client (VPN appliance) and your authentication target, which could be Active Directory (AD), an LDAP directory, or another RADIUS server tooadd Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="6eeec-108">Azure Multi-factor Authentication (MFA) toofunction hello 클라이언트 서버 및 hello 인증 대상 모두와 통신할 수 있도록 hello Azure MFA 서버를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-108">For Azure Multi-Factor Authentication (MFA) toofunction, you must configure hello Azure MFA Server so that it can communicate with both hello client servers and hello authentication target.</span></span> <span data-ttu-id="6eeec-109">Azure MFA 서버 hello RADIUS 클라이언트의 요청을 수락 하며 hello 인증 대상에 대해 자격 증명의 유효성을 검사 하 Azure Multi-factor Authentication을 추가 및 응답 백 toohello RADIUS 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-109">hello Azure MFA Server accepts requests from a RADIUS client, validates credentials against hello authentication target, adds Azure Multi-Factor Authentication, and sends a response back toohello RADIUS client.</span></span> <span data-ttu-id="6eeec-110">hello 인증 요청이 hello 기본 인증 및 hello Azure Multi-factor Authentication이 성공 하는 경우에 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-110">hello authentication request only succeeds if both hello primary authentication and hello Azure Multi-Factor Authentication succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="6eeec-111">MFA 서버 hello PAP (암호 인증 프로토콜) 및 MSCHAPv2 지원 (Microsoft Challenge Handshake 인증 프로토콜)를 RADIUS 서버로 작동할 때 RADIUS 프로토콜을 통해.</span><span class="sxs-lookup"><span data-stu-id="6eeec-111">hello MFA Server only supports PAP (password authentication protocol) and MSCHAPv2 (Microsoft's Challenge-Handshake Authentication Protocol) RADIUS protocols when acting as a RADIUS server.</span></span>  <span data-ttu-id="6eeec-112">Hello MFA 서버가 해당 프로토콜을 지 원하는 RADIUS 프록시 tooanother RADIUS 서버 역할을 하는 경우에 EAP (확장할 수 있는 인증 프로토콜)와 같은 다른 프로토콜을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-112">Other protocols, like EAP (extensible authentication protocol), can be used when hello MFA server acts as a RADIUS proxy tooanother RADIUS server that supports that protocol.</span></span>
>
> <span data-ttu-id="6eeec-113">이 구성에서는 단방향 SMS 및 OATH 토큰 hello와 MFA 서버를 시작할 수 없습니다. 대체 프로토콜을 사용 하 여 성공적인 RADIUS 챌린지 응답 하므로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-113">In this configuration, one-way SMS and OATH tokens don't work since hello MFA Server can't initiate a successful RADIUS Challenge response using alternative protocols.</span></span>

![RADIUS 인증](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a><span data-ttu-id="6eeec-115">RADIUS 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="6eeec-115">Add a RADIUS client</span></span>
<span data-ttu-id="6eeec-116">Windows 서버에 Azure Multi-factor Authentication 서버 설치 hello tooconfigure RADIUS 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-116">tooconfigure RADIUS authentication, install hello Azure Multi-Factor Authentication Server on a Windows server.</span></span> <span data-ttu-id="6eeec-117">Active Directory 환경에 있으면 hello 서버 hello 네트워크 내부 조인된 toohello 도메인 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-117">If you have an Active Directory environment, hello server should be joined toohello domain inside hello network.</span></span> <span data-ttu-id="6eeec-118">다음 프로시저 tooconfigure hello Azure Multi-factor Authentication 서버 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-118">Use hello following procedure tooconfigure hello Azure Multi-Factor Authentication Server:</span></span>

1. <span data-ttu-id="6eeec-119">Azure Multi-factor Authentication 서버 hello hello 왼쪽된 메뉴에 hello RADIUS 인증 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-119">In hello Azure Multi-Factor Authentication Server, click hello RADIUS Authentication icon in hello left menu.</span></span>
2. <span data-ttu-id="6eeec-120">Hello 확인 **RADIUS 인증 사용** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-120">Check hello **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="6eeec-121">Hello 클라이언트 탭에서 hello Azure MFA RADIUS 서비스가 비표준 포트에서 RADIUS 요청 toolisten 있어야 하는 경우 hello 인증 및 계정 포트를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-121">On hello Clients tab, change hello Authentication and Accounting ports if hello Azure MFA RADIUS service needs toolisten for RADIUS requests on non-standard ports.</span></span>
4. <span data-ttu-id="6eeec-122">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-122">Click **Add**.</span></span>
5. <span data-ttu-id="6eeec-123">Hello 어플라이언스/서버의 toohello Azure Multi-factor Authentication 서버, 프로그램 응용 프로그램 이름 (선택 사항) 및 공유 암호를 인증 하는 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-123">Enter hello IP address of hello appliance/server that will authenticate toohello Azure Multi-Factor Authentication Server, an application name (optional), and a shared secret.</span></span>

  <span data-ttu-id="6eeec-124">hello 응용 프로그램 이름은 Azure Multi-factor Authentication 보고서에 표시 되며 SMS 또는 모바일 앱 인증 메시지 내에서 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-124">hello application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>

  <span data-ttu-id="6eeec-125">두 hello Azure Multi-factor Authentication 서버에서 동일 및 어플라이언스/서버 hello 비밀 요구 toobe hello를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-125">hello shared secret needs toobe hello same on both hello Azure Multi-Factor Authentication Server and appliance/server.</span></span>

6. <span data-ttu-id="6eeec-126">Hello 확인 **Multi-factor Authentication 사용자 일치** 모든 사용자가 낮거나 서버 hello 및 주체 toomulti 2 단계 인증으로 가져올 경우 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-126">Check hello **Require Multi-Factor Authentication user match** box if all users have been or will be imported into hello Server and subject toomulti-factor authentication.</span></span> <span data-ttu-id="6eeec-127">많은 수의 사용자가을 아직 가져오지 서버 hello에 2 단계 인증에서 제외 될 경우, hello 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-127">If a significant number of users have not yet been imported into hello Server and/or will be exempt from two-step verification, leave hello box unchecked.</span></span>
7. <span data-ttu-id="6eeec-128">Hello 확인 **대체 OATH 토큰 사용** 대체 toohello 대역의 전화 통화, SMS,으로 toouse OATH 암호 확인 모바일 앱에서 사용할 또는 푸시 알림 경우 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-128">Check hello **Enable fallback OATH token** box if you want toouse OATH passcodes from mobile verification apps as a fallback toohello out-of-band phone call, SMS, or push notification.</span></span>
8. <span data-ttu-id="6eeec-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-129">Click **OK**.</span></span>

<span data-ttu-id="6eeec-130">필요에 따라 많은 추가 RADIUS 클라이언트 8 tooadd-4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-130">Repeat steps 4 through 8 tooadd as many additional RADIUS clients as you need.</span></span>

## <a name="configure-your-radius-client"></a><span data-ttu-id="6eeec-131">RADIUS 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="6eeec-131">Configure your RADIUS client</span></span>

1. <span data-ttu-id="6eeec-132">Hello 클릭 **대상** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-132">Click hello **Target** tab.</span></span>
2. <span data-ttu-id="6eeec-133">Azure MFA 서버 hello가 Active Directory 환경에 도메인 가입 서버에 설치 되어 Windows 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-133">If hello Azure MFA Server is installed on a domain-joined server in an Active Directory environment, select Windows domain.</span></span>
3. <span data-ttu-id="6eeec-134">LDAP 디렉터리에 대해 사용자를 인증해야 하는 경우 **LDAP 바인딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-134">If users should be authenticated against an LDAP directory, select **LDAP bind**.</span></span>

  <span data-ttu-id="6eeec-135">toouse LDAP 바인딩 hello 디렉터리 통합 아이콘을 클릭 하 고 hello 서버 바인딩할 수 tooyour 디렉터리 있도록 hello 설정 탭에서 hello LDAP 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-135">toouse LDAP bind, click hello Directory Integration icon and edit hello LDAP configuration on hello Settings tab so that hello Server can bind tooyour directory.</span></span> <span data-ttu-id="6eeec-136">Hello에서 LDAP를 구성 하기 위한 지침을 확인할 수 있습니다 [LDAP 프록시 구성 가이드](multi-factor-authentication-get-started-server-ldap.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-136">Instructions for configuring LDAP can be found in hello [LDAP Proxy configuration guide](multi-factor-authentication-get-started-server-ldap.md).</span></span>

4. <span data-ttu-id="6eeec-137">다른 RADIUS 서버에 대해 사용자를 인증해야 하는 경우 RADIUS 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-137">If users should be authenticated against another RADIUS server, select RADIUS server(s).</span></span>
5. <span data-ttu-id="6eeec-138">클릭 **추가** tooconfigure hello 서버 toowhich hello Azure MFA 서버는 프록시 hello RADIUS 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-138">Click **Add** tooconfigure hello server toowhich hello Azure MFA Server will proxy hello RADIUS requests.</span></span>
6. <span data-ttu-id="6eeec-139">Hello RADIUS 서버 추가 대화 상자에서 hello RADIUS 서버 및 공유 암호 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-139">In hello Add RADIUS Server dialog box, enter hello IP address of hello RADIUS server and a shared secret.</span></span>

  <span data-ttu-id="6eeec-140">두 hello Azure Multi-factor Authentication 서버에서 동일 하 고 RADIUS 서버 hello 비밀 요구 toobe hello를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-140">hello shared secret needs toobe hello same on both hello Azure Multi-Factor Authentication Server and RADIUS server.</span></span> <span data-ttu-id="6eeec-141">Hello RADIUS 서버에서 다른 포트를 사용 하는 경우 hello 인증 포트와 계정 포트를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-141">Change hello Authentication port and Accounting port if different ports are used by hello RADIUS server.</span></span>

7. <span data-ttu-id="6eeec-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-142">Click **OK**.</span></span>
8. <span data-ttu-id="6eeec-143">Hello Azure MFA 서버를 RADIUS 클라이언트로 추가 hello에 다른 RADIUS 서버로 tooit hello Azure MFA 서버에서에서 보낸 액세스 요청을 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-143">Add hello Azure MFA Server as a RADIUS client in hello other RADIUS server so that it can process access requests sent tooit from hello Azure MFA Server.</span></span> <span data-ttu-id="6eeec-144">동일한 hello Azure Multi-factor Authentication 서버에서에서 구성 된 비밀을 공유 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-144">Use hello same shared secret configured in hello Azure Multi-Factor Authentication Server.</span></span>

<span data-ttu-id="6eeec-145">이러한 단계 tooadd RADIUS 서버를 더 반복한 hello 순서는 hello에 Azure MFA 서버를 호출 하 hello 구성 **위로 이동** 및 **아래로 이동** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-145">Repeat these steps tooadd more RADIUS servers and configure hello order in which hello Azure MFA Server should call them with hello **Move Up** and **Move Down** buttons.</span></span>

<span data-ttu-id="6eeec-146">이 hello Azure Multi-factor Authentication 서버 구성이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-146">This completes hello Azure Multi-Factor Authentication Server configuration.</span></span> <span data-ttu-id="6eeec-147">서버 hello이 이제 hello 구성 된 클라이언트로부터 RADIUS 액세스 요청에 대 한 hello 구성 된 포트에서 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-147">hello Server is now listening on hello configured ports for RADIUS access requests from hello configured clients.</span></span>   

## <a name="radius-client-configuration"></a><span data-ttu-id="6eeec-148">RADIUS 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="6eeec-148">RADIUS Client configuration</span></span>
<span data-ttu-id="6eeec-149">tooconfigure hello RADIUS 클라이언트 hello 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6eeec-149">tooconfigure hello RADIUS client, use hello guidelines:</span></span>

* <span data-ttu-id="6eeec-150">hello RADIUS 서버 역할을 RADIUS toohello Azure Multi-factor Authentication 서버의 IP 주소를 통해 어플라이언스/서버 tooauthenticate 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-150">Configure your appliance/server tooauthenticate via RADIUS toohello Azure Multi-Factor Authentication Server’s IP address, which will act as hello RADIUS server.</span></span>
* <span data-ttu-id="6eeec-151">동일한 공유 암호를 이전에 구성 된 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-151">Use hello same shared secret that was configured earlier.</span></span>
* <span data-ttu-id="6eeec-152">시간 toovalidate hello 사용자의 자격 증명 있도록 hello RADIUS 제한 시간 too30 ~ 60 초로 구성, 2 단계 인증을 수행, 해당 응답을 받 및 다음 toohello RADIUS 액세스 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eeec-152">Configure hello RADIUS timeout too30-60 seconds so that there is time toovalidate hello user’s credentials, perform two-step verification, receive their response, and then respond toohello RADIUS access request.</span></span>
