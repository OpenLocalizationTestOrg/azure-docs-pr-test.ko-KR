---
title: "aaaHow tooview 관련 Azure Data Catalog에서 데이터 자산 | Microsoft Docs"
description: "이 문서에서는 tooview Azure Data Catalog에서 선택한 데이터 자산의 데이터 자산을 연결 하는 방법을 설명 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>어떻게 tooview 데이터 자산 Azure Data Catalog에 관련 되어 있습니까?
Azure Data Catalog tooview 데이터 자산 선택 관련된 tooa 데이터 자산 및 뷰 간에 관계가 있습니다. 

## <a name="supported-data-sources"></a>지원되는 데이터 원본 
Hello 데이터 원본에서 데이터 자산을 등록 하면 Azure Data Catalog hello 선택한 데이터 자산 간의 관계 조인에 대 한 메타 데이터를 자동으로 등록 합니다. 

- SQL Server
- Azure SQL 데이터베이스
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>관련된 데이터 자산 보기
tooview 데이터 자산 관련된 tooa 선택한 데이터 집합을 사용 하 여 hello **관계** hello 다음 이미지에에서 나와 있는 것 처럼 탭: 

![Azure Data Catalog - 관련 데이터 자산 보기](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

이 예제에는 선택한 hello에 대 한 두 개의 관계가 **ProductSubcategory** 데이터 자산: 

- ProductSubcategoryID 열 hello Product 테이블의 외래 키 관계를 선택 하는 hello ProductSubcategory 테이블의 열이 다르다는 것에 있습니다. 
- Hello ProductSubCategory 테이블의 열 ProductCategoryID ProductCategoryID 열이 선택한 hello ProductCategory 테이블의 외래 키 관계를 있습니다.

> [!NOTE]
> Hello 화살표 방향으로 hello hello 관계 트리 보기에서 확인 합니다.  

toosee hello hello 열의 정규화 된 이름 같은 자세한 정보 hello 위로 마우스를 이동 하 고 다음 이미지는 팝업 비슷한 toohello 참조: 

![Azure Data Catalog - 관계 팝업](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

이미 등록 자산 간의 tooinclude 관계는 다시 해당 자산을 등록 합니다.

## <a name="next-steps"></a>다음 단계
- [어떻게 toomanage 데이터 자산](data-catalog-how-to-manage.md)
