---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Slack 구성 | Microsoft Docs"
description: "사용자 계정을 Slack으로 자동으로 프로비전 및 프로비전 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="dfec7-103">자습서: 자동 사용자 프로비전에 대한 Slack 구성</span><span class="sxs-lookup"><span data-stu-id="dfec7-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="dfec7-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Slack으로 자동으로 프로비전 및 프로비전 해제하도록 Slack 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dfec7-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dfec7-105">Prerequisites</span></span>

<span data-ttu-id="dfec7-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="dfec7-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="dfec7-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="dfec7-108">사용 가능한 [추가 플랜](https://aadsyncfabric.slack.com/pricing) 또는 개선을 사용한 Slack 테넌트</span><span class="sxs-lookup"><span data-stu-id="dfec7-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="dfec7-109">팀 관리자 권한이 있는 Slack의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="dfec7-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="dfec7-110">참고: Azure AD 프로비전 통합은 추가 플랜 또는 개선에서 Slack 팀이 이용 가능한 [Slack SCIM API](https://api.slack.com/scim)에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="dfec7-111">Slack에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="dfec7-111">Assigning users to Slack</span></span>

<span data-ttu-id="dfec7-112">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="dfec7-113">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="dfec7-114">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Slack 앱에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="dfec7-115">결정했으면 다음 지시에 따라 이러한 사용자를 Slack 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="dfec7-116">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="dfec7-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="dfec7-117">Slack에 사용자 할당을 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="dfec7-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="dfec7-118">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Slack에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="dfec7-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="dfec7-120">사용자를 Slack에 할당할 때 할당 대화 상자에서 **사용자** 또는 "그룹" 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="dfec7-121">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="dfec7-122">Slack에 사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="dfec7-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="dfec7-123">이 섹션에서는 사용자의 Azure AD를 Slack의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Slack에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="dfec7-124">**팁:** (Azure Portal) [ https://portal.azure.com ] 에 제공된 지침에 따라 Slack에 대해 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="dfec7-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="dfec7-126">Azure AD에서 Slack에 자동 사용자 계정 프로비전을 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="dfec7-127">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="dfec7-128">Single Sign-On에 대한 Slack을 이미 구성한 경우 검색 필드를 사용하여 Slack의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="dfec7-129">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Slack**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="dfec7-130">검색 결과에서 Slack을 선택하고 응용 프로그램의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="dfec7-131">Slack의 인스턴스를 선택한 다음, **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="dfec7-132">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Slack 프로비전](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="dfec7-134">**관리자 자격 증명** 섹션에서 **권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="dfec7-135">그러면 새 브라우저 창에서 Slack 권한 부여 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="dfec7-136">새 창에서 팀 관리자 계정을 사용하여 Slack에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="dfec7-137">표시된 권한 부여 대화 상자에서 프로비전을 사용하도록 설정하려는 Slack 팀을 선택한 다음, **권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="dfec7-138">완료되면 Azure Portal로 돌아가서 프로비전 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![권한 부여 대화 상자](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="dfec7-140">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Slack 앱에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="dfec7-141">연결에 실패하면 Slack 계정에 팀 관리자 권한이 있는지 확인하고 "권한 부여" 단계를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="dfec7-142">프로비전 오류 알림을 받을 개인 또는 그룹의 전자 메일 주소를 **알림 전자 메일** 필드에 입력하고 아래 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="dfec7-143">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-143">Click **Save**.</span></span> 

10) <span data-ttu-id="dfec7-144">매핑 섹션에서 **Azure Active Directory 사용자를 Slack에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="dfec7-145">**특성 매핑** 섹션에서 Azure AD에서 Slack로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="dfec7-146">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Slack의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="dfec7-147">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="dfec7-148">Slack에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="dfec7-149">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-149">Click **Save**.</span></span> 

<span data-ttu-id="dfec7-150">사용자 및 그룹 섹션에서 Slack에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="dfec7-151">초기 동기화는 서비스가 실행되는 동안 약 10분마다 발생하는 차후 동기화보다 수행하는 데 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="dfec7-152">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Slack 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="dfec7-153">[옵션] Slack에 그룹 개체 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="dfec7-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="dfec7-154">필요에 따라 Azure AD에서 Slack으로 그룹 개체의 프로비전을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="dfec7-155">이는 실제 멤버 외에도 실제 그룹 개체가 Azure AD에서 Slack으로 복제된다는 점에서 "사용자 그룹 할당"과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="dfec7-156">예를 들어, Azure AD에서 "내 그룹"이라는 그룹이 있는 경우 Slack 내에 "내 그룹"이라는 동일한 그룹이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="dfec7-157">그룹 개체 프로비전을 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="dfec7-158">매핑 섹션에서 **Azure Active Directory 그룹을 Slack에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="dfec7-159">특성 매핑 블레이드에서 사용을 예로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="dfec7-160">**특성 매핑** 섹션에서 Azure AD에서 Slack으로 동기화할 그룹 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="dfec7-161">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Slack의 그룹을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="dfec7-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-162">Click **Save**.</span></span>

<span data-ttu-id="dfec7-163">이제 **사용자 및 그룹** 섹션의 Slack에 할당된 모든 그룹 개체는 Azure AD에서 Slack으로 완전하게 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="dfec7-164">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Slack 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfec7-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dfec7-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="dfec7-165">Additional Resources</span></span>

* [<span data-ttu-id="dfec7-166">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="dfec7-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="dfec7-167">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="dfec7-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
