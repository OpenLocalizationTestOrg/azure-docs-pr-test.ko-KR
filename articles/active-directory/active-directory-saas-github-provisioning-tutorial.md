---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위해 GitHub 구성 | Microsoft Docs"
description: "Tooconfigure Azure Active Directory tooautomatically 프로 비전 및 프로 비전 해제 사용자 tooGitHub를 계정 하는 방법에 대해 알아봅니다."
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="a6e06-103">자습서: 자동 사용자 프로비전을 위해 GitHub 구성</span><span class="sxs-lookup"><span data-stu-id="a6e06-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="a6e06-104">이 자습서의 hello 목표 tooshow tooperform GitHub 및 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooGitHub에에서 필요한 단계를 hello를입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a6e06-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a6e06-105">Prerequisites</span></span>

<span data-ttu-id="a6e06-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="a6e06-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="a6e06-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="a6e06-108">Hello로 Github 테 넌 트 [비즈니스 계획](https://help.github.com/articles/organization-billing-plans/#business-plan) 또는 더 잘 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a6e06-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="a6e06-109">관리자 권한이 있는 GitHub의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="a6e06-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="a6e06-110">hello 통합 프로 비전 하는 Azure AD에 의존 hello [GitHub SCIM API](https://developer.github.com/v3/scim/), 더 나은 또는 hello 비즈니스 계획에 사용할 수 있는 tooGithub 팀은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="a6e06-111">사용자가 tooGitHub 할당</span><span class="sxs-lookup"><span data-stu-id="a6e06-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="a6e06-112">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="a6e06-113">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="a6e06-114">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour GitHub 앱에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="a6e06-115">결정, 여기 hello 지침에 따라 이러한 사용자 tooyour GitHub 앱을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="a6e06-116">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="a6e06-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="a6e06-117">사용자가 tooGitHub 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="a6e06-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="a6e06-118">것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 tooGitHub tootest hello를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="a6e06-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a6e06-120">Hello 중 하나를 선택 해야 사용자 tooGitHub에 할당할 때 **사용자** 역할 또는 다른 유효한 응용 프로그램 관련 역할 (있는 경우) hello 할당 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="a6e06-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="a6e06-121">hello **기본 액세스** 역할 프로 비전을 사용할 수 없습니다 및 이러한 사용자는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="a6e06-122">사용자 tooGitHub 프로 비전 구성</span><span class="sxs-lookup"><span data-stu-id="a6e06-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="a6e06-123">이 섹션 API를 프로 비전 하는 Azure AD tooGitHub의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 hello 서비스 toocreate 프로 비전, 구성 및 Azure AD에서 사용자 및 그룹 할당에 따라 GitHub에서 할당 된 사용자 계정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a6e06-124">SAML 기반 Single Sign-on tooenabled hello 지침에 제공 된 GitHub에 대해 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a6e06-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="a6e06-126">자동 사용자 계정을 Azure AD에서 tooGitHub 프로 비전 구성</span><span class="sxs-lookup"><span data-stu-id="a6e06-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="a6e06-127">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a6e06-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="a6e06-128">Single sign on에 대 한 GitHub를 이미 구성한 경우 GitHub hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="a6e06-129">그렇지 않은 경우 선택 **추가** 검색 한 **GitHub** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="a6e06-130">GitHub hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="a6e06-131">GitHub의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="a6e06-132">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![GitHub 프로비전](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="a6e06-134">Hello에서 **관리자 자격 증명** 섹션에서 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="a6e06-135">이 작업은 새 브라우저 창에 GitHub 권한 부여 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="a6e06-136">Hello 새 창에서 관리자 계정을 사용 하 여 GitHub에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="a6e06-137">Hello 결과 권한 부여 대화 상자에서 선택한 tooenable에 대 한 프로 비전 한 다음 선택 하는 hello GitHub 팀 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="a6e06-138">완료 되 면, return toohello Azure 포털 toocomplete hello를 프로 비전 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![권한 부여 대화 상자](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="a6e06-140">Hello Azure 포털에에서 입력 **테 넌 트 URL** 클릭 **연결 테스트** tooensure Azure AD tooyour GitHub 앱을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="a6e06-141">Hello 연결이 실패 하는 경우 GitHub 계정에 관리자 권한이 있는지 확인 하 고 **테 넌 트 URl** 올바르게 입력 하면 다음 다시 단계 "권한 부여" hello를 시도 하십시오. (구성할 수 **테 넌 트 URL** 규칙에 의해: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", 조직의 GitHub 계정에서 찾을 수 있습니다: **설정** > **조직**).</span><span class="sxs-lookup"><span data-stu-id="a6e06-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![권한 부여 대화 상자](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="a6e06-143">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 검사 hello 확인란 "보내기" 전자 메일 알림을 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="a6e06-144">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-144">Click **Save**.</span></span> 

10. <span data-ttu-id="a6e06-145">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooGitHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="a6e06-146">Hello에 **특성 매핑을** 섹션에서 Azure AD tooGitHub에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="a6e06-147">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 GitHub에서 되는 사용 되는 toomatch hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="a6e06-148">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="a6e06-149">tooenable hello GitHub 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="a6e06-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="a6e06-150">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-150">Click **Save**.</span></span> 

<span data-ttu-id="a6e06-151">이 작업의 모든 사용자 및/또는 tooGitHub에 hello 사용자 및 그룹 섹션에 할당 된 그룹 hello 초기 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="a6e06-152">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="a6e06-153">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="a6e06-154">Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e06-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a6e06-155">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a6e06-155">Additional resources</span></span>

* [<span data-ttu-id="a6e06-156">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="a6e06-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a6e06-157">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a6e06-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="a6e06-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6e06-158">Next steps</span></span>

* [<span data-ttu-id="a6e06-159">Tooreview 기록 하는 방법을 알아보고 프로 비전 활동에 대 한 보고서</span><span class="sxs-lookup"><span data-stu-id="a6e06-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
