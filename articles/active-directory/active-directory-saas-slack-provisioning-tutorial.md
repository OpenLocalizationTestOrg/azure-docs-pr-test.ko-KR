---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Slack 구성 | Microsoft Docs"
description: "Tooconfigure Azure Active Directory tooautomatically 프로 비전 및 프로 비전 해제 사용자 tooSlack를 계정 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="bd13e-103">자습서: 자동 사용자 프로비전에 대한 Slack 구성</span><span class="sxs-lookup"><span data-stu-id="bd13e-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="bd13e-104">hello이 자습서는 tooperform 여유 시간 및 Azure에 필요한 단계를 hello tooshow tooSlack Azure AD에서에서 AD tooautomatically 프로 비전 및 프로 비전 해제 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bd13e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bd13e-105">Prerequisites</span></span>

<span data-ttu-id="bd13e-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="bd13e-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="bd13e-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="bd13e-108">Hello로는 Slack 테 넌 트 [계획 Plus](https://aadsyncfabric.slack.com/pricing) 또는 더 잘 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="bd13e-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="bd13e-109">팀 관리자 권한이 있는 Slack의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="bd13e-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="bd13e-110">참고: hello hello 의존 하는 Azure AD 통합 프로 비전 [Slack SCIM API](https://api.slack.com/scim) 계획 더하기 또는 더 나은 hello에 사용할 수 있는 tooSlack 팀은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="bd13e-111">사용자가 tooSlack 할당</span><span class="sxs-lookup"><span data-stu-id="bd13e-111">Assigning users tooSlack</span></span>

<span data-ttu-id="bd13e-112">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="bd13e-113">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="bd13e-114">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour Slack 응용 프로그램에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="bd13e-115">결정, 여기 hello 지침에 따라 이러한 사용자 tooyour Slack 앱을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="bd13e-116">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="bd13e-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="bd13e-117">사용자가 tooSlack 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="bd13e-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="bd13e-118">것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooSlack tootest hello를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="bd13e-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bd13e-120">Hello를 선택 해야 사용자 tooSlack에 할당할 때 **사용자** 또는 hello 할당 대화 상자에서 "그룹" 역할.</span><span class="sxs-lookup"><span data-stu-id="bd13e-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="bd13e-121">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="bd13e-122">사용자 tooSlack 프로 비전 구성</span><span class="sxs-lookup"><span data-stu-id="bd13e-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="bd13e-123">이 섹션 API를 프로 비전 하는 Azure AD tooSlack의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 서비스 toocreate 프로 비전 하는 hello 구성 및 Azure AD에서 사용자 및 그룹 할당을 기준으로 Slack에 할당 된 사용자 계정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="bd13e-124">**팁:** SAML 기반 Single Sign-on hello 지침 (Azure 포털)에 제공 된 Slack에 대 한 tooenabled을 선택할 수 있습니다 [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="bd13e-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="bd13e-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="bd13e-126">Azure AD에서 tooSlack 프로비저닝 tooconfigure 자동 사용자 계정:</span><span class="sxs-lookup"><span data-stu-id="bd13e-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="bd13e-127">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd13e-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="bd13e-128">Single sign on에 대 한 여유를 이미 구성한 경우 Slack hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="bd13e-129">그렇지 않은 경우 선택 **추가** 검색 한 **Slack** hello 응용 프로그램 갤러리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="bd13e-130">Slack hello 검색 결과에서 선택한 tooyour 응용 프로그램 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="bd13e-131">여유 시간 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="bd13e-132">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Slack 프로비전](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="bd13e-134">Hello에서 **관리자 자격 증명** 섹션에서 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="bd13e-135">그러면 새 브라우저 창에서 Slack 권한 부여 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="bd13e-136">Hello 새 창에서 팀 관리자 계정을 사용 하 여 Slack에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="bd13e-137">hello 결과 권한 부여 대화 상자에서 선택 hello tooenable에 대 한 프로 비전 한 다음 선택 하는 여유 팀 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="bd13e-138">완료 되 면, return toohello Azure 포털 toocomplete hello를 프로 비전 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![권한 부여 대화 상자](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="bd13e-140">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Slack 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="bd13e-141">Hello 연결에 실패 하면 Slack 계정 팀 관리자 권한이 있는지 확인 하십시오 hello "권한 부여" 단계 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bd13e-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="bd13e-142">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="bd13e-143">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-143">Click **Save**.</span></span> 

10) <span data-ttu-id="bd13e-144">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooSlack**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="bd13e-145">Hello에 **특성 매핑을** 섹션에서 Azure AD tooSlack에서 동기화 되도록 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="bd13e-146">특성으로 선택 된 hello 참고 **일치** 속성이 업데이트 작업에 대 한 사용된 toomatch hello 사용자 계정 Slack에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="bd13e-147">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="bd13e-148">tooenable hello Slack, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="bd13e-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="bd13e-149">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-149">Click **Save**.</span></span> 

<span data-ttu-id="bd13e-150">모든 사용자 및/또는 tooSlack에 hello 사용자 및 그룹 섹션에 할당 된 그룹의 hello 초기 동기화가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="bd13e-151">Hello 초기 동기화 상태로 hello 서비스가 실행 되 고 약 10 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform을 수행 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="bd13e-152">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Slack 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="bd13e-153">[선택 사항] 그룹 개체 tooSlack 프로 비전 구성</span><span class="sxs-lookup"><span data-stu-id="bd13e-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="bd13e-154">필요에 따라 hello tooSlack Azure AD에서에서 그룹 개체 프로 비전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="bd13e-155">"사용자 그룹에 할당" 다릅니다, 그리고 해당 hello 실제 그룹 개체에 또한 tooits 구성원에서에서 복제 됩니다 Azure AD tooSlack 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="bd13e-156">예를 들어, Azure AD에서 "내 그룹"이라는 그룹이 있는 경우 Slack 내에 "내 그룹"이라는 동일한 그룹이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="bd13e-157">tooenable 그룹 개체 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="bd13e-158">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 그룹 tooSlack**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="bd13e-159">특성 매핑 hello 블레이드에서 Enabled tooYes를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="bd13e-160">Hello에 **특성 매핑을** 섹션에서 Azure AD tooSlack에서 동기화 되도록 hello 그룹 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="bd13e-161">특성으로 선택 된 hello 참고 **일치** 속성이 업데이트 작업에 대 한 여유 시간에 사용 되는 toomatch hello 그룹 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="bd13e-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-162">Click **Save**.</span></span>

<span data-ttu-id="bd13e-163">이 결과에 모든 그룹 할당 된 개체 tooSlack hello에 **사용자 및 그룹** 섹션에서 Azure AD tooSlack 완전 하 게 동기화 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="bd13e-164">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Slack 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bd13e-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bd13e-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bd13e-165">Additional Resources</span></span>

* [<span data-ttu-id="bd13e-166">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="bd13e-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="bd13e-167">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bd13e-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
