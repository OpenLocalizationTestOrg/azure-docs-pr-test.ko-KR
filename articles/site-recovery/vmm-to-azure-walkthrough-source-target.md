---
title: "hello 소스 및 대상 Hyper-v 복제 tooAzure (System Center VMM)을 사용한 Azure Site recovery에 대 한를 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 VMM 클라우드에 tooAzure 저장소에서 Hyper-v Vm의 복제에 대 한 원본 및 대상 설정을 hello 단계 tooset을 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>8 단계: hello 소스 및 대상 (VMM)와 Hyper-v 복제 tooAzure에 대 한 설정

후 [자격 증명 모음 만들기](vmm-to-azure-walkthrough-create-vault.md) 지정 하는 tooreplicate,이 문서 tooconfigure 원본을 사용 하 고 System Center Virtual Machine Manager (VMM)의 온-프레미스 Hyper-v 가상 컴퓨터를 복제할 때 대상으로 설정 하 고 hello를 사용 하 여 클라우드 tooAzure, [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

S1. **인프라 준비** > **원본**을 클릭합니다.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. **준비 소스**, 클릭 **+ VMM** tooadd VMM 서버입니다.

    ![원본 설정](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. **서버 추가**, 있는지 여부를 확인 **System Center VMM 서버** 에 표시 **서버 유형** 해당 hello VMM 서버 hello 충족 [필수 구성 요소 및 URL 요구 사항](#prerequisites)합니다.
4. Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.
5. Hello 등록 키를 다운로드 합니다. 설정을 실행할 때 이 키가 필요합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

    ![원본 설정](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Hello VMM 서버에 hello 공급자를 설치 합니다.

1. VMM 서버 hello에 hello 공급자 설정 파일을 실행 합니다.
2. Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.
3. **설치**, 수락 하거나 hello 기본 공급자 설치 위치를 수정 하 고 클릭 **설치**합니다.

    ![설치 위치](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. 설치가 완료 되 면 클릭 **등록** hello 자격 증명 모음에 tooregister hello VMM 서버입니다.
5. Hello에 **자격 증명 모음 설정을** 페이지 **찾아보기** tooselect hello 자격 증명 모음 키 파일입니다. Hello Azure Site Recovery 구독 및 hello 자격 증명 모음 이름을 지정 합니다.

    ![서버 등록](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. **인터넷 연결**, hello VMM 서버에서 실행 중인 공급자는 tooSite 복구를 통해 연결 하는 hello 인터넷 hello 하는 방법을 지정 합니다.

   * Hello 공급자 tooconnect을 직접 하려는 경우 선택 **tooAzure Site Recovery 프록시 없이 직접 연결**합니다.
   * 기존 프록시 인증 필요 또는 사용자 지정 프록시 toouse 하려는 경우 선택 **연결에서 프록시 서버를 사용 하 여 사이트 복구 tooAzure**합니다.
   * 사용자 지정 프록시를 사용 하는 경우 hello 주소, 포트 및 자격 증명을 지정 합니다.
   * 프록시를 사용 하는 경우 해야 이미 허용한에 설명 된 hello Url [필수 구성 요소](#on-premises-prerequisites)합니다.
   * 자동으로 지정 하는 hello를 사용 하 여 VMM RunAs 계정 (DRAProxyAccount) 만들어집니다는 사용자 지정 프록시를 사용 하는 경우 프록시 자격 증명입니다. 이 계정을 올바르게 인증할 수 있도록 hello 프록시 서버를 구성 합니다. VMM RunAs 계정 설정은 hello hello VMM 콘솔에서 수정할 수 있습니다. **설정**를 확장 하 고 **보안** > **실행 계정**, 한 다음 DRAProxyAccount에 대 한 hello 암호를 수정 합니다. 이 설정은 적용 됩니다에 toorestart hello VMM 서비스를 필요 합니다.

     ![인터넷](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. 적용 하거나 데이터 암호화에 자동으로 생성 된 SSL 인증서의 hello 위치를 수정 합니다. 이 인증서는 hello Azure Site Recovery 포털에서 Azure에 의해 보호 되는 클라우드에 대 한 데이터 암호화를 사용 하는 경우에 사용 됩니다. 안전하게 보관해야 합니다. 장애 조치 tooAzure를 실행 하는 경우 해야 toodecrypt, 데이터 암호화를 사용 하는 경우.
8. **서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다. 클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.
9. 사용 하도록 설정 **클라우드 메타 데이터 동기화**hello 자격 증명 모음과 hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용 하려는 경우. 이 작업은 toohappen 각 서버에서 한 번만 필요합니다. Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다. 클릭 **등록** toocomplete hello 프로세스입니다.

    ![서버 등록](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. 등록이 시작됩니다. 등록 완료 되 면 hello 서버에 표시 됩니다 **사이트 복구 인프라** > **VMM 서버**합니다.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Hyper-v 호스트에 hello Azure 복구 서비스 에이전트를 설치 합니다.

1. Hello 공급자를 설정한 후 hello Azure 복구 서비스 에이전트에 대 한 toodownload hello 설치 파일이 필요 합니다. Hello VMM 클라우드의 각 Hyper-v 서버에서 설치 프로그램을 실행 합니다.

    ![Hyper-V 사이트](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. **필수 구성 요소 확인**에서 **다음**을 클릭합니다. 누락된 필수 구성 요소는 자동으로 설치됩니다.

    ![필수 구성 요소 복구 서비스 에이전트](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. **설치 설정**그대로 사용 하거나 hello 설치 위치 및 hello 캐시 위치를 수정 합니다. 5GB 이상의 사용 가능한 저장소에 있는 드라이브에 hello 캐시를 구성할 수 있지만 600 g B 이상의 여유 공간이 있는 드라이브에 캐시 것이 좋습니다. **설치**를 클릭합니다.
4. 설치가 완료 되 면 클릭 **닫기** toofinish 합니다.

    ![MARS 에이전트 등록](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>명령줄 설치
다음 명령을 hello를 사용 하 여 명령줄에서 hello Microsoft Azure 복구 서비스 에이전트를 설치할 수 있습니다.

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>인터넷 프록시 액세스 tooSite Hyper-v 호스트에서 복구를 설정

hello 복구 서비스 에이전트가 Hyper-v 호스트에서 실행 되는 VM 복제에 대 한 인터넷 액세스 tooAzure 필요 합니다. 에 액세스할 때는 hello 인터넷 프록시를 통해이 다음과 같이 설정 합니다.

1. Hello Microsoft Azure 백업 MMC 스냅인에 hello Hyper-v 호스트를 엽니다. 기본적으로 Microsoft Azure 백업에 대 한 바로 가기는 C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 또는 hello 바탕 화면에서 사용할 수 있습니다.
2. Hello 스냅인에서 클릭 **속성 변경**합니다.
3. Hello에 **프록시 구성을** 탭에서 프록시 서버 정보를 지정 합니다.

    ![MARS 에이전트 등록](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. 해당 hello 에이전트 hello에 설명 된 hello Url에 도달할 수 확인 [필수 구성 요소](#on-premises-prerequisites)합니다.

## <a name="set-up-hello-target-environment"></a>Hello 대상 환경 설정
복제에 사용 되는 hello Azure 저장소 계정 toobe를 지정 하 고 hello Azure 네트워크 toowhich Azure Vm 장애 조치 후 연결 됩니다.

1. 클릭 **준비 인프라** > **대상**hello toocreate hello 장애 조치 가상 컴퓨터를 원하는 리소스 그룹을 hello 구독을 선택 합니다. Toouse (기본 또는 리소스 관리) Azure에서 가상 컴퓨터를 조치할 hello에 대 한 원하는 hello 배포 모델을 선택 합니다.

    ![저장소](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.

    ![저장소](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. 저장소 계정을 만들지 않은 toocreate 하나 하려는 경우 리소스 관리자를 사용 하 여 클릭 **저장소 계정 추가** toodo 인라인 있는 합니다.  Hello에 **저장소 계정 만들기** 블레이드 계정 이름, 유형, 구독 및 위치를 지정 합니다. hello 계정 hello에 있어야 합니다. hello와 동일한 위치 복구 서비스 자격 증명 모음입니다.

   ![저장소](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Hello 일반 모델을 사용 하 여 저장소 계정을 toocreate을 원하는 경우 hello Azure 포털에서에서 수행할. [자세히 알아보기](../storage/common/storage-create-storage-account.md)
   * 프리미엄 저장소 계정 복제 된 데이터를 사용 하는 경우 추가 표준 저장소 계정을 설정, toostore 복제 로그를 가져갈 변화 들이 tooon 온-프레미스 데이터를 캡처하는 합니다.
5. Azure 네트워크를 만들지 않은 toocreate 하나 하려는 경우 리소스 관리자를 사용 하 여 클릭 **+ 네트워크** toodo 인라인 있는 합니다. Hello에 **가상 네트워크 만들기** 블레이드 네트워크 이름, 주소 범위, 서브넷 정보, 구독 및 위치를 지정 합니다. hello 네트워크 hello에 있어야 hello와 동일한 위치 복구 서비스 자격 증명 모음입니다.

   ![네트워크](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Hello 일반 모델을 사용 하는 네트워크 toocreate을 원하는 경우 hello Azure 포털에서에서 수행할. [자세히 알아봅니다](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>다음 단계

너무 이동[9 단계: 네트워크 매핑 구성](vmm-to-azure-walkthrough-network-mapping.md)
