---
title: "Tutorial: Azure에서 자동 사용자 프로비전에 대한 Google Apps 구성 | Microsoft Docs"
description: "사용자 계정을 Azure AD에서 Google Apps로 자동으로 프로비전 및 프로비전 해제하도록 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="78ae3-103">자습서: 자동 사용자 프로비전에 대한 Google Apps 구성</span><span class="sxs-lookup"><span data-stu-id="78ae3-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="78ae3-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Google Apps로 자동으로 프로비전하고 프로비전 해제하기 위해 Google Apps 및 Azure AD에서 수행해야 하는 단계를 보여주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78ae3-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="78ae3-105">Prerequisites</span></span>

<span data-ttu-id="78ae3-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="78ae3-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="78ae3-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="78ae3-108">Google Apps for Work 또는 Google Apps for Education에 유효한 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="78ae3-109">어느 서비스에나 평가판 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="78ae3-110">팀 관리자 권한이 있는 Google Apps의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="78ae3-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="78ae3-111">Google Apps에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="78ae3-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="78ae3-112">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="78ae3-113">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="78ae3-114">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Azure AD에서 Google Apps 앱에 액세스해야 하는 사용자를 나타내는 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="78ae3-115">결정이 되면 [엔터프라이즈 앱에 사용자 또는 그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)의 지침에 따라 해당 사용자를 Google Apps 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="78ae3-116">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Google Apps에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="78ae3-117">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="78ae3-118">사용자를 Google Apps에 할당할 때 할당 대화 상자에서 사용자 또는 "그룹" 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="78ae3-119">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="78ae3-120">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="78ae3-120">Enable automated user provisioning</span></span>

<span data-ttu-id="78ae3-121">이 섹션에서는 Azure AD를 Google Apps의 사용자 계정 프로비전 API에 연결하고 Azure AD의 사용자 및 그룹 할당을 기반으로 Google Apps에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="78ae3-122">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Google Apps에 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="78ae3-123">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="78ae3-124">자동 사용자 계정 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="78ae3-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="78ae3-125">Google Apps로 사용자 프로비저닝을 자동화하는 데 실행 가능한 다른 옵션은 온-프레미스 Active Directory ID를 Google Apps에 프로비전하는 [GADS(Google Apps Directory Sync)](https://support.google.com/a/answer/106368?hl=en) 를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="78ae3-126">반대로 이 자습서의 솔루션은 Azure Active Directory(클라우드) 사용자 및 메일 사용이 가능한 그룹을 Google Apps에 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="78ae3-127">관리자 계정을 사용하여 [Google Apps 관리 콘솔](http://admin.google.com/) 에 로그인하고 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="78ae3-128">링크가 보이지 않으면 화면 아래쪽에 있는 **기타 컨트롤** 메뉴에 숨겨져 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![보안을 클릭합니다.][10]

2. <span data-ttu-id="78ae3-130">**보안** 페이지에서 **API 참조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![API 참조를 클릭합니다.][15]

3. <span data-ttu-id="78ae3-132">**API 액세스 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-132">Select **Enable API access**.</span></span>
   
    ![API 참조를 클릭합니다.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="78ae3-134">Google Apps로 프로비전하려는 모든 사용자에 대해 Azure Active Directory에서 해당 사용자 이름을 사용자 지정 도메인에 연결 *해야* 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="78ae3-135">예를 들면 bob@contoso.onmicrosoft.com과 같은 사용자 이름은 Google Apps에서 허용되지 않지만 bob@contoso.com은 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="78ae3-136">Azure AD에서 해당 속성을 편집하여 기존 사용자의 도메인을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="78ae3-137">Azure Active Directory 및 Google Apps 모두에 대한 사용자 지정 도메인을 설정하는 방법에 대한 지침이 아래 단계에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="78ae3-138">Azure Active Directory에 사용자 지정 도메인 이름을 아직 추가하지 않은 경우에는 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="78ae3-139">a.</span><span class="sxs-lookup"><span data-stu-id="78ae3-139">a.</span></span> <span data-ttu-id="78ae3-140">[Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="78ae3-141">디렉터리 목록에서 해당 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="78ae3-142">b.</span><span class="sxs-lookup"><span data-stu-id="78ae3-142">b.</span></span> <span data-ttu-id="78ae3-143">왼쪽 탐색 창에서 **도메인 이름**을 클릭하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![도메인](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![도메인 추가](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="78ae3-146">c.</span><span class="sxs-lookup"><span data-stu-id="78ae3-146">c.</span></span> <span data-ttu-id="78ae3-147">**도메인 이름** 필드에 사용자 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="78ae3-148">이 도메인 이름은 Google Apps에 사용하려는 도메인 이름과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="78ae3-149">준비가 되면 **도메인 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-149">When ready, click the **Add Domain** button.</span></span>
     
     ![도메인 이름](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="78ae3-151">d.</span><span class="sxs-lookup"><span data-stu-id="78ae3-151">d.</span></span> <span data-ttu-id="78ae3-152">**다음** 을 클릭하여 확인 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="78ae3-153">이 도메인을 소유했는지 확인하려면 이 페이지에 제공된 값에 따라 도메인의 DNS 레코드를 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="78ae3-154">**레코드 종류** 옵션에 대해 선택한 항목에 따라 **MX 레코드** 또는 **TXT 레코드**를 사용하여 확인하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="78ae3-155">Azure AD에서 도메인 이름을 확인하는 방법에 대한 포괄적인 지침은 [Azure AD에 자신의 도메인 이름 추가](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78ae3-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![도메인](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="78ae3-157">e.</span><span class="sxs-lookup"><span data-stu-id="78ae3-157">e.</span></span> <span data-ttu-id="78ae3-158">디렉터리에 추가하려는 모든 도메인에 대해 앞의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="78ae3-159">Azure AD에서 모든 도메인을 확인했으므로 이제 Google Apps에서 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="78ae3-160">Google Apps에 아직 등록되지 않은 각 도메인에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="78ae3-161">a.</span><span class="sxs-lookup"><span data-stu-id="78ae3-161">a.</span></span> <span data-ttu-id="78ae3-162">[Google Apps 관리 콘솔](http://admin.google.com/)에서 **도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![도메인을 클릭합니다.][20]

    <span data-ttu-id="78ae3-164">b.</span><span class="sxs-lookup"><span data-stu-id="78ae3-164">b.</span></span> <span data-ttu-id="78ae3-165">**Add a domain or a domain alias(도메인 또는 도메인 별칭 추가)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![새 도메인 추가][21]

    <span data-ttu-id="78ae3-167">c.</span><span class="sxs-lookup"><span data-stu-id="78ae3-167">c.</span></span> <span data-ttu-id="78ae3-168">**다른 도메인 추가**를 선택하고 추가하려는 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![사용자의 도메인 이름을 입력합니다.][22]

    <span data-ttu-id="78ae3-170">d.</span><span class="sxs-lookup"><span data-stu-id="78ae3-170">d.</span></span> <span data-ttu-id="78ae3-171">**Continue and verify domain ownership**(계속해서 도메인 소유권 확인)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="78ae3-172">그런 다음 도메인 이름을 소유하고 있는지 확인하는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="78ae3-173">Google Apps에서 도메인을 확인하는 방법에 대한 포괄적인 지침은</span><span class="sxs-lookup"><span data-stu-id="78ae3-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="78ae3-174">[Google Apps에서 사이트 소유권 확인](https://support.google.com/webmasters/answer/35179)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78ae3-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="78ae3-175">e.</span><span class="sxs-lookup"><span data-stu-id="78ae3-175">e.</span></span> <span data-ttu-id="78ae3-176">Google Apps에 추가하려는 모든 추가 도메인에 대해 앞의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="78ae3-177">Google Apps 테넌트의 주 도메인을 변경하고 Azure AD로 Single Sign-On을 이미 구성한 경우 [2 단계 : Single Sign-On 사용](#step-two-enable-single-sign-on)의 3 단계를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="78ae3-178">[Google Apps 관리 콘솔](http://admin.google.com/)에서 **관리자 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Google Apps 클릭][26]

7. <span data-ttu-id="78ae3-180">사용자 프로비저닝을 관리하는 데 사용할 관리자 계정을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="78ae3-181">해당 계정의 **관리자 역할**에서 해당 역할에 대한 **권한**을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="78ae3-182">이 계정을 프로비전에 사용할 수 있도록 모든 **관리자 API 권한**을 사용하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Google Apps 클릭][27]
   
    > [!NOTE]
    > <span data-ttu-id="78ae3-184">프로덕션 환경을 구성하는 경우 특별히 이 단계를 위해 Google Apps에 관리자 계정을 만드는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="78ae3-185">이러한 계정에는 필요한 API 권한이 있는 계정과 연결된 관리자 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="78ae3-186">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="78ae3-187">이미 Google Apps에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Google Apps 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="78ae3-188">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Google Apps**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="78ae3-189">검색 결과에서 Google Apps를 선택하고 응용 프로그램 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="78ae3-190">Google Apps 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="78ae3-191">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![프로비전](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="78ae3-193">**관리자 자격 증명** 섹션에서 **권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="78ae3-194">그러면 새 브라우저 창에서 Google Apps 권한 부여 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="78ae3-195">Azure Active Directory에 Google Apps 테넌트를 변경할 권한을 제공할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="78ae3-196">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-196">Click **Accept**.</span></span>
    
     ![사용 권한을 확인합니다.][28]

14. <span data-ttu-id="78ae3-198">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Google Apps 앱에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="78ae3-199">연결에 실패하면 Google Apps 계정에 팀 관리자 권한이 있는지 확인하고 **"권한 부여"** 단계를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="78ae3-200">프로비전 오류 알림을 받을 개인 또는 그룹의 이메일 주소를 **알림 메일** 필드에 입력하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="78ae3-201">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-201">Click **Save.**</span></span>

17. <span data-ttu-id="78ae3-202">매핑 섹션에서 **Synchronize Azure Active Directory Users to Google Apps**(Azure Active Directory 사용자를 Google Apps에 동기화)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="78ae3-203">**특성 매핑** 섹션에서 Azure AD에서 Google Apps로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="78ae3-204">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Google Apps의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="78ae3-205">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="78ae3-206">Google Apps에 Azure AD 프로비전 서비스를 사용하도록 설정하려면 설정 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="78ae3-207">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-207">Click **Save.**</span></span>

<span data-ttu-id="78ae3-208">사용자 및 그룹 섹션에서 Google Apps에 할당된 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="78ae3-209">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="78ae3-210">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Google Apps 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ae3-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78ae3-211">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="78ae3-211">Additional resources</span></span>

* [<span data-ttu-id="78ae3-212">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="78ae3-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78ae3-213">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="78ae3-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="78ae3-214">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="78ae3-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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