---
title: "hello 소스 및 대상에 Azure 사이트 복구와 Hyper-v 복제 tooa 보조 사이트를 aaaSet | Microsoft Docs"
description: "어떻게 tooset hello 소스 및 대상 때 설명 Azure Site Recovery와 VMM toosecondary 사이트 Hyper-v Vm을 복제 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>6 단계: hello 복제 원본 및 대상 설정


Hyper-v 복제 tooa 보조 VMM 사이트에 대 한 자격 증명 모음 복구 서비스를 만든 후 [Azure Site Recovery](site-recovery-overview.md),이 문서 tooset hello 소스를 사용 하 고 복제 위치 대상입니다. 

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.




## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

VMM 서버에 hello Azure Site Recovery Provider를 설치 하 고 검색 및 hello 자격 증명 모음에 서버를 등록 합니다.

1. **1단계: 인프라 준비** > **원본**을 클릭합니다.

    ![원본 설정](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. **준비 소스**, 클릭 **+ VMM** tooadd VMM 서버입니다.

    ![원본 설정](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. **서버 추가**, 있는지 여부를 확인 **System Center VMM 서버** 에 표시 **서버 유형** 해당 hello VMM 서버 hello 충족 [필수구성요소](#prerequisites).
4. Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.
5. Hello 등록 키를 다운로드 합니다. 설정을 실행할 때 이 키가 필요합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

    ![원본 설정](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. VMM 서버 hello에 hello Azure Site Recovery Provider를 설치 합니다. 필요 하지 않습니다 tooexplicitly Hyper-v 호스트 서버에 아무 것도 설치 합니다.


## <a name="install-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery Provider 설치

1. 각 VMM 서버에 hello 공급자 설정 파일을 실행 합니다. VMM 클러스터에 배포 된 hello hello 처음 설치할 때 다음을 수행 합니다.
    -  액티브 노드에서 hello 공급자를 설치 하 고 hello 자격 증명 모음에 hello 설치 tooregister hello VMM 서버를 완료 합니다.
    - 그런 다음 설치 hello 공급자 hello에 다른 노드. 클러스터 노드 hello 실행할지 동일한 버전의 hello 공급자입니다.
2. 설치 프로그램 몇 가지 필수 구성 요소 검사를 실행 하 고 권한 toostop hello VMM 서비스를 요청 합니다. 자동으로 설치가 완료 되 면 hello VMM 서비스에 다시 시작 됩니다. VMM 클러스터를 설치 하는 경우 메시지 표시 toostop hello 클러스터 역할입니다.
3. **Microsoft Update**, 공급자 업데이트가 Microsoft Update 정책에 따라 설치 되어 있는지 toospecify에 선택할 수 있습니다.
4. **설치**, 수락 하거나 hello 기본 설치 위치를 수정 하 고 클릭 **설치**합니다.

    ![설치 위치](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. 설치가 완료 되 면 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.

    ![설치 위치](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. **자격 증명 모음 이름**, hello는 hello 서버를 등록할 자격 증명 모음의 hello 이름이 유효한 지 확인 합니다. *다음*을 누릅니다.

    ![서버 등록](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. **인터넷 연결**, hello VMM 서버에서 실행 되는 hello 공급자 tooAzure를 연결 하는 방법을 지정 합니다.

    ![인터넷 설정](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - 해당 hello 공급자 직접 toohello 연결 되도록 지정할 수 있습니다, 인터넷 또는 프록시를 통해.
   - 필요한 경우 프록시 설정을 지정합니다.
   - VMM RunAs 계정 (DRAProxyAccount) 지정 하는 hello를 사용 하 여 자동으로 만들어집니다 프록시를 사용 하는 경우 프록시 자격 증명입니다. 이 계정을 올바르게 인증할 수 있도록 hello 프록시 서버를 구성 합니다. hello RunAs 계정 설정은 수정할 수 있는 hello VMM 콘솔에서 > **설정** > **보안** > **실행 계정**합니다. VMM 서비스 tooupdate 변경 hello를 다시 시작 합니다.
8. **등록 키**선택, hello 키를 Azure Site Recovery에서 다운로드 한 toohello VMM 서버에 복사 합니다.
9. hello 암호화 설정은 VMM 클라우드에 tooAzure의 Hyper-v Vm을 복제 하는 경우에 사용 됩니다. Tooa 보조 사이트를 복제 하는 사용 되지 않습니다.
10. **서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다. 클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.
11. **클라우드 메타 데이터 동기화**hello 자격 증명 모음과 hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용할지 선택 합니다. 이 작업은 toohappen 각 서버에서 한 번만 필요합니다. Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다.
12. 클릭 **다음** toocomplete hello 프로세스입니다. 등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다. hello 서버 hello에 표시 된 **VMM 서버** hello에 탭 **서버** hello 자격 증명 모음에 페이지입니다.

    ![서버](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Hello 서버 hello Site Recovery 콘솔에서 사용할 수 있게 되에서 **소스** > **준비 소스** hello VMM 서버 및 선택 hello 클라우드에 hello Hyper-v 호스트를 선택 합니다. 그런 후 **OK**를 클릭합니다.

Hello 명령줄에서 hello 공급자를 설치할 수도 있습니다.

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Hello 대상 환경 설정

Hello 대상 VMM 서버와 클라우드를 선택 합니다.

1. 클릭 **준비 인프라** > **대상**, 선택한 toouse 원하는 선택 hello 대상 VMM 서버입니다.
2. Site Recovery와 동기화 된 hello 서버에 클라우드가 표시 됩니다. Hello 대상 클라우드를 선택 합니다.

   ![대상](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>다음 단계

너무 이동[7 단계: 네트워크 매핑을 구성](vmm-to-vmm-walkthrough-network-mapping.md)합니다.
