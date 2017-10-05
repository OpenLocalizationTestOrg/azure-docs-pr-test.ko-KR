---
title: "Azure 역할 기반 액세스 제어(RBAC)로 지원 요청을 만들고 관리하기 위한 액세스 권한 제어 | Microsoft Docs"
description: "Azure 역할 기반 액세스 제어(RBAC)로 지원 요청을 만들고 관리하기 위한 액세스 권한 제어"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="5afd9-103">Azure 역할 기반 액세스 제어(RBAC)로 지원 요청을 만들고 관리하기 위한 액세스 권한 제어</span><span class="sxs-lookup"><span data-stu-id="5afd9-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="5afd9-104">[RBAC(역할 기반 액세스 제어)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="5afd9-105">Azure Portal([portal.azure.com](https://portal.azure.com))에서 지원 요청 생성은 Azure의 RBAC 모델을 사용하여 지원 요청을 만들고 관리할 수 잇는 사용자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="5afd9-106">특정 범위(구독, 리소스 그룹 또는 리소스일 수 있음)에서 사용자, 그룹 및 응용 프로그램에 적절한 RBAC 역할을 할당하여 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="5afd9-107">예를 들어 보겠습니다. 구독 범위에서 읽기 권한이 있는 리소스 그룹 소유자는 해당 리소스 그룹의 모든 리소스(예: 웹 사이트, 가상 컴퓨터 및 서브넷)를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="5afd9-108">하지만 가상 컴퓨터 리소스에 대해 지원 요청을 생성하려고 하는 경우 다음 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![구독 오류](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="5afd9-110">지원 요청 관리에서는 구독 범위에서 지원 요청을 만들고 관리할 수 있도록 지원 작업 Microsoft.Support/*를 포함하는 역할 또는 쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="5afd9-111">다음 문서에서는 Azure의 RBAC(역할 기반 액세스 제어)를 사용하여 Azure Portal에서 지원 요청을 만들고 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5afd9-112">시작하기</span><span class="sxs-lookup"><span data-stu-id="5afd9-112">Getting Started</span></span>

<span data-ttu-id="5afd9-113">위의 예를 사용하여 구독 소유자에 의해 구독에 사용자 지정 RBAC 역할이 할당된 경우 리소스에 대한 지원 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="5afd9-114">Azure PowerShell, Azure 명령줄 인터페이스(CLI) 및 REST API를 사용하여 [사용자 지정 RBAC 역할](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="5afd9-115">사용자 지정 역할의 작업 속성은 해당 역할에 액세스 권한이 부여되는 Azure 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="5afd9-116">지원 요청 관리를 위한 사용자 지정 역할을 만들려면 역할에 Microsoft.Support/* 작업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="5afd9-117">지원 요청을 만들고 관리하는 데 사용할 수 있는 사용자 지정 역할 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="5afd9-118">이 역할을 "지원 요청 참여자"로 명명하고 이 문서에서 사용자 지정 역할을 이 용어로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="5afd9-119">[이 비디오](https://www.youtube.com/watch?v=-PaBaDmfwKI)에 간략히 설명된 단계에 따라 구독에 대해 사용자 지정 역할을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="5afd9-120">Azure Portal에서 지원 요청 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="5afd9-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="5afd9-121">예를 들어 보겠습니다. "Visual Studio MSDN 구독"의 소유자라고 합시다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="5afd9-122">Joe는 이 구독에서 일부 리소스 그룹에 대한 리소스 소유자인 여러분의 동료이며 구독에 대해 읽기 권한을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="5afd9-123">동료인 Joe가 이 구독 아래 리소스에 대한 지원 티켓을 만들고 관리할 수 있도록 액세스 권한을 부여하고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="5afd9-124">먼저 구독으로 이동하고 "설정" 아래에서 사용자 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="5afd9-125">구독에 대해 읽기 권한이 있는 Joe를 클릭하고 새 사용자 지정 역할을 할당해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![역할 추가](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="5afd9-127">"사용자" 블레이드에서 [추가]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="5afd9-128">역할 목록에서 사용자 지정 역할 "지원 요청 참여자"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![지원 참여자 역할 추가](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="5afd9-130">역할 이름을 선택한 후 "사용자 추가"를 클릭하고 Joe의 전자 메일 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="5afd9-131">[선택]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-131">Click "Select"</span></span>

    ![사용자 추가](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="5afd9-133">[확인]을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-133">Click "Ok" to proceed</span></span>

    ![액세스 권한 추가](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="5afd9-135">이제 자신의 소유인 구독 아래에 사용자 지정 역할 "지원 요청 참여자"가 새로 추가된 사용자를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![추가된 사용자](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="5afd9-137">Joe가 포털에 로그인하면 자신이 추가된 구독을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="5afd9-138">Joe는 "도움말 및 지원" 블레이드에서 "새 지원 요청"을 클릭하고 "Visual Studio Ultimate with MSDN"에 대한 지원 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![새 지원 요청](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="5afd9-140">"모든 요청을 지원"을 클릭 하면 Joe 목록을 볼 수는이 구독에 대해 생성 하는 지원 요청 ![경우 세부 정보 보기](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="5afd9-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="5afd9-141">Azure Portal에서 지원 요청 액세스 제거</span><span class="sxs-lookup"><span data-stu-id="5afd9-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="5afd9-142">사용자에게 지원 요청을 만들고 관리하기 위한 액세스 권한을 부여할 수 있었던 것처럼 사용자에 대한 액세스 권한을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="5afd9-143">지원 요청을 만들고 관리할 수 있는 기능을 제거하려면 구독으로 이동하고 "설정"을 클릭하고 사용자(이 경우, Joe)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="5afd9-144">역할 이름, "지원 요청 참여자"를 마우스 오른쪽 단추로 클릭하고 "제거"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![지원 요청 액세스 제거](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="5afd9-146">Joe가 포털에 로그인하고 지원 요청을 만들려고 하면 다음 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![구독 오류-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="5afd9-148">Joe가 "모든 지원 요청"을 클릭할 때 지원 요청을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5afd9-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![사례 정보 보기-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
