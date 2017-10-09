---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 ThousandEyes 구성 | Microsoft Docs"
description: "Tooconfigure Azure Active Directory tooautomatically 프로 비전 및 프로 비전 해제 사용자 tooThousandEyes를 계정 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="65370-103">자습서: 자동 사용자 프로비전에 대한 ThousandEyes 구성</span><span class="sxs-lookup"><span data-stu-id="65370-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="65370-104">hello이이 자습서의 단계 tooperform tooautomatically 프로 비전 ThousandEyes와 Azure AD에서에서 필요 하 고 tooThousandEyes Azure AD에서에서 사용자 계정을 프로 비전 해제할 hello tooshow가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="65370-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65370-105">Prerequisites</span></span>

<span data-ttu-id="65370-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="65370-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="65370-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="65370-108">Hello로 ThousandEyes 테 넌 트 [표준 계획](https://www.thousandeyes.com/pricing) 또는 더 잘 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="65370-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="65370-109">관리자 권한이 있는 ThousandEyes의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="65370-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="65370-110">hello 통합 프로 비전 하는 Azure AD에 의존 hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK)를 사용할 수 있는 tooThousandEyes 팀 hello 표준 계획 하거나 더 나은 변수인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="65370-111">사용자가 tooThousandEyes 할당</span><span class="sxs-lookup"><span data-stu-id="65370-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="65370-112">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="65370-113">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65370-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="65370-114">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour ThousandEyes 응용 프로그램에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="65370-115">결정, 여기 hello 지침에 따라 이러한 tooyour 사용자가 ThousandEyes 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65370-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="65370-116">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="65370-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="65370-117">사용자가 tooThousandEyes 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="65370-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="65370-118">것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 tooThousandEyes tootest hello를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="65370-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65370-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="65370-120">Hello 중 하나를 선택 해야 사용자 tooThousandEyes에 할당할 때 **사용자** 역할 또는 다른 유효한 응용 프로그램 관련 역할 (있는 경우) hello 할당 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="65370-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="65370-121">hello **기본 액세스** 역할 프로 비전을 사용할 수 없습니다 및 이러한 사용자는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="65370-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="65370-122">사용자 tooThousandEyes 프로 비전 구성</span><span class="sxs-lookup"><span data-stu-id="65370-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="65370-123">이 섹션 API를 프로 비전 하는 Azure AD tooThousandEyes의 사용자 계정을 연결 하는 방법을 안내 하 고 구성 서비스 toocreate 프로 비전 하는 hello를 업데이트 하 고 ThousandEyes에 사용자 및 그룹 할당을 기준에 할당 된 사용자 계정 사용 안 함 Azure Ad입니다.</span><span class="sxs-lookup"><span data-stu-id="65370-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="65370-124">제공 하는 hello 지침 ThousandEyes에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="65370-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="65370-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="65370-126">자동 사용자 계정을 Azure AD에서 tooThousandEyes 프로 비전 구성</span><span class="sxs-lookup"><span data-stu-id="65370-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="65370-127">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="65370-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="65370-128">이미 구성한 경우 ThousandEyes single sign on, ThousandEyes hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="65370-129">그렇지 않은 경우 선택 **추가** 검색 한 **ThousandEyes** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65370-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="65370-130">ThousandEyes hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="65370-131">ThousandEyes의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="65370-132">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ThousandEyes 프로비전](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="65370-134">Hello에서 **관리자 자격 증명** 섹션, 입력된 hello **암호 토큰** ThousandEyes의 계정에 의해 생성 된 (해당 ThousandEyes 계정 hello 토큰을 찾을 수 있습니다: **보안 & 인증**).</span><span class="sxs-lookup"><span data-stu-id="65370-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes 프로비전](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="65370-136">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour ThousandEyes 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65370-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="65370-137">Hello 연결에 실패 하면 ThousandEyes 계정에 관리자 권한이 있는지 확인 하 고 5 단계를 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="65370-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="65370-138">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 검사 hello 확인란 "보내기" 전자 메일 알림을 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="65370-139">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-139">Click **Save**.</span></span> 

9. <span data-ttu-id="65370-140">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooThousandEyes**합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="65370-141">Hello에 **특성 매핑을** 섹션에서 Azure AD tooThousandEyes에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="65370-142">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 사용 되는 toomatch hello 사용자 계정 ThousandEyes에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65370-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="65370-143">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="65370-144">tooenable hello ThousandEyes, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="65370-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="65370-145">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-145">Click **Save**.</span></span> 

<span data-ttu-id="65370-146">이 작업의 모든 사용자 및/또는 tooThousandEyes에 hello 사용자 및 그룹 섹션에 할당 된 그룹 hello 초기 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="65370-147">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="65370-148">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="65370-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="65370-149">Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.</span><span class="sxs-lookup"><span data-stu-id="65370-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="65370-150">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="65370-150">Additional resources</span></span>

* [<span data-ttu-id="65370-151">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="65370-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="65370-152">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="65370-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="65370-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65370-153">Next steps</span></span>

* [<span data-ttu-id="65370-154">Tooreview 기록 하는 방법을 알아보고 프로 비전 활동에 대 한 보고서</span><span class="sxs-lookup"><span data-stu-id="65370-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
