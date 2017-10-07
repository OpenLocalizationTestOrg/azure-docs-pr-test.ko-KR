---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 LinkedIn Sales Navigator 구성 | Microsoft Docs"
description: "Tooconfigure Azure Active Directory tooautomatically 프로 비전 및 프로 비전 해제 사용자 tooLinkedIn Sales 탐색기를 계정 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a><span data-ttu-id="dc162-103">자습서: 자동 사용자 프로비전에 대한 LinkedIn Sales Navigator 구성</span><span class="sxs-lookup"><span data-stu-id="dc162-103">Tutorial: Configuring LinkedIn Sales Navigator for Automatic User Provisioning</span></span>


<span data-ttu-id="dc162-104">이 자습서의 hello 목표 tooshow tooperform LinkedIn Sales 탐색기와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooLinkedIn Sales 탐색기에에서 필요한 단계를 hello를입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Sales Navigator and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Sales Navigator.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dc162-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dc162-105">Prerequisites</span></span>

<span data-ttu-id="dc162-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="dc162-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="dc162-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="dc162-108">LinkedIn Sales Navigator 테넌트</span><span class="sxs-lookup"><span data-stu-id="dc162-108">A LinkedIn Sales Navigator tenant</span></span> 
*   <span data-ttu-id="dc162-109">액세스 toohello LinkedIn r e 계정 센터와 LinkedIn Sales 탐색 창에서 관리자 계정</span><span class="sxs-lookup"><span data-stu-id="dc162-109">An administrator account in LinkedIn Sales Navigator with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="dc162-110">Hello를 사용 하 여 LinkedIn Sales 탐색기와 azure Active Directory 통합 [SCIM](http://www.simplecloud.info/) 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-110">Azure Active Directory integrates with LinkedIn Sales Navigator using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-sales-navigator"></a><span data-ttu-id="dc162-111">사용자가 tooLinkedIn Sales 탐색기 할당</span><span class="sxs-lookup"><span data-stu-id="dc162-111">Assigning users tooLinkedIn Sales Navigator</span></span>

<span data-ttu-id="dc162-112">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="dc162-113">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="dc162-114">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 Azure AD의 그룹을 tooLinkedIn Sales 탐색기에 액세스 해야 하는 hello 사용자를 나타내는 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Sales Navigator.</span></span> <span data-ttu-id="dc162-115">결정, 여기 hello 지침에 따라 이러한 사용자 tooLinkedIn Sales 탐색기를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-115">Once decided, you can assign these users tooLinkedIn Sales Navigator by following hello instructions here:</span></span>

[<span data-ttu-id="dc162-116">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="dc162-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a><span data-ttu-id="dc162-117">사용자가 tooLinkedIn Sales 탐색기를 할당 하기 위한 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="dc162-117">Important tips for assigning users tooLinkedIn Sales Navigator</span></span>

*   <span data-ttu-id="dc162-118">것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooLinkedIn Sales 탐색기 tootest hello를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Sales Navigator tootest hello provisioning configuration.</span></span> <span data-ttu-id="dc162-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="dc162-120">Hello를 선택 해야 사용자 tooLinkedIn Sales 탐색기에 할당할 때 **사용자** hello 할당 대화 상자에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-120">When assigning a user tooLinkedIn Sales Navigator, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="dc162-121">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a><span data-ttu-id="dc162-122">사용자 프로비저닝 tooLinkedIn Sales 탐색기 구성</span><span class="sxs-lookup"><span data-stu-id="dc162-122">Configuring user provisioning tooLinkedIn Sales Navigator</span></span>

<span data-ttu-id="dc162-123">이 섹션 API를 프로 비전 하는 Azure AD tooLinkedIn Sales 탐색기 SCIM 사용자 계정 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성 업데이트 및 사용자에 따라 LinkedIn Sales 탐색 창에서 할당 된 사용자 계정 사용 안 함 및 Azure AD에서 그룹 할당을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-123">This section guides you through connecting your Azure AD tooLinkedIn Sales Navigator's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="dc162-124">Hello 지침에 제공 된 LinkedIn Sales 탐색 창에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dc162-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a><span data-ttu-id="dc162-126">Sales 탐색기 tooLinkedIn Azure AD에서 프로 비전 tooconfigure 자동 사용자 계정:</span><span class="sxs-lookup"><span data-stu-id="dc162-126">tooconfigure automatic user account provisioning tooLinkedIn Sales Navigator in Azure AD:</span></span>


<span data-ttu-id="dc162-127">hello 첫 번째 단계는 tooretrieve LinkedIn 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="dc162-128">엔터프라이즈 관리자인 경우 액세스 토큰을 자체 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="dc162-129">사용자 계정 센터에서 이동 너무**설정 &gt; 전역 설정** 및 열기 hello **SCIM 설치** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="dc162-130">하지 않고 직접 링크를 통해 hello r e 계정 센터에 액세스 하는, 단계를 수행 하는 hello를 사용 하 여 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="dc162-131">TooAccount 센터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="dc162-132">**관리 &gt; 관리 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="dc162-133">클릭 **통합 고급** hello 왼쪽된 세로 막대에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="dc162-134">방향이 지정 된 toohello r e 계정 센터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="dc162-135">클릭 **+ 새 SCIM 구성 추가** 각 필드에 입력 하 여 hello 절차에 따라 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="dc162-136">자동 할당 라이선스가 활성화되지 않으면 사용자 데이터만 동기화된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="dc162-138">Autolicense 지정을 사용 하는 경우 toonote 응용 프로그램 인스턴스 및 라이선스 유형 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="dc162-139">첫 번째 돌아와에 라이선스가 할당 된, 모든 hello 라이선스는 수행 될 때까지 먼저 기반을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="dc162-141">**토큰 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-141">Click **Generate token**.</span></span> <span data-ttu-id="dc162-142">Hello에서 액세스 토큰 디스플레이 표시 되어야 **액세스 토큰** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="dc162-143">Hello 페이지에서 이동 하기 전에 토큰 tooyour 클립보드 액세스 또는 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="dc162-144">다음으로 toohello 로그인 [Azure 포털](https://portal.azure.com), toohello 찾아보기 및 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="dc162-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="dc162-145">Single sign on LinkedIn Sales 탐색기를 이미 구성한 경우 hello 검색 필드를 사용 하 여 LinkedIn Sales 검색기의 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using hello search field.</span></span> <span data-ttu-id="dc162-146">그렇지 않은 경우 선택 **추가** 검색 한 **LinkedIn Sales 탐색기** hello 응용 프로그램 갤러리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in hello application gallery.</span></span> <span data-ttu-id="dc162-147">LinkedIn Sales 탐색기 hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-147">Select LinkedIn Sales Navigator from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="dc162-148">LinkedIn Sales 탐색기 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-148">Select your instance of LinkedIn Sales Navigator, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="dc162-149">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="dc162-151">아래에 필드를 다음 hello 입력 **관리자 자격 증명** :</span><span class="sxs-lookup"><span data-stu-id="dc162-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="dc162-152">Hello에 **테 넌 트 URL** 필드 https://api.linkedin.com를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="dc162-153">Hello에 **암호 토큰** 필드 1 단계에서 생성 한 hello 액세스 토큰을 입력 하 고 클릭 **연결 테스트** 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="dc162-154">성공 알림을 포털의 hello upperright 쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="dc162-155">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="dc162-156">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-156">Click **Save**.</span></span> 

14) <span data-ttu-id="dc162-157">Hello에 **특성 매핑을** 섹션에서 Azure AD tooLinkedIn Sales 탐색기에서에서 동기화 되도록 하는 hello 사용자 및 그룹 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Sales Navigator.</span></span> <span data-ttu-id="dc162-158">특성으로 선택 된 hello 참고 **일치** 사용된 toomatch hello 사용자 계정 및 업데이트 작업에 대 한 LinkedIn Sales 탐색 창에서 그룹 속성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Sales Navigator for update operations.</span></span> <span data-ttu-id="dc162-159">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-159">Select hello Save button toocommit any changes.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="dc162-161">tooenable hello LinkedIn Sales 탐색기에서 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="dc162-161">tooenable hello Azure AD provisioning service for LinkedIn Sales Navigator, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="dc162-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-162">Click **Save**.</span></span> 

<span data-ttu-id="dc162-163">모든 사용자 및/또는 tooLinkedIn Sales 탐색기 hello 사용자 및 그룹 섹션에서 할당 된 그룹의 hello 초기 동기화가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Sales Navigator in hello Users and Groups section.</span></span> <span data-ttu-id="dc162-164">초기 동기화 hello hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform을 수행 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="dc162-165">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 LinkedIn Sales 탐색기 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dc162-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Sales Navigator app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dc162-166">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="dc162-166">Additional Resources</span></span>

* [<span data-ttu-id="dc162-167">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="dc162-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="dc162-168">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="dc162-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
