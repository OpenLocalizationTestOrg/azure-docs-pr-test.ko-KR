---
title: "aaaSave 검색 및 Azure Data Catalog에서 pin 데이터 자산 | Microsoft Docs"
description: "방법 tooarticle 강조 표시 기능 Azure Data Catalog에서 데이터 원본 및 나중에 사용할 데이터 자산을 저장 하기 위한입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Azure Data Catalog에서 검색 저장 및 데이터 자산 고정
## <a name="introduction"></a>소개
Azure Data Catalog는 데이터 원본 검색에 대한 기능을 제공합니다. 신속 하 게 검색 하 고 hello 카탈로그 toolocate 데이터 소스를 필터링 하 고 보다 쉽게 toofind hello 적절 한 데이터에 hello 작업에 대 한 만들기의 의도 한 목적을 이해 합니다.

어떻게 해야 tooregularly 하지만 동일 하 게 작동 hello로 데이터? 있으며이 경우 여러 사용자가 정기적으로 기술 toohello hello 카탈로그에 동일한 데이터 원본? 이러한 상황에서는 동일한 hello toorepeatedly 문제가 검색 비효율적일 수 있습니다. 저장된 검색 및 고정된 데이터 자산이 유용할 수 있습니다.

## <a name="saved-searches"></a>저장된 검색
데이터 카탈로그에 저장된 검색은 재사용 가능한 사용자 단위 검색 정의입니다. 검색어, 태그 및 다른 필터를 포함하여 검색을 정의한 다음 저장할 수 있습니다. 저장 된 hello 검색 정의 다시 실행할 수 있습니다 이후 tooreturn 해당 검색 조건과 일치 하는 모든 데이터 자산입니다.

### <a name="create-a-saved-search"></a>저장된 검색 만들기
toocreate 저장된 된 검색을 다음 hello지 않습니다.
1. Hello Azure Data Catalog 포털 hello에 **현재 검색** 창 클릭 **저장**합니다. 

    ![현재 검색 설정 저장 링크](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Tooreuse를 원하고 클릭 hello 검색 조건을 입력 **저장**합니다.

    ![현재 검색 설정 저장된 검색 이름](./media/data-catalog-how-to-save-pin/02-name.png)

3. 메시지가 표시 되는 경우 저장 된 검색 hello에 대 한 이름을 입력 합니다. 의미 있는 이름을 선택 하 고 hello 검색에서 반환 되는 hello 데이터 자산을 설명 하는 합니다.

### <a name="manage-saved-searches"></a>저장된 검색 관리
하나 이상의 검색을 저장 한 후 한 **저장 된 검색** 옵션은 hello 아래에 표시 됩니다. **현재 검색** 상자입니다. Hello 목록이 확장 되는 경우 저장 된 모든 검색 표시 됩니다.

 ![저장된 검색의 목록](./media/data-catalog-how-to-save-pin/03-list.png)

Hello 다음 중 하나를 수행 합니다.

* 검색을 tooexecute hello 목록에 저장된 된 검색을 선택 합니다.

* tooview 저장된 된 검색에 대 한 관리 옵션의 목록을 hello 다음 toohello 검색 이름을 화살표를 클릭 합니다.

    ![저장된 검색 관리에 대한 옵션](./media/data-catalog-how-to-save-pin/04-managing.png)

* tooenter hello 저장 된 검색에 대 한 새 이름을 선택 **이름 바꾸기**합니다. hello 검색 정의 변경 되지 않습니다.

* 선택 목록에서 저장 하는 hello 검색 tooremove **삭제**, hello 삭제를 확인 합니다.

* 기본 검색 범위를 선택으로 toomark 저장 hello 검색 **기본값으로 저장**합니다. Hello Azure Data Catalog 홈 페이지에서 "empty"는 검색을 수행 하는 경우 기본 검색 실행 됩니다. 또한 hello 기본 검색 hello hello 위쪽에 표시 되는 것으로 표시 되는 검색을 hello **저장 된 검색** 목록입니다.

### <a name="organizational-saved-searches"></a>조직 저장된 검색
조직의 모든 사용자는 자신의 용도에 대한 검색을 저장할 수 있습니다. 데이터 카탈로그 관리자는 hello 조직 내의 모든 사용자에 대 한 검색을 저장할 수도 수 있습니다. 와 제공 되는 관리자가 검색 결과 저장 하는 경우는 **hello 회사 내에서 공유** 옵션입니다. 이 옵션 공유 hello hello 조직에 저장 된 모든 사용자에 게는 검색을 선택 하면 됩니다.

 ![조직 저장된 검색](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>고정된 데이터 자산
저장된 검색을 사용하여 검색 정의를 저장하고 다시 사용할 수 있습니다. hello 검색에서 반환 되는 hello 데이터 자산 hello 카탈로그 변경의 hello 콘텐츠로 시간이 지남에 따라 변경 될 수 있습니다. 데이터 자산을 고정 하면 특정 데이터 자산 toomake 명시적으로 식별할 수 있습니다 이러한 toouse 검색 필요 없이 쉽게 tooaccess 합니다.

데이터 자산을 고정하는 것은 간단합니다. tooadd hello 데이터 자산 tooyour 고정 목록 클릭 하면 hello **pin** 아이콘입니다. hello 아이콘이 hello 자산 타일 hello tile 보기에서 한 hello Azure Data Catalog 포털에 표시 되는 hello 목록 뷰에서 hello 맨 왼쪽 열에서의 hello 위에 표시 됩니다.

![hello 데이터 자산 고정 아이콘](./media/data-catalog-how-to-save-pin/05-pinning.png)

데이터 자산을 고정 해제하는 것은 동일하게 간단합니다. Hello를 클릭 하기만 하면 **고정 해제** hello 선택한 자산에 대 한 아이콘 tootoggle hello 설정 합니다.

![hello 데이터 자산을 고정 해제 아이콘](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>hello 내 자산 섹션
hello Data Catalog 포털 홈 페이지에는 **내 자산** 관심 toohello 현재 사용자의 자산을 표시 하는 섹션입니다. 이 섹션은 고정된 자산 및 저장된 검색을 모두 포함합니다.

![hello hello 홈 페이지에서 내 자산 섹션](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>요약
Azure 데이터 카탈로그는 사용자 및 다른 조직 멤버 데이터 및 작업을 더 많은 시간을 원하는 시간을 줄일 수 있으므로 쉽게 toodiscover hello 데이터 소스를 구성 하는 기능을 제공 합니다. 저장된 검색 및 고정된 데이터 자산은 이러한 핵심 기능을 작성하므로 사용자가 반복해서 작업하는 데이터 원본을 쉽게 식별할 수 있습니다.
