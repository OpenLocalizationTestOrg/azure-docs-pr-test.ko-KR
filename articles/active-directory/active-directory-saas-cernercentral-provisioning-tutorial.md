---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Cerner Central 구성 | Microsoft Docs"
description: "Azure Active Directory tooautomatically tooconfigure tooa 명단 Cerner 중에 사용자를 프로 비전 방법에 대해 알아봅니다."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="2a008-103">자습서: 자동 사용자 프로비전에 대한 Cerner Central 구성</span><span class="sxs-lookup"><span data-stu-id="2a008-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="2a008-104">이 자습서의 hello 목표 tooshow tooperform Cerner 중부와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooa 사용자 명단 Cerner 중앙에에 필요한 단계를 hello를입니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="2a008-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2a008-105">Prerequisites</span></span>

<span data-ttu-id="2a008-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="2a008-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="2a008-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="2a008-108">Cerner Central 테넌트</span><span class="sxs-lookup"><span data-stu-id="2a008-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="2a008-109">Hello를 사용 하 여 Cerner 중부와 azure Active Directory 통합 [SCIM](http://www.simplecloud.info/) 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="2a008-110">사용자가 tooCerner 중앙 할당</span><span class="sxs-lookup"><span data-stu-id="2a008-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="2a008-111">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="2a008-112">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="2a008-113">구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 Azure AD의 그룹 나타내는 tooCerner 중앙 액세스 해야 하는 hello 사용자를 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="2a008-114">결정, 이러한 사용자 tooCerner 중앙 여기 hello 지침에 따라 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="2a008-115">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="2a008-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="2a008-116">사용자가 tooCerner 중앙 할당 하는 데 중요 한 팁</span><span class="sxs-lookup"><span data-stu-id="2a008-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="2a008-117">것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooCerner 중앙 tootest hello를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="2a008-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="2a008-119">초기 테스트 한 명의 사용자에 대 한 완료 되 면 Cerner 중부 할당 hello 전체 목록은 사용자가 의도 한 tooaccess 모든 Cerner 솔루션 (뿐 아니라 Cerner 중부) 프로 비전 toobe tooCerner의 사용자 명단을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="2a008-120">다른 Cerner 솔루션이이 목록은 hello 사용자 명단에 사용자가 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="2a008-121">Hello를 선택 해야 사용자 tooCerner 중앙에 할당할 때 **사용자** hello 할당 대화 상자에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="2a008-122">Hello "기본 액세스" 역할의 사용자 프로 비전에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="2a008-123">사용자 프로비저닝 tooCerner 중앙 구성</span><span class="sxs-lookup"><span data-stu-id="2a008-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="2a008-124">이 섹션 API를 프로 비전 Cerner의 SCIM 사용자 계정을 사용 하 여 Azure AD tooCerner 중앙 사용자 명단 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성, 업데이트 하 고, Cerner 중앙에서 계정을 기반으로 할당 된 사용자를 사용 하지 않도록 설정 Azure AD에서 사용자 및 그룹 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="2a008-125">[Azure 포털 (https://portal.azure.com)에서 제공 하는 hello 지침 Cerner Central에 대 한 SAML 기반 Single Sign-on tooenabled를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="2a008-126">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="2a008-127">자세한 내용은 참조 hello [대 로그온 단일 자습서 Cerner 중부](active-directory-saas-cernercentral-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="2a008-128">tooCerner 중 Azure AD에서 프로 비전 tooconfigure 자동 사용자 계정:</span><span class="sxs-lookup"><span data-stu-id="2a008-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="2a008-129">순서 tooprovision 사용자 계정 tooCerner 중부 toorequest Cerner 중부 시스템 계정, Cerner에서 필요 하 고 Azure AD tooconnect tooCerner SCIM 끝점을 사용할 수 있는 OAuth 전달자 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="2a008-130">또한 tooproduction를 배포 하기 전에 hello 통합 Cerner 샌드박스 환경에서 수행 될 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="2a008-131">hello 첫 번째 단계는 hello Cerner 관리 tooensure hello 사람 있고 Azure AD 통합 필요한 tooaccess hello 문서 필요한 toocomplete hello 지침 CernerCare 계정.</span><span class="sxs-lookup"><span data-stu-id="2a008-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="2a008-132">필요한 경우 각 해당 환경에 toocreate CernerCare 계정 아래 hello Url을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="2a008-133">샌드박스: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="2a008-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="2a008-134">프로덕션: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="2a008-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="2a008-135">다음으로 Azure AD에 대해 시스템 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="2a008-136">샌드박스 및 프로덕션 환경에 대 한 시스템 계정 toorequest 아래 hello 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="2a008-137">지침: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="2a008-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="2a008-138">샌드박스: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2a008-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="2a008-139">프로덕션: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2a008-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="2a008-140">다음으로 각 시스템 계정에 대해 OAuth 전달자 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="2a008-141">toodo,이 따라 hello 지침은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="2a008-142">지침: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="2a008-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="2a008-143">샌드박스: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2a008-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="2a008-144">프로덕션: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="2a008-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="2a008-145">마지막으로 tooacquire 사용자 명단 영역 Id Cerner toocomplete hello 구성에서 두 hello 샌드박스 및 프로덕션 환경에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="2a008-146">방법에 대 한 내용은 tooacquire이,이 참조: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="2a008-147">이제 Azure AD tooprovision 사용자 계정 tooCerner를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="2a008-148">Toohello 로그인 [Azure 포털](https://portal.azure.com), toohello 찾아보기 및 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2a008-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="2a008-149">Single sign on Cerner 중부를 이미 구성한 경우 hello 검색 필드를 사용 하 여 Cerner 중앙 사이트의 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="2a008-150">그렇지 않은 경우 선택 **추가** 검색 한 **Cerner 중앙** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="2a008-151">Cerner 중앙 hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="2a008-152">Cerner 중앙 사이트의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="2a008-153">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Cerner Central 프로비저닝](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="2a008-155">아래에 필드를 다음 hello 입력 **관리자 자격 증명**:</span><span class="sxs-lookup"><span data-stu-id="2a008-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="2a008-156">Hello에 **테 넌 트 URL** 필드 #4 단계에서 복사한 hello 영역 ID "사용자-명단-영역-ID" 바꿉니다 아래 hello 형식의 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="2a008-157">샌드박스: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="2a008-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="2a008-158">프로덕션: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="2a008-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="2a008-159">Hello에 **암호 토큰** 필드 3 단계에서 생성 된 hello OAuth 전달자 토큰을 입력 하 고 클릭 **연결 테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="2a008-160">성공 알림을 포털의 hello upperright 쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="2a008-161">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="2a008-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-162">Click **Save**.</span></span> 

12. <span data-ttu-id="2a008-163">Hello에 **특성 매핑을** 섹션에서 hello 사용자 및 그룹 특성 toobe Azure AD tooCerner 중부에서에서 동기화를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="2a008-164">특성으로 선택 된 hello **일치** 속성은 사용 되는 toomatch hello 사용자 계정 및 업데이트 작업에 대 한 Cerner 중앙의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="2a008-165">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="2a008-166">tooenable hello Cerner Central 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션</span><span class="sxs-lookup"><span data-stu-id="2a008-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="2a008-167">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-167">Click **Save**.</span></span> 

<span data-ttu-id="2a008-168">모든 사용자의 hello 초기 동기화가 시작 및/또는 그룹이 할당 tooCerner hello 사용자 및 그룹 섹션에서 중부</span><span class="sxs-lookup"><span data-stu-id="2a008-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="2a008-169">hello 초기 동기화는 hello Azure AD에 프로 비전 서비스에서 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="2a008-170">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Cerner 중앙 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="2a008-171">Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a008-172">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2a008-172">Additional resources</span></span>

* [<span data-ttu-id="2a008-173">Cerner Central: Azure AD를 사용하여 ID 데이터 게시</span><span class="sxs-lookup"><span data-stu-id="2a008-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="2a008-174">자습서: Azure Active Directory를 사용한 Single Sign-On에 대한 Cerner Central 구성</span><span class="sxs-lookup"><span data-stu-id="2a008-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="2a008-175">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="2a008-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="2a008-176">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2a008-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="2a008-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a008-177">Next steps</span></span>
* <span data-ttu-id="2a008-178">[Tooreview 기록 하는 방법을 자세히 알아보고 get를 프로 비전 활동 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a008-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
