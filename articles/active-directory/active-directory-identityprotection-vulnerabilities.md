---
title: "Azure Active Directory ID 보호에서 검색하는 취약성 | Microsoft Docs"
description: "Azure Active Directory ID 보호에서 검색하는 취약성에 대한 개요입니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="fa753-104">Azure Active Directory ID 보호에서 검색하는 취약성</span><span class="sxs-lookup"><span data-stu-id="fa753-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="fa753-105">취약점은 공격자에 의해 악용될 수 있는 환경의 단점입니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="fa753-106">이러한 취약성을 해결하여 조직에서 보안 상태를 개선하고 공격자가 이러한 취약성을 악용하지 않도록 방지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="fa753-107">![취약성](./media/active-directory-identityprotection-vulnerabilities/101.png "취약성")</span><span class="sxs-lookup"><span data-stu-id="fa753-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="fa753-108">다음 섹션에서는 ID 보호에서 보고하는 취약성에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="fa753-109">Multi-Factor Authentication 등록 구성되지 않음</span><span class="sxs-lookup"><span data-stu-id="fa753-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="fa753-110">이 취약점을 사용하면 조직에서 Azure Multi-Factor Authentication의 배포를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="fa753-111">Multi-Factor Authentication은 사용자 인증에 두 번째 계층의 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="fa753-112">간단한 로그인 프로세스에 대한 사용자 요구를 충족하는 동안 데이터와 응용 프로그램에 대한 액세스를 보호하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="fa753-113">전화 통화, 문자 메시지 또는 모바일 앱 알림 또는 확인 코드 및 타사 OATH 토큰과 같은 다양한 손쉬운 확인 옵션을 통해 강력한 인증을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="fa753-114">사용자 로그인에 Azure Multi-Factor Authentication을 요구하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="fa753-115">다단계 인증은 ID 보호를 통해 사용할 수 있는 위험 기반 조건부 액세스 정책에서 중요한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="fa753-116">자세한 세부 내용은 [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fa753-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="fa753-117">관리되지 않은 클라우드 앱</span><span class="sxs-lookup"><span data-stu-id="fa753-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="fa753-118">이 취약점을 사용하면 조직에서 관리되지 않은 클라우드 앱을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="fa753-119">오늘날 기업에서 IT 부서는 해당 조직의 사용자가 작업하는 데 사용하고 있는 일부 클라우드 응용 프로그램을 인지하지 못하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="fa753-120">관리자가 회사 데이터에 대한 무단 액세스, 데이터 유출 가능성 및 기타 보안 위험에 대해 우려하는 원인을 쉽게 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="fa753-121">Azure Active Directory를 사용하여 관리되지 않은 클라우드 응용 프로그램을 검색하고 이러한 응용 프로그램을 관리하도록 조직에서 클라우드 앱 검색을 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="fa753-122">자세한 내용은 [Cloud App Discovery를 사용하여 관리되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa753-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="fa753-123">Privileged Identity Management에서 보안 경고</span><span class="sxs-lookup"><span data-stu-id="fa753-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="fa753-124">이 취약점을 사용하여 조직에서 권한있는 ID에 대한 경고를 검색하고 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="fa753-125">사용자가 권한이 필요한 작업을 수행할 수 있도록 조직에서는 Azure AD, Azure 또는 Office 365 리소스에서 기타 SaaS 앱에 대한 임시 또는 영구 액세스 권한을 사용자에게 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="fa753-126">이러한 권한이 있는 사용자는 조직의 공격에 대한 취약성을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="fa753-127">이 취약점을 사용하여 불필요한 액세스 권한이 있는 사용자를 식별하고 적절한 조치를 취해 이들이 미치는 위험을 줄이고 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="fa753-128">조직에서 Azure AD Privileged Identity Management를 사용하여 Azure AD 및 기타 Microsoft 온라인 서비스(Office 365 또는 Microsoft Intune 등)에서 권한 있는 ID 및 리소스에 대한 액세스를 관리, 제어, 모니터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="fa753-129">자세한 내용은 [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa753-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="fa753-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fa753-130">See also</span></span>
* [<span data-ttu-id="fa753-131">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="fa753-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

