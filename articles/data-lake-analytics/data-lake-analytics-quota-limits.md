---
title: "Azure Data Lake Analytics 할당량 제한 | Microsoft Docs"
description: "ADLA(Azure Data Lake Analytics) 계정에서 할당량 한도를 조정하고 늘리는 방법을 알아봅니다."
services: data-lake-analytics
keywords: "Azure 데이터 레이크 분석"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Azure Data Lake Analytics 할당량 한도

ADLA(Azure Data Lake Analytics) 계정에서 할당량 한도를 조정하고 늘리는 방법을 알아봅니다. 이러한 한도를 알면 U-SQL 작업 동작을 이해하는 데 도움이 될 수 있습니다. 모든 할당량 한도는 소프트 한도이며, Microsoft에 문의하여 최대 한도를 늘릴 수 있습니다.

## <a name="azure-subscriptions-limits"></a>Azure 구독 한도

**구독당 최대 ADLA 계정 수:** 5.

 이는 구독당 만들 수 있는 ADLA 계정의 최대 개수입니다. 6번째 ADLA 계정을 만들려고 하면 "구독 이름에 따라 지역에서 허용되는 Data Lake Analytics 계정의 최대 수(5)에 도달했습니다." 오류가 발생합니다. 이 경우 사용하지 않는 모든 ADLA 계정을 삭제하거나 [지원 티켓을 열어](#increase-maximum-quota-limits) Microsoft에 문의합니다.

## <a name="adla-account-limits"></a>ADLA 계정 한도

**계정당 최대 AU(분석 단위) 수:** 250.

이는 계정에서 동시에 실행할 수 있는 AU의 최대 개수입니다. 모든 작업 간에 실행 중인 총 AU 수가 이 한도를 초과하면 최신 작업이 자동으로 큐에 대기됩니다. 예:

* 250AU로 실행되는 작업이 하나뿐인 경우 두 번째 작업을 제출하면 첫 번째 작업이 완료될 때까지 이 작업이 작업 큐에서 대기합니다.
* 이미 5개의 작업이 실행 중이고 각각 50AU를 사용하는 경우 20AU가 필요한 6번째 작업을 제출하면 20AU가 사용 가능 상태가 될 때까지 작업 큐에서 대기합니다.

**계정당 동시 U-SQL 작업의 최대 수:** 20.

이는 계정에서 동시에 실행할 수 있는 작업의 최대 개수입니다. 이 값을 초과하면 최신 작업이 자동으로 큐에 대기합니다.

## <a name="adjust-adla-quota-limits-per-account"></a>계정당 ADLA 할당량 한도 조정

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.
2. 기존 ADLA 계정을 선택합니다.
3. **속성**을 클릭합니다.
4. **병렬 처리** 및 **동시 작업**을 요구 사항에 맞게 조정합니다.

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>최대 할당량 한도 늘리기

1. Azure Portal에서 지원 요청을 엽니다.

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. 문제 유형을 **할당량**으로 선택합니다.
3. **구독**을 선택합니다("평가판" 구독이 아닌지 확인).
4. 할당량 유형을 **Data Lake Analytics**로 선택합니다.

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. 문제의 블레이드에서 요청한 증가 한도 및 이 추가 용량이 필요한 이유에 대한 **세부 정보**를 설명하세요.

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. 연락처 정보를 확인하고 지원 요청을 만듭니다.

Microsoft에서 요청을 검토하고 최대한 빨리 비즈니스 요구를 수용하려고 합니다.

## <a name="next-steps"></a>다음 단계

* [Microsoft Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Azure PowerShell을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-powershell.md)
* [Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
