---
title: "NPS 확장을 사용 하는 Azure MFA를 aaaVPN 통합 | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure에 대 한 hello 서버 NPS (네트워크 정책) 확장을 사용 하는 Azure MFA를 VPN 인프라 통합 설명 합니다."
services: active-directory
keywords: "Azure MFA, VPN 통합, Azure Active Directory, 네트워크 정책 서버 확장"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a><span data-ttu-id="d3bfe-104">VPN 인프라와 Azure Multi-factor Authentication (MFA) hello 정책 서버 NPS (네트워크) 확장을 사용 하 여 Azure에 대 한 통합</span><span class="sxs-lookup"><span data-stu-id="d3bfe-104">Integrate your VPN infrastructure with Azure Multi-Factor Authentication (MFA) using hello Network Policy Server (NPS) extension for Azure</span></span>

## <a name="overview"></a><span data-ttu-id="d3bfe-105">개요</span><span class="sxs-lookup"><span data-stu-id="d3bfe-105">Overview</span></span>

<span data-ttu-id="d3bfe-106">Azure에 대 한 서비스 NPS (네트워크 정책) 확장 hello 허용 조직 toosafeguard 인증 전화 접속 사용자 RADIUS (Remote Service) 클라이언트 인증을 사용 하 여 클라우드 기반 [Azure Multi-factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), 2 단계 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-106">hello Network Policy Service (NPS) extension for Azure allows organizations toosafeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using cloud-based [Azure Multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), which provides two-step verification.</span></span>

<span data-ttu-id="d3bfe-107">이 문서 hello NPS 확장을 사용 하 여 VPN을 사용 하 여 tooconnect tooyour 네트워크를 시도 하는 사용자에 대 한 Azure tooenable 보안 2 단계 인증에 Azure MFA를 hello NPS 인프라 통합에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-107">This article provides instructions for integrating hello NPS infrastructure with Azure MFA using hello NPS extension for Azure tooenable secure two-step verification for users attempting tooconnect tooyour network using a VPN.</span></span> 

<span data-ttu-id="d3bfe-108">hello 네트워크 정책 및 액세스 서비스 (NPS) 조직 hello 다음 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-108">hello Network Policy and Access Services (NPS) gives organizations hello following abilities:</span></span>

* <span data-ttu-id="d3bfe-109">Hello 관리 및 서버에 연결할 수 있는 시간을 연결이 허용 되는지, 연결, hello 기간과 hello 수준의 보안 클라이언트 tooconnect를 사용 하 고 등 해야 합니다는 네트워크 요청 toospecify의 제어를 위한 중앙 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-109">Specify central locations for hello management and control of network requests toospecify who can connect, what times of day connections are allowed, hello duration of connections, and hello level of security that clients must use tooconnect, and so on.</span></span> <span data-ttu-id="d3bfe-110">이러한 정책은 각 VPN 또는 RD(원격 데스크톱) 게이트웨이 서버에 지정하는 대신 중앙 위치에 한 번만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-110">Rather than specify these policies on each VPN or Remote Desktop (RD) Gateway server, these policies can be specified once in a central location.</span></span> <span data-ttu-id="d3bfe-111">hello RADIUS 프로토콜을 사용 하는 인증, 권한 부여 및 계정 (AAA) tooprovide hello 중앙 집중화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-111">hello RADIUS protocol is used tooprovide hello centralized Authentication, Authorization, and Accounting (AAA).</span></span> 
* <span data-ttu-id="d3bfe-112">설정 및 장치 toonetwork 리소스 제한 또는 무제한 액세스를 부여 된 있는지 여부를 결정 하는 네트워크 액세스 보호 (NAP) 클라이언트 상태 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-112">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access toonetwork resources.</span></span>
* <span data-ttu-id="d3bfe-113">액세스 too802.1x 지원 무선 액세스 지점 및 이더넷 스위치에 대 한 의미 tooenforce 인증 및 권한 부여를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-113">Provide a means tooenforce authentication and authorization for access too802.1x-capable wireless access points and Ethernet switches.</span></span>    

<span data-ttu-id="d3bfe-114">자세한 내용은 [NPS(네트워크 정책 서버)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-114">For more information, see [Network Policy Server (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top).</span></span> 

<span data-ttu-id="d3bfe-115">tooenhance 보안 수준이 높은 제공 하 고 규정 준수의 조직에서는 NPS를 통합할 수 있습니다 toobe 수 있는 사용자가 2 단계 인증을 사용 하는 Azure MFA tooensure hello VPN 서버에서 toohello 가상 포트에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-115">tooenhance security and provide high level of compliance, organizations can integrate NPS with Azure MFA tooensure that users use two-step verification toobe able connect toohello virtual port on hello VPN server.</span></span> <span data-ttu-id="d3bfe-116">에 대 한 액세스 권한이 부여 되는 사용자가 toobe, 해당 컨트롤에 자신의 사용자 이름/암호 조합이 hello 사용자 정보로는 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-116">For users toobe granted access, they must provide their username/password combination with information that hello user has in their control.</span></span> <span data-ttu-id="d3bfe-117">이 정보는 신뢰할 수 있어야 하며, 휴대폰 번호, 유선 전화 번호, 모바일 장치 등과 같이 쉽게 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-117">This information must be trusted and not easily duplicated, such as a cell phone number, landline number, application on a mobile device, and so on.</span></span>

<span data-ttu-id="d3bfe-118">Hello Azure에 대 한 NPS 확장의 이전 toohello 가용성, 고객에 대 한 2 단계 인증 tooimplement 입장 통합 NPS 및 Azure MFA 환경 tooconfigure 되었고 hello 온-프레미스 환경에서 별도 MFA 서버를 유지 관리 원격 데스크톱 게이트웨이 및 Azure Multi-factor Authentication 서버 RADIUS를 사용 하 여 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-118">Prior toohello availability of hello NPS extension for Azure, customers who wished tooimplement two-step verification for integrated NPS and Azure MFA environments had tooconfigure and maintain a separate MFA Server in hello on-premises environment as documented in Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS.</span></span>

<span data-ttu-id="d3bfe-119">이제 Azure 용 hello NPS 확장의 가용성을 hello는 온-프레미스 기반 MFA 솔루션 또는 클라우드 기반 MFA 솔루션 toosecure RADIUS 클라이언트 인증 조직 hello 선택 toodeploy를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-119">hello availability of hello NPS extension for Azure now gives organizations hello choice toodeploy either an on-premises based MFA solution or a cloud-based MFA solution toosecure RADIUS client authentication.</span></span>
 
## <a name="authentication-flow"></a><span data-ttu-id="d3bfe-120">인증 흐름</span><span class="sxs-lookup"><span data-stu-id="d3bfe-120">Authentication Flow</span></span>
<span data-ttu-id="d3bfe-121">사용자가 tooa 가상 포트를 VPN 서버에 연결 하는 경우 다양 한 사용자 이름/암호 및 인증서 기반 인증 방법의 조합 hello 사용을 허용 하는 프로토콜을 사용 하 여 인증 먼저 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-121">When a user connects tooa virtual port on a VPN server, they must first authenticate using a variety of protocols, which allow hello use of a combination of user name/password and certificate-based authentication methods.</span></span> 

<span data-ttu-id="d3bfe-122">또한 tooauthenticating 및 신원을 확인에서는 사용자 hello 전화 로그인 사용 권한을 적절 한 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-122">In addition tooauthenticating and verifying identity, users must have hello appropriate dial-in permissions.</span></span> <span data-ttu-id="d3bfe-123">간단한 구현에 대 한 액세스를 허용 하는 이러한 전화 접속 권한은 hello Active Directory 사용자 개체에 직접 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-123">In simple implementations, these dial-in permissions that allow access are set directly on hello Active Directory user objects.</span></span> 

 ![사용자 속성](./media/nps-extension-vpn/image1.png)

<span data-ttu-id="d3bfe-125">간단한 구현을 위해 각 VPN 서버에서 각 로컬 VPN 서버에 정의된 정책에 따라 액세스를 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-125">For simple implementations, each VPN server grants or denies access based on policies defined on each local VPN server.</span></span>

<span data-ttu-id="d3bfe-126">더 큰 및 확장성 구현에서는 hello 해당 권한 부여 정책을 또는 RADIUS 서버에 중앙 집중식으로 VPN 액세스를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-126">In larger and more scalable implementations, hello polices that grant or deny VPN access are centralized on RADIUS servers.</span></span> <span data-ttu-id="d3bfe-127">이 경우 hello VPN 서버 및 역할을 서버 (RADIUS 클라이언트) 연결 요청을 전달 하는 계정 메시지 tooa RADIUS 서버.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-127">In this case, hello VPN server acts as an access server (RADIUS client) that forwards connection requests and account messages tooa RADIUS server.</span></span> <span data-ttu-id="d3bfe-128">VPN 서버 hello에 tooconnect toohello의 가상 포트에 사용자가 인증 되어야 하며 RADIUS 서버에 중앙 집중식으로 정의 된 hello 조건을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-128">tooconnect toohello virtual port on hello VPN server, users must be authenticated and meet hello conditions defined centrally on RADIUS servers.</span></span> 

<span data-ttu-id="d3bfe-129">Azure에 대 한 NPS 확장 hello와 통합 된 hello NPS hello 정상적으로 인증 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-129">When hello NPS extension for Azure is integrated with hello NPS, hello successful authentication flow is as follows:</span></span>

1. <span data-ttu-id="d3bfe-130">hello VPN 서버 hello 사용자 이름 및 암호 tooconnect tooa 같은 리소스에 원격 데스크톱 세션을 포함 하는 VPN 사용자의 인증 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-130">hello VPN server receives an authentication request from a VPN user that includes hello username and password tooconnect tooa resource, such as a Remote Desktop session.</span></span> 
2. <span data-ttu-id="d3bfe-131">VPN 서버 hello 요청 tooa RADIUS 액세스 요청 메시지를 변환 하 고 보냅니다 hello 메시지 RADIUS 클라이언트로 작동 하는, (암호 암호화) hello NPS 확장이 설치 되어 있는 toohello RADIUS (NPS) 서버.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-131">Acting as a RADIUS client, VPN server converts hello request tooa RADIUS Access-Request message and sends hello message (password is encrypted) toohello RADIUS (NPS) server where hello NPS extension is installed.</span></span> 
3. <span data-ttu-id="d3bfe-132">hello 사용자 이름 및 암호 조합이 Active Directory에서 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-132">hello username and password combination is verified in Active Directory.</span></span> <span data-ttu-id="d3bfe-133">경우 hello 사용자 이름 / 암호가 올바르지 않습니다, RADIUS 서버 hello 액세스 거부 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-133">If hello username / password is incorrect, hello RADIUS Server sends an Access-Reject message.</span></span> 
4. <span data-ttu-id="d3bfe-134">NPS 연결 요청을 hello 및 네트워크 정책에 해당할으로 모든 조건에 지정 된 경우 (예를 들어 시간이 나 그룹 구성원 자격 제한과), NPS 확장 hello Azure MFA를 보조 인증에 대 한 요청을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-134">If all conditions as specified in hello NPS Connection Request and Network Policies are met (for example, time of day or group membership restrictions), hello NPS extension triggers a request for secondary authentication with Azure MFA.</span></span> 
5. <span data-ttu-id="d3bfe-135">Azure MFA Azure Active Directory와 통신 하 고, hello 사용자의 세부 정보를 검색, hello 사용자 (문자 메시지, 모바일 앱, 및 등)으로 구성 하는 hello 메서드를 사용 하 여 hello 보조 인증을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-135">Azure MFA communicates with Azure Active Directory, retrieves hello user’s details, and performs hello secondary authentication using hello method configured by hello user (text message, mobile app, and so on).</span></span> 
6. <span data-ttu-id="d3bfe-136">검색에 성공 hello MFA 챌린지의 Azure MFA hello 결과 toohello NPS 확장을 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-136">Upon success of hello MFA challenge, Azure MFA communicates hello result toohello NPS extension.</span></span>
7. <span data-ttu-id="d3bfe-137">Hello 연결 시도가 모두 및 권한 부여, 후 hello 확장이 설치 되어 hello NPS 서버에서 RADIUS 액세스 허용 메시지 toohello VPN 서버 (RADIUS 클라이언트)를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-137">After hello connection attempt is both authenticated and authorized, hello NPS server where hello extension is installed sends a RADIUS Access-Accept message toohello VPN server (RADIUS client).</span></span>
8. <span data-ttu-id="d3bfe-138">hello 사용자 액세스 toohello 가상 포트 VPN 서버에 부여 하 고 암호화 된 VPN 터널을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-138">hello user is granted access toohello virtual port on VPN server and establishes an encrypted VPN tunnel.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3bfe-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d3bfe-139">Prerequisites</span></span>
<span data-ttu-id="d3bfe-140">이 섹션에는 필수 구성 요소 hello Azure MFA 원격 데스크톱 게이트웨이 hello와 통합 하기 전에 필요한 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-140">This section details hello prerequisites necessary before integrating Azure MFA with hello Remote Desktop Gateway.</span></span> <span data-ttu-id="d3bfe-141">시작 하기 전에 다음 필수 구성 요소가 충족 하는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-141">Before you begin, you must have hello following prerequisites in place.</span></span>

* <span data-ttu-id="d3bfe-142">VPN 인프라</span><span class="sxs-lookup"><span data-stu-id="d3bfe-142">VPN infrastructure</span></span>
* <span data-ttu-id="d3bfe-143">NPS(네트워크 정책 및 액세스 서비스) 역할</span><span class="sxs-lookup"><span data-stu-id="d3bfe-143">Network Policy and Access Services (NPS) role</span></span>
* <span data-ttu-id="d3bfe-144">Azure MFA 라이선스</span><span class="sxs-lookup"><span data-stu-id="d3bfe-144">Azure MFA License</span></span>
* <span data-ttu-id="d3bfe-145">Windows Server 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="d3bfe-145">Windows Server software</span></span>
* <span data-ttu-id="d3bfe-146">라이브러리</span><span class="sxs-lookup"><span data-stu-id="d3bfe-146">Libraries</span></span>
* <span data-ttu-id="d3bfe-147">온-프레미스 AD와 동기화되는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3bfe-147">Azure AD synched with on-premises AD</span></span> 
* <span data-ttu-id="d3bfe-148">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="d3bfe-148">Azure Active Directory GUID ID</span></span>

### <a name="vpn-infrastructure"></a><span data-ttu-id="d3bfe-149">VPN 인프라</span><span class="sxs-lookup"><span data-stu-id="d3bfe-149">VPN infrastructure</span></span>
<span data-ttu-id="d3bfe-150">이 문서 위치에서 Microsoft Windows Server 2016을 사용 하 여 작업 VPN 인프라가 해당 hello VPN 서버는 현재 구성 된 tooforward 연결 요청 tooa RADIUS 서버 되었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-150">This article assumes that you have a working VPN infrastructure using Microsoft Windows Server 2016 in place and that hello VPN server is currently not configured tooforward connection requests tooa RADIUS server.</span></span> <span data-ttu-id="d3bfe-151">이 가이드의 hello VPN 인프라 toouse 중앙 RADIUS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-151">You will configure hello VPN infrastructure toouse a central RADIUS server in this guide.</span></span>

<span data-ttu-id="d3bfe-152">현재 위치에 작업 인프라가 없는 경우 hello Microsoft 및 타사 사이트에서 찾을 수 있습니다는 다양 한 VPN 설정 자습서에서 제공 하는 다음 hello 지침으로이 인프라를 신속 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-152">If you do not have a working infrastructure in place, you can quickly create this infrastructure by following hello guidance provided in numerous VPN setup tutorials you can find on hello Microsoft and third-party sites.</span></span> 

### <a name="network-policy-and-access-services-nps-role"></a><span data-ttu-id="d3bfe-153">NPS(네트워크 정책 및 액세스 서비스) 역할</span><span class="sxs-lookup"><span data-stu-id="d3bfe-153">Network Policy and Access Services (NPS) role</span></span>

<span data-ttu-id="d3bfe-154">hello NPS 역할 서비스는 hello RADIUS 서버 및 클라이언트 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-154">hello NPS role service provides hello RADIUS server and client functionality.</span></span> <span data-ttu-id="d3bfe-155">이 문서에서는 사용자 환경에 구성원 서버 또는 도메인 컨트롤러에서 hello NPS 역할을 설치 했거나 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-155">This article assumes you have installed hello NPS role on a member server or domain controller in your environment.</span></span> <span data-ttu-id="d3bfe-156">이 가이드에서는 VPN 구성을 위해 RADIUS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-156">You will configure RADIUS for a VPN configuration in this guide.</span></span> <span data-ttu-id="d3bfe-157">서버에 hello NPS 역할을 설치 _다른_ VPN 서버 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-157">Install hello NPS role on a server _other_ than your VPN server.</span></span>

<span data-ttu-id="d3bfe-158">Hello NPS 역할 설치에 대 한 내용은 Windows Server 2012 서비스 또는 이상에 참조 [NAP 상태 정책 서버 설치](https://technet.microsoft.com/library/dd296890.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-158">For information on installing hello NPS role service Windows Server 2012 or higher, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="d3bfe-159">Windows Server 2016에서는 NAP(네트워크 액세스 정책)가 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-159">Network Access Policy (NAP) is deprecated in Windows Server 2016.</span></span> <span data-ttu-id="d3bfe-160">NPS 포함 하 여 hello 권장 tooinstall NPS 도메인 컨트롤러에 대 한 모범 사례에 대 한 설명을 참조 하십시오. [NPS에 대 한 유용한](https://technet.microsoft.com/library/cc771746)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-160">For a description of best practices for NPS, including hello recommendation tooinstall NPS on a domain controller, see [Best Practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="licenses"></a><span data-ttu-id="d3bfe-161">라이선스</span><span class="sxs-lookup"><span data-stu-id="d3bfe-161">Licenses</span></span>

<span data-ttu-id="d3bfe-162">Azure AD Premium, EMS(Enterprise Mobility plus Security) 또는 MFA 구독을 통해 사용할 수 있는 Azure MFA에 대한 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-162">Required is a license for Azure MFA, which is available through an Azure AD Premium, Enterprise Mobility plus Security (EMS), or an MFA subscription.</span></span> <span data-ttu-id="d3bfe-163">자세한 내용은 참조 [어떻게 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-163">For more information, see [How tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span></span> <span data-ttu-id="d3bfe-164">테스트를 위해 평가판 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-164">For testing purposes, you can use a trial subscription.</span></span>

### <a name="software"></a><span data-ttu-id="d3bfe-165">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="d3bfe-165">Software</span></span>

<span data-ttu-id="d3bfe-166">hello NPS 확장 해야 Windows Server 2008 R2 SP1 이상 hello NPS 역할 서비스가 설치 되어 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-166">hello NPS extension requires Windows Server 2008 R2 SP1 or above with hello NPS role service installed.</span></span> <span data-ttu-id="d3bfe-167">Windows Server 2016을 사용 하 여 모든 hello이이 가이드의에서 단계를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-167">All hello steps in this guide were performed using Windows Server 2016.</span></span>

### <a name="libraries"></a><span data-ttu-id="d3bfe-168">라이브러리</span><span class="sxs-lookup"><span data-stu-id="d3bfe-168">Libraries</span></span>

<span data-ttu-id="d3bfe-169">다음 두 개의 라이브러리 hello 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-169">hello following two libraries are required:</span></span>

* [<span data-ttu-id="d3bfe-170">Visual Studio 2013(X64)용 Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="d3bfe-170">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
* <span data-ttu-id="d3bfe-171">_Windows PowerShell용 Microsoft Azure Active Directory 모듈 버전 1.1.166.0_ 이상</span><span class="sxs-lookup"><span data-stu-id="d3bfe-171">_Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0_ or higher.</span></span> <span data-ttu-id="d3bfe-172">최신 릴리스 hello 및 설치 지침을 참조 하세요. [Microsoft Azure Active Directory PowerShell 모듈 버전 릴리스 기록](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-172">For hello latest release and installation instructions, see [Microsoft Azure Active Directory PowerShell Module Version Release History](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).</span></span>

<span data-ttu-id="d3bfe-173">이러한 라이브러리 언급 하는 기존 문서를 불구 하 고 hello NPS 확장 설치 파일 (버전 0.9.1.2)와 패키징되 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-173">These libraries are not packaged with hello NPS extension setup files (version 0.9.1.2), despite existing documentation that states otherwise.</span></span> <span data-ttu-id="d3bfe-174">여기에 최소한 Visual Studio 2013 용 hello Visual c + + 재배포 가능 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-174">At a minimum, you must install hello Visual C++ Redistributable Packages for Visual Studio 2013.</span></span> <span data-ttu-id="d3bfe-175">이미 hello 설치 과정의 일부로 실행 하는 구성 스크립트를 통해 존재 하지 않는 경우 hello Microsoft Azure Active Directory 모듈에 대 한 Windows PowerShell이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-175">hello Microsoft Azure Active Directory Module for Windows PowerShell is installed, if it is not already present, through a configuration script you run as part of hello setup process.</span></span> <span data-ttu-id="d3bfe-176">경우에 없는 필요 tooinstall 미리이 모듈 이미 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-176">There is no need tooinstall this module ahead of time if it is not already installed.</span></span>

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a><span data-ttu-id="d3bfe-177">온-프레미스 Active Directory와 동기화되는 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3bfe-177">Azure Active Directory synched with on-premises Active Directory</span></span> 

<span data-ttu-id="d3bfe-178">toouse hello NPS 확장 온-프레미스 사용자를 Azure Active Directory와 동기화 하 고 Multi-factor Authentication에 대해 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-178">toouse hello NPS extension, on-premises users must be synced with Azure Active Directory and enabled for Multi-Factor Authentication.</span></span> <span data-ttu-id="d3bfe-179">이 가이드에서는 온-프레미스 사용자가 AD Connect를 사용하여 Azure Active Directory와 동기화된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-179">This guide assumes that on-premises users are synched with Azure Active Directory using AD Connect.</span></span> <span data-ttu-id="d3bfe-180">사용자가 MFA를 사용하도록 설정하기 위한 지침은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-180">Instructions for enabling users for MFA are provided below.</span></span>
<span data-ttu-id="d3bfe-181">Azure AD 연결에 대한 자세한 내용은 [Azure Active Directory와 온-프레미스 디렉터리 통합](../active-directory/connect/active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-181">For information on Azure AD connect, see [Integrate your on-premises directories with Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="d3bfe-182">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="d3bfe-182">Azure Active Directory GUID ID</span></span> 
<span data-ttu-id="d3bfe-183">tooinstall NPS hello tooknow hello hello Azure Active Directory의 GUID를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-183">tooinstall hello NPS, you need tooknow hello GUID of hello Azure Active Directory.</span></span> <span data-ttu-id="d3bfe-184">Hello hello Azure Active Directory의 GUID 찾기에 대 한 지침 hello 다음 섹션에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-184">Instructions for finding hello GUID of hello Azure Active Directory are provided in hello next section.</span></span>

## <a name="configure-radius-for-vpn-connections"></a><span data-ttu-id="d3bfe-185">VPN 연결을 위한 RADIUS 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-185">Configure RADIUS for VPN connections</span></span>

<span data-ttu-id="d3bfe-186">Hello NPS 서버 역할 구성원 서버에 설치한 경우 tooconfigure tooauthenticate 필요 하 고 VPN 연결을 요청 하는 VPN 클라이언트에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-186">If you have installed hello NPS server role on a member server, you need tooconfigure tooauthenticate and authorize VPN client that request VPN connections.</span></span> 

<span data-ttu-id="d3bfe-187">이 섹션에서는 hello 네트워크 정책 서버 역할을 설치 했거나 하지만 구성 하지 사용 하기 위해 인프라에서 있습니다를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-187">This section assumes that you have installed hello Network Policy Server role but have not configured it for use in your infrastructure.</span></span>

>[!NOTE]
><span data-ttu-id="d3bfe-188">인증을 위해 중앙 집중식 RADIUS 서버를 통해 작동하는 VPN 서버가 이미 있는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-188">If you already have a working VPN server that uses a centralized RADIUS server for authentication, you can skip this section.</span></span>
>

### <a name="register-server-in-active-directory"></a><span data-ttu-id="d3bfe-189">Active Directory에 서버 등록</span><span class="sxs-lookup"><span data-stu-id="d3bfe-189">Register Server in Active Directory</span></span>
<span data-ttu-id="d3bfe-190">이 시나리오에서 제대로 toofunction, NPS 서버 hello toobe Active Directory에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-190">toofunction properly in this scenario, hello NPS server needs toobe registered in Active Directory.</span></span>

1. <span data-ttu-id="d3bfe-191">[서버 관리자]를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-191">Open Server Manager.</span></span>
2. <span data-ttu-id="d3bfe-192">[서버 관리자]에서 **도구**를 클릭한 다음 **네트워크 정책 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-192">In Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
3. <span data-ttu-id="d3bfe-193">Hello 네트워크 정책 서버 콘솔에서 마우스 오른쪽 단추로 클릭 **NPS (로컬)**, 클릭 하 고 **Active Directory에 등록 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-193">In hello Network Policy Server console, right-click **NPS (Local)**, and then click **Register server in Active Directory**.</span></span> <span data-ttu-id="d3bfe-194">**확인**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-194">Click **OK** two times.</span></span>

 ![네트워크 정책 서버](./media/nps-extension-vpn/image2.png)

4. <span data-ttu-id="d3bfe-196">Hello 콘솔을 hello 다음 절차에 대 한 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-196">Leave hello console open for hello next procedure.</span></span>

### <a name="use-wizard-tooconfigure-radius-server"></a><span data-ttu-id="d3bfe-197">마법사 tooconfigure RADIUS 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d3bfe-197">Use wizard tooconfigure RADIUS server</span></span>
<span data-ttu-id="d3bfe-198">표준 (마법사 기반)를 사용할 수 있습니다 또는 고급 구성 옵션 tooconfigure hello RADIUS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-198">You can use a standard (wizard-based) or advanced configuration option tooconfigure hello RADIUS server.</span></span> <span data-ttu-id="d3bfe-199">이 섹션에 hello 마법사 기반 표준 구성 옵션의 hello를 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-199">This section assumes hello use of hello wizard-based standard configuration option.</span></span>

1. <span data-ttu-id="d3bfe-200">Hello 네트워크 정책 서버 콘솔에서 클릭 **NPS (로컬)**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-200">In hello Network Policy Server console, click **NPS (Local)**.</span></span>
2. <span data-ttu-id="d3bfe-201">[표준 구성] 아래에서 **전화 접속 또는 VPN 연결을 위한 RADIUS 서버**를 선택한 다음 **VPN 또는 전화 접속 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-201">Under Standard Configuration, select **RADIUS Server for Dial-Up or VPN Connections**, and then click **Configure VPN or Dial-Up**.</span></span>

 ![VPN 구성](./media/nps-extension-vpn/image3.png)

3. <span data-ttu-id="d3bfe-203">Hello 선택 전화 접속 또는 개인 가상 네트워크 연결 유형 페이지에서 선택 **가상 개인 네트워크 연결**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-203">On hello Select Dial-up or Virtual Private Network Connections Type page, select **Virtual Private Network Connections**, and click **Next**.</span></span>

 ![가상 사설망](./media/nps-extension-vpn/image4.png)

4. <span data-ttu-id="d3bfe-205">Hello 지정 전화 접속 또는 VPN 서버 페이지에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-205">On hello Specify Dial-Up or VPN Server page, click **Add**.</span></span>
5. <span data-ttu-id="d3bfe-206">Hello에 **새 RADIUS 클라이언트** 대화 상자에서 이름을 제공 hello 확인 가능 이름은 또는 hello VPN 서버의 IP 주소를 입력 하 고 공유 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-206">In hello **New RADIUS client** dialog box, provide a friendly name, enter hello resolvable name or IP address of hello VPN server, and enter a shared secret password.</span></span> <span data-ttu-id="d3bfe-207">이 공유 비밀 암호는 길고 복잡하게 만들고,</span><span class="sxs-lookup"><span data-stu-id="d3bfe-207">Make this shared secret password long and complex.</span></span> <span data-ttu-id="d3bfe-208">Hello 다음 섹션의 단계에 필요한 만큼이 암호를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-208">Record this password, as you need it for steps in hello next section.</span></span>

 ![새 RADIUS 클라이언트](./media/nps-extension-vpn/image5.png)

6. <span data-ttu-id="d3bfe-210">**확인**을 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-210">Click **OK**, and then **Next**.</span></span>
7. <span data-ttu-id="d3bfe-211">Hello에 **인증 방법 구성** 페이지 hello 기본 선택 항목을 적용 합니다 (Microsoft 암호화 인증 버전 2 (ms-chap v 2) 또는 다른 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-211">On hello **Configure Authentication Methods** page, accept hello default selection (Microsoft Encrypted Authentication version 2 (MS-CHAPv2) or choose another option, and click **Next**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="d3bfe-212">EAP(확장할 수 있는 인증 프로토콜)를 구성하는 경우 MS CHAPv2 또는 PEAP를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-212">If you configure Extensible Authentication Protocol (EAP), you must use either MS CHAPv2 or PEAP.</span></span> <span data-ttu-id="d3bfe-213">다른 EAP는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-213">No other EAP is supported.</span></span>
 
8. <span data-ttu-id="d3bfe-214">Hello 사용자 그룹 지정 페이지에서 클릭 **추가** 하 고 있는 경우 해당 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-214">On hello Specify User Groups page, click **Add** and select an appropriate group, if one exists.</span></span> <span data-ttu-id="d3bfe-215">그렇지 않으면 빈 toogrant 액세스 tooall 사용자 hello 선택 항목을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-215">Otherwise, leave hello selection blank toogrant access tooall users.</span></span>

 ![사용자 그룹 지정](./media/nps-extension-vpn/image7.png)

9. <span data-ttu-id="d3bfe-217">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-217">Click **Next**.</span></span>
10. <span data-ttu-id="d3bfe-218">Hello IP 필터 지정 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-218">On hello Specify IP Filters page, click **Next**.</span></span>
11. <span data-ttu-id="d3bfe-219">Hello 암호화 설정 지정 페이지에서 hello 기본 설정을 적용 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-219">On hello Specify Encryption Settings page, accept hello default settings, and click **Next**.</span></span>

 ![암호화 지정](./media/nps-extension-vpn/image8.png)

12. <span data-ttu-id="d3bfe-221">영역 이름 지정 hello에 hello 이름을 비워 둡니다 hello 기본 설정을 적용 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-221">On hello Specify a Realm Name, leave hello name blank, accept hello default setting, and click **Next**.</span></span>

 ![영역 이름 지정](./media/nps-extension-vpn/image9.png)

13. <span data-ttu-id="d3bfe-223">Hello 새 완료 전화 접속 또는 개인 가상 네트워크 연결 및 RADIUS 클라이언트 페이지에서 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-223">On hello Completing New Dial-up or Virtual Private Network Connections and RADIUS clients page, click **Finish**.</span></span>

 ![연결 완료](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a><span data-ttu-id="d3bfe-225">RADIUS 구성 확인</span><span class="sxs-lookup"><span data-stu-id="d3bfe-225">Verify RADIUS configuration</span></span>
<span data-ttu-id="d3bfe-226">이 섹션에는 hello 마법사를 사용 하 여 만든 hello 구성을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-226">This section details hello configuration you created using hello wizard.</span></span>

1. <span data-ttu-id="d3bfe-227">Hello NPS (로컬) 콘솔에서 hello NPS 서버의 RADIUS 클라이언트를 확장 하 고 선택 **RADIUS 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-227">On hello NPS server, in hello NPS (Local) console, expand RADIUS Clients, and select **RADIUS Clients**.</span></span>
2. <span data-ttu-id="d3bfe-228">Hello 세부 정보 창에서 마법사를 사용 하 여 만든 hello RADIUS 클라이언트를 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-228">In hello details pane, right-click hello RADIUS client you created using wizard, and click **Properties**.</span></span> <span data-ttu-id="d3bfe-229">RADIUS 클라이언트 (hello VPN 서버)에 대 한 hello 속성 아래에 표시 된 유사한 toothose 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-229">hello properties for your RADIUS client (hello VPN server) should be similar toothose shown below.</span></span>

 ![VPN 속성](./media/nps-extension-vpn/image11.png)

3. <span data-ttu-id="d3bfe-231">**취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-231">Click **Cancel**.</span></span>
4. <span data-ttu-id="d3bfe-232">Hello NPS (로컬) 콘솔에서 hello NPS 서버에서 확장 **정책**를 선택 하 고 **연결 요청 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-232">On hello NPS server, in hello NPS (Local) console, expand **Policies**, and select **Connection Request Policies**.</span></span> <span data-ttu-id="d3bfe-233">아래 hello 이미지 유사한 hello VPN 연결 정책이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-233">You should see hello VPN Connections policy that resembles hello image below.</span></span>

 ![연결 요청](./media/nps-extension-vpn/image12.png)

5. <span data-ttu-id="d3bfe-235">[정책] 아래에서 **네트워크 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-235">Under Policies, select **Network Policies**.</span></span> <span data-ttu-id="d3bfe-236">아래 hello 이미지 유사한 가상 개인 네트워크 (VPN) 연결 정책과 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-236">You should a Virtual Private Network (VPN) Connections policy that resembles hello image below.</span></span>

 ![네트워크 속성](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a><span data-ttu-id="d3bfe-238">VPN 서버 toouse RADIUS 인증 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-238">Configure VPN Server toouse RADIUS authentication</span></span>
<span data-ttu-id="d3bfe-239">이 섹션에서는 hello VPN 서버 toouse RADIUS 인증을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-239">In this section, you configure hello VPN server toouse RADIUS authentication.</span></span> <span data-ttu-id="d3bfe-240">이 섹션에서는 VPN 서버의 작업 중인 구성 했지만 hello VPN 서버 toouse RADIUS 인증을 구성 하지 않은 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-240">This section assumes that you have a working configuration of VPN server but have not configured hello VPN server toouse RADIUS authentication.</span></span> <span data-ttu-id="d3bfe-241">Hello VPN 서버를 구성한 후 구성을 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-241">After configuring hello VPN server, you confirm that your configuration is working as expected.</span></span>

>[!NOTE]
><span data-ttu-id="d3bfe-242">RADIUS 인증을 통해 작동하는 VPN 서버 구성이 이미 있는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-242">If you already have a working VPN server configuration that uses RADIUS authentication, you can skip this section.</span></span>
>

### <a name="configure-authentication-provider"></a><span data-ttu-id="d3bfe-243">인증 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-243">Configure authentication provider</span></span>
1. <span data-ttu-id="d3bfe-244">Hello VPN 서버에서 서버 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-244">On hello VPN server, open Server Manager.</span></span>
2. <span data-ttu-id="d3bfe-245">[서버 관리자]에서 **도구**, **라우팅 및 원격 액세스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-245">In Server Manager, click **Tools**, and then **Routing and Remote Access**.</span></span>
3. <span data-ttu-id="d3bfe-246">Hello 라우팅 및 원격 액세스 콘솔에서 마우스 오른쪽 단추로 클릭  **\[서버 이름\] (local)**, 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-246">In hello Routing and Remote Access console, right-click **\[Server Name\] (local)**, and then click **Properties**.</span></span>

 ![라우팅 및 원격 액세스](./media/nps-extension-vpn/image14.png)
 
4. <span data-ttu-id="d3bfe-248">Hello에 **[서버 이름} (로컬) 속성** 대화 상자를 클릭 hello **보안** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-248">In hello **[Server Name} (local) Properties** dialog box, click hello **Security** tab.</span></span> 
5. <span data-ttu-id="d3bfe-249">Hello에 **보안** 인증 공급자에서 탭을 클릭 하 여 **RADIUS 인증**, 차례로 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-249">On hello **Security** tab, under Authentication provider, click **RADIUS Authentication**, and then **Configure**.</span></span>

 ![RADIUS 인증](./media/nps-extension-vpn/image15.png)
 
6. <span data-ttu-id="d3bfe-251">Hello RADIUS 인증 대화 상자에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-251">In hello RADIUS Authentication dialog box, click **Add**.</span></span>
7. <span data-ttu-id="d3bfe-252">서버 이름에 RADIUS 서버 추가 hello hello 이전 섹션에 구성 된 hello RADIUS 서버 hello 이름 또는 hello IP 주소를 추가 하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-252">In hello Add RADIUS Server, in Server name, add hello name or hello IP address of hello RADIUS server you configured in hello previous section.</span></span>
8. <span data-ttu-id="d3bfe-253">공유 암호 클릭 **변경** hello 공유 만들고 이전에 기록 된 암호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-253">In Shared secret, click **Change** and add hello shared secret password you created and recorded earlier.</span></span>
9. <span data-ttu-id="d3bfe-254">시간 제한 (초) 사이의 hello 값 tooa 값 변경 **30** 및 **60**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-254">In Time-out (seconds), change hello value tooa value between **30** and **60**.</span></span> <span data-ttu-id="d3bfe-255">필요한 tooallow toocomplete hello 두 번째 인증 단계 충분 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-255">This is necessary tooallow enough time toocomplete hello second authentication factor.</span></span>
 
 ![RADIUS 서버 추가](./media/nps-extension-vpn/image16.png)
 
10. <span data-ttu-id="d3bfe-257">모든 대화 상자를 닫을 때까지 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-257">Click **OK** until you complete closing all dialog boxes.</span></span>

### <a name="test-vpn-connectivity"></a><span data-ttu-id="d3bfe-258">VPN 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="d3bfe-258">Test VPN connectivity</span></span>
<span data-ttu-id="d3bfe-259">이 섹션에서는 hello VPN 클라이언트가 해당 데이터 및 tooconnect tooVPN 가상 포트를 시도할 때 hello RADIUS 서버에서 권한 부여를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-259">In this section, you confirm that hello VPN client is authenticated and authorized by hello RADIUS server when you attempt tooconnect tooVPN virtual port.</span></span> <span data-ttu-id="d3bfe-260">여기서는 Windows 10을 VPN 클라이언트로 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-260">This section assumes you are using Windows 10 as a VPN client.</span></span> 

>[!NOTE]
><span data-ttu-id="d3bfe-261">이미 VPN 클라이언트 tooconnect toohello VPN 서버를 구성 하 고 hello 설정을 저장 한, 경우에 hello 단계 관련된 tooconfiguring 및 VPN 연결 개체를 저장을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-261">If you already configured a VPN client tooconnect toohello VPN server and have saved hello settings, you can skip hello steps related tooconfiguring and saving a VPN connection object.</span></span>
>

1. <span data-ttu-id="d3bfe-262">VPN 클라이언트 컴퓨터에서 **시작**을 클릭한 다음 **설정**(기어 아이콘)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-262">On your VPN client computer, click **Start**, and then **Settings** (gear icon).</span></span>
2. <span data-ttu-id="d3bfe-263">[창 설정]에서 **네트워크 및 인터넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-263">In Window Settings, click **Network & Internet**.</span></span>
3. <span data-ttu-id="d3bfe-264">**VPN**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-264">Click **VPN**.</span></span>
4. <span data-ttu-id="d3bfe-265">**VPN 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-265">Click **Add a VPN connection**.</span></span>
5. <span data-ttu-id="d3bfe-266">VPN 연결을 추가 VPN 공급자는 만든 다음 필드를 적절 하 게 남은 전체 hello hello 따라 Windows (기본 제공)를 지정 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-266">In Add a VPN connection, specify Windows (built-in) as hello VPN provider, then complete hello remaining fields, as appropriate, and click **Save**.</span></span> 

 ![VPN 연결 추가](./media/nps-extension-vpn/image17.png)
 
6. <span data-ttu-id="d3bfe-268">열기 hello **네트워크 및 공유 센터** 제어판에서.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-268">Open hello **Network and Sharing Center** in Control Panel.</span></span>
7. <span data-ttu-id="d3bfe-269">**어댑터 설정 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-269">Click **Change adapter settings**.</span></span>

 ![어댑터 설정 변경](./media/nps-extension-vpn/image18.png)

8. <span data-ttu-id="d3bfe-271">Hello VPN 네트워크 연결을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-271">Right-click hello VPN network connection, and click Properties.</span></span> 

 ![VPN 네트워크 속성](./media/nps-extension-vpn/image19.png)

9. <span data-ttu-id="d3bfe-273">Hello VPN 속성 대화 상자에서 클릭 hello **보안** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-273">In hello VPN properties dialog box, click hello **Security** tab.</span></span> 
10. <span data-ttu-id="d3bfe-274">Hello 보안 탭에서 확인만 **Microsoft CHAP 버전 2 (MS-CHAP v2)** 을 선택 하 고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-274">On hello Security tab, ensure that only **Microsoft CHAP Version 2 (MS-CHAP v2)** is selected, and click OK.</span></span>

 ![프로토콜 허용](./media/nps-extension-vpn/image20.png)

11. <span data-ttu-id="d3bfe-276">Hello VPN 연결을 마우스 오른쪽 단추로 클릭 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-276">Right-click hello VPN connection, and click **Connect**.</span></span>
12. <span data-ttu-id="d3bfe-277">Hello 설정 페이지에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-277">On hello Settings page, click **Connect**.</span></span>

<span data-ttu-id="d3bfe-278">연결에 성공 아래와 같이 이벤트 ID 6272와 RADIUS 서버 hello에 hello 보안 로그에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-278">A successful connection appears in hello Security log on hello RADIUS server as Event ID 6272, as shown below.</span></span>

 ![이벤트 속성](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="d3bfe-280">문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="d3bfe-280">Troubleshoot Guide</span></span>
<span data-ttu-id="d3bfe-281">Hello VPN 서버 toouse 인증 및 권한 부여에 대 한 중앙 집중식된 RADIUS 서버를 구성 하기 전에 VPN 구성 작동 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-281">Assume that your VPN configuration was working before you configured hello VPN server toouse a centralized RADIUS server for authentication and authorization.</span></span> <span data-ttu-id="d3bfe-282">이 경우 잘못 된 사용자 이름 또는 암호 사용 하 여 RADIUS 서버 또는 hello hello의 구성이 잘못 hello 문제의 원인일 수 있습니다 수 가능성이입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-282">In this case, it is likely that hello issue may be caused by a misconfiguration of hello RADIUS Server or hello use of an invalid username or password.</span></span> <span data-ttu-id="d3bfe-283">예를 들어 hello 사용자 이름에 UPN 접미사를 대체 하는 hello를 사용 하는 경우 hello 로그인 시도가 실패할 수 있습니다 (사용 해야 최상의 결과 동일한 계정 이름을 hello).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-283">For example, if you use hello alternate UPN suffix in hello username, hello login attempt might fail (you should use hello same Account name for best results).</span></span> 

<span data-ttu-id="d3bfe-284">이러한 문제를 간단 하 게 수행할 toostart tooexamine hello 보안 이벤트 로그 켜져 tootroubleshoot RADIUS 서버를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-284">tootroubleshoot these issues, an ideal place toostart is tooexamine hello Security event logs on hello RADIUS server.</span></span> <span data-ttu-id="d3bfe-285">toosave 시간 검색 이벤트에 대 한으로 사용할 수 있습니다 hello 역할 기반 네트워크 정책 및 액세스 서버의 사용자 지정 보기 이벤트 뷰어에서 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-285">toosave time searching for events, you can use hello role-based Network Policy and Access Server custom view in Event Viewer, as show below.</span></span> <span data-ttu-id="d3bfe-286">이벤트 ID 6273 여기서 hello 네트워크 정책 서버에서 거부 액세스 tooa 사용자 이벤트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-286">Event ID 6273 indicates events where hello Network Policy Server denied access tooa user.</span></span> 

 ![이벤트 뷰어](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="d3bfe-288">Multi-Factor Authentication 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-288">Configure Multi-Factor Authentication</span></span>
<span data-ttu-id="d3bfe-289">이 섹션에서는 사용자가 MFA를 사용하도록 설정하고 2단계 인증에 대한 계정을 설정하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-289">This section provides instructions for enabling users for MFA and for setting up accounts for two-step verification.</span></span> 

### <a name="enable-multi-factor-authentication"></a><span data-ttu-id="d3bfe-290">다단계 인증 사용</span><span class="sxs-lookup"><span data-stu-id="d3bfe-290">Enable multi-factor authentication</span></span>
<span data-ttu-id="d3bfe-291">이 섹션에서는 Azure AD 계정에서 MFA를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-291">In this section, you enable Azure AD accounts for MFA.</span></span> <span data-ttu-id="d3bfe-292">사용 하 여 hello **클래식 포털** tooenable 사용자가 MFA에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-292">Use hello **classic portal** tooenable users for MFA.</span></span> 

1. <span data-ttu-id="d3bfe-293">브라우저를 열고 너무 이동[https://manage.windowsazure.com](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-293">Open a browser, and navigate too[https://manage.windowsazure.com](https://manage.windowsazure.com).</span></span> 
2. <span data-ttu-id="d3bfe-294">관리자에 게로 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-294">Log on as hello administrator.</span></span>
3. <span data-ttu-id="d3bfe-295">Hello 포털 hello 왼쪽된 탐색 영역에서 클릭 **ACTIVE DIRECTORY**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-295">In hello portal, in hello left navigation, click **ACTIVE DIRECTORY**.</span></span>

 ![기본 디렉터리](./media/nps-extension-vpn/image23.png)

4. <span data-ttu-id="d3bfe-297">Hello 이름 열에서 클릭 **기본 디렉터리** (또는 다른 디렉터리에 해당 하는 경우).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-297">In hello NAME column, click **Default Directory** (or another directory, if appropriate).</span></span>
5. <span data-ttu-id="d3bfe-298">Hello 빠른 시작 페이지에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-298">On hello Quick Start page, click **Configure**.</span></span>

 ![기본 구성](./media/nps-extension-vpn/image24.png)

6. <span data-ttu-id="d3bfe-300">Hello 구성 페이지에서 아래로 스크롤하여, hello multi-factor 인증 섹션에서 클릭 **서비스 설정 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-300">On hello CONFIGURE page, scroll down and, in hello multi-factor authentication section, click **Manage service settings**.</span></span>

 ![MFA 설정 관리](./media/nps-extension-vpn/image25.png)
 
7. <span data-ttu-id="d3bfe-302">Hello multi-factor authentication 페이지에 hello 기본 서비스 설정을 검토 한 다음 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-302">On hello multi-factor authentication page, review hello default service settings, and then click **Users**.</span></span> 

 ![MFA 사용자](./media/nps-extension-vpn/image26.png)
 
8. <span data-ttu-id="d3bfe-304">Hello 사용자 페이지에서 tooenable MFA에 대 한 선택 하 고 클릭 hello 사용자를 선택 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-304">On hello Users page, select hello users that you wish tooenable for MFA, and then click **Enable**.</span></span>

 ![properties](./media/nps-extension-vpn/image27.png)
 
9. <span data-ttu-id="d3bfe-306">메시지가 표시되면 **다단계 인증 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-306">When prompted, click **Enable multi-factor auth**.</span></span>

 ![MFA 사용](./media/nps-extension-vpn/image28.png)
 
10. <span data-ttu-id="d3bfe-308">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-308">Click **Close**.</span></span> 
11. <span data-ttu-id="d3bfe-309">Hello 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-309">Refresh hello page.</span></span> <span data-ttu-id="d3bfe-310">hello MFA 상태는 변경 된 tooEnabled입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-310">hello MFA status is changed tooEnabled.</span></span>

<span data-ttu-id="d3bfe-311">방법에 대 한 내용은 tooenable 사용자가 Multi-factor Authentication에 대 한 참조 [hello 클라우드에서 Azure Multi-factor Authentication 시작](multi-factor-authentication-get-started-cloud.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-311">For information on how tooenable users for Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](multi-factor-authentication-get-started-cloud.md).</span></span> 

### <a name="configure-accounts-for-two-step-verification"></a><span data-ttu-id="d3bfe-312">2단계 인증에 대한 계정 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-312">Configure accounts for two-step verification</span></span>
<span data-ttu-id="d3bfe-313">사용자가 MFA에 대 한 계정을 활성화 된, 수 toosign tooresources hello 두 번째 인증 단계 2 단계 인증 사용 하는 것에 대 한 신뢰할 수 있는 장치 toouse 성공적으로 구성한 될 때까지 hello MFA 정책에 의해 제어에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-313">Once an account has been enabled for MFA, users are not able toosign in tooresources governed by hello MFA policy until they have successfully configured a trusted device toouse for hello second authentication factor having used two-step verification.</span></span>

<span data-ttu-id="d3bfe-314">이 섹션에서는 2단계 인증에 사용할 신뢰할 수 있는 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-314">In this section, you configure a trusted device for use with two-step verification.</span></span> <span data-ttu-id="d3bfe-315">여러 가지 tooconfigure 있습니다 사용할 수 있는 hello 다음을 비롯 한 이러한:</span><span class="sxs-lookup"><span data-stu-id="d3bfe-315">There are several options available for you tooconfigure these, including hello following:</span></span>

* <span data-ttu-id="d3bfe-316">**모바일 앱**</span><span class="sxs-lookup"><span data-stu-id="d3bfe-316">**Mobile app**.</span></span> <span data-ttu-id="d3bfe-317">Windows Phone, Android 또는 iOS 장치에 hello Microsoft Authenticator 앱을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-317">You install hello Microsoft Authenticator app on a Windows Phone, Android, or iOS device.</span></span> <span data-ttu-id="d3bfe-318">조직의 정책에 따라 두 가지 모드 중 하나에 필요한 toouse hello 앱 중인: (푸시 알림이 표시 됩니다 tooyour 장치) 확인 작업에 대 한 알림을 수신 또는 क ो ड (해야 tooenter은 유효성 검사 하는 코드 30 초 마다 업데이트 포함).</span><span class="sxs-lookup"><span data-stu-id="d3bfe-318">Depending on your organization’s policies, you are required toouse hello app in one of two modes: Receive notifications for verifications (a notification is pushed tooyour device) or Use verification code (you are required tooenter a verification code that updates every 30 seconds).</span></span> 
* <span data-ttu-id="d3bfe-319">**휴대폰 통화 또는 문자 메시지**</span><span class="sxs-lookup"><span data-stu-id="d3bfe-319">**Mobile phone call or text**.</span></span> <span data-ttu-id="d3bfe-320">자동 전화 통화 또는 문자 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-320">You can either receive an automated phone call or text message.</span></span> <span data-ttu-id="d3bfe-321">Hello 전화 통화 옵션을 hello 호출에 응답 하 고 hello # 기호 tooauthenticate 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-321">With hello phone call option, you answer hello call and press hello # sign tooauthenticate.</span></span> <span data-ttu-id="d3bfe-322">Hello 텍스트 옵션을 사용 toohello 문자 메시지에 회신 하거나 hello 로그인 인터페이스에 hello 확인 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-322">With hello text option, you can either reply toohello text message or enter hello verification code into hello sign-in interface.</span></span>
* <span data-ttu-id="d3bfe-323">**사무실 전화 통화**</span><span class="sxs-lookup"><span data-stu-id="d3bfe-323">**Office phone call**.</span></span> <span data-ttu-id="d3bfe-324">이 프로세스는 위의 자동된 전화 통화에 대해 설명 된 것과 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-324">This process is hello same as that described for automated phone calls above.</span></span>

<span data-ttu-id="d3bfe-325">확인을 위해 장치 toouse hello 모바일 앱 tooreceive 푸시 알림을를 설정 하기 위한 다음이 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-325">Follow these instructions for setting up a device toouse hello mobile app tooreceive push notification for verification.</span></span>

1. <span data-ttu-id="d3bfe-326">너무 로그온[https://aka.ms/mfasetup](https://aka.ms/mfasetup) 또는 모든 사이트와 같은 [https://portal.azure.com](https://portal.azure.com), tooauthenticate MFA 사용이 가능한 자격 증명을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-326">Log on too[https://aka.ms/mfasetup](https://aka.ms/mfasetup) or any site, such as [https://portal.azure.com](https://portal.azure.com), where you required tooauthenticate using your MFA-enabled credentials.</span></span> 
2. <span data-ttu-id="d3bfe-327">사용자 이름 및 암호 로그인 시 추가 보안 확인에 대 한 hello 계정을 tooset 라는 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-327">Upon signing in with your username and password, you are presented with a screen that prompts you tooset up hello account for additional security verification.</span></span>

 ![추가 보안](./media/nps-extension-vpn/image29.png)

3. <span data-ttu-id="d3bfe-329">**지금 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-329">Click **Set it up now**.</span></span>
4. <span data-ttu-id="d3bfe-330">Hello 추가 보안 확인 페이지에는 연락처 유형 (인증 전화, 사무실 전화 또는 모바일 앱)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-330">On hello Additional security verification page, select a contact type (authentication phone, office phone, or mobile app).</span></span> <span data-ttu-id="d3bfe-331">그런 다음 국가 또는 지역을 선택하고 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-331">Then select a country or region, and select a method.</span></span> <span data-ttu-id="d3bfe-332">hello 메서드 선택한 연락처 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-332">hello method varies by contact type you select.</span></span> <span data-ttu-id="d3bfe-333">예를 들어 모바일 응용 프로그램을 선택 하는 경우 선택할 수 있습니다 여부를 확인 또는 toouse 확인 코드에 대 한 tooreceive 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-333">For example, if you choose Mobile app, you can select whether tooreceive notifications for verification or toouse a verification code.</span></span> <span data-ttu-id="d3bfe-334">수행 하는 hello 단계 선택 한다고 가정 **모바일 앱** hello로의 연락처 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-334">hello steps that follow assume you choose **Mobile app** as hello contact type.</span></span>

 ![전화 인증](./media/nps-extension-vpn/image30.png)

5. <span data-ttu-id="d3bfe-336">모바일 앱을 선택하고 **확인 시 알림 수신**을 클릭한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-336">Select Mobile app, click **Receive notifications for verification**, and then **Set up**.</span></span> 

 ![모바일 앱 확인](./media/nps-extension-vpn/image31.png)
 
6. <span data-ttu-id="d3bfe-338">아직 수행 하지 않은 경우 hello authenticator 모바일 앱을 장치에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-338">If you haven’t done so already, install hello authenticator mobile app on your device.</span></span> 
7. <span data-ttu-id="d3bfe-339">바코드를 제공 하는 hello 모바일 앱 tooscan hello에 hello 지침에 따라 또는 수동으로 hello 정보를 입력 한 다음 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-339">Follow hello instructions in hello mobile app tooscan hello presented bar code or enter hello information manually, and then click **Done**.</span></span>

 ![모바일 앱 구성](./media/nps-extension-vpn/image32.png)

8. <span data-ttu-id="d3bfe-341">Hello 추가 보안 확인 페이지에서 클릭 **연락처 me** 하 고 회신 전송 toonotification tooyour 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-341">On hello Additional security verification page, click **Contact me** and reply toonotification sent tooyour device.</span></span>
9. <span data-ttu-id="d3bfe-342">액세스 toohello 모바일 앱, 손실 되 고 클릭 경우 hello 추가 보안 확인 페이지에 연락처 번호를 입력 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-342">On hello Additional security verification page, enter a contact number in case you lose access toohello mobile app, and click **Next**.</span></span>

 ![휴대폰 번호](./media/nps-extension-vpn/image33.png)
 
10. <span data-ttu-id="d3bfe-344">추가 보안 확인 hello 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-344">On hello Additional security verification, click **Done**.</span></span>

<span data-ttu-id="d3bfe-345">hello 장치 구성 된 tooprovide 확인의 두 번째 방법은 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-345">hello device is now configured tooprovide a second method of verification.</span></span> <span data-ttu-id="d3bfe-346">2단계 인증을 위한 계정 설정에 대한 자세한 내용은 [2단계 인증을 위한 계정 설정](./end-user/multi-factor-authentication-end-user-first-time.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-346">For information on setting up accounts for two-step verification, see [Set up my account for two-step verification](./end-user/multi-factor-authentication-end-user-first-time.md).</span></span>

## <a name="install-and-configure-nps-extension"></a><span data-ttu-id="d3bfe-347">NPS 확장 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-347">Install and configure NPS extension</span></span>

<span data-ttu-id="d3bfe-348">이 섹션에서는 VPN 서버 hello로 클라이언트 인증에 대 한 VPN toouse Azure MFA를 구성 하기 위한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-348">This section provides instructions for configuring VPN toouse Azure MFA for client authentication with hello VPN Server.</span></span>

<span data-ttu-id="d3bfe-349">설치 하 고 hello NPS 확장을 구성 하면이 서버에서 처리 하는 모든 RADIUS 기반 클라이언트 인증이 필요한 toouse Azure MFA입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-349">Once you install and configure hello NPS extension, all RADIUS-based client authentication that is processed by this server is required toouse Azure MFA.</span></span> <span data-ttu-id="d3bfe-350">그렇지 않은 경우 모든 VPN 사용자가 Azure MFA에 등록 된, 구성 된 toouse MFA가 아닌 다른 RADIUS 서버 tooauthenticate 사용자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-350">If not all your VPN users are enrolled in Azure MFA, you can set up another RADIUS server tooauthenticate users who are not configured toouse MFA.</span></span> <span data-ttu-id="d3bfe-351">또는 MFA에 등록 되어 있는 경우에 두 번째 인증 단계를 사용자가 문제가 tooprovide를 허용 하는 레지스트리 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-351">Or you can create a registry entry that allows challenged users tooprovide a second authentication factor, only if they are enrolled in MFA.</span></span> 

<span data-ttu-id="d3bfe-352">라는 새 문자열 값을 만들고 _HKLM\SOFTWARE\Microsoft\AzureMfa에 REQUIRE_USER_MATCH_, hello 값 tooTRUE 또는 FALSE를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-352">Create a new string value named _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_, and set hello value tooTRUE or FALSE.</span></span> 

 ![사용자 일치 필요](./media/nps-extension-vpn/image34.png)
 
<span data-ttu-id="d3bfe-354">있는 경우 hello 값은 집합 tooTRUE 또는 설정 하지 모든 인증 요청 제목 tooan MFA 챌린지입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-354">If hello value is set tooTRUE or not set, all authentication requests are subject tooan MFA challenge.</span></span> <span data-ttu-id="d3bfe-355">Hello 값 tooFALSE을 설정 하는 경우 MFA 과제 MFA에 등록 된 toousers만 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-355">If hello value is set tooFALSE, MFA challenges are issued only toousers that are enrolled in MFA.</span></span> <span data-ttu-id="d3bfe-356">Hello FALSE 설정 테스트 또는 프로덕션 환경에서 온 보 딩 기간 동안에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-356">Only use hello FALSE setting in testing or in production environments during an onboarding period.</span></span>

### <a name="acquire-azure-active-directory-guid-id"></a><span data-ttu-id="d3bfe-357">Azure Active Directory GUID ID 얻기</span><span class="sxs-lookup"><span data-stu-id="d3bfe-357">Acquire Azure Active Directory GUID ID</span></span>

<span data-ttu-id="d3bfe-358">Hello NPS 확장의 hello 구성의 일부로 해야 toosupply 관리자 자격 증명 및 Azure Active Directory ID hello Azure AD 테 넌 트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-358">As part of hello configuration of hello NPS extension, you need toosupply admin credentials and hello Azure Active Directory ID for your Azure AD tenant.</span></span> <span data-ttu-id="d3bfe-359">hello 단계 아래 설명 tooget hello 테 넌 트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-359">hello steps below show you how tooget hello tenant ID.</span></span>

1. <span data-ttu-id="d3bfe-360">Toohello Azure 포털에 로그인 [https://portal.azure.com](https://portal.azure.com) 테 넌 트 hello Azure의 hello 전역 관리자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-360">Sign in toohello Azure portal at [https://portal.azure.com](https://portal.azure.com) as hello global administrator of hello Azure tenant.</span></span>
2. <span data-ttu-id="d3bfe-361">왼쪽 탐색 hello, 클릭 hello **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-361">In hello left navigation, click hello **Azure Active Directory** icon.</span></span>
3. <span data-ttu-id="d3bfe-362">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-362">Click **Properties**.</span></span>
4. <span data-ttu-id="d3bfe-363">toocopy 디렉터리 ID toohello 클립보드, 선택 hello **복사** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-363">toocopy your Directory ID toohello clipboard, select hello **Copy** icon.</span></span>
 
 ![디렉터리 ID](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a><span data-ttu-id="d3bfe-365">Hello NPS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="d3bfe-365">Install hello NPS extension</span></span>
<span data-ttu-id="d3bfe-366">hello NPS 확장 디자인에 대 한 hello RADIUS 서버로 toobe hello 네트워크 정책에 있는 서버에 설치 및 액세스 서비스 (NPS) 역할이 설치 및 해당 함수를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-366">hello NPS extension needs toobe installed on a server that has hello Network Policy and Access Services (NPS) role installed and that functions as hello RADIUS server in your design.</span></span> <span data-ttu-id="d3bfe-367">원격 데스크톱 서버의 hello NPS 확장을 설치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-367">Don't install hello NPS extension on your Remote Desktop Server.</span></span>

1. <span data-ttu-id="d3bfe-368">hello NPS 확장을 다운로드 [https://aka.ms/npsmfa](https://aka.ms/npsmfa)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-368">Download hello NPS extension from [https://aka.ms/npsmfa](https://aka.ms/npsmfa).</span></span> 
2. <span data-ttu-id="d3bfe-369">Hello 설치 프로그램 실행 파일 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-369">Copy hello setup executable file (NpsExtnForAzureMfaInstaller.exe) toohello NPS server.</span></span>
3. <span data-ttu-id="d3bfe-370">Hello NPS 서버에서 두 번 클릭 **NpsExtnForAzureMfaInstaller.exe**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-370">On hello NPS server, double-click **NpsExtnForAzureMfaInstaller.exe**.</span></span> <span data-ttu-id="d3bfe-371">메시지가 표시되면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-371">If prompted, click **Run**.</span></span>
4. <span data-ttu-id="d3bfe-372">NPS 확장 Azure MFA 대화 상자에 대 한 hello, hello 소프트웨어 사용 조건 검토 확인 **toohello 사용 약관 동의**를 클릭 하 고 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-372">In hello NPS Extension for Azure MFA dialog box, review hello software license terms, check **I agree toohello license terms and conditions**, and click **Install**.</span></span>

 ![NPS 확장](./media/nps-extension-vpn/image36.png)
 
5. <span data-ttu-id="d3bfe-374">NPS 확장 Azure MFA 대화 상자에 대 한 hello, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-374">In hello NPS Extension for Azure MFA dialog box, click **Close**.</span></span>  

 ![성공적인 설치](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a><span data-ttu-id="d3bfe-376">PowerShell 스크립트를 사용 하 여 hello NPS 확장으로 사용 하기 위해 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="d3bfe-376">Configure certificates for use with hello NPS extension using a PowerShell script</span></span>
<span data-ttu-id="d3bfe-377">tooensure 보안 통신 및 보증 인증서가 필요 tooconfigure 사용 하기 위해 hello NPS 확장에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-377">tooensure secure communications and assurance, you need tooconfigure certificates for use by hello NPS extension.</span></span> <span data-ttu-id="d3bfe-378">hello NPS 구성 요소에는 NPS와 함께 사용 하기 위해 자체 서명 된 인증서를 구성 하는 Windows PowerShell 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-378">hello NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="d3bfe-379">hello 스크립트 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-379">hello script performs hello following actions:</span></span>

* <span data-ttu-id="d3bfe-380">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="d3bfe-380">Creates a self-signed certificate</span></span>
* <span data-ttu-id="d3bfe-381">Azure AD에서 사용자 인증서 tooservice의 공개 키를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-381">Associates public key of certificate tooservice principal on Azure AD</span></span>
* <span data-ttu-id="d3bfe-382">저장소 hello hello 로컬 컴퓨터 저장소에서 인증서</span><span class="sxs-lookup"><span data-stu-id="d3bfe-382">Stores hello cert in hello local machine store</span></span>
* <span data-ttu-id="d3bfe-383">Toohello 인증서의 개인 키 toohello 네트워크 사용자 액세스 부여</span><span class="sxs-lookup"><span data-stu-id="d3bfe-383">Grants access toohello certificate’s private key toohello Network User</span></span>
* <span data-ttu-id="d3bfe-384">네트워크 정책 서버 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d3bfe-384">Restarts Network Policy Server service</span></span>

<span data-ttu-id="d3bfe-385">자체 인증서 toouse 하려는 경우 Azure AD에서 tooassociate hello 공용 인증서 toohello 서비스 원칙의 필요 하 고 등입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-385">If you want toouse your own certificates, you need tooassociate hello public of your certificate toohello service principle on Azure AD, and so on.</span></span>
<span data-ttu-id="d3bfe-386">toouse hello 스크립트를 Azure Active Directory 관리자 자격 증명으로 hello 확장을 제공 하 고 앞에서 복사한 Azure Active Directory 테 넌 트 ID hello.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-386">toouse hello script, provide hello extension with your Azure Active Directory administrative credentials and hello Azure Active Directory tenant ID you copied earlier.</span></span> <span data-ttu-id="d3bfe-387">Hello NPS 확장을 설치 하는 각 NPS 서버에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-387">Run hello script on each NPS server where you install hello NPS extension.</span></span>

1. <span data-ttu-id="d3bfe-388">관리 Windows PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-388">Open an administrative Windows PowerShell prompt.</span></span>
2. <span data-ttu-id="d3bfe-389">Hello PowerShell 프롬프트에서 입력 _cd 'c:\Program Files\Microsoft\AzureMfa\Config'_, 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-389">At hello PowerShell prompt, type _cd ‘c:\Program Files\Microsoft\AzureMfa\Config’_, and press **ENTER**.</span></span>
3. <span data-ttu-id="d3bfe-390">_.\AzureMfsNpsExtnConfigSetup.ps1_을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-390">Type _.\AzureMfsNpsExtnConfigSetup.ps1_, and press **ENTER**.</span></span> 
 * <span data-ttu-id="d3bfe-391">hello 스크립트 hello Azure Active Directory PowerShell 모듈 설치 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-391">hello script checks toosee if hello Azure Active Directory PowerShell module is installed.</span></span> <span data-ttu-id="d3bfe-392">이 설치 되어 있지 않으면 hello 스크립트 hello 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-392">If it is not installed, hello script installs hello module for you.</span></span>
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. <span data-ttu-id="d3bfe-394">Hello PowerShell 모듈의 hello 설치를 확인 하는 hello 스크립트, 후 hello Azure Active Directory PowerShell 모듈 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-394">After hello script verifies hello installation of hello PowerShell module, it displays hello Azure Active Directory PowerShell module dialog box.</span></span> <span data-ttu-id="d3bfe-395">Hello 대화 상자에서 Azure AD 관리자 자격 증명 및 암호를 입력 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-395">In hello dialog box, enter your Azure AD admin credentials and password, and click **Sign in**.</span></span> 
 
 ![PowerShell 로그인](./media/nps-extension-vpn/image39.png)
 
5. <span data-ttu-id="d3bfe-397">대화 상자가 나타나면 toohello 클립보드를 앞에서 복사한 hello 테 넌 트 ID를 붙여 넣고 키를 눌러 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-397">When prompted, paste hello tenant ID you copied toohello clipboard earlier, and press **ENTER**.</span></span> 

 ![테넌트 ID](./media/nps-extension-vpn/image40.png)

6. <span data-ttu-id="d3bfe-399">hello 스크립트 자체 서명 된 인증서를 만들고 다른 구성 변경 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-399">hello script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="d3bfe-400">아래에 표시 된 hello 이미지와 같이 hello 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-400">hello output is like hello image shown below.</span></span>

 ![자체 서명된 인증서](./media/nps-extension-vpn/image41.png)

7. <span data-ttu-id="d3bfe-402">Hello 서버를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-402">Reboot hello server.</span></span>
 
### <a name="verify-configuration"></a><span data-ttu-id="d3bfe-403">구성 확인</span><span class="sxs-lookup"><span data-stu-id="d3bfe-403">Verify configuration</span></span>
<span data-ttu-id="d3bfe-404">tooverify hello 구성 tooestablish VPN 서버와 새 VPN 연결 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-404">tooverify hello configuration, you need tooestablish a new VPN connection with VPN server.</span></span> <span data-ttu-id="d3bfe-405">기본 인증을 위해 자격 증명 입력을 시 hello VPN 연결을 대기 hello 보조 인증 toosucceed hello 연결이 설정 되기 전에 아래와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-405">Upon successfully entering your credentials for primary authentication, hello VPN connection waits for hello secondary authentication toosucceed before hello connection is established, as shown below.</span></span> 

 ![구성 확인](./media/nps-extension-vpn/image42.png)

<span data-ttu-id="d3bfe-407">Azure MFA에서 이전에 구성한 hello 보조 확인 방법으로 성공적으로 인증 하는 경우 연결 된 toohello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-407">If you successfully authenticate with hello secondary verification method you previously configured in Azure MFA, you are connected toohello resource.</span></span> <span data-ttu-id="d3bfe-408">그러나 hello 보조 인증 실패할 경우 tooresource 액세스를 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-408">However, if hello secondary authentication is not successful, you are denied access tooresource.</span></span> 

<span data-ttu-id="d3bfe-409">Hello 인증자 아래 hello 예제에서 Windows phone에서 앱 인증이 사용 되는 tooprovide hello 보조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-409">In hello example below, hello Authenticator app on a Windows phone is used tooprovide hello secondary authentication.</span></span>

 ![계정 확인](./media/nps-extension-vpn/image43.png)

<span data-ttu-id="d3bfe-411">Hello 보조 메서드를 사용 하 여 인증 했습니다., 되 면 액세스 toohello 가상 포트 hello VPN 서버에 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-411">Once you have successfully authenticated using hello secondary method, you are granted access toohello virtual port on hello VPN server.</span></span> <span data-ttu-id="d3bfe-412">그러나 필요한 toouse 신뢰할 수 있는 장치에서 모바일 앱을 사용 하 여 보조 인증 방법 이었으므로 hello 로그인 과정에서는 사용자 이름에만 사용 될 수 것 보다 더 안전 / 암호 조합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-412">However, because you were required toouse a secondary authentication method using a mobile app on a trusted device, hello log in process is more secure than it would be using only a username / password combination.</span></span>

### <a name="view-event-viewer-logs-for-successful-logon-events"></a><span data-ttu-id="d3bfe-413">성공적인 로그온 이벤트에 대한 이벤트 뷰어 로그 보기</span><span class="sxs-lookup"><span data-stu-id="d3bfe-413">View Event Viewer logs for successful logon events</span></span>
<span data-ttu-id="d3bfe-414">hello Windows 이벤트 뷰어 로그에서 tooview hello 성공적인 로그온 이벤트를 hello hello NPS 서버에서 Windows PowerShell 명령 tooquery hello Windows 보안 로그를 다음 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-414">tooview hello successful logon events in hello Windows Event Viewer logs, you can issue hello following Windows PowerShell command tooquery hello Windows Security log on hello NPS server.</span></span>

<span data-ttu-id="d3bfe-415">다음 명령을, hello를 사용 하 여 hello 보안 이벤트 뷰어 로그에서 tooquery 성공 로그온 이벤트</span><span class="sxs-lookup"><span data-stu-id="d3bfe-415">tooquery successful logon events in hello Security event viewer logs, use hello following command,</span></span>
* <span data-ttu-id="d3bfe-416">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="d3bfe-416">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span> 

 ![보안 이벤트 뷰어](./media/nps-extension-vpn/image44.png)
 
<span data-ttu-id="d3bfe-418">아래와 같이 hello 보안 로그 또는 네트워크 정책 및 액세스 서비스 사용자 지정 보기 hello도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-418">You can also view hello Security log or hello Network Policy and Access Services custom view, as shown below:</span></span>

 ![네트워크 정책 액세스](./media/nps-extension-vpn/image45.png)

<span data-ttu-id="d3bfe-420">Azure MFA에 대 한 hello NPS 확장을 설치한 hello 서버에서 찾을 수 있습니다 이벤트 뷰어 응용 프로그램 로그에서 특정 toohello 확장 **응용 프로그램 및 서비스 Logs\Microsoft\AzureMfa**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-420">On hello server where you installed hello NPS extension for Azure MFA, you can find Event Viewer application logs specific toohello extension at **Application and Services Logs\Microsoft\AzureMfa**.</span></span> 

* <span data-ttu-id="d3bfe-421">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="d3bfe-421">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span>

 ![이벤트 수](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="d3bfe-423">문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="d3bfe-423">Troubleshoot Guide</span></span>
<span data-ttu-id="d3bfe-424">Hello 구성이 예상 대로 작동 하지 않는 경우 좋은 위치 toostart tootroubleshoot 경우 사용자 hello tooverify가 구성 된 toouse Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-424">If hello configuration is not working as expected, a good place toostart tootroubleshoot is tooverify that hello user is configured toouse Azure MFA.</span></span> <span data-ttu-id="d3bfe-425">Hello 사용자 너무 연결[https://portal.azure.com](https://portal.azure.com)합니다. 보조 인증을 요청받았고 성공적으로 인증할 수 있으면 Azure MFA의 잘못된 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-425">Have hello user connect too[https://portal.azure.com](https://portal.azure.com). If they are prompted for secondary authentication and can successfully authenticate, you can eliminate an incorrect configuration of Azure MFA.</span></span>

<span data-ttu-id="d3bfe-426">Azure MFA hello 사용자에 대해 작동 하 고 hello 관련 이벤트 로그를 검토 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-426">If Azure MFA is working for hello user(s), you should review hello relevant Event logs.</span></span> <span data-ttu-id="d3bfe-427">여기에 hello 이전 섹션에서 설명 하는 hello 보안 이벤트, 운영, 게이트웨이 및 Azure MFA 로그 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-427">These include hello Security Event, Gateway operational, and Azure MFA logs that are discussed in hello previous section.</span></span> 

<span data-ttu-id="d3bfe-428">다음은 실패한 로그온 이벤트(6273 이벤트 ID)를 보여 주는 보안 로그의 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-428">Below is an example output of Security log showing a failed logon event (Event ID 6273):</span></span>

 ![보안 로그](./media/nps-extension-vpn/image47.png)

<span data-ttu-id="d3bfe-430">다음은 hello AzureMFA 로그에서 관련된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-430">Below is a related event from hello AzureMFA logs:</span></span>

 ![Azure MFA 로그](./media/nps-extension-vpn/image48.png)

<span data-ttu-id="d3bfe-432">tooperform 고급 옵션을 참조 하 여 hello NPS 데이터베이스 형식 로그 파일 hello NPS 서비스를 설치한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-432">tooperform advanced troubleshoot options, consult hello NPS database format log files where hello NPS service is installed.</span></span> <span data-ttu-id="d3bfe-433">이러한 로그 파일은 _%SystemRoot%\System32\Logs_ 폴더에 쉼표로 구분된 텍스트 파일로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-433">These log files are created in _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> <span data-ttu-id="d3bfe-434">이러한 로그 파일에 대한 자세한 내용은 [NPS 데이터베이스 형식 로그 파일 해석(영문)](https://technet.microsoft.com/library/cc771748.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-434">For a description of these log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> 

<span data-ttu-id="d3bfe-435">이러한 로그 파일 hello 항목은 스프레드시트나 데이터베이스 가져오지 않고 어려운 toointerpret입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-435">hello entries in these log files are difficult toointerpret without importing them into a spreadsheet or a database.</span></span> <span data-ttu-id="d3bfe-436">숫자를 찾을 수 있습니다 IAS 파서 온라인 tooassist의 로그 파일을 hello 해석에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-436">You can find a number of IAS parsers online tooassist you in interpreting hello log files.</span></span> <span data-ttu-id="d3bfe-437">다음은 하나의 hello 출력 같은 다운로드 가능한 [셰어웨어 응용 프로그램](http://www.deepsoftware.com/iasviewer):</span><span class="sxs-lookup"><span data-stu-id="d3bfe-437">Below is hello output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer):</span></span> 

 ![셰어웨어 응용 프로그램](./media/nps-extension-vpn/image49.png)

<span data-ttu-id="d3bfe-439">마지막으로 추가적인 문제 해결 옵션을 위해 Wireshark 또는 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)와 같은 프로토콜 분석기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-439">Finally, for additional troubleshoot options, you can use a protocol analyzer such as Wireshark or [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> <span data-ttu-id="d3bfe-440">hello Wireshark에서 다음 이미지에서는 hello VPN 서버와 NPS 서버 hello hello RADIUS 메시지</span><span class="sxs-lookup"><span data-stu-id="d3bfe-440">hello following image from Wireshark shows hello RADIUS messages between hello VPN server and hello NPS server.</span></span>

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

<span data-ttu-id="d3bfe-442">자세한 내용은 [기존 NPS 인프라를 Azure Multi-Factor Authentication과 통합](multi-factor-authentication-nps-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bfe-442">For more information, see [Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d3bfe-443">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3bfe-443">Next steps</span></span>
[<span data-ttu-id="d3bfe-444">어떻게 tooget Azure Multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d3bfe-444">How tooget Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-versions-plans.md)

[<span data-ttu-id="d3bfe-445">RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버</span><span class="sxs-lookup"><span data-stu-id="d3bfe-445">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](multi-factor-authentication-get-started-server-rdg.md)

[<span data-ttu-id="d3bfe-446">Azure Active Directory와 온-프레미스 디렉터리 통합</span><span class="sxs-lookup"><span data-stu-id="d3bfe-446">Integrate your on-premises directories with Azure Active Directory</span></span>](../active-directory/connect/active-directory-aadconnect.md)

