---
title: "Azure IoT Suite 및 Azure Active Directory | Microsoft Docs"
description: "Azure IoT Suite에서 Azure Active Directory를 사용하여 사용 권한을 관리하는 방법을 설명합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="60782-103">azureiotsuite.com 사이트에 대한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="60782-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="60782-104">로그인 후 진행되는 작업</span><span class="sxs-lookup"><span data-stu-id="60782-104">What happens when you sign in</span></span>

<span data-ttu-id="60782-105">[azureiotsuite.com][lnk-azureiotsuite]에 처음 로그인하면, 사이트에서는 현재 선택된 AAD(Azure Active Directory) 테넌트 및 Azure 구독을 기반으로 사용자가 가진 사용 권한 수준을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="60782-106">로그인 사용자 이름 옆에 표시되는 테넌트 목록을 채우려면 먼저 사이트가 Azure로부터 사용자가 속하는 AAD 테넌트를 알아내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="60782-107">현재 사이트는 테넌트에 대한 사용자 토큰을 한 번에 하나만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="60782-108">따라서 오른쪽 상단 모서리의 드롭다운을 사용하여 테넌트로 전환하면, 사이트는 이 테넌트에 대한 토큰을 가져오기 위해서 해당 테넌트로 사용자를 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="60782-109">다음으로, 사이트는 사용자가 선택한 테넌트와 연결된 구독을 Azure로부터 알아냅니다.</span><span class="sxs-lookup"><span data-stu-id="60782-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="60782-110">미리 구성된 솔루션을 새로 만들 때 사용할 수 있는 구독이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60782-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="60782-111">마지막으로 사이트는 미리 구성된 솔루션으로 태그가 지정된 구독 및 리소스 그룹에서 모든 리소스를 가져와서 홈 페이지에 타일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="60782-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="60782-112">다음 섹션은 미리 구성된 솔루션에 대한 액세스를 제어하는 역할을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="60782-113">AAD 역할</span><span class="sxs-lookup"><span data-stu-id="60782-113">AAD roles</span></span>

<span data-ttu-id="60782-114">AAD 역할은 권한 프로비전 미리 구성된 솔루션을 제어하고 미리 구성된 솔루션의 사용자를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="60782-115">AAD에서 사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당][lnk-aad-admin]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="60782-116">현재 문서에서는 미리 구성된 솔루션에서 사용된 대로 **전역 관리자** 및 **사용자** 디렉터리 역할에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="60782-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="60782-117">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="60782-117">Global administrator</span></span>

<span data-ttu-id="60782-118">AAD 테넌트에는 여러 명의 전역 관리자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="60782-119">AAD 테넌트를 만들 때, 만드는 사람은 기본적으로 해당 테넌트의 전역 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="60782-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="60782-120">전역 관리자는 미리 구성된 솔루션을 프로비전할 수 있으며 해당 AAD 테넌트 내부의 응용 프로그램에 대해 **관리자** 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="60782-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="60782-121">동일한 AAD 테넌트의 다른 사용자가 응용 프로그램을 만들 경우, 전역 사용자에게 부여되는 기본 역할은 **읽기 전용**입니다.</span><span class="sxs-lookup"><span data-stu-id="60782-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="60782-122">전역 관리자는 [Azure Portal][lnk-portal]을 사용하여 사용자를 응용 프로그램의 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="60782-123">도메인 사용자</span><span class="sxs-lookup"><span data-stu-id="60782-123">Domain user</span></span>

<span data-ttu-id="60782-124">AAD 테넌트에는 여러 명의 도메인 사용자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="60782-125">도메인 사용자는 [azureiotsuite.com][lnk-azureiotsuite] 사이트를 통해 미리 구성된 솔루션을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="60782-126">기본적으로 도메인 사용자에게는 프로비전된 응용 프로그램의 **Admin** 역할이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="60782-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="60782-127">도메인 사용자는 [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo] 또는 [azure-iot-connected-factory][lnk-cf-github-repo] 리포지토리에서 build.cmd 스크립트를 사용하여 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="60782-128">하지만 도메인 사용자에게는 역할을 할당할 권한이 없으므로 도메인 사용자에게 부여되는 기본 역할은 **읽기 전용**입니다.</span><span class="sxs-lookup"><span data-stu-id="60782-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="60782-129">동일한 AAD 테넌트의 다른 사용자가 응용 프로그램을 만들 경우, 해당 도메인 사용자에게는 기본적으로 해당 응용 프로그램에 대한 **읽기 전용** 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="60782-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="60782-130">도메인 사용자는 응용 프로그램에 역할을 할당할 수 없기 때문에, 응용 프로그램을 프로비전했더라도 응용 프로그램에 사용자를 추가하거나 사용자에 대한 역할을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="60782-131">게스트 사용자</span><span class="sxs-lookup"><span data-stu-id="60782-131">Guest User</span></span>

<span data-ttu-id="60782-132">AAD 테넌트에는 여러 명의 게스트 사용자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="60782-133">게스트 사용자는 AAD 테넌트 내에서 제한된 권한 집합을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="60782-134">결과적으로 게스트 사용자는 AAD 테넌트 내에서 미리 구성된 솔루션을 프로비전할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="60782-135">AAD의 사용자 및 역할에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="60782-136">[Azure AD에서 사용자 만들기][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="60782-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="60782-137">[앱에 사용자 할당][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="60782-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="60782-138">Azure 구독 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="60782-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="60782-139">Azure 관리자 역할은 Azure 구독을 AD 텐넌트에 매핑할 수 있는 권한을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="60782-140">[Azure 공동 관리자, 서비스 관리자 및 계정 관리자를 추가 또는 변경하는 방법][lnk-admin-roles] 문서에서 Azure 관리자 역할에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="60782-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="60782-141">응용 프로그램 역할</span><span class="sxs-lookup"><span data-stu-id="60782-141">Application roles</span></span>

<span data-ttu-id="60782-142">응용 프로그램 역할은 미리 구성된 솔루션의 장치에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="60782-143">프로비전된 응용 프로그램에는 정의된 역할 두 개와 정의된 암시적 역할 한 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="60782-144">**관리:** 설정을 추가, 관리, 장치, 제거 및 수정하는 모든 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="60782-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="60782-145">**읽기 전용:** 장치, 규칙, 작업, 작업 및 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="60782-146">[RolePermissions.cs][lnk-resource-cs] 소스 파일에서 각 역할에 할당된 권한을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="60782-147">사용자에 대한 응용 프로그램 역할 변경</span><span class="sxs-lookup"><span data-stu-id="60782-147">Changing application roles for a user</span></span>

<span data-ttu-id="60782-148">다음 절차를 사용하여 Active Directory의 사용자를 미리 구성된 솔루션의 관리자로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="60782-149">사용자에 대한 역할을 변경하려면 AAD 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="60782-150">[Azure Portal][lnk-portal]로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="60782-151">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="60782-152">이 솔루션을 프로비전할 때 azureiotsuite.com에서 선택한 디렉터리를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="60782-153">구독과 관련된 여러 디렉터리가 있는 경우 포털의 오른쪽 상단에 있는 사용자 계정 이름을 클릭하면 디렉터리를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="60782-154">**엔터프라이즈 응용 프로그램** 및 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="60782-155">**모든** 상태의 **모든 응용 프로그램**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="60782-156">미리 구성된 솔루션의 이름을 가진 응용 프로그램을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="60782-157">미리 구성된 솔루션 이름과 일치하는 응용 프로그램의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="60782-158">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="60782-159">역할을 변경할 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="60782-160">**할당**을 클릭하고 사용자에게 할당하려는 역할(예: **Admin**)을 선택한 다음 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="60782-161">FAQ</span><span class="sxs-lookup"><span data-stu-id="60782-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="60782-162">서비스 관리자가 구독과 특정 AAD 테넌트 간의 디렉터리 매핑을 변경하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="60782-163">이 태스크를 완료하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="60782-163">How do I complete this task?</span></span>

1. <span data-ttu-id="60782-164">[Azure 클래식 포털][lnk-classic-portal]로 이동하여 왼쪽에 있는 서비스 목록에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="60782-165">디렉터리 매핑을 변경할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="60782-166">**디렉터리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="60782-167">드롭다운에서 사용할 **디렉터리** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="60782-168">앞으로 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="60782-169">디렉터리 매핑과 영향을 받는 공동 관리자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="60782-170">다른 디렉터리에서 이동하는 경우에는 원래 디렉터리의 공동 관리자가 모두 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="60782-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="60782-171">AAD 테넌트의 도메인 사용자/회원이 미리 구성된 솔루션을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="60782-172">응용 프로그램에 대한 역할을 어떻게 할당하나요?</span><span class="sxs-lookup"><span data-stu-id="60782-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="60782-173">전역 관리자에게 AAD 테넌트에 대한 전역 관리자로 만들어 달라고 요청한 후 사용자에게 직접 역할을 할당하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="60782-174">또는 전역 관리자에게 역할을 직접 할당해 달라고 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="60782-175">미리 구성된 솔루션이 배포된 AAD 테넌트를 변경하려면 다음 질문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="60782-176">원격 모니터링 미리 구성된 솔루션 및 응용 프로그램이 할당되어 있는 AAD 테넌트를 어떻게 변경하나요?</span><span class="sxs-lookup"><span data-stu-id="60782-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="60782-177"><https://github.com/Azure/azure-iot-remote-monitoring>에서 클라우드 배포를 실행하고 새로 생성된 AAD 테넌트와 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="60782-178">AAD 테넌트를 만들 때 기본적으로 전역 관리자가 되기 때문에, 사용자를 추가하고 해당 사용자에 역할을 추가하는 사용 권한을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60782-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="60782-179">[Azure Portal][lnk-portal]에서 AAD 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60782-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="60782-180"><https://github.com/Azure/azure-iot-remote-monitoring>으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="60782-181">`build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}`(예: `build.cmd cloud debug myRMSolution`)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="60782-182">프롬프트가 표시되면, **tenantid** 를 새로 만든 테넌트가(이전 테넌트 대신) 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="60782-183">조직 계정으로 로그인 할 때 서비스 관리자 또는 공동 관리자를 변경하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="60782-184">지원 문서 [조직 계정으로 로그인하였을 때 서비스 관리자 및 공동 관리자 변경][lnk-service-admins]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="60782-185">왜 이 오류가 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="60782-185">Why am I seeing this error?</span></span> <span data-ttu-id="60782-186">"Your account does not have the proper permissions to create a solution.(사용자의 계정에 솔루션을 생성하기에 적합한 권한이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="60782-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="60782-187">Please check with your account administrator or try with a different account.(계정 관리자에게 문의하거나 다른 계정으로 시도하세요.)"</span><span class="sxs-lookup"><span data-stu-id="60782-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="60782-188">지침은 다음 다이어그램을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="60782-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="60782-189">AAD 테넌트에 대한 전역 관리자이고 구독에 대한 공동 관리자임을 확인한 후에 오류가 계속 표시되는 경우 계정 관리자를 통해 사용자를 제거하고 다음과 같은 순서로 필요한 사용 권한을 다시 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="60782-190">먼저 사용자를 전역 관리자로 추가한 다음 Azure 구독에 대한 공동 관리자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="60782-191">문제가 지속되면 [도움말 및 지원][lnk-help-support]에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="60782-192">Azure 구독이 있는데 왜 이런 오류가 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="60782-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="60782-193">"Azure 구독은 미리 구성된 솔루션을 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="60782-194">몇 분 만에 무료 평가판 계정을 만들 수 있습니다."</span><span class="sxs-lookup"><span data-stu-id="60782-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="60782-195">Azure 구독이 있는 것이 확실하다면, 구독에 대한 테넌트 매핑의 유효성을 검사하고 드롭다운에 올바른 테넌트가 선택되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="60782-196">원하는 테넌트가 맞는다는 것을 확인했으면, 이전의 다이어그램에 따라서 구독과 이 AAD 테넌트 매핑의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="60782-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60782-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60782-197">Next steps</span></span>
<span data-ttu-id="60782-198">IoT Suite에 대해 계속 알아보려면 [미리 구성된 솔루션을 사용자 지정][lnk-customize]하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60782-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
