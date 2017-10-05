---
title: "다단계 인증을 요구하는 방법 | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management 확장을 사용하여 권한 있는 ID에 대해 MFA(Multi-Factor Authentication)를 요구하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: b778774fa23be8219db3f716d79bac324a7de9d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-require-mfa-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="092e0-103">Azure AD Privileged Identity Management에서 MFA를 요구하는 방법</span><span class="sxs-lookup"><span data-stu-id="092e0-103">How to require MFA in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="092e0-104">모든 관리자에 대해 Multi-Factor Authentication(MFA)을 요구하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-104">We recommend that you require multi-factor authentication (MFA) for all of your administrators.</span></span> <span data-ttu-id="092e0-105">이렇게 하면 손상된 암호로 인한 공격의 위험이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-105">This reduces the risk of an attack due to a compromised password.</span></span>

<span data-ttu-id="092e0-106">사용자가 로그인할 때 MFA 챌린지를 완료하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-106">You can require that users complete an MFA challenge when they sign in.</span></span> <span data-ttu-id="092e0-107">블로그 게시물 [MFA for Office 365 and MFA for Azure(Office 365용 MFA 및 Azure용 MFA)](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) 에서는 Microsoft Azure Multi-Factor Authentication 제공에 포함된 기능과 Office 및 Azure 구독에 포함된 항목을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-107">The blog post [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compares what is included in Office and Azure subscriptions, with the features contained in the Microsoft Azure Multi-Factor Authentication offering.</span></span>

<span data-ttu-id="092e0-108">사용자가 Azure AD PIM의 역할을 활성화하는 경우 MFA 챌린지를 완료하도록 요구할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-108">You can also require that users complete an MFA challenge when they activate a role in Azure AD PIM.</span></span> <span data-ttu-id="092e0-109">이러한 방식으로 사용자가 로그인 시 MFA 챌린지를 완료하지 않은 경우 PIM에서 이 작업을 수행하도록 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-109">This way, if the user didn't complete an MFA challenge when they signed in, they will be prompted to do so by PIM.</span></span>

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="092e0-110">Azure AD Privileged Identity Management에서 MFA 요구</span><span class="sxs-lookup"><span data-stu-id="092e0-110">Requiring MFA in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="092e0-111">권한 있는 역할 관리자가 PIM의 ID를 관리하는 경우 권한 있는 계정에 대해 MFA를 권장하는 경고가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-111">When you manage identities in PIM as a privileged role administrator, you may see alerts that recommend MFA for privileged accounts.</span></span> <span data-ttu-id="092e0-112">PIM 대시보드에서 보안 경고를 클릭하면 MFA가 필요한 관리자 계정 목록이 포함된 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-112">Click the security alert in the PIM dashboard, and a new blade will open with a list of the administrator accounts that should require MFA.</span></span>  <span data-ttu-id="092e0-113">여러 역할을 선택하고 **수정** 단추를 클릭하여 MFA를 요구하거나, 개별 역할 옆에 있는 줄임표를 클릭한 다음 **수정** 단추를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-113">You can require MFA by selecting multiple roles and then clicking the **Fix** button, or you can click the ellipses next to individual roles and then click the **Fix** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="092e0-114">현재, Azure MFA는 회사 또는 학교 계정에서만 작동하며 Microsoft 계정 (일반적으로 Skype, Xbox, Outlook.com 등과 같은 Microsoft 서비스에 로그인하는 데 사용되는 개인 계정)에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-114">Right now, Azure MFA only works with work or school accounts, not Microsoft accounts (usually a personal account that's used to sign in to Microsoft services like Skype, Xbox, Outlook.com, etc.).</span></span> <span data-ttu-id="092e0-115">이 때문에 Microsoft 계정을 사용하는 사용자는 MFA를 사용하여 해당 역할을 활성화할 수 없기 때문에 적격 관리자가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-115">Because of this, anyone using a Microsoft account can't be an eligible admin because they can't use MFA to activate their roles.</span></span> <span data-ttu-id="092e0-116">이 사용자들이 Microsoft 계정을 사용하여 계속 워크로드를 관리해야 하는 경우 영구 관리자로 승격하세요.</span><span class="sxs-lookup"><span data-stu-id="092e0-116">If these users need to continue managing workloads using a Microsoft account, elevate them to permanent administrators for now.</span></span>
> 
> 

<span data-ttu-id="092e0-117">또한 PIM 대시보드의 역할 섹션에서 클릭하여 특정 역할에 대한 MFA 요구 사항을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-117">Additionally, you can change the MFA requirement for a specific role by clicking on it in the Roles section of the PIM dashboard.</span></span> <span data-ttu-id="092e0-118">역할 블레이드에서 **설정**을 클릭한 다음 다단계 인증 아래 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-118">Then, click on **Settings** in the role blade and then selecting **Enable** under multi-factor authentication.</span></span>

## <a name="how-azure-ad-pim-validates-mfa"></a><span data-ttu-id="092e0-119">Azure AD PIM에서 MFA의 유효성을 검사하는 방법</span><span class="sxs-lookup"><span data-stu-id="092e0-119">How Azure AD PIM validates MFA</span></span>
<span data-ttu-id="092e0-120">사용자가 역할을 활성화할 때 MFA 유효성을 검사하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-120">There are two options for validating MFA when a user activates a role.</span></span>

<span data-ttu-id="092e0-121">가장 간단한 옵션은 권한 있는 역할을 활성화하는 사용자에 대해 Azure MFA를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-121">The simplest option is to rely on Azure MFA for users who are activating a privileged role.</span></span> <span data-ttu-id="092e0-122">이렇게 하려면 먼저 해당 사용자에게 사용이 허가되었는지와 Azure MFA에 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-122">To do this, first check that those users are licensed, if necessary, and have registered for Azure MFA.</span></span> <span data-ttu-id="092e0-123">이 방법에 대한 자세한 내용은 [클라우드에서 Azure Multi-Factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="092e0-123">More information on how to do this is in [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span> <span data-ttu-id="092e0-124">이러한 사용자가 로그인할 때 MFA를 적용하도록 Azure AD를 구성하는 것이 좋지만 필수 사항은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-124">It is recommended, but not required, that you configure Azure AD to enforce MFA for these users when they sign in.</span></span> <span data-ttu-id="092e0-125">MFA 검사가 Azure AD PIM 자체에서도 수행되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-125">This is because the MFA checks will be made by Azure AD PIM itself.</span></span>

<span data-ttu-id="092e0-126">또는 사용자가 온-프레미스를 인증하는 경우 MFA에 대해 책임지는 ID 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-126">Alternatively, if users authenticate on-premises you can have your identity provider be responsible for MFA.</span></span> <span data-ttu-id="092e0-127">예를 들어 Azure AD에 액세스하기 전에 스마트 카드 기반 인증을 요구하도록 AD 페더레이션 서비스를 구성한 경우 [Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) 에 포함된 지침을 참조하여 Azure AD로 클레임을 보내도록 AD FS를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-127">For example, if you have configured AD Federation Services to require smartcard-based authentication before accessing Azure AD, [Securing cloud resources with Azure Multi-Factor Authentication and AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) includes instructions for configuring AD FS to send claims to Azure AD.</span></span> <span data-ttu-id="092e0-128">사용자가 역할을 활성화하려고 할 때 Azure AD PIM은 해당 클레임을 받으면 사용자에 대해 MFA의 유효성이 이미 검사되었다는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="092e0-128">When a user tries to activate a role, Azure AD PIM will accept that MFA has already been validated for the user once it receives the appropriate claims.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="092e0-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="092e0-129">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

