---
title: "Azure Active Directory Id 보호에서 검색 aaaVulnerabilities | Microsoft Docs"
description: "Azure Active Directory Id 보호에서 검색 하는 hello 취약점의 개요를 제공 합니다."
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
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="4ecbe-104">Azure Active Directory ID 보호에서 검색하는 취약성</span><span class="sxs-lookup"><span data-stu-id="4ecbe-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="4ecbe-105">취약점은 공격자에 의해 악용될 수 있는 환경의 단점입니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="4ecbe-106">이러한 취약점 tooimprove hello 보안 상태, 조직의 해결 공격자가 이러한를 이용 하지 못하게 방지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="4ecbe-107">![취약성](./media/active-directory-identityprotection-vulnerabilities/101.png "취약성")</span><span class="sxs-lookup"><span data-stu-id="4ecbe-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="4ecbe-108">hello 다음 섹션에서는 제공 Id 보호에서 보고 하는 hello 취약점의 개요.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="4ecbe-109">Multi-Factor Authentication 등록 구성되지 않음</span><span class="sxs-lookup"><span data-stu-id="4ecbe-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="4ecbe-110">이 취약점을 사용 하면 조직에서 Azure Multi-factor Authentication의 hello 배포를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="4ecbe-111">Azure multi-factor authentication 인증 보안 toouser 인증의 두 번째 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="4ecbe-112">간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="4ecbe-113">전화 통화, 문자 메시지 또는 모바일 앱 알림 또는 확인 코드 및 타사 OATH 토큰과 같은 다양한 손쉬운 확인 옵션을 통해 강력한 인증을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="4ecbe-114">사용자 로그인에 Azure Multi-Factor Authentication을 요구하는 것이 좋습니다. 다단계 인증은 ID 보호를 통해 사용할 수 있는 위험 기반 조건부 액세스 정책에서 중요한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="4ecbe-115">자세한 세부 내용은 [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4ecbe-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="4ecbe-116">관리되지 않은 클라우드 앱</span><span class="sxs-lookup"><span data-stu-id="4ecbe-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="4ecbe-117">이 취약점을 사용하면 조직에서 관리되지 않은 클라우드 앱을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="4ecbe-118">오늘날의 기업에서 IT 부서에서는 인식 하지 않습니다 종종의 사용자가 조직에는 사용할 수 있도록 toodo 작업 된 모든 hello 클라우드 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="4ecbe-119">쉽게 toosee 이유 관리자 toocorporate 데이터를 무단된 액세스, 가능한 데이터 누수 및 기타 보안 위험에 대 한 질문이 있을 경우합니다</span><span class="sxs-lookup"><span data-stu-id="4ecbe-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="4ecbe-120">조직 Cloud App Discovery 관리 되지 않는 toodiscover 클라우드 응용 프로그램 및 배포 toomanage 이러한 응용 프로그램을 Azure Active Directory를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="4ecbe-121">자세한 내용은 [Cloud App Discovery를 사용하여 관리되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="4ecbe-122">Privileged Identity Management에서 보안 경고</span><span class="sxs-lookup"><span data-stu-id="4ecbe-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="4ecbe-123">이 취약점을 사용하여 조직에서 권한있는 ID에 대한 경고를 검색하고 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="4ecbe-124">권한 있는 작업 tooenable 사용자 toocarry, 조직에서는 Azure AD에서 임시 또는 영구 권한 액세스 toogrant 사용자 해야 Azure 또는 Office 365 리소스 또는 다른 SaaS 앱.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="4ecbe-125">각각의 조직 이러한 권한 있는 사용자가 증가 hello 공격 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="4ecbe-126">이 취약점을 사용 하면 불필요 한 권한 있는 액세스 권한이 있는 사용자를 식별 및 tooreduce 적절 한 조치를 수행 하거나 미치는 hello 위험 제거를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="4ecbe-127">Azure AD Privileged Identity Management toomanage, 컨트롤 및 권한 있는 모니터 identities 및 Azure AD에서 자신의 액세스 tooresources로 Office 365 또는 Microsoft Intune과 같은 기타 Microsoft online services 조직에서 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="4ecbe-128">자세한 내용은 [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ecbe-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="4ecbe-129">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4ecbe-129">See also</span></span>
* [<span data-ttu-id="4ecbe-130">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="4ecbe-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

