---
title: Azure Redis Cache aaaHow tooadminister | Microsoft Docs
description: "Tooperform 관리 작업 같은 재부팅 방법을 자세히 알아보고 Azure Redis Cache에 대 한 일정을 업데이트 합니다."
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Azure Redis 캐시 하는 tooadminister 방법
이 항목에서는 tooperform 관리와 같은 작업을 설명 [재부팅](#reboot) 및 [업데이트 예약](#schedule-updates) Azure Redis 캐시 인스턴스에 대 한 합니다.

## <a name="reboot"></a>Reboot
hello **재부팅** 블레이드 있습니다 tooreboot 캐시의 하나 이상의 노드. 이 다시 부팅 기능을 사용 하면 있습니다 tootest 복구를 위한 응용 프로그램 캐시 노드 오류가 없는 경우.

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

Hello 노드 tooreboot를 선택 하 고 클릭 **재부팅**합니다.

![Reboot](./media/cache-administration/redis-cache-reboot.png)

프리미엄 캐시 클러스터링을 사용 해야 하는 경우에 hello 캐시 tooreboot의 어떤 분할 영역을 선택할 수 있습니다.

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot 하나 이상의 노드 캐시의 hello 원하는 노드를 선택 하 고 클릭 **재부팅**합니다. 프리미엄 캐시 클러스터링을 사용 해야 하는 경우 필요한 hello 분할 영역 tooreboot 선택한 다음 클릭 **재부팅**합니다. 몇 분 후 hello 선택한 노드 다시 부팅 하 고 몇 분 후 다시 온라인 상태로 전환 됩니다.

클라이언트 응용 프로그램에 미치는 영향을 hello 다시 부팅 하는 노드를 따라 다릅니다.

* **마스터** -때 hello 마스터 노드는 다시 부팅 된, Azure Redis 캐시 실패 하 toohello 복제본 노드를 통해 및 toomaster 올립니다. 이 장애 조치 하는 동안 짧은 간격으로는 연결이 실패할 수 있다 toohello 캐시 있을 수 있습니다.
* **슬레이브** -hello 종속 노드를 다시 부팅 하는 경우는 일반적으로 영향 toocache 클라이언트가 없습니다.
* **마스터 및 슬레이브** -캐시 노드 모두 재부팅 될 때 hello 주 노드가 온라인 상태가 될 때까지 hello 캐시 및 연결 toohello 캐시 실패에서 모든 데이터가 손실 됩니다. 구성한 경우 [데이터 지 속성](cache-how-to-premium-persistence.md), hello 캐시를 다시 온라인 상태가 되 완전히 hello 가장 최근의 백업 이후에 발생 한 캐시 쓰기가 손실 hello 가장 최근 백업이 복원 됩니다.
* **premium의 노드를 클러스터링을 사용 캐시** -하나를 다시 부팅 하거나 클러스터링 하 여 프리미엄 캐시의 노드 선택 hello에 대 한 동작 hello를 사용 하는 경우 노드는 동일한 경우 다시 부팅 하면 hello 해당 노드 또는 클러스터 되지 않은의 노드에으로 hello 캐시 합니다.

> [!IMPORTANT]
> 이제 모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.
> 
> 

## <a name="reboot-faq"></a>다시 부팅 FAQ
* [노드 하려면 다시 부팅 해야 tootest 내 응용 프로그램과?](#which-node-should-i-reboot-to-test-my-application)
* [캐시 tooclear 클라이언트 연결의 hello를 다시 부팅할 수 있습니까?](#can-i-reboot-the-cache-to-clear-client-connections)
* [다시 부팅하는 경우 캐시의 데이터가 손실되나요?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [PowerShell, CLI 또는 기타 관리 도구를 사용하여 내 캐시를 다시 부팅할 수 있나요?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [어떤 가격 책정 계층 hello 다시 부팅 기능을 사용할 수 있습니까?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>노드 하려면 다시 부팅 해야 tootest 내 응용 프로그램과?
캐시를 다시 부팅 hello hello 주 노드의 오류 로부터 응용 프로그램의 tootest hello 복원 력을 **마스터** 노드. 다시 부팅 hello hello 보조 노드의 오류 로부터 응용 프로그램의 tootest hello 복원 력을 **슬레이브** 노드. tootest hello 복원 력 응용 프로그램의 총 오류 로부터 hello 캐시의 다시 부팅 **둘 다** 노드.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>캐시 tooclear 클라이언트 연결의 hello를 다시 부팅할 수 있습니까?
예, hello 캐시를 다시 부팅 하는 경우 모든 클라이언트 연결이 지워집니다. 다시 부팅 하는 hello 경우 기한 tooa 논리 오류 또는 hello 클라이언트 응용 프로그램의 버그 모든 클라이언트 연결이 사용 되는 위치에 유용할 수 있습니다. 각 가격 책정 계층에 다른 [클라이언트 연결 제한](cache-configure.md#default-redis-server-configuration) 에 대 한 다양 한 크기 hello 및 이러한 한도 도달한 후 클라이언트 연결이 더 이상 허용 됩니다. Hello 캐시를 다시 부팅 하면 모든 클라이언트 연결 방법을 tooclear 제공 합니다.

> [!IMPORTANT]
> 캐시 tooclear 클라이언트 연결을 다시 부팅 하면 StackExchange.Redis hello Redis 노드가 다시 온라인 상태가 되 면 자동으로 다시. Hello 기본 문제 해결 되지 않으면 hello 클라이언트 연결은 계속 toobe 모두 사용 합니다.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>다시 부팅하는 경우 캐시의 데이터가 손실되나요?
두 hello를 다시 부팅 하면 **마스터** 및 **슬레이브** 노드 hello 캐시에 (또는 프리미엄 캐시를 사용 하는 클러스터링을 사용 하는 경우 해당 분할)의 모든 데이터가 손실 됩니다. 구성한 경우 [데이터 지 속성](cache-how-to-premium-persistence.md), hello 가장 최근 백업이 복원 됩니다 hello 캐시 다시 온라인 상태가 되지만 hello 백업을 만든 후에 발생 한 모든 캐시 쓰기 손실 됩니다.

Hello 노드 중 하나를 다시 부팅 하는 경우 데이터가 일반적으로 손실 됩니다. 하지만 수 있습니다. 예를 들어 hello 마스터 노드 다시 부팅 되 고 캐시 쓰기 hello 데이터 hello 캐시 쓰기에서 진행 되는 경우 손실 되었습니다. 데이터 손실에 대 한 또 다른 시나리오는 한 노드를 다시 부팅 하 고 다른 hello 노드 발생 toogo 아래로 tooa 오류 hello에 인해 것 같은 시간입니다. 데이터 손실에 대 한 가능한 원인에 대 한 자세한 내용은 참조 [Redis에서 발생 했습니다 toomy 데이터?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>PowerShell, CLI 또는 기타 관리 도구를 사용하여 내 캐시를 다시 부팅할 수 있나요?
예, PowerShell 명령 참조 [tooreboot Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache)합니다.

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>어떤 가격 책정 계층 hello 다시 부팅 기능을 사용할 수 있습니까?
모든 가격 책정 계층에서 다시 부팅을 사용할 수 있습니다.

## <a name="schedule-updates"></a>업데이트를 예약
hello **업데이트를 예약할** 블레이드 toodesignate 프리미엄 계층 캐시에 대 한 유지 관리 기간을 수 있습니다. Hello 유지 관리 기간을 지정 하면이 기간 동안 모든 Redis 서버 업데이트 수 있습니다. 

> [!NOTE] 
> tooRedis 서버 업데이트 및 Azure 업데이트 또는 hello 캐시를 호스트 하는 hello Vm의 toohello 운영 체제를 업데이트 하지 tooany hello 유지 관리 기간에 적용 됩니다.
> 
> 

![업데이트를 예약](./media/cache-administration/redis-schedule-updates.png)

toospecify 유지 관리 기간 hello 원하는 일 수를 확인 합니다. 각 날에 대 한 hello 유지 관리 창 시작 시간을 지정 고를 클릭 **확인**합니다. Hello 유지 관리 기간에 UTC를 참고 합니다. 

> [!NOTE]
> 업데이트에 대 한 hello 기본 유지 관리 기간에는 5 개의 시간입니다. 이 값은 hello Azure 포털에서에서 구성할 수 있는 되지 않지만 hello를 사용 하 여 PowerShell에서 구성할 수 있습니다 `MaintenanceWindow` hello의 매개 변수 [새로 AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet. 자세한 내용은 [PowerShell, CLI 또는 기타 관리 도구를 사용하여 예약된 업데이트를 관리할 수 있나요?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)를 참조하세요.
> 
> 

## <a name="schedule-updates-faq"></a>업데이트 예약 FAQ
* [Hello 일정 업데이트 기능을 사용 하지 않아도 업데이트 발생 시기는 무엇입니까?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [유지 관리 기간을 예약할 hello 중에 어떤 유형의 업데이트가 수행 되 있습니까?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [PowerShell, CLI 또는 기타 관리 도구를 사용하여 예약된 업데이트를 관리할 수 있나요?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [어떤 가격 책정 계층 hello 일정 업데이트 기능을 사용할 수 있습니까?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Hello 일정 업데이트 기능을 사용 하지 않아도 업데이트 발생 시기는 무엇입니까?
유지 관리 기간을 지정하지 않으면, 언제든지 업데이트가 진행될 수 있습니다.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>유지 관리 기간을 예약할 hello 중에 어떤 유형의 업데이트가 수행 되 있습니까?
만 Redis 서버 hello 예약 된 유지 관리 기간 동안 업데이트 됩니다. hello 유지 관리 기간 tooAzure 업데이트는 적용 되지 않습니다 또는 toohello VM 운영 체제를 업데이트 합니다.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>PowerShell, CLI 또는 기타 관리 도구를 사용하여 관리되는 예약된 업데이트를 수행할 수 있나요?
예, PowerShell cmdlet을 다음 hello를 사용 하 여 예약 된 업데이트를 관리할 수 있습니다.

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>어떤 가격 책정 계층 hello 일정 업데이트 기능을 사용할 수 있습니까?
hello **업데이트를 예약할** 기능은 hello 프리미엄 가격 책정 계층에서에서 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Azure Redis Cache 프리미엄 계층](cache-premium-tier-intro.md) 기능에 대해 더 알아봅니다.

