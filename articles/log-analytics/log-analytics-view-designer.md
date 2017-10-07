---
title: "aaaCreate OMS 로그 분석에 tooanalyze 데이터 뷰 | Microsoft Docs"
description: "로그 분석에서 보기 디자이너 있습니다 toocreate 사용자 지정 보기 hello OMS 리포지토리에 데이터의 각기 다른 시각화를 포함 하는 hello OMS 및 Azure 포털에 표시 됩니다. 이 문서에는 뷰 디자이너 개요 및 사용자 지정 보기를 만들고 편집하는 절차가 포함되어 있습니다."
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
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a><span data-ttu-id="950bb-104">뷰 디자이너 toocreate 사용자 지정 보기를 사용 하 여 로그 분석에서</span><span class="sxs-lookup"><span data-stu-id="950bb-104">Use View Designer toocreate custom views in Log Analytics</span></span>
<span data-ttu-id="950bb-105">hello 뷰 디자이너에서 [로그 분석](log-analytics-overview.md) toocreate 사용자 지정 보기 hello OMS 콘솔에서 hello OMS 리포지토리에 데이터의 각기 다른 시각화를 포함 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-105">hello View Designer in [Log Analytics](log-analytics-overview.md) allows you toocreate custom views in hello OMS console that contain different visualizations of data in hello OMS repository.</span></span> <span data-ttu-id="950bb-106">이 문서에는 뷰 디자이너 개요 및 사용자 지정 보기를 만들고 편집하는 절차가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-106">This article contains an overview of View Designer and procedures for creating and editing custom views.</span></span>

<span data-ttu-id="950bb-107">뷰 디자이너에 적용할 수 있는 다른 문서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-107">Other articles available for View Designer are:</span></span>

* <span data-ttu-id="950bb-108">[참조 바둑판식으로 배열](log-analytics-view-designer-tiles.md) -참조 각 hello에 대 한 hello 설정의 사용자 지정 보기에서 사용할 수 있는 toouse 바둑판식으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-108">[Tile reference](log-analytics-view-designer-tiles.md) - Reference of hello settings for each of hello tiles available toouse in your custom views.</span></span>
* <span data-ttu-id="950bb-109">[시각화 파트 참조](log-analytics-view-designer-parts.md) -참조 각 hello에 대 한 hello 설정의 사용자 지정 보기에서 사용할 수 있는 toouse 바둑판식으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-109">[Visualization part reference](log-analytics-view-designer-parts.md) - Reference of hello settings for each of hello tiles available toouse in your custom views.</span></span>

>[!NOTE]
> <span data-ttu-id="950bb-110">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), hello 모든 보기에서 쿼리를 작성 해야 하는 다음 [새로운 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856078)합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-110">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then queries in all views must be written in hello [new query language](https://go.microsoft.com/fwlink/?linkid=856078).</span></span>  <span data-ttu-id="950bb-111">작업 영역 hello를 업그레이드 하기 전에 생성 된 모든 뷰 automtically 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-111">Any views that were created before hello workspace was upgraded will be automtically converted.</span></span>

## <a name="concepts"></a><span data-ttu-id="950bb-112">개념</span><span class="sxs-lookup"><span data-stu-id="950bb-112">Concepts</span></span>
<span data-ttu-id="950bb-113">Hello 뷰 디자이너를 사용 하 여 만든 뷰는 다음 표에 hello에 hello 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-113">Views created with hello View Designer contain hello elements in hello following table.</span></span>

| <span data-ttu-id="950bb-114">부</span><span class="sxs-lookup"><span data-stu-id="950bb-114">Part</span></span> | <span data-ttu-id="950bb-115">설명</span><span class="sxs-lookup"><span data-stu-id="950bb-115">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="950bb-116">타일</span><span class="sxs-lookup"><span data-stu-id="950bb-116">Tile</span></span> |<span data-ttu-id="950bb-117">Hello 주 로그 분석 개요 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-117">Displayed on hello main Log Analytics Overview dashboard.</span></span>  <span data-ttu-id="950bb-118">Hello에 포함 된 hello 정보를 시각적 요약 포함 사용자 지정 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-118">Includes a visual summarizing of hello information contained in hello custom View.</span></span>  <span data-ttu-id="950bb-119">다른 타일 형식은 hello OMS 리포지토리에 레코드의 각기 다른 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-119">Different Tile types provide different visualizations of records in hello OMS repository.</span></span>  <span data-ttu-id="950bb-120">사용자 지정 보기 타일 tooopen hello hello 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-120">Click on hello Tile tooopen hello Custom View.</span></span> |
| <span data-ttu-id="950bb-121">사용자 지정 보기</span><span class="sxs-lookup"><span data-stu-id="950bb-121">Custom View</span></span> |<span data-ttu-id="950bb-122">Hello 사용자 hello 타일을 클릭할 때 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-122">Displayed when hello user clicks on hello Tile.</span></span>  <span data-ttu-id="950bb-123">시각화 요소를 하나 이상 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-123">Contains one or more visualization parts.</span></span> |
| <span data-ttu-id="950bb-124">시각화 요소</span><span class="sxs-lookup"><span data-stu-id="950bb-124">Visualization Parts</span></span> |<span data-ttu-id="950bb-125">하나 이상의에 따라 hello OMS 리포지토리에 데이터의 시각화 [검색 로그](log-analytics-log-searches.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-125">Visualization of data in hello OMS repository based on one or more [log searches](log-analytics-log-searches.md).</span></span>  <span data-ttu-id="950bb-126">대부분 파트는 높은 수준의 시각화를 제공 하는 헤더 및 hello 상위 결과 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-126">Most parts will include a Header that provides a high level visualization and a List of hello top results.</span></span>  <span data-ttu-id="950bb-127">다른 부분 형식 hello OMS 리포지토리에 레코드의 각기 다른 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-127">Different part types provide different visualizations of records in hello OMS repository.</span></span>  <span data-ttu-id="950bb-128">세부 레코드를 제공 하는 로그 검색 hello 부분 tooperform에 요소를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-128">Click on elements in hello part tooperform a log search providing detailed records.</span></span> |

![뷰 디자이너 개요](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a><span data-ttu-id="950bb-130">뷰 디자이너 tooyour 작업 영역 추가</span><span class="sxs-lookup"><span data-stu-id="950bb-130">Add View Designer tooyour workspace</span></span>
<span data-ttu-id="950bb-131">뷰 디자이너 미리 보기 상태인 동안 추가 해야 tooyour 작업 영역을 선택 하 여 **미리 보기 기능** hello에 **설정을** hello OMS 포털의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-131">While View Designer is in preview, you must add it tooyour workspace by selecting **Preview Features** in hello **Settings** section of hello OMS portal.</span></span>

![미리 보기 사용](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a><span data-ttu-id="950bb-133">보기 만들기 및 편집</span><span class="sxs-lookup"><span data-stu-id="950bb-133">Creating and editing views</span></span>
### <a name="create-a-new-view"></a><span data-ttu-id="950bb-134">새 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="950bb-134">Create a new view</span></span>
<span data-ttu-id="950bb-135">Hello에 새 보기를 열고 **뷰 디자이너** hello 뷰 디자이너를 클릭 하 여 hello 기본 OMS 대시보드의 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-135">Open a new view in hello **View Designer** by clicking on hello View Designer tile in hello main OMS dashboard.</span></span>

![뷰 디자이너 타일](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a><span data-ttu-id="950bb-137">기존 보기 편집</span><span class="sxs-lookup"><span data-stu-id="950bb-137">Edit an existing view</span></span>
<span data-ttu-id="950bb-138">tooedit hello open hello 보기 hello 주 OMS 대시보드에 타일을 클릭 하 여 뷰 디자이너에서에서 기존 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-138">tooedit an existing view in hello View Designer, open hello view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="950bb-139">Hello 클릭 **편집** hello 뷰 디자이너에서에서 tooopen hello 보기 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-139">Then click hello **Edit** button tooopen hello view in hello View Designer.</span></span>

![보기 편집](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a><span data-ttu-id="950bb-141">기존 보기 복제</span><span class="sxs-lookup"><span data-stu-id="950bb-141">Clone an existing view</span></span>
<span data-ttu-id="950bb-142">뷰를 복제 하면 보기를 새로 만들고 hello 뷰 디자이너에서에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-142">When you clone a view, it creates a new view and opens it in hello View Designer.</span></span>  <span data-ttu-id="950bb-143">새 보기 hello hello "복사" 추가 된 toohello 끝에 있는 원래 hello로 이름과 같은 이름을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-143">hello new view will have hello same name as hello original with "Copy" appended toohello end of it.</span></span>  <span data-ttu-id="950bb-144">tooclone 보기, 열기 hello hello 주 OMS 대시보드에 타일을 클릭 하 여 기존 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-144">tooclone a view, open hello existing view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="950bb-145">Hello 클릭 **복제** hello 뷰 디자이너에서에서 tooopen hello 보기 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-145">Then click hello **Clone** button tooopen hello view in hello View Designer.</span></span>

![보기 복제](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a><span data-ttu-id="950bb-147">기존 보기 삭제</span><span class="sxs-lookup"><span data-stu-id="950bb-147">Delete an existing view</span></span>
<span data-ttu-id="950bb-148">toodelete 기존 보기를 hello 주 OMS 대시보드에 타일을 클릭 하 여 열기 hello 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-148">toodelete an existing view, open hello view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="950bb-149">Hello 클릭 **편집** hello 뷰 디자이너에서에서 tooopen hello 보기 단추를 누르고 **보기 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-149">Then click hello **Edit** button tooopen hello view in hello View Designer, and click **Delete View**.</span></span>

![보기 삭제](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a><span data-ttu-id="950bb-151">기존 보기 내보내기</span><span class="sxs-lookup"><span data-stu-id="950bb-151">Export an existing view</span></span>
<span data-ttu-id="950bb-152">사용 하거나 다른 작업 영역으로 가져올 수 있는 보기 tooa JSON 파일을 내보낼 수는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-152">You can export a view tooa JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="950bb-153">tooexport 기존 보기를 hello 주 OMS 대시보드에 타일을 클릭 하 여 열기 hello 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-153">tooexport an existing view, open hello view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="950bb-154">Hello 클릭 **내보내기** 단추 toocreate hello 브라우저 다운로드 폴더의 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-154">Then click hello **Export** button toocreate a file in hello browser's download folder.</span></span>  <span data-ttu-id="950bb-155">hello hello 파일의 hello 이름이 됩니다 hello 확장명이 hello 뷰의 *omsview*합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-155">hello name of hello file will be hello name of hello view with hello extension *omsview*.</span></span>

![보기 내보내기](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a><span data-ttu-id="950bb-157">기존 보기 가져오기</span><span class="sxs-lookup"><span data-stu-id="950bb-157">Import an existing view</span></span>
<span data-ttu-id="950bb-158">다른 관리 그룹에서 내보낸 *omsview* 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-158">You can import an *omsview* file that you exported from another management group.</span></span>  <span data-ttu-id="950bb-159">먼저 기존 보기를 tooimport 새 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-159">tooimport an existing view, first create a new view.</span></span>  <span data-ttu-id="950bb-160">Hello 클릭 **가져오기** 단추와 선택 hello *omsview* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-160">Then click hello **Import** button and select hello *omsview* file.</span></span>  <span data-ttu-id="950bb-161">hello 파일의 hello 구성 hello 기존 보기에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-161">hello configuration in hello file will be copied into hello existing view.</span></span>

![보기 내보내기](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a><span data-ttu-id="950bb-163">뷰 디자이너 작업</span><span class="sxs-lookup"><span data-stu-id="950bb-163">Working with View Designer</span></span>
<span data-ttu-id="950bb-164">hello 뷰 디자이너에 세 개의 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-164">hello View Designer has three panes.</span></span>  <span data-ttu-id="950bb-165">hello **디자인** 창 hello 사용자 지정 보기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-165">hello **Design** pane represents hello custom view.</span></span>  <span data-ttu-id="950bb-166">Hello에서 타일 및 일부 추가 되는 경우 **제어** 창 toohello **디자인** 는 창 toohello 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-166">When you add tiles and parts from hello **Control** pane toohello **Design** pane they are added toohello view.</span></span>  <span data-ttu-id="950bb-167">hello **속성** hello 타일 또는 선택한 부분에 대 한 hello 속성 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-167">hello **Properties** pane will display hello properties for hello tile or selected part.</span></span>

![뷰 디자이너](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a><span data-ttu-id="950bb-169">보기 타일 구성</span><span class="sxs-lookup"><span data-stu-id="950bb-169">Configure view tile</span></span>
<span data-ttu-id="950bb-170">사용자 지정 보기에는 타일 하나만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-170">A custom view can have only a single tile.</span></span>  <span data-ttu-id="950bb-171">선택 hello **타일** hello 탭 **제어** tooview hello 현재 창 바둑판식으로 배열 하거나 대체를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-171">Select hello **Tile** tab in hello **Control** pane tooview hello current tile or select an alternate one.</span></span>  <span data-ttu-id="950bb-172">hello **속성** hello 현재 타일에 대 한 hello 속성 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-172">hello **Properties** pane will display hello properties for hello current tile.</span></span>  <span data-ttu-id="950bb-173">Hello 타일 속성 구성 toohello에 따라 자세한 정보를 hello에 [바둑판식으로 배열 참조](log-analytics-view-designer-tiles.md) 클릭 **적용** toosave 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-173">Configure hello tile properties according toohello detailed information in hello [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** toosave changes.</span></span>

### <a name="configure-visualization-parts"></a><span data-ttu-id="950bb-174">시각화 요소 구성</span><span class="sxs-lookup"><span data-stu-id="950bb-174">Configure visualization parts</span></span>
<span data-ttu-id="950bb-175">보기에는 시각화 요소가 얼마든지 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-175">A view can include any number of visualization parts.</span></span>  <span data-ttu-id="950bb-176">선택 hello **보기** 탭 한 다음 시각화 부 tooadd toohello 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-176">Select hello **View** tab and then a visualization part tooadd toohello view.</span></span>  <span data-ttu-id="950bb-177">hello **속성** hello 선택 부분에 대 한 hello 속성 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-177">hello **Properties** pane will display hello properties for hello selected part.</span></span>  <span data-ttu-id="950bb-178">Hello 뷰 구성 자세한 hello에 대 한 정보를 toohello에 따라 속성 [시각화 파트 참조](log-analytics-view-designer-parts.md) 클릭 **적용** toosave 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-178">Configure hello view properties according toohello detailed information in hello [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** toosave changes.</span></span>

### <a name="delete-a-visualization-part"></a><span data-ttu-id="950bb-179">시각화 요소 삭제</span><span class="sxs-lookup"><span data-stu-id="950bb-179">Delete a visualization part</span></span>
<span data-ttu-id="950bb-180">Hello를 클릭 하 여 hello 보기에서 시각화 파트를 제거할 수 **X** hello의 오른쪽 위 모서리 hello 부분에서에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-180">You can remove a visualization part from hello view by clicking hello **X** button in hello top right corner of hello part.</span></span>

### <a name="rearrange-visualization-parts"></a><span data-ttu-id="950bb-181">시각화 요소 다시 정렬</span><span class="sxs-lookup"><span data-stu-id="950bb-181">Rearrange visualization parts</span></span>
<span data-ttu-id="950bb-182">보기에는 시각화 요소의 행 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-182">Views only have one row of visualization parts.</span></span>  <span data-ttu-id="950bb-183">클릭 하 여 tooa 새 위치로 끌어 뷰의 기존 파트를 다시 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="950bb-183">Rearrange existing parts in a view by clicking and dragging them tooa new location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="950bb-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="950bb-184">Next steps</span></span>
* <span data-ttu-id="950bb-185">추가 [타일](log-analytics-view-designer-tiles.md) tooyour 사용자 지정 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-185">Add [Tiles](log-analytics-view-designer-tiles.md) tooyour custom view.</span></span>
* <span data-ttu-id="950bb-186">추가 [시각화 부분](log-analytics-view-designer-parts.md) tooyour 사용자 지정 보기.</span><span class="sxs-lookup"><span data-stu-id="950bb-186">Add [Visualization Parts](log-analytics-view-designer-parts.md) tooyour custom view.</span></span>
