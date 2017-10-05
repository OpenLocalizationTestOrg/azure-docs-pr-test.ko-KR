---
title: "자습서: Concur와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Concur 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="584c9-103">자습서: 사용자 프로비전에 대한 Concur 구성</span><span class="sxs-lookup"><span data-stu-id="584c9-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="584c9-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Concur로 자동으로 프로비전 및 프로비전 해제하도록 Concur 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="584c9-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="584c9-105">Prerequisites</span></span>

<span data-ttu-id="584c9-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="584c9-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="584c9-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="584c9-108">Concur Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="584c9-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="584c9-109">팀 관리자 권한이 있는 Concur의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="584c9-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="584c9-110">Concur에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="584c9-110">Assigning users to Concur</span></span>

<span data-ttu-id="584c9-111">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="584c9-112">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 “할당된” 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="584c9-113">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Concur 앱에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="584c9-114">결정했으면 다음 지시에 따라 이러한 사용자를 Concur 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="584c9-115">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="584c9-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="584c9-116">Concur에 사용자 할당을 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="584c9-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="584c9-117">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Concur에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="584c9-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="584c9-119">Concur에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="584c9-120">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="584c9-121">사용자 프로비저닝 사용</span><span class="sxs-lookup"><span data-stu-id="584c9-121">Enable user provisioning</span></span>

<span data-ttu-id="584c9-122">이 섹션에서는 사용자의 Azure AD를 Concur의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Concur에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="584c9-123">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Concur에 대해 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="584c9-124">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="584c9-125">사용자 계정 프로비전을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="584c9-125">To configure user account provisioning:</span></span>

<span data-ttu-id="584c9-126">이 섹션은 Concur에 Active Directory 사용자 계정을 프로비전할 수 있도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="584c9-127">Expense Service에서 앱을 사용하도록 설정하려면 웹 서비스 관리자 프로필을 적절히 설치하고 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="584c9-128">T&E 관리 기능으로 사용하는 기존 관리자 프로필에 WS 관리자 역할을 추가하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="584c9-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="584c9-129">Concur 컨설턴트 또는 클라이언트 관리자는 고유한 웹 서비스 관리자 프로필을 만들어야 하고 클라이언트 관리자는 웹 서비스 관리자 기능에 해당 프로필을 사용해야 합니다(예: 앱 사용).</span><span class="sxs-lookup"><span data-stu-id="584c9-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="584c9-130">이러한 프로필은 클라이언트 관리자의 일별 T&E 관리자 프로필에서 별도로 유지되어야 합니다.(T&E 관리자 프로필에 할당된 WSAdmin 역할이 없어야 함)</span><span class="sxs-lookup"><span data-stu-id="584c9-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="584c9-131">앱을 사용하도록 설정하는 데 사용되는 프로필을 만드는 경우 사용자 프로필 필드에 클라이언트 관리자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="584c9-132">이렇게 하면 프로필에 소유권이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="584c9-133">하나 이상의 프로필이 만들어지면 클라이언트는 이 프로필로 로그인하여 [웹 서비스] 메뉴 내의 파트너 앱에 대해 “*사용*” 단추를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="584c9-134">다음과 같은 이유로 이 작업은 일반 T&E 관리에 사용하는 프로필을 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="584c9-135">앱을 사용하도록 설정한 후에 클라이언트가 표시되는 대화창에서 "*예*"를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="584c9-136">클릭함으로써 클라이언트는 파트너 응용 프로그램이 데이터에 액세스하도록 승인하므로 사용자나 파트너가 해당 예 단추를 클릭할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="584c9-137">T&E 관리자 프로필을 사용하여 앱을 사용하도록 설정한 클라이언트 관리자가 퇴사하면(비활성화된 프로필이 발생함) 앱이 다른 WS 관리자 프로필로 설정될 때까지 해당 프로필을 사용하도록 설정된 앱은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="584c9-138">이 때문에 고유한 WS 관리자 프로필을 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="584c9-139">관리자가 퇴사하면 프로필이 비활성화되지 않아도 되기 때문에 활성화된 앱에 영향을 주지 않으면서도 원하는 경우 WS 관리자 프로필로 연결된 이름을 대체 관리자로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="584c9-140">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="584c9-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="584c9-141">**Concur** 테넌트에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="584c9-142">**관리** 메뉴에서 **웹 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="584c9-143">![Concur 테넌트](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur 테넌트")</span><span class="sxs-lookup"><span data-stu-id="584c9-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="584c9-144">왼쪽의 **웹 서비스** 창에서 **파트너 응용 프로그램 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="584c9-145">![파트너 응용 프로그램 사용](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "파트너 응용 프로그램 사용")</span><span class="sxs-lookup"><span data-stu-id="584c9-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="584c9-146">**응용 프로그램 사용** 목록에서 **Azure Active Directory**를 선택하고 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="584c9-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="584c9-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="584c9-148">**예**를 클릭하여 **동작 확인** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="584c9-149">![동작 확인](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "동작 확인")</span><span class="sxs-lookup"><span data-stu-id="584c9-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="584c9-150">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="584c9-151">Single Sign-On에 대한 Concur를 이미 구성한 경우 검색 필드를 사용하여 Concur의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="584c9-152">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Concur**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="584c9-153">검색 결과에서 Concur를 선택하고 응용 프로그램의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="584c9-154">Concur의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="584c9-155">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![프로비전](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="584c9-157">**관리자 자격 증명** 섹션에서 Concur 관리자의 **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="584c9-158">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Concur 앱에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="584c9-159">연결에 실패하면 Concur 계정에 팀 관리자 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="584c9-160">프로비전 오류 알림을 받을 개인 또는 그룹의 메일 주소를 **알림 메일** 필드에 입력하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="584c9-161">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-161">Click **Save.**</span></span>

14. <span data-ttu-id="584c9-162">매핑 섹션에서 **Azure Active Directory 사용자를 Concur에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="584c9-163">**특성 매핑** 섹션에서 Azure AD에서 Concur로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="584c9-164">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Concur의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="584c9-165">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="584c9-166">Concur에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="584c9-167">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-167">Click **Save.**</span></span>

<span data-ttu-id="584c9-168">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-168">You can now create a test account.</span></span> <span data-ttu-id="584c9-169">이제 최대 20분 동안 기다린 후 계정이 Concur에 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="584c9-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="584c9-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="584c9-170">Additional resources</span></span>

* [<span data-ttu-id="584c9-171">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="584c9-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="584c9-172">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="584c9-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="584c9-173">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="584c9-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

