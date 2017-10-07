---
title: "사이트 복구와 aaaMigrate tooAzure | Microsoft Docs"
description: "이 문서에서는 마이그레이션 Vm 및 Azure 사이트 복구와 실제 서버 tooAzure 개요"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>사이트 복구와 tooAzure 마이그레이션

가상 컴퓨터와 물리적 서버와의 마이그레이션에 대 한 hello Azure Site Recovery 서비스를 사용 하 여이 문서에 대 한 개요를 읽습니다.

사이트 복구는 온-프레미스 물리적 서버와 가상 컴퓨터 toohello 클라우드 (Azure) 또는 tooa 보조 데이터 센터의 복제를 조정 함으로써 tooyour BCDR 전략을 강화 하는 Azure 서비스입니다. 기본 위치에서 중단이 발생할 때 장애 조치 toohello 보조 위치 tookeep 앱 및 워크 로드에 사용할 수 있습니다. Toonormal 작업을 반환 하는 경우 백 tooyour 기본 위치를 실패 합니다. [사이트 복구란?](site-recovery-overview.md) 또한 사이트 복구 toomigrate 기존 온-프레미스 작업 부하 tooAzure tooexpedite 클라우드 여행 및 avail hello Azure에서 제공 하는 기능을 사용할 수 있습니다.

간략 한 개요는 방법에 대 한 tooperform 마이그레이션 toothis 비디오를 참조 하십시오.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

이 문서에서는 hello에 대 한 배포 설명 [Azure 포털](https://portal.azure.com)합니다. hello [Azure 클래식 포털](https://manage.windowsazure.com/) 수 toomaintain 사용 되는 기존 사이트 복구 자격 증명 있지만 새 자격 증명 모음을 만들 수 없습니다.

이 문서의 맨 아래 hello에 대 한 설명을 게시 합니다. Hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="what-do-we-mean-by-migration"></a>마이그레이션 기준은 어떤 의미인가요?

온-프레미스 가상 컴퓨터 및 물리적 서버, tooAzure 또는 tooa 보조 사이트의 복제에 대 한 Site Recovery를 배포할 수 있습니다. 복제 하는 컴퓨터를 장애 조치 hello 기본 사이트에서 중단이 발생 하 고 복구 하는 경우 백 toohello 주 사이트 실패 하는 경우. 또한 toothis에서 사용자가 Azure Vm으로 액세스할 수 있도록 사이트 복구 toomigrate Vm 및 물리적 서버 tooAzure 사용할 수 있습니다. 마이그레이션 시 복제 및 hello 주 사이트 tooAzure에서 장애 조치 및 마이그레이션 완료 제스처 작업이 수행 됩니다.

## <a name="what-can-site-recovery-migrate"></a>Site Recovery로 무엇을 마이그레이션할 수 있나요?

다음을 수행할 수 있습니다.

- Azure Vm에서 온-프레미스 Hyper-v Vm, VMware Vm 및 물리적 서버 toorun에서 실행 되는 워크 로드를 마이그레이션하십시오. 이 시나리오에서는 전체 복제 및 장애 복구도 수행할 수 있습니다.
- Azure 지역 간에 [Azure IaaS VM](site-recovery-migrate-azure-to-azure.md)을 마이그레이션합니다. 이 시나리오에서는 현재 마이그레이션만을 지원하며 장애 복구는 지원되지 않습니다.
- 마이그레이션 [AWS Windows 인스턴스](site-recovery-migrate-aws-to-azure.md) tooAzure IaaS Vm입니다. 이 시나리오에서는 현재 마이그레이션만을 지원하며 장애 복구는 지원되지 않습니다.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>온-프레미스 VM 및 물리적 서버를 마이그레이션합니다.

toomigrate 온-프레미스 Hyper-v Vm, VMware Vm 및 물리적 서버, 거의 hello를 일반 복제에 사용 되는 동일한 단계를 수행 합니다.

1. Recovery Services 자격 증명 모음 설정
2. 필요한 hello 관리 서버 구성 (VMM에서 VMware 하이퍼-V-대상에 따라 toomigrate) toohello 자격 증명 모음에 추가 하 고 복제 설정을 지정 합니다.
3. Hello 컴퓨터에 대 한 복제를 사용 하도록 설정 하려면 toomigrate
4. Hello 초기 마이그레이션 후 모든 기능이 예상 대로 작동 하는 간단한 테스트 장애 조치 tooensure를 실행 합니다.
5. 복제 환경이 제대로 작동하는지 확인한 후에 시나리오의 [지원 기능](site-recovery-failover.md)에 따라 계획되거나 계획되지 않은 장애 조치를 사용합니다. 가능하면 계획된 장애 조치를 사용하는 것이 좋습니다.
6. 마이그레이션에 대 한 장애 조치 toocommit 필요 하지 않거나 삭제 키를 누릅니다. Hello를 선택 하는 대신, **마이그레이션을 완료** 옵션 toomigrate 하려는 각 컴퓨터에 대 한 합니다.
     - **복제 항목**hello VM을 마우스 오른쪽 단추로 클릭 하 고 클릭 **마이그레이션을 완료**합니다. 클릭 **확인** toocomplete 합니다. Hello 전체 마이그레이션 작업을 모니터링 하 여에서 hello VM 속성에서 진행률을 추적할 수 있습니다 **사이트 복구 작업이**합니다.
     - hello **마이그레이션을 완료** 동작 hello 마이그레이션 프로세스를 완료 hello 컴퓨터에 대 한 복제를 제거 하 고 hello 컴퓨터에 대 한 사이트 복구 청구를 중지 합니다.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Azure 지역 간 마이그레이션

Site Recovery를 사용하여 지역 간에 Azure VM을 마이그레이션할 수 있습니다. 이 시나리오에서는 마이그레이션만 지원됩니다. 즉, hello Azure Vm을 복제 하 고 장애 조치 tooanother 영역 수 있지만 다시 실패로 지정할 수 없습니다. 복구 서비스 자격 증명 모음을 설정 하는이 시나리오에서는 온-프레미스 구성 서버 toomanage 복제를 배포, toohello 자격 증명 모음을 추가 하 고 복제 설정을 지정 합니다. Hello 컴퓨터 toomigrate, 빠른 실행 및 테스트 장애 조치에 대 한 복제를 설정 합니다. 다음 hello로 예기치 않은 장애 조치가 실행 **마이그레이션을 완료** 옵션입니다.

## <a name="migrate-aws-tooazure"></a>AWS tooAzure 마이그레이션

AWS 인스턴스 tooAzure Vm을 마이그레이션할 수 있습니다. 이 시나리오에서는 마이그레이션만 지원됩니다. 즉, hello AWS 인스턴스를 복제 하 고 장애 조치 tooAzure, 수 있지만 다시 실패로 지정할 수 없습니다. AWS 인스턴스에서에서 처리 되는 hello 동일한 방식으로 마이그레이션하기 위해 물리적 서버입니다. 복구 서비스 자격 증명 모음 설정, 배포는 온-프레미스 구성 서버 toomanage 복제, toohello 자격 증명 모음을 추가 하 복제 설정을 지정 합니다. Hello 컴퓨터 toomigrate, 빠른 실행 및 테스트 장애 조치에 대 한 복제를 설정 합니다. 다음 hello로 예기치 않은 장애 조치가 실행 **마이그레이션을 완료** 옵션입니다.




## <a name="next-steps"></a>다음 단계

- [VMware Vm tooAzure 마이그레이션](site-recovery-vmware-to-azure.md)
- [Hyper-v Vm VMM 클라우드에 tooAzure 마이그레이션하십시오.](site-recovery-vmm-to-azure.md)
- [VMM tooAzure 없이 Hyper-v Vm을 마이그레이션하십시오.](site-recovery-hyper-v-site-to-azure.md)
- [Azure 지역 간에 Azure VM 마이그레이션](site-recovery-migrate-azure-to-azure.md)
- [AWS 인스턴스 tooAzure 마이그레이션](site-recovery-migrate-aws-to-azure.md)
- [마이그레이션된 컴퓨터 tooenable 복제 준비](site-recovery-azure-to-azure-after-migration.md) 재해 복구 요구에 따라 tooanother 영역입니다.
- [Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.
