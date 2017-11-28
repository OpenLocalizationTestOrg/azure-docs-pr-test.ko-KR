---
title: "자습서: Box와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 상자 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="7ac2d-103">자습서: 자동 사용자 프로비전에 대한 Box 구성</span><span class="sxs-lookup"><span data-stu-id="7ac2d-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="7ac2d-104">hello이이 자습서의 목적은 tooperform 상자와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooBox에에서 필요한 tooshow hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-104">hello objective of this tutorial is tooshow hello steps you need tooperform in Box and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooBox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ac2d-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7ac2d-105">Prerequisites</span></span>

<span data-ttu-id="7ac2d-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="7ac2d-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="7ac2d-108">Box Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7ac2d-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="7ac2d-109">팀 관리자 권한이 있는 Box의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="7ac2d-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-toobox"></a><span data-ttu-id="7ac2d-110">사용자가 tooBox 할당</span><span class="sxs-lookup"><span data-stu-id="7ac2d-110">Assigning users tooBox</span></span> 

<span data-ttu-id="7ac2d-111">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="7ac2d-112">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="7ac2d-113">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour 상자 응용 프로그램에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Box app.</span></span> <span data-ttu-id="7ac2d-114">결정, 여기 hello 지침에 따라 이러한 사용자 tooyour 상자 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-114">Once decided, you can assign these users tooyour Box app by following hello instructions here:</span></span>

[<span data-ttu-id="7ac2d-115">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="7ac2d-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="7ac2d-116">사용자 및 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="7ac2d-116">Assign users and groups</span></span>
<span data-ttu-id="7ac2d-117">hello **상자 > 사용자 및 그룹** hello Azure 포털에서에서 탭 있습니다 toospecify 있는 사용자 및 그룹 액세스 tooBox 부여 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-117">hello **Box > Users and Groups** tab in hello Azure portal allows you toospecify which users and groups should be granted access tooBox.</span></span> <span data-ttu-id="7ac2d-118">사용자 또는 그룹의 할당 하면 다음 작업 toooccur hello:</span><span class="sxs-lookup"><span data-stu-id="7ac2d-118">Assignment of a user or group causes hello following things toooccur:</span></span>

* <span data-ttu-id="7ac2d-119">Azure AD 사용자 (또는 중 하나가 직접 할당 그룹 멤버 자격) tooauthenticate tooBox hello 할당을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-119">Azure AD permits hello assigned user (either by direct assignment or group membership) tooauthenticate tooBox.</span></span> <span data-ttu-id="7ac2d-120">사용자를 할당 하지 않으면 Azure AD에서는 이러한 toosign tooBox에 고 hello Azure AD 로그인 페이지에서 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-120">If a user is not assigned, then Azure AD does not permit them toosign in tooBox and returns an error on hello Azure AD sign-in page.</span></span>
* <span data-ttu-id="7ac2d-121">상자는 응용 프로그램 타일 toohello 사용자의 추가 [응용 프로그램 실행 프로그램](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-121">An app tile for Box is added toohello user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="7ac2d-122">자동 프로 비전을 사용 하는 경우 hello 할당 된 사용자 및/또는 그룹 큐 toobe 자동으로 프로 비전을 프로 비전 toohello를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-122">If automatic provisioning is enabled, then hello assigned users and/or groups are added toohello provisioning queue toobe automatically provisioned.</span></span>
  
  * <span data-ttu-id="7ac2d-123">사용자 개체 프로 비전 하는 구성 된 toobe 인 경우에 직접 할당 된 모든 사용자 hello 프로비저닝 큐에 배치 되는 다음 하 고 할당 된 모든 그룹의 구성원 인 모든 사용자가 큐를 프로 비전 하는 hello에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-123">If only user objects were configured toobe provisioned, then all directly assigned users are placed in hello provisioning queue, and all users that are members of any assigned groups are placed in hello provisioning queue.</span></span> 
  * <span data-ttu-id="7ac2d-124">그룹 개체 프로 비전 하는 구성 된 toobe 되었으면 모든 할당된 그룹 개체는 프로 비전 된 tooBox 및 해당 그룹의 구성원 인 모든 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-124">If group objects were configured toobe provisioned, then all assigned group objects are provisioned tooBox, and all users that are members of those groups.</span></span> <span data-ttu-id="7ac2d-125">hello 그룹 및 사용자 멤버 자격 tooBox 기록에 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-125">hello group and user memberships are preserved upon being written tooBox.</span></span>

<span data-ttu-id="7ac2d-126">Hello를 사용할 수 있습니다 **특성 > Single Sign On** SAML 기반 인증 및 hello 중 tooBox 나타난 어떤 사용자 특성 (또는 클레임) tooconfigure 탭 **특성 > 프로 비전** 사용자 및 그룹 특성의 흐름 방식 tooBox Azure AD에서에서 작업을 구축 하는 동안 tooconfigure를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-126">You can use hello **Attributes > Single Sign-On** tab tooconfigure which user attributes (or claims) are presented tooBox during SAML-based authentication, and hello **Attributes > Provisioning** tab tooconfigure how user and group attributes flow from Azure AD tooBox during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-toobox"></a><span data-ttu-id="7ac2d-127">사용자가 tooBox 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="7ac2d-127">Important tips for assigning users tooBox</span></span> 

*   <span data-ttu-id="7ac2d-128">것이 좋습니다 단일 Azure AD 사용자만 할당 tooBox tootest hello를 프로 비전 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-128">It is recommended that a single Azure AD user assigned tooBox tootest hello provisioning configuration.</span></span> <span data-ttu-id="7ac2d-129">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="7ac2d-130">사용자 toobox에 할당할 때 유효한 사용자 역할을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-130">When assigning a user toobox, you must select a valid user role.</span></span> <span data-ttu-id="7ac2d-131">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-131">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="7ac2d-132">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="7ac2d-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="7ac2d-133">이 섹션을 API를 프로 비전 하는 Azure AD tooBox의 사용자 계정을 연결 하는 방법을 안내 하며 서비스 toocreate 프로 비전 하는 hello 구성, 업데이트 하 고, Azure AD에서 사용자 및 그룹 할당을 기준으로 상자에 할당 된 사용자 계정 사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-133">This section guides through connecting your Azure AD tooBox's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="7ac2d-134">자동 프로 비전을 사용 하는 경우 hello 할당 된 사용자 및/또는 그룹 큐 toobe 자동으로 프로 비전을 프로 비전 toohello를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-134">If automatic provisioning is enabled, then hello assigned users and/or groups are added toohello provisioning queue toobe automatically provisioned.</span></span>
    
 * <span data-ttu-id="7ac2d-135">경우에 사용자 개체 구성된 toobe 프로 비전 되 면 다음 직접 할당 된 사용자는 hello 프로비저닝 큐에 배치 되 고 할당 된 모든 그룹의 구성원 인 모든 사용자가 큐를 프로 비전 하는 hello에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-135">If only user objects are configured toobe provisioned, then directly assigned users are placed in hello provisioning queue, and all users that are members of any assigned groups are placed in hello provisioning queue.</span></span> 
    
 * <span data-ttu-id="7ac2d-136">그룹 개체 프로 비전 하는 구성 된 toobe 되었으면 모든 할당된 그룹 개체는 프로 비전 된 tooBox 및 해당 그룹의 구성원 인 모든 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-136">If group objects were configured toobe provisioned, then all assigned group objects are provisioned tooBox, and all users that are members of those groups.</span></span> <span data-ttu-id="7ac2d-137">hello 그룹 및 사용자 멤버 자격 tooBox 기록에 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-137">hello group and user memberships are preserved upon being written tooBox.</span></span>

> [!TIP] 
> <span data-ttu-id="7ac2d-138">SAML 기반 Single Sign-on hello 지침에 제공 된 상자에 대 한 tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-138">You may also choose tooenabled SAML-based Single Sign-On for Box, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7ac2d-139">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="7ac2d-140">tooconfigure 자동 사용자 계정 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-140">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="7ac2d-141">이 섹션의 hello 목적은 toooutline 어떻게 tooBox를 계정 tooenable Active Directory 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-141">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooBox.</span></span>

1. <span data-ttu-id="7ac2d-142">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-142">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="7ac2d-143">Single sign on에 대 한 상자를 이미 구성한 경우 hello 검색 필드를 사용 하 여 상자 인스턴스의 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-143">If you have already configured Box for single sign-on, search for your instance of Box using hello search field.</span></span> <span data-ttu-id="7ac2d-144">그렇지 않은 경우 선택 **추가** 검색 한 **상자** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-144">Otherwise, select **Add** and search for **Box** in hello application gallery.</span></span> <span data-ttu-id="7ac2d-145">Hello 검색 결과에서 상자를 선택 하 고 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-145">Select Box from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="7ac2d-146">기본적으로 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-146">Select your instance of Box, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="7ac2d-147">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-147">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="7ac2d-149">Hello에서 **관리자 자격 증명** 섹션에서 클릭 **Authorize** tooopen 새 브라우저 창에서 상자 로그인 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-149">Under hello **Admin Credentials** section, click **Authorize** tooopen a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="7ac2d-150">Hello에 **로그인 toogrant 액세스 tooBox** 페이지 hello 필요한 자격 증명을 제공 하 고 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-150">On hello **Login toogrant access tooBox** page, provide hello required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="7ac2d-151">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="7ac2d-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="7ac2d-152">클릭 **Grant 액세스 tooBox** tooauthorize이 작업과 tooreturn toohello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-152">Click **Grant access tooBox** tooauthorize this operation and tooreturn toohello Azure portal.</span></span> 
   
    <span data-ttu-id="7ac2d-153">![자동 사용자 프로비저닝 사용](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "자동 사용자 프로비저닝 사용")</span><span class="sxs-lookup"><span data-stu-id="7ac2d-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="7ac2d-154">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour 상자 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-154">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Box app.</span></span> <span data-ttu-id="7ac2d-155">Hello 연결이 실패 하는 경우 Box 계정이 팀 관리자 권한을 확인 하 고 hello 시도 **"권한 부여"** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-155">If hello connection fails, ensure your Box account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="7ac2d-156">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-156">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="7ac2d-157">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-157">Click **Save.**</span></span>

11. <span data-ttu-id="7ac2d-158">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooBox 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7ac2d-158">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooBox.**</span></span>

12. <span data-ttu-id="7ac2d-159">Hello에 **특성 매핑을** 섹션에서 Azure AD tooBox에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-159">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooBox.</span></span> <span data-ttu-id="7ac2d-160">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 사용 되는 toomatch hello 사용자 계정을 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-160">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Box for update operations.</span></span> <span data-ttu-id="7ac2d-161">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-161">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="7ac2d-162">tooenable hello 상자에서 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서</span><span class="sxs-lookup"><span data-stu-id="7ac2d-162">tooenable hello Azure AD provisioning service for Box, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="7ac2d-163">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-163">Click **Save.**</span></span>

<span data-ttu-id="7ac2d-164">하는 모든 사용자 및/또는 tooBox에 hello 사용자 및 그룹 섹션에 할당 된 그룹의 hello 초기 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-164">That starts hello initial synchronization of any users and/or groups assigned tooBox in hello Users and Groups section.</span></span> <span data-ttu-id="7ac2d-165">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-165">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="7ac2d-166">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 상자 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-166">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Box app.</span></span>

<span data-ttu-id="7ac2d-167">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-167">You can now create a test account.</span></span> <span data-ttu-id="7ac2d-168">Hello 계정이 되었습니다 tooverify 동기화 toobox too20 분을 기다리십시오.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-168">Wait for up too20 minutes tooverify that hello account has been synchronized toobox.</span></span>

<span data-ttu-id="7ac2d-169">상자 테 넌 트에 동기화 된 사용자가 나열 됩니다 **관리 되는 사용자가** hello에 **관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ac2d-169">In your Box tenant, synchronized users are listed under **Managed Users** in hello **Admin Console**.</span></span>

<span data-ttu-id="7ac2d-170">![통합 상태](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "통합 상태")</span><span class="sxs-lookup"><span data-stu-id="7ac2d-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7ac2d-171">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7ac2d-171">Additional resources</span></span>

* [<span data-ttu-id="7ac2d-172">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="7ac2d-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ac2d-173">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7ac2d-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7ac2d-174">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7ac2d-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)