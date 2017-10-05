---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 ThousandEyes 구성 | Microsoft Docs"
description: "사용자 계정을 ThousandEyes로 자동으로 프로비전 및 프로비전 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다."
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: e6bc2eab3cc1adcf26857ed98d920177a51455ea
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="a061f-103">자습서: 자동 사용자 프로비전에 대한 ThousandEyes 구성</span><span class="sxs-lookup"><span data-stu-id="a061f-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="a061f-104">이 자습서의 목적은 사용자 계정을 Azure AD에서 ThousandEyes로 자동으로 프로비전 및 프로비전 해제하도록 ThousandEyes 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a061f-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a061f-105">Prerequisites</span></span>

<span data-ttu-id="a061f-106">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a061f-107">Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="a061f-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="a061f-108">[표준 계획](https://www.thousandeyes.com/pricing) 이상을 사용하도록 설정한 ThousandEyes 테넌트</span><span class="sxs-lookup"><span data-stu-id="a061f-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="a061f-109">관리자 권한이 있는 ThousandEyes의 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="a061f-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="a061f-110">Azure AD 프로비전 통합에서는 [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK)를 사용하며, 이 API는 ThousandEyes 팀이 표준 계획 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="a061f-111">ThousandEyes에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a061f-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="a061f-112">Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a061f-113">자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="a061f-114">프로비전 서비스를 구성하고 사용하도록 설정하기 전에 ThousandEyes 앱에 액세스해야 하는 사용자를 나타내는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="a061f-115">결정했으면 다음 지침에 따라 이러한 사용자를 ThousandEyes 앱에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="a061f-116">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="a061f-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="a061f-117">ThousandEyes에 사용자를 할당하기 위한 주요 팁</span><span class="sxs-lookup"><span data-stu-id="a061f-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="a061f-118">단일 Azure AD 사용자를 ThousandEyes에 할당하여 프로비전 구성을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="a061f-119">추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a061f-120">ThousandEyes에 사용자를 할당할 때 [할당] 대화 상자에서 **사용자** 역할이나 다른 유효한 응용 프로그램 관련 역할(사용 가능한 경우)을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="a061f-121">**기본 액세스** 역할은 프로비전에 적합하지 않으므로 이러한 사용자는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="a061f-122">ThousandEyes에 사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="a061f-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="a061f-123">이 섹션에서는 사용자의 Azure AD를 ThousandEyes의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 ThousandEyes에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a061f-124">[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 ThousandEyes에 대해 SAML 기반 Single Sign-On을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a061f-125">Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="a061f-126">Azure AD에서 ThousandEyes에 자동 사용자 계정 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="a061f-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="a061f-127">[Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="a061f-128">이미 ThousandEyes에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 ThousandEyes의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="a061f-129">그러지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **ThousandEyes**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="a061f-130">검색 결과에서 ThousandEyes를 선택하고 응용 프로그램 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a061f-131">ThousandEyes의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a061f-132">**프로비전 모드**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![ThousandEyes 프로비전](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="a061f-134">**관리자 자격 증명** 섹션 아래에 ThousandEyes 계정에서 생성한 **비밀 토큰**을 입력합니다(이 토큰은 ThousandEyes 계정의 **Security & Authentication**(보안 및 인증) 아래에서 확인할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="a061f-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes 프로비전](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="a061f-136">Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 ThousandEyes 앱에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="a061f-137">연결에 실패하면 ThousandEyes 계정에 관리자 권한이 있는지 확인하고 5단계를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="a061f-138">프로비전 오류 알림을 받을 개인 또는 그룹의 메일 주소를 **알림 메일** 필드에 입력하고 “오류가 발생할 경우 메일 알림 보내기” 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="a061f-139">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-139">Click **Save**.</span></span> 

9. <span data-ttu-id="a061f-140">[매핑] 섹션에서 **Synchronize Azure Active Directory Users to ThousandEyes**(Azure Active Directory 사용자를 ThousandEyes에 동기화)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="a061f-141">**특성 매핑** 섹션에서 Azure AD에서 ThousandEyes로 동기화되는 사용자 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="a061f-142">**일치** 속성으로 선택한 특성은 업데이트 작업 시 ThousandEyes의 사용자 계정을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="a061f-143">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a061f-144">ThousandEyes에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="a061f-145">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-145">Click **Save**.</span></span> 

<span data-ttu-id="a061f-146">[사용자 및 그룹] 섹션에서 ThousandEyes에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="a061f-147">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a061f-148">**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 링크를 클릭하여 프로비전 서비스에서 수행한 모든 작업을 설명하는 프로비전 작업 보고서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a061f-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="a061f-149">Azure AD 프로비전 로그를 읽는 방법에 대한 자세한 내용은 [자동 사용자 계정 프로비전에 대한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a061f-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a061f-150">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a061f-150">Additional resources</span></span>

* [<span data-ttu-id="a061f-151">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="a061f-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a061f-152">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a061f-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="a061f-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a061f-153">Next steps</span></span>

* <span data-ttu-id="a061f-154">[프로비전 활동에 대한 로그를 검토하고 보고서를 받아 보는 방법을 살펴봅니다](active-directory-saas-provisioning-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="a061f-154">[Learn how to review logs and get reports on provisioning activity](active-directory-saas-provisioning-reporting.md)</span></span>
