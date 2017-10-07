---
title: "사용자 지정 역할 기반 액세스 제어 역할 aaaCreate toointernal 및 외부 사용자가 Azure에서 할당 | Microsoft Docs"
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
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="f5761-103">역할 기반 액세스 제어 소개</span><span class="sxs-lookup"><span data-stu-id="f5761-103">Intro on role-based access control</span></span>

<span data-ttu-id="f5761-104">역할 기반 액세스 제어 기능은 Azure 포털만 허용 구독 hello 소유자 tooassign 자신의 환경에서 특정 리소스 범위를 관리할 수 있는 상세 역할로 tooother 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="f5761-105">외부 공동 작업자, 공급 업체 또는 freelancers toospecific 환경 하지만 반드시 toohello 전체 인프라 또는 리소스 하나에 액세스 해야 하는 작업 RBAC가 Smb를 위한 대규모 조직에 대 한 보안 관리를 향상 수 있습니다. 대금 청구 관련 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="f5761-106">RBAC hello 관리자 계정 (구독 수준에서 서비스 관리자 역할)에 의해 관리 되는 단일 Azure 구독을 소유 hello 유연성을 허용 하 고 아래에서 여러 사용자가 초대 toowork가 동일한 구독 없이 hello 관리 에 대 한 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="f5761-107">관리 및 결제 관점에서 hello RBAC 기능은 다양 한 시나리오에서 Azure를 사용 하 여에 대 한 시간 및 관리 효율성 옵션 toobe을 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5761-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f5761-108">Prerequisites</span></span>
<span data-ttu-id="f5761-109">RBAC를 사용 하 여 hello Azure 환경에에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="f5761-110">독립 실행형 있는 Azure 구독 toohello 사용자로 할당 소유자 (구독 역할)</span><span class="sxs-lookup"><span data-stu-id="f5761-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="f5761-111">Hello 소유자 역할의 hello Azure 구독</span><span class="sxs-lookup"><span data-stu-id="f5761-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="f5761-112">액세스 toohello가 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f5761-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="f5761-113">리소스 공급자에 따라 toohave hello hello 사용자 구독에 등록 되어 있는지 확인: **Microsoft.Authorization**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="f5761-114">어떻게 tooregister hello 리소스 공급자에 대 한 자세한 내용은 참조 하십시오. [공급자 리소스 관리자, 지역, API 버전 및 스키마](/azure-resource-manager/resource-manager-supported-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f5761-115">Office 365 구독 또는 Azure Active Directory 라이선스 (예: tooAzure Active Directory에 액세스)에서 hello O365 포털 하지 품질에 대 한 RBAC를 사용 하 여 사용자를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="f5761-116">RBAC를 사용할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="f5761-116">How can RBAC be used</span></span>
<span data-ttu-id="f5761-117">RBAC는 Azure에서 세 가지 각기 다른 범위에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="f5761-118">Hello 가장 높은 범위 toohello 가장 낮은 하나에서에서 것은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="f5761-119">구독(높음)</span><span class="sxs-lookup"><span data-stu-id="f5761-119">Subscription (highest)</span></span>
* <span data-ttu-id="f5761-120">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f5761-120">Resource group</span></span>
* <span data-ttu-id="f5761-121">리소스 범위 (hello 최저 액세스 수준 tooan 개별 Azure 리소스 범위 대상으로 지정 된 사용 권한을 제공)</span><span class="sxs-lookup"><span data-stu-id="f5761-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="f5761-122">Hello 구독 범위에서 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="f5761-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="f5761-123">RBAC가 사용되는 일반적인 두 가지 예는 다음과 같습니다(제한되지는 않음).</span><span class="sxs-lookup"><span data-stu-id="f5761-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="f5761-124">특정 리소스 또는 전체 구독 hello toomanage 초대 hello 조직 (hello 관리 사용자의 Azure Active Directory 테 넌 트의 일부가 아님)에서 외부 사용자가</span><span class="sxs-lookup"><span data-stu-id="f5761-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="f5761-125">어느 toohello 내 (의 일부인 hello 사용자의 Azure Active Directory 테 넌 트) hello 조직이 하지만 다른 팀 또는 세분화 된 액세스 해야 하는 그룹의 일부는 사용자와 작업 전체 구독 또는 toocertain 리소스 그룹 또는 리소스의 범위가 hello에 환경</span><span class="sxs-lookup"><span data-stu-id="f5761-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="f5761-126">구독 수준에서 Azure Active Directory 외부 사용자에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f5761-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="f5761-127">RBAC 역할에만 부여할 수 **소유자** hello 구독의 따라서 hello admin 사용자도 로그온 해야이 역할이 미리 할당 되지 않았거나가 hello Azure 구독을 만든 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="f5761-128">Hello Azure 포털에서에서 한 후 로그인 관리자의 경우 선택 "구독" 및 선택한 hello 원하는 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="f5761-129">![Azure 포털에서 구독 블레이드](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) 기본적으로 hello admin 사용자 hello Azure 구독을 구매한 경우 hello 사용자로 표시 됩니다 **계정 관리자**,이 hello 구독 역할 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="f5761-130">Hello Azure 구독 역할에 대 한 자세한 내용은 참조 하십시오. [hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할을 추가 또는 변경](/billing/billing-add-change-azure-subscription-administrator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="f5761-131">이 예제에서는 사용자 hello "alflanigan@outlook.com"는 hello **소유자** "무료 평가판" hello의 구독 hello AAD에서에서 테 넌 트 "Azure 테 넌 트 Default"입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="f5761-132">이 사용자는 hello 작성자 hello로 hello Azure 구독에 있으므로 초기 "Outlook" Microsoft 계정 (Microsoft 계정 = Outlook, Live 등)이 테 넌이 트에 추가 된 다른 모든 사용자에 대 한 기본 도메인 이름은 hello **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="f5761-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="f5761-133">기본적으로 hello 새 도메인의 hello 구문을 함께 hello 테 넌 트 및 추가 hello 확장 만든 hello 사용자의 hello 사용자 이름 및 도메인 이름을 입력 하 여 형식이 **". onmicrosoft.com"**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="f5761-134">또한 사용자가에 로그인 hello 테 넌 트의 사용자 지정 도메인 이름을 추가 하 고 hello 새 테 넌 트에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="f5761-135">에 대 한 자세한 내용은 tooverify Azure Active Directory 테 넌 트에 사용자 지정 도메인 이름을 확인 하려면 어떻게 해야 [추가 사용자 지정 도메인 이름 tooyour 디렉터리](/active-directory/active-directory-add-domain)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="f5761-136">이 예에서 hello "기본 테 넌 트 Azure" 디렉터리는 hello 도메인 이름 가진 사용자만 포함 "@alflanigan.onmicrosoft.com"입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="f5761-137">Hello 구독을 선택한 후 hello admin 사용자가 클릭 해야 **액세스 제어 (IAM)** 차례로 **새 역할을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Azure Portal의 액세스 제어 IAM 기능](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Azure Portal의 액세스 제어 IAM 기능에서 새 사용자 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="f5761-140">hello 다음 단계에 할당 된 tooselect hello 역할 toobe 및 hello RBAC 역할에 할당 될 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="f5761-141">Hello에 **역할** hello 기본 제공 RBAC 역할에 대해서만 Azure에서 사용할 수 있는 드롭다운 메뉴 hello 관리: 사용자에 게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="f5761-142">각 역할 및 해당 할당 가능한 범위에 대한 자세한 설명은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](/active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5761-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="f5761-143">hello 관리: 사용자에는 다음 hello 외부 사용자의 tooadd hello 전자 메일 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="f5761-144">hello 동작은 hello 외부 사용자 toonot에에서 표시 hello 기존 테 넌 트에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="f5761-145">아래에 표시 것 hello 외부 사용자를 초대 후 **구독 > 액세스 제어 (IAM)** 프로그램 RBAC 역할 hello 구독 범위에 현재 할당 되어 있는 모든 hello 현재 사용자와 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![사용 권한을 toonew RBAC 역할 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![구독 수준에서 RBAC 역할 목록](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="f5761-148">hello 사용자 "chessercarlton@gmail.com" 초대 된 toobe 되었습니다는 **소유자** hello "무료 평가판" 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="f5761-149">Hello 외부 사용자는 hello 초대를 보낸 후 활성화 링크를 전자 메일 확인을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="f5761-150">![RBAC 역할에 대한 이메일 초대](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="f5761-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="f5761-151">조직 외부 toohello 되 고, hello 새 사용자가 없습니다 모든 기존 특성 hello "기본 Azure 테 넌 트" 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="f5761-152">Hello 외부 사용자가 부여한 동의 toobe 역할을 지정한 그 hello 구독과 연결 된 hello 디렉토리에 기록 된 후 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![RBAC 역할에 대한 이메일 초대 메시지](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="f5761-154">hello 외부 사용자의 외부 사용자로 Azure Active Directory 테 넌 트 hello에 표시 되 고 Azure 포털 hello와 hello 클래식 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![사용자 블레이드 Azure Active Directory Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![사용자 블레이드 Azure Active Directory Azure 클래식 포털](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="f5761-157">Hello에 **사용자** 보기 두 포털 hello 외부 사용자에 의해 인식 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="f5761-158">hello Azure 포털에서에서 다른 아이콘 유형을 hello</span><span class="sxs-lookup"><span data-stu-id="f5761-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="f5761-159">hello 클래식 포털에서 지점 소싱 다른 hello</span><span class="sxs-lookup"><span data-stu-id="f5761-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="f5761-160">그러나 부여 **소유자** 또는 **참가자** hello에 대 한 액세스 tooan 외부 사용자 **구독** 범위, hello 액세스 toohello admin 사용자 디렉터리를 허용 하지 않습니다 하지 않는 한 hello **전역 관리자** 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="f5761-161">Hello 사용자 속성에서 hello **사용자 유형** 두 개의 공통 매개 변수 있는 **멤버** 및 **게스트** 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="f5761-162">멤버는 게스트는 외부 원본에서 사용자를 초대 toohello 디렉터리 동안 hello 디렉터리에 등록 되어 있는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="f5761-163">자세한 내용은 [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](/active-directory/active-directory-b2b-admin-add-users)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5761-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="f5761-164">Hello 포털에서 hello 자격 증명을 입력 한 후 hello 외부 사용자 선택 hello 올바른 디렉터리 toosign에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="f5761-165">hello 동일한 사용자 수 액세스 toomultiple 디렉터리가 있을 수 둘 중 하나 hello 표시줄 오른쪽에 hello Azure 포털에서 hello 사용자 이름을 클릭 하 여 선택한 hello 드롭다운 목록에서 hello 적절 한 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="f5761-166">Hello 디렉터리에 게스트 하면서 hello 외부 사용자 hello Azure 구독에 대 한 모든 리소스를 관리할 수는 있지만 hello 디렉터리에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![제한 된 tooazure active directory Azure 포털에 액세스](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="f5761-168">Azure Active Directory와 Azure 구독에는 다른 Azure 리소스와 Azure 구독이 가진 것과 같은 자식-부모 관계가 없습니다(예: 가상 컴퓨터, 가상 네트워크, 웹앱, 저장소 등).</span><span class="sxs-lookup"><span data-stu-id="f5761-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="f5761-169">후자의 모든 hello 생성, 관리 되 고 Azure 구독에 사용 되는 toomanage hello 액세스 tooan Azure 디렉터리는 Azure 구독에 따라 요금이 청구 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="f5761-170">자세한 내용은 참조 하십시오. [어떻게 Azure 구독을 관련된 tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="f5761-171">모든 hello 기본 제공 RBAC 역할에서 **소유자** 및 **참가자** hello 환경, 참가자를 만들 수 없는 hello 차이 되 고 새 delete tooall 리소스 완전 한 관리 액세스를 제공 합니다. RBAC 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="f5761-172">hello 다른 기본 제공 역할 같은 **가상 컴퓨터 참가자** hello와 상관 없이 hello 이름을 가리키는 toohello 리소스만 완전 한 관리 액세스를 제공 합니다. **리소스 그룹** 생성 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="f5761-173">할당 hello 기본 제공 RBAC 역할의 **가상 컴퓨터 참가자** 구독 수준에 해당 hello 사용자만 할당 hello 역할을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="f5761-174">그룹을 볼 수 있는 모든 가상 컴퓨터에 관계 없이 해당 배포 날짜 및 hello 리소스의 일부</span><span class="sxs-lookup"><span data-stu-id="f5761-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="f5761-175">Hello 구독에는 완전 한 관리 액세스 toohello 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="f5761-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="f5761-176">Hello 구독에서 다른 리소스 종류를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="f5761-177">요금 청구 관점에서 변경 사항을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="f5761-178">RBAC는 Azure 포털만 기능 되 고, 액세스 toohello 클래식 포털 권한을 부여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="f5761-179">기본 제공 RBAC 역할 tooan 외부 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="f5761-180">이 테스트의 서로 다른 시나리오에 대 한 외부 사용자 hello "alflanigan@gmail.com"으로 추가 됩니다 한 **가상 컴퓨터 참가자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![가상 컴퓨터 참여자 기본 제공 역할](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="f5761-182">이 외부 사용자에 게이 기본 제공 역할에 대 한 일반적인 동작 hello toosee 이며만 가상 컴퓨터와 인접 한 리소스 관리자만 리소스를 배포 하는 동안 필요한 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="f5761-183">기본적으로 이러한 제한 된 역할 액세스를 제공 hello Azure 포털에서에서 만든만 tootheir 연락처 리소스에 관계 없이 일부를 구축할 수 있습니다 hello 클래식 포털도에서 (예: 가상 컴퓨터).</span><span class="sxs-lookup"><span data-stu-id="f5761-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![Azure Portal에서 가상 컴퓨터 참가자 역할 개요](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="f5761-185">동일한 사용자 hello에 대 한 구독 수준에서 부여 액세스할 디렉터리</span><span class="sxs-lookup"><span data-stu-id="f5761-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="f5761-186">hello 프로세스 흐름은 동일한 tooadding 외부 사용자의 경우 모두 액세스 toohello 역할에 부여할 hello 사용자 뿐 아니라 hello 관리자 관점 hello RBAC 역할이 부여 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="f5761-187">hello 차이점은 로그인 한 후 hello 구독 내에서 모든 hello 리소스 범위 hello 대시보드에서 사용할 수 있을 hello 초대 된 사용자는 전자 메일 초대 받지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="f5761-188">Hello 리소스 그룹 범위에서 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="f5761-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="f5761-189">RBAC 역할을 할당 한 **리소스 그룹** 범위는 두 가지 유형의 사용자-외부 또는 내부 hello 구독 수준에서 hello 역할을 할당 하는 데는 동일한 프로세스에 (hello의 일부가 동일한 디렉터리).</span><span class="sxs-lookup"><span data-stu-id="f5761-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="f5761-190">hello 사용자 hello RBAC 역할 할당은 toosee 자신의 환경에서 사용할 수 있는 hello 리소스 그룹 할당 된 액세스 hello에서 **리소스 그룹** hello Azure 포털에서에서 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="f5761-191">Hello 리소스 범위에서 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="f5761-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="f5761-192">Hello 역할 hello 구독 수준에서 또는 hello 리소스 그룹 수준에서 할당 하는 데는 동일한 프로세스에 Azure에서 리소스 범위에는 RBAC 역할을 할당, 다음 hello 동일한 두 시나리오 모두에 대 한 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="f5761-193">Hello RBAC 역할에 할당 되어 있는 hello 사용자가 할당 된 액세스 중 하나에 hello에 hello 항목만 볼 수는 다시 **모든 리소스** 탭에서 대시보드를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="f5761-194">RBAC 모두에서 리소스 그룹 범위 또는 리소스에 대 한 중요 한 측면은 hello 사용자 toomake 있는지 toosign 인 toohello 올바른 디렉터리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![Azure Portal에서 디렉터리 로그인](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="f5761-196">Azure Active Directory 그룹에 대한 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="f5761-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="f5761-197">Hello in Azure 제품 hello 권한 관리, 배포 및 hello 없이 할당된 된 사용자로 다양 한 리소스를 관리의 세 가지 서로 다른 범위에서 RBAC를 사용 하 여 모든 hello 시나리오 개인 구독 관리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="f5761-198">구독, 리소스 그룹 또는 리소스 범위에 대 한 관계 없이 hello RBAC 역할 할당, 뒤에 할당 된 hello 사용자가 만든 모든 hello 리소스 hello 사용자가 액세스할 수 hello 하나의 Azure 구독으로 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="f5761-199">이러한 방식으로 hello 청구 전체 해당 Azure 구독에 대 한 관리자 권한이 있는 사용자가 hello 리소스를 관리 하 고 있는 관계 없이 hello 사용에 대 한 전체 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="f5761-200">대규모 조직의 RBAC 역할을 적용할 수 있습니다 hello에 해당 hello admin 사용자 hello 관점을 고려 하는 Azure Active Directory 그룹에 대 한 동일한 방식으로 toogrant hello 세분화 된 액세스 하려는 각 사용자에 대해 개별적으로 쓰지 전체 부서 또는 팀에 대 한 따라서 매우 시간 및 관리 효율성 옵션으로 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="f5761-201">tooillustrate이 예에서는, hello **참가자** 역할에에서 추가 되었습니다 hello 그룹 tooone hello 구독 수준에서 hello 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![AAD 그룹에 대한 RBAC 역할 추가](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="f5761-203">이러한 그룹은 Azure Active Directory 내에서만 프로비전되고 관리되는 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="f5761-204">사용자 지정 RBAC 역할 tooopen 지원 PowerShell을 사용 하 여 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="f5761-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="f5761-205">Azure에서 사용할 수 있는 hello 기본 제공 RBAC 역할 hello hello 환경에서 사용할 수 있는 리소스에 따라 특정 사용 권한 수준을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="f5761-206">그러나 hello 관리 사용자의 요구 사항에 맞게 이러한 역할이 있으면 hello 옵션 toolimit 액세스가 더 많은 사용자 지정 RBAC 역할을 만들어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="f5761-207">기본 제공 역할 하나 tootake 필요 RBAC 역할 사용자 지정 만들기, 편집 하 고 hello 환경에서 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="f5761-208">hello 다운로드 및 업로드 hello 역할의 PowerShell 또는 CLI를 사용 하 여 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="f5761-209">중요 한 toounderstand hello 필수 구성 요소는 사용자 지정 역할 만들기의 hello 구독 수준에서 세분화 된 액세스 권한을 부여 하 고 지원 요청을 열고의 초대 hello 사용자 hello 유연성 허용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="f5761-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="f5761-210">이 예제에서는 hello 기본 제공 역할에 대 한 **판독기** 범위로 지정 되지 tooedit 있지만 허용 하는 사용자가 액세스 tooview 모든 hello 리소스 하거나 새로 만들 되었습니다 tooallow hello 사용자 hello 옵션 열기 지원 요청을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="f5761-211">hello 내보내기의 첫 번째 작업 hello **판독기** 역할 요구 toobe 완료 PowerShell에서 관리자 권한으로 승격 된 권한으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![판독기 RBAC 역할의 PowerShell 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="f5761-213">Hello 역할의 tooextract hello JSON 템플릿이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-213">Then you need tooextract hello JSON template of hello role.</span></span>





![사용자 지정 판독기 RBAC 역할의 JSON 템플릿](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="f5761-215">일반적인 RBAC 역할은 **작업**, **NotActions** 및 **AssignableScopes**라는 세 가지 주요 섹션으로 구성됩니다,</span><span class="sxs-lookup"><span data-stu-id="f5761-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="f5761-216">Hello에 **동작** 섹션에 나열 된 모든 hello이 역할에 대해 허용 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="f5761-217">각 작업은 리소스 공급자에서 할당 된 중요 한 toounderstand 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="f5761-218">이 경우 지원 티켓 hello 작성용 **Microsoft.Support** 리소스 공급자를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="f5761-219">toobe 수 toosee 리소스 공급자 사용 가능 하 고 구독에 등록 된 모든 hello, PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="f5761-220">또한 hello 사용 가능한 모든 PowerShell cmdlet toomanage hello 리소스 공급자 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="f5761-221">![리소스 공급자 관리의 PowerShell 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="f5761-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="f5761-222">모든 리소스 공급자 hello 섹션 아래에 표시 되는 특정 RBAC 역할에 대 한 작업을 hello toorestrict **NotActions**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="f5761-223">마지막으로, 해당 hello RBAC 역할 안녕하세요 명시적 구독 Id 사용 되는 위치에 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="f5761-224">hello 구독 Id가 나열 됩니다 hello **AssignableScopes**, 그렇지 않으면 있습니다 수 없으며 tooimport hello 역할 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="f5761-225">만들고 hello RBAC 역할 사용자 지정 후 toobe 가져온된 백 hello 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="f5761-226">이 예제에서는이 RBAC 역할에 대 한 사용자 지정 이름을 hello 수준이 "판독기 지원 티켓 액세스" hello 구독 및 tooopen 지원 요청에서 모든 항목 hello 사용자 tooview를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="f5761-227">hello hello 동작 여 지원 요청을 허용 하는 두 개의 기본 제공 RBAC 역할은 **소유자** 및 **참가자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="f5761-228">사용자 toobe 수 tooopen 지원 요청에 대 한 그는 RBAC 역할을 할당 해야 hello 구독 범위 에서만 지원에 대 한 모든 요청은 Azure 구독에 따라 만들어지므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="f5761-229">이 새로운 사용자 지정 역할 hello에서 tooan 사용자 지정 된 같은 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![hello Azure 포털에서에서 가져온 사용자 지정 RBAC 역할의 스크린 샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![hello에 사용자 지정 가져온된 RBAC 역할 toouser 할당의 스크린샷 같은 디렉터리](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![가져온 사용자 지정 RBAC 역할에 대한 사용 권한 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="f5761-233">hello 예제가 되었습니다 추가 사용자 지정이 RBAC 역할의 자세한 tooemphasize hello 제한 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="f5761-234">새 지원 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-234">Can create new support requests</span></span>
* <span data-ttu-id="f5761-235">새 리소스 범위를 만들 수 없습니다(예: 가상 컴퓨터).</span><span class="sxs-lookup"><span data-stu-id="f5761-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="f5761-236">새 리소스 그룹을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-236">Can't create new resource groups</span></span>





![지원 요청을 만드는 사용자 지정 RBAC 역할의 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![사용자 지정 RBAC 역할의 스크린샷 수 없습니다. toocreate Vm](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![사용자 지정 RBAC 역할의 스크린샷 수 없습니다. toocreate 새 RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="f5761-240">사용자 지정 RBAC 역할 tooopen 지원 Azure CLI를 사용 하 여 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="f5761-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="f5761-241">Azure CLI에 hello 방식으로 toogo는 Mac에서 및 액세스 tooPowerShell 필요 없이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="f5761-242">hello 단계 toocreate 사용자 지정 역할 동일 hello 유일한 예외는 CLI를 사용 하 여 hello 역할 다운로드할 수 없습니다는 JSON 템플릿을에에서 볼 수 있는 hello CLI hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="f5761-243">이 예의 기본 제공 역할 hello 선택 **백업 판독기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![백업 읽기 역할의 CLI 스크린샷 표시](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="f5761-245">Hello hello 속성에는 JSON 템플릿을 복사한 후 Visual Studio에서 hello 역할을 편집 **Microsoft.Support** hello에 리소스 공급자를 추가한 **동작** 이 사용자를 열 수 있도록 섹션 toobe hello 백업 자격 증명 모음에 대 한 판독기를 계속 하면서 지원 요청.</span><span class="sxs-lookup"><span data-stu-id="f5761-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="f5761-246">다시이 필요한 tooadd hello 구독 ID가이 역할 hello에 사용 되는 위치 **AssignableScopes** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f5761-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![사용자 지정 RBAC 역할 가져오기의 CLI 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="f5761-248">이제 hello 새 역할을 hello Azure 포털에서에서 사용할 수 있으며 hello 할당 프로세스는 동일 hello 이전 예제와 같이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![CLI 1.0을 사용하여 만든 사용자 지정 RBAC 역할의 Azure Portal 스크린샷](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="f5761-250">Hello 현재 최신 빌드 2017 년 1 hello Azure 클라우드 셸은 일반적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="f5761-251">Azure 클라우드 셸은 보수 tooIDE 및 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="f5761-252">이 서비스에서 Azure 내에서 인증되고 호스트되는 브라우저 기반 셸을 가져오고 컴퓨터에 설치된 CLI 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5761-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
