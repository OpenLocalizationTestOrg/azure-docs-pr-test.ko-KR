---
title: "aaaHow tooscale Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 어떻게 tooscale Azure 시간 계열 Insights 환경"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>어떻게 tooscale 시간 시계열 Insights 환경

이 자습서에서는 어떻게 tooscale 시간 시계열 Insights 환경입니다.

> [!NOTE]
> SKU 형식 전반에서의 강화는 허용되지 않습니다. S1 SKU를 사용한 환경은 S2 환경으로 변환할 수 없습니다.

## <a name="s1-sku-ingress-rates-and-capacities"></a>S1 SKU 수신 속도 및 용량

| S1 SKU 용량 | 수신 속도 | 최대 저장소 용량
| --- | --- | --- |
| 1 | 1GB(1백만 이벤트) | 매달 30GB(3천만 이벤트) |
| 10 | 10GB(1천만 이벤트) | 매달 300GB(3억 이벤트) |

## <a name="s2-sku-ingress-rates-and-capacities"></a>S2 SKU 수신 속도 및 용량

| S2 SKU 용량 | 수신 속도 | 최대 저장소 용량
| --- | --- | --- |
| 1 | 10GB(1천만 이벤트) | 매달 300GB(3억 이벤트) |
| 10 | 100GB(1억 이벤트) | 매달 3TB(30억 이벤트) |

용량은 연속해서 크기가 조정되므로 용량 2의 S1 SKU는 일일 2GB(2백만) 이벤트 수신 속도 및 매달 60GB(6천만 이벤트)를 지원합니다.

## <a name="changing-hello-capacity-of-your-environment"></a>사용자 환경의 hello 용량 변경

1. Hello Azure 포털에서에서 선택 hello 환경 용량 toochange 원하는 합니다.
1. 설정에서 구성을 클릭합니다.
1. Hello 용량 슬라이더 tooselect hello 수신 속도 대 한 hello 요구 사항을 충족 하는 용량과 저장소 용량을 사용 합니다.

## <a name="next-steps"></a>다음 단계

* Hello 새 용량이 충분 한지 확인 tooprevent 제한 합니다. 자세한 내용은 참조 hello *환경 있습니다 수 제한에 이르기* 섹션 [여기](time-series-insights-diagnose-and-solve-problems.md)합니다.
