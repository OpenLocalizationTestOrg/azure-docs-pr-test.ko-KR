---
title: "응용 프로그램 Insights 원격 분석 데이터 모델-aaaAzure 이벤트 원격 분석 | Microsoft Docs"
description: "이벤트 원격 분석을 위한 Azure Application Insights 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>이벤트 원격 분석: Application Insights 데이터 모델

원격 분석 항목 이벤트를 만들 수 있습니다 (에서 [Application Insights](app-insights-overview.md)) toorepresent 응용 프로그램에서 발생 하는 이벤트입니다. 일반적으로 이 작업은 단추 클릭 또는 주문 체크 아웃과 같은 사용자 조작입니다. 초기화 또는 구성 업데이트 같은 응용 프로그램 수명 주기 이벤트일 수도 있습니다. 

의미상으로 이벤트 수도 상관 관계가 지정 된 toorequests 되지 않을 수 있습니다. 하지만 제대로 사용될 경우 이벤트 원격 분석은 요청이나 추적보다 더 중요합니다. 이벤트 비즈니스 원격 분석을 나타내고 보다 낮은 값 제목 tooseparate 해야 [샘플링](app-insights-api-filtering-sampling.md)합니다.

## <a name="name"></a>이름

이벤트 이름입니다. tooallow 적절 한 그룹화 및 유용한 메트릭 적은 수의 별도 이벤트 이름 생성 되도록 응용 프로그램을 제한 합니다. 예를 들어 생성된 이벤트 인스턴스마다 별도의 이름을 사용하지 않습니다.

최대 길이: 512자

## <a name="custom-properties"></a>사용자 지정 속성

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>사용자 지정 측정

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>다음 단계

- Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.
- [사용자 지정 이벤트 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md#trackevent).
- Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.
