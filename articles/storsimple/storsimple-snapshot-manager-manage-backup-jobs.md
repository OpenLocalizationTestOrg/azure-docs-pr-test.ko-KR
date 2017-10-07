---
title: "aaaStorSimple 스냅숏 관리자에 대 한 백업 작업 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 tooview hello 하 및 예약 된 시간, 현재 실행 중인 및 완료 된 백업 작업을 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>StorSimple 스냅숏 관리자 tooview를 사용 하 고 백업 작업 관리

## <a name="overview"></a>개요
hello **작업** hello에 대 한 노드 **범위** 창 표시 hello **예약 된**, **마지막 24 시간**, 및 **실행**대화형으로 또는 구성된 정책에 따라 시작 작업을 백업 합니다. 

이 자습서에서는 hello를 사용 하는 방법에 대해 설명 **작업** 예약, 최근, 및 현재 실행 중인 백업 작업에 대 한 노드 toodisplay 정보입니다. (hello에 작업 및 해당 정보가 hello 목록이 표시 됩니다 **결과** 창입니다.) 또한 나열된 작업을 마우스 오른쪽 단추로 클릭하면 사용 가능한 작업이 나열된 상황에 맞는 메뉴를 표시할 수 있습니다.

## <a name="view-scheduled-jobs"></a>예약된 작업 보기
예약 된 백업 작업을 사용 하 여 hello tooview 절차를 수행 합니다.

#### <a name="tooview-scheduled-jobs"></a>tooview 예약 된 작업
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다. 
2. Hello에 **범위** 창 hello 확장 **작업** 노드를 마우스 클릭 **예약 된**합니다. hello에 다음 정보가 나타납니다 hello **결과** 창:
   
   * **이름** – hello hello 예약 된 스냅숏 이름
   * **그런 다음 실행** – hello의 날짜 및 시간 hello 예약 된 다음 스냅숏
   * **마지막으로 실행** – hello의 날짜 및 시간 hello 가장 최근 예약 된 스냅숏
     
     > [!NOTE]
     > 한 번만 스냅숏에 대 한 hello **다음 실행** 및 **마지막 실행** 동일 hello 됩니다.
     
     ![예약된 백업 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. 특정 작업에 대해 추가 작업 tooperform hello에 hello 작업 이름을 마우스 오른쪽 단추로 클릭 **결과** 창과 hello 메뉴 옵션 중에서 선택 합니다.

## <a name="view-recent-jobs"></a>최근 작업 보기
다음 프로시저 tooview 백업 hello를 사용 하 고 지난 24 시간 동안 hello에서 완료 된 작업을 복원 합니다.

#### <a name="tooview-recent-jobs"></a>tooview 최근 작업
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창 hello 확장 **작업** 노드를 마우스 클릭 **마지막 24 시간**합니다. hello **결과** 창 지난 24 시간 동안 (tooa입니다 최대 64 개 작업) hello에 대 한 백업 작업이 표시 됩니다. hello에 다음 정보가 나타납니다 hello **결과** hello에 따라 창 **보기** 지정할 옵션:
   
   * **이름** – hello hello 예약 된 스냅숏 이름입니다.
   * **시작** – hello 날짜 및 hello 스냅숏 시작 된 시간입니다.
   * **중지** hello 날짜 및 시간 hello 스냅숏이 완료 되거나 종료 때 – 합니다.
   * **경과 된** – hello hello 사이의 시간 크기 **시작 됨** 및 **Stopped** 시간입니다.
   * **상태** – hello hello 최근에 완료 된 작업의 상태입니다. **성공** hello 백업이 성공적으로 만들어졌는지 여부를 나타냅니다. **실패** 해당 hello 작업이 성공적으로 실행 되지 않습니다 나타냅니다.
   * **정보** – hello hello 실패에 대 한 설명입니다.
   * **바이트 (MB)를 처리** – hello (단위: Mb)에서 처리 된 hello 볼륨 그룹의 데이터 양입니다. 
     
     ![Hello 지난 24 시간 동안 실행 된 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. 특정 작업에 대해 추가 작업 tooperform hello에 hello 작업 이름을 마우스 오른쪽 단추로 클릭 **결과** 창과 hello 메뉴 옵션 중에서 선택 합니다.
   
    ![작업 삭제](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>현재 실행 중인 작업 보기
현재 실행 중인 프로시저 tooview 작업을 수행 하는 hello를 사용 합니다.

#### <a name="tooview-currently-running-jobs"></a>현재 실행 중인 작업 tooview
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창 hello 확장 **작업** 노드를 마우스 클릭 **실행**합니다. Hello에 따라 **보기** hello에 다음 정보는 hello 표시를 지정 하는 옵션 **결과** 창:
   
   * **이름** – hello hello 예약 된 스냅숏 이름입니다.
   * **시작** – hello 날짜 및 hello 스냅숏 시작 된 시간입니다.
   * **검사점** – hello hello 백업의 현재 작업 합니다.
   * **상태** – hello 완료 비율입니다.
   * **경과 된** – hello 양을 hello 백업이 시작 된 이후에 경과 된 시간입니다. 
   * **평균 처리량 (MB)** – (Mb)를 처리 하는 데 걸린 총 시간을 처리 하는 데이터 toothat의 총 바이트 수의 비율입니다.
   * **처리된 바이트(MB)** - 처리된 데이터의 총 바이트(MB)
   * **작성된 바이트(MB)** - 작성된 데이터의 총 바이트(MB) 따라서 일반적으로 보다 크면 바이트 처리 hello 및 hello 메타 데이터 뿐만 아니라 hello 데이터 포함 됩니다.
     
     ![현재 실행 중인 작업](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. 특정 작업에 대해 추가 작업 tooperform hello에 hello 작업 이름을 마우스 오른쪽 단추로 클릭 **결과** 창과 hello 메뉴 옵션 중에서 선택 합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* 너무 방법에 대해 알아봅니다[StorSimple 스냅숏 관리자 toomanage hello 백업 카탈로그를 사용 하 여](storsimple-snapshot-manager-manage-backup-catalog.md)합니다.

