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
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>뷰 디자이너 toocreate 사용자 지정 보기를 사용 하 여 로그 분석에서
hello 뷰 디자이너에서 [로그 분석](log-analytics-overview.md) toocreate 사용자 지정 보기 hello OMS 콘솔에서 hello OMS 리포지토리에 데이터의 각기 다른 시각화를 포함 하는 있습니다. 이 문서에는 뷰 디자이너 개요 및 사용자 지정 보기를 만들고 편집하는 절차가 포함되어 있습니다.

뷰 디자이너에 적용할 수 있는 다른 문서는 다음과 같습니다.

* [참조 바둑판식으로 배열](log-analytics-view-designer-tiles.md) -참조 각 hello에 대 한 hello 설정의 사용자 지정 보기에서 사용할 수 있는 toouse 바둑판식으로 표시 합니다.
* [시각화 파트 참조](log-analytics-view-designer-parts.md) -참조 각 hello에 대 한 hello 설정의 사용자 지정 보기에서 사용할 수 있는 toouse 바둑판식으로 표시 합니다.

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), hello 모든 보기에서 쿼리를 작성 해야 하는 다음 [새로운 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856078)합니다.  작업 영역 hello를 업그레이드 하기 전에 생성 된 모든 뷰 automtically 변환 됩니다.

## <a name="concepts"></a>개념
Hello 뷰 디자이너를 사용 하 여 만든 뷰는 다음 표에 hello에 hello 요소를 포함 합니다.

| 부 | 설명 |
|:--- |:--- |
| 타일 |Hello 주 로그 분석 개요 대시보드에 나타납니다.  Hello에 포함 된 hello 정보를 시각적 요약 포함 사용자 지정 보기.  다른 타일 형식은 hello OMS 리포지토리에 레코드의 각기 다른 시각화를 제공합니다.  사용자 지정 보기 타일 tooopen hello hello 클릭 합니다. |
| 사용자 지정 보기 |Hello 사용자 hello 타일을 클릭할 때 표시 됩니다.  시각화 요소를 하나 이상 포함하고 있습니다. |
| 시각화 요소 |하나 이상의에 따라 hello OMS 리포지토리에 데이터의 시각화 [검색 로그](log-analytics-log-searches.md)합니다.  대부분 파트는 높은 수준의 시각화를 제공 하는 헤더 및 hello 상위 결과 목록이 포함 됩니다.  다른 부분 형식 hello OMS 리포지토리에 레코드의 각기 다른 시각화를 제공합니다.  세부 레코드를 제공 하는 로그 검색 hello 부분 tooperform에 요소를 클릭 합니다. |

![뷰 디자이너 개요](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>뷰 디자이너 tooyour 작업 영역 추가
뷰 디자이너 미리 보기 상태인 동안 추가 해야 tooyour 작업 영역을 선택 하 여 **미리 보기 기능** hello에 **설정을** hello OMS 포털의 섹션입니다.

![미리 보기 사용](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>보기 만들기 및 편집
### <a name="create-a-new-view"></a>새 보기 만들기
Hello에 새 보기를 열고 **뷰 디자이너** hello 뷰 디자이너를 클릭 하 여 hello 기본 OMS 대시보드의 타일입니다.

![뷰 디자이너 타일](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>기존 보기 편집
tooedit hello open hello 보기 hello 주 OMS 대시보드에 타일을 클릭 하 여 뷰 디자이너에서에서 기존 보기.  Hello 클릭 **편집** hello 뷰 디자이너에서에서 tooopen hello 보기 단추입니다.

![보기 편집](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>기존 보기 복제
뷰를 복제 하면 보기를 새로 만들고 hello 뷰 디자이너에서에서 엽니다.  새 보기 hello hello "복사" 추가 된 toohello 끝에 있는 원래 hello로 이름과 같은 이름을 갖습니다.  tooclone 보기, 열기 hello hello 주 OMS 대시보드에 타일을 클릭 하 여 기존 보기.  Hello 클릭 **복제** hello 뷰 디자이너에서에서 tooopen hello 보기 단추입니다.

![보기 복제](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>기존 보기 삭제
toodelete 기존 보기를 hello 주 OMS 대시보드에 타일을 클릭 하 여 열기 hello 보기.  Hello 클릭 **편집** hello 뷰 디자이너에서에서 tooopen hello 보기 단추를 누르고 **보기 삭제**합니다.

![보기 삭제](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>기존 보기 내보내기
사용 하거나 다른 작업 영역으로 가져올 수 있는 보기 tooa JSON 파일을 내보낼 수는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md)합니다.  tooexport 기존 보기를 hello 주 OMS 대시보드에 타일을 클릭 하 여 열기 hello 보기.  Hello 클릭 **내보내기** 단추 toocreate hello 브라우저 다운로드 폴더의 파일에에서 있습니다.  hello hello 파일의 hello 이름이 됩니다 hello 확장명이 hello 뷰의 *omsview*합니다.

![보기 내보내기](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>기존 보기 가져오기
다른 관리 그룹에서 내보낸 *omsview* 파일을 가져올 수 있습니다.  먼저 기존 보기를 tooimport 새 보기를 만듭니다.  Hello 클릭 **가져오기** 단추와 선택 hello *omsview* 파일입니다.  hello 파일의 hello 구성 hello 기존 보기에 복사 됩니다.

![보기 내보내기](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>뷰 디자이너 작업
hello 뷰 디자이너에 세 개의 창이 있습니다.  hello **디자인** 창 hello 사용자 지정 보기를 나타냅니다.  Hello에서 타일 및 일부 추가 되는 경우 **제어** 창 toohello **디자인** 는 창 toohello 보기를 추가 합니다.  hello **속성** hello 타일 또는 선택한 부분에 대 한 hello 속성 창에 표시 됩니다.

![뷰 디자이너](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>보기 타일 구성
사용자 지정 보기에는 타일 하나만 있을 수 있습니다.  선택 hello **타일** hello 탭 **제어** tooview hello 현재 창 바둑판식으로 배열 하거나 대체를 선택 합니다.  hello **속성** hello 현재 타일에 대 한 hello 속성 창에 표시 됩니다.  Hello 타일 속성 구성 toohello에 따라 자세한 정보를 hello에 [바둑판식으로 배열 참조](log-analytics-view-designer-tiles.md) 클릭 **적용** toosave 변경 합니다.

### <a name="configure-visualization-parts"></a>시각화 요소 구성
보기에는 시각화 요소가 얼마든지 포함될 수 있습니다.  선택 hello **보기** 탭 한 다음 시각화 부 tooadd toohello 보기.  hello **속성** hello 선택 부분에 대 한 hello 속성 창에 표시 됩니다.  Hello 뷰 구성 자세한 hello에 대 한 정보를 toohello에 따라 속성 [시각화 파트 참조](log-analytics-view-designer-parts.md) 클릭 **적용** toosave 변경 합니다.

### <a name="delete-a-visualization-part"></a>시각화 요소 삭제
Hello를 클릭 하 여 hello 보기에서 시각화 파트를 제거할 수 **X** hello의 오른쪽 위 모서리 hello 부분에서에서 단추입니다.

### <a name="rearrange-visualization-parts"></a>시각화 요소 다시 정렬
보기에는 시각화 요소의 행 하나만 있습니다.  클릭 하 여 tooa 새 위치로 끌어 뷰의 기존 파트를 다시 정렬 합니다.

## <a name="next-steps"></a>다음 단계
* 추가 [타일](log-analytics-view-designer-tiles.md) tooyour 사용자 지정 보기.
* 추가 [시각화 부분](log-analytics-view-designer-parts.md) tooyour 사용자 지정 보기.
