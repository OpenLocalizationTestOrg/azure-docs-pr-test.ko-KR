---
title: "Azure API Management에서 그룹을 사용하여 개발자 계정 관리 | Microsoft Docs"
description: "Azure API 관리에서 그룹을 사용하여 개발자 계정을 관리하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="4600d-103">Azure API 관리에서 개발자 계정을 관리하는 그룹을 만들고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4600d-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="4600d-104">API 관리에서 그룹은 개발자에 대한 제품 표시 여부를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="4600d-105">제품이 먼저 그룹에 표시된 다음, 이러한 그룹의 개발자가 그룹과 연결된 제품을 보고 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="4600d-106">API 관리에는 다음과 같은 변경할 수 없는 시스템 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="4600d-107">**관리자** - Azure 구독 관리자가 이 그룹의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="4600d-108">관리자는 API 관리 서비스 인스턴스를 관리하며 개발자가 사용하는 API, 작업 및 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="4600d-109">**개발자** - 인증된 개발자 포털 사용자가 이 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="4600d-110">개발자는 API를 사용하여 응용 프로그램을 빌드하는 고객입니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="4600d-111">개발자는 개발자 포털에 액세스할 수 있는 권한을 받으며 API의 작업을 호출하는 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="4600d-112">**게스트** - API 관리 인스턴스의 개발자 포털을 방문하는 인증되지 않은 개발자 포털 사용자(예: 잠재 고객)가 이 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="4600d-113">예를 들어 API를 볼 수 있지만 호출할 수는 없는 기능과 같이 특정 읽기 전용 액세스 권한을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="4600d-114">이러한 시스템 그룹 외에도 관리자는 사용자 지정 그룹을 만들거나 [연관된 Azure Active Directory 테넌트에서 외부 그룹을 가져올 수 있습니다][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="4600d-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="4600d-115">사용자 지정 및 외부 그룹은 시스템 그룹과 함께 사용되어 개발자에게 API 제품에 대한 표시 여부 및 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="4600d-116">예를 들어, 특정 파트너 조직과 관련된 개발자를 위한 하나의 사용자 지정 그룹을 만들고 관련 API만을 포함한 제품에서 API에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="4600d-117">사용자는 두 그룹 이상의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="4600d-118">이 가이드에서는 API 관리 인스턴스의 관리자가 새 그룹을 추가하고 이 그룹과 새 제품 및 개발자를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="4600d-119">게시자 포털에서 그룹 만들기 및 관리 외에도 API 관리 REST API [그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx) 엔터티를 사용하여 그룹을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="4600d-120"><a name="create-group"> </a>그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="4600d-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="4600d-121">새 그룹을 만들려면 API 관리 서비스에 대해 Azure Portal에서 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="4600d-122">API 관리 게시자 포털로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-122">This takes you to the API Management publisher portal.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="4600d-124">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4600d-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4600d-125">왼쪽의 **API Management** 메뉴에서 **그룹**을 클릭한 다음 **그룹 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![새 그룹 추가][api-management-add-group]

<span data-ttu-id="4600d-127">그룹의 고유한 이름 및 선택적 설명을 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![새 그룹 추가][api-management-add-group-window]

<span data-ttu-id="4600d-129">새 그룹이 그룹 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="4600d-130">그룹의 **이름** 또는 **설명**을 편집하려면 목록의 그룹 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="4600d-131">그룹을 삭제하려면 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-131">To delete the group, click **Delete**.</span></span>

![그룹 추가됨][api-management-new-group]

<span data-ttu-id="4600d-133">그룹이 생성되었으므로, 제품 및 개발자와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="4600d-134"><a name="associate-group-product"> </a>그룹과 제품 연결</span><span class="sxs-lookup"><span data-stu-id="4600d-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="4600d-135">그룹과 제품을 연결하려면 왼쪽의 **API Management** 메뉴에서 **제품**을 클릭한 다음, 원하는 제품의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![표시 여부 설정][api-management-add-group-to-product]

<span data-ttu-id="4600d-137">**표시 여부** 탭을 선택하여 그룹을 추가 및 제거하고, 제품에 대한 현재 그룹을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="4600d-138">그룹을 추가 또는 제거하려면 원하는 그룹의 확인란을 선택하거나 선택 취소하고 **저장**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="4600d-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![표시 여부 설정][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="4600d-140">Azure Active Directory 그룹을 추가하려면 [Azure API 관리에서 Azure Active Directory를 사용하여 개발자 계정에 권한을 부여하는 방법](api-management-howto-aad.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4600d-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="4600d-141">제품에 대한 **표시 여부** 탭에서 그룹을 구성하려면 **그룹 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="4600d-142">제품이 그룹과 연결되면 그룹의 개발자가 제품을 보고 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="4600d-143"><a name="associate-group-developer"> </a>그룹과 개발자 연결</span><span class="sxs-lookup"><span data-stu-id="4600d-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="4600d-144">그룹과 개발자를 연결하려면 왼쪽의 **API Management** 메뉴에서 **사용자**를 클릭한 다음 그룹과 연결할 개발자 옆의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![그룹에 개발자 추가][api-management-add-group-to-developer]

<span data-ttu-id="4600d-146">원하는 개발자를 선택한 후 **그룹에 추가** 드롭다운에서 원하는 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="4600d-147">**그룹에서 제거** 드롭다운을 사용하여 그룹에서 개발자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![개발자][api-management-add-group-to-developer-saved]

<span data-ttu-id="4600d-149">개발자와 그룹 간의 연결을 추가한 후에는 **사용자** 탭에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="4600d-150"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="4600d-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="4600d-151">그룹에 개발자를 추가하면 개발자가 해당 그룹과 연결된 제품을 보고 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="4600d-152">자세한 내용은 [Azure API Management에서 제품을 만들고 게시하는 방법][How create and publish a product in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4600d-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="4600d-153">게시자 포털에서 그룹 만들기 및 관리 외에도 API 관리 REST API [그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx) 엔터티를 사용하여 그룹을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4600d-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
