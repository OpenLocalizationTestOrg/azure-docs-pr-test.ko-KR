---
title: "사용자 지정 역할 기반 액세스 제어 역할 만들기 및 Azure에서 내부 및 외부 사용자에게 할당 | Microsoft Docs"
description: "내부 및 외부 사용자에게 PowerShell 및 CLI를 사용하여 만든 사용자 지정 RBAC 역할 할당"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="cf4b3-103">역할 기반 액세스 제어 소개</span><span class="sxs-lookup"><span data-stu-id="cf4b3-103">Intro on role-based access control</span></span>

<span data-ttu-id="cf4b3-104">역할 기반 액세스 제어는 구독의 소유자가 해당 환경에서 특정 리소스 범위를 관리할 수 있는 다른 사용자에게 세분화된 역할을 할당하는 Azure Portal에만 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="cf4b3-105">RBAC를 통해 환경에서 특정 리소스에 액세스해야 하지만 전체 인프라 또는 청구 관련 범위에 액세스하지 않아도 되는 외부 공동 작업자, 공급 업체 또는 프리랜서와 함께 작업하는 대규모 조직 및 SMB의 경우 더 나은 보안 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="cf4b3-106">RBAC를 통해 관리자 계정에서 관리하는 Azure 구독을 소유하는 유연성(구독 수준에서 서비스 관리자 역할)을 제공하고 동일한 구독이지만 관리 권한 없이 작업하도록 여러 사용자를 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="cf4b3-107">관리 및 청구 관점에서 RBAC 기능은 다양한 시나리오에서 Azure를 사용하는 시간 및 관리 효율성 옵션으로 증명됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf4b3-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cf4b3-108">Prerequisites</span></span>
<span data-ttu-id="cf4b3-109">Azure 환경에서 RBAC를 사용하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="cf4b3-110">소유자인 사용자에게 할당된 독립 실행형 Azure 구독(구독 역할)</span><span class="sxs-lookup"><span data-stu-id="cf4b3-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="cf4b3-111">Azure 구독의 소유자 역할</span><span class="sxs-lookup"><span data-stu-id="cf4b3-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="cf4b3-112">[Azure Portal](https://portal.azure.com)에 대한 액세스 권한</span><span class="sxs-lookup"><span data-stu-id="cf4b3-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="cf4b3-113">사용자 구독에 등록된 다음과 같은 리소스 공급자: **Microsoft.Authorization**</span><span class="sxs-lookup"><span data-stu-id="cf4b3-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="cf4b3-114">리소스 공급자를 등록하는 방법에 대해 자세히 알아보려면 [Resource Manager 공급자, 지역, API 버전 및 스키마](/azure-resource-manager/resource-manager-supported-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cf4b3-115">O365 포털에서 프로비전된 Office 365 구독 또는 Azure Active Directory 라이선스(예: Azure Active Directory에 액세스)는 RBAC를 사용할 자격이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="cf4b3-116">RBAC를 사용할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="cf4b3-116">How can RBAC be used</span></span>
<span data-ttu-id="cf4b3-117">RBAC는 Azure에서 세 가지 각기 다른 범위에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="cf4b3-118">높은 범위에서 낮은 범위 순으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="cf4b3-119">구독(높음)</span><span class="sxs-lookup"><span data-stu-id="cf4b3-119">Subscription (highest)</span></span>
* <span data-ttu-id="cf4b3-120">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="cf4b3-120">Resource group</span></span>
* <span data-ttu-id="cf4b3-121">리소스 범위(개별 Azure 리소스에 대상으로 지정된 사용 권한을 제공하는 최저 액세스 수준)</span><span class="sxs-lookup"><span data-stu-id="cf4b3-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="cf4b3-122">구독 범위에서 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="cf4b3-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="cf4b3-123">RBAC가 사용되는 일반적인 두 가지 예는 다음과 같습니다(제한되지는 않음).</span><span class="sxs-lookup"><span data-stu-id="cf4b3-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="cf4b3-124">조직의 외부 사용자를 특정 리소스 또는 전체 구독을 관리하도록 초대한 경우(관리 사용자의 Azure Active Directory 테넌트 중 일부가 아님)</span><span class="sxs-lookup"><span data-stu-id="cf4b3-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="cf4b3-125">조직 내에서 사용자와 작업(사용자의 Azure Active Directory 테넌트 중 일부)하지만 환경에서 전체 구독 또는 특정 리소스 그룹이나 리소스 범위에 대한 세분화된 액세스 권한이 필요한 다른 팀 또는 그룹의 일부인 경우</span><span class="sxs-lookup"><span data-stu-id="cf4b3-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="cf4b3-126">구독 수준에서 Azure Active Directory 외부 사용자에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="cf4b3-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="cf4b3-127">RBAC 역할은 구독의 **소유자**만이 부여할 수 있으므로 관리 사용자는 이 역할을 미리 할당받거나 Azure 구독을 만든 사용자 이름으로 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="cf4b3-128">Azure Portal에서 관리자로 로그인한 후에 "구독"을 선택하고 원하는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="cf4b3-129">![Azure Portal의 구독 블레이드](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) 기본적으로 관리 사용자가 Azure 구독을 구매한 경우 사용자는 **계정 관리자**로 표시되고 이는 구독 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="cf4b3-130">Azure 구독 역할에 대한 자세한 내용은 [구독 또는 서비스를 관리하는 Azure 관리자 역할 추가 또는 변경](/billing/billing-add-change-azure-subscription-administrator.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="cf4b3-131">이 예제에서 사용자 "alflanigan@outlook.com"은 AAD 테넌트 "기본 테넌트 Azure"에서 "체험 평가판" 구독의 **소유자**입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="cf4b3-132">이 사용자가 초기 Microsoft 계정 "Outlook"을 사용하여 Azure 구독을 만들었으므로(Microsoft 계정 = Outlook, Live 등) 이 테넌트에 추가된 다른 모든 사용자의 기본 도메인 이름은 **"@alflaniganuoutlook.onmicrosoft.com"**입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="cf4b3-133">기본적으로 테넌트를 만든 사용자의 사용자 이름 및 도메인 이름을 결합하고 **".onmicrosoft.com"** 확장을 추가하여 새 도메인의 구문 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="cf4b3-134">또한 사용자는 새 테넌트에 추가하고 확인한 후에 테넌트에 있는 사용자 지정 도메인 이름을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="cf4b3-135">Azure Active Directory 테넌트에서 사용자 지정 도메인 이름을 확인하는 방법에 대한 자세한 내용은 [디렉터리에 사용자 지정 도메인 이름 추가](/active-directory/active-directory-add-domain)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="cf4b3-136">이 예제에서 "기본 테넌트 Azure" 디렉터리에는 도메인 이름 "@alflanigan.onmicrosoft.com"을 가진 사용자만이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="cf4b3-137">관리 사용자는 구독을 선택한 후에 **액세스 제어(IAM)** 및 **새 역할 추가**를 차례로 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Azure Portal의 액세스 제어 IAM 기능](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Azure Portal의 액세스 제어 IAM 기능에서 새 사용자 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="cf4b3-140">다음 단계에서는 할당하고 역할 및 RBAC 역할에 할당할 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="cf4b3-141">**역할** 드롭다운 메뉴에서는 Azure에서 사용할 수 있는 기본 제공 RBAC 역할만을 관리 사용자에게 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="cf4b3-142">각 역할 및 해당 할당 가능한 범위에 대한 자세한 설명은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](/active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="cf4b3-143">관리 사용자는 외부 사용자의 이메일 주소를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="cf4b3-144">예상된 동작을 기존 테넌트에서 외부 사용자에세 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="cf4b3-145">외부 사용자를 초대한 후에 현재 구독 범위에서 RBAC 역할에 할당한 모든 사용자와 함께 **구독 > 액세스 제어(IAM)**를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![새 RBAC 역할에 사용 권한 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![구독 수준에서 RBAC 역할 목록](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="cf4b3-148">사용자 "chessercarlton@gmail.com"은 "체험 평가판" 구독에 대한 **소유자**로 초대되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="cf4b3-149">외부 사용자는 초대를 보낸 후에 활성화 링크를 포함한 이메일 확인을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="cf4b3-150">![RBAC 역할에 대한 이메일 초대](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="cf4b3-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="cf4b3-151">조직의 외부에 있는 새 사용자는 "기본 테넌트 Azure" 디렉터리에서 기존 특성을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="cf4b3-152">해당 특성은 외부 사용자가 역할을 할당한 구독과 연결되어 있는 디렉터리에 기록하는 데 동의한 후에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![RBAC 역할에 대한 이메일 초대 메시지](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="cf4b3-154">외부 사용자는 지금부터 Azure Active Directory 테넌트에서 외부 사용자로 표시되고 Azure Portal 및 클래식 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![사용자 블레이드 Azure Active Directory Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![사용자 블레이드 Azure Active Directory Azure 클래식 포털](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="cf4b3-157">두 포털의 **사용자** 보기에서 외부 사용자는 다음으로 인식될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="cf4b3-158">Azure Portal에서 다른 아이콘 형식</span><span class="sxs-lookup"><span data-stu-id="cf4b3-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="cf4b3-159">클래식 포털에서 다른 소싱 지점</span><span class="sxs-lookup"><span data-stu-id="cf4b3-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="cf4b3-160">그러나 **구독** 범위에서 외부 사용자에 대한 **소유자** 또는 **참가자** 액세스 권한을 부여하면 **전역 관리자**가 허용하지 않는 한 관리 사용자의 디렉터리에 대한 액세스를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="cf4b3-161">사용자 속성에서 두 공통 매개 변수가 있는 **사용자 형식**, **멤버** 및 **게스트**를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="cf4b3-162">구성원은 디렉터리에 등록되어 있는 사용자인 반면 게스트는 외부 소스의 디렉터리로 초대된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="cf4b3-163">자세한 내용은 [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](/active-directory/active-directory-b2b-admin-add-users)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="cf4b3-164">포털에서 자격 증명을 입력한 후에 외부 사용자가 올바른 디렉터리에 로그인하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="cf4b3-165">동일한 사용자는 여러 디렉터리에 대한 액세스 권한이 있을 수 있고 Azure Portal의 오른쪽 위에 있는 사용자 이름을 클릭 그 중 하나를 선택한 다음 드롭다운 목록에서 적절한 디렉터리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="cf4b3-166">디렉터리에 있는 게스트인 경우 외부 사용자는 Azure 구독에 대한 모든 리소스를 관리할 수 있지만 디렉터리에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![Azure Active Directory Azure Portal에 제한된 액세스](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="cf4b3-168">Azure Active Directory와 Azure 구독에는 다른 Azure 리소스와 Azure 구독이 가진 것과 같은 자식-부모 관계가 없습니다(예: 가상 컴퓨터, 가상 네트워크, 웹앱, 저장소 등).</span><span class="sxs-lookup"><span data-stu-id="cf4b3-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="cf4b3-169">후자가 모두 Azure 구독에서 생성되고 관리되며 요금이 청구되는 반면 Azure 구독은 Azure 디렉터리에 대한 액세스를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="cf4b3-170">자세한 내용은 [Azure 구독과 Azure AD의 연관 관계](/active-directory/active-directory-how-subscriptions-associated-directory)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="cf4b3-171">모든 기본 제공 RBAC 역할에서 **소유자** 및 **참가자**는 환경에서 모든 리소스에 대한 완전한 관리 액세스를 제공합니다. 두 역할의 차이는 새 RBAC 역할을 만들고 삭제할 수 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="cf4b3-172">**가상 컴퓨터 참여자**와 같은 다른 기본 제공 역할은 생성되는 **리소스 그룹**에 관계없이 이름으로 표시된 리소스에만 완전한 관리 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="cf4b3-173">**가상 컴퓨터 참여자**의 기본 제공 RBAC 역할을 구독 수준에서 할당한다는 것은 사용자에게 역할을 할당했다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="cf4b3-174">해당 배포 날짜 및 일부인 리소스 그룹에 관계 없이 모든 가상 컴퓨터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="cf4b3-175">구독에는 가상 컴퓨터에 대한 완전한 관리 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="cf4b3-176">구독에서 다른 리소스 형식을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="cf4b3-177">요금 청구 관점에서 변경 사항을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="cf4b3-178">Azure Portal 기능만 있는 RBAC는 클래식 포털에 대한 액세스 권한을 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="cf4b3-179">외부 사용자에게 기본 제공 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="cf4b3-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="cf4b3-180">이 테스트의 다른 시나리오에서 외부 사용자 "alflanigan@gmail.com"은 **가상 컴퓨터 참여자**로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![가상 컴퓨터 참여자 기본 제공 역할](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="cf4b3-182">이 기본 제공 역할을 가진 외부 사용자에 대한 정상 동작은 가상 컴퓨터와 배포 시 필요한 리소스에 인접한 Resource Manager만을 보고 관리하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="cf4b3-183">기본적으로 이러한 제한된 역할은 Azure Portal에서 만든 해당 리소스에 대해서만 액세스를 제공하지만 일부는 클래식 포털에서도 배포할 수 있습니다(예: 가상 컴퓨터).</span><span class="sxs-lookup"><span data-stu-id="cf4b3-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![Azure Portal에서 가상 컴퓨터 참가자 역할 개요](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="cf4b3-185">구독 수준에서 동일한 디렉터리의 사용자에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="cf4b3-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="cf4b3-186">RBAC 역할을 부여하는 관리자 관점뿐만 아니라 역할에 대한 액세스 권한이 부여된 사용자 관점에서도 프로세스 흐름은 외부 사용자를 추가하는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="cf4b3-187">여기서 차이점은 구독 내의 모든 리소스 범위를 로그인한 후에 대시보드에서 사용할 수 있는 경우 초대받은 사용자가 구독 내에서 어떤 이메일 초대도 수신하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="cf4b3-188">리소스 그룹 범위에서 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="cf4b3-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="cf4b3-189">**리소스 그룹** 범위에서 RBAC 역할을 할당하는 작업은 외부 또는 내부라는 두 종류의 사용자(동일한 디렉터리의 일부)에게 구독 수준에서 역할을 할당하는 동일한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="cf4b3-190">환경에서 리소스 그룹을 확인하는 RBAC 역할이 할당되어 있는 사용자는 Azure Portal의 **리소스 그룹** 아이콘에서 액세스 권한이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="cf4b3-191">리소스 범위에서 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="cf4b3-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="cf4b3-192">Azure의 리소스 범위에서 RBAC 역할을 할당하는 작업은 구독 수준 또는 리소스 그룹 수준에서 역할을 할당하는 동일한 프로세스이며 두 시나리오에 대해 동일한 워크플로를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="cf4b3-193">액세스가 할당된 항목만을 볼 수 있는 RBAC 역할이 할당되어 있는 사용자는 **모든 리소스** 탭 또는 대시보드에서 직접 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="cf4b3-194">RBAC에서 리소스 그룹 범위 또는 리소스 범위에 대한 중요한 측면은 사용자가 올바른 디렉터리에 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![Azure Portal에서 디렉터리 로그인](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="cf4b3-196">Azure Active Directory 그룹에 대한 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="cf4b3-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="cf4b3-197">Azure의 세 가지 다른 범위에서 RBAC를 사용하는 모든 시나리오는 개인 구독을 관리할 필요 없이 할당된 사용자로 다양한 리소스를 관리, 배포 및 관리하는 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="cf4b3-198">RBAC 역할이 구독, 리소스 그룹 또는 리소스 범위에 할당되었는지와 관계없이 뒤에 나오는 할당된 사용자가 만든 리소스는 모두 사용자가 액세스할 수 있는 하나의 Azure 구독에서 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="cf4b3-199">이러한 방식으로 전체 Azure 구독에 대해 청구 관리자 권한을 가진 사용자는 리소스를 관리하는 사용자가 누구인지와 관계없이 소비에 대한 전체 개요를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="cf4b3-200">대규모 조직의 경우 RBAC 역할은 Azure Active Directory 그룹에게 동일한 방식으로 적용되어 관리 사용자가 각 사용자에 각각이 아닌 팀 또는 전체 부서에 대한 세부적인 액세스 권한을 부여하는 관점을 고려할 수 있습니다. 따라서 시간 및 관리 효율성이 뛰어난 옵션으로 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="cf4b3-201">이 예제를 설명하기 위해 **참가자** 역할은 구독 수준에서 테넌트의 그룹 중 하나에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![AAD 그룹에 대한 RBAC 역할 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="cf4b3-203">이러한 그룹은 Azure Active Directory 내에서만 프로비전되고 관리되는 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="cf4b3-204">PowerShell을 사용하여 지원 요청을 여는 사용자 지정 RBAC 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="cf4b3-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="cf4b3-205">Azure에서 사용할 수 있는 기본 제공 RBAC 역할은 환경에서 사용할 수 있는 리소스에 따라 특정 사용 권한 수준을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="cf4b3-206">그러나 이러한 역할이 관리 사용자의 요구에 맞지 않으면 사용자 지정 RBAC 역할을 만들어 액세스를 제한하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="cf4b3-207">사용자 지정 RBAC 역할을 만들려면 기본 제공 역할을 사용하고 편집한 다음 환경에서 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="cf4b3-208">역할의 다운로드 및 업로드는 PowerShell 또는 CLI를 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="cf4b3-209">구독 수준에서 세분화된 액세스 권한을 부여하고 초대받은 사용자에게 지원 요청을 여는 유연성을 허용할 수 있는 사용자 지정 역할을 만드는 필수 구성 요소를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="cf4b3-210">이 예제에서 기본 제공 역할 **판독기**는 사용자에게 모든 리소스 범위를 볼 수 있는 액세스 권한을 허용하지만 편집하거나 새로 만들지 않도록 사용자가 지원 요청을 열 수 있는 옵션을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="cf4b3-211">**판독기** 역할을 내보내는 첫 번째 작업은 PowerShell에서 완료해야 하고 관리자로 승격된 권한으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![판독기 RBAC 역할의 PowerShell 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="cf4b3-213">그런 다음 역할의 JSON 템플릿을 추출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-213">Then you need to extract the JSON template of the role.</span></span>





![사용자 지정 판독기 RBAC 역할의 JSON 템플릿](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="cf4b3-215">일반적인 RBAC 역할은 **작업**, **NotActions** 및 **AssignableScopes**라는 세 가지 주요 섹션으로 구성됩니다,</span><span class="sxs-lookup"><span data-stu-id="cf4b3-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="cf4b3-216">**작업** 섹션에서는 이 역할에 대해 허용된 모든 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="cf4b3-217">리소스 공급자로부터 각 작업이 할당되었음을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="cf4b3-218">이 경우에 지원 티켓을 만들기 위해 **Microsoft.Support** 리소스 공급자를 나열해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="cf4b3-219">사용 가능하고 구독에 등록된 모든 리소스 공급자를 보기 위해 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="cf4b3-220">또한 모든 사용할 수 있는 PowerShell cmdlet을 확인하여 리소스 공급자를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="cf4b3-221">![리소스 공급자 관리의 PowerShell 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="cf4b3-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="cf4b3-222">특정 RBAC 역할에 대해 모든 작업을 제한하려면 리소스 공급자는 **NotActions** 섹션 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="cf4b3-223">마지막으로 RBAC 역할이 포함한 필수 권한은 사용된 명시적 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="cf4b3-224">구독 ID는 **AssignableScopes** 아래에 나열됩니다. 그렇지 않으면 구독에 역할을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="cf4b3-225">RBAC 역할을 만들고 사용자 지정한 후에 환경으로 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="cf4b3-226">이 예제에서 이 RBAC 역할에 대한 사용자 지정 이름은 "판독기 지원 티켓 액세스 수준"이며 사용자가 구독에서 모든 항목을 확인하고 지원 요청을 열 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="cf4b3-227">지원 요청을 여는 작업을 허용하는 두 개의 기본 제공 RBAC 역할은 **소유자** 및 **참가자**입니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="cf4b3-228">지원 요청을 열 수 있는 사용자의 경우 모든 지원 요청이 Azure 구독에 따라 만들어지기 때문에 구독 범위에서만 RBAC 역할을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="cf4b3-229">이 새 사용자 지정 역할이 디렉터리에서 사용자에게 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-229">This new custom role has been assigned to an user from the same directory.</span></span>





![Azure Portal에서 가져온 사용자 지정 RBAC 역할의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![동일한 디렉터리에서 사용자에게 가져온 사용자 지정 RBAC 역할 할당의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![가져온 사용자 지정 RBAC 역할에 대한 사용 권한 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="cf4b3-233">예제는 다음과 같이 이 사용자 지정 RBAC 역할의 한계를 강조하여 추가적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="cf4b3-234">새 지원 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-234">Can create new support requests</span></span>
* <span data-ttu-id="cf4b3-235">새 리소스 범위를 만들 수 없습니다(예: 가상 컴퓨터).</span><span class="sxs-lookup"><span data-stu-id="cf4b3-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="cf4b3-236">새 리소스 그룹을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-236">Can't create new resource groups</span></span>





![지원 요청을 만드는 사용자 지정 RBAC 역할의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![VM을 만들 수 없다는 사용자 지정 RBAC 역할의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![새 RG를 만들 수 없다는 사용자 지정 RBAC 역할의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="cf4b3-240">Azure CLI를 사용하여 지원 요청을 여는 사용자 지정 RBAC 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="cf4b3-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="cf4b3-241">Mac에서 및 PowerShell에 액세스하지 않고 실행하려면 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="cf4b3-242">CLI를 사용하여 JSON 템플릿에서 역할을 다운로드할 수 없지만 CLI에서 볼 수 있다는 예외를 제외하면 사용자 지정 역할을 만드는 단계는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="cf4b3-243">이 예제에서 **백업 판독기**의 기본 제공 역할을 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![백업 읽기 역할의 CLI 스크린샷 표시](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="cf4b3-245">JSON 템플릿의 속성을 복사한 후에 Visual Studio에서 역할을 편집하면 **Microsoft.Support** 리소스 공급자가 **작업** 섹션에 추가되므로 이 사용자는 백업 자격 증명 모음에 대한 판독기를 계속 진행하면서 지원 요청을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="cf4b3-246">다시 이 역할을 **AssignableScopes** 섹션에서 사용하는 구독 ID를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![사용자 지정 RBAC 역할 가져오기의 CLI 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="cf4b3-248">이제 새 역할을 Azure Portal에서 사용할 수 있으며 할당 프로세스는 이전의 예와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![CLI 1.0을 사용하여 만든 사용자 지정 RBAC 역할의 Azure Portal 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="cf4b3-250">최신 빌드 2017인 Azure Cloud Shell을 일반적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="cf4b3-251">Azure Cloud Shell은 IDE 및 Azure Portal을 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="cf4b3-252">이 서비스에서 Azure 내에서 인증되고 호스트되는 브라우저 기반 셸을 가져오고 컴퓨터에 설치된 CLI 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf4b3-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
