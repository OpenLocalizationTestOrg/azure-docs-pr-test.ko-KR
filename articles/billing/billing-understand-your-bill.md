---
title: "aaaUnderstand azure 청구서 | Microsoft Docs"
description: "자세한 내용은 방법 tooread 하 고 사용 현황 및 Azure 구독에 대 한 이해"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Microsoft Azure 청구서 이해
toounderstand Azure 청구 hello 자세한 일일 사용량 파일 및 hello hello Azure 포털에서에서 관리 보고서를 비용 청구서를 비교 합니다.

청구서의 PDF와 자세한 일일 사용량 파일 CSV 다운로드의 복사본이 tooobtain 참조 [Azure 청구서 및 일일 사용 현황 데이터를 청구 가져오기](billing-download-azure-invoice-daily-usage-date.md)합니다. 

청구서 및 자세한 일별 사용 현황 파일의 자세한 용어 및 설명은 [Microsoft Azure 청구서의 용어 이해](billing-understand-your-invoice.md) 및 [Microsoft Azure 자세한 사용 현황의 용어 이해](billing-understand-your-usage.md)를 참조하세요. 

관리 보고서를 비용 hello에 대 한 세부 정보를 참조 하십시오. [Azure 포털 비용 관리](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started)합니다.


## <a name="charges"></a>내 송장에 hello 요금 정확한 지 확인 하려면 어떻게 해야 합니까?
자세한 내용을 보려는 청구서에 대한 요금이 청구되는 경우 다음과 같은 두 가지 옵션이 있습니다.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>옵션 1: 청구서를 검토 하 고 자세한 hello로 hello 사용과 비용을 비교 하 CSV 파일 사용

hello 자세한 사용 CSV 파일을 보여 줍니다 사용자의 요금 청구 기간 및 일일 사용량. tooget 자세한 사용 현황 CSV 파일 참조 [Azure 청구서 및 일일 사용 현황 데이터를 청구 가져오기](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date)합니다.

Hello 미터 수준에서 사용 요금이 표시 됩니다. hello 다음 용어가 처럼 두 hello 송장 이와 같은 기능이 hello 자세한 사용 파일 hello 됩니다. 예를 들어 결제 hello 청구서에 주기 hello 해당 toohello 청구 기간의 hello 자세한 사용 파일에 표시 된 것입니다.

 | 청구서(PDF) | 자세한 사용 현황(CSV)|
 | --- | --- |
|대금 청구 주기 | 청구 기간 |
 |이름 |측정기 범주 |
 |형식 |미터 하위 범주 |
 |리소스 |측정기 이름 |
 |지역 |측정기 영역 |
 |사용 |소비된 수량 |
 |포함됨 |표함된 수량 |
 |청구 가능 |초과 수량 |

hello **사용 요금** 청구서의 섹션에는 청구 기간 동안 사용 된 각 수준에 대 한 hello 총 값입니다. 예를 들어 hello 다음 스크린샷은 hello Azure 스케줄러 서비스에 대 한 사용 요금이 청구 됩니다.

![청구서 사용 요금](./media/billing-understand-your-bill/1.png)

hello **문을** 섹션 자세한 사용 현황 CSV의 표시 hello 동일한 요금이 청구 됩니다. 두 hello *사용 됨* 양 및 *값* hello 송장 일치 합니다.

![CSV 사용 요금](./media/billing-understand-your-bill/2.png)

매일, 이동 toohello 대금이 청구를 간략하게 toosee **일일 사용량** hello CSV의 섹션입니다. 아래 "스케줄러"에 대 한 필터링 *미터 범주* 일 hello 미터는 사용 되 고 사용 된 양을 확인할 수 있습니다. hello *리소스* 및 *리소스 그룹* 정보가 비교에도 나열 됩니다. hello *사용 됨* hello 청구서에 표시 된 값 toowhat의를 추가 해야 합니다.

![일별 사용 현황 섹션 hello CSV에서](./media/billing-understand-your-bill/3.png)

하루에 tooget hello 비용 곱하기 hello *사용 됨* hello 시간과 *속도* hello에서 값 **문을** 섹션.

toolearn hello 송장에 대 한 자세한 참조 [Azure 청구서 이해](billing-understand-your-invoice.md)합니다.

toolearn hello CSV의에서 hello 열 각각에 대 한 참조 [Azure 자세한 사용량을 이해](billing-understand-your-invoice.md)합니다.

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>옵션 2: 청구서를 검토 하 고 hello 사용량과 hello Azure 포털에서에서 비용을 비교 합니다.

Azure 포털 hello 수 사용자 요금을 확인 하는 데도 도움이 됩니다. hello Azure 포털 사용 및 hello 요금 청구서의 간략 한 개요에 대 한 비용 관리 차트를 제공 합니다.

hello 위의 예제에서와 toocontinue 방문 hello [구독 페이지](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)구독을 선택한 다음 선택 **비용 분석**합니다. 여기에서 hello 시간 범위를 지정 하 고 hello Azure 스케줄러 서비스에 대 한 사용 요금을 확인할 수 있습니다.

![Azure Portal의 비용 분석 보기](./media/billing-understand-your-bill/4.png)

toosee hello 일별로 비용 구분 **기록 비용**, hello 행을 클릭 합니다.

![Azure Portal의 비용 내역 뷰](./media/billing-understand-your-bill/5.png)

toolearn 더 참조 [Azure 청구 및 비용 관리를 사용 하 여 예기치 않은 비용을 방지](billing-getting-started.md#costs)합니다.

## <a name="external"></a>외부 서비스 요금은 어떤가요?
외부 서비스(또는 Azure Marketplace 주문)는 독립 서비스 공급업체에서 제공하며 별도로 청구됩니다. hello 요금 Azure 청구서에 표시 하지 않습니다. toolearn 더 참조 [사용자의 Azure 외부 서비스 요금 이해](billing-understand-your-azure-marketplace-charges.md)합니다.

## <a name="payment"></a>지불하려면 어떻게 할까요?

결제 방법으로 신용 카드 또는 직불 카드를 설정한 경우 hello 청구 기간이 종료 된 후 10 일 이내에 자동으로 hello 지불 대금이 청구 됩니다. 신용 카드 명세서에 hello 품목 말하고 **MSFT Azure**합니다.

경우 있습니다 [송장으로 지불](billing-how-to-pay-by-invoice.md), 청구서 hello 맨 아래에 나열 된 지불 toohello 위치 송신 합니다. 자세한 도움말은 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>신용 카드로 지급액의 hello 상태는 어떻게 확인할 수 있습니까?

[지원 티켓을 만드세요](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask 결제의 hello 상태에 대 한 합니다. 

## <a name="tips-for-cost-management"></a>비용 관리 팁
- Hello를 사용 하 여 비용을 예측 [가격 계산기](https://azure.microsoft.com/pricing/calculator/) 및 [총 비용 소유권 계산기의](https://aka.ms/azure-tco-calculator), 가져오고, hello [자세한 가격 정보 각 서비스에 대 한](https://azure.microsoft.com/en-us/pricing/)합니다.
- [청구 경고 설정](billing-set-up-alerts.md)
- [사용 및 비용 hello Azure 포털에 정기적으로 검토](billing-getting-started.md#costs)합니다.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.

도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
