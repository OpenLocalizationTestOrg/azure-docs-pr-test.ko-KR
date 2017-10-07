---
title: "VMM tooa 보조 사이트 (Azure 클래식)에서 Hyper-v Vm aaaReplicate | Microsoft Docs"
description: "이 문서에서는 tooreplicate VMM에서 Hyper-v Vm 클라우드를 Azure Site Recovery와 보조 VMM 사이트 tooa 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>VMM 클라우드 tooa 보조 VMM 사이트에서 Hyper-v 가상 컴퓨터 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmm-to-vmm.md)
> * [클래식 포털](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

hello Azure Site Recovery 서비스 tooyour 비즈니스 연속성 및 조정 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 재해 복구 (BCDR) 전략에 기여합니다. 복제 된 tooAzure 또는 tooa 보조 온-프레미스 데이터 센터 컴퓨터 수 있습니다. 빠른 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)

## <a name="overview"></a>개요
이 문서에서는 hyper-v tooreplicate Hyper-v 가상 컴퓨터에서 Azure Site Recovery를 사용 하 여 VMM 클라우드에 toosecondary VMM 사이트에서 관리 되는 서버를 호스트 하는 방법을 설명 합니다.

hello 문서 필수 구성 요소에 포함 되어, 소스에서 Azure Site Recovery Provider hello 어떻게 tooset 사이트 복구 자격 증명 모음을 설치 하 고 대상 VMM 서버 보여줍니다, hello 서버 hello 자격 증명 모음에 등록, VMM 클라우드에 대 한 보호 설정을 구성 및 사용 하도록 설정 Hyper-v Vm에 대 한 보호를 제공 합니다. 모든 것이 예상 대로 작동 하는지 테스트 hello 장애 조치 toomake까지 완료 합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="architecture"></a>아키텍처
아래 hello 그림은 hello 다양 한 통신 채널 및 오케스트레이션 및 복제에 대 한 Azure Site Recovery에 의해 사용 되는 포트를 보여 줍니다.

![E2E 토폴로지](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>시작하기 전에
다음 필수 조건이 충족되었는지 확인합니다.

| **필수 구성 요소** | **세부 정보** |
| --- | --- |
| **Azure** |[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. [자세히 알아봅니다](https://azure.microsoft.com/pricing/details/site-recovery/) . |
| **VMM** |하나 이상의 VMM 서버가 필요합니다.<br/><br/>VMM 서버 hello 해야 이상을 실행 하 고 hello 최신 누적 업데이트가 설치 된 System Center 2012 SP1.<br/><br/>단일 VMM 서버와 보호를 tooset 원하는 hello 서버에 구성 된 두 개 이상의 클라우드가 있어야 합니다.<br/><br/>각 서버에 구성 된 클라우드가 하나 이상 있어야 VMM 서버 두 개 toodeploy 보호 하려는 경우 hello tooprotect, 원하는 hello 보조 VMM 서버에 구성 된 클라우드가 하나는 기본 VMM 서버에 원하는 toouse 보호 및 복구에 대 한<br/><br/>모든 VMM 클라우드의 hello Hyper-v 기능 프로필 설정 있어야 합니다.<br/><br/>원하는 tooprotect hello 원본 클라우드는 하나 이상의 VMM 호스트 그룹을 포함 해야 합니다. |
| **Hyper-V** |Hello 기본 및 보조 VMM 호스트 그룹에서 하나 이상의 Hyper-v 호스트 서버 및 각 Hyper-v 호스트 서버에서 하나 이상의 가상 컴퓨터 필요.<br/><br/>hello 호스트 및 대상 Hyper-v 서버 해야 이상을 실행 하 고 hello Hyper-v 역할과 Windows Server 2012 및 최신 업데이트가 설치 되어 hello 있어야 합니다.<br/><br/>Vm을 포함 하는 모든 Hyper-v 서버 tooprotect VMM 클라우드에 있어야 두는 것이 좋습니다.<br/><br/>클러스터에서 Hyper-V를 실행하고 있다면 고정 IP 주소 기반 클러스터가 있는 경우 클러스터 broker가 자동으로 만들어지지 않습니다. Tooconfigure hello 클러스터 브로커를 수동으로 필요합니다. [자세히 알아봅니다](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) 를 확인해 보세요. |
| **네트워크 매핑** |네트워크 매핑 toomake 장애 조치 후 복제 된 가상 컴퓨터는 보조 Hyper-v 호스트 서버에 최적으로 배치 하 고 tooappropriate VM 네트워크를 연결할 수 있는지를 구성할 수 있습니다. 네트워크 매핑을 구성 하지 않으면, 복제본 Vm 장애 조치 후 연결 된 tooany 네트워크 수 없습니다.<br/><br/>배포 하는 동안 네트워크 매핑을 tooset hello 가상 컴퓨터 hello 원본 Hyper-v 호스트 서버에 연결 된 tooa VMM VM 네트워크 인지 확인 합니다. 해당 네트워크에는 연결 된 tooa hello 클라우드.와 연결 된 논리 네트워크를 사용 해야 합니다. < b r /<br/>hello 대상 클라우드 복구에 사용 된 hello 보조 VMM 서버에 해당 VM 네트워크를 구성 해야 합니다. 하며 차례로 연결 된 tooa hello 대상 클라우드와 연결 된 논리 네트워크에 해당 해야 합니다. |
| **저장소 매핑** |기본적으로 원본 Hyper-v 호스트 서버 tooa 대상 Hyper-v 호스트 서버에, 가상 컴퓨터를 복제 하면 복제 된 데이터는 Hyper-v 관리자에서 hello 대상 Hyper-v 호스트에 대해 지정 된 hello 기본 위치에 저장 됩니다. 복제된 데이터가 저장된 위치에 대해 더 제어하려면 저장소 매핑을 구성할 수 있습니다<br/><br/> tooconfigure 저장소 매핑을 hello 소스 저장소 분류를 tooset 및 해야 배포를 시작 하기 전에 대상 VMM 서버입니다. |

## <a name="step-1-create-a-site-recovery-vault"></a>1단계: 사이트 복구 자격 증명 모음 만들기
1. Toohello 로그인 [관리 포털](https://portal.azure.com) tooregister hello VMM 서버에서 원하는 합니다.
2. **Data Services** > **Recovery Services**를 확장하고 **Site Recovery 자격 증명 모음**을 클릭합니다.
3. **새로 만들기** > **빠른 생성**을 클릭합니다.
4. **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.
5. **지역** 선택 hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 지원 toocheck 지역에서 지역 가용성 참조 [Azure 사이트 복구 가격 정보](http://go.microsoft.com/fwlink/?LinkId=389880)합니다.
6. **자격 증명 모음 만들기**를 클릭합니다.

    ![자격 증명 모음 만들기](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

체크 인 hello 상태 표시줄 해당 hello 자격 증명 모음을 만들었습니다. hello 자격 증명 모음으로 나열 됩니다 **활성** hello 기본 복구 서비스 페이지에 있습니다.

## <a name="step-2-generate-a-vault-registration-key"></a>2단계: 자격 증명 모음 등록 키 생성
Hello 자격 증명 모음에 등록 키를 생성 합니다. Hello Azure Site Recovery Provider를 다운로드 하 고 hello VMM 서버에 설치 후에 hello 자격 증명 모음에이 키 tooregister hello VMM 서버를 사용 합니다.

1. Hello에 **복구 서비스** 페이지 hello 자격 증명 모음 tooopen hello 빠른 시작 페이지를 클릭 합니다. 빠른 시작 언제 든 지 hello 아이콘을 사용 하 여 열 수도 있습니다.

    ![빠른 시작 아이콘](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Hello 드롭다운 목록에서 선택 **두 온-프레미스 VMM 사이트 간**합니다.
3. **VMM 서버 준비**에서 **등록 키 파일 생성**을 클릭합니다. hello 키 파일이 자동으로 생성 됩니다 및은 생성 된 후 5 일 동안 유효 합니다. Azure 포털 hello hello VMM 서버에서 액세스 하지 하려면 toocopy이 파일 toohello 서버가 필요 합니다.

    ![등록 키](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>3 단계: hello Azure Site Recovery Provider 설치
1. Hello에 **빠른 시작** 페이지 **준비 VMM 서버**, 클릭 **Microsoft Azure 사이트 복구 공급자 다운로드 VMM 서버에 설치에 대 한** tooobtain hello 최신 버전 hello 공급자 설치 파일의 버전입니다.
2. Hello 원본 VMM 서버에서이 파일을 실행 합니다.

   > [!NOTE]
   > VMM 클러스터에 배포 되 고 처음으로 hello에 대 한 hello 공급자를 설치 하는 경우에 액티브 노드에 설치 및 hello 자격 증명 모음에 hello 설치 tooregister hello VMM 서버를 완료 합니다. 그런 다음 hello 공급자에 설치 hello 다른 노드가 있습니다. 모든 노드에서 tooupgrade 필요 하면 모두는 공급자가 될 hello를 업그레이드 하는 경우 실행 hello 동일한 공급자 버전이 참고 합니다.
   >
   >
3. hello 설치 관리자가 몇 **pre-requirements Check** 및 요청 권한 toostop hello VMM 서비스 toobegin 공급자를 설치 합니다. 자동으로 설치가 완료 되 면 hello VMM 서비스에 다시 시작 됩니다. 에 설치 하는 경우 VMM 클러스터 수 toostop hello 클러스터 역할을 라는 메시지가 나타납니다.
4. **Microsoft 업데이트** 에서 업데이트를 선택할 수 있습니다. 이 설정을 사용 하 여 tooyour Microsoft Update 정책에 따라 사용 가능한 공급자 업데이트가 설치 됩니다.

    ![Microsoft 업데이트](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. hello 설치 위치는 너무 설정**<SystemDrive>files\microsoft System Center 2012 R2\Virtual Machine Manager\bin**합니다. Hello 공급자를 설치 하는 설치 단추 toostart hello 클릭 합니다.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. 공급자가 설치 되어 hello 후 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. **자격 증명 모음 이름**, hello는 hello 서버를 등록할 자격 증명 모음의 hello 이름이 유효한 지 확인 합니다. *다음*을 누릅니다.

    ![서버 등록](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. **인터넷 연결** 지정 방법을 hello VMM에서 실행 중인 공급자를 hello 서버 toohello 인터넷 연결 합니다. 선택 **기존 프록시 설정 사용 하 여 연결** toouse hello 기본 인터넷 연결 설정을 hello 서버에 구성 합니다.

    ![인터넷 설정](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Toouse 하려는 경우 사용자 지정 프록시 설정 해야이 hello 공급자를 설치 하기 전에. 사용자 지정 프록시 설정을 구성할 때 toocheck hello 프록시 연결 테스트에 실행 됩니다.
   * 사용자 지정 프록시를 사용 하 여 수행 하거나 기본 프록시에 인증이 필요한 경우 hello 프록시 주소와 포트를 포함 한 tooenter hello 프록시 정보를 해야 합니다.
   * VMM 서버 hello 및 hello hyper-v 호스트에서 액세스할 수 있어야 다음 url
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * 에 설명 된 IP 주소를 hello [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS (443) 프로토콜입니다. Hello 계획 toouse 및 미국 서 부의 Azure 지역의 IP 범위 toowhite 나열 해야 합니다.
   * 자동으로 지정 하는 hello를 사용 하 여 VMM RunAs 계정 (DRAProxyAccount) 만들어집니다는 사용자 지정 프록시를 사용 하는 경우 프록시 자격 증명입니다. 이 계정을 올바르게 인증할 수 있도록 hello 프록시 서버를 구성 합니다. VMM RunAs 계정 설정은 hello hello VMM 콘솔에서 수정할 수 있습니다. toodo이, 열기 hello **설정** 작업 영역에서 확장 **보안**, 클릭 **실행 계정**, 한 다음 DRAProxyAccount에 대 한 hello 암호를 수정 합니다. 이 설정은 적용 됩니다에 toorestart hello VMM 서비스를 필요 합니다.
9. **등록 키**선택, hello 키를 Azure Site Recovery에서 다운로드 한 toohello VMM 서버에 복사 합니다.
10. hello 암호화 설정은 VMM 클라우드에 tooAzure의 Hyper-v Vm을 복제 하는 경우에 사용 됩니다. Tooa 보조 사이트를 복제 하는 사용 되지 않습니다.
11. **서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다. 클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.
12. **클라우드 메타 데이터 동기화** hello 자격 증명 모음과 hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용할지 선택 합니다. 이 작업은 toohappen 각 서버에서 한 번만 필요합니다. Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다.
13. 클릭 **다음** toocomplete hello 프로세스입니다. 등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다. hello 서버에 표시 되 **VMM 서버** > **서버** hello 자격 증명 모음에 있습니다.

    ![서버](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>명령줄 설치
Azure Site Recovery Provider hello hello 명령줄에서 설치할 수도 있습니다. 이 메서드는 Server CORE에 대 한 Windows Server 2012 r 2에서 사용 되는 tooinstall hello 공급자 수 있습니다.

1. Hello 공급자 설치 파일과 등록 키 tooa 폴더를 다운로드 합니다. 예: C:\ASR.
2. Hello System Center Virtual Machine Manager 서비스를 중지 합니다.
3. Hello 공급자 설치 관리자와 명령 프롬프트에서 다음이 명령을 실행 하 여 추출 **관리자** 권한:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. 실행 하 여 hello 공급자를 설치 합니다.

        C:\ASR> setupdr.exe /i
5. 실행 하 여 hello 공급자를 등록 합니다.

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Hello 매개 변수는:

* **/ 자격 증명**:는 hello 등록 키 파일의 위치를 가리키는 hello 위치를 지정 하는 필수 매개 변수  
* **/ FriendlyName**: hello Azure Site Recovery 포털에 표시 되는 hello Hyper-v 호스트 서버 hello 이름에 대 한 필수 매개 변수입니다.
* **/ EncryptionEnabled**: 해야 하는 hello VMM tooAzure 시나리오에만 toouse에서 Azure의 가상 컴퓨터의 암호화 해야 할 경우 선택적 매개 변수입니다. Hello 파일의 해당 hello 이름을 확인 하십시오가 제공 하는 **.pfx** 확장 합니다.
* **/proxyAddress**: hello hello 프록시 서버의 주소를 지정 하는 선택적 매개 변수입니다.
* **/proxyport**: hello hello 프록시 서버의 포트를 지정 하는 선택적 매개 변수입니다.
* **/proxyUsername**: (프록시에 인증이 필요) 하는 경우 hello 프록시 사용자 이름을 지정 하는 선택적 매개 변수입니다.
* **/proxyPassword**:를 지정 하는 선택적 매개 변수 (프록시에 인증이 필요) 하는 경우 프록시 서버 hello에 인증 하기 위해 암호를 hello 합니다.  

## <a name="step-4-configure-cloud-protection-settings"></a>4단계: 클라우드 보호 설정 구성
VMM 서버가 등록되면 클라우드 보호 설정을 구성할 수 있습니다. Hello 옵션을 사용 하는 경우 **hello 자격 증명 모음과 클라우드 데이터를 동기화** hello VMM 서버의 모든 클라우드에 hello에 나타납니다. 하므로 hello 공급자를 설치할 때 **보호 된 항목** hello 자격 증명 모음에는 탭 합니다. 하면 그렇지 않은 경우 hello에서 특정 클라우드를 Azure Site Recovery와 동기화 **일반** hello VMM 콘솔의 hello 클라우드 속성 페이지의 탭 합니다.

![게시된 클라우드](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Hello 빠른 시작 페이지에서 클릭 **VMM 클라우드에 대 한 보호 설정**합니다.
2. Hello에 **VMM 클라우드에** 탭을 선택 hello 클라우드 tooconfigure 원하고 toohello 이동 **구성** 탭 합니다.
3. **대상**에서 **VMM**을 선택합니다.
4. **대상 위치**, 선택 hello toouse 복구에 대 한 원하는 hello 클라우드를 관리 하는 온사이트 VMM 서버입니다.
5. **대상 클라우드**, toouse hello 원본 클라우드에서 가상 컴퓨터의 장애 조치에 대해 원하는 hello 대상 클라우드를 선택 합니다. 다음 사항에 유의하세요.

   * Hello 가상 컴퓨터를 보호 해 줄에 대 한 복구 요구 사항을 충족 하는 대상 클라우드를 선택 하는 것이 좋습니다.
   * 클라우드 tooa 단일 클라우드 쌍에만 속할 수 있습니다-기본 또는 대상 클라우드입니다.
6. **복사 빈도**에서 원본 위치와 대상 위치 간에 데이터를 동기화해야 하는 빈도를 지정합니다. Note hello Hyper-v 호스트는 Windows Server 2012 r 2를 실행 하는 경우이 설정은 적용만 됩니다. 다른 서버의 경우에는 기본 설정인 5분이 사용됩니다.
7. **추가 복구 지점**, toocreate 추가 점을 할지 여부를 지정 합니다. hello 기본 0 값 hello 최신 복구 지점만 주 가상 컴퓨터에 대 한 복제본 호스트 서버에 저장 되어 있음을 나타냅니다. 참고 여러 복구 지점을 사용 하려면 각 복구 지점에 저장 된 hello 스냅숏을 위한 추가 저장소가 필요 합니다. 기본적으로 복구 지점은 매시간마다 만들어지므로 각 복구 지점에는 1시간 동안의 데이터가 포함됩니다. hello VMM 콘솔에 hello 가상 컴퓨터에 할당 하는 hello 복구 지점 값은 hello Azure Site Recovery 콘솔에 할당 하는 hello 값 보다 작을 수 없습니다.
8. **응용 프로그램 일치 스냅숏 빈도**, 빈도 지정 toocreate 응용 프로그램에 일관 된 스냅숏의 합니다. Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다. 응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다. 응용 프로그램 일치 스냅숏을 사용할 경우 영향을 주므로 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능을 확인 합니다. 설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.

    ![보호 설정 구성](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. **데이터 전송 압축**에서 전송되는 복제된 데이터를 압축할지 여부를 지정합니다.
10. **인증**, hello 기본 및 복구 Hyper-v 호스트 서버 간의 트래픽을 인증 하는 방법을 지정 합니다. 작동하는 Kerberos 환경이 구성되어 있지 않으면 HTTPS를 선택합니다. Azure Site Recovery가 HTTPS 인증을 위한 인증서를 자동으로 구성합니다. 수동으로 구성할 필요가 없습니다. Kerberos를 선택 하는 경우 Kerberos 티켓이 hello 호스트 서버의 상호 인증에 사용 됩니다. 기본적으로 포트 8083 및 8084 (인증서용) hello Hyper-v 호스트 서버에 Windows 방화벽 hello에 열 수는 있습니다. 이 설정은 Windows Server 2012 R2에서 실행 중인 Hyper-V 호스트 서버와만 관련이 있습니다.
11. **포트**, hello hello 소스에 포트 번호를 수정 하 고 대상으로 복제 트래픽에 대 한 호스트 컴퓨터가 수신 대기 합니다. 예를 들어 tooapply 서비스 품질 (QoS) 네트워크 대역폭 복제 트래픽을 제한 하려는 경우 hello 설정을 수정할 수 있습니다. Hello 포트가 다른 응용 프로그램에서 사용 되지를 hello 방화벽 설정에서 열려 있는지 확인 합니다.
12. **복제 방법**를 어떻게 hello 소스 tootarget 위치에서 데이터의 초기 복제가 처리 되는 지정, 정기 복제가 시작 하기 전에:

    * **네트워크를 통해**-걸리고 리소스를 많이 사용 될 수 hello 네트워크를 통해 데이터를 복사 합니다. Hello 클라우드 상대적으로 작은 가상 하드 디스크가 있는 가상 컴퓨터를 포함 하 고 hello 기본 사이트와 넓은 광대역 연결을 통해 연결 된 toohello 보조 사이트인 경우이 옵션을 사용 하는 것이 좋습니다. Hello 복사본을 즉시 시작 하거나 시간을 선택 해야 지정할 수 있습니다. 네트워크 복제를 사용하는 경우 사용률이 낮은 시간에 예약하는 것이 좋습니다.
    * **오프 라인**-이 방법은 지정 외부 미디어를 사용 하 여 hello 초기 복제가 수행 됩니다. 네트워크 성능에서 또는 지리적으로 멀리 떨어진 위치에 대 한 tooavoid 성능 저하를 원하는 경우에 유용 합니다. toouse hello 원본 클라우드에서 및 hello 대상 클라우드의 가져오기 위치 hello hello 내보내기 위치를 지정 하는이 방법입니다. 가상 컴퓨터에 대 한 보호를 사용 하도록 설정 하면 hello 가상 하드 디스크가 복사 toohello 지정 된 내보내기 위치 합니다. 하드 디스크 toohello 대상 사이트에 보내고 toohello 가져오기 위치를 복사 합니다. hello 시스템 복사본 hello는 toohello 복제본 가상 컴퓨터 정보를 가져옵니다.
13. 선택 **복제 가상 컴퓨터 삭제** hello를 선택 하 여 hello 가상 컴퓨터 보호를 중지 하는 경우 복제 가상 컴퓨터를 hello toospecify 삭제 되도록 **hello 가상 컴퓨터에 대 한 보호를 삭제 합니다.**  hello 클라우드 속성의 hello 가상 컴퓨터 탭에서 옵션입니다. 이 설정을 사용 하 고, 사용 하지 않도록 설정 하면 보호 hello 가상 컴퓨터가 Azure Site Recovery에서 제거 되, hello 가상 컴퓨터에 대 한 hello 사이트 복구 설정이 hello VMM 콘솔에서 제거 됩니다 및 hello 복제본이 삭제 됩니다.

    ![보호 설정 구성](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Hello 설정을 저장 한 후 작업이 만들어지고 hello에서 모니터링할 수 **작업** 탭 합니다. 복제에 대 한 VMM 원본 클라우드에 hello에서 모든 Hyper-v 호스트 서버를 구성 됩니다. Hello에 클라우드 설정을 수정할 수 있는 **구성** 탭 합니다. Toomodify hello 대상 위치 또는 대상 클라우드를 원하는 경우 hello 클라우드 구성을 제거한 후 hello 클라우드를 다시 구성 해야 합니다.

### <a name="prepare-for-offline-initial-replication"></a>오프라인 초기 복제 준비
오프 라인 초기 복제 작업 tooprepare 다음 toodo hello이 필요 합니다.

* Hello 원본 서버에 있는 hello에서 데이터 내보내기가 수행 될 경로 위치를 지정 합니다. Hello 내보내기 경로에 VMM 서비스 toohello NTFS 및 공유 사용 권한에 대 한 모든 권한을 할당 합니다. Hello 대상 서버의 hello 데이터를 가져올 경로 위치를 실시할를 지정 합니다. Hello이 가져오기 경로에 동일한 권한을 할당 합니다.
* 경우 hello 가져오기 또는 내보내기 경로가 공유 된, hello 원격 컴퓨터에서 hello VMM 서비스 계정에 대 한 관리자, Power User, Print Operator 또는 Server Operator 그룹 멤버 자격 할당 공유 하는 hello에 있습니다.
* 모든 실행 계정 tooadd 호스트를 사용 하는 경우 hello에 가져오기 및 내보내기 경로, 할당 읽기 및 쓰기 권한이 toohello 실행 계정을 VMM에서.
* 공유 내보내기 및 가져오기 hello Hyper-v에서 루프백 구성을 지원 되지 않으므로 Hyper-v 호스트 서버로 사용 되는 모든 컴퓨터에 배치할 수 해야 합니다.
* 원하는 tooprotect, 가상 컴퓨터가 포함 된 각 Hyper-v 호스트 서버에서 Active Directory에서 사용 하도록 설정 하 고 제한 된 위임 tootrust hello 원격 컴퓨터는 hello 가져오기 및 내보내기에 경로 다음과 같이 구성 합니다.
  1. Hello 도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**합니다.
  2. Hello 콘솔 트리에서 클릭 **DomainName** > **컴퓨터**합니다.
  3. 마우스 오른쪽 단추로 클릭 hello Hyper-v 호스트 서버 이름 > **속성**합니다.
  4. Hello에 **위임** 탭 클릭 T**이 컴퓨터에 위임 toospecified 서비스만 rust**합니다.
  5. **모든 인증 프로토콜 사용**을 클릭합니다.
  6. **추가** > **사용자 및 컴퓨터**에 문의하세요.
  7. Hello 내보내기 경로 호스트 하는 hello 컴퓨터의 형식 hello 이름 > **확인**합니다. Hello 사용 가능한 서비스 목록에서 hello CTRL 키를 누른 채 클릭 **cifs** > **확인**합니다. Hello 컴퓨터의 이름을 hello에 대 한 해당 호스트 hello 가져오기 경로 반복 합니다. 필요에 따라 추가 Hyper-V 호스트 서버에 대해 반복합니다.

## <a name="step-5-configure-network-mapping"></a>5단계: 네트워크 매핑 구성
1. Hello 빠른 시작 페이지에서 클릭 **네트워크 매핑**합니다.
2. Toomap 네트워크를 선택 하 고 있는 다음 네트워크가 매핑될 대상 VMM 서버 toowhich hello hello hello 원본 VMM 서버를 선택 합니다. 원본 네트워크 및 연결 된 대상 네트워크의 hello 목록이 표시 됩니다. 현재 매핑되지 않은 네트워크에 대해서는 빈 값이 표시됩니다.
3. **원본 네트워크** > **매핑**에서 네트워크를 선택합니다. hello 서비스는 hello hello 대상 서버의 VM 네트워크를 검색 하 고 표시 합니다. Hello 정보 아이콘 다음 toohello 소스 및 대상 네트워크 이름 tooview hello에 대 한 서브넷 각 네트워크를 클릭 합니다.

    ![네트워크 매핑 구성](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Hello 대화 상자에서 hello 대상 VMM 서버에서 hello VM 네트워크 중 하나를 선택 합니다.

    ![대상 네트워크 선택](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. 대상 네트워크를 선택 하면 hello hello 원본 네트워크를 사용 하는 보호 된 클라우드가 표시 됩니다. 보호에 사용 되는 hello 클라우드와 연결 된 사용 가능한 대상 네트워크도 표시 됩니다. 보호를 위해 사용 하는 사용 가능한 tooall hello 클라우드에 있는 대상 네트워크를 선택 하는 것이 좋습니다. 또는 toohello VMM 서버를 이동 하 고 hello 클라우드 속성 tooadd hello 논리 네트워크 toochoose 원하는 toohello vm 네트워크에 해당 수정할 수도 있습니다.
6. Hello 확인 표시가 toocomplete hello 매핑 프로세스를 클릭 합니다. 작업이 tootrack hello 매핑 진행률을 시작 합니다. Hello에서 볼 수 있습니다 **작업** 탭 합니다.

## <a name="step-6-configure-storage-mapping"></a>6단계: 저장소 매핑 구성
기본적으로 원본 Hyper-v 호스트 서버 tooa 대상 Hyper-v 호스트 서버에, 가상 컴퓨터를 복제 하면 복제 된 데이터는 Hyper-v 관리자에서 hello 대상 Hyper-v 호스트에 대해 지정 된 hello 기본 위치에 저장 됩니다. 복제된 데이터가 저장되는 위치를 제어하려는 경우 다음과 같이 저장소 매핑을 구성할 수 있습니다.

1. 두 hello 소스에서 저장소 분류를 정의 및 대상 VMM 서버입니다. [자세히 알아봅니다](https://technet.microsoft.com/library/gg610685.aspx). 분류에 사용할 수 있는 toohello 소스 및 대상 클라우드의 Hyper-v 호스트 서버 수 있어야 합니다. 분류 필요 하지 않은 toohave hello 같은 유형의 저장소입니다. 예를 들어 Csv를 포함 하는 SMB 공유 tooa 대상 분류를 포함 하는 원본 분류를 매핑할 수 있습니다.
2. 분류가 구현되었으면 매핑을 만들 수 있습니다. toodo hello에이 **빠른 시작** 페이지 > **저장소 매핑**합니다.
3. Hello 클릭 **저장소** 탭 > **저장소 분류 매핑**합니다.
4. Hello에 **저장소 분류 매핑** 탭 hello 원본 분류를 선택 하 고 대상 VMM 서버입니다. 설정을 저장합니다.

    ![대상 네트워크 선택](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>7단계: 가상 컴퓨터 보호 사용
서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다.

1. Hello에 **가상 컴퓨터** hello는 hello에 가상 컴퓨터가 클라우드에 탭을 클릭 **보호 기능을 활성화** > **가상 컴퓨터 추가**합니다.
2. Hello hello 클라우드의 가상 컴퓨터의 목록에서 원하는 tooprotect hello 하나를 선택 합니다.

    ![가상 컴퓨터 보호 사용](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Hello hello에서 보호 사용 작업의 진행률을 추적 **작업** hello 초기 복제를 포함 하 여 탭 합니다. Hello 보호 완료 작업이 실행 hello 가상 컴퓨터 장애 조치에 있게 됩니다. 수 tooview 됩니다 한 후 보호를 사용 하도록 가상 컴퓨터 복제를 Azure에서 해당 합니다.

    ![가상 컴퓨터 보호 작업](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Hello VMM 콘솔에서 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다. 클릭 **보호 사용** hello 도구 모음에 있는 hello **Azure Site Recovery** hello 가상 컴퓨터 속성에서 탭 합니다.
>
>

### <a name="on-board-existing-virtual-machines"></a>기존 가상 컴퓨터 등록
Hyper-v 복제본과 함께 복제 하는 VMM에서 가상 컴퓨터를 기존 tooonboard 맞춰야 다음과 같이 Azure Site Recovery 보호 ç:

1. 기본 클라우드와 보조 클라우드가 있는지 확인합니다. Hello 기존 가상 컴퓨터를 호스트 하는 hello Hyper-v 서버 hello 기본 클라우드에 위치한 hello 복제본 가상 컴퓨터를 호스팅하는 hello Hyper-v 서버 hello 보조 클라우드에 있는지 확인 하십시오. 확인 hello 클라우드에 대 한 보호 설정을 구성 합니다. Hyper-v 복제본에 대 한 현재 구성 된 hello 설정과 일치 해야 합니다. 그렇지 않으면 가상 컴퓨터 복제가 예상대로 작동하지 않을 수 있습니다.
2. Hello 주 가상 컴퓨터에 대 한 보호를 사용 합니다. Azure 사이트 복구 및 VMM은 확인 hello 동일한 복제본 호스트 및 가상 컴퓨터가 감지 되는지, Azure 사이트 복구를 다시 사용 하 고 클라우드 구성 중 구성 된 hello 설정을 사용 하 여 복제를 다시 설정 됩니다.

## <a name="test-your-deployment"></a>배포 테스트
tootest 단일 가상 컴퓨터에 대 한 테스트 장애 조치를 실행 하거나 hello에 대 한 테스트 장애 조치를 실행 하 고 여러 가상 컴퓨터의 구성 된 복구 계획을 만들 수 있습니다 배포를 계획 합니다.  테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.

### <a name="create-a-recovery-plan"></a>복구 계획 만들기
1. Hello에 **복구 계획** 탭을 클릭 **복구 계획 만들기**합니다.
2. Hello 복구 계획 및 소스 및 대상 VMM 서버에 대 한 이름을 지정 합니다. hello 원본 서버 장애 조치 및 복구에 사용할 수 있는 가상 컴퓨터를 포함 해야 합니다. 선택 **Hyper-v** Hyper-v 복제를 위해 구성 된 tooview만 클라우드에 있습니다.

    ![복구 계획 만들기](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. **가상 컴퓨터 선택**에서 복제 그룹을 선택합니다. Hello 복제 그룹과 연결 된 모든 가상 컴퓨터가 선택 되 고 toohello 복구 계획을 추가 합니다. 이러한 가상 컴퓨터가 추가 toohello 복구 계획 기본 그룹-그룹 1입니다. 필요한 경우 그룹을 추가할 수 있습니다. 이때 가상 컴퓨터 복제 후 hello 복구 계획 그룹의 hello 순서에 따라 시작 됩니다.

    ![가상 컴퓨터 추가](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Hello hello 목록에 표시 하는 복구 계획이 만들어진 후 **복구 계획** 탭 합니다.

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
1. Hello에 **복구 계획** 탭을 클릭 하 고 hello 계획 선택 **테스트 장애 조치**합니다.
2. Hello에 **확인 테스트 장애 조치** 페이지에서 **None**합니다. 참고가 옵션을 사용할 수 있음을 hello 장애 조치 복제본 가상 컴퓨터에 연결 된 tooany 네트워크 수 없습니다. 가상 컴퓨터가 실패를 예상 대로 넘는 hello 하지만 복제 네트워크 환경 테스트 하지 않는 테스트 합니다. 너무 방법에 대해[테스트 장애 조치 실행](site-recovery-failover.md) 방법에 대 한 자세한 내용은 toouse 다양 한 네트워킹 옵션입니다.
3. hello 테스트 가상 컴퓨터는 hello에 복제 가상 컴퓨터가 있는 hello 호스트로 호스트 동일 hello에 생성 됩니다. Toohello 추가 되는 hello 복제 가상 컴퓨터의 위치를 가리키는 동일한 클라우드입니다.

### <a name="run-a-recovery-plan"></a>복구 계획 실행
복제 hello 복제 가상 컴퓨터에서 IP 주소는 hello를 되지 않았을 후 주 가상 컴퓨터 hello의 hello IP 주소와 동일 합니다. 가상 컴퓨터를 사용 하는 hello DNS 서버를 업데이트 합니다 후 시작 합니다. 또한 스크립트 tooupdate hello DNS 서버 tooensure 시기 적절 한 업데이트를 추가할 수 있습니다.

#### <a name="script-tooretrieve-hello-ip-address"></a>스크립트 tooretrieve hello IP 주소
이 샘플 스크립트 tooretrieve hello IP 주소를 실행 합니다.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>스크립트 tooupdate DNS
이 샘플 스크립트 tooupdate hello IP 주소를 지정 하는 DNS, 실행 hello 이전 예제 스크립트를 사용 하 여 검색 했습니다.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>사이트 복구에 대한 개인 정보 보호
이 섹션에서는 hello Microsoft Azure Site Recovery 서비스 ("서비스")에 대 한 추가 개인 정보를 제공 합니다. Microsoft Azure 서비스에 대 한 tooview hello 개인정보취급방침 참조는 [Microsoft Azure 개인정보취급방침](http://go.microsoft.com/fwlink/?LinkId=324899)

**기능: 등록**

* **수행하는 작업**: 가상 컴퓨터를 보호할 수 있도록 서버를 서비스에 등록합니다.
* **수집 된 정보**: 서비스를 수집, 처리 및 tooprovide 재해 복구 hello VMM 서버의 hello 서비스 이름을 사용 하 여 지정 hello VMM 서버에서 관리 인증서 정보를 전송 하는 hello 등록 한 후 hello의 이름과 VMM 서버에서 가상 컴퓨터 클라우드입니다.
* **정보 사용**:

  * 관리 인증서-이 옵션은 사용 toohelp 식별 하 고 액세스 toohello 서비스에 대 한 hello 등록 된 VMM 서버를 인증 합니다. hello 서비스 hello hello만 토큰을 등록 하는 hello 인증서 toosecure의 공개 키 부분을 사용 하 여 VMM 서버에 액세스할 수 있습니다. hello 서버 toouse이 토큰 toogain 액세스 toohello 서비스 기능을 필요합니다.
  * Hello VMM 서버의 이름-hello VMM 서버 이름은 필수 tooidentify 이며 위치에 있는 클라우드가 있는 hello에 hello 적절 한 VMM 서버와 통신 합니다.
  * 클라우드 hello VMM 서버에서 이름-hello 서비스 클라우드 쌍 연결/쌍 연결 해제 기능 아래에 설명 된를 사용 하는 경우 hello 클라우드 이름은 필수입니다. Toopair hello 복구 데이터 센터에서 다른 클라우드를 기본 데이터 센터에서 클라우드를 결정할 때는 hello 복구 데이터 센터에서 모든 hello 클라우드의 hello 이름이 표시 됩니다.
* **선택**:이 정보는 hello 서비스 등록 프로세스의 핵심 부분 도움이 되기 때문에 있으며 hello tooidentify hello 뿐만 아니라 tooprovide Azure Site Recovery 보호 하려는 서비스 tooidentify hello VMM 서버 올바른 등록 된 VMM 서버입니다. Toosend이 정보 toohello 서비스를 않으려는 경우에이 서비스를 사용 하지 마십시오. 서버를 등록 한 후 toounregister 나중 하려는 하는 경우, 후 그렇게 hello 서비스 포털 (Azure 포털을 hello은)에서 hello VMM 서버 정보를 삭제 합니다.

**기능: Azure Site Recovery 보호 사용**

* **역할**: hello hello VMM 서버에 설치 된 Azure 사이트 복구 공급자는 hello 서비스와 통신 하기 위한 hello 통로입니다. hello 공급자는 hello VMM 프로세스에서 호스트 되는 동적 연결 라이브러리 (DLL)입니다. 공급자가 설치 되어 hello, 후 hello VMM 관리자 콘솔에서 hello "데이터 센터 복구" 기능이 설정 됩니다. 클라우드에서 기존 또는 새 가상 컴퓨터에는 "데이터 센터 복구" 라는 속성이 사용 하도록 설정할 수 toohelp hello 가상 컴퓨터를 보호 합니다. 이 속성은 설정 되 면 hello 가상 컴퓨터 toohello 서비스의 hello 이름 및 ID 공급자 hello가 보냅니다. hello 가상 보호는 Windows Server 2012 또는 Windows Server 2012 R2 Hyper-v 복제 기술에 의해 활성화 됩니다. hello 가상 컴퓨터 데이터는 하나의 Hyper-v 호스트 tooanother (일반적으로 다른 "복구" 데이터 센터에 있음)에서 복제를 가져옵니다.
* **수집 된 정보**: hello 서비스 수집, 처리 및 hello 이름, ID, 가상 네트워크 및 hello hello 클라우드 이름을 포함 하는 hello 가상 컴퓨터에 대 한 메타 데이터를 전송 속해 있는 합니다.
* **정보의 사용**: hello 서비스 정보 toopopulate hello 가상 컴퓨터 정보 위에 hello를 사용 하 여 서비스 포털에 있습니다.
* **선택**: hello 서비스의 필수적인 부분 이므로 해제할 수 없습니다. 서비스 toohello 전송 되는이 정보를 사용 하지 않으려는 경우 모든 가상 컴퓨터에 대 한 Azure Site Recovery 보호를 사용 하지 않는 합니다. Note hello 공급자 toohello 서비스에서 보내는 모든 데이터 HTTPS를 통해 전송 됩니다.

**기능: 복구 계획**

* **역할**:이 기능은 toobuild hello "복구" 데이터 센터에 대 한 오케스트레이션 계획을 도움이 됩니다. Hello 순서는 hello에 가상 컴퓨터 또는 가상 컴퓨터의 그룹 시작 해야 hello 복구 사이트에서 정의할 수 있습니다. 를 실행 하는 자동화 된 스크립트 toobe 또는 각 가상 컴퓨터에 대 한 복구 hello 시점에 생성 된 모든 수동 작업 toobe 지정할 수 있습니다. 장애 조치 (hello 다음 섹션에 포함 됨)은 일반적으로 hello 조정 된 복구에 대 한 복구 계획 수준에서 트리거됩니다.
* **수집 된 정보**: hello 서비스 수집, 처리 및 가상 컴퓨터 메타 데이터 및 자동화 스크립트 및 수동 작업 메모의 메타 데이터를 포함 하 여 hello 복구 계획에 대 한 메타 데이터를 전송 합니다.
* **정보의 사용**: 위에서 설명한 hello 메타 데이터는 서비스 포털에서 사용 되는 toobuild hello 복구 계획 합니다.
* **선택**: hello 서비스의 필수적인 부분 이므로 해제할 수 없습니다. 서비스 toohello 전송 되는이 정보를 사용 하지 않으려는 경우이 서비스에서 복구 계획을 만들지 마세요.

**기능: 네트워크 매핑**

* **역할**:이 기능을 통해 hello 주 데이터 센터 toohello 복구 데이터 센터에서 toomap 네트워크 정보 있습니다. Hello 가상 컴퓨터는 hello 복구 사이트에서 복구 되 면이 매핑은 해당에 대 한 네트워크 연결을 설정할에서 편리 합니다.
* **수집 된 정보**: hello 네트워크 매핑 기능의 일부로 서비스 hello 수집, 처리 및 hello (주 파일 그룹 및 데이터 센터)에 각 사이트에 대 한 논리 네트워크의 hello 메타 데이터를 전송 합니다.
* **정보의 사용**: hello 서비스 사용 하 여 hello 메타 데이터 toopopulate 서비스 포털 hello 네트워크 정보를 매핑할 수 있습니다.
* **선택**: hello 서비스의 필수적인 부분 이므로 해제할 수 없습니다. 서비스 toohello 전송 되는이 정보를 사용 하지 않으려는 hello 네트워크 매핑 기능을 사용 하지 마십시오.

**기능: 장애 조치(Failover) - 계획됨, 계획되지 않음, 테스트**

* **역할**:이 기능은 하나의 VMM 관리 되는 데이터 센터 tooanother VMM에서 관리 하는 데이터 센터에서 가상 컴퓨터의 장애 조치를 도움이 됩니다. hello 장애 조치 작업의 서비스 포털에서 hello 사용자에 의해 트리거됩니다. 장애 조치에 대 한 다음과 같은 계획 되지 않은 이벤트 (예: 자연 disaster0;의 hello 대/소문자의에서 계획 된 이벤트 (예를 들어 데이터 센터 부하 분산)를 테스트 장애 조치 (예: 복구 계획 예행).

hello VMM 서버에 공급자 hello는 hello 서비스에서에서 hello 이벤트의 알림을 받고을 VMM 인터페이스를 통해 hello Hyper-v 호스트에서 장애 조치 작업을 수행 합니다. 하나의 Hyper-v 호스트 tooanother (일반적으로 다른 "복구" 데이터 센터에서 실행)에서 hello 가상 컴퓨터의 실제 장애 조치 hello Windows Server 2012 또는 Windows Server 2012 R2 Hyper-v 복제 기술에 의해 처리 됩니다. Hello 장애 조치가 완료 되 면 hello hello "복구" 데이터 센터의 hello VMM 서버에 설치 된 공급자 hello 성공 정보 toohello 서비스를 보냅니다.

* **수집 된 정보**: hello 서비스는 hello 장애 조치 동작 정보 정보 toopopulate hello 상태 위에 hello를 사용 하 여 서비스 포털에 있습니다.
* **정보의 사용**: hello 서비스 다음과 같이 hello 정보 사이 사용 합니다.

  * 관리 인증서-이 옵션은 사용 toohelp 식별 하 고 액세스 toohello 서비스에 대 한 hello 등록 된 VMM 서버를 인증 합니다. hello 서비스 hello hello만 토큰을 등록 하는 hello 인증서 toosecure의 공개 키 부분을 사용 하 여 VMM 서버에 액세스할 수 있습니다. hello 서버 toouse이 토큰 toogain 액세스 toohello 서비스 기능을 필요합니다.
  * Hello VMM 서버의 이름-hello VMM 서버 이름은 필수 tooidentify 이며 위치에 있는 클라우드가 있는 hello에 hello 적절 한 VMM 서버와 통신 합니다.
  * 클라우드 hello VMM 서버에서 이름-hello 서비스 클라우드 쌍 연결/쌍 연결 해제 기능 아래에 설명 된를 사용 하는 경우 hello 클라우드 이름은 필수입니다. Toopair hello 복구 데이터 센터에서 다른 클라우드를 기본 데이터 센터에서 클라우드를 결정할 때는 hello 복구 데이터 센터에서 모든 hello 클라우드의 hello 이름이 표시 됩니다.
* **선택**: hello 서비스의 필수적인 부분 이므로 해제할 수 없습니다. 서비스 toohello 전송 되는이 정보를 사용 하지 않으려면이 서비스를 사용 하지 마십시오.

## <a name="next-steps"></a>다음 단계
사용자 환경, 예상 대로 작동 하는 테스트 장애 조치 toocheck 실행 한 후 [알아봅니다](site-recovery-failover.md) 다양 한 유형의 장애 조치를 수행 합니다.
