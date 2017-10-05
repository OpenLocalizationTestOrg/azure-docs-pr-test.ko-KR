---
title: "자습서: Citrix GoToMeeting과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 Citrix GoToMeeting 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="b02b4-103">자습서: 자동 사용자 프로비전에 대한 Citrix GoToMeeting 구성</span><span class="sxs-lookup"><span data-stu-id="b02b4-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="b02b4-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 Citrix GoToMeeting으로 자동으로 프로비전 및 프로비전 해제하도록 Citrix GoToMeeting 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b02b4-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b02b4-105">Prerequisites</span></span>

<span data-ttu-id="b02b4-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="b02b4-107">Azure Active Directory 테넌트.</span><span class="sxs-lookup"><span data-stu-id="b02b4-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b02b4-108">Citrix GoToMeeting Single Sign-On이 설정된 구독.</span><span class="sxs-lookup"><span data-stu-id="b02b4-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="b02b4-109">팀 관리자 권한이 있는 Citrix GoToMeeting의 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="b02b4-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="b02b4-110">Citrix GoToMeeting에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b02b4-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="b02b4-111">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b02b4-112">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b02b4-113">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Citrix GoToMeeting 앱에 대한 액세스가 필요한 사용자를 대표하는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="b02b4-114">결정했으면 다음 지시에 따라 이러한 사용자를 Citrix GoToMeeting 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="b02b4-115">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="b02b4-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="b02b4-116">Citrix GoToMeeting에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="b02b4-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="b02b4-117">프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Citrix GoToMeeting에 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="b02b4-118">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b02b4-119">Citrix GoToMeeting에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="b02b4-120">"기본 액세스" 역할은 프로비전에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="b02b4-121">자동 사용자 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="b02b4-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="b02b4-122">이 섹션에서는 사용자의 Azure AD를 Citrix GoToMeeting의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Citrix GoToMeeting에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b02b4-123">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Citrix GoToMeeting에 대해 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b02b4-124">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="b02b4-125">자동 사용자 계정 프로비전을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="b02b4-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="b02b4-126">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b02b4-127">Single Sign-On에 대한 Citrix GoToMeeting을 이미 구성한 경우 검색 필드를 사용하여 Citrix GoToMeeting의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="b02b4-128">그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Citrix GoToMeeting**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="b02b4-129">검색 결과에서 Citrix GoToMeeting을 선택하고 응용 프로그램의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="b02b4-130">Citrix GoToMeeting의 인스턴스를 선택한 다음, **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="b02b4-131">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![프로비전](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b02b4-133">관리자 자격 증명 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="b02b4-134">a.</span><span class="sxs-lookup"><span data-stu-id="b02b4-134">a.</span></span> <span data-ttu-id="b02b4-135">**Citrix GoToMeeting 관리자 사용자 이름** 텍스트 상자에서 관리자의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="b02b4-136">b.</span><span class="sxs-lookup"><span data-stu-id="b02b4-136">b.</span></span> <span data-ttu-id="b02b4-137">**Citrix GoToMeeting 관리자 암호** 텍스트 상자에서 관리자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="b02b4-138">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Citrix GoToMeeting 앱에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="b02b4-139">연결에 실패하면 Citrix GoToMeeting 계정에 팀 관리자 권한이 있는지 확인하고 **"관리자 자격 증명"** 단계를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="b02b4-140">프로비전 오류 알림을 받을 개인 또는 그룹의 메일 주소를 **알림 메일** 필드에 입력하고 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="b02b4-141">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-141">Click **Save.**</span></span>

9. <span data-ttu-id="b02b4-142">[매핑] 섹션에서 **Azure Active Directory 사용자를 Citrix GoToMeeting에 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="b02b4-143">**특성 매핑** 섹션에서 Azure AD에서 Citrix GoToMeeting으로 동기화할 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="b02b4-144">**일치** 속성으로 선택한 특성은 업데이트 작업 시 Citrix GoToMeeting의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="b02b4-145">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="b02b4-146">Citrix GoToMeeting에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 [설정] 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="b02b4-147">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-147">Click **Save.**</span></span>

<span data-ttu-id="b02b4-148">[사용자 및 그룹] 섹션에서 Citrix GoToMeeting에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="b02b4-149">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="b02b4-150">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Citrix GoToMeeting 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02b4-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b02b4-151">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b02b4-151">Additional resources</span></span>

* [<span data-ttu-id="b02b4-152">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="b02b4-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b02b4-153">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b02b4-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b02b4-154">Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b02b4-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


