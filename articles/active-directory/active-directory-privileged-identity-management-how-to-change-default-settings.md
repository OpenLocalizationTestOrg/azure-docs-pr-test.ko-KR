---
title: "역할 활성화 설정을 관리하는 방법 | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management 확장을 사용하여 권한 있는 ID에 대한 기본 설정을 변경하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="0ae32-103">Azure AD Privileged Identity Management에서 역할 활성화 설정을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="0ae32-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="0ae32-104">권한 있는 역할 관리자는 적격 역할 할당을 활성화한 사용자의 환경을 변경하는 등, 해당 조직에서 Azure AD PIM(Privileged Identity Management)을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="0ae32-105">역할 활성화 설정 관리</span><span class="sxs-lookup"><span data-stu-id="0ae32-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="0ae32-106">[Azure 포털](https://portal.azure.com) 로 이동하여 대시보드에서 **Azure AD Privileged Identity Management** 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="0ae32-107">**권한 있는 역할 관리** > **설정** > **권한 있는 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="0ae32-108">관리하려는 설정의 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="0ae32-109">각 역할에 대한 설정 페이지에서 여러 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="0ae32-110">이러한 설정은 영구 관리자가 아닌, 적격 관리자인 사용자에게만 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="0ae32-111">**활성화**: 역할이 만료되기 전에 활성 상태로 지속되는 시간(시 단위).</span><span class="sxs-lookup"><span data-stu-id="0ae32-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="0ae32-112">이는 1 ~ 72시간 사이가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="0ae32-113">**알림**: 시스템에서 관리자에게 역할을 활성화했는지 확인하는 전자 메일을 전송하게 할지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="0ae32-114">이 정보는 무단 또는 불법 활성화를 탐지하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="0ae32-115">**인시던트/요청 티켓**: 적격 관리자에게 역할을 활성화할 때 티켓 번호를 포함하도록 요구할지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="0ae32-116">이 기능은 역할 액세스 감사를 수행할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="0ae32-117">**Multi-Factor Authentication**: 사용자에게 역할을 활성화하기 전에 MFA로 id를 확인하도록 할지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="0ae32-118">이 작업은 매번 역할을 활성화할 때마다가 아니라 세션당 한 번만 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="0ae32-119">MFA를 사용할 때 염두에 두어야 할 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="0ae32-120">전자 메일 주소에 대 한 Microsoft 계정을 가진 사용자 (일반적으로 @outlook.com, 항상 그렇지는 않지만) Azure MFA에 대해 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="0ae32-121">Microsoft 계정 가진 사용자에게 역할을 할당하려는 경우, 영구 관리자가 되도록 하거나 해당 역할에 대해 MFA를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="0ae32-122">Azure AD 및 Office365에 대해 높은 권한이 있는 역할에 대한 MFA를 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="0ae32-123">이런 안전 기능을 둔 것은 이러한 역할을 신중하게 보호해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0ae32-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="0ae32-124">응용 프로그램 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-124">Application administrator</span></span>
  * <span data-ttu-id="0ae32-125">응용 프로그램 프록시 서버 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="0ae32-126">대금 청구 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-126">Billing administrator</span></span>  
  * <span data-ttu-id="0ae32-127">규정 준수 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-127">Compliance administrator</span></span>  
  * <span data-ttu-id="0ae32-128">CRM 서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-128">CRM service administrator</span></span>
  * <span data-ttu-id="0ae32-129">고객 LockBox 액세스 승인자</span><span class="sxs-lookup"><span data-stu-id="0ae32-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="0ae32-130">디렉터리 기록기</span><span class="sxs-lookup"><span data-stu-id="0ae32-130">Directory writer</span></span>  
  * <span data-ttu-id="0ae32-131">Exchange 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-131">Exchange administrator</span></span>  
  * <span data-ttu-id="0ae32-132">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-132">Global administrator</span></span>
  * <span data-ttu-id="0ae32-133">Intune 서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-133">Intune service administrator</span></span>
  * <span data-ttu-id="0ae32-134">사서함 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="0ae32-135">파트너 계층1 지원</span><span class="sxs-lookup"><span data-stu-id="0ae32-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="0ae32-136">파트너 계층2 지원</span><span class="sxs-lookup"><span data-stu-id="0ae32-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="0ae32-137">권한 있는 역할 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="0ae32-138">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-138">Security administrator</span></span>  
  * <span data-ttu-id="0ae32-139">SharePoint 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="0ae32-140">비즈니스용 Skype 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="0ae32-141">사용자 계정 관리자</span><span class="sxs-lookup"><span data-stu-id="0ae32-141">User account administrator</span></span>  

<span data-ttu-id="0ae32-142">PIM과 함께 MFA를 사용하는 방법에 대한 자세한 내용은 [MFA를 요구하는 방법](active-directory-privileged-identity-management-how-to-require-mfa.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ae32-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="0ae32-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ae32-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

