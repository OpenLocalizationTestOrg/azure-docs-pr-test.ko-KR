---
title: "NPS 확장을 사용하여 Azure MFA와 VPN 통합 | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure용 NPS(네트워크 정책 서버) 확장을 사용하여 VPN 인프라를 Azure MFA와 통합하는 방법을 설명합니다."
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
ms.openlocfilehash: 3dfcf25856ede50266336c2ebb057dd3f7b8897e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-the-network-policy-server-nps-extension-for-azure"></a><span data-ttu-id="440b0-104">Azure용 NPS(네트워크 정책 서버) 확장을 사용하여 Azure MFA(Multi-Factor Authentication)와 VPN 인프라 통합</span><span class="sxs-lookup"><span data-stu-id="440b0-104">Integrate your VPN infrastructure with Azure Multi-Factor Authentication (MFA) using the Network Policy Server (NPS) extension for Azure</span></span>

## <a name="overview"></a><span data-ttu-id="440b0-105">개요</span><span class="sxs-lookup"><span data-stu-id="440b0-105">Overview</span></span>

<span data-ttu-id="440b0-106">Azure용 NPS(네트워크 정책 서비스) 확장을 사용하면 조직에서 2단계 인증을 제공하는 클라우드 기반 [Azure MFA(Multi-Factor Authentication)](multi-factor-authentication-get-started-server-rdg.md)를 사용하여 RADIUS(Remote Authentication Dial-In User Service) 클라이언트 인증을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-106">The Network Policy Service (NPS) extension for Azure allows organizations to safeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using cloud-based [Azure Multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), which provides two-step verification.</span></span>

<span data-ttu-id="440b0-107">이 문서에서는 Azure용 NPS 확장을 사용하여 NPS 인프라와 Azure MFA를 통합하여 VPN을 통해 네트워크에 연결하려는 사용자에 대해 안전한 2단계 인증을 사용하도록 설정하기 위한 지침에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-107">This article provides instructions for integrating the NPS infrastructure with Azure MFA using the NPS extension for Azure to enable secure two-step verification for users attempting to connect to your network using a VPN.</span></span> 

<span data-ttu-id="440b0-108">NPS(네트워크 정책 및 액세스 서비스)는 조직에 다음과 같은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-108">The Network Policy and Access Services (NPS) gives organizations the following abilities:</span></span>

* <span data-ttu-id="440b0-109">연결할 수 있는 사용자, 연결이 허용되는 시간, 연결 기간 및 클라이언트에서 연결에 사용해야 하는 보안 수준 등을 지정하여 네트워크 요청을 관리하고 제어할 수 있는 중앙 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-109">Specify central locations for the management and control of network requests to specify who can connect, what times of day connections are allowed, the duration of connections, and the level of security that clients must use to connect, and so on.</span></span> <span data-ttu-id="440b0-110">이러한 정책은 각 VPN 또는 RD(원격 데스크톱) 게이트웨이 서버에 지정하는 대신 중앙 위치에 한 번만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-110">Rather than specify these policies on each VPN or Remote Desktop (RD) Gateway server, these policies can be specified once in a central location.</span></span> <span data-ttu-id="440b0-111">RADIUS 프로토콜은 중앙 집중식 AAA(인증, 권한 부여 및 계정 관리)를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-111">The RADIUS protocol is used to provide the centralized Authentication, Authorization, and Accounting (AAA).</span></span> 
* <span data-ttu-id="440b0-112">장치가 허용되거나 제한되지 않는지 또는 네트워크 리소스에 대한 액세스가 제한되는지 여부를 결정하는 NAP(네트워크 액세스 보호) 클라이언트 상태 정책을 설정하고 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-112">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access to network resources.</span></span>
* <span data-ttu-id="440b0-113">802.1x 지원 무선 액세스 지점 및 이더넷 스위치에 액세스하기 위한 인증 및 권한 부여를 적용할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-113">Provide a means to enforce authentication and authorization for access to 802.1x-capable wireless access points and Ethernet switches.</span></span>    

<span data-ttu-id="440b0-114">자세한 내용은 [NPS(네트워크 정책 서버)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-114">For more information, see [Network Policy Server (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top).</span></span> 

<span data-ttu-id="440b0-115">보안을 강화하고 높은 수준의 규정 준수를 제공하기 위해 조직에서는 NPS를 Azure MFA와 통합하여 사용자가 2단계 인증을 통해 VPN 서버의 가상 포트에 연결할 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-115">To enhance security and provide high level of compliance, organizations can integrate NPS with Azure MFA to ensure that users use two-step verification to be able connect to the virtual port on the VPN server.</span></span> <span data-ttu-id="440b0-116">사용자가 액세스 권한을 부여받으려면 자신이 제어할 수 있는 정보와 함께 사용자 이름/암호 조합을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-116">For users to be granted access, they must provide their username/password combination with information that the user has in their control.</span></span> <span data-ttu-id="440b0-117">이 정보는 신뢰할 수 있어야 하며, 휴대폰 번호, 유선 전화 번호, 모바일 장치 등과 같이 쉽게 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-117">This information must be trusted and not easily duplicated, such as a cell phone number, landline number, application on a mobile device, and so on.</span></span>

<span data-ttu-id="440b0-118">Azure용 NPS 확장을 사용하기 전에 통합된 NPS 및 Azure MFA 환경에 대한 2단계 인증을 구현하려는 고객은 "RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버"에서 설명한 대로 온-프레미스 환경에서 별도의 MFA 서버를 구성하고 유지 관리해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-118">Prior to the availability of the NPS extension for Azure, customers who wished to implement two-step verification for integrated NPS and Azure MFA environments had to configure and maintain a separate MFA Server in the on-premises environment as documented in Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS.</span></span>

<span data-ttu-id="440b0-119">이제 조직에서는 Azure용 NPS 확장을 통해 온-프레미스 MFA 솔루션 또는 클라우드 기반 MFA 솔루션을 배포하여 RADIUS 클라이언트 인증을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-119">The availability of the NPS extension for Azure now gives organizations the choice to deploy either an on-premises based MFA solution or a cloud-based MFA solution to secure RADIUS client authentication.</span></span>
 
## <a name="authentication-flow"></a><span data-ttu-id="440b0-120">인증 흐름</span><span class="sxs-lookup"><span data-stu-id="440b0-120">Authentication Flow</span></span>
<span data-ttu-id="440b0-121">사용자가 VPN 서버의 가상 포트에 연결하면 사용자 이름/암호와 인증서 기반 인증 방법을 조합하여 사용할 수 있는 다양한 프로토콜로 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-121">When a user connects to a virtual port on a VPN server, they must first authenticate using a variety of protocols, which allow the use of a combination of user name/password and certificate-based authentication methods.</span></span> 

<span data-ttu-id="440b0-122">ID 인증 및 확인 외에도 사용자는 적절한 전화 접속 권한을 가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-122">In addition to authenticating and verifying identity, users must have the appropriate dial-in permissions.</span></span> <span data-ttu-id="440b0-123">간단한 구현에서 액세스를 허용하는 이러한 전화 접속 권한은 Active Directory 사용자 개체에 직접 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-123">In simple implementations, these dial-in permissions that allow access are set directly on the Active Directory user objects.</span></span> 

 ![사용자 속성](./media/nps-extension-vpn/image1.png)

<span data-ttu-id="440b0-125">간단한 구현을 위해 각 VPN 서버에서 각 로컬 VPN 서버에 정의된 정책에 따라 액세스를 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-125">For simple implementations, each VPN server grants or denies access based on policies defined on each local VPN server.</span></span>

<span data-ttu-id="440b0-126">더 크고 확장성 있는 구현에서는 VPN 액세스를 허용하거나 거부하는 정책이 RADIUS 서버에 중앙 집중화됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-126">In larger and more scalable implementations, the polices that grant or deny VPN access are centralized on RADIUS servers.</span></span> <span data-ttu-id="440b0-127">이 경우 VPN 서버는 연결 요청 및 계정 메시지를 RADIUS 서버로 전달하는 액세스 서버(RADIUS 클라이언트) 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-127">In this case, the VPN server acts as an access server (RADIUS client) that forwards connection requests and account messages to a RADIUS server.</span></span> <span data-ttu-id="440b0-128">VPN 서버의 가상 포트에 연결하려면 사용자를 인증하고 RADIUS 서버에서 중앙 집중식으로 정의된 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-128">To connect to the virtual port on the VPN server, users must be authenticated and meet the conditions defined centrally on RADIUS servers.</span></span> 

<span data-ttu-id="440b0-129">Azure용 NPS 확장을 NPS와 통합한 경우 성공적인 인증 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-129">When the NPS extension for Azure is integrated with the NPS, the successful authentication flow is as follows:</span></span>

1. <span data-ttu-id="440b0-130">VPN 서버에서 원격 데스크톱 세션과 같은 리소스에 연결하기 위해 VPN 사용자로부터 사용자 이름과 암호가 포함된 인증 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-130">The VPN server receives an authentication request from a VPN user that includes the username and password to connect to a resource, such as a Remote Desktop session.</span></span> 
2. <span data-ttu-id="440b0-131">RADIUS 클라이언트 역할을 하는 VPN 서버에서 해당 요청을 RADIUS 액세스 요청 메시지로 변환하고 NPS 확장이 설치된 RADIUS(NPS) 서버로 메시지(암호가 암호화 됨)를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-131">Acting as a RADIUS client, VPN server converts the request to a RADIUS Access-Request message and sends the message (password is encrypted) to the RADIUS (NPS) server where the NPS extension is installed.</span></span> 
3. <span data-ttu-id="440b0-132">Active Directory에서 사용자 이름과 암호 조합이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-132">The username and password combination is verified in Active Directory.</span></span> <span data-ttu-id="440b0-133">사용자 이름/암호가 올바르지 않으면 RADIUS 서버에서 액세스 거부 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-133">If the username / password is incorrect, the RADIUS Server sends an Access-Reject message.</span></span> 
4. <span data-ttu-id="440b0-134">NPS 연결 요청 및 네트워크 정책에 지정된 모든 조건(예: 시간 또는 그룹 멤버 자격 제한)이 충족되는 경우 NPS 확장에서 Azure MFA를 통한 보조 인증 요청을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-134">If all conditions as specified in the NPS Connection Request and Network Policies are met (for example, time of day or group membership restrictions), the NPS extension triggers a request for secondary authentication with Azure MFA.</span></span> 
5. <span data-ttu-id="440b0-135">Azure MFA에서 Azure Active Directory와 통신하여 사용자의 세부 정보를 검색하고 사용자가 구성한 방법(문자 메시지, 모바일 앱 등)을 사용하여 보조 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-135">Azure MFA communicates with Azure Active Directory, retrieves the user’s details, and performs the secondary authentication using the method configured by the user (text message, mobile app, and so on).</span></span> 
6. <span data-ttu-id="440b0-136">MFA 챌린지가 성공하면 Azure MFA에서 결과를 NPS 확장으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-136">Upon success of the MFA challenge, Azure MFA communicates the result to the NPS extension.</span></span>
7. <span data-ttu-id="440b0-137">연결 시도가 인증되고 권한이 부여된 후에 확장이 설치된 NPS 서버에서 RADIUS 액세스 허용 메시지를 VPN 서버(RADIUS 클라이언트)로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-137">After the connection attempt is both authenticated and authorized, the NPS server where the extension is installed sends a RADIUS Access-Accept message to the VPN server (RADIUS client).</span></span>
8. <span data-ttu-id="440b0-138">사용자가 VPN 서버의 가상 포트에 대한 액세스 권한을 부여받고 암호화된 VPN 터널을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-138">The user is granted access to the virtual port on VPN server and establishes an encrypted VPN tunnel.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="440b0-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="440b0-139">Prerequisites</span></span>
<span data-ttu-id="440b0-140">이 섹션에서는 Azure MFA와 원격 데스크톱 게이트웨이를 통합하기 전에 필요한 전제 조건에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-140">This section details the prerequisites necessary before integrating Azure MFA with the Remote Desktop Gateway.</span></span> <span data-ttu-id="440b0-141">이 문서를 시작하기 전에 다음과 같은 필수 구성 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-141">Before you begin, you must have the following prerequisites in place.</span></span>

* <span data-ttu-id="440b0-142">VPN 인프라</span><span class="sxs-lookup"><span data-stu-id="440b0-142">VPN infrastructure</span></span>
* <span data-ttu-id="440b0-143">NPS(네트워크 정책 및 액세스 서비스) 역할</span><span class="sxs-lookup"><span data-stu-id="440b0-143">Network Policy and Access Services (NPS) role</span></span>
* <span data-ttu-id="440b0-144">Azure MFA 라이선스</span><span class="sxs-lookup"><span data-stu-id="440b0-144">Azure MFA License</span></span>
* <span data-ttu-id="440b0-145">Windows Server 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="440b0-145">Windows Server software</span></span>
* <span data-ttu-id="440b0-146">라이브러리</span><span class="sxs-lookup"><span data-stu-id="440b0-146">Libraries</span></span>
* <span data-ttu-id="440b0-147">온-프레미스 AD와 동기화되는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="440b0-147">Azure AD synched with on-premises AD</span></span> 
* <span data-ttu-id="440b0-148">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="440b0-148">Azure Active Directory GUID ID</span></span>

### <a name="vpn-infrastructure"></a><span data-ttu-id="440b0-149">VPN 인프라</span><span class="sxs-lookup"><span data-stu-id="440b0-149">VPN infrastructure</span></span>
<span data-ttu-id="440b0-150">이 문서에서는 Microsoft Windows Server 2016을 사용하여 작동 중인 VPN 인프라가 있으며 VPN 서버가 현재 연결 요청을 RADIUS 서버로 전달하도록 구성되지 않았다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-150">This article assumes that you have a working VPN infrastructure using Microsoft Windows Server 2016 in place and that the VPN server is currently not configured to forward connection requests to a RADIUS server.</span></span> <span data-ttu-id="440b0-151">이 가이드에서는 중앙 RADIUS 서버를 사용하도록 VPN 인프라를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-151">You will configure the VPN infrastructure to use a central RADIUS server in this guide.</span></span>

<span data-ttu-id="440b0-152">작동 중인 인프라가 없는 경우 Microsoft 및 타사 사이트에서 찾을 수 있는 다양한 VPN 설정 자습서에서 제공하는 지침에 따라 이 인프라를 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-152">If you do not have a working infrastructure in place, you can quickly create this infrastructure by following the guidance provided in numerous VPN setup tutorials you can find on the Microsoft and third-party sites.</span></span> 

### <a name="network-policy-and-access-services-nps-role"></a><span data-ttu-id="440b0-153">NPS(네트워크 정책 및 액세스 서비스) 역할</span><span class="sxs-lookup"><span data-stu-id="440b0-153">Network Policy and Access Services (NPS) role</span></span>

<span data-ttu-id="440b0-154">NPS 역할 서비스는 RADIUS 서버 및 클라이언트 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-154">The NPS role service provides the RADIUS server and client functionality.</span></span> <span data-ttu-id="440b0-155">이 문서에서는 사용자 환경의 구성원 서버 또는 도메인 컨트롤러에 NPS 역할을 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-155">This article assumes you have installed the NPS role on a member server or domain controller in your environment.</span></span> <span data-ttu-id="440b0-156">이 가이드에서는 VPN 구성을 위해 RADIUS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-156">You will configure RADIUS for a VPN configuration in this guide.</span></span> <span data-ttu-id="440b0-157">VPN 서버가 아닌 _다른_ 서버에 NPS 역할을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-157">Install the NPS role on a server _other_ than your VPN server.</span></span>

<span data-ttu-id="440b0-158">NPS 역할 서비스 Windows Server 2012 이상 설치에 대한 자세한 내용은 [NAP 상태 정책 서버 설치(영문)](https://technet.microsoft.com/library/dd296890.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-158">For information on installing the NPS role service Windows Server 2012 or higher, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="440b0-159">Windows Server 2016에서는 NAP(네트워크 액세스 정책)가 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-159">Network Access Policy (NAP) is deprecated in Windows Server 2016.</span></span> <span data-ttu-id="440b0-160">도메인 컨트롤러에 NPS를 설치하기 위한 권장 사항을 포함하여 NPS에 대한 모범 사례에 대한 자세한 내용은 [NPS 모범 사례(영문)](https://technet.microsoft.com/library/cc771746)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-160">For a description of best practices for NPS, including the recommendation to install NPS on a domain controller, see [Best Practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="licenses"></a><span data-ttu-id="440b0-161">라이선스</span><span class="sxs-lookup"><span data-stu-id="440b0-161">Licenses</span></span>

<span data-ttu-id="440b0-162">Azure AD Premium, EMS(Enterprise Mobility plus Security) 또는 MFA 구독을 통해 사용할 수 있는 Azure MFA에 대한 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-162">Required is a license for Azure MFA, which is available through an Azure AD Premium, Enterprise Mobility plus Security (EMS), or an MFA subscription.</span></span> <span data-ttu-id="440b0-163">자세한 내용은 [Azure Multi-Factor Authentication 획득 방법](multi-factor-authentication-versions-plans.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-163">For more information, see [How to get Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span></span> <span data-ttu-id="440b0-164">테스트를 위해 평가판 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-164">For testing purposes, you can use a trial subscription.</span></span>

### <a name="software"></a><span data-ttu-id="440b0-165">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="440b0-165">Software</span></span>

<span data-ttu-id="440b0-166">NPS 확장을 사용하려면 NPS 역할 서비스가 설치된 Windows Server 2008 R2 SP1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-166">The NPS extension requires Windows Server 2008 R2 SP1 or above with the NPS role service installed.</span></span> <span data-ttu-id="440b0-167">이 가이드의 모든 단계는 Windows Server 2016을 사용하여 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-167">All the steps in this guide were performed using Windows Server 2016.</span></span>

### <a name="libraries"></a><span data-ttu-id="440b0-168">라이브러리</span><span class="sxs-lookup"><span data-stu-id="440b0-168">Libraries</span></span>

<span data-ttu-id="440b0-169">다음 두 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-169">The following two libraries are required:</span></span>

* [<span data-ttu-id="440b0-170">Visual Studio 2013(X64)용 Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="440b0-170">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
* <span data-ttu-id="440b0-171">_Windows PowerShell용 Microsoft Azure Active Directory 모듈 버전 1.1.166.0_ 이상</span><span class="sxs-lookup"><span data-stu-id="440b0-171">_Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0_ or higher.</span></span> <span data-ttu-id="440b0-172">최신 릴리스 및 설치 지침은 [Microsoft Azure Active Directory PowerShell 모듈 버전 릴리스 기록](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-172">For the latest release and installation instructions, see [Microsoft Azure Active Directory PowerShell Module Version Release History](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).</span></span>

<span data-ttu-id="440b0-173">이러한 라이브러리는 달리 명시하지 않은 기존 설명서에도 불구하고 NPS 확장 설치 파일(버전 0.9.1.2)과 함께 패키지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-173">These libraries are not packaged with the NPS extension setup files (version 0.9.1.2), despite existing documentation that states otherwise.</span></span> <span data-ttu-id="440b0-174">적어도 Visual Studio 2013용 Visual C++ 재배포 가능 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-174">At a minimum, you must install the Visual C++ Redistributable Packages for Visual Studio 2013.</span></span> <span data-ttu-id="440b0-175">Windows PowerShell용 Microsoft Azure Active Directory 모듈은 아직 설치되지 않은 경우 설치 프로세스의 일부로 실행되는 구성 스크립트를 통해 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-175">The Microsoft Azure Active Directory Module for Windows PowerShell is installed, if it is not already present, through a configuration script you run as part of the setup process.</span></span> <span data-ttu-id="440b0-176">이 모듈은 아직 설치하지 않은 상태에서 미리 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-176">There is no need to install this module ahead of time if it is not already installed.</span></span>

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a><span data-ttu-id="440b0-177">온-프레미스 Active Directory와 동기화되는 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="440b0-177">Azure Active Directory synched with on-premises Active Directory</span></span> 

<span data-ttu-id="440b0-178">NPS 확장을 사용하려면 온-프레미스 사용자가 Azure Active Directory와 동기화되고 Multi-Factor Authentication을 사용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-178">To use the NPS extension, on-premises users must be synced with Azure Active Directory and enabled for Multi-Factor Authentication.</span></span> <span data-ttu-id="440b0-179">이 가이드에서는 온-프레미스 사용자가 AD Connect를 사용하여 Azure Active Directory와 동기화된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-179">This guide assumes that on-premises users are synched with Azure Active Directory using AD Connect.</span></span> <span data-ttu-id="440b0-180">사용자가 MFA를 사용하도록 설정하기 위한 지침은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-180">Instructions for enabling users for MFA are provided below.</span></span>
<span data-ttu-id="440b0-181">Azure AD 연결에 대한 자세한 내용은 [Azure Active Directory와 온-프레미스 디렉터리 통합](../active-directory/connect/active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-181">For information on Azure AD connect, see [Integrate your on-premises directories with Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="440b0-182">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="440b0-182">Azure Active Directory GUID ID</span></span> 
<span data-ttu-id="440b0-183">NPS를 설치하려면 Azure Active Directory의 GUID를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-183">To install the NPS, you need to know the GUID of the Azure Active Directory.</span></span> <span data-ttu-id="440b0-184">Azure Active Directory의 GUID를 찾기 위한 지침은 다음 섹션에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-184">Instructions for finding the GUID of the Azure Active Directory are provided in the next section.</span></span>

## <a name="configure-radius-for-vpn-connections"></a><span data-ttu-id="440b0-185">VPN 연결을 위한 RADIUS 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-185">Configure RADIUS for VPN connections</span></span>

<span data-ttu-id="440b0-186">구성원 서버에 NPS 서버 역할을 설치한 경우 VPN 연결을 요청하는 VPN 클라이언트를 인증하고 권한을 부여하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-186">If you have installed the NPS server role on a member server, you need to configure to authenticate and authorize VPN client that request VPN connections.</span></span> 

<span data-ttu-id="440b0-187">이 섹션에서는 네트워크 정책 서버 역할을 설치했지만 인프라에서 사용할 수 있도록 구성하지 않았다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-187">This section assumes that you have installed the Network Policy Server role but have not configured it for use in your infrastructure.</span></span>

>[!NOTE]
><span data-ttu-id="440b0-188">인증을 위해 중앙 집중식 RADIUS 서버를 통해 작동하는 VPN 서버가 이미 있는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-188">If you already have a working VPN server that uses a centralized RADIUS server for authentication, you can skip this section.</span></span>
>

### <a name="register-server-in-active-directory"></a><span data-ttu-id="440b0-189">Active Directory에 서버 등록</span><span class="sxs-lookup"><span data-stu-id="440b0-189">Register Server in Active Directory</span></span>
<span data-ttu-id="440b0-190">이 시나리오에서 제대로 작동하려면 NPS 서버를 Active Directory에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-190">To function properly in this scenario, the NPS server needs to be registered in Active Directory.</span></span>

1. <span data-ttu-id="440b0-191">[서버 관리자]를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-191">Open Server Manager.</span></span>
2. <span data-ttu-id="440b0-192">[서버 관리자]에서 **도구**를 클릭한 다음 **네트워크 정책 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-192">In Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
3. <span data-ttu-id="440b0-193">[네트워크 정책 서버] 콘솔에서 **NPS(로컬)**를 마우스 오른쪽 단추로 클릭한 다음 **Active Directory에 서버 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-193">In the Network Policy Server console, right-click **NPS (Local)**, and then click **Register server in Active Directory**.</span></span> <span data-ttu-id="440b0-194">**확인**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-194">Click **OK** two times.</span></span>

 ![네트워크 정책 서버](./media/nps-extension-vpn/image2.png)

4. <span data-ttu-id="440b0-196">다음 절차를 위해 콘솔을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-196">Leave the console open for the next procedure.</span></span>

### <a name="use-wizard-to-configure-radius-server"></a><span data-ttu-id="440b0-197">마법사를 사용하여 RADIUS 서버 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-197">Use wizard to configure RADIUS server</span></span>
<span data-ttu-id="440b0-198">표준(마법사 기반) 또는 고급 구성 옵션을 사용하여 RADIUS 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-198">You can use a standard (wizard-based) or advanced configuration option to configure the RADIUS server.</span></span> <span data-ttu-id="440b0-199">이 섹션에서는 마법사 기반 표준 구성 옵션을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-199">This section assumes the use of the wizard-based standard configuration option.</span></span>

1. <span data-ttu-id="440b0-200">[네트워크 정책 서버] 콘솔에서 **NPS(로컬)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-200">In the Network Policy Server console, click **NPS (Local)**.</span></span>
2. <span data-ttu-id="440b0-201">[표준 구성] 아래에서 **전화 접속 또는 VPN 연결을 위한 RADIUS 서버**를 선택한 다음 **VPN 또는 전화 접속 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-201">Under Standard Configuration, select **RADIUS Server for Dial-Up or VPN Connections**, and then click **Configure VPN or Dial-Up**.</span></span>

 ![VPN 구성](./media/nps-extension-vpn/image3.png)

3. <span data-ttu-id="440b0-203">[전화 접속 또는 가상 사설망 연결 형식 선택] 페이지에서 **가상 사설망 연결**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-203">On the Select Dial-up or Virtual Private Network Connections Type page, select **Virtual Private Network Connections**, and click **Next**.</span></span>

 ![가상 사설망](./media/nps-extension-vpn/image4.png)

4. <span data-ttu-id="440b0-205">[전화 접속 또는 VPN 서버 지정] 페이지에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-205">On the Specify Dial-Up or VPN Server page, click **Add**.</span></span>
5. <span data-ttu-id="440b0-206">**새 RADIUS 클라이언트** 대화 상자에서 친숙한 이름을 제공하고, VPN 서버의 확인할 수 있는 이름 또는 IP 주소를 입력한 다음, 공유 비밀 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-206">In the **New RADIUS client** dialog box, provide a friendly name, enter the resolvable name or IP address of the VPN server, and enter a shared secret password.</span></span> <span data-ttu-id="440b0-207">이 공유 비밀 암호는 길고 복잡하게 만들고,</span><span class="sxs-lookup"><span data-stu-id="440b0-207">Make this shared secret password long and complex.</span></span> <span data-ttu-id="440b0-208">다음 섹션의 단계에 필요하므로 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-208">Record this password, as you need it for steps in the next section.</span></span>

 ![새 RADIUS 클라이언트](./media/nps-extension-vpn/image5.png)

6. <span data-ttu-id="440b0-210">**확인**을 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-210">Click **OK**, and then **Next**.</span></span>
7. <span data-ttu-id="440b0-211">**인증 방법 구성** 페이지에서 기본 선택 사항(Microsoft 암호화 인증 버전 2(MS-CHAPv2))을 그대로 적용하거나 다른 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-211">On the **Configure Authentication Methods** page, accept the default selection (Microsoft Encrypted Authentication version 2 (MS-CHAPv2) or choose another option, and click **Next**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="440b0-212">EAP(확장할 수 있는 인증 프로토콜)를 구성하는 경우 MS CHAPv2 또는 PEAP를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-212">If you configure Extensible Authentication Protocol (EAP), you must use either MS CHAPv2 or PEAP.</span></span> <span data-ttu-id="440b0-213">다른 EAP는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-213">No other EAP is supported.</span></span>
 
8. <span data-ttu-id="440b0-214">[사용자 그룹 지정] 페이지에서 **추가**를 클릭하고 해당 그룹(있는 경우)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-214">On the Specify User Groups page, click **Add** and select an appropriate group, if one exists.</span></span> <span data-ttu-id="440b0-215">그렇지 않으면 선택 사항을 비워 두어 모든 사용자에게 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-215">Otherwise, leave the selection blank to grant access to all users.</span></span>

 ![사용자 그룹 지정](./media/nps-extension-vpn/image7.png)

9. <span data-ttu-id="440b0-217">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-217">Click **Next**.</span></span>
10. <span data-ttu-id="440b0-218">[IP 필터 지정] 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-218">On the Specify IP Filters page, click **Next**.</span></span>
11. <span data-ttu-id="440b0-219">[암호화 설정 지정] 페이지에서 기본 설정을 적용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-219">On the Specify Encryption Settings page, accept the default settings, and click **Next**.</span></span>

 ![암호화 지정](./media/nps-extension-vpn/image8.png)

12. <span data-ttu-id="440b0-221">[영역 이름 지정]에서 이름을 비워 두고, 기본 설정을 적용하고, **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-221">On the Specify a Realm Name, leave the name blank, accept the default setting, and click **Next**.</span></span>

 ![영역 이름 지정](./media/nps-extension-vpn/image9.png)

13. <span data-ttu-id="440b0-223">[새 전화 접속 또는 가상 사설망 연결 및 RADIUS 클라이언트 완료] 페이지에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-223">On the Completing New Dial-up or Virtual Private Network Connections and RADIUS clients page, click **Finish**.</span></span>

 ![연결 완료](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a><span data-ttu-id="440b0-225">RADIUS 구성 확인</span><span class="sxs-lookup"><span data-stu-id="440b0-225">Verify RADIUS configuration</span></span>
<span data-ttu-id="440b0-226">이 섹션에서는 마법사를 사용하여 만든 구성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-226">This section details the configuration you created using the wizard.</span></span>

1. <span data-ttu-id="440b0-227">NPS 서버의 [NPS(로컬)] 콘솔에서 RADIUS 클라이언트를 펼치고 **RADIUS 클라이언트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-227">On the NPS server, in the NPS (Local) console, expand RADIUS Clients, and select **RADIUS Clients**.</span></span>
2. <span data-ttu-id="440b0-228">세부 정보 창에서 마법사를 사용하여 만든 RADIUS 클라이언트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-228">In the details pane, right-click the RADIUS client you created using wizard, and click **Properties**.</span></span> <span data-ttu-id="440b0-229">RADIUS 클라이언트(VPN 서버)에 대한 속성은 아래와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-229">The properties for your RADIUS client (the VPN server) should be similar to those shown below.</span></span>

 ![VPN 속성](./media/nps-extension-vpn/image11.png)

3. <span data-ttu-id="440b0-231">**취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-231">Click **Cancel**.</span></span>
4. <span data-ttu-id="440b0-232">NPS 서버의 [NPS(로컬)] 콘솔에서 **정책**을 펼치고 **연결 요청 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-232">On the NPS server, in the NPS (Local) console, expand **Policies**, and select **Connection Request Policies**.</span></span> <span data-ttu-id="440b0-233">아래 이미지와 비슷한 VPN 연결 정책이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-233">You should see the VPN Connections policy that resembles the image below.</span></span>

 ![연결 요청](./media/nps-extension-vpn/image12.png)

5. <span data-ttu-id="440b0-235">[정책] 아래에서 **네트워크 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-235">Under Policies, select **Network Policies**.</span></span> <span data-ttu-id="440b0-236">아래 이미지와 비슷한 VPN(가상 사설망) 연결 정책이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-236">You should a Virtual Private Network (VPN) Connections policy that resembles the image below.</span></span>

 ![네트워크 속성](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-to-use-radius-authentication"></a><span data-ttu-id="440b0-238">RADIUS 인증을 사용하도록 VPN 서버 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-238">Configure VPN Server to use RADIUS authentication</span></span>
<span data-ttu-id="440b0-239">이 섹션에서는 VPN 서버에서 RADIUS 인증을 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-239">In this section, you configure the VPN server to use RADIUS authentication.</span></span> <span data-ttu-id="440b0-240">이 섹션에서는 VPN 서버의 작동 구성이 있지만 RADIUS 인증을 사용하도록 VPN 서버를 구성하지 않았다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-240">This section assumes that you have a working configuration of VPN server but have not configured the VPN server to use RADIUS authentication.</span></span> <span data-ttu-id="440b0-241">VPN 서버를 구성한 후에 구성이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-241">After configuring the VPN server, you confirm that your configuration is working as expected.</span></span>

>[!NOTE]
><span data-ttu-id="440b0-242">RADIUS 인증을 통해 작동하는 VPN 서버 구성이 이미 있는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-242">If you already have a working VPN server configuration that uses RADIUS authentication, you can skip this section.</span></span>
>

### <a name="configure-authentication-provider"></a><span data-ttu-id="440b0-243">인증 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-243">Configure authentication provider</span></span>
1. <span data-ttu-id="440b0-244">VPN 서버에서 [서버 관리자]를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-244">On the VPN server, open Server Manager.</span></span>
2. <span data-ttu-id="440b0-245">[서버 관리자]에서 **도구**, **라우팅 및 원격 액세스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-245">In Server Manager, click **Tools**, and then **Routing and Remote Access**.</span></span>
3. <span data-ttu-id="440b0-246">[라우팅 및 원격 액세스] 콘솔에서 **\[서버 이름\](로컬)**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-246">In the Routing and Remote Access console, right-click **\[Server Name\] (local)**, and then click **Properties**.</span></span>

 ![라우팅 및 원격 액세스](./media/nps-extension-vpn/image14.png)
 
4. <span data-ttu-id="440b0-248">**[서버 이름} (로컬) 속성** 대화 상자에서 **보안** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-248">In the **[Server Name} (local) Properties** dialog box, click the **Security** tab.</span></span> 
5. <span data-ttu-id="440b0-249">**보안** 탭의 [인증 공급자] 아래에서 **RADIUS 인증**, **구성**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-249">On the **Security** tab, under Authentication provider, click **RADIUS Authentication**, and then **Configure**.</span></span>

 ![RADIUS 인증](./media/nps-extension-vpn/image15.png)
 
6. <span data-ttu-id="440b0-251">[RADIUS 인증] 대화 상자에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-251">In the RADIUS Authentication dialog box, click **Add**.</span></span>
7. <span data-ttu-id="440b0-252">[RADIUS 서버 추가]의 [서버 이름]에서 이전 섹션에서 구성한 RADIUS 서버의 이름 또는 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-252">In the Add RADIUS Server, in Server name, add the name or the IP address of the RADIUS server you configured in the previous section.</span></span>
8. <span data-ttu-id="440b0-253">[공유 비밀]에서 **변경**을 클릭하고 이전에 만들어 기록해 둔 공유 비밀 암호를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-253">In Shared secret, click **Change** and add the shared secret password you created and recorded earlier.</span></span>
9. <span data-ttu-id="440b0-254">[시간 제한(초])에서 값을 **30**에서 **60** 사이의 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-254">In Time-out (seconds), change the value to a value between **30** and **60**.</span></span> <span data-ttu-id="440b0-255">이는 두 번째 인증 요소를 완료할 수 있을 만큼 충분한 시간을 허용하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-255">This is necessary to allow enough time to complete the second authentication factor.</span></span>
 
 ![RADIUS 서버 추가](./media/nps-extension-vpn/image16.png)
 
10. <span data-ttu-id="440b0-257">모든 대화 상자를 닫을 때까지 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-257">Click **OK** until you complete closing all dialog boxes.</span></span>

### <a name="test-vpn-connectivity"></a><span data-ttu-id="440b0-258">VPN 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="440b0-258">Test VPN connectivity</span></span>
<span data-ttu-id="440b0-259">이 섹션에서는 VPN 가상 포트에 연결하려고 할 때 VPN 클라이언트가 RADIUS 서버에서 인증되고 권한을 부여받았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-259">In this section, you confirm that the VPN client is authenticated and authorized by the RADIUS server when you attempt to connect to VPN virtual port.</span></span> <span data-ttu-id="440b0-260">여기서는 Windows 10을 VPN 클라이언트로 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-260">This section assumes you are using Windows 10 as a VPN client.</span></span> 

>[!NOTE]
><span data-ttu-id="440b0-261">이미 VPN 서버에 연결하도록 VPN 클라이언트를 구성하고 해당 설정을 저장한 경우 VPN 연결 개체의 구성 및 저장과 관련된 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-261">If you already configured a VPN client to connect to the VPN server and have saved the settings, you can skip the steps related to configuring and saving a VPN connection object.</span></span>
>

1. <span data-ttu-id="440b0-262">VPN 클라이언트 컴퓨터에서 **시작**을 클릭한 다음 **설정**(기어 아이콘)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-262">On your VPN client computer, click **Start**, and then **Settings** (gear icon).</span></span>
2. <span data-ttu-id="440b0-263">[창 설정]에서 **네트워크 및 인터넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-263">In Window Settings, click **Network & Internet**.</span></span>
3. <span data-ttu-id="440b0-264">**VPN**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-264">Click **VPN**.</span></span>
4. <span data-ttu-id="440b0-265">**VPN 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-265">Click **Add a VPN connection**.</span></span>
5. <span data-ttu-id="440b0-266">[VPN 연결 추가]에서 VPN 공급자로 Windows(기본 제공)를 지정한 다음 나머지 필드를 적절히 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-266">In Add a VPN connection, specify Windows (built-in) as the VPN provider, then complete the remaining fields, as appropriate, and click **Save**.</span></span> 

 ![VPN 연결 추가](./media/nps-extension-vpn/image17.png)
 
6. <span data-ttu-id="440b0-268">[제어판]에서 **네트워크 및 공유 센터**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-268">Open the **Network and Sharing Center** in Control Panel.</span></span>
7. <span data-ttu-id="440b0-269">**어댑터 설정 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-269">Click **Change adapter settings**.</span></span>

 ![어댑터 설정 변경](./media/nps-extension-vpn/image18.png)

8. <span data-ttu-id="440b0-271">VPN 네트워크 연결을 마우스 오른쪽 단추로 클릭하고 [속성]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-271">Right-click the VPN network connection, and click Properties.</span></span> 

 ![VPN 네트워크 속성](./media/nps-extension-vpn/image19.png)

9. <span data-ttu-id="440b0-273">VPN 속성 대화 상자에서 **보안** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-273">In the VPN properties dialog box, click the **Security** tab.</span></span> 
10. <span data-ttu-id="440b0-274">[보안] 탭에서 **Microsoft CHAP 버전 2(MS-CHAP v2)**만 선택했는지 확인하고 [확인]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-274">On the Security tab, ensure that only **Microsoft CHAP Version 2 (MS-CHAP v2)** is selected, and click OK.</span></span>

 ![프로토콜 허용](./media/nps-extension-vpn/image20.png)

11. <span data-ttu-id="440b0-276">VPN 연결을 마우스 오른쪽 단추로 클릭하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-276">Right-click the VPN connection, and click **Connect**.</span></span>
12. <span data-ttu-id="440b0-277">[설정] 페이지에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-277">On the Settings page, click **Connect**.</span></span>

<span data-ttu-id="440b0-278">성공적인 연결은 아래와 같이 RADIUS 서버의 보안 로그에 6272 이벤트 ID로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-278">A successful connection appears in the Security log on the RADIUS server as Event ID 6272, as shown below.</span></span>

 ![이벤트 속성](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="440b0-280">문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="440b0-280">Troubleshoot Guide</span></span>
<span data-ttu-id="440b0-281">인증 및 권한 부여를 위해 중앙 집중식 RADIUS 서버를 사용하도록 VPN 서버를 구성하기 전에 VPN 구성이 작동하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-281">Assume that your VPN configuration was working before you configured the VPN server to use a centralized RADIUS server for authentication and authorization.</span></span> <span data-ttu-id="440b0-282">이 경우 RADIUS 서버의 잘못된 구성 또는 잘못된 사용자 이름 또는 암호의 사용으로 인해 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-282">In this case, it is likely that the issue may be caused by a misconfiguration of the RADIUS Server or the use of an invalid username or password.</span></span> <span data-ttu-id="440b0-283">예를 들어 사용자 이름에 대체 UPN 접미사를 사용하면 로그인 시도가 실패할 수 있습니다(최상의 결과를 얻으려면 동일한 계정 이름을 사용해야 함).</span><span class="sxs-lookup"><span data-stu-id="440b0-283">For example, if you use the alternate UPN suffix in the username, the login attempt might fail (you should use the same Account name for best results).</span></span> 

<span data-ttu-id="440b0-284">이러한 문제를 해결하려면 RADIUS 서버에서 보안 이벤트 로그를 검사하는 것이 가장 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-284">To troubleshoot these issues, an ideal place to start is to examine the Security event logs on the RADIUS server.</span></span> <span data-ttu-id="440b0-285">이벤트 검색 시간을 줄이기 위해 아래와 같이 이벤트 뷰어에서 역할 기반 네트워크 정책 및 액세스 서버 사용자 지정 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-285">To save time searching for events, you can use the role-based Network Policy and Access Server custom view in Event Viewer, as show below.</span></span> <span data-ttu-id="440b0-286">6273 이벤트 ID는 네트워크 정책 서버에서 사용자에 대한 액세스를 거부한 이벤트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-286">Event ID 6273 indicates events where the Network Policy Server denied access to a user.</span></span> 

 ![이벤트 뷰어](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="440b0-288">Multi-Factor Authentication 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-288">Configure Multi-Factor Authentication</span></span>
<span data-ttu-id="440b0-289">이 섹션에서는 사용자가 MFA를 사용하도록 설정하고 2단계 인증에 대한 계정을 설정하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-289">This section provides instructions for enabling users for MFA and for setting up accounts for two-step verification.</span></span> 

### <a name="enable-multi-factor-authentication"></a><span data-ttu-id="440b0-290">다단계 인증 사용</span><span class="sxs-lookup"><span data-stu-id="440b0-290">Enable multi-factor authentication</span></span>
<span data-ttu-id="440b0-291">이 섹션에서는 Azure AD 계정에서 MFA를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-291">In this section, you enable Azure AD accounts for MFA.</span></span> <span data-ttu-id="440b0-292">**클래식 포털**을 사용하여 사용자가 MFA를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-292">Use the **classic portal** to enable users for MFA.</span></span> 

1. <span data-ttu-id="440b0-293">브라우저를 열고 [https://manage.windowsazure.com](https://manage.windowsazure.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-293">Open a browser, and navigate to [https://manage.windowsazure.com](https://manage.windowsazure.com).</span></span> 
2. <span data-ttu-id="440b0-294">관리자 권한으로 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-294">Log on as the administrator.</span></span>
3. <span data-ttu-id="440b0-295">포털의 왼쪽 탐색 영역에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-295">In the portal, in the left navigation, click **ACTIVE DIRECTORY**.</span></span>

 ![기본 디렉터리](./media/nps-extension-vpn/image23.png)

4. <span data-ttu-id="440b0-297">[이름] 열에서 **기본 디렉터리**(또는 해당되는 경우 다른 디렉터리)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-297">In the NAME column, click **Default Directory** (or another directory, if appropriate).</span></span>
5. <span data-ttu-id="440b0-298">[빠른 시작] 페이지에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-298">On the Quick Start page, click **Configure**.</span></span>

 ![기본 구성](./media/nps-extension-vpn/image24.png)

6. <span data-ttu-id="440b0-300">[구성] 페이지에서 아래로 스크롤하고 다단계 인증 섹션에서 **서비스 설정 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-300">On the CONFIGURE page, scroll down and, in the multi-factor authentication section, click **Manage service settings**.</span></span>

 ![MFA 설정 관리](./media/nps-extension-vpn/image25.png)
 
7. <span data-ttu-id="440b0-302">다단계 인증 페이지에서 기본 서비스 설정을 검토한 다음 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-302">On the multi-factor authentication page, review the default service settings, and then click **Users**.</span></span> 

 ![MFA 사용자](./media/nps-extension-vpn/image26.png)
 
8. <span data-ttu-id="440b0-304">[사용자] 페이지에서 MFA를 사용하도록 설정할 사용자를 선택한 다음 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-304">On the Users page, select the users that you wish to enable for MFA, and then click **Enable**.</span></span>

 ![properties](./media/nps-extension-vpn/image27.png)
 
9. <span data-ttu-id="440b0-306">메시지가 표시되면 **다단계 인증 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-306">When prompted, click **Enable multi-factor auth**.</span></span>

 ![MFA 사용](./media/nps-extension-vpn/image28.png)
 
10. <span data-ttu-id="440b0-308">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-308">Click **Close**.</span></span> 
11. <span data-ttu-id="440b0-309">페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-309">Refresh the page.</span></span> <span data-ttu-id="440b0-310">MFA 상태가 [사용]으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-310">The MFA status is changed to Enabled.</span></span>

<span data-ttu-id="440b0-311">사용자가 Azure Multi-Factor Authentication를 사용하도록 설정하는 방법에 대한 자세한 내용은 [클라우드에서 Azure Multi-Factor Authentication 시작](multi-factor-authentication-get-started-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-311">For information on how to enable users for Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](multi-factor-authentication-get-started-cloud.md).</span></span> 

### <a name="configure-accounts-for-two-step-verification"></a><span data-ttu-id="440b0-312">2단계 인증에 대한 계정 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-312">Configure accounts for two-step verification</span></span>
<span data-ttu-id="440b0-313">계정에서 MFA를 사용하도록 설정하면 2단계 인증을 사용하는 두 번째 인증 요소에 사용할 신뢰할 수 있는 장치를 성공적으로 구성할 때까지는 사용자가 MFA 정책이 적용되는 리소스에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-313">Once an account has been enabled for MFA, users are not able to sign in to resources governed by the MFA policy until they have successfully configured a trusted device to use for the second authentication factor having used two-step verification.</span></span>

<span data-ttu-id="440b0-314">이 섹션에서는 2단계 인증에 사용할 신뢰할 수 있는 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-314">In this section, you configure a trusted device for use with two-step verification.</span></span> <span data-ttu-id="440b0-315">이렇게 구성하는 데 사용할 수 있는 옵션으로 다음을 포함하여 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-315">There are several options available for you to configure these, including the following:</span></span>

* <span data-ttu-id="440b0-316">**모바일 앱**</span><span class="sxs-lookup"><span data-stu-id="440b0-316">**Mobile app**.</span></span> <span data-ttu-id="440b0-317">Windows Phone, Android 또는 iOS 장치에 Microsoft Authenticator 앱을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-317">You install the Microsoft Authenticator app on a Windows Phone, Android, or iOS device.</span></span> <span data-ttu-id="440b0-318">조직의 정책에 따라 두 가지 모드, 즉 확인 시 알림 수신(알림이 장치로 푸시됨) 또는 확인 코드 사용(30초마다 업데이트되는 확인 코드를 입력해야 함) 중 하나로 앱을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-318">Depending on your organization’s policies, you are required to use the app in one of two modes: Receive notifications for verifications (a notification is pushed to your device) or Use verification code (you are required to enter a verification code that updates every 30 seconds).</span></span> 
* <span data-ttu-id="440b0-319">**휴대폰 통화 또는 문자 메시지**</span><span class="sxs-lookup"><span data-stu-id="440b0-319">**Mobile phone call or text**.</span></span> <span data-ttu-id="440b0-320">자동 전화 통화 또는 문자 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-320">You can either receive an automated phone call or text message.</span></span> <span data-ttu-id="440b0-321">전화 통화 옵션을 사용하면 호출에 응답하고 # 기호를 눌러 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-321">With the phone call option, you answer the call and press the # sign to authenticate.</span></span> <span data-ttu-id="440b0-322">문자 메시지 옵션을 사용하면 문자 메시지에 회신하거나 로그인 인터페이스에 확인 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-322">With the text option, you can either reply to the text message or enter the verification code into the sign-in interface.</span></span>
* <span data-ttu-id="440b0-323">**사무실 전화 통화**</span><span class="sxs-lookup"><span data-stu-id="440b0-323">**Office phone call**.</span></span> <span data-ttu-id="440b0-324">이 프로세스는 위의 자동 전화 통화에서 설명한 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-324">This process is the same as that described for automated phone calls above.</span></span>

<span data-ttu-id="440b0-325">확인 시 푸시 알림을 수신하는 데 모바일 앱을 사용하도록 장치를 설정하려면 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-325">Follow these instructions for setting up a device to use the mobile app to receive push notification for verification.</span></span>

1. <span data-ttu-id="440b0-326">MFA 지원 자격 증명을 사용하여 인증해야 하는 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 또는 사이트(예: [https://portal.azure.com](https://portal.azure.com))에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-326">Log on to [https://aka.ms/mfasetup](https://aka.ms/mfasetup) or any site, such as [https://portal.azure.com](https://portal.azure.com), where you required to authenticate using your MFA-enabled credentials.</span></span> 
2. <span data-ttu-id="440b0-327">사용자 이름과 암호로 로그인하면 추가 보안 인증을 위해 계정을 설정하라는 메시지가 화면에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-327">Upon signing in with your username and password, you are presented with a screen that prompts you to set up the account for additional security verification.</span></span>

 ![추가 보안](./media/nps-extension-vpn/image29.png)

3. <span data-ttu-id="440b0-329">**지금 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-329">Click **Set it up now**.</span></span>
4. <span data-ttu-id="440b0-330">[추가 보안 인증] 페이지에서 연락처 유형(인증 전화, 사무실 전화 또는 모바일 앱)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-330">On the Additional security verification page, select a contact type (authentication phone, office phone, or mobile app).</span></span> <span data-ttu-id="440b0-331">그런 다음 국가 또는 지역을 선택하고 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-331">Then select a country or region, and select a method.</span></span> <span data-ttu-id="440b0-332">방법은 선택한 연락처 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-332">The method varies by contact type you select.</span></span> <span data-ttu-id="440b0-333">예를 들어 모바일 앱을 선택하면 확인 시 알림을 수신할지 또는 확인 코드를 사용할지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-333">For example, if you choose Mobile app, you can select whether to receive notifications for verification or to use a verification code.</span></span> <span data-ttu-id="440b0-334">다음 단계에서는 연락처 유형으로 **모바일 앱**을 선택한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-334">The steps that follow assume you choose **Mobile app** as the contact type.</span></span>

 ![전화 인증](./media/nps-extension-vpn/image30.png)

5. <span data-ttu-id="440b0-336">모바일 앱을 선택하고 **확인 시 알림 수신**을 클릭한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-336">Select Mobile app, click **Receive notifications for verification**, and then **Set up**.</span></span> 

 ![모바일 앱 확인](./media/nps-extension-vpn/image31.png)
 
6. <span data-ttu-id="440b0-338">인증자 모바일 앱을 아직 설치하지 않았으면 장치에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-338">If you haven’t done so already, install the authenticator mobile app on your device.</span></span> 
7. <span data-ttu-id="440b0-339">모바일 앱의 지침에 따라 제출된 바코드를 스캔하거나 정보를 수동으로 입력한 다음 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-339">Follow the instructions in the mobile app to scan the presented bar code or enter the information manually, and then click **Done**.</span></span>

 ![모바일 앱 구성](./media/nps-extension-vpn/image32.png)

8. <span data-ttu-id="440b0-341">[추가 보안 인증] 페이지에서 **문의처**를 클릭하고 장치로 전송된 알림에 회신합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-341">On the Additional security verification page, click **Contact me** and reply to notification sent to your device.</span></span>
9. <span data-ttu-id="440b0-342">[추가 보안 인증] 페이지에서 모바일 앱에 액세스할 수 없을 경우에 대비하여 연락처 번호를 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-342">On the Additional security verification page, enter a contact number in case you lose access to the mobile app, and click **Next**.</span></span>

 ![휴대폰 번호](./media/nps-extension-vpn/image33.png)
 
10. <span data-ttu-id="440b0-344">[추가 보안 인증]에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-344">On the Additional security verification, click **Done**.</span></span>

<span data-ttu-id="440b0-345">이제 장치는 두 번째 인증 방법을 제공하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-345">The device is now configured to provide a second method of verification.</span></span> <span data-ttu-id="440b0-346">2단계 인증을 위한 계정 설정에 대한 자세한 내용은 [2단계 인증을 위한 계정 설정](./end-user/multi-factor-authentication-end-user-first-time.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-346">For information on setting up accounts for two-step verification, see [Set up my account for two-step verification](./end-user/multi-factor-authentication-end-user-first-time.md).</span></span>

## <a name="install-and-configure-nps-extension"></a><span data-ttu-id="440b0-347">NPS 확장 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-347">Install and configure NPS extension</span></span>

<span data-ttu-id="440b0-348">이 섹션에서는 VPN 서버에서 클라이언트 인증에 Azure MFA를 사용하도록 VPN을 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-348">This section provides instructions for configuring VPN to use Azure MFA for client authentication with the VPN Server.</span></span>

<span data-ttu-id="440b0-349">NPS 확장을 설치하고 구성한 후에 Azure MFA를 사용하려면 이 서버에서 모든 RADIUS 기반 클라이언트 인증을 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-349">Once you install and configure the NPS extension, all RADIUS-based client authentication that is processed by this server is required to use Azure MFA.</span></span> <span data-ttu-id="440b0-350">모든 VPN 사용자가 Azure MFA에 등록되지 않은 경우 MFA를 사용하도록 구성되지 않은 사용자를 인증하도록 다른 RADIUS 서버를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-350">If not all your VPN users are enrolled in Azure MFA, you can set up another RADIUS server to authenticate users who are not configured to use MFA.</span></span> <span data-ttu-id="440b0-351">또는 MFA에 등록된 경우에만 문제가 있는 사용자가 두 번째 인증 요소를 제공할 수 있도록 레지스트리 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-351">Or you can create a registry entry that allows challenged users to provide a second authentication factor, only if they are enrolled in MFA.</span></span> 

<span data-ttu-id="440b0-352">_HKLM\SOFTWARE\Microsoft\AzureMfa에 REQUIRE_USER_MATCH_라는 새 문자열 값을 만들고 이 값을 TRUE 또는 FALSE로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-352">Create a new string value named _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_, and set the value to TRUE or FALSE.</span></span> 

 ![사용자 일치 필요](./media/nps-extension-vpn/image34.png)
 
<span data-ttu-id="440b0-354">값이 TRUE로 설정되거나 설정되지 않으면 모든 인증 요청은 MFA 챌린지의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-354">If the value is set to TRUE or not set, all authentication requests are subject to an MFA challenge.</span></span> <span data-ttu-id="440b0-355">값을 FALSE로 설정하면 MFA 챌린지가 MFA에 등록된 사용자에게만 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-355">If the value is set to FALSE, MFA challenges are issued only to users that are enrolled in MFA.</span></span> <span data-ttu-id="440b0-356">등록 기간 동안 테스트 환경 또는 프로덕션 환경에서만 FALSE 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-356">Only use the FALSE setting in testing or in production environments during an onboarding period.</span></span>

### <a name="acquire-azure-active-directory-guid-id"></a><span data-ttu-id="440b0-357">Azure Active Directory GUID ID 얻기</span><span class="sxs-lookup"><span data-stu-id="440b0-357">Acquire Azure Active Directory GUID ID</span></span>

<span data-ttu-id="440b0-358">NPS 확장 구성의 일환으로 Azure AD 테넌트에 대한 관리자 자격 증명과 Azure Active Directory ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-358">As part of the configuration of the NPS extension, you need to supply admin credentials and the Azure Active Directory ID for your Azure AD tenant.</span></span> <span data-ttu-id="440b0-359">다음 단계에서는 테넌트 ID를 얻는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-359">The steps below show you how to get the tenant ID.</span></span>

1. <span data-ttu-id="440b0-360">[https://portal.azure.com](https://portal.azure.com)의 Azure Portal에 Azure 테넌트의 전역 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-360">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com) as the global administrator of the Azure tenant.</span></span>
2. <span data-ttu-id="440b0-361">왼쪽 탐색 영역에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-361">In the left navigation, click the **Azure Active Directory** icon.</span></span>
3. <span data-ttu-id="440b0-362">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-362">Click **Properties**.</span></span>
4. <span data-ttu-id="440b0-363">디렉터리 ID를 클립보드에 복사하려면 **복사** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-363">To copy your Directory ID to the clipboard, select the **Copy** icon.</span></span>
 
 ![디렉터리 ID](./media/nps-extension-vpn/image35.png)

### <a name="install-the-nps-extension"></a><span data-ttu-id="440b0-365">NPS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="440b0-365">Install the NPS extension</span></span>
<span data-ttu-id="440b0-366">NPS 확장은 NPS(네트워크 정책 및 액세스 서비스) 역할이 설치되고 설계상 RADIUS 서버로 작동하는 서버에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-366">The NPS extension needs to be installed on a server that has the Network Policy and Access Services (NPS) role installed and that functions as the RADIUS server in your design.</span></span> <span data-ttu-id="440b0-367">NPS 확장을 원격 데스크톱 서버에 설치하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-367">Don't install the NPS extension on your Remote Desktop Server.</span></span>

1. <span data-ttu-id="440b0-368">[https://aka.ms/npsmfa](https://aka.ms/npsmfa)에서 NPS 확장을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-368">Download the NPS extension from [https://aka.ms/npsmfa](https://aka.ms/npsmfa).</span></span> 
2. <span data-ttu-id="440b0-369">설치 실행 파일(NpsExtnForAzureMfaInstaller.exe)을 NPS 서버에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-369">Copy the setup executable file (NpsExtnForAzureMfaInstaller.exe) to the NPS server.</span></span>
3. <span data-ttu-id="440b0-370">NPS 서버에서 **NpsExtnForAzureMfaInstaller.exe**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-370">On the NPS server, double-click **NpsExtnForAzureMfaInstaller.exe**.</span></span> <span data-ttu-id="440b0-371">메시지가 표시되면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-371">If prompted, click **Run**.</span></span>
4. <span data-ttu-id="440b0-372">Azure MFA용 NPS 확장 대화 상자에서 소프트웨어 사용 조건을 검토하고, **사용 약관에 동의함**을 선택한 다음, **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-372">In the NPS Extension for Azure MFA dialog box, review the software license terms, check **I agree to the license terms and conditions**, and click **Install**.</span></span>

 ![NPS 확장](./media/nps-extension-vpn/image36.png)
 
5. <span data-ttu-id="440b0-374">Azure MFA용 NPS 확장 대화 상자에서 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-374">In the NPS Extension for Azure MFA dialog box, click **Close**.</span></span>  

 ![성공적인 설치](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-the-nps-extension-using-a-powershell-script"></a><span data-ttu-id="440b0-376">PowerShell 스크립트를 사용하여 NPS 확장에서 사용할 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="440b0-376">Configure certificates for use with the NPS extension using a PowerShell script</span></span>
<span data-ttu-id="440b0-377">보안 통신 및 보증을 보장하려면 NPS 확장에서 사용할 인증서를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-377">To ensure secure communications and assurance, you need to configure certificates for use by the NPS extension.</span></span> <span data-ttu-id="440b0-378">NPS 구성 요소에는 NPS에서 사용할 자체 서명된 인증서를 구성하는 Windows PowerShell 스크립트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-378">The NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="440b0-379">이 스크립트에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-379">The script performs the following actions:</span></span>

* <span data-ttu-id="440b0-380">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="440b0-380">Creates a self-signed certificate</span></span>
* <span data-ttu-id="440b0-381">인증서의 공개 키를 Azure AD의 서비스 사용자에 연결</span><span class="sxs-lookup"><span data-stu-id="440b0-381">Associates public key of certificate to service principal on Azure AD</span></span>
* <span data-ttu-id="440b0-382">로컬 컴퓨터 인증서 저장소에 인증서 저장</span><span class="sxs-lookup"><span data-stu-id="440b0-382">Stores the cert in the local machine store</span></span>
* <span data-ttu-id="440b0-383">네트워크 사용자에게 인증서의 개인 키에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="440b0-383">Grants access to the certificate’s private key to the Network User</span></span>
* <span data-ttu-id="440b0-384">네트워크 정책 서버 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="440b0-384">Restarts Network Policy Server service</span></span>

<span data-ttu-id="440b0-385">사용자 고유의 인증서를 사용하려면 인증서의 공개 키를 Azure AD의 서비스 사용자 등에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-385">If you want to use your own certificates, you need to associate the public of your certificate to the service principle on Azure AD, and so on.</span></span>
<span data-ttu-id="440b0-386">스크립트를 사용하려면 이전에 복사한 Azure Active Directory 관리자 자격 증명과 Azure Active Directory 테넌트 ID를 확장에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-386">To use the script, provide the extension with your Azure Active Directory administrative credentials and the Azure Active Directory tenant ID you copied earlier.</span></span> <span data-ttu-id="440b0-387">NPS 확장을 설치하는 각 NPS 서버에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-387">Run the script on each NPS server where you install the NPS extension.</span></span>

1. <span data-ttu-id="440b0-388">관리 Windows PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-388">Open an administrative Windows PowerShell prompt.</span></span>
2. <span data-ttu-id="440b0-389">PowerShell 프롬프트에서 _cd 'c:\Program Files\Microsoft\AzureMfa\Config'_를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-389">At the PowerShell prompt, type _cd ‘c:\Program Files\Microsoft\AzureMfa\Config’_, and press **ENTER**.</span></span>
3. <span data-ttu-id="440b0-390">_.\AzureMfsNpsExtnConfigSetup.ps1_을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-390">Type _.\AzureMfsNpsExtnConfigSetup.ps1_, and press **ENTER**.</span></span> 
 * <span data-ttu-id="440b0-391">스크립트에서 Azure Active Directory PowerShell 모듈이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-391">The script checks to see if the Azure Active Directory PowerShell module is installed.</span></span> <span data-ttu-id="440b0-392">설치되어 있지 않으면 스크립트에서 해당 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-392">If it is not installed, the script installs the module for you.</span></span>
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. <span data-ttu-id="440b0-394">스크립트에서 PowerShell 모듈 설치를 확인한 후에 Azure Active Directory PowerShell 모듈 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-394">After the script verifies the installation of the PowerShell module, it displays the Azure Active Directory PowerShell module dialog box.</span></span> <span data-ttu-id="440b0-395">대화 상자에서 Azure AD 관리자 자격 증명 및 암호를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-395">In the dialog box, enter your Azure AD admin credentials and password, and click **Sign in**.</span></span> 
 
 ![PowerShell 로그인](./media/nps-extension-vpn/image39.png)
 
5. <span data-ttu-id="440b0-397">메시지가 표시되면 앞에서 복사한 테넌트 ID를 클립보드에 붙여넣고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-397">When prompted, paste the tenant ID you copied to the clipboard earlier, and press **ENTER**.</span></span> 

 ![테넌트 ID](./media/nps-extension-vpn/image40.png)

6. <span data-ttu-id="440b0-399">스크립트에서 자체 서명된 인증서를 만들고 다른 구성 변경 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-399">The script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="440b0-400">출력은 아래 이미지와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-400">The output is like the image shown below.</span></span>

 ![자체 서명된 인증서](./media/nps-extension-vpn/image41.png)

7. <span data-ttu-id="440b0-402">서버를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-402">Reboot the server.</span></span>
 
### <a name="verify-configuration"></a><span data-ttu-id="440b0-403">구성 확인</span><span class="sxs-lookup"><span data-stu-id="440b0-403">Verify configuration</span></span>
<span data-ttu-id="440b0-404">구성을 확인하려면 VPN 서버와의 새 VPN 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-404">To verify the configuration, you need to establish a new VPN connection with VPN server.</span></span> <span data-ttu-id="440b0-405">기본 인증을 위한 자격 증명을 성공적으로 입력하면 아래와 같이 VPN 연결에서 연결이 설정되기 전에 보조 인증이 성공할 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-405">Upon successfully entering your credentials for primary authentication, the VPN connection waits for the secondary authentication to succeed before the connection is established, as shown below.</span></span> 

 ![구성 확인](./media/nps-extension-vpn/image42.png)

<span data-ttu-id="440b0-407">Azure MFA에서 이전에 구성한 보조 인증 방법으로 성공적으로 인증하면 해당 리소스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-407">If you successfully authenticate with the secondary verification method you previously configured in Azure MFA, you are connected to the resource.</span></span> <span data-ttu-id="440b0-408">그러나 보조 인증이 실패하면 리소스에 대한 액세스가 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-408">However, if the secondary authentication is not successful, you are denied access to resource.</span></span> 

<span data-ttu-id="440b0-409">아래 예에서 Windows Phone의 Authenticator 앱이 보조 인증을 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-409">In the example below, the Authenticator app on a Windows phone is used to provide the secondary authentication.</span></span>

 ![계정 확인](./media/nps-extension-vpn/image43.png)

<span data-ttu-id="440b0-411">보조 인증 방법을 사용하여 성공적으로 인증되면 VPN 서버의 가상 포트에 대한 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-411">Once you have successfully authenticated using the secondary method, you are granted access to the virtual port on the VPN server.</span></span> <span data-ttu-id="440b0-412">그러나 신뢰할 수 있는 장치에서 모바일 앱을 사용하여 보조 인증 방법을 사용해야 하므로 로그인 프로세스가 사용자 이름/암호 조합을 사용하는 경우보다 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-412">However, because you were required to use a secondary authentication method using a mobile app on a trusted device, the log in process is more secure than it would be using only a username / password combination.</span></span>

### <a name="view-event-viewer-logs-for-successful-logon-events"></a><span data-ttu-id="440b0-413">성공적인 로그온 이벤트에 대한 이벤트 뷰어 로그 보기</span><span class="sxs-lookup"><span data-stu-id="440b0-413">View Event Viewer logs for successful logon events</span></span>
<span data-ttu-id="440b0-414">Windows 이벤트 뷰어 로그에서 성공적인 로그온 이벤트를 확인하려면 다음 Windows PowerShell 명령을 실행하여 NPS 서버에서 Windows 보안 로그를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-414">To view the successful logon events in the Windows Event Viewer logs, you can issue the following Windows PowerShell command to query the Windows Security log on the NPS server.</span></span>

<span data-ttu-id="440b0-415">보안 이벤트 뷰어 로그에서 성공적인 로그온 이벤트를 쿼리하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-415">To query successful logon events in the Security event viewer logs, use the following command,</span></span>
* <span data-ttu-id="440b0-416">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="440b0-416">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span> 

 ![보안 이벤트 뷰어](./media/nps-extension-vpn/image44.png)
 
<span data-ttu-id="440b0-418">또한 아래와 같이 보안 로그 또는 네트워크 정책 및 액세스 서비스 사용자 지정 보기를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-418">You can also view the Security log or the Network Policy and Access Services custom view, as shown below:</span></span>

 ![네트워크 정책 액세스](./media/nps-extension-vpn/image45.png)

<span data-ttu-id="440b0-420">Azure MFA용 NPS 확장을 설치한 서버에서 **Application and Services Logs\Microsoft\AzureMfa**에 있는 확장과 관련된 이벤트 뷰어 응용 프로그램 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-420">On the server where you installed the NPS extension for Azure MFA, you can find Event Viewer application logs specific to the extension at **Application and Services Logs\Microsoft\AzureMfa**.</span></span> 

* <span data-ttu-id="440b0-421">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="440b0-421">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span>

 ![이벤트 수](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="440b0-423">문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="440b0-423">Troubleshoot Guide</span></span>
<span data-ttu-id="440b0-424">구성이 예상대로 작동하지 않는 경우 사용자가 Azure MFA를 사용하도록 구성되어 있는지 확인하여 문제 해결을 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-424">If the configuration is not working as expected, a good place to start to troubleshoot is to verify that the user is configured to use Azure MFA.</span></span> <span data-ttu-id="440b0-425">사용자가 [https://portal.azure.com](https://portal.azure.com)에 연결하도록 합니다. 보조 인증을 요청받았고 성공적으로 인증할 수 있으면 Azure MFA의 잘못된 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-425">Have the user connect to [https://portal.azure.com](https://portal.azure.com). If they are prompted for secondary authentication and can successfully authenticate, you can eliminate an incorrect configuration of Azure MFA.</span></span>

<span data-ttu-id="440b0-426">Azure MFA가 사용자에 대해 작동하는 경우 관련 이벤트 로그를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-426">If Azure MFA is working for the user(s), you should review the relevant Event logs.</span></span> <span data-ttu-id="440b0-427">여기에는 이전 섹션에서 설명한 보안 이벤트, 게이트웨이 작업 및 Azure MFA 로그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-427">These include the Security Event, Gateway operational, and Azure MFA logs that are discussed in the previous section.</span></span> 

<span data-ttu-id="440b0-428">다음은 실패한 로그온 이벤트(6273 이벤트 ID)를 보여 주는 보안 로그의 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-428">Below is an example output of Security log showing a failed logon event (Event ID 6273):</span></span>

 ![보안 로그](./media/nps-extension-vpn/image47.png)

<span data-ttu-id="440b0-430">다음은 AzureMFA 로그와 관련된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-430">Below is a related event from the AzureMFA logs:</span></span>

 ![Azure MFA 로그](./media/nps-extension-vpn/image48.png)

<span data-ttu-id="440b0-432">고급 문제 해결 옵션을 수행하려면 NPS 서비스가 설치된 NPS 데이터베이스 형식 로그 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-432">To perform advanced troubleshoot options, consult the NPS database format log files where the NPS service is installed.</span></span> <span data-ttu-id="440b0-433">이러한 로그 파일은 _%SystemRoot%\System32\Logs_ 폴더에 쉼표로 구분된 텍스트 파일로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-433">These log files are created in _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> <span data-ttu-id="440b0-434">이러한 로그 파일에 대한 자세한 내용은 [NPS 데이터베이스 형식 로그 파일 해석(영문)](https://technet.microsoft.com/library/cc771748.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-434">For a description of these log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> 

<span data-ttu-id="440b0-435">이러한 로그 파일의 항목은 스프레드시트 또는 데이터베이스로 가져오지 않고는 해석하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-435">The entries in these log files are difficult to interpret without importing them into a spreadsheet or a database.</span></span> <span data-ttu-id="440b0-436">로그 파일을 해석하는 데 도움이 되는 다양한 IAS 파서를 온라인으로 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-436">You can find a number of IAS parsers online to assist you in interpreting the log files.</span></span> <span data-ttu-id="440b0-437">다음은 다운로드할 수 있는 [셰어웨어 응용 프로그램](http://www.deepsoftware.com/iasviewer)의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-437">Below is the output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer):</span></span> 

 ![셰어웨어 응용 프로그램](./media/nps-extension-vpn/image49.png)

<span data-ttu-id="440b0-439">마지막으로 추가적인 문제 해결 옵션을 위해 Wireshark 또는 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)와 같은 프로토콜 분석기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-439">Finally, for additional troubleshoot options, you can use a protocol analyzer such as Wireshark or [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> <span data-ttu-id="440b0-440">다음의 Wireshark 이미지에서는 VPN 서버와 NPS 서버 간의 RADIUS 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="440b0-440">The following image from Wireshark shows the RADIUS messages between the VPN server and the NPS server.</span></span>

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

<span data-ttu-id="440b0-442">자세한 내용은 [기존 NPS 인프라를 Azure Multi-Factor Authentication과 통합](multi-factor-authentication-nps-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="440b0-442">For more information, see [Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="440b0-443">다음 단계</span><span class="sxs-lookup"><span data-stu-id="440b0-443">Next steps</span></span>
[<span data-ttu-id="440b0-444">Azure Multi-Factor Authentication을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="440b0-444">How to get Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-versions-plans.md)

[<span data-ttu-id="440b0-445">RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버</span><span class="sxs-lookup"><span data-stu-id="440b0-445">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](multi-factor-authentication-get-started-server-rdg.md)

[<span data-ttu-id="440b0-446">Azure Active Directory와 온-프레미스 디렉터리 통합</span><span class="sxs-lookup"><span data-stu-id="440b0-446">Integrate your on-premises directories with Azure Active Directory</span></span>](../active-directory/connect/active-directory-aadconnect.md)

