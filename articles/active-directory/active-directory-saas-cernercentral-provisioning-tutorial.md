---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Cerner Central 구성 | Microsoft Docs"
description: "사용자를 Cerner Central의 명단으로 자동으로 프로비전하도록 Azure Active Directory를 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="032c4-103">자습서: 자동 사용자 프로비전에 대한 Cerner Central 구성</span><span class="sxs-lookup"><span data-stu-id="032c4-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="032c4-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Cerner Central의 사용자 명단으로 자동으로 프로비전 및 프로비전 해제하도록 Cerner Central 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="032c4-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="032c4-105">Prerequisites</span></span>

<span data-ttu-id="032c4-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="032c4-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="032c4-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="032c4-108">Cerner Central 테넌트</span><span class="sxs-lookup"><span data-stu-id="032c4-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="032c4-109">Azure Active Directory는 [SCIM](http://www.simplecloud.info/) 프로토콜을 사용하여 Cerner Central과 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="032c4-110">Cerner Central에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="032c4-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="032c4-111">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="032c4-112">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="032c4-113">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Cerner Central에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="032c4-114">결정했으면 다음 지시에 따라 이러한 사용자를 Cerner Central에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="032c4-115">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="032c4-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="032c4-116">Cerner Central에 사용자 할당을 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="032c4-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="032c4-117">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Cerner Central에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="032c4-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="032c4-119">초기 테스트가 한 명의 사용자에 대해 완료되면 Cerner Central은 Cerner의 사용자 명단으로 프로비전되도록 모든 Cerner 솔루션(Cerner Central뿐 아니라)에 액세스하려는 사용자의 전체 목록을 할당하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="032c4-120">다른 Cerner 솔루션은 사용자 명단에서 사용자의 이 목록을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="032c4-121">사용자를 Cerner Central에 할당할 때 할당 대화 상자에서 **사용자** 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="032c4-122">"기본 액세스" 역할이 있는 사용자는 프로비전에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="032c4-123">Cerner Central에 사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="032c4-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="032c4-124">이 섹션에서는 사용자의 Azure AD를 Cerner의 SCIM 사용자 계정 프로비전 API를 사용하여 Cerner Central의 사용자 명단에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Cerner Central에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="032c4-125">[Azure Portal( https://portal.azure.com ) 에 제공된 지침에 따라 Cerner Central에 대해 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="032c4-126">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="032c4-127">자세한 내용은 [Cerner Central Single Sign-On 자습서](active-directory-saas-cernercentral-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="032c4-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="032c4-128">Azure AD에서 Cerner Central에 자동 사용자 계정 프로비전을 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="032c4-129">Cerner Central으로 사용자 계정을 프로비전하기 위해 Cerner에서 Cerner Central 시스템 계정을 요청하고 Azure AD에서 Cerner의 SCIM 끝점에 연결하는 데 사용할 수 있는 OAuth 전달자 토큰을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="032c4-130">또한 프로덕션에 배포하기 전에 Cerner 샌드박스 환경에서 통합을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="032c4-131">첫 번째 단계는 Cerner 및 Azure AD 통합을 관리하는 사용자에게 CernerCare 계정이 있는지 확인합니다. 이 계정은 지침을 완료하는 데 필요한 설명서에 액세스할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="032c4-132">필요한 경우 아래 URL을 사용하여 해당하는 각 환경에서 CernerCare 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="032c4-133">샌드박스: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="032c4-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="032c4-134">프로덕션: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="032c4-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="032c4-135">다음으로 Azure AD에 대해 시스템 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="032c4-136">아래 지침에 따라 샌드박스 및 프로덕션 환경에 대한 시스템 계정을 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="032c4-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="032c4-137">지침: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="032c4-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="032c4-138">샌드박스: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="032c4-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="032c4-139">프로덕션: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="032c4-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="032c4-140">다음으로 각 시스템 계정에 대해 OAuth 전달자 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="032c4-141">이렇게 하려면 아래의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="032c4-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="032c4-142">지침: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="032c4-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="032c4-143">샌드박스: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="032c4-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="032c4-144">프로덕션: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="032c4-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="032c4-145">마지막으로, 구성을 완료하려면 Cerner에서 샌드박스와 프로덕션 환경에 대한 사용자 명단 영역 ID를 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="032c4-146">이 ID를 획득하는 방법에 대한 자세한 내용은 https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="032c4-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="032c4-147">이제 Cerner로 사용자 계정을 프로비전하도록 Azure AD를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="032c4-148">[Azure Portal](https://portal.azure.com)에 로그인하고 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="032c4-149">Single Sign-On에 대한 Cerner Central을 이미 구성한 경우 검색 필드를 사용하여 Cerner Central의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="032c4-150">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Cerner Central**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="032c4-151">검색 결과에서 Cerner Central을 선택하고 응용 프로그램의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="032c4-152">Cerner Central의 인스턴스를 선택한 다음, **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="032c4-153">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Cerner Central 프로비저닝](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="032c4-155">**관리자 자격 증명** 아래에서 다음 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="032c4-156">**테넌트 URL** 필드에 아래 형식으로 URL을 입력합니다. 여기서 "User-Roster-Realm-ID"를 4단계에서 획득한 영역 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="032c4-157">샌드박스: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="032c4-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="032c4-158">프로덕션: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="032c4-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="032c4-159">**비밀 토큰** 필드에 3단계에서 생성한 OAuth 전달자 토큰을 입력하고 **연결 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="032c4-160">포털의 오른쪽 맨 위에 성공 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="032c4-161">프로비전 오류 알림을 받을 개인 또는 그룹의 전자 메일 주소를 **알림 전자 메일** 필드에 입력하고 아래 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="032c4-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-162">Click **Save**.</span></span> 

12. <span data-ttu-id="032c4-163">**특성 매핑** 섹션에서 Azure AD에서 Cerner Central로 동기화될 사용자 및 그룹 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="032c4-164">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Cerner Central에서 사용자 계정 또는 그룹을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="032c4-165">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="032c4-166">Cerner Central에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="032c4-167">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-167">Click **Save**.</span></span> 

<span data-ttu-id="032c4-168">사용자 및 그룹 섹션에서 Cerner Central에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="032c4-169">초기 동기화는 Azure AD 프로비전 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="032c4-170">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Cerner Central 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032c4-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="032c4-171">Azure AD 프로비저닝 로그를 읽는 방법에 대한 자세한 내용은 [자동 사용자 계정 프로비저닝에 대한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="032c4-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="032c4-172">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="032c4-172">Additional resources</span></span>

* [<span data-ttu-id="032c4-173">Cerner Central: Azure AD를 사용하여 ID 데이터 게시</span><span class="sxs-lookup"><span data-stu-id="032c4-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="032c4-174">자습서: Azure Active Directory를 사용한 Single Sign-On에 대한 Cerner Central 구성</span><span class="sxs-lookup"><span data-stu-id="032c4-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="032c4-175">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="032c4-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="032c4-176">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="032c4-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="032c4-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="032c4-177">Next steps</span></span>
* <span data-ttu-id="032c4-178">[프로비저닝 활동에 대한 로그를 검토하고 보고서를 확인하는 방법을 알아봅니다](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="032c4-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
