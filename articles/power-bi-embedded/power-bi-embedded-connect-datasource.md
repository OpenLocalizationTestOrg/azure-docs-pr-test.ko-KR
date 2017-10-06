---
title: "aaaMicrosoft Power BI 포함-tooa 데이터 원본 연결"
description: "Power BI 포함, toodata 소스 연결"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Tooa 데이터 원본에 연결
**Power BI Embedded**를 사용하여 사용자 고유의 앱에 보고서를 포함할 수 있습니다. 앱에 Power BI 보고서를 포함 하는 경우 hello 보고서 toohello 내부에서 데이터를 연결 하는 **가져오기** hello 데이터 또는 복사본 **직접 연결** toohello 데이터 소스를 사용 하 여  **DirectQuery**합니다.

다음은 hello를 사용 하 여 차이점 **가져오기** 및 **DirectQuery**합니다.

| 가져오기 | DirectQuery |
| --- | --- |
| 테이블, 열, *및 데이터* 가져오거나 hello 보고서의 데이터 집합에 복사 됩니다. toosee 해당 오류가 발생 했습니다 toohello 기본 데이터 변경, 새로 고침 또는, 완전 하 고 현재 데이터 집합 가져오기 다시 해야 합니다. |만 *테이블 및 열* 가져오거나 hello 보고서의 데이터 집합에 복사 됩니다. 항상 hello 최신 데이터를 볼 있습니다. |

Power BI Embedded를 사용하면 클라우드 데이터 원본에서 DirectQuery를 사용할 수 있지만, 현재 온-프레미스 데이터 원본에서는 사용할 수 없습니다.

> [!NOTE]
> hello 온-프레미스 데이터 게이트웨이 지원 되지 않습니다 Power BI embedded이 이번에. 즉, DirectQuery를 온-프레미스 데이터 원본과 사용할 수 없습니다.

## <a name="supported-data-sources"></a>지원되는 데이터 원본

**DirectQuery**
* Azure SQL 데이터베이스
* Azure SQL 데이터 웨어하우스

**가져오기**

모든 Power BI Desktop 내에서 사용 가능한 데이터 원본 hello 사용 하 여 가져올 수 있습니다. **하지** 수 toorefresh 내 Power BI 포함 해당 데이터를 수 있습니다. Tooupload 변경 해야 tooyour PBIX 파일 tooPower BI 포함 합니다. 사용 가능한 게이트웨이 toono 때문입니다. 

## <a name="benefits-of-using-directquery"></a>DirectQuery 사용할 경우의 이점
**DirectQuery**를 사용할 경우 다음 두 가지 주요 이점이 있습니다.

* **DirectQuery** 작성할 수 있습니다 시각화 여기서 그렇지 않은 경우는 것이 실행할 수 없는 toofirst 가져오기 매우 큰 데이터 집합을 통해 모든 데이터 hello 합니다.
* 기본 데이터를 변경 하면 데이터 새로 고침 필요할 수 있습니다 하며 일부 보고서에 대 한 hello 필요 toodisplay 현재 데이터 수 대량 데이터 전송에 있으므로 데이터 다시 가져오기를 실행할 수 없습니다. 반면, **DirectQuery** 보고서는 항상 현재 데이터를 사용합니다.

## <a name="limitations-of-directquery"></a>DirectQuery의 제한 사항
   몇 가지 제한 사항이 toousing **DirectQuery**:

* 모든 테이블을 단일 데이터베이스에서 가져와야 합니다.
* Hello 쿼리가 지나치게 복잡 한 경우 오류가 발생 합니다. tooremedy hello 오류는 덜 복잡 하므로 hello 쿼리를 리팩터링 해야 합니다. 사용 하지 않고 tooimport hello 데이터 할 hello 쿼리 해야 복잡할 경우 **DirectQuery**합니다.
* 관계 필터링은 양방향이 아닌 단일 방향 tooa 제한 됩니다.
* Hello 데이터 형식의 열을 변경할 수 없습니다.
* 기본적으로 제한은 측정값에 허용되는 DAX 식에 적용됩니다. [DirectQuery 및 측정값](#measures)을 참조하세요.

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery 및 측정값
기본 데이터 원본의 toohello 전송 tooensure 쿼리의 성능이 적절 한지, 측정값에 제한이 적용 됩니다. 사용 하는 경우 **Power BI Desktop**, 고급 사용자가 선택할 수 toobypass이이 제한을 선택 하 여 **파일 > 옵션 및 설정 > 옵션**합니다. Hello에 **옵션** 대화 상자에서 선택 **DirectQuery**, hello 옵션을 선택 하 고 **DirectQuery 모드에서 제한 되지 않은 측정값 허용**합니다. 이 옵션을 선택하면 측정값에 유효한 모든 DAX 식을 사용할 수 있습니다. 사용자가 알고; 있어야 합니다. 그러나 쿼리가 매우 느려질 toohello 백 엔드 발생할 수 있습니다는 일부 식은 하는 때 매우 잘 수행 hello 데이터를 가져올 때 원본 **DirectQuery** 모드입니다. 

## <a name="see-also"></a>참고 항목
* [Microsoft Power BI Embedded 시작](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)

