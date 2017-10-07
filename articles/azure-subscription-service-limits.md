---
title: "aaaAzure 구독 제한 및 할당량 | Microsoft Docs"
description: "일반적인 Azure 구독 및 서비스 제한, 할당량 및 제약 조건 목록을 제공합니다. 최대 값과 함께 tooincrease 제한 하는 방법에 대 한 정보가 포함 됩니다."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Azure 구독 및 서비스 제한, 할당량 및 제약 조건
이 문서 라고도 할당량 hello 가장 일반적인 Microsoft Azure 제한을 보여 줍니다. 현재 이 문서에서는 일부 Azure 서비스에 대해 다룹니다. 시간이 지남에 따라 hello 목록 확장 될 것이 고 hello 플랫폼의 자세한 toocover를 업데이트 합니다.

방문 하세요 [Azure 가격 책정 개요](https://azure.microsoft.com/pricing/) toolearn Azure 가격에 대 한 자세한 합니다. Hello를 사용 하 여 비용을 예측할 수, [가격 계산기](https://azure.microsoft.com/pricing/calculator/) 또는 hello 가격 책정 서비스에 대 한 세부 정보 페이지를 방문 하 여 (예를 들어 [Windows Vm](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)). 팁 toohelp에 대 한 비용을 관리, 참조 [Azure 청구 및 비용 관리를 사용 하 여 예기치 않은 비용을 방지](billing/billing-getting-started.md)합니다.

> [!NOTE]
> Tooraise hello 제한 또는 hello 위에 할당량 원하면 **기본 제한**, [비용 없이 온라인 고객 지원 요청을 개시](azure-supportability/resource-manager-core-quotas-request.md)합니다. hello 제한 수준을 올릴 수 없습니다 hello 위에 **최대 한도** 다음 표에서 hello에 표시 된 값입니다. 없는 경우 없는 **최대 한도** 열에서 다음 hello 리소스 제한을 조정할 수 없는 경우. 
> 
> 무료 평가판 구독을 제한하거나 할당량을 증가할 수 없습니다. 무료 평가판을 설정한 경우 업그레이드할 수 tooa [종 량 제](https://azure.microsoft.com/offers/ms-azr-0003p/) 구독 합니다. 자세한 내용은 참조 [Azure 무료 평가판 업그레이드 tooPay-으로--제](billing/billing-upgrade-azure-subscription.md)합니다.
> 

## <a name="limits-and-hello-azure-resource-manager"></a>제한 및 hello Azure 리소스 관리자
가능한 toocombine은 이제 여러 Azure 리소스 tooa에서 단일 Azure 리소스 그룹입니다. 리소스 그룹을 사용할 때 전역 졌 제한 될 hello Azure 리소스 관리자가 있는 지역 수준에서 관리 됩니다. Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](azure-resource-manager/resource-group-overview.md)를 참조하세요.

새 테이블 아래의 hello 제한 되었습니다 추가 tooreflect 제한에서 모든 차이점 hello Azure 리소스 관리자를 사용 하는 경우. 예를 들어, **구독 제한** 테이블 및 **구독 제한 - Azure Resource Manager** 테이블이 있습니다. 제한 tooboth 시나리오에 적용 되 hello 첫 번째 테이블에만 표시 됩니다. 별도로 지정하지 않으면 제한은 모든 지역에 걸쳐 전역으로 적용됩니다.

> [!NOTE]
> Hello 서비스 관리 할당량은 Azure 리소스 그룹의 리소스에 대 한 할당량 지역 구독에 액세스할 수 있으며이 아닌 구독 당 중요 tooemphasize 상태가. 코어 할당량을 한 예로 살펴보겠습니다. Toodecide 어떻게 필요한 toorequest 코어를 지 원하는 할당량 증가 해야 할 경우 어떤 지역에서 toouse을 다음 Azure 리소스 그룹에 대 한 특정 요청을 확인 하는 많은 코어 할당량을 hello 금액 및 원하는 지역에 대 한 핵심입니다. 따라서 toouse 30 해야 할 경우 코어가 서 부 유럽 toorun에서 응용 프로그램에 있습니다. 특히 서 부 유럽에서 30 개 코어를 요청 해야 합니다. 하지만 다른 지역에 코어 할당량 없을 것-hello 30 코어 할당량을 갖는 서 부 유럽만 합니다.
> <!-- -->
> 결과적으로, Azure 리소스 그룹 할당량 필요한 toobe 금액을 고려 하 고 배포 하는 각 지역에는 하나의 영역 및 요청 작업에 대 한 결정 하는 유용한 tooconsider 것 것을 알 수 있습니다. 특정 지역의 현재 할당량 검색에 대한 자세한 내용은 [배포 문제 해결](resource-manager-common-deployment-errors.md) 을 참조하세요.
> 
> 

## <a name="service-specific-limits"></a>서비스 특정 제한
* [Active Directory](#active-directory-limits)
* [API 관리](#api-management-limits)
* [앱 서비스](#app-service-limits)
* [응용 프로그램 게이트웨이](#application-gateway-limits)
* [Application Insights](#application-insights-limits)
* [자동화](#automation-limits)
* [Azure Cosmos DB](#azure-cosmos-db-limits)
* [Azure Event Grid](#azure-event-grid-limits)
* [Azure Redis 캐시(영문)](#azure-redis-cache-limits)
* [Azure RemoteApp](#azure-remoteapp-limits)
* [백업](#backup-limits)
* [배치](#batch-limits)
* [BizTalk 서비스](#biztalk-services-limits)
* [CDN](#cdn-limits)
* [Cloud Services](#cloud-services-limits)
* [Container Instances](#container-instances-limits)
* [데이터 팩터리](#data-factory-limits)
* [데이터 레이크 분석](#data-lake-analytics-limits)
* [Data Lake Store](#data-lake-store-limits)
* [DNS](#dns-limits)
* [이벤트 허브](#event-hubs-limits)
* [IoT 허브](#iot-hub-limits)
* [키 자격 증명 모음](#key-vault-limits)
* [Log Analytics/Operational Insights](#log-analytics-limits)
* [미디어 서비스](#media-services-limits)
* [모바일 고객 관리](#mobile-engagement-limits)
* [모바일 서비스](#mobile-services-limits)
* [모니터](#monitor-limits)
* [Multi-Factor Authentication](#multi-factor-authentication)
* [네트워킹](#networking-limits)
* [Network Watcher](#network-watcher-limits)
* [알림 허브 서비스](#notification-hub-service-limits)
* [리소스 그룹](#resource-group-limits)
* [스케줄러](#scheduler-limits)
* [이를 통해 검색](#search-limits)
* [서비스 버스](#service-bus-limits)
* [사이트 복구](#site-recovery-limits)
* [SQL 데이터베이스](#sql-database-limits)
* [저장소](#storage-limits)
* [StorSimple 시스템](#storsimple-system-limits)
* [스트림 분석](#stream-analytics-limits)
* [구독](#subscription-limits)
* [트래픽 관리자](#traffic-manager-limits)
* [가상 컴퓨터](#virtual-machines-limits)
* [가상 컴퓨터 크기 집합](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a>구독 제한
#### <a name="subscription-limits"></a>구독 제한
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>구독 제한 - Azure Resource Manager
다음 제한 hello hello Azure 리소스 관리자 및 Azure 리소스 그룹을 사용할 때 적용 됩니다. Azure 리소스 관리자 hello로 변경 되지 않은 제한 사항은 다음과 같습니다. 이러한 제한에 대 한 toohello 이전 표를 참조 하십시오.

리소스 관리자 요청의 제한 처리에 대한 정보는 [리소스 관리자 요청 제한](resource-manager-request-limits.md)을 참조하세요.

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a>리소스 그룹 제한
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>가상 컴퓨터 제한
#### <a name="virtual-machine-limits"></a>가상 컴퓨터 제한
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a>가상 컴퓨터 제한 - Azure 리소스 관리자
다음 제한 hello hello Azure 리소스 관리자 및 Azure 리소스 그룹을 사용할 때 적용 됩니다. Azure 리소스 관리자 hello로 변경 되지 않은 제한 사항은 다음과 같습니다. 이러한 제한에 대 한 toohello 이전 표를 참조 하십시오.

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>가상 컴퓨터 크기 집합 제한
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a>Container Instances 제한
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a>네트워킹 제한
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>네트워킹 제한
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>Application Gateway 제한
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a>Network Watcher 제한
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a>트래픽 관리자 제한
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>DNS 제한
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>저장소 제한
저장소 계정 제한에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage/common/storage-scalability-targets.md)를 참조하세요.
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a>저장소 서비스 제한
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a>가상 컴퓨터 디스크 제한 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

자세한 내용은 [가상 컴퓨터 크기](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

#### <a name="managed-virtual-machine-disks"></a>관리되는 가상 컴퓨터 디스크

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a>관리되지 않는 가상 컴퓨터 디스크

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>저장소 리소스 공급자 제한
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a>클라우드 서비스 제한
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a>앱 서비스 제한
앱 서비스 제한 hello 다음 웹 앱, 모바일 앱, API 앱 및 논리 앱에 대 한 제한을 포함 합니다.

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>스케줄러 제한
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>배치 제한
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a>BizTalk 서비스 제한
hello 다음 표에 hello 제한을 Azure Biztalk 서비스에 대 한 있습니다.

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a>Azure Cosmos DB 제한
Azure Cosmos DB에는 처리량 및 저장소 수 크기 조정 된 toohandle 응용 프로그램에 필요한 대로 지정 세계적인 규모 데이터베이스입니다. Azure Cosmos DB에는 hello 눈금에 대 한 질문이 있으면 전자 메일을 보내 주십시오 tooaskcosmosdb@microsoft.com합니다.

### <a name="mobile-engagement-limits"></a>모바일 참여 제한
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a>검색 제한
가격 책정 hello 용량 및 검색 서비스의 한계를 결정 합니다. 계층은 다음을 포함합니다.

* *무료* 다중 테넌트 서비스는 다른 Azure 구독자와 공유되며 평가 및 소규모 개발 프로젝트용으로 사용하기 위한 것입니다.
* *기본* 를 항상 사용 가능한 쿼리 워크 로드에 대 한 toothree 복제본에 더 작은 규모로 프로덕션 작업에 대 한 전용된 컴퓨팅 리소스 제공.
* *표준(S1, S2, S3, S3 고밀도)* 은 더 큰 프로덕션 작업용입니다. 여러 수준 작업 부하 프로필에 가장 적합 한 리소스 구성을 선택할 수 있도록 hello 표준 계층 내에 존재 합니다.

**구독당 제한**

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**검색 서비스당 제한**

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

문서 크기, 초, 키, 요청 및 응답을 당 쿼리 등의 보다 세부적인 수준에 대 한 제한에 대해 자세히 toolearn 참조 [서비스에서 Azure 검색의 제한](search/search-limits-quotas-capacity.md)합니다.

### <a name="media-services-limits"></a>미디어 서비스 제한
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>CDN 제한
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>모바일 서비스 제한
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a>모니터 제한
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>알림 허브 서비스 제한
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>이벤트 허브 제한
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>서비스 버스 제한
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>IoT Hub 제한
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>데이터 팩터리 제한
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Data Lake Analytics 제한
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a>Data Lake Store 제한
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a>스트림 분석 제한
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Active Directory 제한
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a>Azure Event Grid 제한
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a>Azure RemoteApp 제한
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>StorSimple 시스템 제한
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a>Log Analytics 한도
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>백업 제한
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>사이트 복구 제한
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Application Insights 제한
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>API 관리 제한
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Azure Redis 캐시 제한
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>키 값 제한
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>자동화 한도
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>SQL 데이터베이스 제한
SQL 데이터베이스 제한은 [SQL 데이터베이스 리소스 제한](sql-database/sql-database-resource-limits.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
[Azure 제한 및 증가 이해](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[클라우드 서비스 크기](cloud-services/cloud-services-sizes-specs.md)

