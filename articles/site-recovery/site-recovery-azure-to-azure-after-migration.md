---
title: "사이트 복구를 사용 하 여 tooAzure 마이그레이션 후 Azure 지역 간 재해 복구를 aaaPrepare 컴퓨터 tooset | Microsoft Docs"
description: "이 문서에서는 tooprepare Azure Site Recovery를 사용 하 여 tooAzure 마이그레이션 후 Azure 지역 간 재해 복구를 tooset 컴퓨터 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Azure Site Recovery를 사용 하 여 Azure Vm tooanother 지역 마이그레이션 tooAzure 후 복제

>[!NOTE]
> Azure VM(가상 컴퓨터)에 대한 Azure Site Recovery 복제는 현재 미리 보기로 제공됩니다.

## <a name="overview"></a>개요

이 문서에서는 이러한 컴퓨터를 마이그레이션한 후 온-프레미스 환경 tooAzure에서 Azure Site Recovery를 사용 하 여 두 Azure 지역 간 복제에 대 한 Azure 가상 컴퓨터를 준비 합니다.

## <a name="disaster-recovery-and-compliance"></a>재해 복구 및 규정 준수
오늘날, 점점 더 많은 기업에서는 해당 작업 tooAzure 이동 하는 합니다. 기업에서는 업무상 중요 한 온-프레미스 프로덕션 이동와 이러한 작업에 대 한 재해 복구를 설정 하는 작업 tooAzure는 규정 준수 및 toosafeguard Azure 지역에서 중단에 대해 필수입니다.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>마이그레이션된 컴퓨터의 복제를 준비하기 위한 단계
tooprepare 마이그레이션된 복제 tooanother Azure 지역을 설정 하기 위한 컴퓨터.

1. 마이그레이션을 완료하려면
2. Hello 필요한 경우 Azure 에이전트를 설치 합니다.
3. Hello 모바일 서비스를 제거 합니다.  
4. Hello VM을 다시 시작 합니다.

이러한 단계는 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>1 단계: Hyper-v Vm, VMware Vm 및 Azure Vm에서 toorun 물리적 서버에서 실행 되는 작업 마이그레이션

tooset 복제 및 프로그램 온-프레미스 Hyper-v, VMware 및 실제 작업 부하 tooAzure hello 단계 수행 hello에 마이그레이션할 [Azure Site Recovery와 Azure 지역 간에 마이그레이션할 Azure IaaS 가상 컴퓨터](site-recovery-migrate-to-azure.md) 문서. 

마이그레이션 후 toocommit 필요 하지 않거나 장애 조치를 삭제 합니다. 키를 누릅니다. 대신, hello 선택 **마이그레이션을 완료** 옵션 toomigrate 하려는 각 컴퓨터에 대해:
1. **복제 항목**hello VM을 마우스 오른쪽 단추로 클릭 하 고 클릭 **마이그레이션을 완료**합니다. 클릭 **확인** toocomplete hello 단계입니다. Hello 전체 마이그레이션 작업을 모니터링 하 여 hello VM 속성에서 진행률을 추적할 수 있습니다 **사이트 복구 작업이**합니다.
2. hello **마이그레이션을 완료** 동작 hello 마이그레이션 프로세스를 완료 hello 컴퓨터에 대 한 복제를 제거 하 고 hello 컴퓨터에 대 한 사이트 복구 청구를 중지 합니다.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>2 단계: hello 가상 컴퓨터에 hello Azure VM 에이전트를 설치 합니다.
Azure hello [VM 에이전트](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) hello 사이트 복구 확장 toowork 및 toohelp hello VM 보호에 대 한 hello 가상 컴퓨터에 설치 해야 합니다.

>[!IMPORTANT]
>Windows 가상 컴퓨터에 9.7.0.0, 버전부터 hello 모바일 서비스 설치 관리자도 hello 최신 사용 가능한 Azure VM 에이전트를 설치 합니다. Hello 가상 컴퓨터 마이그레이션에 에이전트 설치 hello 사이트 복구 확장명을 포함 하는 모든 VM 확장을 사용 하기 위한 필수 구성 요소를 충족 합니다. hello 모바일 서비스 hello에 설치 된 컴퓨터를 마이그레이션할 경우에 수동으로 설치 하는 hello Azure VM 에이전트 요구 toobe은 9.6 또는 이전 버전입니다.

hello 다음 표에서 hello VM 에이전트를 설치 하 고 설치 된 유효성을 검사 하는 방법에 대 한 추가 정보:

| **작업** | **Windows** | **Linux** |
| --- | --- | --- |
| Hello VM 에이전트 설치 |다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야합니다. |Hello 최신 설치 [Linux 에이전트](../virtual-machines/linux/agent-user-guide.md)합니다. 관리자 권한 toocomplete hello 설치를 해야합니다. 배포 리포지토리에서 hello 에이전트를 설치 하는 것이 좋습니다. 우리 *권장 하지는 않습니다* GitHub에서 직접 hello Linux VM 에이전트를 설치 합니다.  |
| Hello VM 에이전트 설치 유효성 검사 |1. Hello Azure VM에서에서 toohello C:\WindowsAzure\Packages 폴더를 찾습니다. 표시 되어야 hello WaAppAgent.exe 파일입니다. <br>2. Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 선택한 후 hello **세부 정보** 탭 hello **제품 버전** 필드 2.6.1198.718 이루어져야 합니다. 이상. |해당 없음 |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>3 단계: 제거 hello hello에서 모바일 서비스 마이그레이션된 가상 컴퓨터

온-프레미스 VMware 컴퓨터 또는 물리적 Windows/Linux 서버를 마이그레이션하는 경우 hello 마이그레이션된 가상 컴퓨터에서 hello 모바일 서비스가 제거 toomanually 해야 합니다.

>[!IMPORTANT]
>이 단계는 마이그레이션된 tooAzure Hyper-v Vm에 대 한 필요 하지 않습니다.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Windows Server VM에서 모바일 서비스 hello 제거
Hello 메서드 toouninstall hello 모바일 서비스는 Windows Server 컴퓨터에서 다음 중 하나를 사용 합니다.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Windows UI hello를 사용 하 여 제거
1. Hello 제어판에서에서 선택 **프로그램**합니다.
2. **Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버**를 선택한 다음 **제거**를 선택합니다.

##### <a name="uninstall-at-a-command-prompt"></a>명령 프롬프트에서 제거
1. 관리자로 명령 프롬프트 창을 엽니다.
2. toouninstall hello 모바일 서비스를 hello 다음 명령을 실행 합니다.

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Linux 컴퓨터에서 hello 모바일 서비스 제거
1. Linux 서버에서 **루트** 사용자로 로그인합니다.
2. 종료, 너무/사용자/로컬/ASR을 이동 합니다.
3. toouninstall hello 모바일 서비스를 hello 다음 명령을 실행 합니다.

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>4 단계: hello VM을 다시 시작

Hello 모바일 서비스를 제거한 후 다시 시작 hello VM 하기 전에 Azure 지역 복제 tooanother를 설정 합니다.


## <a name="next-steps"></a>다음 단계
- [Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.
- [Azure Virtual Machines 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md)에 대해 자세히 알아봅니다.
