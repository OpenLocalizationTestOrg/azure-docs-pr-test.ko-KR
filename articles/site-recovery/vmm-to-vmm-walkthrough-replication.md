---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 사이트에 대 한 복제 정책을 aaaSet | Microsoft Docs"
description: "어떻게 복제 tooa Hyper-v VM에 대 한 정책을 tooset 보조 VMM 인 사이트를 Azure Site Recovery에 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>8단계: 복제 정책 설정

구성한 후 [네트워크 매핑을](vmm-to-vmm-walkthrough-network-mapping.md), Hyper-v 가상 컴퓨터 (VM) 복제 tooa 보조 사이트에 대 한이 문서 tooset 복제 정책을 사용 하 여 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="before-you-start"></a>시작하기 전에

- 복제 정책을 만들 때 hello 정책을 사용 하 여 모든 호스트 해야 합니다는 hello 동일한 운영 체제입니다. v m M 클라우드 hello 서로 다른 버전의 Windows Server를 실행 하는 Hyper-v 호스트를 포함할 수 있으 여러 복제 정책을 경우 해야 합니다.
- Hello 초기 복제 오프 라인으로 수행할 수 있습니다.

## <a name="configure-replication-settings"></a>복제 설정 구성

1. 새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.

    ![네트워크](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. **만들기 및 연결 정책**에서 정책 이름을 지정합니다. hello 소스와 대상 형식이 있어야 **Hyper-v**합니다.
3. **Hyper-v 호스트 버전**를 hello 호스트에서 실행 되는 운영 체제를 선택 합니다.
4. **인증 유형** 및 **인증 포트**, hello 기본 및 복구 Hyper-v 호스트 서버 간의 트래픽을 인증 하는 방법을 지정 합니다. 작동하는 Kerberos 환경이 구성되어 있지 않으면 **인증서** 를 선택합니다. Azure Site Recovery가 HTTPS 인증을 위한 인증서를 자동으로 구성합니다. 않아도 toodo 아무 것도 수동으로 됩니다. 기본적으로 포트 8083 및 8084 (인증서용) hello Hyper-v 호스트 서버에 Windows 방화벽 hello에 열 수는 있습니다. 선택 **Kerberos**, hello 호스트 서버의 상호 인증에는 Kerberos 티켓이 사용 됩니다. 이 설정은 Windows Server 2012 R2에서 실행 중인 Hyper-V 호스트 서버와만 관련이 있습니다.
5. **복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.
6. **복구 지점 보존**, 지정 시간에 시간 hello 보존 기간이 각 복구 지점에 대 한 수입니다. 보호 된 컴퓨터 수 있는 창 내에서 tooany 포인트를 복구 합니다.
7. **앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다. Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다. 응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다. 응용 프로그램 일치 스냅숏을 사용할 경우 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능이 저하 됩니다. 설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.
8. **데이터 전송 압축**에서 전송되는 복제된 데이터를 압축할지 여부를 지정합니다.
9. 선택 **VM 복제본 삭제**, hello 원본 VM에 대 한 보호를 사용 하지 않도록 설정 하는 경우 복제 가상 컴퓨터를 hello toospecify 삭제 되도록 합니다. Hello 소스 hello 사이트 복구 콘솔에서 제거 되는 VM에 대 한 보호를 사용 하지 않도록 설정 하는 경우이 설정을 사용 하면, 사이트 복구 설정이 VMM hello에 대 한는 hello VMM 콘솔에서 제거 되 고 hello 복제본이 삭제 됩니다.
10. **초기 복제 방법**hello 네트워크를 통해 복제 하는 경우, toostart 초기 복제 hello 예약할 하는지 여부를 지정 합니다. toosave 네트워크 대역폭을 tooschedule 할 수 없음 시간 외 것입니다. 그런 후 **OK**를 클릭합니다.

     ![복제 정책](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. 새 정책을 만들 때 hello v m M 클라우드로 자동으로 연결 되어 있습니다. **복제 정책**에서 **확인**을 클릭합니다. 이 복제 정책에 추가 VMM 클라우드에 (및 그 안의 hello Vm) 연결할 수 있습니다 **복제** > 정책 이름 > **VMM 클라우드에 연결**합니다.

     ![복제 정책](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



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



## <a name="next-steps"></a>다음 단계

너무 이동[9 단계: 복제 사용](vmm-to-vmm-walkthrough-enable-replication.md)합니다.
