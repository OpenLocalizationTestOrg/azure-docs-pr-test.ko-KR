---
title: "aaaAzure 고가용성 Advisor 권장 사항을 | Microsoft Docs"
description: "Azure 배포의 Azure 관리자 tooimprove 높은 가용성을 사용 합니다."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Advisor 고가용성 권장 사항

Azure 관리자를 사용 하면 확인 하 고 비즈니스에 중요 한 응용 프로그램의 hello 연속성 개선. Hello에서 관리자가 권장 사항을 고가용성을 얻을 수 있습니다 **고가용성** hello 관리자 대시보드 탭 합니다.

![Hello 관리자 대시보드에서 높은 가용성 단추](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>가상 컴퓨터 내결함성 보장

Advisor는 가용성 집합에 속하지 않는 가상 컴퓨터를 식별하고 이러한 가상 컴퓨터를 가용성 집합으로 이동할 것을 권장합니다. 중복 tooyour 응용 프로그램을 제공 하려면 가용성 집합에 두 개 이상의 가상 컴퓨터를 그룹화 하는 것이 좋습니다. 이 구성을 사용 하면 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 하나 이상의 가상 컴퓨터를 사용할 수 충족 hello Azure 가상 컴퓨터 SLA 합니다. 가용성 집합에 대 한 hello 가상 컴퓨터 또는 tooadd hello 가상 컴퓨터 tooan 기존 가용성 집합 toocreate 중 하나를 선택할 수 있습니다.

> [!NOTE]
> Toocreate를 선택 하면 가용성 집합을 추가 해야 적어도 하나 이상의 가상 컴퓨터에 있습니다. 두 그룹 또는 가용성에서 더 많은 가상 컴퓨터 설정 tooensure 하는 것이 좋습니다 중단이 발생 하는 동안 하나 이상의 컴퓨터를 사용할 수 있습니다.

![Advisor 권장 사항: 가상 컴퓨터 중복성을 위해 가용성 집합 사용](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>가용성 집합 내결함성 보장 

관리자는 단일 가상 컴퓨터를 포함 하는 가용성 집합을 식별 하 고 하나 이상의 가상 컴퓨터 tooit를 추가 하는 것이 좋습니다. 중복 tooyour 응용 프로그램을 제공 하려면 가용성 집합에 두 개 이상의 가상 컴퓨터를 그룹화 하는 것이 좋습니다. 이 구성을 사용 하면 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 하나 이상의 가상 컴퓨터를 사용할 수 충족 hello Azure 가상 컴퓨터 SLA 합니다. 가상 컴퓨터 또는 기존 가상 컴퓨터를 toouse 및 tooadd toocreate 중 하나를 선택할 수 있습니다이 toohello 가용성 집합입니다.  

![관리자의 권장 구성: 하나 이상의 Vm toothis 가용성 집합 추가](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>응용 프로그램 게이트웨이 내결함성 보장
응용 프로그램 게이트웨이에서 구동 되는 중요 한 응용 프로그램의 tooensure hello 비즈니스 연속성, Advisor 결함 허용을 위해 구성 되지 않은 응용 프로그램 게이트웨이 인스턴스를 식별 하 고 사용할 수 있는 수정 작업과 하도록 제안 . Advisor는 중간 규모 또는 대규모 단일 인스턴스 응용 프로그램 게이트웨이를 식별하고 하나 이상의 인스턴스 추가를 권장합니다. 또한 단일 또는 다중 instance 작은 응용 프로그램 게이트웨이 식별 하 고 마이그레이션 toomedium 또는 큰 Sku 것을 권장 합니다. 관리자가 응용 프로그램 게이트웨이 인스턴스는 구성 된 toosatisfy hello 현재 SLA 요구 사항입니다 이러한 리소스에 대 한 이러한 작업 tooensure 권장 합니다.

![Advisor 권장 사항: 두 개 이상의 중간 규모 또는 대규모 응용 프로그램 게이트웨이 인스턴스 배포](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>가상 컴퓨터 디스크의 hello 성능 및 안정성 개선

관리자는 표준 디스크를 사용 하 여 가상 컴퓨터를 식별 하 고 toopremium 디스크 업그레이드할 것을 권장 합니다.
 
Azure Premium Storage는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다. 프리미엄 저장소 계정을 사용하는 가상 컴퓨터 디스크는 SSD(솔리드 스테이트 드라이브)에 데이터를 저장합니다. 응용 프로그램에 대 한 최상의 성능을 위해서는 hello 높은 IOPS toopremium 저장소를 필요로 하는 모든 가상 컴퓨터 디스크를 마이그레이션하는 것이 좋습니다. 

디스크에 높은 IOPS가 필요하지 않으면 표준 저장소에 유지 관리하여 비용을 제한할 수 있습니다. 표준 저장소는 SSD 대신 HDD(하드 디스크 드라이브)에 가상 컴퓨터 디스크 데이터를 저장합니다. 가상 컴퓨터 디스크 toopremium 디스크 toomigrate를 선택할 수 있습니다. 프리미엄 디스크는 대부분의 가상 컴퓨터 SKU에서 지원됩니다. 그러나 경우에 따라 toouse 프리미엄 디스크를 원하는 경우 할 수 있습니다 tooupgrade 가상 컴퓨터가 Sku도.

![관리자의 권장 구성: toopremium 디스크를 업그레이드 하 여 가상 컴퓨터 디스크의 hello 안정성이 개선](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>가상 컴퓨터 데이터를 실수로 삭제되지 않도록 보호
Advisor는 백업이 활성화되지 않은 가상 컴퓨터를 식별하고 백업을 활성화할 것을 권장합니다. 가상 컴퓨터 백업 설정 업무에 중요 한 데이터의 hello 가용성을 보장 하 고 실수로 인 한 삭제 또는 손상에 대 한 보호를 제공 합니다.

![관리자의 권장 구성: 가상 컴퓨터 백업 tooprotect 업무상 중요 한 데이터 구성](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Advisor의 고가용성 권장 사항에 액세스

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 왼쪽된 창에서 클릭 **더 많은 서비스**합니다.

3. Hello 메뉴 창을 아래에서 서비스 **모니터링 및 관리**, 클릭 **Azure 관리자**합니다.  
 hello 관리자 대시보드 표시 됩니다.

4. Hello 관리자 대시보드에서 hello 클릭 **고가용성** 탭을 선택한 다음 tooreceive 권장 사항을 보려는 hello 구독을 선택 합니다.

> [!NOTE]
> 관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다. 구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다. 이 작업은 *한 번만* 수행하면 됩니다. Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.

## <a name="next-steps"></a>다음 단계

Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.
* [소개 tooAzure 관리자](advisor-overview.md)
* [Advisor 시작](advisor-get-started.md)
* [Advisor 비용 권장 사항](advisor-performance-recommendations.md)
* [Advisor 성능 권장 사항](advisor-performance-recommendations.md)
* [Advisor 보안 권장 사항](advisor-security-recommendations.md)

