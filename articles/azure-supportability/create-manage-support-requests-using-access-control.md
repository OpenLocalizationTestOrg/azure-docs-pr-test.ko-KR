---
title: "역할 기반 액세스 제어 (RBAC) toocontrol aaaAzure 권한 toocreate를 액세스 하 고 지원 요청 관리 | Microsoft Docs"
description: "Azure 역할 기반 액세스 제어 (RBAC) toocontrol 권한 toocreate를 액세스 하 고 지원 요청 관리"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="0a4af-103">Azure 역할 기반 액세스 제어 (RBAC) toocontrol 권한 toocreate를 액세스 하 고 지원 요청 관리</span><span class="sxs-lookup"><span data-stu-id="0a4af-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="0a4af-104">[RBAC(역할 기반 액세스 제어)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="0a4af-105">Hello Azure 포털에서에서 요청을 만드는 지원 [portal.azure.com](https://portal.azure.com), 지원 요청을 관리 하 고 만들 수 있는 Azure의 RBAC 모델 toodefine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="0a4af-106">적절 한 RBAC 역할 toousers hello, 그룹 및 응용 프로그램에서 특정 범위를 구독, 리소스 그룹 또는 리소스를 할당 하 여 액세스가 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="0a4af-107">예를 들어 보겠습니다: 리소스 그룹 소유자는 읽기 권한이 있으면 hello 구독 범위에서 웹 사이트, 가상 컴퓨터 및 서브넷 같은 hello 리소스 그룹 아래의 모든 hello 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="0a4af-108">그러나 toocreate hello 가상 컴퓨터 리소스에 대 한 지원 요청을 시도할 때 발생 하면 다음 오류가 hello</span><span class="sxs-lookup"><span data-stu-id="0a4af-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![구독 오류](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="0a4af-110">지원 요청 관리에서 쓰기 권한이 필요 하거나 hello를 가지는 역할 Microsoft.Support/* hello toobe 수 toocreate 구독 범위에서 동작을 지원 하 고 지원 요청을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="0a4af-111">hello 다음 문서에서는 Azure의 사용자 지정 역할 기반 액세스 제어 (RBAC) toocreate를 사용 하 여 hello Azure 포털에서에서 지원 요청을 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0a4af-112">시작하기</span><span class="sxs-lookup"><span data-stu-id="0a4af-112">Getting Started</span></span>

<span data-ttu-id="0a4af-113">위의 hello 예제를 사용 하 여 것이 수 toocreate 지원 요청 리소스에 대 한 hello 구독 소유자가 사용자 지정 RBAC 역할 hello 구독에 할당 된 경우.</span><span class="sxs-lookup"><span data-stu-id="0a4af-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="0a4af-114">[사용자 지정 RBAC 역할](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) Azure PowerShell, Azure 명령줄 인터페이스 (CLI) 및 hello REST API를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="0a4af-115">사용자 지정 역할의 hello 작업 속성 hello Azure 작업 toowhich hello 역할에 대 한 액세스가 허용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="0a4af-116">지원 요청 관리에 대 한 사용자 지정 역할 toocreate hello 역할 hello 동작이 Microsoft.Support/* 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="0a4af-117">다음은 예제 toocreate를 사용 하 고 관리할 수는 사용자 지정 역할의 요청을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="0a4af-118">이 역할 "지원 요청 참가자" 이름을 지정한 우리 있고 언급할 toohello이이 문서에 사용자 지정 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

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

<span data-ttu-id="0a4af-119">에 설명 된 hello 단계에 따라 [이 비디오](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn 어떻게 toocreate 구독에 대 한 사용자 지정 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="0a4af-120">만들기 및 hello Azure 포털에서에서 지원 요청 관리</span><span class="sxs-lookup"><span data-stu-id="0a4af-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="0a4af-121">예를 들어 보겠습니다 – 구독 "Visual Studio MSDN 구독." hello 소유자 인 경우</span><span class="sxs-lookup"><span data-stu-id="0a4af-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="0a4af-122">Joe이이 구독에서 hello 리소스 그룹의 리소스 소유자 toosome 이며 대 한 읽기 권한이 toohello 구독 하 여 피어입니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="0a4af-123">Toogive 액세스 tooyour 피어를 Joe, hello 기능 toocreate 원하는 하 고이 정보를이 구독에 hello 리소스에 대 한 지원 티켓을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="0a4af-124">hello 첫 번째 단계는 toogo toohello 구독 하 고 "설정"에서 사용자의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="0a4af-125">Hello Joe hello 구독에 대해 판독기 액세스를 가진 사용자를 클릭 하 고 새 사용자 지정 역할 toohim 할당 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![역할 추가](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="0a4af-127">"추가" hello "Users" 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="0a4af-128">역할의 hello 목록에서 "지원 요청 참가자" hello 사용자 지정 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![지원 참여자 역할 추가](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="0a4af-130">역할 이름 hello를 선택한 후 "사용자 추가"를 클릭 하 고 hello Joe의 전자 메일 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="0a4af-131">[선택]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-131">Click "Select"</span></span>

    ![사용자 추가](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="0a4af-133">"확인" tooproceed 클릭</span><span class="sxs-lookup"><span data-stu-id="0a4af-133">Click "Ok" tooproceed</span></span>

    ![액세스 권한 추가](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="0a4af-135">이제 hello 새로 추가 된 사용자 지정 역할을 hello 소유자 인 경우 hello 구독 아래의 "지원 요청 참가자" hello 사용자 표시</span><span class="sxs-lookup"><span data-stu-id="0a4af-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![추가된 사용자](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="0a4af-137">Joe hello 포털에 로그인 할 때 추가 된 그 hello 구독 toowhich 그 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="0a4af-138">Joe는 hello "도움말 및 지원" 블레이드에서 "새로운 지원 요청"을 클릭 하 고 "Visual Studio Ultimate와 MSDN"에 대 한 지원 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![새 지원 요청](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="0a4af-140">"모든 요청을 지원"을 클릭 하면 Joe 목록을 볼 수 hello이이 구독에 대해 생성 하는 지원 요청 ![경우 세부 정보 보기](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="0a4af-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="0a4af-141">Hello Azure 포털에서에서 액세스를 요청 하는 지원을 제거합니다</span><span class="sxs-lookup"><span data-stu-id="0a4af-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="0a4af-142">가능한 toogrant 액세스 tooa 사용자 toocreate을 되 고 지원 요청 관리와 마찬가지로 hello 사용자도에 대 한 가능한 tooremove 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="0a4af-143">tooremove 기능 toocreate hello 및 지원 요청 관리 toohello 구독 이동, "설정"을 hello 사용자 (이 경우 Joe)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="0a4af-144">"지원 요청 참가자" hello 역할 이름을 마우스 오른쪽 단추로 클릭 하 고 "제거"를 클릭</span><span class="sxs-lookup"><span data-stu-id="0a4af-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![지원 요청 액세스 제거](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="0a4af-146">Hello 다음 오류가 발생 그 Joe toohello 포털에 로그인 하 toocreate 지원 요청을 시도 하는 경우</span><span class="sxs-lookup"><span data-stu-id="0a4af-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![구독 오류-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="0a4af-148">Joe가 "모든 지원 요청"을 클릭할 때 지원 요청을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4af-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![사례 정보 보기-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
