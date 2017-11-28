---
title: "aaaAzure IoT Suite 및 Azure Active Directory | Microsoft Docs"
description: "Azure IoT Suite는 Azure Active Directory toomanage 권한을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="516a5-103">Hello azureiotsuite.com 사이트에 대 한 권한</span><span class="sxs-lookup"><span data-stu-id="516a5-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="516a5-104">로그인 후 진행되는 작업</span><span class="sxs-lookup"><span data-stu-id="516a5-104">What happens when you sign in</span></span>

<span data-ttu-id="516a5-105">처음으로 로그인 할 hello [azureiotsuite.com][lnk-azureiotsuite], hello 사이트 결정 하 고 현재 hello 기준 사용할 hello 사용 권한 수준을 선택 된 Azure Active Directory (AAD) 테 넌 트 및 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="516a5-106">첫째, toopopulate hello 목록을 표시 하는 테 넌 트가 다음 tooyour 사용자 이름, hello 사이트를 구합니다 Azure에서 어떤 AAD 테 넌 트를에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="516a5-107">현재 hello 사이트 한 번에 한 테 넌 트에 대 한 사용자 토큰을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="516a5-108">따라서 hello 오른쪽 위 모서리에서 hello 드롭다운을 사용 하 여 테 넌 트를 전환할 때는 hello 사이트 로그 toothat 테 넌 트 tooobtain hello 토큰에서 해당 테 넌 트에 대 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="516a5-109">다음으로 hello 사이트 hello과 연결한 구독 테 넌 트를 선택 하는 Azure에서 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="516a5-110">새 미리 구성 된 솔루션을 만들 때 사용할 수 있는 구독 hello를 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="516a5-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="516a5-111">마지막으로 hello 사이트 hello 구독의 모든 hello 리소스를 검색 하 고 리소스 그룹 미리 구성 된 솔루션으로 태그를 지정 하 고 hello 홈 페이지 hello 타일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="516a5-112">다음 섹션 hello 액세스 toohello 미리 구성 된 솔루션을 제어 하는 hello 역할을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="516a5-113">AAD 역할</span><span class="sxs-lookup"><span data-stu-id="516a5-113">AAD roles</span></span>

<span data-ttu-id="516a5-114">hello AAD 역할 제어 hello 기능 미리 구성 된 프로 비전 솔루션 및 미리 구성 된 솔루션에서 사용자를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="516a5-115">AAD에서 사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당][lnk-aad-admin]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="516a5-116">hello 현재 문서에서는 hello **전역 관리자** 및 hello **사용자** hello에서 사용 되는 디렉터리 역할 미리 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="516a5-117">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="516a5-117">Global administrator</span></span>

<span data-ttu-id="516a5-118">AAD 테넌트에는 여러 명의 전역 관리자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="516a5-119">AAD 테 넌 트를 만들 때 기본 hello 해당 테 넌 트의 전역 관리자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="516a5-120">전역 관리자에 게는 미리 구성 된 솔루션을 프로 비전 할 수 있으며가 할당 한 **Admin** AAD 테 넌 트 내 hello 응용 프로그램에 대 한 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="516a5-121">다른 사용자에 동일한 hello 경우 AAD 테 넌 트 응용 프로그램을 만듭니다, 부여 toohello 전역 관리자는 hello 기본 역할 **ReadOnly**합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="516a5-122">전역 관리자 사용자 tooroles hello를 사용 하 여 응용 프로그램에 대해 할당할 수 [Azure 포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="516a5-123">도메인 사용자</span><span class="sxs-lookup"><span data-stu-id="516a5-123">Domain user</span></span>

<span data-ttu-id="516a5-124">AAD 테넌트에는 여러 명의 도메인 사용자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="516a5-125">도메인 사용자 hello 통해 미리 구성 된 솔루션을 프로 비전 할 수 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="516a5-126">Hello 도메인 사용자가 hello 기본적으로 부여 **Admin** 역할 hello에 응용 프로그램을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="516a5-127">도메인 사용자는 hello에 hello build.cmd 스크립트를 사용 하 여 응용 프로그램을 만들 수 [azure iot-원격 액세스 모니터링][lnk-rm-github-repo], [azure iot-예측-유지 관리] [ lnk-pm-github-repo], 또는 [azure iot-연결-공장] [ lnk-cf-github-repo] 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="516a5-128">그러나 hello 기본 역할 toohello 도메인 사용자가을 부여 **ReadOnly**, 도메인 사용자 권한이 tooassign 역할 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="516a5-129">Hello 도메인 사용자가 hello 할당 hello AAD 테 넌 트에 있는 다른 사용자가 응용 프로그램을 만드는 경우 **ReadOnly** 해당 응용 프로그램에 대해 기본적으로 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="516a5-130">도메인 사용자는 응용 프로그램에 역할을 할당할 수 없기 때문에, 응용 프로그램을 프로비전했더라도 응용 프로그램에 사용자를 추가하거나 사용자에 대한 역할을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="516a5-131">게스트 사용자</span><span class="sxs-lookup"><span data-stu-id="516a5-131">Guest User</span></span>

<span data-ttu-id="516a5-132">AAD 테넌트에는 여러 명의 게스트 사용자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="516a5-133">게스트 사용자에 게 hello AAD 테 넌 트의 제한 된 권한 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="516a5-134">따라서 게스트 사용자에 게 hello AAD 테 넌 트에 미리 구성 된 솔루션을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="516a5-135">AAD에서 사용자 및 역할에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="516a5-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="516a5-136">[Azure AD에서 사용자 만들기][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="516a5-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="516a5-137">[사용자가 tooapps 할당][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="516a5-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="516a5-138">Azure 구독 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="516a5-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="516a5-139">hello Azure 관리자 역할 hello 기능 toomap Azure 구독 tooan AD 테 넌 트를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="516a5-140">Hello 문서의 hello Azure 관리자 역할에 대 한 자세한 내용을 알아보려면 [어떻게 tooadd Azure 공동 관리자, 서비스 관리자 및 관리자 계정 변경 또는][lnk-admin-roles]합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="516a5-141">응용 프로그램 역할</span><span class="sxs-lookup"><span data-stu-id="516a5-141">Application roles</span></span>

<span data-ttu-id="516a5-142">hello 응용 프로그램 역할에는 미리 구성 된 솔루션에 대 한 액세스 toodevices를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="516a5-143">프로비전된 응용 프로그램에는 정의된 역할 두 개와 정의된 암시적 역할 한 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="516a5-144">**Admin:** tooadd 모든 권한 관리, 장치, 제거 및 설정을 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="516a5-145">**읽기 전용:** 장치, 규칙, 작업, 작업 및 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="516a5-146">Hello 권한이 hello에 tooeach 역할 할당을 찾을 수 있습니다 [RolePermissions.cs] [ lnk-resource-cs] 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="516a5-147">사용자에 대한 응용 프로그램 역할 변경</span><span class="sxs-lookup"><span data-stu-id="516a5-147">Changing application roles for a user</span></span>

<span data-ttu-id="516a5-148">다음 프로시저 toomake 미리 구성 된 솔루션의 관리자가 Active Directory에서 사용자 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="516a5-149">사용자에 대 한 AAD 전역 관리자 toochange 역할 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="516a5-150">Toohello 이동 [Azure 포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="516a5-151">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="516a5-152">솔루션을 프로 비전 할 때 azureiotsuite.com에 선택한 hello 디렉터리를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="516a5-153">구독에 연결 된 여러 디렉터리를 설정한 경우에 hello의 오른쪽 위에 hello 포털에서 계정 이름을 클릭 하는 경우 서로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="516a5-154">**엔터프라이즈 응용 프로그램** 및 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="516a5-155">**모든** 상태의 **모든 응용 프로그램**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="516a5-156">미리 구성된 솔루션의 이름을 가진 응용 프로그램을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="516a5-157">미리 구성 된 솔루션 이름과 일치 하는 hello 응용 프로그램의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="516a5-158">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="516a5-159">Tooswitch 역할 hello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="516a5-160">클릭 **할당** 및 선택 hello 역할 (같은 **Admin**) tooassign toohello 사용자 원하는 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="516a5-161">FAQ</span><span class="sxs-lookup"><span data-stu-id="516a5-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="516a5-162">서비스 관리자 및 내 구독이 특정 AAD 테 넌 트 간의 toochange hello 디렉터리 매핑을 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="516a5-163">이 태스크를 완료하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="516a5-163">How do I complete this task?</span></span>

1. <span data-ttu-id="516a5-164">Toohello 이동 [Azure 클래식 포털][lnk-classic-portal], 클릭 **설정을** hello 왼쪽에 있는 서비스의 hello 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="516a5-165">Hello 구독 하도록 toochange hello 디렉터리 매핑을 선택을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="516a5-166">**디렉터리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="516a5-167">선택 hello **디렉터리** toouse hello 드롭다운에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="516a5-168">Hello 앞으로 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="516a5-169">Hello 디렉터리 매핑을 확인 하 고 공동 관리자의 영향을 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="516a5-170">다른 디렉터리에서 이동 하는 경우 모든 hello 공동 관리자 hello 원래 디렉터리에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="516a5-171">Hello AAD 테 넌 트에 도메인 사용자/멤버로 하 고 미리 구성 된 솔루션을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="516a5-172">응용 프로그램에 대한 역할을 어떻게 할당하나요?</span><span class="sxs-lookup"><span data-stu-id="516a5-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="516a5-173">전역 관리자 toomake AAD hello에 대 한 전역 관리자 테 넌 트 고객과 게 다음 역할 toousers을 자신에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="516a5-174">또는 전역 관리자 tooassign를 요청 하는 역할을 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="516a5-175">Toochange hello AAD 테 넌 트가 미리 구성 된 솔루션을 배포한, 원하는 경우 hello 다음 질문을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="516a5-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="516a5-176">내 원격 모니터링 미리 구성 된 솔루션 및 응용 프로그램에 할당 된 hello AAD 테 넌 트를 전환 하는 방법</span><span class="sxs-lookup"><span data-stu-id="516a5-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="516a5-177"><https://github.com/Azure/azure-iot-remote-monitoring>에서 클라우드 배포를 실행하고 새로 생성된 AAD 테넌트와 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="516a5-178">기본적으로 AAD 테 넌 트를 만들 때 전역 관리자가 아니므로 tooadd 사용자 사용 권한에 있고 toothose 사용자 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="516a5-179">Hello에서 AAD 디렉터리를 만들 [Azure 포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="516a5-180">너무 이동<https://github.com/Azure/azure-iot-remote-monitoring>합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="516a5-181">`build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}`(예: `build.cmd cloud debug myRMSolution`)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="516a5-182">메시지가 표시 되 면 hello 설정 **tenantid** toobe 이전 테 넌 트 대신 새로 만든된 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="516a5-183">원하는 toochange organisational 계정으로 로그인 하는 경우 공동 관리자 또는 서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="516a5-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="516a5-184">Hello 지원 문서를 참조 [변경 서비스 관리자 및 공동 관리자 organisational 계정으로 로그인 하는 경우][lnk-service-admins]합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="516a5-185">왜 이 오류가 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="516a5-185">Why am I seeing this error?</span></span> <span data-ttu-id="516a5-186">"사용자 계정에 없는 hello 적절 한 사용 권한이 toocreate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="516a5-187">Please check with your account administrator or try with a different account.(계정 관리자에게 문의하거나 다른 계정으로 시도하세요.)"</span><span class="sxs-lookup"><span data-stu-id="516a5-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="516a5-188">다음 지침에 대 한 다이어그램 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="516a5-189">Toosee hello 오류가 계속 되 면 hello AAD 테 넌 트에 대 한 전역 관리자 및 hello 구독에 대 한 공동 관리자는 확인 한 후, 계정 관리자를 통해 hello 사용자를 제거 하 고이 순서에 필요한 사용 권한을 다시 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="516a5-190">첫째, 전역 관리자로 hello 사용자를 추가 하 고 hello Azure 구독에 공동 관리자로 서 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="516a5-191">문제가 지속되면 [도움말 및 지원][lnk-help-support]에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="516a5-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="516a5-192">Azure 구독이 있는데 왜 이런 오류가 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="516a5-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="516a5-193">"Azure 구독은 필요한 toocreate 미리 구성 된 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="516a5-194">몇 분 만에 무료 평가판 계정을 만들 수 있습니다."</span><span class="sxs-lookup"><span data-stu-id="516a5-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="516a5-195">을 사용 하는 Azure 구독이 있는 특정 hello 테 넌 트 구독에 대 한 매핑이 검사 하 고 hello 올바른 테 넌 트 hello 드롭다운에서 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="516a5-196">유효성을 검사 한 경우에 hello 원하는 테 넌 트는 올바른 hello 다이어그램 앞에 따르고 구독과이 AAD 테 넌 트의 hello 매핑의 유효성을 검사할 합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="516a5-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="516a5-197">Next steps</span></span>
<span data-ttu-id="516a5-198">toocontinue IoT Suite에 대 한 학습 하는 방법을 참조 [미리 구성 된 솔루션을 사용자 지정][lnk-customize]합니다.</span><span class="sxs-lookup"><span data-stu-id="516a5-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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
