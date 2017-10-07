---
title: "자습서: 사용자 프로비전에 대한 Workplace by Facebook 구성 | Microsoft Docs"
description: "Facebook에서 Azure AD tooWorkplace에서 tooautomatically 프로 비전 및 프로 비전 해제 사용자 계정을 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="cc4a3-103">자습서: 사용자 프로비전에 대한 Workplace by Facebook 구성</span><span class="sxs-lookup"><span data-stu-id="cc4a3-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="cc4a3-104">프로 비전 하 고 Facebook에서 Azure Active Directory (Azure AD) tooWorkplace에서 사용자 계정을 프로 비전 해제할 단계 필요한 tooautomatically hello이 자습서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc4a3-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cc4a3-105">Prerequisites</span></span>

<span data-ttu-id="cc4a3-106">Facebook에서 작업 공간와 Azure AD 통합 tooconfigure hello 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="cc4a3-107">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="cc4a3-107">An Azure AD subscription</span></span>
- <span data-ttu-id="cc4a3-108">Workplace by Facebook SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="cc4a3-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="cc4a3-109">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="cc4a3-110">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc4a3-111">Azure AD 평가판 환경이 없으면 [1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="cc4a3-112">Facebook에서 사용자가 tooWorkplace 할당</span><span class="sxs-lookup"><span data-stu-id="cc4a3-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="cc4a3-113">Azure AD는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="cc4a3-114">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 Azure AD에서 tooan 응용 프로그램에 할당 된 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="cc4a3-115">구성 및 서비스를 프로 비전 하는 hello를 사용 합니다. Azure AD에서 사용자 및 그룹 결정 전에 Facebook 응용 프로그램에서 tooyour 작업 공간에 액세스 해야 하는 hello 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="cc4a3-116">Facebook 응용 프로그램에서 이러한 사용자 tooyour 작업 공간에 따라 지정할 수 있습니다의 지침을 hello [사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="cc4a3-117">단일 할당 하 여 프로 비전 구성 테스트 hello Facebook에서 Azure AD 사용자 tooWorkplace 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="cc4a3-118">추가 사용자 및 그룹을 나중에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="cc4a3-119">Facebook에서 사용자 tooWorkplace에 할당 하면 올바른 사용자 역할을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="cc4a3-120">hello 액세스 기본 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="cc4a3-121">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="cc4a3-121">Enable automated user provisioning</span></span>

<span data-ttu-id="cc4a3-122">이 섹션 API의 작업 공간 Facebook에서 프로 비전 하 여 Azure AD toohello 사용자 계정에 연결 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="cc4a3-123">또한 tooconfigure hello 프로 비전 서비스 toocreate 업데이트 하 고 Facebook에서 작업 공간에 할당 된 사용자 계정을 사용 하지 않도록 설정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="cc4a3-124">이는 Azure AD에서 사용자 및 그룹 할당에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="cc4a3-125">선택할 수도 있습니다 tooenabled SAML 기반 SSO Facebook에서 작업 공간에 의해 hello의 설명에 따라 hello에 제공 된 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cc4a3-126">SSO는 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="cc4a3-127">Facebook에서 tooWorkplace Azure AD에서 프로 비전 하는 사용자 계정 구성</span><span class="sxs-lookup"><span data-stu-id="cc4a3-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="cc4a3-128">Facebook에서 사용자가 tooWorkplace 할당 하는 hello 기능 tooautomatically의 hello 계정 세부 정보를 동기화 하는 azure AD 지원.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="cc4a3-129">이 자동 동기화를 사용 하면 작업 공간 Facebook tooget hello 데이터 액세스를 위한 tooauthorize 사용자 하기 전에 필요한 hello에 대 한 toosign에 처음으로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="cc4a3-130">또한 Azure AD에서 액세스가 취소되면 Workplace by Facebook에서 사용자 프로비전을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="cc4a3-131">Hello에 [Azure 포털](https://portal.azure.com)선택, **Azure Active Directory** > **엔터프라이즈 앱** > **모든 응용 프로그램**.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="cc4a3-132">SSO에 대 한 Facebook에서 작업 공간을 이미 구성한 경우 hello 검색 필드를 사용 하 여 Facebook에서 작업 공간 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="cc4a3-133">그렇지 않은 경우 선택 **추가** 검색 한 **Facebook에서 작업 공간** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="cc4a3-134">선택 **Facebook에서 작업 공간** hello에서 결과 검색 하 고 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="cc4a3-135">Facebook에서 작업 공간 인스턴스의 선택한 다음 선택 hello **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="cc4a3-136">설정 **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Workplace by Facebook 프로비전 옵션의 스크린샷](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="cc4a3-138">Hello에서 **관리자 자격 증명** 섹션을 hello 입력 **암호 토큰** 및 hello **테 넌 트 URL** Facebook 관리자가 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="cc4a3-139">Hello Azure 포털에서에서 선택 **연결 테스트** tooensure Azure AD는 Facebook 응용 프로그램에서 tooyour 작업 공간 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="cc4a3-140">Hello 연결에 실패 하면 Facebook 계정에 의해 회사 팀 관리자 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="cc4a3-141">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 고 hello 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="cc4a3-142">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-142">Select **Save**.</span></span>

9. <span data-ttu-id="cc4a3-143">Hello 매핑 섹션에서 선택 **Facebook에서 동기화 할 Azure Active Directory 사용자 tooWorkplace**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="cc4a3-144">Hello에 **특성 매핑을** 섹션에서 Facebook에서 tooWorkplace Azure AD에서에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="cc4a3-145">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Facebook에서 작업 공간에서 되는 사용 되는 toomatch hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="cc4a3-146">변경 내용을 선택 toocommit **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="cc4a3-147">tooenable hello hello에 Facebook에서 작업 공간에 대 한 Azure AD 프로 비전 서비스 **설정** 섹션에서 hello 변경 **프로 비전 상태** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="cc4a3-148">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-148">Select **Save**.</span></span>

<span data-ttu-id="cc4a3-149">방법에 대 한 자세한 내용은 tooconfigure 자동 프로 비전, 참조 [Facebook 설명서 hello](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="cc4a3-150">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-150">You can now create a test account.</span></span> <span data-ttu-id="cc4a3-151">Hello 계정이 되었습니다 tooverify 동기화 Facebook에서 tooWorkplace too20 분을 기다리십시오.</span><span class="sxs-lookup"><span data-stu-id="cc4a3-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc4a3-152">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cc4a3-152">Additional resources</span></span>

* [<span data-ttu-id="cc4a3-153">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="cc4a3-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc4a3-154">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cc4a3-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cc4a3-155">Single Sign-on 구성</span><span class="sxs-lookup"><span data-stu-id="cc4a3-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

