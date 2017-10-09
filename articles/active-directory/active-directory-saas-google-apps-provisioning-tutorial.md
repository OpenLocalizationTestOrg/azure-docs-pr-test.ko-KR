---
title: "Tutorial: Azure에서 자동 사용자 프로비전에 대한 Google Apps 구성 | Microsoft Docs"
description: "Azure AD tooGoogle 앱에서에서 tooautomatically 프로 비전 및 프로 비전 해제 사용자 계정을 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="40a87-103">자습서: 자동 사용자 프로비전에 대한 Google Apps 구성</span><span class="sxs-lookup"><span data-stu-id="40a87-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="40a87-104">hello이이 자습서의 단계 tooperform Google Apps와 Azure AD tooautomatically 프로 비전에 필요 하 고 Azure AD tooGoogle 앱에서에서 사용자 계정을 프로 비전 해제할 hello tooshow가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40a87-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="40a87-105">Prerequisites</span></span>

<span data-ttu-id="40a87-106">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="40a87-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="40a87-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="40a87-108">Google Apps for Work 또는 Google Apps for Education에 유효한 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="40a87-109">어느 서비스에나 평가판 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="40a87-110">팀 관리자 권한이 있는 Google Apps의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="40a87-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="40a87-111">TooGoogle 응용 프로그램 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="40a87-112">Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="40a87-113">자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="40a87-114">하기 전에 구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 해야 toodecide 어떤 사용자 및/또는 Azure AD의 그룹을 tooyour Google Apps 응용 프로그램에 액세스 해야 하는 hello 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="40a87-115">여기 hello 지침에 따라 이러한 사용자 tooyour Google Apps 응용 프로그램을 결정 한 후에 할당할 수 있습니다: [사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="40a87-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="40a87-116">것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooGoogle 앱 tootest hello를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="40a87-117">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="40a87-118">사용자 tooGoogle 앱에 할당할 때는 hello 할당 대화 상자에서 hello 사용자 또는 역할 "그룹"를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="40a87-119">hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="40a87-120">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="40a87-120">Enable automated user provisioning</span></span>

<span data-ttu-id="40a87-121">이 섹션 API를 프로 비전 해당 Azure AD tooGoogle 앱의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 hello 서비스 toocreate 프로 비전, 구성 및 Azure AD에서 사용자 및 그룹 할당을 기준으로 Google Apps에 할당 된 사용자 계정 사용 안 함 .</span><span class="sxs-lookup"><span data-stu-id="40a87-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="40a87-122">Hello 지침에 제공 된 Google Apps에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="40a87-123">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="40a87-124">자동 사용자 계정 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="40a87-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="40a87-125">사용자 tooGoogle 앱 프로 비전을 자동화 하기 위한 또 다른 실행 가능한 옵션은 toouse [Google 앱 디렉터리 동기화 (GADS)](https://support.google.com/a/answer/106368?hl=en) 온-프레미스 Active Directory identities tooGoogle 앱 프로 비전입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="40a87-126">반면,이 자습서의 hello 솔루션에는 Azure Active Directory (클라우드) 사용자 및 메일 사용이 가능한 그룹 tooGoogle 앱 프로 비전합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="40a87-127">Hello에 로그인 [Google 앱 관리 콘솔](http://admin.google.com/) 프로그램 관리자 계정을 사용 하 고 클릭 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="40a87-128">Hello 링크 보이지 않으면 hello 아래 숨겨질 수 있습니다 **기타 컨트롤** hello hello 화면 맨 아래에 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![보안을 클릭합니다.][10]

2. <span data-ttu-id="40a87-130">Hello에 **보안** 페이지 **API 참조**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![API 참조를 클릭합니다.][15]

3. <span data-ttu-id="40a87-132">**API 액세스 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-132">Select **Enable API access**.</span></span>
   
    ![API 참조를 클릭합니다.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="40a87-134">응용 프로그램을 Azure Active Directory에서 자신의 사용자 이름 tooprovision tooGoogle 하려는 모든 사용자에 대해 *해야* 동률된 tooa 사용자 지정 도메인 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="40a87-135">예를 들면 bob@contoso.onmicrosoft.com과 같은 사용자 이름은 Google Apps에서 허용되지 않지만 bob@contoso.com은 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="40a87-136">Azure AD에서 해당 속성을 편집하여 기존 사용자의 도메인을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="40a87-137">지침에 다음 단계 tooset Azure Active Directory와 Google Apps에 대 한 사용자 지정 도메인은 포함 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="40a87-138">사용자 지정 도메인 이름을 tooyour Azure Active Directory를 아직 추가 하지 않았다면, 다음 단계를 수행 하는 hello를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="40a87-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="40a87-139">a.</span><span class="sxs-lookup"><span data-stu-id="40a87-139">a.</span></span> <span data-ttu-id="40a87-140">Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="40a87-141">Hello 디렉터리 목록에 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="40a87-142">b.</span><span class="sxs-lookup"><span data-stu-id="40a87-142">b.</span></span> <span data-ttu-id="40a87-143">클릭 **도메인 이름** 왼쪽된 탐색 창의 hello 되 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![도메인](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![도메인 추가](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="40a87-146">c.</span><span class="sxs-lookup"><span data-stu-id="40a87-146">c.</span></span> <span data-ttu-id="40a87-147">Hello에 도메인 이름을 입력 **도메인 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="40a87-148">이 도메인 이름은 hello 해야 합니다. Google Apps toouse 만들려는 경우 같은 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="40a87-149">준비가 되 면 클릭 hello **도메인 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![도메인 이름](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="40a87-151">d.</span><span class="sxs-lookup"><span data-stu-id="40a87-151">d.</span></span> <span data-ttu-id="40a87-152">클릭 **다음** toogo toohello 확인 페이지.</span><span class="sxs-lookup"><span data-stu-id="40a87-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="40a87-153">이 도메인을 소유 하는 tooverify,이 페이지에 제공 된 toohello 값에 따라 hello 도메인의 DNS 레코드를 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="40a87-154">Tooverify 중 하나를 사용 하 여 선택할 수 있으며 **MX 레코드** 또는 **TXT 레코드**hello에 대 한 선택에 따라 **레코드 종류** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="40a87-155">에 대 한 보다 포괄적인 지침은 Azure AD와 tooverify 도메인 이름을 어떻게, [고유한 도메인 이름을 tooAzure AD 추가](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![도메인](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="40a87-157">e.</span><span class="sxs-lookup"><span data-stu-id="40a87-157">e.</span></span> <span data-ttu-id="40a87-158">Hello 이전 tooadd tooyour 디렉터리를 만들려는 경우 모든 hello 도메인에 대 한 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="40a87-159">Azure AD에서 모든 도메인을 확인했으므로 이제 Google Apps에서 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="40a87-160">Google Apps를 통해 이미 등록 되지 않은 각 도메인에 대 한 단계를 수행 하는 hello 수행.</span><span class="sxs-lookup"><span data-stu-id="40a87-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="40a87-161">a.</span><span class="sxs-lookup"><span data-stu-id="40a87-161">a.</span></span> <span data-ttu-id="40a87-162">Hello에 [Google 앱 관리 콘솔](http://admin.google.com/), 클릭 **도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![도메인을 클릭합니다.][20]

    <span data-ttu-id="40a87-164">b.</span><span class="sxs-lookup"><span data-stu-id="40a87-164">b.</span></span> <span data-ttu-id="40a87-165">**Add a domain or a domain alias(도메인 또는 도메인 별칭 추가)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![새 도메인 추가][21]

    <span data-ttu-id="40a87-167">c.</span><span class="sxs-lookup"><span data-stu-id="40a87-167">c.</span></span> <span data-ttu-id="40a87-168">선택 **다른 도메인을 추가**, 싶다는 의사를 tooadd hello 도메인의 hello 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![사용자의 도메인 이름을 입력합니다.][22]

    <span data-ttu-id="40a87-170">d.</span><span class="sxs-lookup"><span data-stu-id="40a87-170">d.</span></span> <span data-ttu-id="40a87-171">**Continue and verify domain ownership**(계속해서 도메인 소유권 확인)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="40a87-172">그런 다음 hello 도메인 이름을 소유 하 고 있음을 hello 단계 tooverify를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="40a87-173">에 대 한 포괄적인 지침은 tooverify Google Apps를 통해 도메인 확인 하려면 어떻게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="40a87-174">[Google Apps에서 사이트 소유권 확인](https://support.google.com/webmasters/answer/35179)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40a87-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="40a87-175">e.</span><span class="sxs-lookup"><span data-stu-id="40a87-175">e.</span></span> <span data-ttu-id="40a87-176">Hello 이전 tooadd tooGoogle 응용 프로그램을 만들려는 경우 다른 도메인에 대 한 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="40a87-177">이미 있는 경우와 Azure ad single sign-on 구성 Google Apps 테 넌 트에 대 한 hello 주 도메인을 변경한 경우 아래의 toorepeat 단계 # 3에 있는 [2 단계: 사용 하도록 설정 Single Sign-on](#step-two-enable-single-sign-on)합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="40a87-178">Hello에 [Google 앱 관리 콘솔](http://admin.google.com/), 클릭 **관리자 역할이 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Google Apps 클릭][26]

7. <span data-ttu-id="40a87-180">어떤 관리자 결정를 계정 toouse toomanage 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="40a87-181">Hello에 대 한 **관리자 역할이** 해당 계정의 hello 편집 **권한** 해당 역할에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="40a87-182">모든 hello 권한이 있는지 확인 **관리자 API 권한** 이 계정을 프로 비전에 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Google Apps 클릭][27]
   
    > [!NOTE]
    > <span data-ttu-id="40a87-184">프로덕션 환경에 구성 하는 경우 toocreate 관리자 계정이 Google Apps에서이 단계에 대해 구체적으로 hello 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="40a87-185">이러한 계정은 연결 된 hello 필요한 API 권한이 있는 관리자 역할에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="40a87-186">Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="40a87-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="40a87-187">Single sign on에 대 한 Google Apps를 이미 구성한 경우 Google Apps hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="40a87-188">그렇지 않은 경우 선택 **추가** 검색 한 **Google Apps** hello 응용 프로그램 갤러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="40a87-189">Google Apps hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="40a87-190">Google Apps의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="40a87-191">집합 hello **프로 비전 모드** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![프로비전](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="40a87-193">Hello에서 **관리자 자격 증명** 섹션에서 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="40a87-194">그러면 새 브라우저 창에서 Google Apps 권한 부여 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="40a87-195">싶다는 의사를 toogive Azure Active Directory 권한 toomake 변경 tooyour Google Apps 테 넌 트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="40a87-196">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-196">Click **Accept**.</span></span>
    
     ![사용 권한을 확인합니다.][28]

14. <span data-ttu-id="40a87-198">Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Google Apps 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="40a87-199">Hello 연결이 실패 하는 경우 Google Apps 계정이 팀 관리자 권한을 확인 하 고 hello 시도 **"권한 부여"** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="40a87-200">개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="40a87-201">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-201">Click **Save.**</span></span>

17. <span data-ttu-id="40a87-202">Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooGoogle 앱.**</span><span class="sxs-lookup"><span data-stu-id="40a87-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="40a87-203">Hello에 **특성 매핑을** 섹션에서 Azure AD tooGoogle 응용 프로그램에서에서 동기화 되는 hello 사용자 특성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="40a87-204">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Google Apps에서 되는 사용 되는 toomatch hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="40a87-205">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="40a87-206">tooenable hello Google Apps, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서</span><span class="sxs-lookup"><span data-stu-id="40a87-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="40a87-207">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-207">Click **Save.**</span></span>

<span data-ttu-id="40a87-208">모든 사용자의 hello 초기 동기화를 시작 및/또는 그룹이 hello 사용자 및 그룹 섹션에서 tooGoogle 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="40a87-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="40a87-209">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="40a87-210">Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Google Apps 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="40a87-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40a87-211">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="40a87-211">Additional resources</span></span>

* [<span data-ttu-id="40a87-212">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="40a87-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40a87-213">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="40a87-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="40a87-214">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="40a87-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png