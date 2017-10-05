---
title: "셀프 서비스 응용 프로그램 할당을 구성하는 방법 | Microsoft Docs"
description: "셀프 서비스 응용 프로그램 액세스를 활성화하여 사용자가 자신의 응용 프로그램을 찾을 수 있도록 함"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7991dc19d41c5eb8e149c3ee08069e1a162929cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-self-service-application-assignment"></a><span data-ttu-id="33eff-103">셀프 서비스 응용 프로그램 할당을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="33eff-103">How to configure self-service application assignment</span></span>

<span data-ttu-id="33eff-104">사용자가 액세스 패널에서 응용 프로그램을 셀프 검색할 수 있도록 하려면 먼저 사용자가 셀프 검색을 수행하고 액세스 권한을 요청할 수 있게 하려는 모든 응용 프로그램에 대해 **셀프 서비스 응용 프로그램 액세스**를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="33eff-105">이 기능은 IT 그룹이 시간과 비용을 절감하는 유용한 방법이며, Azure Active Directory를 사용하는 최신 응용 프로그램 배포의 일부로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="33eff-106">이 기능을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="33eff-107">사용자가 IT 그룹의 도움 없이 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 응용 프로그램을 직접 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="33eff-108">액세스를 요청한 사용자가 누군지 알고, 액세스를 제거하고, 할당된 역할을 관리할 수 있도록 미리 구성된 그룹에 해당 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="33eff-109">필요에 따라 비즈니스 승인자가 응용 프로그램 액세스 요청을 승인할 수 있도록 합니다. 그러면 IT 그룹에서 이러한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="33eff-110">필요에 따라 이 응용 프로그램에 대한 액세스를 승인할 수 있는 최대 10명의 개별 사용자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="33eff-111">필요에 따라 해당 사용자가 응용 프로그램에 로그인하는 데 사용할 수 있는 암호를 비즈니스 승인자가 해당 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 바로 설정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="33eff-112">필요에 따라 자동으로 셀프 서비스 할당 사용자를 응용 프로그램 역할에 직접 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="33eff-113">셀프 서비스 응용 프로그램 액세스를 활성화하여 사용자가 자신의 응용 프로그램을 찾을 수 있도록 함</span><span class="sxs-lookup"><span data-stu-id="33eff-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="33eff-114">셀프 서비스 응용 프로그램 액세스는 사용자가 응용 프로그램을 직접 검색하도록 하고 경우에 따라 비즈니스 그룹이 해당 응용 프로그램에 대한 액세스를 승인하도록 허용하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="33eff-115">비즈니스 그룹이 해당 액세스 패널에서 암호 Single Sign-On 응용 프로그램 권한에 대해 해당 사용자에게 할당된 자격 증명을 관리하도록 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="33eff-116">응용 프로그램에 대한 셀프 서비스 응용 프로그램 액세스를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="33eff-117">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="33eff-118">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="33eff-119">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="33eff-120">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="33eff-121">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="33eff-122">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="33eff-123">셀프 서비스 액세스를 활성화하려는 응용 프로그램을 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="33eff-124">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **셀프 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="33eff-125">이 응용 프로그램에 대한 셀프 서비스 응용 프로그램 액세스를 활성화하려면 **사용자가 이 응용 프로그램에 대한 액세스를 요청하도록 허용하시겠습니까?** 토글을 **예**로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="33eff-126">다음으로 이 응용 프로그램에 대한 액세스를 요청하는 사용자에 추가되어야 하는 그룹을 선택하려면 레이블 **할당된 사용자는 어느 그룹에 추가되어야 합니까?** 옆의 선택기를 클릭하고 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="33eff-127">**선택 사항:** 사용자의 액세스를 허용하기 전에 비즈니스 승인을 필요로 하려는 경우 **이 응용 프로그램에 대한 액세스를 부여하기 전에 승인이 필요합니까?** 토글을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="33eff-128">**선택 사항: 암호 Single Sign-On만을 사용하는 응용 프로그램의 경우** 해당 비즈니스 승인자가 승인된 사용자에 대한 이 응용 프로그램에 전송되는 암호를 지정하도록 허용하려는 경우 **승인자가 이 응용 프로그램에 대한 사용자의 암호를 설정하도록 허용하시겠습니까?** 토글을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="33eff-129">**선택 사항:** 이 응용 프로그램에 대한 액세스를 승인할 수 있는 비즈니스 승인자를 지정하려면 레이블 **이 응용 프로그램에 대한 액세스는 누가 승인할 수 있습니까?** 옆의 선택기를 클릭하여 최대 10명의 개별 비즈니스 승인자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   >[!NOTE]
   ><span data-ttu-id="33eff-130">그룹은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-130">Groups are not supported.</span></span>
   >
   >

13. <span data-ttu-id="33eff-131">**선택 사항:** **역할을 표시하는 응용 프로그램의 경우** 셀프 서비스 승인된 사용자를 역할에 할당하려는 경우 **사용자를 이 응용 프로그램의 어떤 역할에 할당하시겠습니까?** 옆의 선택기를 클릭하여 이 사용자를 할당해야 하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="33eff-132">블레이드의 위쪽에서 **저장** 단추를 클릭하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="33eff-133">셀프 서비스 응용 프로그램 구성을 완료한 후 사용자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)로 이동하고 **+ 추가** 단추를 클릭하여 셀프 서비스 액세스를 활성화한 앱을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="33eff-134">비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="33eff-135">사용자가 승인이 필요한 응용 프로그램에 대한 액세스를 요청한 경우 비즈니스 승인자에게 알리는 메일을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="33eff-136">이러한 승인은 단일 승인 워크플로만 지원합니다. 즉, 여러 승인자를 지정하는 경우 모든 단일 승인자는 응용 프로그램에 대한 액세스를 승인합니다.</span><span class="sxs-lookup"><span data-stu-id="33eff-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33eff-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33eff-137">Next steps</span></span>
[<span data-ttu-id="33eff-138">셀프 서비스 그룹 관리를 위한 Azure Active Directory 설정</span><span class="sxs-lookup"><span data-stu-id="33eff-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
