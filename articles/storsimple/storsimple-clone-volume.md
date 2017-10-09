---
title: "aaaClone StorSimple 볼륨 | Microsoft Docs"
description: "Hello 다른 복제 유형에 대해 설명 및 시기 toouse, 백업 세트 tooclone 개별 볼륨을 사용 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a>Hello StorSimple 관리자 서비스 tooclone 볼륨을 사용 하 여
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>개요
StorSimple Manager 서비스 hello **백업 카탈로그** 페이지 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다. 이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.

![백업 카탈로그 페이지](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

이 자습서에서는 백업 세트 tooclone 개별 볼륨을 사용 하는 방법을 설명 합니다. Hello 차이점에 대해서도 설명 *일시적인* 및 *영구* 를 복제 합니다. 

## <a name="create-a-clone-of-a-volume"></a>볼륨의 클론 만들기
Hello에 복제본을 만들 수 있습니다 동일한 장치나 다른 장치는 로컬 또는 클라우드 스냅숏을 사용 하 여 가상 컴퓨터도 합니다.

#### <a name="tooclone-a-volume"></a>tooclone 볼륨
1. Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 하 고 백업 세트를 선택 합니다.
2. Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다. 클릭 하 고 hello 백업 세트에서 볼륨을 선택 합니다.
   
     ![볼륨 복제](./media/storsimple-clone-volume/HCS_Clone.png) 
3. 클릭 **복제** toobegin hello 선택한 볼륨의 복제 합니다.
4. Hello 복제 볼륨 마법사에서 아래 **이름 및 위치 지정**:
   
   1. 대상 장치를 식별합니다. Hello 위치 hello 복제를 만들 위치입니다. 같은 장치 hello 하거나 다른 장치를 지정할 수도 있습니다. 다른 클라우드 서비스 공급자와 연결 된 볼륨을 선택 하는 경우 (하지 Azure), hello 드롭 다운 목록에 hello 대상 장치는 물리적 장치에만 표시 합니다. 가상 장치에 다른 클라우드 서비스 공급자와 연결된 볼륨을 복제할 수 없습니다.
      
      > [!NOTE]
      > Hello 복제에 필요한 hello 용량 hello 대상 장치에서 사용 가능한 hello 용량 보다 낮은 인지 확인 합니다.
      > 
      > 
   2. 해당 클론에 대한 고유 볼륨 이름을 지정합니다. hello 이름은 3 ~ 127 자 사이 있어야 합니다.
   3. Hello 화살표 아이콘을 클릭 합니다. ![화살표 아이콘](./media/storsimple-clone-volume/HCS_ArrowIcon.png) tooproceed toohello 다음 페이지입니다.
5. **이 볼륨을 사용할 수 있는 호스트 지정**아래:
   
   1. Hello 복제에 대 한 액세스 제어 레코드 (ACR)을 지정 합니다. 새 ACR을 추가 하거나 hello 기존 목록에서 선택할 수 있습니다.
   2. Hello 확인 아이콘을 클릭 합니다. ![check-icon](./media/storsimple-clone-volume/HCS_CheckIcon.png)toocomplete hello 작업입니다.
6. 복제 작업 시작 및 알려 hello 복제 성공적으로 만들어지면 합니다. 클릭 **작업 보기** hello에 toomonitor hello 복제 작업 **작업** 페이지.
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
임시 복제본과 영구 복제본 tooa 다른 장치에 복제 하는 경우에 생성 됩니다. 백업 세트 tooa 다른 장치에서 특정 볼륨을 복제할 수 있습니다. 이러한 방식으로 만들어진 복제본은 *임시* 복제본입니다. hello 임시 복제본 되 고 참조 toohello 원래 볼륨 없게 로컬로 쓰는 동안 해당 볼륨 tooread를 사용 합니다. 

임시 복제본의 클라우드 스냅숏을 수행한 후 생성 되는 복제본 hello 됩니다는 *영구* 복제 합니다. hello 영구 복제본 독립적 이며에서 복제 된 모든 참조가 toohello 원래 볼륨 없는 경우.  

## <a name="scenarios-for-transient-and-permanent-clones"></a>임시 및 영구 클론에 대한 시나리오
hello 다음 섹션에서는 임시 복제본과 영구 복제본을 사용할 수 있는 예제 상황을 설명 합니다.

### <a name="item-level-recovery-with-a-transient-clone"></a>임시 클론을 사용하여 항목 수준 복구
1 년 전에 Microsoft PowerPoint 프레젠테이션 파일 toorecover가 필요합니다. IT 관리자는 해당 기간의 특정 백업을 hello를 식별 하 고 필터 hello 볼륨입니다. 관리자에 게 다음에서 hello 볼륨 복제, hello 파일을 찾고, 찾아 tooyou를 제공 합니다. 이 시나리오에서는 임시 클론이 사용됩니다. 

![동영상 사용 가능](./media/storsimple-clone-volume/Video_icon.png) **동영상 사용 가능**

toowatch hello 복제를 사용 하 여 StorSimple 삭제 toorecover 파일의 기능을 복원 하는 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)합니다.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>영구 복제본을 사용 하는 hello 프로덕션 환경에서 테스트
Tooverify hello 프로덕션 환경에서 테스트 버그를 해야합니다. 이 복제본의 클라우드 스냅숏을 만드는 것으로 hello 프로덕션 환경에서 hello 볼륨의 복제본을 만듭니다. hello 복제 된 볼륨은 독립적인 볼륨이 되므로 합니다. 이 시나리오에서는 영구 클론이 사용됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[백업 세트에서 StorSimple 볼륨을 복원](storsimple-restore-from-backup-set.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

