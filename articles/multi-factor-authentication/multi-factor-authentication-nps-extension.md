---
title: "aaaUse 기존 NPS 서버 tooprovide Azure MFA 기능 | Microsoft Docs"
description: "Azure Multi-factor Authentication에 대 한 네트워크 정책 서버 확장 hello 간단한 솔루션 tooadd 클라우드 기반 2 단계 vericiation 기능 tooyour 기존 인증 인프라입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a><span data-ttu-id="5c64c-103">기존 NPS 인프라를 Azure Multi-Factor Authentication과 통합</span><span class="sxs-lookup"><span data-stu-id="5c64c-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="5c64c-104">클라우드 기반 MFA 기능 tooyour 인증 인프라 기존 서버를 사용 하 여 hello Azure MFA에 대 한 정책 서버 NPS (네트워크) 확장을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-104">hello Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities tooyour authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="5c64c-105">NPS 확장 hello로 tooinstall를 구성 하 고 새 서버를 관리할 필요 없이 전화 통화, 문자 메시지 또는 전화 앱 확인 tooyour 기존 인증 흐름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-105">With hello NPS extension, you can add phone call, text message, or phone app verification tooyour existing authentication flow without having tooinstall, configure, and maintain new servers.</span></span> 

<span data-ttu-id="5c64c-106">Hello Azure MFA 서버를 배포 하지 않고 tooprotect VPN 연결 하려는 조직에이 확장 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-106">This extension was created for organizations that want tooprotect VPN connections without deploying hello Azure MFA Server.</span></span> <span data-ttu-id="5c64c-107">hello NPS 확장 페더레이션 방식 또는 동기화 된 사용자에 대 한 인증의 두 번째 요소를 RADIUS와 클라우드 기반 Azure MFA tooprovide 사이의 어댑터로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-107">hello NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA tooprovide a second factor of authentication for federated or synced users.</span></span>

<span data-ttu-id="5c64c-108">Azure MFA에 대 한 hello NPS 확장을 사용 하는 경우 다음과 같은 구성 요소가 hello hello 인증 흐름에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-108">When using hello NPS extension for Azure MFA, hello authentication flow includes hello following components:</span></span> 

1. <span data-ttu-id="5c64c-109">**NAS/VPN 서버** VPN 클라이언트에서 요청을 받아 RADIUS 요청 tooNPS 서버로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests tooNPS servers.</span></span> 
2. <span data-ttu-id="5c64c-110">**NPS 서버** tooActive 디렉터리 tooperform hello 기본 인증 hello RADIUS 요청 하 고, 요청이 성공 하면 전달 hello 요청 tooany 설치 된 확장에 대 한 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-110">**NPS Server** connects tooActive Directory tooperform hello primary authentication for hello RADIUS requests and, upon success, passes hello request tooany installed extensions.</span></span>  
3. <span data-ttu-id="5c64c-111">**NPS 확장** hello 보조 인증에 대 한 요청 tooAzure MFA를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-111">**NPS Extension** triggers a request tooAzure MFA for hello secondary authentication.</span></span> <span data-ttu-id="5c64c-112">Hello 확장 hello 응답을 받은 후 및 hello MFA 시도 성공 하면 Azure STS에서 발급 하는 MFA 클레임을 포함 하는 보안 토큰에 hello NPS 서버를 제공 하 여 hello 인증 요청이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-112">Once hello extension receives hello response, and if hello MFA challenge succeeds, it completes hello authentication request by providing hello NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="5c64c-113">**Azure MFA** Azure Active Directory tooretrieve hello 사용자 세부 정보와 통신 하 고 확인 방법을 구성 toohello 사용자를 사용 하 여 hello 보조 인증을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-113">**Azure MFA** communicates with Azure Active Directory tooretrieve hello user’s details and performs hello secondary authentication using a verification method configured toohello user.</span></span>

<span data-ttu-id="5c64c-114">다이어그램을 다음 hello이 높은 수준의 인증 요청 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-114">hello following diagram illustrates this high-level authentication request flow:</span></span> 

![인증 흐름 다이어그램](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="5c64c-116">배포 계획</span><span class="sxs-lookup"><span data-stu-id="5c64c-116">Plan your deployment</span></span>

<span data-ttu-id="5c64c-117">특별 한 구성이 필요 하지 hello NPS 확장은 자동 중복성을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-117">hello NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span>

<span data-ttu-id="5c64c-118">Azure MFA가 사용되는 NPS 서버를 필요한 만큼 많이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-118">You can create as many Azure MFA-enabled NPS servers as you need.</span></span> <span data-ttu-id="5c64c-119">여러 서버를 설치한 경우 중 각각에 대해 다른 클라이언트 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="5c64c-120">각 서버에 대한 인증서를 만드는 것은 각 인증서를 개별적으로 업데이트할 수 있고 모든 서버 간의 가동 중지 시간을 걱정하지 않아도 된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span>

<span data-ttu-id="5c64c-121">VPN 서버 67gb toobe hello 새 Azure MFA 사용이 가능한 NPS 서버를 인식 하므로 인증 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-121">VPN servers route authentication requests, so they need toobe aware of hello new Azure MFA-enabled NPS servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c64c-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5c64c-122">Prerequisites</span></span>

<span data-ttu-id="5c64c-123">hello NPS 확장은 기존 인프라와 toowork는 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-123">hello NPS extension is meant toowork with your existing infrastructure.</span></span> <span data-ttu-id="5c64c-124">시작 하기 전에 필수 구성 요소를 다음 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-124">Make sure you have hello following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="5c64c-125">라이선스</span><span class="sxs-lookup"><span data-stu-id="5c64c-125">Licenses</span></span>

<span data-ttu-id="5c64c-126">hello Azure MFA에 대 한 NPS 확장으로 사용할 수 있는 toocustomers는 [Azure Multi-factor Authentication에 대 한 라이선스](multi-factor-authentication.md) (Azure AD Premium, EMS 또는 MFA 구독에 포함 됨).</span><span class="sxs-lookup"><span data-stu-id="5c64c-126">hello NPS Extension for Azure MFA is available toocustomers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span></span>

### <a name="software"></a><span data-ttu-id="5c64c-127">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="5c64c-127">Software</span></span>

<span data-ttu-id="5c64c-128">Windows Server 2008 R2 SP1 이상</span><span class="sxs-lookup"><span data-stu-id="5c64c-128">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="5c64c-129">라이브러리</span><span class="sxs-lookup"><span data-stu-id="5c64c-129">Libraries</span></span>

<span data-ttu-id="5c64c-130">이러한 라이브러리는 hello 확장명이 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-130">These libraries are installed automatically with hello extension.</span></span>
-   [<span data-ttu-id="5c64c-131">Visual Studio 2013(X64)용 Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="5c64c-131">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="5c64c-132">Windows PowerShell용 Microsoft Azure Active Directory 모듈 버전 1.1.166.0</span><span class="sxs-lookup"><span data-stu-id="5c64c-132">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a><span data-ttu-id="5c64c-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c64c-133">Azure Active Directory</span></span>

<span data-ttu-id="5c64c-134">Active Directory 동기화 된 tooAzure hello NPS 확장을 사용 하 여 모든 사용자 해야 Azure AD Connect를 사용 하 고 MFA를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-134">Everyone using hello NPS extension must be synced tooAzure Active Directory using Azure AD Connect, and must be registered for MFA.</span></span>

<span data-ttu-id="5c64c-135">Hello 확장을 설치 하면 Azure AD 테 넌 트에 대 한 hello 디렉터리 ID 및 관리자 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-135">When you install hello extension, you need hello directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="5c64c-136">Hello에 디렉터리 ID를 찾을 수 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-136">You can find your directory ID in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5c64c-137">선택 hello 관리자 권한으로 로그인 **Azure Active Directory** hello 왼쪽에서 아이콘을 선택 합니다 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-137">Sign in as an administrator, select hello **Azure Active Directory** icon on hello left, then select **Properties**.</span></span> <span data-ttu-id="5c64c-138">Hello에 대 한 GUID 복사 hello **디렉터리 ID** 상자 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-138">Copy hello GUID in hello **Directory ID** box and save it.</span></span> <span data-ttu-id="5c64c-139">Hello NPS 확장을 설치할 때 hello 테 넌 트 ID로이 GUID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-139">You use this GUID as hello tenant ID when you install hello NPS extension.</span></span>

![Azure Active Directory 속성에서 디렉터리 ID 찾기](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a><span data-ttu-id="5c64c-141">환경 준비</span><span class="sxs-lookup"><span data-stu-id="5c64c-141">Prepare your environment</span></span>

<span data-ttu-id="5c64c-142">원하는 tooprepare hello NPS 확장을 설치 하기 전에 사용자 환경 toohandle hello 인증 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-142">Before you install hello NPS extension, you want tooprepare you environment toohandle hello authentication traffic.</span></span>

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="5c64c-143">도메인에 가입 된 서버에 hello NPS 역할을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5c64c-143">Enable hello NPS role on a domain-joined server</span></span>

<span data-ttu-id="5c64c-144">NPS 서버 hello tooAzure Active Directory를 연결 하 고 hello MFA 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-144">hello NPS server connects tooAzure Active Directory and authenticates hello MFA requests.</span></span> <span data-ttu-id="5c64c-145">이 역할에 대한 서버를 한 개 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="5c64c-145">Choose one server for this role.</span></span> <span data-ttu-id="5c64c-146">RADIUS를 하지 않은 모든 요청에 대 한 오류를 throw 하는 hello NPS 확장 때문에 다른 서비스의 요청을 처리 하지 않는 하는 서버를 선택 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-146">We recommend choosing a server that doesn't handle requests from other services, because hello NPS extension throws errors for any requests that aren't RADIUS.</span></span>

1. <span data-ttu-id="5c64c-147">서버에서 열고 hello **추가 역할 및 기능 마법사** hello 퀵 스타트 서버 관리자 메뉴에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-147">On your server, open hello **Add Roles and Features Wizard** from hello Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="5c64c-148">설치 유형에 대한 **역할 기반 또는 기능 기반 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-148">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="5c64c-149">선택 hello **네트워크 정책 및 액세스 서비스** 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-149">Select hello **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="5c64c-150">창이 팝업 되도록 tooinform 필수 기능 toorun 하는 경우이 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-150">A window may pop up tooinform you of required features toorun this role.</span></span>
4. <span data-ttu-id="5c64c-151">Hello 확인 페이지까지 hello 마법사를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-151">Continue through hello wizard until hello Confirmation page.</span></span> <span data-ttu-id="5c64c-152">**설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-152">Select **Install**.</span></span>

<span data-ttu-id="5c64c-153">또한이 서버 toohandle를 구성 해야 NPS에 대 한 지정 된 서버를가지고 hello VPN 솔루션에서에서 RADIUS 요청을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-153">Now that you have a server designated for NPS, you should also configure this server toohandle incoming RADIUS requests from hello VPN solution.</span></span>

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a><span data-ttu-id="5c64c-154">VPN 솔루션 toocommunicate hello NPS 서버를 사용 하 여 구성</span><span class="sxs-lookup"><span data-stu-id="5c64c-154">Configure your VPN solution toocommunicate with hello NPS server</span></span>

<span data-ttu-id="5c64c-155">VPN 솔루션에 따라 사용, RADIUS 인증 정책 변경 단계 tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="5c64c-155">Depending on which VPN solution you use, hello steps tooconfigure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="5c64c-156">이 정책 toopoint tooyour RADIUS NPS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-156">Configure this policy toopoint tooyour RADIUS NPS server.</span></span>

### <a name="sync-domain-users-toohello-cloud"></a><span data-ttu-id="5c64c-157">도메인 사용자 toohello 클라우드 동기화</span><span class="sxs-lookup"><span data-stu-id="5c64c-157">Sync domain users toohello cloud</span></span>

<span data-ttu-id="5c64c-158">이 단계에서 테 넌 트에 이미 있을 이지만 Azure AD Connect 데이터베이스 최근에 동기화가 좋은 toodouble 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-158">This step may already be complete on your tenant, but it's good toodouble-check that Azure AD Connect has synchronized your databases recently.</span></span>

1. <span data-ttu-id="5c64c-159">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-159">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="5c64c-160">**Azure Active Directory** > **Azure AD Connect** 선택</span><span class="sxs-lookup"><span data-stu-id="5c64c-160">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="5c64c-161">동기화 상태가 **사용**이고 마지막 동기화가 1시간 미만인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-161">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="5c64c-162">지침을 hello us tookick 동기화의 새로운 라운드 해제 해야 할 경우 [Azure AD Connect 동기화: 스케줄러](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-162">If you need tookick off a new round of synchronization, us hello instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="determine-which-authentication-methods-your-users-can-use"></a><span data-ttu-id="5c64c-163">사용자가 사용할 수 있는 인증 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-163">Determine which authentication methods your users can use</span></span>

<span data-ttu-id="5c64c-164">어떤 인증 방법을 NPS 확장 배포와 함께 사용할 수 있는지에 영향을 미치는 두 가지 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-164">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span></span>

1. <span data-ttu-id="5c64c-165">hello RADIUS 클라이언트 간에 사용 되는 hello 암호화 알고리즘이 (VPN, Netscaler 서버 또는 기타) 및 NPS 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-165">hello password encryption algorithm used between hello RADIUS client (VPN, Netscaler server, or other) and hello NPS servers.</span></span>
   - <span data-ttu-id="5c64c-166">**PAP** hello 클라우드에서 Azure MFA의 모든 hello 인증 방법을 지원: 전화 통화, 단방향 문자 메시지, 모바일 앱 알림 및 모바일 앱 확인 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-166">**PAP** supports all hello authentication methods of Azure MFA in hello cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span></span>
   - <span data-ttu-id="5c64c-167">**CHAPV2** 및 **EAP**는 전화 통화 및 모바일 앱 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-167">**CHAPV2** and **EAP** support phone call and mobile app notification.</span></span>
2. <span data-ttu-id="5c64c-168">hello 입력 클라이언트 응용 프로그램 hello 메서드 (VPN, Netscaler 서버 또는 기타)를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-168">hello input methods that hello client application (VPN, Netscaler server, or other) can handle.</span></span> <span data-ttu-id="5c64c-169">예를 들어 hello VPN 클라이언트에는 다른 방법 텍스트 또는 모바일 앱의 인증 코드에 tooallow hello 사용자 tootype?</span><span class="sxs-lookup"><span data-stu-id="5c64c-169">For example, does hello VPN client have some means tooallow hello user tootype in a verification code from a text or mobile app?</span></span>

<span data-ttu-id="5c64c-170">Hello NPS 확장을 배포 하는 경우에 사용자를 위해 사용할 수 있는 어떤 방법이 이러한 요인 tooevaluate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-170">When you deploy hello NPS extension, use these factors tooevaluate which methods are available for your users.</span></span> <span data-ttu-id="5c64c-171">RADIUS 클라이언트 PAP를 지 원하는 hello 클라이언트 UX에 확인 코드에 대 한 입력된 필드가 없는 경우 다음 전화 통화 및 모바일 앱 알림을 hello 방법은 두 가지가 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-171">If your RADIUS client supports PAP, but hello client UX doesn't have input fields for a verification code, then phone call and mobile app notification are hello two supported options.</span></span>

<span data-ttu-id="5c64c-172">Azure에서 [지원되지 않는 인증 방법을 사용하지 않도록 설정](multi-factor-authentication-whats-next.md#selectable-verification-methods)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-172">You can [disable unsupported authentication methods](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.</span></span>

### <a name="enable-users-for-mfa"></a><span data-ttu-id="5c64c-173">MFA에 대한 사용자 설정</span><span class="sxs-lookup"><span data-stu-id="5c64c-173">Enable users for MFA</span></span>

<span data-ttu-id="5c64c-174">Hello 전체 NPS 확장을 배포 하기 전에 MFA tooenable tooperform 2 단계 인증을 사용 하지 않겠다고 hello 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-174">Before you deploy hello full NPS extension, you need tooenable MFA for hello users that you want tooperform two-step verification.</span></span> <span data-ttu-id="5c64c-175">바로 사용 가능한 추가 때 tootest hello 확장 배포, 완벽 하 게 Multi-factor Authentication에 등록 된 하나 이상의 테스트에서 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-175">More immediately, tootest hello extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span>

<span data-ttu-id="5c64c-176">이러한 단계 tooget 테스트 계정을 시작을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-176">Use these steps tooget a test account started:</span></span>
1. <span data-ttu-id="5c64c-177">역시 로그인[https://aka.ms/mfasetup](https://aka.ms/mfasetup) 테스트 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-177">Sign in too[https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span></span> 
2. <span data-ttu-id="5c64c-178">Hello 프롬프트 tooset을 확인 방법을를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-178">Follow hello prompts tooset up a verification method.</span></span>
3. <span data-ttu-id="5c64c-179">조건부 액세스 정책을 만들거나 또는 [hello 사용자 상태를 변경](multi-factor-authentication-get-started-user-states.md) hello 테스트 계정에 대 한 toorequire 2 단계 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-179">Either create a conditional access policy or [change hello user state](multi-factor-authentication-get-started-user-states.md) toorequire two-step verification for hello test account.</span></span> 

<span data-ttu-id="5c64c-180">사용자가 또한 있어야만 toofollow 이러한 단계 tooenroll hello NPS 확장명이 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-180">Your users also need toofollow these steps tooenroll before they can authenticate with hello NPS extension.</span></span>

## <a name="install-hello-nps-extension"></a><span data-ttu-id="5c64c-181">Hello NPS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="5c64c-181">Install hello NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c64c-182">Hello NPS 확장 hello VPN 액세스 포인트와 다른 서버에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-182">Install hello NPS extension on a different server than hello VPN access point.</span></span>

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a><span data-ttu-id="5c64c-183">다운로드 하 고 Azure MFA에 대 한 hello NPS 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-183">Download and install hello NPS extension for Azure MFA</span></span>

1.  <span data-ttu-id="5c64c-184">[Hello NPS 확장 다운로드](https://aka.ms/npsmfa) hello Microsoft 다운로드 센터에서에서.</span><span class="sxs-lookup"><span data-stu-id="5c64c-184">[Download hello NPS Extension](https://aka.ms/npsmfa) from hello Microsoft Download Center.</span></span>
2.  <span data-ttu-id="5c64c-185">Hello 이진 toohello tooconfigure 원하는 네트워크 정책 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-185">Copy hello binary toohello Network Policy Server you want tooconfigure.</span></span>
3.  <span data-ttu-id="5c64c-186">실행 *setup.exe* hello 설치 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-186">Run *setup.exe* and follow hello installation instructions.</span></span> <span data-ttu-id="5c64c-187">오류가 발생 하면 해당 hello hello 필수 구성 요소 섹션에서 두 개의 라이브러리 성공적으로 설치를 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5c64c-187">If you encounter errors, double-check that hello two libraries from hello prerequisite section were successfully installed.</span></span>

### <a name="run-hello-powershell-script"></a><span data-ttu-id="5c64c-188">Hello PowerShell 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="5c64c-188">Run hello PowerShell script</span></span>

<span data-ttu-id="5c64c-189">이 위치에는 PowerShell 스크립트를 작성 하는 hello 설치 관리자: `C:\Program Files\Microsoft\AzureMfa\Config` (C:\는 설치 드라이브).</span><span class="sxs-lookup"><span data-stu-id="5c64c-189">hello installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="5c64c-190">이 PowerShell 스크립트 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-190">This PowerShell script performs hello following actions:</span></span>

-   <span data-ttu-id="5c64c-191">자체 서명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-191">Create a self-signed certificate.</span></span>
-   <span data-ttu-id="5c64c-192">Hello hello 인증서 toohello 서비스에서 Azure AD 사용자의 공개 키를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-192">Associate hello public key of hello certificate toohello service principal on Azure AD.</span></span>
-   <span data-ttu-id="5c64c-193">Hello cert hello 로컬 컴퓨터 인증서 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-193">Store hello cert in hello local machine cert store.</span></span>
-   <span data-ttu-id="5c64c-194">권한 부여 액세스 toohello 인증서의 개인 키 tooNetwork 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-194">Grant access toohello certificate’s private key tooNetwork User.</span></span>
-   <span data-ttu-id="5c64c-195">NPS hello를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-195">Restart hello NPS.</span></span>

<span data-ttu-id="5c64c-196">사용 하려는 경우가 아니면 toouse 사용자 고유의 인증서 (hello 자체 서명 된 인증서 대신 hello PowerShell 스크립트를 생성 하는) hello PowerShell 스크립트 toocomplete hello 설치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-196">Unless you want toouse your own certificates (instead of hello self-signed certificates that hello PowerShell script generates), run hello PowerShell Script toocomplete hello installation.</span></span> <span data-ttu-id="5c64c-197">여러 서버에 hello 확장을 설치 하는 경우 각 자체 인증서를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-197">If you install hello extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="5c64c-198">관리자 권한으로 Windows PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-198">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="5c64c-199">디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-199">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="5c64c-200">Hello 설치 프로그램에서 만든 hello PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-200">Run hello PowerShell script created by hello installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="5c64c-201">PowerShell이 테넌트 ID에 대해 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-201">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="5c64c-202">Hello hello hello 전제 조건 섹션에서 Azure 포털에서에서 복사한 디렉터리 ID GUID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-202">Use hello Directory ID GUID that you copied from hello Azure portal in hello prerequisites section.</span></span>
5. <span data-ttu-id="5c64c-203">관리자 권한으로 tooAzure AD에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-203">Sign in tooAzure AD as an administrator.</span></span>
6. <span data-ttu-id="5c64c-204">PowerShell은 hello 스크립트가 완료 되 면 성공 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-204">PowerShell shows a success message when hello script is finished.</span></span>  

<span data-ttu-id="5c64c-205">부하 분산에 대해 tooset 되도록 추가 NPS 서버에서 다음이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-205">Repeat these steps on any additional NPS servers that you want tooset up for load balancing.</span></span>

>[!NOTE]
><span data-ttu-id="5c64c-206">Hello PowerShell 스크립트를 사용 하 여 인증서를 생성 하는 대신 자체 인증서를 사용 하는 경우 toohello NPS 명명 규칙을 정렬 됩니다 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-206">If you use your own certificates instead of generating certificates with hello PowerShell script, make sure that they align toohello NPS naming convention.</span></span> <span data-ttu-id="5c64c-207">주체 이름 hello **CN =\<TenantID\>, OU = Microsoft NPS 확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-207">hello subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span></span> 

## <a name="configure-your-nps-extension"></a><span data-ttu-id="5c64c-208">NPS 확장 구성</span><span class="sxs-lookup"><span data-stu-id="5c64c-208">Configure your NPS extension</span></span>

<span data-ttu-id="5c64c-209">이 섹션에는 성공적인 NPS 확장 배포를 위한 디자인 고려 사항 및 제안 사항이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-209">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configuration-limitations"></a><span data-ttu-id="5c64c-210">구성 제한 사항</span><span class="sxs-lookup"><span data-stu-id="5c64c-210">Configuration limitations</span></span>

- <span data-ttu-id="5c64c-211">Azure MFA에 대 한 NPS 확장 hello 도구 toomigrate 사용자와 MFA 서버 toohello 클라우드에서 설정을 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-211">hello NPS extension for Azure MFA does not include tools toomigrate users and settings from MFA Server toohello cloud.</span></span> <span data-ttu-id="5c64c-212">이러한 이유로 기존 배포 하지 않고 새 배포에 대 한 hello 확장을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-212">For this reason, we suggest using hello extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="5c64c-213">Tooperform 증명 접속 사용자에 게 기존 배포에서 hello 확장을 사용 하는 경우 다시 toopopulate가 MFA에 자세히 설명 hello 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-213">If you use hello extension on an existing deployment, your users have tooperform proof-up again toopopulate their MFA details in hello cloud.</span></span>  
- <span data-ttu-id="5c64c-214">NPS 확장 hello hello UPN hello에서 온-프레미스 Active directory tooidentify hello Azure MFA에 hello 보조 인증 hello 확장을 수행 하기 위한 일 수 있습니다 구성된 toouse 대체 로그인 ID 또는 사용자 지정 Active Directory와 같은 다른 식별자를 사용 하 여 UPN 이외의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-214">hello NPS extension uses hello UPN from hello on-premises Active directory tooidentify hello user on Azure MFA for performing hello Secondary Auth. hello extension can be configured toouse a different identifier like alternate login ID or custom Active Directory field other than UPN.</span></span> <span data-ttu-id="5c64c-215">참조 [고급 Multi-factor Authentication에 대 한 hello NPS 확장에 대 한 구성 옵션](multi-factor-authentication-advanced-vpn-configurations.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-215">See [Advanced configuration options for hello NPS extension for Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) for more information.</span></span>
- <span data-ttu-id="5c64c-216">모든 암호화 프로토콜이 모든 확인 메서드를 지원하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-216">Not all encryption protocols support all verification methods.</span></span>
   - <span data-ttu-id="5c64c-217">**PAP**는 전화 통화, 단방향 문자 메시지, 모바일 앱 알림 및 모바일 앱 확인 코드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-217">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span></span>
   - <span data-ttu-id="5c64c-218">**CHAPV2** 및 **EAP**는 전화 통화 및 모바일 앱 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-218">**CHAPV2** and **EAP** support phone call and mobile app notification</span></span>

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="5c64c-219">MFA가 필요한 RADIUS 클라이언트 제어</span><span class="sxs-lookup"><span data-stu-id="5c64c-219">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="5c64c-220">NPS 확장 hello를 사용 하 여 RADIUS 클라이언트에 대해 MFA를 사용 하면이 클라이언트에 대 한 모든 인증 필요 tooperform MFA 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-220">Once you enable MFA for a RADIUS client using hello NPS Extension, all authentications for this client are required tooperform MFA.</span></span> <span data-ttu-id="5c64c-221">일부 RADIUS 클라이언트에 MFA tooenable 하려는 경우 두 명의 NPS 서버를 구성 하 고 그 중 하나에 hello 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-221">If you want tooenable MFA for some RADIUS clients but not others, you can configure two NPS servers and install hello extension on only one of them.</span></span> <span data-ttu-id="5c64c-222">Hello 확장으로 구성 toorequire MFA toosend 요청 toohello NPS 서버와 다른 RADIUS 클라이언트 toohello NPS 서버가 구성 되지 않음 hello 확장명이 원하는 RADIUS 클라이언트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-222">Configure RADIUS clients that you want toorequire MFA toosend requests toohello NPS server configured with hello extension, and other RADIUS clients toohello NPS server not configured with hello extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="5c64c-223">MFA에 등록되지 않은 사용자를 위한 준비</span><span class="sxs-lookup"><span data-stu-id="5c64c-223">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="5c64c-224">MFA에 대해 등록 되지 않은 사용자를 설정한 경우 tooauthenticate 하려고 할 때 수행 되는 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-224">If you have users that aren't enrolled for MFA, you can determine what happens when they try tooauthenticate.</span></span> <span data-ttu-id="5c64c-225">Hello 레지스트리 설정을 사용 하 여 *REQUIRE_USER_MATCH* hello 레지스트리 경로에 *HKLM\Software\Microsoft\AzureMFA* toocontrol hello 기능 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-225">Use hello registry setting *REQUIRE_USER_MATCH* in hello registry path *HKLM\Software\Microsoft\AzureMFA* toocontrol hello feature behavior.</span></span> <span data-ttu-id="5c64c-226">이 설정에는 다음과 같은 단일 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-226">This setting has a single configuration option:</span></span>

| <span data-ttu-id="5c64c-227">키</span><span class="sxs-lookup"><span data-stu-id="5c64c-227">Key</span></span> | <span data-ttu-id="5c64c-228">값</span><span class="sxs-lookup"><span data-stu-id="5c64c-228">Value</span></span> | <span data-ttu-id="5c64c-229">기본값</span><span class="sxs-lookup"><span data-stu-id="5c64c-229">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="5c64c-230">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="5c64c-230">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="5c64c-231">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="5c64c-231">TRUE/FALSE</span></span> | <span data-ttu-id="5c64c-232">(해당 하는 tooTRUE)을 설정 하지</span><span class="sxs-lookup"><span data-stu-id="5c64c-232">Not set (equivalent tooTRUE)</span></span> |

<span data-ttu-id="5c64c-233">이 설정은 hello MFA에 대해 사용자 등록 되지 않은 경우 어떤 toodo toodetermine 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-233">hello purpose of this setting is toodetermine what toodo when a user is not enrolled for MFA.</span></span> <span data-ttu-id="5c64c-234">때 hello 키 존재 하지 않거나을 설정 하지 않으면 tooTRUE, 설정 및 hello 사용자를 등록 하지 않은 hello 확장 실패 합니다 hello MFA 챌린지입니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-234">When hello key does not exist, is not set, or is set tooTRUE, and hello user is not enrolled, then hello extension fails hello MFA challenge.</span></span> <span data-ttu-id="5c64c-235">Hello 키가 설정 되어 tooFALSE hello 사용자가 등록 되지 않은 경우 MFA를 수행 하지 않고 인증이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-235">When hello key is set tooFALSE and hello user is not enrolled, authentication proceeds without performing MFA.</span></span>

<span data-ttu-id="5c64c-236">Toocreate이이 키를 선택 하 고 모두를 등록할 수 있음 Azure MFA에 대해 아직 하 고 사용자는 온 보 딩을 tooFALSE을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-236">You can choose toocreate this key and set it tooFALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span></span> <span data-ttu-id="5c64c-237">그러나 설정 hello 키 허용 하는 사용자에 MFA toosign에 대 한 등록 되지 않은 경우 이후 tooproduction 진행 하기 전에이 키를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-237">However, since setting hello key permits users that aren't enrolled for MFA toosign in, you should remove this key before going tooproduction.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5c64c-238">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5c64c-238">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a><span data-ttu-id="5c64c-239">예상 대로 해당 hello 클라이언트 인증서가 설치 되어 확인 하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="5c64c-239">How do I verify that hello client cert is installed as expected?</span></span>

<span data-ttu-id="5c64c-240">Hello 인증서 저장소에 개인 키를 hello 검사 hello 설치 관리자에서 만든 자체 서명 된 인증서를 hello 부여 된 사용 권한이 toouser 찾아봅니다 **네트워크 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-240">Look for hello self-signed certificate created by hello installer in hello cert store, and check that hello private key has permissions granted toouser **NETWORK SERVICE**.</span></span> <span data-ttu-id="5c64c-241">hello 인증서의 주체 이름이 **CN \<tenantid\>, OU = Microsoft NPS 확장**</span><span class="sxs-lookup"><span data-stu-id="5c64c-241">hello cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a><span data-ttu-id="5c64c-242">Azure Active Directory에서 테 넌 트 관련된 toomy 내 클라이언트 인증서 인지 확인 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="5c64c-242">How can I verify that my client cert is associated toomy tenant in Azure Active Directory?</span></span>

<span data-ttu-id="5c64c-243">PowerShell 명령 프롬프트를 열고 다음 명령이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="5c64c-243">Open PowerShell command prompt and run hello following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="5c64c-244">이 명령은 PowerShell 세션에서 테 넌 트 hello NPS 확장의 인스턴스와 연결 하는 모든 hello 인증서를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-244">These commands print all hello certificates associating your tenant with your instance of hello NPS extension in your PowerShell session.</span></span> <span data-ttu-id="5c64c-245">인증서에 대 한 클라이언트 인증서 hello 개인 키가 없는 "e-64로 인코딩된 X.509(.cer)" 파일로 내보내와 PowerShell에서 hello 목록과 비교 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5c64c-245">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without hello private key, and compare it with hello list from PowerShell.</span></span>

<span data-ttu-id="5c64c-246">유효한-및 유효한-사람이 읽을 수 있는 형식에 있는 타임 스탬프 hello 명령 둘 이상의 인증서를 반환 하는 경우 사용 되는 toofilter 명백한 misfits 아웃 될 수 있습니다 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-246">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used toofilter out obvious misfits if hello command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="5c64c-247">내 요청이 ADAL 토큰 오류로 인해 실패하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5c64c-247">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="5c64c-248">이 오류 때문일 수 있습니다 일부의 이유로 tooone 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-248">This error could be due tooone of several reasons.</span></span> <span data-ttu-id="5c64c-249">Toohelp 문제를 해결 하는 다음이 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-249">Use these steps toohelp troubleshoot:</span></span>

1. <span data-ttu-id="5c64c-250">NPS 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-250">Restart your NPS server.</span></span>
2. <span data-ttu-id="5c64c-251">클라이언트 인증서가 예상대로 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-251">Verify that that client cert is installed as expected.</span></span>
3. <span data-ttu-id="5c64c-252">해당 hello 인증서가 Azure ad 테 넌 트와 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-252">Verify that hello certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="5c64c-253">Hello 확장을 실행 하는 hello 서버에서 액세스할 수 있는 해당 https://login.microsoftonline.com/를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-253">Verify that https://login.microsoftonline.com/ is accessible from hello server running hello extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a><span data-ttu-id="5c64c-254">알리는 hello 사용자를 찾을 수 없습니다는 HTTP 로그에 오류와 함께 인증이 실패 하는 이유</span><span class="sxs-lookup"><span data-stu-id="5c64c-254">Why does authentication fail with an error in HTTP logs stating that hello user is not found?</span></span>

<span data-ttu-id="5c64c-255">AD Connect를 실행 하 고 해당 hello 사용자는 Windows Active Directory 및 Azure Active Directory에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-255">Verify that AD Connect is running, and that hello user is present in both Windows Active Directory and Azure Active Directory.</span></span>

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="5c64c-256">내 모든 인증이 실패한 상태의 로그에 HTTP 연결 오류가 표시되는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5c64c-256">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="5c64c-257">Hello NPS 확장을 실행 하는 hello 서버에서 연결할 수 있는 해당 https://adnotifications.windowsazure.com를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-257">Verify that https://adnotifications.windowsazure.com is reachable from hello server running hello NPS extension.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c64c-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c64c-258">Next steps</span></span>

- <span data-ttu-id="5c64c-259">로그인에 대 한 대체 Id를 구성 하거나에 2 단계 인증을 수행 하지 않아야 하는 Ip에 대 한 예외 목록을 설정 [고급 Multi-factor Authentication에 대 한 hello NPS 확장에 대 한 구성 옵션](nps-extension-advanced-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="5c64c-259">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for hello NPS extension for Multi-Factor Authentication](nps-extension-advanced-configuration.md)</span></span>

- [<span data-ttu-id="5c64c-260">Azure Multi-factor Authentication에 대 한 hello NPS 확장에서에서 오류 메시지를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c64c-260">Resolve error messages from hello NPS extension for Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-nps-errors.md)
