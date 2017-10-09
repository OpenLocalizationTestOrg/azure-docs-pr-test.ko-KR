---
title: "Azure Analysis Services에서 aaaData 모델 호환성 수준 | Microsoft Docs"
description: "테이블 형식 데이터 모델 호환성 수준을 이해합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 테이블 형식 모델에 대한 호환성 수준

*호환성 수준이* hello Analysis Services 엔진 toorelease 관련 동작을 나타냅니다. 변경 내용을 toohello 호환성 수준이 일반적으로 주요 버전의 SQL Server와 일치 합니다. 이러한 변경은 두 플랫폼 간의 toomaintain 패리티 Azure Analysis Services에에서도 구현 됩니다. 호환성 수준 변경은 테이블 형식 모델에서 사용할 수 있는 기능에도 영향을 줍니다. 예를 들어 DirectQuery 및 테이블 형식 개체 메타 데이터는 서로 다른 구현이 hello 호환성 수준에 따라 합니다. 

Azure Analysis Services hello 1400 및 1200 호환성 수준의 테이블 형식 모델을 지원합니다.

hello 최신 호환성 수준은 1400 합니다. 이 수준은 SQL Server 2017 Analysis Services와 일치합니다. Hello 1400 호환성 수준에서 주요 기능은 다음과 같습니다.

*  TOM API 및 TMSL 스크립트에 대한 지원으로 데이터 연결 및 테이블 형식 모델로 가져오기에 대한 새로운 인프라. 이 새로운 기능을 통해 Azure Blob 저장소와 같은 추가 데이터 원본을 지원할 수 있습니다.
*  데이터 가져오기 및 M 식을 사용하여 데이터 변환 및 데이터 매시업 기능.
*  측정값은 DAX 식을 사용하여 세부 정보 행 속성을 지원합니다. 이 속성은 집계 된 보고서에서 toodetailed 데이터 Microsoft Excel toodrill와 같은 클라이언트 도구를 사용 합니다. 예를 들어 지역 및 월에 대 한 총 판매액을 보면 관련 된 hello 주문 세부 정보를 볼 수 있습니다. 
*  테이블 및 열에 대 한 개체 수준 보안 이름이 또한 toohello 데이터 그 안에 포함 됩니다.
*  불균형 계층 구조에 대한 향상된 지원.
*  성능 및 모니터링 향상.
  
## <a name="set-compatibility-level"></a>호환성 수준 설정 
 SSDT에서 새 테이블 형식 모델 프로젝트를 만들 때 hello에 hello 호환성 수준을 지정할 수 있습니다 **테이블 형식 모델 디자이너** 대화 상자. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Hello를 선택 하는 경우 **이 메시지를 다시 표시 안 함** 옵션을 모든 후속 프로젝트 hello 기본값으로 지정 하는 hello 호환성 수준을 사용 합니다. Ssdt의 hello 기본 호환성 수준을 변경할 수 있습니다 **도구** > **옵션**합니다.  
  
 tooupgrade 집합 hello SSDT에서는 기존 테이블 형식 모델 프로젝트 **호환성 수준이** hello 모델의 속성 **속성** 창. 에 유의 해야, hello 호환성 수준이 업그레이드은 취소할 수 없습니다.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>SQL Server Management Studio에서 테이블 형식 모델 데이터베이스에 대한 호환성 수준 확인 
 SSMS에서 hello 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준이**합니다.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>SSMS에서 서버에 대해 지원되는 호환성 수준 확인  
 SSMS에서 hello 서버 이름 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준을 지원**합니다.  
  
 이 속성에는 hello hello 서버 (미리 보기 제외)에서 실행 되는 데이터베이스의 가장 높은 호환성 수준을 지정 합니다. 지원 되는 hello 호환성 수준을 변경할 수 없습니다.  

## <a name="next-steps"></a>다음 단계
  [Azure Portal에서 모델 만들기](analysis-services-create-model-portal.md)   
  [Analysis Services 관리](analysis-services-manage.md)  
