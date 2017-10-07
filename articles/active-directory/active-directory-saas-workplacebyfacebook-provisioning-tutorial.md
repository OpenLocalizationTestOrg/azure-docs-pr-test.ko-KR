---
title: "자습서: Workplace by Facebook과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Facebook에서 회사 사이입니다."
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
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="ee218-103">자습서: 사용자 프로비전에 대한 Workplace by Facebook 구성</span><span class="sxs-lookup"><span data-stu-id="ee218-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="ee218-104">hello이이 자습서의 Facebook 및 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooWorkplace Facebook에서 여 tooperform 작업 공간에 필요한 단계를 hello tooshow가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee218-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ee218-105">Prerequisites</span></span>

<span data-ttu-id="ee218-106">Facebook에서 작업 공간와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="ee218-107">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ee218-107">An Azure AD subscription</span></span>
- <span data-ttu-id="ee218-108">Workplace by Facebook Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ee218-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee218-109">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee218-110">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee218-111">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ee218-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee218-112">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="ee218-113">Facebook에서 사용자가 tooWorkplace 할당</span><span class="sxs-lookup"><span data-stu-id="ee218-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="ee218-114">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ee218-115">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ee218-116">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 Azure AD의 그룹을 나타내는 Facebook 응용 프로그램에서 작업 공간 tooyour 액세스 해야 하는 hello 사용자 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="ee218-117">결정, 여기 hello 지침에 따라 Facebook 응용 프로그램에서 이러한 사용자 tooyour 작업 공간을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="ee218-118">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="ee218-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="ee218-119">Facebook에서 사용자가 tooWorkplace 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="ee218-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="ee218-120">것이 좋습니다는 단일 Azure AD 사용자가 Facebook tootest hello를 프로 비전 구성 하 여 tooWorkplace를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="ee218-121">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ee218-122">Facebook에서 사용자 tooWorkplace에 할당할 때 유효한 사용자 역할을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="ee218-123">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ee218-124">사용자 프로비저닝 사용</span><span class="sxs-lookup"><span data-stu-id="ee218-124">Enable User Provisioning</span></span>

<span data-ttu-id="ee218-125">이 섹션 API를 프로 비전 하는 Facebook의 사용자 계정에 의해 Azure AD tooWorkplace 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성, 업데이트 하 고, 사용자 및 그룹에 따라 Facebook에서 작업 공간에 할당 된 사용자 계정 사용 안 함 Azure AD에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ee218-126">Facebook, hello 지침에 제공 하 여 작업 공간에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee218-127">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="ee218-128">Facebook에서 tooWorkplace Azure AD에서 프로 비전 tooconfigure 사용자 계정:</span><span class="sxs-lookup"><span data-stu-id="ee218-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="ee218-129">이 섹션의 hello 목적은 toooutline 어떻게 Facebook에서 tooWorkplace를 계정 tooenable Active Directory 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="ee218-130">Facebook에서 사용자가 tooWorkplace 할당 하는 hello 기능 tooautomatically의 hello 계정 세부 정보를 동기화 하는 azure AD 지원.</span><span class="sxs-lookup"><span data-stu-id="ee218-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="ee218-131">이 자동 동기화를 사용 하면 작업 공간 Facebook tooget hello 데이터 액세스를 위한 tooauthorize 사용자 하기 전에 필요한 hello에 대 한 toosign에 처음으로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="ee218-132">또한 Azure AD에서 액세스가 취소되면 Workplace by Facebook에서 사용자 프로비전을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="ee218-133">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory** > **엔터프라이즈 앱** > **모든응용프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="ee218-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="ee218-134">Single sign on에 대 한 Facebook에서 작업 공간을 이미 구성한 경우 Facebook hello 검색 필드를 사용 하 여 작업 공간 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="ee218-135">그렇지 않은 경우 선택 **추가** 검색 한 **Facebook에서 작업 공간** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="ee218-136">Facebook에서 작업 공간 hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="ee218-137">Facebook에서 작업 공간 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="ee218-138">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ee218-140">Hello에서 **관리자 자격 증명** 섹션 hello 토큰 암호를 입력 하 고 hello Facebook 관리자가 회사의 테 넌 트 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="ee218-141">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD는 Facebook 응용 프로그램에서 tooyour 작업 공간 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="ee218-142">Hello 연결에 실패 하면 Facebook 계정에 의해 회사가 팀 관리자 권한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="ee218-143">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="ee218-144">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-144">Click **Save.**</span></span>

9. <span data-ttu-id="ee218-145">Hello 매핑 섹션에서 선택 **Facebook에서 동기화 할 Azure Active Directory 사용자 tooWorkplace 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ee218-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="ee218-146">Hello에 **특성 매핑을** 섹션에서 Facebook에서 tooWorkplace Azure AD에서에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="ee218-147">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Facebook에서 작업 공간에서 되는 사용 되는 toomatch hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="ee218-148">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="ee218-149">tooenable hello Facebook, hello 변경 하 여 작업 공간에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="ee218-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="ee218-150">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-150">Click **Save.**</span></span>

<span data-ttu-id="ee218-151">방법에 대 한 자세한 내용은 tooconfigure 자동 프로 비전, 참조 [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="ee218-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="ee218-152">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee218-152">You can now create a test account.</span></span> <span data-ttu-id="ee218-153">Hello 계정이 되었습니다 tooverify 동기화 Facebook에서 tooWorkplace too20 분을 기다리십시오.</span><span class="sxs-lookup"><span data-stu-id="ee218-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee218-154">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ee218-154">Additional resources</span></span>

* [<span data-ttu-id="ee218-155">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="ee218-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee218-156">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ee218-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ee218-157">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ee218-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

