---
title: "StorSimple 8000 시리즈에는 백업에서 볼륨 aaaRestore | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 장치 관리자 서비스 백업 카탈로그 toorestore 백업 세트에서 StorSimple 볼륨에 설명 합니다."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>백업 세트에서 StorSimple 볼륨 복원

## <a name="overview"></a>개요

이 자습서에서는 기존 백업 세트를 사용 하 여 StorSimple 8000 시리즈 장치에 수행 하는 hello 복원 작업을 설명 합니다. 사용 하 여 hello **백업 카탈로그** 블레이드 toorestore 로컬에서 볼륨 또는 클라우드 백업 합니다. hello **백업 카탈로그** 블레이드 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다. 백업 세트에서 복원 작업 hello hello 백그라운드에서 데이터를 다운로드 하는 동안에 즉시 hello 볼륨을 온라인를 제공 합니다.

대체 방법 toostart 복원 하는 경우이 toogo 너무**장치 > [장치] > 볼륨**합니다. Hello에 **볼륨** 블레이드에서 인 볼륨을 마우스 오른쪽 단추로 클릭 tooinvoke hello 상황에 맞는 메뉴를 선택한 다음 선택 **복원**합니다.

## <a name="before-you-restore"></a>복원하기 전에

복원을 시작 하기 전에 다음 제한 사항을 적용 하는 hello를 검토 합니다.

* **Hello 볼륨을 오프 라인으로 수행 해야** – hello 호스트 모두에서 hello 볼륨을 오프 라인 상태로 전환한 hello 복원 작업을 시작 하기 전에 장치 hello 합니다. Hello 복원 작업에 자동으로 hello 장치에서 hello 볼륨을 온라인 상태로, 있지만 hello 호스트에 hello 장치를 온라인을 수동으로 표시 해야 합니다. Hello 볼륨이 hello 장치에서 온라인으로 hello 호스트에서 볼륨을 온라인 hello를 가져올 수 있습니다. (않아도 toowait hello 복원 작업이 완료 될 때까지 합니다.) 너무 절차를 보려면[볼륨을 오프 라인](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)합니다.

* **복원 후 볼륨 종류가** – 삭제 된 볼륨이 복원 hello 스냅숏의 hello 형식에 따라; 즉, 로컬로 고정 된 볼륨은 로컬로 고정 된 볼륨에서 복원 되 고 된 계층화 된 볼륨은 계층화 된 볼륨으로 복원 됩니다.

    기존 볼륨에 대 한 hello 볼륨의 현재 사용 유형을 hello hello 스냅숏에 저장 된 hello 형식을 재정의 합니다. 예를 들어 hello 볼륨 종류가 계층을 지정할 때 만들어진 스냅숏으로에서 볼륨을 복원 하는 경우 수행 된 tooa 변환 작업) (인해 고정 된 볼륨 종류가 이제 인지 로컬로 hello 볼륨을 로컬 고정된 볼륨으로 복원 됩니다. 마찬가지로, 기존 로컬 고정된 볼륨 확장 고 이후에 hello 볼륨을 더 작은 경우에 수행 되는 이전 스냅숏에서 복원 인 경우 hello 복원 된 볼륨 유지 됩니다 hello 현재 확장 된 크기입니다.

    계층화 된 볼륨 tooa 로컬로 고정 된 볼륨에서 볼륨을 변환할 수 없습니다 또는 로컬 고정된 볼륨 tooa에서 계층으로 계층화 된 볼륨 hello 볼륨을 복원 하는 동안 있습니다. Hello 복원 작업이 완료 되 면 다음 hello 볼륨 tooanother 유형을 변환할 수 있습니다 때까지 기다립니다. 볼륨을 변환 하는 방법에 대 한 내용은 이동 너무[hello 볼륨 유형 변경](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)합니다. 

* **hello 볼륨 크기에에서 반영 되어 복원 hello 볼륨** – 삭제 (로컬 고정된 볼륨이 완전히 프로 비전) 되므로 로컬로 고정 된 볼륨을 복원 하는 경우이 중요 한 고려 합니다. 이전에 삭제 된 로컬 고정된 볼륨 toorestore를 시도 하기 전에 충분 한 공간이 있는지 확인 합니다.

* **복원 하는 동안 볼륨을 확장할 수 없지만** – tooexpand hello 볼륨을 시도 하기 전에 hello 복원 작업이 완료 될 때까지 기다립니다. 볼륨을 확장 하는 방법에 대 한 내용은 이동 너무[볼륨 수정](storsimple-8000-manage-volumes-u2.md#modify-a-volume)합니다.

* **로컬 볼륨을 복원 하는 동안에 백업을 수행할 수** 에 대 한 프로시저 너무 –[hello StorSimple 장치 관리자 서비스 toomanage 백업 정책을 사용 하 여](storsimple-8000-manage-backup-policies-u2.md)합니다.

* **복원 작업을 취소할 수** -hello 볼륨 롤백되어 toohello 상태에 있었던 hello 복원 작업을 시작 하기 전에 다음 hello 복원 작업을 취소 하는 경우. 너무 절차를 보려면[작업 취소](storsimple-8000-manage-jobs-u2.md#cancel-a-job)합니다.

## <a name="how-does-restore-work"></a>복원 작업 방법

업데이트 4 이상을 실행하는 장치의 경우 heatmap 기반 복원이 구현됩니다. Hello 호스트 요청 tooaccess 데이터 hello 장치에 도달 하는 대로 이러한 요청은 추적 하 고는 heatmap 만들어집니다. 높은 요청 속도 요청 속도가 느린 toochunks 낮은 열으로 변환 하는 반면 더 높은 열으로는 데이터 청크를 발생 합니다. Hello 데이터 적어도 두 번 toobe로 표시 된 액세스 해야 _핫_합니다. 수정된 파일도 _hot_으로 표시됩니다. Hello 복원을 시작한 후의 데이터 사전 하이드레이션 hello heatmap에 따라 발생 합니다. 업데이트 4 이전 버전에 대 한 hello 데이터 액세스만에 따라 복원 하는 동안 다운로드 됩니다.

다음 제한 사항을 적용 하는 hello tooheatmap 기반 복원 적용 됩니다.

* 열 지도 추적은 계층화된 볼륨에 대해서만 사용하도록 설정되고 로컬로 고정된 볼륨은 지원되지 않습니다.

* Heatmap 기반 복원 tooanother 장치 볼륨을 복제할 때 지원 되지 않습니다. 

* 원위치에서 복원 하는 경우 hello 장치에 hello 볼륨 toobe 복원에 대 한 로컬 스냅숏이 있는 경우 다음 म 수행 하지 리하이드레이션 (한 데이터를 로컬로 사용할 수 이미). 

* 기본적으로 복원 하면 hello 리하이드레이션 작업 시작 됩니다 hello heatmap를 기반으로 데이터를 리하이드레이션 사전입니다. 

업데이트 4에서 Windows PowerShell cmdlet 수 리하이드레이션 작업을 실행 하는 사용 되는 tooquery, 리하이드레이션 작업을 취소 있으며 hello 리하이드레이션 작업의 hello 상태를 가져옵니다.

* `Get-HcsRehydrationJob`-이 cmdlet는 hello 리하이드레이션 작업의 hello 상태를 가져옵니다. 하나의 볼륨에 대해 단일 리하이드레이션 작업이 트리거됩니다.

* `Set-HcsRehydrationJob`-이 cmdlet toopause, 중지, hello 리하이드레이션 진행 중인 경우 hello 리하이드레이션 작업을 다시 시작 합니다.

리하이드레이션 cmdlet에 대 한 자세한 내용은 이동 너무[StorSimple 용 Windows PowerShell cmdlet 참조](https://technet.microsoft.com/library/dn688168.aspx)합니다.

자동 리하이드레이션을 사용하면 일반적으로 일시적인 더 높은 읽기 성능이 예상됩니다. 향상 된 hello 실제 magniutde 액세스 패턴, 데이터 청크 및 데이터 형식 등의 다양 한 요인에 따라 달라 집니다. 

리하이드레이션 작업 toocancel hello PowerShell cmdlet을 사용할 수 있습니다. 이후 복원 hello 모두에 대 한 toopermanently 사용 안 함 리하이드레이션 작업 하려는 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다.

## <a name="how-toouse-hello-backup-catalog"></a>어떻게 toouse hello 백업 카탈로그

hello **백업 카탈로그** 블레이드 백업 세트 선택 toonarrow 수 있는 쿼리를 제공 합니다. Hello 백업 세트를 검색 하는 hello 매개 변수 뒤에 따라 필터링 할 수 있습니다.

* **시간 범위** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.
* **장치** – hello 장치는 hello에 백업 세트 생성 합니다.
* **백업 정책** 또는 **볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.

hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:

* **이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.
* **유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다. 로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다. 로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.
* **크기** – hello hello 백업 세트의 실제 크기입니다.
* **만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다. 
* **볼륨** -hello hello 백업 세트와 연결 된 볼륨의 수입니다.
* **시작** – hello 백업을 tooa 일정에 따라 자동으로 시작 될 수 있습니다 또는 사용자가 수동으로 합니다. (백업 정책 tooschedule 백업을 사용할 수 있습니다. Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 대화형 또는 요청 시 백업 합니다.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>어떻게 toorestore 백업에서 StorSimple 볼륨

Hello를 사용할 수 있습니다 **백업 카탈로그** 블레이드 toorestore 특정 백업에서 StorSimple 볼륨입니다. 그러나 점을 기억할 해당 볼륨을 복원 hello 볼륨 toohello의 상태로 hello 백업을 만들 때 사용 하 게 됩니다. Hello 백업 작업 후 추가 된 모든 데이터는 손실 됩니다.

> [!WARNING]
> 백업에서 복원 hello hello 백업에서 기존 볼륨이 바뀝니다. Hello 백업을 수행한 후에 기록 된 모든 데이터의 손실을 hello 않을 수 있습니다.


### <a name="toorestore-your-volume"></a>toorestore 볼륨
1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **백업 카탈로그**합니다.

2. 백업 세트를 다음과 같이 선택합니다.
   
   1. Hello 시간 범위를 지정 합니다.
   2. Hello 적절 한 장치를 선택 합니다.
   3. Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.
   4. 클릭 **적용** tooexecute이이 쿼리 합니다.

    hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.
   
    ![백업 세트 목록](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다. 이러한 볼륨을 복구 하기 전에 hello 호스트와 장치에서 오프 라인 해야 합니다. Hello에 hello 볼륨을 액세스할 **볼륨** 단계 장치 및 다음에 따라 hello 블레이드 [볼륨을 오프 라인](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake를 오프 라인입니다.
   
   > [!IMPORTANT]
   > 수행 하 여 hello 호스트의 hello 볼륨을 오프 라인으로 먼저 hello 장치에서 hello 볼륨을 오프 라인으로 수행 하기 전에 있는지 확인 합니다. Hello 호스트에서 오프 라인으로 hello 볼륨을 사용 하지 않는 경우 toodata 손상이 될 수 있습니다.
   
4. 뒤로 toohello 이동 **백업 카탈로그** 탭 하 고 백업 세트를 선택 합니다. 마우스 오른쪽 단추로 클릭 한 다음 hello 상황에 맞는 메뉴에서 선택 **복원**합니다.

    ![백업 세트 목록](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. 확인하라는 메시지가 표시됩니다. 검토 hello 정보를 복원 하 고 hello 확인 확인란을 선택 합니다.
   
    ![확인 페이지](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  **복원**을 클릭합니다. 이 명령은 hello에 액세스 하 여 볼 수 있는 복원 작업을 시작 **작업** 페이지.

    ![확인 페이지](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Hello 복원이 완료 된 후 볼륨의 hello 내용을 hello 백업에서 볼륨으로 바뀌는 것을 확인 합니다.


## <a name="if-hello-restore-fails"></a>Hello 복원 실패

어떤 이유로 든 hello 복원 작업이 실패 하는 경우 경고를 받게 됩니다. 이 경우 백업 hello 새로 고침 hello 백업 목록 tooverify 계속 유효 합니다. Hello 백업을 유효한 hello 클라우드에서 복원 하는 경우 다음 연결 문제가 있습니다 수 hello 문제가 발생 했습니다.

toocomplete hello 복원 작업, hello 호스트에서 hello 볼륨을 오프 라인 및 hello 복원 작업을 다시 시도 하십시오. 참고 hello 중에 수행 된 모든 수정 내용을 toohello 볼륨 데이터 복원 프로세스는 손실 됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[관리 StorSimple 볼륨](storsimple-8000-manage-volumes-u2.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

