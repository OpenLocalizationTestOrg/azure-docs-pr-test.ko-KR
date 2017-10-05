---
title: "자습서: Box와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Box 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9f061f3f5a0a4825854b893150ceccc8951487de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="6d402-103">자습서: 자동 사용자 프로비전에 대한 Box 구성</span><span class="sxs-lookup"><span data-stu-id="6d402-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="6d402-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Box로 자동으로 프로비전 및 프로비전 해제하도록 Box 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d402-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d402-105">Prerequisites</span></span>

<span data-ttu-id="6d402-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="6d402-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="6d402-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="6d402-108">Box Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6d402-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="6d402-109">팀 관리자 권한이 있는 Box의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="6d402-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-to-box"></a><span data-ttu-id="6d402-110">Box에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6d402-110">Assigning users to Box</span></span> 

<span data-ttu-id="6d402-111">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="6d402-112">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="6d402-113">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Box 앱에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span></span> <span data-ttu-id="6d402-114">결정했으면 다음 지시에 따라 이러한 사용자를 Box 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-114">Once decided, you can assign these users to your Box app by following the instructions here:</span></span>

[<span data-ttu-id="6d402-115">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="6d402-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="6d402-116">사용자 및 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="6d402-116">Assign users and groups</span></span>
<span data-ttu-id="6d402-117">Azure Portal의 **Box > 사용자 및 그룹** 탭에서 Box에 대한 액세스 권한을 부여해야 하는 사용자 및 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-117">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="6d402-118">사용자 또는 그룹을 할당하면 다음과 같은 상황이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-118">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="6d402-119">Azure AD에서 할당된 사용자에게 Box에 인증하도록 허용합니다(직접 할당 또는 그룹 멤버 자격을 통해).</span><span class="sxs-lookup"><span data-stu-id="6d402-119">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="6d402-120">사용자가 할당되지 않은 경우에는 Azure AD에서 Box에 로그인하도록 허용하지 않으며 Azure AD 로그인 페이지에서 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-120">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="6d402-121">Box의 앱 타일이 사용자의 [응용 프로그램 시작 관리자](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-121">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="6d402-122">자동 프로비전이 설정된 경우 할당된 사용자 및/또는 그룹이 자동으로 프로비전되도록 프로비전 큐에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-122">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="6d402-123">사용자 개체만 프로비전되도록 구성된 경우 직접 할당된 모든 사용자가 프로비전 큐에 배치되며, 할당된 그룹의 멤버인 모든 사용자가 프로비전 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-123">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="6d402-124">그룹 개체가 프로비전되도록 구성된 경우 할당된 모든 그룹 개체 및 해당 그룹의 멤버인 모든 사용자가 Box에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-124">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="6d402-125">그룹 및 사용자 멤버 자격은 Box에 기록될 때 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-125">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="6d402-126">**특성 > Single Sign-On** 탭을 사용하여 SAML 기반 인증 중에 Box에 표시되는 사용자 특성(또는 클레임)을 구성하고, **특성 > 프로비전** 탭을 사용하여 프로비전 작업 중에 사용자 및 그룹 특성이 Azure AD에서 Box로 이동하는 방식을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-126">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-to-box"></a><span data-ttu-id="6d402-127">Box에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="6d402-127">Important tips for assigning users to Box</span></span> 

*   <span data-ttu-id="6d402-128">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Box에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-128">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span></span> <span data-ttu-id="6d402-129">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="6d402-130">Box에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-130">When assigning a user to box, you must select a valid user role.</span></span> <span data-ttu-id="6d402-131">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-131">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="6d402-132">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="6d402-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="6d402-133">이 섹션에서는 사용자의 Azure AD를 Box의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Box에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-133">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="6d402-134">자동 프로비전이 설정된 경우 할당된 사용자 및/또는 그룹이 자동으로 프로비전되도록 프로비전 큐에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-134">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
    
 * <span data-ttu-id="6d402-135">사용자 개체만 프로비전되도록 구성된 경우 직접 할당된 사용자가 프로비전 큐에 배치되며, 할당된 그룹의 멤버인 모든 사용자가 프로비전 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-135">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
    
 * <span data-ttu-id="6d402-136">그룹 개체가 프로비전되도록 구성된 경우 할당된 모든 그룹 개체 및 해당 그룹의 멤버인 모든 사용자가 Box에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-136">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="6d402-137">그룹 및 사용자 멤버 자격은 Box에 기록될 때 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-137">The group and user memberships are preserved upon being written to Box.</span></span>

> [!TIP] 
> <span data-ttu-id="6d402-138">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Box에 대해 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-138">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6d402-139">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="6d402-140">자동 사용자 계정 프로비전을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="6d402-140">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="6d402-141">이 섹션은 Box에 Active Directory 사용자 계정을 프로비전할 수 있도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-141">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

1. <span data-ttu-id="6d402-142">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-142">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="6d402-143">Single Sign-On에 대한 Box를 이미 구성한 경우 검색 필드를 사용하여 Box의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-143">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span></span> <span data-ttu-id="6d402-144">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Box**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-144">Otherwise, select **Add** and search for **Box** in the application gallery.</span></span> <span data-ttu-id="6d402-145">검색 결과에서 Box를 선택하고 응용 프로그램의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-145">Select Box from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="6d402-146">Box의 인스턴스를 선택한 다음, **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-146">Select your instance of Box, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="6d402-147">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-147">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="6d402-149">**관리자 자격 증명** 섹션 아래에서 **권한 부여**를 클릭하여 새 브라우저 창에서 Box 로그인 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-149">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="6d402-150">**Box에 대한 액세스 권한 부여를 위한 로그인** 페이지에서 필요한 자격 증명을 제공한 다음 **권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-150">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="6d402-151">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="6d402-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="6d402-152">**Box에 액세스 허용**을 클릭하여 이 작업에 권한을 부여하고 Azure Portal로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-152">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span></span> 
   
    <span data-ttu-id="6d402-153">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="6d402-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="6d402-154">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Box 앱에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-154">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span></span> <span data-ttu-id="6d402-155">연결에 실패하면 Box 계정에 팀 관리자 권한이 있는지 확인하고 **"권한 부여"** 단계를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-155">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="6d402-156">프로비전 오류 알림을 받을 개인 또는 그룹의 메일 주소를 **알림 메일** 필드에 입력하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-156">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="6d402-157">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-157">Click **Save.**</span></span>

11. <span data-ttu-id="6d402-158">[매핑] 섹션에서 **Azure Active Directory 사용자를 Box에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span></span>

12. <span data-ttu-id="6d402-159">**특성 매핑** 섹션에서 Azure AD에서 Box로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span></span> <span data-ttu-id="6d402-160">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Box의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-160">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span></span> <span data-ttu-id="6d402-161">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-161">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="6d402-162">Box에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 설정 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-162">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="6d402-163">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-163">Click **Save.**</span></span>

<span data-ttu-id="6d402-164">[사용자 및 그룹] 섹션에서 Box에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-164">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span></span> <span data-ttu-id="6d402-165">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-165">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="6d402-166">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Box 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Box app.</span></span>

<span data-ttu-id="6d402-167">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-167">You can now create a test account.</span></span> <span data-ttu-id="6d402-168">이제 최대 20분 동안 기다린 후 계정이 Box에 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-168">Wait for up to 20 minutes to verify that the account has been synchronized to box.</span></span>

<span data-ttu-id="6d402-169">Box 테넌트에서 동기화된 사용자가 **관리 콘솔**의 **관리된 사용자**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d402-169">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="6d402-170">![통합 상태](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "통합 상태")</span><span class="sxs-lookup"><span data-stu-id="6d402-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6d402-171">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6d402-171">Additional resources</span></span>

* [<span data-ttu-id="6d402-172">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="6d402-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d402-173">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6d402-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6d402-174">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6d402-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)