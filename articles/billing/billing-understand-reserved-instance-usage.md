---
title: "종량제 구독에서 Azure Reserved Instance 사용량 이해 | Microsoft Docs"
description: "종량제 구독에서 Reserved Instance의 적용을 이해하기 위해 사용량을 참고하는 자세한 방법"
services: billing
documentationcenter: 
author: manish-shukla01
manager: manshuk
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/03/2017
ms.author: manshuk
ms.openlocfilehash: 6982d6177ef5c94436a28cd68beb9feb5cc343e5
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/16/2017
---
# <a name="understand-reserved-instance-usage-for-your-pay-as-you-go-subscription"></a>종량제 구독에서 Reserved Instance 사용량 이해

[예약 페이지](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade )의 ReservationId 및 [Azure 계정 포털](https://account.azure.com)의 사용량 파일을 사용하여 Reserved Instance의 활용을 이해합니다.


>[!NOTE]
>이 문서는 EA 고객에게는 적용되지 않습니다. EA 고객인 경우 [기업 등록에 Reserved Instance 사용량 이해](billing-understand-reserved-instance-usage-ea.md)를 참조하세요. 또한 이 문서는 예약이 단일 구독에 적용된다고 가정합니다. 예약이 둘 이상의 구독에 적용되면 예약 혜택이 여러 사용량 csv 파일에 걸쳐 있을 수 있습니다. 

다음 섹션에서는 미국 동부 지역에서 Standard_DS1_v2 Windows VM을 실행하고 예약 정보가 다음 표와 같다고 가정합니다.

| 필드 | 값 |
|---| :---: |
|ReservationId |8117adfb-1d94-4675-be2b-f3c1bca808b6|
|수량 |1|
|SKU | Standard_DS1_v2|
|지역 | eastus |

## <a name="reservation-application"></a>예약 응용 프로그램

배포된 VM이 예약 특성과 일치하기 때문에 VM의 하드웨어 부분이 포함됩니다. Reserved Instance에서 포함되지 않는 Windows 소프트웨어를 확인하려면 [Azure Reserve VM Instances Windows 소프트웨어 비용](billing-reserved-instance-windows-software-costs.md)으로 이동하세요.

### <a name="statement-section-of-csv"></a>csv의 문 섹션
csv의 이 섹션에서는 예약의 총 사용량을 보여줍니다. "Reservation-"이 포함된 미터 하위 범주 필드에 필터를 적용하면 데이터가 다음과 같은 스크린샷처럼 표시됩니다. ![다이렉트 문 예약](./media/billing-understand-reserved-instance-usage/billing-payg-reserved-instance-csv-statements.png)

예약 - 기본 VM 줄에는 예에 포함되는 총 시간이 있습니다. 이 줄은 Reserved Instance에서 포함되기 때문에 0원입니다. Reservation-Windows Svr(1 코어) 줄은 Windows 소프트웨어의 비용을 포함합니다.

### <a name="daily-usage-section-of-csv"></a>csv의 일일 사용량 섹션
추가 정보를 필터링하고 예약 ID를 입력합니다. 다음 스크린샷에서는 예약과 관련된 필드를 보여줍니다. 

![일일 사용 요금](./media/billing-understand-reserved-instance-usage/billing-payg-reserved-instance-csv-details.png)

1. 추가 정보 필드의 ReservationId는 VM에 혜택을 적용하는 데 사용된 예약입니다.
2. ConsumptionMeter는 VM에 대한 미터 ID입니다.
3. 예약 - 기본 VM 미터 하위 범주 선은 문 섹션에 있는 0원인 비용 줄을 나타냅니다. 예약에서 이미 이 VM을 실행하는 비용을 지불했습니다.
4. 예약에 대한 미터 ID입니다. 이 미터의 비용은 0원입니다. Reserved Instance를 정규화하는 VM에서는 비용을 설명하는 csv에 이 MeterId를 저장합니다. 
5. Standard_DS1_v2는 하나의 vCPU VM이며 해당 VM은 Azure Hybrid Benefit 없이 배포됩니다. 따라서 이 미터는 Windows 소프트웨어의 추가 요금을 포함합니다. [Azure Reserve VM Instances Windows 소프트웨어 비용](billing-reserved-instance-windows-software-costs.md)을 참조하여 D 시리즈 1 코어 VM에 해당하는 미터를 찾습니다. Azure Hybrid Benefit을 사용하면 이 추가 비용이 적용되지 않습니다. 

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.

다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.