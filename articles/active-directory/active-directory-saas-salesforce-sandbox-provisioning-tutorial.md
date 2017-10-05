---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Salesforce Sandbox 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 7d3c655a754f83284c386d2007c604a731367814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a><span data-ttu-id="2269a-103">자습서: 자동 사용자 프로비전에 대한 Salesforce Sandbox 구성</span><span class="sxs-lookup"><span data-stu-id="2269a-103">Tutorial: Configuring Salesforce Sandbox for Automatic User Provisioning</span></span>

<span data-ttu-id="2269a-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Salesforce Sandbox으로 자동 프로비전 및 프로비전 해제하도록 Salesforce Sandbox 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-104">The objective of this tutorial is to show you the steps you need to perform in Salesforce Sandbox and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce Sandbox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2269a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2269a-105">Prerequisites</span></span>

<span data-ttu-id="2269a-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="2269a-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="2269a-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="2269a-108">Salesforce Sandbox for Work 또는 Salesforce Sandbox for Education에 대한 유효한 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-108">You must have a valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span></span> <span data-ttu-id="2269a-109">어느 서비스에나 평가판 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="2269a-110">팀 관리자 권한이 있는 Salesforce Sandbox의 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="2269a-110">A user account in Salesforce Sandbox with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="2269a-111">Salesforce Sandbox에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2269a-111">Assigning users to Salesforce Sandbox</span></span>

<span data-ttu-id="2269a-112">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="2269a-113">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="2269a-114">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Salesforce Sandbox 앱에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce Sandbox app.</span></span> <span data-ttu-id="2269a-115">결정했으면 다음 지시에 따라 이러한 사용자를 Salesforce Sandbox 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-115">Once decided, you can assign these users to your Salesforce Sandbox app by following the instructions here:</span></span>

[<span data-ttu-id="2269a-116">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="2269a-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="2269a-117">Salesforce Sandbox에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="2269a-117">Important tips for assigning users to Salesforce Sandbox</span></span>

* <span data-ttu-id="2269a-118">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Salesforce Sandbox에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-118">It is recommended that a single Azure AD user is assigned to Salesforce Sandbox to test the provisioning configuration.</span></span> <span data-ttu-id="2269a-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-119">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="2269a-120">Salesforce Sandbox에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-120">When assigning a user to Salesforce Sandbox, you must select a valid user role.</span></span> <span data-ttu-id="2269a-121">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-121">The "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="2269a-122">이 앱은 프로비전 프로세스에서 Salesforce Sandbox의 사용자 지정 역할을 가져오며, 고객이 사용자를 할당할 때 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-122">This app imports custom roles from Salesforce Sandbox as part of the provisioning process, which the customer may want to select when assigning users.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="2269a-123">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="2269a-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="2269a-124">이 섹션에서는 사용자의 Azure AD를 Salesforce Sandbox의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Salesforce Sandbox에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-124">This section guides you through connecting your Azure AD to Salesforce Sandbox's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="2269a-125">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Salesforce Sandbox에 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce Sandbox, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2269a-126">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="2269a-127">자동 사용자 계정 프로비전을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="2269a-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="2269a-128">이 섹션은 Salesforce Sandbox에 Active Directory 사용자 계정을 사용자 프로비저닝할 수 있도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

1. <span data-ttu-id="2269a-129">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="2269a-130">이미 Salesforce Sandbox에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Salesforce Sandbox의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-130">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using the search field.</span></span> <span data-ttu-id="2269a-131">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Salesforce Sandbox**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-131">Otherwise, select **Add** and search for **Salesforce Sandbox** in the application gallery.</span></span> <span data-ttu-id="2269a-132">검색 결과에서 Salesforce Sandbox를 선택하고 응용 프로그램 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-132">Select Salesforce Sandbox from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="2269a-133">Salesforce Sandbox의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-133">Select your instance of Salesforce Sandbox, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="2269a-134">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
    <span data-ttu-id="2269a-135">![프로비전](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="2269a-135">![provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="2269a-136">**관리자 자격 증명** 섹션에서 다음 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="2269a-137">a.</span><span class="sxs-lookup"><span data-stu-id="2269a-137">a.</span></span> <span data-ttu-id="2269a-138">**관리 사용자 이름** 텍스트 상자에 Salesforce.com의 **시스템 관리자** 프로필이 할당된 Salesforce Sandbox 계정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-138">In the **Admin User Name** textbox, type a Salesforce Sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="2269a-139">b.</span><span class="sxs-lookup"><span data-stu-id="2269a-139">b.</span></span> <span data-ttu-id="2269a-140">**관리자 암호** 텍스트 상자에 이 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="2269a-141">Salesforce Sandbox 보안 토큰을 얻으려면 새 탭을 열고 동일한 Salesforce Sandbox 관리자 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-141">To get your Salesforce Sandbox security token, open a new tab and sign into the same Salesforce Sandbox admin account.</span></span> <span data-ttu-id="2269a-142">페이지의 오른쪽 위 모서리에 있는 사용자 이름을 클릭하고 **내 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="2269a-143">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="2269a-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="2269a-144">왼쪽 탐색 창에서 **개인**을 클릭하여 관련된 섹션을 확장한 다음 **내 보안 토큰 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="2269a-145">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="2269a-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="2269a-146">**내 보안 토큰 재설정** 페이지에서 **보안 토큰 재설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-146">On the **Reset My Security Token** page, click the **Reset Security Token** button.</span></span>

    <span data-ttu-id="2269a-147">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="2269a-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="2269a-148">이 관리자 계정과 연결된 전자 메일 받은 편지함을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="2269a-149">Salesforce Sandbox.com에서 새 보안 토큰이 포함된 이메일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-149">Look for an email from Salesforce Sandbox.com that contains the new security token.</span></span>
10. <span data-ttu-id="2269a-150">토큰을 복사하고 Azure AD 창으로 이동하여 **소켓 토큰** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="2269a-151">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Salesforce Sandbox 앱에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce Sandbox app.</span></span>

12. <span data-ttu-id="2269a-152">프로비전 오류 알림을 받을 개인 또는 그룹의 이메일 주소를 **알림 메일** 필드에 입력하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

13. <span data-ttu-id="2269a-153">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="2269a-154">매핑 섹션에서 **Azure Active Directory 사용자를 Salesforce Sandbox에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce Sandbox.**</span></span>

15. <span data-ttu-id="2269a-155">**특성 매핑** 섹션에서 Azure AD에서 Salesforce Sandbox로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce Sandbox.</span></span> <span data-ttu-id="2269a-156">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Salesforce Sandbox의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-156">The attributes selected as **Matching** properties are used to match the user accounts in Salesforce Sandbox for update operations.</span></span> <span data-ttu-id="2269a-157">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="2269a-158">Salesforce Sandbox에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 설정 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-158">To enable the Azure AD provisioning service for Salesforce Sandbox, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="2269a-159">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-159">Click **Save.**</span></span>


<span data-ttu-id="2269a-160">사용자 및 그룹 섹션에서 Salesforce Sandbox에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-160">It starts the initial synchronization of any users and/or groups assigned to Salesforce Sandbox in the Users and Groups section.</span></span> <span data-ttu-id="2269a-161">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-161">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="2269a-162">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Salesforce Sandbox 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on Salesforce Sandbox app.</span></span>

<span data-ttu-id="2269a-163">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-163">You can now create a test account.</span></span> <span data-ttu-id="2269a-164">이제 최대 20분 동안 기다린 후 계정이 Salesforce에 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2269a-164">Wait for up to 20 minutes to verify that the account has been synchronized to salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2269a-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2269a-165">Additional resources</span></span>

* [<span data-ttu-id="2269a-166">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="2269a-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2269a-167">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2269a-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2269a-168">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2269a-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforcesandbox-tutorial.md)