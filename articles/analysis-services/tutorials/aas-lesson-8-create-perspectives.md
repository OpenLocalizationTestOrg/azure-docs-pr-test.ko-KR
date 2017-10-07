---
title: "aaa \"Azure Analysis Services 자습서 단원 8 만들기 큐브 뷰 | \"Microsoft Docs"
description: "큐브 뷰 toocreate Azure Analysis Services tutorial 프로젝트 hello 하는 방법을 설명 합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>단원 8: 큐브 뷰 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 인터넷 판매 큐브 뷰를 만듭니다. 큐브 뷰는 포커스가 있는, 비즈니스 또는 응용 프로그램별 관점을 제공하는 모델의 볼 수 있는 하위 집합을 정의합니다. Tooa 모델 큐브 뷰를 사용 하 여 연결 하는 사용자, 이러한 모델 개체 (테이블, 열, 측정값, 계층 및 Kpi) 해당 큐브 뷰에 정의 된 필드로 표시 됩니다. toolearn 더 참조 [큐브 뷰](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular)합니다.
  
이 단원에서 만드는 Internet Sales 큐브 뷰에 hello hello DimCustomer 테이블 개체는 제외 됩니다. 보기에서 특정 개체를 제외 하는 큐브 뷰를 만들 때 해당 개체는 여전히 hello 모델에 존재 합니다. 그러나 보고 클라이언트 필드 목록에 표시되지 않습니다. 큐브 뷰에 포함되었거나 포함되지 않은 계산된 열과 측정값은 여전히 제외된 개체 데이터에서 계산할 수 있습니다.  
  
hello이 단원의 목적은 toodescribe 어떻게 toocreate 큐브 뷰 및 hello 테이블 형식 모델 작성 도구에 잘 알고 있습니다. 나중에이 모델 tooinclude 추가 테이블을 확장 하는 경우 toodefine 다양 한 뷰포인트 hello 모델의 예를 들어: Inventory 및 Sales 큐브 뷰를 추가로 만들 수 있습니다.  
  
이 단원에서는 시간 toocomplete 예상: **5 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [7 단원: 핵심 성과 지표 만들기](../tutorials/aas-lesson-7-create-key-performance-indicators.md)합니다.  
  
## <a name="create-perspectives"></a>큐브 뷰 만들기  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate를 인터넷 판매 큐브 뷰  
  
1.  Hello 클릭 **모델** 메뉴 > **큐브 뷰** > **만들기 및 관리**합니다.  
  
2.  Hello에 **큐브 뷰** 대화 상자를 클릭 **새 큐브 뷰**합니다.  
  
3.  Hello를 두 번 클릭 **새 큐브 뷰** 열 머리글을 한 후 이름 바꾸기를 **인터넷 판매**합니다.  
  
4.  선택 hello 모든 hello 테이블 *제외 하 고* **DimCustomer**합니다.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    이후의 단원에서는 기능 tootest Excel에서에서 분석 hello이 큐브이 뷰를 사용 합니다. Excel 피벗 테이블 필드 목록 hello hello DimCustomer 테이블을 제외한 각 테이블이 포함 되어 있습니다.  

## <a name="whats-next"></a>다음 작업
[단원 9: 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)
  
  
  
  
