---
title: "aaaCreate 및 Azure 포털 대시보드를 공유 | Microsoft Docs"
description: "이 문서에서 toocreate 및 편집 대시보드 Azure 포털 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="11bab-103">만들고 hello Azure 포털의에서 대시보드 공유</span><span class="sxs-lookup"><span data-stu-id="11bab-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="11bab-104">여러 개의 대시보드를 만들고 액세스 tooyour Azure 권한이 있는 다른 사용자와 공유할 수 있습니다 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="11bab-105">이 문서 작성, 편집, 게시, 및 액세스 toodashboards 관리의 기본 사항 hello 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="11bab-106">대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="11bab-106">Create a dashboard</span></span>
<span data-ttu-id="11bab-107">toocreate 대시보드를 선택 하는 hello **새 대시보드** 단추 다음 toohello 현재 대시보드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![대시보드 만들기](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="11bab-109">이 작업은 새 비어 있는 개인 대시보드를 만들고 대시보드의 이름을 지정하고 타일을 추가하거나 다시 정렬할 수 있는 사용자 지정 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="11bab-110">이 모드에서는 축소 가능한 hello 갤러리 사용 hello 왼쪽된 탐색 메뉴를 통해 바둑판식 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="11bab-111">hello 타일 갤러리 사용 하면 다양 한 방법으로 Azure 리소스에 대 한 타일을 찾을: 여 찾아볼 수 있습니다 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups), 만든 사람으로 리소스 종류가 [태그](../azure-resource-manager/resource-group-using-tags.md), 또는 리소스에 대 한 이름으로 검색 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![대시보드 사용자 지정](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="11bab-113">끌어서 원하는 위치로 hello 대시보드 화면에 놓으면 하 여 타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="11bab-114">특정 리소스에 연결되지 않은 타일에 대한 **일반** 이라는 새 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="11bab-115">이 예제에서는 hello Markdown 타일을 고정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="11bab-116">이 타일 tooadd 사용자 지정 콘텐츠 tooyour 대시보드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="11bab-117">hello 타일 지원 일반 텍스트 [마크 다운 구문](https://daringfireball.net/projects/markdown/syntax), 및 HTML의 제한 된 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="11bab-118">(삽입 하는 등의 작업을 수행할 수 없습니다 안전을 `<script>` 태그를 삽입 하거나 hello 포털을 방해할 수 있는 CSS의 특정 스타일 요소를 사용 하 여.)</span><span class="sxs-lookup"><span data-stu-id="11bab-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![Markdown 추가](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="11bab-120">대시보드 편집</span><span class="sxs-lookup"><span data-stu-id="11bab-120">Edit a dashboard</span></span>
<span data-ttu-id="11bab-121">대시보드를 만든 후 hello 타일 갤러리 또는 블레이드 hello 타일 표현에서 타일을 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="11bab-122">리소스 그룹의 hello 표현을 고정 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="11bab-123">항목, 또는 hello 리소스 그룹 블레이드에서 hello를 검색할 때를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="11bab-124">두 방법 모두 결과적 hello 리소스 그룹의 타일 표현 hello를 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![Pin toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="11bab-126">Hello 항목을 고정 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-126">After pinning hello item, it appears on your dashboard.</span></span>

![대시보드 보기](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="11bab-128">Markdown 타일 및 리소스 그룹 toohello 고정 된 대시보드를 만들었으므로 이제 해당 크기를 조정 하거나 다시 hello 타일 적합 한 레이아웃으로 정렬할 수 म 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="11bab-129">포인터를 두면 및 "..." 선택 하거나 타일을 마우스 오른쪽 단추로 클릭 하 여 해당 타일에 대 한 모든 hello 상황에 맞는 명령을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="11bab-130">기본적으로 두 가지 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-130">By default, there are two items:</span></span>

1. <span data-ttu-id="11bab-131">**대시보드에서 고정 해제** – hello 대시보드에서 hello 타일 제거</span><span class="sxs-lookup"><span data-stu-id="11bab-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="11bab-132">**사용자 지정** – 사용자 지정 모드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-132">**Customize** – enters customize mode</span></span>

![타일 사용자 지정](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="11bab-134">사용자 지정을 선택하여 타일의 크기를 조정하고 순서를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="11bab-135">hello 다음 이미지와 같이 hello 상황에 맞는 메뉴에서 새 크기를 hello 하는 tooresize 타일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![타일 크기 조정](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="11bab-137">하거나 hello 타일 모든 크기를 지 원하는 경우 hello 맨 아래 오른쪽 모서리 toohello 원하는 크기를 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![타일 크기 조정](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="11bab-139">타일의 크기를 조정한 후 hello 대시보드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-139">After resizing tiles, view hello dashboard.</span></span>

![타일 보기](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="11bab-141">대시보드를 사용자 지정 작업을 완료 되 면 hello를 선택 하기만 하면 **사용자 지정 작업은 수행** tooexit 사용자 지정 모드로 마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 지정 작업은 수행** hello 상황에 맞는 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="11bab-142">대시보드 게시 및 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="11bab-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="11bab-143">대시보드를 만들 때에 것을 볼 수 있는 유일한 사용자 hello 즉 기본적으로 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="11bab-144">toomake 것 표시 tooothers hello를 사용 하 여 **공유** 단추 옆에 나타나는 hello 다른 대시보드 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![대시보드 공유](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="11bab-146">Toochoose 대시보드 toobe에 대 한 구독 및 리소스 그룹에 게시는 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="11bab-147">tooseamlessly hello 에코 시스템에 대시보드를 통합, (전자 메일 주소를 입력 하 여 공유할 수 없습니다) 하므로 공유 대시보드 Azure 리소스 그룹으로 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="11bab-148">대부분의 hello 타일 hello 포털에 표시 되는 액세스 toohello 정보에 따라 관리 됩니다 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="11bab-149">액세스 제어 관점에서 공유 대시보드는 가상 컴퓨터 또는 저장소 계정과 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="11bab-150">Azure 구독이 있어야 하 고 팀 멤버의 hello 역할 할당 된 가정해 **소유자**, **참가자**, 또는 **판독기** hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="11bab-151">소유자 또는 참가자 인 사용자는 수 toolist, 보기, 만들기, 수정 또는 해당 구독 내에서 대시보드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="11bab-152">판독기 인 사용자 수 toolist 및 view 대시보드는 있지만 수정 또는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="11bab-153">판독기 액세스 권한이 있는 사용자 수 toomake 로컬 편집 내용을 tooa 공유 대시보드, 있지만 이러한 변경 내용을 다시 toohello 서버 수 없습니다. toopublish 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="11bab-154">그러나 자신의 용도 대 한 hello 대시보드의 전용 복사본을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="11bab-155">늘 그렇듯이 hello 대시보드에서 각 타일에 해당 하는 hello 리소스에 따라 자신의 액세스 제어 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="11bab-156">Hello 포털의 대시보드 리소스 그룹에 배치 하는 위치 패턴이 쪽으로 호출한 환경 가이드 편의 위해 게시 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![대시보드 게시](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="11bab-158">또한 대시보드 tooa 특정 리소스 그룹 toopublish를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="11bab-159">해당 대시보드에 대 한 액세스 제어 hello hello 리소스 그룹에 대 한 액세스 제어 hello와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="11bab-160">해당 리소스 그룹의 hello 리소스를 관리할 수 있는 사용자가 액세스 toohello 대시보드를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![대시보드 tooresource 그룹 게시](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="11bab-162">대시보드를 게시 한 후 hello **공유 + 액세스** 제어 창 새로 고침 되며 hello 게시 된 대시보드를 링크 toomanage 사용자 액세스 toohello 대시보드 포함 하는 방법에 대 한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="11bab-163">이 링크는 hello 표준 역할 기반 액세스 제어 사용 블레이드 toomanage에 대 한 액세스 모든 Azure 리소스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="11bab-164">돌아갈 수 있습니다 항상 toothis 보기를 선택 하 여 **공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-164">You can always get back toothis view by selecting **Share**.</span></span>

![액세스 제어 관리](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="11bab-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11bab-166">Next steps</span></span>
* <span data-ttu-id="11bab-167">toomanage 리소스 참조 [포털을 통해 관리 하는 Azure 리소스](../azure-resource-manager/resource-group-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="11bab-168">toodeploy 리소스 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](../azure-resource-manager/resource-group-template-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11bab-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

