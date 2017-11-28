---
title: "Azure Portal 대시보드 만들기 및 공유 | Microsoft Docs"
description: "이 문서에서는 Azure Portal에서 대시보드를 만들고 편집하는 방법을 설명합니다."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 5429e68723448ff5db6ef0ed8da1b927e97e6dd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-share-dashboards-in-the-azure-portal"></a><span data-ttu-id="b75f6-103">Azure Portal에서 대시보드 만들기 및 공유</span><span class="sxs-lookup"><span data-stu-id="b75f6-103">Create and share dashboards in the Azure portal</span></span>
<span data-ttu-id="b75f6-104">여러 개의 대시보드를 만들고 Azure 구독에 액세스할 수 있는 다른 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="b75f6-105">이 문서에서는 대시보드 만들기, 편집, 게시 및 액세스 관리의 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-105">This article goes through the basics of creating, editing, publishing, and managing access to dashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="b75f6-106">대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="b75f6-106">Create a dashboard</span></span>
<span data-ttu-id="b75f6-107">대시보드를 만들려면 현재 대시보드 이름 옆에 있는 **새 대시보드** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-107">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![대시보드 만들기](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="b75f6-109">이 작업은 새 비어 있는 개인 대시보드를 만들고 대시보드의 이름을 지정하고 타일을 추가하거나 다시 정렬할 수 있는 사용자 지정 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="b75f6-110">이 모드에서는 축소 가능한 타일 갤러리가 왼쪽 탐색 메뉴보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-110">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="b75f6-111">타일 갤러리를 사용하면 다양한 방법으로 Azure 리소스에 대한 타일을 찾을 수 있습니다. [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups), 리소스 형식, [태그](../azure-resource-manager/resource-group-using-tags.md) 또는 이름별로 리소스의 이름을 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-111">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![대시보드 사용자 지정](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="b75f6-113">타일을 원하는 대시보드 화면에 끌어서 놓아 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-113">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="b75f6-114">특정 리소스에 연결되지 않은 타일에 대한 **일반** 이라는 새 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="b75f6-115">이 예제에서는 Markdown 타일을 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-115">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="b75f6-116">이 타일을 사용하여 대시보드에 사용자 지정 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-116">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="b75f6-117">타일은 일반 텍스트인 [Markdown 구문](https://daringfireball.net/projects/markdown/syntax)및 제한된 일련의 HTML을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-117">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="b75f6-118">(안전을 위해 `<script>` 태그를 삽입하거나 포털을 방해할 수 있는 CSS의 특정 스타일 요소를 사용하는 등의 작업을 수행할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="b75f6-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![Markdown 추가](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="b75f6-120">대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="b75f6-120">Edit a dashboard</span></span>
<span data-ttu-id="b75f6-121">대시보드를 만든 후에 타일 갤러리 또는 블레이드의 타일 표현에서 타일을 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-121">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="b75f6-122">리소스 그룹의 표현을 고정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-122">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="b75f6-123">해당 항목을 검색할 때 또는 리소스 그룹 블레이드에서 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-123">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="b75f6-124">두 가지 방법은 리소스 그룹의 타일 표시를 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-124">Both approaches result in pinning the tile representation of the resource group.</span></span>

![대시보드에 고정](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="b75f6-126">항목을 고정한 후에 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-126">After pinning the item, it appears on your dashboard.</span></span>

![대시보드 보기](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="b75f6-128">Markdown 타일 및 대시보드에 고정된 리소스 그룹이 있으므로 타일의 크기를 조정하고 적합한 레이아웃으로 다시 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-128">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="b75f6-129">"..."에 마우스를 가져가고 선택하거나 타일을 마우스 오른쪽 단추로 클릭하여 해당 타일에 대한 상황에 맞는 모든 명령을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-129">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="b75f6-130">기본적으로 두 가지 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-130">By default, there are two items:</span></span>

1. <span data-ttu-id="b75f6-131">**대시보드에서 고정 해제** – 대시보드에서 타일을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-131">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="b75f6-132">**사용자 지정** – 사용자 지정 모드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-132">**Customize** – enters customize mode</span></span>

![타일 사용자 지정](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="b75f6-134">사용자 지정을 선택하여 타일의 크기를 조정하고 순서를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="b75f6-135">타일 크기를 조정하려면 다음 이미지에 나와 있는 것처럼 상황에 맞는 메뉴에서 새 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-135">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![타일 크기 조정](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="b75f6-137">또는 타일이 모든 크기를 지원하는 경우 하단 오른쪽 모서리를 원하는 크기로 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-137">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![타일 크기 조정](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="b75f6-139">타일의 크기를 조정한 후에 대시보드를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-139">After resizing tiles, view the dashboard.</span></span>

![타일 보기](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="b75f6-141">대시보드의 사용자 지정을 완료한 후에 사용자 지정 모드를 종료하려면 **사용자 지정 완료**를 선택하거나 상황에 맞는 메뉴에서 **사용자 지정 완료**를 마우스 오른쪽 단추로 클릭하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-141">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="b75f6-142">대시보드 게시 및 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="b75f6-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="b75f6-143">대시보드를 만들 때 기본적으로 비공개입니다. 즉, 볼 수 있는 유일한 사람은 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-143">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="b75f6-144">다른 사람이 볼 수 있도록 하려면 다른 대시보드 명령 옆에 나타나는 **공유** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-144">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![대시보드 공유](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="b75f6-146">게시하려는 대시보드에 대한 구독 및 리소스 그룹을 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-146">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="b75f6-147">에코시스템에 대시보드를 매끄럽게 통합하기 위해 공유 대시보드를 Azure 리소스로 구현했습니다(따라서 전자 메일 주소를 입력하여 공유할 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="b75f6-147">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="b75f6-148">포털에서 대부분 타일에 표시되는 정보에 대한 액세스는 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-148">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="b75f6-149">액세스 제어 관점에서 공유 대시보드는 가상 컴퓨터 또는 저장소 계정과 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="b75f6-150">Azure 구독을 보유하고 구독의 **소유자**, **참여자** 또는 **읽기 권한자** 역할에 할당된 팀의 구성원이 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-150">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="b75f6-151">소유자 또는 참여자인 사용자는 해당 구독 내에서 대시보드를 나열, 보기, 만들기, 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-151">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="b75f6-152">읽기 권한자인 사용자는 대시보드를 나열 및 볼 수 있지만 수정 또는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-152">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="b75f6-153">읽기 권한자 액세스를 보유한 사용자는 공유 대시보드에 대한 로컬 편집을 만들 수 있지만 해당 변경 내용을 서버로 다시 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-153">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="b75f6-154">그러나 사용하기 위해 대시보드의 개인 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-154">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="b75f6-155">늘 그렇듯이 대시보드의 개별 타일은 해당하는 리소스에 따라 고유한 액세스 제어 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-155">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="b75f6-156">편의를 위해 포털의 게시 환경에서는 **대시보드**라는 리소스 그룹에 대시보드를 배치한 위치의 패턴을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-156">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![대시보드 게시](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="b75f6-158">또한 특정 리소스 그룹에 대시보드를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-158">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="b75f6-159">해당 대시보드에 대한 액세스 제어는 리소스 그룹에 대한 액세스 제어와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-159">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="b75f6-160">해당 리소스 그룹에서 리소스를 관리할 수 있는 사용자는 대시보드에도 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-160">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![리소스 그룹에 대시보드 게시](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="b75f6-162">대시보드를 게시한 후에 **공유 + 액세스** 제어 창이 새로 고쳐지고 대시보드에 대한 사용자 액세스를 관리하는 링크를 포함하여 게시된 대시보드에 대한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-162">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="b75f6-163">이 링크는 Azure 리소스에 대한 액세스를 관리하는 데 사용되는 표준 역할 기반 액세스 제어 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-163">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="b75f6-164">언제든지 **공유**를 선택하여 이 보기로 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b75f6-164">You can always get back to this view by selecting **Share**.</span></span>

![액세스 제어 관리](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="b75f6-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b75f6-166">Next steps</span></span>
* <span data-ttu-id="b75f6-167">리소스를 관리하려면 [포털을 통한 Azure 리소스 관리](../azure-resource-manager/resource-group-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b75f6-167">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="b75f6-168">리소스를 배포하려면 [Resource Manager 템플릿 및 Azure Portal을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b75f6-168">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

