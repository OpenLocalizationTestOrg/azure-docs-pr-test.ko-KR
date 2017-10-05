---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 LinkedIn Sales Navigator 구성 | Microsoft Docs"
description: "사용자 계정을 LinkedIn Sales Navigator로 자동으로 프로비전 및 프로비전 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 86357949c8e6927f78ca5bb8b7e20a6b88c37ef3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a><span data-ttu-id="32ebe-103">자습서: 자동 사용자 프로비전에 대한 LinkedIn Sales Navigator 구성</span><span class="sxs-lookup"><span data-stu-id="32ebe-103">Tutorial: Configuring LinkedIn Sales Navigator for Automatic User Provisioning</span></span>


<span data-ttu-id="32ebe-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 LinkedIn Sales Navigator로 자동으로 프로비전 및 프로비전 해제하도록 LinkedIn Sales Navigator 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Sales Navigator and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Sales Navigator.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="32ebe-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32ebe-105">Prerequisites</span></span>

<span data-ttu-id="32ebe-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="32ebe-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="32ebe-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="32ebe-108">LinkedIn Sales Navigator 테넌트</span><span class="sxs-lookup"><span data-stu-id="32ebe-108">A LinkedIn Sales Navigator tenant</span></span> 
*   <span data-ttu-id="32ebe-109">LinkedIn 계정 센터에 액세스할 수 있는 LinkedIn Sales Navigator의 관리자 계정</span><span class="sxs-lookup"><span data-stu-id="32ebe-109">An administrator account in LinkedIn Sales Navigator with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="32ebe-110">Azure Active Directory는 [SCIM](http://www.simplecloud.info/) 프로토콜을 사용하여 LinkedIn Sales Navigator와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-110">Azure Active Directory integrates with LinkedIn Sales Navigator using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-sales-navigator"></a><span data-ttu-id="32ebe-111">LinkedIn Sales Navigator에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="32ebe-111">Assigning users to LinkedIn Sales Navigator</span></span>

<span data-ttu-id="32ebe-112">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="32ebe-113">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="32ebe-114">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 LinkedIn Sales Navigator에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Sales Navigator.</span></span> <span data-ttu-id="32ebe-115">결정했으면 다음 지시에 따라 이러한 사용자를 LinkedIn Sales Navigator에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-115">Once decided, you can assign these users to LinkedIn Sales Navigator by following the instructions here:</span></span>

[<span data-ttu-id="32ebe-116">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="32ebe-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-sales-navigator"></a><span data-ttu-id="32ebe-117">LinkedIn Sales Navigator에 사용자 할당을 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="32ebe-117">Important tips for assigning users to LinkedIn Sales Navigator</span></span>

*   <span data-ttu-id="32ebe-118">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 LinkedIn Sales Navigator에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-118">It is recommended that a single Azure AD user be assigned to LinkedIn Sales Navigator to test the provisioning configuration.</span></span> <span data-ttu-id="32ebe-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="32ebe-120">사용자를 LinkedIn Sales Navigator에 할당할 때 할당 대화 상자에서 **사용자** 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-120">When assigning a user to LinkedIn Sales Navigator, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="32ebe-121">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-sales-navigator"></a><span data-ttu-id="32ebe-122">LinkedIn Sales Navigator에 사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="32ebe-122">Configuring user provisioning to LinkedIn Sales Navigator</span></span>

<span data-ttu-id="32ebe-123">이 섹션에서는 사용자의 Azure AD를 LinkedIn Sales Navigator의 SCIM 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 LinkedIn Sales Navigator에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-123">This section guides you through connecting your Azure AD to LinkedIn Sales Navigator's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="32ebe-124">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 LinkedIn Sales Navigator에 대해 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="32ebe-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-sales-navigator-in-azure-ad"></a><span data-ttu-id="32ebe-126">Azure AD에서 LinkedIn Sales Navigator에 자동 사용자 계정 프로비전을 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-126">To configure automatic user account provisioning to LinkedIn Sales Navigator in Azure AD:</span></span>


<span data-ttu-id="32ebe-127">첫 번째 단계는 LinkedIn 액세스 토큰을 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="32ebe-128">엔터프라이즈 관리자인 경우 액세스 토큰을 자체 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="32ebe-129">사용자 계정 센터에서 **설정 &gt; 전역 설정**으로 이동하고 **SCIM 설치** 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="32ebe-130">링크를 통하지 않고 계정 센터에 직접 액세스하는 경우 다음 단계를 사용하여 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="32ebe-131">계정 센터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="32ebe-132">**관리 &gt; 관리 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="32ebe-133">왼쪽 세로 막대에서 **고급 통합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="32ebe-134">계정 센터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="32ebe-135">**+ 새 SCIM 구성 추가**를 클릭하고 각 필드를 입력하여 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="32ebe-136">자동 할당 라이선스가 활성화되지 않으면 사용자 데이터만 동기화된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="32ebe-138">자동 라이선스 할당을 사용하는 경우 응용 프로그램 인스턴스 및 라이선스 유형을 메모해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="32ebe-139">라이선스는 모든 라이선스가 취득될 때까지 선착순으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="32ebe-141">**토큰 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-141">Click **Generate token**.</span></span> <span data-ttu-id="32ebe-142">**액세스 토큰** 필드 아래에 액세스 토큰이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="32ebe-143">페이지를 나가기 전에 클립보드 또는 컴퓨터에 액세스 토큰을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="32ebe-144">다음으로, [Azure Portal](https://portal.azure.com)에 로그인하고 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="32ebe-145">Single Sign-On에 대한 LinkedIn Sales Navigator를 이미 구성한 경우 검색 필드를 사용하여 LinkedIn Sales Navigator의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using the search field.</span></span> <span data-ttu-id="32ebe-146">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **LinkedIn Sales Navigator**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in the application gallery.</span></span> <span data-ttu-id="32ebe-147">검색 결과에서 LinkedIn Sales Navigator를 선택하고 응용 프로그램의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-147">Select LinkedIn Sales Navigator from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="32ebe-148">LinkedIn Sales Navigator의 인스턴스를 선택한 다음, **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-148">Select your instance of LinkedIn Sales Navigator, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="32ebe-149">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="32ebe-151">**관리자 자격 증명** 아래에서 다음 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="32ebe-152">**테넌트 URL** 필드에 https://api.linkedin.com을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="32ebe-153">**비밀 토큰** 필드에 1단계에서 생성한 액세스 토큰을 입력하고 **연결 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="32ebe-154">포털의 오른쪽 맨 위에 성공 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="32ebe-155">프로비전 오류 알림을 받을 개인 또는 그룹의 전자 메일 주소를 **알림 전자 메일** 필드에 입력하고 아래 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="32ebe-156">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-156">Click **Save**.</span></span> 

14) <span data-ttu-id="32ebe-157">**특성 매핑** 섹션에서 Azure AD에서 LinkedIn Sales Navigator로 동기화할 사용자 및 그룹 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Sales Navigator.</span></span> <span data-ttu-id="32ebe-158">**일치** 속성으로 선택한 특성은 업데이트 작업 시 LinkedIn Sales Navigator에서 사용자 계정 또는 그룹을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Sales Navigator for update operations.</span></span> <span data-ttu-id="32ebe-159">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-159">Select the Save button to commit any changes.</span></span>

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="32ebe-161">LinkedIn Sales Navigator에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-161">To enable the Azure AD provisioning service for LinkedIn Sales Navigator, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="32ebe-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-162">Click **Save**.</span></span> 

<span data-ttu-id="32ebe-163">사용자 및 그룹 섹션에서 LinkedIn Sales Navigator에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Sales Navigator in the Users and Groups section.</span></span> <span data-ttu-id="32ebe-164">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 수행하는 데 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="32ebe-165">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 LinkedIn Sales Navigator 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ebe-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Sales Navigator app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="32ebe-166">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="32ebe-166">Additional Resources</span></span>

* [<span data-ttu-id="32ebe-167">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="32ebe-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="32ebe-168">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="32ebe-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
