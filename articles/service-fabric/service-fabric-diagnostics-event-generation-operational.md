---
title: "서비스 패브릭 Operational 채널 aaaAzure | Microsoft Docs"
description: "Hello operational 채널의 Azure 서비스 패브릭 클러스터에 생성 된 로그의 포괄적인 목록입니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>작동 채널 

노드 및 클러스터 서비스 패브릭에서 수행 하는 상위 수준 작업에서 로그의 hello 작동 채널이 구성 됩니다. "진단" hello Azure 진단 에이전트가 클러스터에 배포 되 고는 기본적으로 클러스터에 대해 설정 된 경우 tooread hello Operational 채널에서 로그를 구성 합니다. Hello 구성에 대해 자세히 읽어보세요 [Azure 진단 에이전트가](service-fabric-diagnostics-event-aggregation-wad.md) 자세한 로그 또는 성능 카운터를 프로그램 클러스터 toopick의 toomodify hello 진단 구성 합니다. 

## <a name="operational-channel-logs"></a>작동 채널 로그 

다음은 hello operational 채널의 서비스 패브릭에서 제공 하는 로그의 포괄적인 목록입니다. 

| EventId | 이름 | 원본(태스크) | 수준 |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | 정보 제공 |
| 25621 | NodeOpenedSuccess | FabricNode | 정보 제공 |
| 25622 | NodeOpenedFailed | FabricNode | 정보 제공 |
| 25623 | NodeClosing | FabricNode | 정보 제공 |
| 25624 | NodeClosed | FabricNode | 정보 제공 |
| 25625 | NodeAborting | FabricNode | 정보 제공 |
| 25626 | NodeAborted | FabricNode | 정보 제공 |
| 29627 | ClusterUpgradeStart | CM | 정보 제공 |
| 29628 | ClusterUpgradeComplete | CM | 정보 제공 |
| 29629 | ClusterUpgradeRollback | CM | 정보 제공 |
| 29630 | ClusterUpgradeRollbackComplete | CM | 정보 제공 |
| 29631 | ClusterUpgradeDomainComplete | CM | 정보 제공 |
| 23074 | ContainerActivated | Hosting | 정보 제공 |
| 23075 | ContainerDeactivated | Hosting | 정보 제공 |
| 29620 | ApplicationCreated | CM | 정보 제공 |
| 29621 | ApplicationUpgradeStart | CM | 정보 제공 |
| 29622 | ApplicationUpgradeComplete | CM | 정보 제공 |
| 29623 | ApplicationUpgradeRollback | CM | 정보 제공 |
| 29624 | ApplicationUpgradeRollbackComplete | CM | 정보 제공 |
| 29625 | ApplicationDeleted | CM | 정보 제공 |
| 29626 | ApplicationUpgradeDomainComplete | CM | 정보 제공 |
| 18566 | ServiceCreated | FM | 정보 제공 |
| 18567 | ServiceDeleted | FM | 정보 제공 |

## <a name="next-steps"></a>다음 단계

* 전체에 대 한 자세한 [hello 플랫폼 수준에서 이벤트 생성](service-fabric-diagnostics-event-generation-infra.md) 서비스 패브릭에서
* 수정 프로그램 [Azure 진단](service-fabric-diagnostics-event-aggregation-wad.md) 구성 toocollect 더 기록 합니다.
* [Application Insights 설정](service-fabric-diagnostics-event-analysis-appinsights.md) toosee Operational 채널에 기록
