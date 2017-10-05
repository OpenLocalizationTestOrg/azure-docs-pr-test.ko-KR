---
title: "Azure AD 페더레이션 호환성 목록"
description: "이 페이지에 Single Sign-On을 구현하는 데 사용할 수 있는 타사 ID 공급자가 있습니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bce5867017647764546d872d97943d5d4f01f2d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-federation-compatibility-list"></a><span data-ttu-id="ca742-103">Azure AD 페더레이션 호환성 목록</span><span class="sxs-lookup"><span data-stu-id="ca742-103">Azure AD federation compatibility list</span></span>
<span data-ttu-id="ca742-104">Azure Active Directory에서는 임의 타사 솔루션을 요구하지 않고 Office 365용 Single Sign-On과 강화된 응용 프로그램 액세스 보안 및 하이브리드와 클라우드 전용 구현에 대한 기타 Microsoft Online Services를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-104">Azure Active Directory provides single-sign on and enhanced application access security for Office 365 and other Microsoft Online services for hybrid and cloud-only implementations without requiring any non-Microsoft solution.</span></span> <span data-ttu-id="ca742-105">대부분의 Microsoft Online Services와 마찬가지로 Office 365는 디렉터리 서비스, 인증 및 권한 부여에 대해 Azure Active Directory와 통합되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-105">Office 365, like most of Microsoft’s Online services, is integrated with Azure Active Directory for directory services, authentication and authorization.</span></span> <span data-ttu-id="ca742-106">또한 Azure Active Directory는 수천 개의 SaaS 응용 프로그램 및 온-프레미스 웹 응용 프로그램에도 Single Sign-On을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-106">Azure Active Directory also provides single sign-on to thousands of SaaS applications and on-premises web applications.</span></span> <span data-ttu-id="ca742-107">지원되는 SaaS 응용 프로그램에 대한 Azure Active Directory 응용 프로그램 갤러리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-107">Please see the Azure Active Directory application gallery for supported SaaS applications.</span></span>

<span data-ttu-id="ca742-108">타사 페더레이션 솔루션에 투자한 조직의 경우 이 항목에는 해당 조직의 Windows Server Active Directory 사용자를 위해 아래 "Azure Active Directory 페더레이션 호환성 목록"의 타사 ID 공급자를 사용하여 Microsoft Online Services로 Single Sign-On을 구성하는 지침이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-108">For organizations that have invested in non-Microsoft federation solutions, this topic contains guidance for configuring single sign-on for their Windows Server Active Directory users with Microsoft Online services by using non-Microsoft identity providers from the “Azure Active Directory federation compatibility list” below.</span></span> 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
<span data-ttu-id="ca742-109">[Oxford Computer Group](http://oxfordcomputergroup.com/)은 Microsoft를 대신하여 이러한 Single Sign-On 환경을 Azure Active Directory와 공통된 사용 사례 집합에 대해 타사 ID 공급자를 사용하여 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-109">[Oxford Computer Group](http://oxfordcomputergroup.com/), a third-party, on behalf of Microsoft, tested these single sign-on experiences using non-Microsoft identity providers against a set of use cases common with Azure Active Directory.</span></span>

<span data-ttu-id="ca742-110">여기에 나열된 타사 ID 공급자를 가져오는 방법에 대한 내용은 Oxford Computer Group( [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com))에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-110">For information on how you can get your third-party identity provider listed here, contact Oxford Computer Group at [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca742-111">Oxford Computer Group은 이러한 Single Sign-On 시나리오의 페더레이션 기능만을 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-111">Oxford Computer Group tested only the federation functionality of these single sign-on scenarios.</span></span> <span data-ttu-id="ca742-112">Oxford Computer Group은 이러한 Single Sign-On 시나리오의 동기화, 2단계 인증 등 구성 요소에 대한 테스트는 수행하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-112">Oxford Computer Group did not perform any testing of the synchronization, two-factor authentication, etc. components of these single sign-on scenarios.</span></span>
> 
> <span data-ttu-id="ca742-113">UPN에 대한 대체 ID 로그인의 사용도 이 프로그램에서 테스트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-113">Use of Sign-in by Alternate ID to UPN is also not tested in this program.</span></span>
> 
> 

* [<span data-ttu-id="ca742-114">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca742-114">Azure Active Directory</span></span>](#azure-active-directory)
* [<span data-ttu-id="ca742-115">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="ca742-115">AuthAnvil Single Sign On 4.5</span></span>](#authanvil-single-sign-on-45)
* [<span data-ttu-id="ca742-116">BIG-IP with Access Policy Manager BIG-IP 버전 11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="ca742-116">BIG-IP with Access Policy Manager BIG-IP ver. 11.3x – 11.6x</span></span>](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [<span data-ttu-id="ca742-117">BitGlass</span><span class="sxs-lookup"><span data-stu-id="ca742-117">BitGlass</span></span>](#bitglass)
* [<span data-ttu-id="ca742-118">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="ca742-118">CA Secure Cloud</span></span>](#ca-secure-cloud) 
* [<span data-ttu-id="ca742-119">CA SiteMinder 12.52</span><span class="sxs-lookup"><span data-stu-id="ca742-119">CA SiteMinder 12.52</span></span>](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [<span data-ttu-id="ca742-120">Centrify</span><span class="sxs-lookup"><span data-stu-id="ca742-120">Centrify</span></span>](#centrify) 
* [<span data-ttu-id="ca742-121">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="ca742-121">Dell One Identity Cloud Access Manager v7.1</span></span>](#dell-one-identity-cloud-access-manager-v71) 
* [<span data-ttu-id="ca742-122">DigitalPersona 복합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-122">DigitalPersona Composite Authentication</span></span>](#digitalpersona-composite-authentication)
* [<span data-ttu-id="ca742-123">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="ca742-123">IBM Tivoli Federated Identity Manager 6.2.2</span></span>](#ibm-tivoli-federated-identity-manager-622) 
* [<span data-ttu-id="ca742-124">IceWall Federation 버전 3.0</span><span class="sxs-lookup"><span data-stu-id="ca742-124">IceWall Federation Version 3.0</span></span>](#icewall-federation-version-30) 
* [<span data-ttu-id="ca742-125">Memority</span><span class="sxs-lookup"><span data-stu-id="ca742-125">Memority</span></span>](#memority)
* [<span data-ttu-id="ca742-126">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="ca742-126">NetIQ Access Manager 4.x</span></span>](#netiq-access-manager-4x) 
* [<span data-ttu-id="ca742-127">Okta</span><span class="sxs-lookup"><span data-stu-id="ca742-127">Okta</span></span>](#okta) 
* [<span data-ttu-id="ca742-128">OneLogin</span><span class="sxs-lookup"><span data-stu-id="ca742-128">OneLogin</span></span>](#onelogin) 
* [<span data-ttu-id="ca742-129">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="ca742-129">Optimal IDM Virtual Identity Server Federation Services</span></span>](#optimal-idm-virtual-identity-server-federation-services) 
* [<span data-ttu-id="ca742-130">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="ca742-130">PingFederate 6.11, 7.2, 8.x</span></span>](#pingfederate-611-72-8x)
* [<span data-ttu-id="ca742-131">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="ca742-131">RadiantOne CFS 3.0</span></span>](#radiantone-cfs-30) 
* [<span data-ttu-id="ca742-132">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="ca742-132">Sailpoint IdentityNow</span></span>](#sailpoint-identitynow)
* [<span data-ttu-id="ca742-133">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="ca742-133">SecureAuth IdP 7.2.0</span></span>](#secureauth-idp-720) 
* [<span data-ttu-id="ca742-134">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="ca742-134">Sign&go 5.3</span></span>](#signgo-53) 
* [<span data-ttu-id="ca742-135">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="ca742-135">SoftBank Technology Online Service Gate</span></span>](#softbank)
* [<span data-ttu-id="ca742-136">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="ca742-136">VMware Workspace One</span></span>](#vmware-workspace-one)



> [!IMPORTANT]
> <span data-ttu-id="ca742-137">이러한 제품은 타사 제품이므로 Microsoft는 배포, 구성, 문제 해결, 모범 사례 등 이러한 ID 공급자에 관한 문제 및 질문에 대한 지원을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-137">Since these are third-party products, Microsoft does not provide support for the deployment, configuration, troubleshooting, best practices, etc. issues and questions regarding these identity providers.</span></span> <span data-ttu-id="ca742-138">이러한 ID 공급자에 관한 지원 및 질문은 타사 담당자에게 직접 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-138">For support and questions regarding these identity providers, contact the supported third-parties directly.</span></span>
> 
> <span data-ttu-id="ca742-139">이러한 타사 ID 공급자는 Microsoft 클라우드 서비스와의 상호 운용성에 대해 WS-Federation 및 WS-Trust 프로토콜만 사용하여 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-139">These third-party identity providers were tested for interoperability with Microsoft cloud services using WS-Federation and WS-Trust protocols only.</span></span> <span data-ttu-id="ca742-140">SAML 프로토콜을 사용한 테스트는 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-140">Testing did not include using the SAML protocol.</span></span>
> 


## <a name="azure-active-directory"></a><span data-ttu-id="ca742-141">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca742-141">Azure Active Directory</span></span>

<span data-ttu-id="ca742-142">다음은 이 로그온 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-142">The following is the scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="ca742-143">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-143">Client</span></span> | <span data-ttu-id="ca742-144">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-144">Support</span></span> | <span data-ttu-id="ca742-145">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-145">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-146">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-146">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-147">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-147">Supported</span></span> |<span data-ttu-id="ca742-148">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-148">None</span></span> |
| <span data-ttu-id="ca742-149">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-149">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-150">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-150">Supported</span></span> |<span data-ttu-id="ca742-151">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-151">None</span></span> |
| <span data-ttu-id="ca742-152">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-152">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-153">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-153">Supported</span></span> |<span data-ttu-id="ca742-154">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-154">None</span></span> |
| <span data-ttu-id="ca742-155">Office 2016과 같은 ADAL을 사용하는 최신 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-155">Modern Applications using ADAL such as Office 2016</span></span> |<span data-ttu-id="ca742-156">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-156">Supported</span></span> |<span data-ttu-id="ca742-157">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-157">None</span></span> |

<span data-ttu-id="ca742-158">AD FS를 통해 Azure Active Directory를 사용하는 방법에 대한 자세한 내용은 [ADFS(Active Directory Federation Services)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-158">For more information about using Azure Active Directory with AD FS see [Active Directory Federation Services (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).</span></span>

<span data-ttu-id="ca742-159">암호 동기화를 통해 Azure Active Directory를 사용하는 방법에 대한 자세한 내용은 [Azure AD Connect](active-directory-aadconnect.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-159">For more information about using Azure Active Directory with Password sync see [Azure AD Connect](active-directory-aadconnect.md).</span></span>

## <a name="authanvil-single-sign-on-45"></a><span data-ttu-id="ca742-160">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="ca742-160">AuthAnvil Single Sign On 4.5</span></span>

<span data-ttu-id="ca742-161">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-161">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-162">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-162">Client</span></span> | <span data-ttu-id="ca742-163">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-163">Support</span></span> | <span data-ttu-id="ca742-164">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-164">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-165">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-165">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-166">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-166">Supported</span></span> |<span data-ttu-id="ca742-167">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-167">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-168">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-168">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-169">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-169">Supported</span></span> |<span data-ttu-id="ca742-170">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-170">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-171">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-171">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-172">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-172">Supported</span></span> |<span data-ttu-id="ca742-173">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-173">None</span></span> |

<span data-ttu-id="ca742-174">자세한 내용은 [AuthAnvil Single Sign-On](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-174">For more information, see [AuthAnvil Single Sign On.](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).</span></span>


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a><span data-ttu-id="ca742-175">BIG-IP with Access Policy Manager BIG-IP 버전</span><span class="sxs-lookup"><span data-stu-id="ca742-175">BIG-IP with Access Policy Manager BIG-IP ver.</span></span> <span data-ttu-id="ca742-176">11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="ca742-176">11.3x – 11.6x</span></span>

<span data-ttu-id="ca742-177">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-177">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-178">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-178">Client</span></span> | <span data-ttu-id="ca742-179">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-179">Support</span></span> | <span data-ttu-id="ca742-180">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-180">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-181">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-181">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-182">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-182">Supported</span></span> |<span data-ttu-id="ca742-183">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-183">None</span></span> |
| <span data-ttu-id="ca742-184">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-184">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-185">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-185">Not Supported</span></span> |<span data-ttu-id="ca742-186">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-186">Not Supported</span></span> |
| <span data-ttu-id="ca742-187">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-187">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-188">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-188">Supported</span></span> |<span data-ttu-id="ca742-189">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-189">None</span></span> |

<span data-ttu-id="ca742-190">BIG-IP Access Policy Manager에 대한 자세한 내용은 [BIG-IP Access Policy Manager](https://f5.com/products/modules/access-policy-manager)</span><span class="sxs-lookup"><span data-stu-id="ca742-190">For more information about BIG-IP Access Policy Manager, see [BIG-IP Access Policy Manager.](https://f5.com/products/modules/access-policy-manager)</span></span> 

<span data-ttu-id="ca742-191">Active Directory 사용자에게 Single Sign-On 환경을 제공하도록 이 STS를 구성하는 방법에 대한 BIG-IP Access Policy Manager 지침은 pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-191">For the BIG-IP Access Policy Manager instructions on how to configure this STS to provide the single sign-on experience to your Active Directory Users, download the pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).</span></span>

## <a name="bitglass"></a><span data-ttu-id="ca742-192">BitGlass</span><span class="sxs-lookup"><span data-stu-id="ca742-192">BitGlass</span></span>

<span data-ttu-id="ca742-193">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-193">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-194">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-194">Client</span></span> | <span data-ttu-id="ca742-195">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-195">Support</span></span> | <span data-ttu-id="ca742-196">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-196">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-197">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-197">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-198">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-198">Supported</span></span> |<span data-ttu-id="ca742-199">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-199">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-200">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-200">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-201">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-201">Supported</span></span> |<span data-ttu-id="ca742-202">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-202">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-203">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-203">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-204">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-204">Supported</span></span> |<span data-ttu-id="ca742-205">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-205">None</span></span> |

<span data-ttu-id="ca742-206">BitGlass에 대한 자세한 내용은 [BitGlass](http://www.bitglass.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-206">For more information about BitGlass see [BitGlass](http://www.bitglass.com).</span></span>

## <a name="ca-secure-cloud"></a><span data-ttu-id="ca742-207">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="ca742-207">CA Secure Cloud</span></span>

<span data-ttu-id="ca742-208">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-208">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-209">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-209">Client</span></span> | <span data-ttu-id="ca742-210">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-210">Support</span></span> | <span data-ttu-id="ca742-211">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-211">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-212">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-212">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-213">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-213">Supported</span></span> |<span data-ttu-id="ca742-214">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-214">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-215">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-215">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-216">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-216">Supported</span></span> |<span data-ttu-id="ca742-217">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-217">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-218">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-218">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-219">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-219">Supported</span></span> |<span data-ttu-id="ca742-220">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-220">None</span></span> |

<span data-ttu-id="ca742-221">CA Secure Cloud에 대한 자세한 내용은 [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-221">For more information about CA Secure Cloud, see [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).</span></span>

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a><span data-ttu-id="ca742-222">CA SiteMinder 12.52 SP1 누적 릴리스 4</span><span class="sxs-lookup"><span data-stu-id="ca742-222">CA SiteMinder 12.52 SP1 Cumulative Release 4</span></span>

<span data-ttu-id="ca742-223">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-223">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-224">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-224">Client</span></span> | <span data-ttu-id="ca742-225">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-225">Support</span></span> | <span data-ttu-id="ca742-226">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-226">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-227">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-227">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-228">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-228">Supported</span></span> |<span data-ttu-id="ca742-229">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-229">None</span></span> |
| <span data-ttu-id="ca742-230">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-230">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-231">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-231">Supported</span></span> |<span data-ttu-id="ca742-232">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-232">None</span></span> |
| <span data-ttu-id="ca742-233">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-233">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-234">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-234">Supported</span></span> |<span data-ttu-id="ca742-235">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-235">None</span></span> |

<span data-ttu-id="ca742-236">CA SiteMinder에 대한 자세한 내용은 [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-236">For more information about CA SiteMinder, see [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html).</span></span> 

## <a name="centrify"></a><span data-ttu-id="ca742-237">Centrify</span><span class="sxs-lookup"><span data-stu-id="ca742-237">Centrify</span></span>

<span data-ttu-id="ca742-238">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-238">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-239">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-239">Client</span></span> | <span data-ttu-id="ca742-240">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-240">Support</span></span> | <span data-ttu-id="ca742-241">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-241">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-242">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-242">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-243">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-243">Supported</span></span> |<span data-ttu-id="ca742-244">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-244">None</span></span> |
| <span data-ttu-id="ca742-245">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-245">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-246">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-246">Supported</span></span> |<span data-ttu-id="ca742-247">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-247">None</span></span> |
| <span data-ttu-id="ca742-248">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-248">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-249">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-249">Supported</span></span> |<span data-ttu-id="ca742-250">클라이언트 액세스 제어는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-250">Client Access Control is not supported</span></span> |

<span data-ttu-id="ca742-251">Centrify에 대한 자세한 내용은 [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-251">For more information about Centrify, see [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).</span></span>

## <a name="dell-one-identity-cloud-access-manager-v71"></a><span data-ttu-id="ca742-252">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="ca742-252">Dell One Identity Cloud Access Manager v7.1</span></span>

<span data-ttu-id="ca742-253">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-253">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-254">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-254">Client</span></span> | <span data-ttu-id="ca742-255">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-255">Support</span></span> | <span data-ttu-id="ca742-256">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-256">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-257">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-257">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-258">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-258">Supported</span></span> |<span data-ttu-id="ca742-259">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-259">None</span></span> |
| <span data-ttu-id="ca742-260">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-260">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-261">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-261">Supported</span></span> |<span data-ttu-id="ca742-262">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-262">None</span></span> |
| <span data-ttu-id="ca742-263">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-263">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-264">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-264">Supported</span></span> |<span data-ttu-id="ca742-265">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-265">None</span></span> |

<span data-ttu-id="ca742-266">Dell One Identity Cloud Access Manager에 대한 자세한 내용은 [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-266">For more information about Dell One Identity Cloud Access Manager, see [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).</span></span>

 <span data-ttu-id="ca742-267">Office 365 사용자에게 Single Sign-On 환경을 제공하도록 이 STS를 구성하는 방법에 대한 지침은 [Office 365 사용자 구성](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-267">For the instructions on how to configure this STS to provide the single sign-on experience to your Office 365 Users, see [Configure Office 365 Users](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365).</span></span> 

## <a name="digitalpersona-composite-authentication"></a><span data-ttu-id="ca742-268">DigitalPersona 복합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-268">DigitalPersona Composite Authentication</span></span>  

<span data-ttu-id="ca742-269">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-269">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-270">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-270">Client</span></span> | <span data-ttu-id="ca742-271">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-271">Support</span></span> | <span data-ttu-id="ca742-272">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-272">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-273">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-273">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-274">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-274">Supported</span></span> |<span data-ttu-id="ca742-275">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-275">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="ca742-276">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-276">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-277">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-277">Supported</span></span> |<span data-ttu-id="ca742-278">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-278">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="ca742-279">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-279">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-280">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-280">Supported</span></span> |<span data-ttu-id="ca742-281">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-281">None</span></span> |

<span data-ttu-id="ca742-282">자세한 내용은 [DigitalPersona 복합 인증](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-282">For more information see [DigitalPersona Composite Authentication](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).</span></span>


## <a name="ibm-tivoli-federated-identity-manager-622"></a><span data-ttu-id="ca742-283">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="ca742-283">IBM Tivoli Federated Identity Manager 6.2.2</span></span>

<span data-ttu-id="ca742-284">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-284">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-285">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-285">Client</span></span> | <span data-ttu-id="ca742-286">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-286">Support</span></span> | <span data-ttu-id="ca742-287">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-287">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-288">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-288">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-289">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-289">Supported</span></span> |<span data-ttu-id="ca742-290">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-290">None</span></span> |
| <span data-ttu-id="ca742-291">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-291">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-292">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-292">Supported</span></span> |<span data-ttu-id="ca742-293">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-293">None</span></span> |
| <span data-ttu-id="ca742-294">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-294">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-295">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-295">Supported</span></span> |<span data-ttu-id="ca742-296">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-296">None</span></span> |

<span data-ttu-id="ca742-297">IBM Tivoli Federated Identity Manager에 대한 자세한 내용은 [Microsoft 응용 프로그램용 IBM Security Access Manager](http://www-01.ibm.com/support/docview.wss?uid=swg24029517)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-297">For more information about IBM Tivoli Federated Identity Manager, see [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).</span></span>

## <a name="icewall-federation-version-30"></a><span data-ttu-id="ca742-298">IceWall Federation 버전 3.0</span><span class="sxs-lookup"><span data-stu-id="ca742-298">IceWall Federation Version 3.0</span></span>

<span data-ttu-id="ca742-299">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-299">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-300">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-300">Client</span></span> | <span data-ttu-id="ca742-301">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-301">Support</span></span> | <span data-ttu-id="ca742-302">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-302">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-303">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-303">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-304">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-304">Supported</span></span> |<span data-ttu-id="ca742-305">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-305">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-306">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-306">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-307">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-307">Supported</span></span> |<span data-ttu-id="ca742-308">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-308">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-309">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-309">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-310">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-310">Supported</span></span> |<span data-ttu-id="ca742-311">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-311">None</span></span> |

<span data-ttu-id="ca742-312">IceWall Federation에 대한 자세한 내용은 [IceWall Federation 버전 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) 및 [Office 365를 사용하여 IceWall Federation](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-312">For more information about IceWall Federation, see [IceWall Federation Version 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) and [IceWall Federation with Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).</span></span>

## <a name="memority"></a><span data-ttu-id="ca742-313">Memority</span><span class="sxs-lookup"><span data-stu-id="ca742-313">Memority</span></span>

<span data-ttu-id="ca742-314">다음은 이 로그온 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-314">The following is the scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="ca742-315">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-315">Client</span></span> | <span data-ttu-id="ca742-316">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-316">Support</span></span> | <span data-ttu-id="ca742-317">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-317">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-318">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-318">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-319">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-319">Supported</span></span> |<span data-ttu-id="ca742-320">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-320">None</span></span> |
| <span data-ttu-id="ca742-321">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-321">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-322">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-322">Supported</span></span> |<span data-ttu-id="ca742-323">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-323">None</span></span> |
| <span data-ttu-id="ca742-324">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-324">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-325">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-325">Supported</span></span> |<span data-ttu-id="ca742-326">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-326">None</span></span> |

<span data-ttu-id="ca742-327">Memority 사용에 대한 자세한 내용은 [Memority](http://www.memority.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-327">For more information about using Memority see [Memority](http://www.memority.com).</span></span>


## <a name="netiq-access-manager-4x"></a><span data-ttu-id="ca742-328">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="ca742-328">NetIQ Access Manager 4.x</span></span>

<span data-ttu-id="ca742-329">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-329">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-330">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-330">Client</span></span> | <span data-ttu-id="ca742-331">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-331">Support</span></span> | <span data-ttu-id="ca742-332">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-332">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-333">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-333">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-334">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-334">Supported</span></span> |<span data-ttu-id="ca742-335">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-335">None</span></span>|
| <span data-ttu-id="ca742-336">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-336">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-337">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-337">Supported</span></span> |<span data-ttu-id="ca742-338">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-338">None</span></span>|
| <span data-ttu-id="ca742-339">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-339">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-340">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-340">Supported</span></span> |<span data-ttu-id="ca742-341">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-341">None</span></span> |

<span data-ttu-id="ca742-342">자세한 내용은 [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-342">For more information, see [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).</span></span>

## <a name="okta"></a><span data-ttu-id="ca742-343">Okta</span><span class="sxs-lookup"><span data-stu-id="ca742-343">Okta</span></span>

<span data-ttu-id="ca742-344">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-344">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-345">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-345">Client</span></span> | <span data-ttu-id="ca742-346">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-346">Support</span></span> | <span data-ttu-id="ca742-347">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-347">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-348">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-348">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-349">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-349">Supported</span></span> |<span data-ttu-id="ca742-350">Windows 통합 인증에는 추가 웹 서버 및 Okta 응용 프로그램 설치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-350">Integrated Windows Authentication requires setup of additional web server and Okta application.</span></span> |
| <span data-ttu-id="ca742-351">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-351">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-352">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-352">Supported</span></span> |<span data-ttu-id="ca742-353">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-353">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="ca742-354">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-354">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-355">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-355">Supported</span></span> |<span data-ttu-id="ca742-356">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-356">None</span></span> |

<span data-ttu-id="ca742-357">Okta에 대한 자세한 내용은 [Okta](https://www.okta.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-357">For more information about Okta, see [Okta](https://www.okta.com/).</span></span>

## <a name="onelogin"></a><span data-ttu-id="ca742-358">OneLogin</span><span class="sxs-lookup"><span data-stu-id="ca742-358">OneLogin</span></span>

<span data-ttu-id="ca742-359">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-359">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-360">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-360">Client</span></span> | <span data-ttu-id="ca742-361">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-361">Support</span></span> | <span data-ttu-id="ca742-362">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-362">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-363">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-363">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-364">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-364">Supported</span></span> |<span data-ttu-id="ca742-365">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-365">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="ca742-366">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-366">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-367">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-367">Supported</span></span> |<span data-ttu-id="ca742-368">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-368">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="ca742-369">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-369">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-370">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-370">Supported</span></span> |<span data-ttu-id="ca742-371">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-371">None</span></span> |

<span data-ttu-id="ca742-372">OneLogin에 대한 자세한 내용은 [OneLogin](https://www.onelogin.com/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-372">For more information about OneLogin, see [OneLogin](https://www.onelogin.com/).</span></span>

## <a name="optimal-idm-virtual-identity-server-federation-services"></a><span data-ttu-id="ca742-373">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="ca742-373">Optimal IDM Virtual Identity Server Federation Services</span></span>

<span data-ttu-id="ca742-374">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-374">The following is the scenario support matrix this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-375">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-375">Client</span></span> | <span data-ttu-id="ca742-376">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-376">Support</span></span> | <span data-ttu-id="ca742-377">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-377">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-378">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-378">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-379">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-379">Supported</span></span> |<span data-ttu-id="ca742-380">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-380">None</span></span> |
| <span data-ttu-id="ca742-381">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-381">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-382">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-382">Supported</span></span> |<span data-ttu-id="ca742-383">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-383">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="ca742-384">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-384">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-385">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-385">Supported</span></span> |

<span data-ttu-id="ca742-386">클라이언트 액세스 정책에 대한 자세한 내용은 [클라이언트 위치 기반 Office 365 서비스에 대한 액세스 제한](https://technet.microsoft.com/library/hh526961.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-386">For more information about client access polices see [Limiting Access to Office 365 Services Based on the Location of the Client](https://technet.microsoft.com/library/hh526961.aspx).</span></span>





## <a name="pingfederate-611-72-8x"></a><span data-ttu-id="ca742-387">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="ca742-387">PingFederate 6.11, 7.2, 8.x</span></span>

<span data-ttu-id="ca742-388">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-388">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-389">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-389">Client</span></span> | <span data-ttu-id="ca742-390">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-390">Support</span></span> | <span data-ttu-id="ca742-391">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-391">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-392">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-392">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-393">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-393">Supported</span></span> |<span data-ttu-id="ca742-394">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-394">None</span></span> |
| <span data-ttu-id="ca742-395">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-395">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-396">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-396">Supported</span></span> |<span data-ttu-id="ca742-397">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-397">None</span></span> |
| <span data-ttu-id="ca742-398">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-398">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-399">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-399">Supported</span></span> |<span data-ttu-id="ca742-400">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-400">None</span></span> |

<span data-ttu-id="ca742-401">Active Directory 사용자에게 Single Sign-On 환경을 제공하도록 이 STS를 구성하는 방법에 대한 PingFederate 지침은 다음 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-401">For the PingFederate instructions on how to configure this STS to provide the single sign-on experience to your Active Directory users, see one of the following:</span></span> 

- [<span data-ttu-id="ca742-402">PingFederate 6.11</span><span class="sxs-lookup"><span data-stu-id="ca742-402">PingFederate 6.11</span></span>](http://go.microsoft.com/fwlink/?LinkID=266321)
- [<span data-ttu-id="ca742-403">PingFederate 7.2</span><span class="sxs-lookup"><span data-stu-id="ca742-403">PingFederate 7.2</span></span>](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [<span data-ttu-id="ca742-404">PingFederate 8.x</span><span class="sxs-lookup"><span data-stu-id="ca742-404">PingFederate 8.x</span></span>](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a><span data-ttu-id="ca742-405">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="ca742-405">RadiantOne CFS 3.0</span></span>

<span data-ttu-id="ca742-406">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-406">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-407">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-407">Client</span></span> | <span data-ttu-id="ca742-408">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-408">Support</span></span> | <span data-ttu-id="ca742-409">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-409">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-410">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-410">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-411">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-411">Supported</span></span> |<span data-ttu-id="ca742-412">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-412">None</span></span> |
| <span data-ttu-id="ca742-413">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-413">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-414">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-414">Supported</span></span> |<span data-ttu-id="ca742-415">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="ca742-415">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="ca742-416">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-416">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-417">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-417">Supported</span></span> |<span data-ttu-id="ca742-418">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-418">None</span></span> |

<span data-ttu-id="ca742-419">RadiantOne CFS에 대한 자세한 내용은 [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-419">For more information about RadiantOne CFS, see [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).</span></span>

## <a name="sailpoint-identitynow"></a><span data-ttu-id="ca742-420">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="ca742-420">Sailpoint IdentityNow</span></span>

<span data-ttu-id="ca742-421">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-421">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-422">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-422">Client</span></span> | <span data-ttu-id="ca742-423">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-423">Support</span></span> | <span data-ttu-id="ca742-424">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-424">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-425">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-425">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-426">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-426">Supported</span></span> |<span data-ttu-id="ca742-427">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-427">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-428">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-428">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-429">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-429">Supported</span></span> |<span data-ttu-id="ca742-430">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-430">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-431">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-431">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-432">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-432">Supported</span></span> |<span data-ttu-id="ca742-433">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-433">None</span></span> |

<span data-ttu-id="ca742-434">자세한 내용은 [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-434">For more information, see [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).</span></span>

## <a name="secureauth-idp-720"></a><span data-ttu-id="ca742-435">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="ca742-435">SecureAuth IdP 7.2.0</span></span>

<span data-ttu-id="ca742-436">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-436">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="ca742-437">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-437">Client</span></span> | <span data-ttu-id="ca742-438">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-438">Support</span></span> | <span data-ttu-id="ca742-439">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-439">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-440">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-440">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-441">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-441">Supported</span></span> |<span data-ttu-id="ca742-442">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-442">None</span></span> |
| <span data-ttu-id="ca742-443">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-443">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-444">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-444">Supported</span></span> |<span data-ttu-id="ca742-445">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-445">None</span></span> |
| <span data-ttu-id="ca742-446">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-446">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-447">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-447">Supported</span></span> |<span data-ttu-id="ca742-448">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-448">None</span></span> |

<span data-ttu-id="ca742-449">SecureAuth에 대한 자세한 내용은 [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-449">For more information about SecureAuth, see [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).</span></span>














## <a name="signgo-53"></a><span data-ttu-id="ca742-450">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="ca742-450">Sign&go 5.3</span></span>

<span data-ttu-id="ca742-451">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-451">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-452">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-452">Client</span></span> | <span data-ttu-id="ca742-453">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-453">Support</span></span> | <span data-ttu-id="ca742-454">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-454">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-455">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-455">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-456">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-456">Supported</span></span> |<span data-ttu-id="ca742-457">Kerberos 계약 지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-457">Kerberos Contracts supported</span></span> |
| <span data-ttu-id="ca742-458">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-458">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-459">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-459">Supported</span></span> |<span data-ttu-id="ca742-460">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-460">None</span></span> |
| <span data-ttu-id="ca742-461">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-461">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-462">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-462">Supported</span></span> |<span data-ttu-id="ca742-463">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-463">None</span></span> |

<span data-ttu-id="ca742-464">Sign&go 5.3은 Kerberos 계약 구성을 통해 Kerberos 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-464">Sign&go 5.3 supports Kerberos authentication via configuration of a Kerberos Contract.</span></span>  <span data-ttu-id="ca742-465">이 구성에 지원이 필요한 경우 Ilex에 문의하거나 설치 가이드 [Sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-465">For assistance with this configuration, please contact Ilex or view the setup guide [Sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)</span></span>

## <a name="softbank-technology-online-service-gate"></a><span data-ttu-id="ca742-466">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="ca742-466">SoftBank Technology Online Service Gate</span></span>

<span data-ttu-id="ca742-467">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-467">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-468">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-468">Client</span></span> | <span data-ttu-id="ca742-469">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-469">Support</span></span> | <span data-ttu-id="ca742-470">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-470">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-471">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-471">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-472">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-472">Supported</span></span> |<span data-ttu-id="ca742-473">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-473">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-474">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-474">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-475">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-475">Supported</span></span> |<span data-ttu-id="ca742-476">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-476">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-477">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-477">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-478">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-478">Supported</span></span> |<span data-ttu-id="ca742-479">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-479">None</span></span> |

<span data-ttu-id="ca742-480">SoftBank Technology Online Service Gate에 대한 자세한 내용은 [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-480">For more information about SoftBank Technology Online Service Gate see [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)</span></span>

## <a name="vmware-workspace-one"></a><span data-ttu-id="ca742-481">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="ca742-481">VMware Workspace One</span></span>

<span data-ttu-id="ca742-482">다음은 이 Single Sign-On 환경에 대한 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca742-482">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="ca742-483">클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-483">Client</span></span> | <span data-ttu-id="ca742-484">지원</span><span class="sxs-lookup"><span data-stu-id="ca742-484">Support</span></span> | <span data-ttu-id="ca742-485">예외</span><span class="sxs-lookup"><span data-stu-id="ca742-485">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca742-486">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-486">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="ca742-487">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-487">Supported</span></span> |<span data-ttu-id="ca742-488">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-488">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-489">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca742-489">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="ca742-490">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-490">Supported</span></span> |<span data-ttu-id="ca742-491">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ca742-491">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="ca742-492">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca742-492">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="ca742-493">지원됨</span><span class="sxs-lookup"><span data-stu-id="ca742-493">Supported</span></span> |<span data-ttu-id="ca742-494">없음</span><span class="sxs-lookup"><span data-stu-id="ca742-494">None</span></span> |

<span data-ttu-id="ca742-495">자세한 내용은 [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca742-495">For more information about see [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)</span></span>

