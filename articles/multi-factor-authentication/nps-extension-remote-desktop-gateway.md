---
title: "Azure MFA NPS 확장명이 데스크톱 게이트웨이 통합 aaaRemote | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure에 대 한 hello 서버 NPS (네트워크 정책) 확장을 사용 하는 Azure MFA를 원격 데스크톱 게이트웨이 인프라 통합 설명 합니다."
services: active-directory
keywords: "Azure MFA, 원격 데스크톱 게이트웨이 통합, Azure Active Directory, 네트워크 정책 서버 확장"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a><span data-ttu-id="86307-104">Hello 정책 서버 NPS (네트워크) 확장 및 Azure AD를 사용 하 여 원격 데스크톱 게이트웨이 인프라 통합</span><span class="sxs-lookup"><span data-stu-id="86307-104">Integrate your Remote Desktop Gateway infrastructure using hello Network Policy Server (NPS) extension and Azure AD</span></span>

<span data-ttu-id="86307-105">이 문서에서는 Microsoft Azure에 대 한 hello 서버 NPS (네트워크 정책) 확장을 사용 하 여 원격 데스크톱 게이트웨이 인프라와 Azure Multi-factor Authentication (MFA)을 통합 하기 위한 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="86307-105">This article provides details for integrating your Remote Desktop Gateway infrastructure with Azure Multi-Factor Authentication (MFA) using hello Network Policy Server (NPS) extension for Microsoft Azure.</span></span> 

<span data-ttu-id="86307-106">Azure를 사용 하 여 고객 toosafeguard 인증 전화 접속 사용자 RADIUS (Remote Service) 클라이언트 인증의 클라우드 기반 Azure에 대 한 서비스 NPS (네트워크 정책) 확장 hello 허용 [Multi-factor Authentication (MFA)](multi-factor-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-106">hello Network Policy Service (NPS) extension for Azure allows customers toosafeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using Azure’s cloud-based [Multi-Factor Authentication (MFA)](multi-factor-authentication.md).</span></span> <span data-ttu-id="86307-107">이 솔루션은 두 번째 계층을 보안 toouser 로그인 및 트랜잭션에 추가 하는 데 2 단계 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-107">This solution provides two-step verification for adding a second layer of security toouser sign-ins and transactions.</span></span>

<span data-ttu-id="86307-108">이 문서에서는 hello NPS 확장을 사용 하 여 Azure에 대 한 hello NPS 인프라 Azure MFA를 통합 하기 위한 단계별 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-108">This article provides step-by-step instructions for integrating hello NPS infrastructure with Azure MFA using hello NPS extension for Azure.</span></span> <span data-ttu-id="86307-109">이렇게 하면 원격 데스크톱 게이트웨이 tooa에 toolog 시도 하는 사용자에 대 한 보안을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-109">This enables secure verification for users attempting toolog on tooa Remote Desktop Gateway.</span></span> 

<span data-ttu-id="86307-110">hello 네트워크 정책 및 액세스 서비스 (NPS)에서는 조직이 기능 toodo hello 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="86307-110">hello Network Policy and Access Services (NPS) gives organizations hello ability toodo hello following:</span></span>
* <span data-ttu-id="86307-111">연결할 수 있는 사용자 지정 하 여 hello 관리 및 제어의 네트워크 요청에 대 한 중앙 위치를 정의 연결이 허용 되는지 하루 중 어떤 시간 hello 연결, 기간 및 hello 수준의 보안 클라이언트 tooconnect를 사용 하 고 등 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-111">Define central locations for hello management and control of network requests by specifying who can connect, what times of day connections are allowed, hello duration of connections, and hello level of security that clients must use tooconnect, and so on.</span></span> <span data-ttu-id="86307-112">이러한 정책은 각 VPN 또는 RD(원격 데스크톱) 게이트웨이 서버에 지정하는 대신 중앙 위치에 한 번만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-112">Rather than specifying these policies on each VPN or Remote Desktop (RD) Gateway server, these policies can be specified once in a central location.</span></span> <span data-ttu-id="86307-113">RADIUS 프로토콜과 hello hello 중앙 집중식 인증, 권한 부여 및 계정 AAA ()를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-113">hello RADIUS protocol provides hello centralized Authentication, Authorization, and Accounting (AAA).</span></span> 
* <span data-ttu-id="86307-114">설정 및 장치 toonetwork 리소스 제한 또는 무제한 액세스를 부여 된 있는지 여부를 결정 하는 네트워크 액세스 보호 (NAP) 클라이언트 상태 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-114">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access toonetwork resources.</span></span>
* <span data-ttu-id="86307-115">액세스 too802.1x 지원 무선 액세스 지점 및 이더넷 스위치에 대 한 의미 tooenforce 인증 및 권한 부여를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-115">Provide a means tooenforce authentication and authorization for access too802.1x-capable wireless access points and Ethernet switches.</span></span>    

<span data-ttu-id="86307-116">일반적으로 조직 toosimplify NPS RADIUS ()를 사용 하 고 VPN의 hello 관리를 중앙 집중화 정책이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-116">Typically, organizations use NPS (RADIUS) toosimplify and centralize hello management of VPN polices.</span></span> <span data-ttu-id="86307-117">그러나 대부분의 조직에서는 또한 toosimplify NPS를 사용 하 여 고 RD 데스크톱 연결 권한 부여 정책 RD Cap ()의 hello 관리를 중앙 집중화 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-117">However, many organizations also use NPS toosimplify and centralize hello management of RD Desktop Connection Authorization Policies (RD CAPs).</span></span> 

<span data-ttu-id="86307-118">조직에서는 Azure MFA tooenhance 보안 NPS 통합할 수 있고 높은 호환성 수준을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-118">Organizations can also integrate NPS with Azure MFA tooenhance security and provide a high level of compliance.</span></span> <span data-ttu-id="86307-119">이렇게 하면 사용자가 원격 데스크톱 게이트웨이 toohello에 2 단계 확인 toolog를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-119">This helps ensure that users establish two-step verification toolog on toohello Remote Desktop Gateway.</span></span> <span data-ttu-id="86307-120">에 대 한 액세스 권한이 부여 되는 사용자가 toobe, 해당 컨트롤에 자신의 사용자 이름/암호 조합이 hello 사용자 정보로는 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-120">For users toobe granted access, they must provide their username/password combination with information that hello user has in their control.</span></span> <span data-ttu-id="86307-121">이 정보는 신뢰할 수 있어야 하며, 휴대폰 번호, 유선 전화 번호, 모바일 장치 등과 같이 쉽게 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-121">This information must be trusted and not easily duplicated, such as a cell phone number, landline number, application on a mobile device, and so on.</span></span>

<span data-ttu-id="86307-122">Hello Azure에 대 한 NPS 확장의 이전 toohello 가용성, 고객에 대 한 2 단계 인증 tooimplement 입장 통합 NPS 및 Azure MFA 환경 tooconfigure 되었고 hello 온-프레미스 환경에서 별도 MFA 서버를 유지 관리 에 설명 되어 [원격 데스크톱 게이트웨이 및 Azure Multi-factor Authentication 서버 RADIUS를 사용 하 여](multi-factor-authentication-get-started-server-rdg.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-122">Prior toohello availability of hello NPS extension for Azure, customers who wished tooimplement two-step verification for integrated NPS and Azure MFA environments had tooconfigure and maintain a separate MFA Server in hello on-premises environment as documented in [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>

<span data-ttu-id="86307-123">이제 Azure 용 hello NPS 확장의 가용성을 hello는 온-프레미스 기반 MFA 솔루션 또는 클라우드 기반 MFA 솔루션 toosecure RADIUS 클라이언트 인증 조직 hello 선택 toodeploy를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-123">hello availability of hello NPS extension for Azure now gives organizations hello choice toodeploy either an on-premises based MFA solution or a cloud-based MFA solution toosecure RADIUS client authentication.</span></span>

## <a name="authentication-flow"></a><span data-ttu-id="86307-124">인증 흐름</span><span class="sxs-lookup"><span data-stu-id="86307-124">Authentication Flow</span></span>

<span data-ttu-id="86307-125">Toobe 부여는 사용자에 대 한 원격 데스크톱 게이트웨이 통해 toonetwork 리소스에 액세스 한 RD 연결 권한 부여 정책 (RD CAP) 및 하나의 RD 리소스 권한 부여 정책 RD RAP ()에 지정 된 hello 조건을 만족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-125">For users toobe granted access toonetwork resources through a Remote Desktop Gateway, they must meet hello conditions specified in one RD Connection Authorization Policy (RD CAP) and one RD Resource Authorization Policy (RD RAP).</span></span> <span data-ttu-id="86307-126">RD Cap만 사용자가 권한 있는 tooconnect tooRD 게이트웨이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-126">RD CAPs specify who is authorized tooconnect tooRD Gateways.</span></span> <span data-ttu-id="86307-127">RD Rap 원격 데스크톱 또는 원격 앱과 같이 hello 네트워크 리소스를 지정 하면 해당 hello 사용자 수 tooconnect toothrough hello RD 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-127">RD RAPs specify hello network resources, such as remote desktops or remote apps, that hello user is allowed tooconnect toothrough hello RD Gateway.</span></span> 

<span data-ttu-id="86307-128">RD 게이트웨이 구성된 toouse RD Cap 저장소를 중앙 정책 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-128">An RD Gateway can be configured toouse a central policy store for RD CAPs.</span></span> <span data-ttu-id="86307-129">RD Rap hello RD 게이트웨이에서 처리 하면서 중앙 정책을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-129">RD RAPs cannot use a central policy, as they are processed on hello RD Gateway.</span></span> <span data-ttu-id="86307-130">RD 게이트웨이 구성 toouse의 예로 RD Cap에 대 한 중앙 정책 저장소는 hello 중앙 정책 저장소로 사용 하는 RADIUS 클라이언트 tooanother NPS 서버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-130">An example of an RD Gateway configured toouse a central policy store for RD CAPs is a RADIUS client tooanother NPS server that serves as hello central policy store.</span></span>

<span data-ttu-id="86307-131">Azure에 대 한 NPS 확장 hello와 통합 된 hello NPS 및 원격 데스크톱 게이트웨이 hello 정상적으로 인증 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-131">When hello NPS extension for Azure is integrated with hello NPS and Remote Desktop Gateway, hello successful authentication flow is as follows:</span></span>

1. <span data-ttu-id="86307-132">hello 원격 데스크톱 게이트웨이 서버는 원격 데스크톱 사용자 tooconnect tooa 같은 리소스에 원격 데스크톱 세션에서 인증 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-132">hello Remote Desktop Gateway server receives an authentication request from a remote desktop user tooconnect tooa resource, such as a Remote Desktop session.</span></span> <span data-ttu-id="86307-133">클라이언트 역할을 하는 RADIUS hello 원격 데스크톱 게이트웨이 서버 hello 요청 tooa RADIUS 액세스 요청 메시지를 변환 하 고 hello NPS 확장이 설치 되어 hello 메시지 toohello RADIUS (NPS) 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="86307-133">Acting as a RADIUS client, hello Remote Desktop Gateway server converts hello request tooa RADIUS Access-Request message and sends hello message toohello RADIUS (NPS) server where hello NPS extension is installed.</span></span> 
2. <span data-ttu-id="86307-134">hello 사용자 이름 및 Active Directory에서 암호 조합을 확인 하 고 hello 사용자 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-134">hello username and password combination is verified in Active Directory and hello user is authenticated.</span></span>
3. <span data-ttu-id="86307-135">NPS 연결 요청을 hello 및 hello 네트워크 정책을 충족 조건에 지정 된 대로 hello 모든 경우 (예를 들어 시간이 나 그룹 구성원 자격 제한과), NPS 확장 hello Azure MFA를 보조 인증에 대 한 요청을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-135">If all hello conditions as specified in hello NPS Connection Request and hello Network Policies are met (for example, time of day or group membership restrictions), hello NPS extension triggers a request for secondary authentication with Azure MFA.</span></span> 
4. <span data-ttu-id="86307-136">Azure MFA Azure AD와 통신 하 고, hello 사용자의 세부 정보를 검색, hello 사용자 (문자 메시지, 모바일 앱, 및 등)으로 구성 하는 hello 메서드를 사용 하 여 hello 보조 인증을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-136">Azure MFA communicates with Azure AD, retrieves hello user’s details, and performs hello secondary authentication using hello method configured by hello user (text message, mobile app, and so on).</span></span> 
5. <span data-ttu-id="86307-137">검색에 성공 hello MFA 챌린지의 Azure MFA hello 결과 toohello NPS 확장을 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-137">Upon success of hello MFA challenge, Azure MFA communicates hello result toohello NPS extension.</span></span>
6. <span data-ttu-id="86307-138">hello 확장이 설치 되어 hello NPS 서버 hello RD CAP 정책 toohello 원격 데스크톱 게이트웨이 서버에 대 한 RADIUS 액세스 허용 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="86307-138">hello NPS server where hello extension is installed sends a RADIUS Access-Accept message for hello RD CAP policy toohello Remote Desktop Gateway server.</span></span>
7. <span data-ttu-id="86307-139">hello 사용자의 액세스 권한 toohello hello RD 게이트웨이 통해 네트워크 리소스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-139">hello user is granted access toohello requested network resource through hello RD Gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86307-140">필수 조건</span><span class="sxs-lookup"><span data-stu-id="86307-140">Prerequisites</span></span>
<span data-ttu-id="86307-141">이 섹션에는 필수 구성 요소 hello Azure MFA 원격 데스크톱 게이트웨이 hello와 통합 하기 전에 필요한 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-141">This section details hello prerequisites necessary before integrating Azure MFA with hello Remote Desktop Gateway.</span></span> <span data-ttu-id="86307-142">시작 하기 전에 다음 필수 구성 요소가 충족 하는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-142">Before you begin, you must have hello following prerequisites in place.</span></span>  

* <span data-ttu-id="86307-143">RDS(원격 데스크톱 서비스) 인프라</span><span class="sxs-lookup"><span data-stu-id="86307-143">Remote Desktop Services (RDS) infrastructure</span></span>
* <span data-ttu-id="86307-144">Azure MFA 라이선스</span><span class="sxs-lookup"><span data-stu-id="86307-144">Azure MFA License</span></span>
* <span data-ttu-id="86307-145">Windows Server 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="86307-145">Windows Server software</span></span>
* <span data-ttu-id="86307-146">NPS(네트워크 정책 및 액세스 서비스) 역할</span><span class="sxs-lookup"><span data-stu-id="86307-146">Network Policy and Access Services (NPS) role</span></span>
* <span data-ttu-id="86307-147">온-프레미스 AD와 동기화되는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="86307-147">Azure AD synched with on-premises AD</span></span> 
* <span data-ttu-id="86307-148">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="86307-148">Azure Active Directory GUID ID</span></span>

### <a name="remote-desktop-services-rds-infrastructure"></a><span data-ttu-id="86307-149">RDS(원격 데스크톱 서비스) 인프라</span><span class="sxs-lookup"><span data-stu-id="86307-149">Remote Desktop Services (RDS) infrastructure</span></span>
<span data-ttu-id="86307-150">작동 중인 RDS(원격 데스크톱 서비스) 인프라가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-150">You must have a working Remote Desktop Services (RDS) infrastructure in place.</span></span> <span data-ttu-id="86307-151">Azure에서이 인프라를 신속 하 게 만들 수 있습니다, 그렇지 않은 경우 사용 하 여 hello 다음 빠른 시작 템플릿: [원격 데스크톱 세션 컬렉션 만들기 배포](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-151">If you do not, then you can quickly create this infrastructure in Azure using hello following quick start template: [Create Remote Desktop Session Collection deployment](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment).</span></span> 

<span data-ttu-id="86307-152">원하는 경우 toomanually 하나에 따라 hello 단계 toodeploy 신속 하 게 테스트용으로, 온-프레미스 RDS 인프라를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86307-152">If you wish toomanually create an on-premises RDS infrastructure quickly for testing purposes, follow hello steps toodeploy one.</span></span> 
<span data-ttu-id="86307-153">**자세한 정보**: [Azure 빠른 시작으로 RDS 배포](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) 및 [기본 RDS 인프라 배포](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure)</span><span class="sxs-lookup"><span data-stu-id="86307-153">**Learn more**: [Deploy RDS with Azure quick start](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) and [Basic RDS infrastructure deployment](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure).</span></span> 

### <a name="licenses"></a><span data-ttu-id="86307-154">라이선스</span><span class="sxs-lookup"><span data-stu-id="86307-154">Licenses</span></span>
<span data-ttu-id="86307-155">Azure AD Premium, EMS(Enterprise Mobility plus Security) 또는 MFA 구독을 통해 사용할 수 있는 Azure MFA에 대한 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-155">Required is a license for Azure MFA, which is available through an Azure AD Premium, Enterprise Mobility plus Security (EMS), or an MFA subscription.</span></span> <span data-ttu-id="86307-156">자세한 내용은 참조 [어떻게 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-156">For more information, see [How tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span></span> <span data-ttu-id="86307-157">테스트를 위해 평가판 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-157">For testing purposes, you can use a trial subscription.</span></span>

### <a name="software"></a><span data-ttu-id="86307-158">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="86307-158">Software</span></span>
<span data-ttu-id="86307-159">hello NPS 확장 해야 Windows Server 2008 R2 SP1 이상 hello NPS 역할 서비스가 설치 되어 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-159">hello NPS extension requires Windows Server 2008 R2 SP1 or above with hello NPS role service installed.</span></span> <span data-ttu-id="86307-160">Windows Server 2016을 사용 하 여이 섹션의 모든 hello 단계를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-160">All hello steps in this section were performed using Windows Server 2016.</span></span>

### <a name="network-policy-and-access-services-nps-role"></a><span data-ttu-id="86307-161">NPS(네트워크 정책 및 액세스 서비스) 역할</span><span class="sxs-lookup"><span data-stu-id="86307-161">Network Policy and Access Services (NPS) role</span></span>
<span data-ttu-id="86307-162">hello RADIUS 서버 및 클라이언트 기능 뿐만 아니라 네트워크 액세스 정책 상태 관리 서비스 hello NPS 역할 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-162">hello NPS role service provides hello RADIUS server and client functionality as well as Network Access Policy health service.</span></span> <span data-ttu-id="86307-163">인프라의 두 개 이상의 컴퓨터에이 역할을 설치 해야 합니다: 원격 데스크톱 게이트웨이 및 다른 hello 구성원 서버 또는 도메인 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-163">This role must be installed on at least two computers in your infrastructure: hello Remote Desktop Gateway and another member server or domain controller.</span></span> <span data-ttu-id="86307-164">기본적으로 hello 역할은 원격 데스크톱 게이트웨이 hello로 구성 하는 hello 컴퓨터에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-164">By default, hello role is already present on hello computer configured as hello Remote Desktop Gateway.</span></span>  <span data-ttu-id="86307-165">또한에 설치 해야 hello NPS 역할 이상 도메인 컨트롤러 또는 구성원 서버 등의 다른 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-165">You must also install hello NPS role on at least on another computer, such as a domain controller or member server.</span></span>

<span data-ttu-id="86307-166">Hello NPS 역할 설치에 대 한 내용은 Windows Server 2012 또는 이전 서비스, 참조 [NAP 상태 정책 서버 설치](https://technet.microsoft.com/library/dd296890.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-166">For information on installing hello NPS role service Windows Server 2012 or older, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="86307-167">NPS 포함 하 여 hello 권장 tooinstall NPS 도메인 컨트롤러에 대 한 모범 사례에 대 한 설명을 참조 하십시오. [NPS에 대 한 유용한](https://technet.microsoft.com/library/cc771746)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-167">For a description of best practices for NPS, including hello recommendation tooinstall NPS on a domain controller, see [Best Practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a><span data-ttu-id="86307-168">온-프레미스 Active Directory와 동기화되는 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86307-168">Azure Active Directory synched with on-premises Active Directory</span></span> 
<span data-ttu-id="86307-169">toouse hello NPS 확장 온-프레미스 사용자를 Azure AD와 동기화 하 고 MFA에 대해 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-169">toouse hello NPS extension, on-premises users must be synced with Azure AD and enabled for MFA.</span></span> <span data-ttu-id="86307-170">이 섹션에서는 온-프레미스 사용자가 AD Connect를 사용하여 Azure AD와 동기화된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-170">This section assumes that on-premises users are synched with Azure AD using AD Connect.</span></span> <span data-ttu-id="86307-171">Azure AD 연결에 대한 자세한 내용은 [Azure Active Directory와 온-프레미스 디렉터리 통합](../active-directory/connect/active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86307-171">For information on Azure AD connect, see [Integrate your on-premises directories with Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="86307-172">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="86307-172">Azure Active Directory GUID ID</span></span>
<span data-ttu-id="86307-173">NPS tooinstall tooknow hello hello Azure AD의 GUID 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-173">tooinstall NPS, you need tooknow hello GUID of hello Azure AD.</span></span> <span data-ttu-id="86307-174">Hello hello Azure AD의 GUID 찾기에 대 한 지침 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-174">Instructions for finding hello GUID of hello Azure AD are provided below.</span></span>

## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="86307-175">Multi-Factor Authentication 구성</span><span class="sxs-lookup"><span data-stu-id="86307-175">Configure Multi-Factor Authentication</span></span> 
<span data-ttu-id="86307-176">이 섹션에서는 원격 데스크톱 게이트웨이 hello로 Azure MFA를 통합 하기 위한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-176">This section provides instructions for integrating Azure MFA with hello Remote Desktop Gateway.</span></span> <span data-ttu-id="86307-177">관리자로 서 사용자는 자신의 multi-factor 장치 또는 응용 프로그램에 직접 등록할 수 전에 hello Azure MFA 서비스를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-177">As an administrator, you must configure hello Azure MFA service before users can self-register their multi-factor devices or applications.</span></span>

<span data-ttu-id="86307-178">Hello 단계에 따라 [hello 클라우드에서 Azure Multi-factor Authentication 시작](multi-factor-authentication-get-started-cloud.md) Azure AD 사용자에 대 한 MFA tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-178">Follow hello steps in [Getting started with Azure Multi-Factor Authentication in hello cloud](multi-factor-authentication-get-started-cloud.md) tooenable MFA for your Azure AD users.</span></span> 

### <a name="configure-accounts-for-two-step-verification"></a><span data-ttu-id="86307-179">2단계 인증에 대한 계정 구성</span><span class="sxs-lookup"><span data-stu-id="86307-179">Configure accounts for two-step verification</span></span>
<span data-ttu-id="86307-180">계정이 활성화 된 MFA에 로그인 할 수 없습니다 tooresources 적용 hello MFA 정책까지 hello 두 번째 인증 단계 2 단계 인증을 사용 하 여 인증에 대 한 신뢰할 수 있는 장치 toouse를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-180">Once an account has been enabled for MFA, you cannot sign in tooresources governed by hello MFA policy until you have successfully configured a trusted device toouse for hello second authentication factor have authenticated using two-step verification.</span></span>

<span data-ttu-id="86307-181">Hello 단계에 따라 [무엇 Azure Multi-factor Authentication을 의미 합니까 내?](./end-user/multi-factor-authentication-end-user.md) toounderstand 제대로 MFA에 대 한 사용자 계정으로 장치를 구성 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-181">Follow hello steps in [What does Azure Multi-Factor Authentication mean for me?](./end-user/multi-factor-authentication-end-user.md) toounderstand and properly configure your devices for MFA with your user account.</span></span>

## <a name="install-and-configure-nps-extension"></a><span data-ttu-id="86307-182">NPS 확장 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="86307-182">Install and configure NPS extension</span></span>
<span data-ttu-id="86307-183">이 섹션에서는 원격 데스크톱 게이트웨이 hello로 클라이언트 인증을 위해 RDS 인프라 toouse Azure MFA를 구성 하기 위한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-183">This section provides instructions for configuring RDS infrastructure toouse Azure MFA for client authentication with hello Remote Desktop Gateway.</span></span>

### <a name="acquire-azure-active-directory-guid-id"></a><span data-ttu-id="86307-184">Azure Active Directory GUID ID 얻기</span><span class="sxs-lookup"><span data-stu-id="86307-184">Acquire Azure Active Directory GUID ID</span></span>

<span data-ttu-id="86307-185">Hello NPS 확장의 hello 구성의 일환으로, Azure AD 테 넌 트에 대 한 toosupply 관리자 자격 증명와 hello Azure AD ID가 필요 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-185">As part of hello configuration of hello NPS extension, you need toosupply admin credentials and hello Azure AD ID for your Azure AD tenant.</span></span> <span data-ttu-id="86307-186">단계를 수행 하는 hello 알려주는 tooget hello 테 넌 트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-186">hello following steps show you how tooget hello tenant ID.</span></span>

1. <span data-ttu-id="86307-187">Toohello 로그인 [Azure 포털](https://portal.azure.com) 테 넌 트 hello Azure의 hello 전역 관리자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-187">Sign in toohello [Azure portal](https://portal.azure.com) as hello global administrator of hello Azure tenant.</span></span>
2. <span data-ttu-id="86307-188">왼쪽 탐색 hello, 선택 hello **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-188">In hello left navigation, select hello **Azure Active Directory** icon.</span></span>
3. <span data-ttu-id="86307-189">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-189">Select **Properties**.</span></span>
4. <span data-ttu-id="86307-190">Hello 디렉터리 ID 옆에 있는 hello 속성 블레이드 클릭 hello **복사** toocopy hello ID tooclipboard 아래와 같이 아이콘을 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-190">In hello Properties blade, beside hello Directory ID, click hello **Copy** icon, as shown below, toocopy hello ID tooclipboard.</span></span>

 ![properties](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a><span data-ttu-id="86307-192">Hello NPS 확장 설치</span><span class="sxs-lookup"><span data-stu-id="86307-192">Install hello NPS extension</span></span>
<span data-ttu-id="86307-193">Hello NPS 확장 hello 네트워크 정책 및 액세스 서비스 (NPS) 역할이 설치 되어 있는 서버에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-193">Install hello NPS extension on a server that has hello Network Policy and Access Services (NPS) role installed.</span></span> <span data-ttu-id="86307-194">이 설계에 대 한 hello RADIUS 서버로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-194">This functions as hello RADIUS server for your design.</span></span> 

>[!Important]
> <span data-ttu-id="86307-195">원격 데스크톱 게이트웨이 서버의 hello NPS 확장을 설치 하지 않으면 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-195">Be sure you do not install hello NPS extension on your Remote Desktop Gateway server.</span></span>
> 

1. <span data-ttu-id="86307-196">Hello 다운로드 [NPS 확장](https://aka.ms/npsmfa)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-196">Download hello [NPS extension](https://aka.ms/npsmfa).</span></span> 
2. <span data-ttu-id="86307-197">Hello 설치 프로그램 실행 파일 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-197">Copy hello setup executable file (NpsExtnForAzureMfaInstaller.exe) toohello NPS server.</span></span>
3. <span data-ttu-id="86307-198">Hello NPS 서버에서 두 번 클릭 **NpsExtnForAzureMfaInstaller.exe**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-198">On hello NPS server, double-click **NpsExtnForAzureMfaInstaller.exe**.</span></span> <span data-ttu-id="86307-199">메시지가 표시되면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-199">If prompted, click **Run**.</span></span>
4. <span data-ttu-id="86307-200">NPS 확장 Azure MFA 대화 상자에 대 한 hello, hello 소프트웨어 사용 조건 검토 확인 **toohello 사용 약관 동의**를 클릭 하 고 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-200">In hello NPS Extension for Azure MFA dialog box, review hello software license terms, check **I agree toohello license terms and conditions**, and click **Install**.</span></span>
 
  ![Azure MFA 설치](./media/nps-extension-remote-desktop-gateway/image2.png)

5. <span data-ttu-id="86307-202">Azure MFA 대화 상자에 대 한 hello NPS 확장에서에서 닫기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-202">In hello NPS Extension for Azure MFA dialog box, click Close.</span></span> 

  ![Azure MFA용 NPS 확장](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a><span data-ttu-id="86307-204">PowerShell 스크립트를 사용 하 여 hello NPS 확장으로 사용 하기 위해 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="86307-204">Configure certificates for use with hello NPS extension using a PowerShell script</span></span>
<span data-ttu-id="86307-205">다음으로 hello NPS 확장 tooensure 보안 통신 및 보증에서 사용 하기 위해 tooconfigure 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-205">Next, you need tooconfigure certificates for use by hello NPS extension tooensure secure communications and assurance.</span></span> <span data-ttu-id="86307-206">hello NPS 구성 요소에는 NPS와 함께 사용 하기 위해 자체 서명 된 인증서를 구성 하는 Windows PowerShell 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-206">hello NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="86307-207">hello 스크립트 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-207">hello script performs hello following actions:</span></span>

* <span data-ttu-id="86307-208">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="86307-208">Creates a self-signed certificate</span></span>
* <span data-ttu-id="86307-209">Azure AD에서 사용자 인증서 tooservice의 공개 키를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-209">Associates public key of certificate tooservice principal on Azure AD</span></span>
* <span data-ttu-id="86307-210">저장소 hello hello 로컬 컴퓨터 저장소에서 인증서</span><span class="sxs-lookup"><span data-stu-id="86307-210">Stores hello cert in hello local machine store</span></span>
* <span data-ttu-id="86307-211">Toohello 인증서의 개인 키 toohello 네트워크 사용자 액세스 부여</span><span class="sxs-lookup"><span data-stu-id="86307-211">Grants access toohello certificate’s private key toohello network user</span></span>
* <span data-ttu-id="86307-212">네트워크 정책 서버 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="86307-212">Restarts Network Policy Server service</span></span>

<span data-ttu-id="86307-213">자체 인증서 toouse 하려는 경우 Azure AD에서 tooassociate hello 공용 인증서 toohello 서비스 원칙의 필요 하 고 등입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-213">If you want toouse your own certificates, you need tooassociate hello public of your certificate toohello service principle on Azure AD, and so on.</span></span>

<span data-ttu-id="86307-214">toouse hello 스크립트는 Azure AD 관리자 자격 증명에 hello 확장을 제공 하 고 앞에서 복사한 Azure AD 테 넌 트 ID hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-214">toouse hello script, provide hello extension with your Azure AD Admin credentials and hello Azure AD tenant ID that you copied earlier.</span></span> <span data-ttu-id="86307-215">Hello NPS 확장 설치 위치는 각 NPS 서버에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-215">Run hello script on each NPS server where you installed hello NPS extension.</span></span> <span data-ttu-id="86307-216">그런 다음 않습니다 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="86307-216">Then do hello following:</span></span>

1. <span data-ttu-id="86307-217">관리 Windows PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="86307-217">Open an administrative Windows PowerShell prompt.</span></span>
2. <span data-ttu-id="86307-218">Hello PowerShell 프롬프트에서 입력 **cd 'c:\Program Files\Microsoft\AzureMfa\Config'**, 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-218">At hello PowerShell prompt, type **cd ‘c:\Program Files\Microsoft\AzureMfa\Config’**, and press **ENTER**.</span></span>
3. <span data-ttu-id="86307-219">_.\AzureMfsNpsExtnConfigSetup.ps1_을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="86307-219">Type _.\AzureMfsNpsExtnConfigSetup.ps1_, and press **ENTER**.</span></span> <span data-ttu-id="86307-220">hello 스크립트 hello Azure Active Directory PowerShell 모듈 설치 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-220">hello script checks toosee if hello Azure Active Directory PowerShell module is installed.</span></span> <span data-ttu-id="86307-221">설치 되어 있지 않으면 hello 스크립트 hello 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-221">If not installed, hello script installs hello module for you.</span></span>

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. <span data-ttu-id="86307-223">Hello PowerShell 모듈의 hello 설치를 확인 하는 hello 스크립트, 후 hello Azure Active Directory PowerShell 모듈 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-223">After hello script verifies hello installation of hello PowerShell module, it displays hello Azure Active Directory PowerShell module dialog box.</span></span> <span data-ttu-id="86307-224">Hello 대화 상자에서 Azure AD 관리자 자격 증명 및 암호를 입력 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-224">In hello dialog box, enter your Azure AD admin credentials and password, and click **Sign In**.</span></span>

  ![Powershell 계정 열기](./media/nps-extension-remote-desktop-gateway/image5.png)

5. <span data-ttu-id="86307-226">대화 상자가 나타나면 toohello 클립보드를 앞에서 복사한 hello 테 넌 트 ID를 붙여 넣고 키를 눌러 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-226">When prompted, paste hello tenant ID you copied toohello clipboard earlier, and press **ENTER**.</span></span>

  ![테넌트 ID 입력](./media/nps-extension-remote-desktop-gateway/image6.png)

6. <span data-ttu-id="86307-228">hello 스크립트 자체 서명 된 인증서를 만들고 다른 구성 변경 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-228">hello script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="86307-229">아래에 표시 된 hello 이미지와 같이 hello 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-229">hello output should be like hello image shown below.</span></span>

  ![자체 서명된 인증서](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a><span data-ttu-id="86307-231">원격 데스크톱 게이트웨이에서 NPS 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="86307-231">Configure NPS components on Remote Desktop Gateway</span></span>
<span data-ttu-id="86307-232">이 섹션에서는 hello 원격 데스크톱 게이트웨이 연결 권한 부여 정책 및 기타 RADIUS 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-232">In this section, you configure hello Remote Desktop Gateway connection authorization policies and other RADIUS settings.</span></span>

<span data-ttu-id="86307-233">hello 인증 흐름에 RADIUS 메시지 hello 원격 데스크톱 게이트웨이 및 hello NPS 서버 hello NPS 서버를 설치한 간에 교환 될 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-233">hello authentication flow requires that RADIUS messages be exchanged between hello Remote Desktop Gateway and hello NPS server where hello NPS Server is installed.</span></span> <span data-ttu-id="86307-234">즉, hello NPS 확장이 설치 되어 있는 원격 데스크톱 게이트웨이 및 hello 모두 NPS 서버의 RADIUS 클라이언트 설정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-234">This means that you must configure RADIUS client settings on both Remote Desktop Gateway and hello NPS server where hello NPS extension is installed.</span></span> 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a><span data-ttu-id="86307-235">원격 데스크톱 게이트웨이 연결 권한 부여 정책 toouse 중앙 저장소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-235">Configure Remote Desktop Gateway connection authorization policies toouse central store</span></span>
<span data-ttu-id="86307-236">원격 데스크톱 연결 권한 부여 정책 (RD Cap)에 연결 tooa 원격 데스크톱 게이트웨이 서버에 대 한 hello 요구 사항을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-236">Remote Desktop connection authorization policies (RD CAPs) specify hello requirements for connecting tooa Remote Desktop Gateway server.</span></span> <span data-ttu-id="86307-237">RD CAP는 로컬로(기본값) 저장하거나 NPS를 실행하는 중앙 RD CAP 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-237">RD CAPs can be stored locally (default) or they can be stored in a central RD CAP store that is running NPS.</span></span> <span data-ttu-id="86307-238">RDS와 Azure mfa tooconfigure 통합, 중앙 저장소의 toospecify hello 사용을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-238">tooconfigure integration of Azure MFA with RDS, you need toospecify hello use of a central store.</span></span>

1. <span data-ttu-id="86307-239">Hello RD 게이트웨이 서버에서 엽니다 **서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-239">On hello RD Gateway server, open **Server Manager**.</span></span> 
2. <span data-ttu-id="86307-240">Hello 메뉴를 클릭 **도구**, 너무 가리킨**원격 데스크톱 서비스**, 클릭 하 고 **원격 데스크톱 게이트웨이 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-240">On hello menu, click **Tools**, point too**Remote Desktop Services**, and then click **Remote Desktop Gateway Manager**.</span></span>

  ![원격 데스크톱 서비스](./media/nps-extension-remote-desktop-gateway/image8.png)

3. <span data-ttu-id="86307-242">RD 게이트웨이 관리자 hello 단추로 클릭 하 고  **\[서버 이름\] (Local)**를 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-242">In hello RD Gateway Manger, right-click **\[Server Name\] (Local)**, and click **Properties**.</span></span>

  ![서버 이름](./media/nps-extension-remote-desktop-gateway/image9.png)

4. <span data-ttu-id="86307-244">Hello 속성 대화 상자에서 선택 hello **RD CAP** 저장소 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-244">In hello Properties dialog box, select hello **RD CAP** Store tab.</span></span>
5. <span data-ttu-id="86307-245">Hello RD CAP 저장소 탭에서 선택 **NPS를 실행 하는 중앙 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-245">On hello RD CAP Store tab, select **Central Server running NPS**.</span></span> 
6. <span data-ttu-id="86307-246">Hello에 **NPS를 실행 하는 hello 서버에 대 한 이름 또는 IP 주소를 입력** 필드 이름을 입력 합니다 hello IP 주소 또는 서버 hello 서버 hello NPS 확장을 설치 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-246">In hello **Enter a name or IP address for hello server running NPS** field, type hello IP address or server name of hello server where you installed hello NPS extension.</span></span>

  ![이름 또는 IP 주소 입력](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. <span data-ttu-id="86307-248">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-248">Click **Add**.</span></span>
8. <span data-ttu-id="86307-249">Hello에 **공유 암호** 대화 상자에서 공유 암호를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-249">In hello **Shared Secret** dialog box, enter a shared secret, and then click **OK**.</span></span> <span data-ttu-id="86307-250">이 공유 암호 기록 hello 레코드를 안전 하 게 저장 및 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-250">Ensure you record this shared secret and store hello record securely.</span></span>

 >[!NOTE]
 ><span data-ttu-id="86307-251">공유 암호는 hello RADIUS 서버와 클라이언트 간의 tooestablish 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-251">Shared secret is used tooestablish trust between hello RADIUS servers and clients.</span></span> <span data-ttu-id="86307-252">길고 복잡한 암호를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="86307-252">Create a long and complex password.</span></span>
 >

 ![공유 비밀](./media/nps-extension-remote-desktop-gateway/image11.png)

9. <span data-ttu-id="86307-254">클릭 **확인** tooclose hello 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="86307-254">Click **OK** tooclose hello dialog box.</span></span>

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a><span data-ttu-id="86307-255">원격 데스크톱 게이트웨이 NPS에서 RADIUS 시간 제한 값 구성</span><span class="sxs-lookup"><span data-stu-id="86307-255">Configure RADIUS timeout value on Remote Desktop Gateway NPS</span></span>
<span data-ttu-id="86307-256">tooensure 있습니다 toovalidate 사용자의 자격 증명을 시간, 2 단계 인증을 수행 하 고, 응답을 수신 되어 tooRADIUS 메시지 응답, 필요한 tooadjust hello RADIUS 제한 시간 값입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-256">tooensure there is time toovalidate users’ credentials, perform two-step verification, receive responses, and respond tooRADIUS messages, it is necessary tooadjust hello RADIUS timeout value.</span></span>

1. <span data-ttu-id="86307-257">Hello RD 게이트웨이 서버에서 서버 관리자에서 **도구**, 클릭 하 고 **네트워크 정책 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-257">On hello RD Gateway server, in Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
2. <span data-ttu-id="86307-258">Hello에 **NPS (로컬)** 콘솔에서 **RADIUS 클라이언트 및 서버**를 선택 하 고 **원격 RADIUS 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-258">In hello **NPS (Local)** console, expand **RADIUS Clients and Servers**, and select **Remote RADIUS Server**.</span></span>

 ![원격 RADIUS 서버](./media/nps-extension-remote-desktop-gateway/image12.png)

3. <span data-ttu-id="86307-260">Hello 세부 정보 창에서 두 번 클릭 **TS 게이트웨이 서버 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-260">In hello details pane, double-click **TS GATEWAY SERVER GROUP**.</span></span>

 >[!NOTE]
 ><span data-ttu-id="86307-261">NPS 정책에 대 한 hello 중앙 서버를 구성할 때이 RADIUS 서버 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-261">This RADIUS Server Group was created when you configured hello central server for NPS policies.</span></span> <span data-ttu-id="86307-262">RD 게이트웨이 hello hello 그룹에서 1 보다 큰 경우 RADIUS 메시지 toothis 서버 또는 서버 그룹에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-262">hello RD Gateway forwards RADIUS messages toothis server or group of servers, if more than one in hello group.</span></span>
 >

4. <span data-ttu-id="86307-263">Hello에 **TS 게이트웨이 서버 그룹 속성** 대화 상자, 선택 hello IP 주소 또는 toostore RD Cap를 구성한 NPS 서버 hello 및 클릭 한 다음 이름을 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-263">In hello **TS GATEWAY SERVER GROUP Properties** dialog box, select hello IP address or name of hello NPS server you configured toostore RD CAPs, and then click **Edit**.</span></span> 

 ![TS 게이트웨이 서버 그룹](./media/nps-extension-remote-desktop-gateway/image13.png)

5. <span data-ttu-id="86307-265">Hello에 **RADIUS 서버 편집** 대화 상자, 선택 hello **부하 분산** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-265">In hello **Edit RADIUS Server** dialog box, select hello **Load Balancing** tab.</span></span>
6. <span data-ttu-id="86307-266">Hello에 **부하 분산** hello 탭 **시간 (초) 요청이 것으로 간주 되기 전에 응답 없이 삭제** 필드, 30-60 초 사이 tooa 값 3에서 hello 기본값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-266">In hello **Load Balancing** tab, in hello **Number of seconds without response before request is considered dropped** field, change hello default value from 3 tooa value between 30 and 60 seconds.</span></span>
7. <span data-ttu-id="86307-267">Hello에 **서버가 사용할 수 없는 상태로 표시 된 경우 요청 사이의 시간 (초)** 필드 같으면 tooor hello 이전 단계에서 지정한 hello 값 보다 큰은 30 초 tooa 값의 hello 기본 값을 변경 하세요.</span><span class="sxs-lookup"><span data-stu-id="86307-267">In hello **Number of seconds between requests when server is identified as unavailable** field, change hello default value of 30 seconds tooa value that is equal tooor greater than hello value you specified in hello previous step.</span></span>

 ![Radius 서버 편집](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  <span data-ttu-id="86307-269">Tooclose hello 대화 상자에 시간 2 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-269">Click OK two times tooclose hello dialog boxes.</span></span>

### <a name="verify-connection-request-policies"></a><span data-ttu-id="86307-270">연결 요청 정책 확인</span><span class="sxs-lookup"><span data-stu-id="86307-270">Verify Connection Request Policies</span></span> 
<span data-ttu-id="86307-271">기본적으로 hello RD 게이트웨이 toouse 연결 권한 부여 정책에 대 한 중앙 정책 저장소를 구성 하는 경우 hello RD 게이트웨이 구성 된 tooforward CAP 요청 toohello NPS 서버는 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-271">By default, when you configure hello RD Gateway toouse a central policy store for connection authorization policies, hello RD Gateway is configured tooforward CAP requests toohello NPS server.</span></span> <span data-ttu-id="86307-272">hello Azure MFA 확장명이 hello NPS 서버 설치 프로세스 hello RADIUS 액세스 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-272">hello NPS server with hello Azure MFA extension installed, processes hello RADIUS access request.</span></span> <span data-ttu-id="86307-273">단계를 수행 하는 hello 정책 tooverify hello 기본 연결을 요청 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86307-273">hello following steps show you how tooverify hello default connection request policy.</span></span> 

1. <span data-ttu-id="86307-274">RD 게이트웨이 hello hello NPS (로컬) 콘솔에서 확장 **정책**를 선택 하 고 **연결 요청 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-274">On hello RD Gateway, in hello NPS (Local) console, expand **Policies**, and select **Connection Request Policies**.</span></span>
2. <span data-ttu-id="86307-275">**연결 요청 정책**을 마우스 오른쪽 단추로 클릭하고 **TS 게이트웨이 권한 부여 정책**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-275">Right-click **Connect Request Policies**, and double-click **TS GATEWAY AUTHORIZATION POLICY**.</span></span>
3. <span data-ttu-id="86307-276">Hello에 **TS 게이트웨이 권한 부여 정책 속성** 대화 상자를 클릭 hello **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-276">In hello **TS GATEWAY AUTHORIZATION POLICY properties** dialog box, click hello **Settings** tab.</span></span>
4. <span data-ttu-id="86307-277">**설정** 탭의 [연결 요청 전달]에서 **인증**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-277">On **Settings** tab, under Forwarding Connection Request, click **Authentication**.</span></span> <span data-ttu-id="86307-278">RADIUS 클라이언트는 인증에 대 한 구성 된 tooforward 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-278">RADIUS client is configured tooforward requests for authentication.</span></span>

 ![인증 설정](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. <span data-ttu-id="86307-280">**취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-280">Click **Cancel**.</span></span> 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a><span data-ttu-id="86307-281">Hello NPS 확장이 설치 되어 있는 hello 서버의 NPS를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-281">Configure NPS on hello server where hello NPS extension is installed</span></span>
<span data-ttu-id="86307-282">hello NPS 서버 hello NPS 확장 hello NPS 서버에 원격 데스크톱 게이트웨이 hello 사용 하 여 설치 된 요구 toobe 수 tooexchange RADIUS 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-282">hello NPS server where hello NPS extension is installed needs toobe able tooexchange RADIUS messages with hello NPS server on hello Remote Desktop Gateway.</span></span> <span data-ttu-id="86307-283">이 메시지를 교환 tooenable, hello NPS 확장 서비스를 설치한 hello 서버의 tooconfigure hello NPS 구성 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-283">tooenable this message exchange, you need tooconfigure hello NPS components on hello server where hello NPS extension service is installed.</span></span> 

### <a name="register-server-in-active-directory"></a><span data-ttu-id="86307-284">Active Directory에 서버 등록</span><span class="sxs-lookup"><span data-stu-id="86307-284">Register Server in Active Directory</span></span>
<span data-ttu-id="86307-285">이 시나리오에서 제대로 toofunction, NPS 서버 hello toobe Active Directory에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-285">toofunction properly in this scenario, hello NPS server needs toobe registered in Active Directory.</span></span>

1. <span data-ttu-id="86307-286">**서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="86307-286">Open **Server Manager**.</span></span>
2. <span data-ttu-id="86307-287">[서버 관리자]에서 **도구**를 클릭한 다음 **네트워크 정책 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-287">In Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
3. <span data-ttu-id="86307-288">Hello 네트워크 정책 서버 콘솔에서 마우스 오른쪽 단추로 클릭 **NPS (로컬)**, 클릭 하 고 **Active Directory에 등록 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-288">In hello Network Policy Server console, right-click **NPS (Local)**, and then click **Register server in Active Directory**.</span></span> 
4. <span data-ttu-id="86307-289">**확인**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-289">Click **OK** two times.</span></span>

 ![AD에 서버 등록](./media/nps-extension-remote-desktop-gateway/image16.png)

5. <span data-ttu-id="86307-291">Hello 콘솔을 hello 다음 절차에 대 한 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="86307-291">Leave hello console open for hello next procedure.</span></span>

### <a name="create-and-configure-radius-client"></a><span data-ttu-id="86307-292">RADIUS 클라이언트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="86307-292">Create and configure RADIUS client</span></span> 
<span data-ttu-id="86307-293">원격 데스크톱 게이트웨이 hello toobe RADIUS 클라이언트 toohello NPS 서버를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-293">hello Remote Desktop Gateway needs toobe configured as a RADIUS client toohello NPS server.</span></span> 

1. <span data-ttu-id="86307-294">Hello에 hello NPS 확장이 설치 되어 hello NPS 서버 **NPS (로컬)** 콘솔 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트** 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-294">On hello NPS server where hello NPS extension is installed, in hello **NPS (Local)** console, right-click **RADIUS Clients** and click **New**.</span></span>

 ![새 RADIUS 클라이언트](./media/nps-extension-remote-desktop-gateway/image17.png)

2. <span data-ttu-id="86307-296">Hello에 **새 RADIUS 클라이언트** 대화 상자를 같은 친숙 한 이름을 제공 _게이트웨이_, hello hello 원격 데스크톱 게이트웨이 서버의 DNS 이름 또는 IP 주소 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-296">In hello **New RADIUS client** dialog box, provide a friendly name, such as _Gateway_, and hello IP address or DNS name of hello Remote Desktop Gateway server.</span></span> 
3. <span data-ttu-id="86307-297">Hello에 **공유 암호** 및 hello **공유 암호 확인** 필드 입력 hello 이전에 사용한 동일한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-297">In hello **Shared secret** and hello **Confirm shared secret** fields, enter hello same secret that you used before.</span></span>

 ![이름 및 주소](./media/nps-extension-remote-desktop-gateway/image18.png)

4. <span data-ttu-id="86307-299">클릭 **확인** tooclose hello 새 RADIUS 클라이언트 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="86307-299">Click **OK** tooclose hello New RADIUS client dialog box.</span></span>

### <a name="configure-network-policy"></a><span data-ttu-id="86307-300">네트워크 정책 구성</span><span class="sxs-lookup"><span data-stu-id="86307-300">Configure Network Policy</span></span>
<span data-ttu-id="86307-301">Azure MFA 확장 hello로 회수 hello NPS 서버는 hello 연결 권한 부여 정책 (CAP)에 대 한 hello 지정 된 중앙 정책 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-301">Recall hello NPS server with hello Azure MFA extension is hello designated central policy store for hello Connection Authorization Policy (CAP).</span></span> <span data-ttu-id="86307-302">따라서 hello NPS 서버 tooauthorize 유효한 연결 요청에 CAP tooimplement을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-302">Therefore, you need tooimplement a CAP on hello NPS server tooauthorize valid connections requests.</span></span>  

1. <span data-ttu-id="86307-303">Hello NPS (로컬) 콘솔에서 확장 **정책**를 클릭 하 고 **네트워크 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-303">In hello NPS (Local) console, expand **Policies**, and click **Network Policies**.</span></span>
2. <span data-ttu-id="86307-304">마우스 오른쪽 단추로 클릭 **연결 tooother 액세스 서버**를 클릭 하 고 **정책 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-304">Right-click **Connections tooother access servers**, and click **Duplicate policy**.</span></span> 

 ![중복된 정책](./media/nps-extension-remote-desktop-gateway/image19.png)

3. <span data-ttu-id="86307-306">마우스 오른쪽 단추로 클릭 **연결 복사본 tooother 액세스 서버**를 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-306">Right-click **Copy of Connections tooother access servers**, and click **Properties**.</span></span>

 ![네트워크 속성](./media/nps-extension-remote-desktop-gateway/image20.png)

4. <span data-ttu-id="86307-308">Hello에 **연결 복사본 tooother 액세스 서버** 대화 상자, 정책 이름에 적합 한 이름 같은 입력 **RDG_CAP**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-308">In hello **Copy of Connections tooother access servers** dialog box, in Policy Name, enter a suitable name, such as **RDG_CAP**.</span></span> <span data-ttu-id="86307-309">**정책 사용**을 선택하고 **액세스 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-309">Check **Policy Enabled**, and select **Grant access**.</span></span> <span data-ttu-id="86307-310">필요에 따라 네트워크 액세스 형식에서 **원격 데스크톱 게이트웨이**를 선택하거나 **지정되지 않음**으로 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-310">Optionally, in Type of network access, select **Remote Desktop Gateway**, or you can leave it as **Unspecified**.</span></span>

 ![연결 복사본](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  <span data-ttu-id="86307-312">Hello 클릭 **제약 조건을** 탭을 확인 **인증 방법을 협상 하지 않고 허용 클라이언트 tooconnect**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-312">Click hello **Constraints** tab, and check **Allow clients tooconnect without negotiating an authentication method**.</span></span>

 ![클라이언트가 허용 tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. <span data-ttu-id="86307-314">필요에 따라 hello 클릭 **조건** 탭 및 hello 연결 toobe 권한이, 예를 들어 특정 Windows 그룹 멤버 자격에 대해 충족 해야 하는 조건을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-314">Optionally, click hello **Conditions** tab and add conditions that must be met for hello connection toobe authorized, for example, membership in a specific Windows group.</span></span>

 ![조건](./media/nps-extension-remote-desktop-gateway/image23.png)

7. <span data-ttu-id="86307-316">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-316">Click **OK**.</span></span> <span data-ttu-id="86307-317">입력 정보 요청된 tooview hello 해당 하는 도움말 항목을 클릭 하 여 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-317">When prompted tooview hello corresponding Help topic, click **No**.</span></span>
8. <span data-ttu-id="86307-318">액세스 부여 하는 것이 고 hello hello 정책을 사용 하는 hello 목록 위쪽에 새 정책 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-318">Ensure that your new policy is at hello top of hello list, that hello policy is enabled, and that it grants access.</span></span>

 ![네트워크 정책](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a><span data-ttu-id="86307-320">구성 확인</span><span class="sxs-lookup"><span data-stu-id="86307-320">Verify configuration</span></span>
<span data-ttu-id="86307-321">tooverify hello 구성 해야 toolog 원격 데스크톱 게이트웨이 hello에 적합 한 RDP 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-321">tooverify hello configuration, you need toolog on hello Remote Desktop Gateway with a suitable RDP client.</span></span> <span data-ttu-id="86307-322">있는지 toouse 연결 권한 부여 정책에서 허용 하 고 Azure MFA에 대해 사용 하도록 설정 하는 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-322">Be sure toouse an account that is allowed by your Connection Authorization Policies and is enabled for Azure MFA.</span></span> 

<span data-ttu-id="86307-323">Hello 이미지 아래에 표시를 사용 하 여 hello **원격 데스크톱 웹 액세스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="86307-323">As show in hello image below, you can use hello **Remote Desktop Web Access** page.</span></span>

![원격 데스크톱 웹 액세스](./media/nps-extension-remote-desktop-gateway/image25.png)

<span data-ttu-id="86307-325">기본 인증을 위해 자격 증명 입력을 시 hello 원격 데스크톱 연결 대화 상자 아래와 같이 원격 연결을 초기화 하는 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-325">Upon successfully entering your credentials for primary authentication, hello Remote Desktop Connect dialog box shows a status of Initiating remote connection, as shown below.</span></span> 

<span data-ttu-id="86307-326">Azure MFA에서 이전에 구성한 hello 보조 인증 방법으로 성공적으로 인증 하는 경우 연결 된 toohello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-326">If you successfully authenticate with hello secondary authentication method you previously configured in Azure MFA, you are connected toohello resource.</span></span> <span data-ttu-id="86307-327">그러나 hello 보조 인증 실패할 경우 tooresource 액세스를 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-327">However, if hello secondary authentication is not successful, you are denied access tooresource.</span></span> 

![원격 연결 시작](./media/nps-extension-remote-desktop-gateway/image26.png)

<span data-ttu-id="86307-329">Hello 인증자 아래 hello 예제에서 Windows phone에서 앱 인증이 사용 되는 tooprovide hello 보조 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-329">In hello example below, hello Authenticator app on a Windows phone is used tooprovide hello secondary authentication.</span></span>

![계정](./media/nps-extension-remote-desktop-gateway/image27.png)

<span data-ttu-id="86307-331">Hello 보조 인증 방법을 사용 하 여 인증 성공적으로 면 hello 원격 데스크톱 게이트웨이 정상적으로 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-331">Once you have successfully authenticated using hello secondary authentication method, you are logged into hello Remote Desktop Gateway as normal.</span></span> <span data-ttu-id="86307-332">그러나 필요한 toouse 신뢰할 수 있는 장치에서 모바일 앱을 사용 하 여 보조 인증 방법 이므로, hello 로그인 프로세스는 그렇지 않은 경우 복구할 때 보다 더 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-332">However, because you are required toouse a secondary authentication method using a mobile app on a trusted device, hello log-in process is more secure than it would be otherwise.</span></span>

### <a name="view-event-viewer-logs-for-successful-logon-events"></a><span data-ttu-id="86307-333">성공적인 로그온 이벤트에 대한 이벤트 뷰어 로그 보기</span><span class="sxs-lookup"><span data-stu-id="86307-333">View Event Viewer logs for successful logon events</span></span>
<span data-ttu-id="86307-334">tooview hello 성공적인 로그인 이벤트 hello Windows 이벤트 뷰어 로그에서 다음 Windows PowerShell 명령 tooquery hello Windows 터미널 서비스 및 Windows 보안 로그 hello를 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-334">tooview hello successful sign-in events in hello Windows Event Viewer logs, you can issue hello following Windows PowerShell command tooquery hello Windows Terminal Services and Windows Security logs.</span></span>

<span data-ttu-id="86307-335">tooquery 성공적인 로그인 이벤트 hello 게이트웨이 작업 로그에서 _(이벤트 뷰어 \ 응용 프로그램 및 서비스 Logs\Microsoft\Windows\TerminalServices Gateway\Operational_, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="86307-335">tooquery successful sign-in events in hello Gateway operational logs _(Event Viewer\Applications and Services Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, use hello following commands:</span></span>

* <span data-ttu-id="86307-336">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL</span><span class="sxs-lookup"><span data-stu-id="86307-336">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL</span></span> 
* <span data-ttu-id="86307-337">이 명령은 hello 사용자 리소스 권한 부여 정책 요구 사항을 RD RAP ()을 충족 하 고 액세스 권한이 부여 되었습니다 표시 하는 Windows 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-337">This command displays Windows events that show hello user met resource authorization policy requirements (RD RAP) and was granted access.</span></span>

![이벤트 뷰어 보기](./media/nps-extension-remote-desktop-gateway/image28.png)

* <span data-ttu-id="86307-339">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL</span><span class="sxs-lookup"><span data-stu-id="86307-339">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL</span></span>
* <span data-ttu-id="86307-340">이 명령은 사용자 연결 권한 부여 정책 요구 사항을 충족 하는 경우를 보여 주는 hello 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-340">This command displays hello events that show when user met connection authorization policy requirements.</span></span>

![연결 권한 부여](./media/nps-extension-remote-desktop-gateway/image29.png)

<span data-ttu-id="86307-342">또한 이 로그를 보고 300 및 200 이벤트 ID에서 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-342">You can also view this log and filter on event IDs, 300 and 200.</span></span> <span data-ttu-id="86307-343">tooquery 성공 로그온 이벤트 hello 보안 이벤트 뷰어 로그에서 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-343">tooquery successful logon events in hello Security event viewer logs, use hello following command:</span></span>

* <span data-ttu-id="86307-344">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="86307-344">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span> 
* <span data-ttu-id="86307-345">이 명령은 실행할 수 중앙 NPS hello 또는 RD 게이트웨이 서버를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-345">This command can be run on either hello central NPS or hello RD Gateway Server.</span></span> 

![성공적인 로그온 이벤트](./media/nps-extension-remote-desktop-gateway/image30.png)

<span data-ttu-id="86307-347">아래와 같이 hello 보안 로그 또는 네트워크 정책 및 액세스 서비스 사용자 지정 보기 hello도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-347">You can also view hello Security log or hello Network Policy and Access Services custom view, as shown below:</span></span>

![네트워크 정책 및 액세스 서비스](./media/nps-extension-remote-desktop-gateway/image31.png)

<span data-ttu-id="86307-349">Azure MFA에 대 한 hello NPS 확장을 설치한 hello 서버에서 찾을 수 있습니다 이벤트 뷰어 응용 프로그램 로그에서 특정 toohello 확장 _응용 프로그램 및 서비스 Logs\Microsoft\AzureMfa_합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-349">On hello server where you installed hello NPS extension for Azure MFA, you can find Event Viewer application logs specific toohello extension at _Application and Services Logs\Microsoft\AzureMfa_.</span></span> 

![이벤트 뷰어 응용 프로그램 로그](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="86307-351">문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="86307-351">Troubleshoot Guide</span></span>

<span data-ttu-id="86307-352">Hello 구성이 예상 대로 작동 하지 않는 경우 첫 번째 위치 toostart tootroubleshoot hello 경우 사용자 hello tooverify가 구성 된 toouse Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="86307-352">If hello configuration is not working as expected, hello first place toostart tootroubleshoot is tooverify that hello user is configured toouse Azure MFA.</span></span> <span data-ttu-id="86307-353">Hello 사용자 toohello 연결 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-353">Have hello user connect toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="86307-354">사용자가 보조 인증을 요청받았고 성공적으로 인증할 수 있으면 Azure MFA의 잘못된 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-354">If users are prompted for secondary verification and can successfully authenticate, you can eliminate an incorrect configuration of Azure MFA.</span></span>

<span data-ttu-id="86307-355">Azure MFA hello 사용자에 대해 작동 하 고 hello 관련 이벤트 로그를 검토 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-355">If Azure MFA is working for hello user(s), you should review hello relevant Event logs.</span></span> <span data-ttu-id="86307-356">여기에 hello 이전 섹션에서 설명 하는 hello 보안 이벤트, 운영, 게이트웨이 및 Azure MFA 로그 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86307-356">These include hello Security Event, Gateway operational, and Azure MFA logs that are discussed in hello previous section.</span></span> 

<span data-ttu-id="86307-357">다음은 실패한 로그온 이벤트(6273 이벤트 ID)를 보여 주는 보안 로그의 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-357">Below is an example output of Security log showing a failed logon event (Event ID 6273).</span></span>

![실패한 로그온 이벤트](./media/nps-extension-remote-desktop-gateway/image33.png)

<span data-ttu-id="86307-359">다음은 hello AzureMFA 로그에서 관련된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="86307-359">Below is a related event from hello AzureMFA logs:</span></span>

![Azure MFA 로그](./media/nps-extension-remote-desktop-gateway/image34.png)

<span data-ttu-id="86307-361">tooperform 고급 옵션을 참조 하 여 hello NPS 데이터베이스 형식 로그 파일 hello NPS 서비스를 설치한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-361">tooperform advanced troubleshoot options, consult hello NPS database format log files where hello NPS service is installed.</span></span> <span data-ttu-id="86307-362">이러한 로그 파일은 _%SystemRoot%\System32\Logs_ 폴더에 쉼표로 구분된 텍스트 파일로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="86307-362">These log files are created in _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> 

<span data-ttu-id="86307-363">이러한 로그 파일에 대한 자세한 내용은 [NPS 데이터베이스 형식 로그 파일 해석(영문)](https://technet.microsoft.com/library/cc771748.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86307-363">For a description of these log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> <span data-ttu-id="86307-364">이러한 로그 파일의 hello 항목 스프레드시트나 데이터베이스 가져오지 않고 어려운 toointerpret 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-364">hello entries in these log files can be difficult toointerpret without importing them into a spreadsheet or a database.</span></span> <span data-ttu-id="86307-365">여러 IAS 파서를 찾을 수 있습니다 온라인 tooassist 로그 파일을 hello 해석에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-365">You can find several IAS parsers online tooassist you in interpreting hello log files.</span></span> 

<span data-ttu-id="86307-366">hello 아래 이미지 출력을 보여 hello 하나의 같은 다운로드 가능한 [셰어웨어 응용 프로그램](http://www.deepsoftware.com/iasviewer)합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-366">hello image below shows hello output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer).</span></span> 

![셰어웨어 앱](./media/nps-extension-remote-desktop-gateway/image35.png)

<span data-ttu-id="86307-368">마지막으로 추가적인 문제 해결 옵션을 위해 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)와 같은 프로토콜 분석기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86307-368">Finally, for additional troubleshoot options, you can use a protocol analyzer, such [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> 

<span data-ttu-id="86307-369">hello Microsoft 메시지 분석기에서 아래 이미지 표시 hello 사용자 이름을 포함 하는 RADIUS 프로토콜을 필터링 하는 네트워크 트래픽을 **Contoso\AliceC**합니다.</span><span class="sxs-lookup"><span data-stu-id="86307-369">hello image below from Microsoft Message Analyzer shows network traffic filtered on RADIUS protocol that contains hello user name **Contoso\AliceC**.</span></span>

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a><span data-ttu-id="86307-371">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86307-371">Next steps</span></span>
[<span data-ttu-id="86307-372">어떻게 tooget Azure Multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="86307-372">How tooget Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-versions-plans.md)

[<span data-ttu-id="86307-373">RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버</span><span class="sxs-lookup"><span data-stu-id="86307-373">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](multi-factor-authentication-get-started-server-rdg.md)

[<span data-ttu-id="86307-374">Azure Active Directory와 온-프레미스 디렉터리 통합</span><span class="sxs-lookup"><span data-stu-id="86307-374">Integrate your on-premises directories with Azure Active Directory</span></span>](../active-directory/connect/active-directory-aadconnect.md)
