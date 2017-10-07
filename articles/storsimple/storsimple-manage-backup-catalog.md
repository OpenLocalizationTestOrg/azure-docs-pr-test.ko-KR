---
title: "aaaManage StorSimple 백업 카탈로그 | Microsoft Docs"
description: "Toouse hello StorSimple Manager 서비스 백업 카탈로그 페이지 toolist를 선택 하 고 볼륨에 대 한 백업 세트를 삭제 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>사용 하 여 hello StorSimple 관리자 서비스 toomanage 백업 카탈로그
## <a name="overview"></a>개요
StorSimple Manager 서비스 hello **백업 카탈로그** 페이지 수동 또는 예약 된 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다. 이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.

이 자습서에서는 방법 toolist, select 및 삭제 하 여 백업 세트를 설명 합니다. toolearn 어떻게 toorestore 백업에서 장치 이동 너무[장치 백업 세트에서 복원](storsimple-restore-from-backup-set.md)합니다. 볼륨을 tooclone 너무 이동 toolearn[StorSimple 볼륨을 복제](storsimple-clone-volume.md)합니다.

![백업 카탈로그](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

hello **백업 카탈로그** 페이지 쿼리 toonarrow 백업 세트 선택 항목을 제공 합니다. Hello 매개 변수 뒤에 따라 검색 되는 hello 백업 세트를 필터링 할 수 있습니다.

* **장치** – hello 장치는 hello에 백업 세트 생성 합니다.
* **백업 정책 또는 볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.
* **From 및 To** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.

hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:

* **이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.
* **크기** – hello hello 백업 세트의 실제 크기입니다.
* **만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다. 
* **유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다. 로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다. 로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.
* **시작한 사람** – 일정에 따라 또는 사용자가 수동으로 hello 백업을 자동으로 시작 될 수 있습니다. 백업 정책 tooschedule 백업을 사용할 수 있습니다. Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 수동 백업 합니다.

## <a name="list-backup-sets-for-a-volume"></a>볼륨에 대한 목록 백업 세트
다음 단계 toolist hello 볼륨에 대 한 모든 hello 백업을 완료 합니다.

#### <a name="toolist-backup-sets"></a>toolist 백업 세트
1. Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 합니다.
2. 다음과 같이 필터 hello 선택:
   
   1. Hello 적절 한 장치를 선택 합니다.
   2. Hello 드롭 다운 목록에서 볼륨 tooview hello 해당 hello 백업을 선택 합니다.
   3. Hello 시간 범위를 지정 합니다.
   4. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute이이 쿼리 합니다.
      
      hello 백업을 선택 하는 hello 볼륨와 관련 된 백업 세트의 hello 목록에 표시 되어야 합니다.

## <a name="select-a-backup-set"></a>백업 세트를 선택합니다.
다음 단계 tooselect 볼륨 또는 백업 정책에 대 한 하 여 백업 세트 hello를 완료 합니다.

#### <a name="tooselect-a-backup-set"></a>tooselect 백업 세트
1. Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 합니다.
2. 다음과 같이 필터 hello 선택:
   
   1. Hello 적절 한 장치를 선택 합니다.
   2. Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.
   3. Hello 시간 범위를 지정 합니다.
   4. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute이이 쿼리 합니다.
      
      hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.
3. 백업 세트를 선택하고 확장합니다. hello **복원** 및 **삭제** 옵션이 hello hello 페이지 맨 아래에 표시 됩니다. 선택한 백업 세트를 hello에 이러한 작업 중 하나를 수행할 수 있습니다.

## <a name="delete-a-backup-set"></a>백업 세트 삭제
연관 된 tooretain hello 데이터를 더 이상 원하는 백업을 삭제 합니다. Hello 단계 toodelete 백업 세트 다음을 수행 합니다.

#### <a name="toodelete-a-backup-set"></a>toodelete 백업 세트
1. Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그 탭**합니다.
2. 다음과 같이 필터 hello 선택:
   
   1. Hello 적절 한 장치를 선택 합니다.
   2. Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.
   3. Hello 시간 범위를 지정 합니다.
   4. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute이이 쿼리 합니다.
      
      hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.
3. 백업 세트를 선택하고 확장합니다. hello **복원** 및 **삭제** 옵션이 hello hello 페이지 맨 아래에 표시 됩니다. **삭제**를 클릭합니다.
4. Hello 삭제가 진행에서 되 고 성공적으로 완료 되 면 알림이 표시 됩니다. Hello 삭제를 완료 한 후이 페이지에 hello 쿼리를 새로 고칩니다. 백업 세트를 삭제 하는 hello hello 백업 세트 목록에 더 이상 표시 됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[사용 하 여 백업 세트에서 장치를 백업 카탈로그 toorestore hello](storsimple-restore-from-backup-set.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

