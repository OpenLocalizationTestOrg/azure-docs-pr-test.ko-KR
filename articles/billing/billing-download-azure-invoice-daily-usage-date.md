---
title: "Azure 청구 청구서 및 일일 사용 현황 데이터 aaaDownload | Microsoft Docs"
description: "어떻게 toodownload 또는 뷰의 사용자 Azure 청구 청구서 및 일일 사용량 데이터를 설명 합니다."
keywords: "청구서, 청구서 다운로드, azure 청구서, azure 사용 현황"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Azure 청구서 및 일간 사용 현황 데이터 다운로드 또는 보기
Hello에서 청구서를 다운로드할 수 있습니다 [Azure 포털](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) 하거나 전자 메일로 전송 하도록 합니다. toodownload 일일 사용량, 이동 toohello [Azure 계정 센터](https://account.windowsazure.com)합니다. 특정 역할에만 권한이 tooget을 청구 hello 계정 관리자와 같은 송장 및 사용 현황 정보를 갖습니다. 액세스 toobilling 정보 가져오기에 대해 자세히 toolearn 참조 [역할을 사용 하 여 청구 관리 액세스 tooAzure](billing-manage-access.md)합니다.

## <a name="get-your-invoice-in-email-pdf"></a>전자 메일로 청구서 받기(.pdf)
옵트인 수 있으며 전자 메일에서 다른 받는 사람이 tooreceive Azure 청구서를 구성할 수 없습니다. 지원 서비스, 기업 계약, Azure in Open 등의 특정 구독에는 이 기능이 제공되지 않을 수도 있습니다.

1. Hello에서 구독을 선택 [구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)합니다. 소유하고 있는 각 구독에 대해 옵트인합니다. **청구서**를 클릭한 다음 **전자 메일로 청구서 받기**를 클릭합니다. 

    ![Hello에 동의 흐름을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. 클릭 **옵트인** hello 약관에 동의 합니다.

    ![Hello에 동의 흐름을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Hello 계약을 적용 한 후에 받는 사람을 구성할 수 있습니다.

    ![Hello에 동의 흐름을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Hello 단계를 따른 후 전자 메일을 발생 하지 않는 hello에 메일 주소가 올바른지 확인 [프로필에 श े](https://account.windowsazure.com/profile)합니다.

## <a name="download-invoice-from-azure-portal-pdf"></a>Azure Portal에서 청구서 다운로드(.pdf)

1. Hello에서 구독을 선택 [구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) 으로 Azure 포털에서 [액세스 tooinvoices 사용 하는 사용자](billing-manage-access.md)합니다.

2. **청구서**를 선택합니다. 

    ![Hello 사용량 및 청구 옵션을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. 클릭 **청구서 다운로드** tooview PDF 청구서 사본 합니다. 표시 하는 경우 **사용할 수 없는**, 참조 [볼 수 없는 hello 마지막 청구 기간에 대 한 청구서?](#noinvoice)

    ![각 청구 기간의 청구 기간, hello 다운로드 옵션 및 총 요금을 보여주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. 또한 hello 청구 기간을 클릭 하 여 일일 사용량을 볼 수 있습니다. 

청구서에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing-understand-your-bill.md)를 참조하세요. 비용 관리에 대한 도움말은 [Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지](billing-getting-started.md)를 참조하세요.

## <a name="download-usage-from-hello-account-center-csv"></a>사용 현황 hello (.csv) r e 계정 센터에서 다운로드

1. Hello에 로그인 [Azure 계정 센터](https://account.windowsazure.com/subscriptions) 계정 관리자 hello으로 합니다.

2. Hello 송장 및 사용 정보 원하는 hello 구독을 선택 합니다.

3. **청구 내역**을 선택합니다. 

    ![청구 내역 옵션을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. 지난 6 개의 청구 기간 및 기간 unbilled 현재 hello hello에 대 한 문이 볼 수 있습니다. 

    ![각 청구 기간의 청구 기간, 옵션 toodownload 청구서 및 일일 사용량 및 총 요금을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. 선택 **현재 명세서 보기** toosee 예상 요금 hello hello 예상 시간에 생성 되었습니다. 이 정보는 매일 업데이트만 될 뿐 모든 사용량을 포함하지 않습니다. 월별 청구서는 이 예상과 다를 수 있습니다.

    ![Hello 현재 명세서 보기 옵션을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Hello 예상 현재 요금을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. 선택 **사용량 다운로드** CSV 파일로 toodownload hello 일별 사용 현황 데이터. 사용할 수 있는 두 가지 버전이 표시되면 버전 2를 다운로드합니다.

    ![Hello 사용량 다운로드 옵션을 보여 주는 스크린샷](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Hello 계정 관리자만 hello Azure 계정 센터에 액세스할 수 있습니다. 소유자와 같은 다른 대금 청구 관리자 hello를 사용 하 여 사용 현황 정보를 얻을 수 [청구 Api](billing-usage-rate-card-overview.md)합니다.

일간 사용 현황에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing-understand-your-bill.md)를 참조하세요. 비용 관리에 대한 도움말은 [Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지](billing-getting-started.md)를 참조하세요.

## <a name="noinvoice"></a>Hello 마지막 청구 기간에 대 한 송장을 표시 되지 않는 이유

몇 가지 이유로 인해 청구서가 보이지 않을 수 있습니다.

- 구독에 월별 크레딧 금액이 있고 이 금액을 초과하지 않았거나 무료 평가판을 사용하는 경우입니다. 청구서는 비용을 미납한 경우에만 생성됩니다.

- TooAzure 구독 hello 날짜 로부터 30 일 보다 작은 경우

- hello 송장 아직 생성 되지 않습니다. Hello hello 청구 기간 종료 될 때까지 기다립니다.

- 계정 관리자 hello 모르겠으면 이전 송장 노드가 tooyou 아닐 수 있습니다.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
여전히 있는 경우 추가 질문의 대답 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.

