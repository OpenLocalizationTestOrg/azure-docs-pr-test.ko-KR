---
title: "Azure Redis Cache에 대 한 지리적 복제 aaaHow tooconfigure | Microsoft Docs"
description: "어떻게 tooreplicate Azure Redis 캐시 인스턴스를 여러 지리적 지역에 알아봅니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>어떻게 Azure Redis Cache에 대 한 지리적 복제 tooconfigure

지역에서 복제는 두 개의 프리미엄 계층 Azure Redis Cache 인스턴스를 연결하는 메커니즘을 제공합니다. 캐시가 하나는 기본 연결 된 캐시 hello 및 hello hello 보조 연결 캐시로 다른으로 지정 됩니다. hello 보조 연결 된 캐시는 읽기 전용 및 서 면된 toohello 기본 캐시는 데이터 toohello 보조 연결 된 캐시를 복제 합니다. 이 기능은 Azure 지역에서 사용 되는 tooreplicate 캐시 수 있습니다. 이 문서에서는 프리미엄 계층 Azure Redis 캐시 인스턴스에 대 한 가이드 tooconfiguring 지리적 복제를 제공 합니다.

## <a name="geo-replication-prerequisites"></a>지역에서 복제 필수 조건

두 개의 캐시 hello 다음 필수 구성 요소 간의 tooconfigure 지리적 복제를 충족 되어야 합니다.

- 두 캐시 모두 [프리미엄 계층](cache-premium-tier-intro.md) 캐시여야 합니다.
- 두 캐시는 hello에 있어야 합니다. 동일한 Azure 구독.
- hello 보조 연결 된 캐시 해야 수 있거나 hello 가격 계층 또는 기본 연결 된 캐시 hello 보다 더 큰 가격 책정 계층을 동일한 합니다.
- Hello 기본 연결 된 캐시의 클러스터링을 사용, 연결 된 캐시를 보조 hello 가져야 클러스터링을 hello로 사용 hello 기본 연결 된 캐시와 같은 수의 분할 된 데이터베이스입니다.
- 두 캐시 모두 만들어야 하며 실행 중 상태여야 합니다.
- 어느 캐시에서도 지속성을 사용하도록 설정하면 안 됩니다.
- 동일한 VNET은 지원 되는 hello에 대 한 캐시 간의 지리적 복제 합니다. 다른 Vnet에 캐시 간의 지리적 복제도 지원 됩니다 hello Vnet의 리소스 수 tooreach 있는 방식으로 구성 된 두 hello Vnet으로 TCP 연결을 통해 서로 합니다.

지리적 복제를 구성한 후 hello 다음과 같은 제한 사항이 적용 tooyour 연결 된 캐시 쌍:

- hello 보조 연결 된 캐시는 읽기 전용입니다. 여기에서 읽을 수 있지만 모든 데이터 tooit를 쓸 수 없습니다. 
- Hello 링크를 추가 하기 전에 hello 보조 연결 된 캐시에 있는 모든 데이터가 제거 됩니다. 하지만 Hello 지리적 복제는 이후에 제거, hello hello 보조 연결 된 캐시에 남아 있는 데이터를 복제 합니다.
- 시작할 수 없습니다는 [크기 조정 작업이](cache-how-to-scale.md) 어느 캐시 또는 [hello 분할 영역 수를 변경](cache-how-to-premium-clustering.md) hello 캐시에는 클러스터링을 사용 하는 경우.
- 어느 캐시에서도 지속성을 사용하도록 설정할 수 없습니다.
- 사용할 수 있습니다 [내보내기](cache-how-to-import-export-data.md#export) 어느 캐시와만 할 수 있습니다 하지만 [가져오기](cache-how-to-import-export-data.md#import) 기본 hello에 캐시를 연결 합니다.
- 연결 된 캐시 또는 hello 지역 간 복제 링크를 제거할 때까지, 포함 된 hello 리소스 그룹을 삭제할 수 없습니다. 자세한 내용은 참조 [이유 hello 작업 실패 않았지만 toodelete 내 연결 된 캐시를 려 하면?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- 두 개의 캐시 hello 서로 다른 지역에 있는 경우 네트워크 송신 비용 toohello 데이터 영역 toohello 보조 연결 된 캐시에 걸쳐 복제 적용 됩니다. 자세한 내용은 참조 [않는 손실이 tooreplicate 내 데이터 Azure 지역에 걸쳐?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- 기본 캐시 hello (및 해당 복제본) 다운 된 경우에 없는 자동 장애 조치 toohello 보조 연결 된 캐시입니다. 순서 toofailover 클라이언트 응용 프로그램에서 toomanually hello 지리적 복제 연결 제거 해야 하 고 hello 클라이언트 응용 프로그램 toohello 캐시 하는 지점 였던 hello 보조 연결 된 캐시 합니다. 자세한 내용은 참조 [어떻게 toohello 보조 연결 된 캐시 장애 조치할 작동 합니까?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>지역에서 복제 링크 추가

1. 두 개의 프리미엄 캐시 지리적 복제를 함께 toolink 클릭 **지리적 복제** hello 캐시 하기 위한 기본 연결 hello로의 hello 리소스 메뉴에서를 캐시 한 다음 클릭 **추가 캐시 복제 링크**hello에서 **지리적 복제** 블레이드입니다.

    ![링크 추가](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Hello에서 원하는 hello 보조 캐시의 hello 이름을 클릭 **호환 캐시** 목록입니다. 원하는 캐시 hello 목록에 표시 되지 않으면 해당 hello 확인 [지리적 복제 필수 구성 요소](#geo-replication-prerequisites) hello 원하는 보조 캐시 충족에 대 한 합니다. 지역에 따라 toofilter hello 캐시 hello hello에 캐시 된 hello 맵 toodisplay에서 원하는 지역을 클릭 **호환 캐시** 목록입니다.

    ![지역에서 복제 호환되는 캐시](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    Hello 상황에 맞는 메뉴를 사용 하 여 hello 보조 캐시에 대 한 프로세스 또는 뷰 세부 정보를 연결 하는 hello를 시작할 수 있습니다.

    ![지역에서 복제 상황에 맞는 메뉴](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. 클릭 **링크** toolink 함께 두 개의 캐시 hello 및 hello 복제 프로세스를 시작 합니다.

    ![캐시 연결](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. Hello에 hello 복제 프로세스의 hello 진행률을 볼 수 있습니다 **지리적 복제** 블레이드입니다.

    ![연결 상태](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    Hello hello에 상태 연결을 볼 수 있습니다 **개요** 블레이드 두 hello 기본 및 보조 캐시에 대 한 합니다.

    ![캐시 상태](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Hello 복제 프로세스가 완료 되 면 hello **상태 연결** 쪽 변경**Succeeded**합니다.

    ![캐시 상태](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Hello 링크 프로세스, 하는 동안 hello 기본 연결 된 캐시를 계속 사용 하기 위해 사용할 수 있지만 hello 링크 프로세스 완료 될 때까지 hello 보조 연결 된 캐시를 사용할 수 없습니다.

## <a name="remove-a-geo-replication-link"></a>지역에서 복제 링크 제거

1. 지리적 복제를 중지 하 고 두 개의 캐시 간의 tooremove hello 링크 클릭 **캐시의 연결을 해제** hello에서 **지리적 복제** 블레이드입니다.
    
    ![캐시 연결 해제](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Hello 연결 해제 프로세스가 완료 되 면 hello 보조 캐시를 사용할 수 모두 읽기에 씁니다.

>[!NOTE]
>Hello 지리적 복제 링크가 제거 됩니다 hello hello 보조 캐시에 남아 있는 hello 기본 연결 된 캐시에서에서 데이터를 복제 합니다.
>
>

## <a name="geo-replication-faq"></a>지역에서 복제 FAQ

- [표준 또는 기본 계층 캐시에서 지역에서 복제를 사용할 수 있나요?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [내 캐시는 hello 연결 또는 연결 해제 프로세스 중에 사용할 수 있습니까?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [둘 이상의 캐시를 함께 연결할 수 있나요?](#can-i-link-more-than-two-caches-together)
- [서로 다른 Azure 구독의 두 캐시를 연결할 수 있나요?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [크기가 다른 두 캐시를 연결할 수 있나요?](#can-i-link-two-caches-with-different-sizes)
- [클러스터링이 설정된 지역에서 복제를 사용할 수 있나요?](#can-i-use-geo-replication-with-clustering-enabled)
- [VNET의 캐시에 지역에서 복제를 사용할 수 있나요?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [PowerShell 또는 Azure CLI toomanage 지리적 복제를 사용할 수 있습니까?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [비용은 얼마 입니까 것 tooreplicate 내 데이터 Azure 지역에 걸쳐?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [연결 된 캐시 내 toodelete 시도 hello 작업 실패 이유는?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [보조 연결된 캐시에는 어떤 지역을 사용해야 하나요?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [장애 조치 toohello 보조 연결 된 캐시는 어떻게 작동 합니까?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>표준 또는 기본 계층 캐시에서 지역에서 복제를 사용할 수 있나요?

아니요, 지역에서 복제는 프리미엄 계층 캐시에만 사용할 수 있습니다.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>내 캐시는 hello 연결 또는 연결 해제 프로세스 중에 사용할 수 있습니까?

- 지리적 복제를 위한 두 개의 캐시를 함께 연결을 하는 경우 hello 기본 연결 된 캐시를 계속 사용 하기 위해 사용할 수 있지만 hello 링크 프로세스 완료 될 때까지 hello 보조 연결 된 캐시를 사용할 수 없습니다.
- 두 개의 캐시 간의 hello 지역 간 복제 링크를 제거할 때 두 캐시에 계속 사용할 수 있습니다.

### <a name="can-i-link-more-than-two-caches-together"></a>둘 이상의 캐시를 함께 연결할 수 있나요?

아니요, 지역에서 복제를 사용하는 경우 두 개의 캐시만 함께 연결할 수 있습니다.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>서로 다른 Azure 구독의 두 캐시를 연결할 수 있나요?

없음, 모두 캐시는 hello에 있어야 합니다. 동일한 Azure 구독.

### <a name="can-i-link-two-caches-with-different-sizes"></a>크기가 다른 두 캐시를 연결할 수 있나요?

예, 연결 된 보조 hello로 캐시는 hello 기본 연결 된 캐시 보다 큽니다.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>클러스터링이 설정된 지역에서 복제를 사용할 수 있나요?

예, hello를 보유 하는 두 캐시 같은 수의 분할 된 데이터베이스입니다.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>VNET의 캐시에 지역에서 복제를 사용할 수 있나요?

예, VNET의 캐시에 대한 지역에서 복제가 지원됩니다. 

- 동일한 VNET은 지원 되는 hello에 대 한 캐시 간의 지리적 복제 합니다.
- 다른 Vnet에 캐시 간의 지리적 복제도 지원 됩니다 hello Vnet의 리소스 수 tooreach 있는 방식으로 구성 된 두 hello Vnet으로 TCP 연결을 통해 서로 합니다.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>PowerShell 또는 Azure CLI toomanage 지리적 복제를 사용할 수 있습니까?

관리할 수 있습니다이 이번에 지리적 복제를 사용 하 여 hello Azure 포털입니다.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>비용은 얼마 입니까 것 tooreplicate 내 데이터 Azure 지역에 걸쳐?

지리적 복제를 사용할 때는 hello 기본 연결 된 캐시에서 데이터는 복제 된 toohello 보조 연결 캐시입니다. Hello에 캐시는 hello 두 연결 되어 있는 경우 동일한 Azure 지역 hello 데이터 전송에 대 한 요금은 없습니다. Hello 두 연결 되어 있는 경우 다양 한 Azure 지역에 있는 캐시를 hello 지리적 복제 데이터 전송 요금과 해당 데이터 toohello 다른 Azure 지역 복제의 hello 대역폭 비용. 자세한 내용은 [대역폭 가격 정보](https://azure.microsoft.com/pricing/details/bandwidth/)를 참조하세요.

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>연결 된 캐시 내 toodelete 시도 hello 작업 실패 이유는?

두 개의 캐시를 함께 연결를 hello 지역 간 복제 링크를 제거할 때까지 포함 하는 캐시 또는 hello 리소스 그룹을 삭제할 수 없습니다. 사용 하려는 경우 toodelete hello 리소스 그룹에 하나 또는 둘 다의 hello 연결 캐시, hello hello 리소스 그룹의에서 다른 리소스는 삭제 되지만 hello에 유지 되는 hello 리소스 그룹 `deleting` 상태 및 모든 캐시 hello 리소스 그룹에 연결 hello에 남아 `running` 상태입니다. 에 설명 된 대로 hello 리소스 그룹 및 hello toocomplete hello 삭제 연결 hello 지리적 복제 연결 끊기 그 안에 캐시 [지리적 복제 링크가 제거](#remove-a-geo-replication-link)합니다.

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>보조 연결된 캐시에는 어떤 지역을 사용해야 하나요?

일반적으로 것이 좋습니다 프로그램 캐시 tooexist hello에 대 한 동일한 멤버에 액세스 하는 hello 응용 프로그램과 같은 Azure 지역입니다. 응용 프로그램에 주 지역과 대체 지역이 있는 경우 주 캐시와 보조 캐시가 동일한 지역에 있어야 합니다. 쌍을 이루는 지역에 대한 자세한 내용은 [모범 사례 - Azure 쌍을 이루는 지역](../best-practices-availability-paired-regions.md)을 참조하세요.

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>장애 조치 toohello 보조 연결 된 캐시는 어떻게 작동 합니까?

지역에서 복제의 초기 릴리스에서 hello Azure Redis Cache Azure 지역에서 자동 장애 조치를 지원 하지 않습니다. 지역에서 복제는 주로 재해 복구 시나리오에서 사용됩니다. Distater 복구 시나리오에서 고객 상태가 됩니다 hello 전체 응용 프로그램 스택의 백업 지역에 있으므로 시기를 결정 하는 개별 응용 프로그램 구성 요소는 것이 아니라 조정 된 방식으로 자체적으로 tooswitch tootheir 백업. 이 특히 관련 된 tooRedis입니다. Redis의 hello 주요 이점 중 하나는 매우 짧은 대기 시간의 저장소 된다는 점입니다. Redis에서 사용 하는 응용 프로그램 장애 tooa 다른 Azure 지역의 조치 하지만 hello 계산 계층도 하지 않습니다, 그리고 이동 시간 라운드 추가 hello 성능에 거의 영향을 갖기 합니다. 이러한 이유로 같은 tooavoid Redis 장애 조치 자동으로 tootransient 가용성 문제 때문입니다.

현재 tooinitiate hello 장애 조치 해야 tooremove hello 지리적 복제 hello Azure 포털에에서 연결 하 고 다음 hello Redis 클라이언트에서 연결 끝점 hello hello 기본 연결 된 캐시 (이전 링크) toohello 보조 데이터베이스에서 변경 캐시 합니다. 두 개의 캐시 된 연결을 끊을 hello hello 복제본 일반 상태일 때는 읽기 / 쓰기 캐시 다시 및 Redis 클라이언트에서 직접 요청을 수락 합니다.


## <a name="next-steps"></a>다음 단계

Hello에 대 한 자세한 [Azure Redis Cache 프리미엄 계층](cache-premium-tier-intro.md)합니다.

