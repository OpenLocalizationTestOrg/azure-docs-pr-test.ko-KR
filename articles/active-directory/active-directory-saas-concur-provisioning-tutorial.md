---
title: "자습서: Concur와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Concur 사이의 합니다."
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
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="f1411-103">자습서: 사용자 프로비전에 대한 Concur 구성</span><span class="sxs-lookup"><span data-stu-id="f1411-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="f1411-104">hello이이 자습서의 단계에서 Azure AD 및 Concur tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooConcur tooperform 필요한 hello tooshow가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1411-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f1411-105">Prerequisites</span></span>

<span data-ttu-id="f1411-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="f1411-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="f1411-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="f1411-108">Concur Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f1411-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="f1411-109">팀 관리자 권한이 있는 Concur의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="f1411-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="f1411-110">사용자가 tooConcur 할당</span><span class="sxs-lookup"><span data-stu-id="f1411-110">Assigning users tooConcur</span></span>

<span data-ttu-id="f1411-111">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="f1411-112">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="f1411-113">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour Concur 응용 프로그램에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="f1411-114">결정, 여기 hello 지침에 따라 이러한 사용자 tooyour Concur 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="f1411-115">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="f1411-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="f1411-116">사용자가 tooConcur 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="f1411-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="f1411-117">것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooConcur tootest hello를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="f1411-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f1411-119">사용자 tooConcur에 할당할 때 유효한 사용자 역할을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="f1411-120">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="f1411-121">사용자 프로비저닝 사용</span><span class="sxs-lookup"><span data-stu-id="f1411-121">Enable user provisioning</span></span>

<span data-ttu-id="f1411-122">이 섹션 API를 프로 비전 하는 Azure AD tooConcur의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 hello 서비스 toocreate 프로 비전, 구성 및 Azure AD에서 사용자 및 그룹 할당에 따라 Concur에서 할당 된 사용자 계정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="f1411-123">에 제공 된 hello 지침에 따라 Concur에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f1411-124">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="f1411-125">tooconfigure 사용자 계정 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="f1411-126">이 섹션의 hello 목적은 toooutline 어떻게 tooConcur를 계정 tooenable Active Directory 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="f1411-127">tooenable 응용 프로그램 비용 서비스 hello는 웹 서비스 관리자 프로필의 toobe 적절 한 설정 및 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="f1411-128">Hello WS Admin 역할 tooyour 기존 관리자 프로필을 사용 하면 t&e 관리 기능에 대 한 추가 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="f1411-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="f1411-129">Concur 컨설턴트 또는 클라이언트 관리자에 게 고유한 웹 서비스 관리자 프로필을 만들어야 하 고 hello 웹 서비스 관리자 기능 (예를 들어 사용할 수 있도록 앱)에 대 한 클라이언트 관리자에 게가이 프로필을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="f1411-130">이러한 프로필 hello 클라이언트 관리자의 일별 t&e 관리자 프로필과 별도로 유지 해야 합니다 (T hello 및 E 관리자 프로필과 없어야 hello WSAdmin 역할이 할당 된).</span><span class="sxs-lookup"><span data-stu-id="f1411-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="f1411-131">Hello 앱을 사용 하도록 설정에 사용 되는 hello 프로필 toobe를 만들 때 hello 사용자 프로필 필드에 hello 클라이언트 관리자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="f1411-132">소유권 toohello 프로필을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="f1411-133">이 프로필 tooclick hello 만들어지면 클라이언트 hello 하나 이상의 프로필을 만든 후 "*사용*" hello 웹 서비스 메뉴 내의 파트너 앱에 대 한 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="f1411-134">다음 이유로 hello에 대 한이 작업 hello 프로필 일반 t&e 관리에 사용 하면 안 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="f1411-135">hello 클라이언트에 하나 클릭 하는 hello toobe "*예*" 응용 프로그램을 사용 하도록 설정한 후 표시 되는 hello 대화 상자 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="f1411-136">이 승인 hello 클라이언트는 의향이 파트너 응용 프로그램 tooaccess hello에 대 한 데이터를 하므로 또는 hello 파트너가 예 단추를 클릭할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="f1411-137">다른 활성 WS 관리자와 hello 앱 사용 될 때까지 해당 프로필을 사용 하 여 설정 앱 T hello 및 E 관리자 프로필을 사용 하 여 앱 사용 하도록 설정한 클라이언트 관리자가 hello 회사 (비활성화 된 hello 프로필 발생 함)를 완료 하는 경우 작동 하지 않습니다. 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="f1411-138">이 때문에 고유한 WS 관리자 프로필 toocreate 해야 한다 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="f1411-139">관리자가 hello 회사, toohello 응용 프로그램 프로필이 필요 하지 않습니다 비활성화 사용 하도록 설정 하는 hello 영향을 주지 않고 원하는 경우 WS 관리자 프로필 변경 된 toohello 대체 관리자 수를 연결 하는 hello 이름.</span><span class="sxs-lookup"><span data-stu-id="f1411-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="f1411-140">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="f1411-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1411-141">Tooyour 로그온 **Concur** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="f1411-142">Hello에서 **관리** 메뉴 선택 **웹 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="f1411-143">![Concur 테넌트](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur 테넌트")</span><span class="sxs-lookup"><span data-stu-id="f1411-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="f1411-144">왼쪽, hello에서 hello에 **웹 서비스** 창 선택 **파트너 응용 프로그램 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="f1411-145">![파트너 응용 프로그램 사용](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "파트너 응용 프로그램 사용")</span><span class="sxs-lookup"><span data-stu-id="f1411-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="f1411-146">Hello에서 **응용 프로그램 사용** 목록에서 **Azure Active Directory**, 클릭 하 고 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="f1411-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f1411-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="f1411-148">클릭 **예** tooclose hello **동작 확인** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f1411-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="f1411-149">![동작 확인](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "동작 확인")</span><span class="sxs-lookup"><span data-stu-id="f1411-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="f1411-150">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f1411-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="f1411-151">Single sign on에 대 한 Concur를 이미 구성한 경우 hello 검색 필드를 사용 하 여 Concur의 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="f1411-152">그렇지 않은 경우 선택 **추가** 검색 한 **Concur** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="f1411-153">Concur hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="f1411-154">Concur, 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="f1411-155">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![프로비전](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="f1411-157">Hello에서 **관리자 자격 증명** 섹션을 hello 입력 **사용자 이름** 및 hello **암호** Concur 관리자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="f1411-158">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Concur 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="f1411-159">Hello 연결이 실패 하는 경우 Concur 계정이 팀 관리자 권한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="f1411-160">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="f1411-161">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-161">Click **Save.**</span></span>

14. <span data-ttu-id="f1411-162">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooConcur 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f1411-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="f1411-163">Hello에 **특성 매핑을** 섹션에서 Azure AD tooConcur에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="f1411-164">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Concur에서 되는 사용 되는 toomatch hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="f1411-165">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="f1411-166">tooenable hello Concur, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="f1411-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="f1411-167">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-167">Click **Save.**</span></span>

<span data-ttu-id="f1411-168">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1411-168">You can now create a test account.</span></span> <span data-ttu-id="f1411-169">Hello 계정이 되었습니다 tooverify 동기화 tooConcur too20 분을 기다리십시오.</span><span class="sxs-lookup"><span data-stu-id="f1411-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1411-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f1411-170">Additional resources</span></span>

* [<span data-ttu-id="f1411-171">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="f1411-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1411-172">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f1411-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f1411-173">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f1411-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

