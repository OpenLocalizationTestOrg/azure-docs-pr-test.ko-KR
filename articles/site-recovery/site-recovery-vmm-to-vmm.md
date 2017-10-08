---
title: "Azure Site Recovery와 aaaReplicate Hyper-v Vm tooa 보조 사이트 | Microsoft Docs"
description: "Tooreplicate Hyper-v Vm에서 VMM 클라우드 tooa 보조 VMM 사이트를 사용 하 여 Azure 포털을 hello 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>VMM 클라우드 tooa 보조 VMM 사이트에서 hello Azure 포털을 사용 하 여 Hyper-v 가상 컴퓨터 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmm-to-vmm.md)
> * [클래식 포털](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

이 문서에서는 어떻게 tooreplicate 온-프레미스 System Center Virtual Machine Manager (VMM) 클라우드에서 관리 되는 Hyper-v 가상 컴퓨터를 설명 tooa 보조 사이트를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서. 이 [시나리오 아키텍처](site-recovery-components.md)에 대해 자세히 알아봅니다.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="prerequisites"></a>필수 조건

**필수 요소** | **세부 정보**
--- | ---
**Azure** | [Microsoft Azure](http://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. 사이트 복구 가격 책정에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/).
**온-프레미스 VMM** | 두 명의 VMM 서버, hello 기본 사이트와 보조 hello에 각각 하나씩 있는 것이 좋습니다.<br/><br/> 단일 VMM 서버의 클라우드 간에 복제할 수 있습니다.<br/><br/> VMM 서버를 하나 이상 실행 해야 hello 최신 업데이트로 System Center 2012 SP1.<br/><br/> VMM 서버는 인터넷에 연결되어야 합니다.
**VMM 클라우드** | 각 VMM 서버에서 하나 이상의 클라우드가 있어야 하 고 모든 클라우드 hello Hyper-v 용량 프로필이 설정 되어 있어야 합니다. <br/><br/>클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.<br/><br/> 하나의 VMM 서버를만 있는 경우 둘 이상의 클라우드가, tooact를 주 및 보조 필요 합니다.
**Hyper-V** | Hyper-v 서버가 이상 실행 해야 hello Hyper-v 역할을 통해 Windows Server 2012 및 최신 업데이트가 설치 되어 hello 있어야 합니다.<br/><br/> Hyper-V 서버에 VM이 하나 이상 있어야 합니다.<br/><br/>  Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 호스트 그룹에 들어 있어야 합니다.<br/><br/> Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치합니다.<br/><br/> Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Hello 클러스터 브로커를 수동으로 구성 합니다. [자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Hyper-V 서버는 인터넷에 연결되어야 합니다.
**URL** | VMM 서버와 Hyper-v 호스트 수 tooreach 있어야 이러한 Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>배포 단계

다음 항목을 수행합니다.

1. 필수 조건을 확인합니다.
2. Hello VMM 서버와 Hyper-v 호스트를 준비 합니다.
3. Recovery Services 자격 증명 모음을 만듭니다. hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.
4. 원본, 대상 및 복제 설정을 지정합니다.
5. Tooreplicate를 원하는 Vm에서 hello 모바일 서비스를 배포 합니다.
6. 복제를 준비하고 Hyper-V VM에 대한 복제를 활성화합니다.
7. 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>VMM 서버 및 Hyper-V 호스트 준비

배포에 대 한 tooprepare:

1. Hello VMM 서버와 Hyper-v 호스트 hello 위에서 설명한 필수 구성 요소를 준수 하 고 필요한 hello Url에 연결할 수 있는지 확인 합니다.
2. [네트워크 매핑](#network-mapping-overview)을 구성할 수 있도록 VMM 네트워크를 설정합니다.

    - Hello 원본 Hyper-v 호스트 서버에 있는 Vm 연결된 tooa VMM VM 네트워크 인지 확인 합니다. 해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.
    복구를 위해 사용 하는 hello 보조 클라우드 구성 해당 VM 네트워크에 있는지 확인 합니다. 해당 VM 네트워크에 연결 된 tooa hello 보조 클라우드와 연결 된 논리 네트워크 여야 합니다.

3. 에 대 한 준비는 [단일 서버 배포](#single-vmm-server-deployment)hello에 클라우드 간의 tooreplicate Vm 하려는 경우 동일한 VMM 서버입니다.

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기** > **관리** > **Recovery Services**를 차례로 클릭합니다.
3. **이름**, 이름 tooidentify hello 자격 증명 모음을 지정 합니다. 구독이 두 개 이상인 경우 그 중에서 하나를 선택합니다.
4. [리소스 그룹을 만들거나](../azure-resource-manager/resource-group-template-deploy-portal.md) 기존 그룹을 선택합니다. Azure 지역을 지정합니다. 컴퓨터는 복제 된 toothis 영역입니다. 지원 toocheck 지역에서 지역 가용성 참조 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Tooquickly 액세스 hello 자격 증명 모음 대시보드 hello에서 클릭 **Pin toodashboard** > **자격 증명 모음 만들기**합니다.

    ![새 자격 증명 모음](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

hello 새 자격 증명 모음 hello에 나타나는 **대시보드**에 **모든 리소스**, 주 hello에 **복구 서비스 자격 증명 모음** 블레이드입니다.


## <a name="choose-a-protection-goal"></a>보호 목표 선택

기능 선택 tooreplicate를 tooreplicate 하려는 위치 및 원하는 합니다.

2. **Site Recovery** > **1단계: 인프라 준비** > **보호 목표**를 클릭합니다.
3. 선택 **toorecovery 사이트**를 선택 하 고 **Hyper-v와 함께 예,**합니다.
4. 선택 **예** tooindicate VMM toomanage hello Hyper-v 호스트를 사용 하는 합니다.
5. 보조 VMM 서버가 있는 경우 **예**를 선택합니다. 단일 VMM 서버의 클라우드 간에 복제를 배포하는 경우 **아니요**를 클릭합니다. 그런 후 **OK**를 클릭합니다.

    ![목표 선택](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

VMM 서버에 hello Azure Site Recovery Provider를 설치 하 고 검색 및 hello 자격 증명 모음에 서버를 등록 합니다.

1. **1단계: 인프라 준비** > **원본**을 클릭합니다.

    ![원본 설정](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. **준비 소스**, 클릭 **+ VMM** tooadd VMM 서버입니다.

    ![원본 설정](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. **서버 추가**, 있는지 여부를 확인 **System Center VMM 서버** 에 표시 **서버 유형** 해당 hello VMM 서버 hello 충족 [필수구성요소](#prerequisites).
4. Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.
5. Hello 등록 키를 다운로드 합니다. 설정을 실행할 때 이 키가 필요합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

    ![원본 설정](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. VMM 서버 hello에 hello Azure Site Recovery Provider를 설치 합니다. 필요 하지 않습니다 tooexplicitly Hyper-v 호스트 서버에 아무 것도 설치 합니다.


### <a name="install-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery Provider 설치

1. 각 VMM 서버에 hello 공급자 설정 파일을 실행 합니다. VMM 클러스터에 배포 된 hello hello 처음 설치할 때 다음을 수행 합니다.
    -  액티브 노드에서 hello 공급자를 설치 하 고 hello 자격 증명 모음에 hello 설치 tooregister hello VMM 서버를 완료 합니다.
    - 그런 다음 설치 hello 공급자 hello에 다른 노드. 클러스터 노드 hello 실행할지 동일한 버전의 hello 공급자입니다.
2. 설치 프로그램 몇 가지 필수 구성 요소 검사를 실행 하 고 권한 toostop hello VMM 서비스를 요청 합니다. 자동으로 설치가 완료 되 면 hello VMM 서비스에 다시 시작 됩니다. VMM 클러스터를 설치 하는 경우 메시지 표시 toostop hello 클러스터 역할입니다.
3. **Microsoft Update**, 공급자 업데이트가 Microsoft Update 정책에 따라 설치 되어 있는지 toospecify에 선택할 수 있습니다.
4. **설치**, 수락 하거나 hello 기본 설치 위치를 수정 하 고 클릭 **설치**합니다.

    ![설치 위치](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. 설치가 완료 되 면 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.

    ![설치 위치](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. **자격 증명 모음 이름**, hello는 hello 서버를 등록할 자격 증명 모음의 hello 이름이 유효한 지 확인 합니다. *다음*을 누릅니다.

    ![서버 등록](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. **인터넷 연결**, hello VMM 서버에서 실행 되는 hello 공급자 tooAzure를 연결 하는 방법을 지정 합니다.

    ![인터넷 설정](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - 해당 hello 공급자 직접 toohello 연결 되도록 지정할 수 있습니다, 인터넷 또는 프록시를 통해.
   - 필요한 경우 프록시 설정을 지정합니다.
   - VMM RunAs 계정 (DRAProxyAccount) 지정 하는 hello를 사용 하 여 자동으로 만들어집니다 프록시를 사용 하는 경우 프록시 자격 증명입니다. 이 계정을 올바르게 인증할 수 있도록 hello 프록시 서버를 구성 합니다. hello RunAs 계정 설정은 수정할 수 있는 hello VMM 콘솔에서 > **설정** > **보안** > **실행 계정**합니다. VMM 서비스 tooupdate 변경 hello를 다시 시작 합니다.
8. **등록 키**선택, hello 키를 Azure Site Recovery에서 다운로드 한 toohello VMM 서버에 복사 합니다.
9. hello 암호화 설정은 VMM 클라우드에 tooAzure의 Hyper-v Vm을 복제 하는 경우에 사용 됩니다. Tooa 보조 사이트를 복제 하는 사용 되지 않습니다.
10. **서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다. 클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.
11. **클라우드 메타 데이터 동기화**hello 자격 증명 모음과 hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용할지 선택 합니다. 이 작업은 toohappen 각 서버에서 한 번만 필요합니다. Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다.
12. 클릭 **다음** toocomplete hello 프로세스입니다. 등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다. hello 서버 hello에 표시 된 **VMM 서버** hello에 탭 **서버** hello 자격 증명 모음에 페이지입니다.

    ![서버](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Hello 서버 hello Site Recovery 콘솔에서 사용할 수 있게 되에서 **소스** > **준비 소스** hello VMM 서버 및 선택 hello 클라우드에 hello Hyper-v 호스트를 선택 합니다. 그런 후 **OK**를 클릭합니다.

Hello 명령줄에서 hello 공급자를 설치할 수도 있습니다.

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Hello 대상 환경 설정

Hello 대상 VMM 서버와 클라우드를 선택 합니다.

1. 클릭 **준비 인프라** > **대상**, 선택한 toouse 원하는 선택 hello 대상 VMM 서버입니다.
2. Site Recovery와 동기화 된 hello 서버에 클라우드가 표시 됩니다. Hello 대상 클라우드를 선택 합니다.

   ![대상](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>복제 설정 지정

- 복제 정책을 만들 때 정책 hello를 사용 하 여 모든 호스트 해야 합니다는 hello 동일한 운영 체제. v m M 클라우드 hello 서로 다른 버전의 Windows Server를 실행 하는 Hyper-v 호스트를 포함할 수 있으 여러 복제 정책을 경우 해야 합니다.
- Hello 초기 복제 오프 라인으로 수행할 수 있습니다. [자세히 알아보기](#prepare-for-initial-offline-replication)

1. 새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.

    ![네트워크](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. **만들기 및 연결 정책**에서 정책 이름을 지정합니다. hello 소스와 대상 형식이 있어야 **Hyper-v**합니다.
3. **Hyper-v 호스트 버전**를 hello 호스트에서 실행 되는 운영 체제를 선택 합니다.
4. **인증 유형** 및 **인증 포트**, hello 기본 및 복구 Hyper-v 호스트 서버 간의 트래픽을 인증 하는 방법을 지정 합니다. 작동하는 Kerberos 환경이 구성되어 있지 않으면 **인증서** 를 선택합니다. Azure Site Recovery가 HTTPS 인증을 위한 인증서를 자동으로 구성합니다. 않아도 toodo 아무 것도 수동으로 됩니다. 기본적으로 포트 8083 및 8084 (인증서용) hello Hyper-v 호스트 서버에 Windows 방화벽 hello에 열 수는 있습니다. 선택 **Kerberos**, hello 호스트 서버의 상호 인증에는 Kerberos 티켓이 사용 됩니다. 이 설정은 Windows Server 2012 R2에서 실행 중인 Hyper-V 호스트 서버와만 관련이 있습니다.
5. **복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.
6. **복구 지점 보존**, 지정 시간에 시간 hello 보존 기간이 각 복구 지점에 대 한 수입니다. 보호 된 컴퓨터 수 있는 창 내에서 tooany 포인트를 복구 합니다.
7. **앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다. Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다. 응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다. 응용 프로그램 일치 스냅숏을 사용할 경우 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능이 저하 됩니다. 설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.
8. **데이터 전송 압축**에서 전송되는 복제된 데이터를 압축할지 여부를 지정합니다.
9. 선택 **VM 복제본 삭제**, hello 원본 VM에 대 한 보호를 사용 하지 않도록 설정 하는 경우 복제 가상 컴퓨터를 hello toospecify 삭제 되도록 합니다. Hello 소스 hello 사이트 복구 콘솔에서 제거 되는 VM에 대 한 보호를 사용 하지 않도록 설정 하는 경우이 설정을 사용 하면, 사이트 복구 설정이 VMM hello에 대 한는 hello VMM 콘솔에서 제거 되 고 hello 복제본이 삭제 됩니다.
10. **초기 복제 방법**hello 네트워크를 통해 복제 하는 경우, toostart 초기 복제 hello 예약할 하는지 여부를 지정 합니다. toosave 네트워크 대역폭을 tooschedule 할 수 없음 시간 외 것입니다. 그런 후 **OK**를 클릭합니다.

     ![복제 정책](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. 새 정책을 만들 때 hello v m M 클라우드로 자동으로 연결 되어 있습니다. **복제 정책**에서 **확인**을 클릭합니다. 이 복제 정책에 추가 VMM 클라우드에 (및 그 안의 hello Vm) 연결할 수 있습니다 **복제** > 정책 이름 > **VMM 클라우드에 연결**합니다.

     ![복제 정책](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>네트워크 매핑 구성

- 시작하기 전에 [네트워크 매핑](#prepare-for-network-mapping)에 대해 알아봅니다.
- VMM 서버에 가상 컴퓨터가 연결 된 tooa VM 네트워크에 있는지 확인 합니다.


1. **Site Recovery 인프라** > **네트워크 매핑** > **네트워크 매핑**에서 **+네트워크 매핑**을 클릭합니다.

    ![네트워크 매핑](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. **네트워크 매핑을 추가** 탭 hello 소스를 선택 하 고 대상 VMM 서버입니다. hello VMM 서버와 연결 된 hello VM 네트워크가 검색 됩니다.
3. **원본 네트워크**선택, toouse hello 기본 VMM 서버와 연결 된 VM 네트워크의 hello 목록에서 원하는 hello 네트워크입니다.
4. **대상 네트워크**선택, toouse hello 보조 VMM 서버에서 원하는 hello 네트워크입니다. 그런 후 **OK**를 클릭합니다.

    ![네트워크 매핑](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

네트워크 매핑이 시작되면 다음과 같은 동작이 발생합니다.

* Toohello 원본 VM 네트워크에 해당 하는 모든 기존 복제본 가상 컴퓨터에 연결 된 toohello 대상 VM 네트워크 수 있습니다.
* 연결 된 toohello 원본 VM 네트워크는 새 가상 컴퓨터 복제 후 연결 된 toohello 대상 매핑된 네트워크 됩니다.
* 새 네트워크로 기존 매핑을 수정 하는 경우 hello 새 설정을 사용 하 여 복제본 가상 컴퓨터가 연결 됩니다.
* Hello 대상 네트워크에 서브넷이 여러 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제 가상 컴퓨터 장애 조치 후에 대상 서브넷 연결된 toothat 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.

### <a name="configure-storage-mapping"></a>저장소 매핑을 구성합니다.

[저장소 매핑](#prepare-for-storage-mapping) hello 새 Azure 포털에서 지원 되지 않습니다. 그러나 Powershell을 사용하여 활성화할 수 있습니다. [자세히 알아보세요](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping)을 확인하세요.

## <a name="step-5-capacity-planning"></a>5단계: 용량 계획

기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악합니다.

- 다운로드 및 실행 hello [Azure 사이트 복구 Capacity planner](site-recovery-capacity-planner.md), VM 및 각 디스크는 저장소 디스크 복제 환경, Vm을 포함 하는 방법에 대 한 toogather 정보입니다.
- 실시간 복제 정보를 수집 했으면 해당 Vm에 대 한 hello NetQos 정책 toocontrol 복제 대역폭을 수정할 수 있습니다. Thomas Maurer의 블로그에서 [Throttling Hyper-V Replica Traffic(Hyper-V 복제본 트래픽 제한)](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/)을 참조하세요. Hello에 대 한 자세한 정보를 가져올 [New-netqospolicy cmdlet](https://technet.microsoft.com/library/hh967468.aspx.)합니다.

## <a name="enable-replication"></a>복제 활성화

1. **2단계: 응용 프로그램 복제** > **원본**을 클릭합니다. 처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 자격 증명 모음 tooenable 복제 hello에에서 있습니다.

    ![복제 활성화](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. **소스**hello VMM 서버를 선택 하 고 hello 클라우드는 hello tooreplicate 추가할 Hyper-v 호스트 위치 됩니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. **대상**, hello 보조 VMM 서버와 클라우드를 확인 합니다.
4. **가상 컴퓨터**, tooprotect hello 목록에서 원하는 hello Vm을 선택 합니다.

    ![가상 컴퓨터 보호 사용](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Hello의 진행률을 추적할 수 있습니다 **보호 사용** 동작에서 **작업** > **사이트 복구 작업이**합니다. Hello 후 **보호 완료** hello 가상 컴퓨터가 장애 조치에 대해 준비 되었는지, 작업을 완료 합니다.

다음 사항에 유의하세요.

- Hello VMM 콘솔에서 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다. 클릭 **보호 사용** hello 가상 컴퓨터 속성에서 hello 도구 모음 > **Azure Site Recovery** 탭 합니다.
- 복제를 사용 하도록 설정한 후에 VM hello에 대 한 속성을 볼 수 있습니다에 **복제 항목**합니다. Hello에 **Essentials** 대시보드를 hello VM 및 서버 인스턴스의 상태에 대 한 hello 복제 정책에 대 한 정보를 볼 수 있습니다. 자세한 내용을 보려면 **속성** 을 클릭합니다.

### <a name="onboard-existing-virtual-machines"></a>기존 가상 컴퓨터 등록
Hyper-V 복제본을 사용하여 복제 중인 기존 가상 컴퓨터가 VMM에 있는 경우 Azure Site Recovery 복제를 위해 다음과 같이 등록할 수 있습니다.

1. Hello 기존 VM을 호스트 하는 hello Hyper-v 서버 hello 기본 클라우드에 위치한 hello 복제본 가상 컴퓨터를 호스팅하는 hello Hyper-v 서버 hello 보조 클라우드에 있는지 확인 하십시오.
2. 기본 VMM 클라우드 hello에 대 한 복제 정책이 구성 되어 있는지 확인 합니다.
3. Hello 주 가상 컴퓨터에 대 한 복제를 사용 하도록 설정 합니다. Azure 사이트 복구 및 VMM hello 동일한 복제본 호스트 및 가상 컴퓨터가 감지 되는지, 및 Azure 사이트 복구를 다시 사용 hello를 사용 하 여 다시 시작 복제 설정을 지정을 확인 합니다.

## <a name="test-your-deployment"></a>배포 테스트

tootest, 배포를 실행할 수 있습니다는 [테스트 장애 조치](site-recovery-test-failover-vmm-to-vmm.md) 단일 가상 컴퓨터에 대 한 또는 [복구 계획을 만드는](site-recovery-create-recovery-plans.md) 하나 이상의 가상 컴퓨터를 포함 하는 합니다.



## <a name="prepare-for-offline-initial-replication"></a>오프라인 초기 복제 준비

Hello 초기 데이터 복사본에 대 한 오프 라인 복제를 수행할 수 있습니다. 이 작업은 다음과 같이 준비할 수 있습니다.

* Hello 원본 서버에 있는 hello에서 데이터 내보내기가 수행 될 경로 위치를 지정 합니다. Hello 내보내기 경로에 VMM 서비스 toohello NTFS 및 공유 사용 권한에 대 한 모든 권한을 할당 합니다. Hello 대상 서버 hello 데이터를 가져올 경로 위치를 실시할 지정 합니다. Hello이 가져오기 경로에 동일한 권한을 할당 합니다.
* 경우 hello 가져오기 또는 내보내기 경로가 공유 된, hello 원격 컴퓨터에서 hello VMM 서비스 계정에 대 한 관리자, Power User, Print Operator 또는 Server Operator 그룹 멤버 자격 할당 공유 하는 hello에 있습니다.
* 모든 실행 계정 tooadd 호스트를 사용 하 여 hello에 가져오기 및 내보내기 경로, 할당 읽기 및 쓰기 권한이 toohello 실행 계정을 VMM에서.
* 공유 내보내기 및 가져오기 hello Hyper-v에서 루프백 구성을 지원 되지 않으므로 Hyper-v 호스트 서버로 사용 되는 모든 컴퓨터에 배치할 수 해야 합니다.
* 원하는 tooprotect, 가상 컴퓨터가 포함 된 각 Hyper-v 호스트 서버에서 Active Directory에서 사용 하도록 설정 하 고 제한 된 위임 tootrust hello 원격 컴퓨터는 hello 가져오기 및 내보내기에 경로 다음과 같이 구성 합니다.
  1. Hello 도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**합니다.
  2. Hello 콘솔 트리에서 클릭 **DomainName** > **컴퓨터**합니다.
  3. 마우스 오른쪽 단추로 클릭 hello Hyper-v 호스트 서버 이름 > **속성**합니다.
  4. Hello에 **위임** 탭을 클릭 **toospecified 서비스에만 위임에 대 한이 컴퓨터 트러스트**합니다.
  5. **모든 인증 프로토콜 사용**을 클릭합니다.
  6. **추가** > **사용자 및 컴퓨터**에 문의하세요.
  7. Hello 내보내기 경로 호스트 하는 hello 컴퓨터의 형식 hello 이름 > **확인**합니다. Hello 사용 가능한 서비스 목록에서 hello CTRL 키를 누른 채 클릭 **cifs** > **확인**합니다. Hello 컴퓨터의 이름을 hello에 대 한 해당 호스트 hello 가져오기 경로 반복 합니다. 필요에 따라 추가 Hyper-V 호스트 서버에 대해 반복합니다.



## <a name="prepare-for-network-mapping"></a>네트워크 매핑을 준비
네트워크 매핑은 hello 기본 및 보조 VMM 서버를 VMM VM 네트워크 간에 매핑됩니다.

* 장애 조치(Failover) 후 보조 Hyper-V 호스트에 복제본 VM을 최적으로 배치합니다.
* 장애 조치 후 복제 Vm tooappropriate VM 네트워크를 연결 합니다.

다음 사항에 유의하세요.
- 네트워크 매핑은 두 명의 VMM 서버의 VM 네트워크 간 구성할 수 있습니다 또는 단일 VMM 서버에서 두 사이트에서 관리 하는 경우 환영 동일 서버.
- 매핑이 올바르게 구성 되 고 복제가 설정 되어 hello 기본 위치의 VM에 연결 된 tooa 네트워크 됩니다와 hello 대상 위치의 복제본 연결 될 네트워크 tooits에 매핑됩니다.
- 네트워크가 올바르게 설정 되었는지, VMM에서 네트워크 매핑 중 대상 VM 네트워크를 선택 하면, hello 원본 VM 네트워크를 사용 하는 hello VMM 원본 클라우드가 표시 됩니다, hello에 사용 되는 hello 대상 클라우드가 사용 가능한 대상 VM 네트워크와 함께 보호 합니다.
- Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.


다음 예에서는 tooillustrate은이 메커니즘입니다. 뉴욕과 시카고 두 위치에 있는 조직을 보겠습니다.

| **위치** | **VMM 서버** | **VM 네트워크** | **다음으로 매핑** |
| --- | --- | --- | --- |
| 뉴욕 |VMM-뉴욕 |VMNetwork1-뉴욕 |TooVMNetwork1-시카고와 매핑된 |
| VMNetwork2-뉴욕 |매핑되지 않음 | | |
| 시카코 |VMM-시카고 |VMNetwork1-시카고 |매핑된 tooVMNetwork1-뉴욕 |
| VMNetwork2-시카고 |매핑되지 않음 | | |

이 예제에서:

* 연결 된 tooVMNetwork1-뉴욕에 있는 모든 가상 컴퓨터에 대 한 복제 가상 컴퓨터를 만들면 tooVMNetwork1-시카고와 연결된 됩니다.
* VMNetwork2-뉴욕 또는 VMNetwork2-시카고에 대 한 복제 가상 컴퓨터를 만들면 연결된 tooany 네트워크 되지 않습니다.

예제 조직에 hello 논리 네트워크 hello 클라우드와 연결 된 VMM 클라우드가 설정 되어 방법을 다음과 같습니다.

### <a name="cloud-protection-settings"></a>클라우드 보호 설정
| **보호된 클라우드** | **클라우드 보호** | **논리 네트워크(뉴욕)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>해당 없음</p><p></p> |<p>LogicalNetwork1-뉴욕</p><p>LogicalNetwork1-시카고</p> |
| SilverCloud2 |<p>해당 없음</p><p></p> |<p>LogicalNetwork1-뉴욕</p><p>LogicalNetwork1-시카고</p> |

### <a name="logical-and-vm-network-settings"></a>논리 및 VM 네트워크 설정
| **위치** | **논리 네트워크** | **연결된 VM 네트워크** |
| --- | --- | --- |
| 뉴욕 |LogicalNetwork1-뉴욕 |VMNetwork1-뉴욕 |
| 시카코 |LogicalNetwork1-시카고 |VMNetwork1-시카고 |
| LogicalNetwork2Chicago |VMNetwork2-시카고 | |

### <a name="target-networks"></a>대상 네트워크
Hello 대상 VM 네트워크를 선택 하면 이러한 설정에 따라 hello 다음 표에서 사용할 수 있는 hello 선택 항목을 표시 합니다.

| **선택** | **보호된 클라우드** | **클라우드 보호** | **사용 가능한 대상 네트워크** |
| --- | --- | --- | --- |
| VMNetwork1-시카고 |SilverCloud1 |SilverCloud2 |사용 가능 |
| GoldCloud1 |GoldCloud2 |사용 가능 | |
| VMNetwork2-시카고 |SilverCloud1 |SilverCloud2 |사용할 수 없음 |
| GoldCloud1 |GoldCloud2 |사용 가능 | |


### <a name="failback"></a>장애 복구
장애 복구 (역방향 복제)의 hello 경우 어떤 일이 생기 toosee VMNetwork1-뉴욕 매핑된 tooVMNetwork1-시카고와 설정을 다음 hello로 인지를 가정해 보겠습니다.

| **가상 컴퓨터** | **연결 된 tooVM 네트워크** |
| --- | --- |
| VM1 |VMNetwork1-네트워크 |
| VM2(VM1의 복제) |VMNetwork1-시카고 |

이러한 설정을 사용하여 몇 가지 가능한 시나리오에서 발생하는 결과를 검토해 보겠습니다.

| **시나리오** | **결과** |
| --- | --- |
| 장애 조치 후 v M-2의 hello 네트워크 속성 변경 되지 않습니다. |V M-1에 연결 된 toohello 원본 네트워크 유지 됩니다. |
| 장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되고 연결이 끊김 |VM-1의 연결이 끊김 |
| V M-2의 네트워크 속성은 장애 조치 후 변경 되 고 tooVMNetwork2-시카고와 연결된 됩니다. |VMNetwork2-시카고가 매핑되지 않는 경우 VM-1의 연결이 끊김 |
| VMNetwork1-시카고의 네트워크 매핑이 변경됨 |V M-1에 연결 된 toohello 매핑된 네트워크와 지금 tooVMNetwork1-시카고 됩니다. |


## <a name="prepare-for-single-server-deployment"></a>단일 서버 배포 준비


단일 VMM 서버를만 있는 경우 복제 하는 Vm hello VMM 클라우드에 있는 Hyper-v 호스트에서 너무[Azure](site-recovery-vmm-to-azure.md) 또는 tooa 보조 VMM 클라우드입니다. 클라우드 간의 복제 원활 하 게 아니어서 hello 첫 번째 옵션을 좋습니다. 스트레치 된 Windows 클러스터에 배포 된 단일 VMM 서버 또는 단일 독립 실행형 VMM 서버와 클라우드 간의 tooreplicate 않도록 하려는 경우 복제할 수 있습니다.

### <a name="standalone-vmm-server"></a>독립 실행형 VMM 서버

이 시나리오에서는 hello 기본 사이트에서 가상 컴퓨터로 hello 단일 VMM 서버를 배포 하 고 Site Recovery 및 Hyper-v 복제본을 사용 하 여이 VM tooa 보조 사이트를 복제 합니다.

1. **Hyper-V VM에 VMM을 설정합니다**. Hello에 VMM에서 사용 하는 hello SQL Server 인스턴스를 배치 하는 것이 동일한 VM입니다. 하나의 VM에 만든 toobe 시간이 절약 됩니다. SQL Server의 원격 인스턴스 toouse 원하고 중단이 발생 한 경우 있어야만 toorecover 해당 인스턴스에 VMM을 복구할 수 있습니다.
2. **Hello VMM 서버에 둘 이상의 클라우드가 구성 되어 있는지 확인**합니다. 한 클라우드 hello hello 보조 위치로 사용할 tooreplicate을 다른 클라우드 hello Vm이 포함 됩니다. tooprotect 준수 해야 하는 것이 원하는 hello Vm이 포함 된 클라우드 hello [필수 구성 요소](#prerequisites)합니다.
3. 이 문서에 설명된 대로 Site Recovery를 설정합니다. 만들기 및 자격 증명 모음에 hello VMM 서버를 등록, 복제 정책을 설정 및 복제를 사용 하도록 설정 합니다. hello 원본 및 대상 VMM 이름은 같은 hello 됩니다. Hello 네트워크를 통해 초기 복제 발생을 지정 합니다.
4. 네트워크 매핑을 설정할 때 hello VM 네트워크를 보조 클라우드 hello에 대 한 hello 기본 클라우드 toohello VM 네트워크를 매핑합니다.
5. Hello Hyper-v Manager 콘솔에서 VMM VM hello를 포함 하는 hello Hyper-v 호스트에서 Hyper-v 복제본을 사용 하도록 설정 하 고 hello VM에 복제를 사용 합니다. Hyper-v 복제본 설정을 Site Recovery에 의해 재정의 되지 tooensure Site Recovery로 보호 되는 hello VMM 가상 컴퓨터 tooclouds 추가 하지 않으면 있는지 확인 합니다.
6. 사용 하는 장애 조치에 대 한 복구 계획을 만드는 경우 원본에 대 한 동일한 VMM 서버 hello 및 대상 합니다.
7. 전체 가동 중단 시 다음과 같이 장애 조치를 수행하고 복구합니다.

   1. Hello Hyper-v 관리자 콘솔의 hello 기본 VMM VM toohello 보조 사이트를 통해 toofail hello 보조 사이트에서 계획 되지 않은 장애 조치를 실행 합니다.
   2. VMM VM이 위쪽 해당 hello를 확인 하 고 실행 되 고 hello 자격 증명 모음에서 실행 계획 되지 않은 장애 조치 toofail hello Vm을 통해 기본 toosecondary 클라우드에서 키를 누릅니다. Hello 장애 조치 커밋 및 필요한 경우 대체 복구 지점을 선택 합니다.
   3. Hello 계획 되지 않은 장애 조치가 완료 되 면 리소스를 모두 액세스할 수 있습니다 hello 기본 사이트에서 다시.
   4. Hello 기본 사이트를 hello Hyper-v 관리자 콘솔의 hello 보조 사이트에서 다시 사용할 수 있는 VMM VM hello에 대 한 역방향 복제를 사용 하도록 설정 합니다. 이 보조 tooprimary에서 VM hello에 대 한 복제를 시작합니다.
   5. Hello Hyper-v 관리자 콘솔의 hello VMM VM toohello 기본 사이트를 통해 toofail hello 보조 사이트에서 계획된 된 장애 조치를 실행 합니다. Hello 장애 조치를 커밋하십시오. Hello VMM VM은 다시에서 복제할 primary toosecondary 있도록 역방향 복제를 사용 합니다.
   6. Hello 복구 서비스 자격 증명 모음에 hello 작업 부하 Vm의 경우 보조 tooprimary에서 복제 하지 toostart 역방향 복제를 설정 합니다.
   7. Hello 복구 서비스 자격 증명 모음에, 계획 된 장애 조치 toofail 백 hello 작업 부하 Vm toohello 기본 사이트를 실행 합니다. 커밋 장애 조치 toocomplete hello 것입니다. 역방향 복제 toostart 복제 hello 작업 부하 Vm 기본 toosecondary에서 사용 하도록 설정 합니다.

### <a name="stretched-vmm-cluster"></a>늘어난 VMM 클러스터

배포 tooa 보조 사이트를 복제 하는 VM으로 독립 실행형 VMM 서버를 배포 하는 대신 VMM 항상 사용 가능 하 게 만들 하는 Windows 장애 조치 클러스터에서 VM으로 배포 하 여 수 있습니다. 그러면 워크로드 복원력이 제공되고 하드웨어 장애로부터 보호됩니다. 사이트 복구 hello VMM VM로 toodeploy 지리적으로 분산 된 사이트에 걸쳐 늘이기 클러스터에 배포 되어야 합니다. toodo이:

1. Windows 장애 조치 클러스터에서 가상 컴퓨터에 VMM을 설치 하 고 설치 하는 동안 항상 사용 가능 hello 옵션 toorun hello 서버를 선택 합니다.
2. VMM에서 사용 되는 hello SQL Server 인스턴스에 hello hello 보조 사이트에는 데이터베이스의 복제본이 되도록 SQL Server AlwaysOn 가용성 그룹이 포함 된 복제 되어야 합니다.
3. 이 문서 toocreate 자격 증명 모음에에서 hello 지침, hello 서버를 등록 하 고 보호를 설정 합니다. 각 VMM 서버 hello에 hello 복구 서비스 자격 증명 모음에 있는 클러스터 tooregister가 필요 합니다. toodo이를 액티브 노드에서 hello 공급자를 설치 하 고 hello VMM 서버를 등록 합니다. 그런 다음 다른 노드에서 hello 공급자를 설치합니다.
4. 중단이 발생할 때 hello VMM 서버와 해당 SQL Server 데이터베이스, 장애 조치 되며 hello 보조 사이트에서 액세스 합니다.



## <a name="prepare-for-storage-mapping"></a>저장소 매핑 준비


저장소 설정 매핑하여 매핑 저장소 분류를 원본에서 및 대상 VMM 서버 toodo hello 다음:

  * **복제본 가상 컴퓨터에 대해 대상 저장소를 식별**-원본 VM 하드 디스크는 복제 지정한 toohello 저장소 (SMB 공유 또는 클러스터 공유 볼륨 (Csv)) hello 대상 위치에 있습니다.
  * **복제본 가상 컴퓨터 배치**-저장소 매핑을 Hyper-v 호스트 서버에 사용 되는 toooptimally 전체 복제본 가상 컴퓨터. 복제본 가상 컴퓨터는 매핑된 hello 저장소 분류를 액세스할 수 있는 호스트에 배치 됩니다.
  * **저장소 매핑이 없는**-저장소 매핑을 구성 하지 않는 경우 가상 컴퓨터 복제 toohello 기본 저장소 위치 hello 복제 가상 컴퓨터와 관련 된 hello Hyper-v 호스트 서버에 지정 된 됩니다.

다음 사항에 유의하세요.
- 단일 서버에 두 VMM 클라우드 간의 매핑을 설정할 수 있습니다.
- 저장소 분류에는 소스 및 대상 클라우드에 있는 사용 가능한 toohello 호스트 그룹 이어야 합니다.
- 분류 필요 하지 않은 toohave hello 같은 유형의 저장소입니다. 예를 들어 Csv를 포함 하는 SMB 공유 tooa 대상 분류를 포함 하는 원본 분류를 매핑할 수 있습니다.

### <a name="example"></a>예제
분류는 저장소 매핑 중 hello 원본 및 대상 VMM 서버를 선택 하면 VMM에서 제대로 구성 되어, hello 원본 및 대상 분류 표시 됩니다. 저장소 파일 공유 및 뉴욕과 시카고 두 위치에 있는 조직에 대한 분류의 예는 다음과 같습니다.

| **위치** | **VMM 서버** | **파일 공유(원본)** | **분류(원본)** | **다음으로 매핑** | **파일 공유(대상)** |
| --- | --- | --- | --- | --- | --- |
| 뉴욕 |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| 시카코 |VMM_Target | |GOLD_TARGET |매핑되지 않음 | |
|  |SILVER_TARGET |매핑되지 않음 | | | |
|  |BRONZE_TARGET |매핑되지 않음 | | | |

이 예제에서:

* "Gold" 저장소 (SourceShare1)의 가상 컴퓨터에 대 한 복제 가상 컴퓨터를 만들면 복제 tooa gold_target의 임의 위치 저장소 (TargetShare1) 됩니다.
* 은색 저장소 (SourceShare2)의 가상 컴퓨터에 대 한 복제 가상 컴퓨터를 만들면 복제 tooa SILVER_TARGET (TargetShare2) 저장 되 고 등입니다.

### <a name="multiple-storage-locations"></a>여러 저장소 위치
Toomultiple SMB 공유 또는 Csv hello 대상 분류 할당 되 면 hello 가상 컴퓨터가 보호 되 면 hello 가장 적합 한 저장 위치가 자동으로 선택 됩니다. 적절 한 대상 저장소를 사용 하지는 사용할 수 경우 hello hello 기본 분류를 지정 하는 hello Hyper-v 호스트에서 지정한 저장소 위치는 사용 되는 tooplace hello 복제본 가상 하드 디스크입니다.

다음 표에 hello 어떻게 저장소 분류 및 클러스터 공유 볼륨에서에서 설정 하는 예제를 보여 줍니다.

| **위치**: | **분류** | **관련 저장소** |
| --- | --- | --- |
| 뉴욕 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| 시카코 |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

이 표에서이 예에서는 환경에서 가상 컴퓨터 (v m 1-VM5)에 대 한 보호를 사용 하도록 설정 하면 hello 동작을 요약 합니다.

| **가상 컴퓨터** | **원본 저장소** | **원본 분류** | **매핑되는 대상 저장소** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Both GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Both GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Both SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |해당 없음 |Hello Hyper-v 호스트의 hello 기본 저장소 위치를 사용 하므로 매핑이 없습니다 |



### <a name="data-privacy-overview"></a>데이터 프라이버시 개요

이 표는 이 시나리오에서 데이터가 저장되는 방법을 보여 줍니다.

- - -
| 작업 | **세부 정보** | **수집된 데이터** | **사용** | **필수** |
| --- | --- | --- | --- | --- |
| **등록** | 복구 서비스 자격 증명 모음에 VMM 서버를 등록합니다. Toounregister 서버를 나중에 원하는 경우 hello Azure 포털에서에서 hello 서버 정보를 삭제 하 여 그렇게 할 수 있습니다. | VMM 서버를 등록 한 후 사이트 복구 수집, 처리 하 고 hello VMM 서버 및 사이트 복구에서 검색 하는 hello VMM 클라우드의 hello 이름에 대 한 메타 데이터를 전송 합니다. | hello 데이터 사용된 tooidentify의 hello 적절 한 VMM 서버와 통신 및 적절 한 VMM 클라우드에 대 한 설정을 구성 합니다. | 이 기능은 필수입니다. Toosend이 정보 tooSite 복구 않으려는 경우 hello Site Recovery 서비스를 사용 하지 않아야 합니다. |
| **복제 활성화** | hello Azure Site Recovery Provider hello VMM 서버에 설치 되며 hello 통로 hello Site Recovery 서비스와의 통신에 있습니다. hello 공급자는 hello VMM 프로세스에서 호스트 되는 동적 연결 라이브러리 (DLL)입니다. 공급자가 설치 되어 hello, 후 hello VMM 관리자 콘솔에서 hello "데이터 센터 복구" 기능이 설정 됩니다. 신규 및 기존 Vm의 VM에 대 한이 기능 tooenable 보호를 설정할 수 있습니다. |이 속성이 설정 된 hello 공급자 hello VM tooSite 복구의 hello 이름 및 ID를 보냅니다.  Windows Server 2012 또는 Windows Server 2012 R2 Hyper-V 복제본을 통해 복제를 사용할 수 있습니다. hello 가상 컴퓨터 데이터는 하나의 Hyper-v 호스트 tooanother (일반적으로 다른 "복구" 데이터 센터에 있음)에서 복제를 가져옵니다. |Hello 메타 데이터 toopopulate hello VM 정보를 사용 하 여 hello Azure 포털에서에서 사이트 복구 합니다. | 이 기능은 hello 서비스의 필수 요소 이며 해제할 수 없습니다. 않으려면 toosend이이 정보를 Vm에 대 한 사이트 복구 보호를 사용 하지 마십시오. Note hello 공급자 tooSite 복구에서 보내는 모든 데이터 HTTPS를 통해 전송 됩니다. |
| **복구 계획** | 복구 계획 hello 복구 데이터 센터에 대 한 오케스트레이션 계획을 작성 하는 데 도움이 됩니다. Hello 시작 순서를 Vm 또는 가상 컴퓨터의 그룹 해야 수 hello 복구 사이트에서 정의할 수 있습니다. 를 실행 하는 자동화 된 스크립트 toobe 또는 각 VM에 대 한 복구의 hello 시점에 생성 된 모든 수동 작업 toobe 지정할 수 있습니다. 장애 조치는 일반적으로 조정 된 복구에 대 한 hello 복구 계획 수준에서 발생 합니다. | 사이트 복구 수집, 처리 및 가상 컴퓨터 메타 데이터 및 자동화 스크립트 및 수동 작업 메모의 메타 데이터를 포함 하 여 hello 복구 계획에 대 한 메타 데이터를 전송 합니다. |hello 메타 데이터는 hello Azure 포털에서에서 사용 되는 toobuild hello 복구 계획 합니다. |이 기능은 hello 서비스의 필수 요소 이며 해제할 수 없습니다. 않으려면 toosend이 정보 tooSite 복구, 복구 계획을 만들지 마십시오. |
| **네트워크 매핑** | 지도는 hello 주 데이터 센터 toohello 복구 데이터 센터에서 정보를 네트워크입니다. Hello 복구 사이트에서 복구 Vm 네트워크 매핑 네트워크 연결을 만드는 데 해줍니다. |사이트 복구 수집, 처리 및 hello (주 파일 그룹 및 데이터 센터)에 각 사이트에 대 한 논리 네트워크의 hello 메타 데이터를 전송 합니다. |hello 메타 데이터에는 사용 되는 toopopulate 네트워크 설정 되므로 hello 네트워크 정보를 매핑할 수 있습니다. | 이 기능은 hello 서비스의 필수 요소 이며 해제할 수 없습니다. 않으려면 toosend이 정보 tooSite 복구, 네트워크 매핑을 사용 하지 마십시오. |
| **장애 조치(계획됨/계획되지 않음/테스트)** | 장애 조치 한 VMM에서 관리 하는 데이터 센터 tooanother에서 Vm을 통해 실패합니다. hello 장애 조치 동작이 hello Azure 포털에서에서 수동으로 트리거됩니다. |hello VMM 서버에 공급자 hello는 Site Recovery에 의해 hello 장애 조치 이벤트 알림이 전송 되 고 VMM 인터페이스를 통해 hello Hyper-v 호스트에서 장애 조치 작업을 실행 합니다. VM의 실제 장애 조치 한 Hyper-v 호스트 tooanother는 이며 Windows Server 2012 또는 Windows Server 2012 R2 Hyper-v 복제본에 의해 처리입니다. 사이트 복구 aft hello Azure 포털에서에서 toopopulate hello 상태의 hello 장애 조치 동작 정보를 전송 하는 hello 정보를 사용 합니다. | 이 기능은 hello 서비스의 필수 요소 이며 해제할 수 없습니다. Toosend이 정보 tooSite 복구를 원하지 장애 조치를 사용 하지 마십시오. |

## <a name="next-steps"></a>다음 단계

Hello 배포를 테스트 한 후에 대 한 자세한 다른 종류의 [장애 조치](site-recovery-failover.md)
