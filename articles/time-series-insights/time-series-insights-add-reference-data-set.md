---
title: "aaaAdd 참조 데이터 집합 tooyour Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 참조 데이터 집합 tooyour 시간 계열 Insights 환경 추가"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Hello Ibiza 포털을 사용 하 여 시간 시계열 Insights 환경에 대 한 참조 데이터 집합 만들기

참조 데이터 집합은 이벤트 소스를 hello 이벤트와 보강 하는 항목의 컬렉션입니다. Time Series Insights 수신 엔진은 이벤트 원본의 이벤트와 참조 데이터 집합의 항목을 조인합니다. 이렇게 보강된 이벤트는 쿼리에 사용할 수 있습니다. 이 조인은 참조 데이터 집합에 정의 된 hello 키를 기반으로 합니다.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>단계 tooadd 참조 데이터 집합 tooyour 환경

1. Toohello 로그인 [Ibiza 포털](https://portal.azure.com)합니다.
2. Hello hello Ibiza 포털의 왼쪽에 hello 메뉴에서 "모든 리소스"를 클릭 합니다.
3. Time Series Insights 환경을 선택합니다.

    ![Hello 시간 계열 Insights 참조 데이터 집합 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. “참조 데이터 집합”을 선택하고, “+ 추가”를 합니다.

    ![Hello 시간 계열 Insights 참조 데이터 집합 세부 정보 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Hello hello 참조 데이터 집합 이름을 지정 합니다.
6. Hello 키 이름 및 해당 형식을 지정 합니다. 이 이름과 유형의 이벤트 소스에 hello 이벤트에서 사용 되는 toopick hello 올바른 속성입니다. 예를 들어, 키 이름으로 "DeviceId"과 "String" 형식이 제공 하는 경우 시간 시계열 Insights 수신 엔진이 hello 들어오는 이벤트에 "String" 형식의 "DeviceId" hello 이름의 속성을 찾아 다음 hello 합니다. Hello 이벤트와 둘 이상의 키 toojoin를 제공할 수 있습니다. 일치 하는 hello 속성 이름이 대/소문자 구분입니다.

     ![Hello 시간 계열 Insights 참조 데이터 집합 세부 정보 만들기](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. “만들기”를 클릭합니다.

## <a name="next-steps"></a>다음 단계

* 프로그래밍 방식으로 [참조 데이터를 관리](time-series-insights-manage-reference-data-csharp.md)합니다.
* Hello 전체 API 참조에 대 한 참조 [참조 데이터 API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) 문서.
