---
title: "Azure 구독에 대 한 청구 또는 신용 경고를 aaaSet | Microsoft Docs"
description: "갑작스러운 청구에 당황하지 않도록 Azure 청구에 대한 경고를 설정하는 방법을 설명합니다."
keywords: "크레딧 경고, 청구 경고"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Microsoft Azure 구독에 대한 청구 또는 크레딧 경고 설정
Azure 구독에 대 한 hello 계정 관리자 인 경우 hello Azure 청구 경고 서비스 toocreate 사용자 지정 된 청구 경고 데 도움이 되는 모니터링 하 고 Azure 계정에 대 한 대금 청구 작업 관리를 사용할 수 있습니다.

이 서비스는 미리 보기, tooenable 필요 것 hello 미리 보기 기능 페이지에 먼저입니다.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Hello 경고 임계값 및 전자 메일 받는 사람 설정
1. 방문 [hello 미리 보기 기능 페이지](https://account.windowsazure.com/PreviewFeatures) 사용 하도록 설정 하 고 **청구 경고 서비스**합니다.

1. 구독에 대 한 hello 청구 서비스가 켜져 hello 전자 메일 확인을 받은 후 방문 [hello 구독 페이지](https://account.windowsazure.com/Subscriptions) hello 계정 포털에 있습니다. Hello 구독 toomonitor을 클릭 한 다음 클릭 **경고**합니다.

    ![강조 표시 하는 경고의 Azure 계정 센터 hello 구독 보기의 스크린샷][Image1]

2. 그런 다음 클릭 **경고 추가** toocreate 첫 번째 앱. 서로 다른 임계값으로 구독 당 5 개의 청구 경고의 요약을 하 고 각 경고에 대 한 tootwo 전자 메일 받는 사람을 설정할 수 있습니다.

    ![Hello 경고를 추가할 수 있는 경고 보기의 스크린샷][Image2]

3. 경고를 추가 하는 경우에 고유한 이름을 지정, 지출 임계값 선택한 hello 경고가 전송 된 전자 메일 주소를 선택 합니다. Hello 임계값을 설정할 때 하나를 선택할 수 있습니다는 **청구 금액 합계** 또는 **화폐 성 차변** hello에서 **경고에 대 한** 목록입니다. 청구 금액 합계에 대 한 구독 지출이 hello 임계값을 초과 하는 경우 경고가 전송 됩니다. 화폐 성 차변에 대 한 금액 크레딧을 hello 한도 아래로 떨어지면 때 경고가 전송 됩니다. 일반적으로 화폐 성 차변 tooFree 평가판 및 Visual Studio 구독을 적용 합니다.

    ![받는 사람을 구성할 수 있는 hello 추가 경고 보기의 스크린샷][Image3]

Azure에서는 모든 전자 메일 주소를 지원 하지만 hello 전자 메일 주소가 작동 하는지 확인를 하지 있으므로 입력 오류를 다시 확인 합니다.

## <a name="check-on-your-alerts"></a>경고 확인
경고를 설정 하면 r e 계정 센터 hello 나열 하 고 개수를 설정할 수 있습니다 더을 보여 줍니다. 각 경고에 대 한 hello 날짜와 보낸 것, 청구 금액 합계 또는 금액 크레딧에 대 한 경고 인지 시간을 설정 하는 hello 제한 참조 합니다. hello 날짜 및 시간 형식이 24 시간 조정 UTC (Universal Time)이 고 hello 날짜가 yyyy-월-일 형식입니다. Hello 클릭 플러스, hello 목록 tooedit에서 경고에 대 한 서명 하거나 hello 휴지통에 있는 toodelete 클릭 것입니다.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>EA(기업 계약) 고객의 청구 경고
EA 고객은 지출 할당량을 설정하여 등록 상태인 각 부서에 대한 경고를 받을 수 있습니다. 참조 [부서 지출 할당량](https://ea.azure.com/helpdocs/departmentSpendingQuotas) hello EA 포털 tooget 시작에 있습니다.

## <a name="learn-more-about-azure-cost-management"></a>Azure 비용 관리에 대한 자세한 정보
- Hello를 사용 하 여 비용을 예측 [가격 계산기](https://azure.microsoft.com/pricing/calculator/), [총 비용 소유권 계산기의](https://aka.ms/azure-tco-calculator), 및 서비스를 추가 하는 경우.
- [Azure Portal에서 정기적으로 사용량 및 비용을 검토합니다](billing-getting-started.md#costs).
- [Azure Advisor 비용 권장 사항](../advisor/advisor-cost-recommendations.md)을 켭니다.

toolearn 더 참조 [Azure 비용 관리 지침](billing-getting-started.md)합니다.

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
