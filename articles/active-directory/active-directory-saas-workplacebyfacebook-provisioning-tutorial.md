---
title: "자습서: Workplace by Facebook과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Workplace by Facebook 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="ff917-103">자습서: 사용자 프로비전에 대한 Workplace by Facebook 구성</span><span class="sxs-lookup"><span data-stu-id="ff917-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="ff917-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Workplace by Facebook으로 자동으로 프로비전 및 프로비전 해제하도록 Workplace by Facebook 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff917-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ff917-105">Prerequisites</span></span>

<span data-ttu-id="ff917-106">Workplace by Facebook과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="ff917-107">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ff917-107">An Azure AD subscription</span></span>
- <span data-ttu-id="ff917-108">Workplace by Facebook Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ff917-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff917-109">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff917-110">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff917-111">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ff917-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff917-112">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ff917-113">Workplace by Facebook에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="ff917-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="ff917-114">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ff917-115">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ff917-116">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Workplace by Facebook 앱에 액세스해야 하는 사용자를 나타내는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="ff917-117">결정했으면 다음 지시에 따라 이러한 사용자를 Workplace by Facebook 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="ff917-118">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="ff917-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="ff917-119">Workplace by Facebook에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="ff917-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="ff917-120">단일 Azure AD 사용자를 Workplace by Facebook에 할당하여 프로비전 구성을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="ff917-121">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ff917-122">Workplace by Facebook에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="ff917-123">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ff917-124">사용자 프로비저닝 사용</span><span class="sxs-lookup"><span data-stu-id="ff917-124">Enable User Provisioning</span></span>

<span data-ttu-id="ff917-125">이 섹션에서는 사용자의 Azure AD를 Workplace by Facebook의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Workplace by Facebook에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ff917-126">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Workplace by Facebook에 SAML 기반 Single Sign-On을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ff917-127">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="ff917-128">Azure AD에서 Workplace by Facebook에 사용자 계정 프로비전을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="ff917-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="ff917-129">이 섹션의 목적은 Workplace by Facebook에 Active Directory 사용자 계정을 프로비전할 수 있도록 설정하는 방법을 간략하게 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="ff917-130">Azure AD는 할당된 사용자의 계정 세부 정보를 Workplace by Facebook에 자동으로 동기화하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="ff917-131">이 자동 동기화를 사용하면 Workplace by Facebook에서 사용자가 처음으로 로그인하기 전에 사용자에게 액세스 권한을 부여하는 데 필요한 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="ff917-132">또한 Azure AD에서 액세스가 취소되면 Workplace by Facebook에서 사용자 프로비전을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="ff917-133">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory** > **엔터프라이즈 앱** > **모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="ff917-134">이미 Workplace by Facebook에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Workplace by Facebook의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="ff917-135">그러지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Workplace by Facebook**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="ff917-136">검색 결과에서 Workplace by Facebook을 선택하고 응용 프로그램 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ff917-137">Workplace by Facebook의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ff917-138">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ff917-140">**관리자 자격 증명** 섹션 아래에 Workplace by Facebook 관리자의 테넌트 URL과 비밀 토큰을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="ff917-141">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Workplace by Facebook 앱에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="ff917-142">연결에 실패하면 Workplace by Facebook 계정에 팀 관리자 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="ff917-143">프로비전 오류 알림을 받을 개인 또는 그룹의 메일 주소를 **알림 메일** 필드에 입력하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="ff917-144">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-144">Click **Save.**</span></span>

9. <span data-ttu-id="ff917-145">[매핑] 섹션에서 **Synchronize Azure Active Directory Users to Workplace by Facebook**(Azure Active Directory 사용자를 Workplace by Facebook에 동기화)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="ff917-146">**특성 매핑** 섹션에서 Azure AD에서 Workplace by Facebook으로 동기화되는 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="ff917-147">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Workplace by Facebook의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="ff917-148">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="ff917-149">Workplace by Facebook에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="ff917-150">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-150">Click **Save.**</span></span>

<span data-ttu-id="ff917-151">자동 프로비전을 구성하는 방법에 대한 자세한 내용은 [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff917-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="ff917-152">이제 테스트 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-152">You can now create a test account.</span></span> <span data-ttu-id="ff917-153">이제 최대 20분 동안 기다린 후 계정이 Workplace by Facebook에 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff917-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff917-154">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ff917-154">Additional resources</span></span>

* [<span data-ttu-id="ff917-155">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="ff917-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff917-156">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ff917-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ff917-157">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ff917-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

