---
title: "VMM 클라우드 tooAzure aaaReplicate Hyper-v 가상 컴퓨터 | Microsoft Docs"
description: "이 문서에서는 Hyper-v 호스트에 Hyper-v 가상 컴퓨터 tooreplicate System Center VMM 클라우드에 tooAzure에 위치 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>VMM 클라우드 tooAzure에서 Hyper-v 가상 컴퓨터 복제
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [클래식 포털](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - 클래식](site-recovery-deploy-with-powershell.md)
>
>

hello Azure Site Recovery 서비스 tooyour 비즈니스 연속성 및 조정 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 재해 복구 (BCDR) 전략에 기여합니다. 복제 된 tooAzure 또는 tooa 보조 온-프레미스 데이터 센터 컴퓨터 수 있습니다. 빠른 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)

## <a name="overview"></a>개요
이 문서에서는 hyper-v toodeploy tooreplicate Hyper-v 가상 컴퓨터를 Site Recovery VMM 사설 클라우드에 tooAzure에 있는 서버를 호스트 하는 방법을 설명 합니다.

hello 문서 hello 시나리오에 대 한 필수 구성 요소를 포함 하 고 사이트 복구 자격 증명 모음을 tooset hello hello 원본 VMM 서버에 설치 된 Azure 사이트 복구 공급자에 게 어떻게 hello 서버 hello 자격 증명 모음에 등록, Azure 저장소 계정 추가 설치, hello를 보여 줍니다. Hyper-v 호스트 서버에 azure 복구 서비스 에이전트에 적용 된 tooall 보호 된 가상 컴퓨터 되며 다음 이러한 가상 컴퓨터에 대 한 보호를 사용 하도록 설정 하는 VMM 클라우드에 대 한 보호 설정을 구성 합니다. 모든 것이 예상 대로 작동 하는지 테스트 hello 장애 조치 toomake까지 완료 합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="architecture"></a>아키텍처
![아키텍처](./media/site-recovery-vmm-to-azure-classic/topology.png)

* hello Azure 사이트 복구 공급자는 사이트 복구 배포 중에 hello VMM에 설치 하 고 hello VMM 서버가 hello 사이트 복구 자격 증명 모음에 등록 합니다. hello 공급자 toohandle 복제 오케스트레이션 Site Recovery와 통신합니다.
* hello Azure 복구 서비스 에이전트는 사이트 복구 배포 하는 동안 Hyper-v 호스트 서버에 설치 됩니다. 데이터 복제 tooAzure 저장소를 처리합니다.

## <a name="azure-prerequisites"></a>Azure 필수 조건
Azure에서 다음 항목이 필요합니다.

| **필수 요소** | **세부 정보** |
| --- | --- |
| **Azure 계정** |[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. 사이트 복구 가격 책정에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Azure 저장소** |Azure 저장소 계정 복제 toostore 데이터 필요 합니다. 복제된 데이터는 Azure 저장소에 저장되고 장애 조치(Failover) 발생 시 Azure VM이 작동합니다. <br/><br/>[표준 지역 중복 저장소 계정](../storage/common/storage-redundancy.md#geo-redundant-storage)이 필요합니다. hello 계정은 해야 hello Site Recovery 서비스와 동일한 지역 hello와 연결 된 동일한 구독 hello 합니다. Note 복제 toopremium 저장소 계정은 현재 지원 되지 않음 및 사용할 수 있습니다.<br/><br/>[자세히 알아보세요](../storage/common/storage-introduction.md) . |
| **Azure 네트워크** |Azure Vm 연결 하는 Azure 가상 네트워크 필요 합니다 toowhen 장애 조치가 발생 합니다. hello Azure 가상 네트워크에에서 있어야 hello hello 사이트 복구 자격 증명 모음과 동일한 지역입니다. |

## <a name="on-premises-prerequisites"></a>온-프레미스 필수 조건
온-프레미스에서 다음 항목이 필요합니다.

| **필수 요소** | **세부 정보** |
| --- | --- |
| **VMM** |물리적 또는 가상 독립 실행형 서버나 가상 클러스터로 배포된 VMM 서버가 하나 이상 필요합니다. <br/><br/>VMM 서버 hello hello 최신 누적 업데이트가 설치 된 System Center 2012 R2 실행 되어야 합니다.<br/><br/>Hello VMM 서버에 구성 된 클라우드가 하나 이상 필요 합니다.<br/><br/>원하는 tooprotect hello 원본 클라우드는 하나 이상의 VMM 호스트 그룹을 포함 해야 합니다.<br/><br/>Keith Mayer 블로그의 [연습: System Center 2012 SP1 VMM에서 사설 클라우드 만들기](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) 에서 VMM 클라우드 설정에 대해 자세히 알아봅니다. |
| **Hyper-V** |하나 이상의 Hyper-v 호스트 서버 또는 클러스터 v m M 클라우드 hello에 필요 합니다. hello 호스트 서버에 있어야 하 고 하나 이상의 Vm입니다. <br/><br/>이상 hello Hyper-v 서버에서 실행 해야 **Windows Server 2012 R2** hello Hyper-v 역할과 또는 **Microsoft Hyper-v Server 2012 R2** 최신 업데이트가 설치 되어 hello 있어야 하 고 합니다.<br/><br/>Vm을 포함 하는 모든 Hyper-v 서버 tooprotect VMM 클라우드에 있어야 두는 것이 좋습니다.<br/><br/>클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Tooconfigure hello 클러스터 브로커를 수동으로 필요 합니다. [자세히 알아봅니다](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) 를 확인해 보세요. |
| **보호된 컴퓨터** | Vm tooprotect 준수 해야 하는 것이 원하는 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다. |

## <a name="network-mapping-prerequisites"></a>네트워크 매핑 필수 조건
Azure 네트워크 매핑의 가상 컴퓨터를 보호 하는 경우 hello 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크 tooenable hello 다음 간에 매핑합니다.

* 모든 컴퓨터의 장애 조치 있는 hello에 동일한 네트워크 tooeach 기타에 복구 계획과 관계 없이 연결할 수 있습니다.
* Hello 대상 Azure 네트워크에 네트워크 게이트웨이가 설치 되 면 가상 컴퓨터 tooother 온-프레미스 가상 컴퓨터를 연결할 수 있습니다.
* 구성 하지 않으면 네트워크 매핑 장애 조치 hello에 동일한 가상 컴퓨터만 복구 계획 장애 조치 tooAzure 후에 다른 수 tooconnect tooeach 됩니다.

네트워크 매핑을 toodeploy 하려는 경우에 hello 다음이 필요 합니다.

* hello 원본 VMM 서버의 tooprotect 원하는 hello 가상 컴퓨터에 연결 된 tooa VM 네트워크 여야 합니다. 해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.
* Azure 네트워크 toowhich 복제 가상 컴퓨터는 장애 조치 후 연결할 수 있습니다. 장애 조치 hello 시간에이 네트워크를 선택 합니다. hello 네트워크 hello에 있어야 합니다. Azure Site Recovery 구독와 동일한 영역입니다.


VMM에서 네트워크 준비:

   * [논리 네트워크를 설정합니다](https://technet.microsoft.com/library/jj721568.aspx).
   * [VM 네트워크를 설정합니다](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>1단계: 사이트 복구 자격 증명 모음 만들기
1. Toohello 로그인 [관리 포털](https://portal.azure.com) tooregister hello VMM 서버에서 원하는 합니다.
2. **Data Services** > **Recovery Services** > **Site Recovery 자격 증명 모음**을 차례로 클릭합니다.
3. **새로 만들기** > **빠른 생성**을 클릭합니다.
4. **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.
5. **지역**, 선택 hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 지원 toocheck 지역에서 지역 가용성 참조 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
6. **자격 증명 모음 만들기**를 클릭합니다.

    ![새 자격 증명 모음](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

자격 증명 모음 hello hello 상태 표시줄 tooconfirm 올바르게 만들어졌는지 확인 합니다. hello 자격 증명 모음으로 나열 됩니다 **활성** hello 기본 복구 서비스 페이지에 있습니다.

## <a name="step-2-generate-a-vault-registration-key"></a>2단계: 자격 증명 모음 등록 키 생성
Hello 자격 증명 모음에 등록 키를 생성 합니다. Hello Azure Site Recovery Provider를 다운로드 하 고 hello VMM 서버에 설치 후에 hello 자격 증명 모음에이 키 tooregister hello VMM 서버를 사용 합니다.

1. Hello에 **복구 서비스** 페이지 hello 자격 증명 모음 tooopen hello 빠른 시작 페이지를 클릭 합니다. 빠른 시작 언제 든 지 hello 아이콘을 사용 하 여 열 수도 있습니다.

    ![빠른 시작 아이콘](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Hello 드롭다운 목록에서 선택 **온-프레미스 VMM 사이트와 Microsoft Azure 간에**합니다.
3. **VMM 서버 준비**에서 **등록 키 생성** 파일을 클릭합니다. hello 키 파일이 자동으로 생성 됩니다 및은 생성 된 후 5 일 동안 유효 합니다. Hello VMM 서버에서는 hello Azure 포털 하지에 액세스할 때는이 파일 toohello 서버 toocopy 필요 합니다.

    ![등록 키](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>3 단계: hello Azure Site Recovery Provider 설치
1. **빠른 시작** > **준비 VMM 서버**, 클릭 **Microsoft Azure 사이트 복구 공급자 다운로드 VMM 서버에 설치에 대 한** tooobtain hello hello 공급자 설치 파일의 최신 버전입니다.
2. Hello 원본 VMM 서버에서이 파일을 실행 합니다.

   > [!NOTE]
   > VMM 클러스터에 배포 되 고 처음으로 hello에 대 한 hello 공급자를 설치 하는 경우에 액티브 노드에 설치 및 hello 자격 증명 모음에 hello 설치 tooregister hello VMM 서버를 완료 합니다. 그런 다음 hello 공급자에 설치 hello 다른 노드가 있습니다. 공급자는 모두 때문에 모든 노드에서 tooupgrade 해야 될 hello를 업그레이드 하는 경우 실행 hello 동일한 공급자 버전이 참고 합니다.
   >
   >
3. 설치 관리자 hello prerequirements 검사 및 권한을 toostop hello VMM 서비스 toobegin Provider 설치를 요청 합니다. 자동으로 설치가 완료 되 면 hello VMM 서비스에 다시 시작 됩니다. 에 설치 하는 경우 VMM 클러스터 수 toostop hello 클러스터 역할을 라는 메시지가 나타납니다.
4. **Microsoft 업데이트** 에서 업데이트를 선택할 수 있습니다. 이 설정을 사용 하 여 tooyour Microsoft Update 정책에 따라 사용 가능한 공급자 업데이트가 설치 됩니다.

    ![Microsoft 업데이트](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. 공급자가 너무 설정 hello에 대 한 설치 위치를 hello**<SystemDrive>files\microsoft System Center 2012 R2\Virtual Machine Manager\bin**합니다. **Install**을 클릭합니다.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. 공급자가 설치 되어 hello 후 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. **자격 증명 모음 이름**, hello는 hello 서버를 등록할 자격 증명 모음의 hello 이름이 유효한 지 확인 합니다. *다음*을 누릅니다.

    ![서버 등록](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. **인터넷 연결** 지정 방법을 hello VMM에서 실행 중인 공급자를 hello 서버 toohello 인터넷 연결 합니다. 선택 **기존 프록시 설정 사용 하 여 연결** toouse hello 기본 인터넷 연결 설정을 hello 서버에 구성 합니다.

    ![인터넷 설정](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

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
13. 클릭 **다음** toocomplete hello 프로세스입니다. 등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다. hello 서버 hello에 표시 된 **VMM 서버** hello에 탭 **서버** hello 자격 증명 모음에 페이지입니다.

    ![마지막 페이지](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다. hello 서버 hello에 표시 된 **VMM 서버** hello에 탭 **서버** hello 자격 증명 모음에 페이지입니다.

### <a name="command-line-installation"></a>명령줄 설치
또한 hello 다음 명령줄을 사용 하 여 hello Azure Site Recovery Provider를 설치할 수 있습니다. 이 메서드는 Server Core에 대 한 Windows Server 2012 r 2에서 사용 되는 tooinstall hello 공급자 수 있습니다.

1. Hello 공급자 설치 파일과 등록 키 tooa 폴더를 다운로드 합니다. 예: C:\ASR.
2. Hello System Center Virtual Machine Manager 서비스 중지
3. 상승된 된 명령 프롬프트에서 다음이 명령 사용 하 여 hello 공급자 설치 관리자를 추출 합니다.

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. 다음과 같이 hello 공급자를 설치 합니다.

        C:\ASR> setupdr.exe /i
5. 다음과 같이 hello 공급자를 등록 합니다.

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

여기에서 매개 변수는 다음과 같습니다.

* **/ 자격 증명** :는 hello 등록 키 파일의 위치를 가리키는 hello 위치를 지정 하는 필수 매개 변수  
* **/ FriendlyName** : hello Azure Site Recovery 포털에 표시 되는 hello Hyper-v 호스트 서버 hello 이름에 대 한 필수 매개 변수입니다.
* **/ EncryptionEnabled** : 선택적 매개 변수 toospecify tooencryption (rest 암호화)에서 Azure의 가상 컴퓨터를 선택 합니다. hello 파일 이름이 있어야는 **.pfx** 확장 합니다.
* **/proxyAddress** : hello hello 프록시 서버의 주소를 지정 하는 선택적 매개 변수입니다.
* **/proxyport** : hello hello 프록시 서버의 포트를 지정 하는 선택적 매개 변수입니다.
* **/proxyUsername** : hello 프록시 사용자 이름을 지정 하는 선택적 매개 변수입니다.
* **/proxyPassword** : hello 프록시 암호를 지정 하는 선택적 매개 변수입니다.  

## <a name="step-4-create-an-azure-storage-account"></a>4단계: Azure 저장소 계정 만들기
1. 클릭 하 여 Azure 저장소 계정이 없는 경우 **Azure 저장소 계정 추가** toocreate 계정.
2. 지역에서 복제를 사용하는 계정을 만듭니다. Hello hello Azure Site Recovery 서비스와 동일한 지역 또는 hello와 연결할에 해야 동일한 구독 합니다.

    ![저장소 계정](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [저장소 계정 마이그레이션](../azure-resource-manager/resource-group-move-resources.md) 전체 리소스 그룹 내 hello 동일한 구독 또는 구독에서 지원 되지 않습니다 Site Recovery를 배포 하는 데 사용 되는 저장소 계정에 대 한 합니다.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>5 단계: hello Azure 복구 서비스 에이전트 설치
각 Hyper-v 호스트 서버 v m M 클라우드 hello에 hello Azure 복구 서비스 에이전트를 설치 합니다.

1. 클릭 **빠른 시작** > **Azure 사이트 복구 서비스 에이전트 다운로드 및 호스트에 설치** tooobtain hello hello 에이전트 설치 파일의 최신 버전입니다.

    ![복구 서비스 에이전트 설치](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. 각 Hyper-v 호스트 서버 hello 설치 파일을 실행 합니다.
3. Hello에 **필수 구성 요소 확인** 페이지 **다음**합니다. 누락된 필수 구성 요소는 자동으로 설치됩니다.

    ![필수 구성 요소 복구 서비스 에이전트](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. Hello에 **설치 설정** 페이지 tooinstall hello 에이전트와 백업 메타 데이터를 설치할 수는 select hello 캐시 위치를 지정 합니다. **설치**를 클릭합니다.
5. 클릭 하 여 설치를 마친 후 **닫기** toocomplete hello 마법사.

    ![MARS 에이전트 등록](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>명령줄 설치
이 명령을 사용 하 여 hello 명령줄에서 hello Microsoft Azure 복구 서비스 에이전트를 설치할 수도 있습니다.

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>6단계: 클라우드 보호 설정 구성
Hello VMM 서버를 등록 한 후 클라우드 보호 설정을 구성할 수 있습니다. Hello 옵션 사용 하도록 설정한 **hello 자격 증명 모음과 클라우드 데이터를 동기화** hello VMM 서버의 모든 클라우드에 hello에 나타납니다. 하므로 hello 공급자를 설치할 때 <b>보호 된 항목</b> hello 자격 증명 모음에는 탭 합니다.

![게시된 클라우드](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Hello 빠른 시작 페이지에서 클릭 **VMM 클라우드에 대 한 보호 설정**합니다.
2. Hello에 **보호 된 항목** 탭에서 hello 클라우드에서 tooconfigure을 toohello 이동 **구성** 탭 합니다.
3. **대상** select **Azure**을 확인하세요.
4. **저장소 계정** 복제를 위해 사용할 hello Azure 저장소 계정을 선택 합니다.
5. 설정 **저장 된 데이터 암호화** 너무**오프**합니다. 이 설정은 hello 온-프레미스 사이트와 Azure 간에 복제 하는 동안 데이터를 암호화할지를 지정 합니다.
6. **복사 빈도** hello 기본 설정을 그대로 적용 합니다. 이 값은 원본 위치와 대상 위치 사이에 데이터를 동기화해야 하는 빈도를 지정합니다.
7. **복구 지점을 보존할**, hello 기본 설정을 그대로 적용 합니다. 기본값은 0, hello 최신 복구 지점만 주 가상 컴퓨터에 대 한 복제본 호스트 서버에 저장 됩니다.
8. **응용 프로그램 일치 스냅숏 빈도**, hello 기본 설정을 그대로 적용 합니다. 이 값은 얼마나 자주 지정 toocreate 스냅숏을 합니다. Hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure을 사용 합니다.  값을 설정한 경우 구성 하는 추가 복구 지점 수가 hello 보다 작으면 있는지 확인 합니다.
9. **복제 시작 시간**, 데이터 tooAzure의 초기 복제 작업을 시작할지를 지정 합니다. hello 표준 시간대 hello Hyper-v 호스트 서버에서 사용 됩니다. 사용량이 적은 시간 동안 hello 초기 복제를 예약 하는 것이 좋습니다.

    ![클라우드 복제 설정](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Hello 설정을 저장 한 후 작업이 만들어지고 hello에서 모니터링할 수 **작업** 탭 합니다. 복제에 대 한 VMM 원본 클라우드에 hello에서 모든 Hyper-v 호스트 서버를 구성 됩니다.

저장 한 후 클라우드 설정을 수정할 수 있는 hello에 **구성** 탭 toomodify hello 대상 위치나 대상 저장소 계정 tooremove hello 클라우드 구성이 필요 하 고 다시 hello 클라우드를 구성 합니다. Hello 저장소 계정 hello 변경 내용을 변경 하면 hello 저장소 계정 수정 된 후 보호에 사용 되는 가상 컴퓨터에만 적용 되는 참고 합니다. 기존 가상 컴퓨터는 마이그레이션되지 않습니다 toohello 새 저장소 계정입니다.

## <a name="step-7-configure-network-mapping"></a>7단계: 네트워크 매핑 구성
시작 하기 전에 네트워크 매핑을 hello 원본 VMM 서버의 가상 컴퓨터가 연결 된 tooa VM 네트워크에 있는지 확인 합니다. 또한 Azure 가상 네트워크를 하나 이상 만듭니다. 여러 VM 네트워크에 매핑된 tooa 단일 Azure 네트워크 수 있는지 확인 합니다.

1. Hello 빠른 시작 페이지에서 클릭 **네트워크 매핑**합니다.
2. Hello에 **네트워크** 탭 **소스 위치**선택, hello 원본 VMM 서버입니다. **대상 위치** 에서 Azure를 선택합니다.
3. **소스** 네트워크 hello VMM 서버와 관련 된 VM 네트워크의 목록이 표시 됩니다. **대상** 네트워크 hello Azure hello 구독과 연결 된 네트워크 표시 됩니다.
4. Hello 원본 VM 네트워크를 선택 하 고 클릭 **지도**합니다.
5. Hello에 **대상 네트워크 선택** 선택 hello 대상 Azure 네트워크 toouse 원하는 페이지입니다.
6. Hello 확인 표시가 toocomplete hello 매핑 프로세스를 클릭 합니다.

    ![클라우드 복제 설정](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Hello 설정을 저장 한 후 작업을 tootrack hello 매핑 진행률을 시작 하 고 hello [작업] 탭에서 모니터링할 수 있습니다. Toohello 원본 VM 네트워크에 해당 하는 모든 기존 복제본 가상 컴퓨터에 연결 된 toohello 될 대상 Azure 네트워크입니다. 연결 된 toohello 원본 VM 네트워크는 새 가상 컴퓨터 복제 후 매핑된 Azure 네트워크 연결된 toohello 됩니다. 새 네트워크로 기존 매핑을 수정 하는 경우 hello 새 설정을 사용 하 여 복제본 가상 컴퓨터가 연결 됩니다.

Note는 hello 대상 네트워크에 서브넷이 여러 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제 가상 컴퓨터 장애 조치 후에 대상 서브넷 연결된 toothat 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.

> [!NOTE]
> [마이그레이션 네트워크의](../azure-resource-manager/resource-group-move-resources.md) 전체 리소스 그룹 내 hello 동일한 구독 또는 구독에서 지원 되지 않습니다 Site Recovery를 배포 하는 데 사용 되는 네트워크에 대 한 합니다.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>8단계: 가상 컴퓨터의 보호 활성화
서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다. 참고 hello 다음.

* 가상 컴퓨터는 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족해야 합니다.
* tooenable 보호 hello 운영 체제 및 운영 체제 디스크 속성 hello 가상 컴퓨터에 대해 설정 되어야 합니다. 가상 컴퓨터 템플릿을 사용 하 여 VMM에서 가상 컴퓨터를 만들 때 hello 속성을 설정할 수 있습니다. Hello에 기존 가상 컴퓨터에 대 한 이러한 속성을 설정할 수도 있습니다 **일반** 및 **하드웨어 구성** hello 가상 컴퓨터 속성의 탭 합니다. VMM에서 이러한 속성을 설정 하지 않으면 수 수 tooconfigure hello Azure Site Recovery 포털에서 해당 합니다.

    ![가상 컴퓨터 만들기](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![가상 컴퓨터 속성 수정](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. hello에 대 한 tooenable 보호, **가상 컴퓨터** hello는 hello에 가상 컴퓨터가 클라우드에 탭을 클릭 **보호 기능을 활성화** > **가상컴퓨터추가**.
2. Hello hello 클라우드의 가상 컴퓨터의 목록에서 원하는 tooprotect hello 하나를 선택 합니다.

    ![가상 컴퓨터 보호 사용](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Hello의 진행률을 추적 **보호 사용** hello에 대 한 작업 **작업** hello 초기 복제를 포함 하 여 탭 합니다. Hello 후 **보호 완료** 실행 작업 hello 가상 컴퓨터가 장애 조치에 대해 준비 합니다. 수 tooview 됩니다 한 후 보호를 사용 하도록 가상 컴퓨터 복제를 Azure에서 해당 합니다.

    ![가상 컴퓨터 보호 작업](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Hello 가상 컴퓨터 속성을 확인 하 고 필요에 따라 수정 합니다.

    ![가상 컴퓨터 확인](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. Hello에 **구성** 다음과 같은 네트워크 속성 hello 가상 컴퓨터 속성의 탭을 수정할 수 있습니다.

* **Hello 대상 가상 컴퓨터에 네트워크 어댑터 수가** -네트워크 어댑터의 hello 수 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다. 확인 [가상 컴퓨터 크기 사양](../virtual-machines/linux/sizes.md) hello 가상 컴퓨터 크기에서 지원 되는 어댑터의 hello 수에 대 한 합니다. 가상 컴퓨터에 대 한 hello 크기를 수정 하 고 hello 설정을 저장 하는 경우 네트워크 어댑터 수가 hello 바뀝니다 hello 다음 hello를 열 때 **구성** 페이지. 대상 가상 컴퓨터의 네트워크 어댑터의 hello 수는 원본 가상 컴퓨터와 hello 최대 수를 다음과 같이 선택한 hello 가상 컴퓨터의 hello 크기에서 지원 되는 네트워크 어댑터에서 네트워크 어댑터의 최소 수 hello:

  * Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
  * Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.
  * 예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 개 경우 hello 대상 컴퓨터에 두 개의 어댑터 갖습니다. Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.     
* **Hello 대상 가상 컴퓨터의 네트워크** -hello 네트워크 toowhich hello 가상 컴퓨터가 연결 toois 원본 가상 컴퓨터의 hello 네트워크의 네트워크 매핑에 의해 결정 됩니다. Hello 원본 가상 컴퓨터에 둘 이상의 네트워크 어댑터와 소스 네트워크 경우 매핑된 toodifferent 네트워크 대상에 대해 toochoose hello 대상 네트워크 중 하나를 해야 합니다.
* **각 네트워크 어댑터의 서브넷** -hello 서브넷 toowhich hello 장애 조치 가상 컴퓨터를 선택할 수 있습니다 각 네트워크 어댑터에 연결 하는 것입니다.
* **IP 주소를 대상** -경우 원본 가상 컴퓨터의 hello 네트워크 어댑터는 구성 된 toouse는 고정 IP 주소 hello 대상 가상 컴퓨터에 대 한 hello IP 주소를 제공할 수 있습니다. 이 기능을 사용 하 여 장애 조치 후 원본 가상 컴퓨터의 IP 주소가 hello를 유지 합니다. IP 주소가 없습니다. 제공 된 모든 사용 가능한 IP 주소를 장애 조치 시 hello toohello 네트워크 어댑터를 제공 됩니다. Hello 대상 IP 주소를 지정 하 고 Azure에서 실행 중인 다른 가상 컴퓨터에서 이미 사용 하는 경우 장애 조치가 실패 합니다.  

    ![네트워크 속성 수정](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> 고정 IP 주소를 사용하는 Linux 가상 컴퓨터는 지원되지 않습니다.
>
>

## <a name="test-hello-deployment"></a>Hello 배포 테스트
tootest 단일 가상 컴퓨터에 대 한 테스트 장애 조치를 실행 하거나 hello에 대 한 테스트 장애 조치를 실행 하 고 여러 가상 컴퓨터의 구성 된 복구 계획을 만들 수 있습니다 배포를 계획 합니다.  

테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다. 다음 사항에 유의하세요.

* Hello 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 tooconnect toohello 가상 컴퓨터를 사용 하도록 하려는 경우는 hello 테스트 장애 조치를 실행 하기 전에 hello 가상 컴퓨터에서 원격 데스크톱 연결을 사용 합니다.
* 장애 조치 후 공용 IP 주소 tooconnect toohello 원격 데스크톱을 사용 하 여 Azure VM 사용 합니다. Toodo이를 확인 하는 공용 주소를 사용 하 여 연결 tooa 가상 컴퓨터를 방해 하는 모든 도메인 정책 필요가 없습니다.

> [!NOTE]
> tooget hello 최상의 성능을 tooAzure을 장애 조치할 때 이전에 설치한 확인 hello VM에 Azure 에이전트 hello 합니다. 이렇게 하면 부팅이 빨라지고 문제 해결에 도움이 됩니다. Hello 다운로드 [Linux 에이전트](https://github.com/Azure/WALinuxAgent), 또는 hello [Windows 에이전트](http://go.microsoft.com/fwlink/?LinkID=394789)합니다.
>
>

### <a name="create-a-recovery-plan"></a>복구 계획 만들기
1. Hello에 **복구 계획** 탭에서 새 계획을 추가 합니다. 이름을 지정 **VMM** 에 **소스 형식**, 및 hello 원본 VMM 서버에서 **소스**합니다. hello 대상 Azure 됩니다.

    ![복구 계획 만들기](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. Hello에 **가상 컴퓨터 선택** 페이지, 가상 컴퓨터 선택 tooadd toohello 복구 계획 합니다. 이러한 가상 컴퓨터가 추가 toohello 복구 계획 기본 그룹-그룹 1입니다. 단일 복구 계획에서 최대 100개의 가상 컴퓨터가 테스트되었습니다.

* Toohello 계획을 추가 하기 전에 tooverify hello 가상 컴퓨터 속성을 원하는 경우 hello 가상 컴퓨터는 자신이 hello 클라우드의 hello 속성 페이지를 클릭 위치입니다. Hello VMM 콘솔에서 hello 가상 컴퓨터 속성을 구성할 수도 있습니다.
* 모든 표시 되는 hello 가상 컴퓨터 보호에 사용 된 합니다. hello 목록에는 보호 하 고 초기 복제가 완료 되 고 함께 보호에 사용 하는 초기 복제가 보류 중인 사용 되는 가상 컴퓨터 모두 포함 됩니다. 초기 복제가 완료된 가상 컴퓨터만 복구 계획의 일부로 장애 조치(Failover)될 수 있습니다.

    ![복구 계획 만들기](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Hello에 대 한 복구 계획을 만든 후에 그 표시 **복구 계획** 탭 합니다. 추가할 수도 있습니다 [Azure 자동화 runbook](site-recovery-runbook-automation.md) 장애 조치 중 toohello 복구 계획 tooautomate 동작 합니다.

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
테스트 장애 조치 tooAzure 두 가지 방법으로 toorun이 됩니다.

* **테스트 Azure 네트워크 없이 장애 조치**—이 유형의 테스트 장애 조치 hello 가상 컴퓨터에에서 올바로 표시 Azure 확인 합니다. hello 가상 컴퓨터가 장애 조치 후 연결 된 tooany Azure 네트워크를 되지 않습니다.
* **테스트 Azure 네트워크와 장애 조치**—이 유형의 장애 조치 검사를 전체 복제 환경이 hello 올바로 표시 하 고 장애 조치 hello 가상 컴퓨터 연결된 toohello 지정 된 대상 Azure 네트워크 됩니다. 서브넷 처리를 위해 테스트 장애 조치에 대 한 hello 테스트 가상 컴퓨터의 서브넷을 hello 냅니다 hello 복제 가상 컴퓨터의 hello 서브넷에 기반 합니다. 이 복제 가상 컴퓨터의 서브넷을 hello 기반 hello 원본 가상 컴퓨터의 hello 서브넷으로 다른 tooregular 복제 합니다.

Azure 대상 네트워크를 지정 하지 않고 보호 tooAzure 사용 하도록 설정 하는 가상 컴퓨터에 대 한 테스트 장애 조치 toorun 하려는 경우에 아무 것도 tooprepare 필요 하지 않습니다. 테스트 장애 조치 대상 (기본 동작 Azure에서 새 네트워크를 만들 때) Azure 프로덕션 네트워크에서 toocreate 분리 된 새 Azure 네트워크를 사용 해야 하는 Azure 네트워크와 toorun 합니다. 너무 방법에 대해[테스트 장애 조치를 실행](site-recovery-failover.md) 내용을 확인 합니다.

예상 대로 hello 복제 가상 컴퓨터 toowork에 대 한 tooset hello 인프라를 할 수 있습니다. 예를 들어 도메인 컨트롤러 및 DNS와 가상 컴퓨터를 Azure Site Recovery를 사용 하 여 복제 된 tooAzure 수 및 테스트 장애 조치를 사용 하 여 hello 테스트 네트워크에서 만들 수 있습니다. 자세한 내용은 [Active Directory의 테스트 장애 조치(failover) 시 고려 사항](site-recovery-active-directory.md#test-failover-considerations) 섹션을 살펴봅니다.

테스트 장애 조치 toorun 다음 hello지 않습니다.

1. Hello에 **복구 계획** 탭을 클릭 하 고 hello 계획 선택 **테스트 장애 조치**합니다.
2. Hello에 **확인 테스트 장애 조치** 페이지 선택 **None** 또는 특정 Azure 네트워크입니다.  Note hello 테스트 장애 조치 됩니다 없음을 선택 하는 경우 가상 컴퓨터를 hello 검사 tooAzure 올바르게 복제 하지만 복제 네트워크 구성은 확인 하지 않습니다.

    ![네트워크 없음](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. hello 클라우드에 대 한 데이터 암호화를 사용 하는 경우 **암호화 키** 클라우드에 대 한 hello 옵션 tooenable 데이터 암호화를 켤 때 hello 공급자 hello VMM 서버에 설치 하는 동안 실행 된 select hello 인증서 .
4. Hello에 **작업** 탭 장애 조치 진행률을 추적할 수 있습니다. 또한 수 toosee hello Azure 포털에서에서 가상 컴퓨터 테스트 복제본 hello 있어야 합니다. 온-프레미스 네트워크에서 tooaccess 가상 컴퓨터를 설정 하는 경우 원격 데스크톱 연결 toohello 가상 컴퓨터를 시작할 수 있습니다.
5. Hello 장애 조치 hello을에 도달 하면 **완벽 한 테스트** 단계, 클릭 **전체 테스트** toofinish 것입니다. 드릴 다운 toohello 수 있습니다 **작업** tooperform tootrack 장애 조치가 진행 상황 및 상태에 필요한 모든 작업을 탭 합니다.
6. 장애 조치 후 hello Azure 포털에서에서 가상 컴퓨터 테스트 복제본 hello를 볼 수 있습니다. 온-프레미스 네트워크에서 tooaccess 가상 컴퓨터를 설정 하는 경우 원격 데스크톱 연결 toohello 가상 컴퓨터를 시작할 수 있습니다. 다음 hello지 않습니다.

   1. Hello 가상 컴퓨터가 성공적으로 시작 되는지 확인 합니다.
   2. Hello 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 tooconnect toohello 가상 컴퓨터를 사용 하도록 하려는 경우는 hello 테스트 장애 조치를 실행 하기 전에 hello 가상 컴퓨터에서 원격 데스크톱 연결을 사용 합니다. Hello 가상 컴퓨터에서 RDP 끝점 tooadd를 해야합니다. 활용할 수 있습니다는 [Azure 자동화 Runbook](site-recovery-runbook-automation.md) toodo입니다.
   3. 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 공용 IP 주소 tooconnect toohello 가상 컴퓨터를 사용 하는 경우 확인 tooa 가상 컴퓨터는 공용 주소를 사용 하 여 연결 하지 못하게 하는 모든 도메인 정책 필요가 없습니다.
7. Hello 테스트가 완료 된 후 hello 다음을 수행 합니다.

   * 클릭 **hello 테스트 장애 조치가 완료**합니다. Hello 정리 환경 tooautomatically 전원 끄기 테스트 하 고 hello 테스트 가상 컴퓨터를 삭제 합니다.
   * 클릭 **메모** toorecord hello 테스트 장애 조치와 관련 된 내용을 기록한 후 저장 합니다.


## <a name="next-steps"></a>다음 단계
[복구 계획 설정](site-recovery-create-recovery-plans.md) 및 [장애 조치(failover)](site-recovery-failover.md)에 대해 알아봅니다.
