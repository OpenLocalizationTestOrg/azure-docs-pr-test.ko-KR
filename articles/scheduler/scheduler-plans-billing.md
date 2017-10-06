---
title: "aaaPlans 및 Azure 스케줄러에 대 한 요금 청구"
description: "Azure 스케줄러의 버전 및 요금 청구"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Azure 스케줄러의 버전 및 요금 청구
## <a name="job-collection-plans"></a>작업 컬렉션 버전
작업 컬렉션은 Azure 스케줄러의 청구 가능한 엔터티에 hello입니다. 작업 컬렉션은 많은 작업을 포함하며 Free, Standard, Premium 등, 3가지 버전으로 제공됩니다.

| **작업 컬렉션 버전** | **작업 컬렉션당 최대 작업 수** | **최대 되풀이** | **구독당 최대 작업 컬렉션** | **제한** |
|:--- |:--- |:--- |:--- |:--- |
| **Free** |작업 컬렉션당 5개 작업 |시간당 1회. 한 시간에 한 번 이상 작업을 실행할 수 없습니다. |구독 too1 무료 작업 컬렉션을 사용할 수 |[HTTP 아웃바운드 권한 부여 개체](scheduler-outbound-authentication.md) |
| **Standard** |작업 컬렉션당 50개 작업 |1분당 1회. 1분에 한 번 이상 작업을 실행할 수 없습니다. |구독 too100 표준 작업 컬렉션을 사용할 수 |스케줄러의 액세스 toofull 기능 집합 |
| **P10 Premium** |작업 컬렉션당 50개 작업 |1분당 1회. 1분에 한 번 이상 작업을 실행할 수 없습니다. |구독은 too10, 000 P10 프리미엄 작업 컬렉션을 허용 됩니다. 자세한 내용은 <a href="mailto:wapteams@microsoft.com">저희에게 문의</a>하세요. |스케줄러의 액세스 toofull 기능 집합 |
| **P20 Premium** |작업 컬렉션당 1,000개 작업 |1분당 1회. 1분에 한 번 이상 작업을 실행할 수 없습니다. |구독은 too10, 000 P20 프리미엄 작업 컬렉션을 허용 됩니다. 자세한 내용은 <a href="mailto:wapteams@microsoft.com">저희에게 문의</a>하세요. |스케줄러의 액세스 toofull 기능 집합 |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>작업 컬렉션 버전의 업그레이드 및 다운그레이드
업그레이드 하거나 작업 컬렉션 계획을 언제 든 지 hello 무료, 표준 및 프리미엄 계획 중 다운 그레이드할 수 있습니다. 그러나 tooa 무료 작업 컬렉션을 다운 그레이드할 때 hello 다운 그레이드 hello 다음 이유 중 하나에 대해 실패할 수 있습니다.

* Hello 구독에는 무료 작업 컬렉션에 이미 있습니다.
* Hello 작업 컬렉션에서 작업의 무료 작업 컬렉션에서 작업에 허용 된 것 보다 더 높은 되풀이가 있습니다. 무료 작업 컬렉션에서 허용 하는 hello 최대 되풀이 시간 마다 한 번씩은
* Hello jobcollection 있는 5 개 보다 많이 작업
* Hello 작업 컬렉션의 작업을 사용 하는 HTTP 또는 HTTPS 작업에는 [HTTP 권한 부여 아웃 바운드 개체](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>청구 및 Azure 버전
Free 작업 컬렉션에서는 구독이 청구되지 않습니다. 더 나은 거래 toohave는 100 개 이상의 표준 작업 컬렉션 (10 명의 표준 청구 단위), 있는 경우 모든 작업 컬렉션을 hello 프리미엄 요금제에 있습니다.

Standard 작업 컬렉션이 하나이고 Premium 작업 컬렉션이 하나라면 Standard 청구 단위 1개 *와* Premium 청구 단위 1개가 청구됩니다. hello 스케줄러 서비스 비용을 hello tooeither 표준 또는 프리미엄; 설정 된 활성 작업 컬렉션 수에 따라 이 hello 다음 두 섹션의 내용을 설명 합니다.

## <a name="standard-billable-units"></a>Standard 청구 가능 단위
표준 청구 단위 too10 표준 작업 컬렉션을 포함할 수 있습니다. 작업 컬렉션 당 too50 작업도 표준 작업 컬렉션 수 없으므로 한 표준 요금 청구 단위 too500 작업도 – 매달 tooalmost 22 백만 작업 실행을 구독 toohave를 수 있습니다.

Standard 작업 컬렉션 수가 1~10인 경우 1개의 Standard 청구 단위에 대해 청구됩니다. Standard 작업 컬렉션 수가 11~20인 경우 2개의 Standard 청구 단위에 대해 청구됩니다. Standard 작업 컬렉션 수가 21~30인 경우 3개의 Standard 청구 단위에 대해 청구되는 식입니다.

## <a name="p10-premium-billable-units"></a>P10 Premium 청구 가능 단위
P10 프리미엄 청구 단위 too10, 000 P10 프리미엄 작업 컬렉션을 포함할 수 있습니다. 작업 컬렉션 당 too50 작업도 P10 프리미엄 작업 컬렉션 수 없으므로 한 premium 청구 단위를 한 달 tooalmost 22 십억 작업 실행 – too500, 000 작업을 구독 toohave 수 있습니다.

Standard 작업 컬렉션 수가 1~10,000인 경우 1개의 P10 Premium 청구 단위에 대해 청구됩니다. Standard 작업 컬렉션 수가 10,001~20,000인 경우 2개의 P10 Premium 청구 단위에 대해 청구됩니다.

따라서 P10 프리미엄 작업 컬렉션에 있는지 hello 동일한 기능을 응용 프로그램에 작업 컬렉션을 많이 필요한 경우 하지만 hello 표준 작업 컬렉션 가격 나누기를 제공 합니다.

## <a name="p20-premium-billable-units"></a>P20 Premium 청구 가능 단위
P20 프리미엄 청구 단위 too5, 000 P20 프리미엄 작업 컬렉션을 포함할 수 있습니다. P20 프리미엄 작업 컬렉션 too1, 000 작업 컬렉션 작업을 가질 수 있으므로 하나의 프리미엄 청구 단위 too5, 000, 000 작업 – 매달 tooalmost 220 십억 작업 실행을를 구독 toohave를 수 있습니다.

P20 프리미엄 작업 컬렉션 hello P10 프리미엄 작업 컬렉션와 동일한 기능을 제공 하지만 작업 컬렉션 및 총 보다 큰 수를 전체 작업의 P10 프리미엄 가능 하면 toohave 당 큰 숫자 작업을 많은 확장성 지원 합니다.

## <a name="billing-and-active-status"></a>청구 및 활성 상태
작업 컬렉션은 항상 활성화 되어 전체 구독 toobilling 문제 인해 일부 임시 사용할 수 없는 상태 제거 하지 않는 한 합니다. hello 작업 컬렉션은 비용이 청구 방식으로 tooensure만은 tooeither 설정 toohello *무료* 계획 또는 toodelete hello 작업 컬렉션입니다.

Hello 작업 컬렉션의 hello 청구 상태를 변경 하지는 않습니다 – hello 작업 컬렉션은 한 번의 작업은 작업 컬렉션 내 모든 작업을 비활성화할 수 있습니다, 있지만 *여전히* 청구 됩니다. 마찬가지로 빈 작업 컬렉션도 활성 상태로 간주되어 청구됩니다.

## <a name="pricing"></a>가격
가격 세부 정보는 [스케줄러 가격 책정](https://azure.microsoft.com/pricing/details/scheduler/)을 참조하세요.

## <a name="see-also"></a>참고 항목
 [스케줄러란?](scheduler-intro.md)

 [Azure 스케줄러 개념, 용어 및 엔터티 계층 구조](scheduler-concepts-terms.md)

 [Hello Azure 포털에서에서 스케줄러 사용 시작](scheduler-get-started-portal.md)

 [Azure 스케줄러 REST API 참조](https://msdn.microsoft.com/library/mt629143)

 [Azure 스케줄러 PowerShell cmdlet 참조](scheduler-powershell-reference.md)

 [Azure 스케줄러 고가용성 및 안정성](scheduler-high-availability-reliability.md)

 [Azure 스케줄러 제한, 기본값 및 오류 코드](scheduler-limits-defaults-errors.md)

 [Azure 스케줄러 아웃바운드 인증](scheduler-outbound-authentication.md)

