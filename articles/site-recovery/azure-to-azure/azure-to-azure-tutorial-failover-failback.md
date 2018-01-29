---
title: "Azure Site Recovery(미리 보기)를 사용하여 보조 Azure 지역에 복제된 Azure VM 장애 조치(failover) 및 장애 복구(failback)"
description: "Azure Site Recovery를 사용하여 Azure VM 복제를 보조 Azure 지역에 장애 조치(failover) 및 장애 복구(failback)하는 방법을 알아봅니다."
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 11/01/2017
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: 5f37a7b3534102a06f6d5dc6fb91d3abee7c0522
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2017
---
# <a name="fail-over-and-fail-back-azure-vms-between-azure-regions-preview"></a>Azure 지역 간에 Azure VM 장애 조치(Failover) 및 장애 복구(미리 보기)

[Azure Site Recovery](../site-recovery-overview.md) 서비스는 온-프레미스 컴퓨터와 Azure VM(Virtual Machines)의 복제, 장애 조치(failover), 장애 복구(failback)를 관리 및 오케스트레이션하여 재해 복구 전략에 기여합니다.

이 자습서에서는 단일 Azure VM을 보조 Azure 지역에 장애 조치(failover)하는 방법을 설명합니다. 장애 조치(Failover)한 후에 주 지역이 사용 가능해지면 장애 복구(failback)합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure VM 장애 조치(failover)
> * 주 지역에 복제되도록 보조 Azure VM 다시 보호
> * 보조 VM 장애 복구(failback)
> * 보조 지역으로 주 VM 다시 보호

## <a name="prerequisites"></a>필수 조건

- [재해 복구 드릴](azure-to-azure-tutorial-dr-drill.md)을 완료하여 모든 항목이 예상대로 작동하는지 확인합니다.
- 테스트 장애 조치(failover)를 실행하기 전에 VM 속성을 확인합니다. VM은 [Azure 요구 사항](../site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 준수해야 합니다.

## <a name="run-a-failover-to-the-secondary-region"></a>보조 지역으로 장애 조치(failover) 실행

1. **복제된 항목**에서 장애 조치(failover)할 VM > **장애 조치(Failover)**를 선택합니다.

   ![장애 조치(failover)](./media/azure-to-azure-tutorial-failover-failback/failover.png)

2. **장애 조치(Failover)**에서 장애 조치(failover)할 **복구 지점**을 선택합니다. 다음 옵션 중 하나를 사용할 수 있습니다.

   * **최신**(기본값): 이 옵션은 Site Recovery 서비스의 모든 데이터를 처리하고 가장 낮은 RPO(복구 지점 목표)를 제공합니다.
   * **가장 최근에 처리된 시점**: 이 옵션은 Site Recovery 서비스에서 처리한 최근 복구 지점으로 가상 컴퓨터를 되돌립니다.
   * **사용자 지정**: 특정 복구 지점으로 장애 조치(failover)하려면 이 옵션을 사용합니다. 이 옵션은 테스트 장애 조치(failover)를 수행하는 데 유용합니다.

3. 장애 조치를 트리거하기 전에 Site Recovery에서 원본 가상 컴퓨터를 종료하려고 시도하는 경우 **장애 조치(failover)를 시작하기 전에 컴퓨터를 종료합니다**를 선택합니다. 종료가 실패하더라도 장애 조치는 계속됩니다.

4. **작업** 페이지에서 장애 조치(failover) 진행 상황을 확인합니다.

5. 장애 조치 후에 가상 컴퓨터에 로그인하여 해당 가상 컴퓨터의 유효성을 검사합니다. 가상 컴퓨터에 대한 다른 복구 지점으로 이동하려면 **복구 지점 변경** 옵션을 사용할 수 있습니다.

6. 장애 조치된 가상 컴퓨터에 만족하면 장애 조치를 **커밋**할 수 있습니다.
   커밋하면 서비스와 함께 사용할 수 있는 모든 복구 지점이 삭제됩니다. **복구 지점 변경** 옵션은 더 이상 사용할 수 없습니다.

## <a name="reprotect-the-secondary-vm"></a>보조 VM 다시 보호

VM의 장애 조치(failover) 후 주 지역에 다시 복제되도록 다시 보호해야 합니다.

1. VM이 **장애 조치(Failover) 커밋** 상태이고 주 지역을 사용할 수 있는지 확인하면 새 리소스를 만들고 액세스할 수 있습니다.
2. **자격 증명 모음** > **복제된 항목**에서 장애 조치(failover)된 VM을 마우스 오른쪽 단추로 클릭한 다음 **다시 보호**를 선택합니다.

   ![마우스 오른쪽 단추를 클릭하여 다시 보호](./media/azure-to-azure-tutorial-failover-failback/reprotect.png)

2. 보조 지역에서 주 지역으로의 보호 방향이 이미 선택되어 있습니다.
3. **리소스 그룹, 네트워크, 저장소 및 가용성 집합** 정보를 검토합니다. (신규)가 표시된 리소스는 다시 보호 작업의 일부로 생성되었습니다.
4. **확인**을 클릭하여 다시 보호 작업을 트리거합니다. 이 작업은 최신 데이터로 대상 사이트를 시드합니다. 그런 다음 델타를 주 지역에 복제합니다. 이제 VM이 보호된 상태입니다.

## <a name="fail-back-to-the-primary-region"></a>주 지역으로 장애 복구(failback)

VM이 다시 보호된 후 필요에 따라 주 지역으로 장애 복구(failback)할 수 있습니다. 이렇게 하려면 [장애 조치(failover)](#run-a-failover) 지침을 따르세요.
