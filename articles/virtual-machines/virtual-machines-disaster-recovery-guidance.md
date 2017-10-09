---
title: "Azure Vm에 대 한 복구 시나리오 aaaDisaster | Microsoft Docs"
description: "어떤 toodo Azure 서비스 중단 Azure 가상 컴퓨터에 영향을 줍니다 hello 이벤트에 알아봅니다."
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Azure 서비스 중단 Azure Vm에 영향을 줍니다 hello 이벤트에서 어떤 toodo
Microsoft에서는 서비스를 항상 사용 가능한 tooyou 필요할 때 하드 toomake를 파악 합니다. 다만 경우에 따라 계획되지 않은 서비스 중단이 발생하여 강제적으로 제어 영향을 벗어날 때가 있습니다.

Microsoft는 작동 시간 및 연결에 대한 약정으로 해당 서비스에 대한 서비스 수준 약정(SLA)을 제공합니다. 개별 Azure 서비스에 대 한 SLA hello에서 찾을 수 있습니다 [Azure 서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)합니다.

Azure에는 항상 사용 가능한 응용 프로그램을 지원하는 많은 기본 제공 플랫폼 기능이 있습니다. 이러한 서비스에 대한 자세한 내용은 [Azure 응용 프로그램에 대한 재해 복구 및 고가용성](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)을 참조하세요.

이 문서에서는 전체 지역 toomajor 자연 재해나 광범위 한 서비스 중단 인해 중단 되는 실제 재해 복구 시나리오를 설명 합니다. 드물게 발생은 이지만 전체 영역의 중단 되는 hello 가능성을 준비 해야 합니다. 전체 영역에서 발생 하는 서비스 중단을 경우 데이터의 hello 로컬 중복 복사본은 일시적으로 사용할 수 없습니다. 지역에서 복제를 사용하는 경우 Azure 저장소 Blob 및 테이블의 추가 사본 3개는 다른 지역에 저장됩니다. 전체 지역 가동 중단 또는 재해는 hello에 기본 지역을 복구할 수의 hello 이벤트에서 Azure 다시 모든 hello DNS 항목 toohello 지리적 복제 지역 매핑합니다.

이러한 드문 경우를 처리 하는 toohelp, hello hello 전체 영역 응용 프로그램이 Azure 가상 컴퓨터를 배포 하는 서비스 중단의 hello 경우에서 Azure 가상 컴퓨터에 대 한 지침 제공 합니다.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>옵션 1: Azure Site Recovery를 사용하여 장애 조치(failover) 시작
비교적 짧은 시간에 한 번의 클릭으로 응용 프로그램을 복구할 수 있도록 VM에 Azure Site Recovery를 구성할 수 있습니다. 사용자가 선택한 tooAzure 영역 및 제하지 없음 toopaired 영역을 복제할 수 있습니다. [가상 컴퓨터를 복제](https://aka.ms/a2a-getting-started)하여 시작할 수 있습니다. 있습니다 수 [복구 계획을 만드는](../site-recovery/site-recovery-create-recovery-plans.md) 응용 프로그램에 대 한 hello 전체 장애 조치 프로세스를 자동화할 수 있도록 합니다. 있습니다 수 [테스트 프로그램 장애 조치](../site-recovery/site-recovery-test-failover-to-azure.md) 프로덕션 응용 프로그램 또는 hello 진행 중인 복제 영향을 주지 않고 사전에 미리 합니다. 방금 hello 기본 지역 중단 이벤트에서 [장애 조치를 시작할](../site-recovery/site-recovery-failover.md) 대상 지역에서 응용 프로그램 상태로 전환 합니다.


## <a name="option-2-wait-for-recovery"></a>옵션 2: 복구 대기
이 경우에 사용자의 조치가 필요하지 않습니다. 노력 하 고 충분히 toorestore 서비스 가용성을 알고 있습니다. hello 현재 서비스 상태를 확인할 수 있습니다이 [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/)합니다.

Azure 사이트 복구, 읽기 액세스 지역 중복 저장소 또는 이전 toohello 중단 지역 중복 저장소를 설정 하지 않은 경우 hello 최상의 옵션입니다. 설정한 경우 지역 중복 저장소 또는 hello 저장소 계정에 대 한 읽기 액세스 지역 중복 저장소를 VM 가상 하드 드라이브 (Vhd)이 저장 되는 위치, toorecover hello 기본 VHD 이미지를 찾을 수 있으며 tooprovision 여기에서 새 VM을 시도 합니다. 이 옵션은 데이터 동기화를 보장할 수 없기 때문에 권장되는 옵션이 아닙니다. 따라서이 옵션은 toowork를 보장 되지 않습니다.


> [!NOTE]
> 이 프로세스는 사용자가 제어할 수 없으며 지역 전체 서비스 중단에 대해서만 발생합니다. 이 때문에 다른 응용 프로그램별 백업 전략 tooachieve hello 최고 수준의 가용성에 의존 해야 있습니다. 자세한 내용은 hello 섹션을 참조 [재해 복구를 위한 데이터 전략](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery)합니다.
>
>

## <a name="next-steps"></a>다음 단계

- Azure Site Recovery를 사용하여 [Azure 가상 컴퓨터에서 실행 중인 응용 프로그램 보호](https://aka.ms/a2a-getting-started)를 시작합니다.

- toolearn tooimplement 재해 복구 및 고가용성 전략을 참조 하는 방법에 대 한 자세한 [Azure 응용 프로그램에 대 한 고가용성 및 재해 복구](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)합니다.

- 클라우드 플랫폼의 기능에 대 한 자세한 기술적 이해 toodevelop 참조 [Azure 복원 력 기술 지침](../resiliency/resiliency-technical-guidance.md)합니다.


- Hello 지침은 명확 하지 않거나 다른 사용자에 대 한 Microsoft toodo hello 작업 선택에 게 문의 [고객 지원](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.
