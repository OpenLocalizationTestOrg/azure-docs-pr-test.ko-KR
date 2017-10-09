---
title: "aaaManage StorSimple 백업 카탈로그 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 백업 카탈로그 페이지 toolist toouse hello를 선택 하 고 백업 세트를 삭제 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>사용 하 여 hello StorSimple 장치 관리자 서비스 toomanage 백업 카탈로그
## <a name="overview"></a>개요
StorSimple 장치 관리자 서비스 hello **백업 카탈로그** 블레이드 수동 또는 예약 된 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다. 이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.

이 자습서에서는 방법 toolist, select 및 삭제 하 여 백업 세트를 설명 합니다. toolearn 어떻게 toorestore 백업에서 장치 이동 너무[장치 백업 세트에서 복원](storsimple-8000-restore-from-backup-set-u2.md)합니다. 볼륨을 tooclone 너무 이동 toolearn[StorSimple 볼륨을 복제](storsimple-8000-clone-volume-u2.md)합니다.

![백업 카탈로그](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

hello **백업 카탈로그** 블레이드 쿼리 toonarrow 백업 세트 선택 항목을 제공 합니다. Hello 매개 변수 뒤에 따라 검색 되는 hello 백업 세트를 필터링 할 수 있습니다.

* **장치** – hello 장치는 hello에 백업 세트 생성 합니다.
* **백업 정책 또는 볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.
* **From 및 To** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.

hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:

* **이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.
* **크기** – hello hello 백업 세트의 실제 크기입니다.
* **만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다. 
* **유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다. 로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다. 로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.
* **시작한 사람** – 일정에 따라 또는 사용자가 수동으로 hello 백업을 자동으로 시작 될 수 있습니다. 백업 정책 tooschedule 백업을 사용할 수 있습니다. Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 수동 백업 합니다.

## <a name="list-backup-sets-for-a-backup-policy"></a>백업 정책에 대한 백업 세트 나열
백업 정책에 대 한 모든 hello 백업을 hello 단계 toolist 다음을 완료 합니다.

#### <a name="toolist-backup-sets"></a>toolist 백업 세트
1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **백업 카탈로그**합니다.

2. 다음과 같이 필터 hello 선택:
   
   1. Hello 시간 범위를 지정 합니다.
   2. Hello 적절 한 장치를 선택 합니다.
   3. 기준으로 필터링 **백업 정책** tooview hello 해당 hello 백업 합니다.
   3. Hello 백업 정책 드롭다운 목록에서 선택 **모든** tooview 선택한 hello에 대 한 백업을 hello 모든 장치.
   4. 클릭 **적용** tooexecute이이 쿼리 합니다.
      
      선택한 hello 백업 정책과 연결 하는 hello 백업이 백업 세트의 hello 목록에 표시 되어야 합니다.

      ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>백업 세트를 선택합니다.
다음 단계 tooselect 볼륨 또는 백업 정책에 대 한 하 여 백업 세트 hello를 완료 합니다.

#### <a name="tooselect-a-backup-set"></a>tooselect 백업 세트
1. Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **백업 카탈로그**합니다.
2. 다음과 같이 필터 hello 선택:
   
   1. Hello 시간 범위를 지정 합니다. 
   2. Hello 적절 한 장치를 선택 합니다. 
   3. 원하는 tooselect hello 백업에 대 한 볼륨 또는 백업 정책에 의해 필터링 합니다.
   4. 클릭 **적용** tooexecute이이 쿼리 합니다.
      
      hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.

      ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. 백업 세트를 선택하고 확장합니다. 이제 hello 백업 세트를 포함 하는 hello 볼륨에 따라 구분을 볼 수 있습니다. hello **복원** 및 **삭제** 옵션이 hello hello 백업 세트에 대 한 상황에 맞는 메뉴 (오른쪽 클릭)을 통해 제공 됩니다. 선택한 백업 세트를 hello에 이러한 작업 중 하나를 수행할 수 있습니다.

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>백업 세트 삭제
연관 된 tooretain hello 데이터를 더 이상 원하는 백업을 삭제 합니다. Hello 단계 toodelete 백업 세트 다음을 수행 합니다.

#### <a name="toodelete-a-backup-set"></a>toodelete 백업 세트
 Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **백업 카탈로그**합니다.
2. 다음과 같이 필터 hello 선택:
   
   1. Hello 시간 범위를 지정 합니다. 
   2. Hello 적절 한 장치를 선택 합니다. 
   3. 원하는 tooselect hello 백업에 대 한 볼륨 또는 백업 정책에 의해 필터링 합니다.
   4. 클릭 **적용** tooexecute이이 쿼리 합니다.
      
      hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.

      ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. 백업 세트를 선택하고 확장합니다. 이제 hello 백업 세트를 포함 하는 hello 볼륨에 따라 구분을 볼 수 있습니다. hello **복원** 및 **삭제** 옵션이 hello hello 백업 세트에 대 한 상황에 맞는 메뉴 (오른쪽 클릭)을 통해 제공 됩니다. Hello 선택한 백업 세트를 마우스 오른쪽 단추로 클릭 하 고 hello 상황에 맞는 메뉴에서 선택 **삭제**합니다.

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. 확인 메시지가 표시 되 면 hello 표시 정보를 검토 하 고 클릭 **삭제**합니다. hello 선택한 백업이 영구적으로 삭제 됩니다.

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Hello 삭제가 진행에서 되 고 성공적으로 완료 되 면 알림이 표시 됩니다. Hello 삭제를 완료 한 후이 페이지에 hello 쿼리를 새로 고칩니다. 백업 세트를 삭제 하는 hello hello 백업 세트 목록에 더 이상 표시 됩니다.

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[사용 하 여 백업 세트에서 장치를 백업 카탈로그 toorestore hello](storsimple-8000-restore-from-backup-set-u2.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

