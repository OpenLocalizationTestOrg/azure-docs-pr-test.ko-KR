---
title: "StorSimple 가상 배열 백업 aaaClone | Microsoft Docs"
description: "자세한 방법을 tooclone 백업 및 StorSimple 가상 배열에서 파일을 복구 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>StorSimple 가상 배열의 백업에서 복제

## <a name="overview"></a>개요

이 문서에서는 단계별 방법을 tooclone 하 여 백업 세트 공유 또는 볼륨의 Microsoft Azure StorSimple 가상 배열에서 설명 합니다. hello 복제 된 백업을 사용 하는 toorecover 삭제 또는 손상 파일입니다. hello 문서에는 StorSimple 가상 배열에는 항목 수준 복구는 파일 서버로 구성 하는 자세한 단계 tooperform도를 포함 됩니다.

## <a name="clone-shares-from-a-backup-set"></a>백업 세트에서 공유 복제

**Tooclone 공유를 시도 하기 전에 충분 한 공간이 있는지 hello 장치 toocomplete에이 작업을 확인 합니다.** hello에 백업에서 tooclone [Azure 포털](https://portal.azure.com/), hello 다음 단계를 수행 합니다.

#### <a name="tooclone-a-share"></a>tooclone 공유

1. 너무 찾아보기**장치** 블레이드입니다. 장치를 선택하고 클릭한 다음 **공유**를 클릭합니다. Tooclone를 마우스 오른쪽 단추로 클릭 hello 공유 tooinvoke hello 상황에 맞는 메뉴 hello 공유를 선택 합니다. **복제**를 선택합니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. Hello에 **복제** 블레이드에서 클릭 **백업 > 선택** 수행가 다음를 hello 다음 및: 
   
   a.    Hello 시간 범위에 따라이 장치에서 백업을 필터링 합니다. **지난 7일**, **지난 30일** 및 **지난 해** 중에 선택할 수 있습니다.
   
   b.    표시 되는 필터링 된 백업 hello 목록에서 백업 tooclone를 선택 합니다.
   
   c.    **확인**을 클릭합니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. Hello에 **복제** 블레이드에서 클릭 **설정을 대상** 수행가 다음를 hello 다음 및:
   
   a.    공유 이름을 입력합니다. hello 공유 이름은 3 ~ 127 자 이어야 합니다.
   
   b.    필요에 따라 hello 복제 된 공유에 대 한 설명을 제공 합니다.
   
   c.    복원 하는 hello 공유의 hello 유형을 변경할 수 없습니다. 계층화된 공유는 계층화된 공유로 복제되고 로컬로 고정된 공유는 로컬로 고정된 공유로 복제됩니다.
   
   d.    hello 용량에서 복제 하는 hello 공유의 같은 toohello 크기로 설정 됩니다.
   
   e.    이 공유에 대 한 hello 관리자를 할당 합니다. Hello 복제를 완료 한 후 파일 탐색기를 통해 수 toomodify hello 공유 속성을 됩니다.
   
   f.    **확인**을 클릭합니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. 클릭 **복제** toostart 한 복제 작업입니다. Hello 작업이 완료 되 면 hello 복제 작업 시작 하 고 메시지가 표시 됩니다. 이동 toohello toomonitor hello 진행률 **작업** 블레이드에 대 한 클릭 hello 작업 tooview 작업 세부 정보입니다.
5. Hello 복제본을 성공적으로 만든 후 뒤로 toohello 이동 **공유** 블레이드 장치에 있습니다.
6. 장치에서 공유 hello 목록에서 새 복제 된 공유 hello를 볼 수 있습니다. 계층화된 공유는 계층화된 공유로 복제되고 로컬로 고정된 공유는 로컬로 고정된 공유로 복제됩니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>백업 세트에서 볼륨 복제

hello Azure 포털에서에서 백업에서 tooclone 한 tooperform 단계 비슷한 toohello 것을 공유 복제 됩니다. hello에 hello 백업 tooa 새 볼륨을 복제 하는 hello 복제 작업이 동일한 가상 장치 tooa 다른 장치를 복제할 수 없습니다.

#### <a name="tooclone-a-volume"></a>tooclone 볼륨

1. 너무 찾아보기**장치** 블레이드입니다. 장치를 선택하고 클릭한 다음 **볼륨**을 클릭합니다. 문자열 hello 볼륨 tooclone, 원하는 단추로 hello 볼륨 tooinvoke hello 상황에 맞는 메뉴를 클릭 합니다. **복제**를 선택합니다.
   
   ![볼륨 복제](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. Hello에 **복제** 블레이드에서 클릭 **백업** 수행가 다음를 hello 다음 및: 
   
   a.    Hello 시간 범위에 따라이 장치에서 백업을 필터링 합니다. **지난 7일**, **지난 30일** 및 **지난 해** 중에 선택할 수 있습니다. 
   
   b.    표시 되는 필터링 된 백업 hello 목록에서 백업 tooclone를 선택 합니다.
   
   c.    **확인**을 클릭합니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. Hello에 **복제** 블레이드에서 클릭 **대상 볼륨 설정** 수행가 다음를 hello 다음 고::
   
   a. hello 장치 이름이 자동으로 채워집니다.
   
   b. Hello에 대 한 볼륨 이름을 제공 **볼륨을 복제**합니다. hello 볼륨 이름에는 3 too127 문자가 있어야 합니다.
   
   c. hello 볼륨 종류가 toohello 원래 볼륨을 자동으로 설정 됩니다. 계층화된 볼륨은 계층화된 볼륨으로 복제되고 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복제됩니다.
   
   d. Hello에 대 한 **호스트 연결**, 클릭 **선택**합니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. Hello에 **호스트 연결** 블레이드에서 기존 ACR에서 선택 하거나 새 ACR을 추가 합니다. 새 ACR을 tooadd tooprovide ACR 이름 및 IQN hello 호스트 해야 합니다. **선택**을 클릭합니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. 클릭 **복제** toolaunch 한 복제 작업입니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Hello 복제 작업을 만든 후 복제 시작 됩니다. Hello 복제본을 만든 후 장치에 볼륨 블레이드 hello에 표시 됩니다. 계층화된 볼륨은 계층화된 볼륨으로 복제되고 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복제됩니다.
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Hello 볼륨 온라인 볼륨의 hello 목록에 표시 될 때, hello 볼륨은 사용 하기 위해 사용할 수 있습니다. Hello iSCSI 초기자 호스트에서 iSCSI 초기자 속성 창에서 대상 hello 목록을 새로 고칩니다. Hello 복제 볼륨 이름을 포함 하는 새 대상 hello 상태 열에서 '비활성'으로 표시 됩니다.
8. Hello 대상을 선택 하 고 클릭 **연결**합니다. Hello 초기자가 연결 된 toohello 대상, hello 상태 너무 변경 해야**연결 됨**합니다.
9. Hello에 **디스크 관리** 창 hello 탑재 된 볼륨이 표시 hello 다음 그림에에서 나와 있는 것 처럼 합니다. 발견 된 hello 볼륨을 마우스 오른쪽 단추로 클릭 (hello 디스크 이름 클릭)를 클릭 하 고 **온라인**합니다.

> [!IMPORTANT]
> Hello 복제 작업이 실패 하면 볼륨 또는 백업 세트에서 공유 tooclone 시도, 대상 볼륨 또는 공유의 여전히 있습니다 때 hello 포털에서 만들 수 있습니다. 이 대상 볼륨을 삭제 하거나이 요소에서 발생 하는 모든 향후 문제 hello 포털 toominimize에서 공유 하는 것입니다.
> 
> 

## <a name="item-level-recovery-ilr"></a>항목 수준 복구(ILR)

이 릴리스에 hello 항목 수준 복구를 (ILR) 파일 서버로 구성 하는 StorSimple 가상 배열에 도입 되었습니다. hello 기능 hello StorSimple 장치에서 모든 hello 공유의 클라우드 백업에서 파일 및 폴더의 toodo 세분화 된 복구를 허용 합니다. 셀프 서비스 모델을 사용하여 최근 백업에서 삭제된 파일을 복구할 수 있습니다.

모든 공유에는 *.backups* hello 가장 최근 백업이 포함 된 폴더입니다. 원하는 백업 toohello를 탐색 하 고, hello 백업에서 관련 파일 및 폴더를 복사 하 고, 복원할 수 있는 합니다. 이 기능은 백업에서 복원할 수 있도록 tooadministrators 호출을 제거 합니다.

1. Hello ILR를 수행 하는 경우 파일 탐색기를 통해 hello 백업을 볼 수 있습니다. 에 대 한 hello 백업에서 toolook 원하는 hello 특정 공유를 클릭 합니다. 표시 됩니다는 *.backups* 모든 hello 백업을 저장 하는 hello 공유에 만들어지는 폴더입니다. Hello 확장 *.backups* 폴더 tooview hello 백업 합니다. hello 폴더의 전체 백업 계층 hello hello 분해 된 보기를 보여 줍니다. 이 보기에는 몇 초 toocreate는 대개와 요청 시 만들어집니다.
   
   hello 마지막 다섯 개 백업 이러한 방식으로 표시 되 고 사용 하는 tooperform 항목 수준 복구 될 수 있습니다. hello 최근 5 개의 백업을 동시에 포함 될 기본 예약 hello 및 수동 백업을 hello 합니다.
   
   * **예약된 백업**의 이름은 &lt;장치 이름&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC로 지정됩니다.
   * **수동 백업** 의 이름은 Ad-hoc-YYYYMMDD-HHMMSS-UTC로 지정됩니다.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Hello hello 삭제할 파일의 최신 버전을 포함 하는 hello 백업을 식별 합니다. Hello 폴더 이름 각 hello의 경우 앞에 UTC 타임 스탬프가 들어 있지만 hello는 hello 폴더를 만든 시간은 hello 실제 장치 hello 백업 시작 시간입니다. 폴더 타임 스탬프 toolocate hello를 사용 하 고 hello 백업을 식별 합니다.

3. Hello 폴더나 hello 이전 단계에서 식별 된 hello 백업에 toorestore 원하는 hello 파일을 찾습니다. Note hello 파일 또는 폴더에 권한을 가진 사용자를 볼 수 있습니다. 특정 파일이나 폴더에 액세스할 수 없는 경우 공유 관리자에게 문의하세요. 관리자에 게는 파일 탐색기 tooedit hello 공유 사용 권한을 사용 하 고 액세스 toohello 특정 파일 또는 폴더 제공 수 있습니다. 권장된 모범 사례입니다 hello 공유 관리자는 단일 사용자가 아니라 사용자 그룹 이며

4. Hello 파일 또는 hello 폴더 toohello StorSimple 파일 서버에 적절 한 공유에 복사 합니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대 한 자세한[hello 로컬 웹 UI를 사용 하 여 StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.

