---
title: "StorSimple에 대 한 액세스 제어 레코드 aaaManage | Microsoft Docs"
description: "Toouse 액세스 제어 (Acr) toodetermine tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 기록 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Hello StorSimple 관리자 서비스 toomanage 액세스 제어 레코드를 사용 하 여

## <a name="overview"></a>개요
액세스 제어 레코드 (Acr) toospecify tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 허용 합니다. Acr tooa 특정 볼륨을 설정 하 고 hello iSCSI 포함 hello 호스트의 정규화 된 이름 (iqn이 포함). 호스트 tooconnect tooa 볼륨 오류 값을 hello 장치 hello ACR 해당 볼륨에 연결 된 일치 하는 경우 hello 연결이 설정 되 고 hello IQN 이름을 확인 합니다. hello에 대 한 액세스 제어 레코드 hello **구성** StorSimple 장치 관리자 서비스 블레이드의 섹션 hello 해당 hello 호스트의 iqn이 포함 된 모든 hello 액세스 제어 레코드를 표시 합니다.

이 자습서에서는 일반적인 ACR 관련 작업을 수행 하는 hello를 설명 합니다.

* 액세스 제어 레코드 추가
* 액세스 제어 레코드 편집
* 액세스 제어 레코드 삭제

> [!IMPORTANT]
> * ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.
> * 볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.

## <a name="get-hello-iqn"></a>Hello IQN 가져오기

Hello 단계 tooget hello Windows Server 2012를 실행 중인 Windows 호스트의 IQN을 다음을 수행 합니다.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>액세스 제어 레코드 추가
Hello를 사용 하 여 **구성** hello StorSimple 장치 관리자 서비스 블레이드 tooadd Acr의에서 섹션입니다. 일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.

Hello 단계 tooadd ACR 다음을 수행 합니다.

#### <a name="tooadd-an-acr"></a>ACR tooadd

1. Tooyour StorSimple 장치 관리자 서비스를 이동, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.
2. Hello에 **액세스 제어 레코드** 블레이드에서 클릭 **ACR 추가 +**합니다.

    ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr1.png)

3. Hello에 **ACR 추가** 블레이드에서 다음 단계 hello지 않습니다.

    1. ACR의 이름을 지정합니다.
    
    2. Windows Server 호스트의 IQN 이름을 hello 제공 **iSCSI 초기자 이름 (IQN)**합니다.

    3. 클릭 **추가** toocreate hello ACR 합니다.

        ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  hello는 ACR hello Acr의 테이블 형식 목록에 표시 됩니다 새로 추가 합니다.

    ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>액세스 제어 레코드 편집
Hello를 사용 하 여 **구성** hello StorSimple 장치 관리자 서비스 블레이드 tooedit Acr의에서 섹션입니다.

> [!NOTE]
> 현재 사용하지 않고 있는 ACR만 수정하는 것이 좋습니다. 현재 사용 중인 볼륨와 연결 된 ACR tooedit를 먼저 수행 해야 hello 볼륨 오프 라인으로.

Hello 단계 tooedit ACR 다음을 수행 합니다.

#### <a name="tooedit-an-access-control-record"></a>tooedit 액세스 제어 레코드
1.  Tooyour StorSimple 장치 관리자 서비스를 이동, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Hello 액세스 제어 레코드의 테이블 형식 목록 hello 클릭 하 고 hello toomodify 하려는 ACR을 선택 합니다.

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr1.png)

3. Hello에 **액세스 제어 레코드 편집** 블레이드에서 다른 IQN 해당 tooanother 호스트를 제공 합니다.

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr2.png)

4. **Save**를 클릭합니다. 확인하라는 메시지가 표시되면 **예**를 클릭합니다. 

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr3.png)

5. ACR hello 업데이트 될 때 알림을 받습니다. 또한 테이블 형식 목록 hello tooreflect hello 변경을 업데이트합니다.

   
## <a name="delete-an-access-control-record"></a>액세스 제어 레코드 삭제
Hello를 사용 하 여 **구성** hello StorSimple 장치 관리자 서비스 블레이드 toodelete Acr의에서 섹션입니다.

> [!NOTE]
> 현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다. 현재 사용 중인 볼륨와 연결 된 ACR toodelete를 먼저 수행 해야 hello 볼륨 오프 라인으로.

Hello 단계 toodelete 액세스 제어 레코드를 다음을 수행 합니다.

#### <a name="toodelete-an-access-control-record"></a>toodelete 액세스 제어 레코드
1.  Tooyour StorSimple 장치 관리자 서비스를 이동, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Hello 액세스 제어 레코드의 테이블 형식 목록 hello 클릭 하 고 hello toodelete 하려는 ACR을 선택 합니다.

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 선택 **삭제**합니다.

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. 확인 메시지가 표시 되 면 hello 정보를 검토 한 다음 클릭 **삭제**합니다.

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Hello 삭제 완료 될 때 알림을 받습니다. hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 삭제입니다.

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>다음 단계
* [StorSimple 볼륨 관리](storsimple-8000-manage-volumes-u2.md)에 대해 자세히 알아봅니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

