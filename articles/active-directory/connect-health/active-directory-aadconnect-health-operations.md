---
title: "Azure Active Directory Connect Health 작업"
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
ms.openlocfilehash: 06afc6b4149ea1590a2994d1638d6979a89035e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-connect-health-operations"></a><span data-ttu-id="5ca97-103">Azure Active Directory Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="5ca97-103">Azure Active Directory Connect Health operations</span></span>
<span data-ttu-id="5ca97-104">이 항목에서는 Azure AD(Azure Active Directory) Connect Health를 사용하여 수행할 수 있는 다양한 작업에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-104">This topic describes the various operations you can perform by using Azure Active Directory (Azure AD) Connect Health.</span></span>

## <a name="enable-email-notifications"></a><span data-ttu-id="5ca97-105">메일 알림 사용</span><span class="sxs-lookup"><span data-stu-id="5ca97-105">Enable email notifications</span></span>
<span data-ttu-id="5ca97-106">ID 인프라가 정상 상태가 아님을 나타내는 경고가 표시되면 메일 알림을 보내도록 Azure AD Connect Health 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-106">You can configure the Azure AD Connect Health service to send email notifications when alerts indicate that your identity infrastructure is not healthy.</span></span> <span data-ttu-id="5ca97-107">이 작업은 경고가 생성된 경우 및 해결된 경우에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-107">This occurs when an alert is generated, and when it is resolved.</span></span>

![Azure AD Connect Health 메일 알림 설정 스크린샷](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> <span data-ttu-id="5ca97-109">메일 알림은 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-109">Email notifications are enabled by default.</span></span>
>
>

### <a name="to-enable-azure-ad-connect-health-email-notifications"></a><span data-ttu-id="5ca97-110">Azure AD Connect Health 메일 알림을 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="5ca97-110">To enable Azure AD Connect Health email notifications</span></span>
1. <span data-ttu-id="5ca97-111">메일 알림을 받으려는 서비스의 **경고** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-111">Open the **Alerts** blade for the service for which you want to receive email notification.</span></span>
2. <span data-ttu-id="5ca97-112">작업 모음에서 **알림 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-112">From the action bar, click **Notification Settings**.</span></span>
3. <span data-ttu-id="5ca97-113">메일 알림 스위치에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-113">At the email notification switch, select **ON**.</span></span>
4. <span data-ttu-id="5ca97-114">모든 전역 관리자가 메일 알림을 수신하도록 하려는 경우 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-114">Select the check box if you want all global administrators to receive email notifications.</span></span>
5. <span data-ttu-id="5ca97-115">다른 메일 주소로 메일 알림을 받으려는 경우 **추가 메일 받는 사람** 상자에 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-115">If you want to receive email notifications at any other email addresses, specify them in the **Additional Email Recipients** box.</span></span> <span data-ttu-id="5ca97-116">이 목록에서 메일 주소를 제거하려면 항목을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-116">To remove an email address from this list, right-click the entry and select **Delete**.</span></span>
6. <span data-ttu-id="5ca97-117">변경을 완료하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-117">To finalize the changes, click **Save**.</span></span> <span data-ttu-id="5ca97-118">변경 내용은 저장한 후에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-118">Changes take effect only after you save.</span></span>

## <a name="delete-a-server-or-service-instance"></a><span data-ttu-id="5ca97-119">서버 또는 서비스 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="5ca97-119">Delete a server or service instance</span></span>

<span data-ttu-id="5ca97-120">서버를 모니터링 대상에서 제거하려는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-120">In some instances, you might want to remove a server from being monitored.</span></span> <span data-ttu-id="5ca97-121">Azure AD Connect Health 서비스에서 서버를 제거하기 위해 알아야 할 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-121">Here's what you need to know to remove a server from the Azure AD Connect Health service.</span></span>

<span data-ttu-id="5ca97-122">서버를 삭제하는 경우 다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="5ca97-122">When you're deleting a server, be aware of the following:</span></span>

* <span data-ttu-id="5ca97-123">이 작업을 수행하면 해당 서버에서 추가 데이터 수집이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-123">This action stops collecting any further data from that server.</span></span> <span data-ttu-id="5ca97-124">모니터링 서비스에서 이 서버가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-124">This server is removed from the monitoring service.</span></span> <span data-ttu-id="5ca97-125">이 작업을 수행한 후에는 이 서버에 대한 새 경고나 모니터링 데이터, 사용 현황 분석 데이터를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-125">After this action, you are not able to view new alerts, monitoring, or usage analytics data for this server.</span></span>
* <span data-ttu-id="5ca97-126">이 작업을 수행해도 서버에서 Health Agent가 제거되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-126">This action does not uninstall the Health Agent from your server.</span></span> <span data-ttu-id="5ca97-127">이 단계를 수행하기 전에 Health Agent를 제거하지 않은 경우 서버의 Health Agent와 관련된 오류가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-127">If you have not uninstalled the Health Agent before performing this step, you might see errors related to the Health Agent on the server.</span></span>
* <span data-ttu-id="5ca97-128">이 작업을 수행해도 이 서버에서 이미 수집된 데이터는 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-128">This action does not delete the data already collected from this server.</span></span> <span data-ttu-id="5ca97-129">해당 데이터는 Azure 데이터 보존 정책에 따라 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-129">That data is deleted in accordance with the Azure data retention policy.</span></span>
* <span data-ttu-id="5ca97-130">이 작업을 수행한 후 동일한 서버를 다시 모니터링하려는 경우 이 서버에서 Health Agent를 제거한 후 다시 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-130">After performing this action, if you want to start monitoring the same server again, you must uninstall and reinstall the Health Agent on this server.</span></span>

### <a name="to-delete-a-server-from-the-azure-ad-connect-health-service"></a><span data-ttu-id="5ca97-131">Azure AD Connect Health 서비스에서 서버를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="5ca97-131">To delete a server from the Azure AD Connect Health service</span></span>
<span data-ttu-id="5ca97-132">AD FS(Active Directory Federation Services)용 Azure AD Connect Health 및 Azure AD Connect(동기화):</span><span class="sxs-lookup"><span data-stu-id="5ca97-132">Azure AD Connect Health for Active Directory Federation Services (AD FS) and Azure AD Connect (Sync):</span></span>

1. <span data-ttu-id="5ca97-133">**서버 목록** 블레이드에서 제거할 서버 이름을 선택하여 **서버** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-133">Open the **Server** blade from the **Server List** blade by selecting the server name to be removed.</span></span>
2. <span data-ttu-id="5ca97-134">**서버** 블레이드의 작업 모음에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-134">On the **Server** blade, from the action bar, click **Delete**.</span></span>
3. <span data-ttu-id="5ca97-135">확인 상자에 서버 이름을 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-135">Confirm by typing the server name in the confirmation box.</span></span>
4. <span data-ttu-id="5ca97-136">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-136">Click **Delete**.</span></span>

<span data-ttu-id="5ca97-137">Azure Active Directory Domain Services용 Azure AD Connect Health:</span><span class="sxs-lookup"><span data-stu-id="5ca97-137">Azure AD Connect Health for Azure Active Directory Domain Services:</span></span>

1. <span data-ttu-id="5ca97-138">**도메인 컨트롤러** 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-138">Open the **Domain Controllers** dashboard.</span></span>
2. <span data-ttu-id="5ca97-139">제거할 도메인 컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-139">Select the domain controller to be removed.</span></span>
3. <span data-ttu-id="5ca97-140">작업 모음에서 **선택한 항목 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-140">From the action bar, click **Delete Selected**.</span></span>
4. <span data-ttu-id="5ca97-141">서버 삭제 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-141">Confirm the action to delete the server.</span></span>
5. <span data-ttu-id="5ca97-142">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-142">Click **Delete**.</span></span>

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a><span data-ttu-id="5ca97-143">Azure AD Connect Health 서비스에서 서비스 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="5ca97-143">Delete a service instance from Azure AD Connect Health service</span></span>
<span data-ttu-id="5ca97-144">서비스 인스턴스를 제거하려는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-144">In some instances, you might want to remove a service instance.</span></span> <span data-ttu-id="5ca97-145">Azure AD Connect Health 서비스에서 서비스 인스턴스를 제거하기 위해 알아야 할 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-145">Here's what you need to know to remove a service instance from the Azure AD Connect Health service.</span></span>

<span data-ttu-id="5ca97-146">서비스 인스턴스를 삭제하는 경우 다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="5ca97-146">When you're deleting a service instance, be aware of the following:</span></span>

* <span data-ttu-id="5ca97-147">이 작업을 수행하면 현재 서비스 인스턴스가 모니터링 서비스에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-147">This action removes the current service instance from the monitoring service.</span></span>
* <span data-ttu-id="5ca97-148">이 작업을 수행해도 이 서비스 인스턴스의 일부로 모니터링된 서버에서 Health Agent가 제거되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-148">This action does not uninstall or remove the Health Agent from any of the servers that were monitored as part of this service instance.</span></span> <span data-ttu-id="5ca97-149">이 단계를 수행하기 전에 Health Agent를 제거하지 않은 경우 서버의 Health Agent와 관련된 오류가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-149">If you have not uninstalled the Health Agent before performing this step, you might see errors related to the Health Agent on the servers.</span></span>
* <span data-ttu-id="5ca97-150">이 서비스 인스턴스의 모든 데이터는 Azure 데이터 보존 정책에 따라 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-150">All data from this service instance is deleted in accordance with the Azure data retention policy.</span></span>
* <span data-ttu-id="5ca97-151">이 작업을 수행한 후 서비스를 모니터링하려는 경우 모든 서버에서 Health Agent를 제거한 후 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-151">After performing this action, if you want to start monitoring the service, uninstall and reinstall the Health Agent on all the servers.</span></span> <span data-ttu-id="5ca97-152">이 작업을 수행한 후 동일한 서버를 다시 모니터링하려는 경우 해당 서버에서 Health Agent를 제거한 후 다시 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-152">After performing this action, if you want to start monitoring the same server again, uninstall, reinstall, and register the Health Agent on that server.</span></span>

#### <a name="to-delete-a-service-instance-from-the-azure-ad-connect-health-service"></a><span data-ttu-id="5ca97-153">Azure AD Connect Health 서비스에서 서비스 인스턴스를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="5ca97-153">To delete a service instance from the Azure AD Connect Health service</span></span>
1. <span data-ttu-id="5ca97-154">**서비스 목록** 블레이드에서 제거하려는 서비스 식별자(팜 이름)를 선택하여 **서비스** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-154">Open the **Service** blade from the **Service List** blade by selecting the service identifier (farm name) that you want to remove.</span></span>
2. <span data-ttu-id="5ca97-155">**서버** 블레이드의 작업 모음에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-155">On the **Server** blade, from the action bar, click **Delete**.</span></span>
3. <span data-ttu-id="5ca97-156">확인 상자에 서비스 이름(예: sts.contoso.com)을 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-156">Confirm by typing the service name in the confirmation box (for example: sts.contoso.com).</span></span>
4. <span data-ttu-id="5ca97-157">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-157">Click **Delete**.</span></span>
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a><span data-ttu-id="5ca97-158">역할 기반 액세스 제어로 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="5ca97-158">Manage access with Role-Based Access Control</span></span>
<span data-ttu-id="5ca97-159">Azure AD Connect Health에 대한 [RBAC(역할 기반 액세스 제어)](../role-based-access-control-configure.md)는 전역 관리자 이외의 사용자 및 그룹에 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-159">[Role-Based Access Control (RBAC)](../role-based-access-control-configure.md) for Azure AD Connect Health provides access to users and groups other than global administrators.</span></span> <span data-ttu-id="5ca97-160">RBAC는 의도한 사용자 및 그룹에 역할을 할당하고 디렉터리 내의 전역 관리자를 제한하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-160">RBAC assigns roles to the intended users and groups, and provides a mechanism to limit the global administrators within your directory.</span></span>

### <a name="roles"></a><span data-ttu-id="5ca97-161">역할</span><span class="sxs-lookup"><span data-stu-id="5ca97-161">Roles</span></span>
<span data-ttu-id="5ca97-162">Azure AD Connect Health는 다음과 같은 기본 제공 역할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-162">Azure AD Connect Health supports the following built-in roles:</span></span>

| <span data-ttu-id="5ca97-163">역할</span><span class="sxs-lookup"><span data-stu-id="5ca97-163">Role</span></span> | <span data-ttu-id="5ca97-164">권한</span><span class="sxs-lookup"><span data-stu-id="5ca97-164">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="5ca97-165">소유자</span><span class="sxs-lookup"><span data-stu-id="5ca97-165">Owner</span></span> |<span data-ttu-id="5ca97-166">소유자는 *액세스를 관리*(예: 사용자 또는 그룹에 역할 할당)하고, 포털에서 *모든 정보를 확인*(예: 경고 보기)하며, Azure AD Connect Health 내에서 *설정을 변경*(예: 메일 알림)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-166">Owners can *manage access* (for example, assign a role to a user or group), *view all information* (for example, view alerts) from the portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> <br><span data-ttu-id="5ca97-167">기본적으로 Azure AD 전역 관리자에게 이 역할이 할당되며, 이 설정은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-167">By default, Azure AD global administrators are assigned this role, and this cannot be changed.</span></span> |
| <span data-ttu-id="5ca97-168">참여자</span><span class="sxs-lookup"><span data-stu-id="5ca97-168">Contributor</span></span> |<span data-ttu-id="5ca97-169">참가자는 포털에서 *모든 정보를 확인*(예: 경고 보기)하고, Azure AD Connect Health 내에서 *설정을 변경*(예: 메일 알림)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-169">Contributors can *view all information* (for example, view alerts) from the portal, and *change settings* (for example, email notifications) within Azure AD Connect Health.</span></span> |
| <span data-ttu-id="5ca97-170">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="5ca97-170">Reader</span></span> |<span data-ttu-id="5ca97-171">구독자는 Azure AD Connect Health 내의 포털에서 *모든 정보를 확인*(예: 경고 보기)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-171">Readers can *view all information* (for example, view alerts) from the portal within Azure AD Connect Health.</span></span> |

<span data-ttu-id="5ca97-172">다른 모든 역할(예: 사용자 액세스 관리자 또는 DevTest 랩 사용자)은 포털 환경에서 사용할 수 있는 경우에도 Azure AD Connect Health 내의 액세스 권한에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-172">All other roles (such as User Access Administrators or DevTest Labs Users) have no impact to access within Azure AD Connect Health, even if the roles are available in the portal experience.</span></span>

### <a name="access-scope"></a><span data-ttu-id="5ca97-173">액세스 범위</span><span class="sxs-lookup"><span data-stu-id="5ca97-173">Access scope</span></span>
<span data-ttu-id="5ca97-174">Azure AD Connect Health는 다음 두 수준에서 액세스 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-174">Azure AD Connect Health supports managing access at two levels:</span></span>

* <span data-ttu-id="5ca97-175">**모든 서비스 인스턴스**: 대부분의 경우에서 권장되는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-175">**All service instances**: This is the recommended path in most cases.</span></span> <span data-ttu-id="5ca97-176">Azure AD Connect Health에서 모니터링되는 모든 역할 유형에서 모든 서비스 인스턴스(예: AD FS 팜)에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-176">It controls access for all service instances (for example, an AD FS farm) across all role types that are being monitored by Azure AD Connect Health.</span></span>
* <span data-ttu-id="5ca97-177">**서비스 인스턴스**: 역할 유형에 따라 또는 서비스 인스턴스별로 액세스를 분리해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-177">**Service instance**: In some cases, you might need to segregate access based on role types or by a service instance.</span></span> <span data-ttu-id="5ca97-178">이 경우 서비스 인스턴스 수준에서 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-178">In this case, you can manage access at the service instance level.</span></span>  

<span data-ttu-id="5ca97-179">사용 권한은 최종 사용자가 디렉터리 또는 서비스 인스턴스 수준에서 액세스 권한을 가진 경우에 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-179">Permission is granted if an end user has access either at the directory or service instance level.</span></span>

### <a name="allow-users-or-groups-access-to-azure-ad-connect-health"></a><span data-ttu-id="5ca97-180">사용자 또는 그룹에 Azure AD Connect Health에 대한 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="5ca97-180">Allow users or groups access to Azure AD Connect Health</span></span>
<span data-ttu-id="5ca97-181">다음 단계에서는 액세스를 허용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-181">The following steps show how to allow access.</span></span>
#### <a name="step-1-select-the-appropriate-access-scope"></a><span data-ttu-id="5ca97-182">1단계: 적절한 액세스 범위 선택</span><span class="sxs-lookup"><span data-stu-id="5ca97-182">Step 1: Select the appropriate access scope</span></span>
<span data-ttu-id="5ca97-183">Azure AD Connect Health 내에서 *모든 서비스 인스턴스* 수준으로 사용자에게 액세스를 허용하려면 Azure AD Connect Health에서 주 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-183">To allow a user access at the *all service instances* level within Azure AD Connect Health, open the main blade in Azure AD Connect Health.</span></span><br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a><span data-ttu-id="5ca97-184">2단계: 사용자 및 그룹 추가, 역할 할당</span><span class="sxs-lookup"><span data-stu-id="5ca97-184">Step 2: Add users and groups, and assign roles</span></span>
1. <span data-ttu-id="5ca97-185">**구성** 섹션에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-185">From the **Configure** section, click **Users**.</span></span><br><span data-ttu-id="5ca97-186">
   ![사용자가 강조 표시된 Azure AD Connect Health RBAC 주 블레이드 스크린샷](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span><span class="sxs-lookup"><span data-stu-id="5ca97-186">
![Screenshot of Azure AD Connect Health RBAC main blade, with Users highlighted](./media/active-directory-aadconnect-health/RBAC_main_blade.png)</span></span>
2. <span data-ttu-id="5ca97-187">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-187">Select **Add**.</span></span>
3. <span data-ttu-id="5ca97-188">**역할 선택** 창에서 역할(예: **소유자**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-188">In the **Select a role** pane, select a role (for example, **Owner**).</span></span><br><span data-ttu-id="5ca97-189">
   ![Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_add.png)</span><span class="sxs-lookup"><span data-stu-id="5ca97-189">
![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_add.png)</span></span>
4. <span data-ttu-id="5ca97-190">사용자 또는 그룹을 대상으로 한 이름 또는 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-190">Type the name or identifier of the targeted user or group.</span></span> <span data-ttu-id="5ca97-191">동시에 하나 이상의 사용자 또는 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-191">You can select one or more users or groups at the same time.</span></span> <span data-ttu-id="5ca97-192">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-192">Click **Select**.</span></span>
   <span data-ttu-id="5ca97-193">![Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span><span class="sxs-lookup"><span data-stu-id="5ca97-193">![Screenshot of Azure AD Connect Health RBAC Users window](./media/active-directory-aadconnect-health/RBAC_select_users.png)</span></span>
5. <span data-ttu-id="5ca97-194">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-194">Select **OK**.</span></span><br>
6. <span data-ttu-id="5ca97-195">역할 할당이 완료되면 사용자 및 그룹이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-195">After the role assignment is complete, the users and groups appear in the list.</span></span><br><span data-ttu-id="5ca97-196">
   ![새 사용자가 강조 표시된 Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span><span class="sxs-lookup"><span data-stu-id="5ca97-196">
![Screenshot of Azure AD Connect Health RBAC Users window, with new users highlighted](./media/active-directory-aadconnect-health/RBAC_user_list.png)</span></span>

<span data-ttu-id="5ca97-197">이제 할당된 역할에 따라 나열된 사용자 및 그룹에 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-197">Now the listed users and groups have access, according to their assigned roles.</span></span>

> [!NOTE]
> * <span data-ttu-id="5ca97-198">전역 관리자는 항상 모든 작업에 대한 모든 권한을 갖지만 전역 권리자 계정은 앞의 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-198">Global administrators always have full access to all the operations, but global administrator accounts are not present in the preceding list.</span></span>
> * <span data-ttu-id="5ca97-199">사용자 초대 기능은 Azure AD Connect Health 내에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-199">The Invite Users feature is not supported within Azure AD Connect Health.</span></span>
>
>

#### <a name="step-3-share-the-blade-location-with-users-or-groups"></a><span data-ttu-id="5ca97-200">3단계: 사용자 또는 그룹을 사용하여 블레이드 위치 공유</span><span class="sxs-lookup"><span data-stu-id="5ca97-200">Step 3: Share the blade location with users or groups</span></span>
1. <span data-ttu-id="5ca97-201">사용 권한을 할당하면 사용자가 [여기](http://aka.ms/aadconnecthealth)로 이동하여 Azure AD Connect Health에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-201">After you assign permissions, a user can access Azure AD Connect Health by going [here](http://aka.ms/aadconnecthealth).</span></span>
2. <span data-ttu-id="5ca97-202">블레이드에서 사용자는 블레이드 또는 블레이드의 서로 다른 부분을 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-202">On the blade, the user can pin the blade, or different parts of it, to the dashboard.</span></span> <span data-ttu-id="5ca97-203">**대시보드에 고정** 아이콘을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-203">Simply click the **Pin to dashboard** icon.</span></span><br><span data-ttu-id="5ca97-204">
   ![고정 아이콘이 강조 표시된 Azure AD Connect Health RBAC 고정 블레이드 스크린샷](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span><span class="sxs-lookup"><span data-stu-id="5ca97-204">
![Screenshot of Azure AD Connect Health RBAC pin blade, with pin icon highlighted](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)</span></span>

> [!NOTE]
> <span data-ttu-id="5ca97-205">구독자 역할이 할당된 사용자는 Azure Marketplace에서 Azure AD Connect Health 확장을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-205">A user with the Reader role assigned is not able to get Azure AD Connect Health extension from the Azure Marketplace.</span></span> <span data-ttu-id="5ca97-206">사용자가 가져오기에 필요한 "만들기" 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-206">The user cannot perform the necessary "create" operation to do so.</span></span> <span data-ttu-id="5ca97-207">사용자는 앞의 링크로 이동하여 블레이드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-207">The user can still get to the blade by going to the preceding link.</span></span> <span data-ttu-id="5ca97-208">이후 사용의 경우 사용자는 대시보드에 블레이드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-208">For subsequent usage, the user can pin the blade to the dashboard.</span></span>
>
>

### <a name="remove-users-or-groups"></a><span data-ttu-id="5ca97-209">사용자 또는 그룹 제거</span><span class="sxs-lookup"><span data-stu-id="5ca97-209">Remove users or groups</span></span>
<span data-ttu-id="5ca97-210">Azure AD Connect Health RBAC에 추가된 사용자 또는 그룹을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-210">You can remove a user or a group added to Azure AD Connect Health RBAC.</span></span> <span data-ttu-id="5ca97-211">사용자 또는 그룹을 마우스 오른쪽 단추로 클릭하고 **제거**를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca97-211">Simply right-click the user or group, and select **Remove**.</span></span><br><span data-ttu-id="5ca97-212">
![제거가 강조 표시된 Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_remove.png)</span><span class="sxs-lookup"><span data-stu-id="5ca97-212">
![Screenshot of Azure AD Connect Health RBAC Users window, with Remove highlighted](./media/active-directory-aadconnect-health/RBAC_remove.png)</span></span>

[//]: # (End of RBAC section)

## <a name="next-steps"></a><span data-ttu-id="5ca97-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ca97-213">Next steps</span></span>
* [<span data-ttu-id="5ca97-214">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5ca97-214">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="5ca97-215">Azure AD Connect Health 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="5ca97-215">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="5ca97-216">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="5ca97-216">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="5ca97-217">동기화에 대한 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="5ca97-217">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="5ca97-218">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="5ca97-218">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="5ca97-219">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="5ca97-219">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="5ca97-220">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="5ca97-220">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
