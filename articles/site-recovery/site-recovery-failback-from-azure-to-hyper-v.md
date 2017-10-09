---
title: "hyper-v 가상 컴퓨터에 대 한 Azure 사이트 복구에서 aaaFailback | Microsoft Docs"
description: "Azure Site Recovery hello 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 조정합니다. Azure tooon 온-프레미스 데이터 센터에서 장애 복구에 알아봅니다."
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
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Site Recovery에서 Hyper-V 가상 컴퓨터에 대한 장애 복구

이 문서에서는 toofailback 가상 컴퓨터를 Site Recovery에서 보호 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>필수 조건
1. Hello 주 사이트 VMM 서버/Hyper-v 서버가 연결 되어 있는지 확인 합니다.
2. 수행 해야 **커밋** hello 가상 컴퓨터에 있습니다.

## <a name="why-is-there-no-button-called-failback"></a>장애 복구라는 단추가 없는 이유는 무엇입니까?
Hello 포털에는 장애 복구 라는 명시적 제스처 없습니다. 장애 복구를 다시 돌아오는 toohello 주 사이트 단계입니다. 정의 따라 장애 조치는 하면 primary(on-premises) 사이트 toorecovery (Azure) 및 장애 복구에서 장애 조치 hello 가상 컴퓨터 장애 복구에서 가상 컴퓨터를 hello 백업할 때 tooprimary 경우입니다.

장애 조치를 시작할 때 hello 블레이드 hello 작업의 방향 hello에 대 한 알립니다. Hello 방향 Azure tooOn 온-프레미스 인 경우는 장애 복구 됩니다.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>계획 된 장애 조치 제스처 toofailback만 있는 이유는 무엇입니까?
Azure는 항상 사용 가능한 환경이며 가상 컴퓨터를 항상 사용할 수 있습니다. 장애 복구 hello 작업 온-프레미스를 다시 실행을 시작할 수 있도록 tootake 짧은 가동 중지 시간 결정 있는 활동을 계획된 하는 합니다. 이 경우 데이터 손실이 없어야 합니다. 계획 된 장애 조치 제스처를 사용할 수 있으므로, Azure의 hello Vm 해제, hello 최신 변경 내용 다운로드을 확인 데이터는 손실 되지 않습니다.

## <a name="initiate-failback"></a>장애 복구 시작
Hello 기본 toosecondary 위치에서 장애 조치 후 Site Recovery에서 복제 된 가상 컴퓨터가 보호 되지 및 보조 위치 hello 이제 역할을 hello 활성 위치입니다. 이러한 절차 toofail 백 toohello 원래 기본 사이트를 따릅니다. 이 절차에서는 설명 어떻게 toorun 복구에 대 한 계획된 된 장애 조치 계획 합니다. 또는 hello에서 단일 가상 컴퓨터에 대 한 hello 장애 조치를 실행할 수 있습니다 **가상 컴퓨터** 탭 합니다.

1. **복구 계획** > *recoveryplan_name*을 선택합니다. **장애 조치(Failover)** > **Planned 장애 조치(Failover)**에서 의견이나 질문을 게시합니다.
2. Hello에 * * 확인 계획 된 장애 조치 * * 페이지 hello 소스 및 대상 위치를 선택 합니다. Note hello 장애 조치 방향입니다. 기본에서 hello 장애 조치 작동 한 경우이 단지 정보 제공 용 hello 보조 위치에 있는 모든 가상 컴퓨터 및으로 기대 합니다.
3. Azure로부터 장애 복구하는 경우 **데이터 동기화**:에서 설정을 선택합니다.

   * **장애 조치(failover) 전 데이터 동기화(델타 변경 내용만 동기화)** - 가상 컴퓨터를 종료하지 않고 동기화할 때 가상 컴퓨터의 가동 중지 시간을 최소화하는 옵션입니다. 그 다음 hello지 않습니다.
     * 1 단계: Azure의 hello 가상 컴퓨터의 스냅숏을 걸리고 toohello 온-프레미스 Hyper-v 호스트에 복사 합니다. hello 컴퓨터 계속 Azure에서 실행 됩니다.
     * 2 단계: 새 변경 내용이 없습니다 발생할 수 있도록 Azure의 hello 가상 컴퓨터를 종료 합니다. hello 최종 델타 변경 내용 집합이 전송된 toohello 온-프레미스 서버와 hello 온-프레미스 가상 컴퓨터 시작 합니다.

    - **장애 조치 중에만 데이터 동기화(전체 다운로드)** - 오랜 시간 동안 Azure에서 실행한 경우 이 옵션을 사용합니다. 이 옵션은 대부분 hello 디스크의 변경 하 고 체크섬 계산에 시간 toospend 않도록 b 빠릅니다. Hello 디스크의 다운로드를 수행합니다. Hello 온-프레미스 가상 컴퓨터 삭제 된 경우에 유용 합니다.

    >[!NOTE]
    >잠시에 대 한 Azure 실행 되어 한 경우이 옵션을 사용 하는 것이 좋습니다 (한 달 이상) 또는 hello 온-프레미스 가상 컴퓨터가 삭제 되었습니다. 이 옵션 모든 체크섬 계산을 수행 하지 않습니다.
    >
    >




4. hello 클라우드에 대 한 데이터 암호화를 사용 하는 경우 **암호화 키** 선택 hello 발급 된 인증서를 hello VMM 서버에 공급자 설치 중에 데이터 암호화를 사용 하는 경우.
5. Hello 장애 조치를 시작 합니다. Hello에 hello 장애 조치가 진행 상황을 따를 수 **작업** 탭 합니다.
6. Hello 초기 데이터 동기화가 완료 되 고 Azure의 hello 가상 컴퓨터를 준비 tooshut 하는 한 번 hello 장애 조치 하기 전에 hello 옵션 toosynchronize hello 데이터를 선택한 경우 클릭 **작업** 계획 된 장애 조치 작업 이름 **장애 조치 완료**합니다. 이 위치 hello Azure 컴퓨터, 전송 hello toohello 온-프레미스 가상 컴퓨터를 최신 변경 및 시작 되는 VM 온-프레미스 hello를 종료 합니다.
7. 이제 로그인 할 수 있습니다 hello 가상 컴퓨터 toovalidate에 정상적으로 사용할 수는 있습니다.
8. hello 가상 컴퓨터가 커밋 대기 중 상태인 있습니다. 클릭 **커밋** toocommit hello 장애 조치 합니다.
9. Toocomplete hello 장애 복구를 순서 대로 다음을 클릭 합니다. 이제 **역방향 복제** toostart hello 주 사이트의 hello 가상 컴퓨터를 보호 합니다.

## <a name="failback-tooan-alternate-location"></a>장애 복구 tooan 대체 위치
간 보호를 배포한 경우는 [Hyper-v 사이트와 Azure](site-recovery-hyper-v-site-to-azure.md) tooability toofailback Azure tooan 대체 온-프레미스 위치에서 있는 합니다. 새 온-프레미스 하드웨어가를 tooset 해야 할 경우에 유용 합니다. 그 방법은 다음과 같습니다.

1. 새 하드웨어를 설정 하는 경우 Windows Server 2012 r 2를 설치 하 고 hello hello 서버에 Hyper-v 역할.
2. Hello hello 원래 서버에서 사용 했던 동일한 이름이 있는 가상 네트워크 스위치를 만듭니다.
3. 선택 **보호 된 항목** -> **보호 그룹**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> toofail 다시 한 선택 **계획 됨 장애 조치**합니다.
4. **계획된 장애 조치 확인** select **존재하지 않는 경우 온-프레미스 가상 컴퓨터 만들기**에서 의견이나 질문을 게시합니다.
5. **호스트 이름** 선택 hello tooplace hello 가상 컴퓨터를 원하는 새 Hyper-v 호스트 서버입니다.
6. 데이터 동기화에 hello 옵션을 선택할 권장 **hello 장애 조치 하기 전에 hello 데이터 동기화**합니다. 이 옵션은 가상 컴퓨터를 종료하지 않고 동기화하므로 가상 컴퓨터에 대한 가동 중지 시간을 최소화합니다. 그 다음 hello지 않습니다.

   * 1 단계: Azure의 hello 가상 컴퓨터의 스냅숏을 걸리고 toohello 온-프레미스 Hyper-v 호스트에 복사 합니다. hello 컴퓨터 계속 Azure에서 실행 됩니다.
   * 2 단계: 새 변경 내용이 없습니다 발생할 수 있도록 Azure의 hello 가상 컴퓨터를 종료 합니다. hello 마지막 변경 내용 집합이 전송된 toohello 온-프레미스 서버와 hello 온-프레미스 가상 컴퓨터 시작 합니다.
7. 확인 표시 toobegin hello 장애 조치 hello (failback)를 클릭 합니다.
8. Hello 초기 동기화가 완료 되는 Azure의 hello 가상 컴퓨터를 준비 tooshut 후 클릭 **작업** > <planned failover job> > **장애 조치 완료**합니다. 이 종료 hello Azure 기계, 전송 hello 최신 변경 내용 toohello 온-프레미스 가상 컴퓨터를 시작 합니다.
9. 모든 것이 예상 대로 작동 하는 hello 온-프레미스 가상 컴퓨터 tooverify 로그온 할 수 있습니다. 클릭 **커밋** toofinish hello 장애 조치 합니다.
10. 클릭 **역방향 복제** toostart hello 온-프레미스 가상 컴퓨터를 보호 합니다.

    > [!NOTE]
    > 데이터 동기화 단계에서 이루어지는 동안 hello 장애 복구 작업을 취소 하면 hello 온-프레미스 VM 손상 된 상태에 포함 됩니다. 이 Azure VM 디스크 toohello 온-프레미스 데이터 디스크에서 hello 최신 데이터를 복사 하는 데이터 동기화 hello 디스크 데이터에 일관성이 수 없습니다 hello 동기화 완료 될 때까지 때문입니다. 데이터 동기화 취소 된 후 온-프레미스 VM hello 부팅 되 면 부팅 되지 않을 수 있습니다. 장애 조치 toocomplete hello 데이터 동기화를 다시 트리거.
    >
    >



## <a name="next-steps"></a>다음 단계

Hello 장애 복구 작업을 완료 한 후 **커밋** hello 가상 컴퓨터. 커밋은 hello Azure 가상 컴퓨터 및 해당 디스크를 삭제 하 고 다시 보호 하는 hello VM toobe를 준비 합니다.

후 **커밋**, hello를 시작할 수 있습니다 *역방향 복제*합니다. 온-프레미스 백 tooAzure에서 hello 가상 컴퓨터 보호가 시작 됩니다. Hello VM Azure에서 해제 되었습니다. 보내고 따라서 차등만 변경 이후 변경 된 내용만 복제 hello 됩니다이 note 합니다.
