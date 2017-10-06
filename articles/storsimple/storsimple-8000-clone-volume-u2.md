---
title: "StorSimple 8000 시리즈에 있는 볼륨 aaaClone | Microsoft Docs"
description: "Hello 다른 복제 유형 및 사용법에 설명 하 고 StorSimple 8000 시리즈 장치에 백업 세트 tooclone 개별 볼륨을 사용 하는 방법을 설명 합니다."
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Hello StorSimple 장치 관리자 서비스를 사용 하 여 Azure 포털 tooclone 볼륨에

## <a name="overview"></a>개요

이 자습서에서는 백업 세트 tooclone hello 통해 개별 볼륨을 사용 하는 방법을 설명 **백업 카탈로그** 블레이드입니다. Hello 차이점에 대해서도 설명 *일시적인* 및 *영구* 를 복제 합니다. 이 자습서의 지침에 hello tooall hello StorSimple 8000 시리즈 장치를 업데이트 3 이상을 실행 하 고 적용 됩니다.

StorSimple 장치 관리자 서비스 hello **백업 카탈로그** 블레이드 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다. 그런 다음 백업 세트 tooclone에서 볼륨을 선택할 수 있습니다.

 ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>볼륨 복제 시 고려 사항

Hello 볼륨을 복제할 때는 다음 정보를 고려 합니다.

- 복제본을 동일 하 게 작동 hello에 정규 볼륨이 방식으로 합니다. Hello 복제에 대 한 볼륨에서 사용할 수 있는 모든 작업 ´ ù.

- 모니터링 및 기본 백업은 복제된 볼륨에서 자동으로 비활성화됩니다. 모든 백업 tooconfigure 복제본된 볼륨에서는 사용 해야 합니다.

- 로컬 고정 볼륨은 계층화된 볼륨으로 복제됩니다. 로컬로 고정 된 복제 볼륨 toobe hello 필요, hello 복제 작업이 성공적으로 완료 된 후 로컬로 고정 tooa 볼륨을 복제 하는 hello를 변환할 수 있습니다. 로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)합니다.

- Tooconvert 계층화 된 toolocally에서 복제 볼륨 (것은 임시 복제본 여전히) 하는 경우를 복제 한 후 즉시 고정을 시도 하면 다음과 같은 오류 메시지가 hello로 hello 변환에 실패 합니다.

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Tooa 다른 장치에 복제 하는 경우에이 오류가 수신 되었습니다. 먼저 hello 임시 복제본 tooa 영구 복제본을 변환 하는 경우 고정 된 hello 볼륨 toolocally 성공적으로 변환할 수 있습니다. Hello 임시 복제본 tooconvert의 클라우드 스냅숏을 것 tooa 영구 복제본입니다.

## <a name="create-a-clone-of-a-volume"></a>볼륨의 클론 만들기

복제본을 만들 수 있습니다에 로컬을 사용 하 여 동일한 장치나 다른 장치 클라우드 어플라이언스에 hello 또는 클라우드 스냅숏을 합니다.

아래 hello 절차 toocreate hello에서 복제본을 카탈로그를 백업 하는 방법을 설명 합니다.  대체 방법 tooinitiate 복제본이 toogo 너무**볼륨**, 볼륨을 선택 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 선택 **복제**합니다.

Hello 단계 toocreate 볼륨의 복제본을 hello 백업 카탈로그에서 다음을 수행 합니다.

#### <a name="tooclone-a-volume"></a>tooclone 볼륨

1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **백업 카탈로그**합니다.

2. 백업 세트를 다음과 같이 선택합니다.
   
   1. Hello 적절 한 장치를 선택 합니다.
   2. Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.
   3. Hello 시간 범위를 지정 합니다.
   4. 클릭 **적용** tooexecute이이 쿼리 합니다.

    hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.
   
    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다. 이러한 볼륨을 복구 하기 전에 hello 호스트와 장치에서 오프 라인 해야 합니다. Hello에 hello 볼륨을 액세스할 **볼륨** 단계 장치 및 다음에 따라 hello 블레이드 [볼륨을 오프 라인](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake를 오프 라인입니다.
   
   > [!IMPORTANT]
   > 수행 하 여 hello 호스트의 hello 볼륨을 오프 라인으로 먼저 hello 장치에서 hello 볼륨을 오프 라인으로 수행 하기 전에 있는지 확인 합니다. Hello 호스트에서 오프 라인으로 hello 볼륨을 사용 하지 않는 경우 toodata 손상이 될 수 있습니다.
   
4. 뒤로 toohello 이동 **백업 카탈로그** 후 백업 세트의 볼륨을 선택 합니다. 마우스 오른쪽 단추로 클릭 한 다음 hello 상황에 맞는 메뉴에서 선택 **복제**합니다.

   ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. Hello에 **복제** 블레이드에서 다음 단계 hello지 않습니다.
   
    1. 대상 장치를 식별합니다. Hello 위치 hello 복제를 만들 위치입니다. 같은 장치 hello 하거나 다른 장치를 지정할 수도 있습니다.

      > [!NOTE]
      > Hello 복제에 필요한 hello 용량 hello 대상 장치에서 사용 가능한 hello 용량 보다 낮은 인지 확인 합니다.
       
    2. 해당 클론에 대한 고유 볼륨 이름을 지정합니다. hello 이름은 3 ~ 127 자 사이 있어야 합니다.
      
        > [!NOTE]
        > hello **복제본 볼륨으로** 필드가 **계층화 됨** 로컬로 고정 된 볼륨을 복제 하는 경우에 합니다. 이 설정을 변경할 수 없습니다. 그러나 복제 된 볼륨 toobe 로컬로 고정 hello 필요, hello 복제본을 성공적으로 만들면 hello tooa 로컬로 고정 볼륨 복제 변환할 수 있습니다. 로컬로 계층화 된 볼륨 tooa 변환에 대 한 내용은 고정 볼륨에 대 한 이동 너무[hello 볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)합니다.
          
    3. 아래 **호스트 연결**, hello 복제에 대 한 액세스 제어 레코드 (ACR)를 지정 합니다. 새 ACR을 추가 하거나 hello 기존 목록에서 선택할 수 있습니다. ACR hello이이 복제본에 액세스할 수 있는 호스트를 결정 합니다.
      
        ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. 클릭 **복제** toocomplete hello 작업 합니다.

4. 복제 작업이 시작 되 고 hello 복제 성공적으로 만들어지면 알림이 표시 됩니다. 너무 hello 작업 알림을 클릭 하거나**작업** 블레이드 toomonitor hello 복제 작업입니다.

    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Hello 복제 작업이 완료 되 면 tooyour 장치 이동한 다음 클릭 **볼륨**합니다. Hello 볼륨 목록에서 방금 만든 hello에 동일한 hello 복제를 확인 해야 hello 원본 볼륨이 있는 볼륨 컨테이너입니다.

    ![백업 세트 목록](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

이러한 방식으로 만들어진 클론은 임시 클론입니다. 복제 유형에 대한 자세한 내용은 [임시 및 영구 복제본 비교](#transient-vs-permanent-clones)를 참조하세요.


## <a name="transient-vs-permanent-clones"></a>임시 및 영구 복제본 비교
임시 복제본 tooanother 장치를 복제 하는 경우에 생성 됩니다. Hello StorSimple 장치 관리자에서 관리 하는 백업 세트 tooa 다른 장치에서 특정 볼륨을 복제할 수 있습니다. hello 임시 복제본 hello 원본 볼륨에 대 한 참조 toohello 데이터 고 hello 대상 장치에서 해당 데이터 tooread 및 쓰기를 로컬로 사용 합니다.

임시 복제본의 클라우드 스냅숏을 수행 하면 hello 결과 복제는 한 *영구* 복제 합니다. 이 과정에서 hello 데이터의 복사본에 hello 클라우드 및이 데이터는 hello 데이터의 hello 크기에 따라 결정 되는 시간 toocopy hello 만들어지고 hello Azure 대기 시간 (이것이 Azure-Azure 복사) 합니다. 일 tooweeks를 걸릴 수 있습니다. 임시 복제본 hello 영구 복제본 되며 참조 toohello 원래 볼륨 데이터가 없는에서 복제 되었습니다.

## <a name="scenarios-for-transient-and-permanent-clones"></a>임시 및 영구 클론에 대한 시나리오
hello 다음 섹션에서는 임시 복제본과 영구 복제본을 사용할 수 있는 예제 상황을 설명 합니다.

### <a name="item-level-recovery-with-a-transient-clone"></a>임시 클론을 사용하여 항목 수준 복구
1 년 전에 Microsoft PowerPoint 프레젠테이션 파일 toorecover가 필요합니다. IT 관리자가 시간에서 특정 백업을 hello를 식별 하 고 필터 hello 볼륨. 관리자에 게 다음에서 hello 볼륨 복제, hello 파일을 찾고, 찾아 tooyou를 제공 합니다. 이 시나리오에서는 임시 클론이 사용됩니다.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>영구 복제본을 사용 하는 hello 프로덕션 환경에서 테스트
Tooverify hello 프로덕션 환경에서 테스트 버그를 해야합니다. Hello 프로덕션 환경에서 hello 볼륨의 복제본을 만들고이 복제 toocreate는 독립적인 복제 볼륨의 클라우드 스냅숏을 다음 합니다. 이 시나리오에서는 영구 클론이 사용됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[백업 세트에서 StorSimple 볼륨을 복원](storsimple-8000-restore-from-backup-set-u2.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

