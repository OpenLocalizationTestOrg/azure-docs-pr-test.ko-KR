---
title: "자습서: Jive와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Jive 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="474d6-103">자습서: 사용자 프로비전에 대한 Jive 구성</span><span class="sxs-lookup"><span data-stu-id="474d6-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="474d6-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Jive로 자동으로 프로비전 및 프로비전 해제하도록 Jive 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="474d6-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="474d6-105">Prerequisites</span></span>

<span data-ttu-id="474d6-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="474d6-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="474d6-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="474d6-108">Jive Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="474d6-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="474d6-109">팀 관리자 권한이 있는 Jive의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="474d6-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="474d6-110">Jive에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="474d6-110">Assigning users to Jive</span></span>

<span data-ttu-id="474d6-111">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="474d6-112">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="474d6-113">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Jive 앱에 액세스해야 하는 사용자를 나타내는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="474d6-114">결정했으면 다음 지침에 따라 이러한 사용자를 Jive 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="474d6-115">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="474d6-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="474d6-116">Jive에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="474d6-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="474d6-117">단일 Azure AD 사용자를 Jive에 할당하여 프로비전 구성을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="474d6-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="474d6-119">Jive에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="474d6-120">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="474d6-121">사용자 프로비저닝 사용</span><span class="sxs-lookup"><span data-stu-id="474d6-121">Enable User Provisioning</span></span>

<span data-ttu-id="474d6-122">이 섹션에서는 사용자의 Azure AD를 Jive의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Jive에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="474d6-123">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Jive에 대해 SAML 기반 Single Sign-On을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="474d6-124">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="474d6-125">사용자 계정 프로비전을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="474d6-125">To configure user account provisioning:</span></span>

<span data-ttu-id="474d6-126">이 섹션에서는 Jive에 Active Directory 사용자 계정을 프로비저닝할 수 있도록 설정하는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="474d6-127">이 절차의 일부로 Jive.com에 요청해야 하는 사용자 보안 토큰을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="474d6-128">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="474d6-129">이미 Jive에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Jive의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="474d6-130">그러지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Jive**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="474d6-131">검색 결과에서 Jive를 선택하고 응용 프로그램 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="474d6-132">Jive의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="474d6-133">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="474d6-135">**관리자 자격 증명** 섹션에서 다음 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="474d6-136">a.</span><span class="sxs-lookup"><span data-stu-id="474d6-136">a.</span></span> <span data-ttu-id="474d6-137">**Jive 관리자 사용자 이름** 텍스트 상자에서 Jive.com에서 할당된 **시스템 관리자** 프로필을 가진 Jive 계정 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="474d6-138">b.</span><span class="sxs-lookup"><span data-stu-id="474d6-138">b.</span></span> <span data-ttu-id="474d6-139">**Jive 관리자 암호** 텍스트 상자에 이 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="474d6-140">c.</span><span class="sxs-lookup"><span data-stu-id="474d6-140">c.</span></span> <span data-ttu-id="474d6-141">**Jive 테넌트 URL** 텍스트 상자에 Jive 테넌트 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="474d6-142">Jive 테넌트 URL은 조직에서 Jive에 로그인할 때 사용하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="474d6-143">일반적으로 URL 형식은 **www.\<organization\>.jive.com**입니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="474d6-144">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Jive 앱에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="474d6-145">프로비전 오류 알림을 받을 개인 또는 그룹의 전자 메일 주소를 **알림 전자 메일** 필드에 입력하고 아래 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="474d6-146">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-146">Click **Save.**</span></span>

9. <span data-ttu-id="474d6-147">[매핑] 섹션에서 **Synchronize Azure Active Directory Users to Jive**(Azure Active Directory 사용자를 Jive에 동기화)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="474d6-148">**특성 매핑** 섹션에서 Azure AD에서 Jive로 동기화되는 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="474d6-149">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Jive의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="474d6-150">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="474d6-151">Jive에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 [설정] 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="474d6-152">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-152">Click **Save.**</span></span>

<span data-ttu-id="474d6-153">[사용자 및 그룹] 섹션에서 Jive에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="474d6-154">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="474d6-155">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 링크를 클릭하여 Jive 앱의 프로비전 서비스에서 수행한 모든 작업을 설명하는 프로비전 작업 보고서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="474d6-156">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-156">You can now create a test account.</span></span> <span data-ttu-id="474d6-157">이제 최대 20분 동안 기다린 후 계정이 Jive에 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="474d6-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="474d6-158">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="474d6-158">Additional resources</span></span>

* [<span data-ttu-id="474d6-159">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="474d6-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="474d6-160">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="474d6-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="474d6-161">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="474d6-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)