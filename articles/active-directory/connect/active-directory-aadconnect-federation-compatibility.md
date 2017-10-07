---
title: "AD aaaAzure 페더레이션 호환성 목록"
description: "이 페이지에는 Microsoft가 아닌 타사 tooimplement 사용된 될 수 있는 id 공급자 single sign on입니다."
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
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a><span data-ttu-id="2fb6e-103">Azure AD 페더레이션 호환성 목록</span><span class="sxs-lookup"><span data-stu-id="2fb6e-103">Azure AD federation compatibility list</span></span>
<span data-ttu-id="2fb6e-104">Azure Active Directory에서는 임의 타사 솔루션을 요구하지 않고 Office 365용 Single Sign-On과 강화된 응용 프로그램 액세스 보안 및 하이브리드와 클라우드 전용 구현에 대한 기타 Microsoft Online Services를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-104">Azure Active Directory provides single-sign on and enhanced application access security for Office 365 and other Microsoft Online services for hybrid and cloud-only implementations without requiring any non-Microsoft solution.</span></span> <span data-ttu-id="2fb6e-105">대부분의 Microsoft Online Services와 마찬가지로 Office 365는 디렉터리 서비스, 인증 및 권한 부여에 대해 Azure Active Directory와 통합되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-105">Office 365, like most of Microsoft’s Online services, is integrated with Azure Active Directory for directory services, authentication and authorization.</span></span> <span data-ttu-id="2fb6e-106">온-프레미스 웹 응용 프로그램 및 azure Active Directory에는 또한 SaaS 응용 프로그램의 single sign on toothousands 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-106">Azure Active Directory also provides single sign-on toothousands of SaaS applications and on-premises web applications.</span></span> <span data-ttu-id="2fb6e-107">지원 되는 SaaS 응용 프로그램에 대 한 hello Azure Active Directory 응용 프로그램 갤러리를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-107">Please see hello Azure Active Directory application gallery for supported SaaS applications.</span></span>

<span data-ttu-id="2fb6e-108">Microsoft가 아닌 타사 페더레이션 솔루션에 투자 하는 조직에서는이 항목에서는 Microsoft가 아닌 타사 id 공급자를 사용 하 여 Microsoft Online 서비스를 사용 하 여 single sign on Windows Server Active Directory 사용자를 위한 구성에 대 한 지침 hello "Azure Active Directory 페더레이션 호환성 목록에" 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-108">For organizations that have invested in non-Microsoft federation solutions, this topic contains guidance for configuring single sign-on for their Windows Server Active Directory users with Microsoft Online services by using non-Microsoft identity providers from hello “Azure Active Directory federation compatibility list” below.</span></span> 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
<span data-ttu-id="2fb6e-109">[Oxford Computer Group](http://oxfordcomputergroup.com/)은 Microsoft를 대신하여 이러한 Single Sign-On 환경을 Azure Active Directory와 공통된 사용 사례 집합에 대해 타사 ID 공급자를 사용하여 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-109">[Oxford Computer Group](http://oxfordcomputergroup.com/), a third-party, on behalf of Microsoft, tested these single sign-on experiences using non-Microsoft identity providers against a set of use cases common with Azure Active Directory.</span></span>

<span data-ttu-id="2fb6e-110">여기에 나열된 타사 ID 공급자를 가져오는 방법에 대한 내용은 Oxford Computer Group( [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com))에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-110">For information on how you can get your third-party identity provider listed here, contact Oxford Computer Group at [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fb6e-111">Oxford 컴퓨터 그룹에는 이러한 single sign-on 시나리오의 hello 페더레이션 기능만을 테스트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-111">Oxford Computer Group tested only hello federation functionality of these single sign-on scenarios.</span></span> <span data-ttu-id="2fb6e-112">컴퓨터 그룹 Oxford hello 동기화, 다단계 인증, 등 이러한 single sign-on 시나리오의 구성 요소 테스트를 수행 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-112">Oxford Computer Group did not perform any testing of hello synchronization, two-factor authentication, etc. components of these single sign-on scenarios.</span></span>
> 
> <span data-ttu-id="2fb6e-113">로그인의 대체 ID tooUPN 사용이이 프로그램에서 테스트 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-113">Use of Sign-in by Alternate ID tooUPN is also not tested in this program.</span></span>
> 
> 

* [<span data-ttu-id="2fb6e-114">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2fb6e-114">Azure Active Directory</span></span>](#azure-active-directory)
* [<span data-ttu-id="2fb6e-115">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="2fb6e-115">AuthAnvil Single Sign On 4.5</span></span>](#authanvil-single-sign-on-45)
* [<span data-ttu-id="2fb6e-116">BIG-IP with Access Policy Manager BIG-IP 버전 11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-116">BIG-IP with Access Policy Manager BIG-IP ver. 11.3x – 11.6x</span></span>](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [<span data-ttu-id="2fb6e-117">BitGlass</span><span class="sxs-lookup"><span data-stu-id="2fb6e-117">BitGlass</span></span>](#bitglass)
* [<span data-ttu-id="2fb6e-118">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="2fb6e-118">CA Secure Cloud</span></span>](#ca-secure-cloud) 
* [<span data-ttu-id="2fb6e-119">CA SiteMinder 12.52</span><span class="sxs-lookup"><span data-stu-id="2fb6e-119">CA SiteMinder 12.52</span></span>](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [<span data-ttu-id="2fb6e-120">Centrify</span><span class="sxs-lookup"><span data-stu-id="2fb6e-120">Centrify</span></span>](#centrify) 
* [<span data-ttu-id="2fb6e-121">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="2fb6e-121">Dell One Identity Cloud Access Manager v7.1</span></span>](#dell-one-identity-cloud-access-manager-v71) 
* [<span data-ttu-id="2fb6e-122">DigitalPersona 복합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-122">DigitalPersona Composite Authentication</span></span>](#digitalpersona-composite-authentication)
* [<span data-ttu-id="2fb6e-123">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="2fb6e-123">IBM Tivoli Federated Identity Manager 6.2.2</span></span>](#ibm-tivoli-federated-identity-manager-622) 
* [<span data-ttu-id="2fb6e-124">IceWall Federation 버전 3.0</span><span class="sxs-lookup"><span data-stu-id="2fb6e-124">IceWall Federation Version 3.0</span></span>](#icewall-federation-version-30) 
* [<span data-ttu-id="2fb6e-125">Memority</span><span class="sxs-lookup"><span data-stu-id="2fb6e-125">Memority</span></span>](#memority)
* [<span data-ttu-id="2fb6e-126">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-126">NetIQ Access Manager 4.x</span></span>](#netiq-access-manager-4x) 
* [<span data-ttu-id="2fb6e-127">Okta</span><span class="sxs-lookup"><span data-stu-id="2fb6e-127">Okta</span></span>](#okta) 
* [<span data-ttu-id="2fb6e-128">OneLogin</span><span class="sxs-lookup"><span data-stu-id="2fb6e-128">OneLogin</span></span>](#onelogin) 
* [<span data-ttu-id="2fb6e-129">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="2fb6e-129">Optimal IDM Virtual Identity Server Federation Services</span></span>](#optimal-idm-virtual-identity-server-federation-services) 
* [<span data-ttu-id="2fb6e-130">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-130">PingFederate 6.11, 7.2, 8.x</span></span>](#pingfederate-611-72-8x)
* [<span data-ttu-id="2fb6e-131">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="2fb6e-131">RadiantOne CFS 3.0</span></span>](#radiantone-cfs-30) 
* [<span data-ttu-id="2fb6e-132">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="2fb6e-132">Sailpoint IdentityNow</span></span>](#sailpoint-identitynow)
* [<span data-ttu-id="2fb6e-133">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="2fb6e-133">SecureAuth IdP 7.2.0</span></span>](#secureauth-idp-720) 
* [<span data-ttu-id="2fb6e-134">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="2fb6e-134">Sign&go 5.3</span></span>](#signgo-53) 
* [<span data-ttu-id="2fb6e-135">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="2fb6e-135">SoftBank Technology Online Service Gate</span></span>](#softbank)
* [<span data-ttu-id="2fb6e-136">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="2fb6e-136">VMware Workspace One</span></span>](#vmware-workspace-one)



> [!IMPORTANT]
> <span data-ttu-id="2fb6e-137">이러한 타사 제품 이므로 Microsoft는 hello 배포, 구성, 문제 해결, 모범 사례, 등 문제 및 이러한 id 공급자에 관한 질문에 대 한 지원을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-137">Since these are third-party products, Microsoft does not provide support for hello deployment, configuration, troubleshooting, best practices, etc. issues and questions regarding these identity providers.</span></span> <span data-ttu-id="2fb6e-138">지원 및 이러한 id 공급자에 관한 질문에 대 한 연락처 hello 제 3 자가 직접 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-138">For support and questions regarding these identity providers, contact hello supported third-parties directly.</span></span>
> 
> <span data-ttu-id="2fb6e-139">이러한 타사 ID 공급자는 Microsoft 클라우드 서비스와의 상호 운용성에 대해 WS-Federation 및 WS-Trust 프로토콜만 사용하여 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-139">These third-party identity providers were tested for interoperability with Microsoft cloud services using WS-Federation and WS-Trust protocols only.</span></span> <span data-ttu-id="2fb6e-140">테스트 hello SAML 프로토콜을 사용 하 여 포함 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-140">Testing did not include using hello SAML protocol.</span></span>
> 


## <a name="azure-active-directory"></a><span data-ttu-id="2fb6e-141">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2fb6e-141">Azure Active Directory</span></span>

<span data-ttu-id="2fb6e-142">hello 다음은이 로그온 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-142">hello following is hello scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-143">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-143">Client</span></span> | <span data-ttu-id="2fb6e-144">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-144">Support</span></span> | <span data-ttu-id="2fb6e-145">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-145">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-146">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-146">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-147">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-147">Supported</span></span> |<span data-ttu-id="2fb6e-148">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-148">None</span></span> |
| <span data-ttu-id="2fb6e-149">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-149">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-150">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-150">Supported</span></span> |<span data-ttu-id="2fb6e-151">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-151">None</span></span> |
| <span data-ttu-id="2fb6e-152">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-152">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-153">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-153">Supported</span></span> |<span data-ttu-id="2fb6e-154">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-154">None</span></span> |
| <span data-ttu-id="2fb6e-155">Office 2016과 같은 ADAL을 사용하는 최신 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-155">Modern Applications using ADAL such as Office 2016</span></span> |<span data-ttu-id="2fb6e-156">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-156">Supported</span></span> |<span data-ttu-id="2fb6e-157">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-157">None</span></span> |

<span data-ttu-id="2fb6e-158">AD FS를 통해 Azure Active Directory를 사용하는 방법에 대한 자세한 내용은 [ADFS(Active Directory Federation Services)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-158">For more information about using Azure Active Directory with AD FS see [Active Directory Federation Services (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).</span></span>

<span data-ttu-id="2fb6e-159">암호 동기화를 통해 Azure Active Directory를 사용하는 방법에 대한 자세한 내용은 [Azure AD Connect](active-directory-aadconnect.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-159">For more information about using Azure Active Directory with Password sync see [Azure AD Connect](active-directory-aadconnect.md).</span></span>

## <a name="authanvil-single-sign-on-45"></a><span data-ttu-id="2fb6e-160">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="2fb6e-160">AuthAnvil Single Sign On 4.5</span></span>

<span data-ttu-id="2fb6e-161">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-161">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-162">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-162">Client</span></span> | <span data-ttu-id="2fb6e-163">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-163">Support</span></span> | <span data-ttu-id="2fb6e-164">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-164">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-165">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-165">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-166">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-166">Supported</span></span> |<span data-ttu-id="2fb6e-167">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-167">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-168">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-168">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-169">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-169">Supported</span></span> |<span data-ttu-id="2fb6e-170">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-170">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-171">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-171">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-172">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-172">Supported</span></span> |<span data-ttu-id="2fb6e-173">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-173">None</span></span> |

<span data-ttu-id="2fb6e-174">자세한 내용은 [AuthAnvil Single Sign-On](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-174">For more information, see [AuthAnvil Single Sign On.](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).</span></span>


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a><span data-ttu-id="2fb6e-175">BIG-IP with Access Policy Manager BIG-IP 버전</span><span class="sxs-lookup"><span data-stu-id="2fb6e-175">BIG-IP with Access Policy Manager BIG-IP ver.</span></span> <span data-ttu-id="2fb6e-176">11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-176">11.3x – 11.6x</span></span>

<span data-ttu-id="2fb6e-177">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-177">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-178">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-178">Client</span></span> | <span data-ttu-id="2fb6e-179">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-179">Support</span></span> | <span data-ttu-id="2fb6e-180">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-180">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-181">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-181">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-182">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-182">Supported</span></span> |<span data-ttu-id="2fb6e-183">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-183">None</span></span> |
| <span data-ttu-id="2fb6e-184">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-184">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-185">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-185">Not Supported</span></span> |<span data-ttu-id="2fb6e-186">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-186">Not Supported</span></span> |
| <span data-ttu-id="2fb6e-187">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-187">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-188">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-188">Supported</span></span> |<span data-ttu-id="2fb6e-189">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-189">None</span></span> |

<span data-ttu-id="2fb6e-190">BIG-IP Access Policy Manager에 대한 자세한 내용은 [BIG-IP Access Policy Manager](https://f5.com/products/modules/access-policy-manager)</span><span class="sxs-lookup"><span data-stu-id="2fb6e-190">For more information about BIG-IP Access Policy Manager, see [BIG-IP Access Policy Manager.](https://f5.com/products/modules/access-policy-manager)</span></span> 

<span data-ttu-id="2fb6e-191">Pdf hello에 대 한 hello BIG-IP Access Policy Manager 지침은이 STS tooprovide hello single sign on 환경을 tooyour Active Directory 사용자를 다운로드 하는 tooconfigure 어떻게 [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-191">For hello BIG-IP Access Policy Manager instructions on how tooconfigure this STS tooprovide hello single sign-on experience tooyour Active Directory Users, download hello pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).</span></span>

## <a name="bitglass"></a><span data-ttu-id="2fb6e-192">BitGlass</span><span class="sxs-lookup"><span data-stu-id="2fb6e-192">BitGlass</span></span>

<span data-ttu-id="2fb6e-193">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-193">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-194">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-194">Client</span></span> | <span data-ttu-id="2fb6e-195">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-195">Support</span></span> | <span data-ttu-id="2fb6e-196">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-196">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-197">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-197">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-198">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-198">Supported</span></span> |<span data-ttu-id="2fb6e-199">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-199">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-200">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-200">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-201">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-201">Supported</span></span> |<span data-ttu-id="2fb6e-202">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-202">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-203">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-203">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-204">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-204">Supported</span></span> |<span data-ttu-id="2fb6e-205">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-205">None</span></span> |

<span data-ttu-id="2fb6e-206">BitGlass에 대한 자세한 내용은 [BitGlass](http://www.bitglass.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-206">For more information about BitGlass see [BitGlass](http://www.bitglass.com).</span></span>

## <a name="ca-secure-cloud"></a><span data-ttu-id="2fb6e-207">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="2fb6e-207">CA Secure Cloud</span></span>

<span data-ttu-id="2fb6e-208">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-208">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-209">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-209">Client</span></span> | <span data-ttu-id="2fb6e-210">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-210">Support</span></span> | <span data-ttu-id="2fb6e-211">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-211">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-212">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-212">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-213">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-213">Supported</span></span> |<span data-ttu-id="2fb6e-214">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-214">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-215">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-215">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-216">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-216">Supported</span></span> |<span data-ttu-id="2fb6e-217">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-217">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-218">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-218">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-219">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-219">Supported</span></span> |<span data-ttu-id="2fb6e-220">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-220">None</span></span> |

<span data-ttu-id="2fb6e-221">CA Secure Cloud에 대한 자세한 내용은 [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-221">For more information about CA Secure Cloud, see [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).</span></span>

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a><span data-ttu-id="2fb6e-222">CA SiteMinder 12.52 SP1 누적 릴리스 4</span><span class="sxs-lookup"><span data-stu-id="2fb6e-222">CA SiteMinder 12.52 SP1 Cumulative Release 4</span></span>

<span data-ttu-id="2fb6e-223">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-223">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-224">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-224">Client</span></span> | <span data-ttu-id="2fb6e-225">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-225">Support</span></span> | <span data-ttu-id="2fb6e-226">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-226">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-227">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-227">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-228">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-228">Supported</span></span> |<span data-ttu-id="2fb6e-229">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-229">None</span></span> |
| <span data-ttu-id="2fb6e-230">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-230">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-231">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-231">Supported</span></span> |<span data-ttu-id="2fb6e-232">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-232">None</span></span> |
| <span data-ttu-id="2fb6e-233">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-233">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-234">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-234">Supported</span></span> |<span data-ttu-id="2fb6e-235">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-235">None</span></span> |

<span data-ttu-id="2fb6e-236">CA SiteMinder에 대한 자세한 내용은 [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-236">For more information about CA SiteMinder, see [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html).</span></span> 

## <a name="centrify"></a><span data-ttu-id="2fb6e-237">Centrify</span><span class="sxs-lookup"><span data-stu-id="2fb6e-237">Centrify</span></span>

<span data-ttu-id="2fb6e-238">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-238">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-239">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-239">Client</span></span> | <span data-ttu-id="2fb6e-240">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-240">Support</span></span> | <span data-ttu-id="2fb6e-241">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-241">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-242">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-242">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-243">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-243">Supported</span></span> |<span data-ttu-id="2fb6e-244">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-244">None</span></span> |
| <span data-ttu-id="2fb6e-245">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-245">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-246">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-246">Supported</span></span> |<span data-ttu-id="2fb6e-247">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-247">None</span></span> |
| <span data-ttu-id="2fb6e-248">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-248">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-249">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-249">Supported</span></span> |<span data-ttu-id="2fb6e-250">클라이언트 액세스 제어는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-250">Client Access Control is not supported</span></span> |

<span data-ttu-id="2fb6e-251">Centrify에 대한 자세한 내용은 [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-251">For more information about Centrify, see [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).</span></span>

## <a name="dell-one-identity-cloud-access-manager-v71"></a><span data-ttu-id="2fb6e-252">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="2fb6e-252">Dell One Identity Cloud Access Manager v7.1</span></span>

<span data-ttu-id="2fb6e-253">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-253">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-254">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-254">Client</span></span> | <span data-ttu-id="2fb6e-255">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-255">Support</span></span> | <span data-ttu-id="2fb6e-256">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-256">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-257">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-257">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-258">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-258">Supported</span></span> |<span data-ttu-id="2fb6e-259">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-259">None</span></span> |
| <span data-ttu-id="2fb6e-260">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-260">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-261">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-261">Supported</span></span> |<span data-ttu-id="2fb6e-262">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-262">None</span></span> |
| <span data-ttu-id="2fb6e-263">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-263">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-264">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-264">Supported</span></span> |<span data-ttu-id="2fb6e-265">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-265">None</span></span> |

<span data-ttu-id="2fb6e-266">Dell One Identity Cloud Access Manager에 대한 자세한 내용은 [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-266">For more information about Dell One Identity Cloud Access Manager, see [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).</span></span>

 <span data-ttu-id="2fb6e-267">Hello에 대 한 지침은 tooconfigure이 STS tooprovide hello single sign on 환경을 tooyour Office 365 사용자를 확인 하려면 어떻게 [Office 365 사용자 구성](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-267">For hello instructions on how tooconfigure this STS tooprovide hello single sign-on experience tooyour Office 365 Users, see [Configure Office 365 Users](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365).</span></span> 

## <a name="digitalpersona-composite-authentication"></a><span data-ttu-id="2fb6e-268">DigitalPersona 복합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-268">DigitalPersona Composite Authentication</span></span>  

<span data-ttu-id="2fb6e-269">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-269">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-270">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-270">Client</span></span> | <span data-ttu-id="2fb6e-271">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-271">Support</span></span> | <span data-ttu-id="2fb6e-272">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-272">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-273">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-273">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-274">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-274">Supported</span></span> |<span data-ttu-id="2fb6e-275">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-275">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="2fb6e-276">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-276">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-277">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-277">Supported</span></span> |<span data-ttu-id="2fb6e-278">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-278">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="2fb6e-279">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-279">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-280">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-280">Supported</span></span> |<span data-ttu-id="2fb6e-281">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-281">None</span></span> |

<span data-ttu-id="2fb6e-282">자세한 내용은 [DigitalPersona 복합 인증](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-282">For more information see [DigitalPersona Composite Authentication](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).</span></span>


## <a name="ibm-tivoli-federated-identity-manager-622"></a><span data-ttu-id="2fb6e-283">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="2fb6e-283">IBM Tivoli Federated Identity Manager 6.2.2</span></span>

<span data-ttu-id="2fb6e-284">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-284">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-285">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-285">Client</span></span> | <span data-ttu-id="2fb6e-286">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-286">Support</span></span> | <span data-ttu-id="2fb6e-287">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-287">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-288">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-288">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-289">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-289">Supported</span></span> |<span data-ttu-id="2fb6e-290">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-290">None</span></span> |
| <span data-ttu-id="2fb6e-291">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-291">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-292">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-292">Supported</span></span> |<span data-ttu-id="2fb6e-293">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-293">None</span></span> |
| <span data-ttu-id="2fb6e-294">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-294">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-295">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-295">Supported</span></span> |<span data-ttu-id="2fb6e-296">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-296">None</span></span> |

<span data-ttu-id="2fb6e-297">IBM Tivoli Federated Identity Manager에 대한 자세한 내용은 [Microsoft 응용 프로그램용 IBM Security Access Manager](http://www-01.ibm.com/support/docview.wss?uid=swg24029517)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-297">For more information about IBM Tivoli Federated Identity Manager, see [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).</span></span>

## <a name="icewall-federation-version-30"></a><span data-ttu-id="2fb6e-298">IceWall Federation 버전 3.0</span><span class="sxs-lookup"><span data-stu-id="2fb6e-298">IceWall Federation Version 3.0</span></span>

<span data-ttu-id="2fb6e-299">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-299">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-300">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-300">Client</span></span> | <span data-ttu-id="2fb6e-301">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-301">Support</span></span> | <span data-ttu-id="2fb6e-302">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-302">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-303">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-303">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-304">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-304">Supported</span></span> |<span data-ttu-id="2fb6e-305">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-305">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-306">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-306">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-307">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-307">Supported</span></span> |<span data-ttu-id="2fb6e-308">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-308">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-309">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-309">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-310">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-310">Supported</span></span> |<span data-ttu-id="2fb6e-311">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-311">None</span></span> |

<span data-ttu-id="2fb6e-312">IceWall Federation에 대한 자세한 내용은 [IceWall Federation 버전 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) 및 [Office 365를 사용하여 IceWall Federation](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-312">For more information about IceWall Federation, see [IceWall Federation Version 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) and [IceWall Federation with Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).</span></span>

## <a name="memority"></a><span data-ttu-id="2fb6e-313">Memority</span><span class="sxs-lookup"><span data-stu-id="2fb6e-313">Memority</span></span>

<span data-ttu-id="2fb6e-314">hello 다음은이 로그온 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-314">hello following is hello scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-315">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-315">Client</span></span> | <span data-ttu-id="2fb6e-316">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-316">Support</span></span> | <span data-ttu-id="2fb6e-317">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-317">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-318">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-318">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-319">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-319">Supported</span></span> |<span data-ttu-id="2fb6e-320">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-320">None</span></span> |
| <span data-ttu-id="2fb6e-321">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-321">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-322">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-322">Supported</span></span> |<span data-ttu-id="2fb6e-323">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-323">None</span></span> |
| <span data-ttu-id="2fb6e-324">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-324">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-325">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-325">Supported</span></span> |<span data-ttu-id="2fb6e-326">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-326">None</span></span> |

<span data-ttu-id="2fb6e-327">Memority 사용에 대한 자세한 내용은 [Memority](http://www.memority.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-327">For more information about using Memority see [Memority](http://www.memority.com).</span></span>


## <a name="netiq-access-manager-4x"></a><span data-ttu-id="2fb6e-328">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-328">NetIQ Access Manager 4.x</span></span>

<span data-ttu-id="2fb6e-329">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-329">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-330">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-330">Client</span></span> | <span data-ttu-id="2fb6e-331">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-331">Support</span></span> | <span data-ttu-id="2fb6e-332">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-332">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-333">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-333">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-334">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-334">Supported</span></span> |<span data-ttu-id="2fb6e-335">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-335">None</span></span>|
| <span data-ttu-id="2fb6e-336">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-336">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-337">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-337">Supported</span></span> |<span data-ttu-id="2fb6e-338">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-338">None</span></span>|
| <span data-ttu-id="2fb6e-339">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-339">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-340">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-340">Supported</span></span> |<span data-ttu-id="2fb6e-341">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-341">None</span></span> |

<span data-ttu-id="2fb6e-342">자세한 내용은 [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-342">For more information, see [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).</span></span>

## <a name="okta"></a><span data-ttu-id="2fb6e-343">Okta</span><span class="sxs-lookup"><span data-stu-id="2fb6e-343">Okta</span></span>

<span data-ttu-id="2fb6e-344">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-344">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-345">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-345">Client</span></span> | <span data-ttu-id="2fb6e-346">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-346">Support</span></span> | <span data-ttu-id="2fb6e-347">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-347">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-348">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-348">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-349">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-349">Supported</span></span> |<span data-ttu-id="2fb6e-350">Windows 통합 인증에는 추가 웹 서버 및 Okta 응용 프로그램 설치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-350">Integrated Windows Authentication requires setup of additional web server and Okta application.</span></span> |
| <span data-ttu-id="2fb6e-351">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-351">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-352">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-352">Supported</span></span> |<span data-ttu-id="2fb6e-353">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-353">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="2fb6e-354">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-354">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-355">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-355">Supported</span></span> |<span data-ttu-id="2fb6e-356">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-356">None</span></span> |

<span data-ttu-id="2fb6e-357">Okta에 대한 자세한 내용은 [Okta](https://www.okta.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-357">For more information about Okta, see [Okta](https://www.okta.com/).</span></span>

## <a name="onelogin"></a><span data-ttu-id="2fb6e-358">OneLogin</span><span class="sxs-lookup"><span data-stu-id="2fb6e-358">OneLogin</span></span>

<span data-ttu-id="2fb6e-359">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-359">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-360">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-360">Client</span></span> | <span data-ttu-id="2fb6e-361">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-361">Support</span></span> | <span data-ttu-id="2fb6e-362">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-362">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-363">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-363">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-364">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-364">Supported</span></span> |<span data-ttu-id="2fb6e-365">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-365">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="2fb6e-366">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-366">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-367">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-367">Supported</span></span> |<span data-ttu-id="2fb6e-368">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-368">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="2fb6e-369">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-369">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-370">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-370">Supported</span></span> |<span data-ttu-id="2fb6e-371">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-371">None</span></span> |

<span data-ttu-id="2fb6e-372">OneLogin에 대한 자세한 내용은 [OneLogin](https://www.onelogin.com/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-372">For more information about OneLogin, see [OneLogin](https://www.onelogin.com/).</span></span>

## <a name="optimal-idm-virtual-identity-server-federation-services"></a><span data-ttu-id="2fb6e-373">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="2fb6e-373">Optimal IDM Virtual Identity Server Federation Services</span></span>

<span data-ttu-id="2fb6e-374">hello 다음이 single sign-on 환경을 시나리오 지원 매트릭스 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-374">hello following is hello scenario support matrix this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-375">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-375">Client</span></span> | <span data-ttu-id="2fb6e-376">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-376">Support</span></span> | <span data-ttu-id="2fb6e-377">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-377">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-378">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-378">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-379">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-379">Supported</span></span> |<span data-ttu-id="2fb6e-380">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-380">None</span></span> |
| <span data-ttu-id="2fb6e-381">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-381">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-382">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-382">Supported</span></span> |<span data-ttu-id="2fb6e-383">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-383">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="2fb6e-384">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-384">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-385">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-385">Supported</span></span> |

<span data-ttu-id="2fb6e-386">클라이언트에 대 한 자세한 정보에 대 한 액세스 정책을 참조 [액세스 제한 tooOffice 365 서비스 hello hello 클라이언트의 위치에 따라](https://technet.microsoft.com/library/hh526961.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-386">For more information about client access polices see [Limiting Access tooOffice 365 Services Based on hello Location of hello Client](https://technet.microsoft.com/library/hh526961.aspx).</span></span>





## <a name="pingfederate-611-72-8x"></a><span data-ttu-id="2fb6e-387">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-387">PingFederate 6.11, 7.2, 8.x</span></span>

<span data-ttu-id="2fb6e-388">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-388">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-389">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-389">Client</span></span> | <span data-ttu-id="2fb6e-390">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-390">Support</span></span> | <span data-ttu-id="2fb6e-391">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-391">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-392">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-392">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-393">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-393">Supported</span></span> |<span data-ttu-id="2fb6e-394">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-394">None</span></span> |
| <span data-ttu-id="2fb6e-395">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-395">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-396">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-396">Supported</span></span> |<span data-ttu-id="2fb6e-397">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-397">None</span></span> |
| <span data-ttu-id="2fb6e-398">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-398">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-399">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-399">Supported</span></span> |<span data-ttu-id="2fb6e-400">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-400">None</span></span> |

<span data-ttu-id="2fb6e-401">Tooyour Active Directory 사용자에 대 한 hello PingFederate 지침은 어떻게 tooconfigure이 STS tooprovide hello single sign on 환경을 hello 다음 중 하나를 참조:</span><span class="sxs-lookup"><span data-stu-id="2fb6e-401">For hello PingFederate instructions on how tooconfigure this STS tooprovide hello single sign-on experience tooyour Active Directory users, see one of hello following:</span></span> 

- [<span data-ttu-id="2fb6e-402">PingFederate 6.11</span><span class="sxs-lookup"><span data-stu-id="2fb6e-402">PingFederate 6.11</span></span>](http://go.microsoft.com/fwlink/?LinkID=266321)
- [<span data-ttu-id="2fb6e-403">PingFederate 7.2</span><span class="sxs-lookup"><span data-stu-id="2fb6e-403">PingFederate 7.2</span></span>](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [<span data-ttu-id="2fb6e-404">PingFederate 8.x</span><span class="sxs-lookup"><span data-stu-id="2fb6e-404">PingFederate 8.x</span></span>](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a><span data-ttu-id="2fb6e-405">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="2fb6e-405">RadiantOne CFS 3.0</span></span>

<span data-ttu-id="2fb6e-406">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-406">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-407">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-407">Client</span></span> | <span data-ttu-id="2fb6e-408">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-408">Support</span></span> | <span data-ttu-id="2fb6e-409">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-409">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-410">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-410">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-411">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-411">Supported</span></span> |<span data-ttu-id="2fb6e-412">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-412">None</span></span> |
| <span data-ttu-id="2fb6e-413">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-413">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-414">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-414">Supported</span></span> |<span data-ttu-id="2fb6e-415">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="2fb6e-415">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="2fb6e-416">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-416">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-417">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-417">Supported</span></span> |<span data-ttu-id="2fb6e-418">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-418">None</span></span> |

<span data-ttu-id="2fb6e-419">RadiantOne CFS에 대한 자세한 내용은 [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-419">For more information about RadiantOne CFS, see [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).</span></span>

## <a name="sailpoint-identitynow"></a><span data-ttu-id="2fb6e-420">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="2fb6e-420">Sailpoint IdentityNow</span></span>

<span data-ttu-id="2fb6e-421">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-421">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-422">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-422">Client</span></span> | <span data-ttu-id="2fb6e-423">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-423">Support</span></span> | <span data-ttu-id="2fb6e-424">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-424">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-425">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-425">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-426">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-426">Supported</span></span> |<span data-ttu-id="2fb6e-427">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-427">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-428">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-428">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-429">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-429">Supported</span></span> |<span data-ttu-id="2fb6e-430">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-430">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-431">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-431">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-432">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-432">Supported</span></span> |<span data-ttu-id="2fb6e-433">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-433">None</span></span> |

<span data-ttu-id="2fb6e-434">자세한 내용은 [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-434">For more information, see [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).</span></span>

## <a name="secureauth-idp-720"></a><span data-ttu-id="2fb6e-435">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="2fb6e-435">SecureAuth IdP 7.2.0</span></span>

<span data-ttu-id="2fb6e-436">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-436">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="2fb6e-437">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-437">Client</span></span> | <span data-ttu-id="2fb6e-438">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-438">Support</span></span> | <span data-ttu-id="2fb6e-439">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-439">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-440">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-440">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-441">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-441">Supported</span></span> |<span data-ttu-id="2fb6e-442">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-442">None</span></span> |
| <span data-ttu-id="2fb6e-443">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-443">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-444">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-444">Supported</span></span> |<span data-ttu-id="2fb6e-445">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-445">None</span></span> |
| <span data-ttu-id="2fb6e-446">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-446">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-447">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-447">Supported</span></span> |<span data-ttu-id="2fb6e-448">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-448">None</span></span> |

<span data-ttu-id="2fb6e-449">SecureAuth에 대한 자세한 내용은 [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-449">For more information about SecureAuth, see [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).</span></span>














## <a name="signgo-53"></a><span data-ttu-id="2fb6e-450">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="2fb6e-450">Sign&go 5.3</span></span>

<span data-ttu-id="2fb6e-451">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-451">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-452">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-452">Client</span></span> | <span data-ttu-id="2fb6e-453">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-453">Support</span></span> | <span data-ttu-id="2fb6e-454">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-454">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-455">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-455">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-456">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-456">Supported</span></span> |<span data-ttu-id="2fb6e-457">Kerberos 계약 지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-457">Kerberos Contracts supported</span></span> |
| <span data-ttu-id="2fb6e-458">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-458">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-459">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-459">Supported</span></span> |<span data-ttu-id="2fb6e-460">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-460">None</span></span> |
| <span data-ttu-id="2fb6e-461">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-461">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-462">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-462">Supported</span></span> |<span data-ttu-id="2fb6e-463">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-463">None</span></span> |

<span data-ttu-id="2fb6e-464">Sign&go 5.3은 Kerberos 계약 구성을 통해 Kerberos 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-464">Sign&go 5.3 supports Kerberos authentication via configuration of a Kerberos Contract.</span></span>  <span data-ttu-id="2fb6e-465">이 구성 사용 하 여 도움이 필요한 경우 Ilex 또는 보기 hello 설치 가이드를 문의 하십시오 [sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)</span><span class="sxs-lookup"><span data-stu-id="2fb6e-465">For assistance with this configuration, please contact Ilex or view hello setup guide [Sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)</span></span>

## <a name="softbank-technology-online-service-gate"></a><span data-ttu-id="2fb6e-466">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="2fb6e-466">SoftBank Technology Online Service Gate</span></span>

<span data-ttu-id="2fb6e-467">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-467">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-468">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-468">Client</span></span> | <span data-ttu-id="2fb6e-469">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-469">Support</span></span> | <span data-ttu-id="2fb6e-470">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-470">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-471">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-471">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-472">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-472">Supported</span></span> |<span data-ttu-id="2fb6e-473">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-473">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-474">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-474">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-475">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-475">Supported</span></span> |<span data-ttu-id="2fb6e-476">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-476">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-477">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-477">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-478">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-478">Supported</span></span> |<span data-ttu-id="2fb6e-479">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-479">None</span></span> |

<span data-ttu-id="2fb6e-480">SoftBank Technology Online Service Gate에 대한 자세한 내용은 [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-480">For more information about SoftBank Technology Online Service Gate see [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)</span></span>

## <a name="vmware-workspace-one"></a><span data-ttu-id="2fb6e-481">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="2fb6e-481">VMware Workspace One</span></span>

<span data-ttu-id="2fb6e-482">hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-482">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="2fb6e-483">클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-483">Client</span></span> | <span data-ttu-id="2fb6e-484">지원</span><span class="sxs-lookup"><span data-stu-id="2fb6e-484">Support</span></span> | <span data-ttu-id="2fb6e-485">예외</span><span class="sxs-lookup"><span data-stu-id="2fb6e-485">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fb6e-486">Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-486">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="2fb6e-487">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-487">Supported</span></span> |<span data-ttu-id="2fb6e-488">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-488">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-489">Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2fb6e-489">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="2fb6e-490">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-490">Supported</span></span> |<span data-ttu-id="2fb6e-491">Windows 통합 인증은 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-491">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="2fb6e-492">Outlook 및 ActiveSync와 같은 메일 리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2fb6e-492">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="2fb6e-493">지원됨</span><span class="sxs-lookup"><span data-stu-id="2fb6e-493">Supported</span></span> |<span data-ttu-id="2fb6e-494">없음</span><span class="sxs-lookup"><span data-stu-id="2fb6e-494">None</span></span> |

<span data-ttu-id="2fb6e-495">자세한 내용은 [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb6e-495">For more information about see [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)</span></span>

