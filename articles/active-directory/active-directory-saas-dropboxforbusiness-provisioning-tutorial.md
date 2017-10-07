---
title: "자습서: Dropbox for Business와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Dropbox for Business 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="1e75f-103">자습서: 자동 사용자 프로비전에 대한 Dropbox for Business 구성</span><span class="sxs-lookup"><span data-stu-id="1e75f-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="1e75f-104">이 자습서의 hello 목표에는 비즈니스에 대 한 비즈니스 및 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정을 Azure AD tooDropbox에 대 한 tooperform Dropbox에 필요한 단계를 hello tooshow입니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e75f-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1e75f-105">Prerequisites</span></span>

<span data-ttu-id="1e75f-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1e75f-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="1e75f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="1e75f-108">Dropbox for Business Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1e75f-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="1e75f-109">팀 관리자 권한이 있는 Dropbox for Business의 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="1e75f-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="1e75f-110">비즈니스에 대 한 사용자 tooDropbox 할당</span><span class="sxs-lookup"><span data-stu-id="1e75f-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="1e75f-111">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1e75f-112">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1e75f-113">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 Azure AD의 그룹을 나타내는 tooyour Dropbox 비즈니스 앱에 대 한 액세스 해야 하는 hello 사용자 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="1e75f-114">결정, 여기 hello 지침에 따라 비즈니스 앱에 대 한 이러한 사용자 tooyour Dropbox를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="1e75f-115">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="1e75f-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="1e75f-116">비즈니스에 대 한 사용자 tooDropbox를 할당 하기 위한 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="1e75f-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="1e75f-117">것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 비즈니스 tootest hello에 대 한 tooDropbox를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="1e75f-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1e75f-119">사용자 tooDropbox for Business에 할당할 때 유효한 사용자 역할을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="1e75f-120">hello "기본 액세스" 역할 프로 비전을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="1e75f-121">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="1e75f-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="1e75f-122">이 섹션에 Azure AD tooDropbox API를 프로 비전 하는 비즈니스의 사용자 계정에 대 한 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성, 업데이트 하 고, 사용자 및 그룹에 따라 비지니스 용 Dropbox에 할당 된 사용자 계정 사용 안 함 Azure AD에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="1e75f-123">Dropbox for Business에 제공 된 hello 지침에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1e75f-124">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="1e75f-125">tooconfigure 자동 사용자 계정 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="1e75f-126">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="1e75f-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="1e75f-127">Dropbox for Business hello 검색 필드를 사용 하 여 인스턴스에 대 한 single sign on Dropbox for Business 이미 구성한 경우를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="1e75f-128">그렇지 않은 경우 선택 **추가** 검색 한 **Dropbox for Business** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="1e75f-129">Dropbox for Business hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="1e75f-130">Dropbox for Business, 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="1e75f-131">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="1e75f-133">Hello에서 **관리자 자격 증명** 섹션에서 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="1e75f-134">새 브라우저 창에 Dropbox for Business 로그인 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="1e75f-135">Hello에 **Azure AD와 tooDropbox toolink 로그인** 대화 상자에서 Dropbox for Business 테 넌 tooyour 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="1e75f-136">![사용자 프로비전](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "사용자 프로비전")</span><span class="sxs-lookup"><span data-stu-id="1e75f-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="1e75f-137">싶다는 의사를 for Business 테 넌 toogive Azure Active Directory 권한 toomake 변경 tooyour Dropbox를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="1e75f-138">**허용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="1e75f-139">![사용자 프로비전](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "사용자 프로비전")</span><span class="sxs-lookup"><span data-stu-id="1e75f-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="1e75f-140">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD 비즈니스 응용 프로그램을 위한 tooyour Dropbox를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="1e75f-141">Hello 연결이 실패 하는 경우 비즈니스 계정이 팀 관리자 권한을 대 한 Dropbox를 확인 하 고 hello 시도 **"권한 부여"** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="1e75f-142">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="1e75f-143">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-143">Click **Save.**</span></span>

11. <span data-ttu-id="1e75f-144">Hello 매핑 섹션에서 선택 **비즈니스에 대 한 동기화 Azure Active Directory 사용자 tooDropbox 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1e75f-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="1e75f-145">Hello에 **특성 매핑을** 섹션에서 비즈니스에 대 한 Azure AD tooDropbox에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="1e75f-146">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Dropbox for Business에서에서 되는 사용 되는 toomatch hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="1e75f-147">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="1e75f-148">Dropbox for Business 변경 hello에 대 한 프로 비전 서비스를 Azure AD를 hello tooenable **프로 비전 상태** 너무**에** hello 설정 섹션에서</span><span class="sxs-lookup"><span data-stu-id="1e75f-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="1e75f-149">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-149">Click **Save.**</span></span>

<span data-ttu-id="1e75f-150">모든 사용자 및/또는 비즈니스에 대 한 사용자 hello에 tooDropbox 및 그룹 섹션에 할당 된 그룹의 hello 초기 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="1e75f-151">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="1e75f-152">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 비즈니스 앱에 대 한 서비스 Dropbox에 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="1e75f-153">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-153">You can now create a test account.</span></span> <span data-ttu-id="1e75f-154">Too20 hello 계정이 되었습니다 tooverify 비즈니스용 tooDropbox를 동기화 하는 시간 (분)을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="1e75f-155">주기를 프로비전하는 성공적으로 완료된 사용자는 관련된 상태에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e75f-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="1e75f-156">![사용자 할당](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "사용자 할당")</span><span class="sxs-lookup"><span data-stu-id="1e75f-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1e75f-157">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1e75f-157">Additional resources</span></span>

* [<span data-ttu-id="1e75f-158">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="1e75f-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e75f-159">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1e75f-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1e75f-160">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1e75f-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)