---
title: "StorSimple 8000 시리즈 볼륨 aaaClone | Microsoft Docs"
description: "Hello 다른 복제 유형에 대해 설명 및 시기 toouse, 백업 세트 tooclone 개별 볼륨을 사용 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Hello StorSimple 관리자 서비스 tooclone (업데이트 2) 볼륨을 사용 하 여
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>개요
StorSimple Manager 서비스 hello **백업 카탈로그** 페이지 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다. 이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.

![백업 카탈로그 페이지](./media/storsimple-clone-volume-u2/backupCatalog.png)  

이 자습서에서는 백업 세트 tooclone 개별 볼륨을 사용 하는 방법을 설명 합니다. Hello 차이점에 대해서도 설명 *일시적인* 및 *영구* 를 복제 합니다.

> [!NOTE]
> 로컬로 고정된 볼륨은 계층화된 볼륨으로 복제됩니다. 로컬로 고정 된 복제 볼륨 toobe hello 필요, hello 복제 작업이 성공적으로 완료 된 후 로컬로 고정 tooa 볼륨을 복제 하는 hello를 변환할 수 있습니다. 로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-manage-volumes-u2.md#change-the-volume-type)합니다.
> 
> Tooconvert 계층화 된 toolocally에서 복제 볼륨 (것은 임시 복제본 여전히) 하는 경우를 복제 한 후 즉시 고정을 시도 하면 다음과 같은 오류 메시지가 hello hello 변환이 실패 합니다.
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Tooa 다른 장치에 복제 하는 경우에이 오류가 수신 되었습니다. 먼저 hello 임시 복제본 tooa 영구 복제본을 변환 하는 경우 고정 된 hello 볼륨 toolocally 성공적으로 변환할 수 있습니다. 영구 tooconvert hello 임시 복제본 tooa clone의 클라우드 스냅숏을 합니다.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>볼륨의 클론 만들기
복제본을 만들 수 있습니다에 동일한 장치나 다른 장치는 가상 컴퓨터는 로컬을 사용 하 여 hello 또는 클라우드 스냅숏을 합니다.

#### <a name="tooclone-a-volume"></a>tooclone 볼륨
1. Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 하 고 백업 세트를 선택 합니다.
2. Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다. 클릭 하 고 hello 백업 세트에서 볼륨을 선택 합니다.
   
     ![볼륨 복제](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. 클릭 **복제** toobegin hello 선택한 볼륨의 복제 합니다.
4. Hello 복제 볼륨 마법사에서 아래 **이름 및 위치 지정**:
   
   1. 대상 장치를 식별합니다. Hello 위치 hello 복제를 만들 위치입니다. 같은 장치 hello 하거나 다른 장치를 지정할 수도 있습니다. 다른 클라우드 서비스 공급자와 연결 된 볼륨을 선택 하는 경우 (하지 Azure), hello 드롭 다운 목록에 hello 대상 장치는 물리적 장치에만 표시 합니다. 가상 장치에 다른 클라우드 서비스 공급자와 연결된 볼륨을 복제할 수 없습니다.
      
      > [!NOTE]
      > Hello 복제에 필요한 hello 용량 hello 대상 장치에서 사용 가능한 hello 용량 보다 낮은 인지 확인 합니다.
      > 
      > 
   2. 해당 클론에 대한 고유 볼륨 이름을 지정합니다. hello 이름은 3 ~ 127 자 사이 있어야 합니다. 
      
      > [!NOTE]
      > hello **복제본 볼륨으로** 필드가 **계층화 됨** 로컬로 고정 된 볼륨을 복제 하는 경우에 합니다. 이 설정을 변경할 수 없습니다. 그러나 복제 된 볼륨 toobe 로컬로 고정 hello 필요, hello 복제본을 성공적으로 만들면 hello tooa 로컬로 고정 볼륨 복제 변환할 수 있습니다. 로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-manage-volumes-u2.md#change-the-volume-type)합니다.
      > 
      > 
      
        ![복제 마법사 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Hello 화살표 아이콘을 클릭 합니다. ![화살표 아이콘](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello 다음 페이지입니다.
5. **이 볼륨을 사용할 수 있는 호스트 지정**아래:
   
   1. Hello 복제에 대 한 액세스 제어 레코드 (ACR)을 지정 합니다. 새 ACR을 추가 하거나 hello 기존 목록에서 선택할 수 있습니다.
      
        ![복제 마법사 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Hello 확인 아이콘을 클릭 합니다. ![check-icon](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)toocomplete hello 작업입니다.
6. 복제 작업 시작 및 알려 hello 복제 성공적으로 만들어지면 합니다. 클릭 **작업 보기** hello에 toomonitor hello 복제 작업 **작업** 페이지. Hello hello 복제 작업이 완료 되 면 메시지의 뒤에 표시 됩니다.
   
    ![클론 메시지](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Hello 후 복제 작업이 완료 됩니다.
   
   1. Toohello 이동 **장치** 페이지 및 선택 hello **볼륨 컨테이너** 탭 합니다. 
   2. 연결 된 복제 hello 원본 볼륨 hello 볼륨 컨테이너를 선택 합니다. 볼륨의 hello 목록에서 방금 만든 hello 복제를 표시 되어야 합니다.

> [!NOTE]
> 모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다.
> 
> 

이러한 방식으로 만들어진 클론은 임시 클론입니다. 복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.

이 복제본은 이제 정규 볼륨이 및 볼륨에서 사용할 수 있는 모든 작업 hello 복제에 사용할 수 있는 수 있습니다. 모든 백업에 대 한이 볼륨 tooconfigure를 해야 합니다.

## <a name="transient-vs-permanent-clones"></a>임시 및 영구 복제본 비교
임시 복제본 tooa 다른 장치를 복제 하는 경우에 생성 됩니다. Hello StorSimple Manager에서 관리 하는 백업 세트 tooa 다른 장치에서 특정 볼륨을 복제할 수 있습니다. hello 임시 복제본 hello 원본 볼륨에 대 한 참조 toohello 데이터가 있는 됩니다 하 고 해당 데이터 tooread 사용 하며 hello 대상 장치에서 로컬로 작성 됩니다. 

임시 복제본의 클라우드 스냅숏을 수행한 후 생성 되는 복제본 hello 됩니다는 *영구* 복제 합니다. 이 과정에서 hello 데이터의 복사본에 hello 클라우드 및이 데이터는 hello 데이터의 hello 크기에 따라 결정 되는 시간 toocopy hello 만들어지고 hello Azure 대기 시간 (이것이 Azure-Azure 복사) 합니다. 일 tooweeks를 걸릴 수 있습니다. hello 임시 복제본 영구 복제본이 방식이으로 되며 참조 toohello 원래 볼륨 데이터가 없는에서 복제 되었습니다. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>임시 및 영구 클론에 대한 시나리오
hello 다음 섹션에서는 임시 복제본과 영구 복제본을 사용할 수 있는 예제 상황을 설명 합니다.

### <a name="item-level-recovery-with-a-transient-clone"></a>임시 클론을 사용하여 항목 수준 복구
1 년 전에 Microsoft PowerPoint 프레젠테이션 파일 toorecover가 필요합니다. IT 관리자는 해당 기간의 특정 백업을 hello를 식별 하 고 필터 hello 볼륨입니다. 관리자에 게 다음에서 hello 볼륨 복제, hello 파일을 찾고, 찾아 tooyou를 제공 합니다. 이 시나리오에서는 임시 클론이 사용됩니다. 

![동영상 사용 가능](./media/storsimple-clone-volume-u2/Video_icon.png) **동영상 사용 가능**

toowatch hello 복제를 사용 하 여 StorSimple 삭제 toorecover 파일의 기능을 복원 하는 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)합니다.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>영구 복제본을 사용 하는 hello 프로덕션 환경에서 테스트
Tooverify hello 프로덕션 환경에서 테스트 버그를 해야합니다. Hello 프로덕션 환경에서 hello 볼륨의 복제본을 만들고이 복제 toocreate는 독립적인 복제 볼륨의 클라우드 스냅숏을 다음 합니다. 이 시나리오에서는 영구 클론이 사용됩니다.  

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set-u2.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

