---
title: "Azure AD Privileged Identity Management의 역할 | Microsoft Docs"
description: "Azure 권위 있는 ID 관리 확장을 사용하여 권한 있는 ID에 사용되는 역할을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: c20aca4202319154b01d6398570f745636120f49
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a><span data-ttu-id="364bb-103">Azure Active Directory PIM의 다른 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="364bb-103">Different administrative role in Azure Active Directory PIM</span></span>
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

<span data-ttu-id="364bb-104">조직의 사용자를 Azure AD의 다른 관리 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-104">You can assign users in your organization to different administrative roles in Azure AD.</span></span> <span data-ttu-id="364bb-105">이러한 역할 할당은 사용자를 추가 또는 제거하거나 서비스 설정을 변경하는 등 사용자가 Azure AD, Office 365, 기타 Microsoft Online Services, 연결된 응용 프로그램에서 수행할 수 있는 작업을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-105">These role assignments control which tasks, such as adding or removing users or changing service settings, the users are able to perform on Azure AD, Office 365 and other Microsoft Online Services and connected applications.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="364bb-106">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="364bb-107">전역 관리자는 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)에 설명된 대로 `Add-MsolRoleMember` 및 `Remove-MsolRoleMember` 등의 PowerShell cmdlet을 사용하거나 클래식 포털을 통해 Azure AD에서 역할에 **영구적**으로 할당되는 사용자를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-107">A global administrator can update which users are **permanently** assigned to roles in Azure AD, using PowerShell cmdlets such as `Add-MsolRoleMember` and `Remove-MsolRoleMember`, or through the classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="364bb-108">Azure AD Privileged Identity Management(PIM)는 Azure AD에서 사용자에 대한 권한 있는 액세스의 정책을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-108">Azure AD Privileged Identity Management (PIM) manages policies for privileged access for users in Azure AD.</span></span> <span data-ttu-id="364bb-109">PIM은 Azure AD에서 사용자에게 하나 이상의 역할을 할당하고, 다른 사용자를 역할에 영구적으로 할당하거나 또는 역할에 대해 적격이 되도록 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-109">PIM assigns users to one or more roles in Azure AD, and you can assign someone to be permanently in the role, or eligible for the role.</span></span> <span data-ttu-id="364bb-110">사용자가 역할에 영구적으로 할당되거나 적격 역할 할당을 활성화하는 경우 해당 역할에 할당된 권한으로 Azure Active Directory, Office 365 및 기타 응용 프로그램을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-110">When a user is permanently assigned to a role, or activates an eligible role assignment, then they can manage Azure Active Directory, Office 365, and other applications with the permissions assigned to their roles.</span></span>

<span data-ttu-id="364bb-111">영구 및 적격 역할 할당을 비교했을 때 이 둘을 통해 다른 사람에게 주어진 액세스에는 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-111">There's no difference in the access given to someone with a permanent versus an eligible role assignment.</span></span> <span data-ttu-id="364bb-112">유일한 차이는 사람들이 그 액세스를 항상 필요로 하지 않는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-112">The only difference is that some people don't need that access all the time.</span></span> <span data-ttu-id="364bb-113">그런 사람들은 역할에 대해 적격이 되도록 하며, 언제라도 필요할 때 켜고 끄도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-113">They are made eligible for the role, and can turn it on and off whenever they need to.</span></span>

## <a name="roles-managed-in-pim"></a><span data-ttu-id="364bb-114">PIM에서 관리되는 역할</span><span class="sxs-lookup"><span data-stu-id="364bb-114">Roles managed in PIM</span></span>
<span data-ttu-id="364bb-115">Privileged Identity Management를 사용하면 사용자를 다음과 같이 일반적인 관리자 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-115">Privileged Identity Management lets you assign users to common administrator roles, including:</span></span>

* <span data-ttu-id="364bb-116">**전역 관리자** (회사 관리자라고도 함)는 모든 관리 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-116">**Global administrator** (also known as Company administrator) has access to all administrative features.</span></span> <span data-ttu-id="364bb-117">조직에는 전역 관리자가 두 개 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-117">You can have more than one global admin in your organization.</span></span> <span data-ttu-id="364bb-118">Office 365를 자동으로 구입하기 위해 등록한 사람은 전역 관리자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-118">The person who signs up to purchase Office 365 automatically becomes a global admin.</span></span>
* <span data-ttu-id="364bb-119">**권한 있는 역할 관리자** 는 Azure AD PIM을 관리하고 다른 사용자에 대한 역할 할당을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-119">**Privileged role administrator** manages Azure AD PIM and updates role assignments for other users.</span></span>  
* <span data-ttu-id="364bb-120">**대금 청구 관리자** : 구입하고, 구독을 관리하고, 지원 티켓을 관리하고, 서비스 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-120">**Billing administrator** makes purchases, manages subscriptions, manages support tickets, and monitors service health.</span></span>
* <span data-ttu-id="364bb-121">**암호 관리자** : 암호를 재설정하고, 서비스 요청을 관리하고, 서비스 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-121">**Password administrator** resets passwords, manages service requests, and monitors service health.</span></span> <span data-ttu-id="364bb-122">암호 관리자는 사용자의 암호 재설정으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-122">Password admins are limited to resetting passwords for users.</span></span>
* <span data-ttu-id="364bb-123">**서비스 관리자** : 서비스 요청을 관리하고 서비스 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-123">**Service administrator** manages service requests and monitors service health.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="364bb-124">Office 365를 사용하는 경우 사용자에게 서비스 관리자 역할을 할당하기 전에 먼저 Exchange Online 등의 서비스에 사용자 관리 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-124">If you are using Office 365, then before assigning the service admin role to a user, first assign the user administrative permissions to a service, such as Exchange Online.</span></span>
  > 
  > 
* <span data-ttu-id="364bb-125">**사용자 관리 관리자** 는 암호를 다시 설정하고, 서비스 상태를 모니터링하고, 사용자 계정과 사용자 그룹 및 서비스 요청을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-125">**User management administrator** resets passwords, monitors service health, and manages user accounts, user groups, and service requests.</span></span> <span data-ttu-id="364bb-126">사용자 관리 관리자는 전역 관리자를 삭제하거나 다른 관리자 역할을 만들거나 청구, 전역 및 서비스 관리를 위해 암호를 재설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-126">The user management admin can’t delete a global admin, create other admin roles, or reset passwords for billing, global, and service admins.</span></span>
* <span data-ttu-id="364bb-127">**Exchange 관리자** 는 Exchange 관리 센터(EAC)를 통해 Exchange Online에 대한 관리 액세스 권한을 보유하고 Exchange Online에서 거의 모든 태스크를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-127">**Exchange administrator** has administrative access to Exchange Online through the Exchange admin center (EAC), and can perform almost any task in Exchange Online.</span></span>
* <span data-ttu-id="364bb-128">**SharePoint 관리자** 는 SharePoint Online 관리 센터를 통해 SharePoint Online에 대한 관리 액세스 권한을 보유하고 SharePoint Online에서 거의 모든 태스크를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-128">**SharePoint administrator** has administrative access to SharePoint Online through the SharePoint Online admin center, and can perform almost any task in SharePoint Online.</span></span>
* <span data-ttu-id="364bb-129">**비즈니스용 Skype 관리자** 는 비즈니스용 Skype 관리 센터를 통해 비즈니스용 Skype에 대한 관리 액세스 권한을 보유하고 비즈니스용 Skype Online에서 거의 모든 태스크를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-129">**Skype for Business administrator** has administrative access to Skype for Business through the Skype for Business admin center, and can perform almost any task in Skype for Business Online.</span></span>

<span data-ttu-id="364bb-130">[Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md) 및 [Office 365에서 관리자 역할 할당](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)에 대한 자세한 내용을 보려면 이 문서를 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="364bb-130">Read these articles for more details about [assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) and [assigning admin roles in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).</span></span>

<!--**PLACEHOLDER: The above article may not be the one we want since PIM gets roles from places other that Office 365**-->


<span data-ttu-id="364bb-131">PIM에서는 사용자가 [필요할 때 역할을 활성화](active-directory-privileged-identity-management-how-to-add-role-to-user.md)할 수 있도록 [이러한 역할을 사용자에게 할당](active-directory-privileged-identity-management-how-to-activate-role.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-131">From PIM, you can [assign these roles to a user](active-directory-privileged-identity-management-how-to-add-role-to-user.md) so that the user can [activate the role when needed](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

<span data-ttu-id="364bb-132">다른 사용자가 PIM에 액세스하여 관리할 수 있도록 하려는 경우 PIM에 필요한 사용자 역할은 [PIM에 대한 액세스 권한을 제공하는 방법](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-132">If you want to give another user access to manage in PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

<!-- ## The PIM Security Administrator Role **PLACEHOLDER: Need description of the Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a><span data-ttu-id="364bb-133">PIM에서 관리되지 않는 역할</span><span class="sxs-lookup"><span data-stu-id="364bb-133">Roles not managed in PIM</span></span>
<span data-ttu-id="364bb-134">위에서 언급한 것을 제외하고 Exchange Online 또는 SharePoint Online 내에 있는 역할은 Azure AD에 표시되지 않으므로 PIM에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-134">Roles within Exchange Online or SharePoint Online, except for those mentioned above, are not represented in Azure AD and so are not visible in PIM.</span></span> <span data-ttu-id="364bb-135">이러한 Office 365 서비스에서 세분화된 역할 할당 변경에 대한 자세한 내용은 [Office 365의 사용 권한](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364bb-135">For more information on changing fine-grained role assignments in these Office 365 services, see [Permissions in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).</span></span>

<span data-ttu-id="364bb-136">Azure 구독 및 리소스 그룹도 Azure AD에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-136">Azure subscriptions and resource groups are also not represented in Azure AD.</span></span> <span data-ttu-id="364bb-137">Azure 구독을 관리하려면 [Azure 관리자 역할을 추가하거나 변경하는 방법](../billing/billing-add-change-azure-subscription-administrator.md)을 참조하고, Azure RBAC에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364bb-137">To manage Azure subscriptions, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md) and for more information on Azure RBAC see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

<!--**The above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a><span data-ttu-id="364bb-138">사용자 역할 및 로그인</span><span class="sxs-lookup"><span data-stu-id="364bb-138">User roles and signing in</span></span>
<span data-ttu-id="364bb-139">일부 Microsoft 서비스 및 응용 프로그램의 경우 사용자를 역할에 할당하는 방법만으로 사용자를 관리자로 지정하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-139">For some Microsoft services and applications, assigning a user to a role may not be sufficient to enable that user to be an administrator.</span></span>

<span data-ttu-id="364bb-140">Azure 클래식 포털에 액세스하려면 사용자가 Azure 구독을 관리하지 않더라도 사용자는 서비스 관리자이거나 Azure 구독에서 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-140">Access to the Azure classic portal requires the user be a service administrator or co-administrator on an Azure subscription, even if the user does not need to manage the Azure subscriptions.</span></span>  <span data-ttu-id="364bb-141">예를 들어 클래식 포털에서 Azure AD에 대한 구성 설정을 관리하려면 사용자는 Azure AD의 전역 관리자이고 Azure 구독에서 구독 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-141">For example, to manage configuration settings for Azure AD in the classic portal, a user must be both a global administrator in Azure AD and a subscription co-administrator on an Azure subscription.</span></span>  <span data-ttu-id="364bb-142">Azure 구독에 사용자를 추가하는 방법을 알아보려면 [Azure 관리자 역할을 추가 또는 변경하는 방법](../billing/billing-add-change-azure-subscription-administrator.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364bb-142">To learn how to add users to Azure subscriptions, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="364bb-143">Microsoft Online Services에 액세스하려면 서비스 포털을 열거나 관리 작업을 수행하기 전에 사용자에게 라이선스도 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-143">Access to Microsoft Online Services may require the user also be assigned a license before they can open the service's portal or perform administrative tasks.</span></span>

## <a name="assign-a-license-to-a-user-in-azure-ad"></a><span data-ttu-id="364bb-144">Azure AD에서 사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="364bb-144">Assign a license to a user in Azure AD</span></span>
1. <span data-ttu-id="364bb-145">전역 관리자 계정 또는 공동 관리자 계정을 사용하여 [Azure 클래식 포털](http://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-145">Sign in to the [Azure classic portal](http://manage.windowsazure.com) with a global administrator account or a co-administrator account.</span></span>
2. <span data-ttu-id="364bb-146">주 메뉴에서 **모든 항목** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-146">Select **All Items** from the main menu.</span></span>
3. <span data-ttu-id="364bb-147">연결된 라이선스가 있는, 사용하려는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-147">Select the directory you want to work with and that has licenses associated with it.</span></span>
4. <span data-ttu-id="364bb-148">**라이선스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-148">Select **Licenses**.</span></span> <span data-ttu-id="364bb-149">사용 가능한 라이선스 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-149">The list of available licenses will appear.</span></span>
5. <span data-ttu-id="364bb-150">배포하려는 라이선스가 포함된 라이선스 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-150">Select the license plan which contains the licenses that you want to distribute.</span></span>
6. <span data-ttu-id="364bb-151">**사용자 할당**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-151">Select **Assign Users**.</span></span>
7. <span data-ttu-id="364bb-152">라이선스를 할당하려는 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-152">Select the user that you want to assign a license to.</span></span>
8. <span data-ttu-id="364bb-153">**할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-153">Click the **Assign** button.</span></span>  <span data-ttu-id="364bb-154">이제 사용자가 Azure에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364bb-154">The user can now sign in to Azure.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="364bb-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="364bb-155">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

