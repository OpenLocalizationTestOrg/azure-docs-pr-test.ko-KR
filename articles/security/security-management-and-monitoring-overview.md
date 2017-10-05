---
title: "Azure 보안 관리 및 모니터링 개요 | Microsoft Docs"
description: " Azure는 Azure 클라우드 서비스 및 가상 컴퓨터 관리 및 모니터링을 지원하기 위해 보안 메커니즘을 제공합니다.  이 문서에서는 이러한 핵심 보안 기능 및 서비스에 대한 개요를 제공합니다. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 6787877deabafd0b7308e190cb45b4036049b05b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a><span data-ttu-id="0c2a6-104">Azure 보안 관리 및 모니터링 개요</span><span class="sxs-lookup"><span data-stu-id="0c2a6-104">Azure Security Management and Monitoring Overview</span></span>
<span data-ttu-id="0c2a6-105">Azure는 Azure 클라우드 서비스 및 가상 컴퓨터 관리 및 모니터링을 지원하기 위해 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-105">Azure provides security mechanisms to aid in the management and monitoring of Azure cloud services and virtual machines.</span></span> <span data-ttu-id="0c2a6-106">이 문서에서는 이러한 핵심 보안 기능 및 서비스에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-106">This article provides an overview of these core security features and services.</span></span> <span data-ttu-id="0c2a6-107">문서에는 각 문서에 대한 세부 정보를 제공해 줄 링크가 제공되므로 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-107">Links are provided to articles that give details of each so you can learn more.</span></span>

<span data-ttu-id="0c2a6-108">Microsoft 클라우드 서비스의 보안은 사용자와 Microsoft 간의 파트너십과 공동 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-108">The security of your Microsoft cloud services is a partnership and shared responsibility between you and Microsoft.</span></span> <span data-ttu-id="0c2a6-109">공동 책임은 Microsoft가 Microsoft Azure와 해당 데이터 센터의 물리적 보안에 책임을 진다는 것을 의미합니다(잠금식 배지 출입구, 펜스 및 경비원 등의 보안 보호 조치 사용).</span><span class="sxs-lookup"><span data-stu-id="0c2a6-109">Shared responsibility means Microsoft is responsible for the Microsoft Azure and physical security of its data centers (by using security protections such as locked badge entry doors, fences, and guards).</span></span> <span data-ttu-id="0c2a6-110">또한 Azure는 까다로운 고객의 보안, 개인 정보 및 규정 준수 요구 사항을 충족하는 소프트웨어 계층에서 강력한 수준의 클라우드 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-110">In addition, Azure provides strong levels of cloud security at the software layer that meets the security, privacy, and compliance needs of its demanding customers.</span></span>

<span data-ttu-id="0c2a6-111">사용자는 데이터와 ID를 소유하고 있으며, 이들을 보호하고 온-프레미스 리소스의 보안, 제어할 수 있는 클라우드 구성 요소의 보안에 대한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-111">You own your data and identities, the responsibility for protecting them, the security of your on-premises resources, and the security of cloud components over which you have control.</span></span> <span data-ttu-id="0c2a6-112">Microsoft는 사용자에게 사용자의 데이터와 응용 프로그램을 보호하는 데 도움이 되는 보안 제어 및 기능을 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-112">Microsoft provides you with security controls and capabilities to help you protect your data and applications.</span></span> <span data-ttu-id="0c2a6-113">보안에 대한 사용자의 책임 정도는 클라우드 서비스의 형식에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-113">Your degree of responsibility for security is based on the type of cloud service.</span></span>

<span data-ttu-id="0c2a6-114">다음 차트에는 Microsoft와 고객 모두에 대한 책임의 균형이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-114">The following chart summarizes the balance of responsibility for both Microsoft and the customer.</span></span>

![공동 책임][1]

<span data-ttu-id="0c2a6-116">보안 관리에 대해 더 자세히 알아보려면 [Azure의 보안 관리](azure-security-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-116">For a deeper dive into security management, see [Security management in Azure](azure-security-management.md).</span></span>

<span data-ttu-id="0c2a6-117">다음은 이 문서에서 다루고 있는 핵심 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-117">Here are the core features to be covered in this article:</span></span>

* <span data-ttu-id="0c2a6-118">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="0c2a6-118">Role-Based Access Control</span></span>
* <span data-ttu-id="0c2a6-119">맬웨어 방지</span><span class="sxs-lookup"><span data-stu-id="0c2a6-119">Antimalware</span></span>
* <span data-ttu-id="0c2a6-120">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0c2a6-120">Multi-Factor Authentication</span></span>
* <span data-ttu-id="0c2a6-121">Express 경로</span><span class="sxs-lookup"><span data-stu-id="0c2a6-121">ExpressRoute</span></span>
* <span data-ttu-id="0c2a6-122">가상 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="0c2a6-122">Virtual network gateways</span></span>
* <span data-ttu-id="0c2a6-123">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="0c2a6-123">Privileged identity management</span></span>
* <span data-ttu-id="0c2a6-124">ID 보호</span><span class="sxs-lookup"><span data-stu-id="0c2a6-124">Identity protection</span></span>
* <span data-ttu-id="0c2a6-125">보안 센터</span><span class="sxs-lookup"><span data-stu-id="0c2a6-125">Security Center</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="0c2a6-126">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="0c2a6-126">Role-Based Access Control</span></span>
<span data-ttu-id="0c2a6-127">RBAC(역할 기반 액세스 제어)를 통해 Azure 리소스에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-127">Role-Based Access Control (RBAC) provides fine-grained access management for Azure resources.</span></span> <span data-ttu-id="0c2a6-128">RBAC를 사용하여 사용자에게 해당 작업을 수행하는 데 필요한 정도의 액세스 권한만 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-128">Using RBAC, you can grant people only the amount of access that they need to perform their jobs.</span></span>  <span data-ttu-id="0c2a6-129">또한 RBAC는 직원 퇴사 시 클라우드의 리소스에 대한 액세스 권한을 잃도록 해줄 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-129">RBAC can also help you ensure that when people leave the organization they lose access to resources in the cloud.</span></span>

<span data-ttu-id="0c2a6-130">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-130">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-131">RBAC의 Active Directory 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="0c2a6-131">Active Directory team blog on RBAC</span></span>](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [<span data-ttu-id="0c2a6-132">Azure 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="0c2a6-132">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a><span data-ttu-id="0c2a6-133">맬웨어 방지</span><span class="sxs-lookup"><span data-stu-id="0c2a6-133">Antimalware</span></span>
<span data-ttu-id="0c2a6-134">Azure를 통해 가상 컴퓨터를 악성 파일, 애드웨어 및 기타 위협으로부터 보호할 수 있도록 Microsoft, Symantec, Trend Micro, McAfee 및 Kaspersky 등의 주요 보안 공급업체의 맬웨어 방지 소프트웨어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-134">With Azure, you can use antimalware software from major security vendors such as Microsoft, Symantec, Trend Micro, McAfee, and Kaspersky to help protect your virtual machines from malicious files, adware, and other threats.</span></span>

<span data-ttu-id="0c2a6-135">Microsoft 맬웨어 방지는 PaaS 역할 및 가상 컴퓨터 모두에 대한 맬웨어 방지 에이전트를 설치할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-135">Microsoft Antimalware offers you the ability to install an antimalware agent for both PaaS roles and virtual machines.</span></span> <span data-ttu-id="0c2a6-136">System Center Endpoint Protection에 기반한 이 기능은 클라우드에 입증된 온-프레미스 보안 기술을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-136">Based on System Center Endpoint Protection, this feature brings proven on-premises security technology to the cloud.</span></span>

<span data-ttu-id="0c2a6-137">또한, Azure 플랫폼에서 Trend의 [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ 및 [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ 제품에 대한 심층적인 통합도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-137">We also offer deep integration for Trend’s [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ and [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ products in the Azure platform.</span></span> <span data-ttu-id="0c2a6-138">DeepSecurity는 바이러스 백신 솔루션이며 SecureCloud는 암호화 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-138">DeepSecurity is an Antivirus solution and SecureCloud is an encryption solution.</span></span> <span data-ttu-id="0c2a6-139">DeepSecurity는 확장 모델을 사용하여 VM 내부에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-139">DeepSecurity is deployed inside VMs using an extension model.</span></span> <span data-ttu-id="0c2a6-140">포털 UI 및 PowerShell을 사용하여 복제하려는 새 VM 내부의 DeepSecurity를 사용하거나 이미 배포된 기존 VM을 사용할지 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-140">Using the portal UI and PowerShell, you can choose to use DeepSecurity inside new VMs that are being spun up, or existing VMs that are already deployed.</span></span>

<span data-ttu-id="0c2a6-141">SEP(Symantec End Point Protection)도 Azure에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-141">Symantec End Point Protection (SEP) is also supported on Azure.</span></span> <span data-ttu-id="0c2a6-142">포털 통합을 통해 고객은 VM 내에서 SEP를 사용할지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-142">Through portal integration, customers can specify that they intend to use SEP within a VM.</span></span> <span data-ttu-id="0c2a6-143">SEP는 Azure Portal을 통해 완전 새로운 VM에 설치하거나 PowerShell을 사용하여 기존 VM에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-143">SEP can be installed on a brand new VM via the Azure portal or can be installed on an existing VM using PowerShell.</span></span>

<span data-ttu-id="0c2a6-144">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-144">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-145">Azure 가상 컴퓨터에 맬웨어 방지 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="0c2a6-145">Deploying Antimalware Solutions on Azure Virtual Machines</span></span>](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [<span data-ttu-id="0c2a6-146">Azure Cloud Services 및 가상 컴퓨터용 Microsoft 맬웨어 방지 프로그램</span><span class="sxs-lookup"><span data-stu-id="0c2a6-146">Microsoft Antimalware for Azure Cloud Services and Virtual Machines</span></span>](azure-security-antimalware.md)
* [<span data-ttu-id="0c2a6-147">Windows VM에 Trend Micro Deep Security as a Service를 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="0c2a6-147">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>](../virtual-machines/windows/classic/install-trend.md)
* [<span data-ttu-id="0c2a6-148">Windows VM에서 Symantec Endpoint Protection을 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="0c2a6-148">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>](../virtual-machines/windows/classic/install-symantec.md)
* [<span data-ttu-id="0c2a6-149">Azure 가상 컴퓨터에 대한 새로운 맬웨어 방지 옵션 - McAfee Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="0c2a6-149">New Antimalware Options for Protecting Azure Virtual Machines – McAfee Endpoint Protection</span></span>](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a><span data-ttu-id="0c2a6-150">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0c2a6-150">Multi-Factor Authentication</span></span>
<span data-ttu-id="0c2a6-151">Azure MFA(Multi-Factor Authentication)는 두 개 이상의 인증 방법을 사용해야 하고 사용자 로그인 및 트랜잭션에 중요한 제2의 보안 계층을 추가하는 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-151">Azure Multi-factor authentication (MFA) is a method of authentication that requires the use of more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="0c2a6-152">MFA는 간단한 로그인 프로세스에 대한 사용자 요구를 충족하는 동안 데이터와 응용 프로그램에 대한 액세스를 보호하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-152">MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="0c2a6-153">전화 통화, 문자 메시지 또는 모바일 앱 알림 또는 확인 코드 및 타사 OATH 토큰과 같은 다양한 확인 옵션을 통해 강력한 인증을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-153">It delivers strong authentication via a range of verification options—phone call, text message, or mobile app notification or verification code and third party OATH tokens.</span></span>

<span data-ttu-id="0c2a6-154">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-154">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-155">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0c2a6-155">Multi-factor authentication</span></span>](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [<span data-ttu-id="0c2a6-156">Azure Multi-Factor Authentication 정의</span><span class="sxs-lookup"><span data-stu-id="0c2a6-156">What is Azure Multi-Factor Authentication?</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="0c2a6-157">Azure Multi-Factor Authentication 작동 방법</span><span class="sxs-lookup"><span data-stu-id="0c2a6-157">How Azure Multi-Factor Authentication works</span></span>](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a><span data-ttu-id="0c2a6-158">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="0c2a6-158">ExpressRoute</span></span>
<span data-ttu-id="0c2a6-159">Microsoft Azure Express 경로를 사용하면 연결 공급자에서 쉽게 처리된 전용 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-159">Microsoft Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="0c2a6-160">ExpressRoute를 사용하면 Microsoft Azure, Office 365, CRM Online과 같은 Microsoft 클라우드 서비스에 대한 연결을 설정하거나,</span><span class="sxs-lookup"><span data-stu-id="0c2a6-160">With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="0c2a6-161">공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-161">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span> <span data-ttu-id="0c2a6-162">ExpressRoute 연결은 공용 인터넷을 통해 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-162">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="0c2a6-163">이 기능을 사용하면 Express 경로 연결은 인터넷을 통한 일반 연결보다 안정적이고 속도가 빠르며 대기 시간이 짧고 보안성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-163">This allows ExpressRoute connections to offer more reliability, faster speeds, lower latencies, and higher security than typical connections over the Internet.</span></span>

<span data-ttu-id="0c2a6-164">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-164">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-165">Express 경로 기술 개요</span><span class="sxs-lookup"><span data-stu-id="0c2a6-165">ExpressRoute technical overview</span></span>](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a><span data-ttu-id="0c2a6-166">가상 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="0c2a6-166">Virtual network gateways</span></span>
<span data-ttu-id="0c2a6-167">Azure 가상 네트워크 게이트웨이라는 VPN 게이트웨이는 가상 네트워크와 온-프레미스 위치 간에 네트워크 트래픽을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-167">VPN Gateways, also called Azure Virtual Network Gateways, are used to send network traffic between virtual networks and on-premises locations.</span></span> <span data-ttu-id="0c2a6-168">또한 Azure 내의 여러 가상 네트워크 간(VNet 간)에 트래픽을 보내는 데에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-168">They are also used to send traffic between multiple virtual networks within Azure (VNet-to-VNet).</span></span>  <span data-ttu-id="0c2a6-169">VPN 게이트웨이는 Azure와 인프라 사이의 안전한 프레미스 간 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-169">VPN gateways provide secure cross-premises connectivity between Azure and your infrastructure.</span></span>

<span data-ttu-id="0c2a6-170">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-170">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-171">VPN 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="0c2a6-171">About VPN gateways</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="0c2a6-172">Azure 네트워크 보안 개요</span><span class="sxs-lookup"><span data-stu-id="0c2a6-172">Azure Network Security Overview</span></span>](security-network-overview.md)

## <a name="privileged-identity-management"></a><span data-ttu-id="0c2a6-173">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="0c2a6-173">Privileged Identity Management</span></span>
<span data-ttu-id="0c2a6-174">경우에 따라 사용자는 Azure 리소스 또는 기타 SaaS 응용 프로그램에서 권한 있는 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-174">Sometimes users need to carry out privileged operations in Azure resources or other SaaS applications.</span></span> <span data-ttu-id="0c2a6-175">이는 보통 조직이 사용자에게 Azure AD(Azure Active Directory)에서 영구 권한 있는 액세스를 제공해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-175">This often means organizations have to give them permanent privileged access in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0c2a6-176">조직은 사용자가 권한 있는 액세스 권한으로 수행하는 작업을 충분히 모니터링할 수 없으므로 클라우드에 호스트된 리소스의 보안 위험이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-176">This is a growing security risk for cloud-hosted resources because organizations can't sufficiently monitor what those users are doing with their privileged access.</span></span>
<span data-ttu-id="0c2a6-177">또한 권한 있는 액세스가 있는 사용자 계정이 손상되면 이로 인해 전반적인 클라우드 보안에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-177">Additionally, if a user account with privileged access is compromised, that one breach could impact your overall cloud security.</span></span> <span data-ttu-id="0c2a6-178">Azure AD Privileged Identity Management는 권한의 노출 시간을 낮추고 사용에 대한 가시성을 높여 이러한 위험을 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-178">Azure AD Privileged Identity Management helps to resolve this risk by lowering the exposure time of privileges and increasing visibility into usage.</span></span>  

<span data-ttu-id="0c2a6-179">Privileged Identity Management는 할당된 역할에 대한 활성화 프로세스를 완료해야 하는 사용자인, 역할 또는 “적시" 관리자 액세스 권한에 대한 임시 관리자의 개념을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-179">Privileged Identity Management introduces the concept of a temporary admin for a role or “just in time” administrator access, which is a user who needs to complete an activation process for that assigned role.</span></span> <span data-ttu-id="0c2a6-180">활성화 프로세스는 Azure AD에서 할당된 사용자 역할을 지정된 시간(예: 8시간) 동안 비활성에서 활성 상태로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-180">The activation process changes the assignment of the user to a role in Azure AD from inactive to active, for a specified time period such as eight hours.</span></span>

<span data-ttu-id="0c2a6-181">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-181">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-182">Azure AD 권한 있는 ID 관리</span><span class="sxs-lookup"><span data-stu-id="0c2a6-182">Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-configure.md)
* [<span data-ttu-id="0c2a6-183">Azure AD Privileged Identity Management 시작</span><span class="sxs-lookup"><span data-stu-id="0c2a6-183">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a><span data-ttu-id="0c2a6-184">ID 보호</span><span class="sxs-lookup"><span data-stu-id="0c2a6-184">Identity Protection</span></span>
<span data-ttu-id="0c2a6-185">Azure AD(Active Directory) ID 보호는 의심스러운 로그인 활동 및 잠재적 취약성에 대한 통합 뷰를 제공하여 비즈니스를 보호하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-185">Azure Active Directory (AD) Identity Protection provides a consolidated view of suspicious sign-in activities and potential vulnerabilities to help protect your business.</span></span> <span data-ttu-id="0c2a6-186">ID 보호는 무차별 암호 대입 공격(brute-force attack), 자격 증명 유출, 낯선 위치 및 감염된 장치에서 로그인 같은 신호를 기반으로 한 의심스러운 로그인 활동을 검색하며,</span><span class="sxs-lookup"><span data-stu-id="0c2a6-186">Identity Protection detects suspicious activities for users and privileged (admin) identities, based on signals like brute-force attacks, leaked credentials, and sign-ins from unfamiliar locations and infected devices.</span></span>

<span data-ttu-id="0c2a6-187">알림 및 권장된 수정을 제공하여 실시간으로 위험을 완화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-187">By providing notifications and recommended remediation, Identity Protection helps to mitigate risks in real time.</span></span> <span data-ttu-id="0c2a6-188">사용자 위험 심각도를 계산하여 이후 위협으로부터 응용 프로그램 액세스를 자동으로 보호하도록 위험 기반 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-188">It calculates user risk severity, and you can configure risk-based policies to automatically help safeguard application access from future threats.</span></span>

<span data-ttu-id="0c2a6-189">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-189">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-190">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="0c2a6-190">Azure Active Directory Identity Protection</span></span>](../active-directory/active-directory-identityprotection.md)
* [<span data-ttu-id="0c2a6-191">Channel 9: Azure AD 및 ID 표시: ID 보호 미리 보기</span><span class="sxs-lookup"><span data-stu-id="0c2a6-191">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a><span data-ttu-id="0c2a6-192">보안 센터</span><span class="sxs-lookup"><span data-stu-id="0c2a6-192">Security Center</span></span>
<span data-ttu-id="0c2a6-193">Azure 보안 센터는 위협을 예방, 감지 및 대응하는 데 도움이 되며 Azure 리소스의 보안에 대한 향상된 가시성과 제어권을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-193">Azure Security Center helps you prevent, detect, and respond to threats, and provides you increased visibility into, and control over, the security of your Azure resources.</span></span> <span data-ttu-id="0c2a6-194">이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-194">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="0c2a6-195">보안 센터는 다음과 같은 방법을 통해 Azure 리소스의 보안을 최적화하고 모니터링하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-195">Security Center helps you optimize and monitor the security of your Azure resources by:</span></span>

* <span data-ttu-id="0c2a6-196">회사의 보안 요구 사항 및 응용 프로그램 형식 또는 각 구독의 데이터 민감도에 따라 Azure 구독 리소스에 대한 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-196">Enabling you to define policies for your Azure subscription resources according to your company’s security needs and the type of applications or sensitivity of the data in each subscription.</span></span>
* <span data-ttu-id="0c2a6-197">Azure 가상 컴퓨터, 네트워킹 및 응용 프로그램의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-197">Monitoring the state of your Azure virtual machines, networking, and applications.</span></span>
* <span data-ttu-id="0c2a6-198">신속하게 조사해야 하는 정보 및 공격을 해결하는 방법에 대한 권장 사항과 함께 통합 파트너 솔루션의 경고를 포함하여 우선 순위가 지정된 보안 경고의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c2a6-198">Providing a list of prioritized security alerts, including alerts from integrated partner solutions, along with the information you need to quickly investigate and recommendations on how to remediate an attack.</span></span>

<span data-ttu-id="0c2a6-199">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="0c2a6-199">Learn more:</span></span>

* [<span data-ttu-id="0c2a6-200">Azure 보안 센터 소개</span><span class="sxs-lookup"><span data-stu-id="0c2a6-200">Introduction to Azure Security Center</span></span>](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
