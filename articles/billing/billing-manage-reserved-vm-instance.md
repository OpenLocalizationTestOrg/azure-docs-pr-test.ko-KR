---
title: "Azure Reserved Virtual Machine Instances 관리 | Microsoft Docs"
description: "구독 범위를 변경하고 Azure Reserved VM Instances에 대한 액세스 권한을 관리하는 방법에 대해 알아봅니다."
services: billing
documentationcenter: 
author: vikramdesai01
manager: vikramdesai01
editor: 
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/06/2017
ms.author: vikdesai
ms.openlocfilehash: e23eea52ff5d27beacf938a1ef153172e24f1aee
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/16/2017
---
# <a name="manage-reserved-virtual-machine-instances"></a>Reserved Virtual Machine Instances 관리

Azure Reserved VM Instance를 구입한 다음 구매 중에 지정된 구독이 아닌 다른 구독에 예약을 적용하는 것이 좋습니다. 또한 동일한 가상 머신이 여러 구독에서 실행 중인 경우 공유할 예약 범위를 변경하는 것이 좋습니다. 예약 할인을 최대화하려면 구입한 인스턴스 수가 특성 및 실행 중인 가상 머신 수와 일치하는지 확인합니다. Reserved Virtual Machine Instance에 대해 자세히 알아보려면 [Azure 가상 머신을 사전 지불하여 비용 절감](https://go.microsoft.com/fwlink/?linkid=862121)을 참조하세요.

## <a name="change-the-scope-for-a-reservation"></a>예약할 범위 변경
 예약 할인은 예약과 일치하고 예약 범위 내에서 실행되는 가상 머신에 적용됩니다. 예약 범위는 청구 컨텍스트에서 단일 구독이나 모든 구독일 수 있습니다. 단일 구독으로 범위를 설정하는 경우 예약은 선택한 구독에서 실행 중인 가상 머신과 일치됩니다. 범위를 공유로 설정하는 경우 Azure에서 예약은 청구 컨텍스트 내에서 모든 구독에서 실행되는 가상 머신과 일치합니다. 청구 컨텍스트는 예약을 구입하는 데 사용되는 구독에 따라 달라집니다. 자세한 내용은 [Reserved VM Instances를 사용하여 VM 사전 지불](https://go.microsoft.com/fwlink/?linkid=861721)을 참조하세요.

예약의 범위를 업데이트하려면: 
1. [Azure 포털](https://portal.azure.com) 에 로그인합니다.
2. **추가 서비스** > **예약**을 선택합니다.
3. 예약을 선택합니다.
4. **설정** > **구성**을 선택합니다.
5. 범위를 변경합니다. 범위를 공유에서 단일 범위로 변경하는 경우 소유자인 구독만을 선택할 수 있습니다. 동일한 청구 컨텍스트 내에서 예약된 구독만을 선택할 수 있습니다. 청구 컨텍스트는 예약 구입했을 때 선택한 구독에 의해 결정됩니다. 범위는 종량제 제품 MS-AZR-0003P 구독 및 엔터프라이즈 제품 MS-AZR-0017P 구독에만 적용됩니다. 기업 계약의 경우 개발/테스트 구독은 예약 할인에 해당하지 않습니다.

## <a name="split-a-single-reservation-into-two-reservations"></a>단일 예약을 두 개의 예약으로 분할
 둘 이상의 인스턴스를 구입한 다음 예약 내의 인스턴스를 다른 구독에 할당하는 것이 좋습니다. 기본적으로 모든 인스턴스(구매 중에 지정된 수량)에는 단일 구독 또는 공유 중 하나의 범위가 지정됩니다. 예를 들어 10개의 표준 D2 VM을 구입하고, 범위를 구독 A로 지정했습니다. 이제 7개의 예약 VM 인스턴스의 범위를 구독 A로 변경하고 남은 3개의 예약 VM 인스턴스를 구독 B로 변경하려고 합니다. 예약을 분할하면 세분화된 범위 관리에 대한 인스턴스를 배포할 수 있습니다. 공유 범위를 선택하여 구독에 대한 할당을 간소화할 수 있습니다. 하지만 비용 관리 또는 예산 목적으로 인해 특정 구독에 수량을 할당할 수 있습니다.

 PowerShell, CLI 또는 API를 통해 예약을 두 개로 분할할 수 있습니다.

### <a name="split-a-reservation-by-using-powershell"></a>PowerShell을 사용하여 예약 분할
1. 다음 명령을 실행하여 예약 주문 ID를 가져옵니다.

    ```powershell
    # Get the reservation orders you have access to
    Get-AzureRmReservationOrder
    ```
2. 예약의 세부 정보를 가져옵니다.

    ```powershell
    Get-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a
    ```
3. 예약을 두 개로 분할하고 인스턴스를 배포합니다.

    ```powershell
    # Split the reservation. The sum of the Reserved VM instances, the quantity, must equal the total number of instances in the reservation that you're splitting.
    Split-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a -Quantity 3,2
    ```
1. 다음 명령을 실행하여 범위를 업데이트할 수 있습니다.

    ```powershell
    Update-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId 5257501b-d3e8-449d-a1ab-4879b1863aca -AppliedScopeType Single -AppliedScope /subscriptions/15bb3be0-76d5-491c-8078-61fe3468d414
    ```

## <a name="add-or-change-users-who-can-manage-a-reservation"></a>예약을 관리할 수 있는 사용자 추가 또는 변경
예약에 대한 역할에 사용자를 추가하여 예약의 관리를 위임할 수 있습니다. 기본적으로 예약을 구입한 사용자 및 계정 관리자는 예약에 대한 소유자 역할입니다. 

예약 할인을 받은 구독에서 독립적으로 예약에 대한 액세스 권한을 관리할 수 있습니다. 예약을 관리하는 사용 권한을 부여할 때 구독을 관리하는 권한을 제공하는 것은 아닙니다. 또한 누군가에게 예약의 범위 내에서 구독을 관리하는 사용 권한을 부여할 때 예약을 관리하는 권한을 제공하는 것은 아닙니다.
 
예약에 대한 액세스 관리를 위임하려면: 
1.  [Azure 포털](https://portal.azure.com) 에 로그인합니다.
2.  **추가 서비스** > **예약**을 선택하여 액세스할 수 있는 예약을 나열합니다.
3.  다른 사용자에게 액세스 권한을 위임하려는 예약을 선택합니다.
4.  메뉴에서 **액세스 제어(IAM)**를 선택합니다.
5.  **추가** > **역할** > **소유자**(또는 제한된 액세스 권한을 부여하려는 경우 다른 역할)를 선택합니다. 
6. 소유자로 추가할 사용자의 이메일 주소를 입력하세요. 
7. 사용자를 선택한 다음 **저장**을 선택합니다.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의

계속해서 다른 질문이 있는 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.
