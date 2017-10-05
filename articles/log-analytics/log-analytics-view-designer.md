---
title: "OMS Log Analytics에서 데이터를 분석하는 보기 만들기 | Microsoft 문서"
description: "Log Analytics에서 뷰 디자이너를 사용하면 OMS 및 Azure Portal에 표시되고 OMS 리포지토리에 있는 데이터를 여러 방법으로 시각화하는 사용자 지정 보기를 만들 수 있습니다. 이 문서에는 뷰 디자이너 개요 및 사용자 지정 보기를 만들고 편집하는 절차가 포함되어 있습니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: e3c463d749dc4179df58286b9bb75584880a6bc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-view-designer-to-create-custom-views-in-log-analytics"></a><span data-ttu-id="cd7be-104">뷰 디자이너를 사용하여 Log Analytics에서 사용자 지정 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="cd7be-104">Use View Designer to create custom views in Log Analytics</span></span>
<span data-ttu-id="cd7be-105">[Log Analytics](log-analytics-overview.md)에서 뷰 디자이너를 사용하면 OMS 리포지토리에 있는 데이터를 여러 방법으로 시각화하는 사용자 지정 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-105">The View Designer in [Log Analytics](log-analytics-overview.md) allows you to create custom views in the OMS console that contain different visualizations of data in the OMS repository.</span></span> <span data-ttu-id="cd7be-106">이 문서에는 뷰 디자이너 개요 및 사용자 지정 보기를 만들고 편집하는 절차가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-106">This article contains an overview of View Designer and procedures for creating and editing custom views.</span></span>

<span data-ttu-id="cd7be-107">뷰 디자이너에 적용할 수 있는 다른 문서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-107">Other articles available for View Designer are:</span></span>

* <span data-ttu-id="cd7be-108">[타일 참조](log-analytics-view-designer-tiles.md) - 사용자 지정 보기에 사용할 수 있는 타일 각각의 설정에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="cd7be-108">[Tile reference](log-analytics-view-designer-tiles.md) - Reference of the settings for each of the tiles available to use in your custom views.</span></span>
* <span data-ttu-id="cd7be-109">[시각화 요소 참조](log-analytics-view-designer-parts.md) - 사용자 지정 보기에 사용할 수 있는 타일 각각의 설정에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="cd7be-109">[Visualization part reference](log-analytics-view-designer-parts.md) - Reference of the settings for each of the tiles available to use in your custom views.</span></span>

>[!NOTE]
> <span data-ttu-id="cd7be-110">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우 모든 뷰의 쿼리를 [새 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856078)로 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-110">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then queries in all views must be written in the [new query language](https://go.microsoft.com/fwlink/?linkid=856078).</span></span>  <span data-ttu-id="cd7be-111">작업 영역을 업그레이드하기 전에 생성된 모든 뷰는 자동으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-111">Any views that were created before the workspace was upgraded will be automtically converted.</span></span>

## <a name="concepts"></a><span data-ttu-id="cd7be-112">개념</span><span class="sxs-lookup"><span data-stu-id="cd7be-112">Concepts</span></span>
<span data-ttu-id="cd7be-113">뷰 디자이너에서 만드는 보기에 포함되는 요소는 다음 표와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-113">Views created with the View Designer contain the elements in the following table.</span></span>

| <span data-ttu-id="cd7be-114">부</span><span class="sxs-lookup"><span data-stu-id="cd7be-114">Part</span></span> | <span data-ttu-id="cd7be-115">설명</span><span class="sxs-lookup"><span data-stu-id="cd7be-115">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cd7be-116">타일</span><span class="sxs-lookup"><span data-stu-id="cd7be-116">Tile</span></span> |<span data-ttu-id="cd7be-117">기본 Log Analytics 개요 대시보드에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-117">Displayed on the main Log Analytics Overview dashboard.</span></span>  <span data-ttu-id="cd7be-118">사용자 지정 보기에 있는 정보를 요약하는 시각적 개체를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-118">Includes a visual summarizing of the information contained in the custom View.</span></span>  <span data-ttu-id="cd7be-119">타일 유형마다 OMS 리포지토리에 있는 레코드에 대해 차별화된 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-119">Different Tile types provide different visualizations of records in the OMS repository.</span></span>  <span data-ttu-id="cd7be-120">타일을 클릭하면 사용자 지정 보기가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-120">Click on the Tile to open the Custom View.</span></span> |
| <span data-ttu-id="cd7be-121">사용자 지정 보기</span><span class="sxs-lookup"><span data-stu-id="cd7be-121">Custom View</span></span> |<span data-ttu-id="cd7be-122">사용자가 타일을 클릭할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-122">Displayed when the user clicks on the Tile.</span></span>  <span data-ttu-id="cd7be-123">시각화 요소를 하나 이상 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-123">Contains one or more visualization parts.</span></span> |
| <span data-ttu-id="cd7be-124">시각화 요소</span><span class="sxs-lookup"><span data-stu-id="cd7be-124">Visualization Parts</span></span> |<span data-ttu-id="cd7be-125">OMS 리포지토리의 데이터에 대한 [로그 검색](log-analytics-log-searches.md) 하나 이상에 기반한 시각화입니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-125">Visualization of data in the OMS repository based on one or more [log searches](log-analytics-log-searches.md).</span></span>  <span data-ttu-id="cd7be-126">대부분의 요소에는 높은 수준의 시각화와 상위 결과 목록을 제공하는 머리글이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-126">Most parts will include a Header that provides a high level visualization and a List of the top results.</span></span>  <span data-ttu-id="cd7be-127">요소 유형마다 OMS 리포지토리에 있는 레코드에 대해 차별화된 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-127">Different part types provide different visualizations of records in the OMS repository.</span></span>  <span data-ttu-id="cd7be-128">요소의 항목을 클릭하면 상세 레코드를 제공하는 로그 검색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-128">Click on elements in the part to perform a log search providing detailed records.</span></span> |

![뷰 디자이너 개요](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-to-your-workspace"></a><span data-ttu-id="cd7be-130">작업 영역에 뷰 디자이너 추가</span><span class="sxs-lookup"><span data-stu-id="cd7be-130">Add View Designer to your workspace</span></span>
<span data-ttu-id="cd7be-131">뷰 디자이너가 미리 보기 상태에 있는 동안에 OMS 포털의 **설정** 섹션에서 **미리 보기 기능**을 선택하여 작업 영역에 뷰 디자이너를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-131">While View Designer is in preview, you must add it to your workspace by selecting **Preview Features** in the **Settings** section of the OMS portal.</span></span>

![미리 보기 사용](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a><span data-ttu-id="cd7be-133">보기 만들기 및 편집</span><span class="sxs-lookup"><span data-stu-id="cd7be-133">Creating and editing views</span></span>
### <a name="create-a-new-view"></a><span data-ttu-id="cd7be-134">새 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="cd7be-134">Create a new view</span></span>
<span data-ttu-id="cd7be-135">기본 OMS 대시보드에서 뷰 디자이너 타일을 클릭하여 **뷰 디자이너**에서 새 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-135">Open a new view in the **View Designer** by clicking on the View Designer tile in the main OMS dashboard.</span></span>

![뷰 디자이너 타일](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a><span data-ttu-id="cd7be-137">기존 보기 편집</span><span class="sxs-lookup"><span data-stu-id="cd7be-137">Edit an existing view</span></span>
<span data-ttu-id="cd7be-138">뷰 디자이너에서 기존 보기를 편집하려면 기본 OMS 대시보드에서 해당 타일을 클릭하여 해당 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-138">To edit an existing view in the View Designer, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="cd7be-139">그런 다음 **편집** 단추를 클릭하여 뷰 디자이너에서 해당 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-139">Then click the **Edit** button to open the view in the View Designer.</span></span>

![보기 편집](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a><span data-ttu-id="cd7be-141">기존 보기 복제</span><span class="sxs-lookup"><span data-stu-id="cd7be-141">Clone an existing view</span></span>
<span data-ttu-id="cd7be-142">보기를 복제하면 새 보기를 만들고 뷰 디자이너에서 이 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-142">When you clone a view, it creates a new view and opens it in the View Designer.</span></span>  <span data-ttu-id="cd7be-143">새 보기에는 원본과 동일한 이름 끝에 "복사본"이 추가된 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-143">The new view will have the same name as the original with "Copy" appended to the end of it.</span></span>  <span data-ttu-id="cd7be-144">보기를 복제하려면 기본 OMS 대시보드에서 해당 타일을 클릭하여 기존 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-144">To clone a view, open the existing view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="cd7be-145">그런 다음 **복제** 단추를 클릭하여 뷰 디자이너에서 해당 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-145">Then click the **Clone** button to open the view in the View Designer.</span></span>

![보기 복제](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a><span data-ttu-id="cd7be-147">기존 보기 삭제</span><span class="sxs-lookup"><span data-stu-id="cd7be-147">Delete an existing view</span></span>
<span data-ttu-id="cd7be-148">기존 보기를 삭제하려면 기본 OMS 대시보드에서 해당 타일을 클릭하여 해당 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-148">To delete an existing view, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="cd7be-149">그런 다음 **편집** 단추를 클릭하여 뷰 디자이너에서 해당 보기를 열고 **보기 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-149">Then click the **Edit** button to open the view in the View Designer, and click **Delete View**.</span></span>

![보기 삭제](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a><span data-ttu-id="cd7be-151">기존 보기 내보내기</span><span class="sxs-lookup"><span data-stu-id="cd7be-151">Export an existing view</span></span>
<span data-ttu-id="cd7be-152">보기는 다른 작업 영역으로 가져오거나 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-authoring-templates.md)에서 사용할 수 있는 JSON 파일에 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-152">You can export a view to a JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="cd7be-153">기존 보기를 내보려면 기본 OMS 대시보드에서 해당 타일을 클릭하여 해당 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-153">To export an existing view, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="cd7be-154">그런 다음 **내보내기** 단추를 클릭하여 브라우저의 다운로드 폴더에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-154">Then click the **Export** button to create a file in the browser's download folder.</span></span>  <span data-ttu-id="cd7be-155">파일 이름은 보기 이름과 *omsview* 확장명으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-155">The name of the file will be the name of the view with the extension *omsview*.</span></span>

![보기 내보내기](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a><span data-ttu-id="cd7be-157">기존 보기 가져오기</span><span class="sxs-lookup"><span data-stu-id="cd7be-157">Import an existing view</span></span>
<span data-ttu-id="cd7be-158">다른 관리 그룹에서 내보낸 *omsview* 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-158">You can import an *omsview* file that you exported from another management group.</span></span>  <span data-ttu-id="cd7be-159">기존 보기를 가져오려면 먼저 새 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-159">To import an existing view, first create a new view.</span></span>  <span data-ttu-id="cd7be-160">그런 다음 **가져오기** 단추를 클릭하여 *omsview* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-160">Then click the **Import** button and select the *omsview* file.</span></span>  <span data-ttu-id="cd7be-161">파일의 구성이 기존 보기에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-161">The configuration in the file will be copied into the existing view.</span></span>

![보기 내보내기](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a><span data-ttu-id="cd7be-163">뷰 디자이너 작업</span><span class="sxs-lookup"><span data-stu-id="cd7be-163">Working with View Designer</span></span>
<span data-ttu-id="cd7be-164">뷰 디자이너에는 세 개의 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-164">The View Designer has three panes.</span></span>  <span data-ttu-id="cd7be-165">**디자인** 창에서는 사용자 지정 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-165">The **Design** pane represents the custom view.</span></span>  <span data-ttu-id="cd7be-166">**제어** 창에서 **디자인** 창으로 타일과 요소를 추가하면 해당 타일과 요소가 보기에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-166">When you add tiles and parts from the **Control** pane to the **Design** pane they are added to the view.</span></span>  <span data-ttu-id="cd7be-167">**속성** 창에서는 타일 또는 선택한 요소의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-167">The **Properties** pane will display the properties for the tile or selected part.</span></span>

![뷰 디자이너](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a><span data-ttu-id="cd7be-169">보기 타일 구성</span><span class="sxs-lookup"><span data-stu-id="cd7be-169">Configure view tile</span></span>
<span data-ttu-id="cd7be-170">사용자 지정 보기에는 타일 하나만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-170">A custom view can have only a single tile.</span></span>  <span data-ttu-id="cd7be-171">**제어** 창에서 **타일** 탭을 선택하여 현재 타일을 확인하거나 다른 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-171">Select the **Tile** tab in the **Control** pane to view the current tile or select an alternate one.</span></span>  <span data-ttu-id="cd7be-172">**속성** 창에서는 현재 타일의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-172">The **Properties** pane will display the properties for the current tile.</span></span>  <span data-ttu-id="cd7be-173">[타일 참조](log-analytics-view-designer-tiles.md)의 세부 정보에 따라 타일 속성을 구성한 다음 **적용**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-173">Configure the tile properties according to the detailed information in the [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** to save changes.</span></span>

### <a name="configure-visualization-parts"></a><span data-ttu-id="cd7be-174">시각화 요소 구성</span><span class="sxs-lookup"><span data-stu-id="cd7be-174">Configure visualization parts</span></span>
<span data-ttu-id="cd7be-175">보기에는 시각화 요소가 얼마든지 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-175">A view can include any number of visualization parts.</span></span>  <span data-ttu-id="cd7be-176">**보기** 탭, 보기에 추가할 시각화 요소를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-176">Select the **View** tab and then a visualization part to add to the view.</span></span>  <span data-ttu-id="cd7be-177">**속성** 창에서는 선택한 요소의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-177">The **Properties** pane will display the properties for the selected part.</span></span>  <span data-ttu-id="cd7be-178">[시각화 요소 참조](log-analytics-view-designer-parts.md)의 세부 정보에 따라 보기일 속성을 구성한 다음 **적용**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-178">Configure the view properties according to the detailed information in the [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** to save changes.</span></span>

### <a name="delete-a-visualization-part"></a><span data-ttu-id="cd7be-179">시각화 요소 삭제</span><span class="sxs-lookup"><span data-stu-id="cd7be-179">Delete a visualization part</span></span>
<span data-ttu-id="cd7be-180">요소 오른쪽 위 모서리의 **X** 단추를 클릭하면 보기에서 시각화 요소를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-180">You can remove a visualization part from the view by clicking the **X** button in the top right corner of the part.</span></span>

### <a name="rearrange-visualization-parts"></a><span data-ttu-id="cd7be-181">시각화 요소 다시 정렬</span><span class="sxs-lookup"><span data-stu-id="cd7be-181">Rearrange visualization parts</span></span>
<span data-ttu-id="cd7be-182">보기에는 시각화 요소의 행 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-182">Views only have one row of visualization parts.</span></span>  <span data-ttu-id="cd7be-183">기존 요소를 클릭하여 새 위치로 끌어가면 보기에서 해당 요소를 다시 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd7be-183">Rearrange existing parts in a view by clicking and dragging them to a new location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd7be-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd7be-184">Next steps</span></span>
* <span data-ttu-id="cd7be-185">사용자 지정 보기에 [타일](log-analytics-view-designer-tiles.md) 추가</span><span class="sxs-lookup"><span data-stu-id="cd7be-185">Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.</span></span>
* <span data-ttu-id="cd7be-186">사용자 지정 보기에 [시각화 요소](log-analytics-view-designer-parts.md) 추가</span><span class="sxs-lookup"><span data-stu-id="cd7be-186">Add [Visualization Parts](log-analytics-view-designer-parts.md) to your custom view.</span></span>
