---
title: "셀프 서비스 응용 프로그램 액세스를 사용할 때 발생하는 문제 | Microsoft Docs"
description: "셀프 서비스 응용 프로그램 액세스와 관련된 문제 해결"
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
ms.reviewer: japere
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="d8127-103">셀프 서비스 응용 프로그램 액세스를 사용할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="d8127-103">Problem using self-service application access</span></span>

<span data-ttu-id="d8127-104">셀프 서비스 응용 프로그램 액세스는 사용자가 응용 프로그램을 직접 검색하도록 하고 경우에 따라 비즈니스 그룹이 해당 응용 프로그램에 대한 액세스를 승인하도록 허용하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="d8127-105">비즈니스 그룹이 해당 액세스 패널에서 암호 Single Sign-On 응용 프로그램 권한에 대해 해당 사용자에게 할당된 자격 증명을 관리하도록 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="d8127-106">사용자가 액세스 패널에서 응용 프로그램을 셀프 검색할 수 있도록 하려면 먼저 사용자가 셀프 검색을 수행하고 액세스 권한을 요청할 수 있게 하려는 모든 응용 프로그램에 대해 **셀프 서비스 응용 프로그램 액세스**를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="d8127-107">먼저 확인해야 할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="d8127-107">General issues to check first</span></span>

-   <span data-ttu-id="d8127-108">셀프 서비스 응용 프로그램 액세스가 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="d8127-109">“셀프 서비스 응용 프로그램 액세스 구성 방법”을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8127-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="d8127-110">사용자 또는 그룹이 셀프 서비스 응용 프로그램 액세스를 요청하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="d8127-111">사용자가 셀프 서비스 응용 프로그램 액세스를 위한 올바른 위치를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="d8127-112">사용자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)로 이동하고 **+ 추가** 단추를 클릭하여 셀프 서비스 액세스를 활성화한 앱을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="d8127-113">셀프 서비스 응용 프로그램 액세스를 최근에 구성한 경우 몇 분 후에 사용자 액세스 패널에 로그인했다가 다시 로그아웃하여 셀프 서비스 액세스 변경 내용이 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="d8127-114">셀프 서비스 응용 프로그램 액세스 구성 방법</span><span class="sxs-lookup"><span data-stu-id="d8127-114">How to configure self-service application access</span></span>

<span data-ttu-id="d8127-115">응용 프로그램에 대한 셀프 서비스 응용 프로그램 액세스를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="d8127-116">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d8127-117">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8127-118">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8127-119">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8127-120">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d8127-121">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d8127-122">셀프 서비스 액세스를 활성화하려는 응용 프로그램을 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="d8127-123">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **셀프 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d8127-124">이 응용 프로그램에 대한 셀프 서비스 응용 프로그램 액세스를 활성화하려면 **사용자가 이 응용 프로그램에 대한 액세스를 요청하도록 허용하시겠습니까?** 토글을 **예**로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="d8127-125">다음으로 이 응용 프로그램에 대한 액세스를 요청하는 사용자에 추가되어야 하는 그룹을 선택하려면 레이블 **할당된 사용자는 어느 그룹에 추가되어야 합니까?** 옆의 선택기를 클릭하고 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="d8127-126">**선택 사항:** 사용자의 액세스를 허용하기 전에 비즈니스 승인을 필요로 하려는 경우 **이 응용 프로그램에 대한 액세스를 부여하기 전에 승인이 필요합니까?** 토글을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="d8127-127">**선택 사항: 암호 Single Sign-On만을 사용하는 응용 프로그램의 경우** 해당 비즈니스 승인자가 승인된 사용자에 대한 이 응용 프로그램에 전송되는 암호를 지정하도록 허용하려는 경우 **승인자가 이 응용 프로그램에 대한 사용자의 암호를 설정하도록 허용하시겠습니까?** 토글을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="d8127-128">**선택 사항:** 이 응용 프로그램에 대한 액세스를 승인할 수 있는 비즈니스 승인자를 지정하려면 레이블 **이 응용 프로그램에 대한 액세스는 누가 승인할 수 있습니까?** 옆의 선택기를 클릭하여 최대 10명의 개별 비즈니스 승인자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="d8127-129">그룹은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="d8127-130">**선택 사항:** **역할을 표시하는 응용 프로그램의 경우** 셀프 서비스 승인된 사용자를 역할에 할당하려는 경우 **사용자를 이 응용 프로그램의 어떤 역할에 할당하시겠습니까?** 옆의 선택기를 클릭하여 이 사용자를 할당해야 하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="d8127-131">블레이드의 위쪽에서 **저장** 단추를 클릭하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="d8127-132">셀프 서비스 응용 프로그램 구성을 완료한 후 사용자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)로 이동하고 **+ 추가** 단추를 클릭하여 셀프 서비스 액세스를 활성화한 앱을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="d8127-133">비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="d8127-134">사용자가 승인이 필요한 응용 프로그램에 대한 액세스를 요청한 경우 비즈니스 승인자에게 알리는 메일을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="d8127-135">이러한 승인은 단일 승인 워크플로만 지원합니다. 즉, 여러 승인자를 지정하는 경우 모든 단일 승인자는 응용 프로그램에 대한 액세스를 승인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="d8127-136">이러한 문제 해결 단계로 문제가 해결되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="d8127-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="d8127-137">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8127-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="d8127-138">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="d8127-138">Correlation error ID</span></span>

-   <span data-ttu-id="d8127-139">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="d8127-139">UPN (user email address)</span></span>

-   <span data-ttu-id="d8127-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="d8127-140">TenantID</span></span>

-   <span data-ttu-id="d8127-141">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="d8127-141">Browser type</span></span>

-   <span data-ttu-id="d8127-142">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="d8127-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="d8127-143">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="d8127-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8127-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8127-144">Next steps</span></span>
[<span data-ttu-id="d8127-145">셀프 서비스 그룹 관리를 위한 Azure Active Directory 설정</span><span class="sxs-lookup"><span data-stu-id="d8127-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
