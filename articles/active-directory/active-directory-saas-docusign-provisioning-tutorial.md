---
title: "자습서: DocuSign과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 DocuSign 사이의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="ebf06-103">자습서: 사용자 프로비전에 대한 DocuSign 구성</span><span class="sxs-lookup"><span data-stu-id="ebf06-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="ebf06-104">hello이이 자습서의 단계에서 Azure AD 및 DocuSign tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooDocuSign tooperform 필요한 hello tooshow가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebf06-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ebf06-105">Prerequisites</span></span>

<span data-ttu-id="ebf06-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ebf06-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="ebf06-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ebf06-108">DocuSign Single Sign-on이 설정된 구독.</span><span class="sxs-lookup"><span data-stu-id="ebf06-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="ebf06-109">팀 관리자 권한이 있는 DocuSign의 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="ebf06-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="ebf06-110">사용자가 tooDocuSign 할당</span><span class="sxs-lookup"><span data-stu-id="ebf06-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="ebf06-111">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ebf06-112">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="ebf06-113">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour DocuSign 응용 프로그램에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="ebf06-114">결정, 여기 hello 지침에 따라 이러한 사용자 tooyour DocuSign 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="ebf06-115">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="ebf06-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="ebf06-116">사용자가 tooDocuSign 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="ebf06-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="ebf06-117">것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 tooDocuSign tootest hello를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="ebf06-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ebf06-119">사용자 tooDocuSign에 할당할 때 유효한 사용자 역할을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="ebf06-120">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ebf06-121">사용자 프로비저닝 사용</span><span class="sxs-lookup"><span data-stu-id="ebf06-121">Enable User Provisioning</span></span>

<span data-ttu-id="ebf06-122">이 섹션 API를 프로 비전 하는 Azure AD tooDocuSign의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 hello 서비스 toocreate 프로 비전, 구성 및 Azure AD에서 사용자 및 그룹 할당을 기준으로 DocuSign에 할당 된 사용자 계정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="ebf06-123">Hello 지침에 제공 된 DocuSign에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ebf06-124">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="ebf06-125">tooconfigure 사용자 계정 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="ebf06-126">이 섹션의 hello 목적은 toooutline 어떻게 tooDocuSign 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="ebf06-127">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="ebf06-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="ebf06-128">Single sign on DocuSign를 이미 구성한 경우 DocuSign hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="ebf06-129">그렇지 않은 경우 선택 **추가** 검색 한 **DocuSign** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="ebf06-130">DocuSign hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="ebf06-131">DocuSign, 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="ebf06-132">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ebf06-134">Hello에서 **관리자 자격 증명** 섹션에서 다음 구성 설정을 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="ebf06-135">a.</span><span class="sxs-lookup"><span data-stu-id="ebf06-135">a.</span></span> <span data-ttu-id="ebf06-136">Hello에 **관리자 사용자 이름** 텍스트 상자에 DocuSign 계정 hello에 이름을 **시스템 관리자에 게** 프로필 docusign.com 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="ebf06-137">b.</span><span class="sxs-lookup"><span data-stu-id="ebf06-137">b.</span></span> <span data-ttu-id="ebf06-138">Hello에 **관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="ebf06-139">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour DocuSign 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="ebf06-140">Hello에 **알림 전자 메일** 필드에, 개인 또는 프로 비전 오류 알림을 수신 하 고 hello 확인란을 선택 해야 하는 그룹의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="ebf06-141">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-141">Click **Save.**</span></span>

9. <span data-ttu-id="ebf06-142">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooDocuSign 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ebf06-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="ebf06-143">Hello에 **특성 매핑을** 섹션에서 Azure AD tooDocuSign에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="ebf06-144">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 사용 되는 toomatch hello 사용자 계정 DocuSign에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="ebf06-145">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="ebf06-146">tooenable hello DocuSign, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서</span><span class="sxs-lookup"><span data-stu-id="ebf06-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="ebf06-147">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-147">Click **Save.**</span></span>

<span data-ttu-id="ebf06-148">모든 사용자 및/또는 tooDocuSign에 hello 사용자 및 그룹 섹션에 할당 된 그룹의 hello 초기 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="ebf06-149">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="ebf06-150">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 DocuSign 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="ebf06-151">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf06-151">You can now create a test account.</span></span> <span data-ttu-id="ebf06-152">Hello 계정이 되었습니다 tooverify 동기화 tooDocuSign too20 분을 기다리십시오.</span><span class="sxs-lookup"><span data-stu-id="ebf06-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebf06-153">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ebf06-153">Additional resources</span></span>

* [<span data-ttu-id="ebf06-154">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="ebf06-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebf06-155">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ebf06-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ebf06-156">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ebf06-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)