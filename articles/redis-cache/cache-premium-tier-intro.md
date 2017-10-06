---
title: "aaaIntroduction toohello Azure Redis Cache 프리미엄 계층 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Redis 지 속성, Redis 클러스터링 및 프리미엄 계층 Azure Redis 캐시 인스턴스에 대 한 VNET 지원 및 관리"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Toohello Azure Redis Cache 프리미엄 계층 소개
Azure Redis 캐시는 tooyour 데이터 매우 빠른 액세스를 제공 하 여 뛰어나고 응답성이 뛰어난 응용 프로그램을 작성 하는 데 도움이 되는 관리 되는, 분산 캐시입니다. 

새로운 프리미엄 계층은 향상 된 보안와 모든 hello 표준 계층 기능 및 더 나은 성능을 더 큰 작업, 재해 복구, 가져오기/내보내기 등의 기타를 포함 하는 프로그램 Enterprise 준비 계층 번호입니다. 읽기 toolearn hello hello 프리미엄 캐시 계층의 추가 기능에 대 한 자세한를 계속 합니다.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>더 나은 성능을 비교 tooStandard 또는 기본 계층
**표준 또는 기본 계층에 대해 향상된 성능.** Hello 프리미엄 계층의 캐시는 빠른 프로세서를 포함 하 고 더 나은 성능 비교 toohello 기본 또는 표준 계층을 제공 합니다. 하드웨어에 배포 됩니다. 프리미엄 계층 캐시는 처리량은 더 높고 대기 시간은 더 짧습니다. 

**Hello에 대 한 처리량 동일한 크기의 캐시는 비교 tooStandard 계층으로 Premium에서 상위입니다.** 예를 들어 hello 처리량 53 GB P4 (Premium) 캐시는 c 6에 대 한 비교 too150K으로 초당 250 K 요청 (표준).

프리미엄 캐시에서의 크기, 처리량 및 대역폭에 대한 자세한 내용은 [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Redis 데이터 지속성
hello Premium 계층에서는 Azure 저장소 계정에 toopersist hello 캐시 데이터 있습니다. 기본/표준 캐시에서 모든 hello 데이터가 메모리에만 저장 됩니다. 기본 인프라의 경우 문제는 잠재적인 데이터 손실이 있을 수 있다는 점입니다. 데이터 손실 방지 hello 프리미엄 계층 tooincrease 탄력성에서 hello Redis 데이터 지 속성 기능을 사용 하는 것이 좋습니다. Azure Redis Cache는 [Redis 지속성](http://redis.io/topics/persistence)에서 RDB 및 AOF(출시 예정) 옵션을 제공합니다. 

에 대 한 지침은 지 속성을 구성을 참조 하세요. [어떻게 Premium Azure Redis Cache에 대 한 지 속성 tooconfigure](cache-how-to-premium-persistence.md)합니다.

## <a name="redis-cluster"></a>Redis 클러스터
Toocreate 캐시 53 GB 보다 큰 원하는 하거나 여러 Redis 노드에서 tooshard 데이터를 원하는 경우에 Redis hello 프리미엄 계층에서 사용 하지 않는 클러스터링을 사용할 수 있습니다. 각 노드는 고가용성을 위해 Azure에 의해 관리되는 주/복제본 캐시 쌍으로 구성됩니다. 

**Redis 클러스터링은 최대 배율 및 처리량을 제공합니다.** Hello 클러스터의 분할 영역 (노드) hello 수를 늘리면 처리량 선형으로 증가 합니다. 예: 10 분할 영역 P4 클러스터를 만들 경우 hello 사용할 수 있는 처리량은 250 K * 10 초당 요청 수 2.5 백만 = 합니다. Hello를 참조 하십시오 [Azure Redis 캐시 FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) 크기, 처리량 및 프리미엄 캐시와 대역폭에 대 한 자세한 내용은 합니다.

클러스터링을 시작 하는 tooget 참조 [어떻게 Premium Azure Redis Cache에 대 한 클러스터링 tooconfigure](cache-how-to-premium-clustering.md)합니다.

## <a name="enhanced-security-and-isolation"></a>강화된 보안 및 격리
Hello 기본 또는 표준 계층에서 만든 캐시에 액세스할 수 있는 공용 인터넷 hello 합니다. 액세스 toohello 캐시 hello 선택 키에 따라 제한 됩니다. Hello Premium 계층으로 지정된 된 네트워크 내에서 클라이언트에만 hello 캐시에 액세스할 수 있는지 확인할 수 있습니다. [Azure VNet(가상 네트워크)](https://azure.microsoft.com/services/virtual-network/)에서 Redis Cache를 배포할 수 있습니다. 서브넷, 액세스 제어 정책 및 기타 기능 toofurther 제한 액세스 tooRedis 같은 VNet의 모든 hello 기능을 사용할 수 있습니다.

자세한 내용은 참조 [Premium Azure Redis Cache에 대 한 tooconfigure 가상 네트워크를 지 원하는 방법](cache-how-to-premium-vnet.md)합니다.

## <a name="importexport"></a>가져오기/내보내기
가져오기/내보내기는 수 있는 tooimport 데이터를 Azure Redis Cache 또는 Azure Redis 캐시의 데이터를 내보내는에서 가져오기 및 내보내기 Redis 캐시 데이터베이스 (RDB) 스냅숏은 Azure의 프리미엄 캐시 tooa 페이지 blob으로 Azure Redis Cache 데이터 관리 작업 저장소 계정입니다. 이 서로 다른 Azure Redis Cache 인스턴스 간에 toomigrate를 사용 하면 또는 데이터로 사용 하기 전에 hello 캐시를 채우는 합니다.

가져오기에 사용 되는 toobring 클라우드 또는 Linux, Windows 또는 Amazon 웹 서비스 등과 같은 모든 클라우드 공급자에서 실행 되는 Redis를 포함 하 여 환경에서 실행 중인 모든 Redis 서버에서 Redis 호환 RDB 파일 일 수 있습니다. 데이터 가져오기는 쉽게 toocreate 미리 채워진된 데이터와 함께 캐시 됩니다. Hello 가져오기 프로세스 동안 Azure Redis Cache hello RDB 파일을 Azure 저장소에서 메모리에 로드 한 다음 hello 캐시로 hello 키를 삽입 합니다.

내보내기는 Azure Redis Cache tooRedis 호환 RDB 파일에 저장 된 tooexport hello 데이터 수 있습니다. Azure Redis Cache 인스턴스 tooanother 또는 tooanother Redis 서버 하나에서이 기능 toomove 데이터를 사용할 수 있습니다. Hello 내보내기 과정에서 임시 파일 VM 호스트 hello Azure Redis Cache 서버 인스턴스 및 hello 파일은 저장소 계정을 지정 하는 업로드 된 toohello hello에 만들어집니다. 실패 또는 성공 상태가 hello 내보내기 작업이 완료 되 면 hello 임시 파일이 삭제 됩니다.

자세한 내용은 참조 [어떻게 tooimport 데이터를 Azure Redis Cache에서 데이터를 내보내고](cache-how-to-import-export-data.md)합니다.

## <a name="reboot"></a>Reboot
hello 프리미엄 계층에서 허용 tooreboot 있습니다 프로그램 캐시 요청 시의 하나 이상의 노드. 이렇게 하면 tootest 실패 하는 hello 이벤트의 복구 기능에 대 한 응용 프로그램입니다. Hello 다음 노드를 다시 부팅할 수 있습니다.

* 캐시의 마스터 노드
* 캐시의 슬레이브 노드
* 캐시의 마스터 및 슬레이브 노드 둘 다
* Hello 마스터, 슬레이브, 또는 두 노드 모두 hello 캐시에 개별 분할 된 데이터베이스에 대 한 프리미엄 캐시를 사용 하 여 클러스터링, 경우 재부팅할 수 있습니다.

자세한 내용은 [다시 부팅](cache-administration.md#reboot) 및 [다시 부팅 FAQ](cache-administration.md#reboot-faq)를 참조하세요.

>[!NOTE]
>이제 모든 Azure Redis Cache 계층에 다시 부팅 기능을 사용할 수 있습니다.
>
>

## <a name="schedule-updates"></a>업데이트를 예약
hello 예약 된 업데이트 기능 toodesignate를 캐시에 대 한 유지 관리 기간이 있습니다. Hello 유지 관리 기간을 지정 하면이 기간 동안 모든 Redis 서버 업데이트 수 있습니다. toodesignate 유지 관리 기간을 원하는 hello 일 선택한 각 날짜에 대 한 hello 유지 관리 창 시작 시간을 지정 합니다. Hello 유지 관리 기간에 UTC를 참고 합니다. 

자세한 내용은 [업데이트 예약](cache-administration.md#schedule-updates) 및 [업데이트 예약 FAQ](cache-administration.md#schedule-updates-faq)를 참조하세요.

> [!NOTE]
> 만 Redis 서버 hello 예약 된 유지 관리 기간 동안 업데이트 됩니다. hello 유지 관리 기간 tooAzure 업데이트는 적용 되지 않습니다 또는 toohello VM 운영 체제를 업데이트 합니다.
> 
> 

## <a name="geo-replication"></a>지역에서 복제

**지역에서 복제**는 두 개의 프리미엄 계층 Azure Redis Cache 인스턴스를 연결하는 메커니즘을 제공합니다. 캐시가 하나는 기본 연결 된 캐시 hello 및 hello hello 보조 연결 캐시로 다른으로 지정 됩니다. hello 보조 연결 된 캐시는 읽기 전용 및 서 면된 toohello 기본 캐시는 데이터 toohello 보조 연결 된 캐시를 복제 합니다. 이 기능은 Azure 지역에서 사용 되는 tooreplicate 캐시 수 있습니다.

자세한 내용은 참조 [어떻게 Azure Redis Cache에 대 한 지리적 복제 tooconfigure](cache-how-to-geo-replication.md)합니다.


## <a name="tooscale-toohello-premium-tier"></a>tooscale toohello premium 계층
tooscale toohello premium 계층 hello에 hello 프리미엄 계층 중 하나를 선택 하면 **가격 책정 계층 변경** 블레이드입니다. 또한 PowerShell 및 CLI를 사용 하 여 캐시 toohello premium 계층을 확장할 수 있습니다. 단계별 지침은 참조 하십시오. [어떻게 tooScale Azure Redis 캐시](cache-how-to-scale.md) 및 [어떻게 tooautomate 크기 조정 작업](cache-how-to-scale.md#how-to-automate-a-scaling-operation)합니다.

## <a name="next-steps"></a>다음 단계
캐시를 만들고 hello 새로운 프리미엄 계층 기능을 탐색 합니다.

* [어떻게 Premium Azure Redis Cache에 대 한 tooconfigure 지 속성](cache-how-to-premium-persistence.md)
* [프리미엄 Azure Redis Cache에 대 한 tooconfigure 가상 네트워크를 지 원하는 방법](cache-how-to-premium-vnet.md)
* [어떻게 tooconfigure Premium Azure Redis Cache에 대 한 클러스터링](cache-how-to-premium-clustering.md)
* [어떻게 tooimport 데이터를 Azure Redis Cache에서 데이터 내보내기 및](cache-how-to-import-export-data.md)
* [Azure Redis 캐시 하는 tooadminister 방법](cache-administration.md)

