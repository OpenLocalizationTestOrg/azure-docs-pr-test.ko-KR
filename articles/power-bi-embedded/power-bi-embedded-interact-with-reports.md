---
title: "hello JavaScript API를 사용 하 여 보고서와 aaaInteract | Microsoft Docs"
description: "Power BI 포함, hello JavaScript API를 사용 하 여 보고서와 상호 작용"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Hello JavaScript API를 사용 하 여 Power BI 보고서와 상호 작용
hello Power BI JavaScript API를 사용 하면 tooeasily 응용 프로그램에 Power BI 보고서를 포함 합니다. API hello로 응용 프로그램 페이지 및 필터와 같은 다른 보고서 요소 프로그래밍 방식으로 조작할 수 있습니다. 이러한 상호 작용은 Power BI 보고서가 응용 프로그램에 더욱 통합되게 합니다.

Hello 응용 프로그램의 일부로 호스팅되는 iframe을 사용 하 여 응용 프로그램에서 Power BI 보고서를 포함 합니다. hello iframe 한 경계 역할을 응용 프로그램 및 hello 보고서 간에 hello 다음 이미지에서에서 볼 수 있습니다. 

![Javascript API가 포함되지 않은 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

hello JavaScript API hello 없이 보고서 및 응용 프로그램 없습니다 서로 상호 작용 낮지만 hello iframe 훨씬 쉽게 프로세스를 포함 하는 hello를 만듭니다. 이 처럼 상호 작용의 hello 보고서는 실제로 hello 응용 프로그램의 일부와 같은 모습 가능 합니다. hello 보고서 및 응용 프로그램 hello 다음 이미지와 같이 실제로 toocommunicate 주고받는 필요 합니다.

![Javascript API가 포함된 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Power BI JavaScript API hello toowrite 코드를 hello iframe 경계를 통해 안전 하 게 전달할 수 있습니다. 이 사용 하면 응용 프로그램 tooprogrammatically, 보고서 및 toolisten hello 보고서 내에서 사용자가 구성 하는 작업에서 이벤트에 대 한 작업을 수행 합니다.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Power BI JavaScript API hello로 합니까?
Hello JavaScript API로 보고서를 관리, 보고서에서 toopages 탐색, 보고서를 필터링를 처리할 수 있습니다 이벤트를 포함 합니다. hello 다음 다이어그램에서는 hello API의 hello 구조

![Power BI JavaScript API 다이어그램](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>보고서 관리
hello Javascript API hello 보고서 및 페이지 수준에서 toomanage 동작을 사용 합니다.

* 응용 프로그램에서 특정 Power BI 보고서를 안전 하 게 포함-hello 테스트 [데모 응용 프로그램 포함](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * 액세스 토큰 설정
* Hello 보고서 구성
  * 사용 및 hello 필터 창 및 페이지 탐색 창 사용 안 함-hello 시도 [설정 데모 응용 프로그램 업데이트](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * 페이지 및 필터에 대 한 기본값 설정-hello 테스트 [집합 기본값 데모](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* 전체 화면 모드 시작 및 종료

[포함 보고서에 대해 자세히 알아보기](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>보고서에서 toopages 이동
hello JavaScript API enbales 있습니다 toodiscover 모든 보고서 및 tooset hello 현재 페이지에서 페이지입니다. Hello 시도 [탐색 데모 응용 프로그램](http://azure-samples.github.io/powerbi-angular-client/#/scenario3)합니다.

[페이지 탐색에 대해 자세히 알아보기](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>보고서 필터링
기본 및 고급 기능이 포함 된 보고서 및 보고서 페이지에 대 한 필터링 hello JavaScript API를 제공 합니다. Hello 시도 [데모 응용 프로그램을 필터링](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), 여기에 소개 코드를 검토 합니다.  

#### <a name="basic-filters"></a>기본 필터
기본 필터는 열 또는 계층 수준에 배치 되며 값 tooinclude 또는 제외 목록을 포함 합니다.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>고급 필터
Hello 논리 연산자를 사용 하 여 고급 필터 및 또는 OR, 자신의 연산자 및 값 반반씩 하나 또는 두 개의 조건을 적용 하 고 있습니다. 지원되는 조건은 다음과 같습니다.

* 없음
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* 포함
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[필터링에 대해 자세히 알아보기](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>이벤트 처리
또한 hello iframe에 toosending 정보, 응용 프로그램도 정보를 받을 수 hello hello iframe에서 오는 이벤트 뒤에:

* Embed
  * loaded
  * error
* 보고서
  * pageChanged
  * dataSelected(출시 예정)

[이벤트를 처리하는 방법에 대해 자세히 알아보기](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>다음 단계
Hello Power BI JavaScript API에 대 한 자세한 내용은 다음 링크는 hello 확인해 보세요.

* [JavaScript API Wiki](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [개체 모델 참조](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* 샘플
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [라이브 데모](https://microsoft.github.io/PowerBI-JavaScript/demo/)

