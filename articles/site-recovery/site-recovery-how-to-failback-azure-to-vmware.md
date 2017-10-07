---
title: "Azure tooVMware에서 다시 aaaHow toofail | Microsoft Docs"
description: "가상 컴퓨터 tooAzure의 장애 조치 후에 장애 복구 toobring 가상 컴퓨터 백 tooon 온-프레미스를 시작할 수 있습니다. Toofail 다시 하는 방법에 대 한 hello 단계에 알아봅니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Azure tooan 온-프레미스 사이트에서 다시 실패

이 문서에서는 toofail Azure 가상 컴퓨터 toohello 온-프레미스 사이트에서 가상 컴퓨터를 백업 하는 방법을 설명 합니다. 이 문서 toofail의 지침에 따라 hello 후에 다시 VMware 가상 컴퓨터 또는 Windows/Linux 물리적 서버의 한 장애 조치 hello 온-프레미스 사이트 tooAzure에서 hello를 사용 하 여 [복제 VMware 가상 컴퓨터 및 물리적 Azure Site Recovery와 서버 tooAzure](site-recovery-vmware-to-azure-classic.md) 자습서입니다.

> [!WARNING]
> 있는 경우 [마이그레이션을 완료](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), 그룹 또는 삭제 된 가상 컴퓨터 tooanother 리소스 이동된 hello hello Azure 가상 컴퓨터, 그 후 장애 복구를 수 없습니다.

> [!NOTE]
> 장애 조치 VMware 가상 컴퓨터 장애 복구 tooa hyper-v 호스트가 없습니다.

## <a name="overview-of-failback"></a>장애 복구 개요
장애 복구(failback)의 작동 방식은 다음과 같습니다. 장애 조치 tooAzure, 한 후에 몇 가지 단계로 뒤로 tooyour 온-프레미스 사이트를 실패:

1. [다시 보호](site-recovery-how-to-reprotect.md) tooreplicate tooVMware 가상 컴퓨터가 온-프레미스 사이트에서 시작 되도록 Azure에서 가상 컴퓨터를 hello 합니다. 이 프로세스의 일부로 다음 작업을 수행해야 합니다.
    1. 온-프레미스 마스터 대상 설정: Windows 가상 컴퓨터에 대한 Windows 마스터 대상 및 Linux 가상 컴퓨터에 대한 [Linux 마스터 대상](site-recovery-how-to-install-linux-master-target.md).
    2. [프로세스 서버](site-recovery-vmware-setup-azure-ps-resource-manager.md) 설정.
    3. [다시 보호](site-recovery-how-to-reprotect.md) 시작. 그러면 hello 온-프레미스 가상 컴퓨터를 끄고 되 고 동기화 hello Azure 가상 컴퓨터의 hello로 온-프레미스 데이터 디스크.
5. Azure에서 가상 컴퓨터를 tooyour 온-프레미스 사이트를 복제 하는 후에서 시작 하면 오류를 통해 Azure toohello 온-프레미스 사이트입니다.

데이터에 실패 한 다시 tooreplicate tooAzure 시작 되도록 hello 온-프레미스 가상 컴퓨터를 다시 장애를 해제 합니다.

간략 한 개요에 대 한 hello 다음 방법을 통해 toofail tooan Azure에서 온-프레미스 사이트에 대 한 비디오를 시청 합니다.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>뒤로 toohello 원래 위치 또는 대체 위치로 실패

VMware 가상 컴퓨터를 통해 실패 한 경우 동일한 소스 온-프레미스 가상 컴퓨터가 여전히 하는 경우 백 toohello를 실패할 수 있습니다. 이 시나리오에서는 hello 변경만 다시 복제 됩니다. 이 시나리오를 원본 위치 복구라고 합니다. Hello 온-프레미스 가상 컴퓨터가 없는 경우 hello 시나리오는 대체 위치 복구입니다.

> [!NOTE]
> 구성 서버 및 장애 복구 toohello 원래 vCenter만 할 수 있습니다. 새 구성 서버를 배포하고 이것을 사용하여 장애 복구를 수행할 수 없습니다. 또한 새 vCenter hello에 새 vCenter toohello 기존 구성 서버 및 장애 복구를 추가할 수 없습니다.

#### <a name="original-location-recovery"></a>원래 위치 복구

뒤로 toohello 원본 가상 컴퓨터가 실패 조건 다음 hello 요소가 필요 합니다.
* 가상 컴퓨터 hello vCenter 서버에 의해 관리 되는 경우 다음 hello 마스터 대상 ESX 호스트 있어야 액세스 toohello 가상 컴퓨터의 데이터 저장소입니다.
* Hello 가상 컴퓨터가 ESX 호스트에 있지만 hello 가상 컴퓨터의 하드 디스크 hello 데이터 저장소에 있어야 합니다. 그런 다음 vCenter에 의해 관리 되지 hello 마스터 대상의 호스트에 액세스할 수 있습니다.
* 가상 컴퓨터가 ESX 호스트에 vCenter를 사용 하지 않는 경우 다시 보호 하기 전에 hello 마스터 대상의 hello ESX 호스트의 검색을 완료 해야 합니다. 이는 물리적 서버를 장애 복구하는 경우에도 적용됩니다.
* 뒤로 tooa 가상 저장 영역 네트워크 (vSAN) 또는 있으면 hello 디스크가 이미 연결 된 toohello 온-프레미스 가상 컴퓨터 (RDM) 매핑 원시 장치에 기반 하는 디스크를 실패할 수 있습니다.

#### <a name="alternate-location-recovery"></a>대체 위치 복구
Hello 가상 컴퓨터를 다시 보호 하기 전에 hello 온-프레미스 가상 컴퓨터가 없는 경우 대체 위치 복구 hello 시나리오의 명칭은 합니다. hello 다시 보호 워크플로 hello 온-프레미스 가상 컴퓨터를 다시 만듭니다. 또한 전체 데이터 다운로드가 발생합니다.

* Hello 가상 컴퓨터 복구 된 toohello 수 백 tooan 대체 위치를 실패 하는 경우 동일한 ESX 호스트는 hello에 마스터 대상 서버를 배포 합니다. hello toocreate hello 디스크를 사용 하는 데이터 저장소 됩니다 hello hello 가상 컴퓨터를 다시 보호 때 선택 된 동일한 데이터 저장소입니다.
* 만 tooa 가상 컴퓨터 파일 시스템 (VMFS) 데이터 저장소를 실패할 수 있습니다. vSAN 또는 RDM이 있는 경우 다시 보호 및 장애 복구가 작동하지 않습니다.
* 다시 보호 hello 변경 내용이 있고 바로 뒤에 한 명의 큰 초기 데이터 전송을 작업이 포함 됩니다. 이 프로세스는 온-프레미스 가상 컴퓨터 hello 없기 때문에 존재 합니다. hello 전체 데이터 복제를 다시 toobe가 필요 합니다. 이러한 다시 보호는 원래 위치 복구보다 더 많은 시간이 걸립니다.
* 다시 toovSAN 또는 RDM 기반 디스크를 실패로 지정할 수 없습니다. VMFS 데이터 저장소에는 새로운 VMDK(가상 컴퓨터 디스크)만 만들 수 있습니다.

장애 조치 tooAzure, 물리적 컴퓨터가 실패할 수 있습니다 VMware 가상 컴퓨터 (또한: 참조 tooas P2A2V)로 백업 합니다. 이 흐름 hello 대체 위치 복구에 포함 합니다.

* Windows Server 2008 R2 SP1 물리적 서버 보호 하 고 장애 조치 tooAzure를 다시 장애 수 수 없습니다.
* 하나 이상의 마스터 대상 서버와 hello 필요한 ESX/ESXi 호스트 toowhich toofail 다시 필요 하면 검색할 수 있는지 확인 합니다.

## <a name="have-you-completed-reprotection"></a>다시 보호를 완료했습니까?
계속 진행 하기 전에 완료 hello hello 가상 컴퓨터 복제 상태에 있으며 장애 조치 백 tooan 온-프레미스 사이트를 시작할 수 있도록 단계를 다시 보호 합니다. 자세한 내용은 참조 [어떻게 Azure tooon 온-프레미스에서 tooreprotect](site-recovery-how-to-reprotect.md)합니다.

## <a name="prerequisites"></a>필수 조건

* 장애 복구를 수행할 때 구성 서버가 온-프레미스에 있어야 합니다. 장애 복구 하는 동안 hello 가상 컴퓨터는 hello 구성 서버 데이터베이스에 있어야 합니다. 또는 장애 복구 성공 하지 않습니다. 따라서 서버의 예정된 정기 백업을 수행해야 합니다. Hello로 toorestore hello 서버 해야는 재해 되었으면 toowork 장애 복구에 대 한 동일한 IP 주소입니다.
* 장애 복구를 트리거하기 전에 마스터 대상 서버 hello 스냅숏이 없어야 합니다.

## <a name="steps-toofail-back"></a>단계 toofail 다시

> [!IMPORTANT]
> 장애 복구를 시작 하기 전에 hello 가상 컴퓨터의 다시 보호를 완료 했는지 확인 합니다. hello 가상 컴퓨터는 보호 된 상태에 있어야 하며 해당 상태의 해야 **확인**합니다. tooreprotect hello 가상 컴퓨터를 읽을 [어떻게 tooreprotect](site-recovery-how-to-reprotect.md)합니다.

1. Hello에 복제 된 항목 페이지, hello 가상 컴퓨터를 선택 하 고 마우스 오른쪽 단추 클릭 tooselect **계획 되지 않은 장애 조치**합니다.
2. **확인 장애 조치**hello 장애 조치 방향 (Azure)를 확인 한 다음 장애 조치의 hello toouse 되도록 hello 복구 지점 (최신 또는 일관 된 hello 최신 앱)을 선택 합니다. hello 응용 프로그램 일치 시점 hello 최신 지점 뒤에 시간이 며 일부 데이터 손실이 발생 합니다.
3. 장애 조치 중 사이트 복구는 Azure의 hello 가상 컴퓨터를 종료합니다. 예상 대로 해당 장애 복구 완료 확인 한 후에 Azure의 hello 가상 컴퓨터 종료를 확인할 수 있습니다.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>toowhat 복구 지점 백 hello 가상 컴퓨터 실패할 수 있습니다.

장애 복구 하는 동안 두 옵션 toofail 백 hello 가상 컴퓨터/복구 계획이 있는 합니다.

최신 처리 hello 지점 시간을 선택 하면 모든 가상 컴퓨터는 장애 조치 될 tootheir 사용 가능한 최신 시점 시간. Hello 복구 계획 내에서 복제 그룹 인 경우 다음 hello 복제 그룹의 각 가상 컴퓨터 장애 조치 됩니다 tooits 독립 최신 지점 시간.

가상 컴퓨터에 복구 지점이 하나 이상 있어야 가상 컴퓨터를 장애 복구할 수 있습니다. 모든 가상 컴퓨터에 복구 지점이 하나 이상 있어야 복구 계획을 장애 복구할 수 있습니다.

> [!NOTE]
> 최신 복구 지점은 크래시 일관성 복구 지점입니다.

Hello 응용 프로그램 일치 복구 지점을 선택 하는 경우 단일 가상 컴퓨터 장애 복구 tooits 최신 사용 가능한 응용 프로그램 일치 복구 지점을 복구 됩니다. 복제 그룹에는 복구 계획의 hello 경우에서 각 복제 그룹 tooits 공통 사용 가능한 복구 지점을 복구 됩니다.
응용 프로그램 일치 복구 지점의 경우 복구가 지연될 수 있고 데이터가 손실될 수 있습니다.

### <a name="what-happens-toovmware-tools-post-failback"></a>TooVMware 도구 게시 장애 복구 어떻게 되나요?

장애 조치 tooAzure 중 hello VMware 도구 hello Azure 가상 컴퓨터에서 실행할 수 없습니다. Windows 가상 컴퓨터의 경우 ASR 장애 조치 중 hello VMware tools를 해제합니다. Linux 가상 컴퓨터의 경우 ASR 장애 조치 중 hello VMware tools를 제거합니다.

Hello Windows 가상 컴퓨터의 장애 복구 하는 동안 hello VMware 도구는 장애 복구 시 다시 사용할 수 있습니다. 마찬가지로, linux 가상 컴퓨터에 대 한 hello VMware 도구는 컴퓨터에 다시 hello 장애 복구 중입니다.

## <a name="next-steps"></a>다음 단계

Toocommit 장애 복구를 완료 한 후 해야 Azure의 가상 컴퓨터를 복구 하는 hello 가상 컴퓨터 tooensure 삭제 됩니다.

### <a name="commit"></a>커밋
커밋 장애 조치 Azure에서 가상 컴퓨터는 필요한 tooremove hello입니다.
Hello 보호 된 항목을 마우스 오른쪽 단추로 누른 **커밋**합니다. 작업은 hello 장애 조치 Azure의 가상 컴퓨터를 제거 합니다.

### <a name="reprotect-from-on-premises-tooazure"></a>온-프레미스 tooAzure에서 다시 보호

커밋 완료 된 후 가상 컴퓨터가 hello 온-프레미스 사이트에 다시 이지만 보호할 수 없습니다. 다시, toostart tooreplicate tooAzure 다음 hello지 않습니다.

1. **자격 증명 모음** > **설정** > **복제 항목**, 선택 hello 다시 실패 하 고 클릭 한 다음 가상 컴퓨터를  **다시 보호**합니다.
2. 사용 되는 toobe toosend 데이터 백 tooAzure 해야 하는 hello 프로세스 서버 hello 값을 제공 합니다.
3. 클릭 **확인** toobegin hello 다시 보호 작업 합니다.

> [!NOTE]
> 온-프레미스 가상 컴퓨터를 부팅 한 후 시간이 걸리는 hello 에이전트에 대 한 tooregister 백 toohello 구성 서버 (위쪽 too15 분)입니다. 이 시간 동안 실패 하 고 해당 hello 에이전트를 알리는 오류 메시지가 설치 되지 않은 반환을 다시 보호 하십시오. 몇 분 동안 기다린 다음 다시 보호를 다시 시도합니다.

Hello를 다시 보호 한 후 작업을 완료 백 tooAzure hello 가상 컴퓨터가 복제 및 장애 조치를 수행할 수 있습니다.

## <a name="common-issues"></a>일반적인 문제
장애 복구를 수행 하기 전에 해당 hello vCenter가 연결 된 상태에 있는지 확인 합니다. 그렇지 않은 경우 디스크의 연결을 끊고 다시 toohello 첨부 하 가상 컴퓨터가 실패 합니다.
