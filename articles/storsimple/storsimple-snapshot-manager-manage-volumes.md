---
title: "aaaStorSimple 스냅숏 관리자 및 볼륨 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooview hello 하 및 볼륨과 tooconfigure 백업을 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>StorSimple 스냅숏 관리자 tooview를 사용 하 고 볼륨 관리
## <a name="overview"></a>개요
Hello StorSimple 스냅숏 관리자를 사용할 수 있습니다 **볼륨** 노드 (hello에 **범위** 창) tooselect 볼륨에 대 한 정보를 확인 합니다. hello 볼륨 toohello 볼륨 탑재 hello 호스트에서 해당 하는 드라이브로 표시 됩니다. hello **볼륨** 로컬 볼륨 및 볼륨 유형을 hello iSCSI와 장치 사용을 통해 검색 한 볼륨을 포함 하 여 StorSimple에서 지원 되는 노드를 보여 줍니다. 

지원 되는 볼륨에 대 한 자세한 내용은 이동 너무[여러 볼륨 유형에 대 한 지원](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types)합니다.

![결과 창의 볼륨 목록](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

hello **볼륨** 노드 수도 있습니다를 다시 검색 하거나 StorSimple 스냅숏 관리자에서 검색 한 후 볼륨을 삭제 합니다. 

이 자습서에서는 볼륨을 탑재, 초기화 및 포맷한 다음 StorSimple Snapshot Manager를 사용하여 다음 작업을 수행하는 방법에 대해 설명합니다.

* 볼륨에 대한 정보 보기 
* 볼륨 삭제
* 볼륨 다시 검사 
* 기본 볼륨 구성 및 백업
* 동적 미러 볼륨 구성 및 백업

> [!NOTE]
> 모든 hello **볼륨** 노드 작업은 또한 hello에서 사용할 수 있는 **동작** 창.
> 
> 

## <a name="mount-volumes"></a>볼륨 탑재
사용 하 여 hello 프로시저 toomount 다음 초기화 및 StorSimple 볼륨을 포맷 합니다. 이 프로시저는 디스크 관리를 하드 디스크 및 hello 해당 볼륨이 나 파티션을 관리 하기 위한 시스템 유틸리티를 사용 합니다. 디스크 관리에 대 한 자세한 내용은 이동 너무[디스크 관리](https://technet.microsoft.com/library/cc770943.aspx) hello Microsoft TechNet 웹 사이트에 있습니다.

#### <a name="toomount-volumes"></a>toomount 볼륨
1. 호스트 컴퓨터에서 hello Microsoft iSCSI 초기자를 시작 합니다.
2. 대상 포털 hello hello 인터페이스 IP 주소 또는 검색 IP 주소 중 하나를 제공 하 고 toohello 장치를 연결 합니다. Hello 장치가 연결 된 hello 볼륨 tooyour 액세스할 수 있는 Windows 시스템 됩니다. Hello Microsoft iSCSI 초기자를 사용 하는 방법에 대 한 자세한 내용은 "연결 tooan iSCSI 대상 장치" toohello 섹션에서 go [iSCSI 초기자 설치 및 구성 하는 Microsoft][1]합니다.
3. Hello 옵션 toostart 디스크 관리를 다음 중 하나를 사용 합니다.
   
   * Hello에 Diskmgmt.msc 입력 **실행** 상자입니다.
   * 서버 관리자를 시작, hello 확장 **저장소** 노드를 선택한 후 **디스크 관리**합니다.
   * 시작 **관리 도구**, hello 확장 **컴퓨터 관리** 노드를 선택한 후 **디스크 관리**합니다. 
     
     > [!NOTE]
     > 관리자 권한 toorun 디스크 관리를 사용 해야 합니다.
     > 
     > 
4. 온라인 hello 볼륨을 수행 합니다.
   
   1. 디스크 관리에서 **오프라인**으로 표시된 볼륨을 마우스 오른쪽 단추로 클릭합니다.
   2. **디스크 다시 활성화**를 클릭합니다. hello 디스크를 표시 해야 **온라인** 후 hello 디스크 다시 활성화 됩니다.
5. Hello 볼륨을 초기화 합니다.
   
   1. 발견 된 hello 볼륨을 마우스 오른쪽 단추로 클릭 합니다.
   2. Hello 메뉴에서 선택 **디스크 초기화**합니다.
   3. Hello에 **디스크 초기화** 선택 hello 디스크 tooinitialize를 원하고 클릭 한 다음 대화 상자, **확인**합니다.
6. 단순 볼륨을 포맷합니다.
   
   1. Tooformat 되도록 볼륨을 마우스 오른쪽 단추로 클릭 합니다.
   2. Hello 메뉴에서 선택 **새 단순 볼륨**합니다.
   3. Hello 새 단순 볼륨 마법사 tooformat hello 볼륨을 사용 합니다.
      
      * Hello 볼륨 크기를 지정 합니다.
      * 드라이브 문자를 지정합니다.
      * Hello NTFS 파일 시스템을 선택 합니다.
      * 64KB 할당 단위 크기를 지정합니다.
      * 빠른 포맷을 수행합니다.
7. 다중 파티션 볼륨을 포맷합니다. 자세한 내용은 "파티션 및 볼륨" toohello 섹션에서 go [디스크 관리 구현](https://msdn.microsoft.com/library/dd163556.aspx)합니다.

## <a name="view-information-about-your-volumes"></a>볼륨에 대한 정보 보기
다음 로컬 및 Azure StorSimple 볼륨에 대 한 프로시저 tooview 정보 hello를 사용 합니다.

#### <a name="tooview-volume-information"></a>tooview 볼륨 정보
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다. 
2. Hello에 **범위** 창의 hello 클릭 **볼륨** 노드. Hello에 Azure StorSimple 볼륨을 모두 포함 하 여 로컬 및 마운트된 볼륨 목록이 표시 됩니다 **결과** 창. hello에 대 한 열 hello **결과** 창을 구성할 수 있습니다. (마우스 오른쪽 단추 클릭 hello **볼륨** 노드를 **보기**를 선택한 후 **열 추가/제거**.)
   
    ![Hello 열 구성](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | 결과 열 | 설명 |
   |:--- |:--- |
   |  이름 |hello **이름** 열 hello 드라이브 문자가 할당 tooeach 발견 된 볼륨을 포함 합니다. |
   |  장치 |hello **장치** 열 hello 장치 연결된 toohello 호스트 컴퓨터의 hello IP 주소를 포함 합니다. |
   |  장치 볼륨 이름 |hello **장치 볼륨 이름** hello 이름이의 hello 장치 볼륨 toowhich hello 선택한 볼륨이 속해 합니다. Hello 해당 특정 볼륨에 대해 Azure 포털에에서 정의 된 hello 볼륨 이름입니다. |
   |  액세스 경로 |hello **액세스 경로** hello 액세스 경로 toohello 볼륨 열에 표시 됩니다. 이 hello 드라이브 문자나 탑재 지점이 있는 hello에 볼륨은 hello 호스트 컴퓨터에서 액세스할 수 있습니다. |

## <a name="delete-a-volume"></a>볼륨 삭제
Hello 프로시저 toodelete 볼륨을 StorSimple 스냅숏 관리자에서 다음을 사용 합니다.

> [!NOTE]
> 볼륨 그룹에 속해 있는 볼륨은 삭제할 수 없습니다. (hello 삭제 옵션은 볼륨 그룹의 구성원 인 볼륨에 사용할 수 있습니다.) Hello 전체 볼륨 그룹 toodelete hello 볼륨을 삭제 해야 합니다.

#### <a name="toodelete-a-volume"></a>toodelete 볼륨
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 클릭 **볼륨** 노드. 
3. Hello에 **결과** 창, 마우스 오른쪽 단추로 클릭 hello 볼륨 toodelete 되도록 합니다.
4. Hello 메뉴를 클릭 **삭제**합니다. 
   
    ![볼륨 삭제](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. hello **볼륨 삭제** 대화 상자가 나타납니다. 형식 **확인** hello 텍스트 상자와 클릭 **확인**합니다.
6. 기본적으로 StorSimple Snapshot Manager는 삭제하기 전에 볼륨을 백업합니다. 이 예방 조치로 의도 하지 않은 hello 삭제 하는 경우 데이터 손실 로부터 있습니다 보호할 수 있습니다. StorSimple 스냅숏 관리자를 표시 한 **자동 스냅숏** hello 볼륨을 백업 하는 동안 진행률 메시지입니다. 
   
    ![자동 스냅숏 메시지](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>볼륨 다시 검사
다음 프로시저 toorescan hello 볼륨 사용 하 여 hello tooStorSimple 스냅숏 관리자 연결 합니다.

#### <a name="toorescan-hello-volumes"></a>toorescan hello 볼륨
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **볼륨**, 클릭 하 고 **볼륨 다시 검사**합니다.
   
    ![볼륨 다시 검사](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    이 절차는 StorSimple 스냅숏 관리자를 사용 하 여 hello 볼륨 목록을 동기화합니다. 새 볼륨 또는 삭제 된 볼륨과 같은 변경 내용이 hello 결과에 반영 됩니다.

## <a name="configure-and-back-up-a-basic-volume"></a>기본 볼륨 구성 및 백업
다음 프로시저 tooconfigure 기본 볼륨의 백업을 hello를 사용 하 여 백업을 바로 시작 하거나 예약 된 백업에 대 한 정책을 만듭니다.

### <a name="prerequisites"></a>필수 조건
시작하기 전에

* Hello StorSimple 장치 및 호스트 컴퓨터 올바르게 구성 되어 있는지 확인 합니다. 자세한 내용은 이동 너무[온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)합니다.
* StorSimple Snapshot Manager 설치 및 구성 자세한 내용은 이동 너무[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>기본 볼륨의 tooconfigure 백업
1. Hello StorSimple 장치에서 기본 볼륨을 만듭니다.
2. 탑재, 초기화 및에 설명 된 대로 hello 볼륨을 포맷 [볼륨을 탑재](#mount-volumes)합니다. 
3. 바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다. hello StorSimple 스냅숏 관리자 창이 나타납니다. 
4. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **볼륨** 노드를 선택한 후 **볼륨 다시 검사**합니다. Hello에 볼륨 목록이 나타나야 hello 검색이 완료 되 면 **결과** 창. 
5. Hello에 **결과** 창의 hello 볼륨을 마우스 오른쪽 단추로 클릭 한 다음 선택 **볼륨 그룹 만들기**합니다. 
   
    ![볼륨 그룹 만들기](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. Hello에 **볼륨 그룹 만들기** 대화 상자 hello 볼륨 그룹에 대 한 이름을 입력 볼륨 tooit 할당 하 고 클릭 **확인**합니다.
7. Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드. hello 새 볼륨 그룹은 hello 아래에 나타나야 합니다. **볼륨 그룹** 노드. 
8. Hello 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 합니다.
   
   * toostart은 대화형 (주문형) 백업 작업을 클릭 하 여 **백업 수행**합니다. 
   * 자동 백업 tooschedule 클릭 **백업 정책 만들기**합니다. Hello에 **일반** 페이지 hello 목록에서 볼륨 그룹을 선택 합니다. Hello에 **일정** 페이지에서 hello 일정 정보를 입력 합니다. 작업을 마쳤으면 **확인**을 클릭합니다. 
9. hello, 백업 작업이 hello tooconfirm 시작 **작업** hello에 대 한 노드 **범위** 창 hello를 클릭 한 다음 **실행** 노드. hello에 hello 현재 실행 중인 작업 목록이 표시 됩니다 **결과** 창. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>동적 미러 볼륨 구성 및 백업
동적 미러 볼륨의 tooconfigure 백업 단계를 수행 하는 hello를 완료 합니다.

* 1 단계: 사용 하 여 디스크 관리 toocreate 동적 미러 볼륨 
* 2 단계: StorSimple 스냅숏 관리자를 사용 하 여 tooconfigure 백업입니다.

### <a name="prerequisites"></a>필수 조건
시작하기 전에

* Hello StorSimple 장치 및 호스트 컴퓨터 올바르게 구성 되어 있는지 확인 합니다. 자세한 내용은 이동 너무[온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.
* StorSimple Snapshot Manager 설치 및 구성 자세한 내용은 이동 너무[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.
* Hello StorSimple 장치에 두 개의 볼륨을 구성 합니다. (Hello 예제 hello 사용할 수 있는 볼륨은 **디스크 1** 및 **디스크 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>1 단계: 사용 하 여 디스크 관리 toocreate 동적 미러 볼륨
디스크 관리는 하드 디스크와 hello 볼륨 또는 파티션이 포함 된 관리 하기 위한 시스템 유틸리티입니다. 디스크 관리에 대 한 자세한 내용은 이동 너무[디스크 관리](https://technet.microsoft.com/library/cc770943.aspx) hello Microsoft TechNet 웹 사이트에 있습니다.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate 동적 미러 볼륨
1. Hello 옵션 toostart 디스크 관리를 다음 중 하나를 사용 합니다. 
   
   * 열기 hello **실행** 상자에서 입력 **Diskmgmt.msc**, Enter 키를 누릅니다.
   * 서버 관리자를 시작, hello 확장 **저장소** 노드를 선택한 후 **디스크 관리**합니다. 
   * 시작 **관리 도구**, hello 확장 **컴퓨터 관리** 노드를 선택한 후 **디스크 관리**합니다. 
2. Hello StorSimple 장치에 두 개의 볼륨을 사용할 수 있는지 확인 합니다. (Hello 예에서 사용할 수 있는 볼륨 hello는 **디스크 1** 및 **디스크 2**.) 
3. Hello 디스크 관리 창의 hello hello 아래쪽 창 오른쪽 열에서 마우스 오른쪽 단추로 클릭 **디스크 1** 선택 **새 미러 볼륨**합니다. 
   
    ![새 미러 볼륨](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. Hello에 **새 미러 볼륨** 마법사 페이지에서 클릭 **다음**합니다.
5. Hello에 **디스크 선택** 페이지 **디스크 2** hello에 **선택한** 창에서 클릭 **추가**, 클릭 하 고 **다음**. 
6. Hello에 **할당할 드라이브 문자 또는 경로** 페이지 hello 기본값을 적용 하 고 클릭 **다음**합니다. 
7. Hello에 **볼륨 포맷** 페이지 hello **할당 단위 크기** 상자 **64k**합니다. 선택 hello **빠른 포맷 수행** 확인란을 선택한 다음 클릭 **다음**합니다. 
8. Hello에 **새 미러 볼륨 완료 hello** 페이지에서 설정을 검토 하 고 클릭 **마침**합니다. 
9. 기본 디스크 hello tooindicate 동적 디스크 변환된 tooa 됩니다 메시지가 표시 됩니다. **예**를 클릭합니다.
   
    ![동적 디스크 변환 메시지](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. 디스크 관리에서 디스크 1과 디스크 2가 동적 미러 볼륨으로 표시되는지 확인합니다. (**동적** hello 상태 열에 표시 되어야 하 고 용량 막대 색 hello 미러 볼륨을 나타내는 toored 변경 해야 합니다.) 
    
    ![디스크 관리에서 미러링한 동적 디스크](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>2 단계: StorSimple 스냅숏 관리자를 사용 하 여 tooconfigure 백업
다음 프로시저 tooconfigure 동적 미러 볼륨 hello를 사용 하 여 백업을 바로 시작 하거나 예약 된 백업에 대 한 정책을 만듭니다.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>동적 미러 볼륨의 tooconfigure 백업
1. 바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다. hello StorSimple 스냅숏 관리자 창이 나타납니다. 
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **볼륨** 노드 선택한 **볼륨 다시 검사**합니다. Hello에 볼륨 목록이 나타나야 hello 검색이 완료 되 면 **결과** 창. hello 동적 미러 볼륨은 단일 볼륨으로 나열 됩니다. 
3. Hello에 **결과** 창의 hello 동적 미러 볼륨을 마우스 오른쪽 단추로 클릭 **볼륨 그룹 만들기**합니다. 
4. Hello에 **볼륨 그룹 만들기** 대화 상자 hello 볼륨 그룹에 대 한 이름을 입력 hello 동적 미러 볼륨 toothis 그룹에 할당 하 고 클릭 **확인**합니다. 
5. Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드. hello 새 볼륨 그룹은 hello 아래에 나타나야 합니다. **볼륨 그룹** 노드. 
6. Hello 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 합니다. 
   
   * toostart은 대화형 (주문형) 백업 작업을 클릭 하 여 **백업 수행**합니다. 
   * 자동 백업 tooschedule 클릭 **백업 정책 만들기**합니다. Hello에 **일반** 페이지, hello 목록에서 선택 hello 볼륨 그룹입니다. Hello에 **일정** 페이지에서 hello 일정 정보를 입력 합니다. 작업을 마쳤으면 **확인**을 클릭합니다. 
7. 이 실행 될 때 hello 백업 작업을 모니터링할 수 있습니다. Hello에 **범위** 창 hello 확장 **작업** 노드를 차례로 클릭 한 다음 **실행**, hello에 hello 작업 세부 정보 표시 **결과** 창. Hello 세부 정보는 전송 된 toohello hello 백업 작업이 완료 되 면 **마지막 24** 시간 작업 목록입니다. 

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* 너무 방법에 대해 알아봅니다[toocreate StorSimple 스냅숏 관리자를 사용 하 고 볼륨 그룹을 관리](storsimple-snapshot-manager-manage-volume-groups.md)합니다.

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
