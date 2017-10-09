---
title: "스냅숏 관리자 볼륨 그룹 aaaStorSimple | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 toocreate hello 하 고 볼륨 그룹을 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>StorSimple 스냅숏 관리자 toocreate를 사용 하 고 볼륨 그룹 관리
## <a name="overview"></a>개요
Hello를 사용할 수 있습니다 **볼륨 그룹** hello에 대 한 노드 **범위** 창 tooassign 볼륨 toovolume 그룹, 볼륨 그룹에 대 한 정보 보기 백업을 예약 하 고 볼륨 그룹을 편집 합니다.

볼륨 그룹은 백업이 응용 프로그램 일치 지 사용 되는 관련된 볼륨 tooensure의 풀입니다. 자세한 내용은 [볼륨 및 볼륨 그룹](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups)과 [Windows 볼륨 섀도 복사본 서비스와의 통합](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)을 참조하세요.

> [!IMPORTANT]
> * 볼륨 그룹의 모든 볼륨은 단일 클라우드 서비스 공급자에서 가져와야 합니다.
> * 볼륨 그룹을 구성할 때 클러스터 공유 볼륨 (Csv)와 Csv 이외의 hello에 혼합 하지 않는 같은 볼륨 그룹입니다. StorSimple 스냅숏 관리자 Csv의 혼합을 지원 하지 않으며 Csv 이외의 동일한 스냅숏을 hello 합니다.

![볼륨 그룹 노드](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**그림 1: StorSimple 스냅숏 관리자 볼륨 그룹 노드** 

이 자습서에서는 StorSimple 스냅숏 관리자를 사용하여 다음 작업을 수행하는 방법을 설명합니다.

* 볼륨 그룹에 대한 정보 보기
* 볼륨 그룹 만들기
* 볼륨 그룹 백업
* 볼륨 그룹 편집
* 볼륨 그룹 삭제

이러한 모든 작업 에서도 사용할 수 있는 hello **동작** 창.

## <a name="view-volume-groups"></a>볼륨 그룹 보기
Hello를 누르면 **볼륨 그룹** 노드, hello **결과** hello 열 선택 내용에 따라, 창 hello 다음 각 볼륨 그룹에 대 한 정보를 표시 합니다. (열 hello에 hello **결과** 창을 구성할 수 있습니다. 마우스 오른쪽 단추로 클릭 hello **볼륨** 노드를 **보기**를 선택한 후 **열 추가/제거**.)

| 결과 열 | 설명 |
|:--- |:--- |
| 이름 |hello **이름** 열 hello 볼륨 그룹의 hello 이름을 포함 합니다. |
| 응용 프로그램 |hello **응용 프로그램** 열 현재 설치 된 VSS 기록기의 hello 수를 표시 하 고 Windows 호스트 hello에서 실행 합니다. |
| 선택 |hello **선택한** 열 hello 볼륨 그룹에 포함 된 볼륨의 hello 수를 표시 합니다. 영 (0) 응용 프로그램이 없습니다. hello 볼륨 그룹의 hello 볼륨 연관 되어 있음을 나타냅니다. |
| 가져옴 |hello **가져옴** 열 가져온된 볼륨의 hello 수를 표시 합니다. 설정 된 경우 너무**True**,이 열에 표시 하면 볼륨 그룹 hello Azure 포털에서에서 가져온 및 StorSimple 스냅숏 관리자를 만들지 못했습니다. |

> [!NOTE]
> StorSimple 스냅숏 관리자 볼륨 그룹 hello에 표시 됩니다 **백업 정책** hello Azure 포털에서에서 탭 합니다.
> 
> 

## <a name="create-a-volume-group"></a>볼륨 그룹 만들기
다음 프로시저 toocreate 볼륨 그룹 hello를 사용 합니다.

#### <a name="toocreate-a-volume-group"></a>toocreate 볼륨 그룹
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **볼륨 그룹**, 클릭 하 고 **볼륨 그룹 만들기**합니다.
   
    ![볼륨 그룹 만들기](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    hello **볼륨 그룹 만들기** 대화 상자가 나타납니다.
   
    ![볼륨 그룹 만들기 대화 상자](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Hello 다음 정보를 입력 합니다.
   
   1. Hello에 **이름** hello 새 볼륨 그룹에 대 한 고유한 이름을 입력 합니다.
   2. Hello에 **응용 프로그램** 상자의 hello 볼륨을 추가 하려는 toohello 볼륨 그룹에 연결 된 응용 프로그램을 선택 합니다.
      
       hello **응용 프로그램** 상자 목록에 StorSimple 볼륨을 사용 하 고 VSS 기록기는 응용 프로그램만 사용 하도록 설정 합니다. 경우에 볼륨 hello 모든 hello 기록기 인식 VSS 기록기를 사용할 수 볼륨은 StorSimple 볼륨입니다. Hello 응용 프로그램 상자가 비어 있으면 Azure StorSimple 볼륨을 사용 하 고 지원 되는 VSS 기록기는 응용 프로그램이 설치 됩니다. (현재 Azure StorSimple은 Microsoft Exchange 및 SQL Server를 지원합니다.) VSS 기록기에 대한 자세한 내용은 [Windows 볼륨 섀도 복사본 서비스와의 통합](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)을 참조하세요.
      
       응용 프로그램을 선택하면 연결된 모든 볼륨이 자동으로 선택됩니다. 반대로 특정 응용 프로그램과 관련 된 볼륨을 선택 하면 hello에서 응용 프로그램은 자동으로 선택 hello **응용 프로그램** 상자입니다. 
   3. Hello에 **볼륨** 상자에서 StorSimple 볼륨 tooadd toohello 볼륨 그룹을 선택 합니다. 
      
      * 단일 또는 다중 파티션이 있는 볼륨을 포함할 수 있습니다. (다중 파티션 볼륨은 다중 파티션이 있는 기본 디스크 또는 동적 디스크일 수 있습니다.) 다중 파티션이 포함된 볼륨은 단일 단위로 취급됩니다. 따라서 다른 파티션에 hello 파티션 tooa 볼륨 그룹을 모든 hello 중 하나에 추가 하는 경우는 자동으로 추가 된 toothat 볼륨 그룹에서 hello 동일한 시간입니다. 다중 파티션 볼륨 tooa 볼륨 그룹에 추가한 후 hello 다중 파티션 볼륨 계속 toobe 단일 단위로 취급 됩니다.
      * 모든 볼륨 toothem 하지 할당 하 여 빈 볼륨 그룹을 만들 수 있습니다. 
      * 클러스터 공유 볼륨 (Csv)와 Csv 이외의 hello에 혼합 하지 않는 같은 볼륨 그룹입니다. StorSimple 스냅숏 관리자 CSV 볼륨의 혼합을 지원 하지 않으며에서 CSV 이외의 볼륨 hello 같은 스냅숏에 합니다.
4. 클릭 **확인** toosave hello 볼륨 그룹입니다.

## <a name="back-up-a-volume-group"></a>볼륨 그룹 백업
볼륨 그룹을 프로시저 tooback 다음 hello를 사용 합니다.

#### <a name="tooback-up-a-volume-group"></a>볼륨 그룹을 tooback
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드를 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 **백업 수행**합니다.
   
    ![볼륨 그룹 즉시 백업](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. Hello에 **백업 수행** 대화 상자에서 **로컬 스냅숏** 또는 **클라우드 스냅숏**, 클릭 하 고 **만들기**합니다.
   
    ![백업 수행 대화 상자](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. 백업 hello tooconfirm 실행 되 고, 확장 hello **작업** 노드를 차례로 클릭 한 다음 **실행**합니다. hello 백업이 나열 됩니다.
5. 완료 tooview hello hello 확장 하 고 스냅숏을 **백업 카탈로그** 노드, hello 볼륨 그룹 이름을 확장 하 고 클릭 **로컬 스냅숏** 또는 **클라우드 스냅숏**합니다. 성공적으로 완료 되 면 hello 백업이 나열 됩니다.

## <a name="edit-a-volume-group"></a>볼륨 그룹 편집
다음 프로시저 tooedit 볼륨 그룹 hello를 사용 합니다.

#### <a name="tooedit-a-volume-group"></a>tooedit 볼륨 그룹
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드를 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 **편집**합니다.
3. hello * * 볼륨 그룹 만들기 * * 대화 상자가 나타납니다. Hello를 변경할 수 있습니다 **이름**, **응용 프로그램**, 및 **볼륨** 항목입니다.
4. 클릭 **확인** toosave 변경 내용을 합니다.

## <a name="delete-a-volume-group"></a>볼륨 그룹 삭제
다음 프로시저 toodelete 볼륨 그룹 hello를 사용 합니다. 

> [!WARNING]
> Hello 볼륨 그룹과 연결 된 모든 hello 백업이 삭제 됩니다.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete 볼륨 그룹
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 확장 **볼륨 그룹** 노드를 볼륨 그룹 이름을 마우스 오른쪽 단추로 클릭 **삭제**합니다.
3. hello **볼륨 그룹 삭제** 대화 상자가 나타납니다. 형식 **확인** hello 텍스트 상자와 클릭 **확인**합니다.
   
    hello에 hello 목록에서 볼륨 그룹을 삭제 하는 hello 사라집니다 **결과** 창 및 해당 볼륨 그룹에 연관 된 모든 백업이 hello 백업 카탈로그에서 삭제 됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* 너무 방법에 대해 알아봅니다[toocreate StorSimple 스냅숏 관리자를 사용 하 고 백업 정책 관리](storsimple-snapshot-manager-manage-backup-policies.md)합니다.

