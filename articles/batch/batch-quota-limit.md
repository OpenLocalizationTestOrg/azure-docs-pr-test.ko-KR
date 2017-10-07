---
title: "aaaService 할당량 및 Azure 일괄 처리에 대 한 제한을 | Microsoft Docs"
description: "기본 Azure 배치 할당량, 제한 및 제약 조건 및 toorequest 할당량 증가 하는 방법에 대해 알아보기"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>배치 서비스 할당량 및 제한

와 다른 Azure 서비스와 제한 되어 hello 일괄 처리 서비스와 관련 된 특정 리소스입니다. 이러한 제한 중 상당수는 hello 구독 또는 계정 수준에서 Azure에 의해 적용 된 기본 할당량입니다. 이 문서는 그러한 기본값을 설명하고 할당량 증가를 요청하는 방법을 설명합니다.

배치 워크로드를 디자인하고 강화할 때 이 할당량에 주의합니다. 예를 들어 사용자 풀 hello 대상 지정한 계산 노드 수에 도달 되지 않습니다 수에 도달 했 있습니다 hello 코어 할당량 한도 배치 계정 또는 지역 VM 코어 할당량에 대 한 구독에 대 한 합니다.

단일 일괄 처리 계정에 여러 개의 일괄 처리 작업을 실행 하거나 hello에 있는 일괄 처리 계정 간에 작업을 배포할 수 있습니다 동일한 구독 있지만 서로 다른 Azure 지역에 있습니다.

일괄 처리에서 toorun 프로덕션 작업을 하려는 경우에 하나 이상의 hello 기본 위에 hello 할당량 tooincrease를 할 수 있습니다. Tooraise 할당량을 하려는 경우 온라인 열 수 [고객 지원 요청](#increase-a-quota) 비용 없이 합니다.

> [!NOTE]
> 할당량은 신용 한도액일 뿐이며 용량을 보장하는 것은 아닙니다. 대규모 용량이 필요한 경우 Azure 지원에 문의하세요.
> 
> 

## <a name="resource-quotas"></a>리소스 할당량
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>사용자 구독 모드에서 할당량

도 풀 할당 모드를 사용 하 여 일괄 처리 계정을**사용자 구독**, Vm 및 저장소 계정 등의 다른 리소스를 일괄 처리, 풀을 만들 때 구독에 직접 생성 됩니다. hello Azure 배치 코어 할당량에는이 모드에서 만든 tooan 계정을 적용 되지 않습니다. 대신 지역 계산 코어 및 기타 리소스에 대 한 구독에서 hello 할당량 적용 됩니다. [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 이러한 할당량에 대해 자세히 알아보세요.

사용자 구독 모드에서 생성 된 계정에 대 한 리소스 사용량을 계획할 때 (더하기 toocompute 코어)의 일괄 처리 리소스를 다음 참고 hello를 사용 하는 요소가 모든 40 Linux Vm 또는 20 대의 Windows Vm에 대 한 필요 합니다.

| 리소스 | 할당량 | 공급자 |
| --- | ---| --- |
| 저장소 계정 1개 | 저장소 계정 | Microsoft.Storage |
| 공용 IP 주소 1개 | 공용 IP 주소 | Microsoft.Network | 
| 가상 네트워크 1개 | 가상 네트워크 | Microsoft.Network | 
| 네트워크 보안 그룹 1개 | 네트워크 보안 그룹 | Microsoft.Network | 
| 가상 컴퓨터 확장 집합 1개 | 가상 컴퓨터 확장 집합 | Microsoft.Compute | 
| 부하 분산 장치 1개 | 부하 분산 장치 | Microsoft.Network | 

국가별 수준이 나 VM 패밀리당 hello 코어 할당량에 따라 toohello VM 크기 설정 배치 풀 또는 풀에 필요한 같아야 합니다.

| 할당량 | 공급자 |
| --- | ---- |
| 총 지역별 코어 수 | Microsoft.Compute |
| … 제품군 코어 수 | Microsoft.Compute |



## <a name="other-limits"></a>기타 제한
| **리소스** | **최대 제한** |
| --- | --- |
| [동시 작업](batch-parallel-node-tasks.md)  |4 x 노드 코어 수 |
| [응용 프로그램](batch-application-packages.md)  |20 |
| 응용 프로그램당 응용 프로그램 패키지 |40 |
| 각 응용 프로그램 패키지 크기 |약 195GB<sup>1</sup> |
| 최대 시작 태스크 크기 | 32768자<sup>2</sup> |

<sup>1</sup> 최대 블록 Blob 크기에 대한 Azure 저장소 용량 한도<br />
<sup>2</sup> 리소스 파일 및 환경 변수를 포함합니다.

## <a name="view-batch-quotas"></a>배치 할당량 보기
배치 계정 할당량 hello 뷰에서 [Azure 포털][portal]합니다.

1. 선택 **계정 일괄 처리** hello 포털에서 다음에 관심이 hello 일괄 처리 계정을 선택 합니다.
2. 선택 **속성** hello 일괄 처리 계정 메뉴 블레이드에서 합니다.
3. hello를 표시 하는 hello 속성 블레이드 **할당량** toohello 일괄 처리 계정에 현재 적용
   
    ![배치 계정 할당량][account_quotas]

사용자 구독 모드에서 만든 일괄 처리 계정에 대 한 보기 hello 관련 hello Azure 포털의에서 구독 할당량입니다.

1. 선택 **구독**, hello 일괄 처리 계정에는 사용 하는 hello 구독을 선택 합니다.

2. Hello에 **구독** 블레이드를 **사용 + 할당량**합니다.



## <a name="increase-a-quota"></a>할당량 증가
이러한 단계 toorequest 일괄 처리 계정이 나 hello를 사용 하 여 구독에 대 한 할당량 증가 따라 [Azure 포털][portal]합니다. hello 유형의 할당량 증가 배치 계정 hello 풀 할당 모드에 따라 달라 집니다.

### <a name="increase-a-batch-cores-quota"></a>배치 코어 할당량 증가 

배치 계정에서 만들어진 경우 **서비스 일괄 처리** 모드에서는 이러한 단계 toorequest 일괄 처리 코어 할당량 증가 수행:

1. 선택 hello **도움말 + 지원** 포털 대시보드에서 타일 또는 물음표 hello (**?**) hello 포털의 hello 오른쪽 위 모퉁이에 있습니다.
2. **새 기본 지원 요청** > **기본**을 클릭합니다.
3. Hello에 **기본 사항** 블레이드:
   
    a. **문제 형식** > **할당량**
   
    b. 사용 중인 구독을 선택합니다.
   
    c. **할당량 유형** > **배치**
   
    d. **지원 계획** > **할당량 지원 - 포함됨**
   
    **다음**을 누릅니다.
4. Hello에 **문제** 블레이드:
   
    a. 선택 된 **심각도** tooyour에 따라 [비즈니스 영향][support_sev]합니다.
   
    b. **세부 정보**, toochange, hello 일괄 처리 계정 이름 및 hello 새 제한 하려는 각 할당량을 지정 합니다.
   
    **다음**을 누릅니다.
5. Hello에 **연락처 정보** 블레이드:
   
    a. **기본 연락 방법**을 선택합니다.
   
    b. 확인 하 고 필요한 hello 연락처 세부 정보를 입력 합니다.
   
    클릭 **만들기** toosubmit hello 지원 요청.

지원 요청을 제출하면 Azure 지원 팀에서 연락을 드릴 것입니다. Note는 근무일 기준 too2 정도 걸릴 수 있습니다 hello 요청을 완료 합니다.

### <a name="increase-a-subscription-cores-quota"></a>구독 코어 할당량 증가

배치 계정이 **사용자 구독** 모드에서 생성되었으며 추가 지역 또는 VM 제품군 코어가 필요한 경우 구독에서 할당량 증가를 요청합니다. 해당 단계는 [Resource Manager 코어 할당량 증가 요청](../azure-supportability/resource-manager-core-quotas-request.md)을 참조하세요.



## <a name="related-topics"></a>관련된 항목
* [Hello Azure 포털을 사용 하 여 Azure 배치 계정 만들기](batch-account-create-portal.md)
* [Azure 배치 기능 개요](batch-api-basics.md)
* [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
