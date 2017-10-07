---
title: "Azure API 관리에서 그룹을 사용 하 여 aaaManage 개발자 계정을 | Microsoft Docs"
description: "어떻게 toomanage 개발자 계정을 사용 하 여 자세한 내용은 Azure API 관리에서 그룹"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="07e1b-103">Azure API 관리에서 사용 하 여 toocreate 그룹 toomanage 개발자 계정을 어떻게</span><span class="sxs-lookup"><span data-stu-id="07e1b-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="07e1b-104">API 관리 그룹은 제품 toodevelopers 사용 되는 toomanage hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="07e1b-105">제품을 만들어 놓은 첫 번째 표시 toogroups 및 개발자가 해당 그룹에서 보고 하 고 hello 그룹과 연결 된 toohello 제품을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="07e1b-106">API 관리 hello 변경할 수 없는 시스템 그룹 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="07e1b-107">**관리자** - Azure 구독 관리자가 이 그룹의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="07e1b-108">관리자 API 관리 서비스 인스턴스, 관리 Api, 작업 및 개발자가 사용 하는 제품 hello 만들기.</span><span class="sxs-lookup"><span data-stu-id="07e1b-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="07e1b-109">**개발자** - 인증된 개발자 포털 사용자가 이 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="07e1b-110">개발자는 Api를 사용 하 여 응용 프로그램을 구축 하는 hello 고객 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="07e1b-111">개발자는 toohello 개발자 포털 액세스 권한이 부여 된 하 고 API의 hello 작업을 호출 하는 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="07e1b-112">**게스트** -예:이 그룹에는 API 관리 인스턴스 년의 hello 개발자 포털을 방문 하는 잠재 고객의 개발자 포털 사용자가 인증 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="07e1b-113">Hello 기능 tooview Api와 같은 특정 읽기 전용 액세스를 부여할 수 되지만 호출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="07e1b-114">관리자 추가 toothese 시스템 그룹에 사용자 지정 그룹을 만들 수 있습니다 또는 [연결 된 Azure Active Directory 테 넌 트의 외부 그룹을 활용 하 여][leverage external groups in associated Azure Active Directory tenants]합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="07e1b-115">사용자 지정 그룹과 외부 그룹 개발자 가시성 제공 시스템 그룹과 함께 사용할 수 있으며 tooAPI 제품에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="07e1b-116">예를 들어 특정와 개발자가 파트너 조직 및의 액세스 허용 사용자 지정 그룹 하나 만들 수 있습니다 관련 Api만 포함 된 제품에서 Api toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="07e1b-117">사용자는 두 그룹 이상의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="07e1b-118">이 가이드에서는 API 관리 인스턴스의 관리자가 새 그룹을 추가하고 이 그룹과 새 제품 및 개발자를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="07e1b-119">또한 toocreating hello 게시자 포털에서 그룹 관리을 있습니다 수 만들고 hello API 관리 REST API를 사용 하 여 그룹 관리 [그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx) 엔터티.</span><span class="sxs-lookup"><span data-stu-id="07e1b-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="07e1b-120"><a name="create-group"> </a>그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="07e1b-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="07e1b-121">새 그룹을 toocreate 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="07e1b-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="07e1b-122">API 관리 게시자 포털 toohello 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-122">This takes you toohello API Management publisher portal.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="07e1b-124">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="07e1b-125">클릭 **그룹** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **그룹 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![새 그룹 추가][api-management-add-group]

<span data-ttu-id="07e1b-127">Hello 그룹 및 선택적 설명을 대 한 고유한 이름을 입력 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![새 그룹 추가][api-management-add-group-window]

<span data-ttu-id="07e1b-129">hello 그룹 탭 tooedit hello hello 새 그룹이 표시 됩니다 **이름** 또는 **설명** hello 그룹의 hello 목록의 hello 그룹의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="07e1b-130">toodelete hello 그룹에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-130">toodelete hello group, click **Delete**.</span></span>

![그룹 추가됨][api-management-new-group]

<span data-ttu-id="07e1b-132">Hello 그룹을 만든 했으므로 제품 및 개발자와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="07e1b-133"><a name="associate-group-product"> </a>그룹과 제품 연결</span><span class="sxs-lookup"><span data-stu-id="07e1b-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="07e1b-134">제품을 가진 그룹이 tooassociate 클릭 **제품** hello에서 **API 관리** hello에 메뉴 왼쪽과 hello 원하는 제품의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![표시 여부 설정][api-management-add-group-to-product]

<span data-ttu-id="07e1b-136">선택 hello **가시성** tooadd 탭 및 그룹 및 tooview hello hello 제품에 대 한 현재 그룹을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="07e1b-137">tooadd / 제거 그룹을 확인 하거나 hello 원하는 그룹 및 클릭에 대 한 hello 확인란의 선택을 취소 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![표시 여부 설정][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="07e1b-139">tooadd Azure Active Directory 그룹 참조 [tooauthorize 개발자 방법을 사용 하 여 계정을 Azure Active Directory를 Azure API 관리에서](api-management-howto-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="07e1b-140">hello tooconfigure 그룹 **가시성** 제품에 대 한 탭을 클릭 **그룹 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="07e1b-141">제품 그룹에 연결 되 고 나면 개발자가 해당 그룹에서 볼 수 있으며 toohello 제품 구독.</span><span class="sxs-lookup"><span data-stu-id="07e1b-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="07e1b-142"><a name="associate-group-developer"> </a>그룹과 개발자 연결</span><span class="sxs-lookup"><span data-stu-id="07e1b-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="07e1b-143">개발자 tooassociate 그룹 클릭 **사용자** hello에서 **API 관리** 왼쪽, hello 및 hello 개발자 옆의 확인란 hello에 메뉴 tooassociate 사용 하 여 원하는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![개발자 toogroup 추가][api-management-add-group-to-developer]

<span data-ttu-id="07e1b-145">Hello 원하는 개발자가 확인 되 면 클릭 hello에서 원하는 그룹 hello **tooGroup 추가** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="07e1b-146">개발자가 hello를 사용 하 여 그룹에서 제거할 수 **그룹에서 제거** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![개발자][api-management-add-group-to-developer-saved]

<span data-ttu-id="07e1b-148">Hello 개발자 및 hello 그룹 간의 hello 연결이 추가 되 면 hello에서 볼 수 있습니다 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="07e1b-149"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="07e1b-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="07e1b-150">개발자 tooa 그룹에 추가 되 면 확인 하 고 해당 그룹에 연결 된 toohello 제품을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e1b-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="07e1b-151">자세한 내용은 [Azure API Management에서 제품을 만들고 게시하는 방법][How create and publish a product in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e1b-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="07e1b-152">또한 toocreating hello 게시자 포털에서 그룹 관리을 있습니다 수 만들고 hello API 관리 REST API를 사용 하 여 그룹 관리 [그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx) 엔터티.</span><span class="sxs-lookup"><span data-stu-id="07e1b-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
