---
title: "자습서: Salesforce와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Salesforce 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a573a7ef79e28c50ae0923849a88f88af40f21be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="af96b-103">자습서: 자동 사용자 프로비전에 대한 Salesforce 구성</span><span class="sxs-lookup"><span data-stu-id="af96b-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="af96b-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Salesforce로 자동 프로비전 및 프로비전 해제하도록 Salesforce 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af96b-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="af96b-105">Prerequisites</span></span>

<span data-ttu-id="af96b-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="af96b-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="af96b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="af96b-108">Salesforce for Work 또는 Salesforce for Education에 대한 유효한 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="af96b-109">어느 서비스에나 평가판 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="af96b-110">팀 관리자 권한이 있는 Salesforce의 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="af96b-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="af96b-111">Salesforce에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="af96b-111">Assigning users to Salesforce</span></span>

<span data-ttu-id="af96b-112">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="af96b-113">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="af96b-114">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Salesforce 앱에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce app.</span></span> <span data-ttu-id="af96b-115">결정했으면 다음 지시에 따라 이러한 사용자를 Salesforce 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-115">Once decided, you can assign these users to your Salesforce app by following the instructions here:</span></span>

[<span data-ttu-id="af96b-116">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="af96b-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="af96b-117">Salesforce에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="af96b-117">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="af96b-118">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Salesforce에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-118">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="af96b-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="af96b-120">Salesforce에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-120">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="af96b-121">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-121">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="af96b-122">이 앱은 프로비전 프로세스에서 Salesforce의 사용자 지정 역할을 가져오며, 고객이 사용자를 할당할 때 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-122">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="af96b-123">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="af96b-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="af96b-124">이 섹션에서는 사용자의 Azure AD를 Salesforce의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Salesforce에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-124">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="af96b-125">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Salesforce에 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="af96b-126">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="af96b-127">자동 사용자 계정 프로비전을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="af96b-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="af96b-128">이 섹션은 Salesforce에 Active Directory 사용자 계정을 사용자 프로비전할 수 있도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="af96b-129">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="af96b-130">이미 Salesforce에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Salesforce의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="af96b-131">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Salesforce**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-131">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="af96b-132">검색 결과에서 Salesforce를 선택하고 응용 프로그램 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-132">Select Salesforce from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="af96b-133">Salesforce의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-133">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="af96b-134">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
<span data-ttu-id="af96b-135">![프로비전](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="af96b-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="af96b-136">**관리자 자격 증명** 섹션에서 다음 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="af96b-137">a.</span><span class="sxs-lookup"><span data-stu-id="af96b-137">a.</span></span> <span data-ttu-id="af96b-138">**관리 사용자 이름** 텍스트 상자에 Salesforce.com의 **시스템 관리자** 프로필이 할당된 Salesforce 계정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-138">In the **Admin User Name** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="af96b-139">b.</span><span class="sxs-lookup"><span data-stu-id="af96b-139">b.</span></span> <span data-ttu-id="af96b-140">**관리자 암호** 텍스트 상자에 이 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="af96b-141">Salesforce 보안 토큰을 얻으려면 새 탭을 열고 동일한 Salesforce 관리자 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-141">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="af96b-142">페이지의 오른쪽 위 모서리에 있는 사용자 이름을 클릭하고 **내 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="af96b-143">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="af96b-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="af96b-144">왼쪽 탐색 창에서 **개인**을 클릭하여 관련된 섹션을 확장한 다음 **내 보안 토큰 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="af96b-145">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="af96b-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="af96b-146">**내 보안 토큰 재설정** 페이지에서 **보안 토큰 재설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-146">On the **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="af96b-147">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="af96b-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="af96b-148">이 관리자 계정과 연결된 전자 메일 받은 편지함을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="af96b-149">Salesforce.com에서 새 보안 토큰이 포함된 전자 메일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-149">Look for an email from Salesforce.com that contains the new security token.</span></span>
10. <span data-ttu-id="af96b-150">토큰을 복사하고 Azure AD 창으로 이동하여 **소켓 토큰** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="af96b-151">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Salesforce 앱에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

12. <span data-ttu-id="af96b-152">프로비전 오류 알림을 받을 개인 또는 그룹의 이메일 주소를 **알림 메일** 필드에 입력하고 아래의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

13. <span data-ttu-id="af96b-153">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="af96b-154">매핑 섹션에서 **Azure Active Directory 사용자를 Salesforce에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

15. <span data-ttu-id="af96b-155">**특성 매핑** 섹션에서 Azure AD에서 Salesforce로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="af96b-156">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Salesforce의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-156">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="af96b-157">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="af96b-158">Salesforce에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 설정 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-158">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="af96b-159">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-159">Click **Save.**</span></span>

<span data-ttu-id="af96b-160">사용자 및 그룹 섹션에서 Salesforce에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-160">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="af96b-161">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-161">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="af96b-162">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Salesforce 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="af96b-163">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-163">You can now create a test account.</span></span> <span data-ttu-id="af96b-164">이제 최대 20분 동안 기다린 후 계정이 Salesforce에 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af96b-164">Wait for up to 20 minutes to verify that the account has been synchronized to Salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af96b-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="af96b-165">Additional resources</span></span>

* [<span data-ttu-id="af96b-166">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="af96b-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af96b-167">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="af96b-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="af96b-168">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="af96b-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)