---
title: "aaa VM 유지 유지 관리에 대해 Azure에서 Windows Vm | Microsoft Docs"
description: "메모리 보존 업데이트를 위한 전체 VM 마이그레이션"
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>전체 VM 마이그레이션을 사용한 VM 보존 유지 관리

Hello 대부분의 업데이트 있을 없습니다 영향 toohosted Vm, toocomponents 업데이트 또는 서비스 (hello 가상 컴퓨터의 전체 다시 부팅) 없이 최소 수준이 며 toorunning Vm에서에서 발생 하는 경우가 있습니다.

이러한 업데이트는 원위치 실시간 마이그레이션을 가능하게 하는 기술(“메모리 보존 업데이트”)을 통해 완수됩니다. Hello 호스트를 업데이트할 때 "일시 중지 된" 상태로 hello 가상 컴퓨터가 배치는 호스팅 환경 (예: 기본 운영 체제) hello hello 필요한 업데이트 및 패치를 적용 하는 동안 RAM에 hello 메모리를 유지 합니다.
다음의 일시 중지 되 고 30 초 내 hello 가상 컴퓨터 다시 시작 됩니다.
다시 시작 후 hello 클록 hello 가상 컴퓨터에 자동으로 동기화 됩니다.

이 메커니즘을 사용 하 여 모든 업데이트를 배포할 수 있지만 지정 된 짧은 일시 중지 기간 영향 toovirtual 컴퓨터 줄어듭니다 크게 방식으로이에 업데이트를 배포 합니다.

다중 인스턴스 업데이트(가용성 집합의 VM)는 한 번에 하나의 업데이트 도메인에 적용됩니다.

일부 응용 프로그램은 이러한 업데이트로 인해 다른 응용 프로그램보다 더 많은 영향을 받을 수 있습니다. 않을 예를 들어 실시간 이벤트 처리, 미디어 스트리밍을 또는 코드 변환, 또는 처리량이 높은 네트워킹 시나리오를 수행 하는 응용 프로그램 디자인 된 tootolerate 30 초 일시 중지 하지 수 있습니다. 가상 컴퓨터에서 실행 중인 응용 프로그램 호출 hello 하 여 예정 된 업데이트를 알 수 [예약 된 이벤트](../virtual-machines-scheduled-events.md) hello의 API [Azure 메타 데이터 서비스](../virtual-machines-instancemetadataservice-overview.md)합니다.
