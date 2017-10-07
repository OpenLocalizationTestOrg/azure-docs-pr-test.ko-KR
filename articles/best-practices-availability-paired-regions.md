---
title: "BCDR(무중단 업무 방식 및 재해 복구): Azure 쌍을 이루는 지역 | Microsoft Docs"
description: "복원 력 있는 데이터 센터 오류가 발생 하는 동안 응용 프로그램을 Azure 지역 쌍, tooensure에 알아봅니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>BCDR(무중단 업무 방식 및 재해 복구): Azure 쌍을 이루는 지역

## <a name="what-are-paired-regions"></a>쌍을 이루는 지역이란?

Azure는 hello 전 세계 여러 지역에서 작동합니다. Azure 지역에 하나 이상의 Azure 영역을 포함 하는 hello world의 정의 된 영역입니다. Azure 지역은 하나 이상의 데이터 센터를 포함하는 지리적 위치 내의 영역입니다.

각 Azure 영역의 다른 영역 hello 내와 쌍을 이루는 동일한 지역, 지역 쌍을 함께 수행 합니다. hello 예외는 해당 지역 외부 영역을 이루는 브라질 남쪽을입니다.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

그림 1 - Azure 지역 쌍 다이어그램

| Geography | 쌍을 이루는 지역 |  |
|:--- |:--- |:--- |
| 아시아 |동아시아 |동남아시아 |
| 오스트레일리아 |오스트레일리아 동부 |오스트레일리아 남동부 |
| 캐나다 |캐나다 중부 |캐나다 동부 |
| 중국 |중국 북부 |중국 동부|
| 인도 |인도 중부 |인도 남부 |
| 일본 |일본 동부 |일본 서부 |
| 한국 |한국 중부 |한국 남부 |
| 북아메리카 |미국 중북부 |미국 중남부 |
| 북아메리카 |미국 동부 |미국 서부 |
| 북아메리카 |미국 동부 2 |미국 중부 |
| 북아메리카 |미국 서부 2 |미국 중서부 |
| 유럽 |북유럽 |서유럽 |
| 일본 |일본 동부 |일본 서부 |
| 브라질 |브라질 남부(1) |미국 중남부 |
| 미국 정부 |미국 정부 아이오와 |미국 정부 버지니아 |
| 미국 정부 |미국 정부 버지니아 |미국 정부 텍사스 |
| 미국 정부 |미국 정부 텍사스 |미국 정부 애리조나 |
| 미국 정부 |미국 정부 애리조나 |미국 정부 텍사스 |
| 영국 |영국 서부 |영국 남부 |
| 독일 |독일 중부 |독일 북동부 |

표 1 - Azure 지역 쌍 매핑

> (1) 브라질 남부는 해당 지리적 위치 외부에 있는 지역과 쌍을 이루기 때문에 고유합니다. 브라질 남부의 보조 지역은 미국 중남부이지만 미국 중남부의 보조 지역은 브라질 남부가 아닙니다.


Azure의 가용성 및 격리 정책에서 지역 쌍 toobenefit 전체 작업을 복제 하는 것이 좋습니다. 예를 들어 계획 된 Azure 시스템 업데이트 순차적으로 배포 됩니다 (hello에 동시) 쌍 이룬된 지역에 걸쳐 있습니다. 즉, 잘못 된 업데이트의 hello 드문 경우에도 두 영역은 영향을 받지 동시에 합니다. 또한 hello 흔하지 광범위 한 중단, 하나 이상의 영역에서 모든 쌍의 복구 우선 순위를 가지도록 합니다.

## <a name="an-example-of-paired-regions"></a>쌍을 이루는 지역의 예
아래 그림 2에서는 재해 복구에 대 한 hello 지역 쌍을 사용 하는 가상의 응용 프로그램을 보여 줍니다. 녹색 hello 숫자 세 가지 Azure 서비스 (Azure 계산, 저장소, 및 데이터베이스)의 지역 간 활동 hello 선택한 지역에 걸쳐 tooreplicate를 구성 하는 방법을 합니다. hello 주황색 번호로 쌍 이룬된 지역에 걸쳐 배포 hello 특유의 이점은 강조 표시 됩니다.

![쌍을 이루는 지역의 이점 개요](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

그림 2 – 가상의 Azure 지역 쌍

## <a name="cross-region-activities"></a>지역 간 활동
참조 된 tooin으로 그림 2.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **Azure 계산 (PaaS)** – 추가 계산 리소스를 프로 비전 해야 미리 tooensure 리소스가 사용 가능한 다른 지역에서 재해 발생 시. 자세한 내용은 [Azure 복원력 기술 지침](resiliency/resiliency-technical-guidance.md)을 참조하세요.

![저장소](./media/best-practices-availability-paired-regions/2Green.png) **Azure Storage** - GRS(지역 중복 저장소)는 기본적으로 Azure Storage 계정을 만들 때 구성됩니다. Grs를 사용할 경우 데이터는 자동으로 3 번 복제 hello 기본 지역 및 내의 세 번 hello 쌍을 이루는 지역. 자세한 내용은 [Azure 저장소 중복 옵션](storage/common/storage-redundancy.md)을 참조하세요.

![Azure SQL](./media/best-practices-availability-paired-regions/3Green.png) **Azure SQL 데이터베이스** –와 Azure SQL 표준 지역에서 복제, 트랜잭션 tooa 쌍을 이루는 지역의 비동기 복제를 구성할 수 있습니다. 프리미엄 지리적 복제 된 hello world;에서 tooany 지역 복제를 구성할 수 있습니다. 그러나 대부분의 재해 복구 시나리오에 대 한 쌍을 이루는 지역에 이러한 리소스를 배포 하는 것이 좋습니다. 자세한 내용은 [Azure SQL Database의 지역에서 복제](sql-database/sql-database-geo-replication-overview.md)를 참조하세요.

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png) **Azure Resource Manager** Resource Manager는 본질적으로 지역 간 서비스 관리 구성 요소의 논리적 격리를 제공합니다. 즉, 지역에서 논리 오류는 거의 tooimpact 다른 합니다.

## <a name="benefits-of-paired-regions"></a>쌍을 이루는 지역의 이점
참조 된 tooin으로 그림 2.  

![격리](./media/best-practices-availability-paired-regions/5Orange.png)
**물리적 격리** – 가능한 경우 Azure는 모든 지리적 위치에서 실용적이거나 가능한 것은 아니지만 지역 쌍 내 데이터 센터 간에 약 483Km 이상 격리하는 것이 좋습니다. 실제 데이터 센터 분리 hello 자연 재해, 민사 동요, 정전 또는 한 번에 두 지역에 영향을 주는 실제 네트워크 작동 중단 될 가능성을 줄일 수 있습니다. 격리는 hello 지리 (geography 크기, 전원/네트워크 인프라의 가용성, 규정 등) 내에 주체 toohello 제약 합니다.  

![복제](./media/best-practices-availability-paired-regions/6Orange.png)
**플랫폼에서 제공 하는 복제** -지역 중복 저장소와 같은 일부 서비스 제공 toohello 쌍을 이루는 지역 자동 복제 합니다.

![복구](./media/best-practices-availability-paired-regions/7Orange.png)
**지역 복구 순서** – 광범위 한 중단의 hello 이벤트에서 복구 한 영역의 모든 쌍에서 우선 순위가 지정 합니다. 쌍 이룬된 지역에 걸쳐 배포 되는 응용 프로그램에는 우선 순위를 사용 하 여 복구할 hello 지역 중 한 toohave를 보장 됩니다. 쌍으로 연결할 지역에 걸쳐 응용 프로그램을 배포한 경우 복구 지연 될 수 있습니다-에 hello 최악의 사례 hello 선택한 영역에 복구 하는 마지막 두 개의 toobe hello 수 있습니다.

![업데이트](./media/best-practices-availability-paired-regions/8Orange.png)
**순차적 업데이트** -계획 된 Azure 시스템 업데이트를 전달 하는 toopaired 영역 순차적으로 (hello에 동시) toominimize 작동 중단, 버그 및 hello 드문 이벤트의 논리적 오류 hello 효과 잘못 된 업데이트 합니다.

![데이터](./media/best-practices-availability-paired-regions/9Orange.png)
**데이터 상주** – 영역 내에 상주 hello 동일한 순서 toomeet 데이터 상주 요구 사항 세금 및 법 적용 jurisdiction 목적에 쌍 (예외와 함께 hello 브라질 남쪽의)으로 지리적 위치입니다.
