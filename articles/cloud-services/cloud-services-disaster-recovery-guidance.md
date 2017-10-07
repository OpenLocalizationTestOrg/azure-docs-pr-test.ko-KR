---
title: "Azure 클라우드 서비스에 영향을 주는 Azure 서비스 중단의 hello 이벤트에서 aaaWhat toodo | Microsoft Docs"
description: "어떤 toodo hello Azure 클라우드 서비스에 영향을 주는 Azure 서비스 중단 이벤트에 알아봅니다."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Azure 클라우드 서비스에 영향을 주는 Azure 서비스 중단의 hello 이벤트에서 어떤 toodo
Microsoft에서는 서비스를 항상 사용 가능한 tooyou 필요할 때 하드 toomake를 파악 합니다. 다만 경우에 따라 계획되지 않은 서비스 중단이 발생하여 강제적으로 제어 영향을 벗어날 때가 있습니다.

Microsoft는 작동 시간 및 연결에 대한 약정으로 해당 서비스에 대한 서비스 수준 약정(SLA)을 제공합니다. 개별 Azure 서비스에 대 한 SLA hello에서 찾을 수 있습니다 [Azure 서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)합니다.

Azure에는 항상 사용 가능한 응용 프로그램을 지원하는 많은 기본 제공 플랫폼 기능이 있습니다. 이러한 서비스에 대한 자세한 내용은 [Azure 응용 프로그램에 대한 재해 복구 및 고가용성](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)을 참조하세요.

이 문서에서는 전체 지역 toomajor 자연 재해나 광범위 한 서비스 중단 인해 중단 되는 실제 재해 복구 시나리오를 설명 합니다. 드물게 발생은 이지만 전체 영역의 중단 되는 hello 가능성을 준비 해야 합니다. 전체 영역에서 발생 하는 서비스 중단을 경우 데이터의 hello 로컬 중복 복사본은 일시적으로 사용할 수 없습니다. 지역에서 복제를 사용하는 경우 Azure 저장소 Blob 및 테이블의 추가 사본 3개는 다른 지역에 저장됩니다. 전체 지역 가동 중단 또는 재해는 hello에 기본 지역을 복구할 수의 hello 이벤트에서 Azure 다시 모든 hello DNS 항목 toohello 지리적 복제 지역 매핑합니다.

> [!NOTE]
> 이 프로세스는 사용자가 제어할 수 없으며 데이터 센터 전체 서비스 중단에 대해서만 발생합니다. 이 때문에 다른 응용 프로그램별 백업 전략 tooachieve hello 최고 수준의 가용성에 의존 해야 있습니다. 자세한 내용은 [Microsoft Azure에서 빌드된 응용 프로그램에 대한 재해 복구 및 고가용성](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)을 참조하세요. Toobe 수 tooaffect 원하는 경우 고유한 장애 조치의 tooconsider hello 사용 할 수 있습니다 [읽기 액세스 지역 중복 저장소 (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), 다른 지역에 데이터의 읽기 전용 복사본을 만듭니다는 합니다.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>옵션 1: Azure Traffic Manager를 통해 백업 배포 사용
hello 가장 강력한 재해 복구 솔루션에서는 다른 지역에 응용 프로그램의 배포를 여러 개 유지 관리를 사용 하 여 다음 [Azure 트래픽 관리자](../traffic-manager/traffic-manager-overview.md) 둘 사이의 toodirect 트래픽입니다. Azure 트래픽 관리자에서 다중 제공 [라우팅 메서드](../traffic-manager/traffic-manager-routing-methods.md)여부 toomanage 기본/백업 모델이 나 toosplit 사용 하 여 배포 간의 트래픽이 선택할 수 있는, 해당 합니다.

![Azure 트래픽 관리자를 사용하여 지역 간에 Azure 클라우드 서비스 분산](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Hello 가장 빠른 응답 toohello 손실을 영역에 대 한 것이 트래픽 관리자를 구성 하는 중요 [끝점 모니터링](../traffic-manager/traffic-manager-monitoring.md)합니다.

## <a name="option-2-deploy-your-application-tooa-new-region"></a>옵션 2: 응용 프로그램 tooa 새 영역 배포
Hello 이전 옵션에 설명 된 대로 여러 활성 배포를 유지 관리 추가 지속적인 비용을 발생 시킵니다. 복구 시간 목표 (RTO)은 만큼 충분히 유연 하 고 hello 원래 코드 또는 컴파일된 클라우드 서비스 패키지를 다른 영역에 응용 프로그램의 새 인스턴스를 만들 하 고 DNS 레코드 toopoint toohello 새 배포를 업데이트할 수 있습니다.

방법에 대 한 자세한 내용은 toocreate 클라우드 서비스 응용 프로그램을 배포 하 고, 참조 [어떻게 toocreate 클라우드 서비스 및 배포](cloud-services-how-to-create-deploy-portal.md)합니다.

응용 프로그램의 데이터 원본에 따라 응용 프로그램 데이터 소스에 대 한 toocheck hello 복구 절차를 할 수 있습니다.

* Azure 저장소 데이터 원본에 대 한 참조 [Azure 저장소 복제](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck hello에 따라 사용할 수 있는 hello 옵션에는 응용 프로그램에 대 한 복제 모델을 선택 합니다.
* SQL 데이터베이스 원본에 대 한 읽기 [개요: SQL 데이터베이스 비즈니스 연속성 및 데이터베이스 재해 복구 클라우드](../sql-database/sql-database-business-continuity.md) 응용 프로그램에 대 한 선택 hello 복제 모델을 기반으로 사용할 수 있는 hello 옵션에 toocheck 합니다.


## <a name="option-3-wait-for-recovery"></a>옵션 3: 복구 대기
이 경우 사용자의 조치가 필요 하지 않습니다, 하지만 hello 영역 복원 될 때까지 프로그램 서비스를 사용할 수 없습니다. Hello에 hello 현재 서비스 상태를 볼 수 있습니다 [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/)합니다.

## <a name="next-steps"></a>다음 단계
toolearn tooimplement 재해 복구 및 고가용성 전략을 참조 하는 방법에 대 한 자세한 [Azure 응용 프로그램에 대 한 고가용성 및 재해 복구](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)합니다.

클라우드 플랫폼의 기능에 대 한 자세한 기술적 이해 toodevelop 참조 [Azure 복원 력 기술 지침](../resiliency/resiliency-technical-guidance.md)합니다.
