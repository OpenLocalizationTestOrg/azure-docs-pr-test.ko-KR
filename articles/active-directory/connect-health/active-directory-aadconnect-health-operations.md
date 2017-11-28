---
title: "aaaAzure Active Directory Connect Health 작업"
description: "이 문서에서는 Azure AD Connect Health를 배포한 후 수행할 수 있는 추가 작업에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a><span data-ttu-id="6096b-103">Azure Active Directory Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="6096b-103">Azure Active Directory Connect Health operations</span></span>
<span data-ttu-id="6096b-104">이 항목에서는 hello 설명 다양 한 작업 (Azure AD) Azure Active Directory Connect Health를 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-104">This topic describes hello various operations you can perform by using Azure Active Directory (Azure AD) Connect Health.</span></span>

## <a name="enable-email-notifications"></a><span data-ttu-id="6096b-105">메일 알림 사용</span><span class="sxs-lookup"><span data-stu-id="6096b-105">Enable email notifications</span></span>
<span data-ttu-id="6096b-106">경고 id 인프라 정상 인지를 나타낼 때 hello Azure AD Connect Health 서비스 toosend 전자 메일 알림을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-106">You can configure hello Azure AD Connect Health service toosend email notifications when alerts indicate that your identity infrastructure is not healthy.</span></span> <span data-ttu-id="6096b-107">이 작업은 경고가 생성된 경우 및 해결된 경우에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-107">This occurs when an alert is generated, and when it is resolved.</span></span>

![Azure AD Connect Health 메일 알림 설정 스크린샷](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> <span data-ttu-id="6096b-109">메일 알림은 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-109">Email notifications are enabled by default.</span></span>
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a><span data-ttu-id="6096b-110">tooenable Azure AD Connect Health 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="6096b-110">tooenable Azure AD Connect Health email notifications</span></span>
1. <span data-ttu-id="6096b-111">열기 hello **경고** 블레이드 tooreceive 전자 메일 알림을 사용 하도록 원하는 hello 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-111">Open hello **Alerts** blade for hello service for which you want tooreceive email notification.</span></span>
2. <span data-ttu-id="6096b-112">Hello 작업 모음에서 클릭 **알림 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-112">From hello action bar, click **Notification Settings**.</span></span>
3. <span data-ttu-id="6096b-113">Hello 전자 메일 알림 스위치에서 선택 **ON**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-113">At hello email notification switch, select **ON**.</span></span>
4. <span data-ttu-id="6096b-114">모든 전역 관리자 tooreceive 전자 메일 알림을 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-114">Select hello check box if you want all global administrators tooreceive email notifications.</span></span>
5. <span data-ttu-id="6096b-115">다른 전자 메일 주소에서 전자 메일 알림을 tooreceive 원한다 면 hello에 지정 **추가 전자 메일 받는 사람** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-115">If you want tooreceive email notifications at any other email addresses, specify them in hello **Additional Email Recipients** box.</span></span> <span data-ttu-id="6096b-116">이 목록에서 전자 메일 주소 tooremove hello 항목을 마우스 오른쪽 단추로 클릭 하 고 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-116">tooremove an email address from this list, right-click hello entry and select **Delete**.</span></span>
6. <span data-ttu-id="6096b-117">toofinalize hello 변경을 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-117">toofinalize hello changes, click **Save**.</span></span> <span data-ttu-id="6096b-118">변경 내용은 저장한 후에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-118">Changes take effect only after you save.</span></span>

## <a name="delete-a-server-or-service-instance"></a><span data-ttu-id="6096b-119">서버 또는 서비스 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="6096b-119">Delete a server or service instance</span></span>

<span data-ttu-id="6096b-120">어떤 경우에는 서버에서 모니터링 되 고 tooremove를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-120">In some instances, you might want tooremove a server from being monitored.</span></span> <span data-ttu-id="6096b-121">여기에 사용자의 할 tooknow tooremove hello Azure AD Connect Health 서비스에서 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-121">Here's what you need tooknow tooremove a server from hello Azure AD Connect Health service.</span></span>

<span data-ttu-id="6096b-122">서버를 삭제 하는 경우 hello 다음 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-122">When you're deleting a server, be aware of hello following:</span></span>

* <span data-ttu-id="6096b-123">이 작업을 수행하면 해당 서버에서 추가 데이터 수집이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-123">This action stops collecting any further data from that server.</span></span> <span data-ttu-id="6096b-124">이 서버는 모니터링 서비스는 hello에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-124">This server is removed from hello monitoring service.</span></span> <span data-ttu-id="6096b-125">이 작업 후 없는 수 tooview 새 경고, 모니터링 또는이 서버에 대 한 사용 현황 분석 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-125">After this action, you are not able tooview new alerts, monitoring, or usage analytics data for this server.</span></span>
* <span data-ttu-id="6096b-126">이 작업은 서버에서 Health Agent hello를 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-126">This action does not uninstall hello Health Agent from your server.</span></span> <span data-ttu-id="6096b-127">이 단계를 수행 하기 전에 hello Health Agent를 제거 하지 않은 오류 관련된 toohello Health Agent hello 서버에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-127">If you have not uninstalled hello Health Agent before performing this step, you might see errors related toohello Health Agent on hello server.</span></span>
* <span data-ttu-id="6096b-128">이 작업에는 이미이 서버에서 수집 하는 hello 데이터 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-128">This action does not delete hello data already collected from this server.</span></span> <span data-ttu-id="6096b-129">Hello Azure 데이터 보존 정책에 따라 해당 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-129">That data is deleted in accordance with hello Azure data retention policy.</span></span>
* <span data-ttu-id="6096b-130">이 작업을 수행한 후 원하는 경우 toostart 모니터링 hello 동일한 서버 제거 하 고이 서버에서 Health Agent hello를 다시 설치 해야 듯이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-130">After performing this action, if you want toostart monitoring hello same server again, you must uninstall and reinstall hello Health Agent on this server.</span></span>

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a><span data-ttu-id="6096b-131">toodelete hello Azure AD Connect Health 서비스에서 서버</span><span class="sxs-lookup"><span data-stu-id="6096b-131">toodelete a server from hello Azure AD Connect Health service</span></span>
<span data-ttu-id="6096b-132">AD FS(Active Directory Federation Services)용 Azure AD Connect Health 및 Azure AD Connect(동기화):</span><span class="sxs-lookup"><span data-stu-id="6096b-132">Azure AD Connect Health for Active Directory Federation Services (AD FS) and Azure AD Connect (Sync):</span></span>

1. <span data-ttu-id="6096b-133">열기 hello **서버** hello에서 블레이드 **서버 목록** 블레이드 hello 서버 이름 toobe를 선택 하 여 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-133">Open hello **Server** blade from hello **Server List** blade by selecting hello server name toobe removed.</span></span>
2. <span data-ttu-id="6096b-134">Hello에 **서버** 블레이드 hello 작업 모음에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-134">On hello **Server** blade, from hello action bar, click **Delete**.</span></span>
3. <span data-ttu-id="6096b-135">Hello 확인 상자에 hello 서버 이름을 입력 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-135">Confirm by typing hello server name in hello confirmation box.</span></span>
4. <span data-ttu-id="6096b-136">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-136">Click **Delete**.</span></span>

<span data-ttu-id="6096b-137">Azure Active Directory Domain Services용 Azure AD Connect Health:</span><span class="sxs-lookup"><span data-stu-id="6096b-137">Azure AD Connect Health for Azure Active Directory Domain Services:</span></span>

1. <span data-ttu-id="6096b-138">열기 hello **도메인 컨트롤러** 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-138">Open hello **Domain Controllers** dashboard.</span></span>
2. <span data-ttu-id="6096b-139">도메인 컨트롤러 toobe 선택 hello 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-139">Select hello domain controller toobe removed.</span></span>
3. <span data-ttu-id="6096b-140">Hello 작업 모음에서 클릭 **삭제 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-140">From hello action bar, click **Delete Selected**.</span></span>
4. <span data-ttu-id="6096b-141">Hello 동작 toodelete hello 서버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-141">Confirm hello action toodelete hello server.</span></span>
5. <span data-ttu-id="6096b-142">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-142">Click **Delete**.</span></span>

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a><span data-ttu-id="6096b-143">Azure AD Connect Health 서비스에서 서비스 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="6096b-143">Delete a service instance from Azure AD Connect Health service</span></span>
<span data-ttu-id="6096b-144">경우에 따라 tooremove 서비스 인스턴스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-144">In some instances, you might want tooremove a service instance.</span></span> <span data-ttu-id="6096b-145">작업 필요 tooknow tooremove 서비스 인스턴스 hello Azure AD Connect Health 서비스에서 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-145">Here's what you need tooknow tooremove a service instance from hello Azure AD Connect Health service.</span></span>

<span data-ttu-id="6096b-146">서비스 인스턴스를 삭제 하는 경우 hello 다음 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-146">When you're deleting a service instance, be aware of hello following:</span></span>

* <span data-ttu-id="6096b-147">이 작업에서 서비스를 모니터링 하는 hello hello 현재 서비스 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-147">This action removes hello current service instance from hello monitoring service.</span></span>
* <span data-ttu-id="6096b-148">이 작업을 제거 하거나이 서비스 인스턴스의 일부로 모니터링 않은 hello 서버 중 하나에서 hello Health Agent를 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-148">This action does not uninstall or remove hello Health Agent from any of hello servers that were monitored as part of this service instance.</span></span> <span data-ttu-id="6096b-149">이 단계를 수행 하기 전에 hello Health Agent를 제거 하지 않은 오류 관련된 toohello Health Agent hello 서버에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-149">If you have not uninstalled hello Health Agent before performing this step, you might see errors related toohello Health Agent on hello servers.</span></span>
* <span data-ttu-id="6096b-150">이 서비스 인스턴스의 모든 데이터는 hello Azure 데이터 보존 정책에 따라 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-150">All data from this service instance is deleted in accordance with hello Azure data retention policy.</span></span>
* <span data-ttu-id="6096b-151">이 작업을 수행한 후 toostart hello 서비스를 모니터링 하려는 경우 제거 하 고 모든 hello 서버에서 Health Agent hello를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-151">After performing this action, if you want toostart monitoring hello service, uninstall and reinstall hello Health Agent on all hello servers.</span></span> <span data-ttu-id="6096b-152">이 작업을 수행한 후 toostart hello 동일한 서버를 다시 제거, 다시 설치 및 등록을 모니터링 하려는 경우 해당 서버에서 Health Agent hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-152">After performing this action, if you want toostart monitoring hello same server again, uninstall, reinstall, and register hello Health Agent on that server.</span></span>

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a><span data-ttu-id="6096b-153">toodelete hello Azure AD Connect Health 서비스에서 서비스 인스턴스</span><span class="sxs-lookup"><span data-stu-id="6096b-153">toodelete a service instance from hello Azure AD Connect Health service</span></span>
1. <span data-ttu-id="6096b-154">열기 hello **서비스** hello에서 블레이드 **서비스 목록** 블레이드 tooremove 원하는 hello 서비스 id (팜 이름)을 선택 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-154">Open hello **Service** blade from hello **Service List** blade by selecting hello service identifier (farm name) that you want tooremove.</span></span>
2. <span data-ttu-id="6096b-155">Hello에 **서버** 블레이드 hello 작업 모음에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-155">On hello **Server** blade, from hello action bar, click **Delete**.</span></span>
3. <span data-ttu-id="6096b-156">Hello 확인 상자에서 hello 서비스 이름을 입력 하 여 확인 (예: sts.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="6096b-156">Confirm by typing hello service name in hello confirmation box (for example: sts.contoso.com).</span></span>
4. <span data-ttu-id="6096b-157">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-157">Click **Delete**.</span></span>
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a><span data-ttu-id="6096b-158">역할 기반 액세스 제어로 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="6096b-158">Manage access with Role-Based Access Control</span></span>
<span data-ttu-id="6096b-159">[역할 기반 액세스 제어 (RBAC)](../role-based-access-control-configure.md) Azure AD Connect Health 액세스 toousers 및 전역 관리자가 아닌 다른 그룹을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-159">[Role-Based Access Control (RBAC)](../role-based-access-control-configure.md) for Azure AD Connect Health provides access toousers and groups other than global administrators.</span></span> <span data-ttu-id="6096b-160">RBAC 역할 toohello 의도 한 사용자 및 그룹을 할당 하 고 hello toolimit 디렉터리 내에서 전역 관리자는 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-160">RBAC assigns roles toohello intended users and groups, and provides a mechanism toolimit hello global administrators within your directory.</span></span>

### <a name="roles"></a><span data-ttu-id="6096b-161">역할</span><span class="sxs-lookup"><span data-stu-id="6096b-161">Roles</span></span>
<span data-ttu-id="6096b-162">Azure AD Connect Health hello 다음 기본 제공 역할을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-162">Azure AD Connect Health supports hello following built-in roles:</span></span>

| <span data-ttu-id="6096b-163">역할</span><span class="sxs-lookup"><span data-stu-id="6096b-163">Role</span></span> | <span data-ttu-id="6096b-164">권한</span><span class="sxs-lookup"><span data-stu-id="6096b-164">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="6096b-165">소유자</span><span class="sxs-lookup"><span data-stu-id="6096b-165">Owner</span></span> |<span data-ttu-id="6096b-166">소유자 수 *액세스 관리* (예를 들어 역할 tooa 사용자 또는 그룹)를 할당 *모든 정보를 볼* (예를 들어 경고 보기) hello 포털에서 및 *설정을 변경* 드 ( 예를 들어 전자 메일 알림을) Azure AD Connect Health 내에서.</span><span class="sxs-lookup"><span data-stu-id="6096b-166">Owners can *manage access* (for example, assign a role tooa user or group), *view all information* (for example, view alerts) from hello portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> <br><span data-ttu-id="6096b-167">기본적으로 Azure AD 전역 관리자에게 이 역할이 할당되며, 이 설정은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-167">By default, Azure AD global administrators are assigned this role, and this cannot be changed.</span></span> |
| <span data-ttu-id="6096b-168">참여자</span><span class="sxs-lookup"><span data-stu-id="6096b-168">Contributor</span></span> |<span data-ttu-id="6096b-169">참가자 수 *모든 정보를 볼* (예를 들어 경고 보기) hello 포털에서 및 *설정을 변경* (예를 들어 전자 메일 알림을) Azure AD Connect Health 내에서.</span><span class="sxs-lookup"><span data-stu-id="6096b-169">Contributors can *view all information* (for example, view alerts) from hello portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> |
| <span data-ttu-id="6096b-170">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="6096b-170">Reader</span></span> |<span data-ttu-id="6096b-171">판독기 수 *모든 정보를 볼* (예를 들어 경고 보기)에서 Azure AD Connect Health 포털 hello에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-171">Readers can *view all information* (for example, view alerts) from hello portal within Azure AD Connect Health.</span></span> |

<span data-ttu-id="6096b-172">Hello 역할 hello 포털 환경에서 사용할 수 있는 경우에 Azure AD Connect Health를 내 없습니다 영향 tooaccess 있어야 하는 다른 역할 (예: 사용자 액세스 관리자가 또는 DevTest Labs 사용자).</span><span class="sxs-lookup"><span data-stu-id="6096b-172">All other roles (such as User Access Administrators or DevTest Labs Users) have no impact tooaccess within Azure AD Connect Health, even if hello roles are available in hello portal experience.</span></span>

### <a name="access-scope"></a><span data-ttu-id="6096b-173">액세스 범위</span><span class="sxs-lookup"><span data-stu-id="6096b-173">Access scope</span></span>
<span data-ttu-id="6096b-174">Azure AD Connect Health는 다음 두 수준에서 액세스 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-174">Azure AD Connect Health supports managing access at two levels:</span></span>

* <span data-ttu-id="6096b-175">**모든 서비스 인스턴스**:이 hello 대부분의 경우에서 경로 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-175">**All service instances**: This is hello recommended path in most cases.</span></span> <span data-ttu-id="6096b-176">Azure AD Connect Health에서 모니터링되는 모든 역할 유형에서 모든 서비스 인스턴스(예: AD FS 팜)에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-176">It controls access for all service instances (for example, an AD FS farm) across all role types that are being monitored by Azure AD Connect Health.</span></span>
* <span data-ttu-id="6096b-177">**서비스 인스턴스**: 일부 경우에 따라 역할 유형 또는 서비스 인스턴스에 의해 toosegregate 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-177">**Service instance**: In some cases, you might need toosegregate access based on role types or by a service instance.</span></span> <span data-ttu-id="6096b-178">이 경우 hello 서비스 인스턴스 수준에서 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-178">In this case, you can manage access at hello service instance level.</span></span>  

<span data-ttu-id="6096b-179">최종 사용자가 hello 디렉터리 또는 서비스에 액세스할 권한이 부여 되었는지 인스턴스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-179">Permission is granted if an end user has access either at hello directory or service instance level.</span></span>

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a><span data-ttu-id="6096b-180">허용 사용자 또는 그룹 액세스 tooAzure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="6096b-180">Allow users or groups access tooAzure AD Connect Health</span></span>
<span data-ttu-id="6096b-181">hello 다음 단계에서는 tooallow 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="6096b-181">hello following steps show how tooallow access.</span></span>
#### <a name="step-1-select-hello-appropriate-access-scope"></a><span data-ttu-id="6096b-182">1 단계: hello 적절 한 액세스 범위를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-182">Step 1: Select hello appropriate access scope</span></span>
<span data-ttu-id="6096b-183">hello에 대 한 사용자 액세스 tooallow *모든 서비스 인스턴스* Azure AD Connect Health를 Azure AD Connect Health에 주 블레이드를 열고 hello 내의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-183">tooallow a user access at hello *all service instances* level within Azure AD Connect Health, open hello main blade in Azure AD Connect Health.</span></span><br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a><span data-ttu-id="6096b-184">2단계: 사용자 및 그룹 추가, 역할 할당</span><span class="sxs-lookup"><span data-stu-id="6096b-184">Step 2: Add users and groups, and assign roles</span></span>
1. <span data-ttu-id="6096b-185">Hello에서 **구성** 섹션에서 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-185">From hello **Configure** section, click **Users**.</span></span><br><span data-ttu-id="6096b-186">
   ![사용자가 강조 표시된 Azure AD Connect Health RBAC 주 블레이드 스크린샷](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span><span class="sxs-lookup"><span data-stu-id="6096b-186">
![Screenshot of Azure AD Connect Health RBAC main blade, with Users highlighted](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span></span>
2. <span data-ttu-id="6096b-187">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-187">Select **Add**.</span></span>
3. <span data-ttu-id="6096b-188">Hello에 **역할 선택** 창 역할을 선택 합니다 (예를 들어 **소유자**).</span><span class="sxs-lookup"><span data-stu-id="6096b-188">In hello **Select a role** pane, select a role (for example, **Owner**).</span></span><br><span data-ttu-id="6096b-189">
   ![Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_add.png)</span><span class="sxs-lookup"><span data-stu-id="6096b-189">
![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_add.png)</span></span>
4. <span data-ttu-id="6096b-190">Hello 이름 또는 대상으로 하는 hello 사용자 또는 그룹의 식별자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-190">Type hello name or identifier of hello targeted user or group.</span></span> <span data-ttu-id="6096b-191">하나 이상의 사용자 또는 그룹이 hello에서 선택할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-191">You can select one or more users or groups at hello same time.</span></span> <span data-ttu-id="6096b-192">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-192">Click **Select**.</span></span>
   <span data-ttu-id="6096b-193">![Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span><span class="sxs-lookup"><span data-stu-id="6096b-193">![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span></span>
5. <span data-ttu-id="6096b-194">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-194">Select **OK**.</span></span><br>
6. <span data-ttu-id="6096b-195">Hello 역할 할당이 완료 되 면 hello 사용자 및 그룹 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-195">After hello role assignment is complete, hello users and groups appear in hello list.</span></span><br><span data-ttu-id="6096b-196">
   ![새 사용자가 강조 표시된 Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span><span class="sxs-lookup"><span data-stu-id="6096b-196">
![Screenshot of Azure AD Connect Health RBAC Users window, with new users highlighted](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span></span>

<span data-ttu-id="6096b-197">Hello 사용자가 나열 하는 이제 하 고 액세스할 수 있는 그룹, tootheir 할당 된 역할에 따라 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-197">Now hello listed users and groups have access, according tootheir assigned roles.</span></span>

> [!NOTE]
> * <span data-ttu-id="6096b-198">전역 관리자가 전체 액세스 tooall hello 작업 같으면 주도 전역 관리자 계정을 hello 목록 앞에 존재 하지 않는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-198">Global administrators always have full access tooall hello operations, but global administrator accounts are not present in hello preceding list.</span></span>
> * <span data-ttu-id="6096b-199">hello 사용자 초대 기능은 Azure AD Connect Health 내에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-199">hello Invite Users feature is not supported within Azure AD Connect Health.</span></span>
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a><span data-ttu-id="6096b-200">사용자 또는 그룹을 사용 하 여 3 단계: 공유 hello 블레이드 위치</span><span class="sxs-lookup"><span data-stu-id="6096b-200">Step 3: Share hello blade location with users or groups</span></span>
1. <span data-ttu-id="6096b-201">사용 권한을 할당하면 사용자가 [여기](http://aka.ms/aadconnecthealth)로 이동하여 Azure AD Connect Health에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-201">After you assign permissions, a user can access Azure AD Connect Health by going [here](http://aka.ms/aadconnecthealth).</span></span>
2. <span data-ttu-id="6096b-202">Hello 블레이드에서 hello 사용자 hello 블레이드 또는 여러 부분을, toohello 대시보드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-202">On hello blade, hello user can pin hello blade, or different parts of it, toohello dashboard.</span></span> <span data-ttu-id="6096b-203">Hello를 클릭 하기만 하면 **Pin toodashboard** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-203">Simply click hello **Pin toodashboard** icon.</span></span><br><span data-ttu-id="6096b-204">
   ![고정 아이콘이 강조 표시된 Azure AD Connect Health RBAC 고정 블레이드 스크린샷](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span><span class="sxs-lookup"><span data-stu-id="6096b-204">
![Screenshot of Azure AD Connect Health RBAC pin blade, with pin icon highlighted](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span></span>

> [!NOTE]
> <span data-ttu-id="6096b-205">Hello 판독기 역할 할당의 사용자에 hello Azure Marketplace에서에서 수 tooget Azure AD Connect Health 확장명이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-205">A user with hello Reader role assigned is not able tooget Azure AD Connect Health extension from hello Azure Marketplace.</span></span> <span data-ttu-id="6096b-206">hello 사용자 hello 필요한 "만들기" 작업 toodo을 지금 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-206">hello user cannot perform hello necessary "create" operation toodo so.</span></span> <span data-ttu-id="6096b-207">hello 사용자 이동 toohello 앞에 링크 하 여 toohello 블레이드에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-207">hello user can still get toohello blade by going toohello preceding link.</span></span> <span data-ttu-id="6096b-208">후속 사용에 대 한 hello 사용자 hello 블레이드 toohello 대시보드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-208">For subsequent usage, hello user can pin hello blade toohello dashboard.</span></span>
>
>

### <a name="remove-users-or-groups"></a><span data-ttu-id="6096b-209">사용자 또는 그룹 제거</span><span class="sxs-lookup"><span data-stu-id="6096b-209">Remove users or groups</span></span>
<span data-ttu-id="6096b-210">사용자 또는 그룹 추가 제거할 수 있습니다 tooAzure AD 상태 RBAC 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-210">You can remove a user or a group added tooAzure AD Connect Health RBAC.</span></span> <span data-ttu-id="6096b-211">단순히 hello 사용자 또는 그룹을 마우스 오른쪽 단추로 클릭 하 고 선택 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="6096b-211">Simply right-click hello user or group, and select **Remove**.</span></span><br><span data-ttu-id="6096b-212">
![제거가 강조 표시된 Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_remove.png)</span><span class="sxs-lookup"><span data-stu-id="6096b-212">
![Screenshot of Azure AD Connect Health RBAC Users window, with Remove highlighted](./media/active-directory-aadconnect-health/RBAC_remove.png)</span></span>

[//]: # (End of RBAC section)

## <a name="next-steps"></a><span data-ttu-id="6096b-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6096b-213">Next steps</span></span>
* [<span data-ttu-id="6096b-214">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="6096b-214">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="6096b-215">Azure AD Connect Health 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="6096b-215">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="6096b-216">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="6096b-216">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="6096b-217">동기화에 대한 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="6096b-217">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="6096b-218">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="6096b-218">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="6096b-219">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="6096b-219">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="6096b-220">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="6096b-220">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
